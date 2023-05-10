---
keywords: crm;CRM;destinations crm;portée globale;destination crm de diffusion
title: Connexion sortante
description: La destination de diffusion vous permet d’exporter les données de votre compte et de les activer dans le cadre d’Outreach en fonction de vos besoins professionnels.
exl-id: 7433933d-7a4e-441d-8629-a09cb77d5220
source-git-commit: 4ef83c152c4649721c6a424f3ba47b7c6bbfef3f
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 53%

---

# Connexion [!DNL Outreach]

## Présentation {#overview}

[[!DNL Outreach]](https://www.outreach.io/) est une plateforme d’exécution des ventes qui possède le plus grand nombre de données d’interaction entre vendeurs et acheteurs B2B au monde et qui investit de manière significative dans des technologies d’IA propriétaires afin de traduire les données de vente en informations. [!DNL Outreach] aide les entreprises à automatiser l’engagement commercial et à agir sur la base des renseignements fournis par le chiffre d’affaires afin d’améliorer leur efficacité, leur prévisibilité et leur croissance.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [API de ressource de mise à jour de diffusion externe](https://api.outreach.io/api/v2/docs#update-an-existing-resource), qui permet de mettre à jour les identités d’un segment correspondant aux prospects dans [!DNL Outreach].

[!DNL Outreach] utilise OAuth 2 avec l’octroi d’autorisation comme mécanisme d’authentification pour communiquer avec le [!DNL Outreach] [!DNL Update Resource API]. Instructions pour vous authentifier à votre [!DNL Outreach] L’instance est plus loin, dans [Authentification à la destination](#authenticate) .

## Cas d’utilisation {#use-cases}

En tant que marketeur, vous pouvez proposer des expériences personnalisées à vos prospects en fonction des attributs de leurs profils Adobe Experience Platform. Vous pouvez créer des segments à partir de vos données hors ligne et envoyer ces segments vers [!DNL Outreach], pour les afficher dans les flux de prospects dès que les segments et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Conditions préalables d’Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL Outreach], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=fr) créés dans [!DNL Experience Platform].

Si vous avez besoin de conseils pour les statuts de segment, reportez-vous à la documentation d’Adobe pour le [groupe de champs de schéma Détails de l’appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md).

### Conditions préalables de diffusion {#prerequisites-destination}

Notez les conditions préalables suivantes dans [!DNL Outreach], afin d’exporter des données de Platform vers votre compte [!DNL Outreach] :

#### Vous devez disposer d’un compte de contact. {#prerequisites-account}

