---
title: Configuration Edge
seo-title: Configuration Edge pour le SDK Web Experience Platform
description: 'Découvrez comment configurer le réseau Edge Experience Platform. '
seo-description: 'Découvrez comment configurer le réseau Edge Experience Platform. '
translation-type: tm+mt
source-git-commit: efbc080117754cee01f21c9f9ec409204648e757

---


# (bêta) Configuration Edge

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

La configuration du SDK Web d’Adobe Experience Platon est fractionnée en deux emplacements. La commande [configure](configuring-the-sdk.md) du SDK contrôle les éléments qui doivent être gérés sur le client, comme le `edgeDomain`noeud. La configuration edge gère toutes les autres configurations pour le SDK. Lorsqu’une requête est envoyée au réseau Edge d’Adobe Experience Platform, elle `edgeConfigId` est utilisée pour référencer la configuration côté serveur. Cela vous permet de mettre à jour la configuration sans avoir à modifier le code de votre site Web.

## Création d’un identifiant de configuration Edge

Les ID de configuration Edge peuvent être créés dans Lancement à l’aide de l’outil de configuration Edge. Cet outil vous permet de créer à la fois la configuration des arêtes et des environnements dans ces configurations.

![navigation dans l&#39;outil de configuration des bords](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>L’outil de configuration des arêtes est disponible pour les clients figurant sur la liste blanche, qu’ils utilisent le paramètre Lancer comme gestionnaire de balises. En outre, les utilisateurs ont besoin des autorisations Développer dans Lancement. Pour plus d’informations, reportez-vous à l’article Permissions [](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/admin/user-permissions.html) utilisateur dans la documentation sur le lancement.

Vous pouvez créer une configuration de bord en cliquant sur **[UICONTROL New Edge Configuration]** dans la partie supérieure droite de l&#39;écran. Après avoir fourni un nom et une description, vous êtes invité à définir les paramètres par défaut de chaque environnement.

### Paramètres d’Environnement par défaut

Ces paramètres par défaut sont utilisés pour créer vos trois premiers environnements avec des paramètres identiques. Ces trois environnements sont le développement, l&#39;étape et la prod. Ils correspondent aux trois environnements par défaut du lancement. Lorsque vous créez une bibliothèque de lancement sur un environnement de développement, celle-ci utilise automatiquement l’environnement de développement de votre configuration. Vous pouvez modifier les paramètres d’un environnement à votre convenance.

L’ID utilisé dans le SDK en tant qu’ `edgeConfigId` ID composite spécifie la configuration et l’environnement. Si aucun environnement n’est présent, l’environnement de production est utilisé.

### Paramètres d’Environnement

Vous trouverez ci-dessous chacun des paramètres disponibles pour un environnement. La plupart des sections peuvent être activées ou désactivées. Lorsque cette option est désactivée, vos paramètres sont enregistrés mais ne sont pas actifs.

#### [!UICONTROL Identity]

La section d&#39;identité est la seule qui est toujours activée. Deux paramètres sont disponibles : ID Synchronisation des identifiants activée et ID de Conteneur de synchronisation des identifiants.

![Section Identité de l’interface utilisateur de configuration](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID Sync Enabled]

Contrôle si le SDK effectue ou non des synchronisations d’identité avec des partenaires tiers.

##### [!UICONTROL ID Sync Container ID]

Les synchronisations d’identifiants peuvent être regroupées en conteneurs pour permettre l’exécution de différentes synchronisations d’identifiants à des moments différents. Cela contrôle quel conteneur d’ID synchronisé est exécuté pour un ID de configuration donné.

#### Adobe Experience Platform

Les paramètres répertoriés ici vous permettent d’envoyer des données à Adobe Experience Platform. Vous ne devez activer cette section que si vous avez acheté Adobe Experience Platform.

![Bloc des paramètres d’Adobe Experience Platform](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Les sandbox sont des emplacements de la plateforme Adobe Experience Platform qui permettent aux clients d’isoler leurs données et leurs implémentations les unes des autres. Pour plus d’informations sur leur fonctionnement, consultez la documentation [](../../sandboxes/home.md)Sandbox.

##### [!UICONTROL Streaming Inlet]

Une entrée en flux continu est une source HTTP dans Adobe Experience Platform. Elles sont créées sous l’ [!UICONTROL Sources] onglet de la plate-forme Adobe Experience Platform sous la forme d’une API HTTP.

##### [!UICONTROL Event Dataset]

Les configurations Edge prennent en charge l&#39;envoi de données à des jeux de données ayant un schéma de classe [!UICONTROL Experience Event].

#### Adobe Target

Pour configurer Adobe Cible, vous devez fournir un code client. Les autres champs sont facultatifs.

![Bloc des paramètres d’Adobe Cible](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>L&#39;organisation associée au code client doit correspondre à l&#39;organisation dans laquelle l&#39;ID de configuration est créé.

##### [!UICONTROL Client Code]

ID unique d’un compte de cible. Pour le trouver, vous pouvez accéder à [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] en regard du [!UICONTROL download] bouton pour [!UICONTROL at.js] ou [!UICONTROL mbox.js]

##### [!UICONTROL Property Token]

La Cible permet aux clients de contrôler les autorisations en utilisant les propriétés. Vous trouverez des informations détaillées dans la section Permissions [](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) Enterprise de la documentation de la Cible.

Le jeton de propriété se trouve dans [!UICONTROL Adobe Target] > [!UICONTROL setup] > Propriétés [UICONTROL]

##### [!UICONTROL Target Environment ID]

[Les Environnements](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) d’Adobe Cible vous aident à gérer votre mise en oeuvre à toutes les étapes de développement. Ce paramètre spécifie l’environnement que vous allez utiliser avec chaque environnement.

Adobe conseille de définir cette option différemment pour chacun de vos environnements de configuration `dev`, `stage`et `prod` Edge afin de rester simple. Cependant, si vous avez déjà [!UICONTROL Adobe Target environments] défini, vous pouvez les utiliser.

#### Adobe Audience Manager

Pour envoyer des données à Adobe Audience Manager, il suffit d’activer cette section. Les autres paramètres sont facultatifs mais encouragés.

![Bloc des paramètres d’Adobe Audience Manager](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie Destinations Enabled]

Permet au SDK de partager des informations sur les segments par le biais des destinations [de](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) cookies à partir d’Audience Manager.

##### [!UICONTROL URL Destinations Enabled]

Permet au SDK de partager des informations de segment par le biais des destinations [](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)URL. Ils sont configurés dans Audience Manager.

#### Adobe Analytics

Contrôle si les données sont envoyées à Adobe Analytics. Vous trouverez d’autres informations dans la présentation [d’](../solution-specific/analytics/analytics-overview.md)Analytics.

![Bloc des paramètres d’Adobe Analytics](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Report Suite ID]

La suite de rapports se trouve dans la section Admin d’Adobe Analytics sous [!UICONTROL Admin > ReportSuites]. Si plusieurs suites de rapports sont spécifiées, les données sont alors copiées dans chaque suite de rapports.
