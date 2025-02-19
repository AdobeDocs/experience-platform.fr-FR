---
title: Extension des conversions améliorées de Google Ads
description: Découvrez l’extension Google Ads Enhanced Conversions pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# Extension [!DNL Google Ads] Enhanced Conversions

Grâce à l’API [!DNL Google Ads], vous pouvez tirer parti des [conversions améliorées](https://support.google.com/google-ads/answer/9888656) en envoyant des données client propriétaires sous la forme d’ajustements de conversion. Google utilise ces données supplémentaires pour améliorer la création de rapports sur vos conversions en ligne pilotées par les interactions publicitaires.

L’extension de transfert d’événement [[!DNL Google Ads] Enhanced Conversions](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (auparavant appelée extension [!DNL Enhanced Conversions]) fournit un modèle convivial pour mettre en œuvre facilement des conversions améliorées pour l’API [!DNL Google Ads].

>[!IMPORTANT]
>
>Les conversions améliorées ne fonctionnent que pour les types de conversion où les données client sont présentes, comme les abonnements, les inscriptions et les achats. Une ou plusieurs des données client suivantes doivent être disponibles, car elles sont requises lors de la [configuration d’une action de conversion](#conversion-action-event-forwarding) pour une règle de transfert d’événement :
>
>* Adresse e-mail (préférée)
>* Nom et adresse (rue, ville, état/région et code postal)
>* Numéro de téléphone (doit être fourni en plus de l’un des deux autres éléments d’information ci-dessus)

## Présentation de l’implémentation

Les conversions améliorées tirent parti de l’API [!DNL Google Ads] pour ajouter des données propriétaires à une conversion qui s’est produite sur un appareil client, généralement un site web. Cela signifie qu’il existe deux étapes pour implémenter des conversions améliorées :

1. Envoyez une conversion à partir du client.
1. Utilisez le transfert d’événement pour envoyer des données propriétaires supplémentaires qui améliorent les données de conversion envoyées à partir du client.

>[!TIP]
>
>Pour associer l’événement de conversion côté client aux données propriétaires envoyées à partir du transfert d’événement, la `transaction_ID` doit être la même dans les deux appels. Pour plus d’informations sur les endroits où cette valeur doit être fournie pour chaque service, consultez les sections sur la configuration des actions de conversion pour [balises](#conversion-action-tags) et [transfert d’événement](#conversion-action-event-forwarding), respectivement.

Comme l’envoi d’événements de conversion implique une implémentation côté client et côté serveur, ce document couvre les étapes préalables à la configuration de l’extension [[!DNL Google Global Site Tag]  côté client (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) en plus de l’extension [!DNL Enhanced Conversions] pour le transfert d’événement.

La vidéo suivante présente l’extension [!DNL Enhanced Conversions] et décrit les étapes d’implémentation à un haut niveau :

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Envoyer une conversion à l’aide de balises

Pour envoyer un événement de conversion à partir d’un site web, [!DNL Google Global Site Tag] (gtag) doit être déployé. Pour ce faire, vous pouvez utiliser les balises en configurant et en installant l’extension [!DNL Google Global Site Tag] (gtag).

### Configuration et installation de l’extension [!DNL Google Global Site Tag]

Accédez à l’interface utilisateur [!UICONTROL Collecte de données] ou Experience Platform, puis sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. Sélectionnez la propriété de balise sur laquelle vous souhaitez installer l’extension, puis sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Sous l’onglet **[!UICONTROL Catalogue]**, recherchez l’extension [!UICONTROL Google Global Site Tag (gtag)] et sélectionnez **[!UICONTROL Installer]**.

![L’extension [!UICONTROL Google Global Site Tag (gtag)] sélectionnée sous la vue [!UICONTROL Extensions] dans l’interface utilisateur [!UICONTROL Collecte de données].](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

La boîte de dialogue d’installation s’affiche. À partir de là, sélectionnez **[!UICONTROL Ajouter un compte]** et indiquez les valeurs suivantes lorsque vous y êtes invité :

| Propriété du compte | Description |
| --- | --- |
| Nom de compte | Nom unique du compte. Ce nom est uniquement utilisé dans l’interface utilisateur des balises. |
| Identifiant de compte | Identifiant de votre compte [!DNL Google Ads]. Pour trouver cette valeur, connectez-vous à [!DNL Google Ads] et accédez à : **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La chaîne d’identifiant de compte se trouve dans la fenêtre de fragment de code qui commence par `AW-` ou `d`. |
| Produit | Sélectionnez **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Ajouter un compte]** puis **[!UICONTROL Enregistrer]**.

### Ajouter une action de conversion d’envoi {#conversion-action-tags}

Après avoir installé l’extension, vous pouvez commencer à inclure des actions de conversion dans vos règles de balise. Lors de la création ou de la modification d’une règle qui écoute la conversion que vous souhaitez améliorer, sélectionnez **[!UICONTROL Ajouter]** sous [!UICONTROL Actions]. Dans la boîte de dialogue suivante, sélectionnez **[!UICONTROL Google Global Site Tag (gtag)]** dans la liste déroulante [!UICONTROL Extension], puis sélectionnez **[!UICONTROL Envoyer un événement]** sous [!UICONTROL Type d’action].

![Le type d’action [!UICONTROL Envoyer un événement] sélectionné dans la vue de configuration d’action du workflow d’édition de règles.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

D’autres commandes s’affichent pour vous permettre de configurer l’événement [!DNL gtag]. Au minimum, les champs suivants doivent être renseignés :

1. **[!UICONTROL Nom de l’événement (action)]** : saisissez `conversion` comme valeur.
1. Ajoutez un nouveau champ dans lequel la clé est `transaction_id` et la valeur est un [élément de données](../../../ui/managing-resources/data-elements.md) contenant la valeur [ID de transaction](https://support.google.com/google-ads/answer/6386790).
1. **[!UICONTROL Libellé de conversion]** : saisissez le libellé de conversion approprié à partir de votre compte [!DNL Google Ads]. Pour trouver cette valeur, connectez-vous à Google Ads et accédez à **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Le libellé de conversion se trouve sous [!DNL Instructions].

   >[!IMPORTANT]
   >
   >Lorsque vous êtes dans la zone de configuration des balises de votre compte [!DNL Google Ads], assurez-vous que les conversions améliorées sont activées. Pour ce faire, examinez et acceptez les Conditions d’utilisation, puis sélectionnez **[!DNL Turn on enhanced conversions]** et **[!DNL API]** comme méthode de mise en œuvre.

Après avoir configuré l’action, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous convient, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez une nouvelle version [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Envoi de données propriétaires à l’aide du transfert d’événement

Une fois que vous avez la possibilité d’envoyer des événements de conversion du côté client, vous pouvez améliorer ces conversions à l’aide de l’extension de transfert d’événement [!DNL Enhanced Conversions].

### Création d’un secret OAuth 2 Google et d’un élément de données {#create-secret-data-element}

Avant de configurer l’extension, vous devez créer un jeton d’accès dans le transfert d’événement pour vous authentifier auprès de l’API [!DNL Google Ads].

Consultez le guide sur la [création de secrets de transfert d’événement](../../../ui/event-forwarding/secrets.md) pour obtenir des instructions détaillées. Assurez-vous de sélectionner **[!UICONTROL Google OAuth 2]** comme type de secret. Continuez à suivre les invites et, lorsque vous êtes invité à sélectionner un profil de compte Google, sélectionnez le compte ayant accès à l&#39;action de conversion que vous configurez.

Une fois le secret créé, [créez un nouvel élément de données](../../../ui/managing-resources/data-elements.md#create-a-data-element) et sélectionnez **[!UICONTROL Secret]** pour le type d’élément de données. Sélectionnez le secret OAuth 2 Google approprié pour chaque environnement et sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

### Configuration et installation de l’extension [!DNL Enhanced Conversions] {#install-enhanced-conversions}

Recherchez l’extension [!UICONTROL Google Ads Enhanced Conversions] dans le catalogue du transfert d’événements et sélectionnez **[!UICONTROL Installer]**.

![L’extension [!UICONTROL Google Ads Enhanced Conversions] sélectionnée sous la vue [!UICONTROL Extensions] dans l’interface utilisateur [!UICONTROL Collecte de données].](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Pour configurer l’extension, vous devez renseigner les deux champs obligatoires :

1. **[!UICONTROL Identifiant client]** : l’identifiant qui identifie votre compte [!DNL Google Ads] de manière unique. Pour trouver cette valeur, connectez-vous à [!DNL Google Ads] et accédez à **[!DNL Help]** > **[!DNL Customer ID]**.
2. **[!UICONTROL Élément de données de jeton d’accès]** : sélectionnez l’icône de l’élément de données (![icône d’élément de données](/help/images/icons/database.png)) et choisissez l’élément de données secret OAuth 2 de Google que vous [avez configuré à l’étape précédente](#create-secret-data-element) dans le menu.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour installer l’extension.

### Ajouter une action [!UICONTROL Envoyer une conversion] à une règle {#conversion-action-event-forwarding}

Une fois l’extension installée, vous pouvez commencer à inclure les actions [!UICONTROL Envoyer la conversion] dans vos règles de transfert d’événement. Lors de la création ou de la modification d’une règle qui écoute la conversion que vous souhaitez améliorer, sélectionnez **[!UICONTROL Ajouter]** sous [!UICONTROL Actions]. Dans la boîte de dialogue suivante, sélectionnez **[!UICONTROL Conversions améliorées de Google Ads]** dans la liste déroulante [!UICONTROL Extension], puis sélectionnez **[!UICONTROL Envoyer la conversion]** sous [!UICONTROL Type d’action].

![Le type d’action [!UICONTROL Envoyer la conversion] sélectionné dans la vue de configuration des actions du workflow d’édition de règles.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

De nouvelles commandes s’affichent dans le panneau de droite pour vous permettre de configurer votre conversion. Au minimum, les champs suivants doivent être renseignés :

**Informations de conversion**

| Entrée | Description |
| --- | --- |
| Identifiant client | Votre ID de client [!DNL Google Ads]. La valeur par défaut est l’ID de client que vous avez saisi lors de [installation de l’extension](#install-enhanced-conversions). |
| ID de conversion ou libellé de conversion | Valeurs de tracking obtenues depuis [!DNL Google Ads] lors de la configuration du tracking des conversions. Les valeurs commencent par `AW-`.<br><br>Pour plus d’informations sur la façon de trouver ces valeurs, consultez la [[!DNL Google Ads] documentation](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Identifiant de transaction | Sélectionnez un élément de données ayant la même valeur d’ID de transaction [envoyé du côté client](#conversion-action-tags) à l’aide de l’extension [!DNL Google Global Site Tag]. |

**Identification de l&#39;utilisateur**

* Au moins un des trois identifiants d’utilisateur doit être inclus :
   * E-mail
   * Numéro de téléphone
   * Adresse complète

>[!TIP]
>
>Les données d’identification utilisateur doivent être hachées avant d’être envoyées à Google. Si les données ne sont pas hachées lorsque le transfert d’événement les reçoit, activez le bouton (bascule) **[!UICONTROL Normaliser et hacher]** sur un champ donné pour demander à l’extension de hacher la valeur.
>
>![Le bouton (bascule) [!UICONTROL Normaliser et hacher] activé pour l’entrée [!UICONTROL E-mail] dans le formulaire de configuration de l’action [!UICONTROL Envoyer la conversion].](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous convient, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion à [!DNL Google Ads] à l’aide de l’extension de transfert d’événement [!DNL Enhanced Conversions]. Pour plus d’informations sur les fonctionnalités de transfert d’événement d’Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
