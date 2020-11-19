---
title: FAQ sur le SDK Web
seo-title: FAQ sur le SDK Web Adobe Experience Platform
description: Questions fréquentes sur Adobe Experience Platform Web SDK
seo-description: Questions fréquentes sur Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 2%

---


# Questions fréquemment posées

Ce forum aux questions comprend les questions souvent posées au sujet de l&#39;Adobe Web SDK.

## Qu’est-ce que le SDK Web Adobe Experience Platform ?

Adobe Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les différents services de l’Experience Cloud.

Il envoie les données de manière indépendante de la solution (XDM) à Adobe Experience Platform Edge Network, qui les mappe ensuite aux formats et destinations spécifiques de la solution et les envoie en temps réel.

**Plus d&#39;informations**[Adobe Présentation du Sommet](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## En quoi le SDK Web de Adobe Experience Platform diffère-t-il des solutions précédentes ?

### Avant le SDK Adobe Experience Platform

Actuellement, vous devez déployer différentes bibliothèques JavaScript en fonction de chaque solution.

* Chaque solution possède sa propre bibliothèque JavaScript, son propre schéma et son propre domaine.
* Aucune de ces bibliothèques n&#39;a été construite pour fonctionner les unes avec les autres.
* Les cas d’utilisation de solutions croisées et de Adobe Experience Platform exigent que ces bibliothèques disparates soient interdépendantes, ce qui cause des frictions au niveau du déploiement.

Bien que Adobe Experience Platform Launch facilite le déploiement et la gestion de ces bibliothèques, il reste des problèmes avec :

* Taille de la bibliothèque (trop de code d’Adobe sur une page)
* Performances (le chargement des sites prend trop de temps)
* Appels multiples pour un cas d’utilisation unique
* Attente d’un retour ECID avant les appels de personnalisation (cause un décalage)
* Collecte de données fragmentées (qu’est-ce qu’une evar ?)
* Confusion schéma entre les solutions (A4T)
* Beaucoup d&#39;autres choses moins optimales

En outre, il n’existe actuellement aucune bibliothèque JavaScript qui envoie directement des données à Adobe Experience Platform.

### Avec Adobe Experience Platform Web SDK

Le nouveau SDK Web envoie les données des solutions suivantes vers une destination unique (Adobe Experience Platform Edge Network) et résout les cas d’utilisation des solutions les plus courants mentionnés ci-dessus.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID (Identifiant visiteur)
* Adobe Experience Platform

D&#39;autres solutions suivront plus tard cette année.

Adobe Experience Platform Web SDK peut également envoyer des données directement à Adobe Experience Platform. Ces données se trouvent dans XDM et sont mises en correspondance avec le schéma de solution côté serveur.

## Quelle est la valeur de ce nouveau SDK Web ?

**Performances :** Le SDK Web est plus petit que l’utilisation de toutes les bibliothèques d’Adobes actuelles et permet des chargements de page beaucoup plus rapides.

**Simplicité :** La combinaison de XDM, de Web SDK, d’Experience Platform Launch, d’Experience Edge, de solutions Adobe Experience Cloud et de Adobe Experience Platform crée un récit de collecte de données facile à comprendre et simple à suivre.

* **XDM :** Schéma indépendant de la solution que vous utilisez pour envoyer des données à l’Adobe. Plus de balisage pour les eVars ou les mbox.
* **Adobe Experience Platform Web SDK :** Facilite l&#39;envoi et la réception de données vers Adobe Experience Platform Edge Network.
* **Experience Platform Launch :** Simplifie le déploiement et la configuration du SDK Web (et de toute autre balise JavaScript) sur un site.
* **Experience Edge :** acheminer facilement les données vers Adobe Experience Platform et les solutions dans le format dont elles ont besoin.
* **Solutions Adobe Experience Platform et Adobe :** Activez leur proposition de valeur.

**Contrôle :** Comme toutes les données utilisent un seul flux de données connecté, vous pouvez logiquement suivre et contrôler à quoi ressemblent les données à chaque milliseconde de son parcours, depuis et vers les applications.

