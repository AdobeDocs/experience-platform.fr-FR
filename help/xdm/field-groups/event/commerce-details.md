---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma de détails du commerce
topic-legacy: overview
description: Ce document fournit un aperçu du groupe de champs de schéma Détails du commerce .
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 4%

---

# [!UICONTROL Groupe de champs ] Commerce Detailsschema

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Détails du commerce ] est un groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire les données commerciales telles que les informations sur les produits (SKU, nom, quantité) et les opérations standard du panier (commande, passage en caisse, abandon).

![](../../images/field-groups/commerce-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Objet décrivant les retours de produits, l’enregistrement de la garantie et les processus du panier/de la commande. |
| `productListItems` | Tableau des [éléments de liste de produits](../../data-types/product-list-item.md) | Liste d’éléments représentant le ou les produits sélectionnés par un client, avec des options et des tarifs spécifiques à un moment spécifique (qui peuvent différer de l’enregistrement du produit). |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
