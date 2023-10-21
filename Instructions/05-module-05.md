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

1. Selezionare **Chat** dal menu nella parte superiore della schermata. Chat ti porta a Bing Copilot, che usa l'intelligenza artificiale generativa per attivare i risultati della ricerca. Ciò significa che a differenza della ricerca da sola, che restituisce contenuto esistente, Bing Copilot può mettere insieme nuove risposte in base alla modellazione del linguaggio naturale e alle informazioni del Web.  
    
1. Verso la parte inferiore dello schermo, vedrai una finestra **Chiedimi qualsiasi cosa**. Quando si immettono le richieste nella finestra, Bing Copilot usa l'intero thread di conversazione per restituire le risposte. Ad esempio, proviamo a porre una serie di domande sui viaggi. 

## Usare le richieste per generare risposte

1. Digitare un prompt: `What are 3 pros and cons of traveling in the winter?`. Verrà visualizzata una *ricerca:...* e *Generazione...* prima della risposta. Il modello usa la ricerca di risposte come informazioni di base per generare risposte originali. Si noti che la fine della risposta contiene collegamenti alle relative origini. 

![Screenshot della risposta di Bing copilot a una richiesta di viaggio con tre puntini per professionisti e tre puntati per cons.](../media/generative-ai/bing-copilot-response-traveling.png) 

**Nota**: se non viene visualizzato un messaggio **Generazione...* o una risposta elenco puntato, non è ancora stato visualizzato Bing Copilot in azione. È necessario tornare al menu di accesso e connettere l'account corrente in uso con un account personale. 
 
1. Digitare un prompt: `Find me 3 more pros`. Ciò che intendi con questo prompt è che vuoi vedere 3 motivi più positivi per viaggiare in inverno che non sono già stati elencati. Si noti che con questa richiesta si chiede a Bing Copilot di eseguire due operazioni che la ricerca da sola non fa: usare la risposta di chat precedente per escludere ciò che viene restituito nella nuova risposta e usare l'argomento della chat precedente senza indicarlo in modo esplicito. 

1. Digitare un prompt: `Where are 3 places I can go to find fewer crowds?`. 

**Nota**: si noti che, mentre Bing Copilot è in grado di dare una risposta correlata, può eliminare i "ricordi" precedenti del thread di conversazione man mano che continua. Di conseguenza, le risposte che si ottengono potrebbero non essere direttamente correlate al viaggio in inverno. Ciò è in gran parte dovuto alle limitazioni di input del token. Quando chat "ricorda" le parti precedenti di una conversazione, è perché ha salvato una certa quantità di token dalla conversazione. Man mano che vengono introdotti nuovi token tramite le nuove richieste e le risposte, la chat farà passare i token meno recenti. 

1. Il pulsante **Nuovo argomento** accanto alla finestra di chat è utile Bing Copilot per cancellare il thread di conversazione precedente in modo che le risposte ai nuovi argomenti non siano basate sull'argomento precedente. Usare l'icona **Nuovo argomento** accanto alla finestra della chat per cancellare la cronologia dei messaggi. 

## Provare la generazione di immagini

1. Vediamo ora un esempio di generazione di immagini. Digitare un prompt: `Create an image of an elephant eating a hamburger`. Si noti che un messaggio *tenterò di crearlo...* viene visualizzato prima che Bing Copilot restituisca una risposta. 

![Screenshot degli elefanti che mangiano hamgburger.](../media/generative-ai/dall-e-elephant.png)

Importante, si noti che la risposta può essere simile ma non uguale. Ciò è dovuto al fatto che le risposte sono diverse.  

1. Nella risposta c'è testo nella parte inferiore che legge "Powered by DALL-E". Si consideri il modo in cui DALL-E si basa su modelli di linguaggio di grandi dimensioni quando l'input del linguaggio naturale genera immagini. 

1. Tornare alla chat di Bing Copilot facendo clic sull'icona Microsoft Bing nell'angolo superiore destro della schermata. 

## Provare la generazione di codice

1. Verrà ora illustrato un esempio di generazione e traduzione del codice. Digitare un prompt: `Use Python to create a list`. 

1. Digitare nella richiesta: `Translate that into C#`. Si noti come non è necessario specificare cosa "che" è come Bing Copilot sa fare riferimento alla cronologia della conversazione. 

## Bonus 

1. Digitare un prompt: `What are 3 examples of generative AI helping people?`. È possibile usare questo come modo per brainstormare le proprie idee copilote!  