**Moderne et prêt pour l&#39;avenir :** Le SDK Web et sa connexion au réseau Experience Edge ont permis à l’Adobe de moderniser de façon significative la façon dont l’Adobe traite la collecte de données, la personnalisation, le consentement et l’avenir des cookies tiers. (Il active un domaine propriétaire, géré par Adobe.)

**Durée/valeur :** Adobe a travaillé dur (et continuera) pour faciliter au maximum le déploiement du SDK Web via l’Experience Platform Launch et la mise en correspondance des données côté client avec XDM.  Une fois ce travail effectué, toutes les autres solutions d&#39;Adobe et services Adobe Experience Platform peuvent être activés ou désactivés côté serveur. Par exemple, si vous utilisez ceci pour Adobe Analytics et que vous souhaitez activer la Cible ou l’Experience Platform, vous pouvez simplement basculer sur la configuration d’Experience Edge et éclairer ces cas d’utilisation.

## Qu&#39;est-ce que l&#39;Alloy ?

Alloy est le nom de code du SDK Web Adobe Experience Platform. Il est utilisé dans le code source et le nom de fichier du SDK, bien que le SDK Web de Adobe Experience Platform soit le nom officiel.

## Les clients doivent-ils acheter Adobe Experience Platform pour utiliser le SDK Web ?

Non. Tout client Adobe Digital Experience peut l’utiliser. Totalement gratuit. Tout client souhaitant utiliser le SDK Web aura accès à la création de schémas et de jeux de données dans l’interface utilisateur de Adobe Experience Platform.

## Qui doit utiliser le SDK Web ?

Adobe Experience Platform Web SDK a été développé pour les personnes suivantes :

* Utilisateurs de Adobe Experience Platform

   Si vous devez envoyer des données directement d’un périphérique à Adobe Experience Platform, il s’agit de la méthode recommandée officiellement.

   L&#39;Adobe sait que l&#39;utilisation du connecteur Adobe Analytics est plus rapide si le client dispose déjà de Adobe Analytics, mais ce n&#39;est pas la stratégie à long terme pour la collecte de données.

* Clients de la solution Adobe Experience Cloud

   Les nouveaux clients Adobe Analytics, Adobe Audience Manager et Adobe Target doivent début avec le nouveau SDK Web et ne pas utiliser de bibliothèques héritées.

   Les clients existants qui souhaitent obtenir la mise en oeuvre la plus optimisée possible doivent utiliser le nouveau SDK Web.


## Comment puis-je accéder au début à l’aide du SDK Web Adobe Experience Platform ?

Le SDK Web est actuellement accessible au grand public et peut être utilisé pour envoyer des données aux produits Adobe Experience Cloud. La possibilité d&#39;envoyer des données à des solutions tierces est en train d&#39;arriver prochainement. Si vous souhaitez accéder au SDK Web, contactez votre responsable logiciel certifié (CSM) pour début le processus de demande.

## Quels sont les cas d’utilisation actuellement pris en charge par le SDK Web ?

Le SDK Web évolue rapidement. D&#39;autres cas d&#39;utilisation sont en cours de traitement. Vous trouverez ici la [liste des cas d&#39;utilisation actuellement pris en charge.](https://github.com/adobe/alloy/projects/5)

## Les clients actuels doivent-ils remarquer leurs sites ?

Tout dépend. Le SDK Web de Adobe Experience Platform peut être déployé dans deux styles différents. Un futur document de migration fournira des détails supplémentaires.

* **Juste une autre balise :** Si le site est déjà balisé pour des solutions et que vous ne pouvez pas le remarquer, mais que vous souhaitez envoyer des données à Adobe Experience Platform Edge Network pour les cas d’utilisation Experience Platform ou les prochaines fonctionnalités côté serveur Experience Platform Launch (voir ci-dessous), vous pouvez ajouter la `alloy.js` balise au site, où elle fonctionne comme &quot;une autre balise&quot;.

