---
title: FAQ sur Adobe Experience Platform Web SDK
description: Obtenez des réponses aux questions fréquentes sur Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---

# Questions fréquentes

Ce guide répond aux questions les plus fréquemment posées sur Adobe Experience Platform Web SDK.

## En quoi Adobe Experience Platform Web SDK diffère-t-il des solutions précédentes ?

### Antérieur à Experience Platform Web SDK

Actuellement, vous devez déployer différentes bibliothèques JavaScript en fonction de chaque solution individuelle.

* Chaque solution possède sa propre bibliothèque, son propre schéma et son propre domaine JavaScript.
* Aucune de ces bibliothèques n’a été conçue pour fonctionner les unes avec les autres.
* Les cas d’utilisation inter-solutions et Adobe Experience Platform nécessitent que ces bibliothèques disparates soient interdépendantes, ce qui entraîne des problèmes de déploiement.

Bien que les balises dans Experience Platform facilitent autant que possible le déploiement et la gestion de ces bibliothèques, il existe toujours des problèmes avec :

* Taille de la bibliothèque (trop de code Adobe sur une page)
* Performances (le chargement des sites prend trop de temps)
* Appels multiples pour un cas d’utilisation unique
* Attente d’un retour ECID avant les appels de personnalisation (entraîne un décalage)
* Collecte de données fracturée (qu’est-ce qu’une evar ?)
* Confusion de schémas entre les solutions (A4T)
* Beaucoup d&#39;autres choses moins optimales

En outre, il n’existe actuellement aucune bibliothèque JavaScript qui envoie directement des données à Adobe Experience Platform.

### Avec Experience Platform Web SDK

Le nouveau SDK Web envoie les données des solutions suivantes vers une seule destination (Experience Platform Edge Network) et résout les cas d’utilisation de solutions les plus courants mentionnés ci-dessus.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID (Identifiant visiteur)
* Adobe Experience Platform

D’autres solutions suivront.

Adobe Experience Platform Web SDK peut également envoyer des données directement à Adobe Experience Platform. Ces données sont au format XDM et sont mappées au schéma de solution côté serveur.

## Quelle est la valeur de ce nouveau Web SDK ?

**Performances :** le SDK web est plus petit que l’utilisation de toutes les bibliothèques Adobe actuelles et fournit des chargements de page beaucoup plus rapides.

**Simplicité :** la combinaison de XDM, de Web SDK, de balises, d’Edge Network, de solutions Adobe Experience Cloud et de Adobe Experience Platform permet de créer un récit de collecte de données facile à comprendre et simple à suivre.

* **XDM :** schéma indépendant de la solution que vous utilisez pour envoyer des données à Adobe. Plus de balisage pour les evars ou les mbox.
* **Web SDK :** facilite l’envoi et la réception de données vers Adobe Experience Platform Edge Network.
* **Balises :** simplifie le déploiement et la configuration du SDK Web (et de toute autre balise JavaScript) sur un site.
* **Edge Network:** Acheminez facilement les données vers Adobe Experience Platform et les solutions au format dont elles ont besoin.
* **Les solutions Adobe Experience Platform et Adobe :** Activer leur proposition de valeur.

**Contrôle :** étant donné que toutes les données utilisent un flux de données unique et connecté, vous pouvez suivre et contrôler logiquement l’aspect des données à chaque milliseconde de leur parcours, depuis et vers les applications.

**Moderne et prêt pour l’avenir :** le Web SDK et sa connexion à Edge Network ont permis à Adobe de moderniser considérablement la manière dont Adobe traite la collecte de données, la personnalisation, le consentement et l’avenir des cookies tiers. (Il active un domaine propriétaire, géré par Adobe.)

**Délai de rentabilisation :** Adobe a travaillé dur (et continuera à le faire) pour faciliter autant que possible le déploiement de Web SDK par le biais de balises et le mappage des données côté client à XDM. Une fois ce travail terminé, toutes les autres solutions Adobe et tous les autres services Adobe Experience Platform peuvent être activés ou désactivés côté serveur. Par exemple, si vous l’utilisez pour Adobe Analytics et que vous souhaitez activer Target ou Experience Platform, vous pouvez simplement activer la configuration du flux de données et afficher ces cas d’utilisation.

