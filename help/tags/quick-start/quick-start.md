---
title: Guide de démarrage rapide
description: Découvrez comment utiliser rapidement les balises dans Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 45%

---

# Guide de démarrage rapide

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les balises sont Adobe Experience Platform qui  la nouvelle génération de la technologie de gestion des balises. Il est conçu de toutes pièces pour prendre en charge un écosystème ouvert et durable où chacun peut construire ses propres intégrations que les clients Adobe peuvent déployer sur leurs sites. Il s’agit de la première application d’une API, donc tout ce que vous pouvez faire par le biais de l’interface utilisateur, vous pouvez également le faire par programmation via une API.

Processus des balises de base :

1. Configuration de groupes et d’utilisateurs.
2. Connexion.
3. Création d’une propriété.
4. Installation d’extensions.
5. Création de règles et d’éléments de données.
6. Test dans votre environnement de développement.
7. Promotion de la production.

Pour obtenir une vidéo d’introduction, reportez-vous à la documentation [vidéos d’introduction](videos.md) .

## 1. Configuration de groupes et d’utilisateurs

Les balises sont entièrement intégrées à votre Adobe ID. Les autorisations d’utilisateur sont gérées par l’intermédiaire du Admin Console avec d’autres produits et solutions d’Adobe provenant de [!DNL Creative Cloud], [!DNL Document Cloud] et de l’Experience Cloud.

Les balises disposent d’un système de gestion des utilisateurs basé sur les droits. Cela signifie que les droits individuels doivent être accordés explicitement. Ces droits sont octroyés aux groupes, puis les utilisateurs sont ajoutés aux groupes appropriés afin d’y avoir accès. Même si votre entreprise a accès à l’interface utilisateur de collecte de données, les utilisateurs individuels ne peuvent rien faire tant qu’un administrateur de l’organisation ne leur a pas explicitement accordé certains droits.

Pour obtenir des instructions détaillées sur la création de groupes et l’ajout d’utilisateurs pour les balises, reportez-vous au document [autorisations utilisateur](../ui/administration/user-permissions.md) .

## 2. Connexion

