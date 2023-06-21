---
solution: Experience Platform
title: Commencer
description: Découvrez comment commencer à utiliser la fonctionnalité des cahiers de travail des cas d’utilisation .
badgeBeta: label="Beta" type="Informative"
source-git-commit: 297dc9d6252d401f805fa5ebb5cf5111910286cf
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# (Version bêta) Prise en main

>[!AVAILABILITY]
>
>Cette fonctionnalité est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

## Création d’un environnement de test de développement {#create-development-sandbox}

Pour commencer, accédez au [[!UICONTROL Cas d’utilisation des classeurs]](/help/use-case-playbooks/playbooks/overview.md) fonctionnalité, [créer un nouvel environnement de test de développement](/help/sandboxes/ui/user-guide.md#create) (assurez-vous de ne pas sélectionner d’environnement de test de production) avec le nom (et non le titre) contenant : `-ucp` ou `-UCP` dans le suffixe, comme illustré ci-dessous.

![Création d’un environnement de test de développement pour les classeurs de cas d’utilisation](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Vous devriez maintenant voir [!UICONTROL Livres] dans le rail de gauche, sous [!UICONTROL Cas d’utilisation des classeurs] ou sous [!UICONTROL Marketground].

![Cas d’utilisation des classeurs de cas d’utilisation dans l’interface utilisateur après la création d’un environnement de test.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Si vous ne voyez pas [!UICONTROL Livres] dans le rail de gauche comme illustré ci-dessus, utilisez ce lien. `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` pour y accéder directement. Dans le lien, `<YOUR_ORG>` est le nom de votre organisation et `<YOUR_SANDBOX_NAME>` est le nom de l’environnement de test de développement que vous avez créé.

### Configuration des environnements de test pour les utilisateurs Adobe Journey Optimizer {#sandbox-configuration-journey-optimizer}

Si votre entreprise détient une licence pour [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr), vous devez configurer les paramètres prédéfinis de canal dans votre environnement de test, qui définissent les paramètres techniques requis pour vos messages. [Découvrez comment configurer les surfaces de canal dans Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=fr).

## Accorder à votre équipe les autorisations d’accès requises {#grant-access-permissions}

Pour commencer à utiliser [!UICONTROL Cas d’utilisation des classeurs], les membres de votre équipe des opérations marketing ont besoin des autorisations appropriées. Vous pouvez accorder les autorisations suivantes à votre équipe :

* Les membres de l’équipe des opérations marketing qui ne souhaitent parcourir que les livres de jeu peuvent obtenir **read** autorisation.
* Les membres de l’équipe des opérations marketing qui souhaitent créer des instances à partir de classeurs peuvent obtenir **lecture et écriture** autorisations.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment commencer à utiliser [!UICONTROL Cas d’utilisation des classeurs]. Lisez ensuite comment [découvrez le bon playbook](/help/use-case-playbooks/playbooks/discover.md) pour vous et puis [créer des instances à partir de celle-ci](/help/use-case-playbooks/playbooks/create-share-reuse.md).
