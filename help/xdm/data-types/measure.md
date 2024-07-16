---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;mesure;type de données;type de données;type de données
solution: Experience Platform
title: Type de données de mesure
description: Découvrez le type de données Mesurer le modèle de données d’expérience (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 5%

---

# Type de données [!UICONTROL Mesure]

[!UICONTROL Mesure] est un type de données XDM (Experience Data Model) standard qui contient un point de données quantifiable concret d’une mesure particulière. Une mesure est composée d’un identifiant unique et d’une valeur.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `id` | Chaîne | Identifiant unique de cette mesure. Dans le cas d’une collecte de données utilisant des canaux de communication avec perte, tels que des applications mobiles ou des sites web avec des fonctionnalités hors ligne où la transmission de mesures ne peut pas être assurée, cette propriété contient un identifiant unique généré par le client de la mesure prise. Il est recommandé d’effectuer cette opération suffisamment longtemps pour garantir un caractère aléatoire suffisant. <br><br> Si des informations telles que l’horodatage, l’identifiant de l’appareil, l’adresse IP, l’adresse MAC ou d’autres valeurs potentiellement d’identification de l’utilisateur sont intégrées à la génération de `id`, le résultat doit être haché. Cela garantit qu’aucune PII n’est codée dans la valeur, car l’objectif n’est pas d’identifier un utilisateur ou un appareil, mais la mesure spécifique dans le temps. |
| `value` | Double | Valeur quantifiable de cette mesure. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
