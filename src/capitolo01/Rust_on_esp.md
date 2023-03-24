# Rust on ESP (esp-rs)

Per utilizzare Rust sui microcontrollori ESP seguiremo il book ufficiale di _esp-rs_ 👉[The Rust on ESP book](https://esp-rs.github.io/book/).

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
