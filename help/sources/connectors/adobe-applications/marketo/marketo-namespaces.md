---
title: Espaces de noms et schémas B2B
description: Ce document fournit un aperçu des espaces de noms personnalisés requis lors de la création d’un connecteur source B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 14%

---

# Espaces de noms et schémas B2B

>[!NOTE]
>
>Vous pouvez utiliser des modèles dans l’interface utilisateur de Adobe Experience Platform pour accélérer la création de ressources pour les données B2B et B2C. Pour plus d’informations, consultez le guide sur [utilisation de modèles dans l’interface utilisateur de Platform](../../../tutorials/ui/templates.md).

Ce document fournit des informations sur la configuration sous-jacente des espaces de noms et des schémas à utiliser avec des sources B2B. Ce document fournit également des détails sur la configuration de votre utilitaire d’automatisation Postman requis pour générer des espaces de noms et des schémas B2B.

>[!IMPORTANT]
>
>Vous devez avoir accès à [Adobe Real-time Customer Data Platform version B2B](../../../../rtcdp/b2b-overview.md) pour que les schémas B2B participent à [Profil client en temps réel](../../../../profile/home.md).

## Configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma

La première étape de l’utilisation de l’espace de noms B2B et de l’utilitaire de génération automatique de schéma consiste à configurer votre console de développement Platform et [!DNL Postman] environnement.

- Vous pouvez télécharger la collection et l’environnement de génération automatique de l’espace de noms et du schéma à partir de ce [Référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Pour plus d’informations sur l’utilisation des API Platform, y compris sur la manière de rassembler des valeurs pour les en-têtes requis et de lire des exemples d’appels API, consultez le guide sur [Prise en main des API Platform](../../../../landing/api-guide.md).
- Pour plus d’informations sur la génération de vos informations d’identification pour les API Platform, consultez le tutoriel sur [authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md).
- Pour plus d’informations sur la configuration [!DNL Postman] pour les API Platform, consultez le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../../landing/postman.md).

Avec une console de développement Platform et [!DNL Postman] configuré. vous pouvez maintenant commencer à appliquer les valeurs d’environnement appropriées à votre [!DNL Postman] environnement.

Le tableau suivant contient des exemples de valeurs ainsi que des informations supplémentaires sur le remplissage de vos [!DNL Postman] environnement :

| Variable | Description | Exemple |
| --- | --- | --- |
| `CLIENT_SECRET` | Identifiant unique utilisé pour générer votre `{ACCESS_TOKEN}`. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Le jeton Web JSON (JWT) est un identifiant d’authentification utilisé pour générer votre {ACCESS_TOKEN}. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md) pour plus d’informations sur la manière de générer votre `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identifiant unique utilisé pour authentifier les appels vers les API Experience Platform. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Jeton d’autorisation requis pour terminer les appels vers les API Experience Platform. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Le `global` conteneur contient toutes les classes fournies par les Adobes standard et les partenaires Experience Platform, les groupes de champs de schéma, les types de données et les schémas. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur `global`. | `global` |
| `PRIVATE_KEY` | Informations d’identification utilisées pour authentifier vos [!DNL Postman] aux API Experience Platform. Consultez le tutoriel sur la configuration de Developer Console et [configuration de Developer Console et [!DNL Postman]](../../../../landing/postman.md) pour obtenir des instructions sur la manière de récupérer votre {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Informations d’identification utilisées pour l’intégration à Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Le système Identity Management (IMS) fournit la structure d’authentification des services Adobe. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Personne morale pouvant posséder ou accorder une licence pour des produits et des services et permettre l’accès à ses membres. Voir le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../../landing/postman.md) pour obtenir des instructions sur la manière de récupérer votre `{ORG_ID}` informations. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nom de la partition d’environnement de test virtuel que vous utilisez. | `prod` |
| `TENANT_ID` | Identifiant utilisé pour vous assurer que les ressources que vous créez sont des espaces de noms corrects et qu’ils sont contenus dans votre organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Le point de terminaison d’URL vers lequel vous effectuez des appels d’API. Cette valeur est fixe et est toujours définie sur : `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Exécution des scripts

