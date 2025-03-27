---
title: Appliquez des libellés d’accès pour gérer l’accès des utilisateurs aux flux de données sources dans l’interface utilisateur
description: Découvrez comment utiliser l’interface utilisateur d’Experience Platform pour appliquer des libellés d’accès et gérer l’accès des utilisateurs à vos flux de données sources.
exl-id: 7aab9706-2f43-43c7-9878-1959d5a8a6b0
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 3%

---

# Appliquez des libellés d’accès pour gérer l’accès des utilisateurs aux flux de données sources dans l’interface utilisateur

Vous pouvez utiliser les fonctionnalités fournies par [contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md) dans Real-Time CDP pour appliquer des libellés à vos flux de données sources. Grâce à cette fonctionnalité, vous pouvez vous assurer que seul un sous-ensemble d’utilisateurs de votre organisation a accès à des flux de données sources spécifiques.

Lorsque vous ajoutez un libellé d’accès à un flux de données spécifique, seuls les utilisateurs et utilisatrices ayant accès à un rôle auquel ce libellé est affecté peuvent afficher et modifier ce flux de données. Si un flux de données de sources n’est marqué d’aucun libellé, il est visible par tous les utilisateurs appartenant à votre organisation. Par exemple, si vous appliquez le libellé C12 à un flux de données, les utilisateurs affectés à un rôle qui ne dispose pas du libellé C12 ne pourront pas afficher et modifier le flux de données avec le libellé C12.

Lisez ce guide pour plus d’informations sur la manière d’appliquer des libellés d’accès à vos flux de données sources à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Commencer

Avant d’utiliser des libellés de contrôle d’accès, familiarisez-vous d’abord avec les fonctionnalités du contrôle d’accès basé sur les attributs. Pour plus d’informations, consultez la documentation suivante :

* [Présentation du contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md)
* [Guide complet du contrôle d’accès basé sur les attributs](../../../access-control/abac/end-to-end-guide.md)
* [Gestion des libellés à l’aide de l’interface utilisateur des autorisations](../../../access-control/abac/ui/labels.md)
* [Glossaire des étiquettes dʼutilisation des données](../../../data-governance/labels/reference.md)

## Application de libellés d’accès aux flux de données sources

>[!NOTE]
>
>* Vous ne pouvez pas appliquer de libellés à une exécution de flux. Toutefois, les exécutions de flux héritent des libellés que vous appliquez au flux de données parent.
>
>* Si vous ne disposez pas d’un accès en lecture seule à un flux de données, vous ne pourrez pas non plus afficher ses exécutions de flux correspondantes.

Pour appliquer des libellés d’accès à vos flux de données sources, accédez à **[!UICONTROL Sources]** > **[!UICONTROL Flux de données]** puis localisez le flux de données à mettre à jour et limitez l’accès des utilisateurs et utilisatrices.

Sélectionnez ensuite les points de suspension (`...`) dans la colonne [!UICONTROL Nom], puis sélectionnez **[!UICONTROL Appliquer les libellés d’accès]** pour ajouter et gérer des libellés pour le flux de données sélectionné.

![Page flux de données dans les sources avec l’option Appliquer les libellés d’accès sélectionnée.](../../images/tutorials/labels/apply_access_labels.png)

La fenêtre [!UICONTROL Appliquer l’accès et les libellés de gouvernance des données] s’affiche. Utilisez cette fenêtre pour sélectionner les libellés à appliquer à votre flux de données. Vous pouvez également filtrer les libellés par type. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Fenêtre des libellés de gouvernance des données avec le libellé C2 sélectionné.](../../images/tutorials/labels/labels_window.png)

Une fois que vous avez correctement configuré les libellés d’accès à votre flux de données, tout utilisateur n’ayant pas accès à ce libellé ne peut plus récupérer le flux de données. Vous pouvez également utiliser la colonne [!UICONTROL Libellés d’accès] pour afficher les libellés appliqués à un flux de données donné.

## Étapes suivantes

Vous savez désormais comment appliquer des libellés d’accès à vos flux de données sources. Vous pouvez désormais vous assurer que seul un groupe spécifique d’utilisateurs de votre organisation peut accéder à certains flux de données sources. Pour plus d’informations, consultez la documentation suivante :

* [Appliquer des libellés d’accès aux flux de données sources dans l’API](../api/labels.md)
* [Présentation du contrôle d’accès](../../../access-control/home.md)
