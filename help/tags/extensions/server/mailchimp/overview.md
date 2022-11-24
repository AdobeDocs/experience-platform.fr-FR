---
title: Présentation de l’extension Mailchimp
description: Utilisez le transfert d’événement pour déclencher les emails des chimpanzés de courrier électronique.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 7%

---

# Présentation de l’extension de transfert d’événement Mailchimp

>[!NOTE]
>  
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.

Le Mailchimp [transfert d’événement](../../../ui/event-forwarding/overview.md) L’extension envoie des événements à l’API marketing Mailchimp qui peut déclencher des courriers électroniques pour des campagnes marketing, des parcours ou des transactions Mailchimp.

Ce document explique comment configurer l’extension et les règles à l’aide de l’action Ajouter un événement .

## Conditions préalables

Ce document suppose que vous connaissez les produits Mailchimp pertinents utilisés par l’extension. Pour plus d’informations, consultez la documentation d’aide de Mailchimp pour [campagnes](https://mailchimp.com/help/getting-started-with-campaigns/), [parcours](https://mailchimp.com/help/about-customer-journeys/), et [transactions](https://mailchimp.com/help/transactional/).

Un compte Mailchimp est requis pour utiliser cette extension. Vous pouvez vous inscrire à un compte [here](https://login.mailchimp.com/signup/). Dans le tableau de bord du compte Mailchimp, notez les valeurs suivantes à utiliser dans ce guide :

- Votre préfixe de domaine Mailchimp
- Votre clé API
- ID d’audience
- Adresse email &quot;expéditeur&quot; par défaut

En fonction de votre forfait de compte Mailchimp, vous avez peut-être un accès limité aux outils de Parcours client Mailchimp.

>[!TIP]
>  
>Si vous utilisez des automatisations Mailchimp comme les emails transactionnels ou les Parcours client, les étapes et les écrans peuvent être légèrement différents de celles répertoriées ici. Cependant, vous avez toujours besoin des mêmes informations pour utiliser cette extension, comme décrit ci-dessus. Voir [Centre d&#39;aide de Mailchimp](https://mailchimp.com/help/) pour plus d’informations sur chacune de ces valeurs pour votre compte et votre plan spécifiques.

### Préfixe de domaine

Après vous être connecté à Mailchimp et avoir accédé à la vue Tableau de bord, la barre d’adresse de votre navigateur doit afficher une URL telle que `https://us11.admin.mailchimp.com` ou juste `us11.admin.mailchimp.com`. Dans cet exemple, le préfixe `us11` est simplement un espace réservé et votre valeur sera différente. Enregistrez votre URL avec votre préfixe pour une étape ultérieure.

### Clé API

Pour trouver la clé d’API de votre compte, sélectionnez l’icône de votre profil dans l’interface utilisateur de messagerie, puis cliquez sur **Profil**. Vous devriez voir une URL telle que `https://us11.admin.mailchimp.com/account/profile/` mais avec **your** préfixe au lieu de `us11`.

Sélectionner **Extras**, puis **Clés API**:

![Menu Extraits, lien Clés API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Sous **Vos clés d’API**, vous pouvez choisir une clé existante ou sélectionner **Créer Une Clé** pour en créer un. Vous pouvez créer une clé à utiliser spécifiquement avec cette extension. Copiez la clé API et enregistrez-la pour une étape ultérieure. Pour plus d’informations, consultez la documentation de Mailchimp sur la façon de [générer votre clé API ;](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID d’audience et adresse de l’expéditeur

Sélectionner **Audience** dans le volet de navigation de gauche, puis **Tableau de bord Audience**. Sélectionnez ensuite l’audience que vous prévoyez d’utiliser avec cette extension. Pour en savoir plus, consultez le document Mailchimp sur [création d’une audience](https://mailchimp.com/help/create-audience/).

Une fois votre audience créée et sélectionnée, sélectionnez la variable **Gestion de l’audience** menu déroulant et choisissez **Paramètres**. Cet écran affiche divers paramètres pour votre audience.

Au bas de l’écran Paramètres, vous devriez voir `Unique id for audience [audience name]` where `[audience name]` est le nom de votre audience réelle. Copiez l’ID d’audience et enregistrez-le pour une étape ultérieure.

Sélectionner **Nom et valeurs par défaut de l’audience** et confirmez que **Adresse électronique de l’expéditeur par défaut** a la valeur correcte pour vos campagnes. Notez que l’ID d’audience est également répertorié en haut de cette page et qu’il s’agit de la même valeur que celle que vous avez copiée à l’étape précédente.

## Automatisation des emails

Selon votre forfait Mailchimp et si vous utilisez des emails transactionnels, des Parcours client ou d’autres automatisations Mailchimp, vos paramètres de parcours spécifiques peuvent varier.

>[!IMPORTANT]
>  
>Le nom de l’événement que vous avez choisi de déclencher votre automatisation ou votre parcours dans Mailchimp est le même nom que celui que vous devez envoyer avec cette extension. Notez le nom de l’événement dans votre automatisation Mailchimp et enregistrez-le pour une étape ultérieure.

## Installation et configuration

Cette section répertorie les étapes d’installation et de configuration de l’extension. Pour enregistrer la clé API Mailchimp en toute sécurité, vous devez utiliser le transfert d’événement [secrets](../../../ui/event-forwarding/secrets.md).

### Création d’un secret et d’un élément de données

Dans une propriété de transfert d’événement, [créer une [!UICONTROL Jeton] secret](../../../ui/event-forwarding/secrets.md#token) appelé `Mailchimp API Key`.

Ensuite, [créer un élément de données ;](../../../ui/managing-resources/data-elements.md#create-a-data-element) en utilisant la variable [!UICONTROL Core] et une [!UICONTROL Secret] type d’élément de données pour référencer la variable `Mailchimp API Key` secret que vous venez de créer. Entrée `Mailchimp Token` comme nom de l’élément de données.

### Installation et configuration de l’extension 

Dans la même propriété de transfert d’événement, sélectionnez **[!UICONTROL Extensions],** then **[!UICONTROL Catalogue]** pour afficher les extensions disponibles pour l’installation. À partir de là, recherchez l’extension Mailchimp et sélectionnez **[!UICONTROL Installer]**.

![Installer l’extension Mailchimp](../../../images/extensions/server/mailchimp/install.png)

L’écran de configuration s’affiche. Sous **[!UICONTROL Nom de domaine du préfixe de serveur Mailchimp]**, saisissez le domaine que vous avez copié précédemment à partir de votre compte Mailchimp, y compris votre préfixe de domaine unique.

>[!IMPORTANT]
>
>Ne pas inclure `http://` ou `https://` dans ce champ.

![Configurations d’extension](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Sous **[!UICONTROL Jeton Mailchimp]**, sélectionnez l’icône de l’élément de données et choisissez la variable `Mailchimp Token` élément de données que vous avez créé précédemment. Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer les modifications.

L’extension est maintenant installée et configurée pour être utilisée dans votre propriété.

## Collecte de données

Lors de l’utilisation de cette extension dans une [règle](../../../ui/managing-resources/rules.md), il existe plusieurs valeurs de données que l’extension envoie à Mailchimp avec chaque événement. Pour une mise en oeuvre type, vous pouvez configurer la variable [Extension SDK Web Adobe Experience Platform](../../client/sdk/overview.md) pour envoyer ces données à [!DNL Platform Edge Network] à utiliser par l’extension dans la propriété de transfert d’événement.

Les données requises par cette extension peuvent être envoyées à partir du SDK Web sous forme de données XDM ou de données non XDM. Consultez la documentation pour en savoir plus sur [envoi de données XDM](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

Par exemple, si un client effectue un achat ou s’inscrit pour un événement sur votre site, vous pouvez envoyer un email de confirmation par le biais de Mailchimp avec cette extension. Une fois que vous avez envoyé les informations requises du SDK Web vers le réseau Edge, l’extension déclenche le courrier électronique avec Mailchimp.

![Ajout de la configuration des actions d’événement](../../../images/extensions/server/mailchimp/action-configurations.png)

### Éléments de données

La capture d’écran de la section précédente montre les données que vous pouvez envoyer avec chaque événement de cette extension à Mailchimp. Une fois que vous avez configuré le SDK Web pour envoyer ces données au réseau Edge, vous pouvez créer des éléments de données dans la propriété de transfert d’événement afin que l’extension puisse accéder à ces valeurs.

Le tableau ci-dessous fournit des détails supplémentaires pour chaque valeur possible.

| Nom | Exemple de chemin | Type | Description | Obligatoire | Limites |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> ou<br /> `arc.event.data._tenant.emailId` | Chaîne | Adresse de réception du courrier électronique | **Oui** | Doit exister dans l’audience Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> ou<br /> `arc.event.data._tenant.listid` | Chaîne | Audience ID | **Oui** | Doit correspondre à un ID d’audience existant |
| `name` | `arc.event.xdm._tenant.name`<br /> ou<br /> `arc.event.data._tenant.name` | Chaîne | Nom de l’événement | **Oui** | 2 à 30 caractères de longueur |
| `properties` | `arc.event.xdm._tenant.properties`<br /> ou<br /> `arc.event.data._tenant.properties` | Objet | Liste facultative des propriétés au format JSON avec des détails sur l’événement. | Non |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> ou<br /> `arc.event.data._tenant.isSyncing` | booléen | Événements créés avec `is_syncing` défini sur `true` **ne sera pas** automates de déclenchement | Non |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> ou `arc.event.data._tenant.occuredAt`. | Chaîne | Horodatage ISO 8601 du moment où l’événement s’est produit | Non |  |

{style=&quot;table-layout:auto&quot;}

>[!IMPORTANT]
>  
>Le **Exemple de chemin** les valeurs ci-dessus ne sont que des exemples. Les noms des champs et [paths](../../../ui/event-forwarding/overview.md#data-element-path) les éléments de données référencés dans ces éléments peuvent être différents dans votre propriété, selon la manière dont vous avez nommé et configuré le SDK Web dans les étapes ci-dessus.

Dans la propriété de transfert d’événement, vous pouvez créer un élément de données pour chacun des champs décrits ci-dessus. Une fois créés, vous pouvez référencer les éléments de données dans le [!UICONTROL Ajouter un événement] de cette extension.

![Ajout de la configuration des actions d’événement](../../../images/extensions/server/mailchimp/action-configurations.png)

Vous pouvez maintenant utiliser cette extension et l’action Ajouter un événement pour déclencher les emails des chimpanzés de courrier électronique pour vos audiences.

## Validation des données

Lorsque vous utilisez des extensions de transfert d’événement, la variable [Débogueur Adobe Experience Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) est très utile. Dans la section Logs (Journaux), sous Edge logs, vous pouvez voir les requêtes effectuées par vos règles de transfert d’événement après leur déclenchement. Les captures d’écran suivantes présentent une demande envoyée à l’API Mailchimp par l’extension.

![Débogueur Adobe Experience Platform](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Dans le tableau de bord Mailchimp, dans la vue Flux d’activité de votre audience ou membre d’audience, une liste d’événements pour ce membre d’audience ou d’audience est fournie. Cela doit correspondre aux événements envoyés par l’extension et afficher toutes les données facultatives envoyées, ainsi que l’email ou la campagne qu’ils ont reçu. Voir [Guides d’aide sur l’automatisation des emails](https://mailchimp.com/help/automation/) pour plus d’informations.
