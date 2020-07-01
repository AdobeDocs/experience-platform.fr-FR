---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Documentation du produit Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '6594'
ht-degree: 0%

---


# Adobe Experience Platform Glossaire {#adobe-experience-platform-glossary}

## A

**Contrôle d&#39;accès :** {#access-control} Contrôle d&#39;accès pour [!DNL Experience Platform] lier les utilisateurs disposant d’autorisations d’accès et d’environnements de sandbox par le biais de profils de produits à Adobe.

**ID de clé d&#39;accès :** L’ID de clé d’accès est un identifiant unique associé à une clé d’accès secret Amazon S3. L’ID de clé d’accès et la clé d’accès secrète sont utilisés conjointement pour signer les demandes AWS.

**Action :** Dans [!DNL Experience Platform Launch]le cas présent, une action est un type spécifique de composant de règle qui définit ce qui doit se produire une fois qu’un événement s’est produit et que les conditions ont été évaluées et transmises.

**Activer :** Dans [!DNL Real-time Customer Data Platform], activer désigne l’action entreprise par un utilisateur pour mapper un segment ou des profils à une destination telle que [!DNL Oracle Eloqua], [!DNL Google]ou [!DNL Salesforce Marketing Cloud]la destination.

**Activité :** Dans le [!DNL Decisioning Service], une activité est un ensemble d’offres dont le spécialiste du marketing souhaite que le moteur de décision sélectionne la meilleure offre.

**Adobe Admin Console :** Adobe Admin Console fournit un emplacement central pour la gestion des autorisations d’accès et de fonctionnalités pour votre entreprise.

**Adobe Experience Platform :** L&#39;Adobe Experience Platform normalise les données et le contenu dans l&#39;ensemble de l&#39;entreprise, alimente les profils en temps réel pour les consommateurs, permet la science des données et accélère la vitesse de diffusion du contenu afin d&#39;orienter la personnalisation de l&#39;expérience tout au long du parcours des clients.

**Connecteurs Adobe :** Les connecteurs Adobe sont des connexions préconfigurées créées par Adobe pour permettre aux données d’entrer et de sortir [!DNL Experience Platform]. Les connecteurs sont [!DNL Microsoft Dynamics], [!DNL Salesforce], [!DNL Amazon S3]et [!DNL Azure Blob].

**Adobe Intelligent Services :** Adobe Sensei est le cadre du renseignement qui donne le pouvoir [!DNL Experience Platform]. Il fournit également un ensemble de services d&#39;IA qui permet aux marques d&#39;améliorer leur capacité à fournir des expériences client personnalisées en temps réel.

**E/S Adobe :** Les E/S Adobe font partie de [!DNL Experience Platform] et permettent aux développeurs d&#39;accéder à tout ce dont ils ont besoin pour intégrer, étendre et personnaliser l&#39;Adobe Experience Platform, y compris les API, les événements, la console de développement et les outils utiles.

**Adobe Sensei :** Adobe Sensei est le cadre du renseignement qui donne le pouvoir [!DNL Experience Platform]. Il fournit également un ensemble de services d&#39;IA qui permet aux marques d&#39;améliorer leur capacité à fournir des expériences client personnalisées en temps réel.

**Paquet Amazon S3 :** [!DNL Amazon S3] les compartiments sont les conteneurs fondamentaux des données stockées dans l&#39; [!DNL Amazon] écosystème. Les compartiments contiennent des objets, chaque objet est stocké et récupéré à l’aide d’une clé unique attribuée par le développeur.

**Connecteur Amazon S3 :** [!DNL Amazon] Le connecteur S3 permet aux clients de [!DNL Experience Platform] se connecter en toute sécurité et d&#39;accéder à leurs données [!DNL Amazon] S3.

**Ajouter une stratégie d&#39;enregistrement :** La stratégie d’ `Append` enregistrement est une option utilisée lors de la spécification de données tierces à assimiler via une connexion et de l’ajout de toute nouvelle donnée ou ligne à la fin du jeu de données. Les lignes précédemment ingérées restent intactes et seules les lignes créées depuis la dernière exécution planifiée sont ingérées [!DNL Experience Platform]. Les lignes qui ont été modifiées dans le système source restent inchangées [!DNL Experience Platform].

**Gestion du cycle de vie des applications :** La gestion du cycle de vie des applications permet de créer des environnements virtuels distincts pour développer et développer des applications d&#39;expérience numérique.

**Tableau :** Les tableaux sont utilisés pour les éléments triés avec le même type de données.

**Intelligence artificielle :** L&#39;intelligence artificielle est une théorie et un développement de systèmes informatiques capables d&#39;exécuter des tâches qui nécessitent normalement l&#39;intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction entre les langues.

**Attributs :** Les attributs sont des caractéristiques spécifiées qui représentent un profil.

**Fusion d’attributs :** La fusion d’attributs définit comment une stratégie de fusion donne la priorité à la valeur d’attribut de profil en cas de conflit de données.

**Attribution AI :** [!DNL Attribution AI] est un service Adobe Sensei qui offre des fonctionnalités d’attribution algorithmique à plusieurs canaux sur l’ensemble du cycle de vie du client.

**Audience**: Une audience est l’ensemble de profils résultant qui répondent aux critères d’une définition de segment.

**Instantané** de l&#39;Audience : Un instantané d’audience capture tous les profils qui remplissent les critères de segmentation au moment de la segmentation.

