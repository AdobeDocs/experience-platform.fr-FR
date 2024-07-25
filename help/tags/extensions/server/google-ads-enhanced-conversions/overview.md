---
title: Extension Conversions améliorées de Google Ads
description: Découvrez l’extension Conversions améliorées de Google Ads pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# [!DNL Google Ads] Extension de conversion améliorée

À l’aide de l’API [!DNL Google Ads], vous pouvez exploiter les [conversions améliorées](https://support.google.com/google-ads/answer/9888656) en envoyant des données client propriétaires sous la forme d’ajustements de conversion. Google utilise ces données supplémentaires pour améliorer le reporting de vos conversions en ligne générées par les interactions publicitaires.

L’ [[!DNL Google Ads]  extension de transfert d’événement de conversion améliorée](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (précédemment appelée extension [!DNL Enhanced Conversions]) fournit un modèle convivial pour mettre en oeuvre facilement des conversions améliorées pour l’API [!DNL Google Ads].

>[!IMPORTANT]
>
>Les conversions améliorées ne fonctionnent que pour les types de conversion où des données client sont présentes, tels que les abonnements, les inscriptions et les achats. Un ou plusieurs des éléments de données client suivants doivent être disponibles, car ils sont requis lors de la [configuration d’une action de conversion](#conversion-action-event-forwarding) pour une règle de transfert d’événement :
>
>* Adresse électronique (préférée)
>* Nom et adresse du domicile (adresse de la rue, ville, état/région et code postal)
>* Numéro de téléphone (doit être fourni en plus de l’une des deux autres informations ci-dessus)

## Présentation de l’implémentation

Les conversions améliorées tirent parti de l’API [!DNL Google Ads] pour ajouter des données propriétaires à une conversion qui s’est produite sur un appareil client, généralement un site web. Cela signifie qu’il existe deux étapes pour mettre en oeuvre des conversions améliorées :

1. Envoyez une conversion à partir du client.
1. Utilisez le transfert d’événement pour envoyer des données propriétaires supplémentaires qui améliorent les données de conversion envoyées par le client.

>[!TIP]
>
>Pour associer l’événement de conversion côté client aux données propriétaires envoyées à partir du transfert d’événement, `transaction_ID` doit être le même dans les deux appels. Pour plus d’informations sur l’emplacement où cette valeur doit être fournie pour chaque service, consultez les sections sur la configuration des actions de conversion pour les [balises](#conversion-action-tags) et le [transfert d’événement](#conversion-action-event-forwarding), respectivement.

Puisque l’envoi d’événements de conversion implique une mise en oeuvre côté client et côté serveur, ce document couvre les étapes préalables à la configuration de l’extension [[!DNL Google Global Site Tag]  (gtag) côté client](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) en plus de l’extension [!DNL Enhanced Conversions] pour le transfert d’événement.

La vidéo suivante présente l’extension [!DNL Enhanced Conversions] et décrit les étapes de mise en oeuvre à un niveau élevé :

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Envoi d’une conversion à l’aide de balises

Pour envoyer un événement de conversion de sur un site web, [!DNL Google Global Site Tag] (gtag) doit être déployé. Pour ce faire, vous pouvez utiliser des balises en configurant et en installant l’extension [!DNL Google Global Site Tag] (gtag).

### Configuration et installation de l’extension [!DNL Google Global Site Tag]

Accédez à l’interface utilisateur de [!UICONTROL collecte de données] ou l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. Sélectionnez la propriété de balise sur laquelle vous souhaitez installer l’extension, puis sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Sous l’onglet **[!UICONTROL Catalogue]**, recherchez l’extension [!UICONTROL Google Global Site Tag (gtag)] et sélectionnez **[!UICONTROL Installer]**.

![L’extension [!UICONTROL Google Global Site Tag (gtag)] sélectionnée sous la vue [!UICONTROL Extensions] dans l’interface utilisateur de [!UICONTROL collecte de données].](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

La boîte de dialogue d’installation s’affiche. À partir de là, sélectionnez **[!UICONTROL Ajouter un compte]** et fournissez les valeurs suivantes lorsque vous y êtes invité :

| Propriété du compte | Description |
| --- | --- |
| Nom de compte | Nom unique du compte. Ce nom est utilisé uniquement dans l’interface utilisateur des balises. |
| Identifiant de compte | Votre ID de compte [!DNL Google Ads]. Pour trouver cette valeur, connectez-vous à [!DNL Google Ads] et accédez à : **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La chaîne d’ID de compte se trouve dans la fenêtre de fragment de code qui commence par `AW-` ou `d`. |
| Produit | Sélectionnez **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Ajouter un compte]**, puis **[!UICONTROL Enregistrer]**.

### Ajout d’une action de conversion d’envoi {#conversion-action-tags}

Après avoir installé l’extension, vous pouvez commencer à inclure des actions de conversion dans vos règles de balise. Lors de la création ou de la modification d’une règle qui écoute la conversion que vous souhaitez améliorer, sélectionnez **[!UICONTROL Ajouter]** sous [!UICONTROL Actions]. Dans la boîte de dialogue suivante, sélectionnez **[!UICONTROL Google Global Site Tag (gtag)]** dans la liste déroulante [!UICONTROL Extension], puis sélectionnez **[!UICONTROL Envoyer un événement]** sous [!UICONTROL Type d’action].

![Type d’action [!UICONTROL Envoyer un événement] sélectionné dans la vue de configuration des actions du workflow d’édition de règles.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

D’autres contrôles s’affichent, vous permettant de configurer l’événement [!DNL gtag]. Les champs suivants doivent au minimum être renseignés :

1. **[!UICONTROL Nom de l’événement (Action)]** : entrez `conversion` comme valeur.
1. Ajoutez un nouveau champ où la clé est `transaction_id` et la valeur est un [élément de données](../../../ui/managing-resources/data-elements.md) qui contient la valeur [transaction ID](https://support.google.com/google-ads/answer/6386790).
1. **[!UICONTROL Étiquette de conversion]** : saisissez l’étiquette de conversion appropriée de votre compte [!DNL Google Ads]. Pour trouver cette valeur, connectez-vous à Google Ads et accédez à **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Le libellé de conversion se trouve sous [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Pendant que vous vous trouvez dans la zone de configuration des balises de votre compte [!DNL Google Ads], assurez-vous que les conversions améliorées sont activées. Pour ce faire, passez en revue et acceptez les Conditions d’utilisation, puis sélectionnez **[!DNL Turn on enhanced conversions]** et **[!DNL API]** comme méthode de mise en oeuvre.

Après avoir configuré l’action, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Envoi de données propriétaires à l’aide du transfert d’événement

Une fois que vous avez la possibilité d’envoyer des événements de conversion du côté client, vous pouvez améliorer ces conversions à l’aide de l’extension de transfert d’événement [!DNL Enhanced Conversions].

### Création d’un secret Google OAuth 2 et d’un élément de données {#create-secret-data-element}

Avant de configurer l’extension, vous devez créer un jeton d’accès dans le transfert d’événement pour vous authentifier à l’API [!DNL Google Ads].

Pour obtenir des instructions détaillées, consultez le guide sur la [création de secrets de transfert d’événement](../../../ui/event-forwarding/secrets.md) . Veillez à sélectionner **[!UICONTROL Google OAuth 2]** comme type secret. Continuez à suivre les invites. Lorsque vous êtes invité à sélectionner un profil de compte Google, sélectionnez le compte ayant accès à l’action de conversion que vous configurez.

Une fois le secret créé, [créez un élément de données](../../../ui/managing-resources/data-elements.md#create-a-data-element) et sélectionnez **[!UICONTROL Secret]** pour le type d’élément de données. Sélectionnez le secret Google OAuth 2 approprié pour chaque environnement et sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

### Configuration et installation de l’extension [!DNL Enhanced Conversions] {#install-enhanced-conversions}

Recherchez l’extension [!UICONTROL Google Ads Enhanced Conversions] dans le catalogue de transfert d’événement et sélectionnez **[!UICONTROL Install]**.

![L’extension [!UICONTROL Google Ads Enhanced Conversions] sélectionnée sous la vue [!UICONTROL Extensions] dans l’interface utilisateur [!UICONTROL Data Collection].](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Pour configurer l’extension, vous devez renseigner les deux champs requis :

1. **[!UICONTROL ID de client]** : identifiant qui identifie de manière unique votre compte [!DNL Google Ads]. Pour trouver cette valeur, connectez-vous à [!DNL Google Ads] et accédez à **[!DNL Help]** > **[!DNL Customer ID]**.
2. **[!UICONTROL Access Token Data Element]** : sélectionnez l’icône d’élément de données (![Icône d’élément de données](/help/images/icons/database.png)) et choisissez l’élément de données secret Google OAuth 2 que vous [ avez ](#create-secret-data-element) configuré à l’étape précédente dans le menu.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour installer l’extension.

### Ajouter une action [!UICONTROL Envoyer la conversion] à une règle {#conversion-action-event-forwarding}

Une fois l’extension installée, vous pouvez commencer à inclure des actions [!UICONTROL Envoyer la conversion] dans vos règles de transfert d’événement. Lors de la création ou de la modification d’une règle qui écoute la conversion que vous souhaitez améliorer, sélectionnez **[!UICONTROL Ajouter]** sous [!UICONTROL Actions]. Dans la boîte de dialogue suivante, sélectionnez **[!UICONTROL Google Ads Enhanced Conversions]** dans la liste déroulante [!UICONTROL Extension], puis sélectionnez **[!UICONTROL Send Conversion]** sous [!UICONTROL Action Type].

![ Le type d&#39;action [!UICONTROL Envoyer la conversion] sélectionné dans la vue de configuration des actions du workflow d&#39;édition de règles.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

De nouveaux contrôles s’affichent dans le panneau de droite qui vous permettent de configurer votre conversion. Les champs suivants doivent au minimum être renseignés :

**Informations de conversion**

| Entrée | Description |
| --- | --- |
| Identifiant client | Votre ID de client [!DNL Google Ads]. La valeur par défaut est l’ID de client que vous avez saisi lors de l’ [installation de l’extension](#install-enhanced-conversions). |
| Identifiant de conversion ou libellé de conversion | Valeurs de suivi obtenues à partir de [!DNL Google Ads] lors de la configuration du suivi de conversion. Les valeurs commencent par `AW-`.<br><br>Pour plus d&#39;informations sur la recherche de ces valeurs, consultez la [[!DNL Google Ads] documentation](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Identifiant de transaction | Sélectionnez un élément de données ayant la même valeur d’ID de transaction que [envoyé du côté client](#conversion-action-tags) à l’aide de l’extension [!DNL Google Global Site Tag]. |

**Identification de l’utilisateur**

* Au moins l’un des trois identifiants d’utilisateur doit être inclus :
   * E-mail
   * Numéro de téléphone
   * Adresse complète

>[!TIP]
>
>Les données d’identification de l’utilisateur doivent être hachées avant d’être envoyées à Google. Si les données ne sont pas hachées lorsque le transfert d’événement les reçoit, sélectionnez le bouton d’activation/désactivation **[!UICONTROL Normaliser et hachage]** sur un champ donné pour demander à l’extension de hacher la valeur.
>
>![Le bouton bascule [!UICONTROL Normaliser et hachage] activé pour l’entrée [!UICONTROL Email] dans le formulaire de configuration de l’action [!UICONTROL Envoyer la conversion].](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion à [!DNL Google Ads] à l’aide de l’extension de transfert d’événement [!DNL Enhanced Conversions]. Pour plus d’informations sur les fonctionnalités de transfert d’événement en Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
