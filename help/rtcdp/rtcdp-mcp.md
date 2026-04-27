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
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 8a9dd740bb210ef125bca65a8358bb6b51f6d28f
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 2%

---

# Utilisation des clients MCP (Beta) {#rtcdp-mcp}

Vous pouvez utiliser l’intégration Adobe Real-Time CDP MCP pour interroger les audiences, les destinations et l’intégrité de l’activation à l’aide d’invites en langage clair, sans écrire d’appels API ni parcourir les écrans du produit. Cette page explique le fonctionnement de l’intégration, ce que vous pouvez en faire et comment commencer.

>[!AVAILABILITY]
>
>Le serveur MCP Real-Time CDP est distribué sous la forme d’un **serveur de transport HTTP distant** que les utilisateurs installent et configurent dans les clients MCP et les plateformes d’application pris en charge (par exemple, Claude, ChatGPT, Claude Code, Codex, Cursor ou VS Code). L’authentification est gérée via un **flux de connexion basé sur un navigateur** — lorsque votre client se connecte pour la première fois au serveur, il ouvre votre navigateur par défaut afin que vous puissiez vous connecter à l’aide de vos informations d’identification Adobe et autoriser l’accès. Contactez votre représentant Adobe pour accéder à ce programme Beta.

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

Le serveur Real-Time CDP MCP vous permet d’inspecter, de résumer et de résoudre les problèmes d’audiences et de destinations directement à partir de votre assistant d’IA. Toutes les opérations sont **lecture seule** — les surfaces du serveur MCP récupèrent les API comme réponses en langage clair afin que vous puissiez :

* **Obtenir une visibilité instantanée de l’audience** — Renseignez-vous sur les définitions d’audience, l’état du cycle de vie et l’espace de noms en langage clair sans parcourir les menus ni extraire manuellement les rapports.
* **Estimer la taille de l’audience avant l’activation** — Prévisualisez le nombre d’adhésions et les intervalles de confiance pour une requête de segment PQL ou SDD avant de vous engager à créer une audience.
* **Auditer votre portfolio d’activation** — Examiner les destinations configurées, les flux de données qui les alimentent et les connexions source/cible derrière chaque flux — sans analyser JSON ni passer d’un écran à l’autre.
* **Problèmes d’activation par spot au début** — La destination en échec ou en cours de la surface s’exécute au moment où vous demandez, afin que votre équipe puisse agir rapidement.
* **Collaborer autour des données actives** — Les spécialistes du marketing, les ingénieurs de données et les parties prenantes peuvent tous interroger les mêmes données Live Real-Time CDP par l’intermédiaire de leur assistant d’IA, ce qui facilite l’alignement, la prise de décision et le déplacement ensemble.

## Outils disponibles {#mcp-tools}

La disponibilité des outils change rapidement à mesure que nous activons de nouveaux outils. Contactez votre représentant ou représentante Adobe pour obtenir une liste des derniers outils disponibles.

>[!NOTE]
>
>Tous les outils sont **en lecture seule**. Les opérations d’écriture (création, mise à jour ou suppression d’audiences, de destinations ou de flux de données) ne sont pas prises en charge dans la version actuelle de Beta.

## Cas d’utilisation {#mcp-use-cases}

Les exemples suivants montrent comment interagir avec le serveur MCP [!DNL Adobe Real-Time CDP] à l’aide du langage naturel :

