---
title: Notes de mise à jour de Adobe Experience Platform, novembre 2019
description: Les notes de mise à jour de novembre 2019 pour Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 75%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 18 novembre 2019**

Nouvelles fonctionnalités d’Adobe Experience Platform :
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Mises à jour des fonctionnalités existantes :
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basée sur  Experience Platform, la plateforme de données clients en temps réel d’Adobe aide les entreprises à rassembler des données connues et inconnues pour activer les profils des clients avec une prise de décision intelligente tout au long du parcours client. La plateforme de données clients en temps réel associe plusieurs sources de données d’entreprise pour créer des profils unifiés en temps réel qui peuvent être utilisés pour offrir des expériences client personnalisées et individuelles sur tous les canaux et périphériques.

[!DNL Real-time Customer Data Platform] comprend des outils de gouvernance des données, de gestion des identités, de segmentation avancée et de science des données, de sorte que vous puissiez créer des profils et définir des audiences, et obtenir des informations riches tout en étant en mesure d’appliquer des politiques de gouvernance des données strictes.

Adobe se connecte à un vaste écosystème de partenaires, sans oublier les intégrations natives à Adobe Experience Cloud. Vous pouvez ainsi activer ces audiences en toute simplicité et proposer de superbes expériences client sur tous les canaux, de la personnalisation sur site ou in-app aux e-mails, médias achetés, centres d’appel, appareils connectés, etc.

La plateforme CDP en temps réel vous permet :

* d’obtenir un aperçu unique de votre client grâce à la collecte en flux continu des données client de l’ensemble de l’entreprise ;
* de gérer de manière responsable les profils avec des contrôles de confidentialité et de gouvernance fiables pour les identifiants connus et inconnus ;
* de générer des informations exploitables et d’adapter les audiences grâce à l’IA et à l’apprentissage automatique optimisés par Adobe Sensei et conçus pour les spécialistes marketing ;
* de proposer des expériences personnalisées en temps réel sur l’ensemble des canaux et des destinations.

Pour plus d’informations, voir [Documentation Real-time Customer Data Platform](../../rtcdp/overview.md).

**Fonctionnalités clés**

