---
keywords: crm;CRM;destinations crm;Microsoft Dynamics 365;destination Microsoft Dynamics 365 crm
title: Connexion à Microsoft Dynamics 365
description: La destination Microsoft Dynamics 365 vous permet d’exporter les données de votre compte et de les activer dans Microsoft Dynamics 365 pour répondre aux besoins de votre entreprise.
source-git-commit: 12af2ee40d355119104d741630654d2847df6cc5
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 5%

---


# Connexion [!DNL Microsoft Dynamics 365]

## Présentation {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) est une plateforme d’applications métier cloud qui combine la planification des ressources de l’entreprise (ERP) et la gestion de la relation client (CRM), ainsi que des applications de productivité et des outils d’IA, afin d’offrir des opérations de bout en bout plus fluides et plus contrôlées, un meilleur potentiel de croissance et des coûts réduits.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), qui vous permet de mettre à jour les identités d’un segment dans [!DNL Dynamics 365].

[!DNL Dynamics 365] utilise OAuth 2 avec l’octroi d’autorisation comme mécanisme d’authentification pour communiquer avec le [!DNL Contact Entity Reference API]. Instructions pour vous authentifier à votre [!DNL Dynamics 365] sont plus loin, dans la section [Authentification à la destination](#authenticate) .

## Cas d&#39;utilisation {#use-cases}

En tant que marketeur, vous pouvez proposer des expériences personnalisées à vos utilisateurs en fonction des attributs de leurs profils Adobe Experience Platform. Vous pouvez créer des segments à partir de vos données hors ligne et envoyer ces segments vers [!DNL Dynamics 365], pour les afficher dans les flux des utilisateurs dès que les segments et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Conditions préalables des Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la variable [!DNL Dynamics 365] destination, vous devez avoir une [schema](/help/xdm/schema/composition.md), un [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), et [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) créé dans [!DNL Experience Platform].

Reportez-vous à la documentation d’Adobe pour [Groupe de champs Détails de l’appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin d’instructions sur les états de segment.

### [!DNL Microsoft Dynamics 365] conditions préalables {#prerequisites-destination}

Notez les conditions préalables suivantes dans [!DNL Dynamics 365], afin d’exporter des données de Platform vers votre [!DNL Dynamics 365] compte :

#### Vous devez avoir une [!DNL Microsoft Dynamics 365] account {#prerequisites-account}

Accédez au [!DNL Dynamics 365] [essai](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) pour vous enregistrer et créer un compte, le cas échéant.

#### Créer un champ dans [!DNL Dynamics 365] {#prerequisites-custom-field}

Créer un champ personnalisé de type `Simple` avec le type de données de champ comme `Single Line of Text` l’Experience Platform utilisé pour mettre à jour l’état du segment dans [!DNL Dynamics 365].
Reportez-vous à la section [!DNL Dynamics 365] documentation à [créer un champ (attribut)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) si vous avez besoin de conseils supplémentaires.

Exemple de configuration dans [!DNL Dynamics 365] est illustré ci-dessous :
![Copie d’écran de l’interface utilisateur Dynamics 365 présentant les champs personnalisés.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Enregistrement d’une application et d’un utilisateur d’application dans Azure Principale Directory {#prerequisites-app-user}

Pour activer [!DNL Dynamics 365] pour accéder aux ressources dont vous avez besoin pour vous connecter avec votre [!DNL Azure Account] to [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) et créez les éléments suivants :
* Un [!DNL Azure Active Directory] application
* Une entité de service
* Un secret d&#39;application

Vous devrez également [création d’un utilisateur d’application](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] et l’associer à l’application nouvellement créée.

#### Collecte [!DNL Dynamics 365] informations {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la variable [!DNL Dynamics 365] Destination CRM :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Client ID` | Le [!DNL Dynamics 365] ID client pour votre [!DNL Azure Active Directory] application. Reportez-vous à la section [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) pour obtenir des conseils. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | Le [!DNL Dynamics 365] Secret client pour votre [!DNL Azure Active Directory] application. Vous utiliseriez l’option #2 dans la variable [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` pour obtenir des conseils. |
| `Tenant ID` | Le [!DNL Dynamics 365] Identifiant du client pour votre [!DNL Azure Active Directory] application. Reportez-vous à la section [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) pour obtenir des conseils. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | Reportez-vous à la section [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) pour obtenir des conseils. | Si votre [!DNL Dynamics 365] domain est comme ci-dessous, vous avez besoin de la valeur mise en surbrillance.<br> *`org57771b33`.crm.dynamics.com* |

## Éléments de sécurité {#guardrails}

Le [Demandes de limitation et d’attribution](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) détaille la page [!DNL Dynamics 365] Limites d’API associées à votre [!DNL Dynamics 365] licence. Vous devez vous assurer que vos données et votre charge utile sont conformes à ces contraintes.

## Identités prises en charge {#supported-identities}

[!DNL Dynamics 365] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Exemple | Description | Considérations |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Identifiant unique d’un contact. | **Obligatoire**. Reportez-vous à la section [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) pour plus de détails. |

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités. *(par exemple : adresse email, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque état de segment dans [!DNL Dynamics 365] est mis à jour avec l’état du segment correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des segments](#schedule-segment-export-example) étape .</li></ul> |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]** rechercher [!DNL Dynamics 365]. Vous pouvez également la localiser sous le **[!UICONTROL CRM]** catégorie.

### Authentification à la destination {#authenticate}

Pour vous authentifier à la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**.
![Capture d’écran de l’interface utilisateur de Platform montrant comment vous authentifier.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Renseignez les champs obligatoires ci-dessous. Reportez-vous à la section [Collecte des informations d’identification Dynamics 365](#gather-credentials) pour obtenir des conseils.
* **[!UICONTROL ID client]**: Le [!DNL Dynamics 365] ID client pour votre [!DNL Azure Active Directory] application.
* **[!UICONTROL Identifiant du client]**: Le [!DNL Dynamics 365] Identifiant du client pour votre [!DNL Azure Active Directory] application.
* **[!UICONTROL Secret du client]**: Le [!DNL Dynamics 365] Secret client pour votre [!DNL Azure Active Directory] application.
* **[!UICONTROL URL d’environnement]**: Votre [!DNL Dynamics 365] URL de l’environnement.

Si les détails fournis sont valides, l’interface utilisateur affiche une **[!UICONTROL Connecté]** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience de Adobe Experience Platform vers le [!DNL Dynamics 365] destination, vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible. Pour mapper correctement vos champs XDM à [!DNL Dynamics 365] champs de destination, procédez comme suit :

1. Dans le **[!UICONTROL Mappage]** étape, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affiche à l’écran.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform pour Ajouter un nouveau mappage.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** catégorie et sélectionnez `contactId`.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform pour le mappage source.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. Dans le **[!UICONTROL Sélectionner le champ cible]** sélectionnez le type de champ cible vers lequel vous souhaitez mapper votre champ source.
   * **[!UICONTROL Sélectionner un espace de noms d’identité]**: sélectionnez cette option pour mapper votre champ source à un espace de noms d’identité de la liste.
      ![Copie d’écran de l’interface utilisateur de Platform montrant le mapping de ciblage pour contactId.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Ajoutez le mappage suivant entre votre schéma de profil XDM et votre [!DNL Dynamics 365] instance : |Schéma de profil XDM|[!DNL Dynamics 365] Instance| Obligatoire| |—|—|—| |`contactId`|`contactId`| Oui |

   * **[!UICONTROL Sélectionner des attributs personnalisés]**: sélectionnez cette option pour mapper votre champ source à un attribut personnalisé que vous définissez dans la variable **[!UICONTROL Nom de l’attribut]** champ . Voir [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) pour obtenir une liste complète des attributs pris en charge.
      ![Copie d’écran de l’interface utilisateur de Platform montrant le mappage de Target pour le nom de famille.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

      >[!IMPORTANT]
      >
      >Si vous disposez d’un champ source de date ou d’horodatage mappé à un [!DNL Dynamics 365] [date ou horodatage](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) cible , assurez-vous que la valeur mappée n’est pas vide. Si la valeur transmise est vide, un événement *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* et que les données ne seront pas mises à jour. Il s’agit d’une [!DNL Dynamics 365] limitation.

   * Par exemple, en fonction des valeurs que vous souhaitez mettre à jour, ajoutez le mappage suivant entre votre schéma de profil XDM et votre [!DNL Dynamics 365] instance : |Schéma de profil XDM|[!DNL Dynamics 365] Instance| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
      ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les mappages Target.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Planification de l’exportation de segments et exemple {#schedule-segment-export-example}

Dans le [[!UICONTROL Planification de l’exportation de segments]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) à l’étape du workflow d’activation, vous devez mapper manuellement les segments Platform à l’attribut de champ personnalisé dans [!DNL Dynamics 365].

Pour ce faire, sélectionnez chaque segment, puis saisissez l’attribut de champ personnalisé correspondant à partir de [!DNL Dynamics 365] dans le **[!UICONTROL ID de mappage]** champ .

>[!IMPORTANT]
>
>La valeur utilisée pour la variable **[!UICONTROL ID de mappage]** doit correspondre exactement au nom de l’attribut de champ personnalisé créé dans [!DNL Dynamics 365]. Voir [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) si vous avez besoin de conseils pour trouver vos attributs de champ personnalisés.

Voici un exemple :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Planification de l’exportation de segments.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Validation de l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionner **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur de Platform montrant Parcourir les destinations.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que l’état est **[!UICONTROL enabled]**.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’exécution du flux de données des destinations.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Basculez vers le **[!DNL Activation data]** , puis sélectionnez un nom de segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Surveillez le résumé du segment et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Segment.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Connectez-vous au [!DNL Dynamics 365] , puis accédez au [!DNL Customers] > [!DNL Contacts] et vérifiez si les profils du segment ont été ajoutés. Vous pouvez voir que chaque état de segment dans [!DNL Dynamics 365] a été mis à jour avec l’état du segment correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des segments](#schedule-segment-export-example) étape .
   ![Copie d’écran de l’interface utilisateur Dynamics 365 présentant la page Contacts avec les états de segment mis à jour.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers la destination {#unknown-errors}

Lors de la vérification d’une exécution de flux de données, si vous obtenez le message d’erreur suivant : `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Copie d’écran de l’interface utilisateur de Platform affichant une erreur de requête incorrecte.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Pour corriger cette erreur, vérifiez que la variable **[!UICONTROL ID de mappage]** vous avez fourni dans [!DNL Dynamics 365] pour votre segment Platform valide et existe dans [!DNL Dynamics 365].

## Ressources supplémentaires {#additional-resources}

Informations utiles supplémentaires de la [[!DNL Dynamics 365] documentation](https://docs.microsoft.com/en-us/dynamics365/) est ci-dessous :
* [Méthode IOorganizationService.Update(Entity)](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Mise à jour et suppression des lignes du tableau à l’aide de l’API Web](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)