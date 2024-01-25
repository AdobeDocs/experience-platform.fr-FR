---
title: Connexion Zendesk
description: La destination Zendesk vous permet d’exporter les données de votre compte et de les activer dans Zendesk en fonction des besoins de votre entreprise.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 42%

---

# Connexion [!DNL Zendesk]

[[!DNL Zendesk]](https://www.zendesk.fr) est une solution de service client et un outil de vente.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de la fonction [[!DNL Zendesk] API de contacts](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), à **créer et mettre à jour des identités** au sein d’une audience en tant que contacts dans [!DNL Zendesk].

[!DNL Zendesk] utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec le [!DNL Zendesk] API de contacts. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Zendesk] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Le service à la clientèle d’une plateforme multicanal B2C souhaite offrir à ses clients une expérience personnalisée transparente. Le service peut créer des audiences à partir de ses propres données hors ligne pour créer de nouveaux profils utilisateur ou mettre à jour les informations de profil existantes à partir de différentes interactions (par exemple, achats, retours, etc.) et envoyer ces audiences de Adobe Experience Platform vers [!DNL Zendesk]. Consultez les informations mises à jour dans [!DNL Zendesk] garantit que l’agent du service client dispose immédiatement des informations récentes du client, ce qui permet des réponses et une résolution plus rapides.

## Conditions préalables {#prerequisites}

### Conditions préalables d’Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL Zendesk], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créés dans [!DNL Experience Platform].

