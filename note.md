# Appunti di Tech Web
- Siti utili:
    - w3c
    - mdn

- +50% degli accessi ai siti avvengono da telefono

- Produzioamo un html che sia valido. Nella validazione si controlla che il codice sia sintaticamente corretto ( != compilazione)
    - In classe usiamo [W3Validator](https://validator.w3.org/)
- Accessibilità e ranking sono il motivo per cui sono state fatte la maggior parte delle scelte

## HTML5
- Can i use, sito che per ogni browser dice in quale versione è compatibile con certe funzionalità

- Per progetto: HTML con sintassi XML

- Tre elementi da separare: Comportamento (JavaScript), Struttura (codice html) e Presentazione (css)
    - Divisione rende tutto più mantenibile

## Sintassi XHTML

- i tag e gli attributi sono case sensitive (tutto in minuscolo)
- i tag devono sempre essere chiusi (anche se sono vuoti)
    - `<br />` e non `<br>`
    - in realtà nei tag su singola riga si può anche non mettere la chiusura con `/`

- i tag devono essere aperti e chiusi nell’ordine corretto
- l’ordine con cui si inseriscono gli attributi è irrilevante
- i valori degli attributi vanno riportati tra “virgolette doppie”
- tutti gli attributi devono avere un valore
    - può essere ignorata solo per quegli attributi il il valore è il nome dell'attributo
- un elemento in linea non può contenere un elemento di blocco
- I browser cercano di visualizzare al meglio codice non valido, ma questo può portare ad interpretazioni arbitrarie

### Alcune semplificazioni fatte da HTML
- `<!DOCTYPE html>`
- `<meta charset="utf-8">`
- `<script rel="script.js"></script>`
- `<link rel="stylesheet" href="print.css"/>`

### Prologo XML
- Il W3C raccomanda di usare il prologo XML ma molti browser non lo gestiscono bene e causano errori, quindi è da evitare.
- `<?xml version=“1.0” encoding=“ISO-8859-1”?>`   

### Elementi che vengono ignorati dai browser
- le interruzioni di linea non identificate con `<br/>` e non contenute in un tag `<pre>`
- tabulazioni e spazi multipli
- tag `<p>` nidificati
    - `<p>` nidificati sono considerati un errore
- tag sconosciuti
- commenti: <!-- commento -->
    - ATTENZIONE: all’interno di un commento non è possibile inserire la stringa “--” (doppi trattini)

# Come sono formati i nostri file HTML
- `<!DOCTYPE html>` è la prima riga, dice al browser che tipo di file ha davanti
- `<html lang="it">` definisce la lingua principale [Accessibilità]
- `<meta charset="UTF-8" />` dice che tipo di caratteri sto usando. Questo tag meta deve essere contenuto nei primi 512 bit, altrimenti il browser decide da solo.

## Intestazione
- La parte contenuta tra i tag `<head>` e `</head>` viene chiamata intestazione o semplicemente, sezione head.
- In questa sezione si trovano tutti i tag che impartiscono direttive al browser quali: titolo (obbligatorio), comandi meta, richiami ai fogli di stile, script.
- Tutto ciò che si trova all'interno della struttura head non sarà visualizzato ma interpretato dal browser (tranne il titolo, quello lo vede anche l'utente). La sezione head quindi è una zona destinata ad uso esclusivo dei soli comandi che impartiscono direttive ben specifiche

### Elementi dell'Head
- `title`(obbigatorio), `link`,`meta`,`base`,`style` e `script`
- I `link` sono collegamenti a risorse esterne (CSS, icon, ecc)
    - suoi attributi comuni sono `href` e `rel`(relazione). Es:
        - `<link rel=“stylesheet” href=“/file.css” />`
        - `<link rel=“shortcut icon” href=“/img.ico” />`
        - `<link rel=“next” title=“Next page” href=“/next.html” />`
            - da evitare quest'ultima
- La `base` definisce la posizione di base per i collegamenti
    - `<base href=“/miacartella/” />`
- `style` e `script` servono per inserire codice css e js direttamente nella pagina HTML, non sono quindi da usare perché dobbiamo rispettare il principio di separazione. Questi tag sono presenti solo per retrocompatibilità

