---
title: Connexion Demandbase People
description: Utilisez cette destination pour activer vos audiences et les enrichir avec des données tierces Demandbase, pour d’autres cas d’utilisation en aval dans le marketing et les ventes.
exl-id: 748f5518-7cc1-4d65-ab70-4a129d9e2066
source-git-commit: cc05ca282cdfd012366e3deccddcae92a29fef1c
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 24%

---

# Connexion Demandbase People {#demandbase-people}

Activez les profils de vos campagnes Demandbase pour le ciblage, la personnalisation et la suppression des audiences.

>[!IMPORTANT]
>
>Pour les cas d’utilisation B2B où vous devez [activer les audiences de compte](../../ui/activate-account-audiences.md), utilisez plutôt le connecteur de destination [Demandbase](demandbase.md).

## Cas d’utilisation {#use-case}

Les marketeurs peuvent utiliser Adobe Real-Time CDP pour créer une liste de contacts propriétaires destinée aux personnes et l&#39;activer dans Demandbase pour un engagement optimisé et orchestré sur sa plateforme côté demande (DSP) et d&#39;autres canaux tels que LinkedIn.

Cette approche permet aux professionnels du marketing de donner la priorité aux dépenses de campagne sur des personnes connues provenant de leur propre système de gestion de la relation client (CRM) ou d’automatisation du marketing, en s’assurant que les efforts marketing se concentrent sur des prospects à forte valeur ajoutée.

Une fois activée, Demandbase optimise la diffusion des publicités, en affinant les stratégies de ciblage pour maximiser l’engagement, la portée et les taux de conversion, améliorant ainsi l’efficacité de la campagne.

## Identités prises en charge {#supported-identities}

La connexion [!DNL Demandbase People] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| e-mail | Adresses e-mail en clair | Seules les adresses e-mail en texte brut sont prises en charge par la connexion [!DNL Demandbase People]. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-and-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|--------------|-----------|---------------------------|
| Type d’exportation | Exportation d’audience | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination *Demandbase*. |
| Fréquence | Diffusion en continu | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Pour exporter des audiences vers Demandbase, vous avez besoin des éléments suivants :

1. Un compte Demandbase.
2. Jeton API Demandbase. Vous pouvez générer un jeton API avec votre utilisateur dans Demandbase. Pour générer un jeton, accédez à [Mon profil > Jeton API](https://web.demandbase.com/o/ad/at) après vous être connecté à votre compte Demandbase.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

![Ajouter un jeton porteur](../../assets/catalog/advertising/demandbase-people/bearer-token.png)

* **[!UICONTROL Bearer token]** : renseignez le jeton du porteur pour vous authentifier sur la destination. Consultez [conditions préalables](#prerequisites) pour plus d’informations sur la manière d’obtenir le jeton.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Ajouter des informations sur la connexion de destination](../../assets/catalog/advertising/demandbase-people/name-and-description.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

Vous êtes maintenant prêt à activer vos audiences dans Demandbase People.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mappages obligatoires {#mandatory-mappings}

Lors de l’activation des audiences vers la destination [!DNL Demandbase People], vous devez configurer le mappage obligatoire des champs suivant à l’étape de mappage :

| Champ source | Champ cible | Description |
|--------------|--------------|-------------|
| `xdm: workEmail.address` | `Identity: email` | Adresse électronique professionnelle de la personne |

### Mappages recommandés {#recommended-mappings}

Pour une précision de correspondance optimale, incluez les mappages facultatifs suivants dans votre flux d’activation, en plus du [mappage obligatoire](#mandatory-mappings) ci-dessus.

| Champ source | Champ cible | Description |
|--------------|--------------|-------------|
| `xdm: b2b.personKey.sourceKey` | `xdm: externalPersonId` | Identifiant unique de la personne |
| `xdm: person.name.lastName` | `xdm: lastName` | Nom de la personne |
| `xdm: person.name.firstName` | `xdm: firstName` | Prénom de la personne |

### Bonnes pratiques de mappage {#mapping-best-practices}

Lors du mappage de champs à des [!DNL Demandbase People], tenez compte du comportement correspondant suivant :

* **Correspondance de Principal** : si `externalPersonId` est présent, Demandbase l&#39;utilise comme identifiant principal pour la correspondance de personnes.
* **Correspondance de secours** : si `externalPersonId` n&#39;est pas disponible, Demandbase utilise le champ `email` pour l&#39;identification.
* **Obligatoire ou recommandé** : bien que Demandbase n’exige que du `email`, Adobe recommande de mapper tous les champs disponibles à partir du tableau de mappages recommandé ci-dessus, afin d’améliorer la précision des correspondances et les performances de la campagne.

![Mappages de personnes Demandbase](/help/destinations/assets/catalog/advertising/demandbase-people/demandbase-people-mapping.png)

Ces mappages sont nécessaires au bon fonctionnement de la destination et doivent être configurés avant de pouvoir poursuivre le workflow d’activation.

## Notes supplémentaires et légendes importantes {#additional-notes}

* **Mécanismes de sécurisation de l’API Demandbase** : si vous avez exporté des audiences vers Demandbase et que les exportations ont réussi dans Experience Platform, mais que toutes les données n’atteignent pas Demandbase, vous avez peut-être rencontré un ralentissement de l’API du côté Demandbase. Contactez-les pour obtenir des éclaircissements.
* **Suppression de liste** : les listes de personnes sont uniques. Vous ne pouvez donc pas recréer une nouvelle liste portant un nom déjà utilisé. Lorsque vous supprimez des personnes d’une liste, elles ne sont plus disponibles, mais elles ne sont pas supprimées.
* **Durée d&#39;activation** : le chargement des données dans Demandbase est soumis à un traitement durant la nuit.
* **Dénomination de l&#39;audience** : si une audience de personnes portant le même nom a été activée précédemment dans Demandbase, vous ne pouvez pas la réactiver via un autre flux de données vers la destination Demandbase.
