---
title: Gouvernance des données dans Query Service
description: Cette présentation couvre les principaux éléments de la gouvernance des données dans Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3142'
ht-degree: 1%

---

# Gouvernance des données dans Query Service

Adobe Experience Platform rassemble des données issues de plusieurs systèmes d’entreprise et vous permet de nettoyer, de mettre en forme, de manipuler et d’enrichir les données par le biais de Query Service en fonction de vos besoins. Cela permet aux professionnels du marketing d’identifier, de comprendre et d’impliquer les clients plus efficacement. Assurer une gouvernance adéquate des données est un aspect essentiel du traitement des informations personnelles, car certaines données peuvent être soumises à des restrictions d’utilisation basées sur les politiques organisationnelles et les réglementations légales. Il est essentiel de s’assurer que vos données ingérées et leurs opérations associées sont conformes aux politiques d’utilisation des données définies.

La gouvernance des données dans Query Service vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Cela joue un rôle essentiel pour vous assurer que les politiques d’utilisation ont été appliquées conformément aux réglementations définies par votre entreprise.

Il est recommandé aux entreprises qui effectuent régulièrement le traitement des données de mettre en œuvre et d’appliquer ces directives afin de créer un environnement soucieux de la confidentialité pour tous les utilisateurs et utilisatrices.

Les catégories suivantes sont essentielles au respect des réglementations de conformité des données lors de l’utilisation de Query Service :

1. Sécurité
1. Journal
1. Utilisation des données
1. Confidentialité   
1. Hygiène des données

Ce document examine chacun des différents domaines de gouvernance et montre comment faciliter la conformité des données lors de l’utilisation de Query Service. Consultez la [présentation de la gouvernance, de la confidentialité et de la sécurité](../../landing/governance-privacy-security/overview.md) pour obtenir des informations plus générales sur la manière dont Experience Platform vous permet de gérer les données clients et de garantir la conformité.

## Sécurité {#security}

La sécurité des données est le processus de protection des données contre tout accès non autorisé et de sécurisation de l’accès tout au long de leur cycle de vie. L’accès sécurisé est conservé dans Experience Platform par l’application de rôles et d’autorisations grâce à des fonctionnalités telles que le contrôle d’accès basé sur les rôles et le contrôle d’accès basé sur les attributs. Les informations d’identification, SSL et le chiffrement des données sont également utilisés pour assurer la protection des données dans Experience Platform.

La sécurité de Query Service est divisée en plusieurs catégories :

