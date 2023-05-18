# Memoria di sistema

Il termine _memoria di sistema_ (o _memoria primaria_) indica una memoria volatile ad accesso veloce usata dalla CPU per il caricamento di dati ed istruzioni da poter processare.
In genere vengono utilizzate le RAM (_Random Access Memory_).

In base alla tecnologia è possibile distinguere tre tipologie principali di RAM:

#### SRAM

La **SRAM**, acronimo di **Static RAM**, è una memoria ad accesso casuale statica (_non_ necessita di _refresh_[^1]), volatile,
generalmente molto veloce ma anche molto costosa.

Dato il costo elevato, tipicamente viene utilizzata per le memorie cache.

Dal punto di vista energetico e termico ha delle ottime prestazioni.

#### DRAM

**DRAM**, acronimo di **Dynamic RAM**, è una tecnologia per memorie volatili assai più economica e semplice delle SRAM,
ma che richiede il _refresh_[^1] del dato immagazzinato.

È una variante asincrona delle SRAM, ovvero non necessita la sincronizzazione con il _clock_ del sistema.

#### SDRAM

È la variante sincrona delle DRAM (sta per **Syncronous Dynamic RAM**), la cui velocità è quindi collegata al _clock_ dell'elaboratore.

[^1]: Con il termine _refresh_, riferito alle memorie ed in particolare alle DRAM, si intende l'operazione di "rivitalizzazione" (lettura e riscrittura immediata) dei contenuti in memoria per non perdere l'informazione mantenuta nei condensatori che compongono le celle della memoria.
