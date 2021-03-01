---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Glossaire de Adobe Experience Platform
topic: démarrage
description: Glossaire reprenant la terminologie principale d’Experience Platform.
translation-type: tm+mt
source-git-commit: 5575d5e45bddcc007dcf78720cd7a7e20475f78c
workflow-type: tm+mt
source-wordcount: '7139'
ht-degree: 12%

---


# Glossaire Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Contrôle d&#39;accès** : Le contrôle d&#39;accès basé sur les rôles permet aux administrateurs d’attribuer l’accès et les autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création d’environnements de test, la définition de schémas et la gestion des jeux de données.

**ID** de clé d&#39;accès : Un identifiant de clé d&#39;accès est un identifiant unique associé à une clé d&#39;accès secret  [!DNL Amazon] S3. L’ID de clé d’accès et la clé d’accès secrète sont utilisés conjointement pour signer les demandes [!DNL Amazon Web Services] (AWS).

**Action** : Dans  [!DNL Platform Launch]le cas présent, une action est un type spécifique de composant de règle qui définit ce qui doit se produire une fois qu’un événement s’est produit et que les conditions ont été évaluées et transmises.

**Activer** : Activer est l’action effectuée par un utilisateur pour mapper un segment ou des profils à une destination telle que  [!DNL Oracle Eloqua],  [!DNL Google] ou  [!DNL Salesforce Marketing Cloud].

**Activité** : Dans  [!DNL Offer Decisioning], une activité contient la logique qui sous-tend la sélection d’une offre.

**Administrateur** : Une ou plusieurs personnes de votre organisation qui peuvent configurer et personnaliser les autorisations d’Experience Platform dans Adobe Admin Console.

**Adobe Admin Console** : Adobe Admin Console fournit un emplacement central pour la gestion des droits des produits Adobes et de l’accès pour votre entreprise. Grâce à la console, les administrateurs peuvent accorder à des groupes d’utilisateurs des autorisations d’accès pour diverses fonctionnalités de la plate-forme, telles que &quot;Gérer les jeux de données&quot;, &quot;Jeu de données de Vue&quot; ou &quot;Gérer les Profils&quot;.

**Adobe Experience Platform** : Adobe Experience Platform standardise les données et le contenu dans toute l&#39;entreprise, en optimisant les profils en temps réel pour les consommateurs, en permettant la science des données et en accélérant la vitesse de diffusion du contenu afin d&#39;orienter la personnalisation de l&#39;expérience sur le parcours client.

**Adobe Experience Platform Launch** :  [!DNL Platform Launch] est un écosystème de gestion des balises et des SDK, intégré aux Experience Platform et aux  [!DNL Experience Cloud] applications. [!DNL Platform Launch] fournit des outils permettant de déployer, d’unifier et de gérer les intégrations d’analyse, de marketing et de publicité nécessaires pour alimenter les expériences client pertinentes sur tous les périphériques client.

**Service** de Requête Adobe Experience Platform : Permet aux analystes de données d’accéder aux événements et profils de requête pour les utiliser dans les analyses et l’apprentissage automatique. Avec Requête Service, les analystes et les scientifiques de données peuvent extraire tous leurs jeux de données stockés dans l&#39;Experience Platform (y compris les données comportementales ainsi que les points de vente, la gestion de la relation client, etc.) et les requête pour répondre à des questions spécifiques sur les données.

**Service** de segmentation Adobe Experience Platform : Permet de créer des segments et de générer des audiences à partir de vos données de Profil client en temps réel. Ces audiences peuvent ensuite être exportées vers leurs propres jeux de données dans le lac de données.

**Adobe Intelligent Services** : Les services intelligents tels que l&#39;Attribution AI et l&#39;intelligence artificielle sont des modèles d&#39;apprentissage automatique basés sur l&#39;intelligence artificielle qui sont conçus de manière ciblée et nécessitent l&#39;intervention et le fonctionnement d&#39;un Experience Platform.

**Adobe I/O** : Adobe I/O fait partie de l’Experience Platform et permet aux développeurs d’accéder à tout ce dont ils ont besoin pour intégrer, étendre et personnaliser les plateformes, y compris les API, les événements, la console de développement et des outils utiles.

**Adobe Sensei** : Adobe Sensei est le cadre du renseignement qui donne le pouvoir aux Experience Platform. Il fournit également un ensemble de services d’IA qui permet aux marques d’améliorer leur capacité à fournir des expériences client personnalisées en temps réel.

**compartiment** Amazon S3 :  [!DNL Amazon S3] les compartiments sont les conteneurs fondamentaux des données stockées dans l&#39; [!DNL Amazon] écosystème. Les compartiments contiennent des objets, chaque objet est stocké et récupéré à l’aide d’une clé unique attribuée par le développeur.

**Connecteur** Amazon S3 : Le connecteur  [!DNL Amazon] S3 permet aux clients de l&#39;Experience Platform de se connecter en toute sécurité et d&#39;accéder à leurs données  [!DNL Amazon] S3.

**Ajouter une stratégie** d&#39;enregistrement : La stratégie d’enregistrement &quot;annexer&quot; est une option utilisée lors de la spécification de données tierces à assimiler via une connexion et de l’ajout de nouvelles données ou lignes à la fin du jeu de données. Les lignes précédemment ingérées restent intactes et seules les lignes créées depuis la dernière exécution planifiée sont ingérées dans Experience Platform. Toutes les lignes modifiées dans le système source restent inchangées dans Experience Platform.

**Tableau** : Les tableaux sont utilisés pour les éléments triés avec le même type de données.

**Intelligence** artificielle : L&#39;intelligence artificielle est une théorie et un développement de systèmes informatiques capables d&#39;exécuter des tâches qui nécessitent normalement l&#39;intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction entre les langues.

**Attributs** : Les attributs sont des caractéristiques spécifiées qui représentent un profil.

**Fusion** d&#39;attribut : Lors de la définition d’une stratégie de fusion à l’aide de l’API Profil client en temps réel, l’ `attributeMerge` objet indique la manière dont la stratégie de fusion attribuera la priorité aux attributs de profil en cas de conflit de données. Cela équivaut à sélectionner une [!UICONTROL méthode de fusion] lors de la définition d&#39;une stratégie de fusion dans l&#39;interface utilisateur de la plate-forme.

**Attribution AI** :  [!DNL Attribution AI] est un service intelligent optimisé par Adobe Sensei qui offre des fonctionnalités d’attribution algorithmique multi-canal sur l’ensemble du cycle de vie du client.

**Audience** : une audience est l’ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

**Taille** de l&#39;Audience : Une taille d’audience est le nombre total de profils qui répondent aux critères d’une définition de segment et sont éligibles pour l’adhésion à l’audience.

**Instantané** d&#39;Audience : Un instantané d’audience capture tous les profils qui remplissent les critères de segmentation au moment de la segmentation.

## B

**Renvoi** : Pour les sources planifiées, l’option de renvoi permet l’assimilation de données historiques.

