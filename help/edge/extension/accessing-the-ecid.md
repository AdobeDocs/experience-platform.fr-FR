---
title: 'Accès à l''ECID '
description: Adobe Experience Platform Web SDK Extension Exploitation de l'ECID dans Adobe Experience Platform Launch
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---


# Accès à l&#39;ECID

[!DNL Experience Cloud Identity (ECID)] est un identifiant persistant pour un visiteur de votre site Web. Dans certains cas, vous préférerez peut-être accéder à l’ECID (pour l’envoyer à un tiers, par exemple).

Pour accéder à l&#39;ECID dans Adobe Experience Platform Launch, l&#39;Adobe recommande ce qui suit :

1. Assurez-vous que votre propriété est configurée avec [le séquencement du composant de règle](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) activé.
1. Créez une nouvelle règle.
1. Ajoutez un événement [!UICONTROL Bibliothèque chargée] à la règle.
1. Ajoutez une action [!UICONTROL Condition personnalisée] à la règle avec le code suivant (en supposant que le nom que vous avez configuré pour l’instance du SDK soit `alloy`) :

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Enregistrez la règle.

Vous devriez alors pouvoir accéder à l&#39;ECID dans les règles suivantes en utilisant `%ECID%` ou `_satellite.getVar("ECID")` comme vous le feriez pour tout autre élément de données.
