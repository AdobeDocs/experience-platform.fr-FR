---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Glossaire Adobe Experience Platform
description: Glossaire reprenant la terminologie principale d’Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '8009'
ht-degree: 12%

---

# Glossaire Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Contrôle d’accès** : le contrôle d’accès en fonction du rôle permet aux administrateurs d’attribuer des accès et des autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création de sandbox, la définition de schémas et la gestion des jeux de données.

**ID de clé d’accès** : un ID de clé d’accès est un identifiant unique associé à une clé d’accès secrète [!DNL Amazon] S3. L’ID de clé d’accès et la clé d’accès secrète sont utilisés conjointement pour signer les demandes [!DNL Amazon Web Services] (AWS).

**Action** : dans le contexte des balises, une action est un type spécifique de composant de règle qui définit ce qui doit se produire une fois qu’un événement se produit et que les conditions sont évaluées et transmises.

**Activer** : l’activation est l’action effectuée par un utilisateur pour mapper un segment ou des profils à une destination telle que [!DNL Oracle Eloqua], [!DNL Google] ou [!DNL Salesforce Marketing Cloud].

**Activité** : dans [!DNL Offer Decisioning], une activité contient la logique qui sous-tend la sélection d’une offre.

**Administrateur** : au moins une personne de votre organisation peut configurer et personnaliser les autorisations pour Experience Platform dans Adobe Admin Console.

**Adobe Admin Console** : Adobe Admin Console fournit un emplacement central pour la gestion des droits et des accès aux produits Adobe pour votre organisation. Par le biais de la console, les administrateurs et administratrices peuvent accorder des autorisations d’accès à des groupes d’utilisateurs et d’utilisatrices pour diverses fonctionnalités d’Experience Platform, telles que « Gérer les jeux de données », « Afficher les jeux de données » ou « Gérer les profils ».

**Adobe Experience Platform** : Adobe Experience Platform normalise les données et le contenu dans l’ensemble de l’entreprise, alimentant les profils consommateurs en temps réel, permettant l’utilisation de la science des données et accélérant la vitesse de diffusion du contenu afin d’orienter la personnalisation de l’expérience sur le parcours client.

**Adobe Experience Platform Query Service** : permet aux analystes de données d’interroger les événements et les profils à utiliser dans les analyses et le machine learning. Grâce à Query Service, les analystes et les spécialistes des données peuvent extraire tous leurs jeux de données stockés dans Experience Platform (y compris les données comportementales, les points de vente, la gestion de la relation client, etc.) et interroger ces jeux de données pour répondre à des questions spécifiques sur les données.

**Adobe Experience Platform Segmentation Service** : permet de créer des segments et de générer des audiences à partir de vos données du profil client en temps réel. Ces audiences peuvent ensuite être exportées vers leurs propres jeux de données dans le lac de données.

**Adobe Intelligent Services** : les services intelligents tels que l’IA dédiée à l’attribution et l’IA dédiée aux clients sont des modèles d’apprentissage automatique basés sur l’intelligence artificielle qui sont conçus spécifiquement et qui nécessitent l’exécution et le fonctionnement d’Experience Platform.

**Adobe I/O** : Adobe I/O fait partie d’Experience Platform et donne accès à tout ce dont les développeurs ont besoin pour intégrer, étendre et personnaliser Experience Platform, y compris aux API, aux événements, à la console de développement et aux outils utiles.

**Adobe Sensei** : Adobe Sensei est le cadre d’intelligence artificielle qui alimente Experience Platform. Il fournit également un ensemble de services d’IA qui permet aux marques d’améliorer leur capacité à fournir des expériences client personnalisées en temps réel.

**Compartiment Amazon S3** : les compartiments [!DNL Amazon S3] sont les conteneurs de base pour les données stockées dans l’écosystème [!DNL Amazon]. Les compartiments contiennent des objets, chaque objet est stocké et récupéré à l’aide d’une clé unique attribuée par le développeur.

**Connecteur Amazon S3** : le connecteur [!DNL Amazon] S3 permet aux clients d’Experience Platform de se connecter et d’accéder en toute sécurité à leurs données [!DNL Amazon] S3.

**APA** : Le [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) promeut et protège la vie privée des individus et réglemente la façon dont les agences et organisations du gouvernement australien traitent les informations personnelles. Le [!DNL Privacy Act] comprend des principes qui s&#39;appliquent aux organisations du secteur privé. Par exemple, les particuliers ont le droit de comprendre pourquoi les renseignements personnels sont recueillis et comment ils seront utilisés, la possibilité d&#39;y accéder, d&#39;effacer leurs données et de corriger les renseignements personnels.

**Ajouter une stratégie d’enregistrement** : la stratégie d’enregistrement « ajouter » est une option utilisée lors de la spécification des données tierces à ingérer via une connexion et de l’ajout de toute nouvelle donnée ou ligne à la fin du jeu de données. Les lignes précédemment ingérées restent intactes et seules les lignes créées depuis la dernière exécution planifiée sont ingérées dans Experience Platform. Toutes les lignes modifiées dans le système source restent inchangées dans Experience Platform.

**Tableau** : les tableaux sont utilisés pour les éléments ordonnés avec le même type de données.

**Intelligence artificielle** : l’intelligence artificielle est une théorie et le développement de systèmes informatiques capables d’effectuer des tâches qui nécessitent normalement l’intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction entre les langues.

**Attributs** : les attributs sont des caractéristiques spécifiées qui représentent un profil.

**Fusion d’attributs** : lors de la définition d’une politique de fusion à l’aide de l’API Real-Time Customer Profile, l’objet `attributeMerge` indique la manière dont la politique de fusion donnera la priorité aux attributs de profil en cas de conflits de données. Cela revient à sélectionner une [!UICONTROL méthode de fusion] lors de la définition d’une politique de fusion dans l’interface utilisateur d’Experience Platform.

**IA dédiée à l’attribution** : [!DNL Attribution AI] est un service intelligent optimisé par Adobe Sensei qui offre des fonctionnalités d’attribution algorithmique multicanal tout au long du cycle de vie du client.

**Audience** : une audience est l’ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

**Taille de l’audience** : une taille d’audience est le nombre total de profils qui répondent aux critères d’une définition de segment et qui remplissent les critères d’appartenance à l’audience.

**Instantané d’audience** : un instantané d’audience capture tous les profils qui remplissent les critères du segment au moment de la segmentation.

## B

**Renvoi** : pour les sources planifiées, l’option de renvoi permet l’ingestion de données historiques.

**Période de renvoi** : la période de renvoi est une option permettant de définir la durée d’ingestion des données historiques tierces via une connexion source. La sélection d’une période de renvoi « à tout jamais » entraîne l’ingestion de l’historique complet des données sources vers Experience Platform.

**Lot** : un lot est un ensemble de données collectées sur une période de temps et traitées ensemble comme une seule unité. Les jeux de données sont composés de plusieurs lots.

**Identifiant de lot** : un identifiant de lot est un identifiant généré par Adobe pour un lot de données.

**Ingestion par lots** : l’ingestion par lots vous permet d’ingérer des données dans Experience Platform sous forme de fichiers de lots. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique.

