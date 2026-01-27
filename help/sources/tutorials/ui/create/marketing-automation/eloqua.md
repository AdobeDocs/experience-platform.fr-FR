---
title: Connecter Oracle Eloqua (V2) à Experience Platform dans l’interface utilisateur
description: Découvrez comment connecter votre compte Oracle Eloqua à Experience Platform dans l’interface utilisateur.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 7%

---

# Connexion d’[!DNL Oracle Eloqua] (V2) à Experience Platform dans l’interface utilisateur

Le connecteur source [!DNL Oracle Eloqua (V2)] vous permet de connecter votre compte Oracle Eloqua à Adobe Experience Platform, ce qui permet une ingestion automatisée et évolutive des données marketing B2B essentielles, notamment les contacts, les comptes, les campagnes et les activités d’engagement.

Utilisez ce connecteur source pour configurer une authentification sécurisée, sélectionner les entités de données Eloqua exactes dont vous avez besoin et les mapper à des schémas de modèle de données d’expérience (XDM) normalisés. Des options de planification flexibles vous permettent de configurer les chargements de données initiaux et les synchronisations incrémentielles récurrentes, en veillant à ce que vos données marketing restent à jour et exploitables.

Basé sur le framework d’ingestion d’entreprise d’Adobe, le connecteur source [!DNL Oracle Eloqua (V2)] fournit une base fiable et extensible pour l’optimisation des campagnes, la mesure des performances et la personnalisation cross-canal.

Lisez ce guide pour savoir comment connecter votre compte [!DNL Oracle Eloqua] à Adobe Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur d’Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Collecter les informations d’identification requises {#credentials}

Lisez la [[!DNL Eloqua] présentation](../../../../connectors/marketing-automation/eloqua.md) pour plus d’informations sur l’authentification.

## Parcourir le catalogue des sources {#catalog}

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]*. Choisissez une catégorie ou utilisez la barre de recherche pour trouver votre source.

Pour vous connecter à [!DNL Eloqua], accédez à la catégorie *[!UICONTROL Marketing Automation]* , sélectionnez la carte source **[!UICONTROL (V2) Oracle Eloqua]**, puis sélectionnez **[!UICONTROL Set up]**.

>[!TIP]
>
>Les sources du catalogue affichent l’option **[!UICONTROL Set up]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois un compte authentifié créé, cette option devient **[!UICONTROL Add data]**.

![La carte source Eloqua dans le catalogue des sources avec le bouton Configurer en surbrillance.](../../../../images/tutorials/create/eloqua/catalog.png)

## Utiliser un compte existant {#existing}

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Existing account]**, puis sélectionnez le compte [!DNL Eloqua] à utiliser.

![L’option Compte existant sélectionnée dans l’interface de création de compte.](../../../../images/tutorials/create/eloqua/existing.png)

## Créer un nouveau compte {#new}

Pour créer un compte, sélectionnez **[!UICONTROL New account]** et indiquez un nom et une description sous votre [!UICONTROL Source connection details]. Ensuite, sous [!UICONTROL Account authentication], indiquez les valeurs de vos **ID client**, **Secret client**, **Nom d’utilisateur**, **Mot de passe** et **Point d’entrée de base**. Vous pouvez lire le [guide d’authentification](../../../../connectors/marketing-automation/eloqua.md) pour plus d’informations sur ces informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connect to source]** et patientez quelques secondes le temps que votre connexion s’établisse.

![Nouvelle interface de compte avec des champs pour les détails de connexion source et les informations d’authentification.](../../../../images/tutorials/create/eloqua/new.png)

## Sélectionner les données

Utilisez l’interface de sélection des données pour sélectionner l’entité [!DNL Eloqua] à ingérer dans Experience Platform.

>[!TIP]
>
>Lors de la sélection des données, vous remarquerez que, à l’exception des campagnes, les autres entités affichent des données d’exemple représentatives. Cette approche vous permet de prévisualiser les champs et la structure disponibles, car [!DNL Eloqua] API publiques récupèrent actuellement des données réelles pour les campagnes uniquement. Pour les entités restantes, des exemples de données sont fournis pour prendre en charge votre workflow de configuration.

![L’interface de sélection des données affichant les entités de données Eloqua disponibles.](../../../../images/tutorials/create/eloqua/select-data.png)

## Détails du jeu de données et du flux de données {#details}

Ensuite, vous devez fournir des informations sur votre jeu de données et votre flux de données. Au cours de cette étape, vous pouvez utiliser un jeu de données existant ou en créer un nouveau. De plus, vous pouvez éventuellement activer votre jeu de données pour l’ingestion dans le profil client en temps réel au cours de cette étape.

![Interface des détails du jeu de données et du flux de données avec des options pour configurer les propriétés du jeu de données.](../../../../images/tutorials/create/eloqua/details.png)

## Mappage {#mapping}

Les mappages pour les [!DNL Eloqua] sont organisés en quatre types d’entités principaux :

* **Comptes** - Enregistrements d’entreprise/d’organisation provenant de l’[!DNL Eloqua].
* **Activités** - Activités marketing et événements d’engagement de [!DNL Eloqua].
* **Campagnes** - Enregistrements de campagne marketing à partir de [!DNL Eloqua].
* **Contacts** - Enregistrements de personne individuels de [!DNL Eloqua].

