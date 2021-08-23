---
keywords: Experience Platform;profil;profil client en temps réel;stratégies de fusion;IU;interface utilisateur;horodatage ordonné;priorité du jeu de données
title: Présentation des stratégies de fusion
type: Documentation
description: Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chacun de vos clients. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer la priorité des données et les données qui seront combinées pour créer cette vue unifiée.
source-git-commit: a6a49b4cf9c89b5c6b4679f36daede93590ffb3c
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 99%

---


# Présentation des stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chacun de vos clients. Les stratégies de fusion sont les règles utilisées par [!DNL Platform] pour déterminer la priorité des données et les données qui seront combinées pour créer cette vue unifiée.

À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Ce document présente les stratégies de fusion et le rôle qu’elles jouent dans Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique de plusieurs fonctions [!DNL Experience Platform] importantes. Avant de suivre ce guide et d’utiliser des stratégies de fusion, consultez la documentation des services suivants :

* [Real-time Customer Profile](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): permet d’obtenir un profil client en temps réel en rassemblant des identités de sources de données disparates ingérées dans [!DNL Platform].
* [Modèle de données d’expérience (XDM)](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données d’expérience client.

## Comprendre les stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète et unifiée de chacun de vos clients. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée.

Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client.

Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, si un fragment classe le client comme étant « célibataire » tandis qu’un autre le classe comme étant « marié »), la stratégie de fusion détermine les informations qui doivent passer en priorité et être incluses dans le profil de l’individu.

