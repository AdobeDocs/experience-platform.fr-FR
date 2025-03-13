---
solution: Experience Platform
title: 'Assistant AI pour les cas d’utilisation : créez et partagez vos propres playbooks.'
description: Comment créer et partager vos propres playbooks de cas d’utilisation.
role: User
source-git-commit: f813db7599409a8fc048480f7803ed86c9f397fe
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 1%

---


# Créer et partager vos propres playbooks

Le **framework de création de playbooks**, optimisé par l’assistant d’IA d’Adobe, vous permet de créer, de gérer et de partager des playbooks efficacement dans Adobe Experience Platform.

Le cadre suit un processus en trois étapes :

1. **Capture des métadonnées** : utilisez l’assistant AI ou le [formulaire web] pour capturer les métadonnées du playbook.

2. **Association technique** : ajoutez des ressources techniques spécifiques telles que des parcours ou des audiences au playbook. Vous conservez un contrôle total sur le processus de création des playbooks dans votre sandbox de développement, en veillant à l’alignement avec vos schémas et autres structures de données uniques.

3. **Distribution des playbooks** : partagez des playbooks dans différentes organisations. Par exemple, le Centre d&#39;excellence Martech d&#39;ACME en Allemagne peut créer un manuel « doré » et le distribuer à des organisations régionales en Thaïlande, en Australie, etc. pour normaliser le cas d’utilisation marketing.

## Création d’un playbook avec l’assistant Adobe AI

### Présentation du playbook

Vous pouvez créer un playbook de deux manières : en utilisant l’assistant d’IA d’Adobe ou manuellement.

Pour créer un playbook avec l’assistant d’IA d’Adobe, procédez comme suit :

1. Dans le volet de navigation de gauche, sélectionnez **Playbooks**.

