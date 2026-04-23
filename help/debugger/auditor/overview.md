---
title: Onglet Auditeur
description: Découvrez comment utiliser l’onglet Auditor dans Adobe Experience Platform Debugger pour tester vos implémentations Adobe Experience Cloud.
keywords: debugger;extension experience platform debugger;chrome;extension;auditor;dtm;target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 32%

---

# Onglet Auditeur

Dans Adobe Experience Platform Debugger, vous pouvez utiliser l’onglet **[!UICONTROL Auditor]** pour exécuter une série de tests d’audit sur votre page.

Pour utiliser cette fonctionnalité :

1. Sélectionnez **[!UICONTROL Auditor]** dans le volet de navigation de gauche.
1. Sélectionnez **[!UICONTROL Run Auditor Tests]**. Une fois les tests terminés, leurs résultats apparaissent ci-dessous.

![Capture d’écran des résultats du test dans l’onglet Auditor](../images/auditor-results.png)

La liste des résultats contient le test et son résultat, ainsi que des suggestions pour résoudre les problèmes éventuels.

## Interprétation des résultats des tests

Chaque test est pondéré et votre score de test est égal au poids attribué. Si vous réussissez un test avec un poids de 5, vous recevez cinq points.

| Score | Description |
| --- | --- |
| 0 | Vous avertit des problèmes que vous devez connaître, mais n’affectez pas votre score. |
| 1 | Recommande une optimisation. Aucune incidence sur la précision des données. |
| 2 | L’échec de ce test signifie que vous n’aurez pas accès aux dernières fonctionnalités et correctifs de Adobe Experience Cloud. |
| 3 | Tests d’efficacité et de respect des bonnes pratiques lors de la mise en œuvre. |
| 4 | L’échec signifie que vous collectez peut-être des données non fiables. |
| 5 | Un échec peut entraîner une perte de données. |

Tous les tests ont réussi ou échoué. Ils vérifient la conformité ou la non-conformité aux conditions de test. Il n’existe pas de score partiel pour une conformité partielle. Par exemple, si le test vérifie la version la plus récente d’une solution Adobe et que vous n’avez qu’une version de retard, vous obtenez le même score que si vous aviez cinq versions de retard. Les versions les plus récentes incluent des améliorations des performances et des correctifs de bugs. Il est donc recommandé d’utiliser la version la plus récente.

Il est **vivement recommandé** de corriger les résultats de niveau 4 ou 5.

Il est **recommandé** de corriger les résultats de niveau 1 à 3.

## Technologies Adobe prises en charge

La fonction d’audit peut évaluer les technologies Adobe suivantes :

* Adobe Advertising DSP
* Recherche Adobe Advertising
* Adobe Analytics
* Service d’identités d’Adobe Experience Cloud
* Adobe Target
* Balises (anciennement Adobe Experience Platform Launch)

## Schémas de test

Pour plus d’informations sur les structures de test fournies par cette fonctionnalité, reportez-vous aux documents suivants :

* [Cohérence des balises](./tag-consistency.md)
* [Présence des balises](./tag-presence.md)
* [Configuration](./configuration.md)
* [Alertes](./alerts.md)
