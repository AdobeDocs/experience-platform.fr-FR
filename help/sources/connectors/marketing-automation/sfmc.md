---
title: Présentation Du Source Salesforce Marketing Cloud (V2)
description: Découvrez comment connecter Salesforce Marketing Cloud (V2) à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
source-git-commit: 3c200ff1a29c3462a5d4fef554f6a410cfcbdde8
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Présentation de la source [!DNL Salesforce Marketing Cloud] (V2)

>[!IMPORTANT]
>
>La source [[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md) d’origine a été abandonnée en janvier 2026. Aucune migration n’est disponible pour cette source obsolète et vous devez réimplémenter vos données à l’aide de la nouvelle source [!DNL Salesforce Marketing Cloud] (V2).

L’intégration entre Adobe [Real-Time CDP](../../../rtcdp/overview.md) et [!DNL Salesforce Marketing Cloud] est conçue pour tirer parti des extensions de données en raison de la flexibilité et du contrôle qu’elles offrent. Contrairement aux tables système standard (vues de données et objets natifs), qui se limitent à des champs prédéfinis et servent principalement au suivi au niveau du système, les extensions de données vous permettent de définir des champs personnalisés, d’organiser un large éventail de données spécifiques à l’entreprise et d’adapter vos structures de données pour répondre à des besoins uniques.

En raison de ce niveau de personnalisation et d’évolutivité, l’intégration entre Real-Time CDP et [!DNL Salesforce Marketing Cloud] repose sur les extensions de données plutôt que sur les tables système standard. Cette approche offre une base plus flexible, évolutive et intégrée pour la gestion des données, en veillant à ce qu’elle s’aligne sur les objectifs de votre entreprise

Vous pouvez utiliser la source [!DNL Salesforce Marketing Cloud] pour connecter votre compte [!DNL Salesforce Marketing Cloud] à Real-Time CDP et Adobe Experience Platform. Lisez la documentation ci-dessous pour savoir comment commencer.

## Exemples de cas d’utilisation {#use-case-examples}

### Personnaliser des campagnes par e-mail avec les données de contact

Une marque de vente au détail souhaite personnaliser les campagnes par e-mail en fonction des étapes du cycle de vie du client (par exemple, nouveau client, acheteur récurrent, client fidèle). Pour ce faire, ils créent une extension de données de contact pour stocker les informations clés sur le client, y compris le nom, l’e-mail, l’étape du cycle de vie et le comportement d’achat. Ces données sont ensuite ingérées dans Experience Platform pour une segmentation et un ciblage plus approfondis.

En ingérant les données de l’extension de données de contact dans Experience Platform, la marque peut segmenter les clients en fonction de l’étape de leur cycle de vie et de leur comportement d’achat. Par exemple, ils peuvent envoyer une offre de bienvenue aux nouveaux clients, une récompense de fidélité aux acheteurs réguliers ou même réengager les clients inactifs avec des offres ciblées. Cette approche garantit une communication personnalisée et permet une interaction client plus pertinente et plus efficace.

### Ingestion de données Campaign pour une segmentation personnalisée

Une équipe marketing souhaite optimiser ses campagnes par e-mail en ciblant les clients et clientes en fonction de leur engagement dans les campagnes précédentes. Pour ce faire, ils créent une extension de données Campaign dans [!DNL Salesforce Marketing Cloud] stocker les données d’engagement des clients, telles que les ouvertures d’e-mail, les clics et les réponses de campagne. Ces données sont ensuite ingérées dans Experience Platform pour une segmentation et une personnalisation supplémentaires.

En ingérant ces données de l’extension de données Campaign dans Experience Platform, l’équipe marketing peut segmenter les clients en fonction de leur engagement passé, comme ceux qui ont cliqué sur des offres de produit ou ont répondu positivement. Les clients qui se sont engagés peuvent recevoir des promotions ciblées dans les futurs e-mails, tandis que ceux qui ont répondu négativement peuvent recevoir des suivis du service client. Cette intégration à Experience Platform permet à l’équipe marketing de diffuser du contenu plus personnalisé et plus pertinent en fonction du comportement du client ou de la cliente.

### Ciblage des clients en fonction des données d’activités

Une équipe marketing souhaite cibler les clients en fonction de leurs activités, telles que les visites sur le site web, les envois de formulaire ou les interactions avec les campagnes par e-mail précédentes. Pour ce faire, ils créent une extension de données d’activités pour stocker des informations sur les activités d’engagement de chaque client. Ces données sont ensuite ingérées dans Experience Platform pour une segmentation plus poussée et un ciblage de campagne personnalisé.

En ingérant les données de l’extension de données des activités dans Experience Platform, l’équipe marketing peut segmenter les clients en fonction de leur historique d’engagement. Par exemple, les clients qui ont récemment consulté le site web mais n’ont pas effectué d’achat peuvent recevoir des e-mails de rappel avec des offres spéciales. De même, les clients qui ont rempli un formulaire peuvent recevoir des communications de suivi personnalisées. Cette approche garantit que chaque client reçoit du contenu pertinent en fonction de ses activités les plus récentes, ce qui améliore les taux d’engagement et de conversion.

## Conditions préalables {#prerequisites}

Lisez les sections ci-dessous pour connaître les conditions préalables à la configuration que vous devez remplir avant de pouvoir connecter votre source à Experience Platform.

### Configuration de l’application pour l’authentification {#set-up-application-for-authentication}

Lors de la création d’une intégration à [!DNL Salesforce Marketing Cloud], l’une des premières étapes consiste à créer un **Package installé** dans [!DNL Salesforce Marketing Cloud]. Le package installé génère les informations d’identification du client requises pour authentifier les appels API, définit le type d’intégration et les portées d’autorisation associées. En outre, le package installé fournit les points d’entrée d’API corrects pour votre client . Il sert également de conteneur géré pour l’administration, la surveillance et la révocation des accès, ce qui garantit que toutes les intégrations sont sécurisées, auditables et alignées avec le modèle d’authentification recommandé de Salesforce.

Pour créer un package installé, utilisez l’interface utilisateur [!DNL Salesforce Marketing Cloud] et accédez à **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]**, puis sélectionnez **[!DNL New]**. Utilisez l’interface [!DNL New Package Details] pour fournir un nom et des informations pour votre package. Lorsque vous avez terminé, sélectionnez **[!DNL Save]**.

