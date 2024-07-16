---
description: Découvrez comment utiliser des modèles dans l’interface utilisateur de Adobe Experience Platform pour accélérer votre processus d’ingestion de données pour les données B2B.
title: Créer un flux de données de sources à l’aide de modèles dans l’interface utilisateur
badge1: « Version bêta »
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: 4a9cae014a8eba20f93023913f3a73103b16d944
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 44%

---

# Créer un flux de données de sources à l’aide de modèles dans l’interface utilisateur {#create-a-sources-dataflow-using-templates-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_marketo_mapping"
>title="Modèles de sources dans l’interface utilisateur de Platform"
>abstract="Les modèles comprennent des ressources générées automatiquement telles que des schémas, des jeux de données, des identités, des règles de mappage, des espaces de noms d’identité et des flux de données que vous pouvez utiliser lors de l’importation de données d’une source vers Experience Platform. Vous pouvez mettre à jour des ressources générées automatiquement pour les personnaliser en fonction de vos cas d’utilisation."

>[!IMPORTANT]
>
>Les modèles sont en version bêta et sont pris en charge par les sources suivantes :
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>La documentation et les fonctionnalités peuvent changer.

Adobe Experience Platform fournit des modèles préconfigurés que vous pouvez utiliser pour accélérer votre processus d’ingestion de données. Les modèles comprennent des ressources générées automatiquement telles que des schémas, des jeux de données, des identités, des règles de mappage, des espaces de noms d’identité et des flux de données que vous pouvez utiliser lors de l’importation de données d’une source vers Experience Platform.

Avec les modèles, vous pouvez :

* Réduire le délai de valorisation de l’ingestion en accélérant la création de ressources modélisées.
* Minimiser les erreurs qui peuvent se produire pendant le processus d’ingestion manuelle des données.
* Mettre à jour les ressources générées automatiquement à tout moment en fonction de vos cas d’utilisation.

Le tutoriel suivant explique comment utiliser des modèles dans l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Utiliser des modèles dans l’interface utilisateur de Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Sélectionner le type d’entreprise"
>abstract="Sélectionnez le type d’entreprise approprié à votre cas d’utilisation. Votre accès peut varier en fonction de votre compte d’abonnement Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr" text="Présentation de Real-Time CDP"

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] et afficher un catalogue de sources disponibles dans Experience Platform.

Utilisez le menu *[!UICONTROL Catégories]* pour filtrer les sources par catégorie. Vous pouvez également saisir un nom de source dans la barre de recherche pour trouver une source spécifique dans le catalogue.

Accédez à la catégorie [!UICONTROL Adobe applications] pour afficher la carte source [!DNL Marketo Engage], puis sélectionnez [!UICONTROL Ajouter des données] pour commencer.

![Un catalogue de l’espace de travail des sources avec la source de Marketo Engage mise en surbrillance.](../../images/tutorials/templates/catalog.png)

Une fenêtre pop-up s’affiche, vous permettant de parcourir les modèles ou d’utiliser des schémas et des jeux de données existants.

* **Parcourir les modèles** : Les modèles sources créent automatiquement pour vous des schémas, des identités, des jeux de données et des flux de données avec des règles de mappage. Vous pouvez personnaliser ces ressources selon vos besoins.
* **Utiliser mes ressources existantes** : Ingérez vos données à l’aide des jeux de données et des schémas que vous avez créés. Vous pouvez également créer de nouveaux jeux de données et de nouveaux schémas selon vos besoins.

Pour utiliser des ressources générées automatiquement, sélectionnez **[!UICONTROL Parcourir les modèles]** puis **[!UICONTROL Sélectionner]**.

![Fenêtre pop-up contenant des options permettant de parcourir les modèles ou d’utiliser des ressources existantes.](../../images/tutorials/templates/browse-templates.png)

### Authentification

L’étape d’authentification s’affiche et vous invite à créer un compte ou à utiliser un compte existant.

>[!BEGINTABS]

>[!TAB Utiliser un compte existant]

Pour utiliser un compte existant, sélectionnez [!UICONTROL Compte existant] puis sélectionnez le compte à utiliser dans la liste qui s’affiche.

![La page de sélection d’un compte existant avec la liste des comptes existants auxquels vous pouvez accéder.](../../images/tutorials/templates/existing-account.png)

