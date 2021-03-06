---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Glossaire Adobe Experience Platform
topic-legacy: getting started
description: Glossaire reprenant la terminologie principale d’Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: c0f01efa224bffb5b435e2f247e793edfbc576b9
workflow-type: tm+mt
source-wordcount: '7428'
ht-degree: 12%

---

# Glossaire Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Contrôle d’accès**: Le contrôle d’accès en fonction du rôle permet aux administrateurs d’attribuer un accès et des autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création d’environnements de test, la définition de schémas et la gestion des jeux de données.

**Accès à l’ID de clé**: Un identifiant de clé d’accès est un identifiant unique associé à un [!DNL Amazon] Clé d’accès secrète S3. L’identifiant de la clé d’accès et la clé d’accès secrète sont utilisés conjointement pour signer. [!DNL Amazon Web Services] (AWS).

**Action**: Dans le contexte des balises, une action est un type spécifique de composant de règle qui définit ce qui doit se produire une fois qu’un événement se produit et que les conditions sont évaluées et transmises.

**Activer**: Activer est l’action effectuée par un utilisateur pour mapper un segment ou des profils à une destination telle que [!DNL Oracle Eloqua], [!DNL Google]ou [!DNL Salesforce Marketing Cloud].

**Activité**: Dans [!DNL Offer Decisioning], une activité contient la logique qui informe la sélection d’une offre.

**Administrateur**: Une ou plusieurs personnes de votre organisation qui peuvent configurer et personnaliser les autorisations d’Experience Platform dans Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console fournit un emplacement central pour la gestion des droits et accès des produits Adobe pour votre entreprise. Grâce à la console, les administrateurs peuvent octroyer à des groupes d’utilisateurs des autorisations d’accès pour diverses fonctionnalités de Platform, telles que &quot;Gérer les jeux de données&quot;, &quot;Afficher les jeux de données&quot; ou &quot;Gérer les profils&quot;.

**Adobe Experience Platform**: Adobe Experience Platform normalise les données et le contenu dans l’ensemble de l’entreprise, optimise les profils clients en temps réel, permet la science des données et accélère la vitesse de diffusion du contenu afin d’orienter la personnalisation de l’expérience sur le parcours client.

**Adobe Experience Platform Query Service**: Permet aux analystes de données d’interroger les événements et les profils en vue de les utiliser dans les analyses et l’apprentissage automatique. Grâce à Query Service, les analystes et analystes de données peuvent extraire tous leurs jeux de données stockés dans Experience Platform (y compris les données comportementales, ainsi que les points de vente, la gestion de la relation client, etc.) et interroger ces jeux de données pour répondre à des questions spécifiques sur les données.

**Adobe Experience Platform Segmentation Service**: Permet la création de segments et la génération d’audiences à partir de vos données Real-time Customer Profile. Ces audiences peuvent ensuite être exportées vers leurs propres jeux de données dans le lac de données.

**Adobe Intelligent Services**: Les services intelligents tels que Attribution AI et Customer AI sont des modèles d’apprentissage automatique basés sur l’intelligence artificielle conçus spécifiquement pour fonctionner et fonctionner avec des Experience Platform.

**Adobe I/O**: Adobe I/O fait partie de l’Experience Platform et permet d’accéder à tout ce dont les développeurs ont besoin pour intégrer, étendre et personnaliser Platform, y compris les API, les événements, la console de développement et des outils utiles.

**Adobe Sensei**: Adobe Sensei est le cadre d’intelligence qui alimente les Experience Platform. Il fournit également un ensemble de services d’IA qui permet aux marques d’améliorer leur capacité à fournir des expériences client personnalisées en temps réel.

**Compartiment Amazon S3**: [!DNL Amazon S3] Les compartiments sont les conteneurs fondamentaux pour les données stockées dans la variable [!DNL Amazon] écosystème. Les compartiments contiennent des objets, chaque objet est stocké et récupéré à l’aide d’une clé unique attribuée par le développeur.

**Connecteur Amazon S3**: Le [!DNL Amazon] Le connecteur S3 permet aux clients d’Experience Platform de se connecter et d’accéder en toute sécurité à leurs [!DNL Amazon] Données S3.

**Ajout d’une stratégie d’enregistrement**: La stratégie d’enregistrement &quot;d’ajout&quot; est une option utilisée lors de la spécification de données tierces à ingérer via une connexion et de l’ajout de nouvelles données ou lignes à la fin du jeu de données. Les lignes précédemment ingérées restent intactes et seules les lignes créées depuis la dernière exécution planifiée sont ingérées dans Experience Platform. Toutes les lignes modifiées dans le système source restent inchangées dans Experience Platform.

**Tableau**: Les tableaux sont utilisés pour les éléments triés avec le même type de données.

**Intelligence artificielle**: L&#39;intelligence artificielle est une théorie et un développement de systèmes informatiques capables d&#39;exécuter des tâches qui nécessitent normalement l&#39;intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction entre les langues.

**Attributs**: Les attributs sont des caractéristiques spécifiées qui représentent un profil.

**Fusion d’attributs**: Lors de la définition d’une stratégie de fusion à l’aide de l’API Real-time Customer Profile, la variable `attributeMerge` indique la manière dont la stratégie de fusion établit la priorité des attributs de profil en cas de conflit de données. Cela équivaut à sélectionner une [!UICONTROL Méthode de fusion] lors de la définition d’une stratégie de fusion dans l’interface utilisateur de Platform.

**Attribution AI**: [!DNL Attribution AI] est un service intelligent optimisé par Adobe Sensei qui offre des fonctionnalités d’attribution algorithmique à plusieurs canaux sur l’ensemble du cycle de vie des clients.

**Audience** : une audience est l’ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

**Taille de l’audience**: Une taille d’audience est le nombre total de profils qui répondent aux critères d’une définition de segment et répondent aux critères de l’appartenance à une audience.

**Instantané d’audience**: Un instantané d’audience capture tous les profils qui remplissent les critères de segment au moment de la segmentation.

## B

**Renvoi**: Pour les sources planifiées, l’option de renvoi active l’ingestion de données historiques.

**Période de renvoi**: La période de renvoi est une option permettant de définir la durée d’ingestion de données historiques tierces via une connexion source. La sélection d’une période de renvoi &quot;indéfiniment&quot; entraîne l’ingestion de l’historique complet des données source à l’Experience Platform.

**Lot**: Un lot est un ensemble de données collectées sur une période donnée et traitées ensemble comme une seule unité. Les jeux de données sont composés de plusieurs lots.

**Identifiant de lot**: Un identifiant de lot est un identifiant généré par l’Adobe pour un lot de données.

**Ingestion par lots**: L’ingestion par lots vous permet d’ingérer des données dans Experience Platform en tant que fichiers de lot. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique.

