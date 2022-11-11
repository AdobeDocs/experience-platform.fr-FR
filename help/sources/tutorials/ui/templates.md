---
keywords: Experience Platform;accueil;rubriques populaires;
description: Adobe Experience Platform fournit des modèles préconfigurés que vous pouvez utiliser pour accélérer votre processus d’ingestion de données. Les modèles comprennent des ressources générées automatiquement telles que des schémas, des jeux de données, des règles de mappage, des identités, des espaces de noms d’identité et des flux de données que vous pouvez utiliser lors de l’importation de données d’une source vers Experience Platform.
title: (Alpha) Créer un flux de données de sources à l’aide de modèles dans l’interface utilisateur
hide: true
hidefromtoc: true
source-git-commit: d6d8281d1be1468b0c2b7474b80be96949dc7d4c
workflow-type: ht
source-wordcount: '1184'
ht-degree: 100%

---

# (Alpha) Créer un flux de données de sources à l’aide de modèles dans l’interface utilisateur

>[!IMPORTANT]
>
>Les modèles sont en version Alpha et ne sont actuellement pris en charge que par la [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md). La documentation et les fonctionnalités peuvent changer.

Adobe Experience Platform fournit des modèles préconfigurés que vous pouvez utiliser pour accélérer votre processus d’ingestion de données. Les modèles comprennent des ressources générées automatiquement telles que des schémas, des jeux de données, des identités, des règles de mappage, des espaces de noms d’identité et des flux de données que vous pouvez utiliser lors de l’importation de données d’une source vers Experience Platform.

Avec les modèles, vous pouvez :

* Réduire le délai de valorisation de l’ingestion en accélérant la création de ressources modélisées.
* Minimiser les erreurs qui peuvent se produire pendant le processus d’ingestion manuelle des données.
* Mettre à jour les ressources générées automatiquement à tout moment en fonction de vos cas d’utilisation.

Le tutoriel suivant décrit les étapes à suivre pour utiliser des modèles dans l’interface utilisateur de Platform à l’aide de la [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md).

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Utiliser des modèles dans l’interface utilisateur de Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Sélectionner le type d’entreprise"
>abstract="Sélectionnez le type d’entreprise approprié à votre cas d’utilisation. Votre accès peut varier en fonction de votre compte d’abonnement Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=fr" text="Présentation de Real-Time CDP"

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pouvant être utilisées pour créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Dans la catégorie des [!UICONTROL Applications Adobe], sélectionnez **[!UICONTROL Marketo Engage]**, puis **[!UICONTROL Ajouter des données]**.

![Un catalogue de l’espace de travail des sources avec la source de Marketo Engage mise en surbrillance.](../../images/tutorials/templates/catalog.png)

Une fenêtre contextuelle s’affiche, vous permettant de parcourir les modèles ou d’utiliser des schémas et des jeux de données existants.

* **Parcourir les modèles** : Les modèles sources créent automatiquement pour vous des schémas, des identités, des jeux de données et des flux de données avec des règles de mappage. Vous pouvez personnaliser ces ressources selon vos besoins.
* **Utiliser mes ressources existantes** : Ingérez vos données à l’aide des jeux de données et des schémas que vous avez créés. Vous pouvez également créer de nouveaux jeux de données et de nouveaux schémas selon vos besoins.

Pour utiliser des ressources générées automatiquement, sélectionnez **[!UICONTROL Parcourir les modèles]** puis **[!UICONTROL Sélectionner]**.

![Fenêtre contextuelle contenant des options permettant de parcourir les modèles ou d’utiliser des ressources existantes.](../../images/tutorials/templates/browse-templates.png)

### Authentification

L’étape d’authentification s’affiche et vous invite à créer un compte ou à utiliser un compte existant.

#### Compte existant

Pour utiliser un compte existant, sélectionnez [!UICONTROL Compte existant] puis sélectionnez le compte à utiliser dans la liste qui s’affiche.

![La page de sélection d’un compte existant avec la liste des comptes existants auxquels vous pouvez accéder.](../../images/tutorials/templates/existing-account.png)

#### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez les informations de connexion source et les informations d’authentification du compte. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![La page d’authentification d’un nouveau compte avec les détails de connexion source et les informations d’authentification du compte.](../../images/tutorials/templates/new-account.png)

### Sélectionner des modèles

Une fois votre compte authentifié et sélectionné, une liste de modèles s’affiche. Sélectionnez l’icône d’aperçu à côté du nom d’un modèle pour prévisualiser les données d’exemple du modèle.

![Une liste de modèles avec l’icône d’aperçu mise en surbrillance.](../../images/tutorials/templates/templates.png)

