---
title: Migration du mappage ECID d’une personne vers une activité à l’aide de la source du Marketo Engage
description: Découvrez comment migrer votre mappage ECID du jeu de données de personne au jeu de données d’activité à l’aide de la source du Marketo Engage.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Migration du mappage ECID du jeu de données [!DNL Person] vers le jeu de données [!DNL Activity]

Vous pouvez migrer votre mappage ECID de votre jeu de données [!DNL Marketo Engage Person] vers votre jeu de données [!DNL Activity] afin de fournir un comportement plus stable de l’ingestion de données et de la gestion des identités. En outre, cette migration traite des éléments suivants :

| Problème | Solution |
| --- | --- |
| Lorsque votre jeu de données [!DNL Marketo Person] comporte des liens vers plusieurs ECID, l’ingestion de données échoue lorsque le nombre [ total d’identités dans un enregistrement de modèle de données d’expérience (XDM) dépasse 20](../../../../identity-service/guardrails.md). | En migrant le mappage des champs ECID vers [!DNL Activity], vous pouvez vous assurer que le nombre d’identités du flux de données [!DNL Marketo Person] reste dans la limite et permet ainsi l’ingestion des données de réussir. |
| Chaque fois que le jeu de données [!DNL Marketo Person] est ingéré avec des ECID, l’horodatage de tous les ECID du jeu de données [!DNL Marketo Person] est mis à jour avec l’horodatage du dernier enregistrement de personne mis à jour. Cela peut entraîner une [ suppression incorrecte des identités plus récentes du graphique d’identités](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | En migrant les mappages de champs ECID vers [!DNL Activity], Identity Service peut correctement refléter l’horodatage de l’ECID et le mécanisme &quot;premier entré, premier sorti&quot; d’Identity Service fournira un comportement plus stable. |
| Lorsque des ECID sont ingérés via le flux de données [!DNL Marketo Person], les ECID nouvellement ajoutés ne sont pas ingérés dans Experience Platform à moins qu’il n’y ait des mises à jour de l’enregistrement [!DNL Person] dans [!DNL Marketo]. | Lorsqu’un nouvel ECID est lié à l’enregistrement [!DNL Person] dans [!DNL Marketo], vous pouvez ingérer ces données ECID par le biais d’un flux de données [!DNL Marketo Activity] et déclencher immédiatement une mise à jour du graphique d’identités sur Experience Platform. |

Essentiellement, vous devez :

* Mettez à jour votre flux de données [!DNL Marketo Activity].
* Mettez à jour votre flux de données [!DNL Marketo Person].

## Mise à jour du flux de données [!DNL Marketo Activity] {#update-activity-dataflow}

Suivez les étapes ci-dessous pour mettre à jour votre flux de données [!DNL Marketo Activity] :

* Dans l’interface utilisateur de l’Experience Platform, accédez à l’espace de travail *Sources* et recherchez votre flux de données existant pour les données [!DNL Marketo Activity].
* Étant donné que le flux de données est activé, sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez **[!UICONTROL Mettre à jour le flux de données]**.
* Sélectionnez ensuite **[!UICONTROL Suivant]** jusqu’à ce que vous ayez atteint l’interface *Mapping*.
* Dans l&#39;interface *Mapping*, sélectionnez **[!UICONTROL Nouveau champ]**, puis sélectionnez **[!UICONTROL Ajouter un champ calculé]**. À partir de là, vous devez ajouter les éléments suivants :

| Jeu de données source | Champ cible XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Si votre mise à jour d’un flux de données [!DNL Marketo] existant consiste uniquement à ajouter ou supprimer le champ de mappage ECID, le flux de données ignore automatiquement la tâche de renvoi historique. Une nouvelle ingestion des données ne se produit que lorsque des types d’activité tels que &quot;page web de visite&quot; et &quot;page web de clic&quot; se produisent.

## Mise à jour du flux de données [!DNL Marketo Person] {#update-person-dataflow}

Suivez les étapes ci-dessous pour mettre à jour votre flux de données [!DNL Marketo Person] :

* Dans l’interface utilisateur de l’Experience Platform, accédez à l’espace de travail *Sources* et recherchez votre flux de données existant pour les données [!DNL Marketo Person].
* Étant donné que le flux de données est activé, sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez **[!UICONTROL Mettre à jour le flux de données]**.
* Sélectionnez ensuite **[!UICONTROL Suivant]** jusqu’à ce que vous ayez atteint l’interface *Mapping*.
* Dans l&#39;interface *Mapping*, supprimez le champ calculé qui mappe sur `identityMap`, puis sélectionnez **[!UICONTROL Suivant]** et **[!UICONTROL Enregistrer et ingérer]**.

>[!NOTE]
>
>Si votre mise à jour d’un flux de données [!DNL Marketo] existant consiste uniquement à ajouter ou supprimer le champ de mappage ECID, le flux de données ignore automatiquement la tâche de renvoi historique. L’horodatage des ECID qui ont été ingérés précédemment reste le même. Elles ne sont mises à jour que lorsque de nouvelles données correspondant aux ECID existants sont ingérées.

## Étapes suivantes

En lisant ce document, vous savez maintenant comment migrer votre mappage ECID de votre jeu de données [!DNL Marketo Person] vers le jeu de données [!DNL Marketo Activity]. Pour plus d’informations, lisez les [!DNL Marketo] documents suivants :

* [Créez un flux de données à ingérer [!DNL Marketo] des données à Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guide de mappage des champs](../mapping/marketo.md).
