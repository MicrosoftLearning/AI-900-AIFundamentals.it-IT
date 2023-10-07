---
lab:
  title: Esplorare Content Safety Studio
---

I servizi di intelligenza artificiale di Azure consentono agli utenti di creare applicazioni di intelligenza artificiale con API e modelli predefiniti e predefiniti e personalizzabili. In questo esercizio si esaminerà uno dei servizi, Azure AI Content Safety, in Content Safety Studio. 

Content Safety Studio consente di esplorare il modo in cui è possibile moderare il testo e il contenuto dell'immagine. È possibile eseguire test su testo di esempio o immagini e ottenere un punteggio di gravità compreso tra sicurezza e alto per ogni categoria. In questo esercizio del lab verrà creata una risorsa a servizio singolo in Content Safety Studio e testarne le funzionalità. 

> **Nota** L'obiettivo di questo esercizio è quello di ottenere un senso generale del provisioning e dell'uso dei servizi di intelligenza artificiale di Azure. La sicurezza dei contenuti viene usata come esempio, ma non si prevede di acquisire una conoscenza completa della sicurezza dei contenuti in questo esercizio!

## Spostarsi in Content Safety Studio 

![Screenshot della pagina di destinazione di Content Safety Studio.](./media/content-safety/content-safety-getting-started.png)


