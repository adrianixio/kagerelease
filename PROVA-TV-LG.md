# Prova di KageGeki sulla TV LG (webOS) — istruzioni

Serve a vedere se la TV regge l'app prima di costruirla tutta. È una **prova di 15 minuti**: si installa un pacchetto piccolissimo (7 KB), lo si apre, si fanno due foto allo schermo. Non cambia nulla della TV e si cancella alla fine.

Il file è `KageGeki-webos-prova.ipk`, sulla pagina **Releases** del repository (<https://github.com/adrianixio/kagerelease/releases>). Serve una TV LG **del 2022 o più recente** (webOS 22+) e un PC Windows sulla **stessa rete (Wi-Fi o cavo) della TV**.

## 1. Account sviluppatore LG (una volta sola, gratis)

Registrati su <https://webostv.developer.lge.com> (pulsante *Sign up*) con un indirizzo email. Conferma l'email.

## 2. Sulla TV: attiva la modalità sviluppatore

1. Installa l'app **Developer Mode**: dal **LG Content Store** della TV (cerca «Developer Mode») oppure dal sito <https://lgappstv.com> accedendo con l'account sviluppatore e cercando «Developer Mode» (pulsante *Install*). Se non la trovi, avvisami: potrebbe dipendere dal paese.
2. Apri l'app **Developer Mode**, accedi con l'email e la password dell'account sviluppatore.
3. Premi **Dev Mode Status** per attivarla: la TV si riavvia da sola.
4. Riapri **Developer Mode** e attiva anche **Key Server**.
5. Nella schermata vedi in basso a sinistra una **password di 6 caratteri** (maiuscole e minuscole contano): tienila a portata di mano. Vedi anche **Remain Session**, il tempo che resta: è normale che sia limitato, si rinnova col tasto **EXTEND**.

L'indirizzo IP della TV: **Impostazioni › Tutte le impostazioni › Rete › Connessione Wi-Fi** (o cavo) › dettagli; annotalo (es. `192.168.1.60`).

## 3. Sul PC: installa gli strumenti LG e il pacchetto

1. Installa **Node.js** (versione LTS) da <https://nodejs.org> se non c'è.
2. Apri **PowerShell** e scrivi:

```powershell
npm install -g @webos-tools/cli
ares-setup-device
```

3. Nel menu di `ares-setup-device` scegli **add** e inserisci: nome `tv`, indirizzo IP della TV, porta `9922`, utente `prisoner`; salva. Poi:

```powershell
ares-novacom --device tv --getkey
```

Quando lo chiede, scrivi la password di 6 caratteri vista nell'app Developer Mode.

4. Metti `KageGeki-webos-prova.ipk` in una cartella (es. `Download`), vai lì in PowerShell e installa e avvia:

```powershell
ares-install --device tv KageGeki-webos-prova.ipk
ares-launch --device tv it.kagegeki.webos.smoke
```

(In alternativa l'app community *Dev Manager Desktop* fa lo stesso con i pulsanti: <https://github.com/webosbrew/dev-manager-desktop>.)

Se un comando dà errore, **fai una foto o copia il testo dell'errore** e mandamelo: è già un'informazione utile.

## 4. Cosa guardare sulla TV

L'app si chiama **KageGeki prova** (la trovi anche nell'elenco delle app). Quando parte:

- Per circa 12 secondi vedi la schermata del **lanciatore** con alcune righe verdi/rosse.
- Poi si apre da sola la **pagina di prova** con righe numerate da 1 a 6. Non serve premere nulla.

**Foto 1** (dopo circa 1 minuto dall'apertura): una foto leggibile dello schermo.
**Foto 2** (dopo 6-7 minuti, senza toccare nulla): un'altra foto della stessa schermata.

Poi, se ti va (altri 5 minuti):

- Premi qualche tasto del telecomando (**giallo**, **rosso**, **Indietro**, **OK**, **frecce**, **Menu** se c'è) e fai una foto della riga in basso, che mostra il codice del tasto.
- Chiudi l'app con **Indietro**, aspetta due minuti, riaprila e fai un'altra foto: ci dice se il servizio sulla TV si è fermato nel frattempo.
- Riapri l'app e, nei primi 12 secondi, premi **freccia destra**: si apre la «variante B». Foto dopo un minuto.

## 5. Quando hai finito

Per toglierla: dal PC `ares-install --device tv --remove it.kagegeki.webos.smoke` oppure dalla schermata delle app della TV (tieni premuto OK sull'icona › Elimina). La modalità sviluppatore si può lasciare o spegnere dall'app Developer Mode.

Mandami le foto: con quelle capisco se il progetto per la TV LG si può fare così o va ripensato.