**Période** de renvoi : La période de renvoi est une option permettant de définir la durée d’importation des données historiques tierces via une connexion source. La sélection d’une période de renvoi &quot;indéfiniment&quot; aura pour effet d’assimiler à l’Experience Platform l’historique complet des données source.

**Lot** : Un lot est un ensemble de données collectées sur une période donnée et traitées ensemble en une seule unité. Les jeux de données sont composés de plusieurs lots.

**ID** du lot : Un identifiant de lot est un identifiant généré par Adobe pour un lot de données.

**Importation** par lot : L’assimilation de lots vous permet d’assimiler des données dans l’Experience Platform sous forme de fichiers de lots. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique.

**Segmentation** par lot : La segmentation par lots est une alternative à un processus continu de sélection des données et déplace toutes les données de profil à la fois par le biais de définitions de segment afin de produire les audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin de pouvoir être exporté en vue de son utilisation.

**Créer** : Dans  [!DNL Platform Launch], une compilation est un fichier ou un ensemble de fichiers qui contient toutes les configurations et le code nécessaires à l’exécution de la logique métier contenue dans une bibliothèque, ce qui vous permet de déployer cette bibliothèque sur votre site Web ou dans votre application mobile.

**Outils** de veille économique : Les outils de veille économique sont principalement intégrés à  [!DNL Experience Platform Query Service]. Les outils de BI sont des types de programmes d’application qui collectent et traitent de grandes quantités de données non structurées à partir de systèmes internes et externes.

## C

**Recouvrement** : Dans  [!DNL Offer Decisioning]le cas présent, le plafonnement (également appelé plafonnement de fréquence) est utilisé dans les règles de prise de décision pour définir le nombre de présentations d’une offre. Il existe deux types de majuscules : combien de fois une offre peut être proposée pour l’ensemble de l’audience de cible combinée (appelée &quot;cap global&quot;) et combien de fois une offre peut être proposée au même utilisateur final (appelée &quot;cap de Profil&quot;).

**Catalogue** : Dans le contexte des sources et des destinations, un catalogue est une galerie avec des connexions disponibles aux applications d&#39;Adobe et aux technologies tierces. À ne pas confondre avec [!DNL Catalog Service].

**[!DNL Catalog Service]**:  [!DNL Catalog Service] (parfois appelé  [!DNL Catalog]) est le système d’enregistrement pour l’emplacement et la lignée des données à l’intérieur de Adobe Experience Platform. Bien que toutes les données ingérées dans l&#39;Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, [!DNL Catalog] contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche, de surveillance et de gouvernance des données.

**Classe** : Dans le modèle de données d’expérience (XDM), une classe définit le plus petit ensemble de champs utilisé pour créer un schéma et définit le comportement de base de l’objet métier représenté par le schéma.

**Client** : Un client est un outil ou une application externe qui se connecte à  [!DNL Query Service] via le protocole PostgreSQL ou l&#39;API HTTP.

**Collection** : En  [!DNL Offer Decisioning]effet, les collections sont des sous-ensembles d’offres basés sur des conditions prédéfinies définies par un spécialiste du marketing, telles que la catégorie de l’offre.

**Combiner à l’action** marketing d’identification personnelle : Action marketing qui combine des informations d’identification personnelle (PII) avec des données anonymes. Les contrats portant sur des données provenant de réseaux publicitaires, de serveurs d’annonces et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données à l’aide de données directement identifiables.

**Interface** de ligne de commande : Une interface de ligne de commande est un outil basé sur le texte qui peut être utilisé pour se connecter  [!DNL Query Service] pour exécuter des requêtes brutes.

**Composition** : une composition est un groupe de composants qui se forment ensemble pour constituer le schéma.

**Condition** : Dans  [!DNL Platform Launch]le cas présent, une condition est un composant de règle qui évalue une instruction logique devant renvoyer  `true` ou  `false`être renvoyée. Toutes les conditions doivent être évaluées sur `true` et toutes les conditions d’exception doivent être évaluées sur `false` avant l’exécution des actions de la règle.

**Console** : Dans  [!DNL Query Service], la console fournit des informations sur l’état et le fonctionnement d’une requête. La console affiche l&#39;état de la connexion à [!DNL Query Service], les opérations de requête en cours d&#39;exécution et les messages d&#39;erreur qui en résultent.

**Étiquettes** de contrat (&quot;C&quot;) : Les étiquettes d’utilisation des données de contrat (&quot;C&quot;) sont utilisées pour classer les données qui ont des obligations contractuelles ou qui sont liées aux stratégies de gouvernance des données d’un client.

**Libellé** du contrat C1 : Une étiquette d’utilisation des données de  `C1` contrat spécifie que les données peuvent uniquement être exportées à partir de Adobe Experience Cloud sous une forme agrégée sans inclure d’identifiants de périphérique ou de particulier. Par exemple, les données provenant des réseaux sociaux.

**Libellé** du contrat C2 : Une étiquette d’utilisation des données de  `C2` contrat spécifie les données qui ne peuvent pas être exportées vers un tiers. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent l’exportation de données à partir de l’endroit où elles ont été collectées à l’origine. Par exemple, les contrats des réseaux sociaux limitent souvent le transfert des données que vous recevez d’eux. L’étiquette C2 est plus restrictive que la C1, qui ne nécessite que l’agrégation et des données anonymes.

**Libellé** du contrat C3 : Une étiquette d&#39;utilisation des données de  `C3` contrat spécifie les données qui ne peuvent pas être combinées ou utilisées autrement avec des informations directement identifiables. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent la combinaison ou l’utilisation de ces données avec des informations directement identifiables. Par exemple, les contrats pour les données provenant des réseaux publicitaires, des serveurs de publicités et des fournisseurs de données tiers incluent souvent des interdictions contractuelles spécifiques sur l’utilisation des données directement identifiables.

**Libellé** du contrat C4 : Une étiquette d’utilisation des données de  `C4` contrat spécifie que les données ne peuvent pas être utilisées pour cibler des publicités ou du contenu, sur site ou sur plusieurs sites. L’étiquette C4 est l’étiquette la plus restrictive puisqu’elle englobe les étiquettes C5, C6 et C7.

**Libellé** du contrat C5 : Une étiquette d’utilisation des données de  `C5` contrat spécifie que les données ne peuvent pas être utilisées pour le ciblage intersite du contenu ou des publicités intéressant les sites. Le ciblage basé sur l’intérêt, ou la personnalisation, se produit si les trois conditions suivantes sont remplies : Les données collectées sur le site servent à faire des déductions sur l&#39;intérêt d&#39;un utilisateur ; est utilisé dans un autre contexte, tel que sur un autre site ou une autre application ; et est utilisé pour sélectionner le contenu ou les publicités qui sont diffusés en fonction de ces inférences.

