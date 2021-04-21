---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; mesure ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données de mesure
topic-legacy: overview
description: Ce document présente un aperçu du type de données du modèle de données d’expérience de mesure (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 5%

---

# [!UICONTROL Type ] de données de mesure

 Measureest un type de données XDM (Experience Data Model) standard qui contient un point de données quantifiable concret d’une mesure particulière. Une mesure est composée d’un identifiant unique et d’une valeur.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `id` | Chaîne | Identificateur unique de cette mesure. Dans les cas de collecte de données utilisant des canaux de communication avec perte, tels que les applications mobiles ou les sites Web dotés de fonctionnalités hors ligne où la transmission des mesures ne peut pas être assurée, cette propriété contient un identifiant unique généré par le client de la mesure prise. Il est recommandé de le faire suffisamment longtemps pour assurer un caractère assez aléatoire. <br><br> Si des informations telles que l’horodatage, l’ID de périphérique, l’adresse IP, l’adresse MAC ou d’autres valeurs potentiellement identifiables par l’utilisateur sont intégrées à la génération du  `id`fichier, le résultat doit être haché. Cela permet de s’assurer qu’aucune identification personnelle n’est codée dans la valeur, car l’objectif n’est pas d’identifier un utilisateur ou un périphérique, mais la mesure spécifique dans le temps. |
| `value` | Double | Valeur quantifiable de cette mesure. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
