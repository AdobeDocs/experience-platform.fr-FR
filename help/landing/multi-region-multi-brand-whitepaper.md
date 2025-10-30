---
title: Adobe Experience Platform pour les entreprises multi-régions et multi-marques
description: Découvrez comment doter vos équipes d’implémentation des outils et des informations nécessaires pour naviguer efficacement parmi les subtilités de Adobe Experience Platform.
source-git-commit: 6e96cf7660a9a7fe1b4eaef645bca55ed89b7673
workflow-type: tm+mt
source-wordcount: '5322'
ht-degree: 1%

---


# Adobe Experience Platform pour les entreprises multi-régions et multi-marques

## Introduction

Adobe Experience Platform est à l’avant-garde des solutions transformatrices, ce qui vous permet de tirer pleinement parti du potentiel de vos données et contenus client. Avec Experience Platform, vous pouvez centraliser et normaliser les données de divers systèmes et tirer parti de la puissance de la science des données et du machine learning. Le résultat est une amélioration de la création et de la diffusion d’expériences personnalisées qui trouvent un écho auprès de vos clients.

Experience Platform vous permet de représenter la structure et de gérer vos données commerciales pour des implémentations évolutives et flexibles. L’implémentation des applications Platform est un parcours important qui nécessite une planification stratégique et des considérations minutieuses, en particulier si vous intervenez dans des domaines mondiaux, régionaux et spécifiques à une marque, ou une combinaison de tous ces aspects.

Ce livre blanc sert de référence, offrant un point de vue sur le produit et un ensemble de directives. Son principal objectif est de vous fournir, à vous et à vos équipes d’implémentation, les outils et les informations nécessaires pour naviguer efficacement parmi les subtilités d’Experience Platform. En fournissant un cadre structuré pour évaluer vos besoins spécifiques, vos considérations et vos cas d’utilisation réels, il vous dote des connaissances nécessaires pour libérer tout le potentiel d’Experience Platform et des applications basées sur des plateformes. En lisant les sections suivantes, vous trouverez des informations et des recommandations inestimables pour rationaliser le processus de mise en œuvre et améliorer la capacité de votre organisation à fournir des expériences exceptionnelles à votre audience tout en fournissant la gouvernance et les contrôles nécessaires pour maintenir la confidentialité et la conformité.

![Profil unifié CDP](./images/whitepaper/CDPoverview.png)

## Présentation de l’entreprise multi-marque et multi-région

Si vous exploitez une entreprise multi-marque et multi-région, vous avez probablement des exigences de gestion des données uniques pour Experience Platform. La compréhension de vos besoins spécifiques est essentielle pour adapter l’implémentation d’Experience Platform à vos besoins spécifiques.

Lors de l’exploration des options de déploiement, vous devez connaître et prendre en compte les personnes qui interagiront avec Experience Platform et les applications basées sur des plateformes. Concevoir leur expérience en fonction de leurs rôles et intérêts garantit une implémentation réussie. Voici trois personnages clés à prendre en compte lorsque vous explorez les options :

**Marie, la spécialiste marketing :**

- Objectif : acquisition de clients et personnalisation de l’expérience à grande échelle.
- Objectifs : Création de profils complets, amélioration de l’efficacité des médias.

**Ted, le technologue**

- Objectif : Gestion des données organisationnelles.
- Objectifs : assurer la conformité, gérer les silos de données, assurer la maintenance de divers secteurs d’activité.

**Dan, l’architecte de données**

- Focus : Précision et qualité des données.
- Objectifs : garantir la confidentialité et la confiance des données, concevoir des schémas et des modèles de données, gérer les sources de données.

### Une entreprise fonctionnant avec une isolation de données limitée

Un principe architectural clé dans Experience Platform est celui où les données client sont limitées à un sandbox de production spécifique en fonction des politiques et des exigences de gouvernance.

Si votre organisation a besoin d’un environnement de données unique pour exploiter votre expérience marketing à grande échelle, vous pouvez préférer consolider toutes vos données dans un seul sandbox Experience Platform avec des exigences minimales d’isolation des données. Dans cette configuration, les données sont ingérées dans un sandbox et toutes les identités associées sont représentées sous la forme d’un profil unifié unique, qu’il soit identifié par un pseudonyme ou une identité connue. Cela signifie que vos spécialistes marketing peuvent accéder à tous les attributs de profil et données d’événement d’expérience dans Experience Platform à travers votre entreprise. Elles peuvent utiliser ces données avec des applications basées sur des plateformes afin de créer des audiences et des parcours avec un besoin minimal d’empêcher les professionnels du marketing d’utiliser toutes les données, quelle que soit la marque ou la région. Cette approche facilite la segmentation transparente et l’activation des audiences dans les destinations prises en charge par les applications Experience Platform. Cette stratégie fonctionne bien si vous souhaitez exploiter l’ensemble de votre base de clients, quelles que soient les différences régionales ou spécifiques à la marque, pour des efforts marketing unifiés et cohérents.

![Sandbox de production unique avec architecture CDP](./images/whitepaper/Architecture-single-prod-sandbox.png)

#### Fonctionnement

Commençons par planifier l’implémentation et la configuration de votre environnement de niveau supérieur. Ensuite, vous allez décider du nombre de sandbox, de rôles et d’autorisations requis pour utiliser Experience Platform et les applications basées sur Platform de manière optimale pour votre entreprise.

##### Configuration générale de votre implémentation

- Configurez des sandbox pour permettre la création de profils client unifiés.
- Configurez des rôles et des contrôles d’accès pour administrer les sandbox et l’accès aux fonctionnalités pour chaque persona.
- Gérez le cycle de vie du développement avec un sandbox de développement et des outils sandbox.

**Sandbox**

