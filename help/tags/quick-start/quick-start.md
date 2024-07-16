---
title: Guide de démarrage rapide
description: Découvrez comment vous familiariser rapidement avec les balises dans Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 90%

---

# Guide de démarrage rapide

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les balises représentent la nouvelle génération de la technologie de gestion des balises d’Adobe Experience Platform. Elles sont conçues de zéro de manière à prendre en charge un réseau ouvert et durable, où chacun peut construire ses propres intégrations que les clients Adobe peuvent déployer sur leurs sites. Il s’agit de la première application d’une API, donc tout ce que vous pouvez faire par le biais de l’interface utilisateur, vous pouvez également le faire par programmation via une API.

Le workflow de base des balises :

1. Configuration de groupes et d’utilisateurs.
2. Connexion.
3. Création d’une propriété.
4. Installation d’extensions.
5. Création de règles et d’éléments de données.
6. Test dans votre environnement de développement.
7. Promotion de la production.

## 1. Configuration de groupes et d’utilisateurs

Les balises sont totalement intégrées à votre Adobe ID. Les autorisations utilisateur sont gérées via lʼAdmin Console avec dʼautres produits et solutions Adobe depuis [!DNL Creative Cloud], [!DNL Document Cloud] et Experience Cloud.

Les balises disposent dʼun système de gestion des utilisateurs basé sur les droits. Cela signifie que les droits individuels doivent être accordés explicitement. Ces droits sont octroyés aux groupes, puis les utilisateurs sont ajoutés aux groupes appropriés afin d’y avoir accès. Même si votre entreprise a accès à la collecte de données, les utilisateurs individuels ne peuvent rien faire tant qu’un administrateur ne leur a pas explicitement accordé certains droits.

Pour obtenir des instructions détaillées sur la création de groupes et l’ajout d’utilisateurs pour les balises, reportez-vous au [guide des autorisations de collecte de données](../../collection/permissions.md).

## 2. Connexion