**Segmentation par lots**: La segmentation par lots est une alternative à un processus continu de sélection de données et déplace toutes les données de profil à la fois via des définitions de segment pour produire les audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin de pouvoir être exporté en vue de son utilisation.

**Build**: Dans le contexte des balises, une version est un fichier ou un ensemble de fichiers qui contient toutes les configurations et le code nécessaires pour exécuter la logique commerciale contenue dans une bibliothèque, ce qui vous permet de déployer cette bibliothèque sur votre site web ou application mobile.

**Outils de Business Intelligence**: Les outils de Business Intelligence (BI) sont principalement intégrés à [!DNL Experience Platform Query Service]. Les outils de BI sont des types de programmes d’application qui collectent et traitent de grandes quantités de données non structurées à partir de systèmes internes et externes.

## C

**Limitation**: Dans [!DNL Offer Decisioning], la limitation (également appelée limitation de fréquence) est utilisée dans les règles de prise de décision pour définir le nombre de fois où une offre est présentée. Il existe deux types de majuscules : le nombre de fois où une offre peut être proposée dans l’audience cible combinée (appelée &quot;limite globale&quot;) et le nombre de fois où une offre peut être proposée au même utilisateur final (appelée &quot;limite de profil&quot;).

**Catalogue**: Dans le contexte des sources et des destinations, un catalogue est une galerie avec des connexions disponibles aux applications d’Adobe et aux technologies tierces. A ne pas confondre avec [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (parfois appelé [!DNL Catalog]) est le système d’enregistrement de l’emplacement et de la traçabilité des données dans Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous la forme de fichiers et de répertoires, [!DNL Catalog] contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche, de surveillance et de gouvernance des données.

**Classe**: Dans le modèle de données d’expérience (XDM), une classe définit le plus petit ensemble de champs utilisé pour créer un schéma et définit le comportement de base de l’objet commercial représenté par le schéma.

**Client**: Un client est un outil ou une application externe qui se connecte à [!DNL Query Service] via le protocole PostgreSQL ou l’API HTTP.

**Collection**: Dans [!DNL Offer Decisioning], les collections sont des sous-ensembles d’offres basés sur des conditions prédéfinies définies par un marketeur, telles que la catégorie de l’offre.

**Combinaison avec une action marketing PII**: Action marketing qui combine toutes les informations d’identification personnelle avec les données anonymes. Les contrats relatifs aux données provenant de réseaux publicitaires, de serveurs de publicités et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données avec des données directement identifiables.

**Interface de ligne de commande**: Une interface de ligne de commande est un outil texte qui peut être utilisé pour se connecter à [!DNL Query Service] pour l’exécution des requêtes brutes.

**Composition** : une composition est un groupe de composants qui se forment ensemble pour constituer le schéma.

**Condition**: Dans le contexte des balises, une condition est un composant de règle qui évalue une instruction logique qui doit renvoyer `true` ou `false`. Toutes les conditions doivent être évaluées sur `true` et toutes les conditions d’exception doivent être évaluées sur `false` avant l’exécution des actions de la règle.

**Console**: Dans [!DNL Query Service], la console fournit des informations sur l’état et le fonctionnement d’une requête. La console affiche l’état de la connexion à [!DNL Query Service], les opérations de requête en cours d’exécution et les messages d’erreur qui en résultent.

**Étiquettes Contrat (&quot;C&quot;)**: Les libellés d’utilisation des données Contrat (&quot;C&quot;) sont utilisés pour classer les données qui ont des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données d’un client.

**Libellé du contrat C1**: A `C1` L’étiquette d’utilisation des données Contrat indique que les données peuvent uniquement être exportées à partir de Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants individuels ou d’appareil. Par exemple, les données provenant des réseaux sociaux.

**Libellé du contrat C2**: A `C2` le libellé d’utilisation des données de contrat indique les données qui ne peuvent pas être exportées vers un tiers. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent l’exportation de données à partir de l’endroit où elles ont été collectées à l’origine. Par exemple, les contrats des réseaux sociaux limitent souvent le transfert des données que vous recevez d’eux. L’étiquette C2 est plus restrictive que la C1, qui ne nécessite que l’agrégation et des données anonymes.

**Libellé du contrat C3**: A `C3` le libellé d’utilisation des données Contrat spécifie les données qui ne peuvent pas être combinées ou utilisées d’une autre manière avec des informations directement identifiables. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent la combinaison ou l’utilisation de ces données avec des informations directement identifiables. Par exemple, les contrats pour les données provenant des réseaux publicitaires, des serveurs de publicités et des fournisseurs de données tiers incluent souvent des interdictions contractuelles spécifiques sur l’utilisation des données directement identifiables.

**Libellé du contrat C4**: A `C4` le libellé d’utilisation des données Contrat indique que les données ne peuvent pas être utilisées pour cibler des publicités ou du contenu, que ce soit sur site ou entre sites. L’étiquette C4 est l’étiquette la plus restrictive puisqu’elle englobe les étiquettes C5, C6 et C7.

**Libellé du contrat C5**: A `C5` le libellé d’utilisation des données Contrat indique que les données ne peuvent pas être utilisées pour le ciblage intersite de contenu ou de publicités en fonction des intérêts. Le ciblage en fonction des intérêts, ou personnalisation, se produit si les trois conditions suivantes sont remplies : Les données collectées sur site sont utilisées pour établir des inférences sur les intérêts d’un utilisateur ; est utilisé dans un autre contexte, par exemple sur un autre site ou une autre application ; et est utilisé pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Libellé du contrat C6**: A `C6` le libellé d’utilisation des données Contrat indique que les données ne peuvent pas être utilisées pour le ciblage des publicités sur site. Le ciblage des publicités sur site inclut la sélection et la diffusion de publicités sur les sites web ou les applications de votre organisation, ou pour mesurer la diffusion et l’efficacité de ces publicités. Cela inclut l’utilisation de données précédemment collectées sur site sur l’intérêt des utilisateurs pour sélectionner des publicités, traiter les données sur les publicités affichées, le moment et le lieu de leur diffusion, et si les utilisateurs ont pris des mesures en rapport avec la publicité, comme sélectionner une publicité ou effectuer un achat.

**Libellé du contrat C7**: A `C7` le libellé d’utilisation des données Contrat indique que les données ne peuvent pas être utilisées pour le ciblage de contenu sur site. Le ciblage de contenu sur site inclut la sélection et la diffusion de contenu sur les sites web ou les applications de votre entreprise, ou pour mesurer la diffusion et l’efficacité de ce contenu. Cela inclut les informations précédemment collectées sur l’intérêt des utilisateurs à sélectionner le contenu, à traiter les données sur le contenu affiché, la fréquence ou la durée de sa diffusion, le moment et le lieu de sa diffusion, et si les utilisateurs ont pris des mesures relatives au contenu, par exemple en sélectionnant le contenu.

**Libellé du contrat C8**: A `C8` le libellé d’utilisation des données Contrat indique que les données ne peuvent pas être utilisées pour mesurer les sites web ou les applications de votre entreprise. Cela ne comprend pas le ciblage basé sur l’intérêt, qui est la collecte d’informations sur votre utilisation de ce service pour personnaliser par la suite le contenu et/ou la publicité dans d’autres contextes.

**Libellé du contrat C9**: A `C9` le libellé d’utilisation des données Contrat indique que les données ne peuvent pas être utilisées dans les workflows de science des données. Certains contrats prévoient des interdictions explicites sur les données utilisées pour la science des données. Parfois, cela fait partie de conditions qui interdisent l’utilisation de données pour l’intelligence artificielle (IA), l’apprentissage automatique ou la modélisation.

**Libellé du contrat C10**: A `C10` le libellé d’utilisation des données Contrat indique que les données ne peuvent pas être utilisées pour l’activation de l’identité groupée. Certaines stratégies dʼutilisation des données limitent lʼutilisation de données dʼidentité assemblées pour la personnalisation. Le `C10` est automatiquement appliquée aux segments si leurs stratégies de fusion utilisent l’option &quot;graphique privé&quot;.

**Colonne Date de création**: La sélection d’une colonne Date de création est une option lors de la spécification de données tierces via une connexion source. Lorsque la stratégie d’enregistrement d’ajout est sélectionnée et que le schéma du jeu de données contient plusieurs champs de date, vous devez choisir parmi le schéma disponible pour spécifier une colonne clé Date de création . L’option Date de création n’est pas disponible lorsque la stratégie d’enregistrement de remplacement est sélectionnée.

**Créer un tableau comme sélection**: Create Table as Select (CTAS) est une commande SQL qui, lorsqu’elle est exécutée dans le cadre d’une requête SQL complète et valide, demande [!DNL Query Service] pour conserver les résultats de la requête dans un jeu de données. Vous pouvez créer un jeu de résultats, remplacer les résultats précédents ou ajouter des résultats précédents.

**Données intersites**: Les données intersites sont une combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site.

**Action marketing de ciblage intersite**: Action marketing qui utilise les données pour le ciblage publicitaire sur plusieurs sites. La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les données intersites sont généralement collectées et traitées afin d’établir des inférences sur les intérêts des clients.

**Espace de noms d’identité personnalisé**: Les espaces de noms d’identité personnalisés peuvent être créés par votre organisation pour représenter les identités d’une organisation ou d’une entreprise spécifique.

**Libellés personnalisés**: Les libellés d’utilisation des données personnalisés vous permettent de créer et d’appliquer des libellés spécifiques à des champs de données qui répondent à des besoins spécifiques de l’entreprise.

**Customer AI**: Customer AI est un service intelligent optimisé par Adobe Sensei qui enrichit les profils clients avec des propensions basées sur l’IA et renforce la segmentation et le ciblage des clients.

## D

**Quotidien**: Dans le cadre d’exportations de fichiers planifiées, planifie des exportations de fichiers complètes ou incrémentielles une fois par jour, tous les jours, de la date de début à la date de fin à l’heure spécifiée par l’utilisateur.

**Dictionnaire de données**: Dans le contexte des balises, un dictionnaire de données (également appelé mappage de données) est un ensemble d’éléments de données définis dans une propriété.

**Élément de données**: Dans le contexte des balises, un élément de données est un pointeur utilisé dans les règles et les extensions pour pointer vers un élément de données spécifique existant sur l’appareil client.

**Ingestion des données**: L’ingestion de données est le processus d’ajout de données d’une source à un Experience Platform. Les données peuvent être ingérées dans Platform de différentes manières, y compris par flux, lots ou ajoutées via des connecteurs source.

**Couche de données**: Dans le contexte des balises, une couche de données est une structure de données qui existe sur le périphérique client et qui contient des métadonnées sur le contexte dans lequel une page ou un écran est affiché.

**Gouvernance des données**: La gouvernance des données englobe les stratégies et les technologies utilisées pour s’assurer que les données sont conformes aux réglementations et aux politiques organisationnelles en matière d’utilisation des données.

**Partenaires d’intégration des données**: Les partenaires d’intégration des données simplifient et automatisent le chargement et la transformation de volumes massifs de données de plus de 200 sources vers Experience Platform sans écrire de code.

**Libellés de jeux de données**: Les libellés d’utilisation des données peuvent être ajoutés aux jeux de données. Tous les champs de ce jeu de données héritent des libellés du jeu de données.

**Data Science Workspace**: [!DNL Data Science Workspace] dans Experience Platform permet aux clients de créer des modèles d’apprentissage automatique à l’aide de données dans les applications Platform et Adobe afin de créer des segments intelligents, de générer des informations et de fournir des prédictions, ce qui vous permet d’améliorer considérablement les expériences numériques de l’utilisateur final.

**Source de données**: Une source de données est un utilisateur désigné comme étant à l’origine de données. Une source de données peut être une application mobile, des événements de profil et/ou d’expérience, des événements de profil de site web ou un système de gestion de la relation client (CRM).

**Gestionnaire de données**: Un gestionnaire de données est la personne responsable de la gestion, de la supervision et de l’application des ressources de données d’une organisation. Un gestionnaire de données veille également à ce que les politiques de gouvernance des données soient préservées et conservées pour être conformes aux réglementations gouvernementales et aux politiques organisationnelles.

**Flux de données**: Un flux de données est un ensemble ou une collection de messages qui partagent le même schéma et sont envoyés par la même source.

**Type de données**: Un type de données est une ressource XDM réutilisable qui définit un champ de type objet contenant plusieurs propriétés dans une représentation hiérarchique.

**Libellés d’utilisation des données**: Les libellés d’utilisation des données vous permettent de classer les données en fonction des considérations liées à la confidentialité et des conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques d’entreprise. Les libellés d’utilisation des données ajoutés à un jeu de données sont hérités ou appliqués à tous les champs de ce jeu de données. Les libellés d’utilisation des données peuvent également être appliqués directement aux champs.

**Flux de données**: Un flux de données est un pipeline virtuel de données qui s’écoule vers Platform à partir d’une source et vers des destinations.

**Exécution du flux de données**: Une exécution de flux de données est un flux de données qui arrive en Experience Platform selon un planning spécifié par l’utilisateur.

**Jeu de données**: Un jeu de données est une structure de stockage et de gestion pour une collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes).

