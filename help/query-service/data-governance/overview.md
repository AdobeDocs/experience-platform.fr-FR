---
title: Gouvernance des données dans Query Service
description: Cette présentation couvre les principaux éléments de la gouvernance des données dans Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '3129'
ht-degree: 1%

---

# Gouvernance des données dans Query Service

Adobe Experience Platform rassemble les données de plusieurs systèmes d’entreprise et vous permet de nettoyer, de formater, de manipuler et d’enrichir les données par le biais de Query Service selon vos besoins. Cela permet aux marketeurs d’identifier, de comprendre et d’impliquer les clients de manière plus efficace. Assurer une gouvernance adéquate des données est un aspect essentiel de la gestion des informations personnelles, car certaines données peuvent être soumises à des restrictions d’utilisation basées sur les politiques organisationnelles et les réglementations juridiques. Il est essentiel de s’assurer que vos données ingérées et les opérations associées sont conformes aux politiques d’utilisation des données définies.

La gouvernance des données dans Query Service vous permet de gérer les données client et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Cela joue un rôle clé lorsque vous vous assurez que les stratégies d’utilisation ont été appliquées conformément aux réglementations définies par votre entreprise.

Les organisations qui effectuent régulièrement le traitement des données doivent décrire, appliquer et appliquer ces directives afin de créer un environnement soucieux de la confidentialité pour tous les utilisateurs.

Les catégories suivantes sont essentielles pour respecter les réglementations de conformité des données lors de l’utilisation de Query Service :

1. Sécurité
1. Journal
1. Utilisation des données
1. Confidentialité   
1. Hygiène des données

Ce document examine chacun des différents domaines de gouvernance et montre comment faciliter la conformité des données lors de l’utilisation de Query Service. Consultez la [présentation de la gouvernance, de la confidentialité et de la sécurité](../../landing/governance-privacy-security/overview.md) pour plus d’informations sur la manière dont Experience Platform vous permet de gérer les données client et d’assurer la conformité.

## Sécurité {#security}

La sécurité des données est le processus qui consiste à protéger les données contre les accès non autorisés et à garantir un accès sécurisé tout au long de son cycle de vie. L’accès sécurisé est conservé dans Experience Platform par l’application des rôles et des autorisations par des fonctionnalités telles que le contrôle d’accès basé sur les rôles et le contrôle d’accès basé sur les attributs. Les informations d’identification, le protocole SSL et le cryptage des données sont également utilisés pour assurer la protection des données dans Platform.

La sécurité relative à Query Service est divisée en plusieurs catégories :

