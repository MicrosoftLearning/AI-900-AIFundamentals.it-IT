---
lab:
  title: Esplorare i servizi di intelligenza artificiale di Azure
---

> **Importante**
> **Il lab Rilevamento anomalie è stato deprecato e sostituito dall'aggiornamento seguente.**

I servizi di intelligenza artificiale di Azure consentono agli utenti di creare applicazioni di intelligenza artificiale con API e modelli predefiniti e predefiniti e personalizzabili. In questo esercizio si esaminerà uno dei servizi, Azure AI Content Safety, in Content Safety Studio. 

Content Safety Studio consente di esplorare il modo in cui è possibile moderare il contenuto di testo e immagine. È possibile eseguire test su testo o immagini di esempio e ottenere un punteggio di gravità compreso tra sicuro e alto per ogni categoria. In questo esercizio di lab si creerà una risorsa a servizio singolo in Content Safety Studio e si testeranno le relative funzionalità. 

> **Nota** L'obiettivo di questo esercizio è ottenere un'idea generale del provisioning e dell'uso dei servizi di intelligenza artificiale di Azure. Content Safety viene usato come esempio, ma non si prevede di acquisire una conoscenza completa della sicurezza dei contenuti in questo esercizio.

## Esplorare Content Safety Studio 

![Screenshot della pagina di destinazione di Content Safety Studio.](./media/content-safety/content-safety-getting-started.png)


