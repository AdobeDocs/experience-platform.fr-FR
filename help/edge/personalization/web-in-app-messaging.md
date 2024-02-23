---
title: Configuration de la prise en charge de la messagerie web in-app dans le SDK web
description: Découvrez comment configurer l’extension de balise du SDK Web pour prendre en charge la messagerie in-app web.
source-git-commit: a020f880be2606024c6a986dc468d70a2fbdc30f
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Configuration de la prise en charge de la messagerie web in-app dans le SDK web


Les messages in-app sont des notifications que vous pouvez envoyer aux utilisateurs dans votre application web, en les guidant vers des points ciblés spécifiques.

Vous pouvez utiliser ces notifications à différentes fins, par exemple pour promouvoir de nouvelles fonctionnalités, présenter des offres spéciales ou faciliter l’intégration des utilisateurs.

En utilisant les messages in-app, vous pouvez interagir efficacement avec votre audience et l’orienter vers des aspects importants de votre application.

>[!IMPORTANT]
>
>La messagerie web in-app est une [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr) qui utilise le SDK Web pour diffuser le contenu personnalisé.
>
>Pour obtenir des instructions détaillées sur la configuration de votre campagne de messagerie web in-app, voir [Documentation Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html).


## Conditions préalables {#prerequisites}

### Version de l’extension de balise SDK Web {#extension-version}

La fonctionnalité de messagerie in-app web requiert la dernière version de l’extension de balise SDK web.

### Configuration d’une CSP pour la messagerie web in-app {#csp}

Lorsque vous configurez [Messagerie in-app web](../personalization/web-in-app-messaging.md), vous devez inclure la directive suivante dans votre CSP :

```
default-src  blob:;
```

Pour plus d’informations sur la configuration d’une CSP, voir la section [documentation dédiée](../fundamentals/configuring-a-csp.md).

## Configuration de la messagerie web in-app à l’aide de l’extension de balise SDK web {#tag-extension}

Voir [Page de configuration de l’extension de balise SDK Web](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) pour savoir où trouver les paramètres décrits ci-dessous.

Après avoir [installé](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) Pour configurer l’extension pour la messagerie in-app web, procédez comme suit.

Dans le **[!UICONTROL Personnalisation]** , vérifiez les **[!UICONTROL Activer le stockage de personnalisation]** . Cette option permet au SDK Web de suivre les expériences qui ont été vues par l’utilisateur lors du chargement d’une page.

![Image montrant l’option de stockage de personnalisation dans la page de configuration de l’extension de balise.](assets/web-in-app-messaging/enable-personalization-storage.png)


La messagerie web in-app prend en charge deux types de déclencheurs :

