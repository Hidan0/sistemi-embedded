# Arduino IDE

Come è stato già detto Arduino IDE è un ambiente di sviluppo (bundle) che unisce le funzionalità di un editor, compilatore, linker, ecc... è scaricabile ed installabile dal sito di [arduino](https://www.arduino.cc/en/software). Attualmente esistono due versioni principali `v1.*` e `v2.*`, ma il l'utilizzo di base non cambia.

## Installazione

Su Arch:

```bash
pacman -S arduino      # versione 1.*

yay -S arduino-ide-bin # versione 2.* (AUR)
```

## Add-ons

Dato che Arduino IDE si pone come ambiente di sviluppo multipiattaforma, non può sapere a prescindere come è fatta ogni singola board.
Quindi le informazioni delle board vanno importate esternamente e successivamente selezionare la board sulla quale si vuole compilare.

Per importare le informazioni su Arduino, ESP8266 e ESP32 aggiungere i seguenti link nel "board manager" dell'IDE (File -> Preferences -> Additional Boards Manager)

```
http://digistump.com/package_digistump_index.json
http://arduino.esp8266.com/stable/package_esp8266com_index.json
http://raw.githubusercontent.com/esp8266/Arduino/master/boards.txt
http://adafruit.github.io/arduino-board-index/package_adafruit_index.json
https://raw.githubusercontent.com/sparkfun/Arduino_Boards/master/IDE_Board_Manager/package_sparkfun_index.json
https://dl.espressif.com/dl/package_esp32_index.json
```

## Blink

Per questa demo sto utilizzando una ESP8266 WeMos D1 Mini.

Per prima cosa bisogna selezionare la board (Tools -> Board) e scelgo `Generic ESP8266 Module`. Una volta selezionata la board possiamo scrivere il programma che farà lampeggiare il led integrato sul PCB.

```C
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(1000);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(1000);                      // wait for a second
}
```

Infine possiamo compilare e caricare il nostro sketch: Sketch -> Upload
