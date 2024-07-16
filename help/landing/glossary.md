---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Glossaire Adobe Experience Platform
description: Glossaire reprenant la terminologie principale d’Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: b16eae9698de6c20022fdf1a3ff659df35e440f6
workflow-type: tm+mt
source-wordcount: '7996'
ht-degree: 12%

---

# Glossaire Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Contrôle d’accès** : le contrôle d’accès en fonction du rôle permet aux administrateurs d’attribuer un accès et des autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création de sandbox, la définition de schémas et la gestion des jeux de données.

**Identifiant de clé d’accès** : un identifiant de clé d’accès est un identifiant unique associé à une clé d’accès secrète S3 [!DNL Amazon]. L&#39;identifiant de la clé d&#39;accès et la clé d&#39;accès secrète sont utilisés conjointement pour signer les demandes [!DNL Amazon Web Services] (AWS).

**Action** : dans le contexte des balises, une action est un type spécifique de composant de règle qui définit ce qui doit se produire une fois qu’un événement se produit et que les conditions sont évaluées et transmises.

**Activer** : l’activation est l’action effectuée par un utilisateur pour mapper un segment ou des profils à une destination telle que [!DNL Oracle Eloqua], [!DNL Google] ou [!DNL Salesforce Marketing Cloud].

**Activité** : dans [!DNL Offer Decisioning], une activité contient la logique qui informe la sélection d’une offre.

**Administrateur** : une ou plusieurs personnes de votre entreprise qui peuvent configurer et personnaliser les autorisations d’Experience Platform dans Adobe Admin Console.

**Adobe Admin Console** : Adobe Admin Console fournit un emplacement central pour la gestion des droits et accès des produits Adobe pour votre organisation. Grâce à la console, les administrateurs peuvent octroyer à des groupes d’utilisateurs des autorisations d’accès pour diverses fonctionnalités de Platform, telles que &quot;Gérer les jeux de données&quot;, &quot;Afficher les jeux de données&quot; ou &quot;Gérer les profils&quot;.

**Adobe Experience Platform** : Adobe Experience Platform normalise les données et le contenu dans l’ensemble de l’entreprise, optimise les profils clients en temps réel, active la science des données et accélère la vitesse de diffusion du contenu afin d’orienter la personnalisation de l’expérience sur le parcours client.

**Adobe Experience Platform Query Service** : permet aux analystes de données d’interroger des événements et des profils en vue de les utiliser dans les analyses et l’apprentissage automatique. Grâce à Query Service, les analystes et analystes de données peuvent extraire tous leurs jeux de données stockés dans Experience Platform (y compris les données comportementales, ainsi que les points de vente, la gestion de la relation client, etc.) et interroger ces jeux de données pour répondre à des questions spécifiques sur les données.

**Service de segmentation Adobe Experience Platform** : permet de créer des segments et de générer des audiences à partir de vos données de profil client en temps réel. Ces audiences peuvent ensuite être exportées vers leurs propres jeux de données dans le lac de données.

**Adobe Intelligent Services** : les services intelligents tels que Attribution AI et Customer AI sont des modèles d’apprentissage automatique basés sur l’intelligence artificielle conçus spécifiquement pour fonctionner et fonctionner avec un Experience Platform.

**Adobe I/O** : l’Adobe I/O fait partie de l’Experience Platform et permet d’accéder à tout ce dont les développeurs ont besoin pour intégrer, étendre et personnaliser Platform, y compris les API, les événements, la console de développement et des outils utiles.

**Adobe Sensei** : Adobe Sensei est le cadre d’intelligence qui alimente l’Experience Platform. Il fournit également un ensemble de services d’IA qui permet aux marques d’améliorer leur capacité à fournir des expériences client personnalisées en temps réel.

**Compartiment Amazon S3** : [!DNL Amazon S3] les compartiments sont les conteneurs fondamentaux pour les données stockées dans l’écosystème [!DNL Amazon]. Les compartiments contiennent des objets, chaque objet est stocké et récupéré à l’aide d’une clé unique attribuée par le développeur.

**Connecteur Amazon S3** : le connecteur [!DNL Amazon] S3 permet aux clients d’Experience Platform de se connecter et d’accéder en toute sécurité à leurs données S3 [!DNL Amazon].

**APA** : le [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) promeut et protège la vie privée des individus et réglemente la manière dont les agences gouvernementales et les organisations australiennes traitent les informations personnelles. Le [!DNL Privacy Act] comprend des principes qui s’appliquent aux organisations du secteur privé. Par exemple, les individus ont le droit de comprendre pourquoi les informations personnelles sont collectées et comment elles seront utilisées, la possibilité d’accéder à leurs données, de les effacer et de corriger les informations personnelles.

**Stratégie d’enregistrement d’ajout** : la stratégie d’enregistrement &quot;d’ajout&quot; est une option utilisée lors de la spécification de données tierces à ingérer via une connexion et de l’ajout de nouvelles données ou lignes à la fin du jeu de données. Les lignes précédemment ingérées restent intactes et seules les lignes créées depuis la dernière exécution planifiée sont ingérées dans Experience Platform. Toutes les lignes modifiées dans le système source restent inchangées dans Experience Platform.

**Tableau** : les tableaux sont utilisés pour les éléments triés avec le même type de données.

**Intelligence artificielle** : l’intelligence artificielle est une théorie et un développement de systèmes informatiques capables d’exécuter des tâches qui nécessitent normalement l’intelligence humaine, telles que la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction entre les langues.

**Attributs** : les attributs sont des caractéristiques spécifiées qui représentent un profil.

**Fusion d’attributs** : lors de la définition d’une stratégie de fusion à l’aide de l’API Real-Time Customer Profile, l’objet `attributeMerge` indique la manière dont la stratégie de fusion établit la priorité des attributs de profil en cas de conflit de données. Cela équivaut à sélectionner une [!UICONTROL Méthode de fusion] lors de la définition d’une stratégie de fusion dans l’interface utilisateur de Platform.

**Attribution AI** : [!DNL Attribution AI] est un service intelligent optimisé par Adobe Sensei qui offre des fonctionnalités d’attribution algorithmique à plusieurs canaux tout au long du cycle de vie du client.

**Audience** : une audience est l’ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

**Taille de l’audience** : une taille d’audience est le nombre total de profils qui répondent aux critères d’une définition de segment et répondent aux critères de l’appartenance à l’audience.

**Instantané d’audience** : un instantané d’audience capture tous les profils qui remplissent les critères de segment au moment de la segmentation.

## B

**Renvoi** : pour les sources planifiées, l’option de renvoi active l’ingestion de données historiques.

**Période de renvoi** : la période de renvoi est une option permettant de définir la durée d’ingestion de données historiques tierces via une connexion source. La sélection d’une période de renvoi &quot;indéfiniment&quot; entraîne l’ingestion de l’historique complet des données source à l’Experience Platform.

**Lot** : un lot est un ensemble de données collectées sur une période donnée et traitées ensemble comme une seule unité. Les jeux de données sont composés de plusieurs lots.

**Identifiant de lot** : un identifiant de lot est un identifiant généré par l’Adobe pour un lot de données.

**Ingestion par lots** : l’ingestion par lots vous permet d’ingérer des données dans Experience Platform en tant que fichiers de lots. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en une seule unité.

