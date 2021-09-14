---
title: Environnements
description: Découvrez le concept des environnements de balises et leur fonctionnement dans Adobe Experience Platform.
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: ht
source-wordcount: '1468'
ht-degree: 100%

---

# Environnements

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les environnements de balises définissent plusieurs aspects clés des versions de bibliothèque que vous déployez sur votre site web ou application :

* Nom de fichier de la version.
* Le domaine et le chemin d’accès de la version, en fonction de l’hôte affecté à l’environnement.
* Format de fichier de la version, selon l’option d’archivage choisie.

Lorsque vous créez une version de bibliothèque, vous devez l’affecter à un environnement. Les extensions, règles et éléments de données de la version sont ensuite compilés et placés dans l’environnement attribué. Chaque environnement fournit un code incorporé unique qui vous permet d’intégrer la version qui lui est assignée dans votre site.

Il peut y avoir différents artefacts dans chaque environnement. Cela vous permet de tester différentes bibliothèques dans différents environnements lorsque vous les utilisez dans votre processus.

Ce document décrit la procédure à suivre pour installer, configurer et créer différents environnements dans l’interface utilisateur de la collecte de données.

## Types d’environnement

Les balises prennent en charge trois types d’environnements différents, chacun correspondant à un état différent dans le [flux de travaux de publication](./publishing-flow.md) :

| Type d’environnement | Description |
| --- | --- |
| Développement | Cet environnement correspond à la colonne **Développement** du workflow de publication. |
| Évaluation | Cet environnement correspond aux colonnes **Envoyé** et **Approuvé** du workflow de publication. |
| Production | Cet environnement correspond à la colonne **Publié** du workflow de publication. |

Il peut y avoir différents artefacts dans chaque environnement. Cela vous permet de tester différentes bibliothèques dans différents environnements lorsque vous les utilisez dans le workflow de publication.

>[!NOTE]
>
>Chaque environnement ne peut être affecté qu’à une seule version de bibliothèque à la fois. Cependant, il est prévu qu’un seul environnement contienne de nombreuses versions différents au fur et à mesure que vous les utilisez dans le workflow de publication, en réaffectant les versions entre les environnements si nécessaire.

## Installation

Chaque environnement comporte un ensemble d’instructions utilisées pour la connexion à votre application. Pour les propriétés web, ces instructions fournissent des codes incorporés. Pour les propriétés mobiles, ces instructions fournissent le code nécessaire pour instancier les bibliothèques que vous utilisez et récupérer la configuration au moment de l’exécution.

>[!IMPORTANT]
>
>Chaque type d’environnement comporte ses propres instructions d’installation correspondantes. En fonction de l’environnement utilisé, vous devez vous assurer que vous utilisez les codes incorporés et/ou les dépendances appropriés.
>
>Par exemple, le code incorporé de production d’une propriété web prend en charge la mise en cache du navigateur, contrairement aux codes incorporés de développement et de staging. Par conséquent, vous ne devez pas utiliser les codes incorporés de développement ou de staging dans les contextes à trafic élevé ou de production.

Pour accéder aux instructions d’installation d’un environnement, accédez à l’onglet **[!UICONTROL Environnements]** correspondant à votre propriété, puis sélectionnez l’icône **[!UICONTROL Installer]** correspondant à cet environnement.

![](./images/environments/install-buttons.png)

Si vous utilisez une propriété web, vous recevez un code incorporé à utiliser dans la balise `<head>` de votre document. Vous disposez également de l’option permettant de déployer les fichiers de bibliothèque de manière synchrone ou asynchrone au moment de l’exécution. Selon le paramètre choisi, les instructions d’installation affichées seront différentes. Les codes incorporés sont expliqués plus en détail plus loin dans ce document.

![](./images/environments/web-instructions.png)

