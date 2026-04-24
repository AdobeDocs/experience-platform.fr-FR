---
title: Data Governance in Query Service
description: This overview covers the major elements of data governance in Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: c98ae492b12fb5b9596f19a3d64785090439f7e1
workflow-type: tm+mt
source-wordcount: '3182'
ht-degree: 3%

---

# Data governance in Query Service

Adobe Experience Platform brings data from multiple enterprise systems together and allows you to clean, shape, manipulate and enrich the data through Query Service according to your needs. This allows marketers to identify, understand, and engage customers in a better way. Ensuring adequate data governance is a critical aspect of handling personal information as certain data may be subject to usage restrictions based on organizational policies and legal regulations. It is critical to ensure that your ingested data and its related operations are compliant with the defined data usage policies.

Data governance within Query Service allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. This plays a key role when ensuring the usage policies have been applied according to the regulations defined by your business.

Organizations that routinely conduct data processing are recommended to outline, practice, and enforce these guidelines to create a privacy-conscious environment for all users.

The following categories are instrumental in adhering to data compliance regulations when using Query Service:

1. Sécurité
1. Journal
1. Data usage
1. Confidentialité
1. Hygiène des données

This document examines each of the different areas of governance and demonstrates how to facilitate data compliance when using Query Service. See the [governance, privacy, and security overview](../../landing/governance-privacy-security/overview.md) for broader information on how Experience Platform allows you to manage customer data and ensure compliance.

## Sécurité {#security}

Data security is the process of protecting data from unauthorized access and ensuring secure access throughout its lifecycle. Secure access is maintained in Experience Platform through the application of roles and permissions by capabilities such as role-based access control and attribute-based access control. Credentials, SSL, and data encryption are also used to ensure data protection across Experience Platform.

Security in regard to Query Service is divided into the following categories:

