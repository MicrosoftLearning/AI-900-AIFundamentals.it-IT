---
title: Istruzioni online
permalink: index.html
layout: home
ms.openlocfilehash: b85af520a10e63a2f9a5696db03bfd946aff968f
ms.sourcegitcommit: 1ef64e3008a439d0d0bb3d93a27d3df68d3d64a9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/17/2022
ms.locfileid: "140688693"
---
# <a name="azure-ai-fundamentals-exercises"></a>Esercizi su Elementi fondamentali di Azure per intelligenza artificiale

Usare i collegamenti seguenti per completare gli esercizi dei lab pratici per il corso Microsoft [AI-900 *Concetti fondamentali su Microsoft Azure per intelligenza artificiale*](https://docs.microsoft.com/learn/certifications/courses/ai-900t00).

Per completare gli esercizi, è necessaria una sottoscrizione a Microsoft Azure. Se non è stata fornita dal docente, è possibile iscriversi a una versione di valutazione gratuita in [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Esercizi |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
