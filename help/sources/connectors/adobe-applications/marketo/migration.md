---
title: Migration du mappage ECID d’une personne vers une activité à l’aide de la source du Marketo Engage
description: Découvrez comment migrer votre mappage ECID du jeu de données de personne au jeu de données d’activité à l’aide de la source du Marketo Engage.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Migration du mappage ECID depuis [!DNL Person] dataset à [!DNL Activity] dataset

Vous pouvez migrer votre mappage ECID depuis votre [!DNL Marketo Engage Person] jeu de données à [!DNL Activity] jeu de données afin de fournir un comportement plus stable de l’ingestion des données et de la gestion des identités. En outre, cette migration traite des éléments suivants :

| Problème | Solution |
| --- | --- |
| Lorsque la variable [!DNL Marketo Person] Le jeu de données comporte des liens vers plusieurs ECID, l’ingestion de données échoue lorsque la variable [le nombre total d’identités dans un enregistrement de modèle de données d’expérience (XDM) dépasse 20](../../../../identity-service/guardrails.md). | En migrant le mappage des champs ECID vers [!DNL Activity], vous pouvez vous assurer que le nombre d’identités de la variable [!DNL Marketo Person] le flux de données reste dans la limite et permet donc à l’ingestion de données de réussir. |
| Chaque fois que la variable [!DNL Marketo Person] Le jeu de données est ingéré avec des ECID, l’horodatage de tous les ECID des [!DNL Marketo Person] les jeux de données sont mis à jour avec l’horodatage du dernier enregistrement de personne mis à jour. Cela peut se traduire par le [suppression incorrecte des identités plus récentes du graphique d’identités](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | En migrant les mappages de champs ECID vers [!DNL Activity], Identity Service peut correctement refléter l’horodatage de l’ECID et le mécanisme &quot;premier entré, premier sorti&quot; d’Identity Service fournira un comportement plus stable. |
| Lorsque les ECID sont ingérés via [!DNL Marketo Person] flux de données, les ECID nouvellement ajoutés ne sont pas ingérés dans Experience Platform à moins qu’il n’y ait des mises à jour de la variable [!DNL Person] enregistrement dans [!DNL Marketo]. | Lorsqu’un nouvel ECID est lié à la variable [!DNL Person] enregistrement dans [!DNL Marketo], vous pouvez ingérer des données ECID au moyen d’une [!DNL Marketo Activity] flux de données et invite immédiatement une mise à jour du graphique d’identités sur Experience Platform. |

Essentiellement, vous devez :

* Mettez à jour votre [!DNL Marketo Activity] dataflow.
* Mettez à jour votre [!DNL Marketo Person] dataflow.

## Mettre à jour [!DNL Marketo Activity] dataflow {#update-activity-dataflow}

Pour mettre à jour votre [!DNL Marketo Activity] dataflow :

* Dans l’interface utilisateur de l’Experience Platform, accédez au *Sources* workspace et recherchez votre flux de données existant pour [!DNL Marketo Activity] data.
* Étant donné que le flux de données est activé, sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez **[!UICONTROL Mise à jour du flux de données]**.
* Sélectionnez ensuite **[!UICONTROL Suivant]** jusqu’à ce que vous atteigniez le *Mappage* .
* Dans le *Mappage* interface, sélectionnez **[!UICONTROL Nouveau champ]** puis sélectionnez **[!UICONTROL Ajouter un champ calculé]**. À partir de là, vous devez ajouter les éléments suivants :

| Jeu de données source | Champ cible XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Si votre mise à jour est [!DNL Marketo] le flux de données consiste uniquement à ajouter ou supprimer le champ de mappage ECID, puis le flux de données ignore automatiquement la tâche de renvoi historique. Une nouvelle ingestion des données ne se produit que lorsque des types d’activité tels que &quot;page web de visite&quot; et &quot;page web de clic&quot; se produisent.

## Mettre à jour [!DNL Marketo Person] dataflow {#update-person-dataflow}

Pour mettre à jour votre [!DNL Marketo Person] dataflow :

* Dans l’interface utilisateur de l’Experience Platform, accédez au *Sources* workspace et recherchez votre flux de données existant pour [!DNL Marketo Person] data.
* Étant donné que le flux de données est activé, sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez **[!UICONTROL Mise à jour du flux de données]**.
* Sélectionnez ensuite **[!UICONTROL Suivant]** jusqu’à ce que vous atteigniez le *Mappage* .
* Dans le *Mappage* , supprimez le champ calculé auquel correspond `identityMap` puis sélectionnez **[!UICONTROL Suivant]** et **[!UICONTROL Enregistrement et ingestion]**.

>[!NOTE]
>
>Si votre mise à jour est [!DNL Marketo] le flux de données consiste uniquement à ajouter ou supprimer le champ de mappage ECID, puis le flux de données ignore automatiquement la tâche de renvoi historique. L’horodatage des ECID qui ont été ingérés précédemment reste le même. Elles ne sont mises à jour que lorsque de nouvelles données correspondant aux ECID existants sont ingérées.

## Étapes suivantes

En lisant ce document, vous savez maintenant comment migrer votre mappage ECID à partir de votre [!DNL Marketo Person] dataset à [!DNL Marketo Activity] jeu de données. Pour plus d’informations, lisez ce qui suit : [!DNL Marketo] documents :

* [Création d’un flux de données à ingérer [!DNL Marketo] données à l’Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guide de mappage des champs](../mapping/marketo.md).