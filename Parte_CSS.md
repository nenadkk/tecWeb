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
        - 
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




