| Objectif | Exemple d’invite |
| --- | --- |
| **Découverte de catalogue de destinations** | « TikTok est-il disponible en tant que destination dans mon sandbox ? » / « Pour quels types de destination des comptes sont-ils déjà configurés ? » |
| **Inventaire de destination par type** | « Répertorier toutes mes destinations Amazon S3. » / « Des destinations d’exportation de jeux de données sont-elles configurées ? » |
| **Audit de la configuration de destination** | « Dans quel compartiment ma destination `Loyalty S3 Export` écrit-elle ? » / « Afficher le chemin d’accès cible et le format de fichier pour le flux de données [ID]. » |
| **Santé du compte** | « Lequel de mes comptes de destination possède des informations d’identification expirées ? » / « Des comptes Pinterest ou Facebook sont-ils en erreur ? » |
| **Intégrité de l’activation - dernières 24 heures** | « Répertoriez toutes les destinations dont l’exécution a échoué au cours des dernières 24 heures. » / « Ma destination d’exportation de jeu de données a-t-elle envoyé des données au cours des dernières 24 heures ? » |
| **Historique des activations par destination** | « Avez-`Weekly Loyalty Export` exporté quoi que ce soit au cours des 30 derniers jours ? » / « Afficher l’historique d’exécution complet des {NAME} de destination. » |
| **Analyse des échecs** | « Quelle est la raison d’échec la plus courante dans mes destinations basées sur des fichiers cette semaine ? » / « Regrouper les exécutions récentes ayant échoué par type d’erreur. » |
| **Découverte et filtrage d’audiences** | « Répertoriez chaque audience basée sur un fichier CSV dans le sandbox `marketing-prod`. » / « Quelles audiences ont un ID d’audience externe défini ? » |
| **Audit du dimensionnement de l’audience** | « Montrez-moi chaque audience de taille 0. » / « Quelles audiences comptent plus de 1 000 profils ? » |
| **Audit de l’expiration des audiences** | « Quelles destinations ont des audiences dont la date de fin est déjà dépassée ? » / « Répertoriez les audiences dont l’expiration est prévue au cours des 7 prochains jours. » |
| **Empreinte d’activation de l’audience** | « Quelles destinations ont plus de 10 audiences activées ? » / « Quelle audience est activée pour le plus de destinations ? » |
| **Filtre croisé : audience × activation** | « Affichez-moi les audiences dont la taille est supérieure à 1 000 et qui sont activées sur au moins 2 destinations. » / « Audiences volumineuses qui ne sont activées que vers une seule destination. » |
| **Aperçu de l’appartenance à une audience** | « Prévisualisez la taille de l’abonnement pour l’audience `High-Value Loyalty Members`. » / « Estimez la taille de cette requête PQL avant de l’enregistrer : {EXPRESSION}. » |

## Conditions préalables {#mcp-prerequisites}

Avant de connecter le serveur Real-Time CDP MCP à votre client MCP, vérifiez les points suivants :

* Vous disposez d’une licence Real-Time CDP active.
* Vous avez accès à un client pris en charge qui peut se connecter à un serveur MCP distant ou à une application MCP personnalisée, comme Claude, ChatGPT, Claude Code, Codex, Cursor ou VS Code.
* Vous disposez de votre identifiant d’organisation et du nom du sandbox sur lequel vous souhaitez effectuer une requête.
* Vous disposez des autorisations nécessaires dans Adobe Experience Platform pour afficher les audiences, les destinations et les entités de service de flux.

## Connexion au serveur MCP Real-Time CDP {#mcp-connect}

>[!NOTE]
>
>Cette intégration est disponible dans Beta. Les menus client, les exigences de plan et les contrôles d’administration peuvent varier en fonction de l’application et de la version.

Avant de commencer, vérifiez que vous disposez des éléments suivants :

* URL du point d’entrée du serveur MCP : `Available to Beta customers through your Adobe representative`.
* Confirmation que votre utilisateur Adobe a accès à l’organisation Experience Platform et au sandbox cibles.

Le serveur MCP Real-Time CDP est un **serveur MCP HTTP distant**. Pour chaque client, la configuration suit le même modèle :

1. Ajoutez l’URL du serveur .
2. Enregistrez ou activez la connexion.
3. Effectuez la **connexion à Adobe à partir d’un navigateur** la première fois que le client appelle un outil.
4. Fournissez des `imsOrgId` et des `sandboxName` pour chaque requête.

### Installation sur des clients basés sur l’interface utilisateur {#mcp-connect-ui}

#### Claude

