---
lab:
  title: Esplorare la funzionalità di riconoscimento volto
---

# Esplorare la funzionalità di riconoscimento volto

> **Nota:** per completare questo lab è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

Le soluzioni di visione artificiale richiedono spesso una soluzione di intelligenza artificiale (IA) per poter rilevare i visi umani. Si supponga, ad esempio, che l'azienda di vendita al dettaglio Northwind Traders voglia individuare la posizione in cui i clienti si trovano in un negozio per assisterli al meglio. Un modo per eseguire questa operazione consiste nel determinare se sono presenti visi nelle immagini e, in tal caso, identificare le coordinate del rettangolo delimitatore intorno ai visi.

Per testare le funzionalità del servizio Viso, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell. Gli stessi principi e funzionalità sono applicabili a soluzioni reali, ad esempio siti Web o app per smartphone.

## Creare una risorsa *API Viso*

È possibile usare il servizio Viso creando una risorsa **Viso**.

Se non è già stato fatto, creare una risorsa **API Viso** nella sottoscrizione di Azure.

1. In un'altra scheda del browser, aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Fare clic sul pulsante **&#65291;Crea una risorsa**, cercare *Viso* e creare una risorsa **Viso** con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: gratuito F0.

1. Esaminare e creare la risorsa e attendere il completamento della distribuzione. Passare quindi alla risorsa distribuita.

1. Visualizzare la pagina **Chiavi ed endpoint** per la risorsa Viso. Sarà necessario specificare l'endpoint e le chiavi per la connessione dalle applicazioni client.

## Eseguire Cloud Shell

Per testare le funzionalità del servizio Viso, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell in Azure. 

1. Nel portale di Azure, selezionare il pulsante **[>_]** (*Cloud Shell*) nella parte superiore della pagina a destra della casella di ricerca. Si aprirà un riquadro di Cloud Shell nella parte inferiore del portale. 

    ![Avviare Cloud Shell facendo clic sull'icona a destra della casella di ricerca in alto](media/create-face-solutions/powershell-portal-guide-1.png)

1. La prima volta che si apre Cloud Shell, è possibile che venga chiesto di scegliere il tipo di shell da usare (*Bash* o *PowerShell*). Selezionare **PowerShell**. Se questa opzione non viene visualizzata, ignorare il passaggio.  

1. Se viene chiesto di creare una risorsa di archiviazione per Cloud Shell, assicurarsi che sia specificata la sottoscrizione corretta e selezionare **Crea risorsa di archiviazione**. Attendere circa un minuto che la risorsa di archiviazione venga creata.

    ![Creare l'archiviazione facendo clic su Conferma.](media/create-face-solutions/powershell-portal-guide-2.png)       

1. Verificare che nella parte superiore sinistra del riquadro Cloud Shell sia impostato *PowerShell* come tipo di shell. Se è *Bash*, passare a *PowerShell* usando il menu a discesa.

    ![Come trovare il menu a discesa a sinistra per passare a PowerShell](media/create-face-solutions/powershell-portal-guide-3.png) 

1. Attendere l'avvio di PowerShell. Nel portale di Azure verrà visualizzata la schermata seguente:  

    ![Attendere l'avvio di PowerShell.](media/create-face-solutions/powershell-prompt.png)

## Configurare ed eseguire un'applicazione client

Ora che si dispone di un modello personalizzato, è possibile eseguire una semplice applicazione client che usa il servizio Viso.

1. Nella shell dei comandi immettere il comando seguente per scaricare l'applicazione di esempio e salvarla in una cartella denominata ai-900.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    > **Suggerimento:** se questo comando è già stato usato in un altro lab per clonare il repository *ai-900*, è possibile ignorare questo passaggio.

1. I file vengono scaricati in una cartella denominata **ai-900**. Ora si vogliono visualizzare tutti i file disponibili nella risorsa di archiviazione di Cloud Shell e usarli. Digitare il comando seguente nella shell:

     ```PowerShell
    code .
    ```

    Si aprirà un editor come quello illustrato nell'immagine seguente: 

    ![Editor di codice.](media/create-face-solutions/powershell-portal-guide-4.png) 

1. Nel riquadro **File** a sinistra espandere **ai-900** e selezionare **find-faces.ps1**. Questo file contiene codice che usa il servizio Viso per rilevare e analizzare i visi in un'immagine, come illustrato di seguito:

    ![Editor contenente codice per rilevare i visi in un'immagine](media/create-face-solutions/find-faces-code.png)

1. Non preoccuparsi troppo dei dettagli del codice, l'aspetto importante è che sono necessari l'URL dell'endpoint e una delle chiavi per la risorsa Viso. Copiare questi valori dalla pagina **Chiavi ed endpoint** per la risorsa dal portale di Azure e incollarli nell'editor di codice, sostituendo rispettivamente i valori segnaposto **YOUR_KEY** e **YOUR_ENDPOINT**.

    > **Suggerimento:** potrebbe essere necessario usare la barra di separazione per regolare l'area della schermata mentre si usano i riquadri **Chiavi ed endpoint** ed **Editor**.

    Dopo aver incollato i valori della chiave e dell'endpoint, le prime due righe di codice dovrebbero essere simili a quanto segue:

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. In alto a destra nel riquadro dell'editor fare clic sul pulsante **...** per aprire il menu e selezionare **Salva** per salvare le modifiche. Aprire di nuovo il menu e selezionare **Chiudi Editor**.

    L'applicazione client di esempio userà il servizio Viso per analizzare l'immagine seguente, scattata da una fotocamera nel negozio di Northwind Traders:

    ![Immagine di un genitore che usa una fotocamera del cellulare per scattare una foto di un bambino in un negozio](media/create-face-solutions/store-camera-1.jpg)

1. Nel riquadro di PowerShell immettere i comandi seguenti per eseguire il codice:

    ```PowerShell
    cd ai-900
    ./find-faces.ps1 store-camera-1.jpg
    ```

1. Esaminare le informazioni restituite, che includono la posizione del viso nell'immagine. La posizione di un viso è indicata dalle coordinate alto-sinistra e la larghezza e l'altezza di un *rettangolo delimitatore*, come illustrato di seguito:

    ![Immagine di una persona con il viso delineato](media/create-face-solutions/store-camera-1-face.jpg)

    >**Nota:** le funzionalità del servizio Viso che restituiscono caratteristiche personali sono limitate. Per informazioni dettagliate, vedere https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/.

1. Proviamo ora un'altra immagine:

    ![Immagine di una persona con un cestino per gli acquisti](media/create-face-solutions/store-camera-2.jpg)

    Per analizzare la seconda immagine, immettere il comando seguente:

    ```PowerShell
    ./find-faces.ps1 store-camera-2.jpg
    ```

1. Esaminare i risultati dell'analisi del viso per la seconda immagine.

1. Proviamone un'altra ancora:

    ![Immagine di una persona con un carrello per gli acquisti](media/create-face-solutions/store-camera-3.jpg)

    Per analizzare la terza immagine, immettere il comando seguente:

    ```PowerShell
    ./find-faces.ps1 store-camera-3.jpg
    ```

1. Esaminare i risultati dell'analisi del viso per la terza immagine.

## Altre informazioni

Questa semplice app mostra solo alcune delle funzionalità del servizio Viso. Per altre informazioni su cosa è possibile fare con questo servizio, vedere la [pagina dell'API Viso](https://azure.microsoft.com/en-us/products/cognitive-services/vision-services).
