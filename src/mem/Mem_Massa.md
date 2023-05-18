# Memoria di massa

La memoria di massa (intesa come spazio di conservazione) di dati persistenti, possono essere suddivise in base al tipo di supporto fisico utilizzato.

#### ROM

Le **Read Only Memory** sono memorie in sola lettura dove l'informazione è contenuta nei transistor.
Con il progredire delle tecnologie però, le ROM si sono evolute in diverse forme aggirando, almeno in parte, il limite della possibilità di riscrittura.

- **PROM** (**Programmable ROM**): memorie programmabili solo _una_ volta tramite ĺ'uso di corrente elettrica ad alto potenziale;
- **EPROM** (**Eresable Programmable ROM**): a differenza delle EPROM e delle ROM sono riscrivibili, ma solo un numero limitato di volte.
  La programmazione avviene previo "azzeramento" tramite luce ultravioletta.
- **EEPROM** (**Electrically Eresable Programmable ROM**): queste memorie sono cancellabili e riscrivibili elettricamente un numero limitato di volte.

#### Flash Memory

Le **Flash Memory**, di diretta derivazione delle _EEPROM_, si distinguono da queste ultime per la loro capacità di essere cancellate e riscritte a _blocchi_ o _unità_ più piccole e non interamente.

In base al tipo di collegamento delle celle, varia la modalità operativa della memoria, si distinguono due tipi:

- **NAND Memory**: I transistor sono collegati in modo da creare un collegamento in serie tra le celle;
- **NOR Memory**: Tutte le celle sono collegate a massa ad in parallelo alla _bit line_, comportandosi come un NOR Gate. In questo modo, ogni cella è leggibile e scrivibile singolarmente.

| NAND Memory                                               | NOR Memory                                                     |
| --------------------------------------------------------- | -------------------------------------------------------------- |
| Più economiche                                            | Più costose                                                    |
| Occupano meno spazio                                      | Occupano più spazio                                            |
| Ottimizzate sia per lettura che per scrittura             | Ottimizzata per la lettura, minori prestazioni sulla scrittura |
| Utilizzate come storage principale di un sistema embedded | Utilizzate per funzioni a basso livello e di boot              |

#### Supporto Magnetico

Floppy Disk, Hard Disk, Nastri megnetici.

In ambiente embedded difficilmente si avrà a che fare con tali dispositivi.

#### Supporto Ottico

CD, DVD, Blue-Ray.

In ambiente embedded difficilmente si avrà a che fare con tali dispositivi.