**Libellé** du contrat C6 : Une étiquette d’utilisation des données de  `C6` contrat spécifie que les données ne peuvent pas être utilisées pour le ciblage publicitaire sur site. Le ciblage des publicités sur site comprend la sélection et la diffusion des publicités sur les sites Web ou les applications de votre organisation ou pour mesurer la diffusion et l&#39;efficacité de ces publicités. Cela inclut l’utilisation des données collectées sur site sur l’intérêt des utilisateurs pour sélectionner des publicités, traiter les données sur les publicités affichées, le moment et l’endroit où elles ont été affichées et déterminer si les utilisateurs ont pris des mesures en rapport avec la publicité, comme la sélection d’une publicité ou l’achat.

**Étiquette** de contrat C7 : Une étiquette d’utilisation des données de  `C7` contrat spécifie que les données ne peuvent pas être utilisées pour le ciblage du contenu sur site. Le ciblage du contenu sur site comprend la sélection et la diffusion de contenu sur les sites Web ou les applications de votre entreprise ou pour mesurer la diffusion et l’efficacité de ce contenu. Cela inclut les informations collectées précédemment sur l’intérêt des utilisateurs pour la sélection du contenu, le traitement des données sur le contenu affiché, la fréquence ou la durée d’affichage, le moment et l’emplacement d’affichage, ainsi que sur l’action des utilisateurs concernant le contenu, notamment la sélection du contenu.

**Étiquette** de contrat C8 : Une étiquette d’utilisation des données de  `C8` contrat indique que les données ne peuvent pas être utilisées pour mesurer les sites Web ou les applications de votre entreprise. Cela ne comprend pas le ciblage basé sur l’intérêt, qui est la collecte d’informations sur votre utilisation de ce service pour personnaliser par la suite le contenu et/ou la publicité dans d’autres contextes.

**Libellé** du contrat C9 : Une étiquette d&#39;utilisation des données  `C9` de contrat spécifie que les données ne peuvent pas être utilisées dans les workflows de données scientifiques. Certains contrats prévoient des interdictions explicites sur les données utilisées pour la science des données. Parfois, cela fait partie de conditions qui interdisent l’utilisation de données pour l’intelligence artificielle (IA), l’apprentissage automatique ou la modélisation.

**Libellé** du contrat C10 : Une étiquette d&#39;utilisation des données de  `C10` contrat spécifie que les données ne peuvent pas être utilisées pour l&#39;activation d&#39;identité assemblée. Certaines stratégies d’utilisation des données limitent l’utilisation de données d’identité assemblées pour la personnalisation. L&#39;étiquette `C10` est automatiquement appliquée aux segments si leurs stratégies de fusion utilisent l&#39;option &quot;graphique privé&quot;.

**Colonne** Date de création : La sélection d’une colonne Date de création est une option lors de la spécification de données tierces via une connexion source. Lorsque la stratégie d’enregistrement d’ajout est sélectionnée et que le schéma de jeu de données contient plusieurs champs de date, vous devez choisir l’un des schémas disponibles pour spécifier une colonne de clé Date de création. L’option Date de création n’est pas disponible lorsque la stratégie d’enregistrement de remplacement est sélectionnée.

**Créer un tableau comme sélection** : Create Table as Select (CTAS) est une commande SQL qui, lorsqu&#39;elle est exécutée dans le cadre d&#39;une requête SQL complète et valide, demande  [!DNL Query Service] de conserver les résultats de la requête dans un jeu de données. Vous pouvez créer un jeu de résultats, remplacer les résultats précédents ou ajouter des résultats précédents.

**Données** intersites : Les données intersites sont la combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site.

**Action** marketing de ciblage sur plusieurs sites : Action marketing qui utilise les données pour le ciblage publicitaire sur plusieurs sites. La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les données intersites sont généralement collectées et traitées pour faire des inférences sur les intérêts des clients.

**Espace de nommage** d&#39;identité personnalisée : Des espaces de nommage d&#39;identité personnalisés peuvent être créés par votre organisation pour représenter les identités d&#39;une organisation ou d&#39;une entreprise spécifique.

**Libellés** personnalisés : Les étiquettes d’utilisation de données personnalisées vous permettent de créer et d’appliquer des étiquettes spécifiques aux champs de données qui répondent à des besoins spécifiques de l’entreprise.

**AI** du client : L’IA client est un service intelligent optimisé par Adobe Sensei qui enrichit les profils clients avec des propensions basées sur l’IA et permet la segmentation et le ciblage des clients.

## D

**Dictionnaire** de données : Dans  [!DNL Platform Launch]le cas d’un dictionnaire de données (également appelé mappage de données), il s’agit d’un ensemble d’éléments de données définis dans une propriété.

**Élément** de données : Dans  [!DNL Platform Launch]le cas présent, un élément de données est un pointeur utilisé dans les règles et extensions pour pointer vers un élément de données spécifique existant sur le périphérique client.

**Extraction** de données : L&#39;assimilation de données est le processus d&#39;ajout de données d&#39;une source à un Experience Platform. Les données peuvent être ingérées dans la plate-forme de différentes manières, y compris la diffusion en continu, les lots ou ajoutées via des connecteurs source.

**Calque** de données : Dans  [!DNL Platform Launch]le cas présent, une couche de données est une structure de données qui existe sur le périphérique client et qui contient des métadonnées sur le contexte dans lequel une page ou un écran est affiché.

**Gouvernance** des données : La gouvernance des données englobe les stratégies et les technologies utilisées pour s&#39;assurer que les données sont conformes aux règlements et aux politiques organisationnelles en matière d&#39;utilisation des données.

**Partenaires** d&#39;intégration des données : Les partenaires d&#39;intégration de données simplifient et automatisent le chargement et la transformation de volumes massifs de données de plus de 200 sources vers l&#39;Experience Platform sans écrire de code.

**Libellés** des jeux de données : Les étiquettes d’utilisation des données peuvent être ajoutées aux jeux de données. Tous les champs de ce jeu de données héritent des libellés du jeu de données.

**Espace de travail** des sciences de données :  [!DNL Data Science Workspace] dans Experience Platform permet aux clients de créer des modèles d’apprentissage automatique à l’aide de données dans les applications de plateforme et d’Adobe afin de créer des segments intelligents, de générer des aperçus et de fournir des prédictions, ce qui vous permet d’améliorer considérablement les expériences numériques des utilisateurs finaux.

**Source** de données : Une source de données est une origine de données désignée par l’utilisateur. Par exemple, une source de données est une application mobile, un événement de profil et/ou d’expérience, un événement de profil de site Web ou un service de gestion de la relation client.

**Responsable** de données : Le responsable de la gestion, de la surveillance et de l&#39;application des ressources de données d&#39;une organisation est le responsable de l&#39;intendance des données. Un gestionnaire de données veille également à ce que les politiques de gouvernance des données soient préservées et maintenues pour être conformes aux règlements et aux politiques organisationnelles du gouvernement.

**Flux** de données : Un flux de données est un ensemble ou un ensemble de messages qui partagent le même schéma et sont envoyés par la même source.

**Type** de données : Un type de données est une ressource XDM réutilisable qui définit un champ de type objet contenant plusieurs propriétés dans une représentation hiérarchique.

