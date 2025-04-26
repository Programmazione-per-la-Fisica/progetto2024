<!-- omit in toc -->
# Simulazione dell'interazione tra due specie

- [Descrizione del problema](#descrizione-del-problema)
- [Le equazioni di Lotka-Volterra](#le-equazioni-di-lotka-volterra)
  - [Note sulla dinamica del sistema](#note-sulla-dinamica-del-sistema)
  - [Versione discretizzata delle equazioni](#versione-discretizzata-delle-equazioni)
- [Implementazione della simulazione in C++](#implementazione-della-simulazione-in-c)
- [Variazioni sul tema](#variazioni-sul-tema)
- [Riferimenti utili](#riferimenti-utili)

## Descrizione del problema

Il compito consiste nella progettazione e nell'implementazione di una
simulazione che descriva, in uno scenario opportunamente semplificato,
l'interazione tra due specie che coesistono in un _ecosistema_.

La prima delle due specie da considerare è quella delle **prede**, le quali (in
analogia con gli animali erbivori che abitano una zona sufficientemente fertile)
hanno a disposizione una quantità illimitata di cibo. La seconda specie, cioè i
**predatori**, utilizza le prede come fonte di sostentamento.

Nel modello considerato, il processo di caccia avviene con una probabilità
proporzionale al prodotto tra il numero di **prede** ed il numero di
**predatori**.

## Le equazioni di Lotka-Volterra

Detti rispettivamente $x(t)$ e $y(t)$ il numero di **prede** e di **predatori**
ad un dato istante di tempo, il sistema può essere descritto dalla seguente
coppia di equazioni differenziali:

$$
\begin{align*}
\frac{dx}{dt} &= (A - B y(t)) x(t)\\
\frac{dy}{dt} &= (C x(t) - D ) y(t)\\
\end{align*}
$$

Dove i parametri $A$ e $C$ indicano quanto rapidamente le due specie possano
riprodursi, una volta trovato sufficiente sostentamento, mentre i parametri $B$
e $D$ descrivono il tasso di mortalità delle due specie. La mortalità delle
**prede** è dovuta al cadere vittime dei **predatori**, mentre la mortalità dei
**predatori** è dettata dalla loro morte per stenti in caso la quantità di prede
catturate sia insufficiente.

Tutti e quattro i parametri, sono da intendersi maggiori di 0.

Come descritto sopra, il tasso di nutrimento e riproduzione dei predatori
dipende, a meno di una costante, dal prodotto $x(t) \cdot y(t)$, così come il
tasso di mortalità delle prede.

### Note sulla dinamica del sistema

Dato uno stato iniziale con $x(0) > 0$ e $y(0) > 0$, le orbite sel sistema sono
ristrette a coppie di valori $(x(t), y(t))$ positivi.

La soluzione del sistema di equazioni differenziali presenta due punti di
equilibrio:

$$\begin{align*}
e_{1} &= (0, 0)\\
e_{2} &= \left(\frac{D}{C}, \frac{A}{B} \right)\\
\end{align*}$$

Analogamente al caso dell'energia totale di punti materiali sottoposti
all'azione di soli campi di forze conservativi, il sistema è caratterizzato da
un **integrale primo**:

$$\begin{align*}
H(x,y) &= -D\ln(x)+Cx+By-A\ln(y)
\end{align*}$$

che **rimane costante nel tempo**.

### Versione discretizzata delle equazioni

Discretizzando le equazioni di Lotka-Volterra si ottiene:

$$\begin{align*}
x_i &= x_{i-1} + (A - B  y_{i-1}) x_{i-1} \Delta t\\
y_i &= y_{i-1} + (C x_{i-1} - D ) y_{i-1} \Delta t\\
\end{align*}$$

## Implementazione della simulazione in C++

Viene richiesto di sviluppare una simulazione che, introdotto uno stato
iniziale $(x(0), y(0))$ ed una serie di parametri $A, B, C, D$ **validi**,
utilizzi la versione discretizzata delle equazioni di Lotka-Volterra per
calcolare, ad ogni passo dell'evoluzione, i valori $(x_i, y_i, H_i)$.

La durata della simulazione, espressa in multipli interi dell'unità
discretizzata di tempo $\Delta t$, deve essere una variabile che l'utente può
introdurre a _runtime_.

Oltre alle caratteristiche minime che ogni progetto deve soddisfare (menzionate
nella pagina [principale della repository](README.md)), in questo caso sono
posti alcuni vincoli ulteriori.

**In primis**, la descrizione del sistema deve essere implementata tramite una
classe `Simulation` la quale deve, quantomeno:
- contenere un metodo `evolve()` che permetta di fare progredire la
  simulazione di una singola unità $\Delta t$;
- mantenere al suo interno i valori $(x_i, y_i, H_i)$ per tutti gli stati di
  evoluzione del sistema e renderli accessibili all'utente per eventuali stampe
  su schermo o analisi.

**In secondo luogo**, al fine di migliorare la stabilità del calcolo numerico
durante l'evoluzione, si richiede di utilizzare valori di $\Delta t$ dell'ordine
di $0.001$ e di rappresentare internamente $x_i$ ed $y_i$ come numeri `double`,
il cui valore viene espresso come frazione dei valori del punto di equilibrio
$e_{2}$.

> Ad esempio, in un sistema in cui $e_{2} = (1000.0, 800.0)$ la coppia di
> valori $(x_i, y_i) = (1200.0, 1000.0)$, diventerebbe, ai fini del calcolo,
> $(x_i^{rel}, y_i^{rel}) = (1.2, 1.25)$.

Al fine della registrazione dei valori per le analisi successive, $x_i$ ed $y_i$
devono essere di nuovo convertiti al loro valore assoluto.

## Variazioni sul tema

La soluzione minimale del progetto richiede che i dati da salvare possano
essere stampati a schermo o registrati in un file di output.

In aggiunta, è possibile considerare una o più delle seguenti variazioni
**opzionali**:

- si possono implementare gli strumenti per visualizzare in maniera grafica
  l'andamento del numero di **prede**, **predatori** e dell'integrale primo $H$,
  in funzione del tempo;
- si può sviluppare una finestra animata che, al variare del tempo, disegni in
  un piano cartesiano l'_orbita_ del numero di **prede** $x_i$ e **predatori**
  $y_i$;
- in analogia al gioco _game of life_, si può sviluppare una simulazione del
  modello in una griglia discreta, dove prede e predatori possono interagire coi
  loro "vicini";
- ogni altra variazione che vi paia interessante.

## Riferimenti utili

- [Equazioni di Lotka-Volterra - wikipedia](https://it.wikipedia.org/wiki/Equazioni_di_Lotka-Volterra)
- [Game of Life - wikipedia](https://it.wikipedia.org/wiki/Gioco_della_vita)
