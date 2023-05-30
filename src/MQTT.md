# MQTT

**MQTT**, _Message Queuing Telemetry Transport_, è un protocollo di comunicazione _connection oriented_, appoggiato su TCP/IP che si basa sul pattern _publish-subscribe_ (o _observer-observable_).

## Come funziona

Un messaggio MQTT è composto da:

- un **topic** che servirà al _broker_ per la distribuzione, è una stringa il cui contenuto è libero, ma viene specificata la forma sintattica
  da utilizzare per costruirlo (parole separate dal carattere "/").

  Esempi di topic:

  - `Appartamento/Sala/Temperatura`
  - `Appartamento/Cucina/Temperatura`
  - `Appartamento/Balcone/Umidità`

- un **payload**, il corpo del messaggio, è semplicemente una stringa UTF-8, la semantica di tale stringa
  è affidata alle convenzioni stabilite tra chi manda e chi riceve, _non è definita dal protocollo_.
  Può essere un semplice valore, dei valori separati da virgola, una stringa JSON, ecc...

I messaggi vengono inviati da un _nodo client_ della rete MQTT verso un _broker di distribuzione_, il quale li reindirizza a tutti i nodi che
si sono dichiarati interessati a quel tipo di _topic_.

Il _broker_ quindi mantiene e gestisce una lista di nodi client che si sono registrati per uno specifico _topic_,
consentendo anche l'uso di _wildcards_ invece di un _topic_ per esteso.

Due possibili _wildcards_ sono:

- "+": corrisponde a qualsiasi parola _senza_ "/";
- "#": corrisponde a qualsiasi parola che _non inizi_ per "/" ma che lo può contenere.

Esempi di tipic con _wildcards_:

- `Appartamento/+/Temperatura`

  corrisponde a qualunque topic della forma `Appartamento/<parola>/Temperatura`

- `Appartamento/#`

  corrisponde a qualunque topic della forma `Appartamento/<parola>/<altra_parola>/<altra_parola2>/<ecc>/...`

#### Possibile feed di un _broker_

```
...
Appartamento/Sala/Temperatura 21
Appartamento/Cucina/Temperatura 25
Appartamento/Sala/Temperatura 22
Appartamento/Balcone/Umidità 60
Appartamento/Tetto/StazioneUmidità { id: "sx", temp: 25, umid: 60 }
...
```