**Identifiant du jeu de données**: Identifiant généré par l’Adobe pour un jeu de données ingéré.

**Sortie de jeu de données**: La sortie du jeu de données fournit un mécanisme permettant de déterminer l’option &quot;Créer un tableau comme sélectionné&quot; qui sera utilisée pour un jeu particulier. [!DNL Query Service] run.

**Clé de déduplication**: Clé Principale définie par l’utilisateur qui détermine l’identité par laquelle les utilisateurs souhaitent dédupliquer leurs profils. &#x200B;

**Colonne delta**: Une colonne delta vous permet de sélectionner un champ de données source pour représenter un horodatage pour l’ingestion incrémentielle.

**Stratégie d’enregistrement delta**: La stratégie d’enregistrement delta est une option permettant d’ingérer des données tierces via une connexion source. Cette option permet à l’utilisateur de spécifier que les lignes de données sources nouvelles ou modifiées sont assimilées à Experience Platform. De nouvelles lignes sont ajoutées à la fin du jeu de données et les lignes modifiées sont mises à jour dans le jeu de données d’Experience Platform.

**Descripteur**: Dans le modèle de données d’expérience (XDM), un descripteur est un jeu supplémentaire de métadonnées liées au schéma qui décrit un comportement spécifique pour un champ. Les descripteurs peuvent être utilisés par l’Experience Platform pour comprendre le comportement prévu des schémas, comme la relation entre deux schémas.

