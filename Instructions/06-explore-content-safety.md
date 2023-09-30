Content Safety Studio consente di esplorare il modo in cui è possibile moderare il contenuto di testo e immagine. È possibile eseguire test su testo o immagini di esempio e ottenere un punteggio di gravità compreso tra sicuro e alto per ogni categoria. È possibile scoprire rapidamente il funzionamento del servizio Content Safety AI e le funzionalità di cui è in grado. 

In questo esercizio del lab si creerà una risorsa di Servizi di intelligenza artificiale di Azure multiservizio nel portale di Azure ed esaminare l'endpoint e le chiavi. Si userà quindi Content Safety Studio per esplorare le funzionalità del servizio Content Safety AI. 

## Creare una risorsa di Servizi di intelligenza artificiale

1.  In un'altra scheda del browser aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com?azure-portal=true), eseguendo l'accesso con l'account Microsoft.
1.  Fare clic sul pulsante ** crea una risorsa&#65291;** e cercare *i servizi di intelligenza artificiale di Azure*. Selezionare **Crea** un piano **di servizi di intelligenza artificiale di Azure** . Verrà visualizzata una pagina per creare una risorsa dei servizi di intelligenza artificiale di Azure. Configurarlo con le impostazioni seguenti:
- **Sottoscrizione** La sottoscrizione di Azure.
- **Gruppo di risorse**: selezionare o creare un gruppo di risorse appropriato.
- **Area**: scegliere qualsiasi area disponibile.
- **Nome**: immettere un nome univoco.
- **Piano tariffario**: F0 
2.  Esaminare e creare la risorsa e attendere il completamento della distribuzione. 

## Associare la risorsa a Content Safety Studio 
In una scheda del browser separata aprire Content Safety Studio ed eseguire l'accesso. Viene visualizzata la schermata Attività iniziali.

1.  Fare clic sull'ingranaggio Impostazioni nel menu in alto a destra.
2.  Selezionare la risorsa del servizio Intelligenza artificiale di Azure appena creata e quindi fare clic su Usa risorsa.
3.  Visualizzare l'endpoint e la chiave per la risorsa, scorrere, se necessario. Se si archivia il portale di Azure, si noterà che si tratta dell'endpoint e della chiave per la risorsa che mostra che la risorsa è stata associata correttamente a Content Safety Studio.
4.  Fare clic su Content Safety Studio per tornare alla home page. In Moderazione del contenuto del testo fare clic su Prova.
5.  In Eseguire un semplice test fare clic su Contenuto sicuro. Si noti che il testo viene visualizzato nella casella seguente. 
6.  Fare clic su Run test(Esegui test). 
7.  Nel pannello Risultati esaminare i risultati. Esistono quattro livelli di gravità da sicuri ad alto e quattro tipi di contenuto dannoso. Il servizio Content Safety AI considera l'esempio accettabile o meno? 
8.  Provare ora un altro esempio. Selezionare il testo in Contenuto violento con errori di ortografia. Controllare che il contenuto sia visualizzato nella casella seguente.
9.  Fare clic su Esegui test ed esaminare i risultati nel pannello Risultati seguente. Questo esempio è accettabile? In caso contrario, perché no?

È possibile eseguire test su tutti gli esempi forniti, quindi esaminare i risultati.

Al termine, eliminare la risorsa dei servizi di intelligenza artificiale di Azure nel portale di Azure. 