1. Aprire [Content Safety Studio](https://contentsafety.cognitive.azure.com?azure-portal=true). Se non si è connessi, sarà necessario accedere. Selezionare **Accedi** nella parte superiore destra della schermata. Usare la posta elettronica e la password associata alla sottoscrizione di Azure per accedere. 

1. Content Safety Studio è configurato come molti altri studi per i servizi di intelligenza artificiale di Azure. Nel menu nella parte superiore della schermata fare clic sull'icona a sinistra *dell'intelligenza artificiale di Azure*. Verrà visualizzato un elenco a discesa di altri studi progettati per lo sviluppo con i servizi di intelligenza artificiale di Azure. È possibile fare clic di nuovo sull'icona per nascondere l'elenco.

![Screenshot del menu di Content Safety Studio con un interruttore aperto per passare ad altri studi.](./media/content-safety/studio-toggle-icon.png)  

## Associare una risorsa allo studio 

Prima di usare lo studio, è necessario associare una risorsa di servizi di intelligenza artificiale di Azure allo studio. A seconda dello studio, potrebbe essere necessario un'unica risorsa a servizio singolo o usare una risorsa multiservizio generale. Nel caso di Content Safety Studio, è possibile usare il servizio creando una risorsa *sicurezza contenuto* a servizio singolo o servizi di *Intelligenza artificiale di Azure* generico multiservizio. Nei passaggi seguenti verrà creata una risorsa sicurezza contenuto a servizio singolo. 

1. Nella parte superiore destra della schermata fare clic sull'icona **Impostazioni** . 

![Screenshot dell'icona delle impostazioni nella parte superiore destra dello schermo, accanto alla campana, al punto interrogativo e alle icone del sorriso.](./media/content-safety/settings-toggle.png)

1. Nella pagina **Impostazioni** verrà visualizzata una scheda *Directory* e *una scheda Risorsa* . Nella scheda *Risorsa* selezionare **Crea una nuova risorsa**. In questo modo si passa alla pagina per creare una risorsa nel portale di Azure.

> **Nota** La scheda *Directory* consente agli utenti di selezionare directory diverse da cui creare risorse. Non è necessario modificare le impostazioni a meno che non si voglia usare una directory diversa. 

![Screenshot della posizione in cui selezionare creare una nuova risorsa dalla pagina impostazioni di Content Safety Studio.](./media/content-safety/create-new-resource-from-studio.png)

1. Nella pagina *Crea sicurezza contenuto* nel portale di [Azure](https://portal.azure.com?auzre-portal=true) è necessario configurare diversi dettagli per creare la risorsa. Configurarla con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: F0 Gratuito

1. Selezionare **Rivedi e crea** e rivedere la configurazione. Quindi selezionare **Crea**. La schermata indicherà al termine della distribuzione. 

*Congratulazioni! È stata appena creata o effettuato il provisioning di una risorsa dei servizi di intelligenza artificiale di Azure. Quello effettuato in particolare è una risorsa di sicurezza del contenuto a servizio singolo.*

1. Al termine della distribuzione, aprire una nuova scheda e tornare a [Content Safety Studio](https://contentsafety.cognitive.azure.com?azure-portal=true). 

1. Selezionare di nuovo l'icona **Impostazioni** nella parte superiore destra della schermata. Questa volta si noterà che la risorsa appena creata è stata aggiunta all'elenco.  

1. Nella pagina Impostazioni di Content Safety Studio selezionare la risorsa del servizio Intelligenza artificiale di Azure appena creata e fare clic su **Usa risorsa** nella parte inferiore della schermata. Si tornerà alla home page dello studio. È ora possibile iniziare a usare lo studio con la risorsa appena creata.

## Provare la moderazione del testo in Content Safety Studio

1. Nella home page di Content Safety Studio, in *Esegui test di moderazione* passare alla casella Di **testo Moderata** e fare clic su **Prova.**
1. In Eseguire un semplice test fare clic su **Contenuto sicuro**. Si noti che il testo viene visualizzato nella casella seguente. 
1. Fare clic su **Run test**(Esegui test). L'esecuzione di un test chiama il modello di deep learning del Servizio sicurezza contenuto. Il modello di Deep Learning è già stato sottoposto a training per riconoscere il contenuto non sicuro.
1. Nel pannello *Risultati* esaminare i risultati. Esistono quattro livelli di gravità da sicuri ad alto e quattro tipi di contenuto dannoso. Il servizio Content Safety AI considera l'accettabile o meno questo esempio? Ciò che è importante notare è che i risultati si trovano all'interno di un intervallo di attendibilità. Un modello ben sottoposto a training, ad esempio uno dei modelli predefiniti dell'intelligenza artificiale di Azure, può restituire risultati che hanno una probabilità elevata di corrispondere a ciò che un uomo etichetta il risultato. Ogni volta che si esegue un test, si chiama di nuovo il modello. 
1. Provare un altro esempio. Selezionare il testo in Contenuto violento con errori di ortografia. Verificare che il contenuto sia visualizzato nella casella seguente.
1. Fare clic su **Esegui test** e esaminare di nuovo i risultati nel pannello Risultati. 

È possibile eseguire test su tutti gli esempi forniti, quindi esaminare i risultati.

## Consultare le chiavi e l'endpoint

Queste funzionalità testate possono essere programmate in tutti i tipi di applicazioni. Le chiavi e l'endpoint usati per lo sviluppo di applicazioni sono disponibili sia in Content Safety Studio che nel portale di Azure. 

1. In Content Safety Studio tornare alla pagina **Impostazioni** , con la scheda *Risorse* selezionata. Cercare la risorsa usata. Scorrere verso l'interno per visualizzare l'endpoint e la chiave per la risorsa. 
1. Nel portale di Azure si noterà che questi sono gli *stessi* endpoint e chiavi *diverse* per la risorsa. Per estrarlo, passare al [portale di Azure](https://portal.azure.com?auzre-portal=true). Cercare *Content Safety* nella barra di ricerca superiore. Trovare la risorsa e fare clic su di esso. Nel menu a sinistra cercare *Gestione risorse* per *chiavi ed endpoint*. Selezionare **Chiavi ed endpoint** per visualizzare l'endpoint e le chiavi per la risorsa. 

Al termine, è possibile eliminare la risorsa Sicurezza contenuto dal portale di Azure. L'eliminazione della risorsa è un modo per ridurre i costi che si accumulano quando la risorsa esiste nella sottoscrizione. A tale scopo, passare alla pagina **Panoramica** della risorsa Sicurezza contenuto. Selezionare **Elimina** nella parte superiore della schermata. 
