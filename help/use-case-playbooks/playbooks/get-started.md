---
solution: Experience Platform
title: Prise en main des livres de cas d’utilisation
description: Commencez à utiliser la fonctionnalité des Playbooks de cas d’utilisation.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: dfb4549a09628f2fed947ddf76167db28354eb92
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 15%

---


# Commencer

Découvrez comment configurer votre compte pour les classeurs de cas d’utilisation, conçus pour Real-time Customer Data Platform et Adobe Journey Optimizer s’il n’est pas configuré automatiquement. Les trois principales étapes de configuration sont les suivantes :

* Créer un sandbox
* Configurer les autorisations des utilisateurs et des utilisatrices
* Configuration des surfaces des canaux Journey Optimizer pour les notifications par e-mail, push et SMS (si vous envisagez d’utiliser des playbooks Journey Optimizer)

## Configuration des classeurs de cas d’utilisation - Présentation vidéo {#video}

Regardez cette vidéo pour en savoir plus sur les étapes nécessaires à la création de votre environnement de test, à la configuration des autorisations et à la configuration des surfaces des canaux pour les notifications par e-mail, push et SMS dans Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Créer une sandbox de développement {#create-development-sandbox}

Les classeurs de cas d’utilisation utilisent un type spécial d’environnement de test de développement. Pour commencer à utiliser la fonctionnalité des [[!UICONTROL Playbooks de cas d’utilisation]](/help/use-case-playbooks/playbooks/overview.md), [créez une sandbox de développement](/help/sandboxes/ui/user-guide.md#create) (assurez-vous de ne pas sélectionner de sandbox de production) et indiquez dans le suffixe du nom (et non du titre) `-ucp` ou `-UCP`, comme illustré ci-dessous.

>[!IMPORTANT]
>
>Lorsque vous créez un environnement de test de développement, assurez-vous que le nom contient `-ucp` ou `-UCP` dans le suffixe.


![Créer une sandbox de développement pour les playbooks de cas d’utilisation](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Vous devriez maintenant voir [!UICONTROL Livres] dans le rail de gauche, sous [!UICONTROL Cas d’utilisation des classeurs].

![Playbooks de cas d’utilisation dans l’interface utilisateur après la création d’une sandbox.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Si les [!UICONTROL Playbooks] ne s’affichent pas dans le rail de gauche comme illustré ci-dessus, suivez le lien `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` pour y accéder directement. Le lien contient le nom de votre organisation (`<YOUR_ORG>`) et le nom de la sandbox de développement que vous avez créée (`<YOUR_SANDBOX_NAME>`).

## Accorder à votre équipe les autorisations d’accès requises {#grant-access-permissions}

Pour commencer à utiliser [!UICONTROL Cas d’utilisation des classeurs], les membres de votre équipe marketing ont besoin des autorisations appropriées pour pouvoir afficher la liste des playbooks créés ou créer eux-mêmes des playbooks.

**Autorisations requises**

Pour ajouter les autorisations requises, dans l’interface utilisateur Autorisations, ajoutez le nouvel environnement de test du scénario d’utilisation à la section [rôles que vous avez déjà configurés](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), y compris ceux utilisés pour d’autres environnements de test de développement.

![Environnement de test du manuel pour les rôles déjà configurés](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Configurez un rôle pour les livres de lecture :**

Vous pouvez également envisager d’ajouter de nouveaux rôles avec [les autorisations requises](/help/access-control/home.md#sandboxes-and-permissions).

[Configurer un nouveau rôle](/help/access-control/abac/ui/permissions.md) avec les autorisations nécessaires pour les tâches essentielles du playbook. Créez un rôle et ajoutez-y le nouvel environnement de test, comme illustré ci-dessous.

![Création d’un rôle et son ajout à l’environnement de test](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Autorisations pour les instances playbook**

Dans le cadre des cahiers de travail des cas d’utilisation, vous allez créer diverses ressources telles que des schémas, des audiences, des destinations, des parcours. Vous et les autres utilisateurs aurez besoin des autorisations appropriées pour créer ces objets.

**Autorisations pour les schémas**

Pour créer et gérer des schémas, utilisez les autorisations de modélisation des données ; **[!UICONTROL Gestion des schémas]**, **[!UICONTROL Affichage des schémas]**, **[!UICONTROL Gestion des relations]**, **[!UICONTROL Gestion des métadonnées d’identité]**

**Autorisations pour les destinations**

Pour créer et gérer des destinations, utilisez les autorisations de destinations ; **[!UICONTROL Gérer]**, **[!UICONTROL Destinations]**, **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Activation du segment sans mappage]**, **[!UICONTROL Gestion et activation de la destination du jeu de données]**, **[!UICONTROL Création de destination]**.

**Autorisations pour les parcours**

Pour créer et gérer des parcours, utilisez les autorisations Parcours ; **[!UICONTROL Gestion des Parcours]**, **[!UICONTROL Affichage des Parcours]**, **[!UICONTROL Afficher le rapport Parcours]**, **[!UICONTROL Gestion des Parcours]**, **[!UICONTROL Événements]**, **[!UICONTROL Sources de données et actions]**, **[!UICONTROL Affichage des Parcours]**, **[!UICONTROL Événements]**, **[!UICONTROL Sources de données et actions, Parcours de publication]**.

L’image ci-dessous présente un instantané des autorisations recommandées pour les utilisateurs afin d’afficher, de créer et de gérer les livres de lecture et les ressources générées par les livres de lecture.

![Instantané de tous les éléments d’autorisation nécessaires pour créer toutes les instances des livres de lecture](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Ajout d’utilisateurs au rôle**

Une fois que vous [création d’un nouveau rôle](/help/access-control/abac/ui/permissions.md#managing-users-for-role) comme mentionné ci-dessus, ajoutez-vous en tant qu’utilisateur. Si vous créez un rôle avec un accès limité pour un autre ensemble d’utilisateurs disposant d’un accès en lecture seule, incluez uniquement les éléments de vue nécessaires associés à ces autorisations.

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

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Sélectionnez ensuite le canal, les plateformes et les applications que vous avez étudiés dans les configurations de surface de l’application. Sélectionner **Envoyer** pour créer la surface du canal push.

Lisez la documentation sur [comment configurer les surfaces de canal push](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Étapes suivantes {#next-steps}

Maintenant que vous avez suivi toutes les étapes de ce document, vous devez avoir créé un environnement de test de développement avec des classeurs de cas d’utilisation disponibles dans le volet de navigation de gauche. Vous savez également comment octroyer aux membres de votre équipe les autorisations requises pour afficher et gérer des livres de jeu et générer des ressources. À l’étape suivante, lisez la section [découvrez le bon playbook](/help/use-case-playbooks/playbooks/discover.md) pour vous et puis [créer des instances à partir de celle-ci](/help/use-case-playbooks/playbooks/create-share-reuse.md).
