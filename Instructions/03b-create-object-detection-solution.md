---
lab:
  title: Esplorare la funzionalità di rilevamento oggetti
---

# Esplorare la funzionalità di rilevamento oggetti

> **Nota:** per completare questo lab è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

Il *rilevamento oggetti* è una forma di visione artificiale in cui viene eseguito il training di un modello di Machine Learning per classificare singole istanze di oggetti in un'immagine e indicare un *rettangolo delimitatore* che ne contrassegna la posizione. È possibile considerarlo come un'evoluzione della *classificazione immagini* (in cui il modello risponde alla domanda "a cosa corrisponde questa immagine?") per la creazione di soluzioni in cui è possibile porre al modello la domanda "quali oggetti sono presenti in questa immagine e dove si trovano?".

Ad esempio, un'iniziativa di sicurezza stradale potrebbe identificare i pedoni e i ciclisti come utenti più vulnerabili agli incroci stradali. Usando telecamere per monitorare gli incroci, è possibile analizzare immagini di utenti stradali per rilevare pedoni e ciclisti per monitorarne i numeri o anche modificare il comportamento dei segnali stradali.

Il servizio **Visione personalizzata** disponibile in Microsoft Azure offre una soluzione basata sul cloud per la creazione e la pubblicazione di modelli di rilevamento oggetti personalizzati. In Azure è possibile usare il servizio Visione personalizzata per eseguire il training di un modello di rilevamento oggetti in base a immagini esistenti. Sono due gli elementi coinvolti nella creazione di una soluzione di rilevamento oggetti. Prima di tutto, è necessario eseguire il training di un modello per rilevare la posizione e la classe di oggetti usando immagini etichettate. Dopo aver eseguito il training del modello è necessario pubblicarlo come servizio che può essere usato dalle applicazioni.

Per testare le funzionalità del servizio Visione personalizzata per il rilevamento di oggetti nelle immagini, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell. Gli stessi principi e funzionalità sono applicabili a soluzioni reali, ad esempio siti Web o app per dispositivi mobili.

## Creare una risorsa *Servizi di Azure AI*

È possibile usare il servizio Visione personalizzata creando una risorsa **Visione personalizzata** o una risorsa **Servizi di Azure AI**.

> **Nota:** non tutte le risorse sono disponibili in tutte le aree. Indipendentemente dal fatto che si crei una risorsa Visione personalizzata o Servizi di Azure AI, è possibile usare solo le risorse create in [determinate aree](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services) per accedere ai servizi di Visione personalizzata. Per semplicità, è stata preselezionata un'area nelle istruzioni di configurazione riportate di seguito.

Creare una risorsa **Servizi di Azure AI** nella sottoscrizione di Azure.

1. In un'altra scheda del browser, aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Fare clic sul pulsante **&#65291;Crea una risorsa** e cercare *Servizi di Azure AI*. Selezionare **Crea** un piano di **Servizi di Azure AI**. Verrà visualizzata una pagina per creare una risorsa Servizi di Azure AI. Eseguire la configurazione con le seguenti impostazioni:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: Stati Uniti orientali
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: Standard S0.
    - **Selezionando questa casella, confermo di aver letto e compreso tutte le condizioni seguenti**: selezionata.

1. Esaminare e creare la risorsa e attendere il completamento della distribuzione. Passare quindi alla risorsa distribuita.

1. Visualizzare la pagina **Chiavi ed endpoint** per la risorsa Servizi di Azure AI. Sarà necessario specificare l'endpoint e le chiavi per la connessione dalle applicazioni client.

## Creare un progetto di Visione personalizzata

Per eseguire il training di un modello di rilevamento oggetti, è necessario creare un progetto Visione personalizzata basato sulla risorsa di training. A questo scopo, si userà il portale di Visione personalizzata.