Les stratégies de fusion sont réservées à votre organisation IMS, ce qui vous permet de créer différentes stratégies afin de fusionner les schémas selon vos besoins. Vous pouvez également spécifier une stratégie de fusion par défaut qui sera utilisée si elle n’est pas explicitement fournie. Pour en savoir plus, consultez la section [Stratégies de fusion par défaut](#default-merge-policy) plus loin dans ce document.

## Méthodes de fusion {#merge-methods}

Chaque fragment de profil contient des informations pour une seule identité sur le nombre total d’identités pouvant exister pour un individu. Lorsque vous fusionnez ces données pour former un profil client, il existe un risque que ces informations entrent en conflit ; une priorité doit alors être spécifiée.

La sélection d’une méthode de fusion vous permet de spécifier les attributs de jeux de données auxquels donner la priorité en cas de conflit de fusion entre les jeux de données.

Deux méthodes de fusion sont disponibles pour les stratégies de fusion. Chacune de ces méthodes est résumée ci-dessous, et des informations supplémentaires sont fournies dans les sections suivantes :

* **[!UICONTROL Priorité du jeu de données] :** En cas de conflit, donnez la priorité aux fragments de profil en fonction du jeu de données duquel ils sont issus. Lorsque vous sélectionnez cette option, vous devez sélectionner les jeux de données associés et leur ordre de priorité. En savoir plus sur la méthode de fusion [priorité du jeu de données](#dataset-precedence).
* **[!UICONTROL Horodatage ordonné] :** En cas de conflit, la priorité est donnée au fragment de profil qui a été mis à jour le plus récemment. En savoir plus sur la méthode de fusion [timestamp ordered](#timestamp-ordered) .

### Priorité du jeu de données {#dataset-precedence}

Lorsque **[!UICONTROL Priorité du jeu de données]** est sélectionnée comme méthode de fusion pour une stratégie de fusion, vous pouvez donner la priorité aux fragments de profil en fonction du jeu de données duquel ils sont issus. Par exemple, un cas d’utilisation serait la présence d’informations de votre organisation dans un jeu de données que vous préférez ou dont les données sont davantage de confiance par rapport à un autre jeu de données.

Pour créer une stratégie de fusion à l’aide de la **[!UICONTROL priorité du jeu de données]**, vous devez sélectionner les jeux de données Profile et ExperienceEvent inclus, puis classer manuellement les jeux de données Profile par priorité. Une fois les jeux de données sélectionnés et triés, le jeu de données supérieur se verra accorder la priorité la plus élevée, le deuxième jeu de données sera le deuxième plus élevé, etc.

### Horodatage ordonné {#timestamp-ordered}

Lorsque des enregistrements de profil sont intégrés dans Experience Platform, un horodatage système est obtenu au moment de l’intégration et ajouté à l’enregistrement. Lorsque **[!UICONTROL Horodatage ordonné]** est sélectionné comme méthode de fusion pour une stratégie de fusion, les profils sont fusionnés en fonction de l’horodatage système. En d’autres termes, la fusion est effectuée en fonction de l’horodatage du moment où l’enregistrement a été intégré à Platform.

## Combinaison d’identités {#id-stitching}

La combinaison d’identités ([!UICONTROL combinaison d’identités]) est le processus d’identification de fragments de données et de leur combinaison afin de former un enregistrement de profil complet. Pour illustrer les différents comportements de combinaison, imaginez un seul client qui interagit avec une marque à l’aide de deux adresses électroniques différentes.

* **[!UICONTROL Aucun] :** lorsque cette option est sélectionnée, les identifiants ne sont pas regroupés. Lorsqu’il y a segmentation, les identités pouvant appartenir à la même personne ne sont pas regroupées et la segmentation ne prend en compte que les attributs associés à chaque identifiant individuel lorsque vous déterminez si un client est admissible pour l’adhésion au segment. Cela peut se traduire par l’existence de plusieurs profils pour un seul client et par la qualification de chaque profil pour différents segments, entraînant l’envoi de plusieurs messages marketing à un même client.
* **[!UICONTROL Graphique privé] :** lorsque le graphique privé est sélectionné, les différentes identités liées à la même personne sont regroupées. Le client dispose ainsi d’un profil unique, ce qui permet à la segmentation de prendre en compte plusieurs attributs provenant de plusieurs identités associées lors de la détermination de la qualification du segment. Dans ce scénario, le client est susceptible d’avoir un seul profil, de se qualifier pour un segment en fonction de la combinaison d’attributs entre les identités et de ne recevoir qu’un seul message marketing.

Pour en savoir plus sur les identités et leur rôle dans la génération de profils et de segments, commencez par lire la [présentation d’Identity Service](../../identity-service/home.md).

## Stratégie de fusion par défaut {#default-merge-policy}

Une organisation peut créer une stratégie de fusion par défaut à utiliser lors de la fusion de fragments de profils. Cela permet aux utilisateurs de sélectionner facilement la stratégie par défaut lors de l’exécution d’actions dans Experience Platform, telles que l’affichage des profils client ou la création de segments. Dans la plupart des cas, à moins qu’une autre stratégie de fusion ne soit spécifiée, la stratégie de fusion par défaut est utilisée.

Chaque organisation peut créer plusieurs stratégies de fusion liées à une seule classe de schéma XDM. Toutefois, une seule stratégie de fusion par défaut peut être choisie pour chaque classe. Par exemple, votre organisation peut avoir une stratégie de fusion par défaut associée à la classe [!DNL XDM Individual Profile] et une stratégie de fusion par défaut différente pour une classe Inventaire de produits personnalisée.

Si vous créez une stratégie de fusion et la définissez comme stratégie par défaut, la stratégie de fusion par défaut précédente sera automatiquement mise à jour par le système et ne sera plus la stratégie par défaut.

>[!WARNING]
>
>Le nombre de profils et les segments associés à une stratégie de fusion par défaut existante peuvent être affectés. Tout segment auquel une stratégie de fusion par défaut est appliquée est mis à jour vers la nouvelle stratégie de fusion par défaut.

## Étapes suivantes

Après avoir lu ce guide, vous savez maintenant ce que sont les stratégies de fusion et le rôle qu’elles jouent dans Experience Platform. Pour commencer à utiliser des stratégies de fusion dans l’interface utilisateur d’Experience Platform, reportez-vous au [guide de l’interface utilisateur des stratégies de fusion](ui-guide.md). Pour utiliser des stratégies de fusion à l’aide de l’API, consultez le [guide de point d’entrée de l’API des stratégies de fusion](../api/merge-policies.md).
