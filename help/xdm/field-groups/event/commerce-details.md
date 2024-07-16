---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma de détails Commerce
description: Découvrez le groupe de champs de schéma Détails du Commerce .
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 15%

---

# [!UICONTROL Groupe de champs de schéma Détails Commerce]

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Commerce Details] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire les données commerciales telles que les informations sur les produits (SKU, nom, quantité) et les opérations standard du panier (commande, passage en caisse, abandon).

![](../../images/field-groups/commerce-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Objet décrivant les retours de produits, l’enregistrement de la garantie et les processus du panier/de la commande. |
| `productListItems` | Tableau de [ éléments de liste de produits ](../../data-types/product-list-item.md) | Liste d’éléments représentant le ou les produits sélectionnés par un client, avec des options et des tarifs spécifiques à un moment spécifique (qui peuvent différer de l’enregistrement du produit). |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