![Nouvelle interface de package de l’interface utilisateur de Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/new-package.png)

Une fois le nouveau package créé, sélectionnez **[!DNL Add Component]**.

![L’interface Ajouter un composant de l’interface utilisateur de Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/add-component.png)

Sélectionnez **[!DNL API Integration]** comme type de composant.

![La fenêtre de sélection des composants avec « Intégration d’API » sélectionné.](../../images/tutorials/create/sfmc/api-integration.png)

Sélectionnez **[!DNL Server-to-Server]** comme type d’intégration.

![Fenêtre de sélection du type d&#39;intégration](../../images/tutorials/create/sfmc/server-to-server.png)

Enfin, accédez à **[!DNL Scope]** > **[!DNL Data]**. Sous **[!DNL Data Extensions]**, sélectionnez **[!DNL Read]**.

![Section extensions de données de la portée dans Salesforce Marketing](../../images/tutorials/create/sfmc/data-extensions.png)

Sélectionnez **[!DNL Save]**, puis copiez et enregistrez votre **secret client**. Une fois l’opération terminée, sélectionnez **[!DNL Finish]**.

![Fenêtre Salesforce Marketing Cloud permettant de générer un secret client.](../../images/tutorials/create/sfmc/generate-secret.png)

Avant de quitter l’interface utilisateur de [!DNL Salesforce Marketing Cloud], copiez le **identifiant client** et le **préfixe d’URI de base unique**, car vous utiliserez les deux valeurs pour établir une connexion à Experience Platform. Pour l’URI de base d’authentification, veillez à tout supprimer après `.auth.marketingcloudapis.com/`

![Interface des composants de Salesforce Marketing Cloud dans laquelle l’identifiant client et l’URI de base unique peuvent être récupérés.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

Pour obtenir des instructions détaillées sur la création d’un package installé, consultez la [[!DNL Salesforce] documentation](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment).

### Collecter les informations d’identification requises {#gather-required-credentials}

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de [!DNL Salesforce Marketing Cloud] connecter à Experience Platform.

| Informations d’identification | Description |
| --- | --- |
| Identifiant client | Identifiant exposé publiquement utilisé par [!DNL Salesforce Marketing Cloud] pour identifier votre compte lors de l’autorisation d’accès à Experience Platform. L’identifiant client peut être récupéré à partir du panneau Composants de l’interface utilisateur de [!DNL Salesforce Marketing Cloud]. |
| Secret client | Clé confidentielle connue uniquement de l’application cliente et du serveur d’autorisation. Vous pouvez générer votre secret client en suivant les étapes de [configuration de l’application décrites ci-dessus](#set-up-application-for-authentication). |
| Point d’entrée de base | Préfixe de l’URI de base d’authentification pour [!DNL Salesforce Marketing Cloud]. |

{style="table-layout:auto"}

## Connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform

Continuez pour configurer votre connexion source [!DNL Salesforce Marketing Cloud] dans Experience Platform. Pour obtenir un guide détaillé sur la configuration de la connexion via l’interface utilisateur, reportez-vous au [tutoriel ici](../../tutorials/ui/create/marketing-automation/sfmc.md). Lisez ce tutoriel pour en savoir plus sur la connexion de votre compte [!DNL Salesforce Marketing Cloud], la sélection des données, le mappage des champs, la planification des ingestions et la surveillance des flux de données.
