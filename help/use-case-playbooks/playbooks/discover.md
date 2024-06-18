---
solution: Experience Platform
title: Découvrir des livres de lecture
description: Découvrez comment découvrir une galerie de playbooks et commencer avec un environnement de test inspirant.
role: User
source-git-commit: ad3f746580f85e77cba390208d147b35b6854e10
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 2%

---

# Découvrir des livres de lecture

Les classeurs de cas d’utilisation sont disponibles sans frais supplémentaires pour tous les clients Adobe Experience Platform. Pour accéder à une riche galerie de classeurs de cas d’utilisation dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Livres]** dans le volet de navigation de gauche.

![Cas d’utilisation de la galerie de livres de lecture.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Accès direct aux classeurs de cas d’utilisation dans la barre de navigation de gauche.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Sélectionnez un playbook pour accéder à la page des détails, puis sélectionnez **[!UICONTROL Accédez à un environnement de test inspirant.]**. Un modal de confirmation s’affiche. Sélectionner **Confirmer** pour accéder à l’environnement de test inspirant où vous pouvez explorer et tester les différents cas d’utilisation.

Si vous ne disposez pas des autorisations nécessaires pour créer des environnements de test, contactez votre administrateur pour obtenir de l’aide sur la création d’un environnement de test inspirant.

>[!TIP]
>
>Un environnement de test inspirant est un environnement de test de développement dans Adobe Experience Platform où vous pouvez créer, tester et expérimenter différents cas d’utilisation avant de les mettre en oeuvre dans un environnement de production actif.

![Accédez à un environnement de test inspirant.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Si vous n’avez déjà configuré aucun environnement de test inspirant, sélectionnez **[!UICONTROL Créer un environnement de test inspirant]**. Un modal s’affiche. Saisissez le **Nom** et **Titre** dans les zones de champ requises, puis sélectionnez **Créer**. Une fois que vous avez créé l’environnement de test d’inspiration, veillez à [définir des autorisations](/help/access-control/home.md) avant de revenir à la page détails du cas d’utilisation playbooks pour créer une instance.

![Créez un environnement de test inspirant.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Saisissez le nom et le titre pour créer un environnement de test inspirant.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Si vous sélectionnez un scénario d’utilisation en dehors d’un environnement de test inspirant, vous ne pourrez pas créer d’instance. Sur la page Détails, sélectionnez **Accédez à un environnement de test inspirant.** pour accéder à un environnement de test d’inspiration existant, puis sélectionnez **[!UICONTROL Créer une instance]**.

Si vous ne disposez pas des autorisations nécessaires pour créer des environnements de test, contactez votre administrateur pour obtenir de l’aide sur la création d’un environnement de test inspirant.

![Aucune autorisation pour créer un environnement de test.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Si vous avez atteint la limite du nombre d’environnements de test qui vous ont été attribués, un message s’affiche vous demandant de contacter l’administrateur de votre organisation pour augmenter la limite, désactiver ou supprimer certains environnements de test actifs. Une fois votre limite d’environnements de test ajustée ou votre nombre d’environnements de test actifs réduit, vous pouvez créer l’environnement de test inspirant.

![Limite des environnements de test atteinte.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Notez que lorsque vous créez un environnement de test d’inspiration, les surfaces des canaux pour les e-mails, les notifications push et SMS ne sont pas automatiquement configurées. Contactez votre administrateur informatique pour les configurer manuellement ou la création de l’instance peut échouer.

![Configurez les paramètres prédéfinis de canal.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Configuration des environnements de test et des surfaces de canal dans Journey Optimizer {#configure-channel-surfaces}

Si votre entreprise détient une licence pour [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr)et que vous souhaitez utiliser les playbooks conçus pour Journey Optimizer, vous devez configurer les paramètres prédéfinis de canal dans votre environnement de test, qui définissent les paramètres techniques requis pour vos messages. [Découvrez comment configurer les surfaces de canal dans Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=fr).

Pour créer des instances de playbooks dans Journey Optimizer, vous devez configurer les surfaces des canaux pour les notifications par e-mail, push et SMS.

### Surface du canal email

Accédez à `Channels` dans l’interface de Journey Optimizer. Configurez des sous-domaines et des pools d’adresses IP distincts pour les emails marketing et les messages transactionnels, s’ils ne sont pas déjà configurés. Il s’agit des bonnes pratiques pour s’assurer que les messages transactionnels, tels que les courriers électroniques de confirmation de commande, parviennent à vos clients. Entrez les noms, les adresses électroniques et les paramètres supplémentaires. Sélectionner **Envoyer** dans le coin supérieur droit de la page pour créer la surface du canal marketing. Lisez la documentation sur [comment configurer les surfaces de canal de courrier électronique](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Surface du canal SMS

Pour créer une surface de canal SMS, créez d’abord des informations d’identification d’API SMS, puis sélectionnez le fournisseur de votre choix (par exemple, Sinch). Nommez la surface du canal SMS (par exemple, SMS Marketing), sélectionnez la configuration et saisissez un numéro d&#39;expéditeur. Sélectionner **Envoyer** en haut à droite de la page pour enregistrer la surface du canal SMS. Lisez la documentation sur [comment configurer les surfaces de canal SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=fr#message-preset-sms).

Configurez également les canaux des livres de lecture qui contiennent des messages transactionnels, tels que les confirmations de commande.

### Surface du canal push

Vérifiez que les surfaces de l’application sont configurées à partir de l’Experience Platform ou de l’interface Collections de données. Voici à quoi ressemblent les surfaces d’application dans l’environnement Collections de données.

## Étapes suivantes {#next-steps}

Maintenant que vous avez lu ce document, vous devez savoir comment configurer un environnement de test inspirant et vous familiariser avec différentes façons d’accéder aux playbooks de cas d’utilisation dans Platform. À l’étape suivante, découvrez comment [find](/help/use-case-playbooks/playbooks/find.md) le bon playbook.

