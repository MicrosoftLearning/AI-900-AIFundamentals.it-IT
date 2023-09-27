---
lab:
  title: Esplorare Visione artificiale
---

# Esplorare Visione artificiale

> **Nota** Per completare questo lab, è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

Il servizio cognitivo *Visione artificiale* usa modelli di Machine Learning sottoposti a training per analizzare le immagini ed estrarre informazioni su di esse.

Si supponga, ad esempio, che l'azienda di vendita al dettaglio fittizia *Northwind Traders* abbia deciso di implementare un "negozio intelligente", in cui i servizi di intelligenza artificiale mantengono monitorato il negozio per identificare i clienti che richiedono assistenza e indirizzare i dipendenti per aiutarli. Usando il servizio Visione artificiale è possibile analizzare le immagini scattate dalle fotocamere in tutto il negozio per fornire descrizioni significative di ciò che rappresentano.

In questo lab si userà una semplice applicazione da riga di comando per vedere il servizio Visione artificiale in azione. Gli stessi principi e funzionalità sono applicabili a soluzioni reali, ad esempio siti Web o app per smartphone.

## Creare una risorsa *dei servizi di intelligenza artificiale di Azure*

È possibile usare il servizio Visione artificiale creando una risorsa **Visione artificiale** o una risorsa **dei servizi di intelligenza artificiale di Azure**.

Se non è già stato fatto, creare una risorsa dei **servizi di intelligenza artificiale di Azure** nella sottoscrizione di Azure.

1. In un'altra scheda del browser aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Fare clic sul ** pulsante crea una risorsa&#65291;** e cercare *Servizi cognitivi*. Selezionare **Crea** un piano **di Servizi cognitivi** . Verrà visualizzata una pagina per creare una risorsa dei servizi di intelligenza artificiale di Azure. Configurarlo con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: Standard S0
    - **Selezionando questa casella, confermo di aver letto e compreso tutte le condizioni seguenti**: selezionata.

1. Esaminare e creare la risorsa e attendere il completamento della distribuzione. Passare quindi alla risorsa distribuita.

1. Visualizzare la pagina **Chiavi ed endpoint** per la risorsa dei servizi di intelligenza artificiale di Azure. Sarà necessario specificare l'endpoint e le chiavi per la connessione dalle applicazioni client.

## Eseguire Cloud Shell

Per testare le funzionalità del servizio Visione artificiale, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell in Azure.

