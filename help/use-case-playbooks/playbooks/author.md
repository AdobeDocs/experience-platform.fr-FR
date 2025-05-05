---
solution: Experience Platform
title: Découvrez comment créer et partager vos propres playbooks à l’aide de l’assistant d’IA.
description: Comment créer et partager vos propres playbooks de cas d’utilisation.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 5cdbc160369a146da3ae8ca39d8c3095887e03b5
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 0%

---


# Créer et partager vos propres playbooks (Beta)

Le [!DNL Playbook Authoring Framework], optimisé par l’assistant AI dans Adobe Experience Platform, vous permet de créer, gérer et partager des playbooks efficacement dans Adobe Experience Platform.

Le cadre suit un processus en trois étapes :

1. **Capture des métadonnées** : utilisez l’assistant AI ou le formulaire web pour capturer les métadonnées du playbook.

2. **Association technique** : ajoutez des ressources techniques spécifiques telles que des parcours ou des audiences au playbook. Vous conservez un contrôle total sur le processus de création des playbooks dans votre sandbox de développement, en veillant à l’alignement avec vos schémas et autres structures de données uniques.

3. **Distribution des playbooks** : partagez des playbooks dans différentes organisations. Par exemple, le Centre d&#39;excellence Martech d&#39;ACME en Allemagne peut créer un manuel « doré » et le distribuer à des organisations régionales en Thaïlande, en Australie, etc. pour normaliser le cas d’utilisation marketing.

## Créer un playbook

Vous pouvez créer un playbook de deux manières : en utilisant l’assistant d’IA ou manuellement. Lisez les sections suivantes pour savoir comment créer un playbook avec l’assistant AI.

### Présentation du playbook

Pour créer un playbook avec l’assistant d’IA, procédez comme suit :

Dans le panneau de navigation de gauche, sélectionnez **[!UICONTROL Playbooks]**.

