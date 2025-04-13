<!-- omit in toc -->
# Progetto d'esame per l'a.a. 2024/2025

- [Introduzione](#introduzione)
- [Preparazione](#preparazione)
  - [Input al programma](#input-al-programma)
- [Relazione](#relazione)
- [Consegna](#consegna)
  - [Come creare l'archivio](#come-creare-larchivio)
- [Valutazione](#valutazione)
- [Eventuale riconsegna](#eventuale-riconsegna)
- [Uso di sistemi di Intelligenza Artificiale](#uso-di-sistemi-di-intelligenza-artificiale)

## Introduzione

Questa repository contiene la descrizione dei temi proposti per il progetto
d'esame per l'a.a. 2024/2025 e le modalità per la preparazione e la consegna.

Il progetto d'esame consiste nell'implementazione di uno o più programmi in C++,
accompagnati da una breve relazione di presentazione.

I progetti proposti riguardano:

- [Simulazione dell'interazione tra due specie](volterra.md)
- [Simulazione del comportamento di stormi](boids.md)
- [Dinamica in un biliardo triangolare](biliardo.md)

E' possibile presentare il progetto su un altro tema a propria scelta, purché di
complessità paragonabile e concordato preventivamente con i docenti.

## Preparazione

Raccomandiamo di svolgere il progetto in gruppo, fino a un massimo (non
derogabile) di quattro persone; data la sua semplicità, il progetto "Simulazione
dell'interazione tra due specie" può essere svolto in un gruppo di al massimo
due persone. Il progetto può però essere preparato anche singolarmente.

Il programma deve essere scritto in C++ standard, seguendo le indicazioni e le
raccomandazioni fornite a lezione nel corso dell'anno. E' ammesso l'uso di
librerie esterne (ad esempio per la grafica), ma queste devono essere
disponibili sulla piattaforma di riferimento (Ubuntu 24.04, con il compilatore
gcc v. 13).

Ogni programma deve essere costituito da **almeno due** *translation unit*.
Indicativamente la logica del programma va suddivisa tra uno o più header file
(`.hpp`) e tra uno o più file sorgente (`.cpp`); la funzionalità va poi
richiamata da un ulteriore file contenente il `main`.

Il codice deve essere formattato adeguatamente (con `clang-format` o tool
equivalente). Il file di configurazione del tool di formattazione
(`.clang-format` nel caso di `clang-format`) deve essere consegnato insieme al
progetto.

Nomi di file, funzioni, tipi, variabili, ecc. devono essere descrittivi e
seguire convenzioni ortografiche e di lingua uniformi.

I nomi di file e directory non devono contenere spazi ed essere in carattere
minuscolo.

E' richiesta la scrittura di *unit test*, usando *Doctest* o altro strumento
analogo.

Per il *build* del codice deve essere utilizzato [*CMake*](https://cmake.org/).
Questa repository contiene un file [`CMakeLists.txt`](CMakeLists.txt) di
esempio; per adattarlo al proprio progetto seguire i suggerimenti inclusi nel
file stesso sotto forma di commenti. Le opzioni di compilazione, in particolare
per i *warning* e i *sanitizer*, non possono essere rilassate.

I comandi che useremo durante la valutazione per configurare e buildare il
progetto saranno indicativamente i seguenti:

```shell
cmake -S . -B build -G"Ninja Multi-Config"
cmake --build build --config Debug
cmake --build build --config Debug --target test
cmake --build build --config Release
cmake --build build --config Release --target test
```

Sincerarsi quindi che funzionino correttamente.

Né la compilazione né l'esecuzione devono generare messaggi diagnostici, né in
modalità Debug né in modalità Release. Nel caso dovessero esserci segnalazioni
generate da codice di terzi (ad es. dalla libreria grafica), queste vanno
indicate nella relazione.

In questa repository sono già anche disponibili i file [`doctest.h`](doctest.h)
e [`.clang-format`](.clang-format). Quest'ultimo può essere adattato alle
proprie preferenze stilistiche.

I commenti nel codice devono essere minimali e avere lo scopo esclusivo di
aiutare noi a comprendere eventuali passaggi complessi.

Verranno valutati positivamente anche l'uso di *Git* come strumento
collaborativo e l'adozione di ogni altro strumento utile al miglioramento del
software prodotto. Se lo sviluppo avviene in una repository *Git*, potete
indicarne l'indirizzo nella relazione; se la repository è privata ed è tenuta su
[GitHub](https://github.com/), potete condividerla con noi aggiungendo gli
account `giacomini`, `battibass` e `fferrari1990`. Naturalmente questo **non**
sostituisce la consegna secondo le modalità indicate sotto.

### Input al programma

...

## Relazione

La relazione di accompagnamento rappresenta una guida alla comprensione del
codice e alla valutazione del lavoro nel suo complesso. La relazione deve essere
sintetica (indicativamente di lunghezza non superiore a qualche pagina) e deve
contenere:

- autore o autori del lavoro
- eventuali modifiche intercorse dalla consegna precedente
- descrizione sintetica delle principali scelte progettuali e implementative
- istruzioni dettagliate su come eseguire il programma o i programmi che fanno
  parte del progetto
- descrizione del formato di input e di output, con degli esempi
- interpretazione dei risultati ottenuti
- strategia di test per verificare che quanto ottenuto sia ragionevolmente
  esente da errori
- dichiarazione di eventuale uso di sistemi di Intelligenza Artificiale (vedi
  sotto)
- ogni altra informazione utile agli obiettivi sopra citati

La relazione deve essere in formato `pdf` o *markdown* (il formato con cui è
composto questo testo). Per un risultato tipografico eccellente si suggerisce di
provare LaTeX, o sul proprio PC o su strumenti online, ad es.
[overleaf](https://overleaf.com). Se si usano altri sistemi (ad es. MS Word o
LibreOffice), ricordarsi di esportare in formato `pdf`.

## Consegna

La consegna avverrà su [virtuale](https://virtuale.unibo.it) in prossimità di
ogni appello (indicativamente 10 giorni prima, contemporaneamente all'iscrizione
su [AlmaEsami](https://almaesami.unibo.it)) tramite un file archivio `.zip` o
`.tgz`. Ogni studente/studentessa deve inviare l'archivio, anche se il lavoro è
svolto in gruppo. La consegna va fatta ogni volta che ci si iscrive ad un
appello, anche se nel frattempo non sono intercorse modifiche al codice. Se il
lavoro è svolto in gruppo ed è lo stesso per tutti i componenti del gruppo,
chiediamo di caricare lo stesso identico archivio.

L'archivio deve contenere:

- il codice sorgente e tutte e sole le risorse necessarie alla compilazione e
  all'esecuzione (ad esempio eventuali immagini e font)
- una breve relazione di accompagnamento

L'archivio **non** deve contenere altro. A titolo puramente indicativo,
l'archivio non deve contenere:

- la directory di build di CMake
- file di output ottenuti dall'esecuzione del programma
- directory quali `__MACOSX` o file con suffisso `_Zone.Identifier`

Verificare che non ci siano file inutili nascosti; per scoprirli usare il
comando `ls -A`.

Prima di creare l'archivio, verificate attentamente il contenuto e fate
eventualmente pulizia di tutto quanto non va consegnato.

### Come creare l'archivio

Supponendo che tutto il codice e la relazione si trovino in una cartella
`progetto`, per creare un archivio in formato `zip`:

```shell
$ ls
progetto
$ zip -r progetto.zip progetto
$ ls
progetto progetto.zip
```

Per creare un archivio in formato `tgz`:

```shell
$ ls
progetto
$ tar zcf progetto.tgz progetto
$ ls
progetto progetto.tgz
```

Prima di produrre l'archivio sincerarsi che la directory contenga la relazione.
Una volta creato l'archivio, consigliamo di sincerarsi che, una volta
scompattato, contenga tutto quanto necessario per la compilazione e
l'esecuzione. Per scompattare, spostarsi in un'altra cartella e usare i comandi
`unzip progetto.zip` o `tar zxf progetto.tgz`.

## Valutazione

La valutazione si basa su cinque criteri:

- La **qualità della relazione** intende valutare la capacità della relazione di
  accompagnare il lettore nella comprensione del programma, nelle varie scelte
  di design, di implementazione, di ricerca della correttezza. Si tiene inoltre
  in conto la correttezza lessicale e grammaticale, nonché l'uso corretto della
  lingua (italiana o inglese).

- La **qualità del design** del programma intende valutare quanto il design
  dell'applicazione è appropriato per risolvere il problema proposto. Elementi
  considerati sono, a titolo esemplificativo, la suddivisione del codice in
  classi e funzioni dai nomi significativi, la loro progettazione e il loro uso
  secondo le indicazioni date a lezione, la *const-correctness*, la suddivisione
  del codice in più file header e sorgente, il passaggio appropriato dei
  parametri alle funzioni.

- La **qualità dell'implementazione** del programma intende valutare
  l'applicazione corretta ed efficiente dei costrutti del linguaggio C++
  nell'implementazione del programma, secondo le convenzioni consolidate e
  proposte a lezione. Verranno considerati, ad esempio, la leggibilità del
  codice, la scelta di nomi significativi per le variabili, la corretta
  formattazione del codice, l'uso corretto della standard library, l'uso di
  algoritmi invece di cicli espliciti.

- La **correttezza del programma** intende valutare quanto il comportamento del
  programma in esecuzione sia aderente a quanto specificato nella consegna e,
  per quel che riguarda aspetti non specificati o eventuali varianti, nella
  relazione. Verranno anche considerate le strategie e le tecniche utilizzate
  per verificare che il programma si comporti correttamente, la completezza dei
  test, la validazione dei dati di input.

- L'**originalità della soluzione** intende valutare innanzitutto il rispetto di
  quanto previsto nella descrizione del progetto. Un giudizio oltre la
  sufficienza dipende dall'esplorazione di altre opzioni e varianti ovvero
  dall'utilizzo di strumenti, librerie, tecniche aggiuntivi.

Ogni criterio sarà valutato secondo la scala: *insufficiente*, *sufficiente*,
*buono*, *ottimo*. Indipendentemente dalla valutazione complessiva ottenuta, la
sufficienza si intende acquisita solo se la valutazione di ogni singolo criterio
è almeno sufficiente.

## Eventuale riconsegna

La valutazione del progetto vale per tutto l'anno accademico, ma è possibile
effettuare ulteriori riconsegne in caso questa sia risultata insufficiente, o
per migliorarla anche se già sufficiente.

In entrambi i casi, si richiede di **proporre variazioni significative**
rispetto alla consegna precedente.

Riconsegne individuali sono ammesse anche se il progetto è stato sviluppato
originariamente in gruppo, ma i diversi componenti del gruppo si presentano
all'orale ad appelli diversi.

In tal caso, al fine di migliorare la valutazione, è necessario che le
variazioni apportate al progetto *vadano oltre a quelle proposte dai docenti*
durante i colloqui affrontati da coloro che hanno già sostenuto l'esame.

In qualsiasi caso, **le variazioni** intercorse tra le diverse versioni del
progetto **vanno elencate** esplicitamente **all'inizio della nuova relazione**, altrimenti verrà confermata la valutazione precedente.

Si possono presentare progetti che siano già stati presentati in anni accademici
precedenti da parte di persone dello stesso gruppo solo se includono variazioni
significative e originali.

## Uso di sistemi di Intelligenza Artificiale

Ai fini dell'apprendimento è sconsigliato un uso eccessivo di sistemi di
Intelligenza Artificiale, soprattutto per la generazione del codice. L'eventuale
uso deve comunque essere conforme alla [policy di
Ateneo](https://www.unibo.it/it/ateneo/chi-siamo/intelligenza-artificiale/Casi-uso-GenAI-comunita-studentesca-valutazione)
e dichiarato nella relazione.

Naturalmente tutto il codice consegnato deve rispettare le linee guida
raccomandate a lezione e deve essere corretto. Durante l'orale lo studente o la
studentessa devono dimostrare di averlo compreso ed essere in grado di
riprodurlo autonomamente.
