---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Traitement du consentement dans Adobe Experience Platform
description: Découvrez comment traiter les signaux de consentement des clients dans Adobe Experience Platform à l’aide de la norme Adobe 2.0.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 1%

---

# Traitement du consentement dans Adobe Experience Platform

Adobe Experience Platform vous permet de traiter les données de consentement que vous avez collectées auprès de vos clients et de les intégrer à vos profils client stockés. Ces données peuvent ensuite être utilisées par des processus en aval pour déterminer si la collecte de données a lieu pour un client spécifique ou si leurs profils sont utilisés à des fins spécifiques. Par exemple, les données de consentement d’un profil particulier peuvent déterminer si elles peuvent être incluses dans un segment d’audience exporté ou si elles peuvent participer à des canaux marketing spécifiques tels que l’email, les SMS ou les notifications push.

Ce document fournit une vue d’ensemble de la configuration de vos opérations de données Platform pour ingérer les données de consentement des clients générées par une plateforme de gestion du consentement (CMP) et intégrer ces données aux profils client pour les cas d’utilisation en aval.

>[!NOTE]
>
>Ce document se concentre sur le traitement des données de consentement à l’aide de la norme Adobe. Si vous traitez des données de consentement conformément au Transparency and Consent Framework (TCF) 2.0 de l’IAB, consultez le guide sur [Prise en charge de TCF 2.0 dans Adobe Real-time Customer Data Platform](../iab/overview.md).

## Conditions préalables

Ce guide nécessite une compréhension pratique des différents services Experience Platform impliqués dans le traitement des données de consentement :

* [Modèle de données d’expérience (XDM)](/help/xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Service Adobe Experience Platform Identity](/help/identity-service/home.md): résout le problème fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [Profil client en temps réel](/help/profile/home.md): Utilisations [!DNL Identity Service] fonctionnalités pour créer des profils client détaillés à partir de vos jeux de données en temps réel. Real-Time Customer Profile extrait les données du lac de données et conserve les profils clients dans sa propre banque de données distincte.
* [SDK Web Adobe Experience Platform](/help/web-sdk/home.md): une bibliothèque JavaScript côté client qui vous permet d’intégrer divers services Platform à votre site web destiné aux clients.
   * [Commandes de consentement du SDK](../../../../web-sdk/commands/setconsent.md): présentation du cas d’utilisation des commandes du SDK liées au consentement présentée dans ce guide.
* [Adobe Experience Platform Segmentation Service](/help/segmentation/home.md): vous permet de diviser les données de Real-time Customer Profile en groupes d’individus partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.

## Synthèse du flux de traitement du consentement {#summary}

La section suivante décrit le traitement des données de consentement une fois que le système a été correctement configuré :

1. Un client fournit ses préférences de consentement pour la collecte de données par le biais d’une boîte de dialogue sur votre site web.
1. Au chargement de chaque page (ou lorsque votre CMP détecte une modification des préférences de consentement), un script personnalisé sur votre site associe les préférences actuelles à un objet XDM standard. Cet objet est ensuite transmis au SDK Web Platform. `setConsent` .
1. When `setConsent` est appelée, le SDK Web de Platform vérifie si les valeurs de consentement sont différentes de celles qu’il a reçues pour la dernière fois. Si les valeurs sont différentes (ou s’il n’existe aucune valeur précédente), les données de consentement/préférence structurées sont envoyées à Adobe Experience Platform.
1. Les données de consentement/préférence sont ingérées dans une [!DNL Profile]Jeu de données activé dont le schéma contient des champs de consentement/préférence.

Outre les commandes du SDK déclenchées par les hooks de modification du consentement de la CMP, les données de consentement peuvent également être transmises à l’Experience Platform par le biais de toutes les données XDM générées par le client qui sont directement transférées vers un [!DNL Profile]Jeu de données activé.

### Application du consentement

Dans la version actuelle de la prise en charge du traitement du consentement dans Platform, seule l’autorisation de collecte de données (`collect.val`) est automatiquement appliqué par le SDK Web de Platform. Bien que des préférences et des consentements plus granulaires puissent être collectés et conservés dans les profils client, ces signaux supplémentaires doivent être imposés manuellement dans vos propres processus en aval.