- Tag meta http-equiv, possono condizionare il funzionamento della pagina
- Tag meta name, danno info riguardo al documento. E' possibile creare dei propri valori
    - `description` breve descrizione della pagina. E' importante che contenga le keywords
    - `keywords`: lista di parole chiavi separate da una virgola. Se le pagine contengono effettivamente le keyword aumenta la trustness. Meglio che ci siano nei titoli oltre che nei paragrafi
    - `copyright`
    - `author`
    - `robots`
    - `rating`
    - `viweport` aiuta ad adattare i siti su dispositivi diversi (es telefoni)

### Elementi del body
- La parte contenuta tra i tag `<body>` e `</body>` viene chiamata corpo del documento o semplicemente, sezione body.
- L'obbiettivo è dare una struttura semantica, ovvero dividere il testo in parti e indicare l'importanza delle parti.
- La sezione body contiene quindi tutti i tag che descrivono la struttura del documento: non devono essere usati elementi relativi alla presentazione visuale

- Si devono usare gli elementi per il loro significato e non per come vengono visualizzati dai browser 

- Attributi comuni, possono essere messi a qualsiasi tag
    - `class`, assegna una classe di riferimento a cui possono appartenere diversi elementi, anche tag diversi
    - `id`, assegna un identificativo unico all'interno della pagina. Ha maggiore specificità della classe quando si fa il css. Può essere usato come destinazione di un id. Ha maggiore supporto javascript anche con browser vecchi
    - `title`, aggiunge un titolo ad un elemento
    - `style`, istruzioni css in linea per quel tag
    - `xml:lang` indica la lingua. Può essere usato per specificare la lingua di un certo paragrafo se questa non è la stessa della pagina
    - attributi evento, per attaccarci eventi javascript

- Tag generalisti, non hanno nessun valore semantico. Se ciò che si vuole scrivere ha un valore semantico serve usare tag diversi
    - `<div>...</div>` contenitore generico, serve per poter associareil suo contenuto aun foglio di sile. Gli attributi associati a un div si diffondono su tutto il suo contenuto
    - `<span>...</span>` come il `<div>` ma su una sola linea
        - es. di uso: quando c'è una parola in un'altra lingua, si mette quella parola tra `<span` e si da l'attributo `lang` indicando la lingua. A livello visivo non cambia niente ma il motore di ricerca/screen reader sanno che quella è una parola in un'altra lingua

### Markup strutturale
HTML5 aggiunge dei tag per descrivere meglio la struttura del documento

- `header` e `footer`, rispettivamente intestazione(o banner) e piè di pagina. Possono essere presenti più volte nella stessa pagina/sezione . Il `footer` identifica le info su chi ha scritto i contenuti
- `main`, contenuto principale
- `nav`, elementi di supporto alla navigazione. Può essere contenuto nell'header
- `aside`, parte del contenuto che può essere rimossa senza diminuire il significato della pagina, fa da supporto
- `section`, per raggruppare contenuti sullo stesso tema o logicamente collegati
- `article`, porzione di testo autocontenuto e indipendente dal resto del documento che possa essere distribuito in modo autonomo
- Non ricorrere a `section` e `article` per soli motivi di stile. Usare il `div` in quel caso
- `article`, `nav`, `section` e `aside` sono sectioning element, ovvero possono contenere `header`, `nav` e `footer`

