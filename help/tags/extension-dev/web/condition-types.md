---
title: Types de conditions pour les extensions web
description: Découvrez comment définir un module de bibliothèque de types de conditions pour une extension de balise dans une propriété web.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
TQID: https://experienceleague.adobe.com/zhRKBIZo0eLL0nwTqBFLb5q6NkuB-upthSP9A6VWoI8
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 461
ht-degree: 95%

---

# Types de conditions pour les extensions web

Dans le contexte d’une règle, une condition est évaluée une fois qu’un événement s’est produit. Toutes les conditions doivent renvoyer la valeur vraie pour que la règle continue son traitement. Une exception survient lorsque les utilisateurs placent explicitement des conditions dans un compartiment « exception », auquel cas toutes les conditions du compartiment doivent renvoyer la valeur false pour que la règle puisse continuer le traitement.

Par exemple, une extension peut fournir un type de condition « viewport contains » dans lequel l’utilisateur peut spécifier un sélecteur CSS. Lorsque la condition est évaluée sur le site web du client, l’extension peut trouver des éléments correspondant au sélecteur CSS et renvoyer si la fenêtre d’affichage de l’utilisateur contient l’un d’entre eux.

Ce document explique comment définir des types de conditions pour une extension web dans Adobe Experience Platform.

>[!NOTE]
>
>Si vous développez une extension Edge, reportez-vous au guide sur les [types de condition pour les extensions Edge](../edge/condition-types.md) à la place.
>
>Ce document suppose que vous connaissez les modules de bibliothèque et leur intégration dans les extensions web. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types de conditions se composent généralement des éléments suivants :

1. Une [vue](./views.md) affichée dans l’interface utilisateur d’Experience Platform et l’interface utilisateur de la collecte de données, qui permet aux utilisateurs de modifier les paramètres de la condition.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et évaluer une condition.

Un module de bibliothèque de type de condition a un seul objectif : évaluer si quelque chose est vrai ou faux. Ce qu’il évalue ne dépend que de vous.

Par exemple, si vous souhaitez évaluer si l’utilisateur se trouve sur l’hôte `example.com`, votre module peut se présenter comme suit :

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Maintenant, imaginez une situation où vous souhaitez rendre le nom d’hôte configurable par l’utilisateur Adobe Experience Platform Vous pouvez autoriser l’utilisateur à saisir un nom d’hôte, puis enregistrer ce dernier dans l’objet settings. L’objet pourrait ressembler à ceci :

```js
{
  "hostname": "example.com"
}
```

Pour fonctionner sur le nom d’hôte défini par l’utilisateur, votre module doit changer de la façon suivante :

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Données contextuelles de l’événement

Un second argument qui contient des informations contextuelles concernant l’événement qui a déclenché la règle est transmis à votre module. Ces informations peuvent être utiles dans certains cas et peuvent être consultées comme suit :

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

L’objet `event` doit contenir les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `$type` | Chaîne décrivant le nom de l’extension et le nom de l’événement, joints à l’aide d’un point. Par exemple : `youtube.play`. |
| `$rule` | Objet contenant des informations sur la règle en cours d’exécution. L’objet doit contenir les sous-propriétés suivantes :<ul><li>`id` : ID de la règle en cours d’exécution.</li><li>`name` : nom de la règle en cours d’exécution.</li></ul> |

L’extension fournissant le type d’événement qui a déclenché la règle peut éventuellement ajouter toute autre information utile à cet objet `event`.
