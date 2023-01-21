---
lab:
  title: Esplorare la funzionalità di comprensione del linguaggio
---

# <a name="explore-language-understanding"></a>Esplorare la funzionalità di comprensione del linguaggio

> **Nota** Per completare questo lab, è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

Gli utenti hanno aspettative sempre crescenti riguardo alla capacità dei computer di usare l'intelligenza artificiale per comprendere i comandi parlati o digitati in linguaggio naturale. Si può avere ad esempio l'esigenza di implementare un sistema di domotica che consenta di controllare i dispositivi nella propria casa tramite comandi vocali, come "accendi la luce" o "accendi il ventilatore", e di usare un dispositivo basato sull'intelligenza artificiale in grado di comprendere il comando ed eseguire l'azione appropriata.

Per testare le funzionalità del servizio di comprensione del linguaggio di conversazione, verrà usata un'applicazione da riga di comando eseguita in Cloud Shell. Gli stessi principi e funzionalità sono applicabili a soluzioni reali, ad esempio siti Web o app per smartphone.

## <a name="create-a-language-service-resource"></a>Creare una risorsa del *servizio Lingua*

È possibile usare il servizio di comprensione del linguaggio di conversazione creando una risorsa del **servizio Lingua**.

Se non è già stato fatto, creare una risorsa del **servizio Lingua** nella sottoscrizione di Azure.

1. In un'altra scheda del browser aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Fare clic sul pulsante **&#65291;Crea una risorsa**, cercare *Servizio Lingua* e creare una risorsa **Servizio Lingua** con le impostazioni seguenti:
    - Selezionare funzionalità aggiuntive: *mantenere le funzionalità predefinite e fare clic su Continua per creare la risorsa*  
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: Stati Uniti orientali 2
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: S (1.000 chiamate al minuto)
    - **Selezionando questa casella, dichiaro di conoscere e confermare tutti i termini indicati nei nostri principi di intelligenza artificiale responsabile**: selezionata.

1. Esaminare e creare la risorsa e attendere il completamento della distribuzione.

### <a name="create-a-conversational-language-understanding-app"></a>Creare un'app di comprensione del linguaggio di conversazione

Per implementare la comprensione del linguaggio naturale con la funzionalità di comprensione del linguaggio di conversazione, si crea un'app e quindi si aggiungono entità, finalità ed espressioni per definire i comandi che l'app deve eseguire.

1. In una nuova scheda del browser aprire il portale Language Studio all'indirizzo [https://language.azure.com](https://language.azure.com?azure-portal=true) e accedere usando l'account Microsoft associato alla sottoscrizione di Azure.