**Étiquettes** d&#39;utilisation des données : Les étiquettes d’utilisation des données vous permettent de classer les données qui reflètent les considérations liées à la vie privée et les conditions contractuelles afin de les rendre conformes aux réglementations et aux stratégies de l’entreprise. Les étiquettes d’utilisation des données ajoutées à un jeu de données sont héritées ou appliquées à tous les champs de ce jeu de données. Les étiquettes d’utilisation des données peuvent également être appliquées directement aux champs.

**Flux** de données : Un flux de données est un pipeline virtuel de données qui s’écoule vers la plate-forme à partir d’une source et vers des destinations.

**Flux de données exécuté** : Une exécution de flux de données est un flux de données qui arrive dans l’Experience Platform en fonction d’un calendrier défini par l’utilisateur.

**Jeu de données** : Un jeu de données est un concept d&#39;enregistrement et de gestion pour une collection de données, généralement un tableau, qui contient un schéma (colonnes) et des champs (lignes).

**ID** du jeu de données : Identificateur généré par l’Adobe pour un jeu de données assimilé.

**Sortie** du jeu de données : La sortie des jeux de données fournit un mécanisme permettant de déterminer l&#39;option &quot;Créer une table comme sélection&quot; qui sera utilisée pour une  [!DNL Query Service] exécution particulière.

**Colonne** Delta : Une colonne delta vous permet de sélectionner un champ de données source pour représenter un horodatage pour l’assimilation incrémentielle.

**Stratégie** d&#39;enregistrement Delta : La stratégie d’enregistrement delta est une option permettant d’ingérer des données tierces via une connexion source. Cette option permet à l’utilisateur de spécifier que les lignes de données sources nouvelles ou modifiées sont assimilées à Experience Platform. De nouvelles lignes sont ajoutées à la fin du jeu de données et les lignes modifiées sont mises à jour dans le jeu de données d’Experience Platform.

**Descripteur** : Dans le modèle de données d’expérience (XDM), un descripteur est un ensemble supplémentaire de métadonnées liées au schéma qui décrit un comportement spécifique pour un champ. Les descripteurs peuvent être utilisés par les Experience Platform pour comprendre le comportement prévu du schéma, tel que la relation entre deux schémas.

**Destination** : Une destination est un terme général désignant tout point de terminaison, tel qu’une application d’Adobe, une plateforme publicitaire, un service d’enregistrement cloud ou un service marketing, où une audience est activée et diffusée.

**Catégorie** de destination : Une catégorie de destination est un regroupement de destinations ayant des caractéristiques similaires.

**Catalogue** de destination : Un catalogue de destination est une liste de destinations disponibles dans l’Experience Platform.

**Règles** d&#39;appel direct : En  [!DNL Platform Launch]effet, une règle d’appel direct est une règle qui s’exécute lorsqu’elle est appelée directement à partir de la page, en contournant les systèmes de détection et de recherche de événement.

**Nom** d&#39;affichage : Dans le modèle de données d’expérience (XDM), un nom d’affichage est un nom convivial pour un champ affiché dans l’interface utilisateur.

## E

**Offre** éligible : Une offre éligible peut être proposée de façon cohérente à un profil, car elle répond aux contraintes définies en amont.

**Règles d&#39;éligibilité** : Dans  [!DNL Offer Decisioning], les règles d&#39;éligibilité sont appliquées à un profil lié aux contraintes de calendrier, de planification et de plafonnement.

**Action** marketing de ciblage des e-mails : Action marketing qui utilise les données dans les campagnes de ciblage par courriel.

**Incorporer le code** : Dans  [!DNL Platform Launch]le cas présent, le code incorporé est une balise de script placée dans le code HTML sur un site ou un environnement. Le code incorporé indique au navigateur où récupérer la version.

**Énumération** : Une énumération (enum) est un champ XDM limité à un ensemble de valeurs prédéfinies.

**Environnement** : Dans  [!DNL Platform Launch], un environnement est un ensemble d&#39;instructions de déploiement qui spécifie la diffusion hôte et le format de fichier d&#39;une build. Une bibliothèque doit être associée à un environnement avant qu’il puisse être créé.

**Diagnostics** d&#39;erreur : Les diagnostics d’erreur permettent de générer des messages d’erreur détaillés pour les lots assimilés. Le seuil d&#39;erreur permet de configurer le pourcentage d&#39;erreurs acceptables avant l&#39;échec d&#39;un lot.

**Événement** : Dans  [!DNL Platform Launch]le cas d’un événement, il s’agit d’un type spécifique de composant de règle, qui est un déclencheur qui se produit sur un périphérique client pour commencer l’exécution d’une règle.

**Entités** de événement : Dans le cadre de la modélisation des données, les entités de événement représentent des concepts liés aux actions qu’un client peut entreprendre, aux événements système ou à tout autre concept dans lequel vous pouvez suivre les modifications au fil du temps. Les entités qui relèvent de cette catégorie doivent être représentées par des schémas basés sur la classe [!DNL XDM ExperienceEvent].

**Événements** : Les événements sont les données de comportement associées à un profil.

**Le modèle de données d’expérience (XDM)** [!DNL Experience Data Model]  (XDM) est une structure open source qui utilise des schémas standard pour unifier les données à utiliser avec les applications Experience Platform et Adobe Experience Cloud. XDM normalise la structure des données, et accélère et simplifie le processus d’obtention d’insights à partir d’énormes quantités de données.

**Expérience** : Une expérience est le processus de création d’un modèle entraîné en formant l’instance avec une portion d’échantillon des données de production en direct. Ceci est différent d’un modèle formé testé par rapport à un jeu de données de test d’exclusion. Ceci est également différent du concept d&#39;expérience dans certains cadres d&#39;apprentissage automatique où cela signifie en fait un projet de modélisation d&#39;exemple.

**Événement** d’expérience : Un Événement d’expérience représente un instantané du système lorsqu’une interaction ou un événement lié à une expérience client se produit. Les Événements d&#39;expérience sont des données factuelles immuables de ce qui s&#39;est passé et représentent ce qui s&#39;est passé sans agrégation ni interprétation. Dans le modèle de données d’expérience (XDM), ce concept est capturé par la classe [!DNL XDM ExperienceEvent].

**Extension** : Dans  [!DNL Platform Launch]le cas présent, une extension est un package de fonctionnalités ajouté à une  [!DNL Platform Launch] propriété. Une extension est généralement axée sur une solution marketing ou analytique spécifique et fournit les outils nécessaires au déploiement de cette technologie dans un environnement client.

**Package** d&#39;extension : Dans  [!DNL Platform Launch]un paquet d&#39;extension est un fichier ZIP créé et téléchargé par un développeur d&#39;extension qui fournit tout ce dont  [!DNL Platform Launch] les utilisateurs ont besoin pour installer l&#39;extension dans leur propriété. Un package d&#39;extension contient un manifeste spécifiant des informations sur l&#39;extension, le code HTML/JavaScript nécessaire pour que les utilisateurs finaux puissent configurer le comportement de l&#39;extension [!DNL Platform Launch] et le code JavaScript exécutable livré à l&#39;environnement client (si nécessaire).

