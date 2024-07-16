---
title: Création d’une connexion Source Marketo Engage et d’un flux de données dans l’interface utilisateur
description: Ce tutoriel décrit les étapes à suivre pour créer une connexion source Marketo Engage et un flux de données dans l’interface utilisateur afin d’importer des données B2B dans Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 46%

---

# Créer une connexion source et un flux de données [!DNL Marketo Engage] dans l’interface utilisateur

>[!IMPORTANT]
>
>Avant de créer une connexion source [!DNL Marketo Engage] et un flux de données, vous devez d’abord vous assurer que [ a mappé votre ID d’organisation d’Adobe ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) dans [!DNL Marketo]. De plus, vous devez également vous assurer que vous avez renseigné automatiquement vos  [!DNL Marketo] espaces de noms et schémas B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) avant de créer une connexion source et un flux de données.[

Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Marketo Engage] (ci-après dénommé « [!DNL Marketo] ») dans l’interface utilisateur pour importer des données B2B dans Adobe Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Espaces de noms B2B et utilitaire de génération automatique de schéma](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) : les espaces de noms B2B et l’utilitaire de génération automatique de schémas vous permettent d’utiliser [!DNL Postman] pour générer automatiquement des valeurs pour vos espaces de noms et schémas B2B. Vous devez d’abord renseigner vos espaces de noms et schémas B2B, avant de créer une connexion source et un flux de données [!DNL Marketo].
* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données d’expérience client.
   * [Créer et modifier des schémas dans l’interface utilisateur](../../../../../xdm/ui/resources/schemas.md) : découvrez comment créer et modifier des schémas dans l’interface utilisateur.
* [Espaces de noms d’identité](../../../../../identity-service/features/namespaces.md) : les espaces de noms d’identité sont des composants d’[!DNL Identity Service] qui servent d’indicateurs du contexte auquel une identité se rapporte. Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL Marketo] sur Experience Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---- | ---- |
| `munchkinId` | L’identifiant Munchkin est l’identifiant unique d’une instance [!DNL Marketo] spécifique. |
| `clientId` | Identifiant client unique de l’instance [!DNL Marketo]. |
| `clientSecret` | Secret client unique de l’instance [!DNL Marketo]. |

Pour plus d’informations sur l’acquisition de ces valeurs, consultez le [[!DNL Marketo] guide dʼauthentification](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes de la section suivante.

## Connecter votre compte [!DNL Marketo]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie *Adobe applications*, sélectionnez **[!UICONTROL Marketo Engage]**, puis **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les sources dans le catalogue des sources affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée n’a pas encore de compte authentifié. Une fois qu’il existe un compte authentifié, cette option devient **[!UICONTROL Ajouter des données]**.

![Catalogue des sources avec la source du Marketo Engage sélectionnée.](../../../../images/tutorials/create/marketo/catalog.png)

La page **[!UICONTROL Connexion au compte Marketo Engage]** s’affiche. Sur cette page, vous pouvez utiliser un nouveau compte ou accéder à un compte existant.

>[!BEGINTABS]

>[!TAB Créer un compte]

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et fournissez un nom, une description facultative et vos informations d’identification.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte pour l’authentification d’un nouveau compte Marketo.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Utiliser un compte existant]

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** , puis le compte à utiliser dans le catalogue de comptes existant.

Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![ Interface du compte existant dans laquelle vous pouvez sélectionner un compte Marketo existant.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Sélectionner un jeu de données

Une fois le compte [!DNL Marketo] créé, une interface sʼaffiche pour explorer les jeux de données [!DNL Marketo].

La moitié gauche de l’interface est un navigateur de répertoire qui affiche les 10 jeux de données [!DNL Marketo]. Une connexion source [!DNL Marketo] pleinement fonctionnelle nécessite l’ingestion des neuf jeux de données différents. Si vous utilisez également la fonctionnalité Account-Based Marketing (ABM) [!DNL Marketo], vous devez créer un 10e flux de données pour ingérer le jeu de données [!UICONTROL Comptes nommés].

>[!NOTE]
>
>À des fins de concision, le tutoriel suivant utilise [!UICONTROL Opportunités] comme exemple, mais les étapes décrites ci-dessous s’appliquent aux 10 jeux de données [!DNL Marketo].

Sélectionnez le jeu de données à ingérer. Cela met à jour l’interface pour afficher un aperçu de votre jeu de données. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Interface de prévisualisation](../../../../images/tutorials/create/marketo/preview.png)