Pour `claude.ai` et Claude Desktop, ajoutez le serveur Real-Time CDP MCP en tant que **connecteur personnalisé** à l’aide du point d’entrée fourni par votre représentant Adobe. Dans les plans Claude individuels, ajoutez-le sous **Personnaliser > Connecteurs**. Dans les plans Équipe et Entreprise, un propriétaire peut avoir besoin de l&#39;ajouter d&#39;abord sous **Paramètres de l&#39;organisation > Connecteurs**, après quoi chaque utilisateur le connecte dans ses propres paramètres Claude. Une fois configuré, activez le connecteur dans une conversation et effectuez la connexion au navigateur Adobe lors de la première utilisation.

#### ChatGPT

Dans ChatGPT, ajoutez le serveur Real-Time CDP MCP en tant qu’application/connecteur **personnalisé** à l’aide du point d’entrée fourni par votre représentant Adobe. Selon votre plan ChatGPT, cela peut nécessiter l’approbation de **mode Développeur** et de l’administrateur de l’espace de travail. Une fois l’application/le connecteur créé ou activé, connectez-le à partir de **Paramètres > Applications** ou **Paramètres > Applications et connecteurs**, puis authentifiez-le via la connexion au navigateur Adobe lorsque vous y êtes invité.

#### Curseur

Dans Cursor, ajoutez le serveur MCP Real-Time CDP en tant que serveur MCP distant à l’aide du point d’entrée fourni par votre représentant Adobe. Ouvrez **Paramètres > MCP**, ajoutez un nouveau serveur et collez l’URL du point d’entrée. Une fois l’ajout effectué, activez le serveur pour votre espace de travail en sélectionnant **se connecter** pour vous authentifier via le navigateur.

#### Autres clients basés sur l’interface utilisateur

Pour les clients tels que VS Code ou d’autres applications de bureau et web avec prise en charge de MCP à distance, ajoutez le serveur MCP Real-Time CDP en tant que serveur **HTTP à distance** à l’aide du point d’entrée fourni par votre représentant Adobe. Si le client prend en charge des en-têtes ou des jetons du porteur facultatifs, laissez-les vides, sauf instruction contraire spécifique d’Adobe. L’authentification est gérée via le flux de connexion Adobe basé sur le navigateur lors de la première utilisation.

### Installation dans les clients techniques {#mcp-connect-technical}

#### Claude Code

Ajoutez le serveur à partir du terminal :

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

Démarrez ensuite Claude Code et exécutez :

```text
/mcp
```

Sélectionnez le serveur `rtcdp` et terminez le flux de connexion Adobe dans votre navigateur. Si vous avez déjà ajouté le serveur dans `claude.ai`, il peut également apparaître automatiquement dans le code Claude lorsque les deux utilisent le même compte.

#### Codex