## F

**Offres** de secours : Une offre de secours est l’offre par défaut affichée lorsqu’un utilisateur final n’est éligible à aucune des offres de la collection utilisée.

**Mappage** des fonctionnalités : La mise en correspondance des fonctionnalités fait référence au processus de mise en correspondance des fonctionnalités des données dans les fonctions d’entrée et de cible requises par un modèle d’apprentissage automatique.

**Champ** : Un champ est l&#39;élément de niveau le plus bas d&#39;un jeu de données, tel que défini par le schéma XDM du jeu de données. Chaque champ a un nom à des fins de référence et un type pour indiquer le type de données qu’il contient. Les types de champ peuvent inclure (sans s’y limiter) des entiers, des nombres, des chaînes, des booléens et des objets.

**Libellés** des champs : Les libellés de champ sont des libellés de gouvernance des données hérités d’un jeu de données ou appliqués directement à un champ.

**Nom** du champ : Un nom de champ est utilisé pour référencer la valeur d’un champ dans les requêtes et les services en aval.

**Fréquence** : Dans  [!DNL Query Service]le cas présent, la fréquence détermine la fréquence d’exécution d’une requête planifiée périodique.

## G

**Géofence** : Une géofence est une limite géographique virtuelle, définie par un GPS ou la technologie RFID, qui permet au logiciel de déclencher une réponse lorsqu&#39;un dispositif portable entre dans une zone particulière ou en sort.

**RGPD (Règlement général sur la protection des données)** : Le règlement général sur la protection des données (RGPD) est un cadre juridique qui établit des lignes directrices pour la collecte et le traitement des informations à caractère personnel des personnes au sein de l&#39;Union européenne (UE). Le RGPD énonce les principes de la gestion des données et les droits des individus et couvre toutes les entreprises qui traitent les données des citoyens de l’UE.

## H

**Hôte** : Dans  [!DNL Platform Launch], un hôte spécifie l’emplacement, le domaine et les informations d’identification d’utilisateur nécessaires  [!DNL Platform Launch] à la diffusion d’une compilation.

## I

**Identité** : Une identité est un identifiant qui représente de manière unique un client individuel, tel qu’un ID de cookie, un ID d’appareil ou un ID d’adresse électronique.

**Champs** d&#39;identité : Les champs d’identité sont des champs XDM qui sont utilisés pour rassembler des informations sur les clients individuels provenant de plusieurs sources de données. Une identité Principale unique doit être définie pour que le schéma soit activé pour une utilisation dans le Profil client en temps réel.

**Étiquettes** d&#39;identité (&quot;I&quot;) : Les étiquettes d’utilisation des données d’identité (&quot;I&quot;) sont utilisées pour classer les données qui peuvent identifier ou contacter une personne spécifique.

**Graphique** d&#39;identité : Un graphique d&#39;identité est une carte des relations entre les identités recoupées et liées qui existent pour un client individuel. Chaque graphique d&#39;identité est mis à jour en temps quasi réel avec l&#39;activité du client. La structure commune des relations d&#39;identité dans vos données est représentée par le [!UICONTROL Graphique privé], qui sert de modèle structurel pour chaque graphique d&#39;identité individuel.

**Espace de nommage** d&#39;identité : Un espace de nommage d’identité définit le contexte d’un identifiant tel qu’une adresse électronique ou un identifiant de gestion de la relation client.

**Service** d&#39;identité :  [!DNL Experience Platform Identity Service] permet la création et la gestion de types d&#39;identité, ce qui vous permet de lier les identités des clients entre différents périphériques et canaux. La capacité du service à lier les identités permet au Profil client en temps réel de fournir une représentation complète de chaque client.

**Correspondance** d&#39;identité : L’assemblage d’identité est le processus d’identification des fragments de données et de les assembler pour former un enregistrement de profil complet.

**Symbole** d&#39;identité : Un symbole d&#39;identité est l&#39;abréviation d&#39;un espace de nommage d&#39;identité qui peut être utilisé comme référence dans les API.

**Valeur** d&#39;identité : Une valeur d&#39;identité, combinée à un espace de nommage d&#39;identité, est un identifiant qui représente un individu, une organisation ou une ressource unique. Lors de la correspondance de données d’enregistrement entre des fragments de profil, l’espace de nommage et la valeur d’identité doivent correspondre.

**Libellé** d&#39;utilisation des données I1 : Le libellé d’utilisation des  `I1` données permet de classer les données qui peuvent directement identifier ou contacter une personne spécifique plutôt qu’un périphérique.

**Libellé** d&#39;utilisation des données I2 : L’étiquette d’utilisation des  `I2` données sert à classifier les données qui peuvent être utilisées en combinaison avec d’autres données pour identifier indirectement ou contacter une personne spécifique.

**Organisation** IMS : Une organisation IMS (parfois appelée organisation IMS) est le nom utilisé pour identifier une société ou un groupe spécifique au sein d&#39;une société entre des produits Adobes. Les administrateurs peuvent configurer et gérer l’accès et les autorisations des fonctions pour les utilisateurs d’une organisation.

**Ingestion** : Voir assimilation de données.

**Calendrier** d&#39;importation : Un calendrier d’assimilation fournit des options temporelles lors de l’assimilation d’une source à un Experience Platform.

**Fonction** d&#39;entrée : Une fonction d’entrée est spécifiée dans le mappage des fonctionnalités et est utilisée par un modèle d’apprentissage automatique pour faire des prédictions.

**[!DNL Intelligent Services]**:  [!DNL Intelligent Services] tels que  [!DNL Attribution AI] et  [!DNL Customer AI] sont des modèles d&#39;apprentissage automatique basés sur l&#39;intelligence artificielle qui nécessitent l&#39;exécution et le fonctionnement d&#39;Experience Platform (ou d&#39;applications créées sur la plate-forme de données client en temps réel, par exemple).

**Ciblage ou personnalisation** axé sur l’intérêt : Le ciblage basé sur l’intérêt, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies :

1. Les données collectées sur site servent à faire des déductions sur l’intérêt d’un utilisateur.
1. Les données sont utilisées dans un autre contexte, tel que sur un autre site ou une autre application (hors site).
1. Les données permettent de sélectionner le contenu ou les publicités qui sont diffusés en fonction de ces inférences.

## J

**[!DNL JupyterLab]**: Interface Web open source pour Project  [!DNL Jupyter] qui est intégrée dans l’interface utilisateur de la plate-forme.

**[!DNL Jupyter Notebook]**: Intégrés à JupyterLab, les portables Jupyter vous permettent d&#39;effectuer le nettoyage et la transformation des données, la simulation numérique, la modélisation statistique, la visualisation des données, l&#39;apprentissage automatique et plus encore sur vos données Experience Platform dans divers langages tels que Python, Scala et PySpark.

## K

## L

**Bibliothèque** : Dans  [!DNL Platform Launch]une bibliothèque est un ensemble de logiques métier qui contient des instructions sur le comportement de la  [!DNL Platform Launch] bibliothèque sur le périphérique client.