1. Se viene richiesto di scegliere una risorsa del servizio Lingua, selezionare le impostazioni seguenti:
    - **Directory di Azure**: directory di Azure contenente la sottoscrizione.
    - **Sottoscrizione di Azure**: sottoscrizione di Azure in uso.
    - **Language resource** (Risorsa Lingua): risorsa del servizio Lingua creata in precedenza.

    >**Suggerimento** Se ***non*** viene chiesto di scegliere una risorsa Lingua, è possibile che nella sottoscrizione siano presenti più risorse di questo tipo e in tal caso:
    >1. Sulla barra nella parte superiore della pagina fare clic sul pulsante **Impostazioni (&#9881;)** .
    >1. Nella pagina **Impostazioni** visualizzare la scheda **Risorse**.
    >1. Selezionare la risorsa del servizio Lingua e fare clic su **Cambia risorsa**.
    >1. Nella parte superiore della pagina fare clic su **Language Studio** per tornare alla home page di Language Studio.

1. Nella parte superiore del portale scegliere **Comprensione del linguaggio di conversazione** dal menu **Crea nuovo**.

1. Nella finestra di dialogo **Create a project** immettere i dati seguenti nella pagina **Enter basic information** e quindi fare clic su **Next**:
    - **Name**: *creare un nome univoco*
    - **Description**: Domotica semplice
    - **Utterances primary language** (Lingua principale espressioni): Inglese
    - **Enable multiple languages in project**: *non selezionare*

    ![Immettere i dettagli per il progetto.](media/conversational-language-understanding/create-project.png)

    >**Suggerimento** Prendere nota del *nome del progetto* che verrà usato in un secondo momento.

1. Nella pagina *Rivedere e completare* fare clic su **Crea**.

### <a name="create-intents-utterances-and-entities"></a>Creare finalità, espressioni ed entità

Una *finalità* è un'azione che si intende eseguire. Si può ad esempio voler accendere una luce o spegnere un ventilatore. In questo caso, si definiscono due finalità, rispettivamente per attivare un dispositivo e per disattivarne un altro. Per ogni finalità si specificano quindi *espressioni* di esempio che indicano il tipo di lingua usato per definire la finalità.

1. Nel riquadro **Definizione dello schema** assicurarsi che l'opzione **Intenti** sia selezionata, quindi fare clic su **Aggiungi**, aggiungere un intento con il nome **switch_on** (in minuscolo) e infine fare clic su **Aggiungi intento**.

    ![Fare clic su Aggiungi in Intenti nel riquadro Definizione dello schema.](media/conversational-language-understanding/build-schema.png)
    ![Aggiungere la finalità switch_on e quindi selezionare Aggiungi intento.](media/conversational-language-understanding/add-intent.png)

1. Selezionare la finalità **switch_on**. Verrà visualizzata la pagina **Etichettatura dei dati**. Nell'elenco a discesa **Intento** selezionare **switch_on**. Accanto alla finalità **switch_on** digitare l'espressione ***accendi la luce*** e premere **INVIO** per includere l'espressione nell'elenco.

    ![Aggiungere un'espressione al set di training digitando "accendi la luce" in Espressione.](media/conversational-language-understanding/add-utterance-on.png)

1. Il servizio Lingua richiede almeno cinque esempi di espressioni diverse per ogni finalità in modo da eseguire un training sufficiente del modello linguistico. Aggiungere altri cinque esempi di espressione per la finalità **switch_on**:  
    - ***accendi il ventilatore***
    - ***attiva il ventilatore***
    - ***apri la luce***
    - ***accendi la luce***
    - ***avvia il ventilatore***

1. Nel riquadro **Etichettatura delle entità per il training** sul lato destro della schermata selezionare **Etichette** e quindi selezionare **Aggiungi entità**. Digitare **dispositivo** (in minuscolo), selezionare **Elenco** e quindi **Aggiungi entità**.

    ![Aggiungere un'entità selezionando Etichette nel pannello Etichettatura delle entità per il training e quindi selezionare Aggiungi entità.](media/conversational-language-understanding/add-entity.png) 
    ![Digitare il dispositivo in Nome entità e selezionare Elenco, quindi selezionare Aggiungi entità.](media/conversational-language-understanding/add-entity-device.png)

1. Nell'espressione ***avvia il ventilatore*** evidenziare la parola "ventilatore". Nell'elenco visualizzato selezionare **dispositivo** nella casella *Search for an entity*.

    ![Evidenziare la parola ventilatore nell'espressione e selezionare dispositivo.](media/conversational-language-understanding/switch-on-entity.png)

1. Eseguire la stessa procedura per tutte le espressioni. Etichettare il resto delle espressioni relative al *ventilatore* o alla *luce* con l'entità **dispositivo**. Al termine, verificare di avere le espressioni seguenti e selezionare **Salva modifiche**:

    | **finalità** | **espressione** | **entità** |
    | --------------- | ------------------ | ------------------ |
    | switch_on   | Attiva il ventilatore      | Dispositivo: *selezionare il ventilatore* |
    | switch_on   | Apri la luce    | Dispositivo: *selezionare la luce* |
    | switch_on   | Attiva la luce | Dispositivo: *selezionare la luce* |
    | switch_on   | Avvia il ventilatore     | Dispositivo: *selezionare il ventilatore* |
    | switch_on   | Accendi il ventilatore   | Dispositivo: *selezionare il ventilatore* |
    | switch_on   | Accendi la luce   | Dispositivo: *selezionare la luce* |

    ![Al termine, selezionare Salva modifiche.](media/conversational-language-understanding/save-changes.png) 

1. Nel riquadro a sinistra fare clic su **Definizione dello schema** e verificare che l'intento **switch_on** sia elencato. Fare quindi clic su **Add** e aggiungere una nuova finalità con il nome **switch_off** (in minuscolo).

    ![Tornare alla schermata Definizione dello schema e aggiungere un intento switch_off.](media/conversational-language-understanding/add-switch-off.png) 

1. Fare clic sulla finalità **switch_off**. Verrà visualizzata la pagina **Etichettatura dei dati**. Nell'elenco a discesa **Intento** selezionare **switch_off**. Accanto alla finalità **switch_off** aggiungere l'espressione ***spegni la luce***.

1. Aggiungere altri cinque esempi di espressione per la finalità **switch_off**:
    - ***spegni il ventilatore***
    - ***disattiva il ventilatore***
    - ***chiudi la luce***
    - ***spegni la luce***
    - ***arresta il ventilatore***

1. Etichettare la parola *luce* o *ventilatore* con l'entità **dispositivo**. Al termine, verificare di avere le espressioni seguenti e selezionare **Salva modifiche**:  

    | **finalità** | **espressione** | **entità** | 
    | --------------- | ------------------ | ------------------ |
    | switch_off   | Disattiva il ventilatore    | Dispositivo: *selezionare il ventilatore* | 
    | switch_off   | Chiudi la luce  | Dispositivo: *selezionare la luce* |
    | switch_off   | Disattiva la luce | Dispositivo: *selezionare la luce* |
    | switch_off   | Arresta il ventilatore | Dispositivo: *selezionare il ventilatore* |
    | switch_off   | Spegni il ventilatore | Dispositivo: *selezionare il ventilatore* |
    | switch_off   | Spegni la luce | Dispositivo: *selezionare la luce* |

### <a name="train-the-model"></a>Eseguire il training del modello

Ora si è pronti a usare le finalità e le entità definite per eseguire il training del modello linguistico di conversazione per l'app.

1. Sul lato sinistro di Language Studio selezionare **Training jobs**, quindi selezionare **Start a training job**. Usare le seguenti impostazioni: 
    - **Train a new model**: *selezionare l'opzione e scegliere un nome di modello*
    - **Training mode**: Standard training (free)
    - **Data Splitting**: *selezionare Automatically split the testing set from the training data, lasciare le percentuali predefinite*
    - Fare clic su **Train** nella parte inferiore della pagina.

1. Attendere il completamento del training. 

### <a name="deploy-and-test-the-model"></a>Distribuire e testare il modello

Per usare il modello sottoposto a training in un'applicazione client, è necessario distribuirlo come endpoint a cui le applicazioni client possono inviare nuove espressioni, in base alle quali verranno previste le finalità e le entità.

1. Sul lato sinistro di Language Studio selezionare **Deploying a model**.

1. Selezionare il nome del modello e fare clic su **Add deployment**. Usare queste impostazioni:
    - **Creare o selezionare un nome di distribuzione esistente**: *selezionare Creare un nuovo nome di distribuzione. Aggiungere un nome univoco*.
    - **Assegnare il modello sottoposto a training al nome della distribuzione**: *selezionare il nome del modello sottoposto a training*.
    - Fare clic su **Deploy**

    >**Suggerimento** Prendere nota del *nome della distribuzione* che verrà usato in un secondo momento. 

1. Quando il modello viene distribuito, fare clic su **Testing deployments** sul lato sinistro della pagina e quindi selezionare il modello distribuito in **Deployment name**.

1. Immettere il testo seguente e quindi selezionare **Run the test**:

    *attiva la luce*

    ![Testare il modello selezionando il modello distribuito, quindi immettendo testo e selezionando Esegui il test.](media/conversational-language-understanding/test-model.png) 

    Esaminare il risultato restituito, notando che include la finalità prevista (che dovrebbe essere **switch_on**) e l'entità prevista (**dispositivo**) con un punteggio di attendibilità che indica la probabilità calcolata dal modello per la finalità e l'entità previste. La scheda JSON mostra l'attendibilità comparativa per ogni finalità potenziale (quella con il punteggio di attendibilità più alto è la finalità stimata)

1. Deselezionare la casella di testo e testare il modello con le espressioni seguenti in *Immettere il testo, caricare un file o utilizzare uno dei testi di esempio*:
    - *spegni il ventilatore*
    - *apri la luce*
    - *disattiva il ventilatore*

## <a name="run-cloud-shell"></a>Eseguire Cloud Shell

Provare ora ad applicare il modello distribuito. A questo scopo, si userà un'applicazione da riga di comando eseguita in Azure Cloud Shell. 

1. Lasciare aperta la scheda del browser con Language Studio e tornare alla scheda del browser contenente il portale di Azure.

1. Nel portale di Azure selezionare il pulsante **[>_]** (*Cloud Shell*) nella parte superiore della pagina a destra della casella di ricerca. Quando si fa clic sul pulsante viene aperto un riquadro Cloud Shell nella parte inferiore del portale.

    ![Avviare Cloud Shell facendo clic sull'icona a destra della casella di ricerca in alto](media/conversational-language-understanding/powershell-portal-guide-1.png)

1. La prima volta che si apre Cloud Shell, è possibile che venga chiesto di scegliere il tipo di shell da usare (*Bash* o *PowerShell*). Selezionare **PowerShell**. Se questa opzione non viene visualizzata, ignorare il passaggio.  

1. Se viene chiesto di creare una risorsa di archiviazione per Cloud Shell, assicurarsi che sia specificata la sottoscrizione corretta e selezionare **Crea risorsa di archiviazione**. Attendere circa un minuto che la risorsa di archiviazione venga creata. 

    ![Creare l'archiviazione facendo clic su Conferma.](media/conversational-language-understanding/powershell-portal-guide-2.png)

1. Verificare che nella parte superiore sinistra del riquadro Cloud Shell sia impostato *PowerShell* come tipo di shell. Se è *Bash*, passare a *PowerShell* usando il menu a discesa.

    ![Come trovare il menu a discesa a sinistra per passare a PowerShell](media/conversational-language-understanding/powershell-portal-guide-3.png) 

1. Attendere l'avvio di PowerShell. Nel portale di Azure verrà visualizzata la schermata seguente:  

    ![Attendere l'avvio di PowerShell.](media/conversational-language-understanding/powershell-prompt.png) 

## <a name="configure-and-run-a-client-application"></a>Configurare ed eseguire un'applicazione client

Ora si aprirà e si modificherà uno script già scritto, che eseguirà l'applicazione client.

1. Nella shell dei comandi immettere il comando seguente per scaricare l'applicazione di esempio e salvarla in una cartella denominata ai-900.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**Nota** Se questo comando è già stato usato in un altro lab per clonare il repository *ai-900*, è possibile ignorare questo passaggio.

1. I file vengono scaricati in una cartella denominata **ai-900**. Ora si vogliono visualizzare tutti i file presenti in questa cartella e usarli. Digitare i comandi seguenti nella shell:

     ```PowerShell
    cd ai-900
    code .
    ```

    Lo script aprirà un editor come quello illustrato nell'immagine seguente: 

    ![Editor di codice.](media/conversational-language-understanding/powershell-portal-guide-4.png)

1. Nel riquadro **Files** a sinistra selezionare il file **understand.ps1** nella cartella **ai-900**. Nel file è incluso del codice che usa il modello di comprensione del linguaggio di conversazione. 

    ![Il codice per il lab di comprensione del linguaggio con le credenziali necessarie per modificare e salvare prima di eseguire il programma.](media/conversational-language-understanding/understand-code.png)

    Non prestare attenzione eccessiva ai dettagli del codice. L'importante è usare le istruzioni seguenti per modificare il file per specificare il modello linguistico sottoposto a training. 

1. Tornare alla scheda del browser contenente **Language Studio**. In Language Studio aprire la pagina **Deploying a model** e selezionare il modello. Fare quindi clic sul pulsante **Get prediction URL**. Le due informazioni di cui si ha bisogno sono riportate in questa finestra di dialogo:
    - Endpoint per il modello: è possibile copiare l'endpoint dalla casella **Prediction URL**.
    - Chiave per il modello: la chiave si trova in **Sample request** come valore per il parametro **Ocp-Apim-Subscription-Key** e ha un aspetto simile a ***0ab1c23de4f56gh7i8901234jkl567m8***.

1. Copiare il valore dell'endpoint, quindi tornare alla scheda del browser contenente Cloud Shell e incollare tale valore nell'editor di codice, sostituendo **YOUR_ENDPOINT** (tra virgolette). Ripetere la procedura per la chiave, sostituendo **YOUR_KEY**.

1. Sostituire quindi **YOUR_PROJECT_NAME** con il nome del proprio progetto e sostituire **YOUR_DEPLOYMENT_NAME** con il nome del proprio modello distribuito. Le prime righe di codice dovrebbero essere simili a quanto illustrato di seguito:

    ```PowerShell
    $endpointUrl="https://some-name.cognitiveservices.azure.com/language/..."
    $key = "0ab1c23de4f56gh7i8901234jkl567m8"
    $projectName = "name"
    $deploymentName = "name"
    ```

1. In alto a destra nel riquadro dell'editor fare clic sul pulsante **...** per aprire il menu e selezionare **Salva** per salvare le modifiche. Aprire di nuovo il menu e selezionare **Close Editor**.

1. Nel riquadro di PowerShell immettere il comando seguente per eseguire il codice:

    ```PowerShell
    ./understand.ps1 "Turn on the light"
    ```

1. Esaminare i risultati. L'app dovrebbe aver compreso che l'azione prevista è quella di accendere la luce.

1. Provare ora con un altro comando:

    ```PowerShell
    ./understand.ps1 "Switch the fan off"
    ```

1. Esaminare i risultati del comando. L'app dovrebbe aver compreso che l'azione prevista è quella di spegnere il ventilatore.

1. Provare con altri comandi, inclusi alcuni per i quali non è stato eseguito il training del modello, come "Salve" o "accendi il forno". In linea di massima l'app dovrebbe comprendere i comandi per i quali è stato definito il modello di linguaggio, ma non essere in grado di interpretare correttamente altri input.

>**Nota** Sarà necessario iniziare ogni volta con **./understand.ps1** seguito dalla frase. Racchiudere la frase tra virgolette.

## <a name="learn-more"></a>Altre informazioni

Questa app mostra solo alcune delle funzionalità di comprensione del linguaggio di conversazione del servizio Lingua. Per altre informazioni sulle operazioni che è possibile eseguire con questo servizio, vedere la pagina [Comprensione del linguaggio di conversazione](https://docs.microsoft.com/azure/cognitive-services/language-service/conversational-language-understanding/overview). 
