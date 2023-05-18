# Panoramica architetture memorie

Nel mondo informatico il termine "memoria" è utilizzato genericamente per indicare lo "spazio"
dove memorizzare permanentemente o temporaneamente dei dati o codice.

È possibile classificare le memorie in base alla persistenza dei dati, al tipo di accesso dei dati, della velocità, del costo, ecc...

### Persistenza

> Una memoria è detta **volatile** quando il dato immagazzinato non rimane memorizzato per lunghi periodi.

> Una memoria è detta **persistente** quando il dato rimane (o "dovrebbe" rimanere) memorizzato fino ad esplicita cancellazione.

### Accesso

- **Memoria ad accesso casuale (RAM)**: _volatile_ e generalmente "veloce", di costo "elevato",
  in grado di garantire il medesimo tempo di accesso per qualsiasi porzione di essa. È generalmente associata
  alla memoria di sistema.
- **Memoria ad accesso diretto**: _persistente_ e generalmente "lenta", ma con un costo relativo
  più basso delle RAM, offre tempi variabili di accesso in base all'indirizzo di memoria a cui si vuole accedere.
  Di solito utilizzata per memorie di massa.
