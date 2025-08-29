---
title: Destination Marketo Engage
description: Marketo Engage est la seule solution de gestion de l’expérience client (CXM) de bout en bout pour le marketing, la publicité, l’analyse et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion des prospects CRM à l’engagement des clients, en passant par le marketing basé sur les comptes et l’attribution des recettes.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 891484b279d2521115c6b1edc58f45c594a55382
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 27%

---

# (Hérité) (V2) Destination Marketo Engage {#beta-marketo-engage-destination}

## Journal des modifications de destination {#changelog}

<!--
>[!IMPORTANT]
>
>The **[!UICONTROL (Legacy) (V2) Marketo Engage]** will be deprecated in **March 2026**.
>
>To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** destination, review the following key points and required actions:
>
>* All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.
>* **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.

-->

![Image des deux cartes de destination Marketo dans une vue côte à côte.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Améliorations de la destination Marketo V2 :

* Dans Marketo V1, à l’étape de **[!UICONTROL Planification de segment]** du processus d’activation, il vous fallait ajouter manuellement un **ID de mappage** pour exporter des données vers Marketo. Cette étape manuelle n’est plus obligatoire dans Marketo V2.
* Dans Marketo V1, à l’étape de **[!UICONTROL Mappage]** du processus d’activation, vous ne pouviez mapper les champs XDM qu’à trois champs cibles dans Marketo : `firstName`, `lastName` et `companyName`. Avec la version Marketo V2, vous pouvez désormais mapper des champs XDM à de nombreux autres champs dans Marketo. Pour plus d’informations, reportez-vous à la section [attributs pris en charge](#supported-attributes) ci-dessous.

## Vue d’ensemble {#overview}

[!DNL Marketo Engage] est la seule solution de gestion de l’expérience client (CXM) de bout en bout pour le marketing, la publicité, l’analyse et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion des prospects CRM à l’engagement des clients, en passant par le marketing basé sur les comptes et l’attribution des recettes.

La destination permet aux marketeurs de pousser les audiences créées dans Adobe Experience Platform vers Marketo où elles apparaîtront sous forme de listes statiques.

## Identités et attributs pris en charge {#supported-identities-attributes}

>[!NOTE]
>
>Dans l’étape [mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination, il est *obligatoire* de mapper des identités et *facultatif* de mapper des attributs. Le mappage de l’e-mail et/ou de l’ECID depuis l’onglet Espace de noms d’identité est la chose la plus importante à faire pour vous assurer que la personne correspond dans Marketo. L’e-mail de mappage assure le taux de correspondance le plus élevé.

### Identités prises en charge {#supported-identities}

| Identité cible | Description |
|---|---|
| ECID | Un espace de noms représentant l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Pour plus d’informations, consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) . |
| E-mail | Un espace de noms représentant une adresse e-mail. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |

{style="table-layout:auto"}

### Attributs pris en charge {#supported-attributes}

Vous pouvez mapper des attributs d’Experience Platform à l’un des attributs auxquels votre organisation a accès dans Marketo. Dans Marketo, vous pouvez utiliser la [requête d’API Describe](https://developers.marketo.com/rest-api/lead-database/leads/#describe) pour récupérer les champs d’attribut auxquels votre entreprise a accès.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (e-mail, ECID) utilisés dans la destination [!DNL Marketo Engage]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurer la destination et activer les audiences {#set-up}

>[!IMPORTANT]
> 
>* Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions).
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour obtenir des instructions détaillées sur la configuration de la destination et l’activation des audiences, lisez [Envoi d’une audience Adobe Experience Platform vers une liste statique Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=fr) dans la documentation de Marketo.

La vidéo ci-dessous montre également les étapes de configuration d’une destination Marketo et d’activation des audiences.

>[!IMPORTANT]
>
>La vidéo ne reflète pas entièrement les fonctionnalités actuelles. Pour obtenir les informations les plus récentes, reportez-vous au guide ci-dessus. Les parties suivantes de la vidéo sont obsolètes :
> 
>* La carte de destination à utiliser dans l’interface utilisateur d’Experience Platform est **[!UICONTROL Marketo V2]**.
>* La vidéo n’affiche pas le nouveau champ de sélecteur **[!UICONTROL Création de personne]** dans le workflow Se connecter à la destination. Pour utiliser ce champ, vous devez mapper le prénom et le nom lors de l’étape de mappage des attributs.
>* Les deux limites mentionnées dans la vidéo ne s’appliquent plus. Vous pouvez désormais mapper de nombreux autres champs d’attribut de profil en plus des informations d’appartenance à l’audience prises en charge au moment de l’enregistrement de la vidéo. Vous pouvez également exporter vers Marketo des membres de l’audience qui n’existent pas encore dans vos listes statiques Marketo, et ils seront ajoutés aux listes.
>* À l’étape **[!UICONTROL Planifier l’audience]** du workflow d’activation, dans Marketo V1, vous deviez ajouter manuellement un **[!UICONTROL ID de mappage]** pour exporter des données vers Marketo. Cette étape manuelle n’est plus obligatoire dans Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/3440160?quality=12&captions=fre_fr)

## Surveiller la destination {#monitor-destination}

Après vous être connecté à la destination et avoir établi un flux de données de destination, vous pouvez utiliser la [fonctionnalité de surveillance](/help/dataflows/ui/monitor-destinations.md) de Real-Time CDP pour obtenir des informations détaillées sur les enregistrements de profil activés vers la destination dans chaque exécution du flux de données.

Les informations de surveillance de la connexion [!DNL Marketo Engage] comprennent des informations au niveau de l’audience relatives aux identités activées, exclues et en échec dans chaque exécution de flux de données et de flux de données. [En savoir plus](/help/dataflows/ui/monitor-destinations.md#segment-level-view) à propos de la fonctionnalité.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).
