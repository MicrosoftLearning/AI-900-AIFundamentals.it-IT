---
lab:
  title: Esplorare i servizi di intelligenza artificiale di Azure
---

> **Importante**
> **Il lab Rilevamento anomalie è stato deprecato e sostituito dall'aggiornamento seguente.**

I servizi di intelligenza artificiale di Azure consentono agli utenti di creare applicazioni di intelligenza artificiale con API e modelli predefiniti e personalizzabili. In questo esercizio si esaminerà uno dei servizi Content Cassaforte ty di Intelligenza artificiale di Azure in Content Cassaforte ty Studio. 

Content Cassaforte ty Studio consente di esplorare il modo in cui è possibile moderare il contenuto di testo e immagine. È possibile eseguire test su testo o immagini di esempio e ottenere un punteggio di gravità compreso tra sicuro e alto per ogni categoria. In questo esercizio di lab verrà creata una risorsa a servizio singolo in Content Cassaforte ty Studio e ne verranno testate le funzionalità. 

> **Nota** L'obiettivo di questo esercizio è ottenere un'idea generale del provisioning e dell'uso dei servizi di intelligenza artificiale di Azure. Il contenuto Cassaforte ty viene usato come esempio, ma non si prevede di acquisire una conoscenza completa della sicurezza dei contenuti in questo esercizio.

## Esplorare Content Cassaforte ty Studio 

![Screenshot della pagina di destinazione di Content Safety Studio.](./media/content-safety/content-safety-getting-started.png)


