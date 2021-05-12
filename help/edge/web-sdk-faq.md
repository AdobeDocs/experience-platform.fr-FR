---
title: FAQ sur le SDK Web Adobe Experience Platform
description: Obtenez des réponses aux questions fréquentes sur le SDK Web de Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 5ead9dc72b8b9fe89e0a1bc8365ceff8affd3c85
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 2%

---

# Questions fréquemment posées 

Ce guide fournit des réponses aux questions fréquemment posées au sujet du SDK Web de Adobe Experience Platform.

## Qu’est-ce que le SDK Web Adobe Experience Platform ?

Adobe Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les différents services de l’Experience Cloud.

Il envoie les données de manière indépendante de la solution (XDM) à Adobe Experience Platform Edge Network, qui les mappe ensuite aux formats et destinations spécifiques de la solution et les envoie en temps réel.

**Plus d&#39;**
[informationsPrésentation d&#39;Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

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

**Performances :** le kit SDK Web est plus petit que l’utilisation de toutes les bibliothèques d’Adobes actuelles et permet des chargements de pages beaucoup plus rapides.

**Simplicité :** la combinaison de XDM, de Web SDK, d’Experience Platform Launch, d’Experience Edge, de solutions Adobe Experience Cloud et de Adobe Experience Platform crée un récit de collecte de données facile à comprendre et simple à suivre.

* **XDM :** schéma indépendant de la solution que vous utilisez pour envoyer des données à l&#39;Adobe. Plus de balisage pour les eVars ou les mbox.
* **Adobe Experience Platform Web SDK :** facilite l’envoi et la réception de données vers Adobe Experience Platform Edge Network.
* **Experience Platform Launch :** simplifie le déploiement et la configuration du SDK Web (et de toute autre balise JavaScript) sur un site.
* **Expérience Edge : routez** facilement les données vers Adobe Experience Platform et les solutions dans le format dont elles ont besoin.
* **Solutions Adobe Experience Platform et Adobe :** activez leur proposition de valeur.

**Contrôle :** Comme toutes les données utilisent un seul flux de données connecté, vous pouvez logiquement suivre et contrôler à quoi ressemblent les données à chaque milliseconde de son parcours, depuis et vers les applications.

**Moderne et prêt pour l’avenir :** Le kit SDK Web et sa connexion au réseau Experience Edge ont permis à l’Adobe de moderniser de façon significative la manière dont l’Adobe traite la collecte de données, la personnalisation, le consentement et l’avenir des cookies tiers. (Il active un domaine propriétaire, géré par Adobe.)

**Temps/valeur :** l’Adobe a travaillé dur (et continuera) pour faciliter au maximum le déploiement du SDK Web via l’Experience Platform Launch et la mise en correspondance des données côté client avec XDM.  Une fois ce travail effectué, toutes les autres solutions d&#39;Adobe et services Adobe Experience Platform peuvent être activés ou désactivés côté serveur. Par exemple, si vous utilisez ceci pour Adobe Analytics et que vous souhaitez activer la Cible ou l’Experience Platform, il vous suffit de basculer sur la configuration de Datastream et d’éclairer ces cas d’utilisation.

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

Le SDK Web est actuellement accessible au grand public et peut être utilisé pour envoyer des données aux produits Adobe Experience Cloud. La possibilité d&#39;envoyer des données à des solutions tierces est en train d&#39;arriver prochainement. Le SDK est gratuit, est hébergé gratuitement par Adobe et peut être téléchargé afin que vous puissiez l’héberger gratuitement sur vos propres serveurs, si vous le souhaitez. Platform Web SDK nécessite l’accès aux configurations Datastream et au créateur de schémas Adobe Experience Platform XDM, afin que les serveurs d’Adobe puissent gérer correctement les données entrantes en provenance du SDK. Si vous souhaitez obtenir un accès, contactez votre responsable de succès client (CSM) pour début le processus de demande.

## Quels sont les cas d’utilisation actuellement pris en charge par le SDK Web ?

Le SDK Web évolue rapidement. D&#39;autres cas d&#39;utilisation sont en cours de traitement. Vous trouverez la [liste des cas d&#39;utilisation actuellement prise en charge ici.](https://github.com/adobe/alloy/projects/5)

## Les clients actuels doivent-ils remarquer leurs sites ?

Tout dépend. Le SDK Web de Adobe Experience Platform peut être déployé dans deux styles différents. Un futur document de migration fournira des détails supplémentaires.

* **Juste une autre balise :** si le site est déjà balisé pour des solutions et que vous ne pouvez pas le remarquer, mais que vous souhaitez envoyer des données à Adobe Experience Platform Edge Network pour les cas d&#39;utilisation Experience Platform ou les prochaines fonctionnalités côté serveur Experience Platform Launch (voir ci-dessous), vous pouvez ajouter la  `alloy.js` balise au site, où elle fonctionne comme &quot;une autre balise&quot;.

* **La seule et unique balise :** si vous souhaitez utiliser le SDK Web pour une solution Experience Cloud, vous devez l’utiliser pour  __ toutes les solutions de cette page. Par exemple, si votre site est déjà balisé pour Adobe Analytics et que vous souhaitez l’utiliser pour la Cible, vous devez l’utiliser pour les deux, ainsi que pour tout autre site dans le futur.

En d’autres termes, si vous décidez d’utiliser Adobe Experience Platform Web SDK pour des cas d’utilisation sans solution, vous pouvez baliser le site avec `alloy.js` et passer à autre chose comme s’il s’agissait d’une nouvelle solution. Si vous souhaitez l’utiliser pour l’Adobe Analytics, la Cible ou l’Audience Manager, ou pour des cas d’utilisation d’application, vous devrez peut-être supprimer n’importe quel code hérité sur votre page.

## Puis-je migrer les ECIDs lorsque je début d’utiliser l’Alloy pour que les visiteurs de mon site Web ne s’affichent pas comme de nouveaux visiteurs ?

Oui, Adobe Experience Platform Web SDK fournit une fonctionnalité de migration d’identité. Suivez les instructions relatives à la migration des identifiants dans la [documentation du SDK Web de plate-forme](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) pour plus d’informations.

## En quoi le SDK Web est-il différent de l’Adobe Experience Platform Launch ?

* **Experience Platform** Launchis est le gestionnaire de code de périphérique. Utilisez-la pour déployer plus facilement le code. Il est libre et puissant.

* **Adobe Experience Platform Web** SDK est le nom officiel du nouveau code qui serait déployé par l’Experience Platform Launch pour les cas d’utilisation d’Adobe. Il est aussi libre et puissant.

* **`alloy.js`** est le nom de fichier du code du SDK Web de Adobe Experience Platform.

## Dois-je utiliser Adobe Experience Platform Launch pour déployer le SDK Web ?

Non. Vous pouvez télécharger vous-même le fichier `alloy.js`.

Toutefois :

* Adobe Experience Platform Web SDK nécessite un identifiant de flux de données afin que le réseau de périphérie puisse identifier le flux et déterminer ce qu’il convient de faire avec les données. Cet identifiant est créé dans l’Experience Platform Launch. Cela ne signifie pas que vous devez utiliser l’Experience Platform Launch pour créer des propriétés ou déployer le code JavaScript, mais vous devez utiliser l’Experience Platform Launch pour créer un ID de configuration.

* Adobe Experience Platform Launch est non seulement le meilleur gestionnaire de balises et de SDK disponible, mais il facilite également le déploiement de `alloy.js` et la mise en correspondance des données avec les schémas XDM. Si vous décidez de ne pas utiliser d&#39;Experience Platform Launch, vous devrez gérer le déploiement de `alloy.js`, l&#39;événement et le mappage de vos données dans XDM avant de les envoyer. Il s&#39;agit d&#39;un processus _beaucoup_ plus difficile que d&#39;utiliser un Experience Platform Launch.

* Il est recommandé d’utiliser Experience Platform Launch pour déployer `alloy.js`, même s’il s’agit de la seule balise pour laquelle vous l’utilisez.

## Qu&#39;est-ce que &quot;Adobe Experience Platform Launch Server Side&quot; ?

Plus tard dans l’année 2020, l’Experience Platform Launch sortira des fonctionnalités de transfert côté serveur. Si vous utilisez nos SDK et envoyez XDM à Experience Edge, ces nouvelles fonctionnalités vous permettront d’installer de nouvelles extensions côté serveur et de mapper ces données à n’importe quoi (et de les envoyer n’importe où) à partir de notre réseau Edge. Considérez-le comme une &quot;collecte de données en tant que service&quot;.  Cette option sera disponible pour un coût et sera intégrée dans le cadre de Adobe Experience Platform.

## Qu’est-ce qu’un CNAME ou un domaine de premier niveau et pourquoi est-ce important ?

Pour plus d’informations sur un CNAME, consultez la [documentation de l’Adobe](https://docs.adobe.com/content/help/fr-FR/id-service/using/reference/analytics-reference/cname.html).

## Le Adobe Experience Platform Web SDK utilise-t-il des cookies ? Dans l&#39;affirmative, quels cookies utilise-t-il ?

Oui, le SDK Web utilise actuellement entre 1 et 4 cookies en fonction de votre implémentation. Vous trouverez ci-dessous une liste des 4 cookies que vous pouvez voir avec le SDK Web et leur utilisation :

**kndct_orgid_identity :** Le cookie d’identité est utilisé pour stocker l’ECID, ainsi que d’autres informations relatives à l’ECID.

**kndctr_orgid_consentement :** ce cookie stocke les préférences de consentement de l’utilisateur pour le site Web.

**kndctr_orgid_personalization :** ce cookie contient des informations de session que Adobe Target utilise pour personnaliser les pages Web.

**kndctr_orgid_consentcheck :** Ce cookie basé sur la session signale au serveur de rechercher le côté serveur des préférences de consentement.

## Quels navigateurs le kit Adobe Experience Platform Web SDK prend-il en charge ?

Le Adobe Experience Platform Web SDK est conçu pour fonctionner de manière optimale dans les dernières versions de Google Chrome, Safari, Firefox, Internet Explorer 11 et Microsoft Edge Chrome. Vous pouvez rencontrer des problèmes lors de l’utilisation de certaines fonctions sur des versions plus anciennes des navigateurs.

## Où puis-je obtenir plus d’informations sur le SDK Web de Adobe Experience Platform ?

* [Documentation](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/home.html)
* [Code source](https://github.com/adobe/alloy)