Une fois les droits de balise ajoutés à votre Adobe ID, vous devez vous connecter à l’interface utilisateur de l’Experience Platform ou à l’interface utilisateur de collecte de données. Pour ce faire, accédez directement à l’[ écran de connexion de l’Experience Cloud](https://experience.adobe.com/) et sélectionnez **[!UICONTROL Collecte de données]** ou **[!UICONTROL Experience Platform]**.

>[!NOTE]
>
>Si vous disposez dʼun compte unique avec des droits auprès de plusieurs organisations, vous pouvez modifier lʼorganisation en sélectionnant son nom dans la barre de contrôle située en haut de lʼécran et en choisissant une autre organisation dans la liste déroulante.

## 3. Création d’une propriété

Une fois que vous êtes connecté à l’interface utilisateur, la première chose à faire est de créer une propriété. Une propriété est essentiellement un conteneur que vous remplissez avec des extensions, des règles, des éléments de données et des bibliothèques lorsque vous déployez des balises sur votre site. De nombreuses personnes créent une propriété pour chaque site web (ou groupe de sites étroitement liés) où elles souhaitent déployer le même ensemble de balises.

Pour plus d’informations sur la création de propriétés, reportez-vous à la section [Création d’une propriété](../ui/administration/companies-and-properties.md).

## 4. Installation d’extensions

Une extension est une intégration construite par Adobe ou ses partenaires qui ajoute de nouvelles options inépuisables pour les balises que vous pouvez déployer sur vos sites. Si vous considérez une balise comme un système dʼexploitation, les extensions sont les applications que vous installez afin de pouvoir effectuer les actions dont vous avez besoin.

Toutes les nouvelles propriétés sont dotées de l’ [extension Core](../extensions/client/core/overview.md). Les propriétés mobiles sont dotées d’extensions supplémentaires. Lʼextension Core est construite par Adobe afin de fournir un solide ensemble de types dʼéléments de données par défaut pour votre couche de données et de types dʼévénements pour vos règles. La plupart des actions que vous souhaitez effectuer (obtenir un ECID, envoyer des balises [!DNL Adobe Analytics], charger la mbox globale [!DNL Target], etc.) proviennent des extensions que vous installez depuis le catalogue.

Ce qui rend les balises de Platform vraiment uniques, ce sont les extensions que chacun peut construire. Vous souhaitez déposer un pixel de remarketing Facebook sur votre site ? Découvrez l’extension créée par Facebook. Vous souhaitez la même pour Twitter ou LinkedIn ? Utilisez ces extensions. Vous souhaitez réaliser une enquête ? Jetez un œil à Question Pro ou Foresee. Vous souhaitez gérer la confidentialité et le consentement de vos utilisateurs finaux pour les aider avec [!DNL GDPR] ? Allez voir du côté d’Evidon et de Trust Arc. Vous souhaitez avoir des informations granulaires sur le comportement des utilisateurs individuels de votre site ? Clicktale peut vous être utile. Pour plus d’informations, consultez la section sur l’ [ajout d’une nouvelle extension](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Création de règles et d’éléments de données

Les **éléments de données** sont des pointeurs vers les informations que vous souhaitez collecter et envoyer à différents endroits sur votre page :

* Couche de données définie en JSON
* Éléments DOM
* Cookies
* Stockage local et de session
* À peu près tout

Une fois l’élément de données défini, vous pouvez l’utiliser n’importe où dans l’interface utilisateur pour n’importe quelle extension. Pour plus d’informations, voir la documentation sur les [éléments de données](../ui/managing-resources/data-elements.md).

Les **règles** se rapportent au noyau logique de votre mise en œuvre et contrôlent tout ce qui concerne les balises de votre site. Définissez un événement, des conditions et des exceptions, puis les actions et l’ordre. Enfin, publiez vos modifications pour afficher les résultats. Pour plus d’informations, reportez-vous à la section [Règles](../ui/managing-resources/rules.md).

## 6. Test dans votre environnement de développement

### Bibliothèques et versions

Les versions de balise ne sont jamais publiées automatiquement. Chaque ensemble de modifications que vous apportez est encapsulé dans une [bibliothèque](../ui/publishing/libraries.md). Chaque bibliothèque que vous créez hérite automatiquement de tout ce qui se trouve en amont (publié, approuvé ou envoyé) comme ligne de base. Vous devez donc simplement définir les modifications que vous souhaitez apporter. Cette bibliothèque sert de plan directeur pour une [version](../ui/publishing/builds.md). Une version est l’ensemble de fichiers JavaScript déployés et utilisés.

Il est important de comprendre la relation entre votre page web, votre emplacement d’hébergement et les balises.

1. Votre serveur hôte fournit un emplacement pour la publication de la version. La version elle-même contient les fichiers JavaScript requis par la bibliothèque.

   Chaque environnement entretient une relation avec un hôte et l’hôte fournit un point d’entrée indiquant où diffuser la version. L’hôte ne peut appartenir qu’à une seule propriété, mais une propriété peut avoir de nombreux hôtes.

2. Un code incorporé est fourni dans la balise `<script>` de formulaire qui se trouve dans les sections `<head>` du code HTML de votre site web.

   Lorsque vous créez un environnement et joignez un hôte, l’environnement génère automatiquement un code incorporé unique qui vous permet d’intégrer la version qui lui est assignée dans votre site. Le code `<script>` est utilisé pour déployer la version de bibliothèque au moment de l’exécution.

3. Lorsqu’un utilisateur parcourt votre site, la balise `<script>` de code incorporé récupère la version à partir du serveur d’hébergement et exécute dans le navigateur les actions que vous avez définies.

### Hôtes

Un hôte est une connexion entre une propriété de balise et votre emplacement d’hébergement. Les balises prennent actuellement en charge l’hébergement géré par Adobe via un hôte [!DNL Akamai] ou l’auto-hébergement via un hôte SFTP. Chaque fois que vous générez une version, les balises se connectent au serveur défini par votre hôte et transmettent la version.

Si vous choisissez un auto-hébergement, une version de balise peut être poussée directement vers vos serveurs via SFTP; vous pouvez également la pousser vers [!DNL Akamai] avant de la télécharger à l’aide de l’option Archive de votre environnement.

Pour plus d’informations, reportez-vous à la section [Hôtes](../ui/publishing/hosts/hosts-overview.md).

### Environnements

Chaque bibliothèque est créée dans un environnement. Un environnement définit la manière dont vous souhaitez que votre version apparaisse lorsqu’elle est publiée. Vous pouvez spécifier :

* **Hôte :** chaque environnement a besoin d’un hôte qui détermine le point d’entrée où toutes les versions créées dans cet environnement seront poussées.
* **Archive :** le paramètre par défaut consiste à déployer votre version sous la forme d’un fichier .js miniaturisé. Si vous utilisez du code personnalisé, plusieurs fichiers peuvent s’y faire référence. Ils peuvent être combinés en un seul fichier zip et chiffrés.

Après avoir enregistré votre environnement, il génère le code incorporé que vous pouvez copier et coller dans votre site web. Veuillez noter que le code incorporé ne fonctionnera pas tant que vous n’aurez pas créé une bibliothèque et compilé une version. Pour plus d’informations, reportez-vous à la section [Environnements](../ui/publishing/environments.md).

### Publication d’une version pour développement

Voici une description des étapes du processus de publication.

1. Créez un hôte.
1. créer un environnement de développement à l’aide de l’hôte que vous avez créé ;
1. déployer le code incorporé de votre environnement de développement vers votre site de test de développement ;
1. créer une bibliothèque et l’affecter à l’environnement de développement que vous avez créé ;
1. créer votre bibliothèque.

## 7. Promotion de la production

Après avoir testé votre version dans votre environnement de développement, veillez à créer vos environnements d’évaluation et de production et à placer les codes incorporés aux emplacements nécessaires. Pour le faire, vous pouvez réutiliser des hôtes existants.

La promotion d’une bibliothèque jusqu’à la production exige généralement une coordination entre différentes personnes disposant des droits appropriés.

* Un développeur (une personne disposant du droit de développement) envoie la bibliothèque, ce qui change l’état de la bibliothèque en Soumis.
* Un approbateur (une personne disposant du droit d’apporobation) peut créer la bibliothèque dans l’environnement d’étape et l’approuver après le test. L’état de la bibliothèque est ainsi changé en Approuvé. Une seule bibliothèque peut avoir à la fois les états Soumis et Approuvé.
* Un éditeur (une personne disposant du droit de publication) peut créer la bibliothèque dans l’environnement de production.

Vous pouvez octroyer tous ces droits à une même personne.

Pour plus d’informations sur les différents états et options disponibles pendant le processus de publication, reportez-vous à la section [Processus d’approbation](../ui/publishing/publishing-flow.md).

## Ressources supplémentaires

Pour en savoir plus sur les balises, consultez les ressources suivantes :

* **[Communauté de la collecte de données](https://forums.adobe.com/community/experience-cloud/platform/launch)** : posez vos questions et répondez à celles des autres, proposez des idées, prononcez-vous sur les idées des autres. Connectez-vous avec votre Adobe ID.
* **[Developer Docs](../api/overview.md)** : participez à la communauté des développeurs de balises pour créer des extensions ou utiliser les API de balises.
* **[Présentation des tutoriels](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html?lang=fr)** : ces documents vous présentent les concepts de balises, y compris le transfert d’événement et le SDK mobile dans les applications Android.