**Segmentation par lots** : la segmentation par lots est une alternative à un processus de sélection de données en cours et déplace toutes les données de profil à la fois par le biais de définitions de segment pour produire les audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin de pouvoir être exporté en vue de son utilisation.

**Build** : dans le contexte des balises, une version est un fichier ou un ensemble de fichiers qui contient toutes les configurations et le code nécessaires pour exécuter la logique métier contenue dans une bibliothèque, ce qui vous permet de déployer cette bibliothèque sur votre site web ou votre application mobile.

**Outils de Business Intelligence** : les outils de Business Intelligence (BI) sont principalement intégrés à [!DNL Experience Platform Query Service]. Les outils de BI sont des types de programmes d’application qui collectent et traitent de grandes quantités de données non structurées à partir de systèmes internes et externes.

## C

**Limitation** : dans [!DNL Offer Decisioning], la limitation (également appelée limitation de fréquence) est utilisée dans les règles de prise de décision pour définir le nombre de fois où une offre est présentée. Il existe deux types de limites : le nombre de fois où une offre peut être proposée dans l’audience cible combinée (appelée &quot;limite globale&quot;) et le nombre de fois où une offre peut être proposée au même utilisateur final (appelée &quot;limite de profil&quot;).

**Catalogue** : dans le contexte de sources et de destinations, un catalogue est une galerie avec des connexions disponibles aux applications d’Adobe et aux technologies tierces. À ne pas confondre avec [!DNL Catalog Service].

**[!DNL Catalog Service]** : [!DNL Catalog Service] (parfois appelé [!DNL Catalog]) est le système d’enregistrement de l’emplacement et de la traçabilité des données dans Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous la forme de fichiers et de répertoires, [!DNL Catalog] contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche, de surveillance et de gouvernance des données.

**CCPA** : [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) améliore les droits à la vie privée et la protection des consommateurs pour les résidents de Californie, aux États-Unis. Le CCPA accorde plusieurs nouveaux droits à la confidentialité des données aux résidents de Californie, y compris le droit d’accéder et de supprimer leurs données personnelles, de savoir si ces données personnelles sont vendues ou divulguées (et à qui) et le droit de refuser (opt-out) que ces données soient vendues à des tiers.

**Classe** : dans le modèle de données d’expérience (XDM), une classe définit le plus petit ensemble de champs utilisé pour créer un schéma et définit le comportement de base de l’objet commercial représenté par le schéma.

**Client** : un client est un outil ou une application externe qui se connecte à [!DNL Query Service] via le protocole [!DNL PostgreSQL] ou l’API HTTP.

**Collection** : dans [!DNL Offer Decisioning], les collections sont des sous-ensembles d’offres basés sur des conditions prédéfinies définies par un marketeur, telles que la catégorie de l’offre.

**Combiner avec une action marketing PII** : action marketing qui combine toutes les informations d’identification personnelle avec les données anonymes. Les contrats relatifs aux données provenant de réseaux publicitaires, de serveurs de publicités et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données avec des données directement identifiables.

**Interface de ligne de commande** : une interface de ligne de commande est un outil texte qui peut être utilisé pour se connecter à [!DNL Query Service] pour l’exécution de requête brute.

**Composition** : une composition est un groupe de composants qui se forment ensemble pour constituer le schéma.

**Condition** : dans le contexte des balises, une condition est un composant de règle qui évalue une instruction logique qui doit renvoyer `true` ou `false`. Toutes les conditions doivent être évaluées sur `true` et toutes les conditions d’exception doivent être évaluées sur `false` avant l’exécution des actions de la règle.

**Console** : dans [!DNL Query Service], la console fournit des informations sur l’état et le fonctionnement d’une requête. La console affiche le statut de la connexion à [!DNL Query Service], les opérations des requêtes en cours d’exécution et tout message d’erreur résultant de ces requêtes.

**Étiquettes Contrat (&quot;C&quot;)** : les libellés d’utilisation des données Contrat (&quot;C&quot;) sont utilisés pour classer les données qui ont des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre entreprise.

**CPRA** : [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) développe et modifie des parties de l’élément [!DNL California Consumer Privacy Act (CCPA)]. L’ [!DNL CPRA] établit une nouvelle ligne de base pour la confidentialité des données des consommateurs en Californie en augmentant les droits des consommateurs et en élargissant le type de données couvert par une définition plus large des informations personnelles sensibles. En outre, le [!DNL CPRA] a établi l&#39;Agence de protection de la vie privée de Californie, une nouvelle agence dédiée à la mise en oeuvre et à l&#39;application des règles de confidentialité des données.

**Étiquette de contrat C1** : une étiquette d’utilisation des données de contrat `C1` indique que les données peuvent uniquement être exportées à partir de Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants individuels ou d’appareil. Par exemple, les données provenant des réseaux sociaux.

**Étiquette de contrat C2** : une étiquette d’utilisation des données de contrat `C2` spécifie les données qui ne peuvent pas être exportées vers un tiers. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent l’exportation de données à partir de l’endroit où elles ont été collectées à l’origine. Par exemple, les contrats des réseaux sociaux limitent souvent le transfert des données que vous recevez d’eux. L’étiquette C2 est plus restrictive que la C1, qui ne nécessite que l’agrégation et des données anonymes.

**Étiquette de contrat C3** : une étiquette d’utilisation des données de contrat `C3` spécifie des données qui ne peuvent pas être combinées ou utilisées d’une autre manière avec des informations directement identifiables. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent la combinaison ou l’utilisation de ces données avec des informations directement identifiables. Par exemple, les contrats pour les données provenant des réseaux publicitaires, des serveurs de publicités et des fournisseurs de données tiers incluent souvent des interdictions contractuelles spécifiques sur l’utilisation des données directement identifiables.

**Étiquette de contrat C4** : une étiquette d’utilisation des données de contrat `C4` indique que les données ne peuvent pas être utilisées pour cibler des publicités ou du contenu, que ce soit sur site ou entre sites. L’étiquette C4 est l’étiquette la plus restrictive puisqu’elle englobe les étiquettes C5, C6 et C7.

**Étiquette de contrat C5** : une étiquette d’utilisation des données de contrat `C5` spécifie que les données ne peuvent pas être utilisées pour le ciblage intersite de contenu ou de publicités basés sur des intérêts. Le ciblage en fonction des intérêts, ou personnalisation, se produit si les trois conditions suivantes sont remplies : les données collectées sur site sont utilisées pour établir des inférences sur les intérêts d’un utilisateur ; elles sont utilisées dans un autre contexte, par exemple sur un autre site ou une autre application ; elles sont utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Étiquette de contrat C6** : une étiquette d’utilisation des données de contrat `C6` indique que les données ne peuvent pas être utilisées pour le ciblage des publicités sur site. Le ciblage des publicités sur site inclut la sélection et la diffusion de publicités sur les sites web ou les applications de votre organisation, ou pour mesurer la diffusion et l’efficacité de ces publicités. Cela inclut l’utilisation de données précédemment collectées sur site concernant l’intérêt des utilisateurs pour sélectionner des publicités, le traitement des données concernant les publicités affichées, le moment et le lieu de leur diffusion, et le fait de savoir si les utilisateurs ont pris des mesures en rapport avec la publicité, comme sélectionner une publicité ou effectuer un achat.

