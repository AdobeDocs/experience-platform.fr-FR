---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;ExperienceEvent;champs;schémas;Schémas;Conception de schéma;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma des détails de Commerce
description: Découvrez le groupe de champs de schéma Détails du Commerce .
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
TQID: https://experienceleague.adobe.com/exUxw4CK2fbT0hyLZ7PwnnFgTWkzz2dEiGbGoL6rjUk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 182
ht-degree: 13%

---

# [!UICONTROL Détails Commerce &#x200B;] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails &#x200B;] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire des données commerciales telles que des informations sur le produit (SKU, nom, quantité) et des opérations de panier standard (commande, passage en caisse, abandon).

![](../../images/field-groups/commerce-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `commerce` | [&#128279;](../../data-types/commerce.md) | Objet décrivant les retours de produits, l’enregistrement de la garantie et les processus de commande/panier. |
| `productListItems` | Tableau d’[éléments de la liste de produits](../../data-types/product-list-item.md) | Liste d’éléments représentant le ou les produits sélectionnés par un client, avec des options et des prix spécifiques à un moment donné (qui peut différer de l’enregistrement du produit). |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
