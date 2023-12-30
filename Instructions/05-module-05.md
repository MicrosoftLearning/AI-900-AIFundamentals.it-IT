---
lab:
  title: Esplorare l'IA generativa con Copilot di Bing
---

In questo esercizio si esplorerà l'IA generativa con Copilot di Bing 

## Prima di iniziare
È necessario un account Microsoft personale. Se non si dispone di tale account, andare all'indirizzo [signup.live.com](https://signup.live.com/signup?azure-portal=true) e registrarsi.

# Esplorare l'IA generativa con Bing

1. Aprire [Bing.com](https://www.bing.com?azure-portal=true) e accedere con l'account Microsoft personale.

**Nota**: anche se è possibile accedere con l'account aziendale o dell'istituto di istruzione, si noterà un'esperienza utente leggermente diversa rispetto all'accesso con l'account personale. Usando l'account aziendale o dell'istituto di istruzione, verrà visualizzata la chat Bing Enterprise. 

1. Selezionare **Chat** nel menu nella parte superiore della schermata. Il pulsante Chat reindirizza a Copilot di Bing, che usa l'IA generativa per potenziare i risultati della ricerca. Ciò significa che, a differenza della sola ricerca, che restituisce contenuti esistenti, Copilot di Bing è in grado di creare nuove risposte basate sulla creazione di modelli di linguaggio naturale e sulle informazioni del web.  
    
1. Verso la parte inferiore della schermata comparirà la finestra **Chiedimi qualsiasi cosa**. Quando si inseriscono le richieste nella finestra, Copilot di Bing usa l'intero thread della conversazione per fornire le risposte. Ad esempio, proviamo a porre una serie di domande sul tema dei viaggi. 

## Usare le richieste per generare le risposte

1. Digitare una richiesta: `What are 3 pros and cons of traveling in the winter?`. Prima della risposta appariranno le voci *Ricerca in corso per:...* e *Generazione delle risposte per l'utente in corso...*. Il modello usa le risposte cercate come informazioni di base per generare risposte originali. Si noti che la fine della risposta contiene i collegamenti alle origini. 

![Uno screenshot della risposta di Copilot di Bing a una richiesta sull'argomento viaggi con tre punti per i pro e tre per i contro.](../media/generative-ai/bing-copilot-response-traveling.png) 

**Nota**: se non viene visualizzato un messaggio **Generazione delle risposte per l'utente in corso...* o una risposta a 	elenco puntato, non è stato ancora visualizzato Copilot di Bing in azione. È necessario tornare al menu di accesso e connettere l'account corrente in uso con un account personale. 
 
1. Digitare una richiesta: `Find me 3 more pros`. Ciò che si intende con questa richiesta è che si desidera vedere altri 3 motivi positivi per viaggiare in inverno che non siano già stati elencati. Si noti che con questa richiesta si chiede a Copilot di Bing di fare due cose che la ricerca da sola non fa: usare la risposta della chat precedente per escludere ciò che viene visualizzato nella nuova risposta e usare l'argomento della chat precedente senza dichiararlo esplicitamente. 

1. Digitare una richiesta: `Where are 3 places I can go to find fewer crowds?`. 

**Nota**: occorre notare che, sebbene Copilot di Bing sia in grado di fornire una risposta correlata, può inserire "ricordi" precedenti del thread della conversazione mentre si prosegue. Di conseguenza, le risposte ottenute potrebbero non essere direttamente correlate ai viaggi in inverno. Ciò è dovuto in gran parte alle limitazioni di input dei token. Quando la chat "ricorda" parti precedenti di una conversazione, è perché ha salvato una certa quantità di token dalla conversazione. Man mano che si introducono nuovi token tramite le nuove richieste e risposte, la chat lascia andare i token meno recenti. 

1. Il pulsante **Nuovo argomento** accanto alla finestra chat è utile a Copilot di Bing per cancellare il thread della conversazione precedente, in modo che le risposte al nuovo argomento non siano basate sull'argomento precedente. Usare l'icona **Nuovo argomento** in corrispondenza della finestra della chat per cancellare la cronologia dei messaggi. 

## Provare la generazione di immagini

1. Verrà ora illustrato un esempio di generazione di immagini. Digitare una richiesta: `Create an image of an elephant eating a hamburger`. Occorre notare che prima che Copilot di Bing restituisca una risposta appare il messaggio *Provo a creare l'immagine che hai richiesto*. 

![Uno screenshot di elefanti che mangiano hamburger](../media/generative-ai/dall-e-elephant.png)

È importante notare che la risposta può essere simile ma non uguale. Ciò è dovuto al fatto che le risposte sono diverse.  

1. Nella risposta c'è un testo in basso che recita "Con tecnologia DALL-E". Occorre considerare che DALL-E si basa su modelli linguistici di grandi dimensioni, mentre l'input in linguaggio naturale genera immagini. 

1. Tornare alla chat di Copilot di Bing facendo clic sull'icona di Microsoft Bing nell'angolo in alto a destra della schermata. 

## Provare la generazione di codice

1. Verrà ora illustrato un esempio di generazione e traduzione di codice. Digitare una richiesta: `Use Python to create a list`. 

1. Digitare la richiesta: `Translate that into C#`. Occorre notare che non è stato necessario specificare il soggetto nella seconda, poiché Copilot di Bing sa che si riferisce alla cronologia delle conversazioni. 

## Bonus 

1. Digitare una richiesta: `What are 3 examples of generative AI helping people?`. Potrebbe tornare utile come modello di brainstorming per le proprie idee relative a Copilot!  