**Entités** de recherche : Dans le contexte de la modélisation des données, les entités de recherche représentent des concepts qui peuvent être liés à une personne, mais qui ne peuvent pas être directement utilisés pour identifier l&#39;individu. Les entités qui relèvent de cette catégorie doivent être représentées par des schémas basés sur des classes XDM (Experience Data Model) personnalisées.

## M

**Apprentissage automatique (ML)** : L&#39;apprentissage automatique est le domaine d&#39;étude qui permet aux ordinateurs d&#39;apprendre sans être explicitement programmés.

**Modèle** d&#39;apprentissage automatique : Un modèle d’apprentissage automatique est l’instance d’une recette d’apprentissage automatique qui est formée à l’aide de données historiques et de configurations pour résoudre un cas d’utilisation commerciale. Dans Adobe Experience Platform Data Science Workspace, les modèles d&#39;apprentissage automatique sont appelés des recettes.

**Mappage** : Le mappage des données est le processus de mappage des champs de données source aux champs de cible associés dans une destination.

**Action** marketing : Dans le cadre de la gouvernance des données, une action marketing (également appelée cas d’utilisation marketing) est une action entreprise par un utilisateur de données Experience Platform, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

**Méthode** de fusion : Lors de la définition d’une stratégie de fusion à l’aide de l’interface utilisateur de la plate-forme, la méthode de fusion spécifie comment les fragments de données doivent être classés par priorité en cas de conflit. Lorsque vous utilisez l&#39;API Profil client en temps réel pour définir une stratégie de fusion, la méthode de fusion est déterminée à l&#39;aide de l&#39;objet `attributeMerge`.

**Fusionner la stratégie** : Les stratégies de fusion sont des règles que l’Experience Platform utilise pour déterminer comment les fragments de données client provenant de plusieurs sources seront combinés afin de créer un profil individuel. Lorsqu’un conflit de données se produit, la stratégie de fusion détermine quelles données doivent être prioritaires pour l’inclusion dans le profil.

**Mixin** : Dans le modèle de données d’expérience (XDM), un mixin permet aux utilisateurs d’étendre les champs réutilisables pour définir un ou plusieurs attributs destinés à être inclus dans un schéma.

**Module** : Dans  [!DNL Platform Launch], un module est un fragment de code JavaScript exécutable fourni par une extension, qui exécute des actions dans un environnement client sans avoir à créer de règle.

## N

**Sandbox** de non-production : Les sandbox hors production sont généralement utilisés pour des expériences de développement, des tests ou des essais. Contrairement aux sandbox de production, les sandbox hors production peuvent être réinitialisés et supprimés.

**[!DNL Notebooks]**:  [!DNL Notebooks] sont créées à l’aide  [!DNL Jupyter Notebook] et peuvent être exécutées pour effectuer l’analyse des données.

## O

**Offre** : Une offre est un message marketing contenant une proposition commerciale ou commerciale à un client (potentiel). Les Offres ont souvent des règles spécifiques qui déterminent qui peut les voir ou les recevoir.

**[!DNL Offer Decisioning]**:  [!DNL Offer Decisioning] permet aux spécialistes du marketing de gérer les règles et les modèles de Propositions d&#39;offre formés lors de l’interaction avec les utilisateurs finaux en fonction des données collectées sur plusieurs canaux et applications.

**Bibliothèque** d&#39;Offres : La bibliothèque d’offres est une bibliothèque centrale utilisée pour gérer les offres personnalisées et de secours, les règles de décision et les activités.

**Action** marketing de personnalisation sur site : Action marketing qui utilise les données pour la personnalisation du contenu sur site. La personnalisation sur site est toute donnée utilisée pour faire des inférences sur les intérêts des utilisateurs et sert à sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

**Action** marketing de ciblage sur site : Action marketing qui utilise des données pour les publicités sur site, y compris la sélection et la diffusion des publicités sur les sites Web ou les applications de votre entreprise, ou pour mesurer la diffusion et l’efficacité de ces publicités.

**Remplacer la stratégie** d&#39;enregistrement : La stratégie d’enregistrement &quot;Remplacer&quot; est une option permettant d’ingérer des données tierces via une connexion, où vous pouvez spécifier si les données imbriquées seront remplacées selon un calendrier spécifié.

## P

**Importation** partielle : L&#39;assimilation partielle permet l&#39;assimilation d&#39;enregistrements valides de données de lot dans un seuil d&#39;erreur spécifié. Les diagnostics d&#39;erreur pour les enregistrements en échec peuvent être téléchargés ou accessibles dans [!UICONTROL Surveillance] ou [!UICONTROL Sources] aperçu de l&#39;exécution des flux de données.

**Dossiers** de parquets : Un fichier Parquet est un format de fichier d&#39;enregistrement à colonnes avec des structures de données imbriquées complexes. Des fichiers parquet sont nécessaires pour ajouter des données à un jeu de données de schéma.

**Offres** personnalisées : Une offre personnalisée est un message marketing personnalisable basé sur des règles d&#39;éligibilité et des contraintes.

**Emplacements** : un emplacement est l’endroit ou le contexte dans lequel apparaît une offre pour un utilisateur final.

**Espace de travail** Stratégies : Espace de travail dans l’interface utilisateur de la plate-forme qui permet aux responsables de la gestion des données de vue et de gérer les étiquettes et les stratégies d’utilisation des données pour votre entreprise.

**Stratégie** : Une stratégie d’utilisation des données est une règle qui spécifie les actions marketing qui sont restreintes en fonction de l’application des étiquettes d’utilisation appliquées aux données de la plateforme.

**Application des** politiques : Permet d’appliquer des stratégies d’utilisation des données à l’aide d’actions marketing appliquées afin d’empêcher les opérations de données qui constituent des violations de stratégies au sein d’une organisation.

**Clé** Principal : Une clé Principale est une désignation dans un schéma pour identifier de façon unique tous les enregistrements.

**Priorité** : Dans  [!DNL Offer Decisioning], la priorité est utilisée pour classer les offres qui répondent à toutes les contraintes, telles que l’éligibilité, le calendrier et le plafonnement.

**Graphique** d&#39;identité privée : Le graphique d&#39;identité privée (parfois appelé graphique privé) est une carte privée des relations entre les identités recoupées et liées, construite sur la base de vos données propriétaires et visible uniquement par votre organisation. Il n&#39;existe qu&#39;un seul graphique privé pour chaque organisation et sert de modèle structurel pour les graphiques d&#39;identité individuels générés pour chaque client qui interagit avec votre marque.

**Profil** du produit : Les profils de produits permettent aux administrateurs d’accorder à l’utilisateur l’accès à l’ensemble ou à un sous-ensemble de services associés à l’Experience Platform.

**Sandbox** de production : Un sandbox de production est un sandbox destiné à être utilisé dans votre environnement de production. Contrairement aux sandbox hors production, les sandbox de production ne peuvent pas être réinitialisés ni supprimés.

