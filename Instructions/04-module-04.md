---
lab:
  title: Esplorare la funzionalità di analisi del testo
---

# <a name="explore-text-analytics"></a>Esplorare la funzionalità di analisi del testo

> **Nota** Per completare questo lab, è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

L'elaborazione del linguaggio naturale è un ramo dell'intelligenza artificiale che si occupa del linguaggio scritto o parlato. È possibile usare l'elaborazione del linguaggio naturale per creare soluzioni che estraggono il significato semantico dal testo o dal parlato voce o che formulano risposte significative in linguaggio naturale.

*Servizi cognitivi* di Microsoft Azure include le funzionalità di analisi del testo nel servizio *Lingua*, che offre alcune funzionalità predefinite di elaborazione del linguaggio naturale, tra cui l'identificazione delle frasi chiave nel testo e la classificazione del testo in base al sentiment.

Si supponga, ad esempio, che l'agenzia di viaggi fittizia *Margie's Travel* incoraggi i clienti a inviare recensioni per i soggiorni in hotel. È possibile usare il servizio Lingua per riepilogare le recensioni estraendo frasi chiave, determinare quali recensioni sono positive e quali sono negative o analizzare il testo della recensione per individuare le menzioni di entità note, ad esempio località o persone.

Per testare le funzionalità del servizio Lingua, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell. Gli stessi principi e funzionalità sono applicabili a soluzioni reali, ad esempio siti Web o app per smartphone.

## <a name="create-a-cognitive-services-resource"></a>Creare una risorsa per *Servizi cognitivi*

È possibile usare il servizio Lingua creando una risorsa **Lingua** o una risorsa **Servizi cognitivi**.

Se non è già stato fatto, creare una risorsa **Servizi cognitivi** nella sottoscrizione di Azure.

1. In un'altra scheda del browser aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Selezionare il pulsante **&#65291;Crea una risorsa**, cercare *Servizi cognitivi* e creare una risorsa di **Servizi cognitivi** con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare o creare un nuovo gruppo di risorse con un nome univoco*.
    - **Area**: *scegliere una qualsiasi area disponibile*.
    - **Nome**: *immettere un nome univoco*.
    - **Piano tariffario**: Standard S0
    - **Selezionando questa casella, confermo di aver letto e compreso tutte le condizioni seguenti**: selezionata.

1. Esaminare e creare la risorsa.

### <a name="get-the-key-and-endpoint-for-your-cognitive-services-resource"></a>Ottenere la chiave e l'endpoint per la risorsa Servizi cognitivi

1. Attendere il completamento della distribuzione. Passare quindi alla risorsa Servizi cognitivi e nella pagina **Panoramica** selezionare il collegamento per gestire le chiavi per il servizio. L'endpoint e le chiavi saranno necessari per connettersi alla risorsa Servizi cognitivi dalle applicazioni client.

1. Visualizzare la pagina **Chiavi ed endpoint** per la risorsa. Sarà necessario specificare la **chiave** e l'**endpoint** per la connessione dalle applicazioni client.

## <a name="run-cloud-shell"></a>Eseguire Cloud Shell

Per testare le funzionalità di analisi del testo del servizio Lingua, verrà usata una semplice applicazione da riga di comando eseguita in Cloud Shell in Azure.

