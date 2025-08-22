---
title: Connexion Marketo Engage
description: Marketo Engage est la seule solution de gestion de l’expérience client (CXM) de bout en bout pour le marketing, la publicité, l’analyse et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion des prospects CRM à l’engagement des clients, en passant par le marketing basé sur les comptes et l’attribution des recettes.
source-git-commit: 88864353d4872d62258914d6490b90331692fa96
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 17%

---


# Connexion Marketo Engage

## Vue d’ensemble {#overview}

[!DNL Marketo Engage] est la seule solution de gestion de l’expérience client (CXM) de bout en bout pour le marketing, la publicité, l’analyse et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion des prospects CRM à l’engagement des clients, en passant par le marketing basé sur les comptes et l’attribution des recettes.

Utilisez cette destination pour la synchronisation en temps réel des données d’audience et des attributs de profil entre Adobe Experience Platform et Marketo Engage.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Marketo Engage], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation de la synchronisation des audiences {#audience-sync-use-cases}

**Réengager uniquement les prospects connus**

L’équipe marketing souhaite lancer une campagne de reconquête ciblant les prospects qui ne se sont pas engagés depuis plus de 90 jours mais qui existent déjà dans Marketo.

Ils peuvent activer les audiences dans Marketo Engage et utiliser le type de synchronisation **[!UICONTROL Audience uniquement]**.

### Cas d’utilisation de la synchronisation des audiences et des profils {#audience-profile-sync-use-cases}

**Réengagement des prospects connus et mise à jour des prospects**

L’équipe marketing souhaite lancer une campagne de réengagement pour les contacts Marketo existants qui ont montré de l’intérêt en fonction des visites du site web. Ils souhaitent également mettre à jour les informations sur les prospects (comme les préférences, les informations démographiques), mais sans créer de nouvelles personnes dans Marketo.

Ils peuvent activer les audiences dans Marketo Engage et utiliser le type de synchronisation **[!UICONTROL Audience et Profil]** associé à l’action **[!UICONTROL Mettre à jour les personnes existantes uniquement]** pour s’assurer qu’ils ciblent uniquement les audiences qui existent déjà dans Marketo.

**Réengagez et étendez la portée grâce à la synchronisation complète des profils**

L’équipe marketing souhaite activer une audience d’intérêt de produit pour une nouvelle campagne. Bien que de nombreux profils existent déjà dans Marketo, certains sont nouveaux et uniquement présents dans Real-Time CDP. Pour les personnes existantes, ils veulent s’assurer de mettre à jour ces personnes dans Marketo, mais aussi de créer de nouveaux profils.

Ils peuvent activer leurs audiences dans Marketo Engage et utiliser le type de synchronisation **[!UICONTROL Audience et profil]** associé à l’action **[!UICONTROL Mettre à jour les audiences existantes et créer de nouvelles personnes]** pour s’assurer qu’ils ciblent les prospects existants de Marketo et en créent de nouvelles pour les nouvelles audiences exportées depuis Real-Time CDP.

## Conditions préalables {#prerequisites}

L’utilisateur configurant la destination doit disposer de l’autorisation [ Modifier la personne ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) dans son instance et sa partition Marketo.

## Identités prises en charge {#supported-identities}

[!DNL Marketo Engage] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `DedupeField` | Champ utilisé pour identifier et mettre en correspondance des prospects existants dans Marketo. | Au cours de l’étape [mapping](#mapping), mappez tout champ source (tel que des `Email` ou d’autres identifiants personnalisés) que vous souhaitez utiliser comme champ de déduplication à cette identité cible. Pour de meilleurs résultats, choisissez un champ qui est disponible de manière cohérente et unique pour tous vos profils clients. `ECID` n’est pas pris en charge en tant que champ de déduplication. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination. Les deux tableaux ci-dessous indiquent les audiences prises en charge par ce connecteur, par _origine de l’audience_ et _types de profil inclus dans l’audience_ :

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | ✓ | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> <br> |

{style="table-layout:auto"}

Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (e-mail, ECID) utilisés dans la destination [!DNL Marketo Engage]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Comportement de correspondance des leads {#lead-matching}

Comprendre le fonctionnement de la correspondance des prospects Marketo vous permet de choisir la configuration appropriée à votre cas d’utilisation. Le comportement correspondant dépend des paramètres **[!UICONTROL Type de synchronisation]** et **[!UICONTROL Action de la personne]** que vous avez sélectionnés.

Marketo utilise le champ de déduplication **[!UICONTROL Marketo]** que vous sélectionnez pour faire correspondre les profils Experience Platform aux prospects Marketo existants. Le processus correspondant recherche des prospects existants dans toutes les partitions de votre instance Marketo. Reportez-vous au tableau ci-dessous pour comprendre comment les prospects sont créés et mis à jour dans votre instance Marketo en fonction de la configuration sélectionnée.

| Type de synchronisation | Action de personne | Comportement de correspondance |
|-----------|---------------|-------------------|
| **[!UICONTROL Profil uniquement]** | **[!UICONTROL Mettre à jour les personnes existantes et en créer de nouvelles]** | <ul><li>Met à jour les leads existants avec de nouvelles données de profil</li><li>Crée de nouveaux prospects dans la partition sélectionnée pour les profils non correspondants</li></ul> |
| **[!UICONTROL Profil uniquement]** | **[!UICONTROL Mettre à jour les personnes existantes uniquement]** | <ul><li>Met à jour les leads existants avec de nouvelles données de profil</li><li>Aucun nouveau prospect créé pour les profils sans correspondance</li></ul> |
| **[!UICONTROL Audience uniquement]** | S/O | <ul><li>Ajoute des prospects existants aux listes d’audience</li><li>Aucun nouveau prospect créé pour les profils sans correspondance</li></ul> |
| **[!UICONTROL Audience et profil]** | **[!UICONTROL Mettre à jour les personnes existantes et en créer de nouvelles]** | <ul><li>Met à jour les leads existants avec de nouvelles données de profil</li><li>Ajoute des prospects existants aux listes d’audience</li><li>Crée de nouveaux prospects dans la partition sélectionnée pour les profils non correspondants</li><li>Ajoute de nouveaux prospects aux listes d’audience</li></ul> |
| **[!UICONTROL Audience et profil]** | **[!UICONTROL Mettre à jour les personnes existantes uniquement]** | <ul><li>Met à jour les leads existants avec de nouvelles données de profil</li><li>Ajoute des prospects existants aux listes d’audience</li><li>Aucun nouveau prospect créé pour les profils sans correspondance</li></ul> |

{style="table-layout:auto"}

### Considérations importantes

* **Sélection de champ de déduplication** : sélectionnez un champ qui est disponible de manière cohérente et unique pour tous vos profils client (par exemple : adresse e-mail, ID de client)
* **Gestion des partitions** : lorsque vous créez de nouveaux prospects, ils sont placés dans la partition sélectionnée (ou **[!UICONTROL par défaut]** si vous n’avez pas sélectionné de partition)
* **Gestion des doublons** : si plusieurs leads Marketo correspondent au même profil, seul le lead le plus récemment mis à jour sera mis à jour
* **Correspondance entre partitions** : le système effectue une recherche dans toutes les partitions pour trouver les prospects existants, quelle que soit la partition que vous avez sélectionnée pour les nouveaux prospects

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>* Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions).
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Capture d’écran montrant comment s’authentifier à la destination](../../assets/catalog/adobe/marketo-engage-connection/connect-destination.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Exemple de capture d’écran montrant comment remplir les détails pour votre destination](../../assets/catalog/adobe/marketo-engage-connection/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Munchkin ID]** : sélectionnez le [!DNL Marketo Munchkin ID] que vous souhaitez utiliser pour cette destination.
* **[!UICONTROL Workspace ID]** : sélectionnez votre ID d’espace de travail Marketo.
* **[!UICONTROL Type de synchronisation]** : sélectionnez le type de synchronisation à utiliser pour cette destination :
   * **[!UICONTROL Audience et profil]** : sélectionnez cette option lorsque vous souhaitez à la fois ajouter des membres de l’audience aux listes Marketo et tenir à jour leurs informations de profil.
   * **[!UICONTROL Profil uniquement]** : sélectionnez cette option lorsque vous souhaitez tenir les profils de prospect Marketo à jour avec les dernières informations d’Experience Platform.
   * **[!UICONTROL Audience uniquement]** : sélectionnez cette option lorsque vous souhaitez ajouter des membres de l’audience aux listes Marketo sans mettre à jour leurs informations de profil.
* **[!UICONTROL Partition]** : *la sélection de la partition est disponible uniquement lors du choix des types de synchronisation **[!UICONTROL Profil uniquement]**&#x200B;ou **[!UICONTROL Audience et profil]***. Sélectionnez un ID de partition Marketo associé à l’espace de travail de votre choix. Cela vous permet de spécifier quelle partition de prospect dans Marketo recevra les données exportées. Si vous ne choisissez pas de partition spécifique, vos données sont envoyées vers la partition **[!UICONTROL Par défaut]** dans Marketo.
* **[!UICONTROL Champ de déduplication Marketo]** : sélectionnez le champ de déduplication Marketo que vous souhaitez utiliser lors de la mise à jour des prospects Marketo existants. Ce sélecteur affiche les champs que vous avez marqués comme champs de déduplication dans Marketo. Si vous souhaitez qu’un champ spécifique de Marketo s’affiche en tant que champ de déduplication, vous devez le marquer comme un [champ consultable](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/lead-database) dans Marketo.

  >[!NOTE]
  >
  >Les `Lead ID` Marketo et les identifiants Experience Cloud (`ECID`) ne sont pas pris en charge pour la déduplication.

* **[!UICONTROL Action de personne]** : sélectionnez l’action Marketo à exécuter lors de l’exportation de données.
   * **[!UICONTROL Mettre à jour les prospects existants et créer de nouvelles personnes]** : sélectionnez cette option pour mettre à jour les prospects Marketo existants et créer de nouveaux prospects pour les membres de l’audience qui ne sont pas déjà dans Marketo. De nouveaux prospects seront créés dans la partition sélectionnée. Si vous n’avez pas sélectionné de partition, de nouveaux prospects sont créés dans la partition **[!UICONTROL Par défaut]**.
   * **[!UICONTROL Mettre à jour les personnes existantes uniquement]** : sélectionnez cette option lorsque vous souhaitez uniquement mettre à jour les prospects Marketo existants sans en créer de nouveaux. Si plusieurs prospects correspondent au même profil, seul le prospect Marketo le plus récemment mis à jour sera mis à jour avec vos données Experience Platform.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mappages obligatoires {#required-mappings}

Au cours de l’étape de mappage, mappez tout champ source (tel que `email` ou d’autres identifiants personnalisés) que vous souhaitez utiliser comme champ de déduplication à l’identité cible `DedupeField`. Pour de meilleurs résultats, choisissez un champ qui est disponible de manière cohérente et unique pour tous vos profils clients.

Pour que Marketo puisse créer des prospects, vous devez également mapper les attributs cibles requis suivants :

* `firstName` : prénom du prospect
* `lastName` : nom du prospect
* `email` : adresse e-mail du prospect

Si vous utilisez `email` comme champ de déduplication, vous devez également mapper les attributs `firstName` et `lastName` comme illustré dans l’image ci-dessous.

![Capture d’écran montrant le mappage requis lors de l’utilisation d’un e-mail comme champ de déduplication](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email-dedupe.png)

Si vous utilisez un autre champ de déduplication, vous devez mapper manuellement les trois attributs obligatoires (`firstName`, `lastName` et `email`), comme illustré dans l’image ci-dessous.

![Capture d’écran affichant le mappage obligatoire lorsque vous n’utilisez pas E-mail comme champ de déduplication](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Après avoir exporté des audiences vers Marketo Engage, vous devez vous connecter à votre compte Marketo pour vérifier que les audiences ont été activées comme prévu. Vérifiez les partitions de prospect et les espaces de travail appropriés dans Marketo pour vous assurer que les données de l’audience s’affichent correctement et que les actions prévues (telles que la mise à jour ou la création de personnes) ont été effectuées.

Si vous ne voyez pas les données attendues, vérifiez vos paramètres de mappage et d’exportation dans Adobe Experience Platform et réessayez l’exportation.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