**Destination**: Une destination est un terme général pour tout point de terminaison, tel qu’une application d’Adobe, une plateforme publicitaire, un service de stockage dans le cloud ou un service marketing, où une audience est activée et diffusée.

**Catégorie de destination**: Une catégorie de destination est un groupe de destinations ayant des caractéristiques similaires.

**Catalogue de destinations**: Un catalogue de destinations est une liste des destinations disponibles dans Experience Platform.

**Règles d’appel direct**: Dans le contexte des balises, une règle d’appel direct est une règle qui s’exécute lorsqu’elle est appelée directement à partir de la page, en contournant les systèmes de détection d’événement et de recherche.

**Nom d’affichage**: Dans le modèle de données d’expérience (XDM), un nom d’affichage est un nom convivial pour un champ qui s’affiche dans l’interface utilisateur.

## E

**Offre éligible**: Une offre éligible peut être proposée de manière cohérente à un profil, car elle répond aux contraintes définies en amont.

**Règles d’éligibilité**: Dans [!DNL Offer Decisioning], les règles d’éligibilité sont appliquées à un profil lié aux contraintes de calendrier, de planification et de limitation.

**Action marketing de ciblage des emails**: Action marketing qui utilise les données dans les campagnes de ciblage par e-mail.

**Code incorporé**: Dans le contexte des balises , le code incorporé est une balise de script placée dans le HTML sur un site ou un environnement. Le code incorporé indique au navigateur où récupérer la version.

**Énumération**: Une énumération (énumération) est un champ XDM limité à un ensemble de valeurs prédéfinies.

**Environnement**: Dans le contexte des balises, un environnement est un ensemble d’instructions de déploiement qui spécifie la diffusion hôte et le format de fichier d’une version. Une bibliothèque doit être associée à un environnement avant qu’il puisse être créé.

**Diagnostics d’erreur**: Les diagnostics d’erreur permettent de générer des messages d’erreur détaillés pour les lots ingérés. Le seuil d’erreur permet de configurer le pourcentage d’erreurs acceptables avant l’échec d’un lot.

**Événement**: Dans le contexte des balises, un événement est un type spécifique de composant de règle, qui est un déclencheur qui se produit sur un appareil client pour commencer l’exécution d’une règle.

**Entités d’événement**: Dans le cadre de la modélisation des données, les entités d’événement représentent des concepts liés aux actions qu’un client peut entreprendre, aux événements système ou à tout autre concept sur lequel vous souhaitez peut-être suivre les modifications au fil du temps. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la variable [!DNL XDM ExperienceEvent] classe .

**Événements**: Les événements sont les données de comportement associées à un profil.

**Modèle de données d’expérience (XDM)** [!DNL Experience Data Model] (XDM) est un framework open source qui utilise des schémas standard pour unifier les données en vue de les utiliser avec des applications Experience Platform et Adobe Experience Cloud. XDM normalise la structure des données, et accélère et simplifie le processus d’obtention d’insights à partir d’énormes quantités de données.

**Expérience**: Une expérience est le processus de création d’un modèle formé en formant l’instance avec une portion d’échantillon des données de production en direct. Ceci est différent d’un modèle formé testé par rapport à un jeu de données de test d’exclusion. C&#39;est aussi différent du concept d&#39;expérience dans certains cadres d&#39;apprentissage automatique où cela signifie en fait un exemple de projet de modélisation.

**Événement d’expérience**: Un événement d’expérience représente un instantané du système lorsqu’une interaction ou un événement lié à une expérience client se produit. Les événements d’expérience sont des enregistrements factuels non modifiables de ce qui s’est passé et représentent ce qui s’est passé sans agrégation ni interprétation. Dans le modèle de données d’expérience (XDM), ce concept est capturé par la variable [!DNL XDM ExperienceEvent] classe .

**Exporter le fichier complet**: Un fichier d’exportation contenant un instantané complet de toutes les qualifications de profil pour le segment sélectionné.

**Exportation de fichiers incrémentiels**: Série de fichiers exportés où le premier fichier est un instantané complet de toutes les qualifications de profil pour le segment sélectionné et les fichiers suivants sont des qualifications de profil incrémentielles depuis l’exportation précédente.

**Extension**: Dans le contexte des balises, une extension est un module de fonctionnalités ajouté à une propriété de balise. Une extension est généralement axée sur une solution marketing ou analytique spécifique et fournit les outils nécessaires au déploiement de cette technologie dans un environnement client.

**Package d’extension**: Dans le contexte des balises, un package d’extension est un fichier ZIP créé et téléchargé par un développeur d’extensions qui fournit tout le nécessaire pour que les utilisateurs de balises installent l’extension dans leur propriété. Un package d’extension contient un manifeste spécifiant des informations sur l’extension, le HTML/JavaScript nécessaire pour que les utilisateurs finaux configurent le comportement de l’extension de balise et le code JavaScript exécutable diffusé à l’environnement client (si nécessaire).

## F

**Offres de secours**: Une offre de secours est l’offre par défaut affichée lorsqu’un utilisateur final n’est éligible à aucune des offres de la collection utilisée.

**Mappage des fonctionnalités**: Le mappage des fonctionnalités fait référence au processus de mappage des fonctionnalités des données dans les fonctionnalités d’entrée et de cible requises par un modèle d’apprentissage automatique.

