---
title: Présentation de l’extension de l’API de conversion en temps réel du bureau Commerce
description: Découvrez l’extension de l’API de conversion en temps réel de Trade Desk pour le transfert d’événements dans Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: d9d185685106ac160dcbefc5e9567a85c8302a73
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---

# [!DNL The Trade Desk Real-Time Conversions API] présentation de l’extension

Vous pouvez utiliser la variable [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) extension pour envoyer des données de l’Edge Network Adobe Experience Platform vers [!DNL The Trade Desk] en utilisant les fonctionnalités de l’API dans votre [transfert d’événement](../../../ui/event-forwarding/overview.md) règles.

Utilisation [!DNL The Trade Desk Real-Time Conversions API] , vous pouvez tirer parti des fonctionnalités de l’API dans votre [transfert d’événement](../../../ui/event-forwarding/overview.md) règles d’envoi de données à [!DNL The Trade Desk] de l’Edge Network Adobe Experience Platform.

Lisez ce document pour savoir comment installer l’extension et utiliser ses fonctionnalités dans un transfert d’événement. [règle](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Cette page d’extension et de documentation est gérée par [!DNL The Trade Desk] l&#39;équipe. Pour toute demande d&#39;information ou de mise à jour, veuillez les contacter directement.

## Conditions préalables {#prerequisites}

Vous devez disposer d’un identifiant publicitaire, d’un identifiant UPixel et d’un identifiant de dispositif de suivi pertinents, qui sont requis dans votre [!DNL The Trade Desk] afin de configurer la variable [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Si vous êtes un commerçant, vous devrez également obtenir votre identifiant marchand.

## Installez et configurez le [!DNL The Trade Desk] API de conversion en temps réel {#install}

Pour installer l’extension, [création d’une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou sélectionnez une propriété existante à modifier.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans le **[!UICONTROL Catalogue]** , sélectionnez l’onglet **[!UICONTROL Le bureau de commerce]** Carte de l’API Conversions en temps réel, puis sélectionnez **[!UICONTROL Installer]**.

![Le catalogue d’extensions affichant la variable [!DNL The Trade Desk] installation de mise en surbrillance de la carte d’extension.](../../../images/extensions/server/tradedesk/install-extension.png)

Dans l’écran suivant, saisissez la variable [!UICONTROL Identifiant publicitaire], et éventuellement une [!UICONTROL Identifiant du marchand]. Vous pouvez coller les ID directement dans ces entrées ou vous pouvez utiliser un élément de données à la place. Ces valeurs serviront de valeurs par défaut lors de l’appel d’événement à [!DNL The Trade Desk] API de conversion en temps réel. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

Pour savoir comment créer des éléments de données et les rendre disponibles pour les extensions dans votre propriété de balise, suivez la [Création d’éléments de données](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) tutoriel .

![La variable [!DNL The Trade Desk] page de configuration de l’extension avec la fonction [!UICONTROL Identifiant publicitaire] et [!UICONTROL Identifiant du marchand] champs en surbrillance.](../../../images/extensions/server/tradedesk/configure-extension.png)

L’extension est installée et vous pouvez désormais utiliser ses fonctionnalités dans vos règles de transfert d’événement.

## Configurer une règle de transfert d’événement {#rule}

Une fois que vous avez installé et configuré l’extension, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent comment et à quel moment les événements seront envoyés à [!DNL The Trade Desk].

Vous devez envisager de configurer plusieurs règles pour envoyer toutes les règles acceptées. [propriétés de requête](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] et [!DNL The Trade Desk] API de conversion en temps réel.

>[!NOTE]
>
>Les événements doivent être envoyés en temps réel ou aussi près que possible du temps réel.

Création d’un transfert d’événement [règle](../../../ui/managing-resources/rules.md) dans la propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Le bureau de commerce]**. Ensuite, sélectionnez **[!UICONTROL Conversion en temps réel]** pour le **[!UICONTROL Type d’action]**.

![La vue Règles de propriété de transfert d’événement , avec les champs requis pour ajouter une configuration d’action de règle de transfert d’événement mise en surbrillance.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Après la sélection, des contrôles supplémentaires s’affichent pour configurer davantage les données d’événement qui seront envoyées à [!DNL The Trade Desk]. Sélectionner **[!UICONTROL Conserver les modifications]** pour enregistrer la règle.

Les options de configuration sont divisées en trois sections principales, comme indiqué ci-dessous :

**[!UICONTROL Propriétés de requête de base]**

| Entrée | Description |
| --- | --- |
| ID de suivi | ID de plateforme de l’outil de suivi des événements. |
| Identifiant UPix | ID de pixel universel pour l’événement. |
| URL du référent | URL du site web à partir duquel l’événement s’est produit, le cas échéant. |
| Nom de l’événement | Type d’événement défini par la plateforme du partenaire. |
| Valeur | Valeur de suivi des recettes dans la chaîne décimale (par exemple, &quot;19,98&quot;). |
| Devise | Code de devise au format ISO. |
| IP du client | Adresse IPv4 ou IPv6 du client. |
| Identifiant de publicité | Identifiant publicitaire unique pour l’événement. |
| Type d’ID d’annonce | Type de l’ID de publicité, spécifié dans la propriété ID de publicité : TDID, IDFA, AAID, DAID, NAID, IDL, EUID ou UID2. |
| Impression | Chaîne de 36 caractères (y compris des tirets) qui sert d’identifiant unique pour l’impression à laquelle l’événement est attribué. |
| ID de commande | Identifiant de commande associé à l’événement. |
| td1-td10 | Dix propriétés dynamiques personnalisées numérotées de manière séquentielle qui peuvent être utilisées pour fournir des métadonnées de conversion supplémentaires. |

{style="table-layout:auto"}

![La variable [!DNL Basic Request Properties] section présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Voir [!DNL The Trade Desk] documentation destinée aux développeurs pour plus d’informations sur le [propriétés de requête](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) accepté par [!DNL The Trade Desk] API de conversion en temps réel.

**[!UICONTROL Paramètres de requête d’objet]**

Objet JSON contenant plus d’informations. Vous avez la possibilité d’utiliser un jeu réduit d’entrées clé-valeur ou de fournir un fichier JSON brut. De plus, vous pouvez récupérer des données dynamiques d’un élément de données en sélectionnant les disques (![Icône Disque](../../../images/extensions/server/tradedesk/disk-icon.png)) à droite.


![La variable [!DNL Object Request Parameters] pour afficher les champs disponibles.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Voir [Événement de conversion en temps réel](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) pour plus d’informations sur la [!UICONTROL Paramètres de requête d’objet] et leurs propriétés.

**[!UICONTROL Remplacements de configuration]**

>[!NOTE]
>
>La variable [!UICONTROL Remplacements de configuration] vous permet de définir un autre [!DNL Advertiser ID] et/ou [!DNL Merchant ID] sur chaque règle.

| Entrée | Description |
| --- | --- |
| Identifiant annonceur | Identifiant unique de l’annonceur associé à cet événement. Un autre identifiant publicitaire peut être fourni pour remplacer l’identifiant que vous avez fourni dans la configuration de l’extension. |
| Identifiant du marchand | L’identifiant unique que chaque commerçant reçoit de [!DNL The Trade Desk] tout au long de la procédure d’intégration. Un autre identifiant marchand peut être fourni pour remplacer l’identifiant que vous avez fourni dans la configuration de l’extension. |

![La variable [!DNL Configuration Overrides] pour afficher les champs disponibles.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**. Enfin, publiez un nouveau transfert d’événement. [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL The Trade Desk] en utilisant la variable [!DNL The Trade Desk] Extension de l’API Conversions en temps réel. À partir de là, il est recommandé de développer votre intégration en créant des règles distinctes qui envoient des événements de conversion spécifiques selon le cas de chaque campagne. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], lisez le [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).

Voir [!DNL The Trade Desk] documentation sur [bonnes pratiques pour la [!DNL The Trade Desk] API de conversion en temps réel](https://www.facebook.com/business/help/308855623839366?id=818859032317965) pour plus d’informations sur la mise en oeuvre efficace de votre intégration.

Pour plus d’informations sur la façon de déboguer votre implémentation à l’aide de l’outil Experience Platform Debugger et Event Forwarding Monitoring, consultez la section [Adobe Experience Platform Debugger - Aperçu](../../../../debugger/home.md) et [Surveillance des activités dans le transfert d’événement](../../../ui/event-forwarding/monitoring.md).