>[!NOTE]
>
>Pour plus d’informations sur la structure des champs de consentement XDM mentionnés ci-dessus, reportez-vous au guide sur la [[!UICONTROL Consentements et préférences] type de données](/help/xdm/data-types/consents.md).

Une fois le système configuré, le SDK Web Platform interprète la valeur de consentement de collecte de données pour l’utilisateur actuel afin de déterminer si les données doivent être envoyées à l’Edge Network Adobe Experience Platform, abandonnées depuis le client ou conservées jusqu’à ce que l’autorisation de collecte de données soit définie sur oui ou non.

## Déterminer comment générer des données de consentement client dans votre CMP {#consent-data}

Chaque système de CMP étant unique, vous devez déterminer la meilleure manière de permettre à vos clients de fournir un consentement lorsqu’ils interagissent avec votre service. Pour ce faire, utilisez une boîte de dialogue de consentement de cookie, comme dans l’exemple suivant :

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Cette boîte de dialogue doit permettre au client d’activer ou de désactiver des cas d’utilisation de marketing et de personnalisation spécifiques pour ses données. Ces consentements et préférences doivent être conformes au modèle de données que vous avez défini pour la variable [!DNL Profile]Jeu de données activé à l’étape suivante.

## Ajoutez des champs de consentement normalisés à une [!DNL Profile]-enabled dataset {#dataset}

Les données de consentement du client doivent être envoyées à un [!DNL Profile]Jeu de données activé dont le schéma contient des champs de consentement. Ces champs doivent être inclus dans le même schéma et jeu de données que celui que vous utilisez pour capturer des informations d’attributs sur des clients individuels.

Consultez le tutoriel sur [configuration d’un jeu de données pour capturer des données de consentement](./dataset.md) pour obtenir des instructions détaillées sur la manière d’ajouter ces champs obligatoires à un [!DNL Profile]Jeu de données activé avant de poursuivre avec ce guide.

## Mettre à jour [!DNL Profile] stratégies de fusion pour inclure des données de consentement {#merge-policies}

Une fois que vous avez créé une [!DNL Profile]Jeu de données activé pour le traitement des données de consentement, vous devez vous assurer que vos stratégies de fusion ont été configurées pour inclure systématiquement des champs de consentement dans chaque profil client. Cela implique de définir la priorité du jeu de données afin que votre jeu de données de consentement soit hiérarchisé par rapport à d’autres jeux de données potentiellement conflictuels.

>[!NOTE]
>
>Si vous n’avez pas de jeux de données en conflit, vous devez définir la priorité d’horodatage de votre stratégie de fusion à la place. Cela permet de s’assurer que le dernier consentement spécifié par un client est le paramètre de consentement utilisé.

Pour plus d’informations sur l’utilisation des stratégies de fusion, commencez par lire la section [présentation des stratégies de fusion](../../../../profile/merge-policies/overview.md). Lors de la configuration de vos stratégies de fusion, vous devez vous assurer que vos profils incluent tous les attributs de consentement requis fournis par la variable [!UICONTROL Consentements et préférences] groupe de champs de schéma, comme indiqué dans le guide sur [préparation du jeu de données](./dataset.md).

## Importation des données de consentement dans Platform

Une fois que vous disposez de vos jeux de données et des stratégies de fusion pour représenter les champs de consentement requis dans vos profils client, l’étape suivante consiste à importer les données de consentement elles-mêmes dans Platform.

Vous devez principalement utiliser le SDK Web de Adobe Experience Platform pour envoyer des données de consentement à Platform chaque fois que des événements de changement de consentement sont détectés par votre CMP. Si vous collectez des données de consentement sur une plateforme mobile, vous devez utiliser le SDK Adobe Experience Platform Mobile. Vous pouvez également choisir d’ingérer directement vos données de consentement collectées en les mappant au schéma XDM de votre jeu de données de consentement et en les envoyant à Platform par ingestion par lots.

