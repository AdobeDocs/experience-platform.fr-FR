---
keywords: Experience Platform;profil;profil client en temps réel;politiques de fusion;IU;interface utilisateur;horodatage ordonné;priorité du jeu de données
title: Présentation des politiques de fusion
type: Documentation
description: Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chacun de vos clients. Les politiques de fusion sont les règles utilisées par Platform pour déterminer la priorité des données et les données qui seront combinées pour créer cette vue unifiée.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 80%

---

# Présentation des politiques de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chacun de vos clients. Les politiques de fusion sont les règles utilisées par [!DNL Platform] pour déterminer la priorité des données et les données qui seront combinées pour créer cette vue unifiée.

À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des politiques de fusion, gérer des politiques existantes et définir une politique de fusion par défaut pour votre organisation dans l’interface utilisateur. Ce document présente les politiques de fusion et le rôle qu’elles jouent dans Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique de plusieurs fonctions [!DNL Experience Platform] importantes. Avant de suivre ce guide et d’utiliser des politiques de fusion, consultez la documentation des services suivants :

* [Profil client en temps réel](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Service Adobe Experience Platform Identity](../../identity-service/home.md) : active Real-time Customer Profile en rapprochant des identités de sources de données disparates ingérées dans [!DNL Platform].
* [Modèle de données d’expérience (XDM)](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données d’expérience client.

## Comprendre les politiques de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète et unifiée de chacun de vos clients. Les politiques de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée.

Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client.

Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, si un fragment classe le client comme étant « célibataire » tandis qu’un autre le classe comme étant « marié »), la politique de fusion détermine les informations qui doivent passer en priorité et être incluses dans le profil de l’individu.

