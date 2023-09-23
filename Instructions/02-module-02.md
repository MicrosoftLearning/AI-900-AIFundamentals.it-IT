---
lab:
  title: Esplorare la funzionalità di Machine Learning automatizzato in Azure ML
---

# Esplorare la funzionalità di Machine Learning automatizzato in Azure ML

In questo esercizio si userà la funzionalità di Machine Learning automatizzata in Azure Machine Learning per eseguire il training e valutare un modello di Machine Learning. Verrà quindi distribuito e testato il modello sottoposto a training.

Questo esercizio deve richiedere circa **30** minuti per completare.

> **Nota** Per completare questo lab, è necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) in cui si ha accesso amministrativo.

## Creare un'area di lavoro di Machine Learning di Azure

Per usare Azure Machine Learning, è necessario effettuare il provisioning di un'area di lavoro di Azure Machine Learning nella sottoscrizione di Azure. Sarà quindi possibile usare studio di Azure Machine Learning per usare le risorse nell'area di lavoro.

> **Suggerimento**: se si dispone già di un'area di lavoro di Azure Machine Learning, è possibile usarla e passare all'attività successiva.

1. Accedere al [portale di Azure](https://portal.azure.com) `https://portal.azure.com` usando le credenziali Microsoft.

1. Selezionare **+ Creare una risorsa**, cercare *Machine Learning* e creare una nuova risorsa di **Azure Machine Learning** con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure usata*.
    - **Gruppo di risorse**: *creare o selezionare un gruppo di risorse*.
    - **Nome**: *immettere un nome univoco per l'area di lavoro*.
    - **Area**: *selezionare l'area geografica più vicina*.
    - **Account di archiviazione**: *prendere nota del nuovo account di archiviazione predefinito che verrà creato per l'area di lavoro*.
    - **Insieme di credenziali delle chiavi**: *prendere nota del nuovo insieme di credenziali delle chiavi predefinito che verrà creato per l'area di lavoro*.
    - **Application Insights**: *prendere nota della nuova risorsa Application Insights predefinita che verrà creata per l'area di lavoro*.
    - **Registro contenitori**: Nessuno (*ne verrà creato uno automaticamente la prima volta che si distribuisce un modello in un contenitore*).

1. Selezionare **Rivedi e crea** e quindi **Crea**. Attendere che l'area di lavoro venga creata (l'operazione può richiedere alcuni minuti) e quindi passare alla risorsa distribuita.