1. Nel portale di Azure selezionare il pulsante **[>_]** (*Cloud Shell*) nella parte superiore della pagina a destra della casella di ricerca. Verrà aperto un riquadro di Cloud Shell nella parte inferiore del portale.

    ![Avviare Cloud Shell facendo clic sull'icona a destra della casella di ricerca in alto](media/analyze-images-computer-vision-service/powershell-portal-guide-1.png)

1. La prima volta che si apre Cloud Shell, è possibile che venga chiesto di scegliere il tipo di shell da usare (*Bash* o *PowerShell*). Selezionare **PowerShell**. Se questa opzione non viene visualizzata, ignorare il passaggio.  

1. Se viene chiesto di creare una risorsa di archiviazione per Cloud Shell, assicurarsi che sia specificata la sottoscrizione corretta e selezionare **Crea risorsa di archiviazione**. Attendere circa un minuto che la risorsa di archiviazione venga creata.

    ![Creare l'archiviazione facendo clic su Conferma.](media/analyze-images-computer-vision-service/powershell-portal-guide-2.png)

1. Verificare che nella parte superiore sinistra del riquadro di Cloud Shell sia impostato *PowerShell* come tipo di shell. Se è *Bash*, passare a *PowerShell* usando il menu a discesa.

    ![Come trovare il menu a discesa a sinistra per passare a PowerShell](media/analyze-images-computer-vision-service/powershell-portal-guide-3.png)

1. Attendere l'avvio di PowerShell. Nel portale di Azure verrà visualizzata la schermata seguente:  

    ![Attendere l'avvio di PowerShell.](media/analyze-images-computer-vision-service/powershell-prompt.png)

## Configurare ed eseguire un'applicazione client

Ora che si dispone di un ambiente Cloud Shell, è possibile eseguire una semplice applicazione che usa il servizio Visione artificiale per analizzare un'immagine.

1. Nella shell dei comandi immettere il comando seguente per scaricare l'applicazione di esempio e salvarla in una cartella denominata ai-900.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    > **Suggerimento** Se questo comando è già stato usato in un altro lab per clonare il repository *ai-900*, è possibile ignorare questo passaggio.

1. I file vengono scaricati in una cartella denominata **ai-900**. Ora si vogliono visualizzare tutti i file disponibili nella risorsa di archiviazione di Cloud Shell e usarli. Digitare il comando seguente nella shell:

    ```PowerShell
    code .
    ```

    Verrà aperto un editor come quello illustrato nell'immagine seguente:

    ![Editor di codice.](media/analyze-images-computer-vision-service/powershell-portal-guide-4.png)

1. Nel riquadro **File** a sinistra espandere **ai-900** e selezionare **analyze-image.ps1**. Questo file contiene codice che usa il servizio Visione artificiale per analizzare un'immagine, come illustrato di seguito:

    ![Editor contenente il codice per analizzare un'immagine](media/analyze-images-computer-vision-service/analyze-image-code.png)

1. Non preoccuparsi troppo del codice, l'aspetto importante è che sono necessari l'URL dell'endpoint e una delle chiavi per la risorsa Servizi cognitivi. Copiare questi valori dalla pagina **Chiavi ed endpoint** per la risorsa dal portale di Azure e incollarli nell'editor di codice, sostituendo rispettivamente i valori segnaposto **YOUR_KEY** e **YOUR_ENDPOINT**.

    > **Suggerimento** Potrebbe essere necessario usare la barra di separazione per regolare l'area dello schermo mentre si usano i riquadri **Chiavi ed endpoint** ed **Editor**.

    Dopo aver incollato i valori della chiave e dell'endpoint, le prime due righe di codice dovrebbero essere simili a quanto segue:

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. In alto a destra nel riquadro dell'editor fare clic sul pulsante **...** per aprire il menu e selezionare **Salva** per salvare le modifiche.

    L'applicazione client di esempio userà il servizio Visione artificiale per analizzare l'immagine seguente, scattata da una fotocamera nel negozio di Northwind Traders:

    ![Immagine di un genitore che usa una fotocamera del cellulare per scattare una foto di un bambino in un negozio](media/analyze-images-computer-vision-service/store-camera-1.jpg)

1. Nel riquadro di PowerShell immettere i comandi seguenti per eseguire il codice:

    ```PowerShell
    cd ai-900
    ./analyze-image.ps1 store-camera-1.jpg
    ```

1. Esaminare i risultati dell'analisi delle immagini, che includono:
    - Una didascalia suggerita che descrive l'immagine.
    - Un elenco di oggetti identificati nell'immagine.
    - Un elenco di "tag" rilevanti per l'immagine.

1. Proviamo ora un'altra immagine:

    ![Immagine di una persona con un carrello della spesa in un supermercato](media/analyze-images-computer-vision-service/store-camera-2.jpg)

    Per analizzare la seconda immagine, immettere il comando seguente:

    ```PowerShell
    ./analyze-image.ps1 store-camera-2.jpg
    ```

1. Esaminare i risultati dell'analisi dell'immagine per la seconda immagine.

1. Proviamone un'altra ancora:

    ![Immagine di una persona con un carrello per gli acquisti](media/analyze-images-computer-vision-service/store-camera-3.jpg)

    Per analizzare la terza immagine, immettere il comando seguente:

    ```PowerShell
    ./analyze-image.ps1 store-camera-3.jpg
    ```

1. Esaminare i risultati dell'analisi dell'immagine per la terza immagine.

## Altre informazioni

Questa semplice app mostra solo alcune delle funzionalità del servizio Visione artificiale. Per altre informazioni su cosa è possibile fare con questo servizio, vedere la [pagina del servizio Visione artificiale](https://azure.microsoft.com/products/ai-services?activetab=pivot:visiontab).
