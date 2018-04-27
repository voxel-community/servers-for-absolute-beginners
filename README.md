# servers-for-absolute-beginners

Cos'è un server? Come fanno a far funzionare i siti che usiamo ogni giorno? Lo sapevi che in pochi minuti puoi avviare il tuo server senza scrivere una riga di codice?

## Introduzione

Quanti post-it servirebbero per contenere di le ricerche fatte su google ogni giorno?


## Cos'é un server?

I server sono nati nel momento in cui c'é stato il bisogno di condividere delle risorse, dai siti web alle mail, dai file su drive ai film in streaming.
Un server è un PC, può essere potente come un server del datacenter di Google, ma può essere anche un semplice PC, come il tuo.

## Come funzionano i siti?
Il server come dice la parola stessa offre un servizio.
Prendiamo come esempio un web server di Facebook.

Quando digiti l'url di Facebook `www.facebook.com` e clicchi invio stai mandando una richiesta al server di Facebook per farti dare la tua bacheca con le notizie del giorno. Quel server ti invia il sito di Facebook con i tuoi relativi dati. Da una parte abbiamo quindi un "servitore", il `server` di Facebook e dall'altra abbiamo un ricevitore, il tuo browser, detto `client`.

![](/Screen/client-server-model.jpg)

## Come comunicano il server e il client

Ovviamente una parte fondamentale di questo processo di comunicazione è internet, nello specifico, il protocollo HTTP. Ogni Web browser implementa questo protocollo per scambiare informazioni con il server. HTTP utilizza un modello in cui un client effettua una richiesta e il server restituisce una risposta. Le richieste fatte al server possono essere di vario tipo puoi chiedere di ricevere una risorsa, utilizzando il metodo `GET` ma puoi anche pubblicarne una tu con il metodo `POST`. Queste sono tra le chiamate piú utilizzate tra client e server.

## Obiettivo di oggi

Il nostro obiettivo sarà quello di riuscire di creare un programmino che ci permetta di avviare un server sul nostro pc e su di esso rendere un file disponibile accessibile da remoto, ad esempio, tramite un browser.

## Innanzitutto creiamo il file con le nostre informazioni

Per esempio possiamo elencare le lingue che sappiamo parlare.

Per prima cosa quindi apriamo il nostro editor e creiamo un file `informazioni.json` e per comodità salviamolo in una nuova cartella denominata `dati` nella nostra cartella utente.

JSON, JavaScript Object Notation, è un tipo di notazione molto utile per organizzare dei dati attraverso oggetti JavaScript e scambiare informazioni tra un client e un server.

Come prima cosa indichiamo l'url con il quale verrà chiamata la risorsa, se stiamo parlando di lingue un nome appropriato per l'url potrebbe essere `/lingue` e questo farà parte dell'indirizzo web a cui accederemo per fare le nostre operazioni.

Ad esempio in `https://www.facebook.com/girlscodeit/`, la nostra risorsa, la pagina facebook di girlscodeit é raggiungibile tramite `/girlscodeit`.

Per semplicità oggi faremo solo 1 delle 4 operazioni possibili quali: leggere, creare, aggiornare ed eliminare dati. Noi renderemo possibili le letture con il metodo `GET`.


```
{
  "/lingue": {
    "get": {
      "lingue": [
        {
          "nome": "Italiano",
          "livello": "Ottimo"
        }
      ]
    }
  }
}
```
Proviamo ad andare a prendere le nostre lingue.

## Cosa di serve per avviare il nostro server

Essendo `mock-json-servers` il programmino in JavaScript che ci serve per avviare il server, prima di riuscire a installare questo abbiamo bisogno di un motore di JavaScript che si chiama `Node.js`.

`Node.js` è un framework di JavaScript che ci permette tra le varie cose di utilizzare `npm`, Node Packege Manager, il gestore di pacchetti JavaScript.

Nel nostro caso `mock-json-servers` è per l'appunto uno di questi migliaia di pacchetti che gestisce `npm`.


## Le installazioni

