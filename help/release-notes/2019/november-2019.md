---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 18 novembre 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 18 novembre 2019**

Nouvelles fonctionnalités d’Adobe Experience Platform :
* [Plateforme des données clients en temps réel](#rtcdp)
* [Destinations](#destinations)
* [Sources](#sources)

Mises à jour des fonctionnalités existantes :
* [Espace de travail Data Science](#dsw)
* [Système XDM (Experience Data Model)](#xdm)
* [Profil client en temps réel](#profile)
* [Service de segmentation](#segmentation)

## Plateforme des données clients en temps réel {#rtcdp}

Basée sur Adobe Experience Platform, la plate-forme de données clientes en temps réel d’Adobe (CDP en temps réel) permet aux de rassembler des données connues et inconnues afin d’activer le client avec une prise de décision intelligente tout au long du parcours du client. La plateforme CDP en temps réel associe plusieurs sources de données d’entreprise pour créer des profils unifiés en temps réel qui peuvent être utilisés pour offrir des expériences client personnalisées et individuelles sur tous les canaux et périphériques.

La plateforme de données client en temps réel comprend des outils de gouvernance des données, de gestion des identités, de segmentation avancée et de science des données, qui vous permettent de créer des profils et de définir des audiences, mais également d’obtenir des informations précieuses tout en étant en mesure d’appliquer des stratégies de gouvernance des données strictes.

Adobe se connecte à un vaste écosystème de partenaires, sans oublier les intégrations natives à Adobe Experience Cloud. Vous pouvez ainsi activer ces audiences en toute simplicité et proposer de superbes expériences client sur tous les canaux, de la personnalisation sur site ou in-app aux e-mails, médias achetés, centres d’appel, appareils connectés, etc.

La plateforme CDP en temps réel vous permet :

* d’obtenir un aperçu unique de votre client grâce à la collecte en flux continu des données client de l’ensemble de l’entreprise ;
* de gérer de manière responsable les profils avec des contrôles de confidentialité et de gouvernance fiables pour les identifiants connus et inconnus ;
* de générer des informations exploitables et d’adapter les audiences grâce à l’IA et à l’apprentissage automatique optimisés par Adobe Sensei et conçus pour les spécialistes marketing ;
* de proposer des expériences personnalisées en temps réel sur l’ensemble des canaux et des destinations.

Pour plus d’informations, reportez-vous à la documentation [de la plateforme de données clientes en temps réel d’](../../rtcdp/overview.md)Adobe.

**Fonctionnalités clés**

| Fonction | Description |
|---|---|
| Destinations | Intégrations prédéfinies aux plateformes de destination prises en charge par la plateforme de données clientes en temps réel d’Adobe, qui activent les données de manière transparente vers ces partenaires. See [Destinations](#destinations) below for more information. |
| de mesures  | Le Adobe Real-time Customer Data Platform (CDP en temps réel) comprend un de mesures qui présente des informations sur les  et les segments de la base de données. Le  contient également des liens vers des documents d’apprentissage. Voir la section sur les mesures [de plateforme de données clientes en temps](#real-time-customer-data-platform-metrics) réel ci-dessous. |
| Sources | Vous pouvez envoyer des données à partir de différentes sources, notamment les solutions Adobe, le stockage dans le cloud, des logiciels tiers et la gestion de la relation client. Consultez la section [Sources](#sources) ci-dessous pour en savoir plus. |

**Mesures de la plateforme de données clientes en temps réel**

La page d’accueil de la plateforme de données client (CDP) en temps réel d’Adobe inclut un tableau de bord de mesures et s’affiche lorsque vous vous connectez à la plateforme CDP en temps réel.

La page d’accueil n’est qu’un des emplacements où les cartes de mesures apparaissent. La plateforme CDP en temps réel fournit des cartes de mesure tout au long de votre expérience. Ces mesures indiquent les données, les profils et les audiences de segments du système.

Si le système ne contient aucune donnée lorsque vous vous connectez à la plateforme CDP en temps réel, le tableau de bord de la page d’accueil n’apparaît pas. Dans ce cas, la page d’accueil propose des ressources pédagogiques pour une première expérience client. Au fur et à mesure de la collecte des données, le se met automatiquement à jour pour afficher des informations sur ces données.

Pour en savoir plus, reportez-vous à la présentation des mesures de la plateforme de données clientes en temps [réel](../../rtcdp/home-page-dashboards.md)

## Destinations {#destinations}

Les destinations sont des intégrations prédéfinies avec les plateformes de destination prises en charge par la plateforme de données clientes en temps réel d’Adobe, qui activent les données de manière transparente vers ces partenaires. Pour plus d’informations, consultez l’article Présentation [des](../../rtcdp/destinations/destinations-overview.md) destinations.

**Destinations disponibles**

Avec la version de novembre, la plateforme de données clientes en temps réel d’Adobe prend en charge les destinations suivantes :

* Publicité : Google
* Marketing par courriel :  Adobe Campaign, Salesforce Marketing Cloud, Oracle Responsys, Oracle Eloqua

Consultez le catalogue [de](../../rtcdp/destinations/destinations-catalog.md) destination pour en savoir plus sur chacune des destinations.

**Limitations connues**

* Le contrôle permettant d’autoriser les planifications de  de  personnalisées dans le flux [de](../../rtcdp/destinations/activate-destinations.md#activate-data) (étape Planifier) n’est pas disponible avec la version initiale.
* Il n’existe actuellement aucun moyen de modifier ou de supprimer une configuration de destination. Pour contourner cette limitation, vous pouvez activer ou désactiver la destination dans le coin supérieur droit de la page [des détails de la](../../rtcdp/destinations/destination-details-page.md)destination.
* Aucune validation n’est actuellement en place pour les détails, le chemin ou les informations d’identification du compte lors de la connexion à votre destination ou  compte . Assurez-vous de saisir les informations d’identification appropriées et -vérifiez les fautes d’orthographe ou les fautes de frappe.
* Aucun renouvellement des informations d’identification n’est en place avec la version initiale. Une fois qu’un compte a expiré ou doit être actualisé, vous devez créer une nouvelle connexion de destination et remapper les segments précédemment mappés.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plateforme. Vous pouvez assimiler des données à partir de diverses sources, telles qu’Adobe Solutions, des  basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent de vous authentifier auprès de vos  systèmes  et services de gestion de la relation client, de définir les heures d’exécution de l’assimilation et de gérer le débit d’assimilation des données.

**Fonctionnalités clés**

| Fonction | Description |
| ---------- | ------------ |
| Interface utilisateur Sources | Nouvelle interface utilisateur pour la création, l’affichage et la gestion des connexions source. |
|  de restructuré pour les connecteurs CRM | Nouveau flux de travail intuitif de l’interface utilisateur pour la création et la gestion des connecteurs Microsoft Dynamics et Salesforce. |
| Prise en charge des connecteurs pour les  basés sur le cloud  | Les connecteurs peuvent désormais accéder aux  de  basés sur le cloud. Les nouvelles sources incluent les serveurs Amazon S3, Azure Blob et FTP/SFTP. |

**Problèmes connus**

* Les connecteurs source pour les  basés sur le cloud ne prennent pas en charge l’assimilation de fichiers compressés.

Pour plus d’informations sur les sources, consultez [Présentation des sources](../../sources/home.md).

## Espace de travail Data Science {#dsw}

L’espace de travail Data Science d’Adobe Experience Platform permet aux spécialistes des données de générer en toute transparence des informations à partir des données et du contenu dans les applications Adobe et les systèmes tiers en créant et en mettant en oeuvre des modèles d’apprentissage automatique. Data Science Workspace est étroitement intégré à la plate-forme et alimente le cycle de vie des données de bout en bout, y compris l&#39;exploration et la préparation des données XDM, puis le développement et la mise en oeuvre de modèles pour enrichir automatiquement les  de clients en temps réel avec des connaissances d&#39;apprentissage automatique.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Accès aux données à l’aide du SDK de plateforme | Les ordinateurs portables Recettes précompilés et lanceurs en Python utilisent désormais Platform SDK pour accéder aux données. |
| Prise en charge des sandbox | Prise en charge de la prochaine fonctionnalité de sandbox (actuellement en version bêta), notamment la possibilité d’isoler les blocs-notes et les recettes dans des sandbox de développement ou de production. See the [sandboxes overview](../../sandboxes/home.md) for more information. |

Pour plus d’informations, voir la présentation [de](../../data-science-workspace/home.md)Data Science Workspace.

## Système XDM (Experience Data Model) {#xdm}

La normalisation et l’interopérabilité sont les concepts clés de la plateforme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des  pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des  de  clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ---------- | ------------ |
|  de notification | Nouveau  qui représente les données de notification envoyées pendant le processus d’assimilation des données. |
| Adobe AdCloud DSP  | Cinq nouveaux  ont été ajoutés pour représenter les métadonnées DSP (Adobe Advertising Cloud Demand-side Platform) : Placement, Campaign, Package, Annonceur, Compte. |
| Mixage des détails d’implémentation d’ExperienceEvent | Nouveau mixin ExperienceEvent qui ajoute un champ standard pour stocker des informations sur le logiciel utilisé pour collecter les  du. |
|  de confidentialité | Nouveau  de mixage qui ajoute des champs pour accepter les signaux généraux d’exclusion et d’exclusion de vente/partage pour le client en temps réel. |
| Contraintes de format pour `xdm:alternateDisplayInfo` | Les champs &quot;Titre&quot; et &quot;Description&quot; pour `xdm:alternateDisplayInfo` doivent tous deux être des chaînes pour réussir la validation. |
| Modification du nom :  de XDM individuel | Le &quot;titre&quot; de la classe &quot;XDM&quot; a été mis à jour vers &quot;XDM Individuel&quot;. La forme `$id` de la classe n&#39;a pas changé. |

**Problèmes connus**

* Aucun.

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API de registre des et de l&#39;interface utilisateur de l&#39;éditeur de  de, consultez la documentation [du système](../../xdm/home.md)XDM.

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir à vos clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Avec le  Client en temps réel, vous pouvez voir un holistique de chaque client qui combine les données de plusieurs , y compris les données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonction | Description |
| -----------| ---------- |
| Améliorations apportées à la recherche  | Les utilisateurs peuvent désormais rechercher des  à l’aide de descripteurs de référence et d’entités associées. |
| Nettoyer les données d’un jeu de données donné | Les utilisateurs peuvent désormais supprimer les données d’un jeu de données ou d’un lot donné à l’aide de l’API Tâches  système. |
| Améliorations des  du Edge  | Les applications peuvent désormais  Edge  par l’une des identités d’un certain. |
| Configuration des stratégies de fusion par projection | Les applications peuvent désormais configurer des stratégies de fusion par projection afin de générer un  des données tel que régi par une stratégie de fusion spécifique. |
| Attributs calculés | Les attributs calculés calculent automatiquement la valeur des champs en fonction d’autres valeurs, calculs et  de . Les attributs calculés s’appliquent au niveau  du pour  les valeurs de  telles que &quot;achat total&quot;, &quot;valeur de durée de vie&quot; ou &quot;état de l’entonnoir&quot; en fonction d’un entrant, d’un entrant et de données de l’, ou encore d’une valeur entrante, de données de l’algorithme de l’algorithme et de l’algorithme. |

**Corrections de bogues**

* simplifié des stratégies d’assemblage d’ID disponibles dans le processus de création de stratégies de fusion.

**Problèmes connus**

* Aucun.

Pour plus d’informations sur les  des clients en temps réel, y compris des didacticiels et les bonnes pratiques pour travailler avec les données de , veuillez lire la Présentation [de l’](../../profile/home.md)des clients en temps réel.

## Service de segmentation {#segmentation}

Le service de segmentation de la plate-forme Adobe Experience Platform fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer   à partir de vos données de client en temps réel. Ces segments sont configurés et maintenus de manière centralisée sur la plateforme, ce qui les rend facilement accessibles par n’importe quelle application Adobe.

Le service de segmentation définit un sous-ensemble particulier de  de en décrivant les critères qui distinguent un groupe de personnes commercialisables au sein de votre base de clients. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des de séries chronologiques représentant les interactions des clients avec votre marque.

| Fonction | Description |
| -----------| ---------- |
| Segmentation planifiée | Les utilisateurs peuvent désormais activer l’évaluation des segments planifiée pour tous les segments via l’interface utilisateur et l’API. Une fois activés, tous les segments sont évalués une fois par jour. Cela n’affecte pas les capacités de segmentation à la demande qui continuent de fonctionner comme auparavant.<br/><br/>Remarque : La fonction de segmentation planifiée ne peut pas être utilisée dans des sandbox avec plus de cinq stratégies de fusion pour les  XDM individuels. |
| Segmentation en flux continu | La prise en charge de l’évaluation continue des segments (segmentation en flux continu) permet à la plupart des règles de segmentation d’être évaluées au fur et à mesure que les données sont transmises à la plateforme. Cette fonctionnalité signifie que l’adhésion au segment sera à jour sans qu’il soit nécessaire d’exécuter des tâches de segmentation planifiées. Certaines exceptions s’appliquent, comme les segments qui utilisent des relations multientités ou des charges enrichies. |
| Segments comme blocs de création | Lors de la création de segments à l’aide de l’interface utilisateur du créateur de segments, les utilisateurs peuvent désormais utiliser des segments précédemment définis comme blocs de création pour d’autres segments. <ul><li>Référencez l&#39;appartenance  actuelle à l&#39; : se met à jour au fur et à mesure que les gens entrent et sortent de  .</li><li>Copier la logique : prenez la définition de segment sélectionnée et -la dans le nouveau segment.</li></ul> |
| Appartenance au segment  par ID   | L’appartenance à un segment peut désormais être affichée par  d’ID  (courrier électronique, ECID et nombre total). |
| Prise en charge RBAC | Le créateur de segments prend désormais en charge les  et autorisations de base basées sur les rôles. |
| Meilleure prise en charge du partage de  externe  entre les solutions Adobe et Platform | Les utilisateurs peuvent désormais importer des métadonnées de  externe (hors plateforme d’expérience) dans des scénarios où le nombre de  de  est important ou inconnu a priori. Cette version comprend l’accès aux métadonnées   Manager pour les clients qui ont configuré le connecteur de solution. Ces   métadonnées de peuvent être utilisées dans le créateur de segments pour créer des segments de plateforme d’expérience. <br/><br/> En outre, les segments créés dans la plateforme d’expérience seront désormais disponibles pour une utilisation dans les solutions Adobe intégrées, notamment  Gestionnaire de  de, et Ad Cloud. |

**Corrections de bogues**

* Correction d’un problème en raison duquel la segmentation multientité renvoyait zéro  dans le cas de relations imbriquées.
* Correction d’un problème en raison duquel la logique d’exclusion renvoyait des résultats trompeurs.
* Amélioration de la lisibilité des dossiers à plusieurs entités. Ils affichent désormais le nom convivial de la classe XDM.
* Correction d’un problème intermittent en raison duquel plusieurs copies du même dossier XDM s’affichaient.
* La messagerie est maintenant créée pour informer un utilisateur si les estimations de segments ne sont pas disponibles pour la stratégie de fusion sélectionnée.

**Problèmes connus**

* Aucun.

Pour en savoir plus sur le service de segmentation, consultez la présentation [du service de](../../segmentation/home.md)segmentation.