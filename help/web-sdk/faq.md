---
title: FAQ sur le SDK Web Adobe Experience Platform
description: Obtenez des réponses aux questions fréquentes sur le SDK Web de Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: cd2ac132c77d5d2e90c0f881d7b89a3c339fed6f
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 5%

---


# Questions fréquentes

Ce guide répond aux questions fréquentes sur le SDK Web de Adobe Experience Platform.

## Qu’est-ce que le SDK Web Adobe Experience Platform ?

Le SDK Web de Adobe Experience Platform est une bibliothèque JavaScript côté client qui vous permet d’interagir avec les différents services de Adobe Experience Cloud.

Le SDK Web envoie les données de manière indépendante de la solution (XDM) à l’Edge Network Experience Platform, qui mappe ensuite les données aux formats et destinations spécifiques à une solution et les envoie en temps réel.

Pour plus d’informations sur le SDK Web, visionnez la vidéo suivante : [Rencontrez Alloy.js et ne plus jamais baliser pour un eVar ou une mbox](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## En quoi le SDK Web de Adobe Experience Platform diffère-t-il des solutions précédentes ?

### Avant le SDK Web Experience Platform

Actuellement, vous devez déployer différentes bibliothèques JavaScript en fonction de chaque solution.

* Chaque solution possède sa propre bibliothèque JavaScript, son propre schéma et son propre domaine.
* Aucune de ces bibliothèques n&#39;a été construite pour fonctionner les unes avec les autres.
* Les cas d’utilisation inter-solutions et Adobe Experience Platform nécessitent que ces bibliothèques disparates soient interdépendantes, ce qui entraîne des frictions de déploiement.

Bien que les balises dans Platform facilitent le déploiement et la gestion de ces bibliothèques, des problèmes subsistent avec :

* Taille de la bibliothèque (trop de code Adobe sur une page)
* Performances (le chargement des sites prend trop de temps)
* Plusieurs appels pour un cas d’utilisation unique
* Attente du retour d’ECID avant les appels de personnalisation (cause un retard)
* Collecte de données fracturées (qu’est-ce qu’une evar ?)
* Confusions de schémas entre les solutions (A4T)
* Beaucoup d&#39;autres choses moins optimales

En outre, il n’existe actuellement aucune bibliothèque JavaScript qui envoie directement des données à Adobe Experience Platform.

### Avec SDK Web Experience Platform

Le nouveau SDK Web envoie des données pour les solutions suivantes vers une seule destination (Edge Network Experience Platform) et résout les cas d’utilisation de solution susmentionnés les plus courants.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID (Identifiant visiteur)
* Adobe Experience Platform

D&#39;autres solutions suivront.

Le SDK Web de Adobe Experience Platform peut également envoyer des données directement à Adobe Experience Platform. Ces données sont au format XDM et sont mappées au schéma de solution côté serveur.

## Quelle est la valeur de ce nouveau SDK Web ?

**Performance :** Le SDK web est plus petit que l’utilisation de toutes les bibliothèques d’Adobe actuelles et permet des chargements de page beaucoup plus rapides.

**Simplicité :** La combinaison de XDM, SDK Web, balises, Edge Network, solutions Adobe Experience Cloud et Adobe Experience Platform crée un article de collecte de données facile à comprendre et simple à suivre.

* **XDM :** Schéma indépendant de la solution que vous utilisez pour envoyer des données à Adobe. Plus de balisage pour les eVars ou les mbox.
* **SDK Web :** facilite l’envoi et la réception de données à Adobe Experience Platform Edge Network.
* **Balises :** simplifie le déploiement et la configuration du SDK Web (et de toute autre balise JavaScript) sur un site.
* **Edge Network :** acheminez facilement les données vers Adobe Experience Platform et les solutions au format dont elles ont besoin.
* **Solutions Adobe Experience Platform et Adobe :** Activez leur proposition de valeur.

**Contrôle :** Comme toutes les données utilisent un seul flux de données connecté, vous pouvez logiquement suivre et contrôler à quoi ressemblent les données à chaque milliseconde de son parcours, depuis et vers les applications.

**Moderne et prêt pour le futur :** Le SDK Web et sa connexion à l’Edge Network ont permis à l’Adobe de moderniser considérablement la manière dont l’Adobe traite la collecte de données, la personnalisation, le consentement et l’avenir des cookies tiers. (Il active un domaine propriétaire, géré par Adobe.)

**Durée de valeur :** l’Adobe a travaillé dur (et continuera) pour faciliter le déploiement du SDK Web par le biais de balises et de mappage des données côté client sur XDM. Une fois ce travail effectué, toutes les autres solutions d’Adobe et tous les services Adobe Experience Platform peuvent être activés ou désactivés côté serveur. Par exemple, si vous l’utilisez pour Adobe Analytics et que vous souhaitez activer Target ou l’Experience Platform, vous pouvez simplement basculer sur la configuration de la chaîne de données et éclairer ces cas d’utilisation.

## Qu’est-ce que [!DNL alloy.js] ?

[!DNL alloy.js] est le nom de la bibliothèque JavaScript SDK Web. Il est référencé dans le code source et le nom de fichier du SDK.

## Les clients doivent-ils acheter Adobe Experience Platform pour utiliser le [!DNL Web SDK] ?

Non. Tout client Adobe Digital Experience peut utiliser le SDK Web de Adobe Experience Platform gratuitement. Les clients qui souhaitent utiliser [!DNL Web SDK] devront configurer les autorisations appropriées pour créer des schémas, des jeux de données, des espaces de noms d’identité et des flux de données dans l’interface utilisateur de la collecte de données ou l’interface utilisateur Experience Platform.

Pour plus d’informations sur la configuration de ces autorisations, consultez notre documentation sur la [gestion des autorisations de collecte de données](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Qui doit utiliser le SDK Web ?

Le SDK Web de Adobe Experience Platform a été développé pour les clients suivants :

* Utilisateurs de Adobe Experience Platform
   * Si vous devez envoyer des données directement d’un appareil à Adobe Experience Platform, il s’agit de la méthode officiellement recommandée.
   * Adobe sait que l’utilisation du connecteur Adobe Analytics est plus rapide si vous disposez déjà d’Adobe Analytics, mais ce n’est pas la stratégie à long terme pour la collecte de données.

* Clients de la solution Adobe Experience Cloud
   * Les nouveaux clients Adobe Analytics, Adobe Audience Manager et Adobe Target doivent commencer par le nouveau SDK Web et ne pas utiliser de bibliothèques héritées.
   * Les clients existants qui souhaitent obtenir la mise en oeuvre la plus optimisée possible doivent utiliser le nouveau SDK Web.

## Comment accéder au SDK Web ?

Le SDK Web est actuellement disponible pour le grand public et peut être utilisé pour envoyer des données aux produits Adobe Experience Cloud. La possibilité d’envoyer des données à des solutions tierces sera bientôt disponible.

Le SDK est gratuit et est hébergé gratuitement par Adobe. Si nécessaire, vous pouvez le télécharger et l’héberger sur vos propres serveurs sans frais.

Le SDK Web nécessite l’accès aux [configurations de la banque de données](../datastreams/overview.md) et au [créateur de schémas XDM](../xdm/tutorials/create-schema-ui.md) Experience Platform, afin que les serveurs de l’Adobe puissent gérer correctement les données entrantes provenant du SDK. Si vous souhaitez y accéder, contactez votre équipe de compte d’Adobe pour lancer le processus de demande.

## Quels cas pratiques sont actuellement pris en charge par le SDK Web ?

Le SDK Web évolue rapidement. D’autres cas pratiques sont en cours de traitement. Vous trouverez ici la [liste des cas pratiques actuellement pris en charge.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Les clients actuels doivent-ils rebaliser leurs sites ?

Ça dépend. Le SDK Web de Adobe Experience Platform peut être déployé dans deux styles différents. Un futur document de migration fournira des détails supplémentaires.

* **Juste une autre balise :** Si le site est déjà balisé pour les solutions et que vous ne pouvez pas rebaliser, mais que vous souhaitez envoyer des données à Adobe Experience Platform Edge Network pour les cas d’utilisation Experience Platform ou les fonctions de transfert d’événement à venir (voir ci-dessous), vous pouvez ajouter la balise `alloy.js` au site, où elle fonctionne comme &quot;une autre balise seulement&quot;.

* **Balise unique et unique :** Si vous souhaitez utiliser le SDK Web pour une solution Experience Cloud, vous devez l’utiliser pour _toutes_ des solutions de cette page. Par exemple, si votre site est déjà balisé pour Adobe Analytics et que vous souhaitez l’utiliser pour Target, vous devez l’utiliser pour , ainsi que pour tout autre site à l’avenir.

En d’autres termes, si vous décidez d’utiliser le SDK Web de Adobe Experience Platform pour des cas d’utilisation non liés à une solution, vous pouvez baliser le site avec `alloy.js` et passer à la solution comme s’il s’agissait d’une nouvelle solution. Si vous souhaitez l’utiliser pour Adobe Analytics, Target ou Audience Manager, ou pour des cas d’utilisation d’application, vous devrez peut-être supprimer l’un des codes hérités de votre page.

## Puis-je migrer les ECID lorsque je commence à utiliser le SDK Web de sorte que les visiteurs de mon site web ne commencent pas à s’afficher comme de nouveaux visiteurs ?

Oui, le SDK Web de Adobe Experience Platform fournit une fonctionnalité de migration des identités. Pour plus d’informations, suivez les instructions relatives à la migration des identifiants dans la [documentation sur l’identité du SDK Web Platform](/help/web-sdk/identity/overview.md#id-migration) .

## En quoi le SDK Web est-il différent des balises ?

* **Les balises dans Experience Platform** gèrent le code de l’appareil. Utilisez-les pour déployer plus facilement le code. Ils sont libres et puissants.

* **SDK Web Adobe Experience Platform** est le nom officiel du nouveau code qui serait déployé par des balises pour les cas d’utilisation d’Adobe. C&#39;est aussi gratuit et puissant.

* **`alloy.js`** est le nom de fichier du code du SDK Web de Adobe Experience Platform.

## Dois-je utiliser des balises pour déployer le SDK Web ?

Non. Vous pouvez télécharger vous-même le fichier `alloy.js`.

Cependant :

* Le SDK Web de Adobe Experience Platform nécessite un identifiant de flux de données (Datastream ID) afin que le réseau Edge puisse identifier le flux et déterminer ce qu’il faut faire avec les données. Cet identifiant est créé dans Experience Platform. Cela ne signifie pas que vous devez utiliser l’interface utilisateur pour créer des propriétés ou déployer le code JavaScript, mais vous devez utiliser des balises pour créer un ID de configuration.

* Les balises ne sont pas seulement le meilleur gestionnaire de balises et de SDK disponible. Il facilite le déploiement de `alloy.js` et la mise en correspondance des données avec les schémas XDM. Si vous décidez de ne pas utiliser de balises, vous devrez gérer le déploiement `alloy.js`, l’événement et le mappage de vos données dans XDM avant de les envoyer. Il s’agit d’un processus _beaucoup_ plus difficile que l’utilisation de balises.

* Il est recommandé d’utiliser des balises pour déployer `alloy.js`, même s’il s’agit de la seule balise pour laquelle vous l’utilisez.

## Qu’est-ce que le transfert d’événement ?

Si vous utilisez nos SDK et envoyez XDM à l’Edge Network, le transfert d’événement de ces nouvelles fonctionnalités vous permet d’installer de nouvelles extensions côté serveur et de mapper ces données à n’importe quel élément (et de les envoyer n’importe où) de notre réseau Edge. Considérez-le comme une &quot;collecte de données en tant que service&quot;. Cette option est disponible pour un coût et pour être regroupée dans le cadre de Adobe Experience Platform.

## Qu’est-ce qu’un CNAME ou un domaine propriétaire et pourquoi est-ce important ?

Pour plus d’informations sur un CNAME, consultez la [documentation sur l’Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=fr)

## Le SDK Web de Adobe Experience Platform utilise-t-il des cookies ? Si tel est le cas, quels cookies utilise-t-il ?

Oui, le SDK Web utilise actuellement entre un et sept cookies en fonction de votre mise en oeuvre. Vous trouverez ci-dessous une liste des cookies que vous pouvez voir avec le SDK Web et de la manière dont ils sont utilisés :

| **Nom** | **maxAge** | **Âge convivial** | **Description** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 jours | Le cookie d’identité stocke l’ECID, ainsi que d’autres informations relatives à l’ECID. |
| **kndctr_orgid_consent_check** | 7200 | 2 heures | Ce cookie basé sur une session indique au serveur de rechercher les préférences de consentement côté serveur. |
| **kndctr_orgid_consent** | 15552000 | 180 jours | Ce cookie stocke les préférences de consentement de l’utilisateur pour le site web. |
| **kndctr_orgid_cluster** | 1800 | 30 minutes | Ce cookie stocke la région de l’Edge Network qui traite les requêtes de l’utilisateur actuel. La région est utilisée dans le chemin de l’URL afin que l’Edge Network puisse acheminer la requête vers la région appropriée. Ce cookie a une durée de vie de 30 minutes, de sorte que si un utilisateur se connecte à une autre adresse IP, la demande peut être acheminée vers la région la plus proche. |
| **mbox** | 63072000 | 2 ans | Ce cookie s’affiche lorsque le paramètre de migration Target est défini sur true. Cela permet au [cookie mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) Target d’être défini par le SDK Web. |
| **mboxEdgeCluster** | 1800 | 30 minutes | Ce cookie s’affiche lorsque le paramètre de migration Target est défini sur true. Ce cookie permet au SDK Web de communiquer la grappe Edge appropriée à at.js afin que les profils Target puissent rester synchronisés lorsque les utilisateurs naviguent sur un site. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 jours | Ce cookie s’affiche uniquement lorsque la migration des identifiants sur le SDK Web de Adobe Experience Platform est activée. Ce cookie est utile lors de la transition vers le SDK Web alors que certaines parties du site utilisent toujours visitor.js. Voir [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md) pour plus d’informations. |

Lors de l’utilisation du SDK Web, l’Edge Network définit un ou plusieurs des cookies ci-dessus. L’Edge Network définit tous les cookies avec les attributs `secure` et `sameSite="none"`.

Si votre site web comporte actuellement des sections sécurisées et non sécurisées, cela peut interférer avec l’identification de l’utilisateur. Lorsqu’un utilisateur passe d’une section sécurisée du site à une section non sécurisée, l’Edge Network génère un nouveau `ECID` avec la requête.

## Quels sont les navigateurs pris en charge par le SDK Web de Adobe Experience Platform ?

Le SDK Web de Adobe Experience Platform est conçu pour fonctionner de manière optimale dans les dernières versions de Google Chrome, Safari, Firefox, Internet Explorer 11 et Microsoft Edge Chrome. Vous pouvez rencontrer des problèmes lors de l’utilisation de certaines fonctionnalités sur des versions plus anciennes de navigateurs.

## Où puis-je obtenir plus d’informations sur le SDK Web de Adobe Experience Platform ?

* [Documentation](/help/web-sdk/home.md)
* [Code Source](https://github.com/adobe/alloy)

### Prise en charge d’Internet Explorer {#support-internet-explore}

Ce SDK utilise des promesses, qui sont une méthode de communication de l’achèvement des tâches asynchrones. L’implémentation [Promise](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilisée par le SDK est prise en charge en mode natif par tous les navigateurs cibles, à l’exception de [!DNL Internet Explorer]. Pour utiliser le SDK sur [!DNL Internet Explorer], vous devez disposer de `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Pour déterminer si `window.Promise` est déjà polyfillé :

1. Ouvrez votre site web dans [!DNL Internet Explorer].
1. Ouvrez la console de débogage du navigateur.
1. Saisissez `window.Promise` dans la console, puis appuyez sur Entrée.

Si autre chose que `undefined` s’affiche, `window.Promise` est déjà polyfillé. Une autre façon de déterminer si `window.Promise` est polyfillé consiste à charger votre site web après avoir suivi les instructions d’installation ci-dessus. Si le SDK renvoie une erreur à propos d’une promesse, il est probable que `window.Promise` n’ait pas été polyfillé.

Si vous avez déterminé que vous devez polyfiller `window.Promise`, incluez la balise de script suivante au-dessus du code de base fourni précédemment :

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Cette balise charge un script qui s’assure que `window.Promise` est une implémentation de promesse valide.

>[!NOTE]
>
>Si vous choisissez de charger une implémentation de promesse différente, assurez-vous qu&#39;elle prend en charge `Promise.prototype.finally`.