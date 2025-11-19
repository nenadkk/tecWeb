# Tech Web, CSS
CSS (Cascading Style Sheets), "Cascading" indica che possiamo definire lo stile in diversi punti, e in base a dove lo definiamo ha più o meno priorità. 
I livelli inferiori prendono lo stile di quelli superiori.

Se si hanno dubbi se una certa funzionalità css è o meno supportata da un browser si può consultare il sito [CanIUse](https://caniuse.com/).

## I Fogli di stile
Insieme di regole che indicano la formattazione da apllicare.

Vantaggi:
- separaziona della grafica dalla struttura
- controllo più preciso dell'aspetto grafico
- manutenzione più facile
- dimensioni ridotte
- semplice da capire


Se l'orine con cui compaiono le cose non dipende più dal layot, da cosa dipende?
L'ordine con cui metto gli oggetti dipende dal motore di ricerca, quello che voglio far vedere al motore di ricerca lo metto per primo.
In più cerco di strutturare il sito per agevolare gli screen reader.

## Regole di sintassi 
La sintassi di una regola è: `selettore {blocco di dichiarazioni}`
- I selettori sono:
    - selettori di tag:
        - `h1 { color:red; font-family: Helvetica, sans-serif;}`
        - indica che **tutti** gli h1 del documento devono essere rossi e col font Helvetica, se non trova Helvetica usa il font sans serif.
    - selettori di id
    - selettori di classe
- Blocco di dichiarazioni è un insieme di coppie:
```
{
    proprietà: valore;
    proprietà: valore;
    ...
}
```


Regola per i font:
- su dispositivi elettronici si devono usare font senza grazie
- su carta stampata si usano font con grazie
Questo perché rispettivamente questi font aiutano alla lettura. 
Alcuni font possono essere più o meno difficili da leggere per le persone con dislessia.

## Come applicare il CSS
- Attraverso l'attributo "style" dei tag. 
NON SI FA MAI, perché non separa contenuto da presentazione.
- Css enbedded: si mettono le regole nel tag `<style>` all'interno del `<head>`. 
Separa un po' meglio, ma non è comunque il massimo perché se voglio usare su più pagine lo stesso stile allora devo ripetere questo codice su ogni pagina.
```
<html>
    <head>
        <style type=“text/css”>
            h1 {color: red;}
            p {font-family: sans-serif;}
        </style>
    </head>
... testo del documento ...
</html>
```
- Fogli di stile esterni: è il modo migliore per dividere contenuto e presentazione. 
Lo stesso foglio di stile può essere usato su più pagine. 
È possibile importare più fogli di stile, l'ultimo ha la precedenza.
```
<html>
    <head>
        <link rel=“stylesheet” href=“stile.css” type=“text/css”>
    </head>
    ... documento ...
</html>
```

Siccome una pagina può essere visualizzata su più dispositivi possiamo indicare quali fogli di stile usare in base al dispositivo.
Per fare ciò si usa l'attributo `media`, che può avere i seguenti valori:
- `all`: è di default, applica il foglio a tutti indistintamente. Come tutti i valori di default si può anche non mettere per risparmiare bit 
- `screen`: per indicare dispositivi con schermo.
Per distinguere tra pc e dispositivi mobili si deve fare un controllo ulteriore e si applica il foglio di stile in base alla dimensione dello schermo.
- `print`: il foglio di stile che si applica per quando la pagina viene stampata.
- `speech`: c'era una volta per indicare gli screen reader, ma ora non viene più usato.

```
<html>
    <head>
        <title> Esempio con differenti dispositivi </title>
        <link rel=“stylesheet” media=“screen” href=“screen.css” />
        <link rel=“stylesheet” media=“print” href=“print.css” />
        <link rel=“stylesheet” media=“speech” href=“screenreader.css” />
    </head>
    ... documento ...
</html>
```
Per fare il controllo sulla dimensione dello schermo:
```
media="screen and (max-width:480px), only screen and (max-device-width:480px)"
```
La differenza tra `max-width` e `max-device-width` è che `max-width` è la larghezza della finestra, mentre `max-device-width` è la larghezza del dispositivo. 
Nei cellulari questi due valori sono la stessa cosa, quindi si può lasciare `max-width`. 
Occhio che magari se sono su pc e rimpicciolisco troppo la finestra non passi alla modalità telefono.

Un altro modo per inserire il css è con `@import`. Sconsigliata.
```
<html>
    <head>
        <style type=“text/css”>
            @import url(“file.css”) print;
        </style>
    </head>
    ... testo del documento ...
</html>
```
È una via di mezzo tra un enbedded è un foglio di stile esterno. 
Si trova quando si importano font esterni. 
Un tempo veniva usato per nascondere certe cose a browser molto vecchi, oggi non ha più senso.

## Regole di applicazione
Uno stile applicato ad un elemento viene applicato automaticamente anche a tutti i suoi sottoelementi.
La regola viene ereditata dai figli a meno che questi non la sovrascrivano.
```
<body style=“color: blue”>
    <div> ... testo blu... </div>
    <div style=“color: green”>
        ... testo verde...
    </div>
    <div> ... testo blu... </div>
</body>
```
### Procedimento a cascata
Ordine di prirità quando si applicano le regole di stile:
1. Impostazioni personali dell’utente
    - dimensioni del font o estensioni che modificano la pagina
2. Impostazioni di stile inline definite dall’autore della pagina
3. Fogli di stile embedded definiti dall’autore
4. Fogli di stile esterni definiti dall’autore
5. Impostazioni di stile predefinite del browser
    - impostazioni utilizzate quando qualcosa non è definito o se il browser non supporta i CSS
    - cambiano da browser a browser
Dall'alto verso il basso è l'ordine di priorità, dal basso verso l'alto è l'oridine di applicazione. 
QUESTA È UNA DOMANDA D'ESAME.

Per aiutare gli sviluppatori è stata introdotta la definizione di importanza.
Se una regola, ovunque si trovi, ha la clausola `!important` davanti questa automaticamente sale al livello 2 di priorità (solo le impostazioni dell'utente la possono sovrascrivere).
```
selettore { proprietà: valore !important; }
```
Quindi l'ordine diventa così:

1. Impostazioni personali dell’utente
2. Dichiarazioni definite con `!important`
3. Impostazioni di stile inline definite dall’autore della pagina
4. Fogli di stile embedded definiti dall’autore
5. Fogli di stile esterni definiti dall’autore
6. Impostazioni di stile predefinite del browser

Generalmente, `!important` viene usato quando non ho capito perché la mia regola di stile non viene visualizzata. 
Indica quindi che c'è un errore da qualche parte. 
NON USARLO, la prof lo penalizza.

L'unico caso in cui si può usare è se si sta lavorando con dei framework e quindi non si ha il pieno controllo su tutte le regole applicate.

L'uso dell'`!important` è scoraggiato non solo per una questione di purezza del codice ma anche per via delle performance.
Noi vogliamo che il browser renderizzi il pià velocemente possibile le nostre pagine.
Più è complicato il css, più linee ha, più ci metterà il browser a caricare. 
Il browser comincia ad applicare regole, quando una regola viene sovrascritta deve tornare indietro e riapplicare tutto. 
L'`!important` tipicamente fa questo, va a sovrascrivere qualcosa di già caricato e porta il browser a dover fare lavoro in più.

## Selettori
Abbiamo detto che la sintassi è `selettore {regola}`.
I selettori indicano qual è il tag a cui voglio applicare la mia regola.
- Selettori di tipo: si riferiscono all'elemento da formattare
    - `p { font-size: 1em; }`
- Selettori di attributo: valori degli attributi class e id
    - Per selezionare una classe:
        - `.nomeClasse {font-weight: bold}`
    - Per selezionare un attributo id:
        - `#nomeId {color:blue}`

Il seguente paragrafo avrà tutte i gli stili scritti sopra:
```
<p id="nomeId" class="nomeClasse">Esempio</p>
```


La seguente regola si applica solo ai paragrafi con classe "grande":
```
p.grande {font-size: 2.5em; }
```

Un tag può avere un'unico id ma può avere più classi.
Quando si assegnano le classi al tag si separano da uno spazio.

Se ci sono confilitti viene applicata la regola più specifica. 
Se il conflitto avviene tra regole con pari specificità viene applicato l'ultimo inserito.

- Selettore universale
    - `* {font-weight: bold;}
    - si applica a TUTTO
- Raggruppamento di selettori
    - `h1, h2 {color: blue; font-size: 10pt; }`
- Figli e discendenti