* [Envoi de données à Platform](#send-data-platform)
* [Déclenchement manuel des messages](#manual-trigger)

Reportez-vous aux sections suivantes pour configurer l’extension de balise du SDK Web en fonction des déclencheurs que vous souhaitez utiliser.

### Étapes de configuration de la variable **[!UICONTROL Envoi de données à Platform]** trigger {#send-data-platform}

Sélectionnez la propriété de balise qui contient votre extension SDK Web, et [créer une règle](../../tags/ui/managing-resources/rules.md##create-a-rule) avec les paramètres suivants :

1. **[!UICONTROL Extension]** : [!UICONTROL Core]
2. **[!UICONTROL Type d’événement]**: [!UICONTROL Bibliothèque chargée (Haut de page)]

   ![Image montrant l’écran de configuration de l’événement.](assets/web-in-app-messaging/rule-configuration.png)

3. Sélectionner **[!UICONTROL Conserver les modifications]** pour enregistrer la configuration de l’événement.

Vous devez ensuite ajouter une action à la règle que vous avez créée.

1. Dans le [!DNL Actions] , sélectionnez **[!UICONTROL Ajouter]**.
   ![Image affichant l’écran de modification des règles.](assets/web-in-app-messaging/add-action.png)

2. Utilisez ce qui suit : **[!UICONTROL Action]** settings :
   * **[!UICONTROL Extension]**: [!UICONTROL SDK Web Adobe Experience Platform]
   * **[!UICONTROL Type d’action]**: [!UICONTROL Envoyer un événement]

     ![Image affichant l’écran de configuration de l’action.](assets/web-in-app-messaging/action-configuration.png)

3. Dans la partie droite de l’écran, dans la **[!UICONTROL Personnalisation]** , activez la fonction **[!UICONTROL Rendu des décisions de personnalisation visuelle]** .
   ![Image montrant l&#39;écran de configuration de la personnalisation.](assets/web-in-app-messaging/render-visual-personalization.png)

4. Dans la partie droite de l’écran, dans la **[!UICONTROL Contexte de décision]** , définissez les **[!UICONTROL Clé]**/**[!UICONTROL Valeur]** des paires que vous avez utilisées dans la configuration de votre campagne pour remplir les critères du message in-app.
   ![Image montrant l&#39;écran de configuration de la personnalisation.](assets/web-in-app-messaging/decision-context.png)

5. Sélectionner **[!UICONTROL Conserver les modifications]** pour enregistrer votre configuration.


Vous devez ensuite ajouter la règle nouvellement créée à la bibliothèque de propriétés de balise. Pour ce faire, accédez à **[!UICONTROL Flux de publication]** et sélectionnez la règle que vous avez créée précédemment.

![Image affichant l’écran de la bibliothèque.](assets/web-in-app-messaging/add-rule-to-library.png)

Après avoir ajouté la règle à la bibliothèque, sélectionnez **[!UICONTROL Enregistrement et création pour le développement]**.

![Image montrant l&#39;écran de configuration de la personnalisation.](assets/web-in-app-messaging/publish-flow.png)

Le processus de configuration est maintenant terminé et votre message est prêt à être présenté à vos utilisateurs.

### Étapes de configuration pour l’utilisation de déclencheurs manuels {#manual-trigger}

Sélectionnez la propriété de balise qui contient votre extension SDK Web, et [créer une règle](../../tags/ui/managing-resources/rules.md##create-a-rule) avec les paramètres suivants :

1. **[!UICONTROL Extension]** : [!UICONTROL Core]
2. **[!UICONTROL Type d’événement]**: [!UICONTROL Cliquez sur]
3. Définissez le déclencheur d’un élément spécifique sur la page, l’identifiant par un sélecteur CSS de votre choix.

   ![Image montrant l’écran de configuration de l’événement.](assets/web-in-app-messaging/event-configuration-manual.png)


Vous devez ensuite ajouter une action à la règle que vous avez créée.

1. Dans le [!DNL Actions] , sélectionnez **[!UICONTROL Ajouter]**.
   ![Image affichant l’écran de modification des règles.](assets/web-in-app-messaging/add-action.png)

2. Utilisez ce qui suit : **[!UICONTROL Action]** settings :
   * **[!UICONTROL Extension]**: [!UICONTROL SDK Web Adobe Experience Platform]
   * **[!UICONTROL Type d’action]**: [!UICONTROL Évaluation des jeux de règles]

     ![Image affichant l’écran de configuration de l’action.](assets/web-in-app-messaging/manual-trigger-action.png)

3. Sur le côté droit de l’écran, activez l’option **[!UICONTROL Rendu des décisions de personnalisation visuelle]** .
   ![Image montrant l&#39;écran de configuration de la personnalisation.](assets/web-in-app-messaging/manual-trigger-render.png)


4. Dans la partie droite de l’écran, dans la **[!UICONTROL Contexte de décision]** , définissez les **[!UICONTROL Clé]**/**[!UICONTROL Valeur]** des paires que vous avez utilisées dans la configuration de votre campagne pour remplir les critères du message in-app.
   ![Image montrant l&#39;écran de configuration de la personnalisation.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. Sélectionner **[!UICONTROL Conserver les modifications]** pour enregistrer votre configuration.

Vous devez ensuite ajouter la règle nouvellement créée à la bibliothèque de propriétés de balise. Pour ce faire, accédez à **[!UICONTROL Flux de publication]** et sélectionnez la règle que vous avez créée précédemment.

![Image affichant l’écran de la bibliothèque.](assets/web-in-app-messaging/add-rule-to-library.png)

Après avoir ajouté la règle à la bibliothèque, sélectionnez **[!UICONTROL Enregistrement et création pour le développement]**.

![Image montrant l&#39;écran de configuration de la personnalisation.](assets/web-in-app-messaging/publish-flow.png)

Le processus de configuration est maintenant terminé et votre message est prêt à être présenté à vos utilisateurs.

## Configuration de la messagerie web in-app à l’aide de la bibliothèque JavaScript SDK web {#js-library}

Au lieu d’utiliser l’extension de balise du SDK Web, vous pouvez également configurer la messagerie web in-app directement à partir de la bibliothèque JavaScript du SDK Web.



Vous pouvez afficher les messages web in-app à partir de Adobe Journey Optimizer de deux manières.

### Méthode 1 : récupération automatique du contenu de personnalisation {#automatic}

Pour que le SDK Web récupère automatiquement le contenu de personnalisation au chargement de la page, utilisez la méthode `sendEvent` , comme illustré dans l’exemple ci-dessous.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### Méthode 2 : récupération manuelle du contenu de personnalisation selon l’action de l’utilisateur {#manual}

Pour afficher le contenu de personnalisation uniquement après l’exécution d’une action spécifique par l’utilisateur, utilisez la variable `evaluateRulesets` comme illustré dans l’exemple ci-dessous.

Dans cet exemple, le contenu de la personnalisation s&#39;affiche lorsqu&#39;un utilisateur clique sur le bouton **[!UICONTROL Acheter maintenant]** sur votre site web.

```js
 alloy("evaluateRulesets", {
     renderDecisions: true,
     personalization: {
         decisionContext: {
             "userAction": "buy_now"
         }
     }
 });
```

### Configuration du stockage de personnalisation {#personalization-storage}

Vous pouvez choisir d’afficher les messages in-app aux utilisateurs pour un nombre défini de fois, ou chaque fois qu’ils visitent une page, au moyen de la variable `personalizationStorageEnabled` l’option de configuration.

Dans le [Configuration du SDK Web](../fundamentals/configuring-the-sdk.md) définissez la variable `personalizationStorageEnabled` selon vos besoins :

* `personalizationStorageEnabled: true` déclenche le message in-app avec la fréquence que vous avez définie dans la variable [Campagne Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html#configure-inapp).
* `personalizationStorageEnabled: false` déclenche le message in-app à chaque chargement de page.