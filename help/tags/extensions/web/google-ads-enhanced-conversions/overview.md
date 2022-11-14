---
title: Extension Conversions améliorées de Google Ads
description: Découvrez l’extension Conversions améliorées de Google Ads pour le transfert d’événement dans Adobe Experience Platform.
source-git-commit: a279c44ef9df3aa9bfc7763b153b87bde0015d57
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 1%

---

# [!DNL Google Ads] Extension Conversions améliorées

En utilisant la variable [!DNL Google Ads] API, vous pouvez tirer parti de [conversions améliorées](https://support.google.com/google-ads/answer/9888656) en envoyant des données client propriétaires sous la forme d’ajustements de conversion. Google utilise ces données supplémentaires pour améliorer le reporting de vos conversions en ligne générées par les interactions publicitaires.

Le [[!DNL Google Ads] Extension de transfert d’événement Conversions améliorées](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (précédemment appelée [!DNL Enhanced Conversions] (extension) fournit un modèle convivial pour mettre en oeuvre facilement des conversions améliorées pour le [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Les conversions améliorées ne fonctionnent que pour les types de conversion où des données client sont présentes, tels que les abonnements, les inscriptions et les achats. Un ou plusieurs des éléments de données client suivants doivent être disponibles, car ils sont requis lorsque [configuration d’une action de conversion](#conversion-action-event-forwarding) pour une règle de transfert d’événement :
>
>* Adresse électronique (préférée)
>* Nom et adresse du domicile (adresse de la rue, ville, état/région et code postal)
>* Numéro de téléphone (doit être fourni en plus de l’une des deux autres informations ci-dessus)


## Présentation de la mise en œuvre

Les conversions améliorées tirent parti de la [!DNL Google Ads] API permettant d’ajouter des données propriétaires à une conversion survenue sur un appareil client, généralement un site web. Cela signifie qu’il existe deux étapes pour mettre en oeuvre des conversions améliorées :

1. Envoyez une conversion à partir du client.
1. Utilisez le transfert d’événement pour envoyer des données propriétaires supplémentaires qui améliorent les données de conversion envoyées par le client.

>[!TIP]
>
>Pour associer l’événement de conversion côté client aux données propriétaires envoyées à partir du transfert d’événement, la variable `transaction_ID` doit être identique dans les deux appels . Pour plus d’informations sur l’emplacement où cette valeur doit être fournie pour chaque service, consultez les sections sur la configuration des actions de conversion pour [tags](#conversion-action-tags) et [transfert d’événement](#conversion-action-event-forwarding), respectivement.

L’envoi d’événements de conversion impliquant une mise en oeuvre côté client et côté serveur, ce document décrit les étapes préalables à la configuration côté client. [[!DNL Google Global Site Tag] extension (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) en plus de la fonction [!DNL Enhanced Conversions] extension pour le transfert d’événement.

## Envoi d’une conversion à l’aide de balises

Pour envoyer un événement de conversion de sur un site web, procédez comme suit : [!DNL Google Global Site Tag] (gtag) doit être déployé. Pour ce faire, vous pouvez utiliser des balises en configurant et en installant le [!DNL Google Global Site Tag] (gtag) .

### Configurez et installez le [!DNL Google Global Site Tag] extension

Accédez au [!UICONTROL Collecte de données] Interface utilisateur ou interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. Sélectionnez la propriété de balise sur laquelle vous souhaitez installer l’extension, puis cliquez sur **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Sous , **[!UICONTROL Catalogue]** , recherchez la variable [!UICONTROL Balise de site globale Google (gtag)] extension et sélectionner **[!UICONTROL Installer]**.

![Le [!UICONTROL Balise de site globale Google (gtag)] l’extension sélectionnée sous [!UICONTROL Extensions] dans la [!UICONTROL Collecte de données] Interface utilisateur.](../../../images/extensions/google-ads-enhanced-conversions/install-gtag-extension.png)

La boîte de dialogue d’installation s’affiche. À partir de là, sélectionnez **[!UICONTROL Ajouter un compte]** et indiquez les valeurs suivantes lorsque vous y êtes invité :

| Propriété du compte | Description |
| --- | --- |
| Nom de compte | Nom unique du compte. Ce nom est utilisé uniquement dans l’interface utilisateur des balises. |
| Identifiant de compte | Votre [!DNL Google Ads] ID de compte. Pour rechercher cette valeur, connectez-vous à [!DNL Google Ads] et accédez à : **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La chaîne d’identifiant de compte se trouve dans la fenêtre de fragment de code qui commence par `AW-` ou `d`. |
| Produit | Sélectionner **[!UICONTROL Publicités Google (AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Ajouter un compte]**, puis sélectionnez **[!UICONTROL Enregistrer]**.

### Ajout d’une action de conversion d’envoi {#conversion-action-tags}

Après avoir installé l’extension, vous pouvez commencer à inclure des actions de conversion dans vos règles de balise. Lors de la création ou de la modification d’une règle qui écoute la conversion que vous souhaitez améliorer, sélectionnez **[!UICONTROL Ajouter]** under [!UICONTROL Actions]. Dans la boîte de dialogue suivante, sélectionnez **[!UICONTROL Balise de site globale Google (gtag)]** de la [!UICONTROL Extension] menu déroulant, puis sélectionnez **[!UICONTROL Envoi d’un événement]** under [!UICONTROL Type d’action].

![Le [!UICONTROL Envoi d’un événement] type d’action sélectionné dans la vue de configuration des actions du workflow d’édition de règles.](../../../images/extensions/google-ads-enhanced-conversions/select-client-action.png)

D’autres contrôles s’affichent pour vous permettre de configurer la variable [!DNL gtag] . Les champs suivants doivent au minimum être renseignés :

1. **[!UICONTROL Nom de l’événement (action)]**: Entrée `conversion` comme valeur.
1. Ajoutez un nouveau champ où la clé est `transaction_id` et la valeur est une [élément de données](../../../ui/managing-resources/data-elements.md) qui contient le paramètre [transaction ID](https://support.google.com/google-ads/answer/6386790) .
1. **[!UICONTROL Étiquette de conversion]**: Saisissez le libellé de conversion approprié dans votre [!DNL Google Ads] compte . Pour trouver cette valeur, connectez-vous à Google Ads et accédez à **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Le libellé de conversion se trouve sous [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Lorsque vous vous trouvez dans la zone de configuration des balises de votre [!DNL Google Ads] , assurez-vous que les conversions améliorées sont activées. Pour ce faire, passez en revue et acceptez les Conditions d’utilisation, puis sélectionnez **[!DNL Turn on enhanced conversions]** et **[!DNL API]** comme méthode d’implémentation.

Après avoir configuré l’action, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez une nouvelle [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Envoi de données propriétaires à l’aide du transfert d’événement

Une fois que vous avez pu envoyer des événements de conversion du côté client, vous pouvez améliorer ces conversions à l’aide de la variable [!DNL Enhanced Conversions] extension de transfert d’événement.

### Création d’un secret Google OAuth 2 et d’un élément de données {#create-secret-data-element}

Avant de configurer l’extension, vous devez créer un jeton d’accès dans le transfert d’événement pour vous authentifier auprès de [!DNL Google Ads] API.

Consultez le guide sur la [création de secrets de transfert d’événement](../../../ui/event-forwarding/secrets.md) pour obtenir des instructions détaillées. Assurez-vous que vous avez sélectionné **[!UICONTROL Google OAuth 2]** comme type secret. Continuez à suivre les invites. Lorsque vous êtes invité à sélectionner un profil de compte Google, sélectionnez le compte ayant accès à l’action de conversion que vous configurez.

Une fois le secret créé, [créer un élément de données ;](../../../ui/managing-resources/data-elements.md#create-a-data-element) et sélectionnez **[!UICONTROL Secret]** pour le type d’élément de données. Sélectionnez le secret Google OAuth 2 approprié pour chaque environnement et sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

### Configurez et installez le [!DNL Enhanced Conversions] extension {#install-enhanced-conversions}

Recherchez le [!UICONTROL Conversions améliorées de Google Ads] dans le catalogue du transfert d’événements et sélectionnez **[!UICONTROL Installer]**.

![Le [!UICONTROL Conversions améliorées de Google Ads] l’extension sélectionnée sous [!UICONTROL Extensions] dans la [!UICONTROL Collecte de données] Interface utilisateur.](../../../images/extensions/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Pour configurer l’extension, vous devez renseigner les deux champs requis :

1. **[!UICONTROL ID de client]**: L’identifiant qui identifie de manière unique votre [!DNL Google Ads] compte . Pour rechercher cette valeur, connectez-vous à [!DNL Google Ads] et accédez à **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Élément de données de jeton d’accès]**: Sélectionnez l’icône d’élément de données (![Icône Élément de données](../../../images/extensions/google-ads-enhanced-conversions/data-element-icon.png)) et choisissez l’élément de données secret Google OAuth 2 que vous souhaitez [configuré à l’étape précédente](#create-secret-data-element) dans le menu.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour installer l’extension .

### Ajouter un [!UICONTROL Envoyer la conversion] action vers une règle {#conversion-action-event-forwarding}

Une fois l’extension installée, vous pouvez commencer à inclure [!UICONTROL Envoyer la conversion] actions dans vos règles de transfert d’événement. Lors de la création ou de la modification d’une règle qui écoute la conversion que vous souhaitez améliorer, sélectionnez **[!UICONTROL Ajouter]** under [!UICONTROL Actions]. Dans la boîte de dialogue suivante, sélectionnez **[!UICONTROL Conversions améliorées de Google Ads]** de la [!UICONTROL Extension] menu déroulant, puis sélectionnez **[!UICONTROL Envoyer la conversion]** under [!UICONTROL Type d’action].

![Le [!UICONTROL Envoyer la conversion] type d’action sélectionné dans la vue de configuration des actions du workflow d’édition de règles.](../../../images/extensions/google-ads-enhanced-conversions/select-server-action.png)

De nouveaux contrôles s’affichent dans le panneau de droite qui vous permettent de configurer votre conversion. Les champs suivants doivent au minimum être renseignés :

**Informations sur la conversion**

| Entrée | Description |
| --- | --- |
| Client Identifiant | Votre [!DNL Google Ads] ID de client. La valeur par défaut est l’ID de client que vous avez saisi lors de la [installation de l’extension](#install-enhanced-conversions). |
| Identifiant de conversion ou libellé de conversion | Valeurs de suivi obtenues à partir de [!DNL Google Ads] lors de la configuration du suivi des conversions. Les valeurs commencent par `AW-`.<br><br>Pour plus d’informations sur la manière de trouver ces valeurs, reportez-vous à la section [[!DNL Google Ads] documentation](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Identifiant de transaction | Sélectionnez un élément de données ayant la même valeur d’ID de transaction que celle qui est [envoyé du côté client](#conversion-action-tags) en utilisant la variable [!DNL Google Global Site Tag] extension . |

**Identification de l’utilisateur**

* Au moins l’un des trois identifiants d’utilisateur doit être inclus :
   * E-mail
   * Numéro de téléphone
   * Adresse complète

>[!TIP]
>
>Les données d’identification de l’utilisateur doivent être hachées avant d’être envoyées à Google. Si les données ne sont pas hachées lorsque le transfert d’événement les reçoit, sélectionnez la variable **[!UICONTROL Normalisation et hachage]** basculez sur un champ donné pour indiquer à l’extension de hacher la valeur.
>
>![Le [!UICONTROL Normalisation et hachage] bascule activé pour la variable [!UICONTROL Email] entrée dans la fonction [!UICONTROL Envoyer la conversion] formulaire de configuration des actions.](../../../images/extensions/google-ads-enhanced-conversions/hash-user-id-values.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement. [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion à [!DNL Google Ads] en utilisant la variable [!DNL Enhanced Conversions] extension de transfert d’événement. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans Experience Platform, reportez-vous à la section [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).