## Fournir des détails sur les jeux de données et les flux de données {#provide-dataset-and-dataflow-details}

Ensuite, vous devez fournir des informations sur votre jeu de données et votre flux de données.

### Détails du jeu de données {#dataset-details}

Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les données correctement ingérées dans Experience Platform sont stockées dans le lac de données sous la forme de jeux de données. Au cours de cette étape, vous pouvez créer un nouveau jeu de données ou utiliser un jeu de données existant.

>[!BEGINTABS]

>[!TAB Utiliser un nouveau jeu de données]

Pour utiliser un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**, puis fournissez un nom et une description facultative de votre jeu de données. Vous devez également sélectionner un schéma de modèle de données d’expérience (XDM) auquel votre jeu de données adhère.

![Nouvelle interface de sélection de jeux de données.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Utiliser un jeu de données existant]

Si vous disposez déjà d’un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**, puis utilisez l’option **[!UICONTROL Recherche avancée]** pour afficher une fenêtre de tous les jeux de données de votre organisation, y compris leurs détails respectifs, par exemple s’ils sont activés pour l’ingestion dans Real-Time Customer Profile ou non.

![Interface de sélection de jeu de données existante.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Configurations de flux de données {#dataflow-configurations}

>[!IMPORTANT]
>
>La source [!DNL Marketo] utilise l’ingestion par lots pour ingérer tous les enregistrements historiques et utilise l’ingestion par flux pour les mises à jour en temps réel. Cela permet à la source de continuer la diffusion en continu tout en ingérant des enregistrements erronés. Activez le bouton (bascule) **[!UICONTROL Ingestion partielle]**, puis définissez le [!UICONTROL Seuil d’erreur %] au maximum pour empêcher l’échec du flux de données.

Si votre jeu de données est activé pour Real-time Customer Profile, vous pouvez, au cours de cette étape, activer le **[!UICONTROL jeu de données Profile]** pour activer vos données pour l’ingestion par profil. Vous pouvez également utiliser cette étape pour activer les **[!UICONTROL {diagnostics d’erreur]** et l’ **[!UICONTROL ingestion partielle]**.

* **[!UICONTROL Diagnostic d’erreur]** : sélectionnez **[!UICONTROL Diagnostic d’erreur]** pour demander à la source de produire des diagnostics d’erreur que vous pourrez ensuite référencer lors de la surveillance de l’activité de votre jeu de données et de l’état du flux de données.
* **[!UICONTROL Ingestion partielle]** : [L’ingestion par lots partielle](../../../../../ingestion/batch-ingestion/partial.md) permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil configurable. Cette fonctionnalité vous permet d’ingérer toutes vos données précises dans Experience Platform, tandis que toutes vos données incorrectes sont traitées par lots séparément avec des informations sur les raisons de leur non-validité.

Au cours de cette étape, vous pouvez activer **[!UICONTROL Exemple de flux de données]** pour limiter l’ingestion de données et éviter les coûts supplémentaires liés à l’ingestion de toutes les données historiques, y compris les identités de personne.

>[!BEGINSHADEBOX]

**Guide rapide sur l’utilisation d’exemples de flux de données**

Un exemple de flux de données est une configuration que vous pouvez définir pour votre flux de données [!DNL Marketo] afin de limiter votre taux d’ingestion, puis d’essayer des fonctionnalités Experience Platform sans avoir à ingérer de grandes quantités de données.

* Activez les exemples de flux de données pour limiter les données historiques en ingérant jusqu’à 100 000 enregistrements (à partir du plus grand ID d’enregistrement) ou jusqu’aux 10 derniers jours d’activité pendant la tâche de renvoi.
* Lors de l’utilisation de l’exemple de configuration de flux de données pour toutes les entités B2B, vous devez tenir compte du fait qu’il est possible que certains enregistrements associés soient manquants, car l’historique complet des données source n’est pas ingéré.

>[!ENDSHADEBOX]

![La section des configurations de flux de données de la page des détails du flux de données.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

De plus, si vous ingérez des données du jeu de données des entreprises, vous pouvez activer l’option **[!UICONTROL Exclure les comptes non réclamés]** pour exclure les comptes non réclamés de l’ingestion.

Lorsque des individus remplissent un formulaire, [!DNL Marketo] crée un enregistrement de compte fantôme basé sur le nom de la société qui ne contient aucune autre donnée. Pour les nouveaux flux de données, la bascule permettant d’exclure les comptes non réclamés est activée par défaut. Pour les flux de données existants, vous pouvez activer ou désactiver la fonctionnalité, avec des modifications s’appliquant aux données nouvellement ingérées et non aux données existantes.

![Exclure les comptes non réclamés](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Mappez vos champs sources du jeu de données [!DNL Marketo] aux champs XDM cibles.

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Chaque jeu de données [!DNL Marketo] comporte ses propres règles de mappage spécifiques à suivre. Pour plus d’informations sur le mappage de jeux de données [!DNL Marketo] à XDM, consultez les sections suivantes :

* [Activités](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programmes](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Abonnements au programme](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Sociétés](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Listes statiques](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Abonnements à des listes statiques](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Comptes désignés](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Opportunités](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Rôles de contact d’opportunité](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personnes](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface de mappage, consultez le [Guide de l’interface utilisateur de la préparation de données](../../../../../data-prep/ui/mapping.md).

![Interface de mappage pour les données Marketo.](../../../../images/tutorials/create/marketo/mapping.png)

Une fois vos jeux de mappages prêts, cliquez sur **[!UICONTROL Suivant]** et patientez quelques instants le temps que le flux de données soit créé.

## Vérifier le flux de données

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant de l’entité source choisie et le nombre de colonnes au sein de cette entité source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez révisé votre flux de données, sélectionnez **[!UICONTROL Enregistrer et ingérer]** et patientez quelques instants le temps que le flux de données soit créé.

![Page de révision dans laquelle vous pouvez confirmer les détails de votre flux de données avant l’ingestion.](../../../../images/tutorials/create/marketo/review.png)

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées et afficher les informations relatives au taux d’ingestion, aux succès et aux erreurs. Pour plus d’informations sur la surveillance des flux de données, suivez le tutoriel sur la [surveillance des flux de données dans l’interface utilisateur](../../../../../dataflows/ui/monitor-sources.md).

## Supprimer les attributs

Les attributs personnalisés des jeux de données ne peuvent pas être masqués ni supprimés rétroactivement. Si vous souhaitez masquer ou supprimer un attribut personnalisé d’un jeu de données existant, vous devez créer un nouveau jeu de données sans cet attribut personnalisé, un nouveau schéma XDM et configurer un nouveau flux de données pour le nouveau jeu de données que vous souhaitez créer. Vous devez également désactiver ou supprimer le flux de données d’origine constitué du jeu de données et de l’attribut personnalisé que vous souhaitez masquer ou supprimer.

## Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail [!UICONTROL Flux de données]. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression de flux de données dans l’interface utilisateur](../../delete.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour ingérer des données B2B de votre source [!DNL Marketo Engage] vers l’Experience Platform.

## Annexe {#appendix}

Les sections suivantes contiennent des instructions supplémentaires que vous pouvez suivre lors de l’utilisation de la source [!DNL Marketo].

### Messages d’erreur dans l’interface utilisateur {#error-messages}

Les messages d’erreur suivants s’affichent dans l’interface utilisateur lorsque Platform détecte des problèmes liés à votre configuration :

#### [!DNL Munchkin ID] n’est pas mappé à l’organisation appropriée

L’authentification sera refusée si votre [!DNL Munchkin ID] n’est pas mappé à l’organisation Platform que vous utilisez. Configurez le mappage entre votre [!DNL Munchkin ID] et votre organisation à l’aide de l’ [[!DNL Marketo] interface](https://app-sjint.marketo.com/#MM0A1).

![Message d&#39;erreur indiquant que l&#39;instance Marketo n&#39;est pas correctement mappée à l&#39;organisation de l&#39;Adobe.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Identité du Principal manquante

Un flux de données n’enregistre pas et n’ingère pas si une identité principale est manquante. Assurez-vous que [une identité principale existe dans votre schéma XDM](../../../../../xdm/tutorials/create-schema-ui.md) avant de tenter de configurer un flux de données.

![Message d’erreur indiquant que l’identité principale est absente du schéma XDM.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