## Qu’est-ce que `alloy.js` ?

`alloy.js` est le nom de la bibliothèque JavaScript Web SDK. Il est référencé dans le code source et le nom de fichier SDK.

## Les clients doivent-ils acheter Adobe Experience Platform pour utiliser le [!DNL Web SDK] ?

Non. Tout client Adobe Digital Experience peut utiliser Adobe Experience Platform Web SDK gratuitement.

* Les clients qui n’ont *accès* à Experience Platform ou à la plateforme de données clients en temps réel et qui souhaitent utiliser le [!DNL Web SDK] doivent configurer les autorisations appropriées pour créer des schémas et des flux de données dans l’interface utilisateur de collecte de données ou d’Experience Platform.
* Les clients qui ont accès à Experience Platform ou à Real-Time CDP et souhaitent utiliser le [!DNL Web SDK] devront configurer les autorisations appropriées pour créer des schémas, des jeux de données, des espaces de noms d’identité et des flux de données dans l’interface utilisateur de collecte de données ou dans l’interface utilisateur Experience Platform.

Pour plus d’informations sur la configuration de ces autorisations, consultez notre documentation sur la [gestion des autorisations relatives à la collecte de données](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=fr).

## Qui doit utiliser le SDK web ?

Adobe Experience Platform Web SDK a été développé pour les clients suivants :

* Utilisateurs de Adobe Experience Platform
   * Si vous devez envoyer des données directement d’un appareil à Adobe Experience Platform, il s’agit de la méthode officiellement recommandée.
   * Adobe sait que l’utilisation du connecteur Adobe Analytics est plus rapide si vous disposez déjà d’Adobe Analytics, mais ce n’est pas la stratégie à long terme pour la collecte de données.

* clients de la solution Adobe Experience Cloud
   * Les nouveaux clients Adobe Analytics, Adobe Audience Manager et Adobe Target doivent commencer par la nouvelle SDK Web et ne pas utiliser les bibliothèques héritées.
   * Les clients existants qui souhaitent obtenir la mise en œuvre la plus optimisée possible doivent utiliser le nouveau SDK Web.

## Comment puis-je accéder au Web SDK ?

Le Web SDK est actuellement disponible pour le grand public et peut être utilisé pour envoyer des données aux produits Adobe Experience Cloud. La possibilité d’envoyer des données à des solutions tierces sera bientôt disponible.

Le SDK est gratuit et hébergé gratuitement par Adobe. Si nécessaire, vous pouvez le télécharger et l’héberger gratuitement sur vos propres serveurs.

Le SDK Web nécessite l’accès aux [configurations de train de données](/help/datastreams/overview.md) et au créateur de schémas [XDM](/help/xdm/tutorials/create-schema-ui.md) d’Experience Platform, afin que les serveurs Adobe puissent gérer correctement les données entrantes provenant du SDK. Si vous souhaitez obtenir l’accès, contactez l’équipe de votre compte Adobe pour lancer le processus de demande.

## Quels cas pratiques sont actuellement pris en charge par le SDK Web ?

