---
keywords: Experience Platform;profil;profil client en temps réel;stratégies de fusion;interface utilisateur;interface utilisateur;ordre d’horodatage;priorité du jeu de données
title: Présentation des stratégies de fusion
type: Documentation
description: Adobe Experience Platform vous permet de rassembler des fragments de données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète de vos clients. Lorsque vous rassemblez ces données, les stratégies de fusion sont les règles utilisées par Platform pour déterminer la priorité des données et les données qui seront combinées pour créer la vue unifiée.
source-git-commit: c2cc1428e3a70cf987adab583e9f9fb5d5140c74
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 11%

---


# Présentation des stratégies de fusion

Adobe Experience Platform vous permet de rassembler des fragments de données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète de chaque client. Lorsque vous rassemblez ces données, les stratégies de fusion sont les règles utilisées par [!DNL Platform] pour déterminer la priorité des données et les données qui seront combinées pour créer une vue unifiée.

À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Ce document présente les stratégies de fusion et le rôle qu’elles jouent dans Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique de plusieurs fonctions [!DNL Experience Platform] importantes. Avant de suivre ce guide et d’utiliser des stratégies de fusion, consultez la documentation des services suivants :

* [Real-time Customer Profile](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Service Adobe Experience Platform Identity](../../identity-service/home.md) : Active Real-time Customer Profile en établissant un lien entre les identités de sources de données disparates ingérées dans  [!DNL Platform].
* [Modèle de données d’expérience (XDM)](../../xdm/home.md)[!DNL Platform] : cadre normalisé selon lequel Experience organise les données d’expérience client.

## Présentation des stratégies de fusion

Adobe Experience Platform vous permet de rassembler des fragments de données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète et unifiée de chaque client. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée.

Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client.

Lorsque les données provenant de sources multiples entrent en conflit (par exemple, un fragment répertorie le client comme &quot;célibataire&quot; tandis que l’autre le répertorie comme &quot;marié&quot;), la stratégie de fusion détermine les informations à inclure dans le profil de la personne.

