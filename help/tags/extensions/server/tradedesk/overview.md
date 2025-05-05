---
title: Présentation de l’extension de l’API de conversion en temps réel du bureau Commerce
description: Découvrez l’extension de l’API de conversion en temps réel de Trade Desk pour le transfert d’événements dans Adobe Experience Platform.
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: eb650da02ac69c5afbebfe6ba371cc19617f79d0
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---

# Présentation de l’extension [!DNL The Trade Desk Real-Time Conversions API]

Vous pouvez utiliser l’extension [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) pour envoyer des données de l’Edge Network Adobe Experience Platform vers [!DNL The Trade Desk] en utilisant les fonctionnalités de l’API dans vos règles de [transfert d’événement](../../../ui/event-forwarding/overview.md).

À l’aide de l’extension [!DNL The Trade Desk Real-Time Conversions API], vous pouvez exploiter les fonctionnalités de l’API dans vos règles de [transfert d’événement](../../../ui/event-forwarding/overview.md) pour envoyer des données à [!DNL The Trade Desk] à partir de l’Edge Network Adobe Experience Platform.

Lisez ce document pour savoir comment installer l’extension et utiliser ses fonctionnalités dans un transfert d’événement [rule](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Cette page d’extension et de documentation est gérée par l’équipe [!DNL The Trade Desk]. Pour toute demande d&#39;information ou de mise à jour, veuillez les contacter directement.

## Conditions préalables {#prerequisites}

Vous devez disposer d’un identifiant publicitaire, d’un identifiant UPixel et d’un identifiant de dispositif de suivi pertinents à partir de votre compte [!DNL The Trade Desk] pour configurer [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Si vous êtes un commerçant, vous devrez également obtenir votre identifiant marchand.

## Installation et configuration de l’API de conversion en temps réel [!DNL The Trade Desk] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou sélectionnez une propriété existante à modifier à la place.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]**, sélectionnez la carte **[!UICONTROL The Trade Desk]** Real-Time Conversions API, puis sélectionnez **[!UICONTROL Installer]**.

![Le catalogue d’extensions présentant l’installation de mise en surbrillance de la carte d’extension [!DNL The Trade Desk].](../../../images/extensions/server/tradedesk/install-extension.png)

Sur l’écran suivant, saisissez l’[!UICONTROL &#x200B; identifiant publicitaire] et éventuellement un [!UICONTROL &#x200B; identifiant commercial]. Vous pouvez coller les ID directement dans ces entrées ou vous pouvez utiliser un élément de données à la place. Ces valeurs serviront de valeurs par défaut lors d’un appel d’événement à l’API de conversions en temps réel [!DNL The Trade Desk]. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

Pour savoir comment créer des éléments de données et les rendre disponibles pour les extensions dans votre propriété de balise, suivez le tutoriel [Créer des éléments de données](https://experienceleague.adobe.com/fr/docs/platform-learn/data-collection/tags/create-data-elements) .

![La page de configuration de l’extension [!DNL The Trade Desk] avec les champs [!UICONTROL Identifiant publicitaire] et [!UICONTROL Identifiant marchand] surlignés.](../../../images/extensions/server/tradedesk/configure-extension.png)

L’extension est installée et vous pouvez désormais utiliser ses fonctionnalités dans vos règles de transfert d’événement.

## Configurer une règle de transfert d’événement {#rule}

Une fois que vous avez installé et configuré l’extension, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent comment et quand vos événements seront envoyés à [!DNL The Trade Desk].

Vous devez envisager de configurer plusieurs règles afin d’envoyer toutes les [propriétés de requête](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) acceptées via [!DNL The Trade Desk] et l’API de conversions en temps réel [!DNL The Trade Desk].

>[!NOTE]
>
>Les événements doivent être envoyés en temps réel ou aussi près que possible du temps réel.

Créez un nouveau transfert d’événement [rule](../../../ui/managing-resources/rules.md) dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL The Trade Desk]**. Sélectionnez ensuite **[!UICONTROL Conversion en temps réel]** pour le **[!UICONTROL Type d’action]**.

![La vue Règles de propriété de transfert d’événement, avec les champs requis pour ajouter une configuration d’action de règle de transfert d’événement mise en surbrillance.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Après la sélection, des contrôles supplémentaires apparaissent pour configurer davantage les données d’événement qui seront envoyées à [!DNL The Trade Desk]. Sélectionnez **[!UICONTROL Conserver les modifications]** pour enregistrer la règle.

Les options de configuration sont divisées en trois sections principales, comme indiqué ci-dessous :

**[!UICONTROL Propriétés de base de la requête]**

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

![La section [!DNL Basic Request Properties] présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Pour plus d’informations sur les [ propriétés de demande ](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) acceptées par l’API de conversions en temps réel [!DNL The Trade Desk], reportez-vous à la documentation destinée aux développeurs [!DNL The Trade Desk].

**[!UICONTROL Paramètres de requête d’objet]**

Objet JSON contenant plus d’informations. Vous avez la possibilité d’utiliser un jeu réduit d’entrées clé-valeur ou de fournir un fichier JSON brut. De plus, vous pouvez récupérer les données dynamiques d’un élément de données en sélectionnant les disques (![Icône de disque](/help/images/icons/database.png)) à droite.


![La section [!DNL Object Request Parameters] présentant les champs disponibles.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Pour plus d’informations sur les [!UICONTROL &#x200B; paramètres de requête d’objet &#x200B;] et leurs propriétés, reportez-vous à la documentation [Evénement de conversion en temps réel](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) .

**[!UICONTROL Remplacements de configuration]**

>[!NOTE]
>
>Les champs [!UICONTROL Configuration Overrides] vous permettent de définir un [!DNL Advertiser ID] et/ou [!DNL Merchant ID] différent sur chaque règle.

| Entrée | Description |
| --- | --- |
| Identifiant annonceur | Identifiant unique de l’annonceur associé à cet événement. Un autre identifiant publicitaire peut être fourni pour remplacer l’identifiant que vous avez fourni dans la configuration de l’extension. |
| Identifiant du marchand | L’identifiant unique que chaque commerçant reçoit par [!DNL The Trade Desk] tout au long de la procédure d’intégration. Un autre identifiant marchand peut être fourni pour remplacer l’identifiant que vous avez fourni dans la configuration de l’extension. |

![La section [!DNL Configuration Overrides] présentant les champs disponibles.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**. Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL The Trade Desk] à l’aide de l’extension [!DNL The Trade Desk] de l’API de conversion en temps réel. À partir de là, il est recommandé de développer votre intégration en créant des règles distinctes qui envoient des événements de conversion spécifiques selon le cas de chaque campagne. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).

Consultez la documentation [!DNL The Trade Desk] sur les [bonnes pratiques pour l’ [!DNL The Trade Desk] API de conversion en temps réel](https://www.facebook.com/business/help/308855623839366?id=818859032317965) pour plus d’informations sur la mise en oeuvre efficace de votre intégration.

Pour plus d’informations sur la façon de déboguer votre mise en oeuvre à l’aide de l’outil Experience Platform Debugger et Event Forwarding Monitoring, consultez les [ &lbrace;présentation des Adobes Experience Platform Debugger](../../../../debugger/home.md) et [Surveillance des activités dans le transfert d’événement](../../../ui/event-forwarding/monitoring.md).
