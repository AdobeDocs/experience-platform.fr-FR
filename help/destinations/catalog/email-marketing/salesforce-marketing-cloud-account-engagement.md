---
title: Engagement du compte Marketing Cloud Salesforce
description: Découvrez comment utiliser la destination Engagement du compte de Marketing Cloud Salesforce (anciennement appelée Pardot) pour exporter les données de votre compte et les activer dans Engagement du compte de Marketing Cloud Salesforce pour répondre aux besoins de votre entreprise.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 30%

---

# Connexion [!DNL Salesforce Marketing Cloud Account Engagement]

Utilisez la destination [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(anciennement appelée [!DNL Pardot])* pour capturer, suivre, noter et évaluer des pistes. Vous pouvez également concevoir des suivis de piste pour toutes les étapes du pipeline pour les audiences de marché et les groupes de clients ciblés par le biais de campagnes gouttes d’emails et de la gestion des pistes grâce à la nutrition, la notation et la segmentation des campagnes.

Par rapport à [!DNL Salesforce Marketing Cloud Engagement], plus axé sur le marketing **B2C**, [!DNL Marketing Cloud Account Engagement] est idéal pour les cas d’utilisation **B2B** impliquant plusieurs départements et décideurs qui nécessitent des cycles de vente et de décision plus longs. En outre, vous maintenez une proximité et une intégration plus étroites avec votre CRM afin de prendre des décisions de vente et de marketing appropriées. *Remarque : Experience Platform possède également des connexions pour [!DNL Salesforce Marketing Cloud Engagement]. Vous pouvez les vérifier sur les pages [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) et [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md).*

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) exploite le point de terminaison [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) pour **ajouter ou mettre à jour vos pistes** après les avoir activées dans un nouveau segment [!DNL Marketing Cloud Account Engagement].

[!DNL Marketing Cloud Account Engagement] utilise OAuth 2 avec le protocole Authorization Code pour s’authentifier sur l’API [!DNL Account Engagement]. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Marketing Cloud Account Engagement] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Marketing Cloud Account Engagement], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Envoyer des emails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service marketing d’une plate-forme en ligne souhaite diffuser une campagne marketing par e-mail à une audience organisée de pistes B2B. L’équipe marketing de la plateforme peut ajouter de nouvelles pistes ou mettre à jour des informations de piste existantes via Adobe Experience Platform, créer des audiences à partir de leurs propres données hors ligne et envoyer ces audiences à [!DNL Marketing Cloud Account Engagement], qui peuvent ensuite être utilisées pour envoyer le courrier électronique de la campagne marketing.

## Conditions préalables {#prerequisites}

Reportez-vous aux sections ci-dessous pour connaître les conditions préalables à configurer dans Experience Platform et [!DNL Salesforce], ainsi que pour obtenir des informations que vous devez rassembler avant de travailler avec la destination [!DNL Marketing Cloud Account Engagement].

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL Marketing Cloud Account Engagement], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créés dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données de Platform vers votre compte [!DNL Marketing Cloud Account Engagement] :

#### Vous devez avoir un compte [!DNL Marketing Cloud Account Engagement]. {#prerequisites-account}

Un compte [!DNL Marketing Cloud Account Engagement] avec un abonnement au produit [Marketing Cloud Account Engagement](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) est obligatoire pour continuer.