1. In una nuova scheda del browser aprire il portale di Visione personalizzata all'indirizzo [https://customvision.ai](https://customvision.ai?azure-portal=true) ed eseguire l'accesso usando l'account Microsoft associato alla sottoscrizione di Azure.

1. Creare un nuovo progetto con le seguenti impostazioni:
    - **Nome**: sicurezza stradale
    - **Descrizione**: rilevamento oggetti per la sicurezza stradale.
    - **Risorsa**: *la risorsa creata in precedenza*
    - **Tipi di progetto**: Rilevamento oggetti
    - **Domini**: generale \[A1]

1. Attendere che il progetto venga creato e aperto nel browser.

## Aggiungere e contrassegnare le immagini

Per eseguire il training di un modello di rilevamento oggetti, è necessario caricare immagini contenenti le classi che si desidera far identificare al modello e contrassegnarle per indicare i rettangoli delimitatori per ogni istanza dell'oggetto.

1. Scaricare ed estrarre le immagini di training da [https://aka.ms/traffic-images](https://aka.ms/traffic-images). La cartella estratta contiene una raccolta di immagini di ciclisti e pedoni.

1. Nel portale di Visione personalizzata, nel progetto di rilevamento oggetti **Sicurezza stradale**, selezionare **Add images** (Aggiungi immagini) e caricare tutte le immagini nella cartella estratta.

    ![Screenshot della finestra di dialogo Image Upload (Caricamento immagini) in Studio Visione personalizzata.](media/create-object-detection-solution/upload-images.png)

1. Dopo aver caricato le immagini, selezionare la prima per aprirla.

1. Tenere il mouse su qualsiasi oggetto (ciclista o pedone) nell'immagine finché non viene visualizzata un'area rilevata automaticamente. Quindi selezionare l'oggetto e, se necessario, ridimensionare l'area per circondarlo. In alternativa, è possibile trascinare semplicemente il mouse intorno all'oggetto per creare un'area.

    Quando l'oggetto è strettamente selezionato all'interno dell'area rettangolare, inserire il tag appropriato per l'oggetto (*ciclista* o *pedone*) e usare il pulsante **Tag region** (Area del tag) (**+**) per aggiungere il tag al progetto.

    ![Screenshot di un'immagine con un'area contrassegnata nella finestra di dialogo Image Detail (Dettaglio immagine).](media/create-object-detection-solution/tag-image.png)

1. Usare il collegamento **Avanti** (**(>)** a destra per passare all'immagine successiva e aggiungere un tag ai relativi oggetti. Poi continuate a scorrere l'intera raccolta di immagini, assegnando un tag a ogni ciclista e pedone.

    Quando si assegnano tag alle immagini, tenere presente quanto segue:

    - Alcune immagini contengono più oggetti, potenzialmente di tipi diversi. Assegnare un tag a ognuno di essi, anche se si sovrappongono.
    - Dopo aver inserito un tag una volta, è possibile selezionarlo dall'elenco per l'assegnazione di tag a nuovi oggetti.
    - È possibile andare avanti e indietro nelle immagini per modificare i tag.

    ![Screenshot di un'immagine con un'area contrassegnata nella finestra di dialogo Image Detail (Dettaglio immagine).](media/create-object-detection-solution/multiple-objects.png)

1. Al termine dell'assegnazione di tag all'ultima immagine, chiudere l'editor **Image Detail** (Dettaglio immagine) e nella pagina **Training Images** (Immagini di training), in **Tag** selezionare **Tagged** (Contrassegnata) per visualizzare tutte le immagini con tag:

    ![Screenshot delle immagini contrassegnate in un progetto.](media/create-object-detection-solution/tagged-images.png)

## Eseguire il training e testare un modello

Dopo aver contrassegnato le immagini nel progetto, è possibile eseguire il training di un modello.

1. Nel progetto di Visione personalizzata, fare clic su **Train** (Esegui training) per eseguire il training di un modello di rilevamento oggetti usando le immagini con tag. Selezionare l'opzione **Quick Training** (Training rapido).

    > **Suggerimento:**: il training potrebbe richiedere diversi minuti. Durante l'attesa, consultare la sezione [Video analytics for smart cities](https://www.microsoft.com/research/video/video-analytics-for-smart-cities/), che descrive un progetto reale per l'uso della visione artificiale in un'iniziativa di miglioramento della sicurezza stradale.

2. Una volta completato il training, esaminare le metriche delle prestazioni *Precision* (Precisione), *Recall* (Richiamo) e *mAP*, che misurano la validità della stima del modello di rilevamento oggetti e i cui valori dovrebbero essere ragionevolmente elevati.

3. Regolare il valore **Probability Threshold** (Soglia di probabilità) a sinistra, aumentandola dal 50% al 90% e osservare l'impatto sulle metriche delle prestazioni. Questa impostazione determina il valore di probabilità che ogni valutazione del tag deve soddisfare o superare per essere considerata una previsione.

    ![Screenshot delle metriche delle prestazioni per un modello sottoposto a training.](media/create-object-detection-solution/performance-metrics.png)

4. In alto a destra nella pagina fare clic su **Test rapido** e quindi nella casella **URL immagine** immettere `https://aka.ms/pedestrian-cyclist` e visualizzare i risultati.

    Nel riquadro a destra, in **Predictions** (Previsioni), ogni oggetto rilevato viene elencato con il rispettivo tag e la probabilità. Selezionare ogni oggetto per visualizzarlo evidenziato nell'immagine.

    Gli oggetti previsti potrebbero non essere tutti corretti: dopo tutto, ciclisti e pedoni condividono molte caratteristiche comuni. Le previsioni su cui il modello è più attendibile hanno i valori di probabilità più alti. Usare il dispositivo di scorrimento **Valore soglia** per eliminare gli oggetti con una bassa probabilità. Dovrebbe essere possibile trovare un punto in cui sono incluse solo previsioni corrette (probabilmente intorno all'85-90%).

    ![Screenshot delle metriche delle prestazioni per un modello sottoposto a training.](media/create-object-detection-solution/test-detection.png)

5. Quindi chiudere la finestra **Quick Test** (Test rapido).

## Pubblicare il modello di rilevamento oggetti

A questo punto è possibile pubblicare il modello sottoposto a training per poterlo usare da un'applicazione client.

1. Fare clic su **&128504; Pubblica** per pubblicare il modello sottoposto a training con le impostazioni seguenti:
    - **Nome modello**: sicurezza-stradale
    - **Risorsa di previsione**: *la risorsa creata in precedenza*.

1. Dopo la pubblicazione fare clic sull'icona dell'*URL di previsione* (&#127760;) per visualizzare le informazioni necessarie per usare il modello pubblicato.

    ![Screenshot dell'URL di previsione.](media/create-object-detection-solution/prediction-url.png)

In seguito saranno necessari i valori appropriati per l'URL e la chiave di previsione per ottenere una stima da un URL immagine, quindi mantenere aperta questa finestra di dialogo e continuare con l'attività successiva.

## Preparare un'applicazione client

Per testare le funzionalità del servizio Visione personalizzata, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell in Azure.

1. Tornare alla scheda del browser contenente il portale di Azure e selezionare il pulsante **Cloud shell** (**[>_]**) nella parte superiore della pagina a destra della casella di ricerca. Si aprirà un riquadro di Cloud Shell nella parte inferiore del portale.

    La prima volta che si apre Cloud Shell, è possibile che venga chiesto di scegliere il tipo di shell da usare (*Bash* o *PowerShell*). In questo caso, selezionare **PowerShell**.

    Se viene chiesto di creare una risorsa di archiviazione per Cloud Shell, assicurarsi che sia selezionata la sottoscrizione corretta e selezionare **Crea risorsa di archiviazione**. Attendere circa un minuto che la risorsa di archiviazione venga creata.

    Quando Cloud Shell è pronto, dovrebbe essere simile al seguente:
    
    ![Screenshot di Cloud Shell nel portale di Azure.](media/create-object-detection-solution/cloud-shell.png)

    > **Consiglio**: assicurarsi che nella parte superiore sinistra del riquadro di Cloud Shell sia impostato *PowerShell* come tipo di shell. Se è *Bash*, passare a *PowerShell* usando il menu a discesa.

    Si noti che è possibile ridimensionare Cloud Shell trascinando la barra di separazione nella parte superiore del riquadro o usando le icone **&#8212;**, **&#9723;** e **X** nell'angolo in alto a destra del riquadro per ridurre a icona, ingrandire o chiudere il riquadro. Per altre informazioni sull'uso di Azure Cloud Shell, vedere la [documentazione su Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

2. Nella shell dei comandi immettere i comandi seguenti per scaricare i file per questo esercizio e salvarli in una cartella denominata **ai-900** (dopo aver rimosso la cartella, se già esistente)

    ```PowerShell
    rm -r ai-900 -f
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

3. Dopo aver scaricato i file, immettere i comandi seguenti per passare alla directory **ai-900** e modificare il file di codice per questo esercizio:

    ```PowerShell
    cd ai-900
    code detect-objects.ps1
    ```

    Si aprirà un editor come quello illustrato nell'immagine seguente:

     ![Screenshot dell'editor di codice in Cloud Shell.](media/create-object-detection-solution/code-editor.png)

     > **Suggerimento:**: è possibile usare il separatore tra la riga di comando di Cloud Shell e l'editor di codice per ridimensionare i riquadri.

4. Non prestare attenzione eccessiva ai dettagli del codice. L'aspetto importante è che inizia con un codice per specificare l'URL di previsione e la chiave per il modello di Visione personalizzata. È necessario aggiornarli in modo che il resto del codice usi il modello.

    Ottenere l'*URL di previsione* e *la chiave di previsione* dalla finestra di dialogo aperta nella scheda del browser per il progetto di Visione personalizzata. *Se si dispone di un URL immagine*, è necessario usare le versioni.

    Usare questi valori per sostituire i segnaposto **YOUR_PREDICTION_URL** e **YOUR_PREDICTION_KEY** nel file di codice.

    Dopo aver incollato i valori dell'URL e della chiave di previsione, le prime due righe di codice dovrebbero essere simili a questa:

    ```PowerShell
    $predictionUrl="https..."
    $predictionKey ="1a2b3c4d5e6f7g8h9i0j...."
    ```

5. Dopo aver apportato le modifiche alle variabili nel codice, premere **CTRL+S** per salvare il file. Premere quindi **CTRL+Q** per chiudere l'editor di codice.

## Testare l'applicazione client

È ora possibile usare l'applicazione client di esempio per rilevare ciclisti e pedoni nelle immagini.

1. Nel riquadro di PowerShell immettere il comando seguente per eseguire il codice:

    ```PowerShell
    ./detect-objects.ps1 1
    ```

    Questo codice usa il modello per rilevare oggetti nell'immagine seguente:

    ![Fotografia di un pedone e di un ciclista.](media/create-object-detection-solution/road-safety-1.jpg)

1. Esaminare la previsione, che elenca tutti gli oggetti rilevati con una probabilità del 90% o più, insieme alle coordinate di un riquadro delimitatore del testo intorno alla posizione.

1. Proviamo ora un'altra immagine. Eseguire questo comando:

    ```PowerShell
    ./detect-objects.ps1 2
    ```

    Questa volta viene analizzata l'immagine seguente:

    ![Fotografia di un gruppo di pedoni.](media/create-object-detection-solution/road-safety-2.jpg)

Se tutto va bene, il modello di rilevamento oggetti ha rilevato correttamente pedoni e ciclisti nelle immagini di test.

