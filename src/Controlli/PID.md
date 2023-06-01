# Controllo PID

Il **controllo PID** (_Proporzionale-Integrativo-Derivativo_) modella la funzione di trasferimento come una somma pesata
di tre componenti dipendenti dalla funzione di errore \\(e(t)\\):

$$
e(t) = \text{StatoDesiderato} - \text{StatoAttuale}
$$

Le tre componenti del controllo PID rappresentano le seguenti caratteristiche:

- **la distanza assoluta** dallo stato desiderato;
- **la storia** dell'evoluzione dello stato del sistema;
- **la velocità** di variazione dello stato.

La forma generale della funzione è la seguente:

\\[ u(t) = \overbrace{K_p \ast e(t)}^{Proporzionale} + \overbrace{K_i \ast \int_0^t e(t^{\prime})dt^{\prime}}^{Integrativo} + \overbrace{K_d \ast \frac{de(t)}{dt}}^{Derivativo} \\]

Dove \\(K_p,\ K_i,\ K_d\\) sono i coefficienti "peso" che stabiliscono l'apporto delle tre componenti (_Proporzionale_, _Integrativo_, _Derivativo_).

- La componente **proporzionale** utilizza l'errore attuale per valutare quanto il sistema sia lontano dall'obbiettivo;
- la componente **integrativa** calcola il cumulo degli errori da quando il sistema è stato attivato;
- la componente **derivativa** valuta la velocità di allontanamento/avvicinamento all'obbiettivo.
