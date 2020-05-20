---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience, 18 novembre 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 19%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 18 novembre 2019**

Nouvelles fonctionnalités d’Adobe Experience Platform :
* [Plateforme des données clients en temps réel](#rtcdp)
* [Destinations](#destinations)
* [Sources](#sources)

Mises à jour des fonctionnalités existantes :
* [Espace de travail Data Science](#dsw)
* [Système de modèle de données d’expérience (XDM)](#xdm)
* [Profil client en temps réel](#profile)
* [Service de segmentation](#segmentation)

## Plateforme des données clients en temps réel {#rtcdp}

Basée sur Adobe Experience Platform, la plate-forme de données clientes en temps réel d’Adobe (CDP en temps réel) aide les sociétés à rassembler des données connues et inconnues pour activer les profils clients avec une prise de décision intelligente tout au long du parcours des clients. La plateforme CDP en temps réel associe plusieurs sources de données d’entreprise pour créer des profils unifiés en temps réel qui peuvent être utilisés pour offrir des expériences client personnalisées et individuelles sur tous les canaux et périphériques.

La plateforme de données client en temps réel comprend des outils de gouvernance des données, de gestion des identités, de segmentation avancée et de science des données, qui vous permettent de créer des profils et de définir des audiences, mais également d’obtenir des informations précieuses tout en étant en mesure d’appliquer des stratégies de gouvernance des données strictes.

Adobe se connecte à un vaste écosystème de partenaires, sans oublier les intégrations natives à Adobe Experience Cloud. Vous pouvez ainsi activer ces audiences en toute simplicité et proposer de superbes expériences client sur tous les canaux, de la personnalisation sur site ou in-app aux e-mails, médias achetés, centres d’appel, appareils connectés, etc.

La plateforme CDP en temps réel vous permet :

* d’obtenir un aperçu unique de votre client grâce à la collecte en flux continu des données client de l’ensemble de l’entreprise ;
* de gérer de manière responsable les profils avec des contrôles de confidentialité et de gouvernance fiables pour les identifiants connus et inconnus ;
* de générer des informations exploitables et d’adapter les audiences grâce à l’IA et à l’apprentissage automatique optimisés par Adobe Sensei et conçus pour les spécialistes marketing ;
* de proposer des expériences personnalisées en temps réel sur l’ensemble des canaux et des destinations.

Pour plus d’informations, voir la documentation [de la plateforme de données clientes en temps réel d’](../../rtcdp/overview.md)Adobe.

**Fonctionnalités clés**

| Fonction | Description |
|---|---|
| Destinations | Intégrations préétablies avec les plateformes de destination prises en charge par la plateforme de données clientes en temps réel d’Adobe, qui activent les données pour ces partenaires de manière transparente. See [Destinations](#destinations) below for more information. |
| tableau de bord des mesures de Page d&#39;accueil | La page d&#39;accueil Adobe Real-time Customer Data Platform (CDP en temps réel) comprend un tableau de bord de mesures qui affiche des informations sur les profils et les segments. La page d&#39;accueil contient également des liens vers des documents d&#39;apprentissage. Voir la section sur les mesures [de plateforme de données client en temps](#real-time-customer-data-platform-metrics) réel ci-dessous. |
| Sources | Vous pouvez envoyer des données à partir de différentes sources, notamment les solutions Adobe, le stockage dans le cloud, des logiciels tiers et la gestion de la relation client. Consultez la section [Sources](#sources) ci-dessous pour en savoir plus. |

**Mesures de la plateforme de données clientes en temps réel**

La page d’accueil de la plateforme de données client (CDP) en temps réel d’Adobe inclut un tableau de bord de mesures et s’affiche lorsque vous vous connectez à la plateforme CDP en temps réel.

La page d’accueil n’est qu’un des emplacements où les cartes de mesures apparaissent. La plateforme CDP en temps réel fournit des cartes de mesure tout au long de votre expérience. Ces mesures indiquent les données, les profils et les audiences de segments du système.

Si le système ne contient aucune donnée lorsque vous vous connectez à la plateforme CDP en temps réel, le tableau de bord de la page d’accueil n’apparaît pas. Dans ce cas, la page d’accueil propose des ressources pédagogiques pour une première expérience client. Au fur et à mesure de la collecte des données, le tableau de bord se met automatiquement à jour pour afficher des informations sur ces données.

Pour en savoir plus, voir la présentation des mesures de la plateforme de données clientes en temps [réel](../../rtcdp/home-page-dashboards.md)

## Destinations {#destinations}

Les destinations sont des intégrations préétablies avec les plateformes de destination prises en charge par la plateforme de données clientes en temps réel d’Adobe, qui activent les données de manière transparente pour ces partenaires. Pour plus d’informations, consultez l’article Présentation [des](../../rtcdp/destinations/destinations-overview.md) Destinations.

**Destinations disponibles**

Avec la version de novembre, la plateforme de données clientes en temps réel d’Adobe prend en charge les destinations suivantes :

* Publicité : Google
* Marketing par courriel : Adobe Campaign, Salesforce Marketing Cloud, Oracle Responsys, Oracle Eloqua

Consultez le catalogue [de](../../rtcdp/destinations/destinations-catalog.md) destination pour en savoir plus sur chacune des destinations.

**Limitations connues**

* La commande permettant d’autoriser les planifications d’activations personnalisées dans le flux [d’](../../rtcdp/destinations/activate-destinations.md#activate-data) activation (étape de planification) n’est pas disponible avec la version initiale.
* Il n&#39;existe actuellement aucun moyen de modifier ou de supprimer une configuration de destination. Pour contourner cette restriction, vous pouvez activer ou désactiver la destination dans le coin supérieur droit de la page [des détails de la](../../rtcdp/destinations/destination-details-page.md)destination.
* Aucune validation n’est actuellement en place pour les détails, le chemin ou les informations d’identification du compte lors de la connexion à votre compte de destination ou d’enregistrement. Assurez-vous de saisir les informations d’identification appropriées et vérifiez par doublon si vous avez rencontré des fautes d’orthographe ou des fautes de frappe.
* Aucun renouvellement des informations d’identification n’est en place avec la version initiale. Une fois qu’un compte a expiré ou doit être actualisé, vous devez créer une nouvelle connexion de destination et remapper les segments précédemment mappés.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plate-forme. Vous pouvez ingérer des données à partir de diverses sources, telles qu’Adobe Solutions, un enregistrement cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent de vous authentifier sur vos systèmes d’enregistrement et services de gestion de la relation client, de définir les heures d’exécution d’assimilation et de gérer le débit d’assimilation des données.

**Fonctionnalités clés**

| Fonction | Description |
| ---------- | ------------ |
| IU Sources | Nouvelle interface utilisateur pour la création, l’affichage et la gestion des connexions source. |
| workflows reconfigurés pour les connecteurs CRM | Nouveau flux de travail intuitif de l&#39;interface utilisateur pour la création et la gestion des connecteurs Microsoft Dynamics et Salesforce. |
| Prise en charge des connecteurs pour les enregistrements basés sur le cloud | Les connecteurs peuvent désormais accéder aux enregistrements basés sur le cloud. Les nouvelles sources incluent les serveurs Amazon S3, Azure Blob et FTP/SFTP. |

**Problèmes connus**

* Les connecteurs source pour les enregistrements basés sur le cloud ne prennent pas en charge l’assimilation de fichiers compressés.

Pour plus d’informations sur les sources, consultez [Présentation des sources](../../sources/home.md).

## Espace de travail Data Science {#dsw}

L’espace de travail Data Science d’Adobe Experience Platform permet aux spécialistes des données de générer en toute transparence des informations issues des données et du contenu sur les applications Adobe et les systèmes tiers en créant et en mettant en oeuvre des modèles d’apprentissage automatique. Data Science Workspace est étroitement intégré à la plate-forme et alimente le cycle de vie des données de bout en bout, y compris l&#39;exploration et la préparation des données XDM, puis le développement et l&#39;exploitation de modèles pour enrichir automatiquement le Profil client en temps réel avec des connaissances d&#39;apprentissage automatique.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Accès aux données à l’aide du SDK de plate-forme | Les ordinateurs portables de lancement et Recettes préconfigurés en Python utilisent maintenant Platform SDK pour accéder aux données. |
| Prise en charge des sandbox | Prise en charge de la prochaine fonctionnalité de sandbox (actuellement en version bêta), y compris la possibilité d&#39;isoler les blocs-notes et les Recettes dans des sandbox de développement ou de production. See the [sandboxes overview](../../sandboxes/home.md) for more information. |

Pour plus d’informations, voir l’aperçu [de](../../data-science-workspace/home.md)Data Science Workspace.

## Système de modèle de données d’expérience (XDM) {#xdm}

La normalisation et l’interopérabilité sont des concepts clés de la plate-forme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec les services d’Adobe Experience Platform. En respectant les normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune offrant des informations d’une manière plus rapide et plus intégrée. Vous pouvez obtenir des informations précieuses sur les actions client, définir des audiences client par le biais de segments et utiliser les attributs client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ---------- | ------------ |
| schéma de notification | Nouveau schéma qui représente les données de notification envoyées pendant le processus d’assimilation des données. |
| schémas Adobe AdCloud DSP | Cinq nouveaux schémas ont été ajoutés pour représenter les métadonnées DSP (Adobe Advertising Cloud Demand-side platform) : Placement, Campaign, Package, Annonceur, Compte. |
| Mélange des détails d’implémentation d’ExperienceEvent | Nouveau mixin ExperienceEvent qui ajoute un champ standard pour stocker des informations sur le logiciel utilisé pour collecter le événement. |
| Mélange de confidentialité Profil | Nouveau mixin de profil qui ajoute des champs pour accepter les signaux généraux d’exclusion et d’exclusion de vente/partage pour le Profil client en temps réel. |
| Contraintes de format pour `xdm:alternateDisplayInfo` | Les champs &quot;Titre&quot; et &quot;Description&quot; pour `xdm:alternateDisplayInfo` doivent tous deux être des chaînes pour que la validation soit réussie. |
| Modification du nom : Profil XDM individuel | Le &quot;titre&quot; de la classe &quot;Profil XDM&quot; a été mis à jour en &quot;Profil individuel XDM&quot;. La forme `$id` de la classe n&#39;a pas changé. |

**Problèmes connus**

* Aucun.

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API de registre de Schéma et de l&#39;interface utilisateur de l&#39;éditeur de Schémas, consultez la documentation [du système](../../xdm/home.md)XDM.

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet de proposer à vos clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Grâce au Profil client en temps réel, vous pouvez voir une vue holistique de chaque client qui combine les données de plusieurs canaux, y compris les données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonction | Description |
| -----------| ---------- |
| Améliorations apportées à la recherche de Profil | Les utilisateurs peuvent désormais rechercher des profils à l’aide de descripteurs de référence et d’entités associées. |
| Nettoyer les données d’un jeu de données donné | Les utilisateurs peuvent désormais supprimer des données pour un jeu de données ou un lot donné à l’aide de l’API Tâches du système de Profil. |
| Améliorations de la requête Edge Profil | Les applications peuvent désormais requête au Profil Edge en fonction de l’une des identités d’un profil donné. |
| Configurer des stratégies de fusion par projection | Les applications peuvent désormais configurer les stratégies de fusion par projection afin de générer une vue des données telle que régie par une stratégie de fusion spécifique. |
| Attributs calculés | Les attributs calculés calculent automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés s’appliquent au niveau du profil à des valeurs d’agrégat telles que &quot;achat total&quot;, &quot;valeur de durée de vie&quot; ou &quot;état d’entonnoir&quot; en fonction d’un événement entrant, d’un événement et de données de profil entrants, ou d’un événement entrant, de données de profil et de événements historiques. |

**Corrections de bogues**

* liste simplifiée des stratégies d’assemblage d’ID disponibles dans le processus de création de stratégies de fusion.

**Problèmes connus**

* Aucun.

Pour plus d’informations sur le Profil client en temps réel, y compris des didacticiels et les bonnes pratiques pour travailler avec les données de Profil, consultez la Présentation [du Profil client en temps](../../profile/home.md)réel.

## Service de segmentation {#segmentation}

Le service de segmentation de la plateforme Adobe Experience Platform fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données de Profil client en temps réel. Ces segments sont configurés et conservés de manière centralisée sur la plate-forme, ce qui les rend facilement accessibles par toute application Adobe.

Le service de segmentation définit un sous-ensemble particulier de profils en décrivant les critères qui distinguent un groupe de personnes commercialisables au sein de votre base de clients. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries chronologiques représentant les interactions des clients avec votre marque.

| Fonction | Description |
| -----------| ---------- |
| Segmentation planifiée | Les utilisateurs peuvent désormais activer l’évaluation des segments planifiée pour tous les segments via l’interface utilisateur et l’API. Une fois activés, tous les segments sont évalués une fois par jour. Cela n’affecte pas les capacités de segmentation à la demande qui continuent de fonctionner comme auparavant.<br/><br/>Remarque : La fonction de segmentation planifiée ne peut pas être utilisée dans des sandbox avec plus de cinq stratégies de fusion pour un Profil XDM individuel. |
| Segmentation en flux continu | La prise en charge de l’évaluation continue des segments (segmentation en flux continu) permet à la plupart des règles de segmentation d’être évaluées au fur et à mesure que les données sont transmises à la plate-forme. Cette fonctionnalité signifie que l’adhésion au segment sera à jour sans qu’il soit nécessaire d’exécuter des tâches de segmentation planifiées. Certaines exceptions s’appliquent, telles que les segments qui utilisent des relations multientités ou des charges utiles enrichies. |
| Segments en tant que blocs de création | Lors de la création de segments à l’aide de l’interface utilisateur du créateur de segments, les utilisateurs peuvent désormais utiliser des segments précédemment définis comme blocs de création pour d’autres segments. <ul><li>Référencer l&#39;appartenance à l&#39;audience actuelle : à mesure que les gens entrent et sortent des audiences.</li><li>Copier la logique : prenez la définition de segment sélectionnée et duplicata-la dans le nouveau segment.</li></ul> |
| Appartenance au segment de Vue par espace de nommage d’ID | L’appartenance à un segment peut désormais être vue par espace de nommage d’ID (courrier électronique, ECID et nombre total). |
| Prise en charge RBAC | Le créateur de segments prend désormais en charge les contrôles d&#39;accès et autorisations de base basés sur les rôles. |
| Amélioration de la prise en charge du partage des audiences externes entre les solutions Adobe et Platform | Les utilisateurs peuvent désormais importer des métadonnées d’audience externes (hors Plate-forme d’expérience) dans les cas où le nombre d’audiences est élevé ou n’est pas connu a priori. Cette version comprend l’accès aux métadonnées d’Audience Manager pour les clients qui ont configuré le connecteur de solution. Ces métadonnées d’audience peuvent être utilisées dans le créateur de segments pour créer de nouveaux segments de plateforme d’expérience. <br/><br/> En outre, les segments créés dans Experience Platform seront désormais disponibles pour une utilisation dans les solutions Adobe intégrées, y compris Audience Manager, Cible et Ad Cloud. |

**Corrections de bogues**

* Correction d’un problème en raison duquel la segmentation multientité renvoyait zéro profil en cas de relations imbriquées.
* Correction d’un problème en raison duquel la logique d’exclusion renvoyait des résultats trompeurs.
* Amélioration de la lisibilité des dossiers à plusieurs entités. Ils affichent désormais le nom convivial de la classe XDM.
* Correction d’un problème intermittent en raison duquel plusieurs copies du même dossier XDM s’affichaient.
* La messagerie est maintenant générée pour informer un utilisateur si les estimations de segments ne sont pas disponibles pour la stratégie de fusion sélectionnée.

**Problèmes connus**

* Aucun.

Pour en savoir plus sur le service de segmentation, consultez la présentation [du service de](../../segmentation/home.md)segmentation.