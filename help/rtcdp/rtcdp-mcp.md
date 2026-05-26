---
solution: Real-Time Customer Data Platform
title: Utilisation des clients MCP (Beta)
description: Découvrez comment connecter Adobe Real-Time CDP aux clients MCP à l’aide du serveur MCP
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 75e294c1e9b24c3d5c2ada99c0db6d1c891ad1e4
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 2%

---

# Utilisation des clients MCP (Beta) {#rtcdp-mcp}

Vous pouvez utiliser l’intégration Adobe Real-Time CDP MCP pour interroger les audiences, les destinations et l’intégrité de l’activation à l’aide d’invites en langage clair, sans écrire d’appels API ni parcourir les écrans du produit. Cette page explique le fonctionnement de l’intégration, ce que vous pouvez en faire et comment commencer.

>[!AVAILABILITY]
>
>Le serveur MCP Real-Time CDP est distribué sous la forme d’un **serveur de transport HTTP distant** que les utilisateurs installent et configurent dans les clients MCP et les plateformes d’applications pris en charge (par exemple, [!DNL Claude], [!DNL ChatGPT], [!DNL Claude Code], [!DNL Codex], [!DNL Cursor] ou [!DNL VS Code]). L’authentification est gérée via un **flux de connexion basé sur un navigateur** — lorsque votre client se connecte pour la première fois au serveur, il ouvre votre navigateur par défaut afin que vous puissiez vous connecter à l’aide de vos informations d’identification Adobe et autoriser l’accès. Contactez votre représentant Adobe pour accéder à ce programme Beta.

## Beta, sécurité et mentions légales {#mcp-notices}

**Remarque sur la documentation de Beta :** cette documentation couvre une fonctionnalité de Beta et ne constitue pas la documentation finale. Le contenu décrit ici se rapporte à une version de Beta et peut être modifié avant sa disponibilité générale. Adobe ne fait aucune déclaration quant à l’exhaustivité ou l’exactitude de cette documentation.

En utilisant le serveur Adobe Real-Time CDP MCP (Beta) (« Beta »), vous reconnaissez que le Beta est fourni **« tel quel », sans garantie d’aucune sorte**. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Beta. Il est recommandé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ce Beta et/ou des éléments qui l’accompagnent. La version Beta est considérée comme étant une information confidentielle dʼAdobe. Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts rencontrés lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ces commentaires.

>[!WARNING]
>
>Le protocole MCP (Model Context Protocol) est une norme open source émergente qui peut présenter des risques pour la sécurité ou la fiabilité. Les intégrations de serveurs Adobe MCP et la documentation associée sont fournies « en l’état », sans garantie d’aucune sorte.
>
>La connexion des clients ou serveurs MCP aux produits Adobe est une configuration choisie par le client. Les clients sont chargés d’évaluer la sécurité et la pertinence de toute intégration MCP. Adobe n’est pas responsable des problèmes résultant d’une mauvaise configuration, d’une utilisation abusive du MCP, de vulnérabilités dans les implémentations tierces ou d’actions involontaires effectuées par le biais de workflows prenant en charge MCP.
>
>Pour réduire les risques, Adobe encourage à tester les intégrations dans un environnement Sandbox avant une utilisation productive, et à examiner et valider soigneusement toutes les actions et réponses initiées par MCP avant de les confirmer ou de s’y fier.

## Qu&#39;est-ce que le protocole de contexte du modèle ? {#mcp-overview}

Les équipes de marketing, de données et d’expérience client s’appuient de plus en plus sur des applications de chat et des outils de développement tels qu’Anthropic Claude, OpenAI ChatGPT, Cursor et Microsoft Copilot Studio pour rationaliser leur travail quotidien. Ces applications prennent en charge le **Model Context Protocol (MCP)**, une norme ouverte qui permet aux applications d’exposer de manière uniforme les outils back-end à des modèles de langage (LLM) volumineux.

