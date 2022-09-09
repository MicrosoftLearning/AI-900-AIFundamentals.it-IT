---
title: Istruzioni online
permalink: index.html
layout: home
ms.openlocfilehash: 86fa2da9bfa9e4d7edb0c853f77e95fe69e97411
ms.sourcegitcommit: 3fc8440b350b498c2f50ab4ce531a0f906792584
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2022
ms.locfileid: "147866007"
---
# <a name="azure-ai-fundamentals-exercises"></a>Esercizi su Elementi fondamentali di Azure per intelligenza artificiale

Questi esercizi pratici sono progettati a supporto del contenuto di training in [Microsoft Learn](https://docs.microsoft.com/training/).

Per completare gli esercizi, è necessaria una sottoscrizione a Microsoft Azure. È possibile iscriversi per una versione di valutazione gratuita all’indirizzo [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Esercizi |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