- [Node.js](https://nodejs.org/en/download/)(https://nodejs.org/en/download/) npm si scarica insieme a Node. Ricordatevi di riavviare il pc alla prima installazione. Per verificare che si siano correttamente installati possiamo digitare dal terminale i seguenti comandi:
```
node --version
npm --version
```
i quali dovranno restituirci, in caso di successo, le versioni dei due software appena installati.


- [mock-json-server](https://www.npmjs.com/package/mock-json-server)(https://www.npmjs.com/package/mock-json-server)
Per installarlo aprire il terminale e digitare:
```
npm install -g mock-json-server
```

## Avviamo il nostro server

Con il file che abbiamo creato possiamo finalmente avviare il nostro server.
Andiamo sul terminale e digitiamo:

```
mock-json-server dati/informazioni.json
```

Nel caso tu abbia salvato il file in JSON in una cartella diversa da quella detta precedentemente basta che indichi al posto di `dati/` il percorso del tuo file.

`mock-json-servers` oltre che ad avviarci un server ci aiuta a rendere disponibile il nostro file come API così che possiamo accederci dall'esterno.
Proviamoci!!

Andiamo sul browser per accedere alla nostra API che di default se non indichi si avvierà su:
 `http://localhost:8000`
e andiamo cercare la nostra risorsa:
`http://localhost:8000/lingue`

## Aggiungiamo altre risorse

Possiamo provare ad aggiungerge altre risorse. Aggiungiamo i nostri i hobbies
```
{
  "/lingue": {
    "get": {
      "lingue": [
        {
          "nome": "Italiano",
          "livello": "Ottimo"
        }
      ]
    }
  },
  "/hobbies": {
    "get": {
      "hobbies": [
        {
          "tipo": "Guardare Netflix"
        }
      ]
    }
  }
}
```

E andiamo a recuperarli su
`http://localhost:8000/hobbies`


## Per le piú temerarie

Possiamo riprenderemo il CV di paperina fatto durante l'incontro su Bulma e invece di scrivere, per esempio, le lingue che sa parlare Paperina direttamente nell'HTML, le andremo a recuperare dal nostro server.
Insomma, andremo a sostituire queste voci qua:

```
<h2>Competenze Linguistiche</h2>
  <ul>
    <li><h4>Inglese</h4></li>
    <p>Ottimo</p>
    <br>
    <li><h4>Spagnolo</h4></li>
    <p>Buono</p>
```

## Prepare le chiamate HTTP

### Bisogna aggiungere jQuery

Ora possiamo andare a riutilizzare il sito del CV di Paperina e possiamo andare a recuperare i dati che vogliamo.

Per poter chiamare i nostro server però dobbiamo scrivere le funzione che lo facciano, qui ci servirà un po' di `JavaScript`. Una libreria di JavaScript molto utile e pratica è quella di jQuery.
jQuery insieme a AJAX ci permette di scrivere semplici funzioni che vadano a recupere le informazioni che desideriamo tramite delle chiamate HTTP.

Per poter usare jQuery dobbiamo prima però includerlo nel nostro HTML. Tutte le risorse esterne vanno messe all'interno del tag `<head>`

```
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></scrip>
```


Ora dobbiamo effetivamente scrivere queste chiamate:

```
<script>
$(document).ready(function(){
  // funzione per inviare richieste HTTP (metodo GET) con AJAX ha 2 parametri:
  // url: l'indirizzo al quale inviare la chiamata con la risorsa
  // success: funzione da lanciare se la richiesta ha successo che, a sua volta,
  // accetta come parametri i dati restituiti dal server

  $.ajax({
    url: "http://localhost:8000/lingue",
    success: function(result){
      var testo = result.lingue[0].nome
      $("#inglese").html(testo)
  }});
});
</script>
```
Poi dobbiamo scrivere le chiamate che ci servono quindi nell'url inseriamo dove (localhost:25000) e cosa (lingue) andare a prendere la risorsa che effettua il lavoro.

Infine per renderizzare il nostro contenuto dobbiamo iniettare nell'HTML i nostri dati presi dal server:
```
<h2>Competenze Linguistiche</h2>
<ul>
  <li><h4 id="italiano"></h4></li>
  <li><h4 id="inglese"></h4></li>
</ul>
```

## La cassetta degli attrezzi che abbiamo usato:

    - ATOM
      editor che useremo per scrivere il nostro codice
        - HTML
          HyperText Markup Language è il linguaggio utilizzato per creare pagine web e altri tipi di documenti visualizzabili in un browser.
        - JavaScript è il linguaggio utilizzato per creare pagine web piú

    - Node
      è il motore per JavaScript
      |
      - npm
      |  Node Package Manager è la piú grande libreria di pacchetti di JavaScript
      |  |
      |  - mock-json-servers
      |    è un pacchetto di che permette di avviare dei server con dei file JSON
      |    |
      |    - sintassi JSON, Javascript Object notation, è un tipo di formato molto utilizzato per lo scambio dati in applicazioni-client server come API.
      |  
      - jQuery è libreria Javascript molto utilizzata per applicazioni web
        |
        - AJAX, ti permette di fare le chiamate HTTP

    - Terminale o prompt
      vi permette di avere in una finestra il computer senza interfaccia grafica, ovvero di interagire direttamente con esso attraverso i comandi. Ecco una breve guida introduttiva (https://tutorial.djangogirls.org/it/intro_to_command_line/)
    |
    - Per riuscire ad avvviare il nostro server
