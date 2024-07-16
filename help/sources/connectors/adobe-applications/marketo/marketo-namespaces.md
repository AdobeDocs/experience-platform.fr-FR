---
title: Espaces de noms et schémas B2B
description: Ce document fournit un aperçu des espaces de noms personnalisés requis lors de la création d’un connecteur source B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 5e8bb04ca18159eab98b2f7f0bba8cb1488a1f26
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 18%

---

# Espaces de noms et schémas B2B

>[!NOTE]
>
>Vous pouvez utiliser des modèles dans l’interface utilisateur de Adobe Experience Platform pour accélérer la création de ressources pour les données B2B et B2C. Pour plus d’informations, consultez le guide sur l’ [utilisation de modèles dans l’interface utilisateur de Platform](../../../tutorials/ui/templates.md).

Ce document fournit des informations sur la configuration sous-jacente des espaces de noms et des schémas à utiliser avec des sources B2B. Ce document fournit également des détails sur la configuration de votre utilitaire d’automatisation Postman requis pour générer des espaces de noms et des schémas B2B.

>[!IMPORTANT]
>
>Vous devez avoir accès à [Adobe Real-Time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) pour que les schémas B2B puissent participer au [profil client en temps réel](../../../../profile/home.md).

## Configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma

La première étape de l’utilisation de l’espace de noms B2B et de l’utilitaire de génération automatique de schéma consiste à configurer votre console de développement Platform et votre environnement [!DNL Postman].

- Vous pouvez télécharger l’espace de noms et l’environnement de génération automatique de schémas à partir de ce [référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Pour plus d’informations sur l’utilisation des API Platform, y compris sur la manière de rassembler des valeurs pour les en-têtes requis et de lire des exemples d’appels API, consultez le guide de [prise en main des API Platform](../../../../landing/api-guide.md).
- Pour plus d’informations sur la génération de vos informations d’identification pour les API Platform, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md).
- Pour plus d’informations sur la configuration de [!DNL Postman] pour les API Platform, consultez le tutoriel sur la [configuration de la console de développement et [!DNL Postman]](../../../../landing/postman.md).

Avec une console de développement Platform et [!DNL Postman] configurée, vous pouvez maintenant commencer à appliquer les valeurs d’environnement appropriées à votre environnement [!DNL Postman].

Le tableau suivant contient des exemples de valeurs ainsi que des informations supplémentaires sur le remplissage de votre environnement [!DNL Postman] :