**Étiquette de contrat C7** : une étiquette d’utilisation des données de contrat `C7` indique que les données ne peuvent pas être utilisées pour le ciblage de contenu sur site. Le ciblage de contenu sur site inclut la sélection et la diffusion de contenu sur les sites web ou les applications de votre entreprise, ou pour mesurer la diffusion et l’efficacité de ce contenu. Cela inclut les informations précédemment collectées sur l’intérêt des utilisateurs à sélectionner le contenu, à traiter les données sur le contenu affiché, la fréquence ou la durée de sa diffusion, le moment et le lieu de sa diffusion, et si les utilisateurs ont pris des mesures relatives au contenu, par exemple en sélectionnant le contenu.

**Étiquette de contrat C8** : une étiquette d’utilisation des données de contrat `C8` indique que les données ne peuvent pas être utilisées pour mesurer les sites web ou les applications de votre organisation. Cela ne comprend pas le ciblage basé sur l’intérêt, qui est la collecte d’informations sur votre utilisation de ce service pour personnaliser par la suite le contenu et/ou la publicité dans d’autres contextes.

**Étiquette de contrat C9** : une étiquette d’utilisation des données de contrat `C9` indique que les données ne peuvent pas être utilisées dans les workflows de science des données. Certains contrats prévoient des interdictions explicites sur les données utilisées pour la science des données. Parfois, cela fait partie de conditions qui interdisent l’utilisation de données pour l’intelligence artificielle (IA), l’apprentissage automatique ou la modélisation.

**Étiquette de contrat C10** : une étiquette d’utilisation des données de contrat `C10` indique que les données ne peuvent pas être utilisées pour l’activation de l’identité groupée. Certaines politiques dʼutilisation des données limitent lʼutilisation de données dʼidentité assemblées pour la personnalisation. L’étiquette `C10` est automatiquement appliquée aux segments si leurs stratégies de fusion utilisent l’option &quot;graphique privé&quot;.

**Colonne Date de création** : la sélection d’une colonne Date de création est une option lors de la spécification de données tierces via une connexion source. Lorsque la stratégie d’enregistrement d’ajout est sélectionnée et que le schéma du jeu de données contient plusieurs champs de date, vous devez choisir parmi le schéma disponible pour spécifier une colonne clé Date de création . L’option Date de création n’est pas disponible lorsque la stratégie d’enregistrement de remplacement est sélectionnée.

**Create Table as Select** : Create Table as Select (CTAS) est une commande SQL qui, lorsqu’elle est exécutée dans le cadre d’une requête SQL complète et valide, demande à [!DNL Query Service] de conserver les résultats de la requête dans un jeu de données. Vous pouvez créer un jeu de résultats, remplacer les résultats précédents ou ajouter des résultats précédents.

**Données intersites** : les données intersites sont la combinaison de données de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site.

**Action marketing de ciblage intersite** : action marketing qui utilise les données pour le ciblage publicitaire intersite. La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les données intersites sont généralement collectées et traitées afin d’établir des inférences sur les intérêts des clients.

**Espace de noms d’identité personnalisé** : des espaces de noms d’identité personnalisés peuvent être créés par votre organisation pour représenter les identités d’une organisation ou d’une entreprise spécifique.

**Libellés personnalisés** : les libellés d’utilisation des données personnalisés vous permettent de créer et d’appliquer des libellés spécifiques aux champs de données qui répondent à des besoins spécifiques de l’entreprise.

**Customer AI** : Customer AI est un service intelligent optimisé par Adobe Sensei qui enrichit les profils clients avec des propensions basées sur l’IA et permet la segmentation et le ciblage des clients.

## D

**Quotidien** : dans le contexte d’exportations de fichiers planifiées, planifie des exportations de fichiers complètes ou incrémentielles une fois par jour, tous les jours, de la date de début à la date de fin à l’heure spécifiée par l’utilisateur.

**Dictionnaire de données** : dans le contexte des balises, un dictionnaire de données (également appelé mappage de données) est un ensemble d’éléments de données définis dans une propriété.

**Élément de données** : dans le contexte de balises, un élément de données est un pointeur utilisé dans les règles et les extensions pour pointer vers un élément de données spécifique existant sur l’appareil client.

**Ingestion de données** : l’ingestion de données est le processus d’ajout de données d’une source à un Experience Platform. Les données peuvent être ingérées dans Platform de différentes manières, y compris par flux, lots ou ajoutées via des connecteurs source.

**Couche de données** : dans le contexte des balises, une couche de données est une structure de données qui existe sur l’appareil client et qui contient des métadonnées sur le contexte dans lequel une page ou un écran est affiché.

**Gouvernance des données** : la gouvernance des données englobe les stratégies et les technologies utilisées pour s’assurer que les données sont conformes aux réglementations et aux politiques organisationnelles en matière d’utilisation des données.

**Partenaires d’intégration de données** : les partenaires d’intégration de données simplifient et automatisent le chargement et la transformation de volumes massifs de données de plus de 200 sources vers Experience Platform sans écrire de code.

**Libellés de jeux de données** : les libellés d’utilisation des données peuvent être ajoutés aux jeux de données. Tous les champs de ce jeu de données héritent des libellés du jeu de données.

**Data Science Workspace** : [!DNL Data Science Workspace] dans Experience Platform permet aux clients de créer des modèles d’apprentissage automatique à l’aide de données dans Platform et les applications d’Adobe afin de créer des segments intelligents, de générer des insights et de fournir des prédictions, ce qui vous permet d’améliorer considérablement les expériences numériques des utilisateurs finaux.

**Source de données** : une source de données est un utilisateur désigné comme étant l’origine de données. Une source de données peut être une application mobile, des événements de profil et/ou d’expérience, des événements de profil de site web ou un système de gestion de la relation client (CRM).

**Gestionnaire de données** : un gestionnaire de données est la personne responsable de la gestion, de la supervision et de l’application des ressources de données d’une organisation. Un gestionnaire de données veille également à ce que les politiques de gouvernance des données soient préservées et conservées pour être conformes aux réglementations gouvernementales et aux politiques organisationnelles.

**Flux de données** : un flux de données est un ensemble ou une collection de messages qui partagent le même schéma et sont envoyés par la même source.

**Type de données** : un type de données est une ressource XDM réutilisable qui définit un champ de type objet contenant plusieurs propriétés dans une représentation hiérarchique.

**Libellés d’utilisation des données** : les libellés d’utilisation des données vous permettent de classer les données en fonction des considérations liées à la confidentialité et des conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques d’entreprise. Les libellés d’utilisation des données ajoutés à un jeu de données sont hérités ou appliqués à tous les champs de ce jeu de données. Les libellés d’utilisation des données peuvent également être appliqués directement aux champs.

**Flux de données** : un flux de données est un pipeline virtuel de données qui s’écoule vers Platform à partir d’une source et vers des destinations.

**Exécution de flux de données** : une exécution de flux de données est un flux de données qui arrive en Experience Platform en fonction d’une planification spécifiée par l’utilisateur.

**Jeu de données** : un jeu de données est une structure de stockage et de gestion pour une collecte de données, généralement un tableau, qui contient un schéma (des colonnes) et des champs (des lignes).

**Identifiant du jeu de données** : identifiant généré par l’Adobe pour un jeu de données ingéré.

