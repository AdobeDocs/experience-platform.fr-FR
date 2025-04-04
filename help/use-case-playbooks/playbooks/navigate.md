---
solution: Experience Platform
title: Accéder aux playbooks de cas d’utilisation
description: Découvrez comment parcourir une galerie de playbooks et commencer à utiliser un sandbox inspirant.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# Accéder aux playbooks de cas d’utilisation

Les playbooks de cas d’utilisation sont disponibles gratuitement pour tous les clients Adobe Experience Platform. Pour accéder à une riche galerie de playbooks de cas d’utilisation dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Playbooks]** dans le volet de navigation de gauche.

![Galerie de playbooks de cas d’utilisation.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Accès direct aux playbooks de cas d’utilisation dans la barre de navigation de gauche.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Sélectionnez un playbook pour accéder à la page de détails, puis sélectionnez **[!UICONTROL Accéder à un sandbox source d’inspiration]**. Une boîte de dialogue modale de confirmation s’affiche. Sélectionnez **Confirmer** pour accéder au sandbox source d’inspiration où vous pouvez explorer et expérimenter les différents cas d’utilisation.

Si vous n’êtes pas autorisé à créer des sandbox, contactez votre administrateur pour obtenir de l’aide sur la création d’un sandbox source d’inspiration.

>[!TIP]
>
>Un sandbox source d’inspiration est un sandbox de développement dans Adobe Experience Platform où vous pouvez créer, tester et tester différents cas d’utilisation avant de les implémenter dans un environnement de production en direct.

![Accédez à la sandbox source d’inspiration.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Si vous n’avez pas encore configuré de sandbox d’inspiration, sélectionnez **[!UICONTROL Créer un sandbox d’inspiration]**. Une boîte de dialogue modale s’affiche. Saisissez les **Nom** et **Titre** dans les champs obligatoires et sélectionnez **Créer**. Une fois que vous avez créé le sandbox d’inspiration, veillez à [définir des autorisations](/help/access-control/home.md) avant de revenir à la page des détails des playbooks de cas d’utilisation pour créer une instance.

![Créez un sandbox inspirant.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Saisissez un nom et un titre pour créer un sandbox inspirant.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Si vous sélectionnez un playbook de cas d’utilisation en dehors d’un sandbox source d’inspiration, vous ne pourrez pas créer d’instance. Sur la page de détails, sélectionnez **Accéder au sandbox d’inspiration** pour accéder à un sandbox d’inspiration existant, puis sélectionnez **[!UICONTROL Créer une instance]**.

Si vous n’êtes pas autorisé à créer des sandbox, contactez votre administrateur pour obtenir de l’aide sur la création d’un sandbox source d’inspiration.

![Aucune autorisation pour créer un sandbox.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Si vous avez atteint la limite du nombre de sandbox qui vous ont été attribués, un message s’affiche vous demandant de contacter l’administrateur de votre organisation pour augmenter la limite ou désactiver ou supprimer certains sandbox actifs. Une fois votre limite de sandbox ajustée ou votre nombre de sandbox actifs réduit, vous pouvez commencer à créer la sandbox source d’inspiration.

![Limite du sandbox atteinte.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Notez que lorsque vous créez un sandbox source d’inspiration, les surfaces de canal pour les notifications par e-mail, push et SMS ne sont pas automatiquement configurées. Contactez votre administrateur informatique pour les configurer manuellement ou la création de l’instance peut échouer.

![Configuration des préréglages de canal.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Configuration des surfaces de canal et de sandbox dans Journey Optimizer {#configure-channel-surfaces}

Si votre organisation dispose d’une licence pour [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr) et que vous souhaitez utiliser les playbooks conçus pour Journey Optimizer, vous devez configurer les préréglages de canal dans votre sandbox, qui définissent les paramètres techniques requis pour vos messages. [Découvrez comment configurer les surfaces de canal dans Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=fr).

Pour créer des instances de playbooks dans Journey Optimizer, vous devez configurer les surfaces des canaux pour les notifications par e-mail, push et SMS.

### Surface du canal e-mail

Accédez à `Channels` dans l’interface de Journey Optimizer. Configurez des sous-domaines et des pools d&#39;adresses IP distincts pour les e-mails marketing et les messages transactionnels, s&#39;ils ne sont pas déjà configurés. Il s’agit des bonnes pratiques pour s’assurer que les messages transactionnels tels que les e-mails de confirmation de commande, parviennent à vos clients. Saisissez les noms, adresses e-mail et paramètres supplémentaires. Sélectionnez **Envoyer** en haut à droite de la page pour créer la surface du canal marketing. Lisez la documentation sur [comment configurer des surfaces de canal e-mail](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Surface du canal SMS

Pour créer une surface de canal SMS, commencez par créer des informations d’identification d’API SMS, puis sélectionnez le fournisseur préféré (par exemple, Sinch). Nommez la surface de canal SMS (par exemple, Marketing SMS), sélectionnez la configuration, puis saisissez un numéro d’expéditeur. Sélectionnez **Envoyer** en haut à droite de la page pour enregistrer la surface du canal SMS. Lisez la documentation sur [comment configurer des surfaces de canal SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=fr#message-preset-sms).

Configurez également des canaux pour les playbooks contenant des messages transactionnels tels que les confirmations de commande.

### Surface du canal push

Vérifiez que les configurations de canal sont configurées à partir de l’interface d’Experience Platform ou de Collections de données. Voici à quoi ressemblent les configurations de canal dans l’environnement Collections de données.

## Étapes suivantes {#next-steps}

Maintenant que vous avez lu ce document, vous devriez savoir comment configurer un sandbox inspirant et vous familiariser avec les différentes manières d’accéder aux playbooks de cas d’utilisation dans Experience Platform. L’étape suivante consiste à découvrir comment [choisir](/help/use-case-playbooks/playbooks/choose.md) le bon playbook.
