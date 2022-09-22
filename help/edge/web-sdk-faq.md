---
title: FAQ sur le SDK Web Adobe Experience Platform
description: Obtenez des réponses aux questions fréquentes sur le SDK Web de Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 2%

---

# Questions fréquentes

Ce guide répond aux questions fréquentes sur le SDK Web de Adobe Experience Platform.

## Qu’est-ce que le SDK Web de Adobe Experience Platform ?

Le SDK Web de Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les différents services de l’Experience Cloud.

Il envoie les données de manière indépendante de la solution (XDM) à Adobe Experience Platform Edge Network, qui les mappe ensuite aux formats et destinations spécifiques aux solutions et les envoie en temps réel.

**Informations supplémentaires**
[Présentation des Adobes Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## En quoi le SDK Web de Adobe Experience Platform diffère-t-il des solutions précédentes ?

### Avant le SDK Adobe Experience Platform

Actuellement, vous devez déployer différentes bibliothèques JavaScript en fonction de chaque solution.

* Chaque solution possède sa propre bibliothèque JavaScript, son propre schéma et son propre domaine.
* Aucune de ces bibliothèques n&#39;a été construite pour fonctionner les unes avec les autres.
* Les cas d’utilisation inter-solutions et Adobe Experience Platform nécessitent que ces bibliothèques disparates soient interdépendantes, ce qui entraîne des frictions de déploiement.

Bien que les balises dans Platform facilitent le déploiement et la gestion de ces bibliothèques, des problèmes persistent avec :

* Taille de la bibliothèque (trop de code d’Adobe sur une page)
* Performances (le chargement des sites prend trop de temps)
* Plusieurs appels pour un cas d’utilisation unique
* Attente du retour d’ECID avant les appels de personnalisation (cause un retard)
* Collecte de données fracturées (qu’est-ce qu’une evar ?)
* Confusions de schémas entre les solutions (A4T)
* Beaucoup d&#39;autres choses moins optimales

En outre, il n’existe actuellement aucune bibliothèque JavaScript qui envoie directement des données à Adobe Experience Platform.

### Avec le SDK Web Adobe Experience Platform

Le nouveau SDK Web envoie des données pour les solutions suivantes vers une seule destination (réseau Adobe Experience Platform Edge) et résout les cas d’utilisation de solution les plus courants mentionnés ci-dessus.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID (Identifiant visiteur)
* Adobe Experience Platform

D&#39;autres solutions suivront plus tard cette année.

Le SDK Web de Adobe Experience Platform peut également envoyer des données directement à Adobe Experience Platform. Ces données se trouvent dans XDM et sont mappées au schéma de solution côté serveur.

## Quelle est la valeur de ce nouveau SDK Web ?

**Performances :** Le SDK web est plus petit que l’utilisation de toutes les bibliothèques d’Adobe actuelles et permet de charger les pages beaucoup plus rapidement.

**Simplicité :** La combinaison de XDM, de SDK Web, de balises, d’Experience Edge, de solutions Adobe Experience Cloud et de Adobe Experience Platform crée un article de collecte de données facile à comprendre et simple à suivre.

* **XDM :** Schéma indépendant de la solution que vous utilisez pour envoyer des données à Adobe. Plus de balisage pour les eVars ou les mbox.
* **SDK Web Adobe Experience Platform :** Facilite l’envoi et la réception de données vers Adobe Experience Platform Edge Network.
* **Balises :** Simplifie le déploiement et la configuration du SDK Web (et de toute autre balise JavaScript) sur un site.
* **Experience Edge :** acheminez facilement les données vers Adobe Experience Platform et les solutions au format dont elles ont besoin.
* **Solutions Adobe Experience Platform et Adobe :** Activez leur proposition de valeur.

**Contrôle :** Comme toutes les données utilisent un seul flux de données connecté, vous pouvez logiquement suivre et contrôler à quoi ressemblent les données à chaque milliseconde de son parcours, depuis et vers les applications.

**Moderne et prêt pour l&#39;avenir :** Le SDK web et sa connexion au réseau Experience Edge ont permis à Adobe de moderniser de manière significative la manière dont l’Adobe traite la collecte de données, la personnalisation, le consentement et l’avenir des cookies tiers. (Il active un domaine propriétaire, géré par Adobe.)

**Temps jusqu’à la valeur :** Adobe a travaillé dur (et continuera) pour faciliter au maximum le déploiement du SDK Web par le biais de balises et de la mise en correspondance des données côté client avec XDM. Une fois ce travail effectué, toutes les autres solutions d’Adobe et tous les services Adobe Experience Platform peuvent être activés ou désactivés côté serveur. Par exemple, si vous l’utilisez pour Adobe Analytics et que vous souhaitez activer Target ou l’Experience Platform, vous pouvez simplement basculer sur la configuration de la chaîne de données et éclairer ces cas d’utilisation.

## Qu&#39;est-ce qu&#39;Alloy ?

Alloy est le nom de code du SDK Web de Adobe Experience Platform. Il est utilisé dans le code source et le nom de fichier du SDK, bien que le SDK Web de Adobe Experience Platform soit le nom officiel.

## Les clients doivent-ils acheter Adobe Experience Platform pour utiliser la variable [!DNL Web SDK]?

Non. Tout client Adobe Digital Experience peut utiliser le SDK Web de Adobe Experience Platform gratuitement. Les clients qui souhaitent utiliser la variable [!DNL Web SDK] Vous devrez configurer les autorisations appropriées pour créer des schémas, des jeux de données, des espaces de noms d’identité et des flux de données dans l’interface utilisateur de la collecte de données Adobe Experience Platform.

Pour plus d’informations sur la configuration de ces autorisations, consultez notre documentation sur [gestion des autorisations de collecte de données](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## Qui doit utiliser le SDK Web ?

Le SDK Web de Adobe Experience Platform a été développé pour les personnes suivantes :

* Utilisateurs de Adobe Experience Platform
   * Si vous devez envoyer des données directement d’un appareil à Adobe Experience Platform, il s’agit de la méthode officiellement recommandée.
   * Adobe sait que l’utilisation du connecteur Adobe Analytics est plus rapide si le client dispose déjà d’Adobe Analytics, mais ce n’est pas la stratégie à long terme pour la collecte de données.

* Clients de la solution Adobe Experience Cloud
   * Les nouveaux clients Adobe Analytics, Adobe Audience Manager et Adobe Target doivent commencer par le nouveau SDK Web et ne pas utiliser de bibliothèques héritées.
   * Les clients existants qui souhaitent obtenir la mise en oeuvre la plus optimisée possible doivent utiliser le nouveau SDK Web.


## Comment puis-je accéder au SDK Web de Adobe Experience Platform pour commencer ?

Le SDK Web est actuellement disponible pour le grand public et peut être utilisé pour envoyer des données aux produits Adobe Experience Cloud. La possibilité d’envoyer des données à des solutions tierces sera bientôt disponible. Le SDK est gratuit, est hébergé gratuitement par Adobe et peut être téléchargé afin que vous puissiez l’héberger gratuitement sur vos propres serveurs, si vous le souhaitez. Le SDK Web de Platform nécessite l’accès aux configurations du flux de données et au créateur de schémas XDM de Adobe Experience Platform, afin que les serveurs d’Adobe puissent gérer correctement les données entrantes provenant du SDK. Si vous souhaitez y accéder, contactez votre responsable du succès client pour lancer le processus de demande.

## Quels cas pratiques sont actuellement pris en charge par le SDK Web ?

Le SDK Web évolue rapidement. D’autres cas pratiques sont en cours de traitement. Vous trouverez la variable [liste des cas d’utilisation actuellement pris en charge ici.](https://github.com/adobe/alloy/projects/5)

## Les clients actuels doivent-ils rebaliser leurs sites ?

Tout dépend. Le SDK Web de Adobe Experience Platform peut être déployé dans deux styles différents. Un futur document de migration fournira des détails supplémentaires.

* **Une autre balise :** Si le site est déjà balisé pour les solutions et que vous ne pouvez pas le remarquer, mais que vous souhaitez envoyer des données à Adobe Experience Platform Edge Network pour les cas d’utilisation Experience Platform ou les fonctions de transfert d’événement à venir (voir ci-dessous), vous pouvez ajouter la variable `alloy.js` sur le site, où fonctionne comme &quot;juste une autre balise&quot;.

* **La seule et unique balise :** Si vous souhaitez utiliser le SDK Web pour une solution Experience Cloud, vous devez l’utiliser pour _all_ des solutions de cette page. Par exemple, si votre site est déjà balisé pour Adobe Analytics et que vous souhaitez l’utiliser pour Target, vous devez l’utiliser pour , ainsi que pour tout autre site à l’avenir.

En d’autres termes, si vous décidez d’utiliser le SDK Web de Adobe Experience Platform pour des cas d’utilisation non liés à une solution, vous pouvez baliser le site avec `alloy.js` et passer à une nouvelle solution. Si vous souhaitez l’utiliser pour Adobe Analytics, Target ou Audience Manager, ou pour des cas d’utilisation d’application, vous devrez peut-être supprimer l’un des codes hérités de votre page.

## Puis-je migrer les ECID lorsque je commence à utiliser Alloy de sorte que les visiteurs de mon site web ne commencent pas à s’afficher comme de nouveaux visiteurs ?

Oui, le SDK Web de Adobe Experience Platform fournit une fonctionnalité de migration des identités. Suivez les instructions de migration des identifiants dans la section [Documentation sur l’identité du SDK Web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) pour plus d’informations.

## En quoi le SDK Web est-il différent des balises ?

* **Balises dans Experience Platform** gérez le code de l’appareil. Utilisez-les pour déployer plus facilement le code. Ils sont libres et puissants.

* **SDK Web Adobe Experience Platform** est le nom officiel du nouveau code qui serait déployé par des balises pour les cas d’utilisation d’Adobe. C&#39;est aussi gratuit et puissant.

* **`alloy.js`** est le nom de fichier du code du SDK Web de Adobe Experience Platform.

## Dois-je utiliser des balises pour déployer le SDK Web ?

Non. Vous pouvez télécharger le `alloy.js` mettez-vous en file.

Toutefois :

* Le SDK Web de Adobe Experience Platform nécessite un identifiant de flux de données (Datastream ID) afin que le réseau Edge puisse identifier le flux et déterminer ce qu’il faut faire avec les données. Cet identifiant est créé dans Experience Platform. Cela ne signifie pas que vous devez utiliser l’interface utilisateur de la collecte de données pour créer des propriétés ou déployer le code JavaScript, mais vous devez utiliser des balises pour créer un ID de configuration.

* Les balises ne sont pas seulement le meilleur gestionnaire de balises et de SDK disponible. Il facilite le déploiement. `alloy.js` et mapper les données aux schémas XDM. Si vous décidez de ne pas utiliser de balises, vous devrez gérer le déploiement `alloy.js`, l’événement et le mappage de vos données dans XDM avant de les envoyer. Il s’agit d’une _many_ processus plus difficile que l’utilisation de balises.

* Il est recommandé d’utiliser des balises pour le déploiement. `alloy.js`, même s’il s’agit de la seule balise pour laquelle vous l’utilisez.

## Qu’est-ce que le transfert d’événement ?

Si vous utilisez nos SDK et envoyez XDM vers Experience Edge, ces nouvelles fonctionnalités de transfert d’événement vous permettent d’installer de nouvelles extensions côté serveur et de mapper ces données à n’importe quel élément (et de les envoyer n’importe où) de notre réseau Edge. Considérez-le comme une &quot;collecte de données en tant que service&quot;. Cette option est disponible pour un coût et pour être regroupée dans le cadre de Adobe Experience Platform.

## Qu’est-ce qu’un CNAME ou un domaine propriétaire et pourquoi est-ce important ?

Pour plus d’informations sur un CNAME, reportez-vous à la section [Documentation sur les Adobes](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=fr)

## Le SDK Web de Adobe Experience Platform utilise-t-il des cookies ? Si tel est le cas, quels cookies utilise-t-il ?

Oui, le SDK Web utilise actuellement entre 1 et 4 cookies en fonction de votre mise en oeuvre. Vous trouverez ci-dessous une liste des 4 cookies que vous pouvez voir avec le SDK Web et la manière dont ils sont utilisés :

**kndct_orgid_identity :** Le cookie d’identité est utilisé pour stocker l’ECID, ainsi que d’autres informations relatives à l’ECID.

**kndctr_orgid_consent :** Ce cookie stocke les préférences de consentement de l’utilisateur pour le site web.

**kndctr_orgid_cluster :** Ce cookie stocke la région Experience Edge qui traite les requêtes de l’utilisateur actuel. La région est utilisée dans le chemin d’URL afin qu’Experience Edge puisse acheminer la requête vers la région appropriée. Ce cookie a une durée de vie de 30 minutes, de sorte que si un utilisateur se connecte à une autre adresse IP, la demande peut être acheminée vers la région la plus proche.

Lors de l’utilisation du SDK Web, le réseau Edge définit un ou plusieurs des cookies ci-dessus. Le réseau Edge définit tous les cookies avec la variable `secure` et `sameSite="none"` attributs.

Si votre site web comporte actuellement des sections sécurisées et non sécurisées, cela peut interférer avec l’identification de l’utilisateur. Lorsqu’un utilisateur passe d’une section sécurisée du site à une section non sécurisée, le réseau Edge génère une nouvelle `ECID` avec la requête .

## Quels sont les navigateurs pris en charge par le SDK Web de Adobe Experience Platform ?

Le SDK Web de Adobe Experience Platform est conçu pour fonctionner de manière optimale dans les dernières versions de Google Chrome, Safari, Firefox, Internet Explorer 11 et Microsoft Edge Chromium. Vous pouvez rencontrer des problèmes lors de l’utilisation de certaines fonctionnalités sur des versions plus anciennes de navigateurs.

## Où puis-je obtenir plus d’informations sur le SDK Web de Adobe Experience Platform ?

* [Documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=fr)
* [Code source](https://github.com/adobe/alloy)
