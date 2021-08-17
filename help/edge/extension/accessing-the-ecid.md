---
title: 'Accès à l’ECID '
description: Extension SDK Web Adobe Experience Platform Utilisation de l’ECID dans les balises
source-git-commit: befe1efa884706165b8d65803d06f6370a8a60f2
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 10%

---


# Accès à l’ECID

[!DNL Experience Cloud Identity (ECID)] est l’identifiant persistant d’un visiteur de votre site Web. Dans certains cas, vous préférerez peut-être accéder à l’ECID (pour l’envoyer à un tiers, par exemple).

Pour accéder à l’ECID dans des balises, Adobe recommande ce qui suit :

1. Vérifiez que la propriété est configurée avec l’option [séquencement des composants de règle](../../tags/ui/managing-resources/rules.md#sequencing) activée.
1. Créez une nouvelle règle.
1. Ajoutez un événement [!UICONTROL Library Loaded] (Bibliothèque chargée) à la règle.
1. Ajoutez une action [!UICONTROL Condition personnalisée] à la règle avec le code suivant (en supposant que le nom que vous avez configuré pour l’instance du SDK soit `alloy`) :

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Enregistrez la règle.

Vous devriez ensuite pouvoir accéder à l’ECID dans les règles suivantes à l’aide de `%ECID%` ou `_satellite.getVar("ECID")` comme vous le feriez pour tout autre élément de données.
