---
lab:
  title: Esplorare la funzionalità di risposta alle domande
---

# Esplorare la funzionalità di risposta alle domande

> **Nota:** per completare questo lab è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free?azure-portal=true) in cui si ha accesso amministrativo.

Per gli scenari di assistenza ai clienti, è comune creare un bot in grado di interpretare e rispondere alle domande frequenti tramite una finestra di chat del sito Web, un messaggio di posta elettronica o un'interfaccia vocale. Alla base dell'interfaccia del bot si trova una knowledge base di domande e risposte appropriate nella quale il bot può cercare risposte appropriate.

## Creare una knowledge base personalizzata di risposta alla domanda

La funzionalità di risposta alla domanda personalizzata del servizio Lingua consente di creare rapidamente una knowledge base, immettendo coppie di domande e risposte o da un documento o da una pagina Web esistente. Può quindi usare alcune capacità di elaborazione del linguaggio naturale predefinite per interpretare le domande e trovare le risposte appropriate.

1. Aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.

1. Fare clic sul pulsante **&#65291;Crea una risorsa**, cercare *Servizio Lingua* e creare una risorsa **Servizio Lingua** con le impostazioni seguenti, quindi fare clic su **Continua a creare la risorsa**: **Seleziona funzionalità aggiuntive**
    - **Funzionalità predefinite**: *mantenere le funzionalità predefinite*.
    - **Funzionalità personalizzate**: *selezionare Risposta personalizzata alle domande*.

    ![Creazione di una risorsa Servizio Lingua con la risposta personalizzata alle domande abilitata.](media/create-a-bot/create-language-service-resource.png)

1. Nella pagina **Crea Lingua** specificare le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *selezionare un gruppo di risorse esistente o crearne uno nuovo*.
    - **Nome**: *specificare un nome univoco per la risorsa Lingua*.
    - **Piano tariffario**: S (1.000 chiamate al minuto).
    - **Area di Ricerca di Azure**: *qualsiasi località disponibile*.
    - **Piano tariffario di Ricerca di Azure**: Gratuito F (3 indici) - (*Se questo livello non è disponibile, selezionare Standard S (50 indici)*).
    - **Selezionando questa casella, dichiaro di conoscere e confermare tutti i termini indicati nei nostri principi di intelligenza artificiale responsabile**: *selezionata*.

    > **Nota:** se è già stato effettuato il provisioning della risorsa **Ricerca cognitiva di Azure** di livello gratuito, la quota potrebbe non consentire di crearne un'altra. In questo caso, selezionare un livello diverso da **Gratuito F**.

1. Fare clic su **Rivedi e crea** e quindi su **Crea**. Attendere il completamento della distribuzione del servizio Lingua che supporterà la knowledge base della funzionalità di risposta alla domanda personalizzata.

1. In una nuova scheda del browser aprire il portale Language Studio all'indirizzo [https://language.azure.com](https://language.azure.com?azure-portal=true) e accedere usando l'account Microsoft associato alla sottoscrizione di Azure.

1. Se viene richiesto di scegliere una risorsa del servizio Lingua, selezionare le impostazioni seguenti:
    - **Directory di Azure**: directory di Azure contenente la sottoscrizione.
    - **Sottoscrizione di Azure**: sottoscrizione di Azure in uso.
    - **Language resource** (Risorsa Lingua): risorsa del servizio Lingua creata in precedenza.

