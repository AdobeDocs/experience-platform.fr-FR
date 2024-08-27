---
title: Création d’un filtre global
description: Découvrez comment filtrer vos informations sur les données à l’aide d’un filtre personnalisé appliqué globalement.
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: 5dd821383e1b1a7bd4998a6cf14a941bfdf3f26c
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 1%

---

# Créer un filtre global {#create-global-filter}

Pour créer un filtre global, sélectionnez d’abord **[!UICONTROL Ajouter un filtre]** dans la vue de votre tableau de bord, puis **[!UICONTROL Filtre global]** dans le menu déroulant.

>[!IMPORTANT]
>
>Assurez-vous d’associer vos filtres globaux à tous vos graphiques. Il ne s’agit pas d’un processus automatique. Pour utiliser un filtre global, vous devez inclure un [paramètre de requête](../../../../query-service/ui/parameterized-queries.md) dans le SQL de votre graphique, [activer le filtre global](#enable-global-filter) dans le compositeur de widget et [sélectionner une valeur d’exécution](#select-global-filter) pour le paramètre dans la boîte de dialogue de filtre global. Consultez le guide de pro-requête pour savoir comment modifier votre SQL si vous devez incorporer un paramètre de requête.

![ Un tableau de bord personnalisé avec l’option Ajouter un filtre et son menu déroulant en surbrillance.](../../../images/query-pro-mode/add-filter.png)

Vous pouvez rapidement modifier les insights fournis par votre SQL avec des filtres globaux personnalisés.

La boîte de dialogue [!UICONTROL Créer un filtre global] s’ouvre. La création d&#39;un filtre global suit le même processus que la création d&#39;un insight avec SQL. Sélectionnez tout d’abord une base de données (modèle de données d’insights) à interroger, puis saisissez votre code SQL personnalisé dans Query Editor, et enfin sélectionnez l’icône d’exécution (![Icône d’exécution.](/help/images/icons/play.png)).

>[!IMPORTANT]
>
>Lorsque vous créez un filtre global, vous devez inclure un identifiant et une valeur. Les exemples de valeurs vous permettent d’exécuter l’instruction SQL et de créer le graphique. Notez que les exemples de valeurs que vous fournissez lors de la composition de votre instruction sont remplacés par les valeurs réelles que vous sélectionnez pour la date ou le filtre global au moment de l’exécution.

Une fois la requête exécutée, l’onglet Résultats affiche les résultats. Sélectionnez **[!UICONTROL Suivant]**.

![ La [!UICONTROL boîte de dialogue Créer un filtre global] avec le menu déroulant du jeu de données, l’icône d’exécution et Suivant mise en surbrillance.](../../../images/query-pro-mode/global-filter.png)

La dernière étape du workflow de création de filtre global nécessite l’ajout d’un libellé pour votre filtre. Ajoutez un libellé au champ de texte **[!UICONTROL Libellé du filtre]** et sélectionnez un type de filtre dans la liste déroulante.

>[!NOTE]
>
>Seule l’option de type de filtre [!UICONTROL Combo box] est actuellement prise en charge.

Enfin, sélectionnez **[!UICONTROL Sélectionner]** pour revenir à la vue de votre tableau de bord.

![ La [!UICONTROL boîte de dialogue Créer un filtre global] avec l’option Sélectionner et l’entrée de texte Libellé du filtre mise en surbrillance.](../../../images/query-pro-mode/global-filter-label.png)

## Activer le filtre global pour chaque insight {#enable-global-filter}

>[!TIP]
>
>Activez les filtres globaux dans chaque graphique que vous créez. Vous avez ainsi la garantie que les valeurs que vous choisissez comme filtre global à refléter dans tous vos graphiques.

Après avoir créé votre filtre global pour votre tableau de bord, le bouton d’activation/désactivation de ce filtre global devient disponible dans le cadre du compositeur de widgets.

![Le compositeur de widget avec le bouton bascule Filtre global mis en surbrillance.](../../../images/query-pro-mode/global-filter-consent.png)

>[!IMPORTANT]
>
>Assurez-vous que le paramètre de filtre global est inclus dans le SQL de chaque insight.

## Sélectionner un filtre global {#select-global-filter}

Pour ouvrir la boîte de dialogue [!UICONTROL Filtres] qui répertorie tous vos filtres personnalisés, sélectionnez l’icône de filtre (![Icône de filtre).](/help/images/icons/filter.png)) à gauche de votre tableau de bord. Ensuite, pour appliquer les effets sur vos insights de tableau de bord, sélectionnez une option dans le menu déroulant de votre filtre global, puis sélectionnez **[!UICONTROL Appliquer]**.

![Un tableau de bord personnalisé avec la boîte de dialogue de filtrage mise en surbrillance.](../../../images/query-pro-mode/custom-filters.png)

## Effacer le filtre global {#clear-global-filter}

Pour effacer tous vos filtres globaux personnalisés, sélectionnez **[!UICONTROL Effacer tout]** dans la boîte de dialogue [!UICONTROL Filtres] .

![ La boîte de dialogue Filtres avec Effacer tout surligné.](../../../images/query-pro-mode/clear-all.png)

