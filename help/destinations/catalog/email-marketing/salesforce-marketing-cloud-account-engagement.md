---
title: Engagement du compte Salesforce Marketing Cloud
description: Découvrez comment utiliser la destination Engagement du compte Salesforce Marketing Cloud (anciennement Pardot) pour exporter les données de votre compte et les activer dans l’engagement du compte Salesforce Marketing Cloud pour répondre aux besoins de votre entreprise.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 26%

---

# Connexion [!DNL Salesforce Marketing Cloud Account Engagement]

Utilisez la destination [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(anciennement appelée [!DNL Pardot])* pour capturer, suivre, noter et évaluer des pistes. Vous pouvez également concevoir des pistes de prospect pour toutes les étapes du pipeline pour les audiences de marché et les groupes de clients ciblés par le biais de campagnes par e-mail et de la gestion des prospects par le biais de la culture, de la notation et de la segmentation des campagnes.

Par rapport à [!DNL Salesforce Marketing Cloud Engagement] qui est plus orienté vers le marketing **B2C**, [!DNL Marketing Cloud Account Engagement] est idéal pour les cas d’utilisation **B2B** impliquant plusieurs services et décideurs qui nécessitent des cycles de vente et de décision plus longs. De plus, vous maintenez une proximité et une intégration plus étroites avec votre CRM pour prendre des décisions appropriées en matière de vente et de marketing. *Notez qu’Experience Platform dispose également de connexions pour les [!DNL Salesforce Marketing Cloud Engagement]. Vous pouvez les vérifier sur les pages [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) et [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md).*

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) exploite le point d’entrée [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) pour **ajouter ou mettre à jour vos prospects** après les avoir activés dans un nouveau segment de [!DNL Marketing Cloud Account Engagement].

[!DNL Marketing Cloud Account Engagement] utilise le protocole OAuth 2 avec code d’autorisation pour s’authentifier auprès de l’API [!DNL Account Engagement]. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Marketing Cloud Account Engagement] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Marketing Cloud Account Engagement], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Envoyer des e-mails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service marketing d’une plateforme en ligne souhaite diffuser une campagne marketing par e-mail à une audience sélectionnée de prospects B2B. L’équipe marketing de la plateforme peut ajouter de nouveaux prospects ou mettre à jour les informations de prospect existantes via Adobe Experience Platform, créer des audiences à partir de leurs propres données hors ligne et envoyer ces audiences à [!DNL Marketing Cloud Account Engagement], qui peut ensuite être utilisée pour envoyer l’e-mail de campagne marketing.

## Conditions préalables {#prerequisites}

Reportez-vous aux sections ci-dessous pour connaître les conditions préalables à configurer dans Experience Platform et [!DNL Salesforce] et pour obtenir des informations à rassembler avant d’utiliser la destination [!DNL Marketing Cloud Account Engagement].

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL Marketing Cloud Account Engagement], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créés dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données d’Experience Platform vers votre compte [!DNL Marketing Cloud Account Engagement] :

#### Vous devez avoir un compte [!DNL Marketing Cloud Account Engagement]. {#prerequisites-account}

Un compte [!DNL Marketing Cloud Account Engagement] avec un abonnement au produit [Engagement du compte Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) est obligatoire pour continuer.

Votre compte [!DNL Salesforce] doit avoir le [!DNL Salesforce] `Account Engagement Administrator role`. Cela est nécessaire pour [créer des champs de prospect personnalisés](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&type=5).

Enfin, votre compte doit également pouvoir accéder au [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&type=5).

Contactez l’[[!DNL Salesforce] assistance technique](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) ou l’administrateur de votre compte [!DNL Salesforce] si vous n’avez pas de compte ou si le compte ne dispose pas de l’abonnement [!DNL Marketing Cloud Account Engagement] ou de l’[!DNL Account Engagement Administrator role].

#### Collectez les informations d’identification de [!DNL Marketing Cloud Account Engagement]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination [!DNL Marketing Cloud Account Engagement].

| Informations d’identification | Description |
| --- | --- |
| `Username` | Nom d’utilisateur de votre compte [!DNL Marketing Cloud Account Engagement]. |
| `Password` | Mot de passe de votre compte [!DNL Marketing Cloud Account Engagement]. |
| `Account Engagement Business Unit ID` | Pour trouver l’ID d’unité opérationnelle Engagement du compte, utilisez Configurer dans [!DNL Salesforce]. Dans Configuration, saisissez *Configuration de l&#39;unité opérationnelle* dans la zone Recherche rapide. Votre ID d’unité opérationnelle d’engagement de compte commence par `0Uv` et comporte 18 caractères. Si vous ne pouvez pas accéder aux informations de configuration de l&#39;unité opérationnelle, demandez à l&#39;administrateur de votre compte [!DNL Salesforce] de vous fournir les `Account Engagement Business Unit ID`. Si vous avez besoin de conseils supplémentaires, reportez-vous à la page de conseils [[!DNL Salesforce] Authentification](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication). |

{style="table-layout:auto"}

### Mécanismes de sécurisation {#guardrails}

