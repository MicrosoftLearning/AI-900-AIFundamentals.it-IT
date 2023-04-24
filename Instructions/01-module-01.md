---
lab:
  title: Esplorare Servizi cognitivi
  module: Module 1 - Introduction to AI
---

# <a name="explore-cognitive-services"></a>Esplorare Servizi cognitivi

> **Nota** Per completare questo lab, è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

I Servizi cognitivi di Azure incapsulano le funzionalità comuni di intelligenza artificiale, che possono essere suddivise in quattro categorie principali: visione, parlato, lingua e servizi decisionali. In questo esercizio si esaminerà uno dei servizi decisionali per avere un'idea generale di come effettuare il provisioning di una risorsa di Servizi cognitivi e di come usarla in un'applicazione software.

Il servizio cognitivo che si analizzerà in questo esercizio è per la precisione *Rilevamento anomalie*. Rilevamento anomalie viene usato per analizzare i valori dei dati nel corso del tempo e per rilevare eventuali valori insoliti che potrebbero indicare un problema o una situazione su cui condurre ulteriori indagini. Ad esempio, un sensore in un magazzino a temperatura controllata può monitorare la temperatura ogni minuto e registrare i valori misurati. È possibile usare il servizio Rilevamento anomalie per analizzare i valori di temperatura registrati e segnalare quelli che si discostano significativamente dall'intervallo normale di temperature previste.

Per testare le funzionalità del servizio di rilevamento anomalie, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell. Gli stessi principi e funzionalità sono applicabili a soluzioni reali, ad esempio siti Web o app per smartphone.

> **Nota** L'obiettivo di questo esercizio è avere un'idea generale di come viene effettuato il provisioning dei servizi cognitivi e di come vengono usati. Rilevamento anomalie viene usato come esempio, ma non ci si aspetta che con questo esercizio l'utente acquisisca una conoscenza completa del rilevamento delle anomalie.

## <a name="create-an-anomaly-detector-resource"></a>Creare una risorsa *Rilevamento anomalie*

Si inizierà creando una risorsa **Rilevamento anomalie** nella sottoscrizione di Azure:

1. In un'altra scheda del browser aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Fare clic sul pulsante **&#65291;Crea una risorsa**, cercare *Rilevamento anomalie* e creare una risorsa **Rilevamento anomalie** con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare un gruppo di risorse esistente o crearne uno nuovo*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: F0 Gratuito

1. Esaminare e creare la risorsa. Attendere il completamento della distribuzione e quindi passare alla risorsa distribuita.

1. Visualizzare la pagina **Chiavi ed endpoint** per la risorsa Rilevamento anomalie. Sarà necessario specificare l'endpoint e le chiavi per la connessione dalle applicazioni client.

## <a name="run-cloud-shell"></a>Eseguire Cloud Shell

Per testare le funzionalità del servizio Rilevamento anomalie, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell in Azure.