![ « Playbooks » mis en surbrillance dans le volet de navigation de gauche de l’interface utilisateur.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

1. Sélectionnez **Nouveau playbook**, puis sélectionnez **Générer le playbook avec l’assistant d’IA**.

![Sélectionnez le bouton « Nouveau playbook ».](/help/use-case-playbooks/assets/playbooks/authoring/new-playbook.png)

![Bouton « Générer le playbook avec l’assistant AI » mis en surbrillance.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

1. Dans le champ d’invite, décrivez le cas d’utilisation.

**Exemple** : « Contactez les clients ACME qui ont parcouru les chaussures de course, mais qui n’ont pas effectué l’achat. »

![Sélectionnez le bouton « Générer le playbook avec l’assistant AI ».](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

1. Sélectionnez **Générer** pour créer les métadonnées du playbook.

![Zone d’invite avec le bouton « Générer » le playbook en surbrillance.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

1. Une fois générée, sélectionnez **[!UICONTROL Modifier]** pour modifier le titre, la description et les métadonnées générés, si nécessaire.

![Le playbook généré avec le bouton « Modifier » mis en surbrillance.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Pour vous assurer que les ingénieurs de données disposent de tous les détails nécessaires pour configurer le cas d’utilisation, renseignez la section **[!UICONTROL Détails du playbook]**. Bien que facultatifs, ces champs permettent de capturer des informations clés, ce qui facilite la connexion des composants techniques appropriés. Sélectionnez **[!UICONTROL Modifier]** pour ajouter des valeurs aux champs suivants :

* **Industrie**
* **Audience cible**
* **Canal marketing**

![Section Détails du playbook avec le bouton « Modifier » en surbrillance.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Une fois les métadonnées générées, cliquez sur le bouton **Modifier la carte des parcours** pour ajuster les étapes de la carte des parcours selon les besoins.

![Modifier le bouton de mappage de parcours.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Modifiez la carte du parcours une fois que vous avez capturé les métadonnées du playbook.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Procédez ensuite à l’association du playbook aux ressources techniques.

Pour créer un playbook manuellement, sélectionnez **Créer un playbook manuellement**.

![Créer le playbook manuellement](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Un modèle de playbook vierge s’affiche. Renseignez des détails tels que **Titre** et **Description**. Vous pouvez également modifier la carte du parcours pour ajouter des événements et des points de contact si nécessaire.

## Associer un playbook à des ressources techniques

Que vous créiez un playbook manuellement ou avec l’assistant d’IA, vous devez l’associer aux ressources techniques requises. Accédez à l’onglet **[!UICONTROL Technical Assets]** et sélectionnez le produit souhaité. Pour cet exemple, choisissez **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> La prise en charge de Real-Time Customer Data Platform sera ajoutée dans une version ultérieure.

![ l’onglet « Ressources techniques » et le bouton « Ajouter le produit requis » mis en surbrillance.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Sélectionnez **[!UICONTROL Sélectionner une ressource]** pour associer ce playbook à un parcours, comme illustré dans l’image ci-dessous. Sélectionnez ensuite **Publier le playbook** pour finaliser le playbook.

![ bouton « Sélectionner les ressources » mis en surbrillance dans l’onglet « Ressources techniques »](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Sélectionner un parcours ](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Une fois publié, le playbook extrait et associe automatiquement le schéma du parcours et les détails de l’audience.

![Playbook publié](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Tous les playbooks créés sont disponibles dans l’onglet **Vos playbooks**.

![’onglet « Vos playbooks »](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

Vous pouvez sélectionner n’importe quel playbook du catalogue pour créer des instances à réutiliser. Reportez-vous à la documentation pour [savoir comment créer des instances](/help/use-case-playbooks/playbooks/create-share-reuse.md).

![’option « Créer une instance » mise en surbrillance dans l’onglet « Présentation du playbook » une fois que vous avez sélectionné un playbook.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Une fois qu’un playbook est publié, il ne peut pas être modifié. Pour apporter des modifications, supprimez le playbook et recommencez.

## Exemples d’invites

L’assistant AI peut traiter diverses structures d’invite et extraire des détails clés tout en filtrant les informations inutiles. Vous trouverez ci-dessous quelques exemples d’invites utilisateur et leur interprétation par le système :

**Exemple 1 :**

« Créez une campagne intitulée « Achevez l’apparence » afin d’augmenter les ventes et la valeur vie client. La campagne encourage les clients à acheter des ustensiles de cuisine ou des meubles à effectuer un achat complémentaire au moyen de recommandations et d’offres personnalisées liées à leur achat. Envoyez d’abord des recommandations de produits aux clients. S’ils n’effectuent aucun achat dans les 7 jours, ils reçoivent un second message contenant des recommandations et des offres de produits. Utilisez les notifications push et les e-mails pour contacter les clients. Ciblez les clients qui ont effectué un achat au cours des 7 derniers jours dans la catégorie des ustensiles de cuisine ou des meubles et qui n’ont pas été ciblés au cours des 30 derniers jours. Dans le cadre de la campagne, nous voulons mesurer les KPI tels que les clics (e-mail, application, sms, notification push), le CTR, le CTR du portefeuille électronique, le chiffre d’affaires AOV Conversion.CLV, le total des événements d’achat (en magasin, numérique, centre d’appels). »

![Exemple d’invite 1](/help/use-case-playbooks/assets/playbooks/authoring/example-prompt.png)

**Exemple 2 :**

« Nom du projet : Newsletter mode
Contexte : (proactif ou résolution de problèmes) : parcours conçu pour envoyer des newsletters de mode aux clients ACME abonnés à la newsletter.
Objectif : envoyer des e-mails de newsletter sur la mode aux clients ACME abonnés à la communication.
Détails promotionnels : le client reçoit des informations sur la mode dans le canal e-mail chaque semaine. L’e-mail doit être personnalisé et les variations de contenu doivent être basées sur le sexe, la langue et le marché.
Canaux/points de contact du projet : e-mail
Public cible : clients et clientes qui se sont abonnés aux communications de la newsletter ACME Fashion.
KPI/mesures d’engagement/ROI cibles : 1. Augmentez le chiffre d’affaires des produits . 2. Encouragez la fidélisation de la clientèle. »

![Exemple d’invite 2](/help/use-case-playbooks/assets/playbooks/authoring/example-2-prompt.png)

**Exemple 3 :**

« Incitez les acheteurs à acheter des produits au cours d’une campagne promotionnelle continue.
Interagissez avec les acheteurs lors d’une promotion en cours en envoyant une communication appropriée par e-mail, SMS ou notifications push pour acheter des produits. Envoyez-lui un e-mail de rappel après 24 heures indiquant qu’il ne participe pas à la promotion. »

![Exemple d’invite 3](/help/use-case-playbooks/assets/playbooks/authoring/example-3-prompt.png)

**Exemple 4 :**

« Vendre des chaussures aux lycéens. »

![Exemple d’invite 4](/help/use-case-playbooks/assets/playbooks/authoring/example-4-prompt.png)

L’assistant AI supprime tous les détails inutiles tels que « Nom du projet » ou « Arrière-plan ». Il extrait les éléments clés tels que « audience cible », « objectif de la campagne » et « canal marketing » et fonctionne avec n’importe quel style d’entrée.

Ces exemples montrent comment l’IA peut affiner et extraire des détails essentiels des invites utilisateur.

>[!NOTE]
>
> Évitez les PII ou les mots explicites lors de la rédaction de vos invites.

## Instructions relatives au contenu et modération

Lors de la création de playbooks, tenez compte de la langue et du contenu que vous incluez. Les playbooks sont visibles dans l’ensemble de votre organisation et tout contenu offensant ou inapproprié peut être signalé par les utilisateurs.

### Marquage et processus de révision

Si un playbook est signalé pour du contenu inapproprié ou offensant, il est automatiquement signalé à Adobe pour révision. Adobe examine ensuite le contenu signalé. S’il est jugé inapproprié, le client en est informé et le playbook est supprimé.

## Étapes suivantes

Maintenant que vous savez comment créer et publier des playbooks à l’aide de l’assistant d’IA d’Adobe, découvrez comment commencer à utiliser les playbooks disponibles et choisir celui qui convient à votre cas d’utilisation dans [Liste des playbooks](/help/use-case-playbooks/playbooks/choose.md).
