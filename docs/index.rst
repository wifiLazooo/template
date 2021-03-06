.. |br| raw:: html

   <br />
MyC4 Sezione Contest
========

La seguente documentazione riguarda la modalità di integrazione tra |br|
l'app MyCarrefour e la nuova sezione dedicata ai contest Carrefour.

La sezione contiene una index page in cui sono presenti in forma di elenco |br|
con preview, i contest attivi ed i contest che verranno attivati a breve.

Al click di ognuno dei contest attivi, si aprirà una pagina dedicata al contest cliccato, |br|
al quale, l'utente potrà partecipare, senza uscire dall'app MyCarrefour.

Funzionalità
--------

- Carousel gestibile da CMS
- Indice contest attivi e futuri, gestibile da CMS
- Dettaglio contest ottimizzato per la visualizzazione e la fruizione in app
- Metadati aggiuntivi per ogni contest, gestibili da CMS

Content Management System
------------

È possibile gestire l'elenco dei contest ed i loro metadati, |br|
accedendo con un utenza "admin" o "editor" al seguente link https://app.contentful.com/spaces/67w5ozj5347n/

Sono gestiti:

- Contest
- Slide del carousel

**Contest**
	Ogni contest possiede metadati direttamente estrapolati dalla sua versione web |br|
	con in aggiunta alcuni metadati dedicati al contest in-app

	* Data inizio e data di fine concorso
	* Testo di help
	* Cover image
	* Aspetto grafico
	* Sitemap interna

**Slide del carousel**
	Può essere gestita ogni slide del carousel, personalizzandone il contenuto, |br|
	immagine di sfondo e call to action (opzionale).

	In presenza di una sola slide il carousel sarà un componente fisso, senza possibilità di slide.


Integrazione con app myC4
------------

Il modulo è strutturato in maniera da integrarsi con l'app myCarrefour v4.* |br|
e ne condivide la tecnologia Cordova.

Per l'integrazione sarà sufficiente:

	* Includere lo script "myC4-contest.js" all'interno della index dell'app
	* Importare i file di progetto all'interno di una folder  |br|
	esposta dal webserver di cordova. Di default il modulo punta alla folder "/myC4-contest" che dovrà essere presente |br|
	(altrimenti è possibile configurarne una differente intervenendo sulla variabile "baseFolder" nel file "myC4-contest.js")
	* Includere il tag <my-c4-contest></my-c4-contest> all'interno della pagina dedicata ai contest
	* Inizializzare il modulo

**Inizializzazione del modulo**
	Per inizializzare il modulo, una volta eseguiti gli step di integrazione, si deve::

		var success = function(){
			// INITIALIZATION SUCCESS
		};

		var error = function(error){
			// INITIALIZATION ERROR
		};

		var requestLogin = function(error){
			// user not logged, request to login while in contest
			//Redirect to register page expected
		};

		var requestRegistration = function(error){
			// user not logged, request to register while in contest
			//Redirect to register page expected
		};

		MyC4Contests
			.init({
				isUserLogged: true, //or false
				userId: "xyz", //if isUserLogged is false this is emty
				onInit: success,  //called after initialization
				onError: error, //called if error with user
				onRequestLogin: requestLogin,
				onRequestRegistration: requestRegistration

			});

	La chiamata MyC4Contests.init deve essere effettuata quando <my-c4-contest></my-c4-contest> è presente nel dom |br|
	e viene effettuata ogni volta che l'utente apre la pagina contest dal menu dell'app (viene gestita una cache interna |br|
	per evitare di chiedere a SSO l utente piu volte)

	- isUserLogged è una variabile booleana che indica se l'utente è loggato
	- userId è una stringa che contiene l'id di interscambio per ottenere l utente dal servizio SSO
	- onInit riceve una funzione che viene chiamata non appena il modulo è inizializzato
	- onError riceve una funzione che viene chiamata in caso di errore (con l utente, errori di rete vengono gestiti dal modulo)
	- onRequestLogin riceve una funzione  che viene chiamata quando l'utente (non loggato) chiede dal contest di effettuare login 
	- onRequestRegistration  riceve una funzione  che viene chiamata quando l'utente (non loggato) chiede dal contest di effettuare registrazione


Integrazione stili e ui
------------

Il modulo carica dinamicamente il file con gli stili css presente nel path |br|
(è utilizzato un selettore che modifica solamente gli stili degli elementi interni al modulo).

Il modulo carica dinamicamente jquery per le modifiche al dom, solamente se non è gia presente.

sono richieste specifiche aggiuntive per l'integrazione UI (ambiente grafico ionic? jquery ui?)...

Cronologia revisioni
-------

Corrente v1.0

* v1.0


Autori
-------

* Gioele Meoni