**Champ**: Un champ est l’élément de niveau le plus bas d’un jeu de données, tel que défini par le schéma XDM du jeu de données. Chaque champ a un nom à des fins de référencement et un type pour indiquer le type de données qu’il contient. Les types de champ peuvent inclure (sans s’y limiter) des nombres entiers, des nombres, des chaînes, des valeurs booléennes et des objets.

**Groupe de champs**: Voir &quot;Groupe de champs de schéma&quot;.

**Libellés de champ**: Les libellés de champ sont des libellés de gouvernance des données qui sont soit hérités d’un jeu de données, soit appliqués directement à un champ.

**Nom du champ**: Un nom de champ est utilisé pour référencer la valeur d’un champ dans les requêtes et les services en aval.

**Fréquence**: Dans [!DNL Query Service], la fréquence détermine la fréquence d’exécution d’une requête planifiée récurrente.

## G

**Géofence**: Une géobarrière est une limite géographique virtuelle, définie par la technologie GPS ou RFID, qui permet à un logiciel de déclencher une réponse lorsqu’un appareil mobile entre ou quitte une zone particulière.

**RGPD (Règlement général sur la protection des données)**: Le Règlement général sur la protection des données (RGPD) est un cadre juridique qui définit des lignes directrices pour la collecte et le traitement des informations personnelles des individus au sein de l’Union européenne (UE). Le RGPD énonce les principes de la gestion des données et les droits des individus et couvre toutes les entreprises qui traitent les données des citoyens de l’UE.

**Barrières de sécurité**: Les barrières de sécurité sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform. Les barrières de sécurité peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

## H

**Hôte**: Dans le contexte des balises, un hôte spécifie l’emplacement, le domaine et les informations d’identification d’utilisateur nécessaires pour que le système diffuse une version.

**Horaire**: Dans le contexte des exportations de fichiers planifiées, planifie les exportations incrémentielles de fichiers toutes les 3, 6, 8 ou 12 heures.

## I

**Identité**: Une identité est un identifiant qui représente de manière unique un client individuel, tel qu’un identifiant de cookie, un identifiant d’appareil ou un identifiant de courrier électronique.

**Champs d’identité**: Les champs d’identité sont des champs XDM utilisés pour rassembler des informations sur les clients individuels provenant de plusieurs sources de données. Une seule identité Principale doit être définie pour que le schéma puisse être utilisé dans Real-time Customer Profile.

**Étiquettes Identité (&quot;I&quot;)**: Les libellés d’utilisation des données Identité (&quot;I&quot;) sont utilisés pour classer les données pouvant identifier ou contacter une personne spécifique.

**Graphique d’identités**: Un graphique d’identités est une carte des relations entre les identités associées et liées qui existe pour un client individuel. Chaque graphique d’identités se met à jour en temps quasi réel avec l’activité des clients. La structure commune des relations d’identité dans vos données est représentée par la variable [!UICONTROL Graphique privé], qui sert de plan directeur structurel pour chaque graphique d’identités individuel.

**Espace de noms d’identité**: Un espace de noms d’identité définit le contexte d’un identifiant, tel qu’une adresse électronique ou un identifiant CRM.

**Identity Service**: [!DNL Experience Platform Identity Service] permet la création et la gestion des types d’identité, ce qui vous permet de lier les identités client entre les appareils et les canaux. La capacité du service à lier les identités permet à Real-time Customer Profile de fournir une représentation complète de chaque client.

**Combinaison d’identités**: La combinaison d’identités est le processus d’identification des fragments de données et de regroupement pour former un enregistrement de profil complet.

**Symbole d’identité**: Un symbole d’identité est l’abréviation d’un espace de noms d’identité qui peut être utilisé comme référence dans les API.

**Valeur d’identité**: Une valeur d’identité, combinée à un espace de noms d’identité, est un identifiant qui représente un individu, une organisation ou une ressource unique. Lors de la mise en correspondance des données d’enregistrement entre les fragments de profil, l’espace de noms et la valeur d’identité doivent correspondre.

**Libellé d’utilisation des données I1**: Le `I1` le libellé d’utilisation des données sert à classer les données qui peuvent directement identifier ou contacter une personne spécifique plutôt qu’un appareil.

**Libellé d’utilisation des données I2**: Le `I2` le libellé d’utilisation des données sert à classer les données qui peuvent être utilisées en combinaison avec d’autres données pour identifier ou contacter indirectement une personne spécifique.

**Organisation IMS**: Une organisation IMS (parfois appelée organisation IMS) est le nom utilisé pour identifier une société ou un groupe spécifique au sein d’une société dans les produits Adobe. Les administrateurs peuvent configurer et gérer l’accès et les autorisations des fonctionnalités pour les utilisateurs d’une organisation.

**Ingestion**: Voir Ingestion de données.

**Planification de l’ingestion**: Un planning d’ingestion fournit des options temporelles lors de l’ingestion d’une source vers un Experience Platform.

**Fonctionnalité d’entrée**: Une fonctionnalité d’entrée est spécifiée dans le mappage des fonctionnalités et est utilisée par un modèle d’apprentissage automatique pour faire des prédictions.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] par exemple [!DNL Attribution AI] et [!DNL Customer AI] sont des modèles d’apprentissage automatique basés sur l’intelligence artificielle qui nécessitent des Experience Platform (ou des applications reposant sur Platform telles que Real-time Customer Data Platform) pour fonctionner et fonctionner.

**Ciblage ou personnalisation en fonction des intérêts**: Le ciblage en fonction des intérêts, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies :

1. Les données collectées sur site sont utilisées pour établir des inférences sur les intérêts d’un utilisateur.
1. Les données sont utilisées dans un autre contexte, par exemple sur un autre site ou une autre application (hors site).
1. Les données sont utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

## J

**[!DNL JupyterLab]**: Interface web open source pour Project [!DNL Jupyter] qui est intégré à l’interface utilisateur de Platform.

**[!DNL Jupyter Notebook]**: Intégré à JupyterLab, les notebooks Jupyter vous permettent d’effectuer le nettoyage et la transformation des données, la simulation numérique, la modélisation statistique, la visualisation des données, l’apprentissage automatique, etc. sur vos données Experience Platform dans différentes langues, telles que Python, Scala et PySpark.

## K

## L

**Bibliothèque**: Dans le contexte des balises, une bibliothèque est un ensemble de logiques commerciales qui contient des instructions sur le comportement de la bibliothèque de balises sur l’appareil client.

**Entités de recherche**: Dans le contexte de la modélisation des données, les entités de recherche représentent des concepts qui peuvent être associés à une personne, mais qui ne peuvent pas être directement utilisés pour identifier la personne. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur des classes XDM (Experience Data Model) personnalisées.