**Segmentation par lots** : la segmentation par lots est une alternative à un processus de sélection de données en cours et déplace toutes les données de profil à la fois dans les définitions de segment pour produire des audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin de pouvoir être exporté en vue de son utilisation.

**Version** : dans le contexte des balises, une version est un fichier ou un ensemble de fichiers contenant toutes les configurations et le code nécessaires à l’exécution de la logique commerciale contenue dans une bibliothèque, ce qui vous permet de déployer cette bibliothèque sur votre site web ou votre application mobile.

**Outils de Business Intelligence** : les outils de Business Intelligence (BI) sont principalement intégrés à [!DNL Experience Platform Query Service]. Les outils de BI sont des types de programmes d’application qui collectent et traitent de grandes quantités de données non structurées à partir de systèmes internes et externes.

## C

**Limitation** : en [!DNL Offer Decisioning], la limitation (également appelée limitation de la fréquence) est utilisée dans les règles de prise de décision pour définir le nombre de présentations d’une offre. Il existe deux types de limitations : le nombre de fois où une offre peut être proposée à l&#39;audience cible combinée (appelée « limitation globale ») et le nombre de fois où une offre peut être proposée au même utilisateur final (appelée « limitation de profil »).

**Catalogue** : dans le cadre des sources et des destinations, un catalogue est une galerie avec des connexions disponibles aux applications Adobe et aux technologies tierces. À ne pas confondre avec [!DNL Catalog Service].

**[!DNL Catalog Service]** : [!DNL Catalog Service] (parfois appelé [!DNL Catalog]) est le système d’enregistrement de l’emplacement et de la traçabilité des données dans Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, [!DNL Catalog] contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche, de surveillance et de gouvernance des données.

**CCPA** : Le [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) renforce les droits à la vie privée et à la protection des consommateurs pour les résidents de Californie, aux États-Unis. Le CCPA accorde plusieurs nouveaux droits à la confidentialité des données aux résidents de Californie, y compris le droit d’accéder et de supprimer leurs données personnelles, de savoir si ces données personnelles sont vendues ou divulguées (et à qui) et le droit de refuser (opt-out) que ces données soient vendues à des tiers.

**Classe** : dans le modèle de données d’expérience (XDM), une classe définit le plus petit ensemble de champs utilisés pour créer un schéma et définit le comportement de base de l’objet métier que le schéma représente.

**Client** : un client est un outil ou une application externe qui se connecte à [!DNL Query Service] via [!DNL PostgreSQL] protocole ou une API HTTP.

**Collection** : dans [!DNL Offer Decisioning], les collections sont des sous-ensembles d&#39;offres, basés sur des conditions prédéfinies établies par un marketeur, telles que la catégorie de l&#39;offre.

**Combiner avec une action marketing sur les PII** : action marketing qui combine des informations d’identification personnelle (PII) avec des données anonymes. Les contrats relatifs aux données provenant de réseaux publicitaires, de serveurs de publicités et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données avec des données directement identifiables.

**Interface de ligne de commande** : une interface de ligne de commande est un outil textuel qui peut être utilisé pour se connecter à [!DNL Query Service] pour l’exécution de requêtes brutes.

**Composition** : une composition est un groupe de composants qui se forment ensemble pour constituer le schéma.

**Condition** : dans le contexte des balises, une condition est un composant de règle qui évalue une instruction logique qui doit renvoyer `true` ou `false`. Toutes les conditions doivent être évaluées sur `true` et toutes les conditions d’exception doivent être évaluées sur `false` avant l’exécution des actions de la règle.

**Console** : en [!DNL Query Service], la console fournit des informations sur le statut et le fonctionnement d’une requête. La console affiche le statut de la connexion à [!DNL Query Service], les opérations des requêtes en cours d’exécution et tout message d’erreur résultant de ces requêtes.

**Libellés de contrat (« C »)** : les libellés d’utilisation des données de contrat (« C ») sont utilisés pour classer les données contenant des obligations contractuelles ou liées aux politiques de gouvernance des données de votre entreprise.

**CPRA** : la [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) élargit et modifie certaines parties de la [!DNL California Consumer Privacy Act (CCPA)]. La [!DNL CPRA] établit une nouvelle base de référence pour la confidentialité des données des consommateurs en Californie en renforçant les droits des consommateurs et en élargissant le type de données couvertes par une définition plus large des informations personnelles sensibles. En outre, le [!DNL CPRA] a créé la California Privacy Protection Agency, une nouvelle agence dédiée à la mise en œuvre et à l’application des règles de confidentialité des données.

**Libellé de contrat C1** : un libellé d’utilisation des données de contrat `C1` spécifie que les données peuvent uniquement être exportées à partir de Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants d’appareils ou d’individus. Par exemple, les données provenant des réseaux sociaux.

**Libellé de contrat C2** : un libellé d’utilisation des données de contrat `C2` spécifie les données qui ne peuvent pas être exportées vers un tiers. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent l’exportation de données à partir de l’endroit où elles ont été collectées à l’origine. Par exemple, les contrats des réseaux sociaux limitent souvent le transfert des données que vous recevez d’eux. L’étiquette C2 est plus restrictive que la C1, qui ne nécessite que l’agrégation et des données anonymes.

**Libellé de contrat C3** : un libellé d’utilisation de données de contrat `C3` spécifie les données qui ne peuvent pas être combinées ou autrement utilisées avec des informations directement identifiables. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent la combinaison ou l’utilisation de ces données avec des informations directement identifiables. Par exemple, les contrats pour les données provenant des réseaux publicitaires, des serveurs de publicités et des fournisseurs de données tiers incluent souvent des interdictions contractuelles spécifiques sur l’utilisation des données directement identifiables.

**Libellé de contrat C4** : un libellé d’utilisation de données de contrat `C4` spécifie que les données ne peuvent pas être utilisées pour cibler des annonces ou du contenu, sur site ou intersite. L’étiquette C4 est l’étiquette la plus restrictive puisqu’elle englobe les étiquettes C5, C6 et C7.

**Libellé de contrat C5** : un libellé d’utilisation des données de contrat `C5` spécifie que les données ne peuvent pas être utilisées pour le ciblage intersite du contenu ou des annonces en fonction des intérêts. Le ciblage en fonction des intérêts, ou personnalisation, se produit si les trois conditions suivantes sont remplies : les données collectées sur site sont utilisées pour établir des inférences sur les intérêts d’un utilisateur ou d’une utilisatrice ; elles sont utilisées dans un autre contexte, par exemple sur un autre site ou sur une autre application ; et elles sont utilisées pour sélectionner le contenu ou les annonces diffusés en fonction de ces inférences.

**Libellé de contrat C6** : un libellé d’utilisation des données de contrat `C6` spécifie que les données ne peuvent pas être utilisées pour le ciblage d’annonces sur site. Le ciblage des annonces sur site comprend la sélection et la diffusion d’annonces sur les sites web ou applications de votre entreprise ou pour mesurer la diffusion et l’efficacité de ces annonces. Cela inclut l’utilisation des données sur site collectées précédemment concernant l’intérêt des utilisateurs pour sélectionner des publicités, le traitement des données sur les publicités affichées, le moment et le lieu de leur diffusion, et le fait de savoir si les utilisateurs ont pris des mesures en rapport avec la publicité, telles que la sélection d’une publicité ou la réalisation d’un achat.

