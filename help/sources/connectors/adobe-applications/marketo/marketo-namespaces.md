---
title: Espaces de noms et schémas B2B
description: Ce document présente les espaces de noms personnalisés requis lors de la création d’un connecteur source B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 923e56098361b4ef42cbbc2395b748033c0e7b94
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 13%

---

# Espaces de noms et schémas B2B

>[!AVAILABILITY]
>
>Vous devez avoir accès à [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) pour que vos schémas B2B soient qualifiés dans [Real-Time Customer Profile](../../../../profile/home.md).

>[!NOTE]
>
>Vous pouvez utiliser des modèles dans l’interface utilisateur de Adobe Experience Platform pour accélérer la création de ressources pour les données B2B et B2C. Pour plus d’informations, consultez le guide sur [l’utilisation de modèles dans l’interface utilisateur d’Experience Platform](../../../tutorials/ui/templates.md).

Lisez ce document pour plus d’informations sur la configuration sous-jacente des espaces de noms et des schémas à utiliser avec les sources B2B. Ce document fournit également des détails sur la configuration de votre utilitaire d’automatisation Postman requis pour générer des espaces de noms et des schémas B2B.

## Configurer l’utilitaire de génération automatique de schémas et d’espaces de noms B2B

>[!IMPORTANT]
>
>Les informations d’identification du compte de service (JWT) ont été abandonnées. Vous devez vous assurer de migrer votre application ou votre intégration vers les nouvelles informations d’identification de serveur à serveur OAuth avant le 27 janvier 2025. Lisez la documentation suivante pour obtenir des instructions détaillées sur [comment migrer vos informations d’identification JWT vers les informations d’identification OAuth de serveur à serveur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Pour obtenir les informations préalables requises sur la configuration de votre environnement [!DNL Postman] pour prendre en charge l’utilitaire de génération automatique d’espaces de noms et de schémas B2B, consultez la documentation suivante.

- Vous pouvez télécharger la collection d’utilitaires et l’environnement de génération automatique d’espace de noms et de schéma à partir de ce [référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Pour plus d’informations sur l’utilisation des API Experience Platform, notamment sur la collecte des valeurs des en-têtes requis et la lecture d’exemples d’appels d’API, consultez le guide [Prise en main des API Experience Platform](../../../../landing/api-guide.md).
- Pour plus d’informations sur la génération de vos informations d’identification pour les API Experience Platform, consultez le tutoriel sur l’[authentification et accès aux API Experience Platform](../../../../landing/api-authentication.md).
- Pour plus d’informations sur la configuration de [!DNL Postman] pour les API Experience Platform, consultez le tutoriel sur [configuration de Developer Console et  [!DNL Postman]](../../../../landing/postman.md).

Grâce à la console de développement et à la configuration des [!DNL Postman] d’Experience Platform, vous pouvez maintenant commencer à appliquer les valeurs d’environnement appropriées à votre environnement de [!DNL Postman].

Le tableau suivant contient des exemples de valeurs ainsi que des informations supplémentaires sur la population de votre environnement [!DNL Postman] :

| Variable | Description | Exemple |
| --- | --- | --- |
| `CLIENT_SECRET` | Identifiant unique utilisé pour générer votre `{ACCESS_TOKEN}`. Pour plus d’informations sur la récupération de vos [, consultez le tutoriel sur &#x200B;](../../../../landing/api-authentication.md)l’authentification et l’accès aux API Experience Platform`{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `API_KEY` | Identifiant unique utilisé pour authentifier les appels aux API Experience Platform. Pour plus d’informations sur la récupération de vos [, consultez le tutoriel sur &#x200B;](../../../../landing/api-authentication.md)l’authentification et l’accès aux API Experience Platform`{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Jeton d’autorisation requis pour effectuer des appels vers les API Experience Platform. Pour plus d’informations sur la récupération de vos [, consultez le tutoriel sur &#x200B;](../../../../landing/api-authentication.md)l’authentification et l’accès aux API Experience Platform`{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Le conteneur `global` contient toutes les classes, groupes de champs de schéma, types de données et schémas fournis par les partenaires standard d’Adobe et d’Experience Platform. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur `global`. | `global` |
| `TECHNICAL_ACCOUNT_ID` | Informations d’identification utilisées pour intégrer à Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Le système Identity Management (IMS) fournit la structure pour l’authentification aux services Adobe. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entité d’entreprise pouvant posséder des produits et services ou en obtenir la licence et permettre l’accès à ses membres. Consultez le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../../landing/postman.md) pour obtenir des instructions sur la récupération de vos informations de `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nom de la partition de sandbox virtuelle que vous utilisez. | `prod` |
| `TENANT_ID` | Identifiant utilisé pour s’assurer que les ressources que vous créez ont un espace de noms correct et sont contenues dans votre organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Point d’entrée de l’URL vers lequel vous effectuez des appels API. Cette valeur est fixe et est toujours définie sur : `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Exécution des scripts

Une fois votre collection de [!DNL Postman] et votre environnement configurés, vous pouvez exécuter le script via l’interface [!DNL Postman].

Dans l’interface [!DNL Postman], sélectionnez le dossier racine de l’utilitaire de génération automatique, puis sélectionnez **[!DNL Run]** dans l’en-tête supérieur.

![Dossier racine du générateur d’espaces de noms et de schémas dans l’interface utilisateur de Postman. « Exécutions » est mis en surbrillance dans la barre de menus supérieure.](../images/marketo/root_folder.png)

L’interface [!DNL Runner] s’affiche. À partir de là, assurez-vous que toutes les cases à cocher sont sélectionnées, puis sélectionnez **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![L’interface Runner de l’interface utilisateur de Postman avec plusieurs requêtes dans la collection Espaces de noms et Schémas cochées et le bouton « Exécuter les espaces de noms et les schémas » mis en surbrillance sur le côté droit.](../images/marketo/run_generator.png)

Une requête réussie crée les espaces de noms et les schémas requis pour B2B.

## Espaces de noms B2B

Les espaces de noms d’identité sont des composants d’[[!DNL Identity Service]](../../../../identity-service/home.md) qui servent à distinguer le contexte d’une identité. Une identité complète comprend une valeur d’identité et un espace de noms. Lisez la [&#x200B; Présentation des espaces de noms &#x200B;](../../../../identity-service/features/namespaces.md) pour plus d’informations.

Les espaces de noms B2B sont utilisés dans l’identité principale de l’entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de noms B2B.

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Nom d’affichage | Symbole d’identité | Type d’identité |
| --- | --- | --- |
| Personne B2B | `b2b_person` | `CROSS_DEVICE` |
| Compte B2B | `b2b_account` | `B2B_ACCOUNT` |
| Opportunité B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relation de la personne avec l’opportunité B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campagne B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Membre de la campagne B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Liste marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Membre de la liste marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relation avec la personne du compte B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## Schémas B2B

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Experience Platform, un schéma doit être créé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenu dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](../../../../xdm/schema/composition.md).

Le tableau suivant contient des informations sur la configuration sous-jacente des schémas B2B.

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Nom du schéma | Classe de base | Groupes de champs | [!DNL Profile] dans le schéma | Identité principale | Espace de noms d’identité principale | identité Secondaire | Espace de noms d’identité Secondaire | Relation | Remarques |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Compte B2B | [&#x200B; Compte professionnel XDM &#x200B;](../../../../xdm/classes/b2b/business-account.md) | Détails du compte professionnel XDM | Activé | `accountKey.sourceKey` dans la classe de base | Compte B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Compte B2B | <ul><li>`accountParentKey.sourceKey` dans le groupe de champs Détails du compte professionnel XDM</li><li>Propriété de destination : `/accountKey/sourceKey`</li><li>Type : un à un</li><li>Schéma de référence : compte B2B</li><li>Espace De Noms : Compte B2B</li></ul> |
| Personne B2B | [XDM Individual Profile](../../../../xdm/classes/individual-profile.md) | <ul><li>Détails de professionnel XDM</li><li>Composants de professionnel XDM</li><li>IdentityMap</li><li>Détails relatifs au consentement et aux préférences</li></ul> | Activé | `b2b.personKey.sourceKey` dans le groupe de champs Détails professionnels XDM | Personne B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` du groupe de champs Détails professionnels XDM</li><li>`workEmail.address` du groupe de champs Détails professionnels XDM</ol></li> | <ol><li>Personne B2B</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` du groupe de champs Composants professionnels XDM .</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Compte B2B</li><li>Espace De Noms : Compte B2B</li><li>Propriété de destination : accountKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |
| Opportunité B2B | [Opportunité commerciale XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Détails de l’opportunité commerciale XDM | Activé | `opportunityKey.sourceKey` dans la classe de base | Opportunité B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Opportunité B2B | <ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Compte B2B</li><li>Espace De Noms : Compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation du schéma de référence : Opportunités</li></ul> |
| Relation de la personne avec l’opportunité B2B | [Relation de la personne avec l’opportunité commerciale XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Aucune | Activé | `opportunityPersonKey.sourceKey` dans la classe de base | Relation de la personne avec l’opportunité B2B | | | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : b2b.personKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation du schéma de référence : Opportunités</li></ul>**Deuxième relation**<ul><li>`opportunityKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Opportunité B2B </li><li>Espace de noms : opportunité B2B </li><li>Propriété de destination : `opportunityKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : opportunité</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |
| Campagne B2B | [XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) | Détails de XDM Business Campaign | Activé | `campaignKey.sourceKey` dans la classe de base | Campagne B2B | | |
| Membre de la campagne B2B | [Membres de la campagne commerciale XDM](../../../../xdm/classes/b2b/business-campaign-members.md) | Détails du membre de la campagne commerciale XDM | Activé | `ccampaignMemberKey.sourceKey` dans la classe de base | Membre de la campagne B2B | | | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation du schéma de référence : Campagnes</li></ul>**Deuxième relation**<ul><li>`campaignKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Campagne B2B</li><li>Espace de noms : Campagne B2B</li><li>Propriété de destination : `campaignKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Campaign</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |
| Liste marketing B2B | [Liste marketing professionnelle XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | Aucune | Activé | `marketingListKey.sourceKey` dans la classe de base | Liste marketing B2B | Aucune | Aucune | Aucune | La liste statique n’est pas synchronisée à partir de [!DNL Salesforce] et n’a donc pas d’identité secondaire. |
| Membre de la liste marketing B2B | [Membres de la liste marketing professionnelle XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Aucune | Activé | `marketingListMemberKey.sourceKey` dans la classe de base | Membre de la liste marketing B2B | Aucune | Aucune | **Première relation**<ul><li>`PersonKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Listes marketing</li></ul>**Deuxième relation**<ul><li>`marketingListKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Liste Marketing B2B</li><li>Espace De Noms : Liste Marketing B2B</li><li>Propriété de destination : `marketingListKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Liste marketing</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> | Le membre de liste statique n’est pas synchronisé à partir de [!DNL Salesforce] et n’a donc pas d’identité secondaire. |
| Relation avec la personne du compte B2B | [Relation avec la personne du compte professionnel XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mappage d’identités | Activé | `accountPersonKey.sourceKey` dans la classe de base | Relation avec la personne du compte B2B | Aucune | Aucune | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.SourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personnes</li><li>Nom de la relation à partir du schéma de référence : Compte</li></ul>**Deuxième relation**<ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Compte B2B</li><li>Espace De Noms : Compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |

{style="table-layout:auto"}

## Étapes suivantes

Pour découvrir comment connecter vos données [!DNL Marketo] à Experience Platform, consultez le tutoriel sur la [création d’un connecteur source Marketo dans l’interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).

<!--

| B2B Activity | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visit WebPage</li><li>New Lead</li><li>Convert Lead</li><li>Add To List</li><li>Remove From List</li><li>Add To Opportunity</li><li>Remove From Opportunity</li><li>Form Filled Out</li><li>Link Clicks</li><li>Email Delivered</li><li>Email Opened</li><li>Email Clicked</li><li>Email Bounced</li><li>Email Bounced Soft</li><li>Email Unsubscribed</li><li>Score Changed</li><li>Opportunity Updated</li><li>Status in Campaign Progression Changed</li><li>Person Identifier</li><li>Marketo Web URL</li><li>Interesting Moment</li><li>Call Webhook</li><li>Change Campaign Cadence</li><li>Revenue Stage Changed</li><li>Merge Leads</li><li>Email Sent</li><li>Change Campaign Stream</li><li>Add to Campaign</li></ul> | Enabled | `personKey.sourceKey` of Person Identifier field group | B2B Person | None | None | | `ExperienceEvent` is different from entities. The identity of experience event is the person who did the activity. |

-->