Avec votre [!DNL Postman] configuration de la collection et de l’environnement, vous pouvez désormais exécuter le script via la [!DNL Postman] .

Dans le [!DNL Postman] , sélectionnez le dossier racine de l’utilitaire de génération automatique, puis sélectionnez **[!DNL Run]** dans l’en-tête supérieur.

![root-folder](../images/marketo/root-folder.png)

Le [!DNL Runner] s’affiche. À partir de là, assurez-vous que toutes les cases à cocher sont sélectionnées, puis sélectionnez **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

Une requête réussie crée les espaces de noms et les schémas requis pour B2B.

## Espaces de noms B2B

Les espaces de noms d’identité sont un composant de [[!DNL Identity Service]](../../../../identity-service/home.md) qui servent à distinguer le contexte ou le type d’identité. Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. Voir [présentation des espaces de noms](../../../../identity-service/namespaces.md) pour plus d’informations.

Les espaces de noms B2B sont utilisés dans l’identité Principale de l’entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de noms B2B.

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Nom d’affichage | Symbole d’identité | Type d’identité |
| --- | --- | --- |
| Personne B2B | `b2b_person` | `CROSS_DEVICE` |
| Compte B2B | `b2b_account` | `B2B_ACCOUNT` |
| Opportunité B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relation de personne d’opportunité B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campagne B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Membre de campagne B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Liste marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Membre de liste marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relation entre les personnes d’un compte B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## Schémas B2B

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](../../../../xdm/schema/composition.md).

