# AERONAV HAHO — Release Point Planner & Tactical Navigator

Applicazione web progressiva (**PWA**) installabile su smartphone e pronta per la pubblicazione diretta su **GitHub Pages** o qualsiasi hosting statico HTTPS.

## Novità v10
* **Pulsante `↻ AUTO / ORIZ / VERT`** nella barra della scheda navigazione: alterna rotazione automatica, blocco in orizzontale e blocco in verticale (scelta salvata). Il blocco funziona nella PWA installata (Android); in una scheda del browser usa lo schermo intero. Dove il blocco non è supportato (es. iPhone) resta la rotazione automatica del dispositivo.
* **Layout orizzontale**: con lo schermo in orizzontale i campi dati (efficienza, distanza DIP, velocità, direzione, MGRS) passano in una colonna a destra e la mappa, con il mirino e l'auto zoom, usa solo la parte sinistra.
* **Schermo sempre acceso** nel navigatore (Screen Wake Lock), riattivato quando l'app torna in primo piano.
* `manifest.json`: `orientation` ora è `any` (prima `portrait`), altrimenti l'app installata non potrebbe ruotare.

## Novità v9
* **Mappe salvate offline**: le porzioni di mappa (stradale e satellite) visualizzate a ogni zoom vengono salvate dal service worker (fino a 5.000 tasselli, poi i più vecchi vengono eliminati) e riutilizzate senza connessione. Pulsante `SVUOTA` nelle Impostazioni. Le zone mai visualizzate restano vuote offline.
* **Mappa satellitare**: nella scheda `IMPOSTAZIONI` del navigatore nuova sezione `MAPPA DI SFONDO` (Stradale OSM / Satellite Esri World Imagery). La scelta è salvata e applicata anche al Planner (che ha anche un selettore livelli sulla mappa). I tasselli satellitari richiedono connessione dati.
* **Auto zoom del navigatore**: con `AUTO ZOOM` attivo la mappa contiene sempre posizione corrente e DIP selezionato, anche in `HDG UP` (calcolo nello spazio schermo con rotazione bussola) e tenendo conto dei campi dati in alto; si riadatta anche quando ruota la bussola, si ridimensiona o si gira lo schermo.
* **Planner più reattivo**: ricalcolo con ritardo di 200 ms mentre si digita, zoom automatico solo quando la traccia esce dalla vista, DEM e venti scaricati in parallelo.
* **Tracce distinte**: caduta libera (arancio, spessa) e vela aperta (verde), con legenda, frecce di direzione e tooltip con distanza e tempo.
* **Quota lancio e quota apertura** separate nel Planner (al posto del campo unico "Apertura"). I vecchi dati salvati vengono migrati con lancio = apertura.
* **Deriva a paracadute chiuso**: il calcolo HARP ora include la caduta libera (lancio → apertura), con ratei di caduta libera impostabile (default 10.500 ft/min ≈ 53 m/s). Il corpo è trasportato solo dal vento; il tratto è mostrato tratteggiato in arancio.
* **Punto di apertura**: MGRS, deriva (distanza, direzione, tempo di caduta libera) e **pressione al suolo sulla verticale** riferita al QNH (atmosfera ISA, quota suolo da DEM). Il QNH si precompila da Open-Meteo (pressione al livello del mare) ma resta modificabile a mano. Il GPX include il waypoint `OPEN`.

## Novità v8
* **Scheda `IMPOSTAZIONI` nel navigatore**:
  * **Calibrazione Bussola**: quadrante bussola live, procedura guidata di calibrazione magnetometro a 8 (10 secondi), allineamento rapido a rilevamento DIP (`ALLINEA A ROTTA DIP`) e regolazione fine dell'offset / declinazione magnetica (`-180°` / `+180°`).
  * **Unità di Misura**: commutazione immediata tra **Piedi (`ft`) / Metri (`m`)** per quote e distanze, e **Nodi (`knots`) / Metri al secondo (`m/s`)** per velocità orizzontale e rateo di discesa, sincronizzata tra Navigatore e Planner.
