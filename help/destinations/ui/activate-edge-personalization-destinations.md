---
title: Activer les audiences vers des destinations de personnalisation Edge
description: Découvrez comment activer les audiences de Adobe Experience Platform vers les destinations de personnalisation de périphérie pour les cas d’utilisation de la personnalisation de la même page et de la page suivante.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 15%

---


# Activer les audiences vers des destinations de personnalisation Edge

## Vue d’ensemble {#overview}

Adobe Experience Platform utilise la [segmentation Edge](../../segmentation/ui/edge-segmentation.md) avec les [ destinations Edge](/help/destinations/destination-types.md#edge-personalization-destinations) pour permettre aux clients de créer et de cibler des audiences à grande échelle, en temps réel. Cette fonctionnalité vous permet de configurer des cas d’utilisation de personnalisation de la même page et de la page suivante.

Parmi les exemples de destinations de périphérie, citons les connexions [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et [Personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md).

>[!NOTE]
>
>Lors de la [configuration de la connexion Adobe Target](../catalog/personalization/adobe-target-connection.md) *sans* utiliser un identifiant de flux de données, les cas d’utilisation décrits dans cet article ne sont pas pris en charge. Seuls les cas d’utilisation de la personnalisation de session suivante sont pris en charge en l’absence de flux de données.

>[!IMPORTANT]
> 
> * Pour activer les données et activer l’[ étape de mappage](#mapping) du workflow, vous avez besoin des **** **[!UICONTROL Visualiser les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès.
> * Pour activer les données sans passer par l’[ étape de mappage](#mapping) du workflow, vous avez besoin des autorisations **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer le segment sans mappage]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}
> 
> Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Cet article explique le processus requis pour activer les audiences vers les destinations Adobe Experience Platform Edge. Utilisées conjointement avec la [segmentation Edge](../../segmentation/ui/edge-segmentation.md) et le [ mappage facultatif d’attributs de profil](#mapping), ces destinations activent des cas d’utilisation de personnalisation de la même page et de la page suivante sur vos propriétés web et mobiles.

Pour un bref aperçu de la configuration de la connexion Adobe Target pour la personnalisation Edge, regardez la vidéo ci-dessous.

>[!NOTE]
>
>L’interface utilisateur d’Experience Platform est fréquemment mise à jour et peut avoir changé depuis l’enregistrement de cette vidéo. Pour obtenir les informations les plus récentes, reportez-vous aux étapes de configuration décrites dans les sections ci-dessous.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Pour une brève présentation du partage d’audiences et d’attributs de profil vers Adobe Target et des destinations de personnalisation personnalisées, regardez la vidéo ci-dessous.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Cas d’utilisation {#use-cases}

Utilisez des solutions de personnalisation d’Adobe, telles qu’Adobe Target, ou vos propres plateformes de partenaire de personnalisation (par exemple, [!DNL Optimizely], [!DNL Pega]), ainsi que des systèmes propriétaires (par exemple, un CMS interne) pour offrir une expérience de personnalisation client plus approfondie via la destination [Personalization personnalisée](../catalog/personalization/custom-personalization.md). Tout cela tout en tirant parti des fonctionnalités Experience Platform de collecte et de segmentation des données Edge Network.

Les cas d’utilisation décrits ci-dessous incluent à la fois la personnalisation du site et la publicité ciblée sur site.

Pour activer ces cas d’utilisation, les clients ont besoin d’une méthode rapide et simplifiée pour récupérer à la fois les audiences et les informations d’attribut de profil de l’Experience Platform, et envoyer ces informations aux connexions [Adobe Target](../catalog/personalization/adobe-target-connection.md) ou [Personalization personnalisé](../catalog/personalization/custom-personalization.md) dans l’interface utilisateur de l’Experience Platform.

### Personnalisation de la même page {#same-page}

Un utilisateur visite une page de votre site web. Vous pouvez utiliser les informations actuelles sur la visite de la page (par exemple, l’URL de référence, la langue du navigateur, les informations sur les produits intégrés) pour sélectionner l’action ou la décision suivante (par exemple, la personnalisation), à l’aide de la connexion [Personnalisation personnalisée](../catalog/personalization/custom-personalization.md) pour les plateformes autres qu’Adobe (par exemple, [!DNL Pega], [!DNL Optimizely] ou d’autres).

### Personnalisation de la page suivante {#next-page}

Un utilisateur visite la page A de votre site web. En fonction de cette interaction, l’utilisateur a rempli les critères d’un ensemble d’audiences. L’utilisateur clique ensuite sur un lien qui le mène de la page A à la page B. Les audiences auxquelles l’utilisateur s’était qualifié lors de l’interaction précédente sur la page A, ainsi que les mises à jour de profil déterminées par la visite actuelle du site web, seront utilisées pour alimenter l’action ou la décision suivante (par exemple, la bannière publicitaire à afficher au visiteur ou, dans le cas de tests A/B, la version de la page à afficher).

### Personnalisation de la prochaine session {#next-session}

Un utilisateur visite plusieurs pages de votre site web. En fonction de ces interactions, l’utilisateur s’est qualifié pour un ensemble d’audiences. L’utilisateur met ensuite fin à la session de navigation actuelle.

Le lendemain, l’utilisateur revient au même site web client. Les audiences pour lesquelles ils avaient rempli les critères lors de l’interaction précédente avec toutes les pages du site web visitées, ainsi que les mises à jour de profil déterminées par la visite du site web en cours, seront utilisées pour sélectionner l’action/la décision suivante (par exemple, la bannière publicitaire à afficher au visiteur ou, dans le cas d’un test A/B, la version de la page à afficher).

### Personnalisation d’une bannière de page d’accueil {#home-page-banner}

Une société de location et de vente d’habitations souhaite personnaliser sa page d’accueil avec une bannière, en fonction des qualifications d’audience dans Adobe Experience Platform. L’entreprise peut sélectionner les audiences qui doivent bénéficier d’une expérience personnalisée et les envoyer à Adobe Target en tant que critères de ciblage pour leur offre Target.

## Conditions préalables {#prerequisites}

### Configuration d’un flux de données dans l’interface utilisateur de la collecte de données {#configure-datastream}

La première étape de la configuration de votre destination de personnalisation consiste à configurer un flux de données pour le SDK web Experience Platform. Cette opération est effectuée dans l’interface utilisateur de la collecte de données.

Lors de la configuration du flux de données, sous **[!UICONTROL Adobe Experience Platform]** assurez-vous que la **[!UICONTROL Segmentation Edge]** et les **[!UICONTROL Destinations de personnalisation]** sont bien sélectionnées.

>[!TIP]
>
>À compter de la version d’avril 2024, il n’est pas nécessaire de cocher la case Segmentation Edge lors de la [configuration de la connexion à Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md). Dans ce cas, la [personnalisation de session suivante](#next-session) est le seul cas d’utilisation de personnalisation disponible.

![Configuration de la chaîne de données avec la segmentation Edge et les destinations Personalization en surbrillance !](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Pour plus d’informations sur la configuration d’un flux de données, suivez les instructions décrites dans la section [Documentation du SDK web Platform](../../datastreams/configure.md#aep).

### Création d’une stratégie de fusion [!DNL Active-On-Edge] {#create-merge-policy}

Après avoir créé votre connexion de destination, vous devez créer une stratégie de fusion [!DNL Active-On-Edge]. La stratégie de fusion [!DNL Active-On-Edge] garantit que les audiences sont constamment évaluées [sur le serveur Edge](../../segmentation/ui/edge-segmentation.md) et qu’elles sont disponibles pour un cas d’utilisation de la personnalisation en temps réel et de la page suivante.

>[!IMPORTANT]
>
>Actuellement, les destinations Edge ne prennent en charge que l’activation des audiences qui utilisent la [stratégie de fusion active sur Edge](../../segmentation/ui/segment-builder.md#merge-policies) définie par défaut. Si vous mappez des audiences qui utilisent une autre stratégie de fusion avec des destinations de périphérie, ces audiences ne seront pas évaluées.

Suivez les instructions de la section [création d’une politique de fusion](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) et assurez-vous d’activer le bouton **[!UICONTROL Politique de fusion Active-On-Edge]**.

### Création d’une audience dans Platform {#create-audience}

Après avoir créé la stratégie de fusion [!DNL Active-On-Edge], vous devez créer une nouvelle audience dans Platform.

Suivez le guide [créateur d’audiences](../../segmentation/ui/segment-builder.md) pour créer votre nouvelle audience et assurez-vous de [l’affecter](../../segmentation/ui/segment-builder.md#merge-policies) à la stratégie de fusion [!DNL Active-On-Edge] que vous avez créée à l’étape précédente.

### Création d’une connexion de destination {#connect-destination}

Après avoir configuré votre flux de données, vous pouvez commencer à configurer votre destination de personnalisation.

Suivez le [tutoriel sur la création de connexion de destination](../ui/connect-destination.md) pour obtenir des instructions détaillées sur la création d’une connexion de destination.

Selon la destination que vous configurez, reportez-vous aux articles suivants pour connaître les conditions préalables spécifiques à une destination et les informations connexes :

* [Connexion Adobe Target](../catalog/personalization/adobe-target-connection.md#parameters)
* [Connexion de personnalisation personnalisée](../catalog/personalization/custom-personalization.md##parameters)

## Sélectionner votre destination {#select-destination}

Une fois les conditions préalables remplies, vous pouvez sélectionner la destination de personnalisation Edge à utiliser pour la personnalisation de la même page et de la page suivante.

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destinations mis en surbrillance dans l’interface utilisateur de l’Experience Platform.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer les audiences]** sur la carte correspondant à la destination de personnalisation où vous souhaitez activer vos audiences, comme illustré dans l’image ci-dessous.

   ![Activez le contrôle de l’audience mis en surbrillance sur une carte de destination dans le catalogue.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Sélectionnez la connexion de destination que vous souhaitez utiliser pour activer vos audiences, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Sélectionnez l’étape de destination dans le workflow d’activation.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Passez à la section suivante pour [sélectionner vos audiences](#select-audiences).

## Sélectionner vos audiences {#select-audiences}

Utilisez les cases à cocher situées à gauche des noms d’audience pour sélectionner les audiences que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

Pour sélectionner les audiences que vous souhaitez activer vers la destination, utilisez les cases à cocher à gauche des noms d’audience, puis sélectionnez **[!UICONTROL Suivant]**.

Vous pouvez sélectionner plusieurs types d’audiences, selon leur origine :

* **[!UICONTROL Service de segmentation]** : audiences générées dans Experience Platform par le service de segmentation. Pour plus d’informations, consultez la [documentation sur la segmentation](../../segmentation/ui/overview.md) .
* **[!UICONTROL Téléchargement personnalisé]** : audiences générées en dehors de l’Experience Platform et téléchargées dans Platform sous la forme de fichiers CSV. Pour en savoir plus sur les audiences externes, consultez la documentation sur l&#39; [import d&#39;une audience](../../segmentation/ui/audience-portal.md#import-audience).
* Autres types d’audiences, provenant d’autres solutions d’Adobe, telles que [!DNL Audience Manager].

![Sélectionnez l’étape des audiences du workflow d’activation avec plusieurs audiences surlignées.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Attributs de mappage {#mapping}

>[!IMPORTANT]
>
>Les attributs de profil peuvent contenir des données sensibles. Pour protéger ces données, la destination **[!UICONTROL Personalization personnalisée]** nécessite que vous utilisiez l’ [ API serveur Edge Network](../../server-api/overview.md) lors de la configuration de la destination pour la personnalisation basée sur les attributs. Tous les appels de l’API du serveur doivent être effectués dans un [contexte authentifié](../../server-api/authentication.md).
>
><br>Si vous utilisez déjà le SDK Web ou le SDK mobile pour votre intégration, vous pouvez récupérer des attributs via l’API serveur en ajoutant une intégration côté serveur.
>
><br>Si vous ne respectez pas les exigences ci-dessus, la personnalisation sera basée uniquement sur l’appartenance à l’audience.

Sélectionnez les attributs sur lesquels vous souhaitez activer des cas d’utilisation de personnalisation pour vos utilisateurs. Cela signifie que si la valeur d’un attribut change ou qu’un attribut est ajouté à un profil, ce profil devient membre de l’audience et est activé sur la destination de personnalisation.

L’ajout d’attributs est facultatif. Vous pouvez toujours passer à l’étape suivante et activer la personnalisation de la même page et de la page suivante sans sélectionner d’attributs. Si vous n’ajoutez pas d’attributs à cette étape, la personnalisation continuera à se produire en fonction des qualifications d’appartenance à l’audience et de mappage d’identité pour les profils.

![Image montrant l&#39;étape de mappage avec un attribut sélectionné.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Sélectionner les attributs source {#select-source-attributes}

Pour ajouter des attributs source, sélectionnez le contrôle **[!UICONTROL Ajouter un nouveau champ]** sur la colonne **[!UICONTROL Champ Source]** et recherchez ou accédez au champ d’attribut XDM de votre choix, comme illustré ci-dessous.

![Enregistrement d’écran montrant comment sélectionner un attribut cible dans l’étape de mappage.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Sélectionner les attributs de cible {#select-target-attributes}

Pour ajouter des attributs de cible, sélectionnez le contrôle **[!UICONTROL Ajouter un nouveau champ]** sur la colonne **[!UICONTROL Champ cible]** et saisissez le nom de l’attribut personnalisé auquel vous souhaitez mapper l’attribut source.

>[!NOTE]
>
>La sélection des attributs de la cible s’applique uniquement au workflow d’activation [Personalization personnalisée](../catalog/personalization/custom-personalization.md), afin de prendre en charge le mappage de champs de nom convivial dans la plateforme de destination.

![Enregistrement d’écran montrant comment sélectionner un attribut XDM à l’étape de mappage](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Planifier l’export d’audience {#scheduling}

Par défaut, la page [!UICONTROL Planification de l’audience] n’affiche que les audiences nouvellement sélectionnées dans le flux d’activation actuel.

Pour afficher toutes les audiences activées vers votre destination, utilisez l’option de filtrage et désactivez le filtre **[!UICONTROL Afficher les nouvelles audiences uniquement]** .

![Le filtre Toutes les audiences est mis en surbrillance.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

Sur la page **[!UICONTROL Planification de l’audience]**, sélectionnez chaque audience, puis utilisez les sélecteurs **[!UICONTROL Date de début]** et **[!UICONTROL Date de fin]** pour configurer l’intervalle d’heure d’envoi des données à votre destination.

![Étape du planning d&#39;audience du workflow d&#39;activation avec la date de début et de fin mise en surbrillance.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Sélectionnez **[!UICONTROL Suivant]** pour accéder à la page [!UICONTROL Réviser].

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Résumé de la sélection dans l’étape de révision.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Évaluation des politiques de consentement {#consent-policy-evaluation}

Si votre organisation a acheté **Adobe HealthCare Shield** ou **Adobe Privacy &amp; Security Shield**, sélectionnez **[!UICONTROL Afficher les politiques de consentement applicables]** pour identifier les politiques de consentement appliquées et le nombre de profils inclus dans l&#39;activation qui en résulte. Pour plus d’informations, consultez la section [Évaluation de la stratégie de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) .

### Vérifications des stratégies d’utilisation des données {#data-usage-policy-checks}

À l’étape **[!UICONTROL Réviser]**, Experience Platform recherche également toutes les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la politique. Vous ne pouvez pas terminer le workflow d’activation de l’audience tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la façon de résoudre les violations de stratégie, reportez-vous à la section [Violations de stratégie d’utilisation des données](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) de la documentation sur la gouvernance des données.

![Exemple de violation de politique de données.](../assets/common/data-policy-violation.png)

### Filtrage des audiences {#filter-audiences}

Au cours de cette étape, vous pouvez utiliser les filtres disponibles sur la page pour afficher uniquement les audiences dont le planning ou le mapping a été mis à jour dans le cadre de ce workflow. Vous pouvez également basculer entre les colonnes du tableau que vous souhaitez afficher.

![Enregistrement de l’écran montrant les filtres d’audience disponibles dans l’étape de révision.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Si votre sélection vous satisfait et qu’aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