Les stratégies de fusion sont réservées à votre organisation, ce qui vous permet de créer différentes stratégies pour fusionner les schémas de la manière spécifique dont vous avez besoin. Vous pouvez également spécifier une politique de fusion par défaut qui sera utilisée si elle n’est pas explicitement fournie. Pour en savoir plus, consultez la section sur les [stratégies de fusion par défaut](#default-merge-policy) plus loin dans ce document. Notez qu’un maximum de cinq stratégies de fusion est autorisé par organisation.

## Méthodes de fusion {#merge-methods}

Chaque fragment de profil contient des informations pour une seule identité sur le nombre total d’identités pouvant exister pour un individu. Lorsque vous fusionnez ces données pour former un profil client, il existe un risque que ces informations entrent en conflit ; une priorité doit alors être spécifiée.

La sélection d’une méthode de fusion vous permet de spécifier les attributs de jeux de données auxquels donner la priorité en cas de conflit de fusion entre les jeux de données.

Deux méthodes de fusion sont disponibles pour les politiques de fusion. Chacune de ces méthodes est résumée ci-dessous, et des informations supplémentaires sont fournies dans les sections suivantes :

* **[!UICONTROL Priorité du jeu de données] :** En cas de conflit, donnez la priorité aux fragments de profil en fonction du jeu de données duquel ils sont issus. Lorsque vous sélectionnez cette option, vous devez sélectionner les jeux de données associés et leur ordre de priorité. En savoir plus sur la méthode de fusion [priorité du jeu de données](#dataset-precedence).
* **[!UICONTROL Horodatage ordonné] :** En cas de conflit, la priorité est donnée au fragment de profil qui a été mis à jour le plus récemment. En savoir plus sur la méthode de fusion [horodatage ordonné](#timestamp-ordered)

### Priorité du jeu de données {#dataset-precedence}

Lorsque **[!UICONTROL Priorité du jeu de données]** est sélectionnée comme méthode de fusion pour une politique de fusion, vous pouvez donner la priorité aux fragments de profil en fonction du jeu de données duquel ils sont issus. Par exemple, un cas d’utilisation serait la présence d’informations de votre organisation dans un jeu de données que vous préférez ou dont les données sont davantage de confiance par rapport à un autre jeu de données.

Pour créer une politique de fusion à l’aide de la **[!UICONTROL priorité du jeu de données]**, vous devez sélectionner les jeux de données Profile et ExperienceEvent inclus, puis classer manuellement les jeux de données Profile par priorité. Une fois les jeux de données sélectionnés et triés, le jeu de données supérieur se verra accorder la priorité la plus élevée, le deuxième jeu de données sera le deuxième plus élevé, etc.

### Horodatage ordonné {#timestamp-ordered}

Lorsque des enregistrements de profil sont intégrés dans Experience Platform, un horodatage système est obtenu au moment de l’intégration et ajouté à l’enregistrement. Lorsque **[!UICONTROL Horodatage ordonné]** est sélectionné comme méthode de fusion pour une politique de fusion, les profils sont fusionnés en fonction de l’horodatage système. En d’autres termes, la fusion est effectuée en fonction de l’horodatage du moment où l’enregistrement a été intégré à Platform.

## Combinaison d’identités {#id-stitching}

La combinaison d’identités ([!UICONTROL combinaison d’identités]) est le processus d’identification de fragments de données et de leur combinaison afin de former un enregistrement de profil complet. Pour illustrer les différents comportements de combinaison, imaginez un seul client qui interagit avec une marque à l’aide de deux adresses électroniques différentes.

* **[!UICONTROL Aucun] :** lorsque cette option est sélectionnée, les identifiants ne sont pas regroupés. Lorsque la segmentation se produit, les identités qui peuvent appartenir à la même personne ne sont pas regroupées et la segmentation ne prend en compte que les attributs associés à chaque ID individuel lorsque vous déterminez si un client est admissible pour l’appartenance à l’audience. Cela peut se traduire par l’existence de plusieurs profils pour un seul client et par la qualification de chaque profil pour différentes audiences, ce qui entraîne l’envoi de plusieurs messages marketing à un même client.
* **[!UICONTROL Graphique privé] :** lorsque le graphique privé est sélectionné, les différentes identités liées à la même personne sont regroupées. Le client dispose ainsi d’un profil unique, ce qui permet à la segmentation de prendre en compte plusieurs attributs provenant de plusieurs identités associées lors de la détermination de la qualification du segment. Dans ce scénario, le client est susceptible d’avoir un seul profil, de se qualifier pour une audience en fonction de la combinaison d’attributs entre les identités et de ne recevoir qu’un seul message marketing.

Pour en savoir plus sur les identités et leur rôle dans la génération de profils et d’audiences, commencez par lire la [présentation d’Identity Service](../../identity-service/home.md).

## Politique de fusion par défaut {#default-merge-policy}

Une organisation peut créer une politique de fusion par défaut à utiliser lors de la fusion de fragments de profils. Cela permet aux utilisateurs de sélectionner facilement la stratégie par défaut lors de l’exécution d’actions dans Experience Platform, telles que l’affichage des profils client ou la création d’audiences. Dans la plupart des cas, à moins qu’une autre politique de fusion ne soit spécifiée, la politique de fusion par défaut est utilisée.

Chaque organisation peut créer plusieurs politiques de fusion liées à une seule classe de schéma XDM. Toutefois, une seule politique de fusion par défaut peut être choisie pour chaque classe. Par exemple, votre organisation peut avoir une politique de fusion par défaut associée à la classe [!DNL XDM Individual Profile] et une politique de fusion par défaut différente pour une classe Inventaire de produits personnalisée.

Si vous créez une politique de fusion et la définissez comme politique par défaut, la politique de fusion par défaut précédente sera automatiquement mise à jour par le système et ne sera plus la politique par défaut.

>[!WARNING]
>
>Le nombre de profils et les audiences avec une stratégie de fusion par défaut associée peuvent être affectés. Toute audience à laquelle une stratégie de fusion par défaut est appliquée sera mise à jour vers la nouvelle stratégie de fusion par défaut.

## Étapes suivantes

Après avoir lu ce guide, vous savez maintenant ce que sont les politiques de fusion et le rôle qu’elles jouent dans Experience Platform. Pour commencer à utiliser des politiques de fusion dans l’interface utilisateur d’Experience Platform, reportez-vous au [guide de l’interface utilisateur des politiques de fusion](ui-guide.md). Pour utiliser des politiques de fusion à l’aide de l’API, consultez le [guide de point d’entrée de l’API des politiques de fusion](../api/merge-policies.md).