Reportez-vous à la documentation Experience Platform pour [Groupe de champs Détails de l’appartenance à une audience](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin de conseils sur les états d’audience.

### Conditions préalables de [!DNL Zendesk] {#prerequisites-destination}

Pour exporter des données de Platform vers votre [!DNL Zendesk] vous devez disposer d’un [!DNL Zendesk] compte .

#### Collectez les informations d’identification de [!DNL Zendesk]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la variable [!DNL Zendesk] destination :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Bearer token` | Le jeton d’accès que vous avez généré dans votre [!DNL Zendesk] compte . <br> Suivez la documentation pour [générer une [!DNL Zendesk] jeton d’accès](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) si vous n&#39;en avez pas. | `a0b1c2d3e4...v20w21x22y23z` |

## Mécanismes de sécurisation {#guardrails}

La variable [Tarifs et limites de taux](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) détaille la page [!DNL Zendesk] Limites d’API associées à votre compte. Vous devez vous assurer que vos données et votre payload sont conformes à ces contraintes.

## Identités prises en charge {#supported-identities}

[!DNL Zendesk] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Exemple | Description | Obligatoire |
|---|---|---|---|
| `email` | `test@test.com` | Adresse électronique du contact. | Oui |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque état de segment dans [!DNL Zendesk] est mis à jour avec l’état d’audience correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des audiences](#schedule-segment-export-example) étape .</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Zendesk]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL CRM]**.

### S’authentifier auprès de la destination {#authenticate}

Renseignez les champs obligatoires ci-dessous. Voir [Collecte [!DNL Zendesk] informations](#gather-credentials) pour obtenir des conseils.
* **[!UICONTROL Jeton de porteur]**: le jeton d’accès que vous avez généré dans votre [!DNL Zendesk] compte .

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

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL Zendesk], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible.

Attributs spécifiés dans la variable **[!UICONTROL Champ cible]** doit être nommé exactement comme décrit dans le tableau mappings d’attributs , car ces attributs forment le corps de la requête.

Attributs spécifiés dans la variable **[!UICONTROL Champ source]** ne suivez aucune restriction de ce type. Vous pouvez le mapper en fonction de vos besoins, mais si le format de données n’est pas correct lorsqu’il est envoyé vers [!DNL Zendesk] cela entraînera une erreur.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL Zendesk], procédez comme suit :

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.
1. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’attribut XDM ou choisissez l’option **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité.
1. Dans le **[!UICONTROL Sélectionner le champ cible]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité cible, ou choisissez la catégorie **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’un des attributs de schéma pris en charge.
   * Répétez ces étapes pour ajouter les mappages obligatoires suivants. Vous pouvez également ajouter tout autre attribut que vous souhaitez mettre à jour entre votre schéma de profil XDM et votre [!DNL Zendesk] instance : |Champ source|Champ cible| Obligatoire| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`| Oui | |`IdentityMap: Email`|`Identity: email`| Oui | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
     ![Exemple de capture d’écran de l’interface utilisateur de Platform avec mappages d’attributs.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>La variable `Attribute: last_name` et `Identity: email` les mappings de ciblage sont obligatoires pour cette destination. Si ces mappages sont manquants, tous les autres mappages sont ignorés et ne sont pas envoyés à [!DNL Zendesk].

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Planification de l’export d’audience et exemple {#schedule-segment-export-example}

Dans le [[!UICONTROL Planification de l’exportation des audiences]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) à l’étape du workflow d’activation, vous devez mapper manuellement les audiences Platform à l’attribut de champ personnalisé dans [!DNL Zendesk].

Pour ce faire, sélectionnez chaque segment, puis saisissez l’attribut de champ personnalisé correspondant à partir de [!DNL Zendesk] dans le champ **[!UICONTROL ID de mappage]**.

Voici un exemple :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Planification de l’exportation d’audience.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionner **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** et accédez à la liste des destinations.
1. Sélectionnez ensuite la destination et passez au **[!UICONTROL Données d’activation]** , puis sélectionnez un nom d’audience.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Surveillez la synthèse de l’audience et assurez-vous que le nombre de profils correspond au nombre dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le segment.](../../assets/catalog/crm/zendesk/segment.png)

1. Connectez-vous au [!DNL Zendesk] , puis accédez à la **[!UICONTROL Contacts]** pour vérifier si les profils de l’audience ont été ajoutés. Cette liste peut être configurée pour afficher les colonnes des champs supplémentaires créés avec l&#39;audience**[!UICONTROL ID de mappage]Statuts des ** et de l’audience.
   ![Capture d’écran de l’interface utilisateur de Zendesk montrant la page Contacts avec les champs supplémentaires créés avec le nom de l’audience.](../../assets/catalog/crm/zendesk/contacts.png)

1. Vous pouvez également effectuer une analyse approfondie dans une **[!UICONTROL Personne]** et vérifiez les **[!UICONTROL Champs supplémentaires]** affichant le nom de l’audience et les états de l’audience.
   ![Capture d’écran de l’interface utilisateur de Zendesk montrant la page Personne avec la section Champs supplémentaires affichant le nom de l’audience et le statut de l’audience.](../../assets/catalog/crm/zendesk/contact.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Informations utiles supplémentaires de la section [!DNL Zendesk] la documentation est la suivante :
* [Effectuer votre premier appel](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Champs personnalisés](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Journal des modifications

Cette section répertorie les nouvelles fonctionnalités et les mises à jour importantes de la documentation consacrée au connecteur de destination.

+++ Afficher le journal des modifications

| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Avril 2023 | Mise à jour de la documentation | <ul><li>Nous avons mis à jour la variable [use-case](#use-cases) avec un exemple plus clair de à quel moment les clients pourraient bénéficier de l’utilisation de cette destination.</li> <li>Nous avons mis à jour la variable [mapping](#mapping-considerations-example) pour refléter les mappages requis corrects. La variable `Attribute: last_name` et `Identity: email` les mappings de ciblage sont obligatoires pour cette destination. Si ces mappages sont manquants, tous les autres mappages sont ignorés et ne sont pas envoyés à [!DNL Zendesk].</li> <li>Nous avons mis à jour la variable [mapping](#mapping-considerations-example) avec des exemples clairs de mappages obligatoires et facultatifs.</li></ul> |
| Mars 2023 | Version initiale | Version initiale de la destination et publication de la documentation. |

{style="table-layout:auto"}

+++