**Profil** : À ne pas confondre avec le Profil client en temps réel en tant que service, un profil est une représentation complète d&#39;un client individuel, construite à partir de données d&#39;enregistrement fusionnées et de séries chronologiques provenant de sources multiples.

**Accès** au profil : Le point de  `/entities` terminaison de l’API Profil client en temps réel vous permet d’accéder aux données d’enregistrement et aux événements de séries chronologiques dans le magasin de données de Profil. Voir aussi : Entités de profil

**Données** du profil : Les données de profil se rapportent à toutes les données qui se trouvent dans le magasin de données de Profil.

**Stockage** de données de profil : Le magasin de données de Profil (parfois appelé le magasin de Profils) est un système d’enregistrement de données distinct du lac de données, utilisé par le Profil client en temps réel pour créer et stocker des profils.

**Entités** de profil : Les entités de profil représentent des attributs relatifs à une personne, généralement un client. Les entités qui relèvent de cette catégorie doivent être représentées par des schémas basés sur la classe [!DNL XDM Individual Profile]. Voir aussi : Accès aux profils

**Exportation** de profil :  [!DNL Profile] export est l’un des deux types de destinations en Experience Platform. [!DNL Profile] export génère un fichier contenant des profils et des attributs et utilise des données d’identification personnelle brutes avec le courrier électronique afin de les intégrer aux plateformes de marketing et d’automatisation du courrier électronique.

**Fragment** de profil : Un fragment de profil est l&#39;information de profil d&#39;une seule identité sur la liste des identités qui existent pour un client particulier.

**ID** du profil : Un ID de profil est un identifiant généré automatiquement associé à un type d&#39;identité et représente un profil.

**Propriété** : Dans  [!DNL Platform Launch]un cas, une propriété est un conteneur pour tout ce qui est nécessaire pour déployer un ensemble de balises.

## Q

**Requête** : Les requêtes sont des demandes de données provenant de tables de base de données.

**Éditeur** de requête : Requête Editor est un outil permettant d&#39;écrire, de valider et d&#39;envoyer des instructions SQL dans  [!DNL Query Service].

## R

**Plate-forme** de données client en temps réel :  [!DNL Real-time Customer Data Platform] rassemble des données clients connues et inconnues afin de créer des profils clients fiables avec une intégration simplifiée, une segmentation intelligente et une activation en temps réel sur le parcours client numérique.

**Profil** client en temps réel : Le Profil client en temps réel (parfois appelé Profil) offre une vue holistique de chaque client en combinant des données provenant de plusieurs canaux, notamment en ligne, hors ligne, CRM et tiers. Profil vous permet de consolider vos données client en profils individuels offrant des comptes interactifs horodatés pour chaque interaction client.

**Recette** : Une recette est le terme Adobe d&#39;une spécification de modèle et est un conteneur de niveau supérieur représentant des processus d&#39;apprentissage automatique spécifiques, des algorithmes d&#39;IA, la logique de traitement et les paramètres de configuration nécessaires pour créer et exécuter un modèle formé et aider ainsi à résoudre des problèmes commerciaux spécifiques.

**Enregistrer** : Un enregistrement est une donnée qui persiste sous forme de lignes dans un jeu de données.

**Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.

**Périodique** : Dans  [!DNL Query Service]le cas présent, une périodicité définit si une requête doit être exécutée une seule fois ou sur une base récurrente.

**Représentation** : Dans  [!DNL Offer Decisioning]un cas, une représentation est une information utilisée par un canal pour afficher une offre, telle que l’emplacement ou la langue.

**Ressource** : Dans  [!DNL Platform Launch]un environnement client, une ressource est un terme générique qui fait référence aux options que l’ [!DNL Platform Launch] utilisateur peut configurer dans l’ client, y compris les extensions, les éléments de données et les règles.

**Contrôle d&#39;accès** basé sur les rôles : Le contrôle d&#39;accès basé sur les rôles permet aux administrateurs d’attribuer l’accès et les autorisations aux utilisateurs d’Experience Platform. Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création d’environnements de test, la définition de schémas et la gestion des jeux de données.

**Règle** : Dans  [!DNL Platform Launch]un cas, une règle est un ensemble de composants définissant un ensemble spécifique de événements, de conditions et d’actions qui doivent être regroupés logiquement.

**Composant** de règle : Dans  [!DNL Platform Launch], les composants de règle sont les événements, les conditions et les actions qui constituent une règle.

**Exécution** : L’exécution spécifie un environnement d’exécution pour une recette d’apprentissage automatique. [!DNL Python], R,  [!DNL Spark]PySpark et Tensorflow vous permettent de saisir une URL vers une image Docker pour une source de recettes.

## S

**Exemples de données** : L’exemple de données est la prévisualisation d’un fichier de données, généralement les 100 premières lignes, qui fournit à un chercheur en données ou une idée du schéma ou des données qu’il contient.

**Sandbox** : Un sandbox est une construction virtuelle qui partitionne une instance de plateforme unique en un environnement virtuel distinct, afin d&#39;aider à développer et à développer des applications d&#39;expérience numérique.

**Sandbox reset** : Une réinitialisation de sandbox supprime toutes les données, y compris les données, les profils et les segments dans un sandbox. Les réinitialisations de sandbox peuvent affecter les données connectées à des destinations internes ou externes.

**Interrupteur** sandbox : Le contrôle sandbox Switch dans l’Experience Platform permet aux utilisateurs de naviguer entre les sandbox auxquels ils ont accès. Le fait de changer d’environnement de test modifie tout le contenu et peut modifier l’accès aux fonctionnalités en fonction des autorisations.

**Planification** : Une planification est une spécification définie par l’utilisateur concernant la fréquence ou la cadence d’assimilation des données d’une source de données tierce à Adobe Experience Platform.

**Scoring** : Le score est le processus de génération d’informations à partir de données à l’aide d’un modèle formé.

**Schéma** : Un schéma est un ensemble de règles qui représentent et valident la structure et le format des données. Un schéma est constitué d&#39;une classe et d&#39;un ou de plusieurs mixins facultatifs et est utilisé pour créer des jeux de données et des séries de données. Un schéma peut inclure des attributs comportementaux, des horodatages, des identités, des définitions d’attributs, des relations, etc.

**Bibliothèque** de schémas : La bibliothèque de Schémas contient des ressources XDM standard mises à disposition par Adobe, ainsi que des ressources personnalisées définies par votre organisation.

**Registre** des schémas : Le registre des Schémas fournit une interface utilisateur et une API RESTful utilisées pour vue et gérer toutes les ressources liées au schéma dans la bibliothèque de Schémas.

**Clé** d&#39;accès secrète : Une clé d’accès secrète est une clé  [!DNL Amazon] S3 utilisée conjointement avec l’ID de clé d’accès pour signer les requêtes AWS.

**Segment** : Un segment est un ensemble de règles qui incluent des attributs et des données de événement qui permettent à un certain nombre de profils de devenir une audience.

