---
title: Guide de l’interface utilisateur des attributs calculés
description: Découvrez comment créer, afficher et mettre à jour des attributs calculés à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: bc621167-6dba-473e-90e4-aac7ceb6579a
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 7%

---

# Guide de l’interface utilisateur des attributs calculés

>[!NOTE]
>
>Pour accéder aux attributs calculés, vous devez disposer des autorisations appropriées (**Afficher les attributs calculés** et **Gérer les attributs calculés**). Pour plus d’informations sur les autorisations requises, consultez la [documentation sur le contrôle d’accès](../../access-control/home.md). Pour savoir comment appliquer ces autorisations, consultez le [guide de gestion des autorisations](../../access-control/ui/permissions.md).

Dans Adobe Experience Platform, les attributs calculés sont des fonctions utilisées pour agréger les données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation.

Ce document fournit un guide sur la création et la mise à jour des attributs calculés à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Commencer

Ce guide de l’interface utilisateur nécessite une compréhension des différents services [!DNL Experience Platform] impliqués dans la gestion de [!DNL Real-Time Customer Profiles]. Avant de lire ce guide ou de travailler dans l’interface utilisateur, consultez la documentation relative aux services suivants :

- [[!DNL Real-Time Customer Profile]](../home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.

## Affichage des attributs calculés {#view}

Dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche, puis **[!UICONTROL Attributs calculés]** pour afficher la liste des attributs calculés disponibles pour votre organisation. Cela inclut des informations sur le nom, la description, la date de dernière évaluation et le statut de la dernière évaluation de l’attribut calculé.

![La section [!UICONTROL Profil] et les onglets [!UICONTROL Attributs calculés] sont mis en surbrillance, ce qui montre aux utilisateurs comment accéder à la page de navigation des attributs calculés.](./images/ui/browse.png)

Pour sélectionner les champs visibles, vous pouvez sélectionner ![l&#39;icône de configuration des colonnes](/help/images/icons/column-settings.png) pour ajouter ou supprimer les champs à afficher.

| Champ | Description |
| ----- | ----------- |
| [!UICONTROL Nom] | Nom d’affichage de l’attribut calculé. |
| [!UICONTROL Description] | Description de l’attribut calculé. |
| [!UICONTROL Méthode d’évaluation] | Méthode d’évaluation de l’attribut calculé. Actuellement, seul **batch** est pris en charge. |
| [!UICONTROL Dernière évaluation] | Cet horodatage représente la dernière opération d’évaluation réussie. Seuls les événements qui se sont produits **avant** cet horodatage sont pris en compte dans la dernière évaluation réussie. |
| [!UICONTROL Dernier état d’évaluation] | État qui indique si l’attribut calculé a été correctement calculé lors de la dernière exécution d’évaluation. Les valeurs possibles sont **[!UICONTROL Success]** ou **[!UICONTROL Failed]**. |
| [!UICONTROL Actualiser la fréquence] | Une indication sur la fréquence à laquelle l’attribut calculé doit être actualisé. Les valeurs possibles sont toutes les heures, tous les jours, toutes les semaines ou tous les mois. |
| [!UICONTROL Actualisation rapide] | Une valeur qui indique si l’actualisation rapide est activée ou non pour cet attribut de calcul. Si l’actualisation rapide est activée, l’attribut calculé peut être actualisé quotidiennement, plutôt que sur une base hebdomadaire, bimensuelle ou mensuelle. Cette valeur s’applique uniquement aux attributs calculés avec une période de recherche en amont plus longue que la base hebdomadaire. |
| [!UICONTROL Statut du cycle de vie] | État actuel de l’attribut calculé. Il existe trois états possibles : <ul><li>**[!UICONTROL Version préliminaire] :** L’attribut calculé n’a **pas** de champ créé sur le schéma pour l’instant. Dans cet état, l’attribut calculé peut être modifié. </li><li>**[!UICONTROL Publié] :** L’attribut calculé comporte un champ créé sur le schéma et est prêt à être utilisé. Dans cet état, l’attribut calculé **ne peut pas** être modifié.</li><li>**[!UICONTROL Inactif] :** L’attribut calculé est désactivé. Pour plus d’informations sur l’état inactif, consultez la [page FAQ](./faq.md#inactive-status). </li> |
| [!UICONTROL Créé] | Horodatage indiquant la date et l’heure de création de l’attribut calculé. |
| [!UICONTROL Dernière modification] | Horodatage indiquant la date et l’heure de la dernière modification de l’attribut calculé. |

Vous pouvez également filtrer les attributs calculés affichés en fonction de l’état du cycle de vie. Sélectionnez l’icône ![funnel](/help/images/icons/filter.png) .

![L’icône de filtre est mise en surbrillance.](./images/ui/select-filter.png)

Vous pouvez désormais choisir de filtrer les attributs calculés par état ([!UICONTROL Version préliminaire], [!UICONTROL Publié] et [!UICONTROL Inactif]).

![Les options que vous pouvez filtrer par attributs calculés sont mises en surbrillance. Ces options incluent [!UICONTROL Version préliminaire], [!UICONTROL Publiée] et [!UICONTROL Inactive].](./images/ui/view-filters.png)

De plus, vous pouvez sélectionner un attribut calculé pour afficher des informations plus détaillées à son sujet. Pour plus d’informations sur la page des détails des attributs calculés, consultez la [section des détails d’un attribut calculé](#view-details).

## Création d’un attribut calculé {#create}

Pour créer un attribut calculé, sélectionnez **[!UICONTROL Créer un attribut calculé]** pour entrer dans le nouveau workflow d’attribut calculé.

![Le bouton [!UICONTROL Créer des attributs calculés] est mis en surbrillance, ce qui montre aux utilisateurs comment accéder à la page de création d’un attribut calculé.](./images/ui/create.png)

La page **[!UICONTROL Créer un attribut calculé]** s’affiche. Sur cette page, vous pouvez ajouter les informations de base pour l’attribut calculé que vous souhaitez créer.

| Champ | Description |
| ----- | ----------- |
| [!UICONTROL Nom d’affichage] | Nom par lequel l’attribut calculé sera connu. Vous devez conserver ce nom d’affichage unique pour chaque attribut calculé. En règle générale, ce nom d’affichage doit contenir des identifiants liés à l’attribut calculé. Ainsi, par exemple, &quot;Somme des achats de chaussures au cours des 7 derniers jours&quot;. |
| [!UICONTROL Nom du champ] | Nom utilisé pour faire référence à l’attribut calculé dans d’autres services en aval. Ce nom est dérivé automatiquement du nom d’affichage et est écrit en CamelCase. |
| [!UICONTROL Description] | Une description de l’attribut calculé que vous essayez de créer. |

![La section [!UICONTROL Informations de base] de la page [!UICONTROL Créer un attribut calculé] est mise en surbrillance.](./images/ui/basic-information.png)

Après avoir ajouté les détails des attributs calculés, vous pouvez commencer à définir vos règles.

### Définition des conditions de filtrage des événements

Pour créer une règle, commencez par sélectionner les attributs de la section **[!UICONTROL Événements]** afin de filtrer les événements sur lesquels vous souhaitez effectuer une agrégation. Actuellement, seuls les attributs d’événement de type non tableau sont pris en charge.

![La section [!UICONTROL Événements] est mise en surbrillance.](./images/ui/events.png)

Après avoir sélectionné l’attribut à utiliser dans la définition d’attribut calculée, vous pouvez choisir à quoi cette valeur sera comparée.

![Les types de comparaison disponibles sont affichés.](./images/ui/select-comparison.png)

### Fonction d&#39;agrégation d&#39;application

Vous pouvez désormais appliquer une fonction au champ à partir de la sortie conditionnelle. Sélectionnez tout d’abord le type de fonction d’agrégation. Les options disponibles sont les suivantes : [!UICONTROL Somme], [!UICONTROL Min], [!UICONTROL Max], [!UICONTROL Count] et [!UICONTROL Le plus récent]. Vous trouverez plus d’informations sur ces fonctions dans la [section fonctions](./overview.md#functions) de la présentation des attributs calculés.

![Les fonctions d’attribut calculées sont affichées.](./images/ui/select-function.png)

Après avoir choisi une fonction, vous pouvez choisir le champ sur lequel vous souhaitez effectuer l’agrégat. Les champs éligibles à sélectionner dépendent de la fonction sélectionnée.

![Le champ en surbrillance affiche l’attribut que vous choisissez pour agréger la fonction.](./images/ui/select-eligible-field.png)

### Durée de recherche en amont

Après avoir appliqué la fonction d’agrégation, vous devrez définir la période de recherche arrière de l’attribut calculé. Cette période de recherche arrière spécifie la durée pendant laquelle vous souhaitez agréger des événements. Cette durée peut être spécifiée en termes d’heures, de jours, de semaines ou de mois.

![La durée de recherche arrière est mise en surbrillance.](./images/ui/select-lookback-duration.png)

### Actualisation rapide {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Actualisation rapide"
>abstract="Une actualisation rapide vous permet de garder vos attributs à jour. L’activation de cette option vous permet d’actualiser quotidiennement vos attributs calculés, même pour des périodes de recherche en amont plus longues, ce qui vous permet de réagir rapidement aux activités de l’utilisateur ou de l’utilisatrice. Cette valeur s’applique uniquement aux attributs calculés avec une période de recherche en amont plus longue que la base hebdomadaire."

Lors de l’application de la fonction d’agrégation, vous pouvez activer une actualisation rapide si la période de recherche arrière est supérieure à une semaine.

![La case à cocher [!UICONTROL Actualisation rapide] est mise en surbrillance.](./images/ui/enable-fast-refresh.png)

Une actualisation rapide vous permet de garder vos attributs à jour. L’activation de cette option vous permet d’actualiser quotidiennement vos attributs calculés, même pour des périodes de recherche en amont plus longues, ce qui vous permet de réagir rapidement aux activités de l’utilisateur.

Pour plus d’informations sur l’actualisation rapide, consultez la [section d’actualisation rapide](./overview.md#fast-refresh) de la présentation des attributs calculés.

Une fois ces étapes terminées, vous pouvez choisir d’enregistrer cet attribut calculé en tant que brouillon ou de le publier immédiatement.

![Les boutons [!UICONTROL Enregistrer en tant que brouillon] et [!UICONTROL Publish] sont mis en surbrillance.](./images/ui/draft-or-publish.png)

## Affichage des détails d’un attribut calculé {#view-details}

Pour afficher les détails d’un attribut calculé, sélectionnez l’attribut calculé dont vous souhaitez afficher les détails sur la page [!UICONTROL **Parcourir**].

![Un attribut calculé est mis en surbrillance.](./images/ui/select.png)

Le contenu de la page diffère, selon que l’attribut calculé est **[!UICONTROL Publié]** ou dans **[!UICONTROL Version préliminaire]**.

### Attribut calculé publié {#published}

Lors de la sélection d’un attribut calculé publié, la page Détails des attributs calculés s’affiche.

![La page des détails de l’attribut calculé s’affiche.](./images/ui/details.png)

Cette page affiche un résumé des détails de l’attribut calculé, ainsi qu’un graphique indiquant la répartition de valeurs et des exemples de profils remplissant les critères pour l’attribut calculé.

>[!NOTE]
>
>La répartition des valeurs reflète la répartition des valeurs d’attribut pour les profils au moment de la tâche d’échantillonnage. La valeur d’attribut calculée dans l’exemple de profil reflète la dernière valeur de profil fusionnée pour quelques exemples de profils.

### Brouillon d’attribut calculé {#draft}

Lors de la sélection d’un brouillon d’attribut calculé, la page **[!UICONTROL Modifier les attributs calculés]** s’affiche. Cette page, tout comme la page [!UICONTROL Créer des attributs calculés] , vous permet de modifier les informations de base de votre attribut calculé, ainsi que sa définition, avant de vous permettre de mettre à jour le brouillon ou de le publier.

![La page [!UICONTROL Modifier les attributs calculés] s’affiche.](./images/ui/edit.png)

## Utilisation d’attributs calculés {#usage}

>[!IMPORTANT]
>
>Si vous utilisez un attribut calculé avec la fonction **Le plus récent** dans une définition de segment, vous **devez** inclure **à la fois** la valeur et la valeur d’horodatage dans l’objet attribut calculé.
>
>Par exemple, si vous créez une définition de segment qui recherche &quot;Tous les profils ayant une adresse électronique valide&quot; où le champ de l’adresse électronique est renseigné par un attribut calculé avec la fonction la plus récente, vous **devez** inclure la valeur de l’adresse électronique existe **et** l’horodatage de l’adresse électronique existe.

Après avoir créé un attribut calculé, vous pouvez utiliser les attributs calculés **publish** dans d’autres services en aval. Les attributs calculés étant des champs d’attribut de profil créés dans votre schéma d’union de profil, vous pouvez rechercher des valeurs d’attribut calculées pour un profil client en temps réel, les utiliser dans une audience, les activer vers une destination ou les utiliser pour la personnalisation dans parcours dans Adobe Journey Optimizer.

>[!NOTE]
>
>Les attributs calculés **ne peuvent pas** être utilisés dans l’audience **compositions**.

![Le Créateur de segments s’affiche, présentant un attribut calculé dans le cadre de la composition des définitions de segment.](./images/ui/use-ca.png)

## Étapes suivantes

Pour en savoir plus sur les attributs calculés, consultez la [présentation des attributs calculés](./overview.md). Pour plus d’informations sur la création et la configuration des attributs calculés à l’aide de l’API, consultez le [guide de développement des attributs calculés](./api.md).
