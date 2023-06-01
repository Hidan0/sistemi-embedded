# Controlli automatici

Il ruolo più frequente di un sistema embedded è quello del controllo di un sistema fisico.

Lo _stato_ del sistema viene specificato in maniera formale in fase di progettazione. In produzione
lo stato effettivo del sistema viene osservato per verificare il corretto funzionamento rispetto
alle specifiche.

## Stato di un sistema

Un sistema può essere descritto tramite variabili di ingresso (come una tensione di alimentazione, segnale da un sensore) e di uscita (come il numero di giri di un motore).

Le variabili in **ingresso** si dividono in:

- **di controllo**: parametri direttamente modificabili che influenzano lo stato del sistema;
- **di ambiente/disturbo**: paramentri non modificabili, o difficilmente modificabili, ma che possono influenzare il comportamento globale del sistema.

Le variabili di **uscita** (o di stato) si dividono in:

- **di prestazione**: l'_output_ effettivo che si intende ottenere dal sistema;
- **intermedie**: variabili più facilmente misurabili rispetto a quelle "di prestazione"
  ma ad esse collegate.

Per esempio, consideriamo il sistema di controllo di un drone e le possibili variabili:

- _di controllo_: la tensione di alimentazione che regola i giri motore dei rotori;
- _di ambiente/disturbo_: l'angolo del drone, le oscillazioni, la velocità;
- _di prestazione_: il drone vola e risponde ai comandi, mantiene un angolo, altitudine corretta;
- _intermedie_: velocità verticale.

## Modello matematico

Il modello tipicamente utilizzato per rappresentare il funzionamento del sistema definisce una "_funzione di trasferimento_" \\(f\\):

$$
\frac{dU(t)}{dt} = f(U(t),\ C(t),\ A(t))
$$

dove:

- \\(U\\) è il vettore delle variabili di uscita;
- \\(C\\) è il vettore delle variabili di controllo;
- \\(A\\) è il vettore delle variabili ambientali.

Nel discreto la funzione \\(f\\) diventa:

$$
U(t+1) = f(U(t),\ C(t),\ A(t))
$$

cioè il valore della variabile di uscita all'istante \\(t+1\\) dipende dai valori all'instante \\(t\\).

Rappresenta quindi una variazione di stato nel **tempo** dipendente dai valori delle variabili di ingresso, dai disturbi e dai valori delle variabili di uscita precedenti.

Questo modello viene detto a **loop chiuso** o con _retroazione/feedback_.

Se le variabili di uscita non vengono prese in considerazione si parla di modello a **loop aperto** o _senza retroazione/feeback_.

$$
\frac{dU(t)}{dt} = f(C(t),\ A(t))
$$

La differenza tra i due modelli risiede nel fatto che nel modello _open loop_ il comportamento previsto del sistema è _hardcoded_,
senza alcuna valutazione del risultato effettivo dell'azione.
Nel modello senza retroazione il costo di progettazione risiede nel perfezionamento della formula che deve
essere quanto più rappresentativa della situazione reale.

Nel modello _closed loop_, invece, è possibile incorporare azioni correttive in base all'output effettivamente ottenuto.
È importante quindi, studiare attentamente il meccanismo di feedback per determinare la reattività adeguata alla funzione di trasferimento.