1. Aprire [Content Safety Studio](https://contentsafety.cognitive.azure.com?azure-portal=true). Se non si è connessi, sarà necessario eseguire l'accesso. Selezionare **Accedi** in alto a destra nella schermata. Usare l'indirizzo di posta elettronica e la password associati alla sottoscrizione di Azure per accedere. 

1. Content Safety Studio è configurato come molti altri studi per i servizi di intelligenza artificiale di Azure. Nel menu nella parte superiore della schermata fare clic sull'icona a sinistra *dell'intelligenza artificiale di Azure*. Verrà visualizzato un elenco a discesa di altri studi progettati per lo sviluppo con i servizi di intelligenza artificiale di Azure. È possibile fare di nuovo clic sull'icona per nascondere l'elenco.

![Screenshot del menu di Content Safety Studio con un interruttore aperto per passare ad altri studi.](./media/content-safety/studio-toggle-icon.png)  

## Associare una risorsa allo studio 

Prima di usare lo studio, è necessario associare una risorsa dei servizi di intelligenza artificiale di Azure allo studio. A seconda dello studio, è possibile che sia necessaria una risorsa a servizio singolo specifica o che sia possibile usare una risorsa multiservizio generale. Nel caso di Content Safety Studio, è possibile usare il servizio creando una risorsa *Content Safety* a servizio singolo o una risorsa generale per servizi di intelligenza artificiale di *Azure* . Nei passaggi seguenti verrà creata una risorsa Content Safety a servizio singolo. 

1. Nella parte superiore destra della schermata fare clic sull'icona **Impostazioni** . 

![Screenshot dell'icona delle impostazioni in alto a destra della schermata, accanto alla campana, al punto interrogativo e alle icone del sorriso.](./media/content-safety/settings-toggle.png)

1. Nella pagina **Impostazioni** verrà visualizzata una scheda *Directory* e *una scheda Risorsa* . Nella scheda *Risorsa* selezionare **Crea una nuova risorsa**. Verrà visualizzata la pagina per creare una risorsa nel portale di Azure.

> **Nota** La scheda *Directory* consente agli utenti di selezionare directory diverse da cui creare le risorse. Non è necessario modificare le impostazioni a meno che non si voglia usare una directory diversa. 

![Screenshot della posizione in cui selezionare crea una nuova risorsa dalla pagina delle impostazioni di Content Safety Studio.](./media/content-safety/create-new-resource-from-studio.png)

1. Nella pagina *Crea sicurezza contenuto* nel portale di [Azure](https://portal.azure.com?auzre-portal=true) è necessario configurare diversi dettagli per creare la risorsa. Configurarlo con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: F0 Gratuito

1. Selezionare **Rivedi e crea** ed esaminare la configurazione. Selezionare quindi **Crea**. La schermata indicherà al termine della distribuzione. 

*Congratulazioni! È stata appena creata, o ne è stato effettuato il provisioning, una risorsa dei servizi di intelligenza artificiale di Azure. Quello di cui è stato effettuato il provisioning in particolare è una risorsa del servizio Content Safety a servizio singolo.*

1. Al termine della distribuzione, aprire una nuova scheda e tornare a [Content Safety Studio](https://contentsafety.cognitive.azure.com?azure-portal=true). 

1. Selezionare di nuovo l'icona **Impostazioni** in alto a destra della schermata. Questa volta si noterà che la risorsa appena creata è stata aggiunta all'elenco.  

1. Nella pagina Impostazioni di Content Safety Studio selezionare la risorsa del servizio Intelligenza artificiale di Azure appena creata e fare clic su **Usa risorsa** nella parte inferiore della schermata. Si tornerà alla home page di Studio. È ora possibile iniziare a usare lo studio con la risorsa appena creata.

## Provare la moderazione del testo in Content Safety Studio

1. Nella home page di Content Safety Studio, in *Esegui test di moderazione*, passare alla casella **Contenuto di testo Moderato** e fare clic su **Prova**.
1. In Eseguire un semplice test fare clic su **Contenuto sicuro**. Si noti che il testo viene visualizzato nella casella seguente. 
1. Fare clic su **Run test**(Esegui test). L'esecuzione di un test chiama il modello di Deep Learning di Content Safety Service. Il modello di Deep Learning è già stato sottoposto a training per riconoscere contenuti non sicuri.
1. Nel pannello *Risultati* esaminare i risultati. Esistono quattro livelli di gravità da sicuri ad alto e quattro tipi di contenuto dannoso. Il servizio Content Safety AI considera l'esempio accettabile o meno? È importante notare che i risultati sono entro un intervallo di confidenza. Un modello con training ottimale, ad esempio uno dei modelli predefiniti di Intelligenza artificiale di Azure, può restituire risultati con una probabilità elevata di corrispondenza di ciò che un essere umano etichetta il risultato. Ogni volta che si esegue un test, chiamare di nuovo il modello. 
1. Provare ora un altro esempio. Selezionare il testo in Contenuto violento con errori di ortografia. Controllare che il contenuto sia visualizzato nella casella seguente.
1. Fare clic su **Esegui test** ed esaminare di nuovo i risultati nel pannello Risultati. 

È possibile eseguire test su tutti gli esempi forniti, quindi esaminare i risultati.

## Controllare le chiavi e l'endpoint

Queste funzionalità testate possono essere programmate in tutti i tipi di applicazioni. Le chiavi e l'endpoint usati per lo sviluppo di applicazioni sono disponibili sia in Content Safety Studio che nel portale di Azure. 

1. In Content Safety Studio tornare alla pagina **Impostazioni** , con la scheda *Risorse* selezionata. Cercare la risorsa usata. Scorrere per visualizzare l'endpoint e la chiave per la risorsa. 
1. Nel portale di Azure si noterà che si tratta dello *stesso* endpoint e *delle chiavi diverse* per la risorsa. Per verificarlo, passare al portale di [Azure](https://portal.azure.com?auzre-portal=true). Cercare *Content Safety* nella barra di ricerca superiore. Trovare la risorsa e fare clic su di essa. Nel menu a sinistra cercare *Chiavi ed endpoint* in *Gestione risorse*. Selezionare **Chiavi ed endpoint** per visualizzare l'endpoint e le chiavi per la risorsa. 

Al termine, è possibile eliminare la risorsa Content Safety dal portale di Azure. L'eliminazione della risorsa è un modo per ridurre i costi accumulati quando la risorsa esiste nella sottoscrizione. A tale scopo, passare alla pagina **Panoramica** della risorsa Content Safety. Selezionare **Elimina** nella parte superiore della schermata. 
