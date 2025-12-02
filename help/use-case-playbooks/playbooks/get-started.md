---
solution: Experience Platform
title: Prise en main des playbooks de cas d’utilisation
description: Commencez à utiliser la fonctionnalité des Playbooks de cas d’utilisation.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: d6b62b9539a04be2d2adc7aa66436a294e08303a
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 8%

---


# Commencer

Découvrez comment configurer votre compte pour les playbooks de cas d’utilisation, conçus pour Real-Time Customer Data Platform et Adobe Journey Optimizer, s’ils ne sont pas configurés automatiquement. Les trois principales étapes de configuration sont les suivantes :

* Créer un sandbox
* Configurer les autorisations des utilisateurs et des utilisatrices
* Configurer des surfaces de canal Journey Optimizer pour les notifications par e-mail, push et SMS (si vous envisagez d’utiliser des playbooks Journey Optimizer)

Pour accéder à une riche galerie de playbooks de cas d’utilisation dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Playbooks]** dans le volet de navigation de gauche. Lisez la documentation sur la façon de [parcourir les playbooks de cas d’utilisation](../playbooks/navigate.md) et de commencer à utiliser un [sandbox inspirant](../playbooks/navigate.md).

## Configuration des playbooks de cas d’utilisation - Présentation vidéo {#video}