Si vous avez besoin d’accéder à des champs supplémentaires par rapport à ceux fournis par défaut, vous pouvez ajouter ces champs à l’aide du processus de mappage de la préparation des données dans Experience Platform. Si le schéma par défaut (standard) ne prend pas en charge certains de vos champs obligatoires, vous avez la possibilité de définir un schéma personnalisé dans Experience Platform. Utilisez cette fonctionnalité pour créer et mapper les champs nécessaires afin d’ingérer en toute transparence toutes les données pertinentes de [!DNL Eloqua] dans Experience Platform.

Résumé des étapes suivantes :

* Passez en revue les champs mappés par défaut disponibles avec l’intégration.
* Pendant l’étape de mappage, incluez tous les champs supplémentaires nécessaires dans [!DNL Eloqua].
* Si de nouveaux champs ne sont pas présents dans le schéma standard, étendez ou créez un schéma personnalisé dans Experience Platform qui inclut ces champs.
* Effectuez le mappage pour vous assurer que toutes les données souhaitées sont ingérées.

Pour vous assurer que les informations de votre CRM externe sont reflétées avec précision, utilisez simplement la fonction de champ calculé dans la préparation des données afin de mettre à jour l’espace réservé `{CRM_INSTANCE_ID}` avec l’identifiant d’instance CRM spécifique dans le champ de données source. Vous avez ainsi la possibilité d’adapter l’intégration à la configuration unique de votre entreprise.

Pour utiliser l’éditeur de champ calculé, sélectionnez le champ source à mettre à jour.

![Le champ source Eloqua avec des champs calculés.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

Pour les utilisateurs [!DNL Salesforce], utilisez l’éditeur de champ calculé et mettez à jour la `{CRM_INSTANCE_ID}` avec l’ID d’instance approprié.

![Champ calculé pour Salesforce.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

Pour les utilisateurs [!DNL Microsoft], utilisez l’éditeur de champ calculé et mettez à jour la `{CRM_INSTANCE_ID}` avec l’ID d’instance approprié.

![Champ calculé pour Dynamics.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

Une fois la mise à jour des champs calculés terminée, sélectionnez **[!UICONTROL Next]** pour continuer.

![L’interface de mappage affichant les mappages de champs pour les entités de données Eloqua.](../../../../images/tutorials/create/eloqua/mapping.png)

## Planification

>[!NOTE]
>
>Voici les champs delta utilisés en interne pour le chargement incrémentiel des données :
>
>* **Contacts :** `C_DateModified`
>* **Comptes:** `M_DateModified`
>* **Activité:** `CreatedAt`
>* **Objets personnalisés :** `UpdatedAt`
>* **Campaign:** `updatedAt`

Une fois le mappage terminé, vous pouvez configurer un planning d’ingestion pour votre flux de données. Définissez votre [!UICONTROL Frequency] sur `Once` pour configurer une exécution d’ingestion unique. Pour une ingestion incrémentielle, vous pouvez définir votre [!UICONTROL Frequency] sur `Hour`, `Day` ou `Week`. Lors de l’utilisation de l’ingestion incrémentielle, vous devez également configurer le [!UICONTROL Interval] pour définir le temps écoulé entre les exécutions d’ingestion. Par exemple, une fréquence d’ingestion définie sur `Day` et un intervalle défini sur `15` signifie que votre flux de données est planifié pour ingérer des données tous les 15 jours.

La fréquence d’ingestion par minute n’est pas disponible pour la source de [!DNL Eloqua]. La planification la plus fréquente que vous pouvez choisir est horaire. Sélectionnez une planification qui correspond à vos besoins en matière de fraîcheur des données. Gardez à l’esprit que le choix d’une planification plus fréquente augmentera les coûts de calcul.

![L’interface de planification avec des options pour configurer la fréquence et l’intervalle d’ingestion.](../../../../images/tutorials/create/eloqua/scheduling.png)

## Réviser

Une fois le planning d’ingestion configuré, utilisez l’interface [!UICONTROL Review] pour confirmer les détails de votre flux de données. Sélectionnez **[!UICONTROL Finish]** pour terminer la configuration et patientez quelques instants le temps que votre flux de données se lance.

![L’interface de révision affichant un résumé de la configuration du flux de données avant la fin.](../../../../images/tutorials/create/eloqua/review.png)

## Surveiller

Une fois le flux de données sélectionné, il effectue un renvoi unique des données, puis une synchronisation incrémentielle selon le planning spécifié. Vous pouvez surveiller le statut de la synchronisation en accédant au flux de données. Pour plus d’informations, consultez le guide sur la [surveillance des flux de données des sources dans l’interface utilisateur](../../../../../dataflows/ui/monitor-sources.md).

## Étapes suivantes

Vous avez maintenant terminé l’installation et la configuration de votre source de [!DNL Eloqua] dans Experience Platform. Une fois votre flux de données établi, vos données [!DNL Eloqua] seront ingérées en fonction du planning choisi et mappées aux schémas du modèle de données d’expérience (XDM) standard. Continuez à surveiller vos flux de données et à explorer vos données ingérées dans Platform pour obtenir des informations et activer vos cas d’utilisation marketing. Pour obtenir des configurations et un dépannage plus avancés, consultez la documentation associée ou contactez les ressources d’assistance Adobe.

Pour plus d’informations, consultez la documentation suivante :

* [Présentation des sources](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