1. Selezionare **Avvia studio** (in alternativa, aprire una nuova scheda nel browser e passare a [https://ml.azure.com](https://ml.azure.com?azure-portal=true)) e accedere allo studio di Azure Machine Learning usando il proprio account Microsoft. Chiudere tutti i messaggi visualizzati.

1. Nello studio di Azure Machine Learning verrà visualizzata l'area di lavoro appena creata. In caso contrario, selezionare **Tutte le aree di lavoro** nel menu a sinistra e selezionare l'area di lavoro appena creata.

## Abilitare le funzionalità di anteprima

Alcune funzionalità di Azure Machine Learning sono in anteprima e devono essere abilitate in modo esplicito nell'area di lavoro.

1. In Azure Machine Learning Studio fare clic su **Gestisci funzionalità di anteprima** (icona a voce alta - &#128363;).

    ![Screenshot del pulsante Gestisci funzionalità di anteprima nel menu.](../instructions/media/use-automated-machine-learning/severless-compute-1.png)

1. Abilitare la funzionalità di anteprima seguente:

    - *Esperienza guidata per l'invio di processi di training con calcolo serverless*

## Usare Machine Learning automatizzato per eseguire il training di un modello

Machine Learning automatizzato consente di provare più algoritmi e parametri per eseguire il training di più modelli e identificare quello migliore per i dati. In questo esercizio si userà un set di dati dei dettagli del noleggio di biciclette cronologici per eseguire il training di un modello che stima il numero di noleggio biciclette che dovrebbe essere previsto in un determinato giorno, in base alle caratteristiche stagionali e meteorologiche.

> **Citazione**: *i dati usati in questo esercizio sono derivati da [Capital Bikeshare](https://www.capitalbikeshare.com/system-data) e vengono usati in conformità al [contratto di licenza](https://www.capitalbikeshare.com/data-license-agreement) dei dati pubblicati*.


1. In [studio di Azure Machine Learning](https://ml.azure.com?azure-portal=true) visualizzare la pagina **Machine Learning automatizzata** (in **Creazione**).

1. Creare un nuovo processo di Machine Learning automatizzato con le impostazioni seguenti, usando **Avanti** in base alle esigenze per eseguire l'avanzamento tramite l'interfaccia utente:

    **Impostazioni di base**:

    - **Nome processo**: mslearn-bike-automl
    - **Nome nuovo esperimento**: mslearn-bike-rental
    - **Descrizione**: Machine Learning automatizzato per la stima del noleggio di biciclette
    - **Tag**: *nessuno*

   **Tipo di attività & dati**:

    - **Selezionare il tipo di attività: Regressione**
    - **Selezionare il set di dati**: Creare un nuovo set di dati con le impostazioni seguenti:
        - **Tipo di dati**:
            - **Nome**: noleggi di biciclette
            - **Descrizione**: Dati di noleggio biciclette storici
            - **Tipo**: tabulare
        - **Origine dati**:
            - Selezionare **da file Web**
        - **Web URL** (URL Web): 
            - **Web URL** (URL Web): `https://aka.ms/bike-rentals`
            - **Ignora convalida dei dati**: *non selezionare*
        - **Impostazioni**:
            - **Formato di file**: delimitato
            - **Delimitatore**: virgola
            - **Codifica**: UTF-8
            - **Intestazioni colonna**: solo il primo file ha intestazioni
            - **Ignora righe**: Nessuno
            - **Il set di dati contiene dati su più righe**: *non selezionare*
        - **Schema**:
            - Includi tutte le colonne diverse da **Path**
            - Rivedi i tipi rilevati automaticamente

        Selezionare il set di dati **bike-rentals** dopo averla creata.

    **Impostazioni attività**:

    - **Tipo di attività**: Regressione
    - **Set di dati**: noleggi di biciclette
    - **Colonna di destinazione**: Noleggi (integer)
    - **Impostazioni di configurazione aggiuntive**:
        - **Metrica primaria**: Errore quadratico medio normalizzato
        - **Spiegare il modello migliore**: *Non selezionato*
        - **Usare tutti i modelli supportati**: <u>deselezionato</u>. *Durante il processo si proveranno solo alcuni algoritmi specifici.*
        - **Modelli consentiti**: *selezionare solo **RandomForest** e **LightGBM**. Normalmente si vorrà provare il maggior numero possibile di modelli, ma ogni modello aggiunto aumenta il tempo necessario per eseguire il processo.*
    - **Limiti**: *Espandere questa sezione*
        - **Numero massimo di prove**: 3
        - **Numero massimo di prove simultanee**: 3
        - **Numero massimo di nodi**: 3
        - **Soglia di punteggio metrica**: *0,85 (in modo che se un modello ottiene un punteggio di metrica di errore quadratico quadratico normalizzato pari a 0,085 o minore, il processo termina.*
        - **Timeout**: 15
        - **Timeout iterazione**: 5
        - **Abilitare la terminazione anticipata**: *selezionata*
    - **Convalida e test**:
        - **Tipo di convalida**: suddivisione tra training e convalida
        - **Percentuale di dati di convalida**: 10
        - **Set di dati di test**: Nessuno

    **Compute**:

    - **Selezionare il tipo di calcolo**: Serverless
    - **Tipo di macchina virtuale**: CPU
    - **Livello macchina virtuale**: priorità bassa
    - **Dimensioni della macchina virtuale**: Standard_DS3_V2
    - **Numero di istanze**: 1

1. Inviare il processo di training. Viene avviato automaticamente.

1. Attendere il completamento del processo. L'operazione potrebbe richiedere un po' di tempo.

## Esaminare il modello migliore

Al termine del processo di Machine Learning automatizzato, è possibile esaminare il modello migliore sottoposto a training.

1. Nella scheda **Panoramica** del processo di Machine Learning automatizzato prendere nota del riepilogo del modello migliore.
    ![Screenshot del riepilogo del modello migliore del processo di Machine Learning automatizzato con una casella attorno al nome dell'algoritmo.](media/use-automated-machine-learning/complete-run.png)

    > **Nota** È possibile che venga visualizzato un messaggio nello stato "Avviso: punteggio di uscita specificato dall'utente raggiunto...". Si tratta di un messaggio previsto. Continuare con il passaggio successivo.
  
1. Selezionare il testo in **Nome dell'algoritmo** per il modello migliore per visualizzarne i dettagli.

1. Selezionare la scheda **Metriche** e selezionare i grafici **residui** e **predicted_true**, se non sono già selezionati. 

    Esaminare i grafici che mostrano le prestazioni del modello. Il grafico dei residui mostra i **residui** (le differenze tra i valori *stimati* e effettivi) come istogramma. Il grafico **predicted_true** confronta i valori stimati rispetto ai valori true. 

## Distribuire e testare il modello

1. Nella scheda **Modello** per il modello migliore sottoposto a training dal processo di Machine Learning automatizzato selezionare **Distribuisci** e usa l'opzione **Servizio Web** per distribuire il modello con le impostazioni seguenti:
    - **Nome**: previsione-noleggi
    - **Descrizione**: prevedere i noleggi di biciclette
    - **Tipo di ambiente di calcolo**: Istanza di Azure Container
    - **Abilitare l'autenticazione**: *selezionata*

1. Attendere l'avvio della distribuzione. L'operazione potrebbe richiedere alcuni secondi. Lo **stato Di distribuzione** per l'endpoint **predict-rentals** verrà indicato nella parte principale della pagina come *In esecuzione*.
1. Attendere che lo **stato Distribui** venga modificato *in Successed*. Questo può richiedere 5-10 minuti.

## Testare il servizio distribuito

A questo punto è possibile testare il servizio distribuito.

1. In studio di Azure Machine Learning, nel menu a sinistra selezionare **Endpoint** e aprire l'endpoint in tempo reale **predict-rentals**.

1. Nella pagina dell'endpoint **predict-rentals** in tempo reale visualizzare la scheda **Test** .

1. Nel riquadro **Dati di input per testare l'endpoint** sostituire il modello JSON con i dati di input seguenti:

    ```JSON
    {
      "Inputs": { 
        "data": [
          {
            "day": 1,
            "mnth": 1,   
            "year": 2022,
            "season": 2,
            "holiday": 0,
            "weekday": 1,
            "workingday": 1,
            "weathersit": 2, 
            "temp": 0.3, 
            "atemp": 0.3,
            "hum": 0.3,
            "windspeed": 0.3 
          }
        ]    
      },   
      "GlobalParameters": 1.0
    }
    ```

1. Fare clic sul pulsante **Test**.

1. Esaminare i risultati del test, che includono un numero stimato di noleggi in base alle funzionalità di input, simile al seguente:

    ```JSON
    {
      "Results": [
        444.27799000000000
      ]
    }
    ```

    Il riquadro di test ha considerato i dati di input e ha usato il modello sottoposto a training per restituire il numero stimato di noleggi.


Di seguito vengono descritte le operazioni eseguite. È stato usato un set di dati cronologici relativi al noleggio di biciclette per eseguire il training di un modello. Il modello stima il numero di noleggi di biciclette previsti in un determinato giorno, in base a *caratteristiche* stagionali e meteorologiche.

## Eliminazione

Il servizio Web creato è ospitato in un'*Istanza di contenitore di Azure*. Se non si vogliono eseguire altri esperimenti con tale servizio, è consigliabile eliminare l'endpoint per evitare di accumulare tempi di utilizzo superflui per Azure. È anche necessario eliminare il cluster di calcolo.

1. In [Azure Machine Learning Studio](https://ml.azure.com?azure-portal=true) nella scheda **Endpoint** selezionare l'endpoint **previsione-noleggi**. Selezionare quindi **Elimina** e confermare l'eliminazione dell'endpoint.

    L'eliminazione del calcolo garantisce che la sottoscrizione non venga addebitata per le risorse di calcolo. Verrà tuttavia addebitato un importo ridotto per l'archiviazione dei dati, fintanto che l'area di lavoro di Azure Machine Learning è presente nella sottoscrizione. Se è stata completata l'esplorazione di Azure Machine Learning, è possibile eliminare l'area di lavoro di Azure Machine Learning e le risorse associate.

Per eliminare l'area di lavoro:

1. Nel [portale di Azure](https://portal.azure.com?azure-portal=true), nella pagina **Gruppi di risorse**, aprire il gruppo di risorse specificato durante la creazione dell'area di lavoro di Azure Machine Learning.
2. Fare clic su **Elimina gruppo di risorse**, digitare il nome del gruppo di risorse per confermare che si vuole eliminarlo e quindi selezionare **Elimina**.