**Libellé de contrat C7** : un libellé d’utilisation des données de contrat `C7` spécifie que les données ne peuvent pas être utilisées pour le ciblage de contenu sur site. Le ciblage du contenu sur site comprend la sélection et la diffusion de contenu sur les sites web ou les applications de votre entreprise ou pour mesurer la diffusion et l’efficacité de ce contenu. Cela inclut les informations précédemment collectées sur l’intérêt des utilisateurs pour sélectionner du contenu, le traitement des données concernant le contenu diffusé, la fréquence ou la durée de sa diffusion, le moment et le lieu de sa diffusion, et le fait de savoir si les utilisateurs ont pris des mesures en rapport avec le contenu, par exemple en sélectionnant le contenu.

**Libellé de contrat C8** : un libellé d’utilisation des données de contrat `C8` spécifie que les données ne peuvent pas être utilisées pour mesurer les sites web ou les applications de votre organisation. Cela ne comprend pas le ciblage basé sur l’intérêt, qui est la collecte d’informations sur votre utilisation de ce service pour personnaliser par la suite le contenu et/ou la publicité dans d’autres contextes.

**Libellé de contrat C9** : un libellé d’utilisation des données de contrat `C9` spécifie que les données ne peuvent pas être utilisées dans les workflows de science des données. Certains contrats prévoient des interdictions explicites sur les données utilisées pour la science des données. Parfois, cela fait partie de conditions qui interdisent l’utilisation de données pour l’intelligence artificielle (IA), l’apprentissage automatique ou la modélisation.

**Libellé de contrat C10** : un libellé d’utilisation des données de contrat `C10` spécifie que les données ne peuvent pas être utilisées pour l’activation de l’identité groupée. Certaines politiques dʼutilisation des données limitent lʼutilisation de données dʼidentité assemblées pour la personnalisation. Le libellé `C10` est automatiquement appliqué aux segments si leurs politiques de fusion utilisent l’option « graphique privé ».

**Colonne de date créée** : la sélection d’une colonne de date créée est une option lors de la spécification de données tierces via une connexion source. Lorsque la stratégie d’enregistrement d’ajout est sélectionnée et que le schéma du jeu de données contient plusieurs champs de date, vous devez choisir parmi les schémas disponibles pour spécifier une colonne clé de date créée. L’option Date de création n’est pas disponible lorsque la stratégie d’enregistrement de remplacement est sélectionnée.

**Create Table as Select** : la commande CTAS (Create Table as Select) est une commande SQL qui, lorsqu’elle est exécutée dans le cadre d’une requête SQL complète et valide, [!DNL Query Service] demande de conserver les résultats de la requête dans un jeu de données. Vous pouvez créer un nouveau jeu de résultats, remplacer les résultats précédents ou ajouter aux résultats précédents.

**Données intersites** : les données intersites sont la combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site.

**Action marketing de ciblage intersite** : action marketing qui utilise des données pour le ciblage publicitaire intersite. La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les données intersites sont généralement collectées et traitées afin d’établir des inférences sur les intérêts des clients.

**Espace de noms d’identité personnalisé** : votre organisation peut créer des espaces de noms d’identité personnalisés pour représenter les identités d’une organisation ou d’une analyse de rentabilité spécifique.

**Libellés personnalisés** : les libellés d’utilisation des données personnalisés vous permettent de créer et d’appliquer des libellés spécifiques aux champs de données qui répondent à des besoins professionnels spécifiques.

**IA dédiée aux clients** : l’IA dédiée aux clients est un service intelligent optimisé par Adobe Sensei qui enrichit les profils clients avec des propensions basées sur l’IA et renforce la segmentation et le ciblage des clients.

## D

**Quotidien** : dans le cadre d’exportations de fichiers planifiées, planifie des exportations de fichiers complets ou incrémentiels une fois par jour, tous les jours, de la date de début à la date de fin à l’heure spécifiée par l’utilisateur.

**Dictionnaire de données** : dans le contexte des balises, un dictionnaire de données (également appelé mappage de données) est un ensemble d’éléments de données défini dans une propriété.

**Élément de données** : dans le contexte des balises, un élément de données est un pointeur utilisé dans les règles et extensions pour pointer vers une donnée spécifique existant sur l’appareil client.

**Ingestion des données** : l’ingestion des données est le processus d’ajout de données d’une source à Experience Platform. Les données peuvent être ingérées par Experience Platform de différentes manières : en flux continu, par lots ou ajoutées par le biais des connecteurs source.

**Couche de données** : dans le contexte des balises, une couche de données est une structure de données qui existe sur l’appareil client et qui contient des métadonnées sur le contexte dans lequel une page ou un écran est affiché.

**Gouvernance des données** : la gouvernance des données englobe les stratégies et technologies utilisées pour s’assurer que les données sont conformes aux réglementations et aux politiques organisationnelles en matière d’utilisation des données.

**Partenaires d’intégration des données** : les partenaires d’intégration des données simplifient et automatisent le chargement et la transformation de volumes considérables de données de plus de 200 sources vers Experience Platform sans avoir à écrire de code.

**Libellés du jeu de données** : les libellés d’utilisation des données peuvent être ajoutés aux jeux de données. Tous les champs de ce jeu de données héritent des libellés du jeu de données.

**Workspace de science des données** : [!DNL Data Science Workspace] dans Experience Platform permet aux clients de créer des modèles de machine learning à l’aide de données dans les applications Experience Platform et Adobe, afin de créer des segments intelligents, de générer des informations et de fournir des prédictions, ce qui vous permet d’améliorer considérablement les expériences digitales des utilisateurs finaux.

**Source de données** : une source de données est une origine de données désignée par l’utilisateur. Une source de données peut être, par exemple, une application mobile, des événements de profil et/ou d’expérience, des événements de profil de site web ou un CRM.

**Gestionnaire de données** : un gestionnaire de données est la personne responsable de la gestion, de la supervision et de l’application des ressources de données d’une organisation. Un gestionnaire de données s’assure également que les politiques de gouvernance des données sont protégées et conservées conformément aux réglementations gouvernementales et aux politiques organisationnelles.

**Flux de données** : un flux de données est un ensemble ou une collection de messages qui partagent le même schéma et sont envoyés par la même source.

**Type de données** : un type de données est une ressource XDM réutilisable qui définit un champ de type objet contenant plusieurs propriétés dans une représentation hiérarchique.

**Libellés d’utilisation des données** : les libellés d’utilisation des données vous permettent de classer les données en fonction des considérations liées à la confidentialité et des conditions contractuelles afin de les rendre conformes aux réglementations et aux politiques d’entreprise. Les libellés d’utilisation des données ajoutés à un jeu de données sont hérités ou appliqués à tous les champs de ce jeu. Les libellés d’utilisation des données peuvent également être appliqués directement aux champs.

**Flux de données** : un flux de données est un pipeline virtuel de données qui entre dans Experience Platform à partir d’une source et vers des destinations.

**Exécution du flux de données** : une exécution de flux de données est un flux de données qui arrive dans Experience Platform selon un planning spécifié par l’utilisateur.

**Jeu de données** : un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’un tableau, qui contient un schéma (colonnes) et des champs (lignes).

**Identifiant du jeu de données** : identifiant généré par Adobe pour un jeu de données ingéré.

