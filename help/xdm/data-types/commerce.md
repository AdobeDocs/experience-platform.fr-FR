---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; commerce ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données Commerce
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Commerce Experience Data Model).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---

# [!UICONTROL Type ] de données commerciales

 Commerceest un type de données standard de modèle de données d’expérience (XDM) qui décrit les enregistrements liés à l’achat et à la vente d’activités.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `order` | [[!UICONTROL Commande]](./order.md) | Décrit la commande passée pour un ou plusieurs produits. |
| `cartAbandons` | [[!UICONTROL Mesure]](./measure.md) | Utilisé pour décrire lorsqu’une liste de produits a été identifiée comme n’étant plus accessible ou ne pouvant plus être achetée par l’utilisateur. |
| `checkouts` | [[!UICONTROL Mesure]](./measure.md) | Action pendant le processus de passage en caisse d&#39;une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s&#39;il y a plusieurs étapes dans un processus de passage en caisse. S’il existe plusieurs étapes, les informations de événement et la page ou l’expérience référencée sont utilisées pour identifier l’étape et les événements individuels représentés dans l’ordre. |
| `inStorePurchase` | [[!UICONTROL Mesure]](./measure.md) | Décrit une valeur associée à un achat en magasin pour une utilisation d’analyse. |
| `productListAdds` | [[!UICONTROL Mesure]](./measure.md) | Ajout d’un produit à la liste de produits, tel qu’un produit ajouté à un panier. |
| `productListOpens` | [[!UICONTROL Mesure]](./measure.md) | Initialisations d’une nouvelle liste de produits, telle qu’un panier en cours de création. |
| `productListRemovals` | [[!UICONTROL Mesure]](./measure.md) | Suppression ou suppression d’une entrée de produit d’une liste de produits, telle qu’un produit supprimé d’un panier. |
| `productListReopens` | [[!UICONTROL Mesure]](./measure.md) | Liste de produit précédemment abandonnée qui a été réactivée par l’utilisateur. |
| `productListViews` | [[!UICONTROL Mesure]](./measure.md) | Décrit quand une ou plusieurs vues d&#39;une liste de produits se sont produites. |
| `productViews` | [[!UICONTROL Mesure]](./measure.md) | Décrit le moment où une ou plusieurs vues d&#39;un produit ont eu lieu. |
| `purchases` | [[!UICONTROL Mesure]](./measure.md) | Permet de suivre quand une commande a été acceptée. Le événement d’achat est la seule action requise dans une conversion commerciale. Une liste de produit doit être référencée dans le événement d’achat. |
| `saveForLaters` | [[!UICONTROL Mesure]](./measure.md) | Une liste de produit est enregistrée pour une utilisation ultérieure, telle qu’une liste de souhait. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