Les sandbox constituent des partitions virtuelles au sein d’une instance d’Experience Platform unique, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience digitale. Tout le contenu et les actions réalisés dans un sandbox sont limités à celui-ci et n’en affectent aucun autre, y compris les données et l’accès aux données. Deux types de sandbox sont pris en charge sur Experience Platform :

- **Sandbox de production** : un sandbox de production est conçu pour être utilisé avec des profils dans votre environnement de production. Experience Platform vous permet de créer plusieurs sandbox de production afin de fournir les fonctionnalités de données appropriées tout en maintenant l’isolation opérationnelle.

- **Sandbox de développement** : un sandbox de développement peut être utilisé exclusivement à des fins de développement et de test avec des profils hors production.

Vous pouvez créer plusieurs sandbox de n’importe quel type. Pour ce type d’entreprise, nous utiliserons un sandbox de production et un sandbox de développement pour illustrer la manière d’exécuter et d’exploiter ce type d’entreprise.

![CDP-Créer un sandbox](./images/whitepaper/Create-sandbox.png)

Dans le sandbox de production, nous prévoyons que vous ingériez vos données de profil de production et d’événement d’expérience afin de créer un profil unifié pour vos activités marketing. Pour plus d’informations sur la manière de combiner des données connues et anonymes provenant de plusieurs sources d’entreprise afin de créer des profils client qui peuvent être utilisés pour fournir des expériences client personnalisées sur tous les canaux et appareils en temps réel, consultez la [documentation d’Adobe Real-Time Customer Data Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/rtcdp/home).

**Contrôles d’accès**

Vous pouvez définir des contrôles d’accès avec des rôles et des autorisations pour contrôler l’accès aux ressources de l’application en fonction du persona et de ses fonctionnalités requises. De plus, vous avez la possibilité de limiter l’accès à des champs spécifiques des données de profil. Vous devez effectuer cette étape en profondeur pour mieux gérer l’utilisation d’Experience Platform, des applications basées sur des plateformes et de vos données client.

Imaginez un ingénieur de données qui n’a pas besoin d’accéder à toutes les fonctionnalités d’Experience Platform et des applications basées sur des plateformes. Ils sont généralement chargés de créer des définitions de données (schémas), de configurer des sources de données pour ingérer des données et de créer des jeux de données. Cependant, ils peuvent ne pas être la même personne qui crée et active des audiences pour des expériences client personnalisées. Pour ce personnage, créez un rôle, ajoutez les autorisations appropriées et accordez l’accès uniquement aux fonctionnalités requises. En revanche, une personne spécialiste du marketing ne créerait pas de schémas et n’ingèrerait pas de données, mais se concentrerait plutôt sur la création et l’activation d’audiences pour permettre des expériences client personnalisées.

Si vous le souhaitez, envisagez d’ajouter des contrôles d’accès granulaires pour limiter l’accès à des champs spécifiques sur le profil client unifié avec la fonctionnalité de contrôle d’accès basé sur les attributs/contrôle d’accès au niveau du champ . Il s’agit de mécanismes de gouvernance dans Experience Platform qui vous permettent de restreindre l’accès aux attributs de données en fonction de libellés prédéfinis. Grâce au contrôle d’accès au niveau du champ, les données d’identification personnelle peuvent être régies et l’accès est limité à tous les workflows d’Experience Platform et d’applications. Pour plus d’informations sur les fonctionnalités de contrôle d’accès, consultez la [documentation sur le contrôle d’accès](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/home).

![Contrôles d’accès CDP, configuration des autorisations de rôle](./images/whitepaper/Access-Controls-Configure-RolePermissions.png)

**Cycle de vie du développement avec les sandbox de développement**

Un sandbox de développement se comporte de la même manière qu’un sandbox de production pour tous les aspects fonctionnels. C&#39;est différent en ce sens qu&#39;il y aura des mécanismes de sécurisation contractuels pour vous maintenir dans les limites de votre licence. Il est conçu exclusivement pour le développement et le test avec des profils hors production, prenant en charge jusqu’à 10 % de votre engagement de profil sous licence (mesuré de manière cumulée sur tous les sandbox de développement autorisés). Pour plus d’informations et pour connaître les mécanismes de sécurisation, consultez la [documentation de présentation des sandbox](https://experienceleague.adobe.com/fr/docs/experience-platform/sandbox/home) et la [page de descriptions des produits](https://helpx.adobe.com/fr/legal/product-descriptions.html) pour obtenir plus d’informations sur les droits.

Vous pouvez disposer de plusieurs sandbox de développement (jusqu’à 4 dans cet exemple d’entreprise, car nous utilisons un sandbox de production) pour le cycle de vie du développement et des tests.

**Exportation et importation de packages avec l’outil sandbox**

La fonctionnalité d’outils de sandbox permet aux utilisateurs disposant des autorisations appropriées de compresser leur travail à partir d’un sandbox de développement et de l’exporter vers un référentiel. Ce référentiel est accessible aux autres utilisateurs qui peuvent importer ces packages dans leurs sandbox désignés. Cette fonctionnalité garantit des configurations cohérentes entre les sandbox, ce qui facilite les processus d’exportation et d’importation transparents.

L’utilisation de l’outil sandbox améliore considérablement la précision de la configuration et réduit le temps nécessaire à la mise en œuvre. Il permet le déplacement efficace des configurations réussies entre différents sandbox.

Grâce à la fonction d’outil Sandbox, vous pouvez sélectionner différents objets et les exporter dans un package. Un package peut inclure un ou plusieurs objets, mais tous les objets doivent provenir du même sandbox.

**Automatisation des sandbox via les API**

Vous avez la possibilité d’utiliser les API Experience Platform pour automatiser les déploiements de sandbox et les tâches de configuration. Les API permettent un contrôle programmable pour les tâches répétitives telles que l’exportation, l’importation ou la modification des configurations de sandbox, offrant ainsi une certaine flexibilité si vous préférez les workflows automatisés.