Les stratégies de fusion sont réservées à votre organisation IMS, ce qui vous permet de créer différentes stratégies pour fusionner les schémas de la manière spécifique dont vous avez besoin. Vous pouvez également spécifier une stratégie de fusion par défaut qui sera utilisée si elle n’est pas explicitement fournie. Pour en savoir plus, consultez la section [Stratégies de fusion par défaut](#default-merge-policy) plus loin dans ce document.

## Méthodes de fusion {#merge-methods}

Chaque fragment de profil contient des informations pour une seule identité sur le nombre total d’identités pouvant exister pour un individu. Lorsque vous fusionnez ces données pour former un profil client, il existe un risque que ces informations entrent en conflit et une priorité doit être spécifiée.

La sélection d’une méthode de fusion vous permet de spécifier les attributs de jeu de données à prioriser en cas de conflit de fusion entre les jeux de données.

Deux méthodes de fusion sont disponibles pour les stratégies de fusion. Chacune de ces méthodes est résumée ci-dessous avec des détails supplémentaires fournis dans les sections suivantes :

* **[!UICONTROL Priorité du jeu de données] :** en cas de conflit, donnez la priorité aux fragments de profil en fonction du jeu de données à partir duquel ils sont issus. Lorsque vous sélectionnez cette option, vous devez choisir les jeux de données associés et leur ordre de priorité. En savoir plus sur la méthode de fusion [priorité du jeu de données](#dataset-precedence).
* **[!UICONTROL Classement de l’horodatage] :**  en cas de conflit, la priorité est donnée au fragment de profil qui a été mis à jour le plus récemment. En savoir plus sur la méthode de fusion [horodatage ordonné](#timestamp-ordered).
   * **Horodatages personnalisés :** la méthode de fusion ordonnée d’horodatage prend également en charge les horodatages personnalisés qui ont la priorité sur les horodatages système lors de la fusion de données dans le même jeu de données (identités multiples) ou dans plusieurs jeux de données. Pour en savoir plus, consultez la section sur [à l’aide d’horodatages personnalisés](#custom-timestamps).

### Priorité du jeu de données {#dataset-precedence}

Lorsque **[!UICONTROL La priorité du jeu de données]** est sélectionnée comme méthode de fusion pour une stratégie de fusion, vous pouvez donner la priorité aux fragments de profil en fonction du jeu de données à partir duquel ils sont venus. Par exemple, un cas d’utilisation serait la présence d’informations de votre organisation dans un jeu de données que vous préférez ou dont les données sont davantage de confiance par rapport à un autre jeu de données.

Pour créer une stratégie de fusion à l’aide de la **[!UICONTROL priorité du jeu de données]**, vous devez sélectionner les jeux de données Profile et ExperienceEvent inclus, puis classer manuellement les jeux de données Profile par priorité. Une fois les jeux de données sélectionnés et triés, le jeu de données supérieur se verra accorder la priorité la plus élevée, le deuxième jeu de données sera le deuxième plus élevé, etc.

### Horodatage ordonné {#timestamp-ordered}

Lorsque des enregistrements de profil sont ingérés dans Experience Platform, un horodatage système est obtenu au moment de l’ingestion et ajouté à l’enregistrement. Lorsque **[!UICONTROL L’horodatage ordonné]** est sélectionné comme méthode de fusion pour une stratégie de fusion, les profils sont fusionnés en fonction de l’horodatage système. En d’autres termes, la fusion est effectuée en fonction de l’horodatage du moment où l’enregistrement a été ingéré dans Platform.

#### Utilisation d’horodatages personnalisés {#custom-timestamps}

Parfois, il peut arriver qu’il soit nécessaire de fournir un horodatage personnalisé et que la stratégie de fusion respecte l’horodatage personnalisé plutôt que l’horodatage système. Par exemple, renseignez des données ou assurez-vous que l’ordre des événements est correct si les enregistrements sont ingérés dans le désordre.

Pour utiliser un horodatage personnalisé, le groupe de champs **[!UICONTROL Détails de l’audit du système source externe]** doit être ajouté à votre schéma de profil. Une fois ajouté, l’horodatage personnalisé peut être renseigné à l’aide du champ `lastUpdatedDate`. Lorsqu’un enregistrement est ingéré avec le champ `lastUpdatedDate` renseigné, l’Experience Platform utilise ce champ pour fusionner des enregistrements dans les jeux de données. Si `lastUpdatedDate` n’est pas présent, ou n’est pas renseigné, Platform continuera à utiliser l’horodatage système.

>[!NOTE]
>
>Vous devez vous assurer que l’horodatage `lastUpdatedDate` est renseigné lors de l’ingestion d’une mise à jour sur le même enregistrement.

La capture d’écran suivante affiche les champs du groupe de champs [!UICONTROL Détails de l’audit du système source externe] . Pour obtenir des instructions détaillées sur l’utilisation des schémas à l’aide de l’interface utilisateur de Platform, notamment sur l’ajout de groupes de champs aux schémas, consultez le [tutoriel sur la création d’un schéma à l’aide de l’interface utilisateur](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-field-group.png)

Pour utiliser des horodatages personnalisés à l’aide de l’API, reportez-vous à la section [du guide de point de terminaison des stratégies de fusion sur l’utilisation d’horodatages personnalisés](../api/merge-policies.md#custom-timestamps).

## Combinaison d’identités {#id-stitching}

La combinaison d’identités ([!UICONTROL la combinaison d’identifiants]) est le processus d’identification des fragments de données et de combinaison pour former un enregistrement de profil complet. Pour illustrer les différents comportements de combinaison, imaginez un seul client qui interagit avec une marque à l’aide de deux adresses électroniques différentes.

* **[!UICONTROL Aucun] :** lorsque cette option est sélectionnée, les identifiants ne sont pas regroupés. Lorsque la segmentation se produit, les identités qui peuvent appartenir à la même personne ne sont pas regroupées et la segmentation ne prend en compte que les attributs associés à chaque ID individuel lorsque vous déterminez si un client est admissible pour l’adhésion au segment. Cela peut se traduire par l’existence de plusieurs profils pour un seul client et par la qualification de chaque profil pour différents segments, ce qui entraîne l’envoi de plusieurs messages marketing à un même client.
* **[!UICONTROL Graphique privé] :** lorsque le graphique privé est sélectionné, plusieurs identités liées à la même personne sont regroupées. Le client dispose ainsi d’un profil unique et permet à la segmentation de prendre en compte plusieurs attributs provenant de plusieurs identités associées lors de la détermination de la qualification du segment. Dans ce scénario, le client est susceptible d’avoir un seul profil, de se qualifier pour un segment en fonction de la combinaison d’attributs entre les identités et de ne recevoir qu’un seul message marketing.

Pour en savoir plus sur les identités et leur rôle dans la génération de profils et de segments, commencez par lire la [présentation d’Identity Service](../../identity-service/home.md).

## Stratégie de fusion par défaut {#default-merge-policy}

Une organisation peut créer une stratégie de fusion par défaut à utiliser pour son organisation lors de la fusion de fragments de profil. Cela permet aux utilisateurs de sélectionner facilement la stratégie par défaut lors de l’exécution d’actions dans Experience Platform, telles que l’affichage des profils client ou la création de segments. Dans la plupart des cas, à moins qu’une autre stratégie de fusion ne soit spécifiée, la stratégie de fusion par défaut est utilisée.

Chaque organisation peut créer plusieurs stratégies de fusion liées à une seule classe de schéma XDM. Toutefois, une seule stratégie de fusion par défaut peut être déclarée pour chaque classe. Par exemple, votre organisation peut avoir une stratégie de fusion par défaut associée à la classe [!DNL XDM Individual Profile] et une stratégie de fusion par défaut différente pour une classe Inventaire de produits personnalisée.

Si vous créez une stratégie de fusion et la définissez comme stratégie par défaut, la stratégie de fusion par défaut précédente sera automatiquement mise à jour par le système pour ne plus être la stratégie par défaut.

>[!WARNING]
>
>Le nombre de profils et les segments associés à une stratégie de fusion par défaut existante peuvent être affectés. Tout segment auquel une stratégie de fusion par défaut est appliquée est mis à jour vers la nouvelle stratégie de fusion par défaut.

## Étapes suivantes

Après avoir lu ce guide, vous savez maintenant quelles sont les stratégies de fusion et le rôle qu’elles jouent dans Experience Platform. Pour commencer à utiliser des stratégies de fusion dans l’interface utilisateur de l’Experience Platform, reportez-vous au [guide de l’interface utilisateur des stratégies de fusion](ui-guide.md). Pour utiliser des stratégies de fusion à l’aide de l’API, consultez le [guide de point de terminaison de l’API des stratégies de fusion](../api/merge-policies.md).