Si vous utilisez une propriété mobile, des instructions distinctes vous sont données pour l’installation des dépendances pour Android (via [Gradle](https://gradle.org/)) et iOS (via [CocoaPods](https://cocoapods.org/)).

![](./images/environments/mobile-instructions.png)

## Configuration mobile

Pour les propriétés mobiles, vous pouvez voir les options de configuration d’un environnement en le sélectionnant dans la liste. À partir de là, vous pouvez modifier le nom de l’environnement. Actuellement, les environnements mobiles ne peuvent utiliser que des hôtes gérés par Adobe.

![](./images/environments/mobile-config.png)

Pour plus d’informations, consultez la présentation sur les [hôtes](./hosts/hosts-overview.md).

## Configuration web

Pour les propriétés web, les paramètres de l’environnement affecté déterminent les éléments suivants :

* **Hôte** : emplacement du serveur sur lequel vous souhaitez déployer votre version.
* **Paramètre d’archivage** : indique si le système doit générer un ensemble de fichiers déployable ou les compresser dans un format d’archive.
* **Code incorporé** : code `<script>` à incorporer dans le code HTML des pages de votre site web, utilisé pour déployer la version de la bibliothèque au moment de l’exécution.

Dans l’onglet [!UICONTROL Environnements], sélectionnez un environnement répertorié pour afficher ses commandes de configuration.

![](./images/environments/environment-config.png)

### Hôte {#host}

Sélectionnez **[!UICONTROL Hôte]** pour choisir un hôte préconfiguré pour l’environnement dans le menu déroulant.

![](./images/environments/select-host.png)

Une fois une version créée, celle-ci est déployée vers l’emplacement spécifié pour l’hôte affecté. Pour plus d’informations sur la création et la configuration des hôtes dans l’interface utilisateur de la collecte de données, reportez-vous à la [présentation des hôtes](./hosts/hosts-overview.md).

### Paramètre d’archivage {#archive}

La plupart des versions se composent de plusieurs fichiers. Les versions multi-fichiers contiennent un fichier de bibliothèque principal (lié dans le code incorporé) qui contient les références internes aux autres fichiers qui sont extraites selon les besoins.

Le bouton **[!UICONTROL Créer une archive]** vous permet d’activer/désactiver le paramètre d’archivage de l’environnement. Par défaut, l’option d’archivage est désactivée et la version est diffusée dans un format qui s’exécute en l’état (JavaScript pour les propriétés web et JSON pour les propriétés mobiles).

Si vous choisissez d’activer le paramètre d’archivage, d’autres paramètres de configuration s’affichent dans l’interface utilisateur, vous permettant éventuellement de chiffrer le fichier d’archive et de définir un chemin d’accès à la bibliothèque si vous utilisez l’auto-hébergement.

![](./images/environments/archive-settings.png)

Le chemin d’accès peut être soit une URL complète, soit un chemin relatif utilisable pour plusieurs domaines. Ce chemin est important, car la plupart des versions comportent plusieurs fichiers qui contiennent des références internes les uns aux autres.

Si vous utilisez l’option d’archivage, tous les fichiers de la version sont fournis sous la forme d’un fichier .zip. Ce format peut s’avérer utile si :

1. vous auto-hébergez la bibliothèque, mais ne souhaitez pas configurer un hôte SFTP pour la diffusion ;
1. vous devez exécuter une analyse du code sur la version avant son déploiement ;
1. vous souhaitez simplement consulter le contenu de la version.

### Code incorporé {#embed-code}

Un code incorporé est une balise `<script>` qui doit être placée dans les sections `<head>` des pages de votre site web pour charger et exécuter le code que vous créez. Chaque configuration d’environnement génère automatiquement son propre code incorporé. Il vous suffit donc de le copier et de le coller dans votre site sur les pages sur lesquelles vous souhaitez exécuter les balises.

Lorsque vous consultez les instructions d’installation, vous pouvez choisir que le script charge les fichiers de bibliothèque de manière synchrone ou asynchrone. Ce paramètre n’est pas persistant et ne reflète pas la manière dont vous avez réellement implémenté les balises sur votre site. Au contraire, il ne vise qu’à montrer la manière appropriée d’installer l’environnement.

>[!WARNING]
>
>Selon le contenu de votre bibliothèque de balises, le comportement de vos règles et d’autres éléments peut varier entre le déploiement synchrone et asynchrone. Il est donc important de tester minutieusement les modifications que vous apportez.

#### Déploiement asynchrone

Un déploiement asynchrone permet au navigateur de continuer à charger le reste de la page pendant la récupération de la bibliothèque. Il n’y a qu’un seul code incorporé lors de l’utilisation de ce paramètre, qui doit être placé dans le document `<head>`.

Pour plus d’informations sur ce paramètre, voir le guide sur le [déploiement asynchrone](../client-side/asynchronous-deployment.md).

#### Déploiement synchrone

Lorsque le navigateur lit un code incorporé à l’aide d’un déploiement synchrone, il récupère la bibliothèque de balises et l’exécute avant de continuer à charger la page.

Les codes incorporés synchrones se composent de deux balises `<script>` qui doivent être placées dans le code HTML de votre site web. Une balise `<script>` doit être placée dans le document `<head>`, tandis que l’autre doit être placée juste avant la balise `</body>` de fermeture.

#### Mises à jour du code incorporé

Les codes incorporés étant générés en fonction des configurations de votre environnement, certaines modifications de configuration mettent automatiquement à jour le code incorporé de l’environnement en question. Ces modifications comprennent :

* Passer d’un hôte géré par Adobe à un hôte SFTP ou vice versa.
* Modifier le paramètre d’archivage.
* Mettre à jour le champ du chemin si le paramètre d’archivage est activé.

>[!WARNING]
>
>Lorsque le code incorporé d’un environnement change dans une balise, vous devez mettre à jour manuellement les codes incorporés dans votre code HTML. Pour éviter une maintenance coûteuse, vous ne devez mettre à jour votre ou vos codes incorporés que lorsque cela est absolument nécessaire.

## Création d’un environnement

Trois environnements sont automatiquement affectés à une propriété lors de sa création : développement, staging et production. Ces environnements suffisent pour exécuter le processus de publication. Cependant, vous pouvez ajouter d’autres environnements de développement si vous le souhaitez, car cela peut s’avérer utile pour des équipes plus importantes dans lesquelles plusieurs développeurs travaillent simultanément sur différents projets.

Dans l’onglet [!UICONTROL Environnements] de votre propriété, sélectionnez **[!UICONTROL Ajouter un environnement]**.

![](./images/environments/create-new.png)

Dans l’écran suivant, sélectionnez l’option **[!UICONTROL Développement]**.

![](./images/environments/create-development.png)

L’écran suivant vous permet de nommer le nouvel environnement, de sélectionner un hôte et de choisir un paramètre d’archivage. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]** pour créer l’environnement.

![](./images/environments/create-config.png)

L’onglet [!UICONTROL Environnements] réapparaît, et les instructions d’installation du nouvel environnement s’affichent.

![](./images/environments/create-install.png)

## Étapes suivantes

Grâce à ce document, vous devriez mieux comprendre la configuration des environnements dans l’interface utilisateur et leur installation sur votre site web ou dans votre application. Vous êtes maintenant prêt à publier vos versions de bibliothèque.

Lorsque vous publiez des itérations de votre bibliothèque au fil du temps, il peut s’avérer nécessaire d’effectuer le tracking et l’archivage des versions précédentes à des fins de dépannage et de restauration. Pour plus d’informations, consultez le guide sur la [republication des anciennes bibliothèques](./republish.md).
