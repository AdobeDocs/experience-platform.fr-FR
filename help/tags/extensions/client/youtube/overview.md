---
title: Présentation de l’extension de suivi vidéo YouTube
description: Découvrez lʼextension de balise de suivi vidéo YouTube dans Adobe Experience Platform.
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 78%

---

# Présentation de l’extension de suivi vidéo YouTube

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

**Conditions préalables**

Chaque propriété de balise dans Adobe Experience Platform requiert que les extensions suivantes soient installées et configurées à partir de lʼécran Extensions :

* Adobe Analytics
* du service d’identification des visiteurs Experience Cloud
* Extension Core

Utilisez la [ « Incorporer un lecteur à l’aide d’une balise \&lt;iframe\> »](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) extrait de code de la documentation Google destinée aux développeurs dans l’HTML de chaque page web sur laquelle un lecteur vidéo doit être rendu.

Cette extension, la version 2.0.1, prend en charge l’incorporation d’une ou de plusieurs vidéos YouTube sur une seule page web via l’insertion d’un attribut `id` avec une valeur unique dans la balise de script iframe, et l’ajout de `enablejsapi=1` et `rel=0` à la fin de la valeur de l’attribut `src`, si le code ne s’y trouve pas déjà. Par exemple :

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Cette extension est également conçue pour vérifier dynamiquement la valeur d’un attribut d’identification unique, telle que `player1`, que les paramètres de chaîne de requête `enablejsapi` et `rel` existent ou non et que les valeurs attendues soient correctes ou non. Par conséquent, la balise de script YouTube peut être ajoutée à une page web avec ou sans l’attribut `id` et indépendamment de l’inclusion ou non des paramètres de la chaîne de requête `enablejsapi` et `rel`.

>[!NOTE]
>
>Sur les pages comportant plusieurs vidéos, chaque vidéo utilise le même jeu de configuration défini par la règle de balise qui sʼexécute sur cette page. Par exemple, si vous créez une règle avec un événement qui se déclenche lorsque la vidéo atteint 50 %, chaque vidéo de la page déclenche la règle au point de repère de 50 %.

L’extension repose sur la logique suivante pour réécrire les iFrames :

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Par conséquent, il y aura un léger scintillement après le chargement de la page. Ce comportement est attendu.

## Éléments de données

L’extension contient six éléments de données. Aucun ne nécessite d’être configuré.

* **Position du curseur de lecture :** lorsquʼil est appelé dans une règle de balise, cet élément de données enregistre lʼemplacement, en secondes, de la position du curseur sur la chronologie de la vidéo.
* **ID de la vidéo :** indique l’ID YouTube associé à la vidéo.
* **Nom de la vidéo :** indique le nom descriptif ou convivial de la vidéo.
* **URL de la vidéo :** renvoie l’URL YouTube.com pour la vidéo actuellement chargée/en cours de lecture.
* **Durée de la vidéo :** enregistre la durée totale, en secondes, de la vidéo.
* **Version de l’extension :** cet élément de données enregistre la version de l’extension de suivi YouTube, comme « Video Tracking_YouTube_2.0.0 », par exemple.

## Événements

L’extension comprend huit événements et seul le suivi des points de repère personnalisés requiert une configuration.

* **Vidéo prête :** se déclenche lorsque la vidéo est guidée et prête à être lue.
* **Début vidéo :** déclenche le premier démarrage de la vidéo et lorsque `player.getCurrentTime() === 0`
* **Relecture vidéo :** se déclenche lorsque la vidéo est guidée et relue après le démarrage initial. Ce déclencheur se déclenche à chaque lecture.
* **Vidéo mise en pause :** se déclenche lorsque la vidéo est mise en pause.
* **Reprise de la vidéo :** se déclenche lorsque la vidéo reprend et lorsque `player.getCurrentTime() !== 0`
* **Suivi des points de repère personnalisés :** se déclenche lorsque la vidéo atteint le pourcentage de vidéo indiqué. Par exemple, si une vidéo dure 60 secondes et que le repère spécifié est de 50 %, lʼévénement se déclenche lorsque la position du curseur de lecture est égale à 30 secondes. Le suivi des points de repère s’applique à la lecture initiale et à la relecture. Remarquez que si lʼutilisateur effectue une recherche sur un point de repère, lʼévénement ne se déclenche pas. Les événements du point de repère ne se déclenchent que lorsque le curseur de lecture traverse lʼemplacement du point de repère calculé sur la chronologie et que le lecteur vidéo est en cours de lecture.
* **Mémoire tampon de la vidéo :** se déclenche lorsque le lecteur télécharge une certaine quantité de données avant de commencer la lecture de la vidéo.
* **Fin de la vidéo :** se déclenche lorsqu’une vidéo est entièrement terminée.

## Utilisation

Une règle de balise peut être définie pour chaque événement vidéo (les sept événements répertoriés ci-dessus). Créez une règle de balise spécifique pour chaque événement dont vous souhaitez effectuer le suivi. Si vous ne souhaitez pas effectuer le suivi dʼun événement, ne créez pas de règle pour celui-ci.

Les règles comportent trois actions :

* **Définir des variables :** définissez les variables Adobe Analytics (les faire correspondre à tous les éléments de données inclus ou à certains d’entre eux).
* **Envoyer la balise :** envoyez la balise Adobe Analytics en tant qu’appel de suivi des liens personnalisé et indiquez une valeur « Nom du lien ».
* **Effacer les variables :** effacez les variables Adobe Analytics.

## Exemple de règle de balise pour « Vidéo lancée »

Les objets dʼextension vidéo suivants doivent être inclus.

* **Événements** : « Vidéo lancée » (cet événement déclenche la règle lorsque le visiteur lance une vidéo YouTube).

* **Condition :** aucune

* **Actions** : utilisez l’action **extension Analytics** pour « Définir les variables », afin de mapper :

   * L’événement pour Début vidéo,
   * Une valeur prop/eVar pour l’élément de données Durée de la vidéo
   * Une valeur prop/eVar pour l’élément de données ID de la vidéo
   * Une valeur prop/eVar pour l’élément de données Nom de la vidéo
   * Une valeur prop/eVar pour l’élément de données URL de la vidéo

  Insérez ensuite l’action « Envoyer la balise » (`s.tl`) avec le nom de lien « Début vidéo », suivie d’une action « Effacer les variables ».

>[!TIP]
> 
>Pour les implémentations dans lesquelles il est impossible d’utiliser plusieurs eVars ou props pour chaque élément vidéo, les valeurs des éléments de données peuvent être concaténées dans Experience Platform, analysées dans les rapports de classification à l’aide de l’outil Créateur de règles de classification, comme expliqué dans [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=fr), puis appliquées en tant que segment dans Analysis Workspace.

Pour concaténer des valeurs d’informations vidéo, créez un nouvel élément de données appelé « Métadonnées vidéo », puis programmez-le à extraire tous les éléments de données vidéo (répertoriés ci-dessus) et à les assembler. Par exemple :

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```

Pour plus d’informations sur la création et l’utilisation efficace des éléments de données dans Experience Platform, consultez la documentation [éléments de données](../../../ui/managing-resources/data-elements.md).
