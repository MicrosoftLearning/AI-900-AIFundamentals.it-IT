## Sviluppo locale 

Se stai lavorando sul tuo computer locale, puoi seguire questi passaggi per configurare il tuo ambiente e lavorare con i laboratori.  

### C++ Redistributable 
1. Scarica e installa il [Visual C++ Redistributable (x64)](https://aka.ms/vs/16/release/vc_redist.x64.exe) 

### Python e pacchetti necessari 
1. Installa [Python 3.6.1](https://www.python.org/downloads/release/python-361/)  
   - **Importante**: seleziona le opzioni per aggiungere Python alla variabile PATH e per registrarlo come ambiente Python predefinito 
2. Dopo l'installazione, apri il *Prompt dei comandi* e inserisci il comando seguente per installare i pacchetti necessari: 

> pip install ipython jupyter matplotlib pillow richiede azure-cognitiveservices-vision-computervision azure-cognitiveservices-vision-customvision azure-cognitiveservices-vision-face azure-cognitiveservices-language-textanalytics azure.cognitiveservices.speech azure_ai_formrecognizer 

### Visual Studio Code 
1. Se non Visual Studio Code non è già disponibile, [scaricarlo qui](https://code.visualstudio.com/Download). Dopo l'installazione, avviare Visual Studio Code e nella scheda Estensioni (CTRL+MAIUSC+X), cercare e installare l'estensione **Python** da Microsoft.

2. In Visual Studio Code, apri un nuovo terminale, digita **git clone https://github.com/MicrosoftLearning/AI-900IT-Microsoft-Azure-AI-Fundamentals** e seleziona *invio*. 

