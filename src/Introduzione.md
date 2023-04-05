# Introduzione ai Sistemi Embedded

## I sistemi embedded

Non vi è una definizione vera e propria di _sistema embedded_ in quanto risulterebbe generica e includerebbe diversi dispositivi.
Vi è invece una netta distinzione dal punto di vista _funzionale_, dato che un _sistema embedded_ esegue tipicamente poche funzioni e in maniera impeccabile (possibilmente).

> Un **Sistema Embedded** è un sistema di elaborazione "incorporato, incapsulato" (tipicamente non visibile) all'interno di un altro apparato.

Si possono distinguere tre macro-gruppi di sistemi embedded:

- _PLC_
- _Microcontrollori_
- _SoC_

## PLC

I **PLC** (_Programmable Logic Controller_) sono dei dispositivi relativamente semplici, generalmente pensati per lavorare su sistemi di automazione industriali e non destinati alla produzione su vasta scala.
Dato il loro utilizzo industriale, sono molto robusti sia a livello elettronico che fisico.

✨ _Fuffa proprietaria_ ✨

## MCU e SoC

### Microcontrollori

Un **Micro-controller unit** (**MCU**) è un piccolo computer su un circuito integrato (_IC_) che contiene una unità di elaborazione, RAM, memoria programmabile, GPIO, ecc. Tipicamente _monoprogrammato_.

Un esempio di MCU sono _Arduino_, _ESP8266_.

### System on Chip

**System on Chip** (**SoC** o **SOC**) è un termine recente, vago e poco definito.
Un _SoC_ ha una dotazione più ricca rispetto ad un MCU: contiene CPU, RAM, processori di supporto, codec, GPU, ecc.

Un esempio di SoC è _Raspberry_.

### Differenze tra MCU e SoC

La linea che separa _MCU_ e _SoC_ è davvero sottile ed è difficile trovare una distinzione netta.

Le differenze principali sono le seguenti:

| MCU                                                                                                  | SoC                                                                                             |
| ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Contiene un singolo chip con periferiche non specifiche                                              | Contiene un singolo chip con periferiche più specifiche                                         |
| Incapsulamento di un numero ridotto e limitato di periferiche                                        | Incapsulamento di molte periferiche                                                             |
| Destinato a piccole applicazioni e dalla bassa complessità                                           | Destinato ad applicazioni con maggiori requisiti e maggiore complessità                         |
| Poco costoso                                                                                         | Più costoso, stampato su richiesta                                                              |
| Tipicamente senza SO                                                                                 | SO incluso                                                                                      |
| Basso consumo energetico, alimentabile a batteria                                                    | Consumo di energia elevato e variabile a seconda delle applicazioni                             |
| Fornisce valore riducendo al minimo i costi                                                          | Fornisce valore massimizzando la funzionalità                                                   |
| La memoria è minima, spesso misurata in KB                                                           | È inclusa una maggiore quantità di memoria, che può essere di MB o GB                           |
| La memoria esterna può variare da KB a MB tramite Flash o EEPROM                                     | La memoria esterna può variare da MB a TB tramite Flash, SSD o HDD                              |
| Le applicazioni includono termostati programmabili, elettrodomestici e strumenti industriali, ecc... | Le applicazioni comprendono smartphone, router di rete ed emulatori di console di gioco, ecc... |

## Componenti fondamentali di un sistema embedded

### GPIO

La differenza più nota con i computer moderni è che un sistema embedded si interfaccia con il mondo esterno attraverso segnali elettrici.
I **GPIO**, _General Purpose Input Output_, servono proprio a questo.

La _board_ è capace di interfacciarsi e interpretare il mondo fisico attraverso l'uso di traduttori:

- **attuatore**: da _board_ a _mondo esterno_
- **sensore**: da _mondo esterno_ a _board_

In una board non tutti i pin offrono le funzionalità di _GPIO_, possono essere ad esempio solo di alimentazione.

### Oscillatore

Un altro compenente importante è l'**oscillatore**, un circuito elettronico che genera forme d'onda di frequenza, utilizzato come sorgente di _clock_.

È un componente necessario in quanto detta il tempo di elebarazione del sistema: i vari componenti hanno velocità differenti, dunque è necessario un sistema per sincronizzarli.

Tipicamente è posto fuori dalla CPU perchè più è bassa la velocità di clock (come nei MCU) e più è grande il cristallo di quarzo all'interno dell'oscillatore.
