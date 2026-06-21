---
title: Accès à l’ECID
description: Découvrez comment accéder à l’Experience Cloud ID à partir de la préparation des données ou des balises
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
TQID: https://experienceleague.adobe.com/4k6I22EfvjFzCd1ypMIgDYibE7lMxf7P-XJZ-kFKnCc
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: e43347a8-f2c5-4aa4-8623-6f13875d7e3aid: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: aff8c1fa-1be7-48bd-92b8-4b12a668ca13id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 283
ht-degree: 4%

---

# Accès à l’ECID

Le [!DNL Experience Cloud Identity (ECID)] est un identifiant persistant attribué à un utilisateur ou une utilisatrice qui visite votre site web. Dans certains cas, vous pouvez préférer accéder au [!DNL ECID] (l’envoyer à un tiers, par exemple). Un autre cas d’utilisation consiste à définir le [!DNL ECID] dans un champ XDM personnalisé, en plus de l’avoir dans le mappage d’identité.

Vous pouvez accéder à l’ECID par le biais de [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md) (recommandé) ou par le biais de balises.

## Accès à l’ECID par le biais de la préparation des données (méthode préférée) {#accessing-ecid-data-prep}

Cette méthode utilise [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md) pour configurer un mappage personnalisé pour la `ECID`.

Consultez la documentation [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md) pour savoir comment utiliser cette fonctionnalité.

Si vous souhaitez définir l’ECID dans un champ XDM personnalisé, en plus de l’avoir dans le mappage d’identités, vous pouvez le faire en définissant l’`source` sur le chemin suivant :

```js
xdm.identityMap.ECID[0].id
```

Définissez ensuite la cible sur un chemin XDM où le champ est de type `string`.

![](./assets/access-ecid-data-prep.png)

## Balises

Si vous devez accéder au [!DNL ECID] côté client, utilisez l’approche des balises comme décrit ci-dessous.

1. Assurez-vous que votre propriété est configurée avec le [séquencement des composants de règle](/help/tags/ui/managing-resources/rules.md#sequencing) activé.
1. Créez une nouvelle règle. Cette règle doit être utilisée exclusivement pour capturer le [!DNL ECID] sans autre action importante.
1. Ajoutez un événement [!UICONTROL Library Loaded] à la règle.
1. Ajoutez une action [!UICONTROL Code personnalisé] à la règle avec le code suivant (en supposant que le nom que vous avez configuré pour l’instance SDK soit `alloy` et qu’il n’existe pas déjà un élément de données du même nom) :

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Enregistrez la règle.

Vous devriez ensuite pouvoir accéder au [!DNL ECID] dans les règles suivantes à l’aide de `%ECID%` ou `_satellite.getVar("ECID")`, comme vous le feriez pour tout autre élément de données.
