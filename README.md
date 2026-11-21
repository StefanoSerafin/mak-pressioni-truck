# mak-pressioni-truck — PRESSIONI FLOTTE TRUCK, versione di Stefano

Web app per i gommisti truck: flotte, mezzi con schema assi, letture di pressione e battistrada per ruota con semaforo, storico e consumo per ruota, PDF per il cliente flotta, export/import JSON con unione tra dispositivi. Dati solo sul telefono (IndexedDB), nessun server.

LIVE: https://stefanoserafin.github.io/mak-pressioni-truck/

## Origine

Basata su PRESSIONI FLOTTE TRUCK di Matteo Varietà (`MAKWHEELS/workspace-interattivo-mak/pressioni-flotte-truck/`, 14/11/2026), copiata il 2026-11-21. Il formato dei file dati (`mate-pressioni-truck`) è lo stesso: i backup passano da una versione all'altra.

## Differenze rispetto all'originale

- **Contatto con l'agente**: nella scheda flotta, se ci sono mezzi senza TPMS o con TPMS da verificare, bottone «Chiedi un'offerta TPMS a Stefano» (WhatsApp con numero di mezzi, ruote e misure, senza il nome della flotta); scheda «Il tuo agente MAK» in Impostazioni e nella pagina `#/agente`, link nel piede. Il PDF per il cliente flotta resta del gommista, senza i contatti dell'agente. Dati dell'agente nella costante `AGENTE`.
- **Import sicuro**: `pulisciImport()` tiene solo i campi attesi, del tipo atteso (id, date, posizioni ruota, valori ammessi, foto solo `data:image`); `fmtD()` neutralizza il testo che non è una data. Prima un file .json preparato apposta eseguiva codice all'apertura della Home (provato).
- **iPhone**: l'avviso in Safari dice che i dati di Safari e quelli dell'icona sulla Home sono separati.
- jsPDF caricato solo quando si crea il PDF (il service worker lo tiene comunque per l'offline).
- Togliendo l'abbinamento trattore/semirimorchio si toglie anche dall'altro mezzo.
- I pulsanti a segmenti non stanno più dentro una `<label>` (toccare il titolo cambiava la scelta).
- Informativa aggiornata (`AVVISO_VER` 2026-11-21) con il paragrafo sul contatto con l'agente.

## Limiti noti

- L'origine `stefanoserafin.github.io` è condivisa con le altre app di Stefano: tutte le pagine dell'origine potrebbero leggere l'archivio del browser.
- Unione tra dispositivi a record intero: se due telefoni modificano la stessa lettura vince la più recente.
- Foto salvate come testo nell'archivio e nei backup: file pesanti con molte foto.
- Nessun conteggio d'uso (niente `conta.js`).

## Pubblicazione

File statici, nessun build. Modifica `index.html`, aumenta `APP_VER` e il nome della cache in `sw.js` se cambiano file precaricati, poi commit e push: GitHub Pages dal ramo `main`.