Accédez au [!DNL Outreach] [connexion](https://accounts.outreach.io/users/sign_in) pour vous enregistrer et créer un compte, le cas échéant. Voir également la section [!DNL Outreach] support [page](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account) pour plus d’informations.

Notez les éléments ci-dessous avant de vous authentifier à la destination CRM [!DNL Outreach] :

| Informations d’identification | Description |
|---|---|
| E-mail | Votre [!DNL Outreach] adresse électronique du compte |
| Mot de passe | Votre [!DNL Outreach] mot de passe du compte |

#### Configuration d’étiquettes de champ personnalisées {#prerequisites-custom-fields}

[!DNL Outreach] prend en charge les champs personnalisés pour [prospects](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). Voir [Comment ajouter un champ personnalisé dans Outreach](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach) pour plus d’informations. Pour faciliter l’identification, il est recommandé de mettre à jour manuellement les étiquettes avec les noms de segment correspondants au lieu de conserver les valeurs par défaut. Par exemple, comme ci-dessous :

[!DNL Outreach] page paramètres pour les prospects qui affichent des champs personnalisés.
![Capture d’écran de l’interface utilisateur de diffusion présentant les champs personnalisés de la page des paramètres.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] page paramètres pour les prospects affichant des champs personnalisés avec *convivial* libellés correspondant aux noms des segments. Vous pouvez afficher l’état du segment sur la page des prospects par rapport à ces libellés.
![Capture d’écran de l’interface utilisateur de diffusion montrant les champs personnalisés avec les libellés associés sur la page des paramètres.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> Les noms de libellé sont uniquement destinés à faciliter l’identification. Ils ne sont pas utilisés lors de la mise à jour des prospects.

## Mécanismes de sécurisation

Le [!DNL Outreach] L’API est limitée à un taux de 10 000 demandes par heure par utilisateur. Si vous atteignez cette limite, vous recevrez une `429` réponse avec le message suivant : `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

Si vous avez reçu ce message, vous devez mettre à jour votre planning d’exportation de segments afin qu’il soit conforme au seuil de taux.

Reportez-vous à la section [[!DNL Outreach] documentation](https://api.outreach.io/api/v2/docs#rate-limiting) pour plus d’informations.

## Identités prises en charge {#supported-identities}

[!DNL Outreach] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] identifier. Il s’agit d’une valeur numérique correspondant au profil du prospect.</li><li>L’identifiant doit correspondre à l’identifiant dans la variable [!DNL Outreach] URL du prospect en cours de mise à jour.</li><li>Reportez-vous à la documentation de [[!DNL Outreach] ](https://api.outreach.io/api/v2/docs#update-an-existing-resource) pour plus d’informations.</li></ul> | Obligatoire |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li> Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque statut du segment dans [!DNL Outreach] est mis à jour avec le statut du segment correspondant de Platform, en fonction de la valeur de l’[!UICONTROL identifiant de mappage] fournie pendant l’étape de [planification des segments](#schedule-segment-export-example).</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | <ul><li> Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
> Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Outreach]. Vous pouvez également localiser cet élément dans la catégorie CRM.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Capture d’écran de l’interface utilisateur de Platform montrant comment s’authentifier auprès d’Outreach.](../../assets/catalog/crm/outreach/authenticate-destination.png)

Vous verrez s’afficher la variable [!DNL Outreach] page de connexion. Indiquez votre adresse électronique.

![Capture d’écran de l’interface utilisateur de diffusion montrant le champ de saisie d’un courrier électronique pour l’authentification auprès d’Outreach.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

Indiquez ensuite votre mot de passe.

![Capture d’écran de l’interface utilisateur de diffusion montrant l’étape du champ de saisie du mot de passe pour l’authentification auprès d’audience.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL Nom d’utilisateur]**: Votre [!DNL Outreach] adresse électronique du compte.
* **[!UICONTROL Mot de passe]**: Votre [!DNL Outreach] mot de passe du compte.

Si les détails fournis sont valides, l’interface utilisateur affiche un statut **Connecté** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant comment remplir les détails pour la destination de diffusion.](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
> Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL Outreach], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents issus de la destination cible. Pour mapper correctement vos champs XDM vers les champs de destination [!DNL Outreach], procédez comme suit :

1. Dans le [!UICONTROL Mappage] étape, cliquez sur **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.
   ![Copie d’écran de l’interface utilisateur de Platform montrant comment ajouter un nouveau mappage](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. Dans le [!UICONTROL Sélectionner le champ source] , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** et ajoutez les mappages souhaités.
   ![Copie d’écran de l’interface utilisateur de Platform affichant Mappage de la source](../../assets/catalog/crm/outreach/source-mapping.png)

1. Dans la fenêtre [!UICONTROL Sélectionner le champ cible], sélectionnez le type de champ cible vers lequel vous souhaitez mapper votre champ source.
   * **[!UICONTROL Sélectionner un espace de noms d’identité]** : sélectionnez cette option pour mapper votre champ source vers un espace de noms d’identité de la liste.
      ![Copie d’écran de l’interface utilisateur de Platform montrant le mapping de ciblage à l’aide de OutreachId.](../../assets/catalog/crm/outreach/target-mapping.png)

   * Ajoutez le mappage suivant entre votre schéma de profil XDM et votre instance [!DNL Outreach] :
|Schéma de profil XDM|[!DNL Outreach] Instance| Obligatoire|
|—|—|—| |`Oid`|`OutreachId`| Oui |

   * **[!UICONTROL Sélectionner des attributs personnalisés]** : sélectionnez cette option pour mapper votre champ source vers un attribut personnalisé que vous définissez dans le champ [!UICONTROL Nom de l’attribut]. Voir [[!DNL Outreach] documentation des prospects](https://api.outreach.io/api/v2/docs#prospect) pour obtenir une liste complète des attributs pris en charge.
      ![Copie d’écran de l’interface utilisateur de Platform montrant le mappage de Target à l’aide de Nom.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * Par exemple, en fonction des valeurs que vous souhaitez mettre à jour, ajoutez le mappage suivant entre votre schéma de profil XDM et votre [!DNL Outreach] instance : |Schéma de profil XDM|[!DNL Outreach] Instance| |—|—| |`person.name.firstName`|`firstName`| |`person.name.lastName`|`lastName`|

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
      ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/crm/outreach/mappings.png)

### Planifier l’exportation de segments et exemple {#schedule-segment-export-example}

* Lors de l’exécution de la variable [Planification de l’exportation de segments](../../ui/activate-segment-streaming-destinations.md) vous devez mapper manuellement les segments Platform à l’attribut de champ personnalisé dans [!DNL Outreach].

* Pour cela, sélectionnez chaque segment, puis saisissez la valeur numérique correspondante qui correspond au *Champ personnalisé `N` Libellé* champ depuis [!DNL Outreach] dans le **[!UICONTROL ID de mappage]** champ .

   >[!IMPORTANT]
   >
   > * Valeur numérique *(`N`)* utilisé dans la variable [!UICONTROL ID de mappage] doit correspondre à la clé d’attribut personnalisée suffixée avec la valeur numérique dans [!DNL Outreach]. Exemple : *Champ personnalisé `N` Libellé*.
   > * Il vous suffit de spécifier la valeur numérique, et non l’ensemble du libellé du champ personnalisé.
   > * [!DNL Outreach] prend en charge un maximum de 150 champs de libellé personnalisés.
   > * Voir [[!DNL Outreach] documentation des prospects](https://api.outreach.io/api/v2/docs#prospect) pour plus d’informations.


   * Par exemple :

      | [!DNL Outreach] Champ | ID de mappage de plateforme |
      |---|---|
      | Champ personnalisé `4` Libellé | `4` |

      ![Copie d’écran de l’interface utilisateur de Platform présentant un exemple d’identifiant de mappage lors de l’exportation du segment Planifier .](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur de Platform montrant la navigation des destinations.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que le statut est **[!UICONTROL activé]**.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’exécution du flux de données des destinations pour la destination sélectionnée.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. Basculez vers l’onglet **[!DNL Activation data]**, puis sélectionnez un nom de segment.
   ![Capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. Surveillez le résumé du segment et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Copie d’écran de l’interface utilisateur de Platform présentant le résumé du segment.](../../assets/catalog/crm/outreach/segment.png)

1. Connectez-vous au site web de [!DNL Outreach], puis accédez à [!DNL Apps] > [!DNL Contacts] et vérifiez si les profils du segment ont été ajoutés. Comme vous pouvez le constater, chaque statut de segment dans [!DNL Outreach] a été mis à jour avec le statut du segment correspondant de Platform, en fonction de la valeur de l’[!UICONTROL identifiant de mappage] fournie lors de la [planification des segments](#schedule-segment-export-example).

![Capture d’écran de l’interface utilisateur de diffusion montrant la page Perspectives de diffusion avec les états de segment mis à jour.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

Lors de la vérification d’une exécution de flux de données, le message d’erreur suivant peut s’afficher : `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Copie d’écran de l’interface utilisateur de Platform affichant la mauvaise erreur de requête.](../../assets/catalog/crm/outreach/error.png)

Pour corriger cette erreur, vérifiez que la variable [!UICONTROL ID de mappage] que vous avez fourni dans Platform pour votre [!DNL Outreach] est valide et existe dans [!DNL Outreach].

## Ressources supplémentaires {#additional-resources}

Le [[!DNL Outreach] documentation](https://api.outreach.io/api/v2/docs/) contient des détails sur [Réponses d’erreur](https://api.outreach.io/api/v2/docs#error-responses) que vous pouvez utiliser pour déboguer les problèmes.