La fenêtre d’aperçu s’affiche, vous permettant d’explorer et d’examiner des données d’exemple de votre modèle. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Compris]**.

![La fenêtre d’aperçu des données d’exemple.](../../images/tutorials/templates/preview-sample-data.png)

Sélectionnez ensuite dans la liste le modèle que vous souhaitez utiliser. Vous pouvez sélectionner plusieurs modèles et créer plusieurs flux de données à la fois. Cependant, un modèle ne peut être utilisé qu’une seule fois par compte. Une fois les modèles sélectionnés, cliquez sur **[!UICONTROL Terminer]** et patientez quelques instants le temps que les ressources se génèrent.

Si vous sélectionnez un ou des éléments partiels dans la liste des modèles disponibles, tous les schémas B2B et les espaces de noms d’identité seront quand même générés afin de garantir que les relations B2B entre les schémas soient correctement configurées.

>[!NOTE]
>
>Les modèles déjà utilisés seront désactivés de la sélection.

![La liste des modèles avec le modèle Rôle de contact d’opportunité sélectionné.](../../images/tutorials/templates/select-template.png)

### Vérifier les ressources {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Vérifier vos ressources générées automatiquement"
>abstract="La génération de toutes les ressources peut prendre jusqu’à cinq minutes. Si vous choisissez de quitter la page, une notification vous sera envoyée pour revenir une fois les ressources terminées. Vous pouvez vérifier les ressources une fois qu’elles ont été générées et effectuer des configurations supplémentaires dans votre flux de données à tout moment."

La page [!UICONTROL Vérifier les ressources de modèle] affiche les ressources générées automatiquement dans le cadre de votre modèle. Dans cette page, vous pouvez afficher les schémas, les jeux de données, les espaces de noms d’identité et les flux de données générés automatiquement associés à votre connexion source. La génération de toutes les ressources peut prendre jusqu’à cinq minutes. Si vous choisissez de quitter la page, une notification vous sera envoyée pour revenir une fois les ressources terminées. Vous pouvez vérifier les ressources une fois qu’elles ont été générées et effectuer des configurations supplémentaires dans votre flux de données à tout moment.

Les flux de données générés automatiquement sont activés par défaut. Sélectionnez les points de suspension (`...`) à côté du nom du flux de données, puis sélectionnez **[!UICONTROL Prévisualiser les mappages]** pour afficher les jeux de mappages créés pour votre flux de données.

![Une fenêtre déroulante avec l’option Prévisualiser les mappages sélectionnée.](../../images/tutorials/templates/preview.png)

Une page d’aperçu s’affiche, vous permettant d’examiner la relation de mappage entre vos champs de données sources et vos champs de schéma cibles. Une fois que vous avez consulté les mappages de votre flux de données. Sélectionnez **[!UICONTROL J’ai compris.]**

![La fenêtre de prévisualisation du mappage.](../../images/tutorials/templates/preview-mappings.png)

Vous pouvez mettre à jour vos flux de données à tout moment après leur exécution. Sélectionnez les points de suspension (`...`) à côté du nom du flux de données, puis sélectionnez **[!UICONTROL Mettre à jour le flux de données]**. Vous accédez à la page du processus des sources dans laquelle vous pouvez mettre à jour les détails de votre flux de données, y compris les paramètres d’ingestion partielle, les diagnostics d’erreur et les notifications d’alerte, ainsi que le mappage de votre flux de données.

Vous pouvez utiliser la vue de l’éditeur de schémas pour mettre à jour votre schéma généré automatiquement. Consultez le guide sur l’[utilisation de l’éditeur de schéma](../../../xdm/tutorials/create-schema-ui.md) pour plus d’informations.

![Une fenêtre déroulante avec l’option Mettre à jour les flux de données sélectionnée.](../../images/tutorials/templates/update.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez désormais créé des flux de données, ainsi que des ressources telles que des schémas, des jeux de données et des espaces de noms d’identité à l’aide de modèles. Pour obtenir des informations générales sur les sources, consultez la [présentation des sources](../../home.md).

## Annexe

La section suivante fournit des informations supplémentaires concernant les modèles.

### Utilisez le panneau des notifications pour revenir à la page de révision.

Les modèles sont pris en charge par les alertes Adobe Experience Platform. Vous pouvez utiliser le panneau de notifications pour recevoir des mises à jour sur le statut de vos ressources et également revenir à la page de révision.

Sélectionnez l’icône de notification dans l’en-tête supérieur de l’interface utilisateur de Platform, puis sélectionnez l’alerte de statut pour afficher les ressources que vous souhaitez consulter.

![Le panneau des notifications de l’interface utilisateur de Platform avec une notification signalant l’échec d’un flux de données mise en surbrillance.](../../images/tutorials/templates/notifications.png)