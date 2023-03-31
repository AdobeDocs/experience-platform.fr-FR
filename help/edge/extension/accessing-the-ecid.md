---
title: Accès à l’ECID
description: Découvrez comment accéder à l’ID Experience Cloud (ECID) dans les balises Adobe Experience Platform
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# Accès à l’ECID

Le [!DNL Experience Cloud ID (ECID)] est un identifiant d’Experience Cloud persistant qui peut vous aider à identifier les visiteurs de votre site web. Dans certaines circonstances, comme l’envoi de l’identifiant à une plateforme tierce, vous devrez peut-être accéder à la variable [!DNL ECID].

Pour accéder au [!DNL ECID] dans les balises , procédez comme suit :

1. Vérifiez que votre propriété est configurée avec [séquencement des composants de règle](../../tags/ui/managing-resources/rules.md#sequencing) activée.
2. Créez une nouvelle règle.
3. Ajouter un [!UICONTROL Bibliothèque chargée] à la règle.
4. Ajouter un [!UICONTROL Condition personnalisée] à la règle, avec le code suivant (en supposant que le nom que vous avez configuré pour l’instance du SDK est `alloy`) :

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. Enregistrez la règle.

Vous devriez maintenant pouvoir accéder au [!DNL ECID] dans les règles suivantes, en utilisant `%ECID%` ou `_satellite.getVar("ECID")`, comme vous accédez à tout autre élément de données.