1. Aprire Content [Cassaforte ty Studio](https://contentsafety.cognitive.azure.com?azure-portal=true). Se non si è connessi, sarà necessario eseguire l'accesso. Selezionare **Accedi** in alto a destra nella schermata. Usare il messaggio di posta elettronica e la password associati alla sottoscrizione di Azure per accedere. 

1. Content Cassaforte ty Studio è configurato come molti altri studi per i servizi di intelligenza artificiale di Azure. Nel menu nella parte superiore della schermata fare clic sull'icona a sinistra dell'intelligenza artificiale* di *Azure. Verrà visualizzato un elenco a discesa di altri studi progettati per lo sviluppo con i servizi di intelligenza artificiale di Azure. È possibile fare di nuovo clic sull'icona per nascondere l'elenco.

![Screenshot del menu di Content Cassaforte ty Studio con un interruttore selezionato aperto per passare ad altri studi.](./media/content-safety/studio-toggle-icon.png)  

## Associare una risorsa allo studio 

Prima di usare lo studio, è necessario associare una risorsa dei servizi di intelligenza artificiale di Azure allo studio. A seconda dello studio, potrebbe essere necessaria una risorsa a servizio singolo specifica o può usare una risorsa multiservizio generale. Nel caso di Content Cassaforte ty Studio, è possibile usare il servizio creando una risorsa content Cassaforte ty a servizio *singolo o *una risorsa generale per servizi* di intelligenza artificiale di* Azure. Nei passaggi seguenti verrà creata una risorsa content Cassaforte ty a servizio singolo. 

1. Nella parte superiore destra della schermata fare clic sull'icona **Impostazioni**. 

![Screenshot dell'icona delle impostazioni in alto a destra dello schermo, accanto alle icone a campana, punto interrogativo e sorriso.](./media/content-safety/settings-toggle.png)

1. **Nella pagina Impostazioni** verrà visualizzata una scheda Directory* e *una *scheda Risorsa*. Nella *scheda Risorsa* selezionare **Crea una nuova risorsa**. Verrà visualizzata la pagina per creare una risorsa nel portale di Azure.

> **Nota La** *scheda Directory* consente agli utenti di selezionare directory diverse da cui creare risorse. Non è necessario modificarne le impostazioni, a meno che non si desideri usare una directory diversa. 

![Screenshot della posizione in cui selezionare crea una nuova risorsa nella pagina impostazioni di Content Cassaforte ty Studio.](./media/content-safety/create-new-resource-from-studio.png)

1. Nella *pagina Crea contenuto Cassaforte ty* nel [portale](https://portal.azure.com?auzre-portal=true) di Azure è necessario configurare diversi dettagli per creare la risorsa. Configurarlo con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: F0 gratuito

1. Selezionare **Rivedi e crea** ed esaminare la configurazione. Selezionare quindi **Crea**. La schermata indicherà quando la distribuzione è stata completata. 

*Congratulazioni! È stata appena creata, o ne è stato effettuato il provisioning, una risorsa dei servizi di intelligenza artificiale di Azure. Quello di cui è stato effettuato il provisioning in particolare è una risorsa del servizio content Cassaforte ty a servizio singolo.*

1. Al termine della distribuzione, aprire una nuova scheda e tornare a [Content Cassaforte ty Studio](https://contentsafety.cognitive.azure.com?azure-portal=true). 

1. Selezionare di nuovo l'icona **Impostazioni** in alto a destra dello schermo. Questa volta si noterà che la risorsa appena creata è stata aggiunta all'elenco.  

1. Nella pagina Impostazioni content Cassaforte ty Studio selezionare la risorsa del servizio Azure per intelligenza artificiale appena creata e fare clic su **Usa risorsa nella parte inferiore della schermata**. Si tornerà alla home page dello studio. A questo punto è possibile iniziare a usare lo studio con la risorsa appena creata.

## Provare la moderazione del testo in Content Cassaforte ty Studio

1. Nella home page content Cassaforte ty Studio, in *Esegui test* di moderazione passare alla **casella Contenuto moderato** e fare clic su **Prova**.
1. In Eseguire un test semplice fare clic su **Cassaforte Contenuto**. Si noti che il testo viene visualizzato nella casella seguente. 
1. Fare clic su **Run test**(Esegui test). L'esecuzione di un test chiama il modello di Deep Learning di Content Cassaforte ty Service. Il modello di Deep Learning è già stato sottoposto a training per riconoscere contenuti non sicuri.
1. *Nel pannello Risultati* esaminare i risultati. Esistono quattro livelli di gravità da sicuri ad alto e quattro tipi di contenuto dannoso. Il servizio content Cassaforte ty per intelligenza artificiale considera questo esempio accettabile o meno? È importante notare che i risultati si trovano entro un intervallo di confidenza. Un modello con training ottimale, ad esempio uno dei modelli predefiniti di Intelligenza artificiale di Azure, può restituire risultati con una probabilità elevata di corrispondenza di ciò che un essere umano etichetta il risultato. Ogni volta che si esegue un test, chiamare di nuovo il modello. 
1. Provare ora un altro esempio. Selezionare il testo in Contenuto violento con errori di ortografia. Verificare che il contenuto sia visualizzato nella casella seguente.
1. Fare clic su **Esegui test** ed esaminare di nuovo i risultati nel pannello Risultati. 

È possibile eseguire test su tutti gli esempi forniti, quindi esaminare i risultati.

## Vedere le chiavi e l'endpoint

Queste funzionalità testate possono essere programmate in tutti i tipi di applicazioni. Le chiavi e l'endpoint usati per lo sviluppo di applicazioni sono disponibili sia in Content Cassaforte ty Studio che nel portale di Azure. 

1. In Content Cassaforte ty Studio tornare alla **pagina Impostazioni**, con la *scheda Risorse* selezionata. Cercare la risorsa usata. Scorrere per visualizzare l'endpoint e la chiave per la risorsa. 
1. Nel portale di Azure si noterà che si tratta dello *stesso endpoint e *delle chiavi diverse* per* la risorsa. Per verificarlo, passare al [portale](https://portal.azure.com?auzre-portal=true) di Azure. *Cercare Content Cassaforte ty* sulla barra di ricerca superiore. Trovare la risorsa e fare clic su di essa. Nel menu a sinistra cercare Chiavi ed endpoint* in *Gestione* *risorse. Selezionare Chiavi ed endpoint** per visualizzare **l'endpoint e le chiavi per la risorsa. 

Al termine, è possibile eliminare la risorsa Content Cassaforte ty dal portale di Azure. L'eliminazione della risorsa è un modo per ridurre i costi che si accumulano quando la risorsa esiste nella sottoscrizione. A tale scopo, passare alla **pagina Panoramica** della risorsa Content Cassaforte ty. Selezionare **Elimina** nella parte superiore della schermata. 