Votre compte [!DNL Salesforce] doit avoir le [!DNL Salesforce] `Account Engagement Administrator role`. Cela est nécessaire pour [créer des champs de prospects personnalisés](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Enfin, votre compte doit également pouvoir accéder à [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Contactez l’ [[!DNL Salesforce] assistance](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) ou votre administrateur de compte [!DNL Salesforce] si vous n’avez pas de compte, ou si l’abonnement [!DNL Marketing Cloud Account Engagement] ou [!DNL Account Engagement Administrator role] manque au compte.

#### Collectez les informations d’identification de [!DNL Marketing Cloud Account Engagement]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination [!DNL Marketing Cloud Account Engagement].

| Informations d’identification | Description |
| --- | --- |
| `Username` | Votre nom d&#39;utilisateur de compte [!DNL Marketing Cloud Account Engagement]. |
| `Password` | Votre mot de passe de compte [!DNL Marketing Cloud Account Engagement]. |
| `Account Engagement Business Unit ID` | Pour trouver l’identifiant de l’unité opérationnelle d’engagement de compte, utilisez Configuration dans [!DNL Salesforce]. Dans Configuration, saisissez *Configuration de l’unité opérationnelle* dans la zone Recherche rapide. L’identifiant de l’unité opérationnelle chargée de l’engagement du compte commence par `0Uv` et comporte 18 caractères. Si vous ne pouvez pas accéder aux informations de configuration de l’unité opérationnelle, demandez à votre administrateur de compte [!DNL Salesforce] de vous fournir les `Account Engagement Business Unit ID`. Si vous avez besoin de conseils supplémentaires, reportez-vous à la page de recommandation [[!DNL Salesforce] Authentication](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) . |

{style="table-layout:auto"}

### Mécanismes de sécurisation {#guardrails}

Reportez-vous aux [!DNL Marketing Cloud Account Engagement] [limites de taux](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) qui détaillent les limites imposées par votre plan et qui s’appliqueraient également aux exécutions Experience Platform.

>[!IMPORTANT]
>
>Si l&#39;administrateur de votre compte [!DNL Salesforce] a restreint l&#39;accès aux plages d&#39;adresses IP de confiance, vous devez les contacter pour que [les adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) soient placées sur la liste autorisée. Reportez-vous à la documentation [!DNL Salesforce] [Limiter l’accès aux plages d’adresses IP approuvées pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

## Identités prises en charge {#supported-identities}

[!DNL Marketing Cloud Account Engagement] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Prospect Email Address | Obligatoire |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Pour chaque audience sélectionnée dans Platform, l’état du segment [!DNL Salesforce Marketing Cloud Account Engagement] correspondant est mis à jour avec son état d’audience de Platform.</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Salesforce Marketing Cloud Account Engagement]. Vous pouvez également la localiser sous la catégorie **[!UICONTROL Marketing par e-mail]**.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**. Vous accédez à la page de connexion [!DNL Salesforce]. Saisissez vos informations d’identification de compte [!DNL Marketing Cloud Account Engagement] et sélectionnez [!DNL Log In].

![Copie d’écran de l’interface utilisateur de Platform montrant comment s’authentifier pour l’engagement du compte Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Ensuite, sélectionnez [!UICONTROL Autoriser] dans la fenêtre suivante pour accorder des autorisations à l’application **Adobe Experience Platform** pour accéder à votre compte [!DNL Salesforce Marketing Cloud Account Engagement]. *Vous n’aurez besoin de le faire qu’une seule fois*.

![Fenêtre contextuelle de confirmation de capture d’écran de l’application Salesforce pour accorder des autorisations à l’application Experience Platform d’accès à l’engagement du compte Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un message : *Vous avez réussi à vous connecter au compte d’engagement du Marketing Cloud Salesforce* et un état **[!UICONTROL Connecté]** avec une coche verte, vous pouvez passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire. Pour obtenir des conseils, reportez-vous à la section [Rassembler [!DNL Marketing Cloud Account Engagement] les informations d’identification](#gather-credentials) .

![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Champ | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Un nom par lequel vous reconnaîtrez cette destination à l’avenir. |
| **[!UICONTROL Description]** | Description qui vous aidera à identifier cette destination ultérieurement. |
| **[!UICONTROL Identifiant de l’unité opérationnelle d’engagement de compte]** | Votre [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL Marketing Cloud Account Engagement], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL Marketing Cloud Account Engagement], procédez comme suit.

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]**, choisissez la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez l’attribut XDM ou l’attribut **[!UICONTROL Sélectionner l’espace de noms d’identité]** et sélectionnez une identité.
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]** , choisissez l’ **[!UICONTROL espace de noms d’identité]** et sélectionnez une identité ou choisissez la catégorie **[!UICONTROL Sélectionner des attributs personnalisés]** et spécifiez dans la liste [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) du schéma disponible.

   * Répétez ces étapes pour ajouter les mappages entre votre schéma de profil XDM et [!DNL Marketing Cloud Account Engagement] :

     | Champ source | Champ cible | Obligatoire |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | Oui |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * Un exemple avec les mappages ci-dessus est illustré ci-dessous :
     ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Accédez à l’une des audiences que vous avez sélectionnées. Sélectionnez l’onglet **[!DNL Activation data]** . La colonne **[!UICONTROL ID de mappage]** affiche le nom du champ personnalisé généré dans la page [!DNL Marketing Cloud Account Engagement Prospects].
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant l’ID de mappage pour un segment sélectionné.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Connectez-vous au site web [[!DNL Salesforce]](https://login.salesforce.com/). Accédez ensuite à la page **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** et vérifiez si les prospects de l&#39;audience ont été ajoutés/mis à jour. Vous pouvez également accéder à [[!DNL Salesforce Pardot]](https://pi.pardot.com/) et à la page **[!DNL Prospects]**.
   ![Copie d’écran de l’interface utilisateur Salesforce affichant la page Perspectives.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Pour vérifier si les prospects ont été mis à jour, sélectionnez un prospect et vérifiez si le champ de prospect personnalisé a été mis à jour avec le statut de l&#39;audience Experience Platform.
   ![Copie d’écran de l’interface utilisateur Salesforce affichant la page Prospect sélectionnée, le champ de prospect personnalisé est mis à jour avec l’état de l’audience.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [Documentation de l’API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
