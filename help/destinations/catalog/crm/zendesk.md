---
title: Connexion Zendesk
description: La destination Zendesk vous permet d’exporter les données de votre compte et de les activer dans Zendesk en fonction des besoins de votre entreprise.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 61%

---

# Connexion [!DNL Zendesk]

[[!DNL Zendesk]](https://www.zendesk.fr) est une solution de service client et un outil de vente.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [[!DNL Zendesk] API de contacts](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), pour créer et mettre à jour des identités dans un segment en tant que contacts dans [!DNL Zendesk].

[!DNL Zendesk] utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec le [!DNL Zendesk] API de contacts. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Zendesk] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

En tant que professionnel du marketing, vous pouvez proposer des expériences personnalisées à vos utilisateurs en fonction des attributs de leurs profils Adobe Experience Platform. Vous pouvez créer des segments à partir de vos données hors ligne et envoyer ces segments vers [!DNL Zendesk], pour les afficher dans les flux des utilisateurs dès que les segments et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Conditions préalables d’Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL Zendesk], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=fr) créés dans [!DNL Experience Platform].

Reportez-vous à la documentation Experience Platform pour [Groupe de champs Détails de l’appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin d’instructions sur les états de segment.

### Conditions préalables de [!DNL Zendesk] {#prerequisites-destination}

Pour exporter des données de Platform vers votre [!DNL Zendesk] vous devez disposer d’un compte [!DNL Zendesk] compte .

#### Collectez les informations d’identification de [!DNL Zendesk]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination [!DNL Zendesk] :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Bearer token` | Le jeton d’accès que vous avez généré dans votre [!DNL Zendesk] compte . <br> Suivez la documentation pour [générer une [!DNL Zendesk] jeton d’accès](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) si vous n&#39;en avez pas. | `a0b1c2d3e4...v20w21x22y23z` |

## Mécanismes de sécurisation {#guardrails}

Le [Tarifs et limites de taux](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) détaille la page [!DNL Zendesk] Limites d’API associées à votre compte. Vous devez vous assurer que vos données et votre payload sont conformes à ces contraintes.

## Identités prises en charge {#supported-identities}

[!DNL Zendesk] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Exemple | Description | Obligatoire |
|---|---|---|---|
| `email` | `test@test.com` | Adresse électronique du contact. | Oui |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque statut du segment dans [!DNL Zendesk] est mis à jour avec le statut du segment correspondant de Platform, en fonction de la valeur de l’**[!UICONTROL identifiant de mappage]** fournie pendant l’étape de [planification des segments](#schedule-segment-export-example).</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Zendesk]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL CRM]**.

### S’authentifier auprès de la destination {#authenticate}

Renseignez les champs obligatoires ci-dessous. Reportez-vous à la section [ [!DNL Zendesk] Collecter des informations d’identification ](#gather-credentials) pour obtenir des conseils.
* **[!UICONTROL Jeton porteur]**: Le jeton d’accès que vous avez généré dans votre [!DNL Zendesk] compte .

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**.
![Capture d’écran montrant comment s’authentifier sur l’interface utilisateur de Platform.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un statut **[!UICONTROL Connecté]** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL Zendesk], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents issus de la destination cible.

Attributs spécifiés dans la variable **[!UICONTROL Champ cible]** doit être nommé exactement comme décrit dans le tableau mappings d’attributs , car ces attributs forment le corps de la requête.

Attributs spécifiés dans la variable **[!UICONTROL Champ source]** ne suivez aucune restriction de ce type. Vous pouvez le mapper en fonction de vos besoins, mais si le format de données n’est pas correct lorsqu’il est envoyé vers [!DNL Zendesk] cela entraînera une erreur.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL Zendesk], procédez comme suit :

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.
1. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’attribut XDM ou choisissez l’option **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité.
1. Dans le **[!UICONTROL Sélectionner le champ cible]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité ou choisissez **[!UICONTROL Sélectionner des attributs personnalisés]** et sélectionnez un attribut selon vos besoins.
   * Répétez ces étapes pour ajouter les mappages suivants entre votre schéma de profil XDM et votre [!DNL Zendesk] instance : |Champ source|Champ cible| Obligatoire| |—|—|—| |`xdm: person.name.lastName`|`Attribute: last_name` <br>ou `Attribute: name`| Oui | |`IdentityMap: Email`|`Identity: email`| Oui |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
      ![Exemple de capture d’écran de l’interface utilisateur de Platform avec mappages d’attributs.](../../assets/catalog/crm/zendesk/mappings.png)

      >[!IMPORTANT]
      >
      >Les deux mappages de champs cibles sont obligatoires et requis pour [!DNL Zendesk] au travail.
      >
      >Le mappage pour *Nom* ou *Nom* est requis dans le cas contraire : [!DNL Zendesk] L’API ne répond pas avec une erreur et toute valeur d’attribut transmise est ignorée.

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Planifier l’exportation de segments et exemple {#schedule-segment-export-example}

Dans l’étape [[!UICONTROL Planier l’exportation de segments]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) du workflow d’activation, vous devez mapper manuellement les segments Platform vers l’attribut de champ personnalisé dans [!DNL Zendesk].

Pour ce faire, sélectionnez chaque segment, puis saisissez l’attribut de champ personnalisé correspondant à partir de [!DNL Zendesk] dans le champ **[!UICONTROL ID de mappage]**.

Voici un exemple :
![Capture d’écran de l’interface utilisateur de Platform montrant la planification de l’exportation de segments.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionner **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** et accédez à la liste des destinations.
1. Sélectionnez ensuite la destination et passez au **[!UICONTROL Données d’activation]** , puis sélectionnez un nom de segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Surveillez le résumé du segment et assurez-vous que le nombre de profils correspond au nombre dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le segment.](../../assets/catalog/crm/zendesk/segment.png)

1. Connectez-vous au [!DNL Zendesk] , puis accédez au **[!UICONTROL Contacts]** pour vérifier si les profils du segment ont été ajoutés. Cette liste peut être configurée pour afficher les colonnes des champs supplémentaires créés avec le segment. **[!UICONTROL ID de mappage]** et les états des segments.
   ![Capture d’écran de l’interface utilisateur de Zendesk montrant la page Contacts avec les champs supplémentaires créés avec le nom du segment.](../../assets/catalog/crm/zendesk/contacts.png)

1. Vous pouvez également effectuer une analyse approfondie dans une **[!UICONTROL Personne]** et vérifiez les **[!UICONTROL Champs supplémentaires]** affichant le nom du segment et les états du segment.
   ![Capture d’écran de l’interface utilisateur de Zendesk montrant la page Personne avec la section Champs supplémentaires affichant le nom du segment et les états du segment.](../../assets/catalog/crm/zendesk/contact.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Retrouvez d’autres informations utiles de la documentation de [!DNL Zendesk] ci-dessous :
* [Effectuer votre premier appel](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Champs personnalisés](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)