Real-Time CDP fournit désormais un serveur MCP qui surface les opérations d’audience, de destination et d’activation directement dans toute application compatible MCP. Grâce à l’intégration de Real-Time CDP MCP, différentes personnes peuvent collaborer autour des mêmes données de segmentation et d’activation, sans avoir à écrire de requêtes sur les API REST de Adobe Experience Platform ni à parcourir plusieurs écrans d’interface utilisateur. Les clients peuvent décrire leur intention par la conversation et laisser le LLM appeler les outils MCP appropriés.

## Fonctionnalités principales {#mcp-capabilities}

Le serveur MCP Real-Time CDP est une surface de surveillance et de triage **lecture seule**. Il expose les API de récupération sur les audiences, les destinations, les sources, les identités et la résolution de profil comme des réponses en langage clair dans votre assistant d’IA, sans écrire de requêtes ni parcourir les écrans de produits. Aucune donnée ne peut être créée, modifiée ou supprimée via le serveur MCP.

>[!IMPORTANT]
>
>Tous les outils du Beta actuel sont **en lecture seule**. Les opérations d’écriture, notamment la création, l’activation, la mise à jour ou la suppression d’audiences, de destinations ou de flux de données, ne sont pas prises en charge.

La version de Beta comprend les 18 outils suivants :

| Outil | Description |
| --- | --- |
| `search_audiences` | Répertoriez et recherchez des audiences par nom, type d’entité, état du cycle de vie, espace de noms d’identité ou origine. |
| `preview_audience_membership` | Estimez la taille d’une expression de segment PQL ou SDD avant de l’enregistrer en tant qu’audience. |
| `inspect_audience_evaluation_jobs` | Récupérez les enregistrements de tâche d’évaluation de segment pour diagnostiquer pourquoi une audience par lots n’est pas actualisée ou pour confirmer l’historique des évaluations récentes. |
| `inspect_audience_export_jobs` | Récupérez les enregistrements de tâche d’exportation d’audience pour confirmer les exportations terminées ou pour afficher les détails de l’échec. |
| | |
| `search_destination_connectors` | Répertorier les types de connecteurs de destination disponibles dans la plateforme (par exemple, [!DNL Amazon S3], [!DNL Google Ads], [!DNL Salesforce] CRM). |
| `search_destination_accounts` | Répertorier les comptes de destination authentifiés : instances configurées d’un type de connecteur de destination. |
| `search_destination_input_connections` | Récupérez l’entrée côté Experience Platform d’un flux de destination : l’audience ou le jeu de données en cours d’exportation. |
| `search_destination_output_connections` | Récupérez le point d’entrée externe d’un flux de destination : chemin d’accès cible, format de fichier et configuration de diffusion. |
| `search_destination_flows` | Répertorier et inspecter les flux d’activation de destination configurés, y compris leur état, leurs mappages et leur planning. |
| `inspect_flow_runs` | Récupérez l’historique d’exécution des flux source et de destination : statut, durée, nombre d’enregistrements et détails d’échec par exécution. |
| | |
| `search_source_connectors` | Répertorier les types de connecteurs source disponibles dans la plateforme. |
| `search_source_accounts` | Répertorier les comptes sources authentifiés : instances configurées d’un type de connecteur source. |
| `search_source_input_connections` | Récupérez la couche de sélection des données d’un flux source, c’est-à-dire ce qui est extrait d’un compte. |
| `search_source_output_connections` | Récupérez la destination du jeu de données Experience Platform d’un flux source (où se trouvent les données ingérées). |
| `search_source_flows` | Répertorier et inspecter les pipelines d’ingestion source configurés, y compris leur état, leurs mappages et leur planning. |
| | |
| `search_identity_namespaces` | Répertorier les définitions d’espaces de noms d’identité dans votre sandbox : espaces de noms standard Adobe et personnalisés. |
| `search_merge_policies` | Répertorier les enregistrements de politique de fusion qui contrôlent la manière dont les profils clients en temps réel sont assemblés à partir des fragments de profil. |
| `search_organizations` | Répertoriez les organisations Adobe accessibles à l’utilisateur authentifié. |

## Cas d’utilisation {#mcp-use-cases}