Regardez cette vidéo pour en savoir plus sur les étapes nécessaires à la création de votre sandbox, à la configuration des autorisations et à la configuration des surfaces de canal pour les notifications par e-mail, push et SMS dans Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Créer une sandbox de développement {#create-development-sandbox}

Les playbooks de cas d’utilisation utilisent un type spécial de sandbox de développement. Pour commencer et accéder à la fonctionnalité de [[!UICONTROL Use Case Playbooks]](/help/use-case-playbooks/playbooks/overview.md), [créez un nouveau sandbox de développement](/help/sandboxes/ui/user-guide.md#create) (veillez à ne pas sélectionner de sandbox de production) dont le nom (et non le titre) contient `-ucp` ou `-UCP` comme illustré ci-dessous.

>[!IMPORTANT]
>
>Lorsque vous créez un nouveau sandbox de développement, assurez-vous que le nom contient `-ucp` ou `-UCP` dans le suffixe .


![Créer une sandbox de développement pour les playbooks de cas d’utilisation](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Vous devriez maintenant voir [!UICONTROL Playbooks] dans le rail de gauche sous [!UICONTROL Use Case Playbooks].

![Playbooks de cas d’utilisation dans l’interface utilisateur après la création d’une sandbox.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Si vous ne voyez pas [!UICONTROL Playbooks] dans le rail de gauche, comme illustré ci-dessus, utilisez ce `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` de lien pour y accéder directement. Le lien contient le nom de votre organisation (`<YOUR_ORG>`) et le nom de la sandbox de développement que vous avez créée (`<YOUR_SANDBOX_NAME>`).

## Accorder à votre équipe les autorisations d’accès requises {#grant-access-permissions}

Pour commencer à utiliser [!UICONTROL Use Case Playbooks], les membres de votre équipe marketing doivent disposer des autorisations appropriées afin de pouvoir afficher la liste des playbooks créés ou en créer eux-mêmes.

**Autorisations requises**

Pour ajouter les autorisations requises, dans l’interface utilisateur Autorisations, incluez le nouveau sandbox de playbook de cas d’utilisation dans [rôles que vous avez déjà configurés](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), y compris ceux utilisés pour d’autres sandbox de développement.

![Sandbox des playbooks pour les rôles déjà configurés](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Configurer un rôle pour les playbooks :**

Vous pouvez également envisager d’ajouter de nouveaux rôles avec [les autorisations requises](/help/access-control/home.md#sandboxes-and-permissions).

[Configurez un nouveau rôle](/help/access-control/abac/ui/permissions.md) avec les autorisations nécessaires pour les tâches essentielles du playbook. Créez un rôle et ajoutez-y le nouveau sandbox, comme illustré ci-dessous.

![Créer un rôle et l’ajouter au sandbox](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Autorisations pour les instances de playbook**

Dans le cadre des playbooks de cas d’utilisation, vous allez créer différentes ressources telles que des schémas, des audiences, des destinations, des parcours. Vous et d’autres utilisateurs aurez besoin des autorisations appropriées pour créer ces objets.

**Autorisations pour les schémas**

Pour créer et gérer des schémas, utilisez les autorisations de modélisation des données : **[!UICONTROL Manage Schemas]**, **[!UICONTROL View Schemas]**, **[!UICONTROL Manage Relationships]**, **[!UICONTROL Manage Identity Metadata]**

**Autorisations pour les destinations**

Pour créer et gérer des destinations, utilisez les autorisations de Destinations : **[!UICONTROL Manage]**, **[!UICONTROL Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL Manage and Activate Dataset Destination]**, **[!UICONTROL Destination Authoring]**.

**Autorisations pour parcours**

Pour créer et gérer des parcours, utilisez les autorisations des Parcours : **[!UICONTROL Manage Journeys]**, **[!UICONTROL View Journeys]**, **[!UICONTROL View Journeys Report]**, **[!UICONTROL Manage Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions]**, **[!UICONTROL View Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions, Publish Journeys]**.

L’image ci-dessous présente un instantané des autorisations recommandées pour que les utilisateurs puissent afficher, créer et gérer des playbooks et les ressources générées par les playbooks.

![Instantané de tous les éléments d’autorisation nécessaires pour créer toutes les instances des playbooks](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Ajouter des utilisateurs au rôle**

Une fois que vous avez [créé un nouveau rôle](/help/access-control/abac/ui/permissions.md#managing-users-for-role) comme indiqué ci-dessus, ajoutez-vous en tant qu’utilisateur. Si vous créez un rôle avec un accès limité pour un autre ensemble d’utilisateurs ayant un accès en lecture seule, incluez uniquement les éléments d’affichage nécessaires associés à ces autorisations.

## Configuration des surfaces de canal et de sandbox dans Journey Optimizer {#configure-channel-surfaces}

Si votre organisation dispose d’une licence pour [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/ajo-home) et que vous souhaitez utiliser les playbooks conçus pour Journey Optimizer, configurez les surfaces de canal dans votre sandbox. Les surfaces de canal définissent tous les paramètres techniques requis pour vos messages, tels que le type d’e-mail, le nom et l’adresse e-mail de l’expéditeur, les applications mobiles, la configuration des SMS, etc. [Découvrez comment configurer les surfaces de canal dans Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces).

Pour créer des instances de playbooks dans Journey Optimizer, vous devez configurer les surfaces des canaux pour les notifications par e-mail, push et SMS.

### Surface du canal e-mail

Accédez à `Channels` dans l’interface de Journey Optimizer. Configurez des sous-domaines et des pools d&#39;adresses IP distincts pour les e-mails marketing et les messages transactionnels, s&#39;ils ne sont pas déjà configurés. Il s’agit des bonnes pratiques pour s’assurer que les messages transactionnels tels que les e-mails de confirmation de commande, parviennent à vos clients. Saisissez les noms, adresses e-mail et paramètres supplémentaires. Sélectionnez **Envoyer** en haut à droite de la page pour créer la surface du canal marketing. Lisez la documentation sur [comment configurer des surfaces de canal e-mail](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Surface du canal SMS

Pour créer une surface de canal SMS, commencez par créer des informations d’identification d’API SMS, puis sélectionnez le fournisseur préféré (par exemple, Sinch). Nommez la surface de canal SMS (par exemple, Marketing SMS), sélectionnez la configuration, puis saisissez un numéro d’expéditeur. Sélectionnez **Envoyer** en haut à droite de la page pour enregistrer la surface du canal SMS. Lisez la documentation sur [comment configurer des surfaces de canal SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=fr#message-preset-sms).

Configurez également des canaux pour les playbooks contenant des messages transactionnels tels que les confirmations de commande.

### Surface du canal push

Vérifiez que les configurations de canal sont configurées à partir de l’interface d’Experience Platform ou de Collections de données. Voici à quoi ressemblent les configurations de canal dans l’environnement Collections de données.

<!-- ![Channel configurations in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Sélectionnez ensuite le canal, les plateformes et les applications que vous avez examinés dans les configurations de canal. Sélectionnez **Envoyer** pour créer la surface de canal push.

Lisez la documentation sur [comment configurer des surfaces de canal push](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Étapes suivantes {#next-steps}

Maintenant que vous avez suivi toutes les étapes de ce document, vous devriez avoir créé un sandbox de développement avec des playbooks de cas d’utilisation disponibles dans le volet de navigation de gauche. Vous savez également comment accorder aux membres de votre équipe les autorisations requises pour afficher et gérer les playbooks et générer des ressources. L’étape suivante consiste à lire comment [choisir le playbook approprié](/help/use-case-playbooks/playbooks/choose.md) puis [&#x200B; créer des instances à partir de celui-ci](/help/use-case-playbooks/playbooks/create-share-reuse.md).