Le Web SDK évolue rapidement. D’autres cas d’utilisation sont en cours de traitement. Vous trouverez la [liste des cas d’utilisation actuellement pris en charge ici.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Les clients actuels doivent-ils modifier les balises de leurs sites ?

Ça dépend. Adobe Experience Platform Web SDK peut être déployé dans deux styles différents. Un futur document de migration fournira des détails supplémentaires.

* **Une autre balise :** si le site est déjà balisé pour des solutions et que vous ne pouvez pas le rebaliser, mais que vous souhaitez envoyer des données à Adobe Experience Platform Edge Network pour des cas d’utilisation Experience Platform ou les fonctionnalités de transfert d’événement à venir (voir ci-dessous), vous pouvez ajouter la balise `alloy.js` au site, où elle fonctionne comme « une autre balise ».

* **La seule et unique balise :** si vous souhaitez utiliser le Web SDK pour une solution Experience Cloud, vous devez l’utiliser pour _toutes_ les solutions de cette page. Par exemple, si votre site est déjà balisé pour Adobe Analytics et que vous souhaitez l’utiliser pour Target, vous devez l’utiliser pour les deux, ainsi que pour tout autre site à l’avenir.

En d’autres termes, si vous décidez d’utiliser Adobe Experience Platform Web SDK pour des cas d’utilisation hors solution, vous pouvez baliser le site avec `alloy.js` et passer à autre chose comme s’il s’agissait d’une nouvelle solution. Si vous souhaitez l’utiliser pour Adobe Analytics, Target ou Audience Manager, ou pour des cas d’utilisation d’application, vous devrez peut-être supprimer l’un des codes hérités sur votre page.

## Puis-je migrer les ECID lorsque je commence à utiliser Web SDK afin que les visiteurs de mon site web ne commencent pas à apparaître comme de nouveaux visiteurs ?

Oui, Adobe Experience Platform Web SDK offre une fonctionnalité de migration d’identité. Suivez les instructions relatives à la migration des identifiants dans la documentation sur les identités [Experience Platform Web SDK](/help/collection/use-cases/identity/id-overview.md#migrating-visitor-api-ecid) pour plus d’informations.

## En quoi le SDK Web diffère-t-il des balises ?

* **Balises dans Experience Platform** gérez le code de l’appareil. Utilisez-les pour déployer plus facilement le code. Ils sont libres et puissants.

* **Adobe Experience Platform Web SDK** est le nom officiel du nouveau code qui serait déployé par les balises pour les cas d’utilisation Adobe. Il est aussi libre et puissant.

* **`alloy.js`** est le nom de fichier du code Adobe Experience Platform Web SDK.

## Dois-je utiliser des balises pour déployer le SDK web ?

Non. Vous pouvez télécharger le fichier `alloy.js` vous-même.

Cependant :

* Adobe Experience Platform Web SDK requiert un élément appelé Identifiant de flux de données afin que le réseau Edge puisse identifier le flux et déterminer ce qu’il doit faire des données. Cet identifiant est créé dans Experience Platform. Cela ne signifie pas que vous devez utiliser l’interface utilisateur pour créer des propriétés ou déployer le code JavaScript, mais vous devez utiliser des balises pour créer un identifiant de configuration.

* Les balises ne sont pas seulement le meilleur gestionnaire de balises et de SDK disponible. Il facilite également le déploiement de `alloy.js` et le mappage de données aux schémas XDM. Si vous décidez de ne pas utiliser de balises, vous devrez gérer le déploiement de `alloy.js`, les événements et le mappage de vos données dans XDM avant de les envoyer. Il s’agit d’un processus _beaucoup_ plus difficile que l’utilisation de balises.

* Il est recommandé d’utiliser des balises pour déployer `alloy.js`, même s’il s’agit de la seule balise pour laquelle vous l’utilisez.

## Qu’est-ce que le transfert d’événement ?

Si vous utilisez nos SDK et envoyez XDM à Edge Network, ces nouvelles fonctionnalités de transfert d’événement vous permettent d’installer de nouvelles extensions côté serveur et de mapper ces données à n’importe quel élément (et de les envoyer n’importe où) à partir de notre réseau Edge. Considérez cela comme un « service de collecte de données ». Ce service sera disponible moyennant un coût, et sera également inclus dans Adobe Experience Platform.

## Qu’est-ce qu’un CNAME ou un domaine propriétaire et pourquoi est-ce important ?

Voir le [programme de certificat géré par Adobe](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/adobe-managed-cert) dans le guide des services principaux.

## Le Adobe Experience Platform Web SDK utilise-t-il des cookies ? Dans l&#39;affirmative, quels cookies utilise-t-elle ?

Voir [Cookies Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/cookies/web-sdk) dans le guide des services principaux.

## Quels navigateurs Adobe Experience Platform Web SDK prend-il en charge ?

Adobe Experience Platform Web SDK est conçu pour fonctionner de manière optimale avec les dernières versions de Google Chrome, Safari, Firefox et Microsoft Edge Chromium. Vous rencontrerez peut-être des problèmes pour utiliser certaines fonctionnalités sur les versions plus anciennes des navigateurs ou les navigateurs obsolètes, tels qu’Internet Explorer.

## Où puis-je obtenir le code source pour le Web SDK ?

Voir le référentiel [Alloy](https://github.com/adobe/alloy) sur GitHub.