Reportez-vous à la section [!DNL Marketing Cloud Account Engagement] [limites de taux](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) qui détaille les limites imposées par votre plan et qui s’appliqueraient également aux exécutions Experience Platform.

>[!IMPORTANT]
>
>Si l’administrateur de votre compte [!DNL Salesforce] a limité l’accès aux plages d’adresses IP de confiance, vous devez le contacter pour obtenir [les adresses IP d’Experience Platformplacer sur la liste autorisée &#x200B;](/help/destinations/catalog/streaming/ip-address-allow-list.md). Reportez-vous à la documentation [!DNL Salesforce] [Limiter l’accès aux plages d’adresses IP de confiance pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) si vous avez besoin de conseils supplémentaires.

## Identités prises en charge {#supported-identities}

[!DNL Marketing Cloud Account Engagement] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresse électronique du prospect | Obligatoire |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Profile-based]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Pour chaque audience sélectionnée dans Experience Platform, le statut du segment [!DNL Salesforce Marketing Cloud Account Engagement] correspondant est mis à jour avec son statut d’audience à partir d’Experience Platform.</li></ul> |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, recherchez [!DNL Salesforce Marketing Cloud Account Engagement]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL Email marketing]** .

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Connect to destination]**. Vous accédez alors à la page de connexion [!DNL Salesforce]. Saisissez les informations d’identification de votre compte [!DNL Marketing Cloud Account Engagement] et sélectionnez [!DNL Log In].

![Capture d’écran de l’interface utilisateur d’Experience Platform montrant comment s’authentifier auprès de l’engagement du compte Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Sélectionnez ensuite [!UICONTROL Allow] dans la fenêtre suivante pour accorder des autorisations à l’application **Adobe Experience Platform** afin d’accéder à votre compte [!DNL Salesforce Marketing Cloud Account Engagement]. *Vous ne devrez effectuer cette opération qu’une seule fois*.

Fenêtre contextuelle de confirmation de capture d’écran de l’application Salesforce ![pour autoriser l’accès de l’application Experience Platform à l’engagement du compte Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un message : *Vous vous êtes connecté avec succès au compte Engagement du compte Marketing Cloud Salesforce* message et un statut de **[!UICONTROL Connected]** avec une coche verte, vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire. Reportez-vous à la section [Collecter [!DNL Marketing Cloud Account Engagement] informations d’identification](#gather-credentials) pour obtenir des conseils.

![Capture d’écran de l’interface utilisateur d’Experience Platform affichant les détails de la destination.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Champ | Description |
| --- | --- |
| **[!UICONTROL Name]** | Nom par lequel vous reconnaîtrez cette destination à l’avenir. |
| **[!UICONTROL Description]** | Une description qui vous aidera à identifier cette destination à l’avenir. |
| **[!UICONTROL Account Engagement Business Unit ID]** | Votre [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL Marketing Cloud Account Engagement], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Experience Platform et leurs équivalents issus de la destination cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL Marketing Cloud Account Engagement], procédez comme suit.

1. À l’étape **[!UICONTROL Mapping]**, sélectionnez **[!UICONTROL Add new mapping]**. Une nouvelle ligne de mappage s’affichera à l’écran.
1. Dans la fenêtre **[!UICONTROL Select source field]** , choisissez la catégorie **[!UICONTROL Select attributes]** et sélectionnez l’attribut XDM ou choisissez le **[!UICONTROL Select identity namespace]** et sélectionnez une identité.
1. Dans la fenêtre **[!UICONTROL Select target field]** , choisissez le **[!UICONTROL Select identity namespace]** et sélectionnez une identité ou choisissez **[!UICONTROL Select custom attributes]** catégorie et spécifiez dans la liste des [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) du schéma disponible.

   * Répétez ces étapes pour ajouter tous les mappages entre votre schéma de profil XDM et [!DNL Marketing Cloud Account Engagement] :

     | Champ source | Champ cible | Obligatoire |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | Oui |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * Un exemple avec les mappages ci-dessus est illustré ci-dessous :
     ![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform montrant les mappings de ciblage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Accédez à l’une des audiences que vous avez sélectionnées. Sélectionnez l’onglet **[!DNL Activation data]** . La colonne **[!UICONTROL Mapping ID]** affiche le nom du champ personnalisé généré dans la page [!DNL Marketing Cloud Account Engagement Prospects].
   ![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform montrant l’identifiant de mappage pour un segment sélectionné.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Connectez-vous au site Web [[!DNL Salesforce]](https://login.salesforce.com/). Accédez ensuite à la page **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** et vérifiez si les prospects de l’audience ont été ajoutés/mis à jour. Vous pouvez également accéder à [[!DNL Salesforce Pardot]](https://pi.pardot.com/) et à la page **[!DNL Prospects]**.
   ![Capture d’écran de l’interface utilisateur de Salesforce montrant la page Prospects.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Pour vérifier si les prospects ont été mis à jour, sélectionnez un prospect et vérifiez si le champ du prospect personnalisé a été mis à jour avec le statut de l’audience Experience Platform.
   ![Capture d’écran de l’interface utilisateur de Salesforce montrant la page de prospect sélectionnée, le champ de prospect personnalisé est mis à jour avec le statut de l’audience.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [documentation API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
