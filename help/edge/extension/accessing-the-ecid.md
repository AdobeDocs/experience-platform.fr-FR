---
title: 'Accès à l’ECID '
description: Extension SDK Web Adobe Experience Platform Utilisation de l’ECID dans les balises
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 9%

---


# Accès à l’ECID

[!DNL Experience Cloud Identity (ECID)] est l’identifiant persistant d’un visiteur de votre site Web. Dans certains cas, vous préférerez peut-être accéder à l’ECID (pour l’envoyer à un tiers, par exemple).

Pour accéder à l’ECID dans des balises, Adobe recommande ce qui suit :

1. Vérifiez que la propriété est configurée avec l’option [séquencement des composants de règle](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) activée.
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
