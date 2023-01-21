---
lab:
  title: Esplorare le funzionalità di traduzione
---

# <a name="explore-translation"></a>Esplorare le funzionalità di traduzione

> **Nota** Per completare questo lab, è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

Una delle forze trainanti per sviluppo della civiltà è stata la capacità degli uomini di comunicare tra loro. Nella maggior parte delle attività umane, la comunicazione è fondamentale.

L'intelligenza artificiale (IA) può semplificare la comunicazione traducendo testo o voce tra lingue diverse e contribuendo così ad abbattere le barriere alla comunicazione tra paesi e culture.

Per testare le funzionalità del servizio Traduttore, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell. Gli stessi principi e funzionalità sono applicabili a soluzioni reali, ad esempio siti Web o app per smartphone.

## <a name="create-a-cognitive-services-resource"></a>Creare una risorsa per *Servizi cognitivi*

È possibile usare il servizio Traduttore creando una risorsa **Traduttore** o una risorsa **Servizi cognitivi**.

Se non è già stato fatto, creare una risorsa **Servizi cognitivi** nella sottoscrizione di Azure.

1. In un'altra scheda del browser aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Selezionare il pulsante **&#65291;Crea una risorsa**, cercare *Servizi cognitivi* e creare una risorsa di **Servizi cognitivi** con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: Standard S0
    - **Selezionando questa casella, confermo di aver letto e compreso tutte le condizioni seguenti**: selezionata.

1. Esaminare e creare la risorsa e attendere il completamento della distribuzione. Passare quindi alla risorsa distribuita.

1. Visualizzare la pagina **Chiavi ed endpoint** per la risorsa Servizi cognitivi. Sarà necessario specificare le chiavi e la posizione per connettersi dalle applicazioni client.

### <a name="get-the-key-and-location-for-your-cognitive-services-resource"></a>Ottenere la chiave e la posizione per la risorsa Servizi cognitivi

1. Attendere il completamento della distribuzione. Passare quindi alla risorsa Servizi cognitivi e nella pagina **Panoramica** selezionare il collegamento per gestire le chiavi per il servizio. Le chiavi e la posizione saranno necessarie per connettersi alla risorsa Servizi cognitivi dalle applicazioni client.

1. Visualizzare la pagina **Chiavi ed endpoint** per la risorsa. Saranno necessarie la **posizione/area** e la **chiave** per la connessione dalle applicazioni client.

> **Nota** Per usare il servizio Traduttore non è necessario usare l'endpoint di Servizi cognitivi. Viene fornito un endpoint globale solo per il servizio Traduttore. 

## <a name="run-cloud-shell"></a>Eseguire Cloud Shell

Per testare le funzionalità del servizio Traduttore, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell in Azure. 

1. Nel portale di Azure selezionare il pulsante **[>_]** (*Cloud Shell*) nella parte superiore della pagina a destra della casella di ricerca. Verrà aperto un riquadro di Cloud Shell nella parte inferiore del portale.

    ![Avviare Cloud Shell facendo clic sull'icona a destra della casella di ricerca in alto](media/translate-text-and-speech/powershell-portal-guide-1.png)

1. La prima volta che si apre Cloud Shell, è possibile che venga chiesto di scegliere il tipo di shell da usare (*Bash* o *PowerShell*). Selezionare **PowerShell**. Se questa opzione non viene visualizzata, ignorare il passaggio.  

1. Se viene chiesto di creare una risorsa di archiviazione per Cloud Shell, assicurarsi che sia specificata la sottoscrizione corretta e selezionare **Crea risorsa di archiviazione**. Attendere circa un minuto che la risorsa di archiviazione venga creata.

    ![Creare l'archiviazione facendo clic su Conferma.](media/translate-text-and-speech/powershell-portal-guide-2.png)

1. Verificare che nella parte superiore sinistra del riquadro Cloud Shell sia impostato *PowerShell* come tipo di shell. Se è *Bash*, passare a *PowerShell* usando il menu a discesa. 

    ![Come trovare il menu a discesa a sinistra per passare a PowerShell](media/translate-text-and-speech/powershell-portal-guide-3.png) 

1. Attendere l'avvio di PowerShell. Nel portale di Azure verrà visualizzata la schermata seguente:  

    ![Attendere l'avvio di PowerShell.](media/translate-text-and-speech/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>Configurare ed eseguire un'applicazione client

Ora che si dispone di un modello personalizzato, è possibile eseguire una semplice applicazione client che usa il servizio di traduzione.

1. Nella shell dei comandi immettere il comando seguente per scaricare l'applicazione di esempio e salvarla in una cartella denominata ai-900.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**Suggerimento** Se questo comando è già stato usato in un altro lab per clonare il repository *ai-900*, è possibile ignorare questo passaggio.

1. I file vengono scaricati in una cartella denominata **ai-900**. Ora si vogliono visualizzare tutti i file disponibili nella risorsa di archiviazione di Cloud Shell e usarli. Digitare il comando seguente nella shell: 

     ```PowerShell
    code .
    ```

    Verrà aperto un editor come quello illustrato nell'immagine seguente: 

    ![Editor di codice.](media/translate-text-and-speech/powershell-portal-guide-4.png)

1. Nel riquadro **File** a sinistra espandere **ai-900** e selezionare **translator.ps1**. Questo file contiene codice che usa il servizio Traduttore:

    ![Editor contenente il codice per l'uso del servizio Traduttore](media/translate-text-and-speech/translate-code.png)

1. Non preoccuparsi troppo dei dettagli del codice, l'aspetto importante è che sono necessari l'area/posizione e una delle chiavi per la risorsa Servizi cognitivi. Copiare questi valori dalla pagina **Chiavi ed endpoint** per la risorsa dal portale di Azure e incollarli nell'editor di codice, sostituendo rispettivamente i valori segnaposto **YOUR_KEY** e **YOUR_LOCATION**.

    Dopo aver incollato i valori della chiave e della posizione, le prime due righe di codice dovrebbero avere un aspetto simile al seguente:

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."
    $location="somelocation"
    ```

1. In alto a destra nel riquadro dell'editor fare clic sul pulsante **...** per aprire il menu e selezionare **Salva** per salvare le modifiche. Aprire di nuovo il menu e selezionare **Close Editor**.

    L'applicazione client di esempio userà il servizio Traduttore per eseguire diverse attività:
    - Tradurre testo dall'inglese al francese, all'italiano e al cinese.
    - Tradurre audio dall'inglese in testo in francese

    Usare il lettore video seguente per ascoltare l'audio di input che verrà elaborato dall'applicazione:

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWORN0" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>


    > **Nota** Un'applicazione reale potrebbe accettare l'input da un microfono e inviare la risposta a un altoparlante, ma in questo semplice esempio si userà l'input preregistrato in un file audio.

1. Nel riquadro Cloud Shell immettere il comando seguente per eseguire il codice:

    ```PowerShell
    cd ai-900
    ./translator.ps1
    ```

1. Esaminare l'output. Si è vista la traduzione dal testo in inglese al francese, all'italiano e al cinese?  Si è visto l'audio in inglese "hello" tradotto in testo in francese?

## <a name="learn-more"></a>Altre informazioni

Questa semplice app mostra solo alcune delle funzionalità del servizio Traduttore. Per altre informazioni su cosa è possibile fare con questo servizio, vedere la [pagina del servizio Traduttore](https://docs.microsoft.com/azure/cognitive-services/translator/translator-overview).