**Sortie du jeu de données** : la sortie du jeu de données fournit un mécanisme permettant de déterminer ce que l’option « Créer une table en tant que sélectionner » sera utilisée pour une exécution de [!DNL Query Service] spécifique.

**Clé de déduplication** : clé primaire définie par l’utilisateur qui détermine l’identité par laquelle les utilisateurs souhaitent dédupliquer leurs profils&#x200B;

**Colonne delta** : une colonne delta permet de sélectionner un champ de données source pour représenter une date et une heure pour l’ingestion incrémentielle.

**Stratégie d’enregistrement delta** : la stratégie d’enregistrement delta est une option permettant d’ingérer des données tierces via une connexion source. Cette option permet à l’utilisateur de spécifier que les lignes de données sources nouvelles ou modifiées sont assimilées à Experience Platform. De nouvelles lignes sont ajoutées à la fin du jeu de données et les lignes modifiées sont mises à jour dans le jeu de données d’Experience Platform.

**Descriptor** : dans le modèle de données d’expérience (XDM), un descripteur est un ensemble supplémentaire de métadonnées liées au schéma qui décrit un comportement spécifique pour un champ. Les descripteurs peuvent être utilisés par Experience Platform pour comprendre le comportement de schéma prévu, tel que la relation entre deux schémas.

**Destination** : une destination est un terme général pour tout point d’entrée, tel qu’une application Adobe, une plateforme publicitaire, un service de stockage dans le cloud ou un service marketing, où une audience est activée et diffusée.

**Catégorie de destination** : une catégorie de destination est un groupe de destinations ayant des caractéristiques similaires.

**Catalogue de destinations** : un catalogue de destinations est une liste de destinations disponibles dans Experience Platform.

**Règles d’appel direct** : dans le contexte des balises, une règle d’appel direct est une règle qui s’exécute lorsqu’elle est appelée directement à partir de la page, en contournant les systèmes de détection des événements et de recherche.

**Nom d’affichage** : dans le modèle de données d’expérience (XDM), un nom d’affichage est un nom convivial pour un champ qui s’affiche dans l’interface utilisateur.

## E

**Offre éligible** : une offre éligible peut être proposée de manière cohérente à un profil, dans la mesure où elle répond aux contraintes définies en amont.

**Règles d’éligibilité** : dans [!DNL Offer Decisioning], les règles d’éligibilité sont appliquées à un profil associé aux contraintes de calendrier, de planning et de limitation.

**Action marketing de ciblage par e-mail** : action marketing qui utilise des données dans les campagnes de ciblage par e-mail.

**Code incorporé** : dans le contexte des balises, le code incorporé est une balise de script placée dans l’HTML sur un site ou un environnement. Le code incorporé indique au navigateur où récupérer la version.

**Énumération** : une énumération (enum) est un champ XDM limité à un ensemble de valeurs prédéfinies.

**Environnement** : dans le contexte des balises, un environnement est un ensemble d’instructions de déploiement qui spécifie la diffusion hôte et le format de fichier d’une version. Une bibliothèque doit être associée à un environnement avant qu’il puisse être créé.

**Diagnostics d’erreur** : les diagnostics d’erreur permettent la génération de messages d’erreur détaillés pour les lots ingérés. Le seuil d’erreur vous permet de configurer le pourcentage d’erreurs acceptables avant l’échec d’un lot.

**Événement** : dans le contexte des balises, un événement est un type spécifique de composant de règle, qui est un déclencheur qui se produit sur un appareil client pour commencer l’exécution d’une règle.

**Entités d’événement** : dans le contexte de la modélisation des données, les entités d’événement représentent des concepts liés aux actions qu’un client ou une cliente peut entreprendre, aux événements système ou à tout autre concept dans lequel vous souhaitez peut-être suivre les modifications au fil du temps. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la classe [!DNL XDM ExperienceEvent].

**Événements** : les événements sont les données de comportement associées à un profil.

**Modèle de données d’expérience (XDM)** [!DNL Experience Data Model] (XDM) est un framework open source qui utilise des schémas standard pour unifier les données en vue de les utiliser avec des applications Experience Platform et Adobe Experience Cloud. XDM normalise la structure des données, et accélère et simplifie le processus d’obtention d’informations à partir d’énormes quantités de données.

**Expérience** : une expérience est le processus de création d’un modèle formé en formant l’instance avec une partie d’exemple de données de production actives. Ceci est différent d’un modèle formé testé par rapport à un jeu de données de test d’exclusion. Cela diffère également du concept d’expérience dans certains frameworks de machine learning, où il s’agit en fait d’un exemple de projet de modélisation.

**Événement d’expérience** : un événement d’expérience représente un instantané du système lorsqu’une interaction ou un événement lié à une expérience client a lieu. Les événements d’expérience sont des enregistrements de faits non modifiables de ce qui s’est produit et représentent ce qui s’est produit sans agrégation ni interprétation. Dans le modèle de données d’expérience (XDM), ce concept est capturé par la classe [!DNL XDM ExperienceEvent].

**Exporter un fichier complet** : fichier d’exportation contenant un cliché instantané complet de toutes les qualifications de profil pour le segment sélectionné.

**Exporter des fichiers incrémentiels** : une série de fichiers exportés où le premier fichier est un cliché instantané complet de toutes les qualifications de profil pour le segment sélectionné, et les fichiers suivants sont des qualifications de profil incrémentielles depuis l’exportation précédente.

**Extension** : dans le contexte des balises, une extension est un package de fonctionnalités ajoutées à une propriété de balise. Une extension est généralement axée sur une solution marketing ou analytique spécifique et fournit les outils nécessaires au déploiement de cette technologie dans un environnement client.

**Package d’extension** : dans le contexte des balises, un package d’extension est un fichier ZIP créé et chargé par un développeur d’extensions qui fournit tout le nécessaire pour que les utilisateurs de balises installent l’extension dans leur propriété. Un package d’extension contient un manifeste spécifiant des informations sur l’extension, l’HTML/JavaScript nécessaire aux utilisateurs finaux pour configurer le comportement de l’extension de balise et le JavaScript exécutable diffusé dans l’environnement client (si nécessaire).

## F

**Offres de secours** : une offre de secours est l&#39;offre par défaut affichée lorsqu&#39;un utilisateur final n&#39;est pas éligible à l&#39;une des offres de la collection utilisée.

**Mappage de fonctionnalités** : le mappage de fonctionnalités fait référence au processus de mappage de fonctionnalités à partir de données dans les fonctionnalités d’entrée et de cible requises par un modèle de machine learning.

**Champ** : un champ est l’élément de niveau le plus bas d’un jeu de données, tel que défini par le schéma XDM du jeu de données. Chaque champ possède un nom à des fins de référencement et un type pour indiquer le type de données qu’il contient. Les types de champ peuvent inclure (sans s’y limiter) des entiers, des nombres, des chaînes, des valeurs booléennes et des objets.

**Groupe de champs** : voir « Groupe de champs de schéma ».

**Libellés de champ** : les libellés de champ sont des libellés de gouvernance des données qui sont hérités d’un jeu de données ou appliqués directement à un champ.

**Nom du champ** : un nom de champ est utilisé pour référencer la valeur d’un champ dans les requêtes et les services en aval.

