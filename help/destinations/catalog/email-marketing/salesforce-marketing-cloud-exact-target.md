---
keywords: e-mail;e-mail;destinations d’e-mail;salesforce;api salesforce destination marketing cloud
title: (API) Connexion au Marketing Cloud Salesforce
description: La destination de Marketing Cloud Salesforce (anciennement connue sous le nom d’ExactTarget) vous permet d’exporter les données de votre compte et de les activer dans le Marketing Cloud Salesforce pour répondre aux besoins de votre entreprise.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2dda77c3d9a02b53a02128e835abf77ab97ad033
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 6%

---

# Connexion [!DNL (API) Salesforce Marketing Cloud]

## Présentation {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (anciennement appelée ExactTarget) est une suite de marketing numérique qui vous permet de créer et de personnaliser des parcours pour que les visiteurs et les clients puissent personnaliser leur expérience.

>[!IMPORTANT]
> 
> Notez la différence entre cette connexion et l’autre [Connexion au Marketing Cloud Salesforce](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/salesforce-marketing-cloud.html?lang=en) qui se trouve dans la section Catalogue des emails . L’autre connexion au Marketing Cloud Salesforce vous permet d’exporter des fichiers vers un emplacement de stockage spécifié, alors qu’il s’agit d’une connexion en continu basée sur l’API.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [API REST des contacts de mise à jour Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html), qui vous permet d’ajouter des contacts/de mettre à jour les données de contact pour vos besoins professionnels après les avoir activés dans un nouveau segment Salesforce.

