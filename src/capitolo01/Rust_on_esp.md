# Rust on ESP (esp-rs)

Per utilizzare Rust sui microcontrollori ESP seguiremo il book ufficiale di _esp-rs_ 👉[The Rust on ESP book](https://esp-rs.github.io/book/).

Altre risorse utili:

- [Getting Started with ESP8266](https://lastminuteengineers.com/getting-started-with-esp8266/)
- [Docs ESP8266](https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/index.html#introduction)

## Setup

Ad oggi, nella mainline di Rust non esiste il supporto per l'architettura `Extensa` (l'architettura di ESP8266 e ESP32).
Per questo motivo useremo il fork `esp-rs/rust` che aggiunge il supporto a tale architettura.

Ci sono diverse opzioni disponibili per l'installazione del fork di Rust, il metodo consigliato è attraverso il tool [esp-rs/espup](https://github.com/esp-rs/espup).

### Installazione toolchain

#### espup

`espup` è uno strumento per l'installazione e la manutenzione dell'ecosistema necessario a sviluppare applicazioni in Rust per i chip Espressif (sia `Xtensa` che `RISC-V`).

Si occupa di intallare il compilatore corretto (il fork `esp-rs/rust`), la toolchain `nightly` con i target necessari, la toolchain `LLVM`, la toolchain `GCC` e molte altre cose.

Per installare `espup`

```bash
cargo install espup
```

una volta che `espup` è stato installato, si può eseguire

```bash
espup install
```

con l'installazione verrà creato un file (`export-esp.sh`) che esporta le variabili d'ambiente necessarie. Questo file dovrà essere "caricato" ogni volta che si vorrà usare la toolchain.

#### espflash

`espflash` è un tool da riga di comando per il flash dei dispositivi ESP (supporta ESP32, ESP32-C2, ESP32-C3, ESP32-S2, ESP32-S3 e ESP8266).

Per installare `espflash`

```bash
cargo install cargo-espflash espflash
```

## Blink su ESP8266

La prima cosa da fare è caricare le variabili d'ambiente necessarie:

```bash
. $HOME/export-esp.sh
```

Successivamente creare il progetto, usando `cargo` possiamo eseguire

```bash
cargo new esp8266-blink
```

In `Cargo.toml` inserisco le dipendenze necessarie:

```toml
[package]
name = "esp8266-blink"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
esp8266-hal = "0.5.1"
panic-halt = "0.2.0"
```

Vanno creati due file aggiuntivi `rust-toolchain.toml` e `.cargo/config.toml`.

`rust-toolchain.toml`:

```toml
[toolchain]
channel = "esp"
targets = ["xtensa-esp8266-none-elf"]
```

`.cargo/config.toml`:

```toml
[target.xtensa-esp8266-none-elf]
runner = "espflash flash --monitor /dev/ttyUSB0"

[build]
rustflags = [
  "-C", "link-arg=-nostartfiles",
  "-C", "link-arg=-Wl,-Tlink.x",
]
target = "xtensa-esp8266-none-elf"

[unstable]
build-std = ["core"]
```

A questo punto il progetto si presenterà con la seguente struttura:

```
├── .cargo
│   └── config.toml
├── src
│   └── main.rs
├── .gitignore
├── Cargo.toml
└── rust-toolchain.toml
```

In `src/main.rs` scriviamo finalmente il codice del programma:

```rust
#![no_std]
#![no_main]

use esp8266_hal::prelude::*;
use esp8266_hal::target::Peripherals;
use panic_halt as _;

#[entry]
fn main() -> ! {
    let dp = Peripherals::take().unwrap();
    let pins = dp.GPIO.split();
    let mut led = pins.gpio2.into_push_pull_output();
    let (mut timer1, _) = dp.TIMER.timers();

    led.set_high().unwrap();

    loop {
        timer1.delay_ms(1000);
        led.toggle().unwrap();
    }
}
```

Infine per compilare il programma eseguo

```bash
cargo espflash --release /dev/ttyUSB0
```

Nel mio caso al termine della compilazione -- per qualche motivo -- ottengo il seguente errore:

```bash
error: could not compile `esp8266-blink` due to 2 previous errors
error: linker `xtensa-lx106-elf-gcc` not found
  |
  = note: No such file or directory (os error 2)

error: aborting due to previous error
```

Per risolverlo mi è bastato installare il seguente pacchetto (su Arch)

```bash
yay -S xtensa-lx106-elf-gcc
```

Anche in questo caso c'è un file da caricare ogni volta che si vuole utilizzare il tool

```bash
source /etc/profile.d/xtensa-lx106-elf-gcc.sh
```

Rieseguento il comando per la compilazione questa volta andrà a buon fine!.
