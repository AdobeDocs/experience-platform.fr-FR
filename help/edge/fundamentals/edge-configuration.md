---
title: Configuration Edge
seo-title: Configuration Edge pour le SDK Web Experience Platform
description: 'Découvrez comment configurer le réseau Edge Experience Platform. '
seo-description: 'Découvrez comment configurer le réseau Edge Experience Platform. '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 4%

---


# Configuration du bord

La configuration du Adobe Experience Platform [!DNL Web SDK] est fractionnée en deux emplacements. La commande [configure](configuring-the-sdk.md) du SDK contrôle les éléments qui doivent être gérés sur le client, comme le `edgeDomain`noeud. La configuration edge gère toutes les autres configurations pour le SDK. Lorsqu’une requête est envoyée au Adobe Experience Platform [!DNL Edge Network], `edgeConfigId` elle est utilisée pour référencer la configuration côté serveur. Cela vous permet de mettre à jour la configuration sans avoir à modifier le code de votre site Web.

## Création d’un identifiant de configuration Edge

Les ID de configuration Edge peuvent être créés dans l’Adobe [!DNL Launch] à l’aide de l’outil de configuration Edge. Cet outil vous permet de créer à la fois la configuration des arêtes et des environnements dans ces configurations.

![navigation dans l&#39;outil de configuration des bords](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>L’outil de configuration des arêtes est disponible pour les clients de la liste autorisée, qu’ils utilisent [!DNL Launch] ou non comme gestionnaire de balises. En outre, les utilisateurs ont besoin des autorisations de développement dans [!DNL Launch]. Pour plus d’informations, reportez-vous à l’article Permissions [](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/admin/user-permissions.html) utilisateur dans la [!DNL Launch] documentation.

Vous pouvez créer une configuration de bord en cliquant sur **[!UICONTROL Nouvelle configuration]** de bord dans la zone supérieure droite de l’écran. Après avoir fourni un nom et une description, vous êtes invité à définir les paramètres par défaut de chaque environnement.

### Paramètres d’Environnement par défaut

Ces paramètres par défaut sont utilisés pour créer vos trois premiers environnements avec des paramètres identiques. Ces trois environnements sont *dev*, *stage* et *prod*. Ils correspondent aux trois environnements par défaut de [!DNL Launch]. Lorsque vous créez une [!DNL Launch] bibliothèque dans un environnement de développement, celle-ci utilise automatiquement l’environnement de développement de votre configuration. Vous pouvez modifier les paramètres d’un environnement à votre convenance.

L’ID utilisé dans le SDK en tant qu’ `edgeConfigId` ID composite spécifie la configuration et l’environnement. Si aucun environnement n’est présent, l’environnement de production est utilisé.

### Paramètres d’Environnement

Vous trouverez ci-dessous chacun des paramètres disponibles pour un environnement. La plupart des sections peuvent être activées ou désactivées. Lorsque cette option est désactivée, vos paramètres sont enregistrés mais ne sont pas principaux.

#### [!UICONTROL Identité]

La section d&#39;identité est la seule qui est toujours activée. Deux paramètres sont disponibles : &quot;[!UICONTROL ID Syncs Enabled]&quot; et &quot;ID de Conteneur Sync&quot;.

![Section Identité de l’interface utilisateur de configuration](../../assets/edge_configuration_identity.png)

##### [!UICONTROL Synchronisation des identifiants activée]

Contrôle si le SDK effectue ou non des synchronisations d’identité avec des partenaires tiers.

##### [!UICONTROL ID Conteneur de synchronisation]

Les synchronisations d’identifiants peuvent être regroupées en conteneurs pour permettre l’exécution de différentes synchronisations d’identifiants à des moments différents. Cela contrôle quel conteneur d’ID synchronisé est exécuté pour un ID de configuration donné.

#### Adobe Experience Platform

Les paramètres répertoriés ici vous permettent d&#39;envoyer des données au Adobe Experience Platform. Vous ne devez activer cette section que si vous avez acheté le Adobe Experience Platform.

![Bloc des paramètres Adobe Experience Platform](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Environnement de test]

Les sandbox sont des emplacements dans la Adobe Experience Platform qui permettent aux clients d’isoler leurs données et leurs implémentations les unes des autres. Pour plus d’informations sur leur fonctionnement, consultez la documentation [](../../sandboxes/home.md)Sandbox.

##### [!UICONTROL Entrée de diffusion en continu]

Une entrée en flux continu est une source HTTP dans le Adobe Experience Platform. Elles sont créées sous l’onglet &quot;[!UICONTROL Sources]&quot; dans Adobe Experience Platform sous la forme d’une API HTTP.

##### [!UICONTROL Jeu de données événement]

Les configurations Edge prennent en charge l’envoi de données à des jeux de données ayant un schéma de Événement [!UICONTROL d’]expérience de classe.

#### Adobe Target

Pour configurer Adobe Target, vous devez fournir un code client. Les autres champs sont facultatifs.

![Bloc des paramètres Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>L&#39;organisation associée au code client doit correspondre à l&#39;organisation dans laquelle l&#39;ID de configuration est créé.

##### [!UICONTROL Code client]

ID unique d’un compte de cible. Pour ce faire, vous pouvez naviguer jusqu’à [!UICONTROL Adobe Target] > [!UICONTROL Configuration]> [!UICONTROL Implémentation] > [!UICONTROL modifier les paramètres en regard du bouton télécharger pour le fichier at.js ou le fichier mbox.js.]

##### [!UICONTROL Jeton de propriété]

[!DNL Target] permet aux clients de contrôler les autorisations en utilisant les propriétés. Vous trouverez des informations détaillées dans la section Permissions [](https://docs.adobe.com/content/help/fr-FR/target/using/administer/manage-users/enterprise/properties-overview.html) Enterprise de la [!DNL Target] documentation.

Le jeton de propriété se trouve dans [!UICONTROL Adobe Target] > [!UICONTROL configuration] > [!UICONTROL Propriétés.]

##### [!UICONTROL ID d’Environnement cible]

[Les Environnements](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) d’Adobe Target vous aident à gérer votre mise en oeuvre à toutes les étapes de développement. Ce paramètre spécifie l’environnement que vous allez utiliser avec chaque environnement.

Adobe recommande de définir cette variable différemment pour chacun de vos environnements de configuration `dev`, `stage`et `prod` Edge afin de garder les choses simples. Cependant, si vous avez déjà défini des environnements Adobe Target, vous pouvez les utiliser.

#### Adobe Audience Manager

Pour envoyer des données à Adobe Audience Manager, il suffit d’activer cette section. Les autres paramètres sont facultatifs mais encouragés.

![Audience d&#39;Adobe Gérer les paramètres Bloc](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Destinations des cookies activées]

Permet au SDK de partager des informations sur les segments par le biais des destinations [de](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) cookies à partir de [!DNL Audience Manager].

##### [!UICONTROL Destinations d’URL activées]

Permet au SDK de partager des informations de segment par le biais des destinations [](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)URL. Ceux-ci sont configurés dans [!DNL Audience Manager].

#### Adobe Analytics

Contrôle si les données sont envoyées à Adobe Analytics. Vous trouverez d’autres informations dans la présentation [d’](../solution-specific/analytics/analytics-overview.md)Analytics.

![Bloc des paramètres Adobe Analytics](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Identifiant de Report Suite]

La suite de rapports se trouve dans la section Admin Adobe Analytics sous [!UICONTROL Admin > ReportSuites]. Si plusieurs suites de rapports sont spécifiées, les données sont alors copiées dans chaque suite de rapports.