* [Contrôle d’accès](#access-control) : l’accès est contrôlé par des rôles et des autorisations, y compris des autorisations au niveau des jeux de données et des colonnes.
* Sécurisation des données par le biais de la [connectivité](#connectivity) : les données sont sécurisées via Experience Platform et des clients externes en établissant une connexion limitée avec des informations d’identification arrivant à expiration ou non.
* Sécurisation des données par [chiffrement et clés gérées par le client ou la cliente (CMK)](#encryption-and-customer-managed-keys) : accès contrôlé par chiffrement lorsque les données sont inactives.

### Contrôle d’accès {#access-control}

Le contrôle d’accès dans Adobe Experience Platform vous permet d’utiliser [Adobe Admin Console](https://adminconsole.adobe.com/) pour gérer l’accès aux fonctionnalités de Query Service à l’aide d’autorisations basées sur les rôles. De même, vous pouvez contrôler l’accès à des attributs de données spécifiques par le biais de la gestion des libellés sur les schémas et les champs de données.

Cette section décrit les autorisations de contrôle d’accès requises qu’un utilisateur doit posséder pour utiliser pleinement les fonctionnalités de Query Service. Consultez les documents [gestion des autorisations](../../access-control/ui/permissions.md) et [gestion des utilisateurs](../../access-control/ui/users.md) pour obtenir des instructions détaillées sur l’attribution de l’accès à un profil de produit.

#### Autorisations appropriées

Les autorisations de contrôle d’accès appropriées sont définies dans les tableaux ci-dessous en fonction de leur niveau de portée.

**Autorisations d’exécution des requêtes**

Pour exécuter des requêtes dans Query Service, un rôle doit être attribué à un utilisateur avec l’autorisation suivante :

| Autorisation | Description |
|---|---|
| [!UICONTROL Gestion des requêtes] | Cette autorisation permet aux utilisateurs et utilisatrices d’exécuter des requêtes d’exploration des données et par lots, qui peuvent lire un jeu de données existant ou écrire des données sur des jeux de données. Cela inclut les requêtes `CREATE TABLE AS SELECT` (`CTAS`) et `INSERT INTO AS SELECT` (`ITAS`). |

**Autorisations des jeux de données**

Cette section sert de guide pour l’accès basé sur les ressources requis pour accéder aux jeux de données lors de l’interrogation de données par le biais de Query Service.

Grâce à l’interface Autorisations , vous pouvez définir un contrôle d’accès basé sur les ressources pour un jeu de données et un schéma avec les autorisations suivantes :

| Autorisation | Description |
|---|---|
| [!UICONTROL Gestion des jeux de données] | Cette autorisation fournit un accès en lecture seule aux schémas et permet d’accéder à la lecture, la création, la modification et la suppression des jeux de données à utiliser avec Query Service. |
| [!UICONTROL Affichage des jeux de données] | Cette autorisation permet un accès en lecture seule aux jeux de données et aux schémas à utiliser avec Query Service. |

#### Contrôle d’accès pour les colonnes/champs

La fonctionnalité de contrôle d’accès basé sur les attributs permet aux utilisateurs de Query Service de restreindre l’accès aux données utilisateur critiques. L’accès peut être accordé ou restreint en fonction des autorisations attribuées à un rôle. L’accès des utilisateurs et utilisatrices aux différentes colonnes est contrôlé par les libellés d’utilisation des données pertinents et les jeux d’autorisations appliqués aux rôles affectés aux utilisateurs et utilisatrices.

Le balisage des groupes et classes de champs de schéma avec des libellés d’utilisation des données applique des restrictions d’utilisation des données à tous les schémas avec les mêmes groupes et classes de champs. Consultez la présentation du [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md) pour obtenir des informations complètes sur cette fonctionnalité.

Cette fonctionnalité vous permet d’accorder des droits d’accès sur des colonnes confidentielles aux groupes d’utilisateurs de votre choix. Le contrôle d’accès sur une colonne peut restreindre les fonctionnalités de lecture et d’écriture d’un type particulier d’utilisateur.

Le contrôle d’accès des colonnes peut être appliqué au niveau du schéma pour les schémas standard et ad hoc. Appliquez des libellés d’utilisation des données aux schémas XDM pour restreindre l’accès à une ou plusieurs colonnes. L’étiquetage des données est appliqué de manière cohérente, même pour les jeux de données créés via Query Service à l’aide d’un schéma prédéfini ou d’un schéma ad hoc généré dans le cadre d’une opération CTAS.

Une fois le niveau d’accès approprié appliqué à l’aide des libellés et des rôles, le comportement système suivant se produit lorsqu’un utilisateur ou une utilisatrice tente d’accéder aux données non accessibles :

1. Si l’accès à l’une des colonnes d’un schéma a été refusé à un utilisateur, celui-ci se voit également refuser l’autorisation de lire ou d’écrire sur la colonne restreinte. Cela s’applique aux scénarios courants suivants :

   * **Cas 1** : lorsqu’un utilisateur ou une utilisatrice tente d’exécuter une requête affectant uniquement une colonne restreinte, le système renvoie une erreur indiquant que la colonne n’existe pas.
   * **Cas 2** : lorsqu’un utilisateur ou une utilisatrice tente d’exécuter une requête avec plusieurs colonnes, y compris une colonne restreinte, le système renvoie une sortie pour toutes les colonnes non restreintes uniquement.

1. Si un utilisateur ou une utilisatrice tente d’accéder à un champ calculé, il ou elle doit avoir accès à tous les champs utilisés dans la composition, ou le système lui refuse également l’accès au champ calculé.

#### Contrôles d’accès pour les vues

Query Service permet d’utiliser le langage SQL ANSI standard pour les instructions [`CREATE VIEW`](../sql/syntax.md#create-view). Pour les workflows de données hautement sensibles, vous devez appliquer les contrôles appropriés lors de la création de vues.

Le mot-clé `CREATE VIEW` définit une vue d&#39;une requête, mais la vue n&#39;est pas matérialisée physiquement. Au lieu de cela, la requête est exécutée chaque fois que la vue est référencée dans une requête. Lorsqu’un utilisateur crée une vue à partir d’un jeu de données, les règles de contrôle d’accès basées sur les rôles et les attributs pour le jeu de données parent ne sont **appliquées de manière hiérarchique** Par conséquent, vous devez définir explicitement des autorisations sur chacune des colonnes lors de la création d’une vue.

#### Création de restrictions d’accès basées sur les champs sur des jeux de données accélérés {#create-field-based-access-restrictions-on-accelerated-datasets}

Grâce à la fonctionnalité de contrôle d’accès basé sur les attributs [attribute-based access control](../../access-control/abac/overview.md) vous pouvez définir des portées d’utilisation des données ou de l’organisation sur les jeux de données de faits et de dimensions dans la [boutique accélérée](../data-distiller/sql-insights/send-accelerated-queries.md). Cela permet aux administrateurs et administratrices de gérer l’accès à des segments spécifiques et de mieux gérer l’accès accordé aux utilisateurs et utilisatrices ou groupes d’utilisateurs et d’utilisatrices.

Pour créer des restrictions d’accès basées sur les champs sur des jeux de données accélérés, vous pouvez utiliser les requêtes CTAS de Query Service pour créer des jeux de données accélérés et structurer ces jeux de données en fonction des schémas XDM ou des schémas ad hoc existants. Les administrateurs peuvent ensuite [ajouter et modifier des libellés d’utilisation des données pour le schéma](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) ou [schéma ad hoc](./ad-hoc-schema-labels.md#edit-governance-labels). Vous pouvez appliquer, créer et modifier des libellés à vos schémas à partir de l’espace de travail [!UICONTROL Libellés] de l’interface utilisateur [!UICONTROL Schémas].

Les libellés d’utilisation des données peuvent également être [appliqués ou modifiés directement sur le jeu de données](../../data-governance/labels/user-guide.md#add-labels) via l’interface utilisateur des jeux de données, ou créés à partir de l’espace de travail Contrôle d’accès [!UICONTROL Libellés]. Pour plus d’informations, consultez le guide sur la façon de [créer un libellé](../../access-control/abac/ui/labels.md).

L’accès des utilisateurs et utilisatrices à des colonnes individuelles peut ensuite être contrôlé par les libellés d’utilisation des données joints et les jeux d’autorisations appliqués aux rôles affectés aux utilisateurs et utilisatrices.

### Connectivité {#connectivity}

Query Service est accessible via l’interface utilisateur d’Experience Platform ou en formant une connexion avec des clients compatibles externes. L’accès à tous les fronts disponibles est contrôlé par un ensemble d’informations d’identification.

#### Connectivité via des clients externes

L’accès à Query Service à l’aide d’un client tiers nécessite des informations d’identification pour l’autorisation. Ces informations d’identification sont obligatoires pour accéder à Query Service avec l’un des clients externes compatibles. Vous pouvez vous connecter à des clients externes à l’aide des informations d’identification [expirantes](#expiring-credentials) ou [non expirantes](#non-expiring-credentials).

#### Durée de connexion limitée via les informations d’identification arrivant à expiration {#expiring-credentials}

[Informations d’identification arrivant à expiration](../ui/credentials.md) permet aux utilisateurs de former une connexion temporaire avec un client externe. Cet ensemble d’informations d’identification n’est valide que pendant 24 heures. L’expiration de ces types d’informations d’identification est visible avec l’onglet Informations d’identification dans le tableau de bord de Query Service.

![Onglet Informations d’identification de l’espace de travail Query Service avec les informations d’identification arrivant à expiration en surbrillance.](../images/data-governance/overview/expiring-credentials.png)

#### Informations d’identification sans date d’expiration {#non-expiring-credentials}

[Informations d’identification non expirantes](../ui/credentials.md#non-expiring-credentials) vous permettent de former une connexion permanente avec un client externe, ce qui facilite la connexion à Query Service sans avoir besoin d’un mot de passe manuel.

Pour activer l’option de génération d’informations d’identification non expirantes, vous devez suivre le [workflow prérequis](../ui/credentials.md#prerequisites) indiqué. Dans le cadre de ce processus, l’administrateur de votre organisation doit configurer les autorisations pour le profil de produit, ce qui permet à l’administrateur de contrôler les comptes ayant accès à l’utilisation d’informations d’identification non expirantes.

Des rôles peuvent être attribués aux comptes d’utilisateurs et d’utilisatrices techniques autorisés avec des informations d’identification non expirantes afin d’assurer une gouvernance des données appropriée en définissant la portée de leur accès en lecture et écriture en fonction de leurs responsabilités et besoins. Consultez la section précédente sur l’[utilisation d’autorisations basées sur les rôles par le biais du contrôle d’accès](#access-control) pour gérer l’accès à Query Service.

Une fois le workflow prérequis terminé, les utilisateurs autorisés peuvent [générer les informations d’identification de connexion requises](../ui/credentials.md#generate-credentials).

#### Chiffrement des données SSL

Pour une sécurité renforcée, Query Service fournit une prise en charge native des connexions SSL pour chiffrer les communications client/serveur. Experience Platform prend en charge différentes options SSL pour répondre à vos besoins en matière de sécurité des données et équilibrer la charge de traitement du chiffrement et de l’échange de clés.

Pour plus d’informations, notamment sur la connexion à l’aide de la valeur de paramètre SSL `verify-full`, consultez le guide sur les options [SSL disponibles pour les connexions clientes tierces à Query Service](../clients/ssl-modes.md).

### Chiffrement et clés gérées par le client (CMK) {#encryption-and-customer-managed-keys}

Le chiffrement est l’utilisation d’un processus algorithmique pour transformer les données en texte codé et illisible afin de s’assurer que les informations sont protégées et inaccessibles sans clé de déchiffrement.

La conformité des données de Query Service garantit que les données sont toujours chiffrées. Les données en transit sont toujours conformes au protocole HTTPS et les données au repos sont chiffrées dans un magasin Azure Data Lake à l’aide de clés au niveau du système. Pour plus d’informations, consultez la documentation sur [comment les données sont chiffrées dans Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md). Pour plus d’informations sur la manière dont les données au repos sont chiffrées dans Azure Data Lake Storage, consultez la [documentation Azure officielle](https://docs.microsoft.com/fr-fr/azure/data-lake-store/data-lake-store-encryption).

Les données en transit sont toujours conformes au protocole HTTPS. De même, lorsque les données sont au repos dans le lac de données, le chiffrement est effectué avec la clé de gestion du client (CMK), qui est déjà prise en charge par la gestion du lac de données. La version actuellement prise en charge est TLS1.2. Consultez la documentation [clés gérées par le client (CMK)](../../landing/governance-privacy-security/customer-managed-keys/overview.md) pour savoir comment configurer vos propres clés de chiffrement pour les données stockées dans Adobe Experience Platform.


## Journal {#audit}

Query Service enregistre l’activité de l’utilisateur et classe cette activité dans différents types de journaux. Les journaux fournissent des informations sur **qui** a effectué **quoi** action et **quand**. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’ID d’e-mail de l’utilisateur ou de l’utilisatrice qui a exécuté l’action et des attributs supplémentaires liés au type d’action.

Toutes les catégories de journal peuvent être demandées par un utilisateur d’Experience Platform selon ses besoins. Cette section fournit des détails sur le type d’informations capturées pour Query Service et l’endroit où ces informations sont accessibles.

### Journaux de requête {#query-logs}

L’interface utilisateur des journaux de requête vous permet de surveiller et de consulter les détails d’exécution de toutes les requêtes qui ont été exécutées via Query Editor ou l’API Query Service. Cela apporte de la transparence aux activités de Query Service, ce qui vous permet de vérifier les métadonnées de **toutes** les requêtes qui ont été exécutées dans Query Service. Il inclut tous les types de requêtes, qu’il s’agisse d’une requête exploratoire, par lots ou planifiée.

Les journaux de requête sont accessibles via l’interface utilisateur d’Experience Platform dans l’onglet [!UICONTROL  Journaux ] de l’espace de travail [!UICONTROL Requêtes].

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

1. **Journaux de métadonnées de requête** : lorsqu’une requête est exécutée, diverses sous-requêtes principales associées (telles que l’analyse) sont exécutées. Ces types de requêtes sont appelés requêtes « métadonnées ». Leurs détails pertinents se trouvent dans les journaux d’audit.
1. **Journaux de session** : le système crée un journal d’entrée de session pour un utilisateur lorsqu’il se connecte à Query Service, qu’il exécute ou non une requête.
1. **Journaux de connexion client tiers** : un journal d’audit de connectivité est généré lorsqu’un utilisateur connecte correctement Query Service à un client tiers.

Pour plus d’informations sur la manière dont les journaux d’audit peuvent aider votre organisation à aborder la conformité des données, consultez la [ présentation des journaux d’audit ](../../landing/governance-privacy-security/audit-logs/overview.md).

## Utilisation des données {#data-usage}

Le cadre de gouvernance des données dans Experience Platform offre un moyen uniforme d’utiliser les données de manière responsable sur l’ensemble des solutions, services et plateformes Adobe. Il coordonne l’approche systémique de la capture, de la communication et de l’utilisation des métadonnées dans l’ensemble de Adobe Experience Cloud. Cela permet aux contrôleurs de données d’étiqueter les données en fonction des actions marketing nécessaires et des restrictions placées sur ces données à partir de ces actions marketing prévues. Consultez la présentation des [libellés d’utilisation des données](../../data-governance/labels/overview.md) pour plus d’informations sur la manière dont la gouvernance des données vous permet d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs.

Il est recommandé d’œuvrer à la conformité des données à chaque étape du parcours des données. À cette fin, les jeux de données dérivés qui utilisent des schémas ad hoc doivent être étiquetés de manière appropriée dans le cadre de la gouvernance des données. Il existe deux types de jeux de données dérivés formés par Query Service : les jeux de données qui utilisent un schéma standard et les jeux de données qui utilisent un schéma ad hoc.

>[!NOTE]
>
>Les jeux de données créés à l’aide de Query Service sont appelés « jeux de données dérivés ».

Comme les schémas ad hoc sont créés par un utilisateur individuel dans un but spécifique, les champs de schéma XDM sont des espaces de noms pour ce jeu de données spécifique et ne sont pas destinés à être utilisés dans différents jeux de données. Par conséquent, les schémas ad hoc ne sont pas visibles par défaut dans l’interface utilisateur d’Experience Platform. Bien qu’il n’y ait pas de différence dans l’application des libellés d’utilisation des données entre les schémas standard et ad hoc, les schémas ad hoc créés par Query Service à des fins de libellés doivent d’abord être rendus visibles dans l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez le guide sur la [découverte de schémas ad hoc dans l’interface utilisateur d’Experience Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas).

Après avoir accédé au schéma, vous pouvez [appliquer des libellés à des champs individuels](../../xdm/tutorials/labels.md). Une fois qu’un schéma a été libellé, tous les jeux de données qui dérivent de ce schéma héritent de ces libellés. À partir de là, vous pouvez configurer des politiques d’utilisation des données qui peuvent restreindre l’activation des données avec certains libellés vers certaines destinations. Pour plus d’informations, consultez la présentation des [politiques d’utilisation des données](../../data-governance/policies/overview.md).

## Confidentialité    {#privacy}

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