Ajoutez le serveur à partir du terminal :

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
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
url = "<endpoint provided by your Adobe representative>"
```

### Paramètres de requête requis {#mcp-connect-params}

Chaque appel d’outil nécessite deux paramètres qui définissent la portée de la requête :

* `imsOrgId` : votre identifiant d’organisation, mappé à l’en-tête `x-gw-ims-org-id` sur les appels API Experience Platform en aval.
* `sandboxName` : nom du sandbox Experience Platform, mappé à l’en-tête `x-sandbox-name`.

## Limites connues (Beta) {#mcp-limitations}

Les restrictions suivantes s’appliquent à la version Beta actuelle du serveur MCP [!DNL Adobe Real-Time CDP] :

| Limite | Description | Solution de contournement |
| --- | --- | --- |
| **Surface en lecture seule** | Le serveur MCP n’expose que les API de récupération. Vous ne pouvez pas créer, mettre à jour, activer ou supprimer des audiences, des destinations ou des flux de données. | Utilisez l’interface utilisateur de Real-Time CDP ou les API REST AEP pour les opérations d’écriture. |
| **Aucune mesure d’engagement ou de diffusion** | Le serveur MCP ne renvoie pas les statistiques de diffusion, d’engagement ou de conversion en aval des plateformes de destination. | Utilisez les propres rapports de la plateforme de destination, Customer Journey Analytics MCP ou Adobe Analytics MCP pour les données d’engagement et de conversion. |
| **La requête de segment doit être créée en externe** | `Preview Audience Membership` nécessite une expression PQL ou SDD valide en entrée ; le serveur MCP ne compose pas la requête pour vous. | Créez l’expression PQL/SDD dans l’interface utilisateur du créateur de segments ou via l’API Segmentation Service, puis collez-la dans l’invite MCP. |
| **Pagination via des jetons de continuation** | Les outils de liste renvoient des résultats paginés. L’énumération complète sur de très grands sandbox nécessite le chaînage des appels `continuationToken`. | Requêtes étroites à l’aide de filtres (nom, état, spécification de connexion, période) plutôt que d’énumérer la liste complète. |
| **Le filtrage des exécutions d’activation est uniquement temporel** | `Inspect Activation Runs` prend en charge le filtrage par statut et date et heure d’achèvement (epoch ms UTC), mais pas directement par type d’erreur ou plateforme de destination. | Le filtre par `flowId` (obtenu à partir de `List Configured Destinations`) vers la portée s’exécute vers une destination spécifique. |
| **Configuration de la région requise** | Les appels d’outils échouent avec le HTTP 403 « La région de l’utilisateur est manquante » si la passerelle MCP n’est pas configurée pour la région de votre utilisateur. | Contactez votre représentant Adobe pour confirmer que la passerelle est configurée pour votre région avant la première utilisation. |

## Questions fréquentes {#mcp-faq}

+++Quels clients MCP sont pris en charge ?

Le serveur Real-Time CDP MCP fonctionne avec des clients pris en charge qui peuvent se connecter à des serveurs MCP distants ou à des applications MCP personnalisées, notamment Claude, ChatGPT, Claude Code, Codex, Cursor et VS Code. Le flux de configuration dépend du client : les clients basés sur l’interface utilisateur ajoutent généralement le serveur à partir des paramètres, tandis que les clients techniques tels que Claude Code et Codex peuvent l’ajouter à partir de la ligne de commande ou des fichiers de configuration.
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

+++Mes données sont-elles envoyées au fournisseur du client MCP ?

Lorsque vous envoyez une invite, le client MCP peut envoyer le contexte approprié (y compris les données Real-Time CDP renvoyées par le serveur MCP) à son modèle pour traitement. Consultez les politiques de confidentialité et de gestion des données de votre fournisseur client MCP avant de vous connecter aux données de production.
+++

+++De quelles autorisations ai-je besoin dans Real-Time CDP ?

Vous avez besoin au minimum d’autorisations **Affichage** pour les objets que vous souhaitez interroger : audiences, destinations et entités de service de flux. Aucune autorisation d’écriture n’est requise, car le serveur MCP effectue uniquement des opérations de lecture. Contactez votre administrateur [!DNL Adobe Experience Platform] si vous n’êtes pas sûr de votre niveau d’accès actuel.
+++

+++Puis-je utiliser le serveur MCP dans les environnements Sandbox ?

Oui. Chaque appel d’outil nécessite un paramètre `sandboxName`. De ce fait, le serveur MCP respecte toujours la configuration de votre sandbox [!DNL Adobe Experience Platform]. Vous pouvez interroger n’importe quel sandbox auquel vous avez accès en spécifiant son nom dans votre invite.
+++

+++Quelle est la différence entre Prévisualiser l’appartenance à l’audience et rechercher des audiences existantes ?

`Search Existing Audiences` renvoie les audiences qui ont déjà été créées et enregistrées dans votre sandbox. `Preview Audience Membership` prend une expression de segment PQL ou SDD brute et renvoie une estimation de taille pour celle-ci, ce qui est utile pour dimensionner une requête *avant* vous l’enregistrez en tant qu’audience.
+++

+++Puis-je interroger les audiences de compte ainsi que les audiences de profil ?

Oui. `Search Existing Audiences` et `Preview Audience Membership` prennent en charge un paramètre de type d’entité. Les audiences de profil peuvent être exprimées en PQL ou en SDD ; les audiences de compte utilisent toujours la syntaxe SDD (relationnelle).
+++