Le Marketing Cloud Salesforce utilise OAuth 2 avec les informations d’identification du client comme mécanisme d’authentification pour communiquer avec l’API REST Salesforce. Les instructions d’authentification à votre instance Salesforce sont présentées ci-dessous, dans la section [Authentification à la destination](#authenticate) .

## Cas d&#39;utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination de Marketing Cloud Salesforce, voici un exemple de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Envoyer des emails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service des ventes d’une plateforme de location de maisons souhaite diffuser un email marketing à un public client ciblé. L’équipe marketing de la plateforme peut ajouter de nouveaux contacts/mettre à jour des contacts existants *(et leurs adresses électroniques)* via Adobe Experience Platform, créez des segments à partir de leurs propres données hors ligne et envoyez ces segments au Marketing Cloud Salesforce, qui peut ensuite être utilisé pour envoyer le courrier électronique de campagne marketing.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer les données vers la destination de Marketing Cloud Salesforce, vous devez disposer d’un [schema](/help/xdm/schema/composition.md), un [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), et [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) créé dans [!DNL Experience Platform].

### Conditions préalables dans Salesforce CRM {#prerequisites-destination}

Notez les conditions préalables suivantes dans Salesforce, afin d’exporter des données de Platform vers votre compte de Marketing Cloud Salesforce :

#### Vous devez disposer d’un compte Salesforce. {#prerequisites-account}

Accédez à Salesforce [essai](https://www.salesforce.com/in/form/signup/freetrial-sales/) pour enregistrer et créer un compte Salesforce, le cas échéant.

#### Créer un champ personnalisé dans Salesforce {#prerequisites-custom-field}

Vous devez créer un attribut personnalisé de type `Text Area Long`, que l’Experience Platform utilisera pour mettre à jour l’état du segment dans le Marketing Cloud Salesforce. Dans le workflow d’ activation des segments vers la destination, dans la variable **[Planification du segment](#schedule-segment-export-example)** vous utiliserez l’attribut personnalisé comme identifiant de mappage pour chaque segment que vous activez.

Reportez-vous à la documentation du Marketing Cloud Salesforce pour [créer des champs personnalisés](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si vous avez besoin de conseils supplémentaires.

>[!IMPORTANT]
>
> Veillez à créer l’attribut personnalisé sous le jeu d’attributs &quot;Démographie des emails&quot; dans votre compte de Marketing Cloud Salesforce.

>[!NOTE]
>
> * Le nombre d’attributs personnalisés autorisés par objet varie en fonction de votre édition Salesforce. Reportez-vous à la documentation de Salesforce pour [champs personnalisés autorisés par objet](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.
> * Si vous avez atteint cette limite dans Salesforce, vous devez supprimer l’attribut personnalisé de Salesforce qui a été utilisé pour stocker l’état du segment par rapport aux segments plus anciens dans Experience Platform avant de pouvoir utiliser un nouveau mappingId.


Reportez-vous à la documentation Adobe Experience Platform pour [Groupe de champs Détails de l’appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin d’instructions sur les états de segment.

#### Collecte des informations d’identification Salesforce {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination de Marketing Cloud Salesforce.

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| <ul><li>Préfixe de Marketing Cloud Salesforce</li></ul> | Voir [Préfixe de domaine de Marketing Cloud Salesforce](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) pour plus d’informations. | <ul><li>Si votre domaine est tel que ci-dessous, vous avez besoin de la valeur mise en surbrillance.<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.accuracy.target.com</i></li></ul> |
| <ul><li>Identifiant client</li><li>Secret client</li></ul> | Reportez-vous à la section [Documentation de Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) si vous avez besoin de conseils supplémentaires. | <ul><li>r23kxxxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Identités prises en charge {#supported-identities}

Le Marketing Cloud Salesforce prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| contactKey | Clé de contact Salesforce. Reportez-vous à la section [Documentation de Salesforce](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) si vous avez besoin de conseils supplémentaires. | Obligatoire |

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

![Catalogue](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/catalog.png)

### Authentification à la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Exemple de capture d’écran montrant comment s’authentifier au Marketing Cloud Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL Subdomain]**: Votre préfixe de domaine de Marketing Cloud Salesforce. Par exemple, si votre domaine est *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.accuracy.target.com*, vous avez besoin de la valeur mise en surbrillance.
* **[!UICONTROL ID client]**: Votre identifiant client Salesforce.
* **[!UICONTROL Secret du client]**: Votre secret client Salesforce.

Si les détails fournis sont valides, l’interface utilisateur affiche une **Connecté** avec une coche verte, vous pouvez ensuite passer à l’étape suivante.

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Exemple de capture d’écran montrant comment remplir des détails pour le Marketing Cloud Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Nom du client]**: Il peut s’agir de n’importe quelle valeur, mais cette dernière est obligatoire. Dans le cas contraire, l’activation de la destination échouera.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement les données d’audience de Adobe Experience Platform vers la destination de Marketing Cloud Salesforce, vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible. Pour mapper correctement vos champs XDM aux champs de destination du Marketing Cloud Salesforce, procédez comme suit.

Liste des mappages d’attributs pouvant être configurés pour la variable [API REST Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) est indiqué ci-dessous. La destination utilise la variable [API REST des définitions d’ensemble d’attributs de recherche Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) pour récupérer les attributs définis dans Salesforce pour vos contacts et spécifiques à votre compte.

>[!IMPORTANT]
> 
> Bien que les noms d’attribut soient conformes à votre compte Salesforce, les mappages pour `contactKey` et `personalEmail.address` sont obligatoires.

1. À l’étape Mappage , cliquez sur **[!UICONTROL Ajouter un nouveau mappage]**. Vous pouvez désormais voir une nouvelle ligne de mappage sur l’écran.
   ![Ajouter un nouveau mappage](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. Dans la fenêtre de sélection du champ source, lors de la sélection du champ source, choisissez la **[!UICONTROL Sélectionner des attributs]** et ajoutez les mappages souhaités.
   ![Mappage des sources](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. Dans la fenêtre de sélection du champ cible , sélectionnez le champ cible et choisissez l&#39;option **[!UICONTROL Sélectionner un espace de noms d’identité]** et ajoutez les mappages souhaités.
   ![Mapping de ciblage](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

1. Pour mapper des attributs personnalisés, sélectionnez la fenêtre Champ cible , sélectionnez le champ cible et choisissez l&#39;option **[!UICONTROL Sélectionner des attributs]** > **Démographie des emails** catégorie. Indiquez ensuite le nom d’attribut cible souhaité et ajoutez les mappages souhaités.
   ![Mapping de ciblage](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

1. Par exemple, vous pouvez ajouter le mappage suivant entre votre schéma de profil XDM et votre [!DNL Salesforce Marketing Cloud] instance :

   |  | Schéma de profil XDM | [!DNL Salesforce Marketing Cloud] Instance | Obligatoire |
   |---|---|---|---|
   | Attributs | <ul><li>person.name.firstName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>Email Demographics.First Name</code></li><li>Adresses électroniques.Adresse électronique</code></li></ul> | <ul><li>-</li><li>Oui</code></li></ul> |
   | Identités | <ul><li>contactKey</code></li></ul> | <ul><li>salesforceContactKey</code></li></ul> | Oui |

1. Un exemple d’utilisation de ces mappages est illustré ci-dessous :
   ![Nom du mappage de la cible](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### Planification de l’exportation de segments et exemple {#schedule-segment-export-example}

Lors de l’exécution de la variable [Planification de l’exportation de segments](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) , vous devez mapper manuellement les segments Platform à l’attribut personnalisé dans Salesforce.

Pour ce faire, sélectionnez chaque segment, puis saisissez l’attribut personnalisé correspondant à partir de Salesforce dans la variable **[!UICONTROL ID de mappage]** champ .

>[!IMPORTANT]
>
> La valeur utilisée pour l’ID de mappage doit correspondre exactement au nom de l’attribut personnalisé créé dans Salesforce sous le jeu d’attributs &quot;Démographie des emails&quot;.

Voici un exemple :
![Planification de l’exportation de segments](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## Validation de l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionner **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.

   ![Parcourir les destinations](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que l’état est **[!UICONTROL enabled]**.

   ![Exécution du flux de données des destinations](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Basculez vers le **[!DNL Activation data]** , puis sélectionnez un nom de segment.

   ![Données d’activation des destinations](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Surveillez le résumé du segment et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.

   ![Segment](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Connectez-vous au site web du Marketing Cloud Salesforce. Accédez ensuite à la **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** et vérifiez si les profils du segment ont été ajoutés.

   ![Contacts Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Pour vérifier si des profils ont été mis à jour, accédez au **[!DNL Email]** vérifiez si les valeurs d’attribut du profil du segment ont été mises à jour.

   ![Contacts Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers le Marketing Cloud Salesforce {#unknown-errors}

Lors de la vérification d’une exécution de flux de données, si le message d’erreur ci-dessous s’affiche, vérifiez que l’ID de mappage que vous avez fourni dans [!DNL Salesforce CRM] pour votre segment Platform valide et existe dans [!DNL Salesforce CRM].
![Erreur](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

## Ressources supplémentaires {#additional-resources}

* [Portail de développement Salesforce](https://developer.salesforce.com/)

### Limites {#limits}

* Salesforce impose certains [limites de taux](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
* Reportez-vous à la section [erreurs de limites de taux](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) pour vérifier les erreurs que vous pouvez rencontrer.
* Reportez-vous à la section [Tarifs de l&#39;engagement Marketing Cloud Salesforce](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) page à *Téléchargement du graphique de comparaison de l’édition complète* en pdf qui détaille les limites imposées par votre plan.
* Le [Présentation des API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) détails de la page des limites supplémentaires.
* Un élément de la base de connaissances rassemblant ces détails est disponible [here](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits#:~:text=Day%2FHour%2FMinute%20Limit&amp;text=We%20recommend%20a%20limit%20of,per%20minute%20for%20SOAP%20calls.&amp;text=As%20has%20been%20added%20in,interaction%20with%20the%20REST%2DAPI).