1. Nel portale di Azure selezionare il pulsante **[>_]** (*Cloud Shell*) nella parte superiore della pagina a destra della casella di ricerca. Verrà aperto un riquadro di Cloud Shell nella parte inferiore del portale.

    ![Avviare Cloud Shell facendo clic sull'icona a destra della casella di ricerca in alto](media/anomaly-detector/powershell-portal-guide-1.png)

1. La prima volta che si apre Cloud Shell, è possibile che venga chiesto di scegliere il tipo di shell da usare (*Bash* o *PowerShell*). Selezionare **PowerShell**. Se questa opzione non viene visualizzata, ignorare il passaggio.  

1. Se viene chiesto di creare una risorsa di archiviazione per Cloud Shell, assicurarsi che sia specificata la sottoscrizione corretta e selezionare **Crea risorsa di archiviazione**. Attendere circa un minuto che la risorsa di archiviazione venga creata.

    ![Creare l'archiviazione facendo clic su Conferma.](media/anomaly-detector/powershell-portal-guide-2.png)

1. Verificare che nella parte superiore sinistra del riquadro Cloud Shell sia impostato *PowerShell* come tipo di shell. Se è *Bash*, passare a *PowerShell* usando il menu a discesa.

    ![Come trovare il menu a discesa a sinistra per passare a PowerShell](media/anomaly-detector/powershell-portal-guide-3.png)

1. Attendere l'avvio di PowerShell. Nel portale di Azure verrà visualizzata la schermata seguente:  

    ![Attendere l'avvio di PowerShell.](media/anomaly-detector/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>Configurare ed eseguire un'applicazione client

Ora che si dispone di un ambiente Cloud Shell, è possibile eseguire una semplice applicazione che usa il servizio Rilevamento anomalie per analizzare i dati.

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

    ![Editor di codice.](media/anomaly-detector/powershell-portal-guide-4.png)

1. Nel riquadro **File** a sinistra espandere **ai-900** e selezionare **detect-anomalies.ps1**. Questo file contiene un codice che usa il servizio Rilevamento anomalie, come illustrato di seguito:

    ![Editor contenente codice per rilevare le anomalie](media/anomaly-detector/detect-anomalies-code.png)

1. Non preoccuparsi troppo dei dettagli del codice, l'aspetto importante è che sono necessari l'URL dell'endpoint e una delle chiavi per la risorsa Rilevamento anomalie. Copiare questi valori dalla pagina **Chiavi ed endpoint** per la risorsa (che dovrebbe essere ancora presente nella parte superiore del browser) e incollarli nell'editor di codice, sostituendo rispettivamente i valori segnaposto **YOUR_KEY** e **YOUR_ENDPOINT**.

    > **Suggerimento** Potrebbe essere necessario usare la barra di separazione per regolare l'area dello schermo mentre si usano i riquadri **Chiavi ed endpoint** ed **Editor**.

    Dopo aver incollato i valori della chiave e dell'endpoint, le prime due righe di codice dovrebbero essere simili a quanto segue:

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. In alto a destra nel riquadro dell'editor fare clic sul pulsante **...** per aprire il menu e selezionare **Salva** per salvare le modifiche. Aprire di nuovo il menu e selezionare **Close Editor**.

    Si ricordi che il rilevamento anomalie è una tecnica di intelligenza artificiale usata per determinare se i valori in una serie rientrano nei parametri previsti. L'applicazione client di esempio userà il servizio Rilevamento anomalie per analizzare un file contenente una serie di valori di data/ora e numerici. L'applicazione deve restituire risultati che indichino, a ogni punto nel tempo, se il valore numerico rientra nei parametri previsti.

1. Nel riquadro di PowerShell immettere i comandi seguenti per eseguire il codice:

    ```PowerShell
    cd ai-900
    .\detect-anomalies.ps1
    ```

1. Esaminare i risultati, osservando che la colonna finale dei risultati è **True** o **False** per indicare se il valore registrato a ogni data/ora è considerato un'anomalia o meno. Considerare come si potrebbero usare queste informazioni in una situazione reale. Quale azione potrebbe essere attivata dall'applicazione se i valori della temperatura del frigorifero o della pressione sanguigna fossero rilevati come anomalie?  

## <a name="learn-more"></a>Altre informazioni

Questa semplice app mostra solo alcune delle funzionalità del servizio Rilevamento anomalie. Per altre informazioni su cosa è possibile fare con questo servizio, vedere la [pagina del servizio Rilevamento anomalie](https://azure.microsoft.com/services/cognitive-services/anomaly-detector/).

## <a name="clean-up"></a>Eliminazione

È consigliabile, alla fine di un progetto, verificare se le risorse create sono ancora necessarie. L'esecuzione continua delle risorse può avere un costo. 

Se si continua con altri moduli di Concetti fondamentali sull'intelligenza artificiale, è possibile conservare le risorse per usarle in altri lab.

Se l'apprendimento è stato completato, è possibile eliminare il gruppo di risorse o le singole risorse dalla sottoscrizione di Azure:

1. Nel [portale di Azure](https://portal.azure.com/), nella pagina **Gruppi di risorse**, aprire il gruppo di risorse specificato durante la creazione della risorsa.

2. Fare clic su **Elimina gruppo di risorse**, digitare il nome del gruppo di risorse per confermare che si desidera eliminarlo e quindi selezionare **Elimina**. È anche possibile scegliere di eliminare le singole risorse selezionandole, facendo clic sui tre puntini di sospensione per visualizzare altre opzioni e quindi facendo clic su **Elimina**.