>[!TAB Créer un compte]

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez les informations de connexion source et les informations d’authentification du compte. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![La page d’authentification d’un nouveau compte avec les détails de connexion source et les informations d’authentification du compte.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Sélectionner des modèles

Une fois votre compte authentifié, vous pouvez désormais sélectionner le modèle à utiliser pour votre flux de données.

+++[!DNL Marketo Engage] modèles
Le tableau suivant décrit les modèles disponibles pour la source [!DNL Marketo Engage].

| [!DNL Marketo Engage] modèles | Description |
| --- | --- |
| Activités | Le modèle Activités capture des instantanés d’activités basés sur un événement, tels que des interactions par e-mail, des interactions sur le site web et des appels de vente. |
| Sociétés | Le modèle Sociétés capture les détails du compte commercial, tels que les informations démographiques, le lieu et les informations de facturation de l’entreprise. |
| Comptes désignés | Le modèle Comptes nommés capture les détails des comptes qui ont été déterminés comme des comptes cibles à poursuivre. |
| Opportunités | Le modèle Opportunités capture les détails des opportunités commerciales tels que le type, l’étape de vente et les comptes associés. |
| Rôles de contact d’opportunité | Le modèle Rôles de contact d’opportunité capture des détails sur les rôles des prospects associés à une opportunité particulière. |
| Personnes | Le modèle Personnes capture les attributs des personnes individuelles, tels que les détails démographiques, les coordonnées et les préférences de consentement. |
| Adhésions aux programmes | Le modèle Adhésions au programme capture les détails des contacts associés à une campagne d’entreprise, notamment les cadences de formation et les réponses des contacts. |
| Programmes | Le modèle Programmes capture les détails des campagnes commerciales, tels que l’état, les canaux, les chronologies et les coûts. |
| Adhésions à liste statique | Le modèle Adhésions à liste statique capture les relations entre les personnes et leur appartenance dans des listes statiques. |
| Listes statiques | Le modèle Liste statique capture les listes instanciées de personnes pour des cas d’utilisation spécifiques. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] modèles B2B
Le tableau suivant décrit les modèles B2B disponibles pour la source [!DNL Salesforce].

| [!DNL Salesforce] modèles B2B | Description |
| --- | --- |
| Contact de compte | Le modèle Relation contact compte capture la relation entre un contact et un ou plusieurs comptes. |
| Comptes | Le modèle Compte capture les détails du compte commercial, tels que les informations démographiques, le lieu et les informations de facturation de l’entreprise. |
| Membres de la campagne | Le modèle Membres de la campagne capture la relation entre un prospect ou un contact individuel et une campagne [!DNL Salesforce] spécifique. |
| Campagnes | Le modèle Campagnes capture les détails du compte d’entreprise, tels que les informations démographiques, le lieu et les informations de facturation de l’entreprise. |
| Contacts | Le modèle Contact capture les attributs des contacts, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |
| Prospects | Le modèle Pistes capture les attributs des pistes, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |
| Opportunités | Le modèle Opportunités capture les détails des opportunités commerciales tels que le type, l’étape de vente et le compte associé. |
| Rôles de contact d’opportunité | Le modèle Rôles de contact d’opportunité capture des détails sur les rôles des prospects associés à une opportunité particulière. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] modèles B2C
Le tableau suivant décrit les modèles B2C disponibles pour la source [!DNL Salesforce].

| [!DNL Salesforce] modèles B2C | Description |
| --- | --- |
| Contact | Le modèle Contact capture les attributs des contacts, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |
| Lead | Le modèle de piste capture les attributs des pistes, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] modèles B2B
Le tableau suivant décrit les modèles B2B disponibles pour la source [!DNL Microsoft Dynamics].

| [!DNL Microsoft Dynamics] modèles B2B | Description |
| --- | --- |
| Comptes | Le modèle Compte capture les détails du compte commercial, tels que les informations démographiques, le lieu et les informations de facturation de l’entreprise. |
| Campagnes | Le modèle Campagnes capture les détails du compte d’entreprise, tels que les informations démographiques, le lieu et les informations de facturation de l’entreprise. |
| Contacts | Le modèle Contact capture les attributs des contacts, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |
| Prospects | Le modèle Pistes capture les attributs des pistes, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |
| Liste marketing | Le modèle Liste marketing capture un groupe de clients existants ou potentiels créés pour une campagne marketing ou à d’autres fins de vente. |
| Membres de la liste marketing | Les membres de la liste marketing capturent les détails d’un type d’enregistrement de client, tel que les prospects, les comptes ou les contacts, dans une liste marketing. |
| Opportunités | Le modèle Opportunités capture les détails des opportunités commerciales tels que le type, l’étape de vente et le compte associé. |
| Rôles de contact d’opportunité | Le modèle Rôles de contact d’opportunité capture des détails sur les rôles des prospects associés à une opportunité particulière. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] modèles B2C
Le tableau suivant décrit les modèles B2C disponibles pour la source [!DNL Microsoft Dynamics].

