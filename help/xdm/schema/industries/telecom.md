---
solution: Experience Platform
title: Modèle de données du secteur des télécommunications ERD
topic-legacy: overview
description: Affichez un diagramme des relations d’entité (ERD) qui décrit un modèle de données normalisé pour le secteur des télécommunications, compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
source-git-commit: 88c17992a391b24a76c3e387d3033df4c75a6aa6
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


#  ERD du modèle de données du secteur des télécommunications

Le diagramme de relation des entités suivant (ERD) représente un modèle de données normalisé pour le secteur des télécommunications. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans est basée sur une classe [Modèle de données d’expérience (XDM) ](../composition.md#class) sous-jacente.
* Pour une entité donnée, chaque ligne marquée dans **bold** représente un groupe de champs ou un type de données, avec les champs pertinents qu’elle fournit ci-dessous dans le texte non en gras.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;identité Principale&quot;.
* Les relations d’entité sont marquées comme étant non dépendantes, puisque les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>L’entité Événement d’expérience comprend un champ &quot;_ID&quot;, qui représente l’attribut unique (`_id`) fourni par la classe XDM ExperienceEvent. Consultez le document de référence sur [XDM ExperienceEvent](../../classes/experienceevent.md) pour plus d’informations sur ce qui est attendu pour cette valeur.