**Fréquence** : en [!DNL Query Service], la fréquence détermine la fréquence d’exécution d’une requête planifiée récurrente.

## G

**Géofence** : une géofence est une limite géographique virtuelle, définie par la technologie GPS ou RFID, qui permet au logiciel de déclencher une réponse lorsqu’un appareil mobile entre ou quitte une zone particulière.

**RGPD (Règlement général sur la protection des données)** : le Règlement général sur la protection des données (RGPD) est un cadre juridique qui définit des lignes directrices pour la collecte et le traitement des informations personnelles des individus au sein de l’Union européenne (UE). Le RGPD énonce les principes de la gestion des données et les droits des individus et couvre toutes les entreprises qui traitent les données des citoyens de l’UE.

**Mécanismes de sécurisation** : les mécanismes de sécurisation sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform. Les mécanismes de sécurisation peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

## H

**HIPAA** : la [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) est une loi fédérale des États-Unis créée pour améliorer l’efficacité des soins de santé, améliorer la portabilité de l’assurance maladie et protéger la vie privée des patients et des membres des régimes d’assurance maladie. En vertu de la loi HIPAA, les individus ont le droit d&#39;accéder à leurs informations, de les modifier et d&#39;obtenir des copies de leurs dossiers médicaux ou de leurs informations de santé. Les entités couvertes et les entreprises associées des entités couvertes doivent respecter les réglementations HIPAA.

**Hôte** : dans le contexte des balises, un hôte spécifie l’emplacement, le domaine et les informations d’identification de l’utilisateur nécessaires pour que le système diffuse une version.

**Par heure** : dans le contexte des exportations de fichiers planifiées, planifie des exportations de fichiers incrémentiels toutes les 3, 6, 8 ou 12 heures.

## I

**Identité** : une identité est un identifiant qui représente de manière unique un client individuel, tel qu’un identifiant de cookie, un identifiant d’appareil ou un identifiant de courrier électronique.

**Champs d’identité** : les champs d’identité sont des champs XDM utilisés pour rassembler des informations sur les clients individuels provenant de plusieurs sources de données. Une seule identité principale doit être définie pour que le schéma soit activé pour une utilisation dans le profil client en temps réel.

**Libellés d’identité (« I »)** : les libellés d’utilisation des données d’identité (« I ») sont utilisés pour classer les données permettant d’identifier ou de contacter une personne spécifique.

**Graphique d’identités** : un graphique d’identités est une carte des relations entre les identités assemblées et liées qui existent pour un client individuel. Chaque graphique d’identité est mis à jour en temps quasi réel avec l’activité du client. La structure commune des relations d’identité dans vos données est représentée par le [!UICONTROL graphique privé], qui sert de plan directeur structurel pour chaque graphique d’identité individuel.

**Espace de noms d’identité** : un espace de noms d’identité définit le contexte d’un identifiant, tel qu’une adresse e-mail ou un identifiant CRM.

**Service d’identités** : [!DNL Experience Platform Identity Service] permet la création et la gestion de types d’identité, ce qui vous permet de lier les identités des clients sur plusieurs appareils et canaux. La capacité du service à lier les identités entre elles permet au profil client en temps réel de fournir une représentation complète de chaque client individuel.

**Combinaison d’identités** : la combinaison d’identités est le processus d’identification de fragments de données et de leur combinaison pour former un enregistrement de profil complet.

**Symbole d’identité** : un symbole d’identité est l’abréviation d’un espace de noms d’identité qui peut être utilisé comme référence dans les API.

**Valeur d’identité** : une valeur d’identité, combinée à un espace de noms d’identité, est un identifiant qui représente un individu, une organisation ou une ressource unique. Lors de la mise en correspondance des données d’enregistrement sur les fragments de profil, l’espace de noms et la valeur d’identité doivent correspondre.

**Libellé d’utilisation des données I1** : le libellé d’utilisation des données `I1` est utilisé pour classer les données qui peuvent directement identifier ou contacter une personne spécifique plutôt qu’un appareil.

**Libellé d’utilisation des données I2** : le libellé d’utilisation des données `I2` est utilisé pour classer les données qui peuvent être utilisées en combinaison avec d’autres données pour identifier ou contacter indirectement une personne spécifique.

**Organisation IMS** : une organisation IMS (parfois appelée organisation IMS) est le nom utilisé pour identifier une société ou un groupe spécifique au sein d’une société sur plusieurs produits Adobe. Les administrateurs peuvent configurer et gérer l’accès et les autorisations des fonctionnalités pour les utilisateurs d’une organisation.

**Ingestion** : consultez la section Ingestion des données.

**Planification de l’ingestion** : une planification de l’ingestion fournit des options temporelles lors de l’ingestion d’une source vers Experience Platform.

**Fonction d’entrée** : une fonction d’entrée est spécifiée dans le mappage des fonctionnalités et est utilisée par un modèle de machine learning pour effectuer des prédictions.

**[!DNL Intelligent Services]** : les [!DNL Intelligent Services] telles que [!DNL Attribution AI] et [!DNL Customer AI] sont des modèles d’apprentissage automatique basés sur l’intelligence artificielle qui nécessitent Experience Platform (ou des applications reposant sur Experience Platform telles qu’Adobe Real-Time Customer Data Platform) pour fonctionner.

**Ciblage en fonction des intérêts ou personnalisation** : le ciblage en fonction des intérêts, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies :

1. Les données collectées sur site sont utilisées pour établir des inférences sur l’intérêt d’un utilisateur.
1. Les données sont utilisées dans un autre contexte, par exemple sur un autre site ou sur une autre application (hors site).
1. Les données sont utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

## J

**[!DNL JupyterLab]** : interface web open source pour Project [!DNL Jupyter] intégrée à l’interface utilisateur d’Experience Platform.

**[!DNL Jupyter Notebook]** : intégrés à JupyterLab, les notebooks Jupyter vous permettent d’effectuer un nettoyage et une transformation des données, une simulation numérique, une modélisation statistique, une visualisation des données, un machine learning et plus encore sur vos données Experience Platform dans divers langages tels que Python, Scala et PySpark.

## K

## L

**LGPD** : Le [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) vise à réglementer le traitement des données personnelles de toutes les personnes physiques au Brésil. Le LGPD donne aux citoyens brésiliens le droit d&#39;accéder à leurs données personnelles et de les supprimer, de savoir si leurs données personnelles sont vendues ou divulguées (et à qui), et le droit de refuser que leurs données soient vendues à des tiers.

**Bibliothèque** : dans le contexte des balises, une bibliothèque est un ensemble de logiques commerciales qui contient des instructions sur le comportement de la bibliothèque de balises sur l’appareil client.

