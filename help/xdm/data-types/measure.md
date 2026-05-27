---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;mesure;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de mesure
description: Découvrez le type de données du modèle de données d’expérience de mesure (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
TQID: https://experienceleague.adobe.com/aNvqpcpEDybeIUE1pUW3hPE20hPIVcwnLyKa7x1v5sk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 5%

---

# Type de données [!UICONTROL Measure]

[!UICONTROL Measure] est un type de données standard du modèle de données d’expérience (XDM) qui contient un point de données quantifiable concret d’une mesure particulière. Une mesure est composée d’un identifiant unique et d’une valeur.

![mesurer l’image](../images/data-types/measure.PNG){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `id` | Chaîne | Identifiant unique de cette mesure. Dans le cas de la collecte de données à l’aide de canaux de communication avec perte, tels que des applications mobiles ou des sites web avec une fonctionnalité hors ligne, pour lesquels la transmission des mesures ne peut pas être assurée, cette propriété contient un identifiant unique, généré par le client, de la mesure prise. Il est recommandé de rendre cette opération suffisamment longue pour garantir un caractère aléatoire suffisant. <br><br> Si des informations telles que la date et l’heure, l’ID d’appareil, l’adresse IP, l’adresse MAC ou d’autres valeurs d’identification d’utilisateur sont intégrées à la génération du `id`, le résultat doit être haché. Cela permet de s’assurer qu’aucune PII n’est codée dans la valeur, car l’objectif n’est pas d’identifier un utilisateur ou un appareil, mais la mesure spécifique dans le temps. |
| `value` | Double | Valeur quantifiable de cette mesure. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