Vous trouverez des détails sur chacune de ces méthodes dans les sous-sections ci-dessous.

### Configuration du SDK Web Experience Platform pour traiter les données de consentement {#web-sdk}

Une fois que vous avez configuré votre CMP pour écouter les événements de modification du consentement sur votre site web, vous pouvez intégrer le SDK Web Experience Platform pour recevoir les paramètres de consentement mis à jour et les envoyer à Platform à chaque chargement de page et chaque fois qu’un événement de modification du consentement se produit. Consultez le guide sur la [configuration du SDK Web pour traiter les données de consentement du client](../sdk.md) pour plus d’informations.

### Configuration du SDK Mobile Experience Platform pour traiter les données de consentement {#mobile-sdk}

Si des préférences de consentement du client sont requises dans votre application mobile, vous pouvez intégrer le SDK Mobile Experience Platform pour récupérer et mettre à jour les paramètres de consentement, en les envoyant à Platform chaque fois que l’API de consentement est appelée.

Reportez-vous à la documentation du SDK Mobile pour [configuration de l’extension mobile Consent](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) et [utilisation de l’API de consentement](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Pour plus d’informations sur la gestion des problèmes de confidentialité à l’aide du SDK Mobile, reportez-vous à la section . [Confidentialité et RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Ingestion directe des données de consentement conformes à XDM {#batch}

Vous pouvez ingérer des données de consentement conformes à XDM à partir d’un fichier CSV à l’aide de l’ingestion par lots. Cela peut s’avérer utile si vous disposez d’un journal des données de consentement collectées antérieurement qui doivent encore être intégrées à vos profils client.

Suivez le tutoriel sur [mappage d’un fichier CSV à XDM](../../../../ingestion/tutorials/map-csv/overview.md) pour savoir comment convertir vos champs de données en XDM et les ingérer dans Platform. Lorsque vous sélectionnez la variable [!UICONTROL Destination] pour le mappage, veillez à sélectionner la variable **[!UICONTROL Utiliser un jeu de données existant]** et choisissez l’option [!DNL Profile]Jeu de données de consentement activé que vous avez créé précédemment.

## Tester votre mise en oeuvre {#test-implementation}

Après avoir ingéré les données de consentement du client dans votre [!DNL Profile]Jeu de données compatible, vous pouvez vérifier vos profils mis à jour pour vérifier s’ils contiennent des attributs de consentement.

>[!IMPORTANT]
>
>Pour afficher les attributs d’un profil existant dans l’interface utilisateur, vous devez connaître au moins une valeur d’identité (et son espace de noms correspondant) associée à ce profil.
>
>Si vous n’avez pas accès à ces informations, vous pouvez choisir d’ingérer vos propres données de consentement de test et de les associer à une valeur d’identité/à un espace de noms qui vous est propre.

Voir la section sur [navigation des profils par identité](../../../../profile/ui/user-guide.md#browse) dans le [!DNL Profile] Guide de l’interface utilisateur pour connaître les étapes spécifiques à la recherche des détails d’un profil.

Par défaut, les nouveaux attributs de consentement n’apparaîtront pas dans le tableau de bord d’un profil. Par conséquent, vous devez accéder au **[!UICONTROL Attributs]** sur la page détails d’un profil afin de confirmer qu’il a été ingéré comme prévu. Consultez le guide sur la [tableau de bord du profil](../../../../profile/ui/profile-dashboard.md) pour savoir comment personnaliser le tableau de bord en fonction de vos besoins.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Étapes suivantes

Ce guide explique comment configurer vos opérations Platform pour traiter les données de consentement des clients à l’aide de la norme Adobe et faire en sorte que ces attributs soient représentés dans les profils client. Vous pouvez désormais intégrer les préférences de consentement des clients en tant que facteur déterminant dans la qualification des segments et dans d’autres cas d’utilisation en aval.

Pour plus d’informations sur les fonctionnalités liées à la confidentialité des Experience Platform, consultez la présentation de [gouvernance, confidentialité et sécurité dans Platform](../../overview.md).