![Interface utilisateur de Platform avec l’option « Playbooks » mise en surbrillance dans le panneau de navigation de gauche.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Sélectionnez **[!UICONTROL Nouveau playbook]**, puis sélectionnez **Générer le playbook avec l’assistant d’IA**.

![ L’interface de création du playbook affichant l’option « Générer le playbook avec l’assistant AI » sélectionnée.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Utilisez le champ d’invite pour décrire le cas d’utilisation. Par exemple :

« Contactez les clients ACME qui ont parcouru les chaussures de course mais n’ont pas effectué l’achat. »

![Interface de création du playbook mettant en surbrillance la zone de formulaire web dans laquelle les utilisateurs peuvent saisir une invite.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Sélectionnez **[!UICONTROL Générer]** pour créer les métadonnées du playbook.

![Interface de création du playbook affichant le bouton « Générer » en surbrillance dans la zone de l’invite.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Une fois générée, sélectionnez **[!UICONTROL Modifier]** pour modifier le titre, la description et les métadonnées générés, si nécessaire.

![Un playbook généré avec le bouton « Modifier » mis en surbrillance, permettant aux utilisateurs et aux utilisatrices de modifier les métadonnées.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Pour vous assurer que les ingénieurs de données disposent de tous les détails nécessaires pour configurer le cas d’utilisation, renseignez la section **[!UICONTROL Détails du playbook]**. Bien que facultatifs, ces champs permettent de capturer des informations clés, ce qui facilite la connexion des composants techniques appropriés. Sélectionnez **[!UICONTROL Modifier]** pour ajouter des valeurs aux champs suivants :

* **Industrie**
* **Audience cible**
* **Canal marketing**

![La section des détails du playbook avec le bouton « Modifier » mis en surbrillance afin que vous puissiez ajouter ou modifier des détails tels que le secteur, l’audience cible et le canal marketing.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Une fois les métadonnées générées, sélectionnez **[!UICONTROL Modifier la carte de parcours]** pour ajuster les étapes de la carte de parcours selon les besoins.

![ Le bouton « Modifier la carte de parcours » pour modifier les étapes de la carte de parcours ](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Interface de l’éditeur de carte de parcours permettant d’ajuster les étapes après avoir capturé les métadonnées du playbook.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Ensuite, passez à l’association du playbook avec les ressources techniques. Pour créer un playbook manuellement, sélectionnez **[!UICONTROL Créer un playbook manuellement]**.

![L’option « Créer manuellement un playbook » pour démarrer un playbook à partir d’un modèle vierge.](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Un modèle de playbook vierge s’affiche. Renseignez des détails tels que **Titre** et **Description**. Vous pouvez également modifier la carte du parcours pour ajouter des événements et des points de contact si nécessaire.

## Associer un playbook à des ressources techniques

Que vous créiez un playbook manuellement ou avec l’assistant d’IA, vous devez l’associer aux ressources techniques requises. Accédez à l’onglet **[!UICONTROL Technical Assets]** et sélectionnez le produit souhaité. Pour cet exemple, sélectionnez **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> La prise en charge de Real-Time CDP sera ajoutée dans une version ultérieure.

![Onglet « Assets technique » avec le bouton « Ajouter le produit requis » mis en surbrillance et que vous pouvez utiliser pour associer des ressources techniques au playbook.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Sélectionnez **[!UICONTROL Sélectionner une ressource]** pour associer ce playbook à un parcours, comme illustré dans l’image ci-dessous. Sélectionnez ensuite **Publier le playbook** pour finaliser le playbook.

![Onglet « Assets technique » avec le bouton « Sélectionner les ressources » mis en surbrillance que vous pouvez utiliser pour associer un parcours au playbook.](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Sélectionnez un parcours pour l’associer à un playbook.](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Une fois publié, le playbook extrait et associe automatiquement le schéma du parcours et les détails de l’audience.

![Un playbook publié présentant les métadonnées et les ressources techniques associées.](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Tous les playbooks créés sont disponibles dans l’onglet **Vos playbooks**.

![’onglet « Vos playbooks » affiche une liste des playbooks créés.](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

Vous pouvez sélectionner n’importe quel playbook du catalogue pour créer des instances à réutiliser. Reportez-vous à la documentation pour [savoir comment créer des instances](/help/use-case-playbooks/playbooks/create-share-reuse.md).

![Onglet « Présentation du playbook » avec l’option « Créer une instance » mise en surbrillance.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Une fois qu’un playbook est publié, il ne peut pas être modifié. Pour apporter des modifications, supprimez le playbook et recommencez.

## Exemples d’invites

L’assistant AI peut traiter diverses structures d’invite et extraire des détails clés tout en filtrant les informations inutiles. Vous trouverez ci-dessous quelques exemples d’invites utilisateur et comment le système les interprète.

**Exemple 1 :**

« Créez une campagne intitulée « Achevez l’apparence » afin d’augmenter les ventes et la valeur vie client. La campagne encourage les clients à acheter des ustensiles de cuisine ou des meubles à effectuer un achat complémentaire au moyen de recommandations et d’offres personnalisées liées à leur achat. Envoyez d’abord des recommandations de produits aux clients. S’ils n’effectuent aucun achat dans les 7 jours, ils reçoivent un second message contenant des recommandations et des offres de produits. Utilisez les notifications push et les e-mails pour contacter les clients. Ciblez les clients qui ont effectué un achat au cours des 7 derniers jours dans la catégorie des ustensiles de cuisine ou des meubles et qui n’ont pas été ciblés au cours des 30 derniers jours. Dans le cadre de la campagne, nous voulons mesurer les KPI tels que les clics (e-mail, application, sms, notification push), le CTR, le CTR du portefeuille électronique, le chiffre d’affaires AOV Conversion.CLV, le total des événements d’achat (en magasin, numérique, centre d’appels). »

![Exemple d’invite longue saisie dans la zone de saisie de texte pour générer un playbook.](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**Exemple 2 :**

« Nom du projet : Newsletter mode
Contexte : (proactif ou résolution de problèmes) : parcours conçu pour envoyer des newsletters de mode aux clients ACME abonnés à la newsletter.
Objectif : envoyer des e-mails de newsletter sur la mode aux clients ACME abonnés à la communication.
Détails promotionnels : le client reçoit des informations sur la mode dans le canal e-mail chaque semaine. L’e-mail doit être personnalisé et les variations de contenu doivent être basées sur le sexe, la langue et le marché.
Canaux/points de contact du projet : e-mail
Public cible : clients et clientes qui se sont abonnés aux communications de la newsletter ACME Fashion.
KPI/mesures d’engagement/ROI cibles : 1. Augmentez le chiffre d’affaires des produits . 2. Encouragez la fidélisation de la clientèle. »

![Exemple d’invite organisée de type liste saisie dans la zone de saisie de texte pour générer un playbook.](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**Exemple 3 :**

« Incitez les acheteurs à acheter des produits au cours d’une campagne promotionnelle continue.
Interagissez avec les acheteurs lors d’une promotion en cours en envoyant une communication appropriée par e-mail, SMS ou notifications push pour acheter des produits. Envoyez-lui un e-mail de rappel après 24 heures indiquant qu’il ne participe pas à la promotion. »

![Exemple d’invite concise saisie dans la zone de saisie de texte pour générer un playbook.](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**Exemple 4 :**

« Vendre des chaussures aux lycéens. »

![Exemple d’invite d’une seule ligne saisie dans la zone de saisie de texte pour générer un playbook.](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

L’assistant AI supprime tous les détails inutiles tels que « Nom du projet » ou « Arrière-plan ». Il extrait les éléments clés tels que « audience cible », « objectif de la campagne » et « canal marketing » et fonctionne avec n’importe quel style d’entrée.

Ces exemples montrent comment l’IA peut affiner et extraire des détails essentiels des invites utilisateur.

>[!NOTE]
>
> Évitez les PII ou les mots explicites lors de la rédaction de vos invites.

## Instructions relatives au contenu et modération

Lors de la création de playbooks, tenez compte de la langue et du contenu que vous incluez. Les playbooks sont visibles dans l’ensemble de votre organisation, ainsi que tout contenu offensant ou inapproprié signalé par les utilisateurs et utilisatrices.

### Marquage et processus de révision

Si un playbook contient du contenu inapproprié ou offensant, Adobe reçoit automatiquement un rapport à des fins de révision. Adobe examine le contenu avec indicateur, avertit le client s’il le juge inapproprié et supprime le playbook.

## Partage de playbooks dans les sandbox {#share-playbooks-sandboxes}

Lorsque vous créez et publiez un playbook dans un sandbox, il est automatiquement disponible dans tous les sandbox de votre organisation. Cette fonctionnalité élimine le besoin de partage manuel et vous permet de créer facilement des instances du playbook dans n’importe quel autre sandbox.

>[!TIP]
>
>Si le playbook référence des champs qui ne sont pas disponibles dans le schéma d’union du sandbox cible ou si vous ne disposez pas des autorisations nécessaires, un message d’erreur s’affiche lorsque vous essayez de créer l’instance. Le message indique les champs manquants et/ou les autorisations.

Si des champs sont manquants dans votre schéma d’union, une boîte de dialogue les met en surbrillance lors de l’importation.

![Boîte de dialogue répertoriant les champs manquants dans le schéma d’union lors du processus d’importation du playbook.](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## Partage de vos playbooks dans toutes les organisations {#sharing-playbooks-organizations}

Le partage de playbooks entre les organisations permet d’assurer la cohérence et l’efficacité lorsque plusieurs équipes doivent suivre les mêmes bonnes pratiques. Pour partager un playbook d’une organisation à une autre, procédez comme suit :

1. **Connectez-vous à l’organisation source** : accédez à l’organisation qui contient le playbook que vous avez créé et que vous souhaitez partager à partir de l’onglet **[!UICONTROL Vos playbooks]**.
2. **Publier le playbook** : si le playbook n’est pas déjà publié, vous devez le publier avant de le partager.

   >[!NOTE]
   >
   >Un partenariat doit être établi entre les organisations source et cible pour permettre le partage des playbooks. Découvrez comment [créer une demande de partenariat d’organisation](/help/sandboxes/ui/sharing-packages-across-orgs.md#create-an-organization-partnership-request).

3. **Lancer le partage** : une fois le playbook publié et le partenariat établi, sélectionnez **[!UICONTROL Partager le playbook]**.
4. **Sélectionnez l’organisation cible** : sélectionnez l’organisation avec laquelle vous souhaitez partager le playbook lorsque vous y êtes invité.
5. **Confirmer et partager** : confirmez votre sélection. Vous recevrez des messages de confirmation indiquant que le partage a réussi.
6. **Vérifier l’organisation cible** : connectez-vous à l’organisation cible pour vérifier que le playbook est disponible.
7. **Importer le playbook** : sélectionnez **[!UICONTROL Importer]** pour importer le playbook dans l’organisation cible. Vous pouvez l’afficher dans l’onglet **Playbooks**.

Si le playbook n’apparaît pas, assurez-vous qu’il est publié et que le partenariat d’organisation est actif.

>[!IMPORTANT]
>
>Le partage de playbook transitif n’est pas pris en charge. Si vous partagez un playbook d’une organisation à une autre, puis que vous l’importez, il ne peut pas être partagé à nouveau de l’organisation de réception vers une troisième organisation.

## Autorisations nécessaires {#required-permissions}

Pour accéder au sandbox et utiliser cette fonctionnalité, vous avez besoin des autorisations suivantes :

### Autorisations des sandbox

Ces autorisations sont requises pour accéder à l’environnement Sandbox où la fonctionnalité existe :

* **Gérer le sandbox**
* **Afficher sandbox**

* **Autorisations de partage de packages** :

Ces autorisations sont requises pour la fonctionnalité de partage interne :

* [**Gérer le package**](/help/sandboxes/ui/sandbox-tooling.md)
* [**Partager le package**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

Utilisez ces autorisations pour :

* Saisir l’environnement du sandbox
* Accès à la fonctionnalité dans le sandbox
* Gérer et partager des packages selon les besoins

Ces autorisations se trouvent dans la section **[!UICONTROL Sandbox]** de la liste des autorisations.

![La liste des autorisations avec les autorisations appropriées pour la gestion et le partage des playbooks mise en surbrillance.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### Parcours et objets associés - autorisations

Lors de la création de Parcours qui utilisent des playbooks, vous pouvez référencer d’autres objets, tels que **Canaux**, **Audiences** et d’autres entités. Chacun de ces objets possède son propre jeu d’autorisations.

Il s’agit des autorisations essentielles pour les actions liées au Parcours, telles que :

* **Afficher le parcours**
* **Gérer le parcours**
* Autorisations liées à des objets tels que les audiences et les canaux

Vous avez également besoin des autorisations d’audience suivantes :

* **Lecture de segment**
* **Profil lu**
* **Jeu de données lu**

Les Parcours étant extrêmement flexibles et pouvant impliquer de nombreux objets interconnectés, leurs [autorisations complètes](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/access-control/privacy/high-low-permissions) sont documentées séparément et peuvent varier en fonction de votre cas d’utilisation particulier.

## Étapes suivantes

Maintenant que vous comprenez comment créer, publier et partager des playbooks à l’aide de l’assistant d’IA, découvrez comment commencer à utiliser les playbooks disponibles et choisir celui qui convient à votre cas d’utilisation dans [Liste des playbooks](/help/use-case-playbooks/playbooks/choose.md).