| Variable | Description | Exemple |
| --- | --- | --- |
| `CLIENT_SECRET` | Identifiant unique utilisé pour générer votre `{ACCESS_TOKEN}`. Pour plus d’informations sur la récupération de votre `{CLIENT_SECRET}`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md) . | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Le jeton Web JSON (JWT) est un identifiant d’authentification utilisé pour générer votre {ACCESS_TOKEN}. Pour plus d’informations sur la génération de votre `{JWT_TOKEN}`, consultez le tutoriel sur l’ [authentification et l’accès aux API Experience Platform](../../../../landing/api-authentication.md) . | `{JWT_TOKEN}` |
| `API_KEY` | Identifiant unique utilisé pour authentifier les appels vers les API Experience Platform. Pour plus d’informations sur la récupération de votre `{API_KEY}`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md) . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Jeton d’autorisation requis pour terminer les appels vers les API Experience Platform. Pour plus d’informations sur la récupération de votre `{ACCESS_TOKEN}`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md) . | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Concernant [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Le conteneur `global` contient toutes les classes d’Adobe standard et de partenaire Experience Platform fournies, les groupes de champs de schéma, les types de données et les schémas. Concernant [!DNL Marketo], cette valeur est fixe et est toujours définie sur `global`. | `global` |
| `PRIVATE_KEY` | Informations d’identification utilisées pour authentifier votre instance [!DNL Postman] auprès des API Experience Platform. Consultez le tutoriel sur la configuration de Developer Console et la [configuration de Developer Console et [!DNL Postman]](../../../../landing/postman.md) pour obtenir des instructions sur la récupération de votre {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Informations d’identification utilisées pour l’intégration à Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Le système Identity Management (IMS) fournit la structure d’authentification des services Adobe. Concernant [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Personne morale pouvant posséder ou accorder une licence pour des produits et des services et permettre l’accès à ses membres. Consultez le tutoriel sur la [configuration de Developer Console et [!DNL Postman]](../../../../landing/postman.md) pour obtenir des instructions sur la récupération de vos informations `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nom de la partition d’environnement de test virtuel que vous utilisez. | `prod` |
| `TENANT_ID` | Identifiant utilisé pour vous assurer que les ressources que vous créez sont des espaces de noms corrects et qu’ils sont contenus dans votre organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Le point de terminaison d’URL vers lequel vous effectuez des appels d’API. Cette valeur est fixe et est toujours définie sur : `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Exécution des scripts

Avec votre collection [!DNL Postman] et votre environnement configuré, vous pouvez désormais exécuter le script via l’interface [!DNL Postman].

Dans l’interface [!DNL Postman], sélectionnez le dossier racine de l’utilitaire de génération automatique, puis sélectionnez **[!DNL Run]** dans l’en-tête supérieur.

![root-folder](../images/marketo/root-folder.png)

L’interface [!DNL Runner] s’affiche. À partir de là, assurez-vous que toutes les cases à cocher sont sélectionnées, puis sélectionnez **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

Une requête réussie crée les espaces de noms et les schémas requis pour B2B.

## Espaces de noms B2B

Les espaces de noms d’identité sont un composant de [[!DNL Identity Service]](../../../../identity-service/home.md) qui sert à distinguer le contexte d’une identité. Une identité entièrement qualifiée comprend une valeur d’identité et un espace de noms. Pour plus d’informations, consultez la [présentation des espaces de noms](../../../../identity-service/features/namespaces.md) .

Les espaces de noms B2B sont utilisés dans l’identité principale de l’entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de noms B2B.

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Nom d’affichage | Symbole d’identité | Type d’identité |
| --- | --- | --- |
| Personne B2B | `b2b_person` | `CROSS_DEVICE` |
| Compte B2B | `b2b_account` | `B2B_ACCOUNT` |
| Opportunité B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relation de personne d’opportunité B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campagne B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Membre de la campagne B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Liste marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Membre de la liste marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relation entre personnes de compte B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## Schémas B2B

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](../../../../xdm/schema/composition.md).

Le tableau suivant contient des informations sur la configuration sous-jacente des schémas B2B.

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Nom du schéma | Classe de base | Groupes de champs | [!DNL Profile] dans le schéma | Identité principale | Espace de noms d’identité du Principal | Identité Secondaire | Espace de noms d’identité Secondaire | Relation | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Compte B2B | [Compte professionnel XDM](../../../../xdm/classes/b2b/business-account.md) | Détails du compte professionnel XDM | Activé | `accountKey.sourceKey` dans la classe de base | Compte B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Compte B2B | <ul><li>`accountParentKey.sourceKey` dans le groupe de champs Détails du compte d’entreprise XDM</li><li>Propriété de destination : `/accountKey/sourceKey`</li><li>Type : un pour un</li><li>Schéma de référence : compte B2B</li><li>Espace de noms : compte B2B</li></ul> |
| Personne B2B | [XDM Individual Profile](../../../../xdm/classes/individual-profile.md) | <ul><li>Détails de professionnel XDM</li><li>Composants de professionnel XDM</li><li>IdentityMap</li><li>Détails relatifs au consentement et aux préférences</li></ul> | Activé | `b2b.personKey.sourceKey` dans le groupe de champs Détails de la personne professionnelle XDM | Personne B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` du groupe de champs Détails de la personne professionnelle XDM</li><li>`workEmail.address` du groupe de champs Détails de la personne professionnelle XDM</ol></li> | <ol><li>Personne B2B</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` du groupe de champs Composants de personne professionnelle XDM</li><li>Type : plusieurs à un</li><li>Schéma de référence : compte B2B</li><li>Espace de noms : compte B2B</li><li>Propriété de destination : accountKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| Opportunité B2B | [Opportunité commerciale XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Détails de l’opportunité commerciale XDM | Activé | `opportunityKey.sourceKey` dans la classe de base | Opportunité B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Opportunité B2B | <ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : compte B2B</li><li>Espace de noms : compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : opportunités</li></ul> |
| Relation de personne d’opportunité B2B | [Relation de personne d’opportunité commerciale XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Aucun | Activé | `opportunityPersonKey.sourceKey` dans la classe de base | Relation de personne d’opportunité B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Relation de personne d’opportunité B2B | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : b2b.personKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : opportunités</li></ul>**Deuxième relation**<ul><li>`opportunityKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : opportunité B2B </li><li>Espace de noms : opportunité B2B </li><li>Propriété de destination : `opportunityKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : opportunité</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| Campagne B2B | [XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) | Détails de XDM Business Campaign | Activé | `campaignKey.sourceKey` dans la classe de base | Campagne B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Campagne B2B |
| Membre de la campagne B2B | [ Membres XDM Business Campaign ](../../../../xdm/classes/b2b/business-campaign-members.md) | Détails du membre de la campagne commerciale XDM | Activé | `ccampaignMemberKey.sourceKey` dans la classe de base | Membre de la campagne B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Membre de la campagne B2B | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Campagnes</li></ul>**Deuxième relation**<ul><li>`campaignKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : campagne B2B</li><li>Espace de noms : Campagne B2B</li><li>Propriété de destination : `campaignKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Campaign</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| Liste marketing B2B | [Liste XDM Business Marketing](../../../../xdm/classes/b2b/business-marketing-list.md) | Aucun | Activé | `marketingListKey.sourceKey` dans la classe de base | Liste marketing B2B | Aucun | Aucun | Aucun | La liste statique n’est pas synchronisée à partir de [!DNL Salesforce] et n’a donc pas d’identité secondaire. |
| Membre de la liste marketing B2B | [ Membres de la liste XDM Business Marketing ](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Aucun | Activé | `marketingListMemberKey.sourceKey` dans la classe de base | Membre de la liste marketing B2B | Aucun | Aucun | **Première relation**<ul><li>`PersonKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : listes marketing</li></ul>**Deuxième relation**<ul><li>`marketingListKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : liste marketing B2B</li><li>Espace de noms : liste marketing B2B</li><li>Propriété de destination : `marketingListKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Liste marketing</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> | Le membre de liste statique n’est pas synchronisé à partir de [!DNL Salesforce] et n’a donc pas d’identité secondaire. |
| Activité B2B | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visite WebPage</li><li>Nouveau prospect</li><li>Convertir le prospect</li><li>Ajouter à la liste</li><li>Supprimer de la liste</li><li>Ajouter à l’opportunité</li><li>Supprimer de l’opportunité</li><li>Formulaire complété</li><li>Clics sur les liens</li><li>E-mail remis</li><li>E-mail ouvert</li><li>E-mail faisant l’objet d’un clic</li><li>E-mail non remis</li><li>Non-remise temporaire de l’e-mail</li><li>E-mail : désabonné</li><li>Score modifié</li><li>Opportunité mise à jour</li><li>État dans la progression de la campagne modifiée</li><li>Identifiant de la personne</li><li>URL web Marketo</li><li>Moment intéressant</li><li>Appeler le Webhook</li><li>Modifier le rythme de la campagne</li><li>Étape de revenu modifiée</li><li>Fusionner les prospects</li><li>E-mail envoyé</li><li>Modifier le flux de la campagne</li><li>Ajouter à Campaign</li></ul> | Activé | `personKey.sourceKey` du groupe de champs Identifiant de personne | Personne B2B | Aucun | Aucun | **Première relation**<ul><li>Champ `listOperations.listKey.sourceKey`</li><li>Type : un pour un</li><li>Schéma de référence : liste marketing B2B</li><li>Espace de noms : liste marketing B2B</li></ul>**Deuxième relation**<ul><li>Champ `opportunityEvent.opportunityKey.sourceKey`</li><li>Type : un pour un</li><li>Schéma de référence : opportunité B2B</li><li>Espace de noms : opportunité B2B</li></ul>**Troisième relation**<ul><li>Champ `leadOperation.campaignProgression.campaignKey.sourceKey`</li><li>Type : un pour un</li><li>Schéma de référence : campagne B2B</li><li>Espace de noms : Campagne B2B</li></ul> | `ExperienceEvent` est différent des entités. L’identité de l’événement d’expérience est la personne qui a effectué l’activité. |
| Relation entre personnes de compte B2B | [Relation avec la personne du compte XDM ](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mappage d’identités | Activé | `accountPersonKey.sourceKey` dans la classe de base | Relation entre personnes de compte B2B | Aucun | Aucun | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : Personne B2B</li><li>Espace de noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.SourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personnes</li><li>Nom de la relation à partir du schéma de référence : Compte</li></ul>**Deuxième relation**<ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma de référence : compte B2B</li><li>Espace de noms : compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |

{style="table-layout:auto"}

## Étapes suivantes

Pour savoir comment connecter vos données [!DNL Marketo] à Platform, consultez le tutoriel sur la [création d’un connecteur source Marketo dans l’interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