Pour plus d’informations sur l’outil sandbox, consultez la [documentation sur l’outil sandbox](https://experienceleague.adobe.com/fr/docs/experience-platform/sandbox/ui/sandbox-tooling).

| ![CDP-Créer un package](./images/whitepaper/create-package.png) | ![Packages de liste CDP](./images/whitepaper/list-packages.png) |
| --- | --- |

### Isolation des données spécifiques à la région ou à la marque

Si vous avez besoin d’une isolation complète (par exemple, régionale ou basée sur une marque), vous pouvez fonctionner sous des politiques d’accès aux données strictes ou des exigences légales limitant l’accès de vos équipes de marque aux données spécifiques à leurs régions ou marques respectives. Vous définissez des modèles d’accès en fonction des données spécifiques à la région ou à la marque, garantissant ainsi la conformité aux protocoles internes, réglementaires et de gouvernance des données. Cette approche est essentielle si vous travaillez dans des secteurs fortement réglementés (p. ex., le traitement des données personnelles identifiables) ou si vous devez conserver des données distinctes et segmentées pour différentes régions géographiques ou identités de marque.

![Plusieurs sandbox de production avec architecture CDP](./images/whitepaper/Architecture-multiple-prod-sandbox.png)

#### Fonctionnement

Commençons par planifier votre implémentation, configurer votre environnement de niveau supérieur et décider du nombre de sandbox, de rôles et d’autorisations requis pour exploiter Experience Platform et les applications basées sur des plateformes de manière optimale pour votre entreprise.

##### Configuration générale pour une implémentation multi-sandbox

- Configurez plusieurs sandbox de production pour permettre la création de profils client unifiés dans chaque sandbox.

- Configurez des rôles et des contrôles d’accès pour administrer les sandbox et l’accès aux fonctionnalités pour chaque persona.

- Gérez le cycle de vie du développement avec l’outil sandbox.

- Création de rapports globale et activation (agrégation de données provenant de plusieurs sandbox pour obtenir des informations sur plusieurs organisations avec Customer Journey Analytics).

**Sandbox**

Contrairement à une configuration avec un seul sandbox de production, vous pouvez avoir besoin d’une approche plus complexe si vous avez besoin d’une isolation complète des données et des workflows. C’est là que plusieurs sandbox de production entrent en jeu, chacun représentant une unité d’isolement adaptée à vos besoins spécifiques.

Comme mentionné, chaque sandbox est une partition virtuelle au sein d’une instance de plateforme unique. Ces sandbox vous permettent de gérer vos données, workflows et processus dans un environnement contrôlé qui n’interfère pas avec les autres sandbox. Alors que les sandbox de développement sont destinés aux activités de test et de développement avec des profils hors production, les sandbox de production sont la colonne dorsale des opérations en direct, prenant en charge l’ingestion de données de production réelles pour les activités marketing en situation réelle.

Principaux avantages d’une isolation propre dans les sandbox de production :

1. **Gouvernance et conformité des données :** si vous travaillez dans des secteurs réglementés ou des régions appliquant des lois strictes en matière de confidentialité des données, vous devez vous assurer que les données d’une région ou d’une marque restent isolées. Plusieurs sandbox de production vous permettent de vous conformer aux exigences de gouvernance ou aux normes spécifiques du secteur en veillant à ce que les données ne soient accessibles que dans le sandbox approprié.

2. **Efficacité opérationnelle :** en isolant les données et les workflows, vous pouvez gérer vos opérations plus efficacement. Vos équipes responsables de différentes régions ou marques peuvent travailler indépendamment au sein de leurs sandbox dédiés, sans avoir à se soucier des fuites de données accidentelles ou des accès non autorisés.

3. **Workflows personnalisés :** vous pouvez personnaliser chaque sandbox de production en fonction des besoins spécifiques de votre région ou de la marque qu’elle représente. Vous pouvez ainsi implémenter des workflows personnalisés, des modèles de données et des stratégies marketing optimisés pour ce segment.

4. **Évolutivité :** au fur et à mesure de votre croissance, vous pouvez facilement créer des sandbox de production supplémentaires pour accueillir de nouvelles régions ou marques. Cette évolutivité garantit que la plateforme peut s’adapter à l’évolution de vos besoins sans compromettre l’intégrité des données ni les performances.

5. **Contrôle amélioré :** avec plusieurs sandbox de production, vos administrateurs disposent d’un contrôle précis sur les autorisations d’accès, l’ingestion des données et l’exécution des workflows. Vous pouvez ainsi adopter une approche plus sécurisée et organisée de la gestion des opérations complexes dans votre entreprise internationale.

**Contrôles d’accès**

Dans le contexte de plusieurs sandbox de production, les contrôles d’accès restent un composant essentiel de la gestion des données et des workflows dans Experience Platform. Cependant, la complexité augmente car vos administrateurs doivent s’assurer que les utilisateurs peuvent uniquement accéder aux sandbox appropriés à leurs rôles, tout en activant les opérations entre sandbox pour les utilisateurs qui en ont besoin, tels que vos équipes marketing couvrant plusieurs régions ou les ingénieurs de données responsables de l’ingestion des données globale et de la modélisation des données.

**Définition des rôles et des autorisations dans les sandbox :**

Comme dans le scénario sandbox de production unique, vous pouvez définir des politiques de contrôle d’accès avec des rôles et des autorisations adaptés aux besoins de différents rôles. Cependant, vous devez tenir compte de la manière dont ces rôles s’étendent sur différents sandbox dans un environnement multi-sandbox.

Par exemple :

- **Spécialistes marketing régionaux :** si vos spécialistes marketing exercent leurs activités dans plusieurs régions, il se peut que leurs rôles doivent s’étendre sur plusieurs sandbox. Vous pouvez leur accorder les autorisations nécessaires pour accéder aux ressources sur plusieurs sandbox tout en vous assurant que leur accès est toujours limité aux données et workflows appropriés dans chaque sandbox.

- **Ingénieurs de données :** les ingénieurs de données chargés de la création des modèles de données, de la définition des schémas et de la gestion de l’ingestion des données peuvent avoir besoin d’accéder à tous les sandbox. Vous pouvez concevoir leurs rôles pour leur permettre d’opérer sur l’ensemble de la plateforme tout en limitant leur accès aux seules fonctionnalités et données pertinentes pour leurs tâches. Par exemple, votre ingénieur de données travaillant sur les modèles de données pour l’Europe et l’Amérique du Nord peut accéder aux sandbox de production pour ces régions avec l’autorisation de modifier les schémas et d’ingérer des données. Cependant, ils ne pourraient pas accéder aux fonctions marketing, telles que la création et l’activation d’audiences.

**Considérations relatives au contrôle d’accès granulaire :**

Dans un environnement multi-sandbox, le contrôle d’accès granulaire devient encore plus critique. Le contrôle d’accès basé sur les attributs (contrôle d’accès au niveau du champ/contrôle d’accès au niveau de l’objet) vous permet de restreindre davantage l’accès à des champs de données spécifiques au sein des profils ou de certaines audiences, en veillant à ce que les informations sensibles ou d’identification personnelle soient protégées sur tous vos sandbox. Par exemple :

- Vous pouvez restreindre l’accès à certains champs de données d’un sandbox aux seuls utilisateurs de cette région. Cela permet de s’assurer que les informations d’identification personnelle ou les données sensibles ne sont visibles que par ceux qui en ont besoin, conformément aux réglementations de confidentialité et aux politiques de gouvernance internes.

- Pour les utilisateurs et utilisatrices disposant d’un accès entre sandbox, le contrôle d’accès basé sur les attributs garantit que même s’ils ou elles ont accès à plusieurs sandbox, leur visibilité sur les données sensibles est limitée par leur rôle et un besoin d’en connaître.

Avantages des contrôles d’accès basés sur les rôles et les attributs :

1. En contrôlant l’accès en fonction des rôles et des attributs, vous pouvez réduire considérablement le risque d’accès non autorisé aux données et vous assurer que seules les personnes disposant des autorisations appropriées peuvent afficher ou manipuler des informations sensibles.

2. Des rôles et des autorisations clairs et bien définis permettent de rationaliser les opérations, car chaque personne a accès aux fonctionnalités et aux données dont elle a besoin sans encombrement ni risque inutiles. Cette clarté permet des workflows efficaces et réduit le frottement.

3. Au fur et à mesure que votre entreprise se développe et évolue, les contrôles d’accès peuvent être ajustés pour s’adapter à de nouvelles régions, marques ou rôles. La possibilité de modifier l’accès sans interrompre les workflows existants est essentielle pour mettre à l’échelle vos opérations.

4. Les administrateurs peuvent conserver un contrôle centralisé sur tous les sandbox, ce qui garantit une cohérence dans la manière dont les contrôles d’accès sont appliqués dans l’ensemble de votre entreprise tout en permettant la personnalisation pour différentes régions ou marques.

**Cycle de vie du développement avec les sandbox de développement**

La gestion du cycle de vie du développement sur plusieurs régions et marques au sein d’Experience Platform nécessite une approche robuste qui garantit cohérence, efficacité et évolutivité. Les sandbox de développement prennent en charge le cycle de vie du développement dans un environnement complexe avec de nombreux sandbox de production. Ils sont améliorés par la fonctionnalité d’outils Sandbox, qui permet un partage et un déploiement de configuration transparents dans différents environnements.

Les sandbox de développement jouent un rôle essentiel dans le cycle de vie du développement. Ces sandbox fournissent un environnement isolé où les développeurs et les ingénieurs de données peuvent créer, tester et itérer sur des configurations sans affecter les données de production. Bien que fonctionnellement similaires aux sandbox de production, les sandbox de développement diffèrent, car ils sont destinés aux tests avec des profils hors production et sont régis par des limites contractuelles, telles que la prise en charge de jusqu’à 10 % de votre engagement de profil sous licence sur tous les sandbox de développement autorisés.

Vous pouvez créer plusieurs sandbox de développement pour prendre en charge différentes équipes ou régions. Cela permet à chacune de vos équipes de tester des workflows spécifiques à sa région ou à sa marque, en s’assurant que les environnements de production restent stables et sécurisés pendant le développement. Si vous disposez de nombreux sandbox de production, nous vous recommandons d’utiliser un pool de sandbox de développement pour prendre en charge plusieurs régions/marques.

**Exportation et importation de packages avec l’outil sandbox**

La fonctionnalité d’outil de sandbox est un outil puissant si vous gérez plusieurs sandbox. Il permet aux développeurs, aux ingénieurs de données et aux spécialistes du marketing de regrouper leur travail dans un sandbox de développement, y compris des schémas, des modèles de données et d’autres configurations, puis de les exporter vers un référentiel. À partir de là, d’autres utilisateurs peuvent accéder à ces packages et les importer dans leurs sandbox désignés, ce qui facilite le partage et le déploiement transparents de configurations réussies dans l’ensemble de l’entreprise.

Par exemple, votre ingénieur de données travaillant dans un sandbox de développement pour la région Amérique du Nord peut créer un schéma et le compresser avec toutes ses dépendances. Un autre ingénieur de données d’une autre région, comme l’Europe, peut accéder à ce package et l’importer dans son sandbox régional. Ce processus garantit la cohérence de la modélisation et de la configuration des données dans l’ensemble de votre entreprise, ce qui réduit le risque d’erreurs et améliore l’efficacité opérationnelle.

Avantages de l’outil Sandbox dans un environnement multi-sandbox :

1. L’outil Sandbox simplifie le cycle de vie du développement en permettant de partager facilement les configurations réussies entre plusieurs sandbox. Cela permet de réduire les redondances et de s’assurer que les bonnes pratiques sont mises en œuvre de manière cohérente dans toutes les régions ou marques.

2. La possibilité d’exporter et d’importer des packages dans différents sandbox améliore l’interopérabilité au sein de l’entreprise. Les équipes de différentes régions peuvent collaborer plus efficacement, en s’assurant que leurs configurations s’alignent sur les objectifs globaux de l’entreprise tout en répondant aux exigences régionales ou spécifiques à la marque.

3. À mesure que les entreprises se développent et ajoutent des sandbox pour s’adapter à de nouvelles régions ou marques, l’outil sandbox offre l’évolutivité nécessaire à la gestion efficace de ces environnements. Les nouveaux sandbox peuvent être rapidement configurés à l’aide de packages existants, ce qui accélère le processus d’intégration et réduit le temps nécessaire à la mise en ligne.

4. En regroupant les configurations et les dépendances dans un sandbox de développement, puis en les déployant dans des sandbox de production, les entreprises peuvent s’assurer que leurs configurations sont exactes et cohérentes sur l’ensemble du panorama. Cela réduit la probabilité d’erreurs et améliore la fiabilité globale de la plateforme.

5. Avec l’outil sandbox, la transition du développement à la production est fluide et contrôlée. Une fois les configurations testées et validées dans un sandbox de développement, elles peuvent être exportées et importées dans un sandbox de production, avec l’assurance qu’elles s’exécuteront comme prévu.

**Rapports globaux et activation**

Cela implique l’agrégation de données provenant de plusieurs sandbox pour obtenir des informations sur plusieurs organisations, nécessitant souvent un sandbox de création de rapports dédié pour l’intégration à Customer Journey Analytics.

Bien que l’approche de sandbox de production multiple offre clairement des avantages d’isolement pour les opérations régionales et spécifiques à la marque, elle introduit également des défis qui nécessitent des solutions créatives. L’un des principaux défis est la capacité à analyser les données sur les sandbox à des fins de création de rapports et de campagnes globales. Les entreprises ont souvent besoin de comprendre le parcours client à un niveau mondial, ce qui implique l’intégration de données provenant de plusieurs sandbox et l’activation d’efforts marketing entre sandbox. Nous décrivons ci-dessous les approches permettant de relever ces défis.

**Création de rapports globaux dans les sandbox**

Lorsqu’une entreprise fonctionne avec plusieurs sandbox de production, chacun représentant une région ou une marque, l’analyse des données client sur tous les sandbox devient complexe. Par exemple, la création d’une vue unifiée du parcours client sur différentes marques nécessite la consolidation des données de ces environnements isolés.

**Sandbox global dédié**

![Sandbox de création de rapports globaux dédiés à CDP](./images/whitepaper/dedicated-global-reporting-sandbox.png)

Ce sandbox agit comme un référentiel central où les données des sandbox individuels spécifiques à une région ou à une marque sont consolidées. Une solution courante consiste à utiliser Query Service dans chaque sandbox pour extraire les données client pertinentes. Cela peut inclure des profils et des événements d’expérience qui doivent être analysés pour différentes régions ou marques. Une fois les données préparées à partir de chaque sandbox, elles sont ingérées dans le sandbox de reporting global pour analyse et création d’audiences.

Utilisez Customer Journey Analytics pour effectuer une analyse cross-marché et cross-marque sur les données agrégées dans le sandbox global afin d’obtenir une vue complète des interactions client sur toutes les marques et régions. Cela leur permet de générer des informations précieuses, telles que l’identification des clients qui interagissent avec plusieurs marques et la création d’audiences inter-marques ou inter-régions. Ces informations peuvent être utilisées à diverses fins, notamment pour activer des stratégies marketing, personnaliser les expériences client et stimuler la croissance de l’entreprise.

**Partage d’audiences**

Le sandbox global permet également aux équipes marketing internationales de définir et de gérer des audiences à plus grande échelle. À l’aide des outils de sandbox, ces audiences globales (définitions uniquement, et non données) peuvent être exportées du sandbox global vers des sandbox individuels de marque ou régionaux, ce qui permet aux équipes marketing locales de les évaluer et de les activer dans leurs marchés respectifs.

En outre, vous pouvez utiliser la correspondance de segments Experience Platform, une fonctionnalité de Platform qui permet le partage de segments entre sandbox (audience qualifiée) entre différentes entités organisationnelles ou commerciales.

Ce service de partage de segments permet à deux utilisateurs ou plus d’échanger des données de segment de manière sécurisée, contrôlée et respectueuse de la vie privée.

Pour plus d’informations sur la fonction Correspondance de segments, consultez la [documentation sur la correspondance de segments](https://experienceleague.adobe.com/fr/docs/experience-platform/segmentation/ui/segment-match/overview).

### Combinaison d’approches pour les opérations mondiales, régionales et spécifiques à la marque

De nombreuses entreprises multi-marques opèrent à l&#39;échelle mondiale et, à ce titre, recherchent souvent un mélange d&#39;approches de gestion des données à la fois unifiées et isolées. Dans ce scénario, ils cherchent à séparer les données pour plusieurs régions ou pays. Les marques au sein de l’organisation peuvent s’attendre à opérer exclusivement sur les données associées à leur marque spécifique, le tout dans les mêmes limites de données d’une zone géographique ou d’un pays. Cette approche permet une gestion centralisée des données au niveau régional ou national tout en facilitant le marketing et les opérations de données spécifiques à la marque. Il s’agit d’un modèle qui combine les avantages d’une gestion unifiée des données avec la nécessité d’une isolation propre à la marque et à la région.

Reconnaissant ces différentes exigences, Experience Platform peut être configuré pour vous fournir une solution de gestion des données hautement adaptable et flexible, afin que les entreprises multi-marques et multi-régions puissent représenter efficacement votre entreprise au sein de la plateforme. Que l’objectif soit d’optimiser les données clients collectives, de maintenir une isolation stricte des données ou d’atteindre un équilibre entre les deux, Experience Platform est équipé pour répondre aux divers besoins de votre entreprise.

![CDP-Architecture : une approche mixte](./images/whitepaper/Architecture-blend-sandbox.png)

#### Fonctionnement

Commençons par planifier votre implémentation, configurer votre environnement de niveau supérieur et décider du nombre de sandbox, de rôles et d’autorisations requis pour exploiter de manière optimale Experience Platform et les applications basées sur des plateformes pour cette entreprise.

##### Configuration générale pour cette entreprise

- Configurez plusieurs sandbox de production pour permettre la création de profils client unifiés.

- Configurez des rôles et des contrôles d’accès pour administrer les sandbox et l’accès aux fonctionnalités pour chaque persona.

- Configurer le contrôle d’accès basé sur les attributs : contrôle d’accès au niveau du champ/au niveau de l’objet pour des contrôles granulaires sur les attributs de profil et les audiences.

- Gérez le cycle de vie du développement avec les sandbox de développement et les outils sandbox.

- Création de rapports globaux.

**Sandbox**

Configurez un sandbox par marque/région. Reportez-vous aux sections ci-dessus pour créer plusieurs sandbox de production.

**Contrôles d’accès**

Rôles et autorisations utilisateur :

- Créez le rôle « **Professionnel du marketing - Global** » et accordez les autorisations de création, d’affichage et de gestion des audiences. En outre, ce rôle sera autorisé à afficher toutes les données client.

- Créez des rôles et accordez l’accès uniquement à certaines fonctionnalités pour la personne appropriée. Par exemple, les rôles utilisateur « **Marketer—Germany** » et « **Marketer—France** » n’obtiendraient l’autorisation de créer, d’afficher et de gérer les audiences que sur la base des données par pays, grâce à une combinaison de contrôle d’accès au niveau du champ, de contrôle d’accès au niveau de l’objet et d’audiences par défaut.

- Créez le rôle « **Technologue - Global** » et accordez les autorisations appropriées pour créer et gérer des schémas, des jeux de données, des politiques, des sources, etc. Ce rôle serait responsable de toute l’administration et des configurations nécessaires.

###### Conception de schéma et contrôle d’accès basé sur les attributs : contrôle d’accès au niveau du champ

**Modèle de données d’expérience (XDM)**

Schéma de données normalisé dans Experience Platform qui garantit une structure de données cohérente et l’interopérabilité entre toutes les applications basées sur la plateforme.

**Contrôle d’accès basé sur les attributs : contrôle d’accès au niveau du champ et option de modélisation des données :**

- Créez un modèle de données pour inclure des champs XDM (PII) spécifiques au client qui doivent être limités pour chaque pays.

- Créez et appliquez des libellés de pays aux champs XDM. Libellés = Allemagne, France, Irlande, Pays-Bas, etc.

- Ajoutez des libellés au rôle approprié. Par exemple, ajoutez le libellé Allemagne au rôle « Spécialiste marketing - Allemagne ».

Schéma de profil individuel XDM :

```
\- PII
\- Germany
    \- name --> Label: "Germany"
    \- email --> Label: "Germany"
    \- birthdate --> Label: "Germany"

\- France
    \- name --> Label: "France"
    \- email --> Label: "France"
    \- birthdate --> Label: "France"

\- Netherland
    \- name --> Label: "Netherland", "Germany"
    \- email --> Label: "Netherland", "Germany"
    \- birthdate --> Label: "Netherland", "Germany"

\- Loyalty
    \- member
    \- registrationDate
```

###### Audiences : utilisez le contrôle d’accès basé sur les attributs : contrôle d’accès au niveau de l’objet pour contrôler l’accès aux audiences spécifiques à la marque ou au pays

**Contrôle d’accès basé sur les attributs : contrôle d’accès au niveau de l’objet pour les audiences :**

- Créez des audiences et contrôlez qui peut les afficher.

- Créez et appliquez des libellés de pays aux audiences. Libellés = Allemagne, France, Irlande, Pays-Bas, etc.

- Ajoutez des libellés au rôle approprié. Par exemple, ajoutez le libellé « Allemagne » au rôle « Spécialiste marketing - Allemagne ».

![Audiences libellées CDP](./images/whitepaper/label-audience.png)

###### Incluez une audience par défaut lors de la création d’audiences spécifiques à une marque ou un pays

**Audience par défaut : alternative au contrôle d’accès au niveau des lignes :**

- Actuellement, le créateur d’audiences vous permet d’inclure des audiences existantes en tant que blocs de création dans votre processus de création d’audiences.

- Le résultat serait dérivé de l’audience, suivi des attributs et des événements.

- Il n’existe aucun mécanisme pour ajouter automatiquement une ou plusieurs audiences au moment de la composition.

![CDP-Ajouter une audience par défaut](./images/whitepaper/default-audience.png)

###### Activation et filtrage des profils au niveau de la marque/du pays

**Option de politique de consentement personnalisée :**

Vous pouvez ainsi contrôler ou filtrer les profils au moment de l’activation :

- Créez une action marketing.

- Créez une destination et associez l’action marketing.

- Créez une politique de consentement personnalisée.

>[!NOTE]
>
> Le SKU de Privacy and Security Shield est nécessaire pour créer des politiques de consentement.

![Politique de consentement et filtrage des activations personnalisés CDP](./images/whitepaper/custom-consent-policy.png)

Complexité de la politique de consentement et d’activation multimarque :

La gestion de l’activation des audiences sur plusieurs marques nécessite une gouvernance détaillée des politiques de consentement, afin de s’assurer que les exigences uniques de chaque marque sont satisfaites. En outre, Adobe Privacy and Security Shield (une fonctionnalité de conformité d’Experience Platform qui applique les politiques de protection des données et assure l’alignement de la réglementation sur divers canaux d’activation) peut imposer des limites spécifiques sur la manière dont les politiques de consentement sont appliquées sur différents canaux d’activation. Vous devez évaluer attentivement ces considérations et mettre en œuvre des cadres de gouvernance pour maintenir la conformité et l’efficacité opérationnelle.

Vous devez également vous familiariser avec les complexités liées aux configurations de politique de consentement et aux activations spécifiques aux canaux. La définition explicite des politiques de consentement pour chaque région ou marque et la gestion cohérente de ces configurations sont essentielles à la conformité et à l’efficacité opérationnelle.

## Considérations générales

Dans certains scénarios, vous pouvez choisir de déployer des applications Experience Platform et basées sur des plateformes sur plusieurs ID d’organisation plutôt que d’utiliser un seul ID d’organisation avec de nombreux sandbox. Cette approche peut présenter des avantages en termes de résidence des données, de sécurité et d’administration, mais elle ajoute également de la complexité. Voici les principales considérations à prendre en compte pour déterminer quand une approche multi-organisation peut être appropriée.

### Qu’est-ce qu’un identifiant d’organisation ?

- Un ID d’organisation correspond à l’implémentation Adobe de Federated ID et du protocole OAuth 2.0.

- Un identifiant d’organisation est un ensemble de toutes les applications, utilisateurs et autorisations auxquels une organisation a droit en vertu des conditions contractuelles d’Adobe.

- Les comptes utilisateur et les autorisations sont gérés via l’Admin Console de chaque organisation.

- Les identifiants d’organisation régissent également la manière dont les solutions Adobe interagissent les unes avec les autres. Les solutions d’une même organisation peuvent être interopérables.

- En règle générale, un identifiant d’organisation est déployé dans une seule zone géographique.

![Option Plusieurs organisations IMS avec architecture CDP](./images/whitepaper/Architecture-multi-imsorg.png)

**Plusieurs ID d’organisation : avantages et considérations&#x200B;**

| Avantages | Considérations |
| -------- | -------------- |
| Vous trouverez ci-dessous une liste des avantages liés à l’utilisation de plusieurs ID d’organisation : <ul><li>Flexibilité pour stocker des données dans des régions mondiales particulières.</li><li>&#x200B;Connexions utilisateur distinctes par instance : en d’autres termes, Wholefoods ne peut pas se connecter à Audible&#x200B;</li><li>Des points d’entrée d’API dédiés qui permettent à chaque marché/unité opérationnelle de créer des connexions personnalisées selon les besoins dans son propre environnement&#x200B;</li><li>Chaque unité opérationnelle possède ses propres clés gérées par le client&#x200B;.</li><li>Les demandes RGPD peuvent être effectuées par unité opérationnelle&#x200B;.</li><li>Stockage et calcul totalement isolés entre les unités commerciales&#x200B;.</li><li>Réduit certaines barrières/limites de performances au niveau de l’organisation&#x200B;.</li><li>Plus de flexibilité avec la configuration et le mélange des SKU entre les unités commerciales. Par exemple, une organisation peut avoir un SKU de Adobe Journey Optimizer différent d’une autre organisation.</li></ul> | Voici quelques éléments à prendre en compte lorsque vous disposez de plusieurs ID d’organisation : <ul><li>Plusieurs ID d’organisation à gérer, au lieu d’un seul&#x200B;</li><li>Plusieurs instances/environnements distincts à gérer (intégrations, chargements de données, etc.).</li><li>&#x200B;Les ECID seront uniques par organisation, ce qui rend difficile la mise en correspondance des données entre les unités commerciales&#x200B;.</li><li>Devrait migrer/réimplémenter Analytics et Target par organisation - perdrait le cumul global (s’il est actuellement utilisé). &#x200B;</li><li>Une orchestration plus importante est nécessaire pour effectuer les demandes RGPD entre les unités commerciales&#x200B;.</li><li>Certaines intégrations d’applications basées sur Experience Platform stockent des métadonnées au niveau de l’organisation. Tout n’est pas « en sandbox » par les sandbox&#x200B;</li><li>L’ID d’organisation est épinglé sur une région. L’emplacement d’hébergement d’Adobe AWS se trouve actuellement aux États-Unis uniquement. Adobe ne prend pas en charge la migration d’une région d’hébergement vers une autre&#x200B;</li><li>Edge ne prend pas en charge le sandbox (pour le transfert d’événement).</li></ul> |

**ID d’organisation unique : avantages et considérations**

![Plusieurs sandbox de production avec architecture CDP](./images/whitepaper/Architecture-multiple-prod-sandbox.png)

| Avantages | Considérations |
| -------- | -------------- |
| Vous trouverez ci-dessous une liste des avantages liés à l’utilisation d’un identifiant d’organisation unique : <ul><li>Fournissez des sandbox individuels pour créer une séparation logique entre les unités opérationnelles au sein d’une région déployée</li><li>ID d’organisation unique à gérer par le service informatique pour les utilisateurs, le provisionnement, etc.</li><li>Aucune migration des balises Adobe, de Target, d’Analytics, etc., si vous conservez le même ID d’organisation.</li><li>Aucune réinitialisation n’est requise pour les ECID existants. Cela empêche l’« altération » des données Adobe Analytics.</li><li>Connexion unique pour les ressources marketing globales.</li><li>Les droits d’accès des utilisateurs et utilisatrices permettent de contrôler qui a accès à quels sandbox, avec des niveaux appropriés de contrôle d’accès en fonction du rôle.</li><li>Tirez parti des instances Global Analytics et Target et des données des suites de rapports.</li></ul> | Voici quelques éléments à prendre en compte lorsque vous disposez d’un identifiant d’organisation unique : <ul><li>Les données seront stockées dans une seule région.</li><li>Besoin potentiel de consolider les données en un seul identifiant d’organisation.</li><li>Toutes les unités opérationnelles partageraient la même infrastructure entre les applications (Experience Platform de base, Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics).</li><li>Mécanismes de sécurisation : certains sont globaux par organisation, comme la segmentation en flux continu, qui est de 1,5 000 RPS.</li><li>Les requêtes RGPD fonctionnent au niveau de l’organisation et ne peuvent pas être ciblées sur des sandbox spécifiques.</li><li>Les clés gérées par le client sont définies au niveau de l’ID d’organisation. Avec cette approche, toutes les sandbox des unités opérationnelles partageraient la même clé de chiffrement.</li><li>Il faudra clarifier les licences d’entreprise dans DX et CC pour s’assurer que les applications sont configurées avec les ID d’organisation appropriés.</ul></li> |

**Avantages et considérations**

Plusieurs ID d’organisation régissent l’accès des utilisateurs et utilisatrices, les droits et la ségrégation des données au niveau de l’organisation par rapport à un ID d’organisation unique, qui régit au niveau du sandbox.

| Scénario/Exigence | Plusieurs ID d’organisation | Plusieurs sandbox (identifiant d’organisation unique) |
| ----------------------------------- | --------------------------------------------------- | ----------------------------------------------- |
| Résidence des données | Isolation complète et ID d’organisation spécifiques à une région | Déploiement sur une seule région |
| Gouvernance et isolation des données | Séparation complète et isolement | Isolation opérationnelle, identifiant d&#39;organisation partagé |
| Gestion de la conformité (ex. : RGPD) | Requêtes distinctes par ID d’organisation | Une requête unique s’applique à tous les sandbox |
| Coût de l’infrastructure et licences | Potentiellement plus élevé en raison d’une configuration dupliquée | Généralement plus faible avec une administration centralisée |
| Rapports globaux et activation | Défis dus à des environnements isolés | Création de rapports et activation inter-régions facilitées |
| Complexité administrative | Supérieur en raison de plusieurs identifiants d’organisation isolés | Administration centralisée et réduite |

## Conclusion sommaire

Experience Platform fournit aux entreprises un cadre robuste pour centraliser, gérer et activer les données clients sur des modèles commerciaux multi-marques et multi-régions. Ce livre blanc a exploré les principales stratégies de déploiement, les modèles de gouvernance et les bonnes pratiques pour optimiser l’implémentation d’Experience Platform pour les organisations présentant des besoins opérationnels et d’isolement des données variables.

## Principaux points à retenir

1. **Modèles de déploiement flexibles**

   - Les entreprises peuvent choisir entre des approches **à sandbox unique, multi-sandbox ou hybrides** en fonction de leurs exigences opérationnelles, de conformité et de gouvernance.

   - **organisations internationales** peuvent avoir besoin de plusieurs sandbox de production pour se conformer aux exigences de gouvernance tout en maintenant l’efficacité opérationnelle.

2. **Gouvernance des données et contrôle d’accès**

   - **Le contrôle d’accès basé sur les attributs, le contrôle d’accès au niveau du champ et le contrôle d’accès au niveau de l’objet** permettent une gouvernance précise de l’accès aux données.

   - Vous devez définir **des rôles et des autorisations clairs** pour différentes personnes (par exemple, les spécialistes marketing, les architectes des données et les équipes informatiques) afin de garantir une utilisation appropriée des données.

3. **Automatisation et outils des sandbox**

   - **L’outil Sandbox** simplifie la gestion des configurations et permet aux équipes d’exporter et d’importer efficacement des paramètres.

   - L’**automatisation basée sur les API** est une option disponible pour les entreprises qui cherchent à rationaliser les déploiements de sandbox et la gouvernance à grande échelle.

4. **Rapports globaux et stratégies d’activation**

   - Les entreprises qui utilisent **Customer Journey Analytics** doivent tenir compte de la synchronisation des données et des implications commerciales lors de la consolidation des rapports globaux.

   - La **Correspondance de segments** fournit un mécanisme conforme à la confidentialité pour le partage d’audiences entre sandbox, assurant ainsi des activations marketing transparentes.

5. **Considérations relatives aux ID multi-organisations et aux sandbox**

   - Vous devez évaluer soigneusement s’il convient de déployer **plusieurs ID d’organisation ou plusieurs sandbox** en fonction de la résidence des données, de la conformité et des besoins opérationnels.

   - Les **identifiants d’organisation** offrent une isolation complète **&#x200B; tandis que les configurations multi-sandbox offrent une flexibilité opérationnelle dans un cadre de gouvernance partagé**.

## Réflexions finales

À mesure que les entreprises développent leurs fonctionnalités d’expérience digitale, Experience Platform sert de plateforme fondamentale pour stimuler le marketing piloté par les données, l’intelligence client et les activations cross-canal. Une implémentation réussie nécessite une planification minutieuse de la **gouvernance des sandbox, des politiques de conformité et des workflows opérationnels** afin d’assurer l’efficacité et l’évolutivité à long terme.

En tirant parti des bonnes pratiques décrites dans ce livre blanc, vous pouvez **optimiser Experience Platform pour les opérations multi-marques et multi-régions** afin d’assurer une gestion des données transparente, la conformité et des expériences client personnalisées à grande échelle.

## Accusé de réception

Ce livre blanc a été élaboré à partir des informations et des commentaires d’experts en la matière de différentes équipes, afin d’assurer l’exactitude, la clarté et les conseils pratiques. Nous remercions tous nos collègues de leur contribution et de leur examen précieux. Leur expertise a permis d’affiner ce document afin de mieux servir les entreprises mettant en œuvre Adobe Experience Platform dans des environnements multi-marques et multi-régions.