[Retour au début](#adobe-experience-platform-glossary)

## B

**Renvoi :** Dans [!DNL Real-time Customer Data Platform]les connexions source planifiées, le renvoi permet l’assimilation de données historiques.

**Période de renvoi :** `Backfill period` est une option permettant de définir la durée d’importation des données historiques tierces via une connexion. La sélection d’une période de renvoi indéfiniment ingère l’historique complet des données source à [!DNL Experience Platform].

**Lot :** Le lot est un ensemble de données collectées sur une période donnée et traitées ensemble en une seule unité.

**ID du lot :** L’ID de lot est un identifiant généré par Adobe pour un lot de données.

**Ingestion par lots :** L’assimilation de lots permet aux utilisateurs d’assimiler des pétaoctets de données et de les rendre disponibles dans les systèmes d’entreprise. Grâce aux technologies les plus récentes, les utilisateurs peuvent désormais intégrer n&#39;importe quel schéma XDM et non XDM dans [!DNL Experience Platform].

**Segmentation par lots :** La segmentation par lots est une alternative à un processus continu de sélection des données et déplace toutes les données de profil à la fois par le biais de définitions de segment afin de produire les audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin de pouvoir être exporté en vue de son utilisation.

**Créer :** Dans [!DNL Experience Platform Launch], une compilation est une bibliothèque déployée. La compilation est un fichier ou un ensemble de fichiers qui contient toutes les configurations et le code nécessaires pour exécuter la logique métier contenue dans cette bibliothèque.

**Outils Business Intelligence :** L&#39;intelligence d&#39;affaires, également appelée outils de &quot;BI&quot;, est principalement intégrée au [!DNL Experience Platform Query Service]système. Les outils BI sont des types de logiciels d&#39;application qui collectent et traitent de grandes quantités de données non structurées provenant de systèmes internes et externes.

[Retour au début](#adobe-experience-platform-glossary)

## C

**Capping :** Dans le [!DNL Decisioning Service], le plafonnement est utilisé dans les règles de prise de décision pour définir le nombre de présentations d’une offre. Il existe deux types de casquettes : le nombre de fois où une offre peut être proposée dans l&#39;audience combinée de cible, également appelée &quot;casquette globale&quot;, et le nombre de fois où une offre peut être proposée au même utilisateur final, également appelé &quot;casquette de Profil&quot;.

**Catalogue :** Dans [!DNL Real-time Customer Data Platform], dans les sources et les destinations, un catalogue est une galerie avec des connexions disponibles aux applications Adobe et aux technologies tierces.

**Classe :** Une classe définit le plus petit ensemble de champs utilisé pour créer un schéma et est le comportement de base qui décrit l&#39;objet métier.

**Client :** Un client est un outil ou une application externe qui se connecte à [!DNL Query Service] via le protocole postgres ou l’API HTTP.

**Collection :** Dans le [!DNL Decisioning Service], les collections sont des sous-ensembles d’offres basés sur des conditions prédéfinies définies par un spécialiste du marketing, telles que la catégorie de l’offre.

**Interface de ligne de commande :** L&#39;interface de ligne de commande est un outil de ligne de commande utilisé pour se connecter à [!DNL Query Service] des fins d&#39;exécution de requête brute.

**Composition**: Une composition est un groupement de composants qui se forment ensemble pour constituer le schéma.

**Connexion :** Une connexion est un pipeline virtuel qui permet aux données d&#39;entrer et de sortir [!DNL Experience Platform]. Les connexions sont maintenant remplacées par Sources.

**Connecteur :** Les connecteurs d’Adobe Experience Platform Source aident les utilisateurs à assimiler facilement des données provenant de plusieurs sources, ce qui leur permet de structurer, d’étiqueter et d’améliorer les données à l’aide de [!DNL Experience Platform Services]. Les données peuvent être ingérées à partir de diverses sources, telles que l’enregistrement cloud, les logiciels tiers et les systèmes de gestion de la relation client.

**Condition :** Dans l’Experience Platform Launch, une condition est un composant de règle qui évalue une instruction logique qui doit renvoyer `true` ou `false`. Toutes les conditions doivent être évaluées `true` et toutes les conditions d’exception doivent l’être `false` avant l’exécution des actions de la règle.

**Console :** Dans [!DNL Query Service], la console fournit des informations sur l’état et le fonctionnement d’une Requête. La console affiche l&#39;état de la connexion à [!DNL Query Service], les opérations de requête en cours d&#39;exécution et les messages d&#39;erreur qui en résultent.

**Étiquettes des données de contrat &quot;C&quot; :** Les étiquettes de contrat `C` permettent de classer les données qui ont des obligations contractuelles ou qui sont liées aux stratégies de gouvernance des données d’un client.

**Étiquette de contrat C1 :** `C1` L’étiquette de gouvernance des données de contrat spécifie que les données peuvent uniquement être exportées à partir d’Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants de périphérique ou de particulier. Par exemple, les données provenant des réseaux sociaux.

**Étiquette de contrat C2 :** `C2` l’étiquette de gouvernance des données de contrat spécifie les données qui ne peuvent pas être exportées vers un tiers. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent l&#39;exportation de données d&#39;où elles ont été collectées à l&#39;origine.  Par exemple, les contrats de réseaux sociaux limitent souvent le transfert de données que vous recevez d&#39;eux. C2 est plus restrictif que C1, qui ne nécessite que l&#39;agrégation et les données anonymes.

**Étiquette de contrat C3 :** `C3` l&#39;étiquette de gouvernance des données contractuelles spécifie les données qui ne peuvent pas être combinées ou utilisées autrement avec des informations directement identifiables. Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent la combinaison ou l&#39;utilisation de ces données avec des informations directement identifiables.  Par exemple, les contrats pour les données provenant des réseaux publicitaires, des serveurs d’annonces et des fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques sur l’utilisation de données directement identifiables.

**Étiquette de contrat C4 :** `C4` l’étiquette de gouvernance des données de contrat spécifie que les données ne peuvent pas être utilisées pour cibler des publicités ou du contenu, sur site ou entre sites. C4 est l&#39;étiquette la plus restrictive puisqu&#39;elle englobe les étiquettes C5, C6 et C7.

**Étiquette de contrat C5 :** `C5` l’étiquette de gouvernance des données de contrat spécifie que les données ne peuvent pas être utilisées pour le ciblage intersite basé sur les intérêts du contenu ou des publicités. Le ciblage basé sur l’intérêt, ou la personnalisation, se produit si les trois conditions suivantes sont remplies :  Les données collectées sur le site servent à faire des inférences sur l’intérêt d’un utilisateur, sont utilisées dans un autre contexte, tel que sur un autre site ou une autre application, et servent à sélectionner le contenu ou les publicités qui sont diffusés en fonction de ces inférences.

**Étiquette de contrat C6 :** `C6` l’étiquette de gouvernance des données de contrat spécifie que les données ne peuvent pas être utilisées pour le ciblage publicitaire sur site. Les données ne peuvent pas être utilisées pour le ciblage des publicités sur site, y compris la sélection et la diffusion des publicités sur les sites Web ou les applications de votre entreprise, ni pour mesurer la diffusion et l&#39;efficacité de ces publicités.  Cela inclut l’utilisation des données collectées sur site sur l’intérêt des utilisateurs pour sélectionner des publicités, traiter les données sur les publicités affichées, le moment et l’endroit où elles ont été affichées et déterminer si les utilisateurs ont pris des mesures en rapport avec la publicité, comme cliquer sur une publicité ou faire un achat.

**Étiquette de contrat C7 :** `C7` l’étiquette de gouvernance des données de contrat spécifie que les données ne peuvent pas être utilisées pour le ciblage du contenu sur site.  Les données ne peuvent pas être utilisées pour le ciblage du contenu sur site, y compris la sélection et la diffusion de contenu sur les sites Web ou les applications de votre entreprise, ni pour mesurer la diffusion et l&#39;efficacité de ce contenu.  Cela inclut les informations collectées précédemment sur l’intérêt des utilisateurs à sélectionner le contenu, à traiter les données sur le contenu affiché, la fréquence ou la durée d’affichage, le moment et l’emplacement d’affichage, et à déterminer si les utilisateurs ont pris des mesures en rapport avec le contenu, notamment en cliquant sur le contenu.

**Étiquette de contrat C8 :** `C8` l’étiquette de gouvernance des données de contrat spécifie que les données ne peuvent pas être utilisées pour la mesure des sites Web ou des applications de votre entreprise. Les données ne peuvent pas être utilisées pour mesurer, comprendre et générer des rapports sur l’utilisation par les utilisateurs des sites ou applications de votre entreprise. Cela n’inclut pas le ciblage basé sur les intérêts, qui est la collecte d’informations sur votre utilisation de ce service pour personnaliser ultérieurement le contenu et/ou la publicité dans d’autres contextes.

**Étiquette de contrat C9 :** `C9` l&#39;étiquette de gouvernance des données contractuelles spécifie que les données ne peuvent pas être utilisées dans les workflows Data Science. Certains contrats comportent des interdictions explicites sur les données utilisées pour la science des données.  Il arrive que ces termes interdisent l&#39;utilisation de données pour l&#39;intelligence artificielle (IA), l&#39;apprentissage automatique (ML) ou la modélisation.

**Colonne de date de création :** La sélection d’une `Created Date` colonne est une option lors de la spécification de données tierces via une connexion. Lorsque la stratégie d’enregistrement d’ajout est sélectionnée et que le jeu de données contient plusieurs dates liées au schéma, l’utilisateur doit choisir entre la date et l’heure disponibles et le schéma pour spécifier une colonne de `Created Date` clé. `Created Date` n’est pas disponible lorsque la stratégie d’enregistrement de remplacement est sélectionnée.

**Créer un tableau comme sélection :** La commande Create Table as Select est une commande SQL qui, lorsqu&#39;elle est exécutée dans le cadre d&#39;une requête SQL complète et valide, demande à l&#39;utilisateur [!DNL Query Service] de conserver les résultats de la requête dans un jeu de données sur le lac Data. Les options incluent : Créer, Remplacer tout le précédent et Ajouter au précédent.

**Données intersites :** Les données intersites sont la combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site.

**Espace de nommage d&#39;identité personnalisée :** Les espaces de nommage d&#39;identité personnalisés sont des identifiants créés par le client qui représentent les identités d&#39;une organisation ou d&#39;une entreprise spécifique.

**AI du client :** Customer AI est un service Adobe Sensei qui enrichit les profils clients grâce à des propensions basées sur l’IA et permet la segmentation et le ciblage des clients.

[Retour au début](#adobe-experience-platform-glossary)

## J

**Dictionnaire de données :** Dans [!DNL Experience Platform Launch]un dictionnaire de données, il s’agit d’un ensemble d’éléments de données définis dans une propriété.

**Elément de données :** Dans [!DNL Experience Platform Launch]le cas présent, un élément de données est un pointeur utilisé dans les règles et extensions pour pointer vers un élément de données spécifique existant sur le périphérique client.

**Couche de données :** Dans [!DNL Experience Platform Launch]le cas présent, une couche de données est une structure de données qui existe sur le périphérique client et qui contient des métadonnées sur le contexte dans lequel une page ou un écran est affiché.

**Mappage de données :** Le mappage des données est le processus de mappage des champs de données source aux champs de cible liés à la destination.

**Flux de données :** Un flux de données est un ensemble ou un ensemble de messages qui partagent le même schéma et sont envoyés par la même source.

**Gouvernance des données :** [!DNL Data governance] englobe les stratégies et les technologies utilisées pour s&#39;assurer que les données sont conformes aux règlements et aux politiques de l&#39;organisation en matière d&#39;utilisation des données.

**Étiquettes de gouvernance des données :** [!DNL Data governance] les étiquettes permettent aux utilisateurs de classifier les données qui reflètent les considérations liées à la vie privée et les conditions contractuelles afin de se conformer aux règlements et aux politiques de l&#39;entreprise. [!DNL Data governance] les étiquettes ajoutées à un jeu de données sont héritées ou appliquées à tous les champs de ce jeu de données. [!DNL Data governance] les libellés peuvent également être appliqués directement aux champs.

**Partenaires d&#39;intégration de données :** Les partenaires d&#39;intégration de données simplifient et automatisent le chargement et la transformation de volumes massifs de données de plus de 200 sources vers [!DNL Experience Platform] sans écrire de code.

**Étiquettes des jeux de données :** Les étiquettes d’utilisation des données peuvent être ajoutées aux jeux de données. Tous les champs de ce jeu de données héritent des étiquettes du jeu de données.

**Espace de travail des sciences de données :** [!DNL Data Science Workspace] permet [!DNL Experience Platform] aux clients de créer des modèles d’apprentissage automatique utilisant des données dans les applications [!DNL Experience Platform] Adobe et afin de générer des aperçus et des prédictions intelligents pour tisser de superbes expériences numériques d’utilisateur final.

**Source de données :** Une source de données est une origine de données désignée par l’utilisateur. Par exemple, une source de données est une application mobile, un événement de profil et/ou d’expérience, un événement de profil de site Web ou un service de gestion de la relation client.

**Progression des données :** Le responsable de la gestion, de la surveillance et de l&#39;application des ressources de données d&#39;une organisation est le responsable de l&#39;intendance des données. Un gestionnaire de données veille également à ce que les politiques de gouvernance des données soient préservées et maintenues pour être conformes aux règlements et aux politiques organisationnelles du gouvernement.

**Type de données :** Le type de données est un objet réutilisable avec des propriétés dans une représentation hiérarchique.

**Étiquettes d’utilisation des données :** Les étiquettes d’utilisation des données permettent aux utilisateurs de classer les données en catégories qui reflètent les considérations liées à la vie privée et les conditions contractuelles afin de se conformer aux réglementations et aux politiques de l’entreprise.

**Flux de données :** Dans [!DNL Real-time Customer Data Platform]le cas d’un flux de données, il s’agit d’un pipeline virtuel de données entrant [!DNL Platform] d’une source et sortant vers des destinations.

**Jeu de données :** Un jeu de données est un concept d&#39;enregistrement et de gestion pour une collection de données, généralement un tableau, qui contient des schémas (colonnes) et des champs (lignes).

**ID du jeu de données :** Identifiant généré par Adobe pour un jeu de données assimilé.

**Sortie du jeu de données :** La sortie d&#39;un jeu de données fournit un mécanisme permettant de déterminer l&#39;utilisation de l&#39;option *Créer une table comme sélection* pour une [!DNL Query Service] exécution particulière.

**Événement de décision :** Un événement de décision est utilisé pour recueillir des observations sur le résultat et le contexte d&#39;une activité de décision. Le événement de décision permet de savoir comment la décision a été prise, quand elle a eu lieu, quelles options ont été proposées (choisies) et quel état contextuel a existé qui a influencé la décision ou a pu être observé pendant le processus de décision. Le événement de décision capture également l’ID de proposition, un identifiant unique global qui peut être utilisé pour corréler la décision à d’autres événements.

**Règle de décision :** Dans le [!DNL Decisioning Service]cas présent, une règle de décision est la logique qui définit et contrôle ce qui, quand, où et comment une offre est présentée aux utilisateurs finaux.

**Service de prise de décision :** L’interface utilisateur [!DNL Decisioning Service] est un ensemble de services qui permet aux spécialistes du marketing de créer et de proposer des expériences d’offre personnalisées pour les utilisateurs finaux sur plusieurs canaux et applications à l’aide de règles de décision et de logique métier.

**Colonne delta :** Dans [!DNL Real-time Customer Data Platform]la colonne delta, vous pouvez sélectionner un champ de données source pour un horodatage d’assimilation incrémentielle.

**Stratégie d&#39;enregistrement Delta :** `Delta save strategy` est une option permettant d’ingérer des données tierces via une connexion. L’option permet à l’utilisateur de spécifier si des lignes de données source nouvelles ou modifiées sont assimilées [!DNL Experience Platform]. De nouvelles lignes sont ajoutées à la fin du jeu de données et les lignes modifiées sont mises à jour dans le jeu de données le [!DNL Experience Platform].

**Destination :** Dans [!DNL Real-time Customer Data Platform] une destination est un terme général pour tout système, tel qu’une application Adobe, un serveur publicitaire ou un réseau publicitaire où une audience est activée et diffusée.

**Catégorie de destination :** Une catégorie de destination est un groupe de destinations présentant des caractéristiques similaires. [!DNL Real-time Customer Data Platform]

**Catalogue de destination :** Un catalogue de destination est une liste de destinations disponibles dans le [!DNL Real-time Customer Data Platform].

**Nom d’affichage :** Le nom d’affichage est un nom convivial d’un champ qui s’affiche dans l’interface utilisateur.

**DULE :** DULE est un acronyme pour *Data Usage Labeling and Enforcement*. DULE est un élément clé de la gouvernance des données et un ensemble de fonctionnalités clés qui permet d&#39;étiqueter et d&#39;appliquer des politiques d&#39;accès aux données pour répondre aux besoins de gouvernance au sein d&#39;une organisation.

[Retour au début](#adobe-experience-platform-glossary)

## e

**Diagnostics d&#39;erreur :** Les diagnostics d’erreur permettent de générer des messages d’erreur détaillés pour les lots assimilés. Le seuil d&#39;erreur permet de configurer le pourcentage d&#39;erreurs acceptables avant que le lot entier ne soit mis en échec.

**Offre éligible :** Dans le [!DNL Decisioning Service]cas, une offre éligible répond aux contraintes définies en amont qui peuvent être offertes de manière cohérente à un profil.

**Règles d&#39;éligibilité :** Dans le [!DNL Decisioning Service], les règles d&#39;éligibilité sont appliquées à un profil lié aux contraintes de calendrier, de planification et de plafonnement.

**Code incorporé :** Dans [!DNL Experience Platform Launch]le cas présent, le code incorporé est une balise de script placée dans le code HTML sur un site ou un environnement. Le code incorporé indique au navigateur où récupérer la compilation.

**Énumération :** Un énumération est une liste de valeurs qui représente les données valides d’un champ.

**Environnement :** Dans [!DNL Experience Platform Launch], un environnement est un ensemble d&#39;instructions de déploiement qui spécifie la diffusion hôte et le format de fichier d&#39;une build. Une bibliothèque doit être associée à un environnement avant de pouvoir être créée.

**Événement** Dans [!DNL Experience Platform Launch], un événement est un type spécifique de composant de règle, un déclencheur qui se produit sur un périphérique client pour commencer l’exécution d’une règle.

**Événements :** Les Événements sont les données de comportement associées à un profil.

**Modèle de données d’expérience (XDM) :** [!DNL Experience Data Model] (XDM) est le concept d’utilisation de schémas standard pour unifier les données en vue de les utiliser avec [!DNL Experience Platform] les applications Adobe Experience Cloud. XDM normalise la structure des données et accélère et simplifie le processus d&#39;obtention de connaissances à partir de quantités massives de données.

**Experience Platform Launch :** [!DNL Launch] est un écosystème de gestion des balises et des SDK, intégré aux [!DNL Experience Platform] applications et aux [!DNL Experience Cloud] applications. [!DNL Launch] fournit des outils permettant de déployer, d’unifier et de gérer les intégrations d’analyses, de marketing et de publicité nécessaires pour alimenter les expériences client pertinentes sur tous les périphériques client.

**Extensions Experience Platform Launch :** [!DNL Experience Platform Launch] les extensions permettent la diffusion de données de événement brutes directement vers [!DNL Real-time Customer Data Platform] les destinations. L’installation [!DNL Launch] des extensions nécessite l’accès aux [!DNL Launch] propriétés.

**Expérience :** Une expérience est un processus de création d’un modèle entraîné en formant l’instance avec une portion d’échantillon des données de production en direct.

**Expériences :** Les expériences sont le processus d&#39;application d&#39;un modèle formé à une petite partie des données de production en direct pour valider ses performances. Il s’agit d’un modèle différent d’un modèle entraîné qui est testé par rapport à un jeu de données de test d’absence. Ceci est également différent du concept d&#39;Expérience dans certains cadres ML où cela signifie en fait un exemple de projet de modélisation.

**ExperienceEvent :** ExperienceEvent est un schéma [!DNL Experience Platform] standard qui capture les observations, y compris le moment et l&#39;identité du sujet concerné. Les Événements d&#39;expérience sont des enregistrements factuels de ce qui s&#39;est passé, représentant ce qui s&#39;est passé sans agrégation ni interprétation.

**Extension :** Dans [!DNL Experience Platform Launch]le cas présent, une extension est un package de fonctionnalités ajouté à une [!DNL Launch] propriété.  Une extension est généralement axée sur une solution marketing ou d’analyse particulière et fournit les outils nécessaires pour déployer cette technologie dans un environnement client.

**Package d’extension :** Dans [!DNL Experience Platform Launch]un paquet d&#39;extension est un fichier .zip créé et téléchargé par un développeur d&#39;extension qui fournit tout ce dont [!DNL Launch] les utilisateurs ont besoin pour installer l&#39;extension dans leur propriété.  Un package d&#39;extension contient un manifeste spécifiant les informations relatives à l&#39;extension, au code HTML et au code JavaScript nécessaires pour que les utilisateurs finaux puissent configurer le comportement de l&#39; [!DNL Launch] extension et le code JavaScript exécutable envoyé à l&#39;environnement client, le cas échéant.

[Retour au début](#adobe-experience-platform-glossary)

## f

**Offres de secours :** Dans le [!DNL Decisioning Service], une offre de secours est l’offre par défaut affichée lorsqu’un utilisateur final n’est pas éligible pour l’une des offres de la collection utilisée.

**Mappage des fonctionnalités :** La mise en correspondance des fonctionnalités fait référence au processus de mise en correspondance des fonctionnalités des données dans les fonctions d’entrée et de cible requises par un modèle d’apprentissage automatique.

**Champ :** Un champ est l’élément de niveau le plus bas d’un jeu de données. Chaque champ a un nom de référence et un type pour identifier le type de données qu’il contient. Les types de champ peuvent être : entier, nombre, chaîne, Boolean et schéma.

**Libellés des champs :** Les libellés de champ sont des libellés de gouvernance des données hérités d’un jeu de données ou appliqués directement à un champ.

**Nom du champ :** Field est le nom utilisé pour référencer le champ dans les requêtes et services.

**Fréquence :** La fréquence détermine la fréquence d’exécution d’une [!DNL Query Service] requête planifiée périodique.

[Retour au début](#adobe-experience-platform-glossary)

## g

**Géofence :** Une géofence est une limite géographique virtuelle, définie par un GPS ou la technologie RFID, qui permet au logiciel de déclencher une réponse lorsqu&#39;un dispositif portable entre dans une zone particulière ou en sort.

**RGPD :** Le règlement général sur la protection des données (RGPD) est un cadre juridique qui établit des lignes directrices pour la collecte et le traitement des informations à caractère personnel des personnes au sein de l&#39;Union européenne (UE). Le RGD énonce les principes du data Management et des droits de l&#39;individu et couvre toutes les sociétés qui traitent des données des citoyens de l&#39;UE.

**Étiquette des données du RGPD :** L&#39;étiquette de gouvernance du RGPD est utilisée pour définir les champs qui peuvent contenir des identifiants personnels à utiliser dans l&#39;accès au RGMD et/ou la suppression de demandes.

[Retour au début](#adobe-experience-platform-glossary)

## H

**Hôte :** Dans [!DNL Experience Platform Launch], un hôte spécifie l’emplacement, le domaine et les informations d’identification d’utilisateur nécessaires pour [!DNL Launch] diffuser une compilation.

[Retour au début](#adobe-experience-platform-glossary)

## I

**Identité :** L’identité est un identifiant tel qu’un ID de cookie, un ID de périphérique ou un ID de courrier électronique qui représente de manière unique un client final.

**Étiquettes de données &quot;I&quot; d&#39;identité :** `Identity I` les étiquettes permettent de classer les données qui peuvent identifier ou contacter une personne spécifique.

**Image d&#39;identité :** Le graphique d&#39;identité est une carte des relations entre les identités recoupées et liées, qui se met à jour en temps quasi réel avec l&#39;activité du client.

**Espace de nommage d&#39;identité :** Un espace de nommage d&#39;identité est un identifiant tel que l&#39;ID de cookie, l&#39;ID de périphérique ou l&#39;ID de courrier électronique pour indiquer le contexte d&#39;où proviennent les données et est utilisé pour reconnaître et lier les identités entre [!DNL Experience Cloud].

**Service d&#39;identité :** [!DNL Experience Platform Identity Service] L&#39;interface utilisateur permet la création et la gestion de types d&#39;identité afin de permettre la liaison d&#39;identités entre les périphériques et les canaux pour une vue utilisateur complète à partir de [!DNL Real-time Customer Profile].

**Correspondance d&#39;identité :** L’assemblage d’identité est le processus d’identification des fragments de données et de leur assemblage pour former un enregistrement complet d’un profil.

**Symbole d&#39;identité :** Le symbole d’identité est l’abréviation d’un espace de nommage d’identité qui peut être utilisé comme référence dans les API.

**Valeur d&#39;identité :** La valeur d&#39;identité est une donnée associée à une identité assignée dans le schéma. Lors de la correspondance de données d’enregistrement entre les profils, la valeur d’identité et l’espace de nommage doivent correspondre.

**Étiquette de données I1 :** Le libellé `I1` des données est utilisé pour classer les données directement identifiables qui peuvent identifier ou contacter une personne spécifique plutôt qu’un dispositif.

**Libellé des données I2 :** L&#39;étiquette `I2` de données sert à classer les données indirectement identifiables qui peuvent être utilisées en combinaison avec d&#39;autres données pour identifier ou contacter une personne spécifique.

**Envoi :** L&#39;importation est le processus d&#39;ajout de données d&#39;une source à [!DNL Experience Platform]. Les données peuvent être ingérées [!DNL Experience Platform] de différentes manières, y compris en flux continu, par lots ou ajoutées via un connecteur.

**Planification de l&#39;importation :** La planification de l&#39;importation fournit des options temporelles lors de l&#39;assimilation d&#39;une source à [!DNL Experience Platform]une autre.

**Fonction d’entrée :** La fonction d’entrée est spécifiée dans le mappage des fonctionnalités et est utilisée par un modèle d’apprentissage automatique pour effectuer des prédictions.

**Services intelligents :** [!DNL Intelligent Services] comme [!DNL Attribution AI] et [!DNL Customer AI] sont l&#39;apprentissage automatique, des modèles conçus de façon ciblée et basés sur l&#39;intelligence artificielle qui nécessitent le [!DNL Experience Platform] fonctionnement et le fonctionnement.

**Ciblage ou personnalisation axé sur l’intérêt :** Le ciblage basé sur l’intérêt, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies : les données collectées sur le site servent à faire des inférences sur l’intérêt d’un utilisateur, les données sont utilisées dans un autre contexte, tel que sur un autre site ou une autre application (hors site), et si les données sont utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

[Retour au début](#adobe-experience-platform-glossary)

## j

**[!DNL JupyterLab]:**Une interface web open-source pour Project[!DNL Jupyter]et est étroitement intégrée dans[!DNL Experience Platform].

**[!DNL Jupyter Notebook]:**Application Web open source qui permet aux utilisateurs de créer et de partager des documents contenant du code en direct, des équations, des visualisations et du texte narratif.

## k

[Retour au début](#adobe-experience-platform-glossary)

## l

**Bibliothèque :** Dans [!DNL Experience Platform Launch], une bibliothèque est un ensemble de logiques métier qui contient des instructions sur le comportement de la [!DNL Launch] bibliothèque sur le périphérique client.

[Retour au début](#adobe-experience-platform-glossary)

## M

**Machine Learning (ML) :** L&#39;apprentissage automatique est le domaine d&#39;étude qui permet aux ordinateurs d&#39;apprendre sans être explicitement programmés.

**Modèle d&#39;apprentissage automatique :** Un modèle d’apprentissage automatique est l’instance d’une recette d’apprentissage automatique qui est formée à l’aide de données historiques et de configurations pour résoudre un cas d’utilisation commerciale. En Adobe [!DNL Data Science Workspace], les modèles d&#39;apprentissage automatique sont appelés des recettes.

**Mappage :** Dans [!DNL Real-time Customer Data Platform]le cas présent, le mappage des données est le processus de mappage des champs de données source aux champs de cible liés à la destination.

**Action marketing :** Une action marketing, dans le cadre de la gouvernance des données, est une action entreprise par un utilisateur de [!DNL Experience Platform] données, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

**Méthode de fusion :** Une `merge method` option de stratégie de fusion permet de hiérarchiser la fusion des fragments de données. Les options de la méthode de fusion sont fusionnées par ordre de priorité du jeu de données ou par horodatage du jeu de données.

**Fusionner la stratégie :** Une stratégie de fusion est un ensemble de règles utilisées par [!DNL Profile] pour déterminer comment les données seront hiérarchisées et combinées en une vue unifiée dans certaines conditions.

**Mixin :** Un mixin permet aux utilisateurs d’étendre les champs réutilisables qui contiennent des variables définissant un ou plusieurs attributs destinés à être inclus dans un schéma ou ajoutés à une classe.

**Colonne de date modifiée :** La sélection d’une `Modified Date` colonne est une option lors de la spécification de données tierces via une connexion. Lorsque la stratégie d&#39; `Delta` enregistrement est sélectionnée et que le jeu de données contient plusieurs schémas liés à la date, l&#39;utilisateur doit choisir un schéma de type de date/heure disponible pour spécifier la colonne de clé de date modifiée. `Modified Date` n’est pas disponible lorsque la stratégie d’ `Overwrite` enregistrement est sélectionnée.

**Module :** Dans [!DNL Experience Platform Launch], un module est un fragment de code JavaScript exécutable fourni par une extension, qui exécute des actions dans un environnement client sans que l’ [!DNL Launch] utilisateur ait à créer une règle.

[Retour au début](#adobe-experience-platform-glossary)

## N

**Sandbox hors production :** Les sandbox hors production sont une forme de virtualisation des données qui vous permet d&#39;isoler les données des autres sandbox et sont généralement utilisés pour des expériences de développement, des tests ou des essais. Les sandbox hors production peuvent être réinitialisés et supprimés.

**[!DNL Notebooks]:**[!DNL Notebooks]sont créés à l’aide *[!DNL Jupyter Notebook]*d’une description de l’analyse, de résultats et peuvent être exécutés pour effectuer l’analyse des données.

[Retour au début](#adobe-experience-platform-glossary)

## o

**Offre :** Dans le [!DNL Decisioning Service], une offre est un message marketing auquel des règles peuvent être associées et qui indique qui peut être autorisé à voir l’offre.

**Décision sur l&#39;Offre :** Dans le [!DNL Decisioning Service]cadre de la prise de décision par offre, un spécialiste du marketing peut gérer les règles et les modèles de Propositions d&#39;offre formés lorsqu’il s’adresse à un utilisateur final en fonction des données collectées sur plusieurs canaux et applications.

**Bibliothèque d&#39;Offres :** Dans le [!DNL Decisioning Service], la bibliothèque d’offres est une bibliothèque centrale utilisée pour gérer les offres personnalisées et de secours, les règles de décision et les activités.

**Organisation :** Une organisation est le nom utilisé pour identifier une société ou un groupe spécifique au sein d’une société sur plusieurs produits Adobe. L’administrateur peut configurer et gérer l’accès et les autorisations des fonctions pour les utilisateurs d’une organisation.

**Remplacer la stratégie d&#39;enregistrement :** `Overwrite` la stratégie d’enregistrement est une option permettant d’ingérer des données tierces via une connexion, où l’utilisateur indique si les données imbriquées seront remplacées selon un calendrier spécifié. [!DNL Experience Platform] ingère le jeu de données spécifié à partir de la source tierce et remplace le jeu de données sur [!DNL Experience Platform].

[Retour au début](#adobe-experience-platform-glossary)

## p

**Importation partielle :** L&#39;assimilation partielle permet l&#39;assimilation d&#39;enregistrements valides de données de lot dans un seuil d&#39;erreur spécifié. Les diagnostics d&#39;erreur pour les enregistrements défaillants peuvent être téléchargés ou accessibles dans le contrôle.

**Dossiers de parquets :** Un fichier en parquet est un format de fichier en enregistrement à colonnes avec des structures de données imbriquées complexes. Des fichiers de parquets sont nécessaires pour ajouter des données à un jeu de données de schéma.

**Offres personnalisées :** Dans la [!DNL Decisioning Service], une offre personnalisée est un message marketing personnalisable basé sur des règles d&#39;éligibilité et des contraintes.

**Emplacements :** Dans le [!DNL Decisioning Service], un emplacement correspond à l’emplacement ou au contexte dans lequel une offre s’affiche pour un utilisateur final.

**Stratégie :** Une stratégie d’utilisation des données est une règle qui spécifie les actions marketing qui sont limitées en fonction de l’application d’étiquettes d’utilisation des données sur les données dans [!DNL Experience Platform].

**Clé de Principal :** La clé de Principal est une désignation dans un schéma pour identifier de manière unique tous les enregistrements.

**Priorité :** Dans le [!DNL Decisioning Service], la priorité est utilisée pour classer les offres qui répondent à toutes les contraintes, telles que l’éligibilité, le calendrier et le plafonnement.

**Graphique d&#39;identité privée :** Private Identity Graph est une carte privée des relations entre les identités assemblées et liées qui sont visibles par votre entreprise uniquement et créées sur la base de vos données propriétaires.

**Profil du produit :** Les profils de produits permettent aux administrateurs d’accorder à l’utilisateur l’accès à l’ensemble ou à un sous-ensemble de services associés à [!DNL Experience Platform].

**Production Sandbox :** Un sandbox de production d&#39;isolation des données virtuelles sur Platform qui ne peut pas être réinitialisé ou supprimé.

**Profil :** [!DNL Profile] est un modèle de données [!DNL Experience Platform] standard utilisé pour définir les attributs des consommateurs. Un profil peut également être un agrégat de données et d’attributs liés à une personne ou un appareil.

**Exportation Profil :** [!DNL Profile] export est l&#39;un des deux types de destinations dans [!DNL Real-time Customer Data Platform]. [!DNL Profile] export génère un fichier contenant des profils et des attributs, utilise des données d’identification personnelle brutes avec le courrier électronique et est utilisé pour l’intégration avec les plateformes de marketing et d’automatisation du courrier électronique.

**Fragment de Profil FProfile :** Un fragment de profil est l’information de profil d’une seule identité sur la liste des identités qui existent pour un utilisateur particulier.

**ID Profil :** Un ID de profil est un identifiant généré automatiquement associé à un type d&#39;identité et représente un profil.

**Propriété :** Dans [!DNL Experience Platform Launch]un cas, une propriété est un conteneur pour tout ce qui est nécessaire pour déployer un ensemble de balises.

[Retour au début](#adobe-experience-platform-glossary)

## q

**Requêtes :** Une requête est une demande de données provenant de tables de base de données.

**Éditeur de Requête :** Requête Editor est un outil permettant d&#39;écrire, de valider et d&#39;envoyer des instructions SQL dans [!DNL Query Service].

**Requête Service pour Adobe Experience Platform :** *[!DNL Experience Platform Query Service]* permet aux analystes de données d’effectuer des requêtes [!DNL ExperienceEvents] et des fichiers XDM pour les utiliser dans les analyses et l’apprentissage automatique. Grâce à [!DNL Query Service]eux, les analystes et les scientifiques de données pourront extraire tous leurs ensembles de données stockés dans [!DNL Experience Platform] - y compris les données comportementales ainsi que le point de vente, la gestion de la relation client, etc. - et les requêtes à ces ensembles de données pour répondre à des questions spécifiques sur les données.

[Retour au début](#adobe-experience-platform-glossary)

## r

**Platform de données client en temps réel :** Adobe [!DNL Real-time Customer Data Platform] rassemble des données clients connues et inconnues pour créer des profils clients de confiance avec une intégration simplifiée, une segmentation intelligente et une activation en temps réel tout au long du parcours client numérique.

**Profil client en temps réel :** [!DNL Real-time Customer Profile] est un profil centralisé pour une gestion d’expérience ciblée et personnalisée.

**Recette :** Une recette est le terme Adobe pour une spécification de modèle et est un conteneur de niveau supérieur qui représente un apprentissage automatique, un algorithme AI ou un ensemble d&#39;algorithmes, une logique de traitement et une configuration nécessaires pour créer et exécuter un modèle formé et aider ainsi à résoudre des problèmes commerciaux spécifiques.

**Enregistrer :** Un enregistrement est une donnée qui persiste sous forme de lignes dans un jeu de données.

**Périodicité :** Une périodicité définit si une [!DNL Query Service] requête doit être exécutée une seule fois ou de manière récurrente.

**Représentation :** Dans la [!DNL Decisioning Service], une représentation est une information utilisée par un canal, telle que l’emplacement ou la langue d’affichage d’une offre.

**Ressource :** Dans [!DNL Experience Platform Launch], &quot;ressource&quot; est un terme générique désignant les options que l’ [!DNL Launch] utilisateur peut configurer dans l’environnement client, y compris les extensions, les éléments de données et les règles.

**Contrôle d&#39;accès basé sur les rôles :** Le contrôle d&#39;accès basé sur les rôles permet aux administrateurs d’attribuer l’accès et les autorisations aux utilisateurs de [!DNL Experience Platform]. Les autorisations incluent la possibilité de vue et/ou d&#39;utiliser [!DNL Experience Platform] des fonctionnalités, telles que la création de sandbox, la définition de schémas et la gestion de jeux de données.

**Règle :** Dans [!DNL Experience Platform Launch]un cas, une règle est un ensemble de composants de règle définissant un ensemble spécifique de événements, de conditions et d’actions qui doivent être regroupés logiquement.

**Composant de règle :** Dans [!DNL Experience Platform Launch], les composants de règle sont les événements, les conditions et les actions qui constituent une règle.

**Exécution :** L’exécution spécifie un environnement d’exécution pour une recette d’apprentissage automatique. [!DNL Python], R, [!DNL Spark], PySpark et Tensorflow permettent d&#39;entrer une URL vers une image de docker pour une source de recettes.

[Retour au début](#adobe-experience-platform-glossary)

## S

**Exemple de données :** Les données d’exemple sont la prévisualisation d’un fichier de données, généralement les 100 premières lignes, qui permet à un chercheur en données de déterminer quel schéma ou quelles données se trouvent dans le fichier de données.

**Sandbox :** Un sandbox est une forme d’isolation des données virtuelles au sein d’une organisation d’utilisateurs sur [!DNL Experience Platform].

**Réinitialisation du sandbox :** Réinitialisation du sandbox, supprime toutes les données, y compris les données, les profils et les segments dans un sandbox. La réinitialisation du sandbox peut affecter les données connectées à des destinations internes ou externes.

**Commutateur sandbox :** Le contrôle sandbox dans [!DNL Experience Platform] permet aux utilisateurs de naviguer entre les sandbox auxquels ils ont accès. Le changement d’un sandbox modifiera tout le contenu et peut modifier l’accès aux fonctionnalités en fonction des autorisations.

**Planification :** La planification est une spécification définie par l’utilisateur sur la fréquence ou la cadence d’assimilation des données d’une source de données tierce à Adobe [!DNL Experience Platform].

**Scoring :** Le score est le processus de génération d’informations à partir de données à l’aide d’un modèle formé.

**Schéma :** Le Schéma est constitué d&#39;une classe et d&#39;un mixin facultatif et est utilisé pour créer des jeux de données et des flux de données. Un schéma comprend des attributs comportementaux, un horodatage, une identité, des définitions d’attributs et des relations.

**Descripteur de Schéma :** Le descripteur de Schéma est une métadonnée supplémentaire liée au schéma qui décrit le comportement qui peut être utilisé par [!DNL Experience Platform] pour comprendre le comportement de schéma prévu, tel que la relation entre deux schémas.

**Clé d&#39;accès secrète :** Une clé d’accès secrète est une clé [!DNL Amazon] S3 utilisée conjointement avec l’ID de clé d’accès pour signer les demandes AWS.

**Segment :** Un segment est un ensemble de règles qui incluent des attributs et des données de événement qui permettent à un certain nombre de profils de devenir une audience.

**Créateur de segments :** [!DNL Segment Builder] est l’environnement de développement visuel utilisé pour créer des définitions de segment et sert de composant commun à toutes les applications utilisant [!DNL Real-time Customer Profile] la segmentation sur [!DNL Experience Platform].

**Définition de segment :** La définition de segment est le jeu de règles utilisé pour décrire les principales caractéristiques ou le comportement d’une audience de cible. Une fois conceptualisée, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres d’audience admissibles pour un segment.

**Méthode d&#39;évaluation des segments :** L’évaluation planifiée des segments permet d’établir un calendrier récurrent pour l’exécution d’une tâche d’exportation à un moment précis, tandis que l’évaluation à la demande implique la création d’une tâche de segment pour créer immédiatement l’audience.

**Exportation de segments :** L’exportation de segments est l’un des deux types de destinations et envoie les profils qui remplissent les conditions requises et qui ont été mappés à la destination. Utilise des segments et des identifiants utilisateur et des données pseudonymes et s’intègre généralement aux réseaux sociaux et à d’autres plateformes de cible de médias numériques.

**ID de segment :** L’identifiant de segment est un identifiant généré automatiquement associé à un segment.

**Appartenance au segment :** L’appartenance au segment affiche le segment auquel un profil fait actuellement partie.

**Règles de segmentation :** Les règles de segmentation indiquent où et comment l’utilisateur définit ce que les profils qualifient pour le segment.

**Type de segment :** Il existe deux types de segments : L’un est un segment qui se met à jour dynamiquement avec [!DNL Experience Platform] les modifications de données, et l’autre est un instantané d’audience qui capture toutes les règles de segment de réunion de profils, et celles-ci ne changent pas.

**Segmentation :** La segmentation consiste à diviser un grand groupe de clients, de prospects ou de consommateurs en groupes plus petits qui partagent des attributs similaires et réagissent de la même manière aux stratégies marketing.

**Sensei ML Framework :** Sensei ML Framework est un cadre unifié d&#39;apprentissage automatique à travers Adobe qui utilise les données [!DNL Experience Platform] pour donner aux scientifiques des données les moyens de développer des services de renseignement basés sur l&#39;apprentissage automatique d&#39;une manière plus rapide, évolutive et réutilisable.

**Étiquettes de données sensibles :** Les libellés &quot;S&quot; sensibles sont utilisés pour classer les données jugées sensibles, par exemple les différents types de données comportementales ou géographiques que vous souhaitez marquer comme sensibles.

**Services :** Un cadre puissant pour rendre opérationnels les services d&#39;IA et de ML en exploitant les services intelligents Adobe. Les services offrent des expériences client personnalisées en temps réel ou rendent opérationnels des services intelligents personnalisés.

**Étiquette de données S1 :** `S1` l’étiquette de données est utilisée pour classifier les données spécifiant la latitude et la longitude qui peuvent être utilisées pour déterminer l’emplacement précis d’un périphérique.

**Étiquette de données S2 :** `S2` l’étiquette de données est utilisée pour classifier les données qui peuvent être utilisées pour déterminer une zone de géo-barrière définie de manière générale.

**Source :** La source est un terme général pour tout connecteur d’entrée dans le [!DNL Real-time Customer Data Platform].

**Attribut source :** Un attribut source est un champ du jeu de données source.  Les attributs source sont mappés aux champs de schéma de cible.

**Connecteur source :** Les connecteurs d’Adobe Experience Platform Source aident les utilisateurs à assimiler facilement des données provenant de plusieurs sources, ce qui leur permet de structurer, d’étiqueter et d’améliorer les données à l’aide de [!DNL Experience Platform Services]. Les données peuvent être ingérées à partir de diverses sources, telles que l’enregistrement cloud, les logiciels tiers et les systèmes de gestion de la relation client.

**Catégorie source :** Une catégorie source est un regroupement de sources [!DNL Real-time Customer Data Platform] présentant des caractéristiques similaires.

**Catalogue source :** Un catalogue source est une liste de sources disponibles dans le [!DNL Real-time Customer Data Platform].

**Espace de nommage d&#39;identité standard :** Les espaces de nommage d&#39;identité standard sont des identifiants prédéfinis Adobe, notamment les solutions standards Adobe et industrielles utilisées pour identifier les utilisateurs.

**Schéma standard :** Les schémas standard sont composés de classes et de mixins et sont destinés à être réutilisés.

**Ingestion en flux continu :** L’assimilation en flux continu fournit aux utilisateurs une méthode d’envoi en temps réel de données depuis les périphériques client et serveur [!DNL Experience Platform] .

**URL du point de terminaison de la diffusion en continu :** Une URL de point de terminaison de flux continu est un point de terminaison unique fourni par Adobe et lié à l’organisation IMS d’un client pour diffuser des données dans [!DNL Experience Platform].

**Segmentation en flux continu :** La segmentation en flux continu est un processus continu de sélection des données qui met à jour les segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données entrantes vers [!DNL Real-time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui garantit que votre audience de cible reste pertinente.

**Symbole :** Symbole est l&#39;abréviation d&#39;un espace de nommage d&#39;identité qui peut être utilisé comme référence dans les API.

**Vue système :** La Vue système est une représentation visuelle des jeux de données source qui transitent par [!DNL Real-time Customer Profile] les destinations.

[Retour au début](#adobe-experience-platform-glossary)

## T

**Fonctionnalités de la Cible :** La fonction de Cible est spécifiée dans le mappage des fonctionnalités est la fonction prédite par un modèle.

**Modèle formé :** Un modèle formé représente la sortie exécutable d&#39;un processus de formation de modèle, dans lequel un ensemble de données de formation a été appliqué à l&#39;instance de modèle. Un modèle formé conserve une référence à tout service Web intelligent créé à partir de celui-ci. Le modèle formé est adapté pour le score et la création d&#39;un service web intelligent. Les modifications apportées à un modèle entraîné peuvent être suivies en tant que nouvelle version.

**Jeton :** Un jeton est un type de sécurité d’authentification à deux facteurs qui peut être utilisé pour autoriser l’utilisation de services informatiques avec [!DNL Query Service].

**Type :** Le type est la classe de problème d&#39;apprentissage automatique pour laquelle une recette est conçue et est utilisée après la formation pour aider à personnaliser l&#39;évaluation de la course de formation.

[Retour au début](#adobe-experience-platform-glossary)

## u

**Schéma Union :** Le schéma d&#39;Union est une consolidation des schémas qui ont été activés pour [!DNL Real-time Customer Profile].

[Retour au début](#adobe-experience-platform-glossary)

## v

[Retour au début](#adobe-experience-platform-glossary)

## w

[Retour au début](#adobe-experience-platform-glossary)

## X

**XDM (modèle de données d’expérience) :** XDM (Experience Data Model) est le concept d’utilisation de schémas standard pour unifier les données à utiliser avec [!DNL Experience Platform] les applications Adobe Experience Cloud. XDM est une spécification formelle utilisée pour représenter toutes les données d&#39;expérience client dans un seul langage ou un modèle de données standard et normalise la structure des données et accélère et simplifie le processus d&#39;obtention de connaissances à partir de quantités massives de données.

**Événement de décision XDM :** Un événement décisionnel permet de recueillir des observations sur le résultat et le contexte d&#39;une activité de décision, y compris des renseignements sur la façon dont la décision a été prise, le moment où elle a eu lieu, les options proposées (et choisies) et l&#39;état contextuel qui a influé sur la décision ou qui a pu être observé pendant le processus de décision. DecisionEvents capture également l’ID de proposition, un identifiant unique global qui peut être utilisé pour corréler la décision à d’autres événements. Les événements de décision sont non seulement liés aux Événements d’expérience qui ont influé sur une décision, mais aussi aux événements d’expérience qui sont une réponse directe à une proposition. On s’attend à ce que les applications référencent l’ID de proposition dans chaque événement ExperienceEvent qui a été influencé par les propositions. L’historique proposition-réponse d’un profil individuel est conservé à l’aide des ID de proposition.

**XDM ExperienceEvent :** Un événement ExperienceEvent est un enregistrement factuel de ce qui s’est produit, y compris le moment et l’identité de la personne impliquée. ExpérienceEvents peut être explicite (actions humaines directement observables) ou implicite (élevée sans action humaine directe) et sont enregistrés sans agrégation ni interprétation. Elles sont essentielles pour l’analyse du domaine temporel, car elles permettent l’observation et l’analyse des changements qui surviennent dans une période donnée et la comparaison entre plusieurs périodes pour suivre les tendances.

**Profil individuel XDM :** Un MDM [!DNL Individual Profile] constitue une représentation singulière des attributs et des intérêts des individus identifiés et partiellement identifiés. Les profils moins identifiés peuvent contenir uniquement des signaux comportementaux anonymes, tels que des cookies de navigateur, tandis que les profils fortement identifiés peuvent contenir des informations personnelles détaillées telles que le nom, la date de naissance, l’emplacement et l’adresse électronique. À mesure qu&#39;un profil se développe, il devient un solide référentiel de renseignements personnels, d&#39;informations d&#39;identification, de coordonnées et de préférences de communication pour une personne.

**Système XDM :** XDM System est l&#39;infrastructure, la sémantique des données et le flux de travail dans [!DNL Experience Platform] lequel repose un schéma standard.

[Retour au début](#adobe-experience-platform-glossary)

## Y

[Retour au début](#adobe-experience-platform-glossary)

## Z

[Retour au début](#adobe-experience-platform-glossary)