## M

**Apprentissage automatique (ML)**: L&#39;apprentissage automatique est le domaine d&#39;étude qui permet aux ordinateurs d&#39;apprendre sans être explicitement programmés.

**Modèle d’apprentissage automatique**: Un modèle d’apprentissage automatique est une instance d’une recette d’apprentissage automatique formée à l’aide de données historiques et de configurations pour résoudre un cas d’utilisation commerciale. Dans Adobe Experience Platform Data Science Workspace, les modèles d’apprentissage automatique sont appelés recettes.

**Attribut obligatoire**: Une case à cocher activée par l’utilisateur qui garantit que tous les enregistrements de profil contiennent l’attribut sélectionné. Par exemple : tous les profils exportés contiennent une adresse email.

**Mappage**: Le mappage des données est le processus de mappage des champs de données sources aux champs cibles associés dans une destination.

**Action marketing**: Dans le cadre de la gouvernance des données, une action marketing (également appelée cas d’utilisation marketing) est une action entreprise par un utilisateur de données Experience Platform, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

**Méthode de fusion**: Lors de la définition d’une stratégie de fusion à l’aide de l’interface utilisateur de Platform, la méthode de fusion spécifie comment les fragments de données doivent être hiérarchisés en cas de conflit. Lors de l’utilisation de l’API Real-time Customer Profile pour définir une stratégie de fusion, la méthode de fusion est déterminée à l’aide de la variable `attributeMerge` .

**Stratégie de fusion**: Les stratégies de fusion sont des règles utilisées par Experience Platform pour déterminer comment les fragments de données client provenant de plusieurs sources seront combinés afin de créer un profil individuel. Lorsqu’un conflit de données se produit, la stratégie de fusion détermine les données qui doivent être incluses en priorité dans le profil.

**Mixin**: Voir &quot;Groupe de champs de schéma&quot;.

**Module**: Dans le contexte des balises, un module est un fragment de code JavaScript exécutable fourni par une extension, qui exécute des actions dans un environnement client sans avoir à créer de règle.

## N

**Environnement de test hors production**: Les environnements de test hors production sont des environnements de test généralement utilisés pour des expériences de développement, des tests ou des tests. Contrairement aux environnements de test de production, les environnements de test hors production peuvent être réinitialisés et supprimés.

**[!DNL Notebooks]**: [!DNL Notebooks] sont créés à l’aide de [!DNL Jupyter Notebook] et peuvent être exécutés pour exécuter l’analyse des données.

## O

**Offre**: Une offre est un message marketing contenant une proposition d’entreprise ou de vente à un client (potentiel). Les offres comportent souvent des règles spécifiques qui déterminent qui peut les voir ou les recevoir.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] permet aux marketeurs de gérer des règles et des modèles formés de propositions d’offre lors de l’interaction avec les utilisateurs finaux en fonction des données collectées sur l’ensemble des canaux et des applications.

**Bibliothèque d’offres**: La bibliothèque d’offres est une bibliothèque centrale utilisée pour gérer les offres personnalisées et de secours, les règles de décision et les activités.

**Action marketing de personnalisation sur site**: Action marketing qui utilise les données pour la personnalisation de contenu sur site. La personnalisation sur site est une donnée utilisée pour établir des inférences sur les intérêts des utilisateurs et pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Action marketing de ciblage sur site**: Action marketing qui utilise les données pour les publicités sur site, y compris la sélection et la diffusion de publicités sur les sites web ou les applications de votre entreprise, ou pour mesurer la diffusion et l’efficacité de ces publicités.

**Une fois**: Dans le contexte des exportations de fichiers planifiées, planifie une exportation de fichiers unique, à la demande et complète.

**Stratégie d’enregistrement de remplacement**: La stratégie d’enregistrement &quot;Overwrite&quot; (Remplacer) est une option permettant d’ingérer des données tierces via une connexion. Vous pouvez y indiquer si les données ingérées seront remplacées selon un calendrier spécifié.

## P

**Ingestion partielle**: L’ingestion partielle permet l’ingestion d’enregistrements valides de données de lot dans un seuil d’erreur spécifié. Les diagnostics d’erreur pour les enregistrements en échec peuvent être téléchargés ou accessibles dans [!UICONTROL Surveillance] ou [!UICONTROL Sources] présentation de l’exécution des flux de données.

**Fichiers parquet**: Un fichier Parquet est un format de fichier de stockage en colonnes avec des structures de données imbriquées complexes. Des fichiers parquet sont nécessaires pour ajouter des données à un jeu de données de schéma.

**Offres personnalisées**: Une offre personnalisée est un message marketing personnalisable basé sur des règles d’éligibilité et des contraintes.

**Emplacements** : un emplacement est l&#39;endroit ou le contexte dans lequel apparaît une offre pour un utilisateur final.

**Espace de travail des stratégies**: Espace de travail de l’interface utilisateur de Platform qui permet aux gestionnaires de données d’afficher et de gérer les libellés et stratégies d’utilisation des données pour votre organisation.

**Stratégie**: Une stratégie d’utilisation des données est une règle qui spécifie les actions marketing qui sont limitées en fonction de l’application des libellés d’utilisation appliqués aux données de Platform.

**Application des stratégies**: Permet d’appliquer des stratégies d’utilisation des données avec des actions marketing appliquées afin d’empêcher les opérations de données qui constituent des violations de stratégie au sein d’une organisation.

**Clé Principal**: Une clé Principale est une désignation dans un schéma pour identifier de manière unique tous les enregistrements.

**Priorité**: Dans [!DNL Offer Decisioning], la priorité est utilisée pour classer les offres qui répondent à toutes les contraintes, telles que l’éligibilité, le calendrier et la limitation.

**Graphique d’identités privé**: Le graphique d’identités privé (parfois appelé graphique privé) est une carte privée des relations entre les identités associées et liées, créée sur la base de vos données propriétaires et visible uniquement par votre organisation. Il n’existe qu’un seul graphique privé pour chaque organisation et sert de plan structurel pour les graphiques d’identités individuels générés pour chaque client qui interagit avec votre marque.

**Profil de produit**: Les profils de produit permettent aux administrateurs d’accorder à l’utilisateur l’accès à l’ensemble ou à un sous-ensemble de services associés à l’Experience Platform.

**Environnement de test de production**: Un environnement de test de production est un environnement de test destiné à être utilisé dans votre environnement de production. Contrairement aux environnements de test hors production, les environnements de test de production ne peuvent pas être réinitialisés ni supprimés.

**Profil**: À ne pas confondre avec Real-time Customer Profile en tant que service, un profil est une représentation complète d’un client individuel, construite à partir de données d’enregistrement fusionnées et de série temporelle provenant de plusieurs sources.