Per controllare se il documento è stato strutturato bene una buona possibilità è verificare il sommario generato automaticamente: [Silktide](http://gsnedders.html5.org/outliner/)

Se il browser non supporta il markup strutturale esiste una [libreria Javascript](http://html5shiv.googlecode.com/svn/trunk/html5.js) che la interpreta per lui 

IMP.: Non mettere troppi heading e troppo lunghi nel sito perché il browser pensa che lo fai per ingannarlo per dare più valore alle tue keyword

Esempio header (corretto)
```
<header>
    <img src="/img/logo_unipd.png", alt="logo Università Padova" />
    <div id="headerText">
        <nav>
            <form>...</form>
        </nav>
        <h1>Corsi di laurea in informatica</h1>
        <p>Sito dedicato ai corsi di laure in informatica</p>
    </div>

```
In diversi siti nel tag `<header>` si potrebbe trovare scritto `<header role="banner">`. `<header>` definisce di base il banner, `role="banner"` si usava col `<div>` per dire che quel `<div>` aveva il ruolo di banner. Adesso non è necessario metterlo perché è già considerato "di default".

- Caratteri speciali 
    - `"` si inserisce con `&quot`
    - `<` si inserisce con `&lt`
    - `>` si inserisce con `&gt`
    - `€` si inserisce con `&euro`
    - `&` si inserisce con `&amp`
- Enfasi del testo
    - `<em> </em>` = enfasi, sostituisce `<i>` (italic)
    - `<strong> </strong>` =  forte enfasi, sostituisce `<b>` (bold)
- Intestazioni
    - sei livelli di intestazione: h1,h2 ... h6
    - va rispettato l'ordine, non puoi saltare da h1 ad h5
    - bisogna pensare alla struttura del documento e non a come vengono visualizzati
        - la visualizzazione può essere modificata con css

- Regole per scrivere i titoli
    - Scrivi un titolo unico per ogni pagina
    - Cerca di essere conciso e descrittivo
    - Evita titoli vaghi e generici
    - Utilizza la maiuscola per la prima lettera della frase o la prima lettera di ogni parola
    - Crea contenuti degni di click ed evita i clickbait
    - Pensa all’intento di ricerca
    - Includi la parola chiave principale quando ha senso farlo
    - Massimo 60 caratteri


La marcatura del testo deve corrispondere al significato semantico dell’elemento in essa racchiuso:
```
<body>
    <p class=“titolo”>....</p>
    <p>...</p>
    
    <p class=“sottotitolo”>....</p>
    <p>.. </p>
</body>
```

## Citazioni
- `blockquote` è un tag di blocco che riporta una citazione, un `q` è il corrispondente di `span` (quidi su singola riga) con la caratteristica semantica di una citazione
- si può usare l'attributo `cite` per dare una fonte, necessita di un url necessariamente, in alternativa c'è `title`
- in HTML5 il tag `<cite>` esistema ma deve essere il titolo di un libro, film ecc

## Abbreviazioni, acronimi, indirizzi
- acronimo è diverso da abbreviazione, acronimo è quando leggo tutte le lettere (es. NATO)
    - nel caso delle abbreviazioni devo indicare nell'attributo title per esteso cosa vuol dire

## Tag per testo particolare
- `code`, per del codice
- `var`, indentifica delle variabili nel codice
- `samp`, per quando c'è l'outup di un programma
- `pre` testo preformattato, dove spazi e a capo hanno valore

- `ins` : identifica un inserimento redazionale. Solitamente è visualizzato sottolineato  
- `del` : identifica una cancellazione redazionale. Solitamente è visualizzata barrata
- Possono essere usati sia come elementi in linea che di blocco

Alcuni tag semantici più interessanti sono
- `time`, con attributo `datetime` che contiene data/ora in formato XML
- `mark` evidenzia il testo
    - (tralasciando gli heading) i motori di ricerca danno la seguente importanza: strong > em > mark
- `meter` indica una scala con un max e un min
- `progress`, per indicare un valore che sta cambiando. Va usato con javascritp se si vuole far vedere una barra che avanza. Se un valore che voglio mostrare è fisso non uso `progress` per indicarlo
- `small` note a piè pagina
- `figure`/`picture`
    - se voglio inserire un'immagine uso `<img>`
    - se voglio aggiungere un testo all'immagine, come una didascalia all'immagine nei libri allora uso `<figure>`
    - se voglio inserire un'immagine che cambia (risoluzione o formato) in base al dispositivo, uso `<picture>`

## Elenchi 
Key word che appaiono all'interno di un punto elenco sono considerate di più dal browser rispetto a quelle che appaiono nel testo normale.
Sono molto importanti perché attirano l'attenzione. 
Un testo organizzato per punti elenco è più facilmente leggibile.

Tre tipi di elenchi:
- `<ul>`, unordered list 
    - i cui elementi vanno identificati con `<li>` list item
- `<ol>` ordered list 
    - anche qui gli elementi sono `<li>`
    - l'attributo `reverse` permette di invertire la lista
    - l'attributo `start` dice da che numero partire
    - l'attributo `type` dice il tipo di marcatore. DA NON USARE, se serve cambiare marcatore lo si fa da css
    - si può attribuitre un `value` ai punti della lista

- `<dl>` liste di definizione, come in un enciclopedia, un elenco di voci che vengono poi descritte
    - `<dt>` indica la voce da definire
    - `<dd>` indica la definizione della voce, possono esserci più `<dd>` per ogni `<dt>`

La navigazione dovrebbe contenere il menù come elenco di link. I link attivi non devono avere la `<a>` perché i broser ad oggi mettono le pagine caricate in cache, non appare neanche il caricamento della pagina e all'utente sembra che il sito non funzioni. ERRORE GRAVE

## Immagini
Il tag principale è `<img>`. 
Attributi:
    - `src` indica l'immagine da prendere
    - `alt` indica il testo alternativo. Testo che descrive l'immagine. Deve essere breve, per aiutare ma non rallentare troppo. E' OBBLIGATORIO, anche se vuoto deve esserci
    - `longdesc` da un URI a pagine che descrivono le immagini, per immagini che non possono essere descritte velocemente. DEPRECATO
    - `width` e `height`, è possibile definire altezza e larghezza sia in HTML che in css. Nella stragrande maggioranza dei casi si fa nel Css per mantenere la divisione tra presentazione e contenuto, però metterlo in html PUO' migliorare l'esperienza utente. Siccome l'html è il primo file che il browser riceve, se la dimensiode dell'immagine è già lì il rendering è più veloce. Se la pagina è particolarmente complessa ha senso mettere le dimensioni all'interno del'html. 

CI SONO DEI TEST PER CAPIRE QUANDO È IL CASO DI FARLO? O È SOLO A DISCREZIONE DELLO SVILUPPATORE

### Lazy loading
Raramente una pagina è completamente visualizzata, spesso per vederne il resto usiamo lo scroll. Visto che dobbiamo far caricare il più velocemente possibile la pagine, possiamo dire al browser che un'immagine va caricata solo quando viene visualizzata.
Si fa tramite l'attributo `loading`, che può avere il valore `eager` (default) che carica subito l'immagine, oppure `lazy` che la carica solo quando visibile.
Questo velocizza il caricamento iniziale ma potrebbe rallentare il caricamento durante lo scrolling. 
Per non appesantire la pagina si da questo attributo solo alle immagini "below the fold" ovvero quelle che non sono visualizzate senza lo scroll.

Per aggiungere una didascalia:
```
<figure>
    <img src="figure.jpg">
    <figcaption>Didascalia della figura</figcaption>
</figure>
```
Una figura non deve necessariamente avere un'immagine.
Un'immagine che è associata a una didascalia non ha bisogno dell'attributo `alt`. Però potrebbe essere comunque necessario. 

Le keyword all'interno di un `alt` sono importanti.
Esempio di uso del `<picture>`:
```
<picture>
    <source media="(min-width:650px)" srcset="img_pink_flowers.jpg">
    <source media="(min-width:465px)"srcset="img_white_flower.jpg">
    <img src="img_orange_flowers.jpg" alt  ="Flowers">
</picture>

```

## Link
Tag `<a>` per inserire un link. La destinazione sta all'interno di `href`. All'interno del tag può esserci anche un'immagine e in quel caso deve l'alt non descrive l'immagine ma il suo scopo.

Per evitare il disorientamento serve che gli utenti riconoscano i link e capiscano dove li porta. La sorgente del link deve essere significativa, è bene che non sia l'immagine ma anche in quel caso deve essere esplicitato il suo ruolo. Nel caso di un logo che porta alla home, l'`alt` è "home pagina" e non la descrizione del logo.

Se il link non porta a una pagina ma a (esempio) a un dowload serve specificarlo e dire la dimensione del download.












# APPUNTI 22/10

```
*{
    padding:0em;
    margin: 0em;
 }
```
Tolgo margini e spazi che possono essere eventualmente aggiunti dal browser in modo da poter essere sicuro che quelli che imposto io appaiano correttamente


Quando inserisco un immagine devo mettere un background che sia del colore predominante dell'immagine perché se l'immagine non si carica ci sarebbe testo bianco su sfondo bianco.

Background contain -> l'immagine si vede completamente ma non per forza riempie tutto lo spazio. A meno che io non metta non-repeat l'immagine si ripete 

Background -> si riempie tutto lo spazio ma non per forza si vede bene l'immagine

Usare sempre unità di misura relative e mai assolute


# Laboratorio 24/10
- sopra i 1200 pixel si muove la testa per leggere, questo alla lunga stanca l'utente