* [Contrôle d’accès](#access-control) : l’accès est contrôlé par le biais de rôles et d’autorisations, y compris les autorisations de niveau jeu de données et colonne.
* Sécurisation des données par l’intermédiaire de la [connectivité](#connectivity) : les données sont sécurisées par le biais de clients Platform et externes en établissant une connexion limitée avec des informations d’identification arrivant à expiration ou des informations d’identification non arrivant à expiration.
* Sécurisation des données par le biais de [clés de cryptage et de gestion client (CMK)](#encryption-and-customer-managed-keys) : accès contrôlé par le cryptage lorsque les données sont au repos.

### Contrôle d’accès {#access-control}

Le contrôle d’accès dans Adobe Experience Platform vous permet d’utiliser [Adobe Admin Console](https://adminconsole.adobe.com/) pour gérer l’accès aux fonctionnalités de Query Service à l’aide d’autorisations basées sur les rôles. De même, vous pouvez contrôler l’accès à des attributs de données spécifiques par le biais de la gestion des libellés sur les schémas et les champs de données.

Cette section décrit les autorisations de contrôle d’accès requises qu’un utilisateur doit posséder pour utiliser pleinement les fonctionnalités de Query Service. Pour obtenir des instructions détaillées sur l’attribution de l’accès à un profil de produit, consultez les documents sur les [autorisations de gestion](../../access-control/ui/permissions.md) et la [gestion des utilisateurs](../../access-control/ui/users.md) .

#### Autorisations pertinentes

Les permissions de contrôle d&#39;accès appropriées sont définies dans les tableaux ci-dessous en fonction de leur niveau de portée.

**Autorisations d’exécution de requête**

Pour exécuter des requêtes dans Query Service, un utilisateur doit se voir attribuer un rôle avec l’autorisation suivante :

| Autorisation | Description |
|---|---|
| [!UICONTROL Gestion des requêtes] | Cette autorisation permet aux utilisateurs d’exécuter des explorations de données et des requêtes par lots, qui peuvent soit lire un jeu de données existant, soit écrire des données sur des jeux de données. Cela inclut les requêtes `CREATE TABLE AS SELECT` (`CTAS`) et `INSERT INTO AS SELECT` (`ITAS`). |

**Autorisations des jeux de données**

Cette section sert de guide pour l’accès en fonction des ressources requis pour accéder aux jeux de données lors de l’interrogation de données via Query Service.

Grâce à l’interface d’autorisations, vous pouvez définir un contrôle d’accès basé sur les ressources pour un jeu de données et un schéma avec les autorisations suivantes :

| Autorisation | Description |
|---|---|
| [!UICONTROL Gestion des jeux de données] | Cette autorisation fournit un accès en lecture seule aux schémas et permet d’accéder à la lecture, la création, la modification et la suppression de jeux de données à utiliser avec Query Service. |
| [!UICONTROL Affichage des jeux de données] | Cette autorisation permet un accès en lecture seule aux jeux de données et aux schémas à utiliser avec Query Service. |

#### Contrôle d’accès pour les colonnes/champs

La fonctionnalité de contrôle d’accès basé sur les attributs permet aux utilisateurs de Query Service de restreindre l’accès aux données utilisateur critiques. L’accès peut être accordé ou restreint en fonction des autorisations affectées à un rôle. L’accès des utilisateurs à des colonnes individuelles est contrôlé par les libellés d’utilisation des données pertinents et les jeux d’autorisations appliqués aux rôles affectés aux utilisateurs.

Le balisage des groupes de champs de schéma et des classes avec des libellés d’utilisation des données applique des restrictions d’utilisation des données à tous les schémas avec les mêmes groupes et classes de champs. Pour obtenir des informations complètes sur cette fonctionnalité, consultez la présentation du [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md) .

Cette fonctionnalité vous permet d’accorder des droits d’accès sur des colonnes confidentielles aux groupes d’utilisateurs de votre choix. Le contrôle d’accès sur une colonne peut restreindre les fonctionnalités de lecture et d’écriture pour un type particulier d’utilisateur.

Le contrôle d’accès des colonnes peut être appliqué au niveau du schéma pour les schémas standard et ad hoc. Appliquez des libellés d’utilisation des données aux schémas XDM pour restreindre l’accès à une ou plusieurs colonnes. L’étiquetage des données est appliqué de manière cohérente, même pour les jeux de données créés via Query Service à l’aide d’un schéma prédéfini ou d’un schéma ad hoc généré dans le cadre de l’opération CTAS.

Une fois le niveau d’accès approprié appliqué à l’aide de libellés et de rôles, le comportement système suivant se produit lorsqu’un utilisateur tente d’accéder aux données non accessibles :

1. Si un utilisateur s’est vu refuser l’accès à l’une des colonnes d’un schéma, il se voit également refuser l’autorisation de lire ou d’écrire sur la colonne restreinte. Cela s’applique aux scénarios courants suivants :

   * **Cas 1** : lorsqu’un utilisateur tente d’exécuter une requête affectant uniquement une colonne restreinte, le système renvoie une erreur que la colonne n’existe pas.
   * **Cas 2** : lorsqu’un utilisateur tente d’exécuter une requête avec plusieurs colonnes, y compris une colonne restreinte, le système renvoie une sortie pour toutes les colonnes non restreintes uniquement.

1. Si un utilisateur tente d&#39;accéder à un champ calculé, il doit avoir accès à tous les champs utilisés dans la composition ou le système lui refuse également l&#39;accès au champ calculé.

#### Contrôles d’accès pour les vues

Query Service permet d’utiliser le langage SQL ANSI standard pour les instructions [`CREATE VIEW`](../sql/syntax.md#create-view). Pour les workflows de données hautement sensibles, vous devez appliquer les contrôles appropriés lors de la création de vues.

Le mot-clé `CREATE VIEW` définit une vue d’une requête, mais la vue n’est pas matérialisée physiquement. Au lieu de cela, la requête est exécutée chaque fois que la vue est référencée dans une requête. Lorsqu’un utilisateur crée une vue à partir d’un jeu de données, les règles de contrôle d’accès basées sur les rôles et les attributs du jeu de données parent sont **et non** hiérarchiquement appliquées. Par conséquent, vous devez définir explicitement des autorisations sur chacune des colonnes lors de la création d’une vue.

#### Création de restrictions d’accès basées sur les champs sur les jeux de données accélérés {#create-field-based-access-restrictions-on-accelerated-datasets}

Avec la [fonctionnalité de contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md), vous pouvez définir des portées d’utilisation des données ou organisationnelles sur les jeux de données de faits et de dimensions dans la [boutique accélérée](../data-distiller/sql-insights/send-accelerated-queries.md). Cela permet aux administrateurs de gérer l’accès à des segments spécifiques et de mieux gérer l’accès attribué aux utilisateurs ou groupes d’utilisateurs.

Pour créer des restrictions d’accès basées sur les champs sur des jeux de données accélérés, vous pouvez utiliser les requêtes CTAS de Query Service pour créer des jeux de données accélérés et structurer ces jeux de données en fonction de schémas XDM ou de schémas ad hoc existants. Les administrateurs peuvent ensuite [ajouter et modifier des libellés d’utilisation des données pour le schéma](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) ou le [schéma ad hoc](./ad-hoc-schema-labels.md#edit-governance-labels). Vous pouvez appliquer, créer et modifier des libellés à vos schémas à partir de l’espace de travail [!UICONTROL Étiquettes] de l’interface utilisateur [!UICONTROL Schémas].

Les libellés d’utilisation des données peuvent également être [appliqués ou modifiés directement sur le jeu de données](../../data-governance/labels/user-guide.md#add-labels) via l’interface utilisateur des jeux de données, ou créés à partir de l’espace de travail [!UICONTROL Étiquettes] du contrôle d’accès. Pour plus d’informations, consultez le guide sur la création d’une nouvelle étiquette [1} .](../../access-control/abac/ui/labels.md)

L’accès des utilisateurs à des colonnes individuelles peut ensuite être contrôlé par les libellés d’utilisation des données joints et les jeux d’autorisations appliqués aux rôles affectés aux utilisateurs.

### Connectivité {#connectivity}

Query Service est accessible par le biais de l’interface utilisateur de Platform ou en établissant une connexion avec des clients externes compatibles. L’accès à tous les fronts disponibles est contrôlé par un ensemble d’informations d’identification.

#### Connectivité par le biais de clients externes

L’accès à Query Service à l’aide d’un client tiers nécessite des informations d’identification pour l’autorisation. Ces informations d’identification sont obligatoires pour accéder à Query Service avec l’un des clients externes compatibles. Vous pouvez vous connecter à des clients externes à l’aide des [informations d’identification arrivant à expiration](#expiring-credentials) ou des [informations d’identification non arrivant à expiration](#non-expiring-credentials).

#### Délai de connexion limité via l’expiration des informations d’identification {#expiring-credentials}

[Les informations d’identification d’expiration](../ui/credentials.md) permettent aux utilisateurs de former une connexion temporaire avec un client externe. Cet ensemble d’informations d’identification n’est valide que pendant 24 heures. L’expiration de ces types d’informations d’identification est visible avec l’onglet Informations d’identification dans le tableau de bord Query Service.

![L’onglet des informations d’identification dans l’espace de travail Query Service avec les informations d’identification arrivant à expiration sont surlignées.](../images/data-governance/overview/expiring-credentials.png)

#### Informations d’identification sans date d’expiration {#non-expiring-credentials}

[Les informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials) vous permettent de former une connexion permanente avec un client externe, ce qui facilite la connexion à Query Service sans avoir besoin d’un mot de passe manuel.

Pour activer l’option de génération d’informations d’identification non arrivant à expiration, vous devez suivre le [workflow prérequis](../ui/credentials.md#prerequisites) décrit. Dans le cadre de ce processus, l’administrateur de votre organisation doit configurer des autorisations pour le profil de produit, ce qui permet à l’administrateur de contrôler quels comptes ont accès pour utiliser des informations d’identification qui n’expirent pas.

Les comptes d’utilisateurs techniques autorisés avec des informations d’identification non arrivant à expiration peuvent se voir attribuer des rôles pour garantir une gouvernance des données appropriée en définissant la portée de leur accès en lecture et écriture en fonction de leurs responsabilités et besoins. Consultez la section précédente sur [ l’utilisation d’autorisations basées sur les rôles par le biais du contrôle d’accès](#access-control) pour gérer l’accès à Query Service.

Une fois le workflow prérequis terminé, les utilisateurs autorisés peuvent désormais [générer les informations d’identification de connexion requises](../ui/credentials.md#generate-credentials).

#### Cryptage des données SSL

Pour une sécurité accrue, Query Service fournit une prise en charge native des connexions SSL pour chiffrer les communications client/serveur. Platform prend en charge diverses options SSL pour répondre à vos besoins en matière de sécurité des données et équilibrer les frais de traitement liés au cryptage et à l’exchange des clés.

Pour plus d’informations, notamment sur la connexion à l’aide de la valeur de paramètre SSL `verify-full`, consultez le guide sur les options [SSL disponibles pour les connexions de clients tiers à Query Service](../clients/ssl-modes.md) .

### Chiffrement et clés gérées par le client (CMK) {#encryption-and-customer-managed-keys}

Le cryptage est l’utilisation d’un processus algorithmique pour transformer les données en texte codé et illisible, afin de garantir que les informations sont protégées et inaccessibles sans clé de décryptage.

La conformité des données de Query Service garantit que les données sont toujours cryptées. Les données en transit sont toujours conformes au protocole HTTPS et les données au repos sont chiffrées dans un magasin Azure Data Lake à l’aide de clés au niveau du système. Pour plus d’informations, consultez la documentation sur le [mode de cryptage des données dans Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md) . Pour plus d’informations sur la façon dont les données au repos sont chiffrées dans Azure Data Lake Storage, consultez la [documentation Azure officielle](https://docs.microsoft.com/fr-fr/azure/data-lake-store/data-lake-store-encryption).

Les données en transit sont toujours conformes au protocole HTTPS. De même, lorsque les données sont au repos dans le lac de données, le chiffrement est effectué avec la clé de gestion client (CMK), qui est déjà prise en charge par Data Lake Management. La version actuellement prise en charge est TLS1.2. Consultez la [ documentation sur les clés gérées par le client (CMK)](../../landing/governance-privacy-security/customer-managed-keys/overview.md) pour savoir comment configurer vos propres clés de chiffrement pour les données stockées dans Adobe Experience Platform.


## Journal {#audit}

Query Service enregistre l’activité de l’utilisateur et classe cette activité dans différents types de journaux. Consigne les informations d’approvisionnement sur **who** a effectué l’action **what** et **when**. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’e-mail de l’utilisateur qui a exécuté l’action et des attributs supplémentaires liés au type d’action.

Toutes les catégories de journaux peuvent être demandées selon vos besoins par un utilisateur de Platform. Cette section fournit des détails sur le type d’informations capturées pour Query Service et l’emplacement d’accès à ces informations.

### Journaux de requête {#query-logs}

L’interface utilisateur des logs de requête vous permet de surveiller et de consulter les détails d’exécution de toutes les requêtes qui ont été exécutées via Query Editor ou l’API Query Service. Cela apporte de la transparence aux activités de Query Service, ce qui vous permet de vérifier les métadonnées de **tous** les requêtes qui ont été exécutées sur Query Service. Il comprend tous les types de requêtes, qu’il s’agisse d’une requête exploratoire, de lot ou planifiée.

Les journaux de requêtes sont accessibles via l’interface utilisateur de Platform dans l’onglet [!UICONTROL Journaux] de l’espace de travail [!UICONTROL  Requêtes].

![Onglet Journal des requêtes avec le panneau des détails en surbrillance.](../images/data-governance/overview/queries-log.png)

### Journaux d’audit {#audit-logs}

Les journaux d’audit contiennent des informations plus détaillées que les journaux de requête et vous permettent de filtrer les journaux en fonction d’attributs tels que l’utilisateur, la date, le type de requête, etc. Outre les détails disponibles dans l’interface utilisateur du journal de requête, les journaux d’audit stockent les détails sur les utilisateurs individuels, ainsi que leurs données de session ou leur connectivité à un client tiers.

En fournissant un enregistrement exact des actions des utilisateurs, un journal d’audit peut vous aider à résoudre les problèmes et à aider votre entreprise à respecter efficacement les politiques de gestion des données de l’entreprise et les exigences réglementaires. Les journaux d’audit fournissent un enregistrement de toutes les activités de Platform. Grâce aux journaux d’audit, vous pouvez contrôler les actions des utilisateurs concernant l’exécution des requêtes, les modèles et les requêtes planifiées afin d’accroître la transparence et la visibilité des actions effectuées par les utilisateurs dans Query Service.

Le tableau suivant indique les catégories de requêtes capturées par les journaux d’audit et les types d’actions qu’ils enregistrent :

| Catégorie | Type d’action |
|---|---|
| Requête | Exécuter |
| Modèle de requête | Créer, supprimer, mettre à jour |
| Requête planifiée | Créer, supprimer, mettre à jour |

Vous trouverez ci-dessous une liste de trois journaux de serveur étendus qui contiennent plus de détails que ceux trouvés dans les journaux de requête. Les journaux étendus se trouvent dans les catégories de requête des journaux d’audit :

1. **Meta query logs** : lorsqu’une requête est exécutée, différentes sous-requêtes du serveur principal associées (telles que l’analyse) sont exécutées. Ces types de requêtes sont appelés requêtes de &quot;métadonnées&quot;. Vous trouverez leurs informations pertinentes dans les journaux d’audit.
1. **Journaux de session** : le système crée un journal d’entrée de session pour un utilisateur lorsqu’il se connecte à Query Service, qu’il exécute une requête ou non.
1. **Journaux de connexion client tiers** : un journal d’audit de connectivité est généré lorsqu’un utilisateur connecte Query Service à un client tiers.

Pour plus d’informations sur la manière dont les journaux d’audit peuvent aider votre entreprise à approcher la conformité des données, consultez la [présentation des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md) .

## Utilisation des données {#data-usage}

Le cadre de gouvernance des données de Platform fournit un moyen uniforme d’utiliser les données de manière responsable sur toutes les solutions, services et plateformes d’Adobe. Il coordonne l’approche systémique de la capture, de la communication et de l’utilisation des métadonnées dans l’ensemble de Adobe Experience Cloud. Cela permet aux contrôleurs de données d’étiqueter les données en fonction des actions marketing nécessaires et des restrictions imposées à ces données à partir des actions marketing prévues. Pour plus d’informations sur la manière dont la gouvernance des données vous permet d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, consultez la présentation sur les [libellés d’utilisation des données](../../data-governance/labels/overview.md) .

Il est recommandé d’oeuvrer à la conformité des données à chaque étape du parcours des données. À cette fin, les jeux de données dérivés qui utilisent des schémas ad hoc doivent être correctement étiquetés dans le cadre de la gouvernance des données. Il existe deux types de jeux de données dérivés formés par Query Service : les jeux de données qui utilisent un schéma standard et les jeux de données qui utilisent un schéma ad hoc.

>[!NOTE]
>
>Les jeux de données créés à l’aide de Query Service sont appelés &quot;jeux de données dérivés&quot;.

Comme les schémas ad hoc sont créés par un utilisateur individuel à des fins spécifiques, les champs de schéma XDM sont des espaces de noms pour ce jeu de données spécifique et ne sont pas destinés à être utilisés dans différents jeux de données. Par conséquent, les schémas ad hoc ne sont pas visibles par défaut dans l’interface utilisateur Experience Platform. Bien qu’il n’y ait aucune différence dans l’application des libellés d’utilisation des données entre les schémas standard et ad hoc, les schémas ad hoc créés par Query Service à des fins d’étiquetage doivent d’abord être rendus visibles dans l’interface utilisateur de Platform. Pour plus d’informations, consultez le guide sur la [découverte de schémas ad hoc dans l’interface utilisateur de Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) .

Après avoir accédé au schéma, vous pouvez [appliquer des libellés à des champs individuels](../../xdm/tutorials/labels.md). Une fois qu’un schéma a été étiqueté, tous les jeux de données qui dérivent de ce schéma héritent de ces libellés. À partir de là, vous pouvez configurer des stratégies d’utilisation des données qui peuvent restreindre l’activation de certaines destinations aux données avec certains libellés. Pour plus d’informations, consultez la présentation des [stratégies d’utilisation des données](../../data-governance/policies/overview.md).

## Confidentialité    {#privacy}

[Privacy Service](../../privacy-service/home.md) vous aide à gérer les demandes de clients pour accéder à leurs données et les supprimer conformément aux réglementations légales en matière de confidentialité. Pour ce faire, il recherche les données pour les identifiants préexistants et accède ou supprime ces données en fonction de la tâche de confidentialité demandée. Les données doivent disposer de libellés appropriés afin que le service puisse déterminer les champs auxquels accéder ou ceux qu’il doit supprimer au cours des tâches relatives à la confidentialité. Les données qui font l’objet de demandes d’accès à des informations personnelles doivent contenir des informations d’identité client afin de lier les différents éléments de données à la personne à laquelle la demande d’accès à des informations personnelles s’applique. Query Service peut enrichir les données qu’il utilise avec un identifiant unique afin de répondre aux tâches de confidentialité.

Les demandes d’accès à des informations personnelles peuvent être envoyées au lac de données ou à l’entrepôt de données Profile. Les enregistrements supprimés du lac de données n’entraînent pas la suppression des profils qui ont été créés à partir de ces enregistrements. En outre, une tâche de suppression des informations personnelles du lac de données ne supprime pas leur profil. Par conséquent, toute information (qui contient cet identifiant de profil) ingérée après la fin de la tâche de confidentialité met à jour ce profil normalement. Cela confirme la nécessité d’identifier correctement les données utilisées dans les schémas ad hoc.

Consultez la documentation du Privacy Service pour plus d’informations sur les [données d’identité pour les demandes d’accès à des informations personnelles](../../privacy-service/identity-data.md) et sur la configuration de vos opérations de données et l’utilisation des technologies d’Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.

Les fonctionnalités de Query Service pour la gouvernance des données simplifient et rationalisent le processus de catégorisation des données et d’adhésion aux réglementations sur l’utilisation des données. Une fois les données identifiées, Query Service vous permet d’affecter l’identité principale à tous les jeux de données de sortie. Vous **devez** ajouter des identités dans le jeu de données pour faciliter les demandes de confidentialité des données et travailler à la conformité des données.

Les champs de données de schéma peuvent être définis en tant que champ d’identité via l’interface utilisateur de Platform et Query Service vous permet également de [marquer les identités principales à l’aide de la commande SQL &#39;ALTER TABLE&#39;](../sql/syntax.md#alter-table). La définition d’une identité à l’aide de la commande `ALTER TABLE` est particulièrement utile lorsque des jeux de données sont créés à l’aide de SQL plutôt que directement à partir d’un schéma via l’interface utilisateur de Platform. Consultez la documentation pour obtenir des instructions sur la [définition de champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md) lors de l’utilisation de schémas standard.

## Hygiène des données {#data-hygiene}

L’hygiène des données désigne le processus de réparation ou de suppression de données susceptibles d’être obsolètes, inexactes, mal formatées, dupliquées ou incomplètes. Ces processus garantissent que les jeux de données sont précis et cohérents sur tous les systèmes. Il est important d’assurer une hygiène adéquate des données à chaque étape du parcours des données et même à partir de l’emplacement de stockage initial des données. Dans Experience Platform Query Service, il s’agit du lac de données ou de la boutique accélérée.

Vous pouvez affecter une identité à un jeu de données dérivé pour permettre à leur gestion des données de suivre les services d’hygiène des données centralisés de Platform.

Inversement, lorsque vous créez un jeu de données agrégé sur le magasin accéléré, les données agrégées ne peuvent pas être utilisées pour dériver les données d’origine. Grâce à cette agrégation de données, la nécessité d’augmenter les demandes d’hygiène des données est éliminée.

Une exception à ce scénario est le cas de la suppression. Si une suppression de l’hygiène des données est demandée sur un jeu de données et avant que la suppression ne soit terminée, une autre requête de jeu de données dérivé est exécutée, alors le jeu de données dérivé capturera les informations du jeu de données d’origine. Dans ce cas, vous devez garder à l’esprit que si une demande de suppression d’un jeu de données a été envoyée, vous ne devez pas exécuter de requêtes de jeu de données nouvellement dérivées utilisant la même source de jeu de données.

Pour plus d’informations sur l’hygiène des données dans Adobe Experience Platform, consultez la [présentation de l’hygiène des données](../../hygiene/home.md) .