**Entités de recherche** : dans le contexte de la modélisation des données, les entités de recherche représentent des concepts qui peuvent être associés à une personne individuelle, mais qui ne peuvent pas être directement utilisés pour identifier la personne. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur des classes de modèle de données d’expérience (XDM) personnalisées et liées à une entité de profil par le biais d’une [&#x200B; relation de schéma &#x200B;](../xdm/tutorials/relationship-ui.md).

## M

**Machine learning (ML)** : le machine learning est le domaine d&#39;étude qui permet aux ordinateurs d&#39;apprendre sans être explicitement programmés.

**Modèle de machine learning** : un modèle de machine learning est une instance d’une recette de machine learning qui est entraînée à l’aide de données historiques et de configurations pour résoudre un cas d’utilisation commercial. Dans Adobe Experience Platform Data Science Workspace, les modèles de machine learning sont appelés recettes.

**Attribut obligatoire** : case à cocher activée par l’utilisateur pour s’assurer que tous les enregistrements de profil contiennent l’attribut sélectionné. Par exemple : tous les profils exportés contiennent une adresse e-mail.

**Mappage** : le mappage des données est le processus de mappage des champs de données sources aux champs cibles associés dans une destination.

**Action marketing** : dans le cadre de la gouvernance des données, une action marketing (également appelée cas d’utilisation marketing) est une action entreprise par un utilisateur de données Experience Platform pour laquelle il est nécessaire de vérifier les violations des politiques d’utilisation des données.

**Méthode de fusion** : lors de la définition d’une politique de fusion à l’aide de l’interface utilisateur d’Experience Platform, la méthode de fusion spécifie la priorité des fragments de données en cas de conflit. Lors de l’utilisation de l’API Real-Time Customer Profile pour définir une politique de fusion, la méthode de fusion est déterminée à l’aide de l’objet `attributeMerge`.

**Politique de fusion** : les politiques de fusion sont des règles utilisées par Experience Platform pour déterminer comment des fragments de données client provenant de plusieurs sources seront combinés pour créer un profil individuel. Lorsqu’un conflit de données se produit, la politique de fusion détermine quelles données doivent être prioritaires pour être incluses dans le profil.

**MHMDAa** : la [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true) renforce les droits à la confidentialité des consommateurs concernant leurs données de santé. Elle impose la divulgation, le consentement des consommateurs et les droits de suppression des données de santé, et interdit la vente de données de santé sans autorisation. En outre, la loi interdit l’utilisation de clôtures géologiques autour des établissements de santé.

**Mixin** : voir « Groupe de champs de schéma ».

**Module** : dans le contexte des balises, un module est un extrait de code JavaScript exécutable fourni par une extension, qui effectue des actions dans un environnement client, sans avoir à créer de règle.

## N

**[!DNL New Zealand Privacy Act]** : La [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) contrôle la manière dont les agences peuvent collecter, utiliser, divulguer, stocker et donner accès aux informations personnelles des citoyens et des organisations néo-zélandais. En 2020, la dernière version de la loi a apporté d&#39;importantes mises à jour à ces lois sur la protection des renseignements personnels, notamment de nouvelles infractions, l&#39;augmentation des amendes, l&#39;obligation de signaler les atteintes à la protection des données et l&#39;augmentation des pouvoirs du commissaire à la protection de la vie privée.

**Sandbox hors production** : les sandbox hors production sont des sandbox généralement utilisés pour les expériences de développement, les tests ou les tests. Contrairement aux sandbox de production, les sandbox hors production peuvent être réinitialisés et supprimés.

**[!DNL Notebooks]** : les [!DNL Notebooks] sont créées à l’aide de [!DNL Jupyter Notebook] et peuvent être exécutées pour effectuer une analyse des données.

## O

**Offre** : une offre est un message marketing contenant une proposition commerciale ou de vente à un client (potentiel). Les offres comportent souvent des règles spécifiques qui déterminent qui est éligible pour les voir ou les recevoir.

**[!DNL Offer Decisioning]** : [!DNL Offer Decisioning] permet aux spécialistes marketing de gérer des règles et des modèles formés de propositions d’offres lorsqu’ils interagissent avec les utilisateurs finaux en fonction des données collectées sur les canaux et les applications.

**Bibliothèque des offres** : la bibliothèque des offres est une bibliothèque centrale utilisée pour gérer les offres personnalisées et de secours, les règles de décision et les activités.

**Action marketing de personnalisation sur site** : action marketing qui utilise des données pour la personnalisation de contenu sur site. La personnalisation sur site correspond à toutes les données utilisées pour faire des inférences sur les intérêts des utilisateurs et qui sont utilisées pour sélectionner le contenu ou les annonces diffusés en fonction de ces inférences.

**Action marketing de ciblage sur site** : action marketing qui utilise des données pour les annonces sur site, y compris la sélection et la diffusion des annonces sur les sites web ou les applications de votre organisation, ou pour mesurer la diffusion et l’efficacité de ces annonces.

**Une fois** : dans le contexte des exportations de fichiers planifiées, planifie une exportation de fichiers complets, unique et à la demande.

**Remplacer la stratégie d’enregistrement** : la stratégie d’enregistrement « Remplacer » est une option pour l’ingestion de données tierces via une connexion, où vous pouvez spécifier si les données ingérées seront remplacées selon un planning spécifié.

## P

**Ingestion partielle** : l’ingestion partielle permet d’ingérer des enregistrements valides de données de lots au sein d’un seuil d’erreur spécifié. Les diagnostics d’erreur pour les enregistrements ayant échoué peuvent être téléchargés ou accessibles dans la présentation de l’exécution du flux de données [!UICONTROL Surveillance] ou [!UICONTROL Sources].

**Fichiers Parquet** : un fichier Parquet est un format de fichier de stockage en colonnes avec des structures de données imbriquées complexes. Des fichiers parquet sont nécessaires pour ajouter des données à un jeu de données de schéma.

**PDPA** : la [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) a été introduite pour protéger les propriétaires de données thaïlandais contre la collecte, l&#39;utilisation ou la divulgation illégale de leurs données personnelles. Inspiré du RGPD de l&#39;Union européenne, le règlement accorde aux citoyens thaïlandais le droit de demander l&#39;accès à leurs données personnelles stockées ou leur suppression.

<!-- Not yet released
**PDPD**: The [[!DNL Personal Data Protection Decree] (PDPD) 
-->

**Offres personnalisées** : une offre personnalisée est un message marketing personnalisable, basé sur des règles et des contraintes d&#39;éligibilité.

**Emplacements** : un emplacement est l&#39;endroit ou le contexte dans lequel apparaît une offre pour un utilisateur final.

**Espace de travail des politiques** : espace de travail de l’interface utilisateur d’Experience Platform qui permet aux gestionnaires de données d’afficher et de gérer les libellés et les politiques d’utilisation des données pour votre organisation.

**Politique** : une politique d’utilisation des données est une règle qui spécifie les actions marketing qui sont restreintes en fonction de l’application de libellés d’utilisation appliqués aux données Experience Platform.

**Application des politiques** : permet d’appliquer des politiques d’utilisation des données avec des actions marketing appliquées afin d’empêcher les opérations de données qui constituent des violations de politique au sein d’une organisation.

**clé de Principal** : une clé primaire est une désignation dans un schéma pour identifier de manière unique tous les enregistrements.

**Priorité** : dans [!DNL Offer Decisioning], la priorité est utilisée pour classer les offres répondant à toutes les contraintes comme l&#39;éligibilité, le calendrier et la limitation.

**Graphique d’identités privé** : le graphique d’identités privé (parfois appelé graphique privé) est une carte privée des relations entre les identités assemblées et liées qui est créée en fonction de vos données propriétaires et n’est visible par que votre organisation. Il n’existe qu’un seul graphique privé pour chaque organisation. Il sert de plan directeur structurel pour les graphiques d’identité individuels générés pour chaque client qui interagit avec votre marque.

**Profil de produit** : les profils de produit permettent aux administrateurs d’accorder à l’utilisateur l’accès à l’ensemble ou à un sous-ensemble de services associés à Experience Platform.

**Sandbox de production** : un sandbox de production est un sandbox destiné à être utilisé dans votre environnement de production. Contrairement aux sandbox hors production, les sandbox de production ne peuvent pas être réinitialisés ni supprimés.

**Profil** : à ne pas confondre avec le profil client en temps réel en tant que service, un profil est une représentation complète d’un client individuel, construite à partir d’enregistrements et de séries temporelles fusionnés provenant de plusieurs sources.

**Accès au profil** : le point d’entrée `/entities` de l’API Real-Time Customer Profile vous permet d’accéder aux données d’enregistrement et aux événements de série temporelle dans la banque de données Profile. Voir aussi : Entités de profil

**Données de profil** : les données de profil font référence à toutes les données qui se trouvent dans la banque de données Profil.

**Banque de données de profil** : la banque de données de profil (parfois appelée banque de données de profil) est un système de stockage de données distinct du lac de données, utilisé par le profil client en temps réel pour créer et stocker des profils.

**Entités de profil** : les entités de profil représentent les attributs relatifs à une personne, généralement un client. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la classe [!DNL XDM Individual Profile]. Voir aussi : Accès aux profils

**Exportation de profils** : l’exportation de [!DNL Profile] est l’un des deux types de destinations dans Experience Platform. [!DNL Profile] exportation génère un fichier contenant des profils et des attributs et utilise les données PII brutes avec la messagerie électronique afin de les intégrer aux plateformes de marketing et d&#39;automatisation des courriers électroniques.

**Fragment de profil** : un fragment de profil correspond aux informations de profil d’une seule identité sur la liste des identités qui existent pour un client particulier.

**Identifiant de profil** : un identifiant de profil est un identifiant généré automatiquement et associé à un type d’identité et représente un profil.

**Propriété** : dans le contexte des balises, une propriété est un conteneur pour tout ce qui est nécessaire au déploiement d’un ensemble de balises.

## Q

**Requête** : les requêtes sont des demandes de données provenant de tables de la base de données.

**Query Editor** : le Query Editor est un outil permettant d’écrire, de valider et d’envoyer des instructions SQL dans [!DNL Query Service].

## R

**Real-Time Customer Data Platform** : Adobe Real-Time Customer Data Platform (Real-Time CDP) rassemble des données client connues et inconnues pour créer des profils client de confiance avec une intégration simplifiée, une segmentation intelligente et une activation en temps réel sur le parcours client numérique.

**Real-Time Customer Profile** : le profil client en temps réel (parfois appelé Profil) fournit une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos données client en profils individuels offrant des comptes horodatés et exploitables de chaque interaction client.

**Recette** : une recette est un terme Adobe désignant une spécification de modèle et un conteneur de niveau supérieur représentant des processus de machine learning spécifiques, des algorithmes d’IA, une logique de traitement et des paramètres de configuration requis pour créer et exécuter un modèle formé et ainsi résoudre des problèmes d’entreprise spécifiques.

**Enregistrement** : un enregistrement est une donnée qui persiste sous forme de lignes dans un jeu de données.

**Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.

**Récurrence** : dans [!DNL Query Service], une périodicité définit si une requête doit être exécutée une seule fois ou de manière récurrente.

**Représentation** : dans [!DNL Offer Decisioning], une représentation est une information utilisée par un canal pour afficher une offre, comme la localisation ou la langue.

**Ressource** : dans le contexte des balises, une ressource est un terme générique qui fait référence aux options que l’utilisateur de balises peut configurer dans l’environnement client, y compris les extensions, les éléments de données et les règles.

**Contrôle d’accès en fonction du rôle** : le contrôle d’accès en fonction du rôle permet aux administrateurs d’attribuer des accès et des autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création de sandbox, la définition de schémas et la gestion des jeux de données.

**Règle** : dans le contexte des balises, une règle est un ensemble de composants définissant un ensemble spécifique d’événements, de conditions et d’actions à regrouper logiquement.

**Composant de règle** : dans le contexte des balises, les composants de règle sont les événements, les conditions et les actions qui constituent une règle.

**Runtime** : le runtime spécifie un environnement d’exécution pour une recette de machine learning. Les runtimes [!DNL Python], R, [!DNL Spark], PySpark et Tensorflow vous permettent de saisir une URL vers une image Docker pour une source de recette.

## S

**Données d’exemple** : les données d’exemple sont un aperçu d’un fichier de données, généralement les 100 premières lignes, qui fournit à un spécialiste des données ou à un ingénieur une idée du schéma ou des données dans le fichier de données.

**Sandbox** : un sandbox est une structure virtuelle qui partitionne une instance Experience Platform unique en un environnement virtuel distinct, afin de favoriser le développement et l’évolution d’applications d’expérience digitale.

**Réinitialisation du sandbox** : une réinitialisation du sandbox supprime toutes les données, y compris les données, les profils et les segments, d’un sandbox. Les réinitialisations de sandbox peuvent affecter les données connectées à des destinations internes ou externes.

**Sélecteur de sandbox** : le sélecteur de sandbox d’Experience Platform permet aux utilisateurs de naviguer entre les sandbox auxquels ils ont accès. Le fait de changer de sandbox modifie tout le contenu et peut modifier l’accès aux fonctionnalités en fonction des autorisations.

**Planification** : une planification est une spécification définie par l’utilisateur sur la fréquence ou la cadence d’ingestion des données d’une source de données tierce vers Adobe Experience Platform.

**Notation** : la notation est le processus de génération d’informations à partir de données à l’aide d’un modèle formé.

**Schéma** : un schéma est un ensemble de règles qui représente et valide la structure et le format des données. Un schéma se compose d’une classe et d’un ou de plusieurs groupes de champs facultatifs et est utilisé pour créer des jeux de données et des flux de données. Un schéma peut inclure des attributs comportementaux, des horodatages, des identités, des définitions d’attribut, des relations, etc.

**Groupe de champs de schéma** : dans le modèle de données d’expérience (XDM), un groupe de champs de schéma permet aux utilisateurs d’étendre les champs réutilisables pour définir un ou plusieurs attributs destinés à être inclus dans un schéma.

**Bibliothèque de schémas** : la bibliothèque de schémas contient des ressources XDM standard mises à disposition par Adobe, ainsi que des ressources personnalisées définies par votre organisation.

**Registre des schémas** : le registre des schémas fournit une interface utilisateur et une API RESTful utilisées pour afficher et gérer toutes les ressources liées aux schémas de la bibliothèque des schémas.

**Clé d’accès secrète** : une clé d’accès secrète est une clé S3 [!DNL Amazon] utilisée conjointement avec l’ID de clé d’accès pour signer les requêtes AWS.

**Segment** : un segment est un ensemble de règles qui inclut des attributs et des données d’événement qui qualifient un certain nombre de profils pour devenir une audience.

**Créateur de segments** : le [!DNL Segment Builder] est un environnement de développement visuel utilisé pour créer des définitions de segment. Il sert de composant commun à toutes les applications utilisant Experience Platform Segmentation Service.

**Définition d’un segment** : une définition de segment est l’ensemble de règles utilisé pour décrire les caractéristiques ou le comportement clés d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.

**Méthode d’évaluation de segment** : il existe deux méthodes d’évaluation de segment : planifiée et à la demande. L’évaluation planifiée active une planification récurrente pour exécuter une tâche d’exportation à un moment spécifique, tandis que l’évaluation à la demande implique la création d’une tâche de segmentation pour créer l’audience immédiatement.

**Exportation des segments** : l’exportation de segments est l’un des deux types de destinations dans Experience Platform. Avec l’exportation de segments, vous pouvez envoyer les profils qui remplissent les critères et qui ont été mappés à la destination. Elle utilise les identifiants de segment et d’utilisateur, ainsi que les données pseudonymes, et s’intègre généralement aux réseaux sociaux et aux autres plateformes cible de médias numériques.

**Identifiant de segment** : un identifiant de segment est un identifiant généré automatiquement et associé à un segment.

**Appartenance à un segment** : l’appartenance à un segment affiche le ou les segments dont fait actuellement partie un profil.

**Règles de segment** : les règles de segment définissent les conditions qui déterminent si un profil est admissible pour un segment.

**Segmentation** : la segmentation est le processus de division d’un groupe important de clients, de prospects ou de consommateurs en groupes plus petits qui partagent des attributs similaires et qui réagissent de la même manière à des stratégies marketing spécifiques.

**Sensei ML Framework** : Sensei ML Framework est une structure de machine learning (ML) unifiée qui utilise les données Experience Platform pour permettre aux spécialistes des données de développer des services intelligents pilotés par ML de manière plus rapide, évolutive et réutilisable.

**Libellés sensibles (« S »)** : les libellés sensibles (« S ») sont utilisés pour catégoriser les données considérées comme sensibles, telles que les différents types de données comportementales ou géographiques que vous souhaitez marquer comme sensibles.

**Services** : un cadre puissant pour rendre opérationnels les services d’IA et de ML en utilisant les services intelligents d’Adobe. Services offre des expériences client personnalisées en temps réel ou rendent opérationnels des services intelligents personnalisés.

**Action marketing de personnalisation d’identité unique** : action marketing qui utilise des données pour la personnalisation de contenu sur site. La personnalisation sur site correspond à toutes les données utilisées pour faire des inférences sur les intérêts des utilisateurs et qui servent à sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Libellé d’utilisation des données S1** : un libellé d’utilisation des données `S1` est utilisé pour classer les données spécifiant la latitude et la longitude pouvant être utilisées pour déterminer l’emplacement précis d’un appareil.

Libellé d’utilisation des données **S2** : un libellé d’utilisation des données `S2` est utilisé pour classer les données qui peuvent être utilisées pour déterminer une zone de limite géographique plus large.

**Source** : source est un terme général pour tout connecteur d’entrée dans Experience Platform. Voir aussi : Connecteur Source

**Attribut Source** : un attribut source est un champ dans le jeu de données source. Les attributs sources sont mappés aux champs de schémas sources.

**Catalogue Source** : le catalogue source est la liste des connecteurs source disponibles dans Experience Platform.

**Catégorie Source** : une catégorie de sources est un groupe de sources ayant des caractéristiques similaires.

**Connecteur Source** : les connecteurs Source (également appelés sources) aident les utilisateurs à ingérer facilement des données provenant de plusieurs sources, ce qui permet de structurer, d’étiqueter et d’améliorer les données à l’aide des services Experience Platform. Les données peuvent être ingérées à partir de différentes sources, comme le stockage dans le cloud, les logiciels tiers et les systèmes de gestion de la relation client.

**Connexion en continu** : une connexion en continu est un point d’entrée unique fourni par Adobe et lié à votre organisation pour diffuser des données dans Experience Platform.

**Espace de noms d’identité standard** : les espaces de noms d’identité standard sont des espaces de noms d’identité prédéfinis fournis par Adobe, qui représentent des solutions standard couramment utilisées pour identifier les clients.

**Ingestion par flux** : l’ingestion par flux vous permet d’envoyer en temps réel des données d’appareils côté client et côté serveur vers Experience Platform.

**Segmentation par flux** : la segmentation par flux est un processus continu de sélection des données qui met à jour les segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-Time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

**Vue du système** : la vue du système est une représentation visuelle des jeux de données sources qui transitent par les [!DNL Real-Time Customer Profile] vers les destinations.

## T

**Balises** : dans Adobe Experience Platform, les balises fournissent des outils pour déployer, unifier et gérer les intégrations d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes sur tous les appareils clients.

**Fonctionnalités Target** : dans le mappage de fonctionnalités, une fonctionnalité cible est la fonctionnalité prédite par un modèle.

**Données de série temporelle** : les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un objet d’enregistrement.

**Modèle entraîné** : un modèle entraîné représente la sortie exécutable d’un processus d’entraînement de modèle, dans lequel un ensemble de données d’entraînement a été appliqué à l’instance de modèle. Un modèle formé conserve une référence au service web intelligent qui est créé à partir de celui-ci. Un modèle formé est adapté à la notation et à la création d’un service web intelligent.

**Jeton** : un jeton est un type de sécurité d’authentification à deux facteurs qui peut être utilisé pour autoriser l’utilisation de services informatiques avec [!DNL Query Service].

## U

**UCPA** : la [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) donne au consommateur le droit de savoir quelles données personnelles une entreprise collecte, comment l’entreprise utilise ses données personnelles et si l’entreprise vend ses données personnelles. Les consommateurs peuvent exiger que l&#39;entreprise supprime ou cesse de vendre leurs données personnelles.

**Schéma d’union** : un schéma d’union est une consolidation des schémas qui partagent la même classe et qui ont été activés pour [!DNL Real-Time Customer Profile]. Plusieurs schémas d’union peuvent exister pour une organisation, mais il ne peut y avoir qu’un seul schéma d’union par classe.

## V

**VCDPA** : la [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) fournit de nouveaux droits de confidentialité des données aux résidents de Virginie (« consommateurs »), y compris le droit d’accès, de suppression et de correction des données personnelles. Les consommateurs ont également le droit de refuser la vente de données personnelles, de refuser le profilage basé sur les données personnelles et de refuser le traitement à des fins publicitaires personnelles.

## W

## X

**XDM** : consultez la section Modèle de données d’expérience (XDM).

**Événement de décision XDM** : l’événement de décision XDM est une classe basée sur une série temporelle utilisée pour capturer des observations sur le résultat et le contexte d’une activité de décision. Cela comprend des renseignements sur la façon dont la décision a été prise, le moment où elle a été prise, les options proposées (et choisies) et l&#39;état contextuel qui a influencé la décision ou qui a pu être observé pendant le processus de décision.

**XDM ExperienceEvent** : XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) se produit, y compris le moment et l’identité du titulaire concerné. Voir aussi : Événement d’expérience

**XDM Individual Profile** : XDM [!DNL Individual Profile] est une classe basée sur les enregistrements qui forme une représentation unique des attributs des sujets identifiés et partiellement identifiés.  Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses e-mail.

**Système XDM** : le système XDM représente le framework qui rend les schémas XDM opérationnels pour une utilisation dans les services Experience Platform en aval.

## Y

## Z