**Accès au profil**: Le `/entities` Le point de terminaison de l’API Real-time Customer Profile vous permet d’accéder aux données d’enregistrement et aux événements de série temporelle dans la banque de données Profile. Voir aussi : Entités de profil

**Données de profil**: Les données de profil font référence à toutes les données qui se trouvent dans la banque de données Profile.

**Entrepôt de données de profil**: La banque de données Profile (parfois appelée banque de données Profile) est un système de stockage de données distinct du lac de données, utilisé par Real-time Customer Profile pour créer et stocker des profils.

**Entités de profil**: Les entités de profil représentent les attributs relatifs à une personne, généralement un client. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la variable [!DNL XDM Individual Profile] classe . Voir aussi : Accès au profil

**Export de profil**: [!DNL Profile] export est l’un des deux types de destinations dans Experience Platform. [!DNL Profile] export génère un fichier contenant des profils et des attributs et utilise des données d’informations d’identification personnelles brutes avec les emails afin de s’intégrer aux plateformes de marketing et d’automatisation des emails.

**Fragment de profil**: Un fragment de profil correspond aux informations de profil d’une seule identité de la liste des identités qui existe pour un client particulier.

**Identifiant de profil**: Un identifiant de profil est un identifiant généré automatiquement, associé à un type d’identité et qui représente un profil.

**Propriété**: Dans le contexte des balises, une propriété est un conteneur pour tout ce qui est nécessaire au déploiement d’un ensemble de balises.

## Q

**Requête**: Les requêtes sont des requêtes de données provenant de tables de base de données.

**Éditeur de requêtes**: Query Editor est un outil permettant d’écrire, de valider et d’envoyer des instructions SQL dans [!DNL Query Service].

## R

**Real-time Customer Data Platform**: [!DNL Real-time Customer Data Platform] rassemble des données clients connues et inconnues afin de créer des profils clients de confiance avec une intégration simplifiée, une segmentation intelligente et une activation en temps réel sur le parcours client numérique.

**Real-time Customer Profile**: Real-time Customer Profile (parfois appelé Profile) offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment en ligne, hors ligne, CRM et tiers. Profile vous permet de consolider vos données client en profils individuels offrant des comptes horodatés exploitables de chaque interaction client.

**Recette**: Une recette est le terme d’Adobe pour une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente des processus d’apprentissage automatique spécifiques, des algorithmes d’IA, une logique de traitement et des paramètres de configuration nécessaires pour créer et exécuter un modèle formé et ainsi aider à résoudre des problèmes d’entreprise spécifiques.

**Enregistrement**: Un enregistrement est une donnée qui persiste sous forme de lignes dans un jeu de données.

**Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.

**Périodicité**: Dans [!DNL Query Service], une périodicité définit si une requête doit être exécutée une seule fois ou de manière récurrente.

**Représentation**: Dans [!DNL Offer Decisioning], une représentation est une information utilisée par un canal pour afficher une offre, comme l’emplacement ou la langue.

**Ressource**: Dans le contexte des balises, une ressource est un terme générique qui fait référence aux options que l’utilisateur peut configurer dans l’environnement client, y compris les extensions, les éléments de données et les règles.

**Contrôle d’accès en fonction du rôle**: Le contrôle d’accès en fonction du rôle permet aux administrateurs d’attribuer un accès et des autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création d’environnements de test, la définition de schémas et la gestion des jeux de données.

**Règle**: Dans le contexte des balises, une règle est un ensemble de composants définissant un ensemble spécifique d’événements, de conditions et d’actions qui doivent être regroupés logiquement.

**Composant de règle**: Dans le contexte des balises, les composants de règle sont les événements, les conditions et les actions qui constituent une règle.

**Exécution**: Runtime spécifie un environnement d’exécution pour une recette d’apprentissage automatique. [!DNL Python], R, [!DNL Spark]Les environnements d’exécution , PySpark et Tensorflow vous permettent de saisir une URL vers une image Docker pour une source de recette.

## S

**Exemples de données**: Les exemples de données sont un aperçu d’un fichier de données, généralement les 100 premières lignes, qui fournit à un spécialiste des données ou à un ingénieur une idée du schéma ou des données qu’il contient.

**Sandbox**: Un environnement de test est une structure virtuelle qui partitionne une instance de Platform unique en un environnement virtuel distinct, afin de favoriser le développement et l’évolution d’applications d’expérience numérique.

**Réinitialisation des environnements de test**: La réinitialisation d’un environnement de test supprime toutes les données, y compris les données, les profils et les segments d’un environnement de test. Les réinitialisations des environnements de test peuvent affecter les données connectées à des destinations internes ou externes.

**Sélecteur d’environnement de test**: Le sélecteur d’environnements de test dans Experience Platform permet aux utilisateurs de naviguer entre les environnements de test auxquels ils ont accès. Le fait de changer d’environnement de test modifie tout le contenu et peut modifier l’accès aux fonctionnalités en fonction des autorisations.

**Planification**: Une planification est une spécification définie par l’utilisateur sur la fréquence ou la cadence d’ingestion des données d’une source de données tierce vers Adobe Experience Platform.

**Notation**: La notation est le processus de génération d’informations à partir de données à l’aide d’un modèle formé.

**Schéma**: Un schéma est un ensemble de règles qui représente et valide la structure et le format des données. Un schéma est constitué d’une classe et d’un ou de plusieurs groupes de champs facultatifs. Il est utilisé pour créer des jeux de données et des flux de données. Un schéma peut inclure des attributs comportementaux, des horodatages, des identités, des définitions d’attributs, des relations, etc.

**Groupe de champs de schéma**: Dans le modèle de données d’expérience (XDM), un groupe de champs de schéma permet aux utilisateurs d’étendre les champs réutilisables pour définir un ou plusieurs attributs destinés à être inclus dans un schéma.

**Bibliothèque de schémas**: La bibliothèque de schémas contient des ressources XDM standard du secteur mises à disposition par Adobe, ainsi que des ressources personnalisées définies par votre organisation.

**Registre des schémas**: Le registre des schémas fournit une interface utilisateur et une API RESTful utilisées pour afficher et gérer toutes les ressources liées aux schémas dans la bibliothèque des schémas.

**Clé d’accès secrète**: Une clé d’accès secrète est une [!DNL Amazon] Clé S3 utilisée conjointement avec l’ID de clé d’accès pour signer les demandes AWS.

**Segment**: Un segment est un ensemble de règles qui incluent des attributs et des données d’événement qui permettent à un certain nombre de profils de devenir une audience.

**Créateur de segments**: Le [!DNL Segment Builder] est un environnement de développement visuel utilisé pour créer des définitions de segment. Il sert de composant commun à toutes les applications utilisant Experience Platform Segmentation Service.

