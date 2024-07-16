---
title: Modèles de rapport Power BI pour les tableaux de bord de Platform
description: Utilisez les modèles de rapport pour explorer les données d’Experience Platform à l’aide de Power BI.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 729d218f72a8caecc90a98810b973d0754f7757b
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 92%

---

# Modèles de rapport Power BI pour les tableaux de bord

La fonctionnalité de modèles de rapport Power BI vous permet de créer des rapports attrayants remplis de données provenant d’Adobe Experience Platform. Le processus d’installation simplifié installe automatiquement les widgets standard pour Real-Time Customer Profile, la segmentation et les destinations. L’installation connecte également Power BI à vos modèles de données afin que vous puissiez facilement personnaliser et étendre vos modèles de rapport. Ces rapports peuvent être partagés dans l’ensemble de l’organisation sans que les destinataires aient besoin d’informations d’identification pour votre organisation sur Platform.

Ce document explique comment connecter Adobe Experience Platform à l’application Power BI et utiliser des modèles de rapport pour partager des informations de données Platform clés avec des utilisateurs externes.

## Prise en main

Avant de poursuivre ce tutoriel, il est recommandé de bien comprendre la [composition de schéma](../../xdm/schema/composition.md) en Experience Platform et la manière dont les attributs sont inclus dans Real-time Customer Profile par le biais du [schéma d’union](../../xdm/schema/composition.md#union).

Pour installer l’intégration de l’application Power BI, les utilisateurs doivent avoir au préalable acquis les autorisations Platform suivantes :

- Gestion des requêtes
- Gestion des sandbox

Pour savoir comment attribuer ces autorisations, veuillez lire la documentation sur le [contrôle d’accès](../../access-control/home.md).

Vous devez également disposer d’un compte Power BI pour suivre ce tutoriel. Pour créer un compte, accédez à la [page d’accueil de Power BI](https://powerbi.microsoft.com/fr-fr/) et suivez le processus d’inscription. Les utilisateurs de ce compte Power BI doivent également activer le paramètre **Créer un espace de travail** dans leurs paramètres Power BI. Ce paramètre se trouve dans les paramètres du client du portail d’administration Power BI. Si votre compte est fourni par votre client ou votre employeur, contactez votre administrateur respectif pour activer ce paramètre.

![Paramètres de création d’espace de travail du portail d’administration Power BI.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Pour que l’onglet Tableaux de bord s’affiche dans le volet de navigation de gauche de l’interface utilisateur de Platform et que la vue Inventaire du tableau de bord soit visible, vous devez avoir accès à l’un des tableaux de bord Profil, Segmentation ou Destination dans le cadre de votre licence Platform.

## Installation de l’intégration de l’application Power BI

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Tableaux de bord]** dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Tableaux de bord]. L’onglet [!UICONTROL Parcourir] affiche une liste des vues de tableau de bord actuellement disponibles. Pour en savoir plus sur l’affichage des tableaux de bord disponibles, consultez la [documentation relative à l’inventaire](../inventory.md).

Sélectionnez ensuite l’onglet **[!UICONTROL Intégrations]**. La page d’intégration de l’application Power BI s’affiche. À partir de là, sélectionnez **[!UICONTROL Installer]** pour commencer l’installation.

>[!NOTE]
>
>Le bouton [!UICONTROL Installer] est désactivé, sauf si vous disposez des autorisations de gestion des sandbox et de Query Service.

![Écran de détails de Power BI avec le bouton Installer en surbrillance.](../images/power-bi/details-screen.png)

### Fournir les informations d’identification

La première étape du processus d’installation consiste à fournir des informations d’identification non expirantes pour l’intégration de l’application Power BI. Deux options sont disponibles pour fournir celles-ci : [[!UICONTROL Créer des informations d’identification]](#create-new-credentials) ou [[!UICONTROL Utiliser des informations d’identification existantes]](#use-existing-credentials). Sélectionnez le bouton (bascule) approprié pour continuer.

#### Création d’informations d’identification {#create-new-credentials}

Deux champs sont obligatoires lors de la génération d’informations d’identification : [!UICONTROL Nom] et [!UICONTROL Affecté à]. Le champ [!UICONTROL Affecté à] correspond à l’adresse e-mail associée à votre compte Power BI.

![Écran de génération d’informations d’identification de Power BI.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>La création d’informations d’identification non expirantes requiert l’attribution de certains rôles et autorisations. Les autorisations nécessaires sont celles de la gestion des sandbox et de l’intégration de Query Service. Les rôles obligatoires sont les rôles d’administrateur et de développeur d’Adobe Experience Platform. Pour savoir comment attribuer ces autorisations, veuillez lire la documentation sur le [contrôle d’accès](../../access-control/home.md).

Pour en savoir plus sur la génération d’informations d’identification Query Service non expirantes, reportez-vous au [guide des informations d’identification non expirantes](../../query-service/ui/credentials.md#non-expiring-credentials).

Après avoir généré pour la première fois des informations d’identification non expirantes, un fichier JSON est téléchargé sur l’ordinateur. Ce fichier JSON peut ensuite être partagé avec d’autres utilisateurs en tant qu’informations d’identification pour terminer le processus d’installation.

#### Utilisation d’informations d’identification existantes {#use-existing-credentials}

Un fichier d’informations d’identification JSON peut également être chargé pour passer la validation. Ces fichiers JSON contenant les valeurs d’informations d’identification non expirantes sont téléchargés sur l’ordinateur local utilisé lors de la création d’informations d’identification non expirantes.

>[!IMPORTANT]
>
>Pour utiliser des informations d’identification non expirantes existantes, l’utilisateur doit déjà avoir reçu des informations d’identification. Si l’utilisateur n’a pas d’informations d’identification attribuées et ne peut pas en créer à l’aide d’Adobe Admin Console, il ne peut pas poursuivre le processus d’installation.

Sélectionnez **[!UICONTROL Charger le fichier d’informations d’identification]**, puis sélectionnez le fichier JSON approprié à charger dans la boîte de dialogue qui s’affiche.

![Écran des informations d’identification de Power BI avec le bouton Charger le fichier d’informations d’identification en surbrillance](../images/power-bi/upload-credential-file.png).

Une fois que vous avez fourni les informations d’identification non expirantes, elles sont automatiquement validées par Platform. Un message de confirmation apparaît lorsque la validation est effectuée avec succès. Sélectionnez **[!UICONTROL Suivant]** pour consulter l’accord de consentement pour l’application Power BI.

![Écran de validation des informations d’identification non expirantes avec le bouton Suivant en surbrillance.](../images/power-bi/successfully-uploaded-credential-file.png)

### Donner son consentement

L’écran relatif au consentement apparaît. Sélectionnez **[!UICONTROL Vérifier le consentement]** pour ouvrir une nouvelle fenêtre détaillant les autorisations requises pour que Power BI accède et utilise vos données conformément aux conditions d’utilisation et à la déclaration de confidentialité.

![Écran relatif au consentement avec le bouton Vérifier le consentement en surbrillance.](../images/power-bi/provide-consent-display.png)

Sélectionnez **[!UICONTROL Accepter]** pour octroyer à Power BI l’autorisation d’accéder et d’utiliser vos données Platform.

![Demande d’autorisations pour l’application Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Si vous quittez le processus d’installation à tout moment avant d’avoir donné votre consentement, l’intégration de l’application Power BI n’est pas installée dans l’inventaire des tableaux de bord.

Après avoir donné votre consentement, le modèle de rapport est automatiquement installé dans l’environnement Power BI dans le cadre du processus d’installation. Power BI utilise ensuite les informations d’identification non expirantes pour accéder à Platform, exécuter séquentiellement toutes les requêtes SQL et remplir le modèle de rapport avec les données renvoyées.

Sélectionnez **[!UICONTROL Terminer]** pour revenir à l’inventaire des tableaux de bord.

![Écran relatif au consentement avec le bouton Terminer en surbrillance.](../images/power-bi/finish-consent-review.png)

Maintenant que le modèle de rapport Power BI est installé, il apparaît dans la liste des tableaux de bord disponibles sous l’onglet [!UICONTROL Parcourir]. Sélectionnez **[!UICONTROL Power BI]** dans la liste pour accéder à l’environnement Power BI.

![Power BI répertorié dans l’inventaire des tableaux de bord.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Les administrateurs Power BI doivent s’assurer que les utilisateurs disposent des autorisations d’accès appropriées pour afficher ces tableaux de bord dans l’environnement Power BI.

## Espace de travail Power BI

Après vous être connecté à [l’espace de travail Power BI](https://dxt.powerbi.com), des modèles de rapport sont disponibles pour chacun des services auxquels vous avez accès. Les modèles de rapport incluent les tableaux de bord des profils, des segments et des destinations **uniquement** s’ils disposent des autorisations d’affichage correspondantes.

Les widgets standard des profils, des segments et des destinations sont disponibles par défaut dans les modèles de rapport Power BI.

>[!NOTE]
>
>Les autorisations de modification doivent être activées pour un tableau de bord donné afin de permettre l’installation de celui-ci dans l’environnement Power BI.

![Rapport de modèle de profil Power BI utilisant les widgets standard de profil de Platform.](../images/power-bi/profile-report-template.png)

Une fois qu’un tableau de bord est installé dans Power BI, les modèles de rapport s’affichent par défaut pour tous les utilisateurs. Si vous souhaitez restreindre l’accès à certains modèles de rapport, assurez-vous de désactiver l’accès des utilisateurs concernés depuis l’environnement Power BI.

## Personnalisation de votre modèle de rapport Power BI

Grâce à l’utilisation de widgets personnalisés, vous pouvez ajouter des attributs personnalisés à votre modèle de données pour enrichir les modèles de rapport fournis par Power BI.

>[!NOTE]
>
>Les attributs que vous pouvez utiliser pour les widgets personnalisés dépendent de ce qui est disponible dans le schéma d’union. Pour savoir comment afficher et explorer les schémas d’union au profit de vos widgets personnalisés, consultez le [guide de l’interface utilisateur du schéma d’union](../../profile/ui/union-schema.md).

### Création d’un widget personnalisé

Les widgets personnalisés sont créés à l’aide de la bibliothèque de widgets. Consultez la [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour une introduction à la fonctionnalité et le [tutoriel sur la création d’un widget personnalisé](../customize/custom-widgets.md) pour des instructions spécifiques.

>[!IMPORTANT]
>
>Les widgets personnalisés nouvellement créés ne sont **pas** automatiquement synchronisés entre les tableaux de bord Adobe Experience Platform et les modèles de rapport Power BI. Tout widget personnalisé créé dans l’interface utilisateur de Platform doit être recréé manuellement dans l’environnement Power BI.

### Recréation de votre widget personnalisé dans l’environnement Power BI

Une fois que votre tableau de bord contient les mesures et attributs appropriés dans des widgets personnalisés, vous pouvez modifier le modèle de rapport affiché dans l’environnement Power BI. Consultez la [documentation de Power BI](https://docs.microsoft.com/fr-FR/power-bi/) pour savoir comment modifier un rapport via son interface utilisateur.

## Suppression de l’intégration de l’application Power BI

Pour supprimer le tableau de bord, accédez à l’inventaire des tableaux de bord et sélectionnez l’icône supprimer (![](../images/power-bi/delete-icon.png)) à côté du nom du tableau de bord.

>[!NOTE]
>
>Seul l’utilisateur qui a installé le tableau de bord Power BI peut supprimer l’intégration à partir de l’interface utilisateur de Platform.

![Onglet Parcourir de l’écran d’inventaire des tableaux de bord affiché avec le bouton Parcourir et l’icône Supprimer en surbrillance.](../images/power-bi/delete-power-bi-dashboard.png)

Une fenêtre contextuelle de confirmation apparaît. Sélectionnez **[!UICONTROL Supprimer]** pour confirmer le processus.

>[!IMPORTANT]
>
>La suppression du tableau de bord Power BI de l’interface utilisateur de Platform n’entraîne **pas** la suppression des modèles de rapport disponibles dans votre environnement Power BI. Si vous souhaitez supprimer complètement les informations contenues dans les modèles de rapport Power BI, vous devez vous connecter à votre compte Power BI et supprimer les modèles de rapport de cet environnement. Une fois la suppression effectuée, l’utilisateur peut réinstaller le tableau de bord Power BI en suivant les mêmes instructions d’installation que celles décrites ci-dessus.

## Étapes suivantes

Grâce à la lecture de ce document, vous comprenez mieux comment les modèles de rapport Power BI peuvent être intégrés à Platform pour partager des informations de données attrayantes à partir de vos tableaux de bord de profils, de segments ou de destinations. Consultez la section [Présentation de la personnalisation des tableaux de bord](../customize/overview.md) pour en savoir plus sur la personnalisation de vos tableaux de bord.
