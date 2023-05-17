---
title: Istruzioni online
permalink: index.html
layout: home
---

# <a name="azure-ai-fundamentals-exercises"></a>Esercizi su Elementi fondamentali di Azure per intelligenza artificiale

Questi esercizi pratici sono progettati a supporto del contenuto di training in [Microsoft Learn](https://docs.microsoft.com/training/).

Per completare gli esercizi, è necessaria una sottoscrizione a Microsoft Azure. È possibile iscriversi per una versione di valutazione gratuita all’indirizzo [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions'" %}
| Esercizi |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