**Définition de segment**: Une définition de segment est le jeu de règles utilisé pour décrire les caractéristiques ou le comportement clés d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.

**Méthode d’évaluation des segments**: Il existe deux méthodes d’évaluation de segment : planifié et à la demande. L’évaluation planifiée active un planning récurrent pour exécuter une tâche d’exportation à un moment spécifique, tandis que l’évaluation sur demande implique la création d’une tâche de segmentation pour créer immédiatement l’audience.

**Exportation de segments**: L’exportation de segments est l’un des deux types de destinations dans Experience Platform. Avec l’exportation de segments, vous pouvez envoyer les profils qui remplissent les critères et qui ont été mappés à la destination. Elle utilise les identifiants de segment et d’utilisateur, ainsi que les données pseudonymes, et s’intègre généralement aux réseaux sociaux et aux autres plateformes cible de médias numériques.

**Identifiant de segment**: Un identifiant de segment est un identifiant généré automatiquement associé à un segment.

**abonnement au segment**: L’adhésion au segment affiche le ou les segments auxquels fait actuellement partie un profil.

**Règles de segment**: Les règles de segment définissent les conditions qui déterminent si un profil est admissible pour un segment.

**Segmentation**: La segmentation consiste à diviser un grand groupe de clients, de prospects ou de consommateurs en groupes plus petits partageant des attributs similaires et réagissant de la même manière à des stratégies marketing spécifiques.

**Structure ML Sensei**: Sensei ML Framework est une structure d’apprentissage automatique unifiée qui tire parti des données Experience Platform pour permettre aux spécialistes des données de développer des services d’intelligence pilotés par ML d’une manière plus rapide, évolutive et réutilisable.

**Étiquettes Sensibles (&quot;S&quot;)**: Les étiquettes Sensibles (&quot;S&quot;) sont utilisées pour classer les données jugées sensibles, par exemple les différents types de données comportementales ou géographiques que vous souhaitez marquer comme sensibles.

**Services**: Un cadre puissant pour rendre opérationnels les services d’intelligence artificielle et d’apprentissage automatique en exploitant les services intelligents d’Adobe. Services offre des expériences client personnalisées en temps réel ou rendent opérationnels des services intelligents personnalisés.

**Action marketing de personnalisation d’identité unique**: Action marketing qui utilise les données pour la personnalisation de contenu sur site. La personnalisation sur site correspond à toutes les données utilisées pour faire des inférences sur les intérêts des utilisateurs et qui servent à sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Libellé d’utilisation des données S1**: Un `S1` le libellé d’utilisation des données sert à classer les données spécifiant la latitude et la longitude qui peuvent être utilisées pour déterminer l’emplacement précis d’un appareil.

**Libellé d’utilisation des données S2**: Un `S2` le libellé d’utilisation des données sert à classer les données qui peuvent être utilisées pour déterminer une zone de géobarrière définie de manière générale.

**Source**: Une source est un terme général pour tout connecteur d’entrée dans Platform. Voir aussi : Connecteur source

**Attribut source**: Un attribut source est un champ du jeu de données source. Les attributs sources sont mappés aux champs de schémas sources.

**Catalogue de sources**: Le catalogue source est la liste des connecteurs source disponibles dans Experience Platform.

**Catégorie de sources**: Une catégorie de sources est un groupe de sources ayant des caractéristiques similaires.

**Connecteur source**: Les connecteurs source (également appelés sources) aident les utilisateurs à ingérer facilement des données provenant de plusieurs sources, ce qui permet de structurer, d’étiqueter et d’améliorer les données à l’aide de services Experience Platform. Les données peuvent être ingérées à partir de différentes sources, comme le stockage dans le cloud, les logiciels tiers et les systèmes de gestion de la relation client.

**Connexion en continu**: Une connexion en continu est un point de terminaison unique fourni par Adobe et lié à l’organisation IMS d’un client pour diffuser des données dans Experience Platform.

**Espace de noms d’identité standard**: Les espaces de noms d’identité standard sont des espaces de noms d’identité prédéfinis fournis par Adobe, qui représentent les solutions standard couramment utilisées pour identifier les clients.

**Ingestion par flux**: L’ingestion par flux vous permet d’envoyer en temps réel des données de périphériques côté client et côté serveur vers Experience Platform.

**Segmentation par flux**: La segmentation par flux est un processus continu de sélection des données qui met à jour les segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

**Vue du système**: La vue système est une représentation visuelle des jeux de données source qui transitent par [!DNL Real-time Customer Profile] vers les destinations.

## T

**Balises**: Dans Adobe Experience Platform, les balises fournissent des outils pour déployer, unifier et gérer les intégrations d’analyse, de marketing et de publicité qui sont nécessaires pour alimenter les expériences client pertinentes sur tous les appareils client.

**Fonctionnalités de Target**: Dans le mappage des fonctionnalités, une fonctionnalité cible est la fonctionnalité prédite par un modèle.

**Données de série temporelle**: Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet enregistré.

**Modèle formé**: Un modèle formé représente la sortie exécutable d’un processus de formation de modèle, dans lequel un ensemble de données d’entraînement a été appliqué à l’instance de modèle. Un modèle formé conserve une référence au service web intelligent qui est créé à partir de celui-ci. Un modèle formé est adapté à la notation et à la création d’un service web intelligent.

**Jeton**: Un jeton est un type de sécurité d’authentification à deux facteurs qui peut être utilisé pour autoriser l’utilisation de services informatiques avec [!DNL Query Service].

## U

**Schéma d’union**: Un schéma d’union est une consolidation des schémas qui partagent la même classe et qui ont été activés pour [!DNL Real-time Customer Profile]. Plusieurs schémas d’union peuvent exister pour une organisation, mais il ne peut y avoir qu’un seul schéma d’union par classe.

## V

## W

## X

**XDM**: Voir Modèle de données d’expérience (XDM).

**Événement de décision XDM**: XDM Decision Event est une classe basée sur une série temporelle utilisée pour recueillir des observations sur le résultat et le contexte d’une activité de décision. Cela comprend des renseignements sur la façon dont la décision a été prise, le moment où elle a eu lieu, les options proposées (et choisies) et l’état contextuel qui a influé sur la décision ou qui a pu être observé pendant le processus de décision.

**XDM ExperienceEvent**: XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) s’est produit, y compris le moment et l’identité du sujet concerné. Voir aussi : Événement d’expérience

**XDM Individual Profile**: XDM [!DNL Individual Profile] est une classe basée sur des enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

**Système XDM**: Le système XDM représente la structure qui rend les schémas XDM opérationnels pour les utiliser dans les services Experience Platform en aval.

## Y

## Z
