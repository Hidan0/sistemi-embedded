# Ambiente di sviluppo

Nei seguenti capitoli vedremo come impostare il proprio ambiente di sviluppo in due modi diversi, il primo (supportato dal corso) con [Arduino IDE](https://www.arduino.cc/en/software), il secondo con Rust🦀 ([esp-rs](https://github.com/esp-rs)).

## Permessi (in Linux)

In entrambi i casi l'utente per comunicare con la board deve accedere in lettura e scrittura al file del dispositivo creati da `udev` come `/dev/ttyUSB0`.

Eseguendo il comando

```bash
ls -ls /dev/ttyUSB0
```

oppure

```bash
stat /dev/ttyUSB0
```

è possibile visuallizzare l'id del gruppo (su Arch è `uucp`, un altro potrebbe essere `dialout`; in ogni caso è utile visuallizzare la wiki della propria distro).
A questo punto possiamo aggiungere il nostro utente al gruppo:

```bash
usermod -a -G <group> <username>
```