**Sortie du jeu de données** : la sortie du jeu de données fournit un mécanisme pour déterminer ce que l’option &quot;Créer un tableau comme sélectionner&quot; sera utilisée pour une exécution [!DNL Query Service] spécifique.

**Clé de déduplication** : clé primaire définie par l’utilisateur qui détermine l’identité par laquelle les utilisateurs souhaitent que leurs profils soient dédupliqués. &#x200B;

**Colonne delta** : une colonne delta vous permet de sélectionner un champ de données source pour représenter un horodatage pour l’ingestion incrémentielle.

**Stratégie d’enregistrement delta** : la stratégie d’enregistrement delta est une option permettant d’ingérer des données tierces via une connexion source. Cette option permet à l’utilisateur de spécifier que les lignes de données sources nouvelles ou modifiées sont assimilées à Experience Platform. De nouvelles lignes sont ajoutées à la fin du jeu de données et les lignes modifiées sont mises à jour dans le jeu de données d’Experience Platform.

**Descripteur** : dans le modèle de données d’expérience (XDM), un descripteur est un jeu supplémentaire de métadonnées liées au schéma qui décrit un comportement spécifique pour un champ. Les descripteurs peuvent être utilisés par l’Experience Platform pour comprendre le comportement prévu des schémas, comme la relation entre deux schémas.

**Destination** : une destination est un terme général pour tout point de terminaison, tel qu’une application d’Adobe, une plateforme publicitaire, un service de stockage dans le cloud ou un service marketing, où une audience est activée et diffusée.

**Catégorie de destination** : une catégorie de destination est un groupe de destinations ayant des caractéristiques similaires.

**Catalogue des destinations** : un catalogue des destinations est une liste des destinations disponibles dans Experience Platform.

**Règles d’appel direct** : dans le contexte de balises, une règle d’appel direct est une règle qui s’exécute lorsqu’elle est appelée directement à partir de la page, en contournant les systèmes de détection d’événement et de recherche.

**Nom d’affichage** : dans le modèle de données d’expérience (XDM), un nom d’affichage est un nom convivial pour un champ qui s’affiche dans l’interface utilisateur.

## E

**Offre éligible** : une offre éligible peut être proposée de manière cohérente à un profil, car elle répond aux contraintes définies en amont.

**Règles d’éligibilité** : dans [!DNL Offer Decisioning], les règles d’éligibilité sont appliquées à un profil lié aux contraintes de calendrier, de planification et de limitation.

**Action marketing de ciblage d’email** : action marketing qui utilise des données dans les campagnes de ciblage d’email.

**Code incorporé** : dans le contexte de balises, le code incorporé est une balise de script placée dans l’HTML sur un site ou un environnement. Le code incorporé indique au navigateur où récupérer la version.

**Énumération** : une énumération (énumération) est un champ XDM limité à un ensemble de valeurs prédéfinies.

**Environnement** : dans le contexte des balises, un environnement est un ensemble d’instructions de déploiement qui spécifie la diffusion hôte et le format de fichier d’une version. Une bibliothèque doit être associée à un environnement avant qu’il puisse être créé.

**Diagnostic d’erreur** : les diagnostics d’erreur permettent de générer des messages d’erreur détaillés pour les lots ingérés. Le seuil d’erreur permet de configurer le pourcentage d’erreurs acceptables avant l’échec d’un lot.

**Événement** : dans le contexte des balises, un événement est un type spécifique de composant de règle, qui est un déclencheur qui se produit sur un appareil client pour commencer l’exécution d’une règle.

**Entités d’événement** : dans le cadre de la modélisation des données, les entités d’événement représentent des concepts liés aux actions qu’un client peut entreprendre, aux événements système ou à tout autre concept sur lequel vous souhaitez peut-être suivre les modifications au fil du temps. Les entités qui font partie de cette catégorie doivent être représentées par des schémas basés sur la classe [!DNL XDM ExperienceEvent].

**Events** : les événements sont les données de comportement associées à un profil.

**Modèle de données d’expérience (XDM)** [!DNL Experience Data Model] (XDM) est un framework open source qui utilise des schémas standard pour unifier les données à utiliser avec des applications Experience Platform et Adobe Experience Cloud. XDM normalise la structure des données, et accélère et simplifie le processus d’obtention d’informations à partir d’énormes quantités de données.

**Expérience** : une expérience est le processus de création d’un modèle formé en entraînant l’instance avec une portion d’échantillon des données de production en direct. Ceci est différent d’un modèle formé testé par rapport à un jeu de données de test d’exclusion. C&#39;est aussi différent du concept d&#39;expérience dans certains cadres d&#39;apprentissage automatique où cela signifie en fait un exemple de projet de modélisation.

**Événement d’expérience** : un événement d’expérience représente un instantané du système lorsqu’une interaction ou un événement lié à une expérience client a lieu. Les événements d’expérience sont des enregistrements factuels non modifiables de ce qui s’est passé et représentent ce qui s’est passé sans agrégation ni interprétation. Dans le modèle de données d’expérience (XDM), ce concept est capturé par la classe [!DNL XDM ExperienceEvent].

**Exporter le fichier complet** : un fichier d’exportation contenant un instantané complet de toutes les qualifications de profil pour le segment sélectionné.

**Exporter les fichiers incrémentiels** : série de fichiers exportés où le premier fichier est un instantané complet de toutes les qualifications de profil pour le segment sélectionné et les fichiers suivants sont des qualifications de profil incrémentielles depuis l’exportation précédente.

**Extension** : dans le contexte des balises, une extension est un package de fonctionnalités ajoutées à une propriété de balise. Une extension est généralement axée sur une solution marketing ou analytique spécifique et fournit les outils nécessaires au déploiement de cette technologie dans un environnement client.

**Package d’extension** : dans le contexte de balises, un package d’extension est un fichier ZIP créé et téléchargé par un développeur d’extensions qui fournit tout le nécessaire pour que les utilisateurs de balises installent l’extension dans leur propriété. Un package d’extension contient un manifeste spécifiant des informations sur l’extension, l’HTML/JavaScript nécessaire pour que les utilisateurs finaux configurent le comportement de l’extension de balise et le JavaScript exécutable diffusé à l’environnement client (si nécessaire).

## F

**Offres de secours** : une offre de secours est l’offre par défaut affichée lorsqu’un utilisateur final n’est éligible à aucune des offres de la collection utilisée.

**Mappage des fonctionnalités** : le mappage des fonctionnalités fait référence au processus de mappage des fonctionnalités des données dans les fonctionnalités d’entrée et de cible requises par un modèle d’apprentissage automatique.

**Field** : un champ est l’élément de niveau le plus bas d’un jeu de données, tel que défini par le schéma XDM du jeu de données. Chaque champ a un nom à des fins de référencement et un type pour indiquer le type de données qu’il contient. Les types de champ peuvent inclure (sans s’y limiter) des nombres entiers, des nombres, des chaînes, des valeurs booléennes et des objets.

**Groupe de champs** : voir &quot;Groupe de champs de schéma&quot;.

**Libellés de champ** : les libellés de champ sont des libellés de gouvernance des données qui sont soit hérités d’un jeu de données, soit appliqués directement à un champ.

**Nom du champ** : un nom de champ est utilisé pour référencer la valeur d’un champ dans les requêtes et les services en aval.

