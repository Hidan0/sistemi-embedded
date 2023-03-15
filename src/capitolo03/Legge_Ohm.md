# Legge di Ohm

È una formula matematica che lega la tensione (\\(V\\)) e l'intensità di corrente (\\(I\\)) alla _resistenza_ (\\(R\\)) di un conduttore, ed è così espressa:

$$I=\frac{V}{R}$$

e le relative formule a seconda dell'incognita:

$$R=\frac{V}{I},\ V = R \ast I$$

La legge dice che l'intensità di corrente in un conduttore è direttamente proporzionale alla tensione e inversamente proporzionale alla _resistenza del conduttore_.
L'unità di misura della resistenza è l'_Ohm_ (simbolo \\(\Omega\\)).

### Resistenza

La resistenza "naturale" (chiamata _resistività_, simbolo \\(\rho\\)) di un conduttore è dovuta al tipo di materiale usato.
Un conduttore può essere quindi più o meno buono, non esiste di tipo "booleano" in cui fa o non fa passare corrente.

La resistenza di un conduttore è in funzione del materiale di cui è fatto, della sua lunghezza e della sua sezione: aumenta con la lunghezza del conduttore, diminuisce con il diminuire della sezione del conduttore.

Anche i componenti elettronici hanno una loro resistenza interna.

## Potenza

La corrente limitata attraverso l'uso di resistenze, produce calore. Posso quindi esprimere la _potenza_ (\\(P\\), unità di misura _Watt_, simbolo \\(\mathsf{W}\\)) come _calore dissipato_:

$$ P = R \ast I^2 $$

Dato un conduttore con una resistenza nota, se gli facessi passare una qualunque corrente all'interno, saprei che la potenza che dissipa è proporzionale alla resistenza per il quadrato dell'intensità:

- se aumento la resistenza, aumenta la potenza dissipata;
- se aumento l'intensità, aumenta (di molto) la potenza dissipata.

È utile per il dimensionamento del circuito: per ottimizzare la potenza dissipata potrei lavorare sulle resistenze (cambiare materiale, accorciare i cavi, fare cavi più grossi -- ove possibile --), ma otterrei miglioramenti di poco conto; potrei invece lavorare sull'intensità.

Riscrivo la formula della potenza usando la legge di Ohm:

$$P = R \ast I^2 = R \ast \left(\frac{V}{R}\right)^2=\frac{V^2}{R}=V \ast I$$

Usata per esprimere la potenza trasportata.
