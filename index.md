---
title: Istruzioni ospitate online
permalink: index.html
layout: home
---

# Esercizi su Elementi fondamentali di Azure per intelligenza artificiale

Questa repository contiene le esercitazioni pratiche per il corso Microsoft [AI-900 *Microsoft Azure per intelligenza artificiale*](https://docs.microsoft.com/it-it/learn/certifications/courses/ai-900t00) e i relativi moduli autogestiti su Microsoft Learn: [Introduzione all'intelligenza artificiale in Azure](https://docs.microsoft.com/learn/paths/get-started-with-artificial-intelligence-on-azure/), [Creare modelli predittivi senza codice con Azure Machine Learning](https://docs.microsoft.com/it-it/learn/paths/create-no-code-predictive-models-azure-machine-learning/), [Esplorare la visione artificiale in Microsoft Azure](https://docs.microsoft.com/learn/paths/explore-computer-vision-microsoft-azure/), [Esplorare l’elaborazione del linguaggio naturale](https://docs.microsoft.com/learn/paths/explore-natural-language-processing/) e [Esplorare l'intelligenza artificiale per la conversazione](https://docs.microsoft.com/learn/paths/explore-conversational-ai/). Gli esercizi si integrano con i materiali di formazione e permettono di fare pratica con le tecnologie descritte. 

Per completare gli esercizi, è necessaria una sottoscrizione a Microsoft Azure. Se non è stata fornita dal docente, puoi registrare un account gratuito alla pagina [https://azure.microsoft.com/it-it/](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Esercizi |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