Le serveur Real-Time CDP MCP est conçu pour la **surveillance et le tri**. Étant donné que le serveur fonctionne avec des identifiants plutôt que des noms, un workflow type commence par une liste : demandez à Claude de vous montrer les éléments disponibles, choisissez l’élément souhaité, puis posez des questions de suivi à l’aide de l’identifiant qu’il renvoie.

| Objectif | Exemple d’invite |
| --- | --- |
| **Liste des audiences** | « Répertorier mes audiences dans le sandbox `prod`. » |
| **Inspecter une audience spécifique** | « Afficher les détails et l’état du cycle de vie pour l’ID d’audience `abc123`. » |
| **Diagnostiquer un échec d’évaluation** | « Affichez les traitements d’évaluation les plus récents et signalez les échecs. » |
| **Vérifier une tâche d’exportation** | « Répertoriez les tâches d’exportation d’audience récentes et affichez le statut de chacune d’elles. » |
| **Estimer la taille de l’audience** | « Estimez la taille de cette expression PQL avant de l’enregistrer : `homeAddress.country = 'US'`. » |
| | |
| **Liste des types de connecteur de destination** | « Quels types de connecteur de destination sont disponibles dans mon sandbox ? » |
| **Liste des comptes de destination configurés** | « Répertorier mes comptes de destination et leur état de connexion. » |
| **Liste des flux de destination** | « Répertorier mes flux d’activation de destination et afficher ceux qui sont activés ou désactivés. » |
| **Inspecter un flux de destination** | « Afficher la configuration complète pour l’ID de flux de destination `xyz789`. » |
| **Vérifier l’intégrité du compte de destination** | « Répertoriez mes comptes de destination et signalez ceux qui sont en état d’erreur. » |
| **Surveiller les exécutions d’activation récentes** | « Afficher les exécutions de flux des dernières 24 heures et signaler les échecs. » |
| **Enquête sur une exécution ayant échoué** | « Affichez-moi l’historique d’exécution de l’ID de flux `xyz789` et résumez les erreurs. » |
| | |
| **Liste des flux sources** | « Répertoriez mes flux d’ingestion sources et affichez leur état actuel. » |
| **Inspecter un flux source** | « Montrez-moi la configuration de l’ID de flux source `src456` - Qu’ingère-t-il et où se trouve-t-il ? » |
| **Vérifier l’intégrité de l’exécution d’ingestion** | « Afficher l’historique d’exécution récent pour les échecs de `src456` d’identifiant de flux source et d’indicateur. » |
| | |
| **Liste des espaces de noms d’identité** | « Quels espaces de noms d’identité sont configurés dans mon sandbox ? » |
| **Liste des politiques de fusion** | « Répertoriez mes politiques de fusion et indiquez laquelle est la valeur par défaut. » |
| **Rechercher l’ID de votre organisation** | « Répertoriez les organisations Adobe auxquelles j’ai accès. » |

## Accès et activation {#mcp-access}

>[!AVAILABILITY]
>
>Le serveur Real-Time CDP MCP est dans Beta et n’est pas ouvert pour l’inscription en libre-service. L’accès se fait sur invitation uniquement et nécessite que votre organisation Adobe soit explicitement placée sur la liste autorisée avant de pouvoir se connecter.

Pour demander l’accès :

1. Contactez votre représentant de compte Adobe (responsable du succès client, gestionnaire de compte technique ou gestionnaire de compte) et exprimez votre intérêt pour le programme Real-Time CDP MCP Beta.
2. Votre représentant Adobe se coordonnera avec l’équipe produit pour évaluer l’éligibilité et activer votre identifiant d’organisation.
3. Une fois activé, votre représentant Adobe confirmera l’accès et fournira tout matériel d’intégration supplémentaire.

>[!NOTE]
>
>Seules les organisations qui ont été explicitement activées peuvent se connecter au serveur MCP Real-Time CDP. Toute tentative de connexion avant l’activation entraînera une erreur d’authentification.

## Conditions préalables {#mcp-prerequisites}

Avant de connecter le serveur Real-Time CDP MCP à votre client MCP, vérifiez les points suivants :