* **La seule et unique balise :** Si vous souhaitez utiliser le SDK Web pour une solution Experience Cloud, vous devez l’utiliser pour _toutes les_ solutions de cette page. Par exemple, si votre site est déjà balisé pour Adobe Analytics et que vous souhaitez l’utiliser pour la Cible, vous devez l’utiliser pour les deux, ainsi que pour tout autre site dans le futur.

En d’autres termes, si vous décidez d’utiliser Adobe Experience Platform Web SDK pour des cas d’utilisation sans solution, vous pouvez baliser le site avec `alloy.js` et passer à autre chose comme s’il s’agissait d’une nouvelle solution. Si vous souhaitez l’utiliser pour l’Adobe Analytics, la Cible ou l’Audience Manager, ou pour des cas d’utilisation d’application, vous devrez peut-être supprimer n’importe quel code hérité sur votre page.

## Puis-je migrer les ECIDs lorsque je début d’utiliser l’Alloy pour que les visiteurs de mon site Web ne s’affichent pas comme de nouveaux visiteurs ?

Oui, Adobe Experience Platform Web SDK fournit une fonctionnalité de migration d’identité. Suivez les instructions de [ce document](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) pour en savoir plus.

## En quoi le SDK Web est-il différent de l’Adobe Experience Platform Launch ?

* **Experience Platform Launch** est le gestionnaire de code de périphérique. Utilisez-la pour déployer plus facilement le code. Il est libre et puissant.

* **Adobe Experience Platform Web SDK** est le nom officiel du nouveau code qui serait déployé par l’Experience Platform Launch pour les cas d’utilisation d’Adobe. Il est aussi libre et puissant.

* **`alloy.js`** est le nom de fichier du code du SDK Web de Adobe Experience Platform.

## Dois-je utiliser Adobe Experience Platform Launch pour déployer le SDK Web ?

Non. Vous pouvez télécharger le `alloy.js` fichier vous-même.

Cependant :

* Le SDK Web de Adobe Experience Platform nécessite un identifiant de configuration Experience Edge pour que le réseau Edge puisse identifier le flux et déterminer ce qu’il faut faire avec les données. Cet identifiant est créé dans l’Experience Platform Launch. Cela ne signifie pas que vous devez utiliser l’Experience Platform Launch pour créer des propriétés ou déployer le code JavaScript, mais vous devez utiliser l’Experience Platform Launch pour créer un ID de configuration.

* Adobe Experience Platform Launch est non seulement le meilleur gestionnaire de balises et de SDK disponible, mais il facilite également le déploiement `alloy.js` et la mise en correspondance des données vers les schémas XDM. Si vous décidez de ne pas utiliser d’Experience Platform Launch, vous devrez gérer le déploiement `alloy.js`, l’événement et le mappage de vos données dans XDM avant de les envoyer. C&#39;est un processus _beaucoup_ plus difficile que d&#39;utiliser un Experience Platform Launch.

* Il est recommandé d’utiliser Experience Platform Launch pour le déploiement `alloy.js`, même s’il s’agit de la seule balise pour laquelle vous l’utilisez.

## Qu&#39;est-ce que &quot;Adobe Experience Platform Launch Server Side&quot; ?

Plus tard dans l’année 2020, l’Experience Platform Launch sortira des fonctionnalités de transfert côté serveur. Si vous utilisez nos SDK et envoyez XDM à Experience Edge, ces nouvelles fonctionnalités vous permettront d’installer de nouvelles extensions côté serveur et de mapper ces données à n’importe quoi (et de les envoyer n’importe où) à partir de notre réseau Edge. Considérez-le comme une &quot;collecte de données en tant que service&quot;.  Cette option sera disponible pour un coût et sera intégrée dans le cadre de Adobe Experience Platform.

## Qu’est-ce qu’un CNAME ou un domaine de premier niveau et pourquoi est-ce important ?

Pour plus d’informations sur un CNAME, consultez la documentation de l’ [Adobe.](https://docs.adobe.com/content/help/fr-FR/id-service/using/reference/analytics-reference/cname.html)

## Où puis-je obtenir plus d’informations sur le SDK Web de Adobe Experience Platform ?

* [Documentation](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/home.html)
* [Code source](https://github.com/adobe/alloy)
