---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des sandbox de contrôle d’accès basé sur les attributs
description: Gérez les sandbox via l’interface Autorisations dans Adobe Experience Cloud.
exl-id: c21eb319-fc0d-442a-b778-bbfa2d6bb22d
source-git-commit: 8c9503c9923372ef919d485d4ec0e3ebda5a2413
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 26%

---

# Gestion des sandbox {#mange-sandboxes}

>[!CONTEXTUALHELP]
>id="platform_permissions_sandboxes_about"
>title="Que sont les sandbox ?"
>abstract="Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Tout le contenu et les actions réalisés dans un sandbox sont limités à celui-ci et n’en affectent aucun autre. L’accès aux sandbox est géré par l’intermédiaire des rôles."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home" text="Présentation des sandbox"

Les sandbox sont des partitions virtuelles au sein d’une seule instance de Adobe Experience Platform qui intègrent de manière transparente le processus de développement de vos applications d’expérience digitale. Tout le contenu et les actions réalisés dans un sandbox sont limités à celui-ci et n’en affectent aucun autre. Pour plus d’informations sur les sandbox, consultez la [présentation des sandbox](../../../sandboxes/home.md).

## Explorer les sandbox {#explore-sandboxes}

Pour afficher les détails d’un sandbox et les rôles associés, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Sélectionnez **[!UICONTROL Sandboxes]** dans la section **[!UICONTROL Resources]** du panneau de gauche.

Une liste des sandbox de votre organisation s’affiche. Sélectionnez le sandbox à afficher dans la liste. Vous pouvez également rechercher un sandbox en saisissant son nom dans la barre de recherche ou le filtrer par type en sélectionnant l’icône de filtre (![icône de filtre](../../../images/icons/filter.png)) et en utilisant le menu déroulant **[!UICONTROL Sandbox Type]**.

![Espaces de travail Sandbox dans Autorisations.](../../images/ui/sandboxes/sandboxes-overview.png){zoomable="yes"}

>[!NOTE]
>
>L’espace de travail Sandbox dans Autorisations n’autorise aucune action de gestion des sandbox. Pour gérer les sandbox, sélectionnez l’option **[!UICONTROL Open sandbox manager]** dans le coin supérieur droit de l’espace de travail.

L’onglet **[!UICONTROL Details]** donne un aperçu du sandbox. La vue d’ensemble affiche les **[!UICONTROL Title]**, **[!UICONTROL Sandbox Name]**, **[!UICONTROL Type]**, **[!UICONTROL Region]**, **[!UICONTROL Modified]** date, **[!UICONTROL Modified by]** et les **[!UICONTROL Status]** du sandbox.

![Espace de travail Détails du sandbox.](../../images/ui/sandboxes/sandbox-details.png){zoomable="yes"}

Sélectionnez l’onglet **[!UICONTROL Roles]** pour afficher les rôles affectés au sandbox. Sélectionner un rôle vous amènera à l’espace de travail du rôle.

<!-- To manage the role's sandboxes, follow the [](./roles.md) guide. -->

![Espace de travail Rôles du sandbox.](../../images/ui/sandboxes/sandbox-roles.png){zoomable="yes"}


## Étapes suivantes

Vous savez maintenant comment afficher les détails et les rôles d’un sandbox. Pour en savoir plus sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../overview.md).
