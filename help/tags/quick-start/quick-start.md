---
title: Guide de démarrage rapide
description: Découvrez comment vous familiariser rapidement avec les balises dans Adobe Experience Platform.
source-git-commit: 010e05968f1d7ad5675b0f0af43d9cfcc1f3a2ff
workflow-type: ht
source-wordcount: '1532'
ht-degree: 100%

---

# Guide de démarrage rapide

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les balises représentent la nouvelle génération de technologie de gestion des balises dʼAdobe Experience Platform. Elles sont conçues de toutes pièces de manière à prendre en charge un écosystème ouvert et durable, où chacun peut construire ses propres intégrations que les clients dʼAdobe peuvent déployer sur leurs sites. Il s’agit de la première application d’une API, donc tout ce que vous pouvez faire par le biais de l’interface utilisateur, vous pouvez également le faire par programmation via une API.

Worflow de balises de base :

1. Configuration de groupes et d’utilisateurs.
2. Connexion.
3. Création d’une propriété.
4. Installation d’extensions.
5. Création de règles et d’éléments de données.
6. Test dans votre environnement de développement.
7. Promotion de la production.

## 1. Configuration de groupes et d’utilisateurs

Les balises sont totalement intégrées à votre Adobe ID. Les autorisations utilisateur sont gérées via lʼAdmin Console avec dʼautres produits et solutions Adobe depuis [!DNL Creative Cloud], [!DNL Document Cloud] et Experience Cloud.

Les balises possèdent un système de gestion utilisateur basé sur les droits. Cela signifie que les droits individuels doivent être accordés explicitement. Ces droits sont octroyés aux groupes, puis les utilisateurs sont ajoutés aux groupes appropriés afin d’y avoir accès. Même si votre organisation a accès à lʼinterface utilisateur de la collecte de données, les utilisateurs individuels ne peuvent rien faire tant quʼun administrateur de lʼorganisation ne leur a pas explicitement accordé des droits.

Pour obtenir des instructions détaillées sur la création de groupes et lʼajout dʼutilisateurs pour les balises, consultez le document sur les [autorisations utilisateur](../ui/administration/user-permissions.md).

## 2. Connexion