**Créateur** de segments : Il  [!DNL Segment Builder] s’agit d’un environnement de développement visuel utilisé pour créer des définitions de segment. Il sert de composant commun à toutes les applications utilisant le service de segmentation des Experience Platform.

**Définition** de segment : Une définition de segment est le jeu de règles utilisé pour décrire les principales caractéristiques ou le comportement d’une audience de cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.

**Méthode** d&#39;évaluation des segments : Il existe deux méthodes d’évaluation des segments : planifié et à la demande. L’évaluation planifiée permet d’établir un calendrier récurrent pour l’exécution d’une tâche d’exportation à un moment précis, tandis que l’évaluation à la demande implique la création d’une tâche de segment pour créer immédiatement l’audience.

**Exportation** de segments : L’exportation de segments est l’un des deux types de destinations dans l’Experience Platform. Avec l’exportation de segments, vous pouvez envoyer les profils qui remplissent les conditions requises et qui ont été mappés à la destination. Elle utilise les identifiants de segment et d’utilisateur, ainsi que les données pseudonymes, et s’intègre généralement aux réseaux sociaux et aux autres plateformes cible de médias numériques.

**ID** de segment : Un ID de segment est un identifiant généré automatiquement associé à un segment.

**Appartenance** au segment : L’appartenance à un segment affiche le ou les segments auxquels un profil fait actuellement partie.

**Règles** de segmentation : Les règles de segmentation définissent les conditions qui déterminent si un profil est admissible pour un segment.

**Segmentation** : La segmentation consiste à diviser un grand groupe de clients, de prospects ou de consommateurs en groupes plus petits qui partagent des attributs similaires et réagissent de la même manière à des stratégies marketing spécifiques.

**Sensei ML Framework** : Sensei ML Framework est un cadre unifié d&#39;apprentissage automatique (ML) qui exploite les données Experience Platform pour permettre aux chercheurs en données de développer des services de renseignement pilotés par ML d&#39;une manière plus rapide, évolutive et réutilisable.

**Étiquettes** sensibles (&quot;S&quot;) : Les libellés sensibles (&quot;S&quot;) sont utilisés pour classer les données jugées sensibles, par exemple les différents types de données comportementales ou géographiques à marquer comme sensibles.

**Services** : Un cadre puissant pour rendre opérationnels les services d&#39;IA et de ML en exploitant les services intelligents Adobes. Services offre des expériences client personnalisées en temps réel ou rendent opérationnels des services intelligents personnalisés.

**Action** marketing de personnalisation d&#39;identité unique : Action marketing qui utilise les données pour la personnalisation du contenu sur site. La personnalisation sur site est toute donnée utilisée pour faire des inférences sur les intérêts des utilisateurs et sert à sélectionner le contenu ou les publicités qui sont diffusés en fonction de ces inférences.

**Étiquette** d&#39;utilisation des données S1 : Un libellé d’utilisation des  `S1` données est utilisé pour classer les données spécifiant la latitude et la longitude qui peuvent être utilisées pour déterminer l’emplacement précis d’un périphérique.

**Étiquette** d&#39;utilisation des données S2 : Un libellé d’utilisation des  `S2` données est utilisé pour classer les données qui peuvent être utilisées pour déterminer une zone de géofence définie de manière générale.

**Source** : Une source est un terme général pour tout connecteur d’entrée dans la plate-forme. Voir aussi : Connecteur source

**Attribut** source : Un attribut source est un champ du jeu de données source. Les attributs sources sont mappés aux champs de schémas sources.

**Catalogue** source : Le catalogue source est la liste des connecteurs source disponibles dans l’Experience Platform.

**Catégorie** source : Une catégorie source est un groupement de sources présentant des caractéristiques similaires.

**Connecteur** source : Les connecteurs de source (également appelés sources) permettent aux utilisateurs d’assimiler facilement des données provenant de plusieurs sources, ce qui permet de structurer, d’étiqueter et d’améliorer les données à l’aide de services Experience Platform. Les données peuvent être ingérées à partir de différentes sources, comme le stockage dans le cloud, les logiciels tiers et les systèmes de gestion de la relation client.

**Connexion** en flux continu : Une connexion en flux continu est un point de terminaison unique fourni par l’Adobe et lié à l’organisation IMS d’un client pour diffuser des données dans l’Experience Platform.

**Espace de nommage** d&#39;identité standard : Les espaces de nommage d&#39;identité standard sont des espaces de nommage d&#39;identité prédéfinis fournis par l&#39;Adobe, qui représentent des solutions standard couramment utilisées pour identifier les clients.

**Prise en charge** en flux continu : L’assimilation en flux continu vous permet d’envoyer des données en temps réel à l’Experience Platform à partir d’appareils côté client et serveur.

**Segmentation** en flux continu : La segmentation en flux continu est un processus continu de sélection des données qui met à jour les segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

**Vue** système : La Vue système est une représentation visuelle des jeux de données source qui circulent  [!DNL Real-time Customer Profile] vers les destinations.

## T

**Fonctionnalités** de la cible : Dans le mappage des fonctionnalités, une fonction de cible est la fonction prédite par un modèle.

**Données** de série chronologique : Les données de séries chronologiques fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet enregistré.

**Modèle** formé : Un modèle formé représente la sortie exécutable d&#39;un processus de formation de modèle, dans lequel un ensemble de données de formation a été appliqué à l&#39;instance de modèle. Un modèle formé conserve une référence au service web intelligent qui est créé à partir de celui-ci. Un modèle de formation est adapté à la notation et à la création d&#39;un service web intelligent.

**Jeton** : Un jeton est un type de sécurité d’authentification à deux facteurs qui peut être utilisé pour autoriser l’utilisation de services informatiques avec  [!DNL Query Service].

## U

**Schéma** Union : Un schéma d’union est une consolidation des schémas qui partagent la même classe et ont été activés pour  [!DNL Real-time Customer Profile]. Plusieurs schémas d&#39;union peuvent exister pour une organisation, mais il ne peut y avoir qu&#39;un seul schéma d&#39;union par classe.

## V

## W

## X

**XDM** : Voir Modèle de données d’expérience (XDM).

**Événement** de décision XDM : Le Événement de décision XDM est une classe fondée sur des séries chronologiques qui permet de recueillir des observations sur le résultat et le contexte d&#39;une activité de décision. Cela comprend des renseignements sur la façon dont la décision a été prise, le moment où elle a été prise, les options proposées (et choisies) et l&#39;état contextuel qui a influé sur la décision ou qui a pu être observé pendant le processus de décision.

**XDM ExperienceEvent** : XDM ExperienceEvent est une classe basée sur des séries chronologiques utilisée pour capturer l&#39;état du système lorsqu&#39;un événement (ou un ensemble de événements) s&#39;est produit, y compris le moment et l&#39;identité du sujet concerné. Voir aussi : Événement d’expérience

**Profil** XDM individuel : XDM  [!DNL Individual Profile] est une classe basée sur des enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

**Système** XDM : Le système XDM représente le cadre qui rend opérationnels les schémas XDM pour les utiliser dans les services Experience Platform en aval.

## Y

## Z