1. Nel portale di Azure selezionare il pulsante **[>_]** (*Cloud Shell*) nella parte superiore della pagina a destra della casella di ricerca. Verrà aperto un riquadro di Cloud Shell nella parte inferiore del portale.

    ![Avviare Cloud Shell facendo clic sull'icona a destra della casella di ricerca in alto](media/analyze-text-language-service/powershell-portal-guide-1.png)

1. La prima volta che si apre Cloud Shell, è possibile che venga chiesto di scegliere il tipo di shell da usare (*Bash* o *PowerShell*). Selezionare **PowerShell**. Se questa opzione non viene visualizzata, ignorare il passaggio.  

1. Se viene chiesto di creare una risorsa di archiviazione per Cloud Shell, assicurarsi che sia specificata la sottoscrizione corretta e selezionare **Crea risorsa di archiviazione**. Attendere circa un minuto che la risorsa di archiviazione venga creata.

    ![Creare l'archiviazione facendo clic su Conferma.](media/analyze-text-language-service/powershell-portal-guide-2.png)

1. Verificare che nella parte superiore sinistra del riquadro Cloud Shell sia impostato *PowerShell* come tipo di shell. Se è *Bash*, passare a *PowerShell* usando il menu a discesa.

    ![Come trovare il menu a discesa a sinistra per passare a PowerShell](media/analyze-text-language-service/powershell-portal-guide-3.png)

1. Attendere l'avvio di PowerShell. Nel portale di Azure verrà visualizzata la schermata seguente:  

    ![Attendere l'avvio di PowerShell.](media/analyze-text-language-service/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>Configurare ed eseguire un'applicazione client

Ora che si dispone di un modello personalizzato, è possibile eseguire una semplice applicazione client che usa il servizio Lingua.

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

    ![Editor di codice.](media/analyze-text-language-service/powershell-portal-guide-4.png)

1. Nel riquadro **File** a sinistra espandere **ai-900** e selezionare **analyze-text.ps1**. Questo file contiene codice che usa il servizio Lingua:

    ![Editor contenente codice per l'uso del servizio Lingua](media/analyze-text-language-service/analyze-text-code.png)

1. Non prestare attenzione eccessiva ai dettagli del codice. Nel portale di Azure passare alla risorsa Servizi cognitivi. Selezionare quindi la pagina **Chiavi ed endpoint** nel riquadro a sinistra. Copiare la chiave e l'endpoint dalla pagina e incollarli nell'editor di codice, sostituendo rispettivamente i valori segnaposto **YOUR_KEY** e **YOUR_ENDPOINT**.

    > **Suggerimento** Potrebbe essere necessario usare la barra di separazione per regolare l'area dello schermo mentre si usano i riquadri **Chiavi ed endpoint** ed **Editor**.

    ![Trovare la scheda Chiavi ed endpoint nel riquadro sinistro della risorsa Servizi Cognitivi.](media/analyze-text-language-service/key-endpoint-support.png)

    Dopo aver sostituito i valori della chiave e dell'endpoint, le prime righe del codice dovrebbero essere simili a quanto segue:

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."
    $endpoint="https..."
    ```

1. In alto a destra nel riquadro dell'editor fare clic sul pulsante **...** per aprire il menu e selezionare **Salva** per salvare le modifiche. Aprire di nuovo il menu e selezionare **Close Editor**.

    L'applicazione client di esempio userà il servizio Lingua di Servizi cognitivi per rilevare la lingua, estrarre le frasi chiave, determinare il sentiment ed estrarre entità note per le recensioni.

1. In Cloud Shell immettere il comando seguente per eseguire il codice:

    ```PowerShell
    cd ai-900
    ./analyze-text.ps1 review1.txt
    ```

    Verrà esaminato questo testo:

    >Good Hotel and staff The Royal Hotel, London, UK 3/2/2018 Clean rooms, good service, great location near Buckingham Palace and Westminster Abbey, and so on. We thoroughly enjoyed our stay. The courtyard is very peaceful and we went to a restaurant which is part of the same group and is Indian ( West coast so plenty of fish) with a Michelin Star. We had the taster menu which was fabulous. The rooms were very well appointed with a kitchen, lounge, bedroom and enormous bathroom. Thoroughly recommended.

1. Esaminare l'output.

1. Nel riquadro di PowerShell immettere il comando seguente per eseguire il codice:

    ```PowerShell
    ./analyze-text.ps1 review2.txt
    ```

    Verrà esaminato questo testo:

    >Tired hotel with poor service The Royal Hotel, London, United Kingdom 5/6/2018 This is an old hotel (has been around since 1950's) and the room furnishings are average - becoming a bit old now and require changing. The internet didn't work and had to come to one of their office rooms to check in for my flight home. The website says it's close to the British Museum, but it's too far to walk.

1. Esaminare l'output.

1. Nel riquadro di PowerShell immettere il comando seguente per eseguire il codice:

    ```PowerShell
    ./analyze-text.ps1 review3.txt
    ```

    Verrà esaminato questo testo:

    >Good location and helpful staff, but on a busy road.
    The Lombard Hotel, San Francisco, USA 8/16/2018 We stayed here in August after reading reviews. We were very pleased with location, just behind Chestnut Street, a cosmopolitan and trendy area with plenty of restaurants to choose from. The Marina district was lovely to wander through, very interesting houses. Make sure to walk to the San Francisco Museum of Fine Arts and the Marina to get a good view of Golden Gate bridge and the city. On a bus route and easy to get into centre. Rooms were clean with plenty of room and staff were friendly and helpful. The only down side was the noise from Lombard Street so ask to have a room furthest away from traffic noise.

1. Esaminare l'output.

1. Nel riquadro di PowerShell immettere il comando seguente per eseguire il codice:

    ```PowerShell
    ./analyze-text.ps1 review4.txt
    ```

    Verrà esaminato questo testo:

    >Very noisy and rooms are tiny The Lombard Hotel, San Francisco, USA 9/5/2018 Hotel is located on Lombard street which is a very busy SIX lane street directly off the Golden Gate Bridge. Traffic from early morning until late at night especially on weekends. Noise would not be so bad if rooms were better insulated but they are not. Had to put cotton balls in my ears to be able to sleep--was too tired to enjoy the city the next day. Rooms are TINY. I picked the room because it had two queen size beds--but the room barely had space to fit them. With family of four in the room it was tight. With all that said, rooms are clean and they've made an effort to update them. The hotel is in Marina district with lots of good places to eat, within walking distance to Presidio. May be good hotel for young stay-up-late adults on a budget

1. Esaminare l'output.

## <a name="learn-more"></a>Altre informazioni

Questa semplice app mostra solo alcune delle funzionalità del servizio Lingua. Per altre informazioni su cosa è possibile fare con questo servizio, vedere la [pagina del servizio Lingua](https://azure.microsoft.com/services/cognitive-services/language-service/).