Une fois les droits relatifs aux balises ajoutés à votre Adobe ID, vous devez vous connecter à lʼinterface utilisateur de la collecte de données. Pour ce faire, accédez directement à lʼ [écran de connexion Experience Cloud](https://experiencecloud.adobe.com), puis sélectionnez l’interface utilisateur de la collecte de données dans l’onglet Accès rapide.

>[!NOTE]
>
>Si vous disposez dʼun compte unique avec des droits auprès de plusieurs organisations, vous pouvez modifier lʼorganisation en sélectionnant son nom dans la barre de contrôle située en haut de lʼécran et en choisissant une autre organisation dans la liste déroulante.

## 3. Création d’une propriété

Une fois que vous êtes connecté à lʼinterface utilisateur de la collecte de données, la première étape consiste à créer une propriété. Une propriété est essentiellement un conteneur que vous remplissez avec des extensions, des règles, des éléments de données et des bibliothèques lorsque vous déployez des balises sur votre site. De nombreuses personnes créent une propriété pour chaque site web (ou groupe de sites étroitement liés) où elles souhaitent déployer le même ensemble de balises.

Pour plus d’informations sur la création de propriétés, reportez-vous à la section [Création d’une propriété](../ui/administration/companies-and-properties.md).

## 4. Installation d’extensions

Une extension est une intégration construite par Adobe ou un partenaire Adobe qui ajoute de nouvelles options inépuisables pour les balises que vous pouvez déployer sur vos sites. Si vous considérez une balise comme un système dʼexploitation, les extensions sont les applications que vous installez afin dʼeffectuer les actions spécifiques dont vous avez besoin.

Toutes les nouvelles propriétés sont dotées de l’ [extension Core](../extensions/web/core/overview.md). Les propriétés mobiles sont dotées d’extensions supplémentaires. Lʼextension Core est construite par Adobe afin de fournir un solide ensemble de types dʼéléments de données par défaut pour votre couche de données et de types dʼévénements pour vos règles. La plupart des actions que vous souhaitez effectuer (obtenir un ECID, envoyer des balises [!DNL Adobe Analytics], charger la mbox globale [!DNL Target], etc.) proviennent des extensions que vous installez depuis le catalogue.

Ce qui rend les balises de Platform vraiment uniques, ce sont les extensions que chacun peut construire. Vous souhaitez déposer un pixel de remarketing Facebook sur votre site ? Découvrez l’extension créée par Facebook. Vous souhaitez la même pour Twitter ou LinkedIn ? Utilisez ces extensions. Vous souhaitez réaliser une enquête ? Jetez un œil à Question Pro ou Foresee. Vous souhaitez gérer la confidentialité et le consentement de vos utilisateurs finaux pour les aider avec [!DNL GDPR] ? Allez voir du côté d’Evidon et de Trust Arc. Vous souhaitez avoir des informations granulaires sur le comportement des utilisateurs individuels de votre site ? Clicktale peut vous être utile. Pour plus d’informations, consultez la section sur l’ [ajout d’une nouvelle extension](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Création de règles et d’éléments de données

Les **éléments de données** sont des pointeurs vers les informations que vous souhaitez collecter et envoyer à différents endroits sur votre page :

* Couche de données définie en JSON
* Éléments DOM
* Cookies
* Stockage local et de session
* À peu près tout

Une fois lʼélément de données défini, vous pouvez lʼutiliser nʼimporte où dans lʼinterface utilisateur de la collecte de données pour nʼimporte quelle extension. Pour plus dʼinformations, voir la documentation sur les [Éléments de données](../ui/managing-resources/data-elements.md).

Les **règles** se rapportent au noyau logique de votre mise en œuvre et contrôlent tout ce qui concerne les balises de votre site. Définissez un événement, des conditions et des exceptions, puis les actions et l’ordre. Enfin, publiez vos modifications pour afficher les résultats. Pour plus d’informations, reportez-vous à la section [Règles](../ui/managing-resources/rules.md).

## 6. Test dans votre environnement de développement

### Bibliothèques et versions

Les versions de balise ne sont jamais publiées automatiquement. Chaque ensemble de modifications que vous apportez est encapsulé dans une [bibliothèque](../ui/publishing/libraries.md). Chaque bibliothèque que vous créez hérite automatiquement de tout ce qui se trouve en amont (publié, approuvé ou envoyé) comme ligne de base. Vous devez donc simplement définir les modifications que vous souhaitez apporter. Cette bibliothèque sert de plan directeur pour une [version](../ui/publishing/builds.md). Une version est l’ensemble de fichiers JavaScript déployés et utilisés.

Il est important de comprendre la relation entre votre page web, votre emplacement dʼhébergement et les balises.

1. Votre serveur hôte fournit un emplacement pour publier la version. La version elle-même contient les fichiers JavaScript requis par la bibliothèque.

   Chaque environnement possède une relation avec un hôte, et celui-ci fournit un point dʼentrée indiquant où diffuser la version. Lʼhôte ne peut appartenir quʼà une seule propriété, bien quʼune propriété puisse avoir de nombreux hôtes.

2. Un code incorporé est fourni dans la balise `<script>` de formulaire qui se trouve dans les sections `<head>` du code HTML de votre site web.

   Lorsque vous créez un environnement et que vous joignez un hôte, lʼenvironnement génère automatiquement un code incorporé unique qui vous permet dʼintégrer la version qui lui est attribuée dans votre site. Le code `<script>` est utilisé pour déployer la version de bibliothèque au moment de lʼexécution.

3. Lorsquʼun utilisateur parcourt votre site, la balise `<script>` de code incorporé récupère la version à partir du serveur hôte et exécute les actions que vous avez définies dans le navigateur.

### Hôtes

Un hôte constitue une connexion entre une propriété de balise et votre emplacement dʼhébergement. Les balises prennent actuellement en charge lʼhébergement géré par Adobe via un hôte [!DNL Akamai] ou lʼauto-hébergement via un hôte SFTP. Chaque fois que vous générez une version, les balises se connectent au serveur défini par votre hôte et transmettent la version.

Si vous utilisez lʼauto-hébergement, vous pouvez envoyer une version de balise directement vers vos serveurs via SFTP ou lʼenvoyer vers [!DNL Akamai] et la télécharger à lʼaide de lʼoption Archiver de votre environnement.

Pour plus d’informations, reportez-vous à la section [Hôtes](../ui/publishing/hosts/hosts-overview.md).

### Environnements

Chaque bibliothèque est créée dans un environnement. Un environnement définit la manière dont vous souhaitez que votre version apparaisse lorsqu’elle est publiée. Vous pouvez spécifier :

* **Héberger :** chaque environnement nécessite un hôte qui détermine le point dʼentrée vers lequel toutes les versions créées dans cet environnement seront envoyées.
* **Archiver :** le paramètre par défaut consiste à déployer votre version sous la forme dʼun fichier .js miniaturisé. Si vous utilisez un code personnalisé, plusieurs fichiers peuvent se référer les uns aux autres. Ces fichiers peuvent être combinés en un seul fichier zip et chiffrés.

Après avoir enregistré votre environnement, il génère le code incorporé que vous pouvez copier et coller dans votre site web. Veuillez noter que le code incorporé ne fonctionnera pas tant que vous nʼaurez pas créé une bibliothèque et produit une version. Pour plus d’informations, reportez-vous à la section [Environnements](../ui/publishing/environments.md).

### Publication d’une version pour développement

Suivez les étapes du processus de publication ci-dessous.

1. Créez un hôte.
1. créer un environnement de développement à l’aide de l’hôte que vous avez créé ;
1. déployer le code incorporé de votre environnement de développement vers votre site de test de développement ;
1. créer une bibliothèque et l’affecter à l’environnement de développement que vous avez créé ;
1. créer votre bibliothèque.

## 7. Promotion de la production

Après avoir testé votre version dans votre environnement de développement, assurez-vous de créer vos environnements dʼévaluation et de production et de placer les codes incorporés aux emplacements adéquats. Vous pouvez réutiliser des hôtes existants à cette fin.

La promotion d’une bibliothèque jusqu’à la production exige généralement une coordination entre différentes personnes disposant des droits appropriés.

* Un développeur (une personne disposant du droit de développement) envoie la bibliothèque, ce qui change l’état de la bibliothèque en Soumis.
* Un approbateur (une personne disposant du droit d’apporobation) peut créer la bibliothèque dans l’environnement d’étape et l’approuver après le test. L’état de la bibliothèque est ainsi changé en Approuvé. Une seule bibliothèque peut avoir à la fois les états Soumis et Approuvé.
* Un éditeur (une personne disposant du droit de publication) peut créer la bibliothèque dans l’environnement de production.

Vous pouvez octroyer tous ces droits à une même personne.

Pour plus d’informations sur les différents états et options disponibles pendant le processus de publication, reportez-vous à la section [Processus d’approbation](../ui/publishing/publishing-flow.md).

## Ressources supplémentaires

Pour en savoir plus sur les balises, consultez les ressources suivantes :

* **[Communauté de la collecte de données](https://forums.adobe.com/community/experience-cloud/platform/launch)** : posez vos questions et répondez à dʼautres, proposez des idées, votez pour les idées des autres. Connectez-vous avec votre Adobe ID.
* **[Documentation pour les développeurs](https://developer.adobelaunch.com/)** : participez à la communauté des développeurs de balises pour créer des extensions ou utiliser les API des balises.
* **[Présentation des tutoriels](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html?lang=fr)** : ces documents vous initient aux concepts des balises, notamment le transfert dʼévénements et le SDK mobile dans les applications Android.