* [Access control](#access-control): Access is controlled through roles and permissions including dataset and column-level permissions.
* Securing data through [connectivity](#connectivity): Data is secured through Experience Platform and external clients by achieving a limited connection with expiring credentials, or non-expiring credentials.
* Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest.

### Contrôle d’accès {#access-control}

Access control in Adobe Experience Platform is managed by role-based permissions that determine which users can use Query Service features. Similarly, you can control access to specific data attributes through label management on schemas and data fields.

This section outlines the required access control permissions that a user must have in order to fully utilize Query Service features. See the documents on [managing permissions](../../access-control/ui/permissions.md) and [managing users](../../access-control/ui/users.md) for detailed instructions on assigning access to a product profile.

#### Autorisations appropriées

Les autorisations de contrôle d’accès appropriées sont définies dans les tableaux ci-dessous en fonction de leur niveau de portée.

**Autorisations d’exécution des requêtes**

Pour exécuter des requêtes dans Query Service, un rôle doit être attribué à un utilisateur avec l’autorisation suivante :

| Autorisation | Description |
|---|---|
| [!UICONTROL Manage Queries] | Cette autorisation permet aux utilisateurs et utilisatrices d’exécuter des requêtes d’exploration des données et par lots, qui peuvent lire un jeu de données existant ou écrire des données sur des jeux de données. Cela inclut les requêtes `CREATE TABLE AS SELECT` (`CTAS`) et `INSERT INTO AS SELECT` (`ITAS`). |

**Autorisations des jeux de données**

Cette section sert de guide pour l’accès basé sur les ressources requis pour accéder aux jeux de données lors de l’interrogation de données par le biais de Query Service.

Grâce à l’interface Autorisations , vous pouvez définir un contrôle d’accès basé sur les ressources pour un jeu de données et un schéma avec les autorisations suivantes :

| Autorisation | Description |
|---|---|
| [!UICONTROL Manage Datasets] | Cette autorisation fournit un accès en lecture seule aux schémas et permet d’accéder à la lecture, la création, la modification et la suppression des jeux de données à utiliser avec Query Service. |
| [!UICONTROL View Datasets] | Cette autorisation permet un accès en lecture seule aux jeux de données et aux schémas à utiliser avec Query Service. |

#### Contrôle d’accès pour les colonnes/champs

La fonctionnalité de contrôle d’accès basé sur les attributs permet aux utilisateurs de Query Service de restreindre l’accès aux données utilisateur critiques. L’accès peut être accordé ou restreint en fonction des autorisations attribuées à un rôle. L’accès des utilisateurs et utilisatrices aux différentes colonnes est contrôlé par les libellés d’utilisation des données pertinents et les jeux d’autorisations appliqués aux rôles affectés aux utilisateurs et utilisatrices.

Le balisage des groupes et classes de champs de schéma avec des libellés d’utilisation des données applique des restrictions d’utilisation des données à tous les schémas avec les mêmes groupes et classes de champs. Consultez la présentation du [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md) pour obtenir des informations complètes sur cette fonctionnalité.

Cette fonctionnalité vous permet d’accorder des droits d’accès sur des colonnes confidentielles aux groupes d’utilisateurs de votre choix. Le contrôle d’accès sur une colonne peut restreindre les fonctionnalités de lecture et d’écriture d’un type particulier d’utilisateur.

Le contrôle d’accès des colonnes peut être appliqué au niveau du schéma pour les schémas standard et ad hoc. Appliquez des libellés d’utilisation des données aux schémas XDM pour restreindre l’accès à une ou plusieurs colonnes. L’étiquetage des données est appliqué de manière cohérente, même pour les jeux de données créés via Query Service à l’aide d’un schéma prédéfini ou d’un schéma ad hoc généré dans le cadre d’une opération CTAS.

Une fois le niveau d’accès approprié appliqué à l’aide des libellés et des rôles, le comportement système suivant se produit lorsqu’un utilisateur ou une utilisatrice tente d’accéder aux données non accessibles :

1. Si l’accès à l’une des colonnes d’un schéma a été refusé à un utilisateur, celui-ci se voit également refuser l’autorisation de lire ou d’écrire sur la colonne restreinte. Cela s’applique aux scénarios courants suivants :

   * **Case 1**: When a user tries to execute a query affecting only a restricted column, the system throws an error that the column doesn&#39;t exist.
   * **Case 2**: When a user tries to execute a query with multiple columns including a restricted column, the system returns output for all non-restricted columns only.

1. If a user tries to access a calculated field, the user is required to have access to all the fields used in the composition or the system denies access to the calculated field as well.

#### Access controls for views

Query Service provides the ability to use standard ANSI SQL for [`CREATE VIEW`](../sql/syntax.md#create-view) statements. For highly sensitive data workflows, you must enforce appropriate controls when creating views.

The `CREATE VIEW` keyword defines a view of a query but the view is not physically materialized. Instead, the query is run every time the view is referenced in a query. When a user creates a view from a dataset, the role- and attribute-based access control rules for the parent dataset are **not** hierarchically applied. As a result, you must explicitly set permissions on each of the columns when a view is created.

#### Create field-based access restrictions on accelerated datasets {#create-field-based-access-restrictions-on-accelerated-datasets}

With the [attribute-based access control capability](../../access-control/abac/overview.md) you can define organizational or data usage scopes on fact and dimension datasets in the [accelerated store](../data-distiller/sql-insights/send-accelerated-queries.md). This allows administrators to manage access to specific segments and better manage the access given to users or groups of users.

To create field-based access restrictions on accelerated datasets, you can use Query Service CTAS queries to create accelerated datasets and structure these datasets based on existing XDM schemas or ad hoc schemas. Administrators can then [add and edit data usage labels for the schema](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) or [ad hoc schema](./ad-hoc-schema-labels.md#edit-governance-labels). You can apply, create, and edit labels to your schemas from the [!UICONTROL Labels] workspace in the [!UICONTROL Schemas] UI.

Data usage labels can also be [applied or edited directly onto the dataset](../../data-governance/labels/user-guide.md#add-labels) through the Datasets UI, or created from the Access Control [!UICONTROL Labels] workspace. See the guide on how to [create a new label](../../access-control/abac/ui/labels.md) for more information.

User access to individual columns can then be controlled by the attached data usage labels and the permission sets applied to the roles that are assigned to users.

### Connectivité {#connectivity}

Query Service is accessible through the Experience Platform UI or by forming a connection with external compatible clients. Access to all available fronts is controlled by a set of credentials.

#### Connectivity through external clients

Access to Query Service using a third-party client requires credentials for authorization. These credentials are mandatory to access Query Service with any of the compatible external clients. You can connect to external clients by using either [expiring credentials](#expiring-credentials) or [non-expiring credentials](#non-expiring-credentials).

#### Limited connection time via expiring credentials {#expiring-credentials}

[Expiring credentials](../ui/credentials.md) allow users to form a temporary connection with an external client. This set of credentials is only valid for 24 hours. The expiry of these types of credentials can be seen along with the credential tab in the Query Service dashboard.

![The credentials tab in Query Service workspace with expiring credentials highlighted.](../images/data-governance/overview/expiring-credentials.png)

#### Informations d’identification n’expirant pas {#non-expiring-credentials}

[Non-expiring credentials](../ui/credentials.md#non-expiring-credentials) allow you to form a permanent connection with an external client, making it easier to connect to Query Service without the need for a manual password.

To enable the option of generating non-expiring credentials, you must follow the outlined [pre-requisite workflow](../ui/credentials.md#prerequisites). As part of this process, your organization administrator is required to configure permissions for the product profile, giving the administrator control over which accounts have access to use non-expiring credentials.

Technical user accounts permitted with non-expiring credentials can be assigned roles to ensure appropriate data governance by defining the scope of their read and write access based on their responsibilities and needs. See the earlier section on [using role-based permissions through access control](#access-control) to manage access to Query Service.

Once the prerequisite workflow has been completed, authorized users can now [generate the required connection credentials](../ui/credentials.md#generate-credentials).

#### SSL data encryption

For increased security, Query Service provides native support for SSL connections to encrypt client/server communications. Experience Platform supports various SSL options to suit your data security needs and balance the processing overhead of encryption and key exchange.

See the guide on available [SSL options for third-party client connections to Query Service](../clients/ssl-modes.md) for more information, including how to connect using the `verify-full` SSL parameter value.

### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys}

Encryption is the use of an algorithmic process to transform data into encoded and unreadable text to ensure the information is protected and inaccessible without a decryption key.

Query Service data compliance ensures that data is always encrypted. Data-in-transit is always HTTPS compliant, and data-at-rest is encrypted in an Azure Data Lake store using system-level keys. See the documentation on [how data is encrypted in Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md) for more information. For details on how data at rest is encrypted in Azure Data Lake Storage, see the [official Azure documentation](https://docs.microsoft.com/fr-fr/azure/data-lake-store/data-lake-store-encryption).

Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. See the [customer-managed keys (CMK) documentation](../../landing/governance-privacy-security/customer-managed-keys/overview.md) to learn how to set up your own encryption keys for data stored in Adobe Experience Platform.


## Journal {#audit}

Query Service records user activity and categorizes that activity in different log types. Les journaux fournissent des informations sur **qui** a effectué **quoi** action et **quand**. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’ID d’e-mail de l’utilisateur ou de l’utilisatrice qui a exécuté l’action et des attributs supplémentaires liés au type d’action.

Toutes les catégories de journal peuvent être demandées par un utilisateur d’Experience Platform selon ses besoins. Cette section fournit des détails sur le type d’informations capturées pour Query Service et l’endroit où ces informations sont accessibles.

### Journaux de requête {#query-logs}

L’interface utilisateur des journaux de requête vous permet de surveiller et de consulter les détails d’exécution de toutes les requêtes qui ont été exécutées via Query Editor ou l’API Query Service. Cela apporte de la transparence aux activités de Query Service, ce qui vous permet de vérifier les métadonnées de **toutes** les requêtes qui ont été exécutées dans Query Service. Il inclut tous les types de requêtes, qu’il s’agisse d’une requête exploratoire, par lots ou planifiée.

Les journaux de requête sont accessibles via l’interface utilisateur d’Experience Platform dans l’onglet [!UICONTROL Logs] de l’espace de travail [!UICONTROL Queries].

![Onglet Journal des requêtes avec le panneau des détails mis en surbrillance.](../images/data-governance/overview/queries-log.png)

### Journaux d’audit {#audit-logs}

Les journaux d’audit contiennent des informations plus détaillées que les journaux de requête et vous permettent de filtrer les journaux en fonction d’attributs tels que l’utilisateur, la date, le type de requête, etc. Outre les détails disponibles dans l’interface utilisateur du journal de requête, les journaux d’audit stockent les détails sur les utilisateurs individuels ainsi que leurs données de session ou leur connectivité à un client tiers.

En fournissant un enregistrement exact des actions des utilisateurs, un journal d&#39;audit peut vous aider à résoudre les problèmes et à vous conformer efficacement aux politiques de gestion des données d&#39;entreprise et aux exigences réglementaires. Les journaux d’audit fournissent un enregistrement de toutes les activités Experience Platform. Grâce aux journaux d’audit, vous pouvez auditer les actions des utilisateurs et utilisatrices relatives à l’exécution des requêtes, aux modèles et aux requêtes planifiées, afin d’accroître la transparence et la visibilité des actions effectuées par les utilisateurs et utilisatrices dans Query Service.

Le tableau suivant indique les catégories de requête capturées par les journaux d’audit et les types d’action qu’ils enregistrent :

| Catégorie | Type d’action |
|---|---|
| Requête | Exécuter |
| Modèle de requête | Créer, Supprimer, Mettre À Jour |
| Requête planifiée | Créer, Supprimer, Mettre À Jour |

Vous trouverez ci-dessous une liste de trois journaux de serveur étendus contenant plus de détails que ceux trouvés dans les journaux de requête. Les journaux étendus se trouvent dans les catégories de requête des journaux d’audit :

1. **Journaux de requêtes Meta** : lorsqu’une requête est exécutée, diverses sous-requêtes principales associées (telles que l’analyse) sont exécutées. Ces types de requêtes sont appelés requêtes « métadonnées ». Leurs détails pertinents se trouvent dans les journaux d’audit.
1. **Journaux de session** : le système crée un journal d’entrée de session pour un utilisateur lorsqu’il se connecte à Query Service, qu’il exécute ou non une requête.
1. **Journaux de connexion client tiers** : un journal d’audit de connectivité est généré lorsqu’un utilisateur connecte correctement Query Service à un client tiers.

Pour plus d’informations sur la manière dont les journaux d’audit peuvent aider votre organisation à aborder la conformité des données, consultez la [&#x200B; présentation des journaux d’audit &#x200B;](../../landing/governance-privacy-security/audit-logs/overview.md).

## Utilisation des données {#data-usage}

Le cadre de gouvernance des données dans Experience Platform offre un moyen uniforme d’utiliser les données de manière responsable sur l’ensemble des solutions, services et plateformes Adobe. Il coordonne l’approche systémique de la capture, de la communication et de l’utilisation des métadonnées dans l’ensemble de Adobe Experience Cloud. Cela permet aux contrôleurs de données d’étiqueter les données en fonction des actions marketing nécessaires et des restrictions placées sur ces données à partir de ces actions marketing prévues. Consultez la présentation des [libellés d’utilisation des données](../../data-governance/labels/overview.md) pour plus d’informations sur la manière dont la gouvernance des données vous permet d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs.

Il est recommandé d’œuvrer à la conformité des données à chaque étape du parcours des données. À cette fin, les jeux de données dérivés qui utilisent des schémas ad hoc doivent être étiquetés de manière appropriée dans le cadre de la gouvernance des données. Il existe deux types de jeux de données dérivés formés par Query Service : les jeux de données qui utilisent un schéma standard et les jeux de données qui utilisent un schéma ad hoc.

>[!NOTE]
>
>Les jeux de données créés à l’aide de Query Service sont appelés « jeux de données dérivés ».

Comme les schémas ad hoc sont créés par un utilisateur individuel dans un but spécifique, les champs de schéma XDM sont des espaces de noms pour ce jeu de données spécifique et ne sont pas destinés à être utilisés dans différents jeux de données. Par conséquent, les schémas ad hoc ne sont pas visibles par défaut dans l’interface utilisateur d’Experience Platform. Bien qu’il n’y ait pas de différence dans l’application des libellés d’utilisation des données entre les schémas standard et ad hoc, les schémas ad hoc créés par Query Service à des fins de libellés doivent d’abord être rendus visibles dans l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez le guide sur la [découverte de schémas ad hoc dans l’interface utilisateur d’Experience Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas).

Après avoir accédé au schéma, vous pouvez [appliquer des libellés à des champs individuels](../../xdm/tutorials/labels.md). Une fois qu’un schéma a été libellé, tous les jeux de données qui dérivent de ce schéma héritent de ces libellés. À partir de là, vous pouvez configurer des politiques d’utilisation des données qui peuvent restreindre l’activation des données avec certains libellés vers certaines destinations. Pour plus d’informations, consultez la présentation des [politiques d’utilisation des données](../../data-governance/policies/overview.md).

## Confidentialité {#privacy}

[Privacy Service](../../privacy-service/home.md) vous aide à gérer les demandes d’accès et de suppression des données des clients conformément aux réglementations légales en matière de confidentialité. Pour ce faire, il recherche des identifiants préexistants dans les données et accède ou supprime ces données en fonction de la tâche de confidentialité demandée. Les données doivent disposer de libellés appropriés afin que le service puisse déterminer les champs auxquels accéder ou ceux qu’il doit supprimer au cours des tâches relatives à la confidentialité. Les données soumises à des demandes d’accès à des informations personnelles doivent contenir des informations d’identité client afin de lier les différents éléments de données avec la personne à laquelle la demande d’accès à des informations personnelles s’applique. Query Service peut enrichir les données qu’il utilise avec un identifiant unique dans le but de satisfaire les tâches liées à la confidentialité.

Les demandes d’accès à des informations personnelles peuvent être envoyées au lac de données ou à la banque de données Profile. Les enregistrements supprimés du lac de données n’entraînent pas la suppression des profils qui ont été effectués à partir de ces enregistrements. En outre, une tâche de confidentialité visant à supprimer des informations personnelles du lac de données ne supprime pas leur profil, de sorte que toute information (qui contient cet identifiant de profil) ingérée après la fin de la tâche de confidentialité met à jour ce profil comme d’habitude. Cela réaffirme la nécessité d’identifier correctement les données utilisées dans les schémas ad hoc.

Consultez la documentation de Privacy Service pour plus d’informations sur [les données d’identité pour les demandes d’accès à des informations personnelles](../../privacy-service/identity-data.md) et sur la manière de configurer vos opérations de données et d’exploiter les technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.

Les fonctionnalités de Query Service pour la gouvernance des données simplifient et rationalisent le processus de catégorisation des données et le respect des réglementations d’utilisation des données. Une fois les données identifiées, Query Service vous permet d’allouer l’identité principale à tous les jeux de données de sortie. Vous **devez** ajouter des identités au jeu de données pour faciliter les demandes relatives à la confidentialité des données et travailler à la conformité des données.

Les champs de données de schéma peuvent être définis comme un champ d’identité via l’interface utilisateur d’Experience Platform. Query Service vous permet également de [marquer les identités principales à l’aide de la commande SQL « ALTER TABLE »](../sql/syntax.md#alter-table). La définition d’une identité à l’aide de la commande `ALTER TABLE` est particulièrement utile lorsque les jeux de données sont créés à l’aide de SQL plutôt que directement depuis un schéma via l’interface utilisateur d’Experience Platform. Consultez la documentation pour obtenir des instructions sur la manière de [définir des champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md) lors de l’utilisation de schémas standard.

## Hygiène des données {#data-hygiene}

Le « nettoyage de données » fait référence au processus de réparation ou de suppression de données qui peuvent être obsolètes, inexactes, incorrectement formatées, dupliquées ou incomplètes. Ces processus permettent de s’assurer que les jeux de données sont précis et cohérents sur tous les systèmes. Il est important d’assurer une hygiène adéquate des données à chaque étape du parcours des données et même depuis l’emplacement de stockage initial des données. Dans Experience Platform Query Service, il s’agit du lac de données ou de la boutique accélérée.

Vous pouvez attribuer une identité à un jeu de données dérivé pour permettre sa gestion des données selon les services centralisés d’hygiène des données d’Experience Platform.

À l’inverse, lorsque vous créez un jeu de données agrégé sur la boutique accélérée, les données agrégées ne peuvent pas être utilisées pour dériver les données d’origine. Grâce à cette agrégation de données, il n’est plus nécessaire d’augmenter les demandes d’hygiène de données.

Le cas de la suppression constitue une exception à ce scénario. Si une suppression de l’hygiène des données est demandée sur un jeu de données et qu’avant que la suppression ne soit terminée, une autre requête de jeu de données dérivé est exécutée, puis le jeu de données dérivé capture des informations à partir du jeu de données d’origine. Dans ce cas, vous devez garder à l’esprit que si une demande de suppression d’un jeu de données a été envoyée, vous ne devez pas exécuter de requêtes de jeu de données nouvellement dérivées à l’aide de la même source de jeu de données.

Consultez la [présentation de l’hygiène des données](../../hygiene/home.md) pour plus d’informations sur l’hygiène des données dans Adobe Experience Platform.
