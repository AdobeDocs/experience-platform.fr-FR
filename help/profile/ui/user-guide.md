---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;profil unifié;profil unifié;unifié;profil;unifié;profil;rtcp;activer le profil;activer le profil;schéma d’union;PROFIL D’UNION;profil d’union
title: Guide de l’interface utilisateur de Real-Time Customer Profile
description: Real-Time Customer Profile offre une vue d’ensemble de chaque client, en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Ce document sert de guide pour interagir avec Real-time Customer Profile dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 7%

---

# Guide de l’interface utilisateur de [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] crée une vue d’ensemble de chacun de vos clients, en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Ce document sert de guide pour interagir avec [!DNL Real-Time Customer Profile] données dans l’interface utilisateur de Adobe Experience Platform.

## Commencer

Ce guide de l’interface utilisateur nécessite une compréhension des différentes [!DNL Experience Platform] services impliqués dans la gestion [!DNL Real-Time Customer Profiles]. Avant de lire ce guide ou de travailler dans l’interface utilisateur, consultez la documentation relative aux services suivants :

* [[!DNL Real-Time Customer Profile] aperçu](../home.md): fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Identity Service]](../../identity-service/home.md): activables [!DNL Real-Time Customer Profile] en rapprochant des identités de sources de données disparates lors de leur ingestion dans [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

## [!UICONTROL Vue d’ensemble]

Dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche pour ouvrir la **[!UICONTROL Présentation]** qui affiche le tableau de bord du profil.

>[!NOTE]
>
>Si votre organisation découvre Platform et ne dispose pas encore de jeux de données Profile actifs ni de stratégies de fusion, la variable [!UICONTROL Profils] tableau de bord n’est pas visible. Au lieu de cela, la variable [!UICONTROL Présentation] Cet onglet affiche des liens et de la documentation pour vous aider à prendre en main Real-time Customer Profile.

### Tableau de bord du profil {#profile-dashboard}

Le tableau de bord du profil décrit les mesures clés liées aux données de profil de votre entreprise.

Pour en savoir plus, consultez la [guide du tableau de bord de profil](../../dashboards/guides/profiles.md).

![Le tableau de bord Profil s’affiche.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Parcourir] mesures d’onglets

Sélectionnez la variable **[!UICONTROL Parcourir]** pour afficher plusieurs mesures liées aux données de profil de votre entreprise. Vous pouvez également utiliser cet onglet pour parcourir la banque de profils à l’aide d’une stratégie de fusion ou d’une identité, comme indiqué dans la section suivante de ce guide.

Sur le côté droit du **[!UICONTROL Parcourir]** est l’onglet [nombre de profils](#profile-count) ainsi qu’une liste [profils par espace de noms](#profiles-by-namespace).

>[!NOTE]
>
>Ces mesures de profil peuvent différer des mesures affichées sur la variable [tableau de bord du profil](#profile-dashboard) car ils sont évalués à l’aide de la stratégie de fusion par défaut de votre organisation. Pour plus d’informations sur l’utilisation des stratégies de fusion, y compris sur la définition d’une stratégie de fusion par défaut, voir la section [présentation des stratégies de fusion](../merge-policies/overview.md).

Outre ces mesures, cette section fournit une date et une heure de dernière mise à jour, indiquant le moment où les mesures ont été évaluées pour la dernière fois.

![Les mesures Profil s’affichent et sont mises en surbrillance.](../images/user-guide/browse-metrics.png)

### Nombre de profils {#profile-count}

Le nombre de profils affiche le nombre total de profils de votre organisation dans Experience Platform, une fois que la politique de fusion par défaut de votre organisation a fusionné des fragments de profil afin de former un seul et même profil pour chaque client. En d’autres termes, votre organisation peut disposer de plusieurs fragments de profil liés à un seul client qui interagit avec votre marque sur différents canaux, mais ces fragments sont fusionnés (selon la politique de fusion par défaut) et renvoient le nombre de profils « 1 », car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils avec des attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de série temporelle (événement), tels que les profils Adobe Analytics. Le nombre de profils est régulièrement actualisé afin de fournir un nombre total de profils à jour dans Platform.

#### Mise à jour de la mesure de comptage des profils

Lorsque l’ingestion d’enregistrements dans la variable [!DNL Profile] store augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour le nombre. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l’ingestion par lots, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre de profils.

### [!UICONTROL Profils par espace de noms] {#profiles-by-namespace}

La variable **[!UICONTROL Profils par espace de noms]** mesure affiche le nombre total et la ventilation des espaces de noms sur tous les profils fusionnés de votre banque de profils. Le nombre total de profils par espace de noms (c’est-à-dire en additionnant les valeurs affichées pour chaque espace de noms) sera toujours supérieur à la mesure du nombre de profils, car plusieurs espaces de noms peuvent y être associés. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

#### Mise à jour de la [!UICONTROL Profils par espace de noms] metric

Semblable au [nombre de profils](#profile-count) lors de l’ingestion d’enregistrements dans la variable [!DNL Profile] store augmente ou réduit le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour les mesures d’espace de noms. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l’ingestion par lots, dans les 15 minutes suivant l’ingestion d’un lot dans la variable [!DNL Profile] magasin, si le seuil d’augmentation ou de diminution de 5 % est atteint, une tâche est exécutée pour mettre à jour les mesures.

## Utilisation [!UICONTROL Parcourir] onglet pour afficher les profils

Sur le **[!UICONTROL Parcourir]** vous pouvez afficher des exemples de profils à l’aide d’une stratégie de fusion ou rechercher des profils spécifiques à l’aide d’un espace de noms et d’une valeur d’identité.

![Les profils appartenant à l’organisation s’affichent.](../images/user-guide/none-selected.png)

### Parcourir par [!UICONTROL Stratégie de fusion]

La variable **[!UICONTROL Parcourir]** est défini par défaut sur la stratégie de fusion par défaut de votre organisation. Pour choisir une autre stratégie de fusion, sélectionnez la variable `X` en regard du nom de la stratégie de fusion, puis utilisez le sélecteur pour ouvrir la **[!UICONTROL Sélectionner une stratégie de fusion]** boîte de dialogue.

>[!NOTE]
>
>Si aucune stratégie de fusion n’est sélectionnée, utilisez le bouton de sélecteur situé en regard de la propriété **[!UICONTROL Stratégie de fusion]** pour ouvrir la boîte de dialogue de sélection.

![Le sélecteur de stratégie de fusion est mis en surbrillance.](../images/user-guide/browse-by-merge-policy.png)

Pour choisir une stratégie de fusion dans le **[!UICONTROL Sélectionner une stratégie de fusion]** , sélectionnez le bouton radio en regard du nom de la stratégie, puis utilisez **[!UICONTROL Sélectionner]** pour revenir au [!UICONTROL Parcourir] . Vous pouvez ensuite sélectionner **[!UICONTROL Affichage]** pour actualiser les exemples de profils et voir un échantillon de profils auxquels la nouvelle stratégie de fusion est appliquée.

![Une boîte de dialogue dans laquelle vous pouvez sélectionner la stratégie de fusion à filtrer s’affiche.](../images/user-guide/select-merge-policy.png)

Les profils affichés représentent un échantillon de 20 profils au maximum de la banque de profils de votre entreprise, une fois la stratégie de fusion sélectionnée appliquée. Les exemples de profils pour la stratégie de fusion sélectionnée sont actualisés lorsque de nouvelles données sont ajoutées à la banque de profils de votre entreprise.

Pour afficher les détails de l’un des profils d’exemple, sélectionnez l’option **[!UICONTROL Identifiant de profil]**. Pour plus d’informations, reportez-vous à la section suivante de ce guide sur [affichage des détails du profil](#profile-detail).

![Les exemples de profils correspondant à la stratégie de fusion s’affichent.](../images/user-guide/sample-profiles.png)

Pour en savoir plus sur les stratégies de fusion et leur rôle dans Platform, voir [présentation des stratégies de fusion](../merge-policies/overview.md).

### Parcourir par [!UICONTROL Identité] {#browse-identity}

Sur le **[!UICONTROL Parcourir]** vous pouvez utiliser un espace de noms d’identité afin de rechercher un profil spécifique en fonction d’une valeur d’identité. Pour naviguer selon une identité, vous devez fournir une stratégie de fusion, un espace de noms d’identité et une valeur d’identité.

![Le sélecteur de stratégie de fusion est mis en surbrillance.](../images/user-guide/browse-by-merge-policy.png)

Si nécessaire, utilisez la méthode **[!UICONTROL Stratégie de fusion]** pour ouvrir le sélecteur **[!UICONTROL Sélectionner une stratégie de fusion]** et choisissez la stratégie de fusion que vous souhaitez utiliser.

![Une boîte de dialogue dans laquelle vous pouvez sélectionner la stratégie de fusion à filtrer s’affiche.](../images/user-guide/select-merge-policy.png)

Ensuite, utilisez la méthode **[!UICONTROL Espace de noms d’identité]** pour ouvrir le sélecteur **[!UICONTROL Sélectionner un espace de noms d’identité]** et choisissez l’espace de noms par lequel vous souhaitez effectuer une recherche. Si votre organisation dispose de nombreux espaces de noms, vous pouvez utiliser la barre de recherche dans la boîte de dialogue pour commencer à saisir le nom d’un espace de noms.

Vous pouvez sélectionner un espace de noms pour afficher des détails supplémentaires ou sélectionner le bouton radio pour choisir un espace de noms. Vous pouvez ensuite utiliser **[!UICONTROL Sélectionner]** pour continuer.

![Une boîte de dialogue dans laquelle vous pouvez sélectionner l’espace de noms d’identité à filtrer s’affiche.](../images/user-guide/select-identity-namespace.png)

Après avoir sélectionné une [!UICONTROL Espace de noms d’identité] et de revenir à la [!UICONTROL Parcourir] vous pouvez saisir une **[!UICONTROL Valeur d’identité]** associé à l’espace de noms que vous avez sélectionné.

>[!NOTE]
>
>Cette valeur est spécifique à un profil client individuel et doit être une entrée valide pour l’espace de noms fourni. Par exemple, la sélection de l’espace de noms d’identité &quot;E-mail&quot; nécessite une valeur d’identité sous la forme d’une adresse électronique valide.

![La valeur d’identité à filtrer est mise en surbrillance.](../images/user-guide/filter-identity-value.png)

Une fois qu’une valeur a été saisie, sélectionnez **[!UICONTROL Affichage]** et un seul profil correspondant à la valeur est renvoyé. Sélectionnez la variable **[!UICONTROL Identifiant de profil]** pour afficher les détails du profil.

![Le profil correspondant à la valeur d’identité est mis en surbrillance.](../images/user-guide/filtered-identity-value.png)

## Affichage des détails du profil {#profile-detail}

Après avoir sélectionné une **[!UICONTROL Identifiant de profil]**, la variable **[!UICONTROL Détail]** s’ouvre. Les informations de profil affichées dans la **[!UICONTROL Détail]** a été fusionné à partir de plusieurs fragments de profil pour former une vue unique du client individuel. Cela inclut les détails du client tels que les attributs de base, les identités liées et les préférences de canal.

Les champs par défaut affichés peuvent également être modifiés au niveau de l’organisation afin d’afficher les attributs de profil préférés. Pour en savoir plus sur la personnalisation de ces champs, notamment des instructions étape par étape sur l’ajout et la suppression d’attributs et le redimensionnement des panneaux du tableau de bord, consultez la section [guide de personnalisation des détails du profil](profile-customization.md).

![L’onglet Détails est mis en surbrillance. Les détails du profil s’affichent.](../images/user-guide/profile-detail.png)

Vous pouvez afficher des informations supplémentaires relatives au profil client individuel en sélectionnant un autre des onglets disponibles. Ces onglets comprennent les attributs, les événements et l’onglet abonnement à l’audience qui affiche les audiences pour lesquelles le profil est actuellement qualifié.

### Onglet Attributs

La variable **[!UICONTROL Attributs]** L’onglet fournit une vue de liste résumant tous les attributs associés à un seul profil, une fois la stratégie de fusion spécifiée appliquée.

Ces attributs peuvent également être affichés sous forme d’objet JSON en sélectionnant pour **[!UICONTROL Afficher JSON]**. Cela s’avère utile pour les utilisateurs qui souhaitent mieux comprendre comment les attributs de profil sont ingérés dans Platform.

![L’onglet Attributs est surligné. Les attributs de profil s’affichent.](../images/user-guide/attributes.png)

Pour afficher les attributs disponibles sur l’Edge, sélectionnez **[!UICONTROL Edge]** sur le sélecteur d’emplacement des données.

![Le sélecteur d’emplacement de données dans l’onglet Attributs est mis en surbrillance.](../images/user-guide/attributes-select.png)

Pour plus d’informations sur les profils Edge, veuillez lire la section [documentation sur les profils Edge](../edge-profiles.md).

### Onglet Événements

La variable **[!UICONTROL Événements]** Cet onglet contient les données des 100 événements d’expérience les plus récents associés au client. Ces données peuvent inclure les ouvertures de courrier électronique, les activités de panier et les pages vues. Sélection **[!UICONTROL Afficher tout]** pour chaque événement individuel fournit des champs et des valeurs supplémentaires capturés dans le cadre de l’événement.

Les événements peuvent également être affichés sous la forme d’un objet JSON en sélectionnant pour **[!UICONTROL Afficher JSON]**. Cela s’avère utile pour comprendre comment les événements sont capturés dans Platform.

![L’onglet Événements est mis en surbrillance. Les événements de profil s’affichent.](../images/user-guide/events.png)

### Onglet abonnement à l’audience

La variable **[!UICONTROL abonnement à l’audience]** affiche une liste avec le nom et la description des audiences auxquelles appartient actuellement le profil client individuel. Cette liste est mise à jour automatiquement lorsque le profil est admissible ou expire à partir des audiences. Le nombre total d&#39;audiences pour lesquelles le profil est actuellement qualifié s&#39;affiche sur le côté droit de l&#39;onglet.

Pour plus d’informations sur la segmentation dans Experience Platform, reportez-vous au [Documentation d’Adobe Experience Platform Segmentation Service](../../segmentation/home.md).

![L’onglet Appartenance à une audience est mis en surbrillance. Les détails de l’appartenance à l’audience du profil s’affichent.](../images/user-guide/audience-membership.png)

Pour afficher l’appartenance à l’audience des profils disponibles sur Edge, sélectionnez **[!UICONTROL Edge]** dans le sélecteur d’emplacement des données. Vous trouverez plus d’informations sur la segmentation Edge dans la section [guide de segmentation Edge](../../segmentation/ui/edge-segmentation.md).

![Le sélecteur d’emplacement de données dans l’onglet abonnement de l’audience est mis en surbrillance.](../images/user-guide/audience-membership-select.png)

## Politiques de fusion

À partir de la page principale **[!UICONTROL Profils]** , sélectionnez **[!UICONTROL Stratégies de fusion]** pour afficher la liste des stratégies de fusion appartenant à votre organisation. Chaque stratégie répertoriée affiche son nom, qu’il s’agisse de la stratégie de fusion par défaut ou de la classe de schéma à laquelle elle s’applique.

Pour plus d’informations sur les politiques de fusion, consultez [Présentation des politiques de fusion](../merge-policies/overview.md).

![L’onglet Stratégies de fusion est surligné. Les stratégies de fusion appartenant à l’organisation s’affichent.](../images/user-guide/merge-policies.png)

## Schéma d’union {#union-schema}

À partir de la page principale **[!UICONTROL Profils]** , sélectionnez **[!UICONTROL Schéma d’union]** pour afficher les schémas d’union disponibles pour vos données ingérées. Un schéma d’union est une combinaison de tous les [!DNL Experience Data Model] Champs (XDM) de la même classe, dont les schémas ont été activés pour une utilisation dans [!DNL Real-Time Customer Profile].

Pour plus d’informations sur les schémas d’union, consultez la section [guide de l’interface utilisateur de schéma d’union](union-schema.md).

![L’onglet Schéma d’union est mis en surbrillance. Les schémas d’union appartenant à l’organisation s’affichent.](../images/user-guide/union-schema.png)

## Attributs calculés {#computed-attributes}

À partir de la page principale **[!UICONTROL Profils]** , sélectionnez **[!UICONTROL Attributs calculés]** pour afficher la liste des attributs calculés qui appartiennent à votre organisation.

![L’onglet Attributs calculés est mis en surbrillance.](../images/user-guide/computed-attributes.png)

Pour plus d’informations sur les attributs calculés, veuillez lire le [présentation des attributs calculés](../computed-attributes/overview.md). Pour plus d’informations sur l’utilisation des attributs calculés dans l’interface utilisateur de Platform, veuillez lire le [guide de l’interface utilisateur des attributs calculés](../computed-attributes/ui.md).

## Étapes suivantes

En lisant ce guide, vous savez comment afficher et gérer les données de profil de votre entreprise à l’aide de l’interface utilisateur d’Experience Platform. Pour plus d’informations sur l’utilisation des données de profil à l’aide des API Experience Platform, reportez-vous au [Guide de l’API Real-Time Customer Profile](../api/overview.md).