**Fréquence** : dans [!DNL Query Service], la fréquence détermine la fréquence d’exécution d’une requête planifiée récurrente.

## G

**Géofence** : une géobarrière est une limite géographique virtuelle, définie par la technologie GPS ou RFID, qui permet à un logiciel de déclencher une réponse lorsqu’un appareil mobile entre ou quitte une zone particulière.

**RGPD (Règlement général sur la protection des données)** : le règlement général sur la protection des données (RGPD) est un cadre juridique qui définit des lignes directrices pour la collecte et le traitement des informations personnelles des individus au sein de l’Union européenne (UE). Le RGPD énonce les principes de la gestion des données et les droits des individus et couvre toutes les entreprises qui traitent les données des citoyens de l’UE.

**Barrières de sécurité** : les barrières de sécurité sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform. Les mécanismes de sécurisation peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

## H

**HIPAA** : [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) est une loi fédérale des États-Unis créée pour améliorer l&#39;efficacité des soins de santé, améliorer la portabilité de l&#39;assurance maladie et protéger la vie privée des patients et des membres des régimes de santé. En vertu de l&#39;HIPAA, les individus ont le droit d&#39;accéder à leurs informations et de les modifier, ainsi que d&#39;obtenir des copies de leurs dossiers médicaux ou de leurs données médicales. Les entités couvertes et les associés commerciaux des entités couvertes doivent respecter les règles du HIPAA.

**Hôte** : dans le contexte des balises, un hôte spécifie l’emplacement, le domaine et les informations d’identification d’utilisateur nécessaires au système pour diffuser une version.

**Horaire** : dans le contexte d’exportations de fichiers planifiées, planifie des exportations incrémentielles de fichiers toutes les 3, 6, 8 ou 12 heures.

## I

**Identité** : une identité est un identifiant qui représente de manière unique un client individuel, comme un identifiant de cookie, un identifiant d’appareil ou un identifiant de courrier électronique.

**Champs d’identité** : les champs d’identité sont des champs XDM utilisés pour rassembler des informations sur les clients individuels provenant de plusieurs sources de données. Une seule identité principale doit être définie pour que le schéma puisse être utilisé dans Real-time Customer Profile.

**Libellés d’identité (&quot;I&quot;)** : les libellés d’utilisation des données d’identité (&quot;I&quot;) sont utilisés pour classer les données qui peuvent identifier ou contacter une personne spécifique.

**Graphique d’identités** : un graphique d’identités est une carte des relations entre les identités associées et liées qui existent pour un client individuel. Chaque graphique d’identités se met à jour en temps quasi réel avec l’activité des clients. La structure commune des relations d’identité dans vos données est représentée par le [!UICONTROL graphique privé], qui sert de plan structurel pour chaque graphique d’identités individuel.

**Espace de noms d’identité** : un espace de noms d’identité définit le contexte d’un identifiant tel qu’une adresse électronique ou un identifiant CRM.

**Identity Service** : [!DNL Experience Platform Identity Service] permet la création et la gestion des types d’identité, ce qui vous permet de lier les identités des clients entre appareils et canaux. La capacité du service à lier les identités permet à Real-time Customer Profile de fournir une représentation complète de chaque client.

**Combinaison d’identités** : la combinaison d’identités est le processus d’identification des fragments de données et de regroupement pour former un enregistrement de profil complet.

**Symbole d’identité** : un symbole d’identité est l’abréviation d’un espace de noms d’identité qui peut être utilisé comme référence dans les API.

**Valeur d’identité** : une valeur d’identité, combinée à un espace de noms d’identité, est un identifiant qui représente un individu, une organisation ou une ressource unique. Lors de la mise en correspondance des données d’enregistrement entre les fragments de profil, l’espace de noms et la valeur d’identité doivent correspondre.

**Libellé d’utilisation des données I1** : l’étiquette d’utilisation des données `I1` est utilisée pour classer les données qui peuvent identifier directement une personne spécifique ou la contacter plutôt qu’un appareil.

**Libellé d’utilisation des données I2** : le libellé d’utilisation des données `I2` est utilisé pour classer les données qui peuvent être utilisées en combinaison avec toute autre donnée pour identifier indirectement ou contacter une personne spécifique.

**Organisation IMS** : une organisation IMS (parfois appelée organisation IMS) est le nom utilisé pour identifier une société ou un groupe spécifique au sein d’une société dans les produits Adobe. Les administrateurs peuvent configurer et gérer l’accès et les autorisations des fonctionnalités pour les utilisateurs d’une organisation.

**Ingestion** : voir Ingestion de données.

**Planification de l’ingestion** : un planning d’ingestion fournit des options temporelles lors de l’ingestion d’une source vers un Experience Platform.

**Fonctionnalité d’entrée** : une fonctionnalité d’entrée est spécifiée dans le mappage des fonctionnalités et est utilisée par un modèle d’apprentissage automatique pour faire des prédictions.

**[!DNL Intelligent Services]** : [!DNL Intelligent Services] tels que [!DNL Attribution AI] et [!DNL Customer AI] sont des modèles d’apprentissage automatique basés sur l’intelligence artificielle qui nécessitent des Experience Platform (ou des applications reposant sur Platform telles qu’Adobe Real-Time Customer Data Platform) pour fonctionner et s’exécuter.

**Ciblage ou personnalisation en fonction des intérêts** : le ciblage en fonction des intérêts, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies :

1. Les données collectées sur site sont utilisées pour établir des inférences sur les intérêts d’un utilisateur.
1. Les données sont utilisées dans un autre contexte, par exemple sur un autre site ou une autre application (hors site).
1. Les données sont utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

## J

**[!DNL JupyterLab]** : interface web open source pour le projet [!DNL Jupyter] intégré à l’interface utilisateur de Platform.

**[!DNL Jupyter Notebook]** : intégré à JupyterLab, les notebooks Jupyter vous permettent d’effectuer le nettoyage et la transformation des données, la simulation numérique, la modélisation statistique, la visualisation des données, l’apprentissage automatique, etc. sur vos données Experience Platform dans divers langages tels que Python, Scala et PySpark.

## K

## L

**LGPD** : [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) vise à réglementer le traitement des données personnelles de tous les individus ou personnes physiques au Brésil. La LGPD donne aux citoyens brésiliens le droit d&#39;accéder à leurs données personnelles et de les supprimer, de savoir si leurs données personnelles sont vendues ou divulguées (et à qui), et le droit de refuser que leurs données soient vendues à des tiers.

**Bibliothèque** : dans le contexte des balises, une bibliothèque est un ensemble de logiques commerciales qui contient des instructions sur le comportement de la bibliothèque de balises sur l’appareil client.

**Entités de recherche** : dans le cadre de la modélisation des données, les entités de recherche représentent des concepts qui peuvent être associés à une personne, mais qui ne peuvent pas être directement utilisés pour identifier la personne. Les entités qui appartiennent à cette catégorie doivent être représentées par des schémas basés sur des classes XDM (Experience Data Model) personnalisées et liées à une entité de profil par le biais d’une [relation de schéma](../xdm/tutorials/relationship-ui.md).

## M

**Apprentissage automatique (ML)** : l’apprentissage automatique est le domaine d’étude qui permet aux ordinateurs d’apprendre sans être explicitement programmés.