| [!DNL Microsoft Dynamics] modèles B2C | Description |
| --- | --- |
| Contact | Le modèle Contact capture les attributs des contacts, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |
| Lead | Le modèle de piste capture les attributs des pistes, tels que les détails démographiques, les coordonnées et les entités commerciales associées. |

{style="table-layout:auto"}

+++

Selon le type d’entreprise sélectionné, une liste de modèles s’affiche. Sélectionnez l’icône d’aperçu ![icône d’aperçu](../../images/tutorials/templates/preview-icon.png) en regard d’un nom de modèle pour prévisualiser des données d’exemple du modèle.

![Une liste de modèles avec l’icône d’aperçu mise en surbrillance.](../../images/tutorials/templates/templates.png)

La fenêtre d’aperçu s’affiche, vous permettant d’explorer et d’examiner des données d’exemple de votre modèle. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Compris]**.

![La fenêtre d’aperçu des données d’exemple.](../../images/tutorials/templates/preview-sample-data.png)

Sélectionnez ensuite dans la liste le modèle que vous souhaitez utiliser. Vous pouvez sélectionner plusieurs modèles et créer plusieurs flux de données à la fois. Cependant, un modèle ne peut être utilisé qu’une seule fois par compte. Une fois les modèles sélectionnés, cliquez sur **[!UICONTROL Terminer]** et patientez quelques instants le temps que les ressources se génèrent.

Si vous sélectionnez un ou des éléments partiels dans la liste des modèles disponibles, tous les schémas B2B et les espaces de noms d’identité seront quand même générés afin de garantir que les relations B2B entre les schémas soient correctement configurées.

>[!NOTE]
>
>Les modèles déjà utilisés seront désactivés de la sélection.

![La liste des modèles avec le modèle Rôle de contact d’opportunité sélectionné.](../../images/tutorials/templates/select-template.png)

### Définir un planning

Les sources [!DNL Microsoft Dynamics] et [!DNL Salesforce] prennent toutes deux en charge les flux de données de planification.

Utilisez l’interface de planification pour configurer un planning d’ingestion pour vos flux de données. Définissez la fréquence d’ingestion sur **Once** pour créer une ingestion unique.

![ Interface de planification pour les modèles Dynamics et Salesforce.](../../images/tutorials/templates/schedule.png)

Vous pouvez également définir la fréquence d&#39;ingestion sur **Minute**, **Heure**, **Jour** ou **Semaine**. Si vous planifiez votre flux de données pour plusieurs assimilations, vous devez définir un intervalle pour établir une période entre chaque ingestion. Par exemple, une fréquence d’ingestion définie sur **Heure** et un intervalle défini sur **15** signifie que votre flux de données est planifié pour ingérer des données toutes les **15 heures**.

Au cours de cette étape, vous pouvez également activer le **renvoi** et définir une colonne pour l’ingestion incrémentielle de données. Le renvoi est utilisé pour ingérer des données historiques, tandis que la colonne que vous définissez pour l’ingestion incrémentielle permet de différencier les nouvelles données des données existantes.

Une fois que vous avez terminé la configuration de votre planning d&#39;ingestion, sélectionnez **[!UICONTROL Terminer]**.

![ L’interface de planification pour les modèles Dynamics et Salesforce avec le renvoi activé.](../../images/tutorials/templates/backfill.png)

### Vérifier les ressources {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Vérifier vos ressources générées automatiquement"
>abstract="La génération de toutes les ressources peut prendre jusqu’à cinq minutes. Si vous choisissez de quitter la page, une notification vous sera envoyée pour revenir une fois les ressources terminées. Vous pouvez vérifier les ressources une fois qu’elles ont été générées et effectuer des configurations supplémentaires dans votre flux de données à tout moment."

La page [!UICONTROL Vérifier les ressources de modèle] affiche les ressources générées automatiquement dans le cadre de votre modèle. Dans cette page, vous pouvez afficher les schémas, les jeux de données, les espaces de noms d’identité et les flux de données générés automatiquement associés à votre connexion source. La génération de toutes les ressources peut prendre jusqu’à cinq minutes. Si vous choisissez de quitter la page, une notification vous sera envoyée pour revenir une fois les ressources terminées. Vous pouvez vérifier les ressources une fois qu’elles ont été générées et effectuer des configurations supplémentaires dans votre flux de données à tout moment.

Par défaut, les flux de données générés automatiquement sont définis sur un état de brouillon afin de permettre une personnalisation plus poussée des configurations, telles que les règles de mappage ou les fréquences planifiées. Sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez **[!UICONTROL Prévisualiser les mappages]** pour afficher les jeux de mappages créés pour votre flux de données de brouillon.