Le tableau suivant contient des informations sur la configuration sous-jacente des schémas B2B.

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Nom du schéma | Classe de base | Groupes de champs | [!DNL Profile] schéma in | Identité principale | Espace de noms d’identité Principal | Identité secondaire | Espace de noms d’identité Secondaire | Relation | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Compte B2B | [Compte d’entreprise XDM](../../../../xdm/classes/b2b/business-account.md) | Détails du compte commercial XDM | Activé | `accountKey.sourceKey` dans la classe de base | Compte B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Compte B2B | <ul><li>`accountParentKey.sourceKey` dans le groupe de champs Détails du compte d’entreprise XDM</li><li>Propriété de destination : `/accountKey/sourceKey`</li><li>Type : un-à-un</li><li>Schéma de référence : Compte B2B</li><li>Espace de noms : Compte B2B</li></ul> |
| Personne B2B | [XDM Individual Profile](../../../../xdm/classes/individual-profile.md) | <ul><li>Détails de professionnel XDM</li><li>Composants de professionnel XDM</li><li>IdentityMap</li><li>Détails du consentement et des préférences</li></ul> | Activé | `b2b.personKey.sourceKey` dans le groupe de champs Détails de la personne professionnelle XDM | Personne B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` du groupe de champs Détails de la personne active XDM</li><li>`workEmail.address` du groupe de champs Détails de la personne active XDM</ol></li> | <ol><li>Personne B2B</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` du groupe de champs Composants de personne professionnelle XDM</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Compte B2B</li><li>Espace de noms : Compte B2B</li><li>Propriété de destination : accountKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| Opportunité B2B | [XDM Business Opportunity](../../../../xdm/classes/b2b/business-opportunity.md) | Détails des opportunités commerciales XDM | Activé | `opportunityKey.sourceKey` dans la classe de base | Opportunité B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Opportunité B2B | <ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Compte B2B</li><li>Espace de noms : Compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Opportunités</li></ul> |
| Relation de personne d’opportunité B2B | [Relation avec la personne de XDM Business Opportunity](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Aucun | Activé | `opportunityPersonKey.sourceKey` dans la classe de base | Relation de personne d’opportunité B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Relation de personne d’opportunité B2B | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : b2b.personKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Opportunités</li></ul>**Deuxième relation**<ul><li>`opportunityKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Opportunité B2B </li><li>Espace de noms : Opportunité B2B </li><li>Propriété de destination : `opportunityKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Opportunité</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| Campagne B2B | [XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) | Détails de XDM Business Campaign | Activé | `campaignKey.sourceKey` dans la classe de base | Campagne B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Campagne B2B |
| Membre de campagne B2B | [Membres de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) | Détails des membres XDM Business Campaign | Activé | `ccampaignMemberKey.sourceKey` dans la classe de base | Membre de campagne B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Membre de campagne B2B | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Campagnes</li></ul>**Deuxième relation**<ul><li>`campaignKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Campagne B2B</li><li>Espace de noms : Campagne B2B</li><li>Propriété de destination : `campaignKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Campagne</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| Liste marketing B2B | [Liste XDM Business Marketing](../../../../xdm/classes/b2b/business-marketing-list.md) | Aucun | Activé | `marketingListKey.sourceKey` dans la classe de base | Liste marketing B2B | Aucun | Aucun | Aucun | La liste statique n’est pas synchronisée à partir de [!DNL Salesforce] et ne possède donc pas d’identité secondaire. |
| Membre de liste marketing B2B | [Membres de la liste XDM Business Marketing](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Aucun | Activé | `marketingListMemberKey.sourceKey` dans la classe de base | Membre de liste marketing B2B | Aucun | Aucun | **Première relation**<ul><li>`PersonKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Listes marketing</li></ul>**Deuxième relation**<ul><li>`marketingListKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Liste marketing B2B</li><li>Espace de noms : Liste marketing B2B</li><li>Propriété de destination : `marketingListKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Liste marketing</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> | Le membre de liste statique n’est pas synchronisé à partir de [!DNL Salesforce] et ne possède donc pas d’identité secondaire. |
| Activité B2B | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visite WebPage</li><li>Nouvelle piste</li><li>Convertir le prospect</li><li>Ajouter à la liste</li><li>Supprimer de la liste</li><li>Ajouter à l’opportunité</li><li>Supprimer de l’opportunité</li><li>Formulaire rempli</li><li>Clics sur les liens</li><li>Email diffusé</li><li>Courrier électronique ouvert</li><li>Courrier électronique cliqué</li><li>Email bounce</li><li>Email Bounce Soft</li><li>Désabonnement du courrier électronique</li><li>Score modifié</li><li>Opportunité mise à jour</li><li>État dans la progression de la campagne modifiée</li><li>Identifiant de personne</li><li>URL web Marketo</li><li>Moment intéressant</li><li>Appelez Webhook</li><li>Modifier la date de campagne</li><li>Évaluation des recettes modifiée</li><li>Fusion des pistes</li><li>E-mails envoyés</li><li>Modification du flux de campagne</li><li>Ajouter à Campaign</li></ul> | Activé | `personKey.sourceKey` du groupe de champs Identifiant de personne | Personne B2B | Aucun | Aucun | **Première relation**<ul><li>`listOperations.listKey.sourceKey` field</li><li>Type : un-à-un</li><li>Schéma de référence : Liste marketing B2B</li><li>Espace de noms : Liste marketing B2B</li></ul>**Deuxième relation**<ul><li>`opportunityEvent.opportunityKey.sourceKey` field</li><li>Type : un-à-un</li><li>Schéma de référence : Opportunité B2B</li><li>Espace de noms : Opportunité B2B</li></ul>**Troisième relation**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` field</li><li>Type : un-à-un</li><li>Schéma de référence : Campagne B2B</li><li>Espace de noms : Campagne B2B</li></ul> | `ExperienceEvent` est différent des entités. L’identité de l’événement d’expérience est la personne qui a effectué l’activité. |
| Relation entre les personnes d’un compte B2B | [Relation avec la personne du compte d’entreprise XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mappage d’identités | Activé | `accountPersonKey.sourceKey` dans la classe de base | Relation entre les personnes d’un compte B2B | Aucun | Aucun | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.SourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personnes</li><li>Nom de la relation à partir du schéma de référence : Compte</li></ul>**Deuxième relation**<ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : Multiple-à-un</li><li>Schéma de référence : Compte B2B</li><li>Espace de noms : Compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |

{style="table-layout:auto"}

## Étapes suivantes

Pour savoir comment connecter votre [!DNL Marketo] data to Platform, consultez le tutoriel sur [création d’un connecteur source Marketo dans l’interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