**Modèle d’apprentissage automatique** : un modèle d’apprentissage automatique est une instance d’une recette d’apprentissage automatique formée à l’aide de données historiques et de configurations pour résoudre un cas d’utilisation commerciale. Dans Adobe Experience Platform Data Science Workspace, les modèles d’apprentissage automatique sont appelés recettes.

**Attribut obligatoire** : case à cocher activée par l’utilisateur qui garantit que tous les enregistrements de profil contiennent l’attribut sélectionné. Par exemple : tous les profils exportés contiennent une adresse email.

**Mapping** : le mappage des données est le processus de mappage des champs de données sources aux champs cibles associés dans une destination.

**Action marketing** : dans le cadre de la gouvernance des données, une action marketing (également appelée cas d’utilisation marketing) est une action entreprise par un utilisateur de données Experience Platform, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

**Méthode de fusion** : lors de la définition d’une stratégie de fusion à l’aide de l’interface utilisateur de Platform, la méthode de fusion spécifie comment les fragments de données doivent être hiérarchisés lorsqu’un conflit se produit. Lors de l’utilisation de l’API Real-time Customer Profile pour définir une stratégie de fusion, la méthode de fusion est déterminée à l’aide de l’objet `attributeMerge`.

**Stratégie de fusion** : les stratégies de fusion sont des règles utilisées par l’Experience Platform pour déterminer comment les fragments de données client provenant de plusieurs sources seront combinés afin de créer un profil individuel. Lorsqu’un conflit de données se produit, la stratégie de fusion détermine les données qui doivent être incluses en priorité dans le profil.

**MHMDAa** : [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&amp;full=true) améliore les droits de confidentialité pour les consommateurs concernant leurs données d’intégrité. Elle exige la divulgation, le consentement des consommateurs et les droits de suppression des données de santé, et interdit la vente de données de santé sans autorisation. En outre, la loi interdit l&#39;utilisation de la géoclôture autour des établissements de santé.

**Mixin** : voir &quot;Groupe de champs de schéma&quot;.

**Module** : dans le contexte des balises, un module est un fragment de code de JavaScript exécutable fourni par une extension, qui effectue des actions dans un environnement client sans avoir à créer de règle.

## N

**[!DNL New Zealand Privacy Act]** : [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) contrôle la manière dont les agences peuvent collecter, utiliser, divulguer, stocker et donner accès aux informations personnelles des citoyens et organisations néo-zélandais. En 2020, la dernière version de la loi a introduit des mises à jour significatives de ces lois sur la protection de la vie privée, y compris de nouvelles infractions, une augmentation des amendes, des notifications obligatoires pour les violations de données et une augmentation des pouvoirs du commissaire à la protection de la vie privée.

**Environnement de test hors production** : les environnements de test hors production sont généralement utilisés pour des expériences de développement, des tests ou des tests. Contrairement aux environnements de test de production, les environnements de test hors production peuvent être réinitialisés et supprimés.

**[!DNL Notebooks]** : [!DNL Notebooks] sont créés à l’aide de [!DNL Jupyter Notebook] et peuvent être exécutés pour exécuter l’analyse des données.

## O

**Offre** : une offre est un message marketing contenant une proposition commerciale ou de vente à un client (potentiel). Les offres comportent souvent des règles spécifiques qui déterminent qui peut les voir ou les recevoir.

**[!DNL Offer Decisioning]** : [!DNL Offer Decisioning] permet aux marketeurs de gérer des règles et des modèles formés de propositions d’offre lors de l’interaction avec les utilisateurs finaux en fonction des données collectées sur l’ensemble des canaux et des applications.

**Bibliothèque d’offres** : la bibliothèque d’offres est une bibliothèque centrale utilisée pour gérer les offres personnalisées et de secours, les règles de décision et les activités.

**Action marketing de personnalisation sur site** : action marketing qui utilise des données pour la personnalisation de contenu sur site. La personnalisation sur site est une donnée utilisée pour établir des inférences sur les intérêts des utilisateurs et pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Action marketing de ciblage sur site** : action marketing qui utilise les données pour les publicités sur site, y compris la sélection et la diffusion de publicités sur les sites web ou les applications de votre entreprise, ou pour mesurer la diffusion et l’efficacité de ces publicités.

**Une fois** : dans le contexte d’exportations de fichiers planifiées, planifie une exportation de fichiers unique, à la demande et complète.

**Stratégie d’enregistrement de remplacement** : la stratégie d’enregistrement &quot;Remplacer&quot; est une option permettant d’ingérer des données tierces via une connexion, où vous pouvez spécifier si les données ingérées seront remplacées selon un calendrier spécifié.

## P

**Ingestion partielle** : l’ingestion partielle permet l’ingestion d’enregistrements valides de données de lot dans un seuil d’erreur spécifié. Les diagnostics d’erreur pour les enregistrements en échec peuvent être téléchargés ou accessibles dans la présentation de l’exécution du flux de données [!UICONTROL Surveillance] ou [!UICONTROL Sources].

**Fichier parquet** : un fichier parquet est un format de fichier de stockage en colonnes avec des structures de données imbriquées complexes. Des fichiers parquet sont nécessaires pour ajouter des données à un jeu de données de schéma.

**PDPA** : le [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) a été introduit pour protéger les propriétaires de données thaïlandais de la collecte, de l’utilisation ou de la divulgation illégale de leurs données personnelles. Inspirée par le RGPD de l&#39;Union européenne, la réglementation accorde aux citoyens thaïlandais le droit de demander l&#39;accès à leurs données personnelles stockées ou de les supprimer.