| Fonctionnalité | Description |
|---|---|
| Destinations  | Intégrations préconfigurées avec des plateformes de destination prises en charge par Adobe [!DNL Real-time Customer Data Platform] qui activent les données vers ces partenaires de manière transparente. Pour plus d’informations, consultez [Destinations](#destinations) ci-dessous. |
| Tableau de bord de mesures de la page d’accueil | La page d’accueil de Real-time Customer Data Platform (CDP en temps réel) comprend un tableau de bord de mesures qui affiche des informations sur les profils et les segments. La page d’accueil contient également des liens vers des documents d’apprentissage. Consultez la section sur les [mesures de la plateforme de données clients en temps réel](#real-time-customer-data-platform-metrics) ci-dessous. |
| Sources | Vous pouvez envoyer des données à partir de différentes sources, notamment les solutions Adobe, le stockage dans le cloud, des logiciels tiers et la gestion de la relation client. Pour en savoir plus, consultez la section [Sources](#sources) ci-dessous. |

**[!DNL Real-time Customer Data Platform]mesures**

La page d’accueil de Real-time Customer Data Platform (plateforme de données clients en temps réel), qui comprend un tableau de bord de mesures, s’affiche lorsque vous vous connectez à la plateforme de données clients en temps réel.

La page d’accueil n’est qu’un des emplacements où les cartes de mesures apparaissent. La plateforme CDP en temps réel fournit des cartes de mesure tout au long de votre expérience. Ces mesures indiquent les données, les profils et les audiences de segments du système.

Si le système ne contient aucune donnée lorsque vous vous connectez à la plateforme CDP en temps réel, le tableau de bord de la page d’accueil n’apparaît pas. Dans ce cas, la page d’accueil propose des ressources pédagogiques pour une première expérience client. À mesure que les données sont collectées, le tableau de bord se met automatiquement à jour pour afficher des informations sur ces données.

Pour en savoir plus, consultez la [présentation des mesures de la plateforme de données clients en temps réel](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations]Les sont des intégrations prédéfinies avec des plateformes de destination prises en charge par la plateforme de données clients en temps réel d’Adobe, qui activent les données vers ces partenaires de manière transparente. Pour plus d’informations, consultez la [présentation des destinations](../../destinations/home.md).

**Destinations disponibles**

La version de novembre permet à la plateforme de données clients en temps réel d’Adobe de prendre en charge les destinations suivantes :

* Publicité: [!DNL Google]
* Marketing par e-mail : Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Consultez le [catalogue des destinations](../../destinations/catalog/overview.md) pour en savoir plus sur chacune des destinations.

**Limites connues**

* Le contrôle permettant de définir des plannings d’activation personnalisés dans le flux d’activation (étape de planification) n’est pas disponible dans la version initiale.
* Il n’existe actuellement aucun moyen de modifier ou de supprimer une configuration de destination. Vous pouvez contourner cette limite en activant ou en désactivant la destination dans le coin supérieur droit de la [page de détails des destinations](../../destinations/ui/destination-details-page.md).
* Aucune validation n’est actuellement en place pour les détails, le chemin ou les informations d’identification du compte lors de la connexion à votre compte de destination ou de stockage. Assurez-vous de saisir les informations d’identification correctes et vérifiez qu’il n’y a pas de fautes d’orthographe ou de frappe.
* La version initiale n’offre aucun renouvellement des informations d’identification. Une fois qu’un compte a expiré ou doit être actualisé, vous devez créer une nouvelle connexion de destination et remapper les segments précédemment mappés.

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les solutions Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier auprès de vos services de gestion de la relation client et de vos systèmes de stockage, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ---------- | ------------ |
| Interface utilisateur des sources | Une nouvelle interface utilisateur pour la création, l’affichage et la gestion des connexions source. |
| Processus restructurés pour les connecteurs de gestion de la relation client | Nouveau workflow d’interface utilisateur intuitif pour la création et la gestion [!DNL Microsoft Dynamics] et [!DNL Salesforce] connecteurs. |
| Prise en charge des connecteurs pour le stockage dans le cloud | Les connecteurs peuvent désormais accéder au stockage dans le cloud. Nouvelles sources : [!DNL Amazon S3], [!DNL Azure Blob]et les serveurs FTP/SFTP. |

**Problèmes connus**

* Les connecteurs source pour le stockage dans le cloud ne prennent pas en charge l’ingestion de fichiers compressés.

Pour plus d’informations sur les sources, consultez [Présentation des sources](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] permet aux spécialistes des données de générer en toute transparence des informations à partir de données et de contenu dans les applications Adobe et les systèmes tiers en créant et en mettant en oeuvre des modèles d’apprentissage automatique. [!DNL Data Science Workspace] est étroitement intégré à et alimente le cycle de vie de la science des données de bout en bout, y compris l’exploration et la préparation des données XDM, puis le développement et la mise en œuvre de modèles pour enrichir automatiquement avec des insights d’apprentissage automatique.[!DNL Platform][!DNL Real-time Customer Profile]

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Accès aux données à l’aide de [!DNL Platform] SDK | Recettes préconfigurées et notebooks de lancement dans [!DNL Python] now use [!DNL Platform] SDK pour l’accès aux données. |
| Prise en charge des environnements de test | Prise en charge de la fonctionnalité d’environnement de test à venir (actuellement en version bêta), notamment la possibilité d’isoler les notebooks et les recettes dans des environnements de test de développement ou de production. Pour plus d’informations, consultez la [présentation des environnements de test](../../sandboxes/home.md). |

Pour plus d’informations, consultez la [présentation de Data Science Workspace](../../data-science-workspace/home.md).

## Système d’[!DNL Experience Data Model] (XDM) {#xdm}

La normalisation et l’interopérabilité sont des concepts clés pour [!DNL Experience Platform]. Le [!DNL Experience Data Model] (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ---------- | ------------ |
| Schéma de notification | Un nouveau schéma qui représente les données de notification envoyées pendant le processus d’ingestion des données. |
| Schémas DSP d’Adobe AdCloud | Cinq nouveaux schémas ont été ajoutés pour représenter les métadonnées de la plateforme DSP (Demand Side Platform) Adobe Advertising Cloud : positionnement, campagne, package, annonceur, compte. |
| Groupes de champs de schéma Détails de l’implémentation d’ExperienceEvent | Nouveau groupe de champs ExperienceEvent qui ajoute un champ standard pour stocker des informations sur le logiciel utilisé pour collecter l’événement. |
| [!DNL Profile Privacy] groupes de champs | Nouveaux groupes de champs de profil qui ajoutent des champs pour accepter les signaux d’opposition généraux et de vente/partage pour [!DNL Real-time Customer Profile]. |
| Contraintes de format de `xdm:alternateDisplayInfo` | Les champs « Titre » et « Description » de `xdm:alternateDisplayInfo` doivent tous deux être des chaînes pour être validés. |
| Changement de nom : XDM [!DNL Individual Profile] | Le &quot;titre&quot; de &quot;XDM&quot; [!DNL Profile]La classe &quot;a été mise à jour vers &quot;XDM&quot; [!DNL Individual Profile]&quot;. Le format `$id` de la classe n’a pas changé. |

**Problèmes connus**

* Aucun.

Pour en savoir plus sur l’utilisation de XDM à l’aide de la variable [!DNL Schema Registry] API et [!DNL Schema Editor] dans l’interface utilisateur, veuillez lire [Documentation du système XDM](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Avec [!DNL Real-time Customer Profile], vous pouvez obtenir une vue d’ensemble de chaque client qui combine des données provenant de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| -----------| ---------- |
| Améliorations apportées aux [!DNL Profile] recherche | Les utilisateurs peuvent désormais rechercher des profils à l’aide de descripteurs de référence et d’entités connexes. |
| Nettoyage des données d’un jeu de données spécifique | Les utilisateurs peuvent désormais supprimer des données pour un jeu de données ou un lot donné à l’aide de la variable [!DNL Profile] API des tâches système. |
| Edge [!DNL Profile] améliorations des requêtes | Les applications peuvent désormais interroger Edge [!DNL Profile] par l’une des identités d’un profil donné. |
| Configuration des stratégies de fusion par projection | Les applications peuvent désormais configurer des stratégies de fusion par projection afin de générer une vue des données telles qu’elles sont régies par une stratégie de fusion spécifique. |
| Attributs calculés | Les attributs calculés calculent automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés interviennent au niveau du profil pour agréger des valeurs comme « achat total », « valeur de durée de vie » ou « état de l’entonnoir » en fonction d’un événement entrant, d’un événement entrant et de données de profil, ou d’un événement entrant, de données de profil et d’événements historiques. |

**Corrections de bogues**

* Une liste simplifiée des stratégies de combinaison des identifiants disponibles dans le processus de création de stratégies de fusion.

**Problèmes connus**

* Aucun.

Pour plus d’informations sur [!DNL Real-time Customer Profile], y compris des tutoriels et des bonnes pratiques pour travailler avec [!DNL Profile] data, veuillez lire la [Présentation de Real-time Customer Profile](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

| Fonctionnalité | Description |
| -----------| ---------- |
| Segmentation planifiée | Les utilisateurs peuvent désormais activer l’évaluation de segmentation planifiée pour tous les segments via l’interface utilisateur et l’API. Une fois activée, tous les segments sont évalués une fois par jour. Cela n’affecte pas les fonctionnalités de segmentation sur demande dont le fonctionnement reste inchangé.<br/><br/>Remarque : la fonctionnalité de segmentation planifiée ne peut pas être utilisée dans les environnements de test comportant plus de cinq stratégies de fusion pour [!DNL XDM Individual Profile]. |
| Segmentation par flux | La prise en charge de l’évaluation continue des segments (segmentation par flux) permet d’évaluer la plupart des règles de segmentation à mesure que les données sont transmises à [!DNL Platform]. Cette fonctionnalité signifie que l’adhésion au segment sera à jour sans devoir exécuter des tâches de segmentation planifiées. Certaines exceptions s’appliquent, comme les segments utilisant des relations à plusieurs entités ou comportant des payloads enrichis. |
| Segments définis comme des blocs de création | Lors de la création de segments à l’aide de l’interface utilisateur du créateur de segments, les utilisateurs peuvent désormais utiliser des segments précédemment définis comme des blocs de création pour d’autres segments. <ul><li>Référencer l’appartenance à l’audience actuelle : elle est mise à jour lorsque les individus rejoignent et quittent les audiences.</li><li>Copier la logique : prenez la définition de segment sélectionnée et dupliquez-la dans le nouveau segment.</li></ul> |
| Affichage de l’adhésion au segment par espace de noms d’identifiant | L’adhésion au segment peut désormais être affichée à l’aide de l’espace de noms d’identifiant (courrier électronique, ECID et nombre total). |
| Prise en charge des RBAC | Le créateur de segments prend désormais en charge les autorisations et les contrôles d’accès en fonction du rôle. |
| Amélioration de la prise en charge du partage des audiences externes entre [!DNL Platform] et les solutions d’Adobe | Les utilisateurs peuvent désormais introduire des éléments externes (non[!DNL Experience Platform]) métadonnées d’audience dans les cas où le nombre d’audiences est important ou inconnu à priori. Cette version comprend l’accès aux [!DNL Audience Manager] métadonnées pour les clients qui ont configuré le connecteur de solution. Ces métadonnées d’audience peuvent être utilisées dans le créateur de segments pour créer [!DNL Experience Platform] segments. <br/><br/> En outre, les segments créés dans [!DNL Experience Platform] sera désormais disponible pour une utilisation dans les solutions Adobe intégrées, notamment [!DNL Audience Manager], [!DNL Target], et [!DNL Ad Cloud]. |

**Corrections de bogues**

* Correction d’un problème provoquant le renvoi d’aucun profil par la segmentation d’entités multiples dans le cas de relations imbriquées.
* Correction d’un problème provoquant le renvoi de résultats trompeurs par une logique d’exclusion.
* Amélioration de la lisibilité des dossiers à plusieurs entités. Ils affichent désormais le nom convivial de la classe XDM.
* Correction d’un problème intermittent entraînant l’apparition de plusieurs copies du même dossier XDM.
* Les messages sont maintenant émis pour informer un utilisateur en cas d’indisponibilité des estimations de segments pour la stratégie de fusion sélectionnée.

**Problèmes connus**

* Aucun.

Pour en savoir plus sur [!DNL Segmentation Service], veuillez lire la [Présentation de Segmentation Service](../../segmentation/home.md).