![Une fenêtre déroulante avec l’option Prévisualiser les mappages sélectionnée.](../../images/tutorials/templates/preview.png)

Une page d’aperçu s’affiche, vous permettant d’examiner la relation de mappage entre vos champs de données sources et vos champs de schéma cibles. Une fois que vous avez consulté les mappages de votre flux de données. Sélectionnez **[!UICONTROL J’ai compris.]**

![La fenêtre de prévisualisation du mappage.](../../images/tutorials/templates/preview-mappings.png)

Vous pouvez mettre à jour vos flux de données à tout moment après leur exécution. Sélectionnez les points de suspension (`...`) à côté du nom du flux de données, puis sélectionnez **[!UICONTROL Mettre à jour le flux de données]**. Vous accédez à la page du processus des sources dans laquelle vous pouvez mettre à jour les détails de votre flux de données, y compris les paramètres d’ingestion partielle, les diagnostics d’erreur et les notifications d’alerte, ainsi que le mappage de votre flux de données.

Vous pouvez utiliser la vue de l’éditeur de schémas pour mettre à jour votre schéma généré automatiquement. Consultez le guide sur l’[utilisation de l’éditeur de schéma](../../../xdm/tutorials/create-schema-ui.md) pour plus d’informations.

![Une fenêtre déroulante avec l’option Mettre à jour les flux de données sélectionnée.](../../images/tutorials/templates/update.png)

>[!TIP]
>
>Vous pouvez accéder à votre flux de données de brouillon via la page de catalogue [!UICONTROL Flux de données] de l’espace de travail des sources. Sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur, puis sélectionnez le flux de données à mettre à jour dans la liste.
>
>![Liste des flux de données existants dans le catalogue des flux de données de l’espace de travail des sources.](../../images/tutorials/templates/dataflows.png)

### Publish de votre flux de données

Commencez le processus de publication en parcourant le workflow des sources. Après avoir sélectionné [!UICONTROL Mettre à jour le flux de données], vous êtes dirigé vers l’étape *[!UICONTROL Ajouter des données]* du workflow. Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![L’étape d’ajout de données pour un flux de données de brouillon](../../images/tutorials/templates/continue-draft.png)

Ensuite, confirmez les détails de votre flux de données et configurez les paramètres pour les diagnostics d’erreur, l’ingestion partielle et les notifications d’alerte. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Étape de détail du flux de données pour un flux de données de brouillon.](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>Vous pouvez à tout moment sélectionner **[!UICONTROL Enregistrer en tant que brouillon]** pour arrêter et enregistrer les modifications que vous avez apportées à votre flux de données.

L’étape de mappage s’affiche. Pendant cette étape, vous pouvez reconfigurer les configurations de mappage de votre flux de données. Pour obtenir un guide complet sur les fonctions de prép de données utilisées pour le mappage, consultez le [guide de l’interface utilisateur de prép de données](../../../data-prep/ui/mapping.md).

![Étape de mappage d’un flux de données de brouillon.](../../images/tutorials/templates/mapping.png)

Enfin, passez en revue les détails de votre flux de données, puis sélectionnez **[!UICONTROL Enregistrer et ingérer]** pour publier votre brouillon.

![Étape de révision d’un flux de données de brouillon.](../../images/tutorials/templates/review.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez désormais créé des flux de données, ainsi que des ressources telles que des schémas, des jeux de données et des espaces de noms d’identité à l’aide de modèles. Pour obtenir des informations générales sur les sources, consultez la [présentation des sources](../../home.md).

## Alertes et notifications {#alerts-and-notifications}

Les modèles sont pris en charge par les alertes Adobe Experience Platform. Vous pouvez utiliser le panneau de notifications pour recevoir des mises à jour sur l’état de vos ressources et également revenir à la page de révision.

Sélectionnez l’icône de notification dans l’en-tête supérieur de l’interface utilisateur de Platform, puis sélectionnez l’alerte de statut pour afficher les ressources que vous souhaitez consulter.

![Le panneau des notifications de l’interface utilisateur de Platform avec une notification signalant l’échec d’un flux de données mise en surbrillance.](../../images/tutorials/templates/notifications.png)

Vous pouvez mettre à jour les paramètres d’alerte de vos modèles afin de recevoir des notifications par courrier électronique et dans Platform sur l’état de vos flux de données. Pour plus d’informations sur la configuration des alertes, consultez le guide sur [l’abonnement aux alertes pour les flux de données de sources](../ui/alerts.md).