* Vous disposez d’une licence Real-Time CDP active.
* Votre organisation Adobe a été activée pour le programme Beta par votre représentant Adobe (voir [Accès et activation](#mcp-access)).
* Vous avez accès à un client MCP pris en charge, tel que [!DNL Claude], [!DNL ChatGPT], [!DNL Claude Code], [!DNL Codex], [!DNL Cursor] ou [!DNL VS Code].
* Vous disposez de votre identifiant d’organisation et du nom du sandbox sur lequel vous souhaitez effectuer une requête.
* Vous disposez des autorisations nécessaires dans Adobe Experience Platform pour afficher les audiences, les destinations et les entités de service de flux.

## Connexion au serveur MCP Real-Time CDP {#mcp-connect}

Le point d’entrée du serveur MCP Real-Time CDP est le suivant :

```
https://rtcdp-mcp.adobe.io/mcp
```

Le serveur utilise un **transport HTTP distant (HTTP diffusable)** avec un **flux de connexion Adobe basé sur le navigateur**. Pour chaque client, le modèle de configuration est le même :

1. Ajoutez l&#39;URL du serveur : `https://rtcdp-mcp.adobe.io/mcp`
2. Enregistrez ou activez la connexion.
3. Effectuez la **connexion à Adobe à partir d’un navigateur** la première fois que le client appelle un outil.
4. Fournissez des `imsOrgId` et des `sandboxName` au début de chaque session.

### Configuration JSON générale {#mcp-connect-json}

Pour les clients qui acceptent une configuration de serveur MCP basée sur JSON, comme Claude Desktop (`claude_desktop_config.json`), VS Code ou tout client qui lit un fichier `mcp.json`, utilisez l’un des formats suivants selon que votre client prend en charge le protocole HTTP distant natif ou nécessite un pont local :

**Via `mcp-remote` pont (Claude Desktop et autres clients qui nécessitent un pont local)**

```json
{
  "mcpServers": {
    "rtcdp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://rtcdp-mcp.adobe.io/mcp"
      ]
    }
  }
}
```

**HTTP distant natif (clients qui le prennent directement en charge)**

```json
{
  "mcpServers": {
    "rtcdp": {
      "url": "https://rtcdp-mcp.adobe.io/mcp",
      "transport": "http"
    }
  }
}
```

>[!NOTE]
>
>Aucune clé API, aucun jeton porteur ou aucun en-tête supplémentaire n’est requis dans la configuration. L’authentification est entièrement gérée via le flux de connexion Adobe basé sur le navigateur lors de la première utilisation.

### Installation sur des clients basés sur l’interface utilisateur {#mcp-connect-ui}

#### Claude

Pour `claude.ai` et Claude Desktop, ajoutez le serveur Real-Time CDP MCP en tant que **connecteur personnalisé** à l’aide du `https://rtcdp-mcp.adobe.io/mcp` d’URL du serveur.

* **Plans individuels** — Dans Claude, accédez à **Personnaliser → connecteurs**, sélectionnez **Ajouter un connecteur** et saisissez l’URL du serveur.
* **Plans d’équipe et d’entreprise** — Un espace de travail **Propriétaire** ou **Propriétaire de Principal** ajoute le connecteur sous **Paramètres de l’organisation → Connecteurs**. Une fois ajouté, chaque utilisateur l’active dans ses propres paramètres Claude.

Une fois le connecteur ajouté, activez-le dans une conversation et terminez la connexion au navigateur Adobe lors de la première utilisation. Claude découvre automatiquement le serveur d’autorisation d’Adobe ; aucun identifiant ou secret client n’est requis.

#### ChatGPT

Dans [!DNL ChatGPT], ajoutez le serveur Real-Time CDP MCP en tant que **connecteur personnalisé** :

1. Accédez à **Paramètres → connecteurs** (ou **Paramètres → applications et connecteurs**, en fonction de votre formule).
2. Sélectionnez **Ajouter un connecteur** et saisissez `https://rtcdp-mcp.adobe.io/mcp` comme URL du serveur.
3. Enregistrez le connecteur. Selon votre plan de [!DNL ChatGPT], cette étape peut nécessiter l’approbation de l’administrateur de l’espace de travail ou du mode **Développeur**.
4. Une fois le connecteur activé, authentifiez-vous via la connexion au navigateur Adobe lorsque vous y êtes invité lors de la première utilisation.

#### Curseur

Dans Cursor, ajoutez le serveur MCP Real-Time CDP en tant que serveur MCP distant :

1. Ouvrez **Settings → MCP**.
2. Sélectionnez **Ajouter un nouveau serveur** et saisissez `https://rtcdp-mcp.adobe.io/mcp` comme URL du serveur.
3. Sélectionnez **se connecter** pour déclencher la connexion à Adobe à partir du navigateur et l’authentifier.

Une fois connectés, les outils Real-Time CDP sont disponibles dans les modes Compositeur et Agent du curseur.

#### Autres clients basés sur l’interface utilisateur

Pour les clients tels que VS Code ou d’autres applications de bureau et web avec prise en charge de MCP à distance, ajoutez le serveur MCP Real-Time CDP en tant que serveur **HTTP à distance** à l’aide de `https://rtcdp-mcp.adobe.io/mcp`. Si le client prend en charge des en-têtes ou des jetons du porteur facultatifs, laissez-les vides ; l’authentification est gérée via le flux de connexion Adobe basé sur le navigateur lors de la première utilisation.

### Installation dans les clients techniques {#mcp-connect-technical}

#### Claude Code

Ajoutez le serveur à partir du terminal :

```bash
claude mcp add --transport http rtcdp https://rtcdp-mcp.adobe.io/mcp
```

Démarrez ensuite Claude Code et exécutez :

```text
/mcp
```

Sélectionnez le serveur `rtcdp` et terminez le flux de connexion Adobe dans votre navigateur. Si vous avez déjà ajouté le serveur dans `claude.ai`, il peut apparaître automatiquement dans le code Claude lorsque les deux sont connectés au même compte.

#### Codex

Ajoutez le serveur à partir du terminal :

```bash
codex mcp add rtcdp --url https://rtcdp-mcp.adobe.io/mcp
```

Authentifiez le serveur :

```bash
codex mcp login rtcdp
```

Vérifiez la configuration :

```bash
codex mcp list
```

Vous pouvez également ajouter directement le serveur à `~/.codex/config.toml` :

```toml
[mcp_servers.rtcdp]
url = "https://rtcdp-mcp.adobe.io/mcp"
```

### Paramètres de requête requis {#mcp-connect-params}

Chaque appel d’outil nécessite deux paramètres qui définissent la portée de la requête à votre client Adobe Experience Platform :

* `imsOrgId` : votre identifiant d’organisation, mappé à l’en-tête `x-gw-ims-org-id` sur les appels API Experience Platform en aval.
* `sandboxName` : nom du sandbox Experience Platform, mappé à l’en-tête `x-sandbox-name`.

Fournissez-les au début de chaque session. Par exemple :

> « Utilisez les `1234ABCD@AdobeOrg` d’organisation et les `prod` de sandbox pour cette session. »

Si vous ne connaissez pas votre identifiant d’organisation, demandez à votre assistant d’IA d’appeler `search_organizations` . Il affichera chaque organisation à laquelle vos informations d’identification Adobe peuvent accéder.

## Limites connues (Beta) {#mcp-limitations}

Les restrictions suivantes s’appliquent à la version Beta actuelle du serveur MCP [!DNL Adobe Real-Time CDP] :

| Limite | Description | Solution de contournement |
| --- | --- | --- |
| **Surface en lecture seule** | Le serveur MCP n’expose que les API de récupération. Vous ne pouvez pas créer, mettre à jour, activer ou supprimer des audiences, des destinations ou des flux de données. | Utilisez l’interface utilisateur de Real-Time CDP ou les API REST Experience Platform pour les opérations d’écriture. |
| **Aucune mesure d’engagement ou de diffusion** | Le serveur MCP ne renvoie pas les statistiques de diffusion, d’engagement ou de conversion en aval des plateformes de destination. | Utilisez les propres rapports de la plateforme de destination, Customer Journey Analytics MCP ou Adobe Analytics MCP pour les données d’engagement et de conversion. |
| **La requête de segment doit être créée en externe** | `Preview Audience Membership` nécessite une expression PQL ou SDD valide en entrée ; le serveur MCP ne compose pas la requête pour vous. | Créez l’expression PQL/SDD dans l’interface utilisateur du créateur de segments ou via l’API Segmentation Service, puis collez-la dans l’invite MCP. |
| **Pagination via des jetons de continuation** | Les outils de liste renvoient des résultats paginés. L’énumération complète sur de très grands sandbox nécessite le chaînage des appels `continuationToken`. | Requêtes étroites à l’aide de filtres (nom, état, spécification de connexion, période) plutôt que d’énumérer la liste complète. |
| **Le filtrage des exécutions d’activation est uniquement temporel** | `Inspect Activation Runs` prend en charge le filtrage par statut et date et heure d’achèvement (epoch ms UTC), mais pas directement par type d’erreur ou plateforme de destination. | Le filtre par `flowId` (obtenu à partir de `List Configured Destinations`) vers la portée s’exécute vers une destination spécifique. |
| **Identifiant de l’organisation requis au début de la session** | Chaque appel d’outil (à l’exception de `search_organizations`) nécessite `imsOrgId` et `sandboxName` comme paramètres explicites. Si elles ne sont pas fournies, les appels d’outils échouent. | Au début de chaque session, indiquez à votre assistant IA : « Utilisez les `<YOUR_ORG_ID>` d’organisation et les `<SANDBOX_NAME>` de sandbox pour cette session ». Si vous ne connaissez pas votre identifiant d’organisation, appelez-`search_organizations` d’abord. Il renverra les organisations auxquelles vos informations d’identification peuvent accéder. |

## Questions fréquentes {#mcp-faq}

+++Quels clients MCP sont pris en charge ?

Le serveur MCP Real-Time CDP fonctionne avec tout client qui prend en charge les serveurs MCP distants ou les connecteurs personnalisés, notamment [!DNL Claude], [!DNL ChatGPT], [!DNL Claude Code], [!DNL Codex], [!DNL Cursor] et [!DNL VS Code]. Le flux de configuration dépend du client : les clients basés sur l’interface utilisateur ajoutent généralement le serveur à partir d’un panneau de paramètres ou de connecteurs, tandis que les clients techniques tels que Claude Code et Codex peuvent l’ajouter à partir de la ligne de commande ou des fichiers de configuration.
+++

+++Comment puis-je y accéder ?

L’accès se fait sur invitation uniquement pendant la Beta. Contactez votre représentant de compte Adobe (responsable du succès client, gestionnaire de compte technique ou gestionnaire de compte) pour demander une inscription. Votre représentant Adobe se coordonnera avec l’équipe produit pour activer votre organisation. Voir [Accès et activation](#mcp-access) pour plus d’informations.
+++

+++Comment fonctionne l’authentification ?

L’authentification est gérée via une **connexion par navigateur**. Lorsque votre client MCP appelle un outil pour la première fois, il ouvre votre navigateur par défaut à une page de connexion à Adobe. Une fois que vous avez authentifié et autorisé le client, la session est établie et les appels d’outil suivants la réutilisent. Aucune clé d’API ou information d’identification de longue durée ne doit être stockée dans votre configuration client.
+++

+++À quels objets Real-Time CDP puis-je accéder via MCP ?

Vous pouvez accéder aux audiences, aux types de destination, aux comptes de destination configurés, aux flux de données de destination, aux connexions source et cible et à l’historique d’exécution de l’activation. Les opérations sont en lecture seule (récupération des API) ; les opérations d’écriture ne sont pas prises en charge dans la version actuelle.
+++

+++Ai-je besoin d’un accès développeur pour utiliser le serveur MCP Real-Time CDP ?

Non. Le serveur MCP est conçu à la fois pour les professionnels du marketing et pour les techniciens. Les marketeurs peuvent interagir avec celui-ci à l’aide d’invites en langage naturel dans tout client MCP pris en charge, tandis que les ingénieurs de données et les développeurs peuvent l’utiliser dans les outils de développement qui prennent en charge MCP.
+++