1. Se ***non*** viene chiesto di scegliere una risorsa Lingua, è possibile che nella sottoscrizione siano presenti più risorse di questo tipo e in tal caso:
    1. Sulla barra nella parte superiore della pagina fare clic sul pulsante **Impostazioni (&#9881;)**.
    2. Nella pagina **Impostazioni** visualizzare la scheda **Risorse**.
    3. Selezionare la risorsa del servizio Lingua appena creata e fare clic su **Cambiare risorsa**.
    4. Nella parte superiore della pagina fare clic su **Language Studio** per tornare alla pagina iniziale di Language Studio.

1. Nella parte superiore del portale di Language Studio scegliere **Risposta personalizzata alle domande** dal menu **Crea nuovo**.

1. Nella pagina **Scegli l'impostazione della lingua per la risorsa *nome della risorsa*** selezionare **Seleziona la lingua quando si crea un progetto in questa risorsa** e fare clic su **Avanti**.

1. Nella pagina **Enter basic information** (Immetti informazioni di base) immettere i dati seguenti e fare clic su **Avanti**:
    - **Risorsa Lingua**: *scegliere la risorsa Lingua*.  
    - **Risorsa Ricerca di Azure**: *scegliere la risorsa Ricerca di Azure*.
    - **Nome**: MargiesTravel
    - **Descrizione**: knowledge base semplice
    - **Lingua di origine**: inglese
    - **Risposta predefinita quando non viene restituita alcuna risposta**: Nessuna risposta trovata

1. Nella pagina **Rivedere e completare** fare clic su **Crea progetto**.

1. Verrà visualizzata la pagina **Gestisci origini**. Fare clic su **&#65291;Aggiungi origine** e selezionare **URL**.

1. Nella casella **Aggiungi URL** fare clic su **+ Aggiungi URL**. Digitare quanto segue e selezionare **Aggiungi tutto**:
    - **Nome URL**: MargiesKB
    - **URL**: `https://raw.githubusercontent.com/MicrosoftLearning/AI-900-AIFundamentals/main/data/qna/margies_faq.docx`
    - **Classifica struttura file**: *Rilevamento automatico* 

## Modificare la knowledge base

La knowledge base si basa sui dettagli nel documento delle domande frequenti e su alcune risposte predefinite. È possibile aggiungere coppie di domande e risposte personalizzate per integrare questi dati.

1. Fare clic su **Modifica knowledge base** nel pannello a sinistra. Fare quindi clic su **+ Aggiungi coppia di domande**.

1. Nella casella **Domande** digitare `Hello` e quindi fare clic su **Invia modifiche**.

1. Fare clic su **+ Aggiungi frase alternativa** e digitare `Hi`, quindi fare clic su **Invia modifiche**.

1. Nella casella **Risposta e richieste** digitare `Hello`. Mantenere **Origine**: Editoriale.

1. Fare clic su **Invia**. In alto nella pagina fare quindi clic su **Salva modifiche**. Potrebbe essere necessario modificare le dimensioni della finestra per visualizzare il pulsante.

## Eseguire il training e il test della knowledge base

Ora che è stata creata una knowledge base, è possibile testarla.

1. Nella parte superiore della pagina fare clic su **Test** per testare la knowledge base.

1. Nella parte inferiore del riquadro di test immettere il messaggio *Hi*. Dovrebbe essere restituita la risposta **Hello**.

1. Nel riquadro di test, in basso, immettere il messaggio *I want to book a flight*. Dovrebbe essere restituita una risposta appropriata dalle domande frequenti.

    > **Nota:** la risposta include una *risposta breve* oltre a un *passaggio di risposta* più dettagliato: il passaggio di risposta mostra il testo completo nel documento delle domande frequenti per la domanda più simile, mentre la risposta breve viene estratta in modo intelligente dal passaggio. È possibile controllare se la risposta breve proviene dalla risposta usando la casella di controllo **Visualizza risposta breve** nella parte superiore del riquadro di test.

1. Provare un'altra domanda, ad esempio *How can I cancel a reservation?*

1. Al termine del test della knowledge base, fare clic su **Test** per chiudere il riquadro di test.

## Creare un bot per la knowledge base

La knowledge base offre un servizio back-end che le applicazioni client possono usare per rispondere alle domande tramite una qualche forma di interfaccia utente. In genere, queste applicazioni client sono bot. Per rendere la knowledge base disponibile per un bot, è necessario pubblicarla come servizio accessibile tramite HTTP. È quindi possibile usare il servizio Azure Bot per creare e ospitare un bot che usa la knowledge base per rispondere alle domande dell'utente.

1. A sinistra della pagina di Language Studio fare clic su **Distribuisci knowledge base**.

1. Nella parte superiore della pagina fare clic su **Distribuisci**. Una finestra di dialogo chiederà se si vuole distribuire il progetto. Seleziona **Distribuisci**.

1. Dopo aver distribuito il servizio, fare clic su **Crea un bot**. Verrà aperto il portale di Azure in una nuova scheda del browser, dove è possibile creare un bot per app Web nella sottoscrizione di Azure in uso.

1. Nel portale di Azure, creare una bot per app Web. È possibile che venga visualizzato un messaggio di avviso per verificare che l'origine del modello sia attendibile. Non è necessario eseguire alcuna azione per il messaggio. Continuare aggiornando le impostazioni seguenti:

    - **Dettagli del progetto**
        - **Sottoscrizione**: *la sottoscrizione di Azure usata*
        - **Gruppo di risorse**: *gruppo di risorse contenente la risorsa Lingua*
    - **Dettagli istanza**
        - **Posizione del gruppo di risorse**: *la stessa posizione del servizio Lingua*.
    - **Azure Bot**
        - **Handle di bot**: *nome univoco per il bot* (*pre-popolato*)
    - **Scegliere il piano tariffario**
        - **Piano tariffario**: gratuito F0 (potrebbe essere necessario selezionare *Cambia piano*).
    - **ID app Microsoft**
        - **Tipo di creazione**: *selezionare Crea nuova identità gestita assegnata dall'utente* 

5. Selezionare **Avanti: App Web >** per continuare ad aggiornare le impostazioni. 
    - **Servizio app**
        - **Nome dell'app**: *uguale a **Handle di bot** con **.azurewebsites.net** aggiunto automaticamente*
        - **Lingua dell'SDK**: *scegliere C# o Node.js*
    - **Piano di servizio app**
        - **Tipo di creazione**: *selezionare Create new app service plan (Crea nuovo piano di servizio app)*
    - **Impostazioni app**
        - **Chiave risorsa Lingua**: *è necessario copiare la chiave della risorsa Lingua e incollarla qui.* 
        
        > **Nota:** per passare alla chiave della risorsa Lingua, aprire [https://portal.azure.com](https://portal.azure.com?azure-portal=true). Nella pagina iniziale fare clic su *Gruppi di risorse* e individuare il gruppo di risorse in cui è stata creata la risorsa Lingua. Selezionare la risorsa Lingua e passare al relativo menu a sinistra. Selezionare *Chiavi ed endpoint*. Copiare una delle chiavi. 

    -  
        - **Nome progetto della lingua**: MargiesTravel
        - **Nome host dell'endpoint di servizio della lingua**: *pre-popolato con l'endpoint di servizio della lingua*
    - **Dettagli del servizio della lingua**
        - **ID sottoscrizione**: *pre-popolato con il proprio ID sottoscrizione*
        - **Nome gruppo di risorse**: *pre-popolato con il proprio nome del gruppo di risorse.*
        - **Nome dell'account**: *pre-popolato con il nome della risorsa*

1. Selezionare **Rivedi e crea**.

1. Attendere che il bot venga creato (l'icona di notifica a forma di campana in alto a destra si muove durante l'attesa). Quindi, nella notifica di completamento della distribuzione, fare clic su **Vai alla risorsa** (oppure in alternativa, sulla pagina iniziale, fare clic su **Gruppi di risorse**, aprire il gruppo di risorse in cui è stato creato il bot per app Web e selezionarlo.)

1. Nel riquadro sinistro del bot cercare **Impostazioni**, fare clic su **Test in chat Web** e attendere che il bot visualizzi il messaggio **Hello and Welcome** (l'inizializzazione potrebbe richiedere alcuni secondi).

1. Usa l'interfaccia della chat di test per assicurarti che il bot risponda alle domande dalla tua knowledge base come previsto. Ad esempio, provare a inviare *I need to cancel my hotel*.

Sperimentare l'uso del bot. Probabilmente si noterà che può rispondere alle domande disponibili nelle domande frequenti in modo abbastanza accurato, ma avrà una capacità limitata di interpretare le domande per cui non è stato sottoposto a training. È sempre possibile usare Language Studio per modificare la knowledge base per migliorarla e ripubblicarla.

## Altre informazioni

- Per altre informazioni sul servizio di risposta alla domanda, vedere la [documentazione](https://docs.microsoft.com/azure/cognitive-services/language-service/question-answering/overview).
- Per altre informazioni sul servizio Bot Microsoft, vedere [la pagina del servizio Azure Bot](https://azure.microsoft.com/services/bot-service/).
