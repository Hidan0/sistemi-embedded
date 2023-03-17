# Blink demo su ESP8266

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

In `rust-toolchain.toml` impostiamo la toolchain corretta:

```toml
[toolchain]
channel = "esp"
```

Mentre in `.cargo/config.toml` configuriamo i comandi di `cargo`:

```toml
[target.xtensa-esp8266-none-elf]
runner = "espflash /dev/ttyUSB0"

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
cargo run --release
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
