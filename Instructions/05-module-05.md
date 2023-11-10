---
lab:
  title: Esplorare l'intelligenza artificiale generativa con Bing Copilot
---

In questo esercizio si esaminerà l'intelligenza artificiale generativa con Bing Copilot. 

## Prima di iniziare
È necessario un account Microsoft personale. Se non ne hai uno, vai a [signup.live.com](https://signup.live.com/signup?azure-portal=true) per iscriverti.

# Esplorare l'intelligenza artificiale generativa con Bing

1. Aprire [Bing.com](https://www.bing.com?azure-portal=true) e accedere con l'account Microsoft personale.

**Nota**: anche se è possibile accedere con l'account aziendale o dell'istituto di istruzione, si noterà un'esperienza utente leggermente diversa rispetto all'accesso con l'account personale. Usando l'account aziendale o dell'istituto di istruzione, verrà visualizzata la chat Bing Enterprise. 

1. Selezionare **Chat** dal menu nella parte superiore della schermata. Chat offre a Bing Copilot, che usa l'intelligenza artificiale generativa per potenziare i risultati della ricerca. Ciò significa che a differenza della sola ricerca, che restituisce contenuto esistente, Bing Copilot può mettere insieme nuove risposte in base alla modellazione del linguaggio naturale e alle informazioni del Web.  
    
1. Verso la parte inferiore dello schermo, vedrai una finestra **Chiedimi qualcosa**. Quando si immettono richieste nella finestra, Bing Copilot usa l'intero thread di conversazione per restituire le risposte. Ad esempio, proviamo a porre una serie di domande sul viaggio. 

## Usare le richieste per generare risposte

1. Digitare un prompt: `What are 3 pros and cons of traveling in the winter?`. Prima della risposta verrà visualizzata una *ricerca:...* e *Generazione.* Il modello usa le risposte cercate come informazioni di base per generare risposte originali. Si noti che la fine della risposta contiene collegamenti alle relative origini. 

![Screenshot della risposta del copilota Bing a una richiesta di viaggio con tre punti elenco per professionisti e tre punti elenco per contro.](../media/generative-ai/bing-copilot-response-traveling.png) 

**Nota**: se non viene visualizzato un messaggio **Generazione...* o una risposta elenco puntato, non è stato ancora visualizzato Bing Copilot in azione. È necessario tornare al menu di accesso e connettere l'account corrente in uso con un account personale. 
 
1. Digitare un prompt: `Find me 3 more pros`. Ciò che intendi con questa richiesta è che vuoi vedere 3 motivi più positivi per viaggiare in inverno che non sono già stati elencati. Si noti che con questo prompt si chiede a Bing Copilot di eseguire due operazioni che la ricerca da sola non esegue: usare la risposta di chat precedente per escludere ciò che viene restituito nella nuova risposta e usare l'argomento della chat precedente senza specificarlo in modo esplicito. 

1. Digitare un prompt: `Where are 3 places I can go to find fewer crowds?`. 

**Nota: si noti** che, mentre Bing Copilot è in grado di fornire una risposta correlata, può eliminare "memorie" precedenti del thread di conversazione mentre continua. Di conseguenza, le risposte che si ottengono potrebbero non essere direttamente correlate a viaggiare in inverno. Ciò è in gran parte dovuto alle limitazioni di input del token. Quando la chat "ricorda" parti precedenti di una conversazione, è perché ha salvato una certa quantità di token dalla conversazione. Man mano che vengono introdotti nuovi token tramite le nuove richieste e le risposte, la chat lascerà passare i token meno recenti. 

1. Il **pulsante Nuovo argomento** accanto alla finestra della chat è utile di Bing Copilot per cancellare il thread di conversazione precedente, in modo che le risposte ai nuovi argomenti non siano basate sull'argomento precedente. Usare l'icona **Nuovo argomento** accanto alla finestra della chat per cancellare la cronologia dei messaggi. 

## Provare la generazione di immagini

1. Verrà ora illustrato un esempio di generazione di immagini. Digitare un prompt: `Create an image of an elephant eating a hamburger`. Si noti che un messaggio *che tenterò di creare viene* visualizzato prima che Bing Copilot restituisca una risposta. 

![Screenshot degli elefanti che mangiano hamgburger.](../media/generative-ai/dall-e-elephant.png)

Importante notare che la risposta può essere simile ma non la stessa. Ciò è dovuto al fatto che le risposte sono diverse.  

1. Nella risposta c'è testo nella parte inferiore che legge "Powered by DALL-E". Si consideri il modo in cui DALL-E si basa su modelli linguistici di grandi dimensioni quando l'input del linguaggio naturale genera immagini. 

1. Tornare alla chat di Bing Copilot facendo clic sull'icona Di Microsoft Bing nell'angolo in alto a destra della schermata. 

## Provare la generazione di codice

1. Verrà ora illustrato un esempio di generazione e traduzione del codice. Digitare un prompt: `Use Python to create a list`. 

1. Digitare nel prompt: `Translate that into C#`. Si noti che non è stato necessario specificare il "che" è come Bing Copilot sa fare riferimento alla cronologia delle conversazioni. 

## Bonus 

1. Digitare un prompt: `What are 3 examples of generative AI helping people?`. Puoi usarlo come un modo per brainstormare le tue idee copilote!  