<!-- Not yet released
**PDPD**: The [[!DNL Personal Data Protection Decree] (PDPD) 
-->

**Offres personnalisées** : une offre personnalisée est un message marketing personnalisable basé sur des règles d’éligibilité et des contraintes.

**Emplacements** : un emplacement est l&#39;endroit ou le contexte dans lequel apparaît une offre pour un utilisateur final.

**Espace de travail des stratégies** : espace de travail de l’interface utilisateur de Platform qui permet aux gestionnaires de données d’afficher et de gérer les libellés et stratégies d’utilisation des données pour votre organisation.

**Stratégie** : une stratégie d’utilisation des données est une règle qui spécifie les actions marketing limitées en fonction de l’application des libellés d’utilisation appliqués aux données de Platform.

**Application des stratégies** : vous permet d’appliquer des stratégies d’utilisation des données avec des actions marketing appliquées afin d’empêcher les opérations de données qui constituent des violations de stratégie au sein d’une organisation.

**Clé de Principal** : une clé primaire est une désignation dans un schéma pour identifier de manière unique tous les enregistrements.

**Priorité** : dans [!DNL Offer Decisioning], la priorité est utilisée pour classer les offres qui répondent à toutes les contraintes, telles que l’éligibilité, le calendrier et la limitation.

**Graphique d’identités privé** : le graphique d’identités privé (parfois appelé graphique privé) est une carte privée des relations entre les identités associées et liées, qui est créée sur la base de vos données propriétaires et qui est visible uniquement par votre organisation. Il n’existe qu’un seul graphique privé pour chaque organisation et sert de plan structurel pour les graphiques d’identités individuels générés pour chaque client qui interagit avec votre marque.

**Profil de produit** : les profils de produit permettent aux administrateurs d’accorder à l’utilisateur l’accès à l’ensemble ou à un sous-ensemble de services associés à l’Experience Platform.

**Environnement de test de production** : un environnement de test de production est un environnement de test destiné à être utilisé dans votre environnement de production. Contrairement aux environnements de test hors production, les environnements de test de production ne peuvent pas être réinitialisés ni supprimés.

**Profil** : à ne pas confondre avec Real-Time Customer Profile en tant que service, un profil est une représentation complète d’un client individuel, construite à partir de données d’enregistrement fusionnées et de séries temporelles provenant de plusieurs sources.

**Accès au profil** : le point de terminaison `/entities` de l’API Real-Time Customer Profile vous permet d’accéder aux données d’enregistrement et aux événements de série temporelle dans la banque de données Profile. Voir aussi : Entités de profil

**Données de profil** : les données de profil font référence à toutes les données qui se trouvent dans la banque de données de profil.

**Banque de données de profil** : La banque de données de Profile (parfois appelée banque de données Profile) est un système de stockage de données distinct du lac de données, utilisé par Real-Time Customer Profile pour créer et stocker des profils.

**Entités de profil** : les entités de profil représentent des attributs relatifs à une personne, généralement un client. Les entités qui font partie de cette catégorie doivent être représentées par des schémas basés sur la classe [!DNL XDM Individual Profile]. Voir aussi : Accès aux profils

**Export de profil** : [!DNL Profile] l’exportation est l’un des deux types de destinations dans Experience Platform. [!DNL Profile] L’exportation génère un fichier contenant des profils et des attributs et utilise des données d’informations d’identification personnelles brutes avec le courrier électronique afin de s’intégrer aux plateformes de marketing et d’automatisation des courriers électroniques.

**Fragment de profil** : un fragment de profil est les informations de profil d’une seule identité de la liste des identités qui existent pour un client particulier.

**Identifiant de profil** : un identifiant de profil est un identifiant généré automatiquement associé à un type d’identité et représente un profil.

**Propriété** : dans le contexte des balises, une propriété est un conteneur pour tout ce qui est nécessaire au déploiement d’un ensemble de balises.

## Q

**Requête** : les requêtes sont des requêtes de données provenant de tables de base de données.

**Éditeur de requêtes** : Query Editor est un outil permettant d’écrire, de valider et d’envoyer des instructions SQL dans [!DNL Query Service].

## R

**Real-Time Customer Data Platform** : Adobe Real-Time Customer Data Platform (Real-Time CDP) rassemble des données clients connues et inconnues afin de créer des profils clients approuvés avec une intégration simplifiée, une segmentation intelligente et une activation en temps réel sur le parcours client numérique.

**Real-Time Customer Profile** : Real-Time Customer Profile (parfois appelé Profile) offre une vue d’ensemble de chaque client en combinant des données provenant de plusieurs canaux, notamment en ligne, hors ligne, CRM et tiers. Profile vous permet de consolider vos données client en profils individuels offrant des comptes horodatés exploitables de chaque interaction client.

**Recette** : une recette est le terme d’Adobe d’une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente des processus d’apprentissage automatique spécifiques, des algorithmes d’IA, une logique de traitement et des paramètres de configuration requis pour créer et exécuter un modèle formé et ainsi aider à résoudre des problèmes d’entreprise spécifiques.

**Enregistrement** : un enregistrement est une donnée qui persiste sous forme de lignes dans un jeu de données.

**Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.

**Périodicité** : dans [!DNL Query Service], une périodicité définit si une requête doit s’exécuter une seule fois ou de manière récurrente.

**Représentation** : dans [!DNL Offer Decisioning], une représentation est une information utilisée par un canal pour afficher une offre, comme l’emplacement ou la langue.

**Ressource** : dans le contexte des balises, une ressource est un terme générique qui fait référence aux options que l’utilisateur peut configurer dans l’environnement client, y compris les extensions, les éléments de données et les règles.

**Contrôle d’accès en fonction du rôle** : le contrôle d’accès en fonction du rôle permet aux administrateurs d’attribuer un accès et des autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création de sandbox, la définition de schémas et la gestion des jeux de données.

**Règle** : dans le contexte des balises, une règle est un ensemble de composants définissant un ensemble spécifique d’événements, de conditions et d’actions qui doivent être regroupés logiquement.

**Composant de règle** : dans le contexte des balises, les composants de règle sont les événements, les conditions et les actions qui constituent une règle.

**Runtime** : Runtime spécifie un environnement d’exécution pour une recette d’apprentissage automatique. Les instances [!DNL Python], R, [!DNL Spark], PySpark et Tensorflow vous permettent de saisir une URL vers une image Docker pour une source de recette.

## S

**Exemple de données** : les exemples de données sont un aperçu d’un fichier de données, généralement les 100 premières lignes, qui fournit à un spécialiste des données ou à un ingénieur une idée du schéma ou des données qu’il contient.

**Sandbox** : un environnement de test est une structure virtuelle qui partitionne une instance de plateforme unique en un environnement virtuel distinct, afin de favoriser le développement et l’évolution d’applications d’expérience numérique.

**Réinitialisation d’un environnement de test** : une réinitialisation d’un environnement de test supprime toutes les données, y compris les données, les profils et les segments d’un environnement de test. Les réinitialisations des environnements de test peuvent affecter les données connectées à des destinations internes ou externes.

**Sélecteur d’environnement de test** : la commande de sélecteur d’environnement de test dans Experience Platform permet aux utilisateurs de naviguer entre les environnements de test auxquels ils ont accès. Le fait de changer de sandbox modifie tout le contenu et peut modifier l’accès aux fonctionnalités en fonction des autorisations.

**Schedule** : une planification est une spécification définie par l’utilisateur sur la fréquence ou la cadence d’ingestion des données d’une source de données tierce vers Adobe Experience Platform.

**Scoring** : la notation est le processus de génération d’informations à partir de données à l’aide d’un modèle formé.

**Schéma** : un schéma est un ensemble de règles qui représentent et valident la structure et le format des données. Un schéma est constitué d’une classe et d’un ou de plusieurs groupes de champs facultatifs. Il est utilisé pour créer des jeux de données et des flux de données. Un schéma peut inclure des attributs comportementaux, des horodatages, des identités, des définitions d’attributs, des relations, etc.

**Groupe de champs de schéma** : dans le modèle de données d’expérience (XDM), un groupe de champs de schéma permet aux utilisateurs d’étendre les champs réutilisables pour définir un ou plusieurs attributs destinés à être inclus dans un schéma.

**Bibliothèque de schémas** : la bibliothèque de schémas contient des ressources XDM standard du secteur mises à disposition par Adobe, ainsi que des ressources personnalisées définies par votre organisation.

**Registre des schémas** : le registre des schémas fournit une interface utilisateur et une API RESTful utilisées pour afficher et gérer toutes les ressources liées aux schémas dans la bibliothèque des schémas.

**Clé d’accès secrète** : une clé d’accès secrète est une clé S3 [!DNL Amazon] utilisée conjointement avec l’identifiant de clé d’accès pour signer des demandes AWS.

**Segment** : un segment est un ensemble de règles qui incluent des attributs et des données d’événement qui permettent à un certain nombre de profils de devenir une audience.

**Créateur de segments** : [!DNL Segment Builder] est un environnement de développement visuel utilisé pour créer des définitions de segment. Il sert de composant commun à toutes les applications utilisant Experience Platform Segmentation Service.

**Définition de segment** : une définition de segment est l’ensemble de règles utilisé pour décrire les caractéristiques ou le comportement clés d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.

**Méthode d’évaluation de segment** : il existe deux méthodes d’évaluation de segment : planifiée et à la demande. L’évaluation planifiée active un planning récurrent pour exécuter une tâche d’exportation à un moment spécifique, tandis que l’évaluation sur demande implique la création d’une tâche de segmentation pour créer immédiatement l’audience.

**Exportation de segments** : l’exportation de segments est l’un des deux types de destinations dans Experience Platform. Avec l’exportation de segments, vous pouvez envoyer les profils qui remplissent les critères et qui ont été mappés à la destination. Elle utilise les identifiants de segment et d’utilisateur, ainsi que les données pseudonymes, et s’intègre généralement aux réseaux sociaux et aux autres plateformes cible de médias numériques.

**Identifiant de segment** : un identifiant de segment est un identifiant généré automatiquement associé à un segment.

**Appartenance au segment** : l’adhésion au segment affiche le ou les segments auxquels fait actuellement partie un profil.

**Règles de segment** : les règles de segment définissent les conditions qui déterminent si un profil est admissible pour un segment.

**Segmentation** : la segmentation consiste à diviser un grand groupe de clients, de prospects ou de consommateurs en groupes plus petits partageant des attributs similaires et réagissant de la même manière à des stratégies marketing spécifiques.

**Sensei ML Framework** : Sensei ML Framework est un framework d’apprentissage automatique unifié qui exploite des données Experience Platform pour permettre aux spécialistes des données de développer des services d’intelligence pilotés par ML d’une manière plus rapide, évolutive et réutilisable.

**Étiquettes Sensibles (&quot;S&quot;)** : les étiquettes Sensibles (&quot;S&quot;) sont utilisées pour catégoriser des données jugées sensibles, telles que différents types de données comportementales ou géographiques que vous souhaitez marquer comme sensibles.

**Services** : cadre puissant pour rendre opérationnels les services d’intelligence artificielle et d’apprentissage automatique en exploitant les services intelligents d’Adobe. Services offre des expériences client personnalisées en temps réel ou rendent opérationnels des services intelligents personnalisés.

**Action marketing de personnalisation d’identité unique** : action marketing qui utilise des données pour la personnalisation de contenu sur site. La personnalisation sur site correspond à toutes les données utilisées pour faire des inférences sur les intérêts des utilisateurs et qui servent à sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Libellé d’utilisation des données S1** : un libellé d’utilisation des données `S1` est utilisé pour classer les données spécifiant la latitude et la longitude qui peuvent être utilisées pour déterminer l’emplacement précis d’un appareil.

**Libellé d’utilisation des données S2** : un libellé d’utilisation des données `S2` est utilisé pour classer les données qui peuvent être utilisées pour déterminer une zone de géobarrière définie plus largement.

**Source** : une source est un terme général pour tout connecteur d’entrée dans Platform. Voir aussi : Connecteur Source

**Attribut Source** : un attribut source est un champ dans le jeu de données source. Les attributs sources sont mappés aux champs de schémas sources.

**Catalogue Source** : le catalogue source est la liste des connecteurs source disponibles dans Experience Platform.

**Catégorie Source** : une catégorie de source est un groupe de sources ayant des caractéristiques similaires.

**Connecteur Source** : les connecteurs Source (également appelés sources) aident les utilisateurs à ingérer facilement des données provenant de plusieurs sources, ce qui permet de structurer, d’étiqueter et d’améliorer les données à l’aide de services Experience Platform. Les données peuvent être ingérées à partir de différentes sources, comme le stockage dans le cloud, les logiciels tiers et les systèmes de gestion de la relation client.

**Connexion en continu** : une connexion en continu est un point de terminaison unique fourni par Adobe et lié à votre organisation pour diffuser des données dans Experience Platform.

**Espace de noms d’identité standard** : les espaces de noms d’identité standard sont des espaces de noms d’identité prédéfinis fournis par Adobe, qui représentent les solutions standard généralement utilisées pour identifier les clients.

**Ingestion par flux** : l’ingestion par flux vous permet d’envoyer en temps réel des données de périphériques côté client et côté serveur vers Experience Platform.

**Segmentation par flux** : la segmentation par flux est un processus continu de sélection de données qui met à jour les segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-Time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

**Vue du système** : la vue du système est une représentation visuelle des jeux de données source qui transitent par [!DNL Real-Time Customer Profile] vers les destinations.

## T

**Balises** : dans Adobe Experience Platform, les balises fournissent des outils pour déployer, unifier et gérer les intégrations d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes sur tous les appareils client.

**Fonctionnalités cibles** : dans le mappage des fonctionnalités, une fonctionnalité cible est la fonctionnalité prédite par un modèle.

**Données de série temporelle** : les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.

**Modèle formé** : un modèle formé représente la sortie exécutable d’un processus de formation de modèle, dans lequel un ensemble de données d’apprentissage a été appliqué à l’instance de modèle. Un modèle formé conserve une référence au service web intelligent qui est créé à partir de celui-ci. Un modèle formé est adapté à la notation et à la création d’un service web intelligent.

**Jeton** : un jeton est un type de sécurité d’authentification à deux facteurs qui peut être utilisé pour autoriser l’utilisation de services informatiques avec [!DNL Query Service].

## U

**UCPA** : [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) crée le droit pour un consommateur de savoir quelles données personnelles une entreprise collecte, comment l&#39;entreprise utilise ses données personnelles et si l&#39;entreprise vend ses données personnelles. Les consommateurs peuvent demander à l’entreprise de supprimer ou d’arrêter la vente de leurs données personnelles.

**Schéma d’union** : un schéma d’union est une consolidation des schémas qui partagent la même classe et qui ont été activés pour [!DNL Real-Time Customer Profile]. Plusieurs schémas d’union peuvent exister pour une organisation, mais il ne peut y avoir qu’un seul schéma d’union par classe.

## V

**VCDPA** : [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) fournit de nouveaux droits de confidentialité des données aux résidents de la Virginie (&quot;Consommateurs&quot;), y compris le droit d’accéder à des données personnelles, de les supprimer et de les corriger. Les consommateurs ont également le droit de se désabonner de la vente de données personnelles, de se désabonner du profilage basé sur les données personnelles et du traitement des fins publicitaires personnelles.

## W

## X

**XDM** : voir Modèle de données d’expérience (XDM).

**Événement de décision XDM** : l’événement de décision XDM est une classe basée sur une série temporelle utilisée pour recueillir des observations sur le résultat et le contexte d’une activité de décision. Cela comprend des renseignements sur la façon dont la décision a été prise, le moment où elle a eu lieu, les options proposées (et choisies) et l’état contextuel qui a influé sur la décision ou qui a pu être observé pendant le processus de décision.

**XDM ExperienceEvent** : XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) s’est produit, y compris le moment et l’identité du sujet concerné. Voir aussi : Événement d’expérience

**XDM Individual Profile** : XDM [!DNL Individual Profile] est une classe basée sur les enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés.  Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses e-mail.

**Système XDM** : le système XDM représente la structure qui rend les schémas XDM opérationnels pour les utiliser dans les services Experience Platform en aval.

## Y

## Z
