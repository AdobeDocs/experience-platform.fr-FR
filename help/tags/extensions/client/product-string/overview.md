---
title: Présentation de l’extension Adobe Analytics Product String
description: Découvrez l’extension de balise Adobe Analytics Product String présente dans Adobe Experience Platform.
exl-id: a49feb4e-f166-41d2-9f85-639f6ff8bb8f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 100%

---

# Présentation de l’extension Adobe Analytics Product String

La variable `products` surveille la manière dont les utilisateurs interagissent avec les produits de votre site. Par exemple, la variable `products` peut surveiller le nombre de fois où un produit est affiché, ajouté au panier, passé en caisse et acheté. Elle peut également surveiller l’efficacité relative des catégories de marchandisage de votre site.

La variable `products` doit toujours être définie conjointement avec un événement de succès.

L’extension [!DNL Adobe Analytics Product String Builder] définit automatiquement la variable `products` en parcourant votre couche de données, en accédant à toutes les données nécessaires liées au produit et en les formatant dans la syntaxe appropriée illustrée ci-dessous. Vous n’avez plus besoin d’écrire et de gérer du code JavaScript personnalisé pour effectuer ces actions complexes.

## Syntaxe de la variable Products

```bash
Category;Product;Quantity;Price;eventN=X|eventN2=X2;eVarN=merch_category|eVarN2=merch_category2
```

Pour obtenir une documentation complète, consultez la page [Produits](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=fr).

## Instructions d’extension

### Configuration d’action

Ajoutez l’action « Adobe Analytics Product String - Set s.products » à votre règle.

![Configuration d’action](./images/screenshot-action-config.png)

### Définition des données de produit standard

Définissez ensuite vos variables de couche de données. Après avoir configuré l’action comme indiqué à l’étape précédente, l’écran suivant s’affiche :

![Champs standard](./images/screenshot-standard-fields.png)

Pour chacun des points de données que vous souhaitez inclure à la chaîne de produit, saisissez le chemin d’accès à la variable de couche de données appropriée.

Par exemple, si votre couche de données est structurée de la manière suivante :

```json
digitalData = {
  "transaction": {
    "item": [{
      "productInfo": {
        "productName": "My Product"
      }
    }]
  }
};
```

vous devez saisir le chemin d’accès suivant dans le champ « Variable de l’ID/du nom du produit » pour capturer la variable `productName` :

```json
digitalData.transaction.item.productInfo.productName
```

>[!NOTE]
>
>si vous utilisez un élément de données pour renseigner ce champ, il doit être configuré à l’aide du type d’élément « Constante » ou « Code personnalisé » et doit renvoyer le chemin d’accès ci-dessus sous la forme d’un littéral de chaîne.

### Type de prix

Le paramètre `price` de la chaîne de produit [!DNL Adobe Analytics] doit correspondre au prix total du nombre d’unités achetées et non au prix unitaire pour ce produit. Lorsque vous activez le champ Price dans l’action d’extension, vous devez indiquer si votre couche de données indique le prix total ou le prix unitaire. En cas d’utilisation du prix unitaire, l’extension [!DNL Adobe Analytics Product String] multipliera automatiquement le prix unitaire par la quantité pour obtenir le prix total et définir la chaîne de produit correctement.

![Type de prix](./images/screenshot-price-type.png)

### Événements personnalisés et eVars de marchandisage

![Événements et eVars](./images/screenshot-events-evars.png)

Si votre mise en œuvre utilise des événements personnalisés ou des eVars de marchandisage, procédez comme suit :

1. Cliquez sur le bouton **[!UICONTROL Add]** associé.
1. Sélectionnez l’événement ou l’eVar que vous devez définir dans la liste déroulante.
1. Saisissez le chemin d’accès à la variable de couche de données appropriée en utilisant la même syntaxe que celle décrite ci-dessus.

### Séquence d’actions

Cette action doit s’accompagner d’une action « Adobe Analytics - Définir les variables » définissant les événements de succès correspondants, ainsi que d’une action « Adobe Analytics - Envoyer une balise ». La séquence d’actions appropriée est illustrée ci-dessous.

![Champs standard](./images/screenshot-action-type.png)

### Conditions

* Une [couche de données](https://theblog.adobe.com/data-layers-buzzword-best-practice/) basée sur un objet avec des variables pour toutes les données liées au produit (comme l’ID du produit, la quantité, le prix). Cette extension ne fonctionne pas avec les couches de données basées sur des tableaux.
* L’extension [Adobe Analytics](../analytics/overview.md) doit être installée.
