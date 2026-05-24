---
title: Migrer le mappage ECID d’une personne vers une activité à l’aide de la source Marketo Engage
description: Découvrez comment migrer votre mappage ECID du jeu de données de personne vers le jeu de données d’activité à l’aide de la source Marketo Engage.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
TQID: https://experienceleague.adobe.com/SoKZ0Cg-VzZ-ooMrTYiun62RQnglkhMM-DonNSjc6Ac
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 538
ht-degree: 1%

---

# Migration du mappage ECID d’[!DNL Person] jeu de données vers [!DNL Activity] jeu de données

Vous pouvez migrer votre mappage ECID de votre jeu de données [!DNL Marketo Engage Person] vers votre jeu de données [!DNL Activity] afin de fournir un comportement plus stable de l’ingestion des données et de la gestion des identités. En outre, cette migration répond aux besoins suivants :

| Problème | Solution |
| --- | --- |
| Lorsque votre jeu de données [!DNL Marketo Person] comporte des liens vers plusieurs ECID, l’ingestion des données échoue lorsque le [ nombre total d’identités dans un enregistrement de modèle de données d’expérience (XDM) dépasse 20 ](../../../../identity-service/guardrails.md). | En migrant le mappage des champs ECID vers [!DNL Activity], vous pouvez vous assurer que le nombre d’identités du flux de données [!DNL Marketo Person] reste dans la limite et permettre ainsi à l’ingestion des données de réussir. |
| Chaque fois que le jeu de données [!DNL Marketo Person] est ingéré avec des ECID, l’horodatage de tous les ECID du jeu de données [!DNL Marketo Person] est mis à jour avec l’horodatage de la dernière mise à jour de l’enregistrement Personne. Cela peut entraîner la suppression [ incorrecte des identités plus récentes du graphique d’identités](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | En migrant les mappages de champs ECID vers [!DNL Activity], Identity Service peut refléter correctement la date et l’heure des ECID et le mécanisme de « premier entré, premier sorti » d’Identity Service offrira un comportement plus stable. |
| Lorsque des ECID sont ingérés par le biais d’[!DNL Marketo Person] flux de données, les ECID nouvellement ajoutés ne sont pas ingérés dans Experience Platform, sauf si l’enregistrement [!DNL Person] est mis à jour dans [!DNL Marketo]. | Lorsqu’un nouvel ECID est lié à l’enregistrement [!DNL Person] dans [!DNL Marketo], vous pouvez ingérer ces données ECID par le biais d’un flux de données [!DNL Marketo Activity] et demander immédiatement une mise à jour du graphique d’identité dans Experience Platform. |

En substance, vous devez :

* Mettez à jour votre flux de données [!DNL Marketo Activity].
* Mettez à jour votre flux de données [!DNL Marketo Person].

## Mettre à jour [!DNL Marketo Activity] flux de données {#update-activity-dataflow}

Pour mettre à jour votre flux de données [!DNL Marketo Activity], procédez comme suit :

* Dans l’interface utilisateur d’Experience Platform, accédez à l’espace de travail *Sources* et recherchez votre flux de données existant pour les données [!DNL Marketo Activity].
* Étant donné que le flux de données est activé, sélectionnez les points de suspension (`...`) à côté du nom du flux de données, puis sélectionnez **[!UICONTROL Update dataflow]**.
* Sélectionnez ensuite **[!UICONTROL Next]** jusqu’à atteindre l’interface *Mappage*.
* Dans l’interface *Mappage*, sélectionnez **[!UICONTROL New field]** puis **[!UICONTROL Add calculated field]**. À partir de là, vous devez ajouter les éléments suivants :

| Jeu de données source | Champ cible XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Si votre mise à jour d’un flux de données [!DNL Marketo] existant consiste uniquement à ajouter ou à supprimer le champ de mappage ECID, le flux de données ignore automatiquement la tâche de renvoi historique. L’ingestion de nouvelles données ne se produit que lorsque des types d’activité tels que « Visiter la page web » et « Cliquer sur la page web » se produisent.

## Mettre à jour [!DNL Marketo Person] flux de données {#update-person-dataflow}

Pour mettre à jour votre flux de données [!DNL Marketo Person], procédez comme suit :

* Dans l’interface utilisateur d’Experience Platform, accédez à l’espace de travail *Sources* et recherchez votre flux de données existant pour les données [!DNL Marketo Person].
* Étant donné que le flux de données est activé, sélectionnez les points de suspension (`...`) à côté du nom du flux de données, puis sélectionnez **[!UICONTROL Update dataflow]**.
* Sélectionnez ensuite **[!UICONTROL Next]** jusqu’à atteindre l’interface *Mappage*.
* Dans l’interface *Mappage*, supprimez le champ calculé qui mappe à `identityMap`, puis sélectionnez **[!UICONTROL Next]** et **[!UICONTROL Save & Ingest]**.

>[!NOTE]
>
>Si votre mise à jour d’un flux de données [!DNL Marketo] existant consiste uniquement à ajouter ou à supprimer le champ de mappage ECID, le flux de données ignore automatiquement la tâche de renvoi historique. L’horodatage des ECID précédemment ingérés reste le même. Elles ne sont mises à jour que lorsque de nouvelles données correspondant aux ECID existants sont ingérées.

## Étapes suivantes

En lisant ce document, vous savez désormais comment migrer votre mappage ECID de votre jeu de données [!DNL Marketo Person] vers [!DNL Marketo Activity] jeu de données . Pour plus d’informations, consultez les documents [!DNL Marketo] suivants :

* [Créez un flux de données pour ingérer  [!DNL Marketo]  données dans Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guide de mappage des champs](../mapping/marketo.md).
