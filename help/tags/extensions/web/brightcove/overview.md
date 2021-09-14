---
title: Présentation de l’extension de suivi vidéo BrightCove
description: Découvrez lʼextension de balise de suivi vidéo BrightCove dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '915'
ht-degree: 100%

---

# Présentation de l’extension de suivi vidéo BrightCove

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## Prérequis

Pour chaque propriété de balise dans Adobe Experience Platform, les extensions suivantes doivent être installées et configurées dans lʼécran Extension :

* Adobe Analytics
* Service d’identification des visiteurs Experience Cloud
* Extensions Core installées

Utilisez le fragment de code « Code incorporé sur la page (avancé) » dans le code HTML de chaque page web sur laquelle un lecteur vidéo doit apparaître. Lʼextrait de code HTML « Code incorporé sur la page (avancé) » se trouve dans la [documentation Brightcove](https://fr.studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Le lien suivant fournit des informations supplémentaires sur [la manière de générer un code incorporé pour les lecteurs vidéo de prévisualisation et publiés](https://fr.studio.support.brightcove.com/players/generating-player-embed-code.html).

Cette extension (version 1.1.0) prend en charge lʼincorporation de plusieurs vidéos BrightCove sur une seule page web. Sʼil existe plusieurs propriétés `id` parmi les balises Embed avancées, assurez-vous quʼelles possèdent toutes des valeurs uniques. Par exemple, `player1`, `player2`, etc.

>[!NOTE]
>
>Sur les pages comportant plusieurs vidéos, chaque vidéo utilise le même jeu de configurations défini par la règle de la balise qui sʼexécute sur cette page. Par exemple, si vous créez une règle avec un événement qui se déclenche lorsque la vidéo est terminée à 50 %, chaque vidéo de la page déclenche la règle au point de repère de 50 %.

Si la page web utilisant cette extension interagit avec la vidéo avant que le script associé ne soit complètement chargé, deux options sʼoffrent à vous pour résoudre ce problème. Soit la bibliothèque de balises peut être chargée de manière synchrone, soit lʼélément `<script type="text/javascript">\_satellite.pageBottom();\</script\>` peut être placé avant lʼincorporation de la vidéo sur la page.

Pour plus dʼinformations sur les méthodes et les événements des composants utilisés dans cette extension, voir la [documentation de lʼAPI BrightCove](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer).

## Éléments de données

L’extension contient sept éléments de données. Aucun ne nécessite d’être configuré.

* **Position de la tête de lecture :** lorsque cet élément de données est appelé dans une règle de balise, il enregistre en secondes la position de la tête de lecture sur le montage vidéo.
* **Identifiant du compte de la vidéo :** cet élément de données enregistre l’identifiant du compte Brightcove qui a publié la vidéo.
* **Durée de la vidéo :** cet élément de données enregistre la durée totale, en secondes, du contenu vidéo. De plus, une mesure calculée peut être créée dans Analytics pour convertir cette valeur en minutes ou en heures.
* **Prise en charge des publicités vidéo :** cet élément de données indique si les publicités sont prises en charge dans la vidéo ou non.
* **Identifiant de la vidéo :** cet élément de données indique l’identifiant BrightCove associé à la vidéo.
* **Nom de la vidéo :** cet élément de données indique le nom descriptif ou convivial de la vidéo.
* **Balises de la vidéo :** cet élément de données indique les scripts spécifiques associés à la vidéo.

## Événements

L’extension comprend sept événements et seul le suivi personnalisé par points de repère requiert une configuration.

* **Suivi personnalisé par points de repère :** cet événement se déclenche lorsque la vidéo atteint le pourcentage de vidéo indiqué. Par exemple, si une vidéo dure 60 secondes et que la valeur indiquée est de 50 %, lʼévénement se déclenche à 30 secondes de vidéo.

>[!NOTE]
>
>Veuillez noter que cet événement se déclenche à chaque fois que ce point de repère est atteint. Par exemple, si l’utilisateur atteint le repère des 50 %, retourne à un point antérieur de la vidéo, puis atteint à nouveau le repère, l’événement se déclenche à nouveau.

* **Vidéo terminée :** cet événement se déclenche lorsquʼune vidéo est entièrement terminée.
* **Métadonnées vidéo chargées :** cet événement est déclenché lorsque le lecteur a reçu les informations initiales de durée et de dimension.
* **Vidéo mise en pause :** cet événement se déclenche lorsque la vidéo est mise en pause.
* **Vidéo reprise :** cet événement se déclenche lorsque la vidéo reprend après avoir été mise en pause.
* **Modification de lʼaffichage de la vidéo :** cet événement se déclenche lorsque la vidéo passe en mode Plein écran puis le quitte.
* **Vidéo lancée :** cet événement se déclenche lorsque la vidéo est lancée pour la première fois.

## Utilisation

Une règle de balise peut être définie pour chaque événement vidéo (les sept événements répertoriés ci-dessus). Créez une règle de balise spécifique pour chaque événement dont vous souhaitez effectuer le suivi. Si vous ne souhaitez pas suivre un événement, il vous suffit de l’omettre pour créer une règle pour celui-ci.

Les règles comportent trois actions :

1. Définir les variables Adobe Analytics. (Créer des éléments de données pour tous ou certains des éléments de données répertoriés ci-dessus.)
1. Envoyer la balise Adobe Analytics.
1. Effacer les variables Adobe Analytics.

## Exemple de règle de balise pour « Vidéo lancée »

Les objets dʼextension vidéo suivants doivent être inclus :

* **Événements**

   1. « Vidéo lancée » : cet événement déclenche la règle lorsque le visiteur lance une vidéo BrightCove.

* **Condition**

   1. Aucun

* **Actions**

   1. Dans une action Analytics « Définir des variables », définissez :

      * L’événement pour **Vidéo lancée** (exemple : event17)
      * Une valeur prop/eVar pour lʼélément de données **Nom de la vidéo** (exemple : eVar10)
      * Une valeur prop/eVar pour lʼélément de données **Durée de la vidéo** (exemple : eVar11)
      * Une valeur prop/eVar pour lʼélément de données **Emplacement actuel de la vidéo** (exemple : eVar12)
   1. L’action Analytics « Envoyer la balise » (`s.tl`)
   1. L’action Analytics « Effacer les variables »


>[!TIP]
>
>Pour ceux qui ne souhaitent pas fournir plusieurs valeurs eVar ou prop pour chaque élément vidéo, il existe une autre méthode. Les valeurs des éléments de données peuvent être concaténées dans lʼinterface utilisateur de la collecte de données. Elles sont ensuite analysées dans des rapports de classification à lʼaide de lʼoutil Créateur de règles de classification. Pour plus dʼinformations, voir la documentation sur lʼ[Outil Créateur de règles de classification](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=fr). Suite à lʼanalyse, elles sont appliquées en tant que segment dans Analysis Workspace.
>
>Pour ce faire, créez un nouvel élément de données appelé par exemple « Métadonnées vidéo » et programmez-le pour extraire tous les éléments de données vidéo (répertoriés ci-dessus) et les concaténer.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
