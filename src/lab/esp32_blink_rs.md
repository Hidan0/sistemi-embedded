# Blink demo su ESP32

Generare un progetto per ESP32 è estremamente semplice in quanto esp-rs mantiene attivamante due repository template basate sul tool `cargo-generate`:

- [esp-template](https://github.com/esp-rs/esp-template) - `no_std` template
- [esp-idf-template](https://github.com/esp-rs/esp-idf-template) - `std` template

Per installare `cargo-generate`:

```
$ cargo install cargo-generate
```

Per generare un progetto esp-template:

```
$ cargo generate --git https://github.com/esp-rs/esp-template
```

Per generare un progetto esp-idf-template:

```
$ cargo generate --git https://github.com/esp-rs/esp-idf-template cargo
```

Per entrambi i casi spunterà un prompt interattivo con delle domande riguardo al target dell'applicazione.

## Versione bare-metal

```rust
#![no_std]
#![no_main]

use esp_backtrace as _;
use esp_println::println;
use hal::{
    clock::ClockControl, peripherals::Peripherals, prelude::*, timer::TimerGroup, Delay, Rtc, IO,
};

#[entry]
fn main() -> ! {
    let peripherals = Peripherals::take();
    let system = peripherals.DPORT.split();
    let clocks = ClockControl::boot_defaults(system.clock_control).freeze();

    // Disable the RTC and TIMG watchdog timers
    let mut rtc = Rtc::new(peripherals.RTC_CNTL);
    let timer_group0 = TimerGroup::new(peripherals.TIMG0, &clocks);
    let mut wdt0 = timer_group0.wdt;
    let timer_group1 = TimerGroup::new(peripherals.TIMG1, &clocks);
    let mut wdt1 = timer_group1.wdt;

    rtc.rwdt.disable();
    wdt0.disable();
    wdt1.disable();
    // ------

    let io = IO::new(peripherals.GPIO, peripherals.IO_MUX);
    let mut led = io.pins.gpio13.into_push_pull_output();

    led.set_high().unwrap();

    let mut delay = Delay::new(&clocks);

    loop {
        led.toggle().unwrap();
        delay.delay_ms(500u32);
    }
}
```

Lo sketch è simile alla versione ESP8266 tranne per qualche piccola differenza nel _Hardware Abstraction Layer_.

Il nuovo blocco di codice istanzia alcune periferiche (in particolare l'RTC e i due TimerGroup) per disabilitare il _watchdog_ che viene attivato dopo l'avvio.

## Versione std

```rust
use esp_idf_hal::delay::FreeRtos;
use esp_idf_hal::gpio::*;
use esp_idf_hal::peripherals::Peripherals;

fn main() {
    esp_idf_sys::link_patches();

    let peripherals = Peripherals::take().unwrap();
    let mut led = PinDriver::output(peripherals.pins.gpio13).unwrap();

    loop {
        led.set_high().unwrap();
        // we are sleeping here to make sure the watchdog isn't triggered
        FreeRtos::delay_ms(1000);

        led.set_low().unwrap();
        FreeRtos::delay_ms(1000);
    }
}
```

Dato che la versione `std` utilizza il framework [ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/about.html) di Espressif, l'API è leggermente diversa.

- La chiamata alla funzione `esp_idf_sys::link_patches` assicura che alcune patch di ESP-IDF implementate in Rust siano collegate all'eseguibile finale;
- `PinDriver` viene utilizzato per impostare le modalità dei PIN;
