<!-- markdownlint-disable-file MD014 MD028 -->

<!-- omit in toc -->
# Installazione di SFML 2.6 su macOS

- [Introduzione](#introduzione)
- [Installazione di SFML 2.6](#installazione-di-sfml-26)
- [Installazione della versione 16.4 beta dei Command Line Tools](#installazione-della-versione-164-beta-dei-command-line-tools)

> [!CAUTION]
> Le istruzioni riportate di seguito sono valide **unicamente** per gli
> utilizzatori di macOS, i quali:
>
> - abbiano una versione del sistema operativo compatibile con _Homebrew_
>   (Ventura, Sonoma, Sequoia);
> - abbiano necessità di utilizzare SFML 2.6 per **collaborare con studenti che
>   utilizzano Ubuntu** (installazione nativa o tramite WSL);
> - incorrano in errori nella compilazione del progetto (non di configurazione
>   dell'area di _build_ o _linking_) imputabili direttamente a SFML.

## Introduzione

Come descritto altrove durante il corso, quest'anno utilizziamo come
**piattaforma di riferimento Ubuntu 24.04**. Pertanto, per lo sviluppo
collaborativo di progetti che fanno uso di librerie esterne (es. SFML), vogliamo
che i diversi ambienti di sviluppo (es. quelli basati su macOS) siano "il più
simile possibile" a quello in Ubuntu 24.04.

Questo significa che **gli utenti macOS che collaborano con utenti
Windows/Linux** devono **installare SFML 2.6**, se ne fanno uso.

> [!IMPORTANT]
> Singoli individui o gruppi che sviluppano il progetto d'esame utilizzando
> unicamente macOS possono avvalersi di SFML 3.0, ma devono **specificarlo
> nella relazione**.

La ricetta di installazione, risulta leggermente più complicata del solito, a
causa di una **incompatibilità** tra il pacchetto **SFML** fornito con brew e la
**versione stabile dell'ambiente di sviluppo _X code_ o dei _X code Command Line
Tools_**.

## Installazione di SFML 2.6

All'oggi, brew installa "di default" **SFML 3.0**; permette però anche
l'installazione di versioni di SFML della famiglia di _release_ 2.X.

Per effettuare il _downgrade_ a SFML 2.6 procedete come indicato qui:

```zsh
$ brew remove sfml
...
$ brew install sfml@2
...
```

Potete verificare la correttezza dell'installazione tramite il comando:

```zsh
$ brew info sfml@2
==> sfml@2: stable 2.6.2 (bottled) [keg-only]
Multi-media library with bindings for multiple languages
https://www.sfml-dev.org/
Installed
...
```

A questo punto, è necessario aggiungere alcune variabili d'ambiente nel file
`.zshrc` che configura il terminale di macOS alla sua apertura.

Per farlo eseguite il comando:

```zsh
$ code ${HOME}/.zshrc
```

e aggiungete la seguente riga in fondo al file appena aperto:

```zsh
export SFML_DIR="/opt/homebrew/opt/sfml@2/"
```

salvate il file, chiudete il terminale e riapritelo per configurarlo
correttamente.

## Installazione della versione 16.4 beta dei Command Line Tools

Il problema di compatibilità riportato sopra **si verifica** se è installata la
versione **16.3** di _X code_ o dei _Command Line Tools_, che porta con se la
versione del compilatore `clang-1700.0.13.3` .

Potete verificare la versione installata sul vostro portatile usando il comando:

```zsh
$ g++ --version       
Apple clang version 17.0.0 (clang-1700.0.13.3)
Target: arm64-apple-darwin24.5.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```

In caso di riscontro positivo consigliamo di scaricare la versione **16.4 beta**
dei **Command Line Tools**, che trovate
[a questa pagina web](https://developer.apple.com/download/all/?q=xcode).

> [!IMPORTANT]
> È necessario ricordare e-mail e password del proprio apple ID per effettuare
> il download.

> [!IMPORTANT]
> Considerando i limiti della rete wireless durante i laboratori, vi
> **consigliamo vivamente** di **scaricare il pacchetto da casa**.
>
> Potremo poi installarlo e configurarlo assieme in laboratorio, qualora
> preferiate non farlo da soli.

Procedete quindi cliccando sul pacchetto
`Command_Line_Tools_for_Xcode_16.4_beta.dmg` per effettuare l'installazione.

Una volta terminato il processo, aprite di nuovo il terminale e digitate:

```zsh
$ sudo xcode-select -s /Library/Developer/CommandLineTools/
Password:
```

poi:

```zsh
$ g++ --version                                            
Apple clang version 17.0.0 (clang-1700.0.13.5)
Target: arm64-apple-darwin24.5.0
Thread model: posix
InstalledDir: /Library/Developer/CommandLineTools/usr/bin
```

per verificare il corretto aggiornamento della versione di compilatore (e
libreria standard) a `clang-1700.0.13.5` (o superiori).