Une fois les droits de balise ajoutés à votre Adobe ID, vous devez vous connecter à l’interface utilisateur de la collecte de données. Pour ce faire, accédez directement à l’[écran de connexion Experience Cloud](https://experiencecloud.adobe.com), puis sélectionnez **[!UICONTROL Lancer / Collecte de données]** dans l’onglet Accès rapide .

>[!NOTE]
>
>Si vous disposez d’un compte unique avec des droits sur plusieurs organisations, vous pouvez modifier l’organisation en sélectionnant le nom de l’organisation dans la barre de contrôle située en haut de l’écran et en choisissant une autre organisation dans la liste déroulante.

## 3. Création d’une propriété

Une fois que vous êtes connecté à l’interface utilisateur de la collecte de données, la première chose à faire est de créer une propriété. Une propriété est essentiellement un conteneur que vous remplissez avec des extensions, des règles, des éléments de données et des bibliothèques lorsque vous déployez des balises sur votre site. De nombreuses personnes créent une propriété pour chaque site web (ou groupe de sites étroitement liés) où elles souhaitent déployer le même ensemble de balises.

Pour plus d’informations sur la création de propriétés, reportez-vous à la section [Création d’une propriété](../ui/administration/companies-and-properties.md).

## 4. Installation d’extensions

Une extension est une intégration construite par Adobe ou un partenaire d’Adobe qui ajoute de nouvelles options inépuisables pour les balises que vous pouvez déployer sur vos sites. Si vous considérez une balise comme un système d’exploitation, les extensions sont les applications que vous installez pour effectuer les tâches spécifiques dont vous avez besoin.

Toutes les nouvelles propriétés sont dotées de l’ [extension Core](../extensions/web/core/overview.md). Les propriétés mobiles sont dotées d’extensions supplémentaires. L’extension Core est construite par Adobe afin de fournir un solide ensemble par défaut de types d’éléments de données pour votre couche de données et de types d’événements pour vos règles. La plupart des actions que vous souhaitez effectuer (obtenir un ECID, envoyer des balises [!DNL Adobe Analytics], charger la mbox globale [!DNL Target], etc.) proviennent des extensions que vous installez depuis le catalogue.

Ce qui rend les balises de Platform vraiment uniques, c’est que ces extensions peuvent être créées par n’importe qui. Vous souhaitez déposer un pixel de remarketing Facebook sur votre site ? Découvrez l’extension créée par Facebook. Vous souhaitez la même pour Twitter ou LinkedIn ? Utilisez ces extensions. Vous souhaitez réaliser une enquête ? Jetez un œil à Question Pro ou Foresee. Avez-vous besoin de gérer la confidentialité et le consentement de vos utilisateurs finaux pour les aider avec [!DNL GDPR] ? Allez voir du côté d’Evidon et de Trust Arc. Souhaitez-vous obtenir des informations détaillées sur le comportement des utilisateurs individuels de votre site ? Clicktale peut vous être utile. Pour plus d’informations, reportez-vous à la section [Ajout d’une nouvelle extension](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Création de règles et d’éléments de données

Les **éléments de données** sont des pointeurs vers les informations que vous souhaitez collecter et envoyer à différents endroits sur votre page :

* Couche de données définie en JSON
* Éléments DOM
* Cookies
* Stockage local et de session
* À peu près tout

Une fois l’élément de données défini, vous pouvez l’utiliser n’importe où dans l’interface utilisateur de collecte de données pour n’importe quelle extension. Pour plus d’informations, voir la documentation sur [Éléments de données](../ui/managing-resources/data-elements.md) .

Les **règles** se rapportent au noyau logique de votre mise en œuvre et contrôlent tout ce qui concerne les balises de votre site. Définissez un événement, des conditions et des exceptions, puis les actions et l’ordre. Enfin, publiez vos modifications pour afficher les résultats. Pour plus d’informations, reportez-vous à la section [Règles](../ui/managing-resources/rules.md).

## 6. Test dans votre environnement de développement

### Bibliothèques et versions

Les versions de balise ne sont jamais publiées automatiquement. Chaque ensemble de modifications que vous apportez est encapsulé dans une [bibliothèque](../ui/publishing/libraries.md). Chaque bibliothèque que vous créez hérite automatiquement de tout ce qui se trouve en amont (publié, approuvé ou envoyé) comme ligne de base. Vous devez donc simplement définir les modifications que vous souhaitez apporter. Cette bibliothèque sert de plan directeur pour une [version](../ui/publishing/builds.md). Une version est l’ensemble de fichiers JavaScript déployés et utilisés.

Il est important de comprendre la relation entre votre page web, votre emplacement d’hébergement et les balises.

1. Votre serveur hôte fournit un emplacement pour publier la version. La version elle-même contient les fichiers JavaScript requis par la bibliothèque .

   Chaque environnement entretient une relation avec un hôte et l’hôte fournit un point de terminaison indiquant où diffuser la version. L’hôte ne peut appartenir qu’à une seule propriété, bien qu’une propriété puisse avoir de nombreux hôtes.

2. Un code incorporé est fourni dans la balise `<script>` de formulaire qui se trouve dans les sections `<head>` du code HTML de votre site web.

   Lorsque vous créez un environnement et joignez un hôte, l’environnement génère automatiquement un code incorporé unique qui vous permet d’intégrer la version qui lui est assignée dans votre site. Le code `<script>` est utilisé pour déployer la version de bibliothèque au moment de l’exécution.

3. Lorsqu’un utilisateur navigue sur votre site, la balise `<script>` du code incorporé récupère la version à partir du serveur hôte et effectue les actions que vous avez définies dans le navigateur.

### Hôtes

Un hôte est une connexion entre une propriété de balise et votre emplacement d’hébergement. Les balises prennent actuellement en charge l’hébergement géré par Adobe via un hôte [!DNL Akamai] ou l’auto-hébergement via un hôte SFTP. Chaque fois que vous générez une version, les balises se connectent au serveur défini par votre hôte et distribuent la version.

Si vous êtes auto-hébergé, une version de balise peut envoyer directement vers vos serveurs via SFTP ou vous pouvez la transférer vers [!DNL Akamai] et la télécharger à l’aide de l’option Archiver de votre environnement.

Pour plus d’informations, reportez-vous à la section [Hôtes](../ui/publishing/hosts/hosts-overview.md).

### Environnements

Chaque bibliothèque est créée dans un environnement. Un environnement définit la manière dont vous souhaitez que votre version apparaisse lorsqu’elle est publiée. Vous pouvez spécifier :

* **Hôte :** chaque environnement a besoin d’un hôte qui détermine le point de terminaison où toutes les versions créées dans cet environnement seront poussées.
* **Archive :**  le paramètre par défaut est de déployer votre version sous la forme d’un fichier .js minifié. Si vous utilisez du code personnalisé, plusieurs fichiers peuvent s’y faire référence. Ils peuvent être combinés en un seul fichier zip et chiffrés.

Après avoir enregistré votre environnement, il génère le code incorporé que vous pouvez copier et coller dans votre site web. Notez que le code incorporé ne fonctionnera pas tant que vous n’aurez pas créé une bibliothèque et créé une version. Pour plus d’informations, reportez-vous à la section [Environnements](../ui/publishing/environments.md).

### Publication d’une version pour développement

Le processus de publication est décrit dans les étapes ci-dessous.

1. Créez un hôte.
1. créer un environnement de développement à l’aide de l’hôte que vous avez créé ;
1. déployer le code incorporé de votre environnement de développement vers votre site de test de développement ;
1. créer une bibliothèque et l’affecter à l’environnement de développement que vous avez créé ;
1. créer votre bibliothèque.

## 7. Promotion de la production

Après avoir testé votre version dans votre environnement de développement, veillez à créer vos environnements d’évaluation et de production et à placer les codes incorporés aux emplacements nécessaires. Vous pouvez réutiliser des hôtes existants à cette fin.

La promotion d’une bibliothèque jusqu’à la production exige généralement une coordination entre différentes personnes disposant des droits appropriés.

* Un développeur (une personne disposant du droit de développement) envoie la bibliothèque, ce qui change l’état de la bibliothèque en Soumis.
* Un approbateur (une personne disposant du droit d’apporobation) peut créer la bibliothèque dans l’environnement d’étape et l’approuver après le test. L’état de la bibliothèque est ainsi changé en Approuvé. Une seule bibliothèque peut avoir à la fois les états Soumis et Approuvé.
* Un éditeur (une personne disposant du droit de publication) peut créer la bibliothèque dans l’environnement de production.

Vous pouvez octroyer tous ces droits à une même personne.

Pour plus d’informations sur les différents états et options disponibles pendant le processus de publication, reportez-vous à la section [Processus d’approbation](../ui/publishing/publishing-flow.md).

## Ressources supplémentaires

Pour en savoir plus sur les balises, consultez les ressources suivantes :

[https://forums.adobe.com/community/experience-cloud/platform/launchAsk](https://forums.adobe.com/community/experience-cloud/platform/launchAsk) et répondez aux questions, proposez des idées, votez pour les idées des autres. Connectez-vous avec votre Adobe ID.

* **[Communauté de collecte de données](https://forums.adobe.com/community/experience-cloud/platform/launch)** : Posez vos questions et répondez à d&#39;autres, proposez des idées, votez pour les idées des autres. Connectez-vous avec votre Adobe ID.
* **[Developer Docs](https://developer.adobelaunch.com/)** : Participez à la communauté des développeurs de balises pour créer des extensions ou utiliser les API de balises.
* **[Présentation des Tutorials](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html?lang=fr)** : Ces documents vous présentent les concepts de balises, y compris le transfert d’événement et le SDK mobile dans les applications Android.
