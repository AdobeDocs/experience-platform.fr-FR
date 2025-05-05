---
title: Présentation de l’extension de suivi vidéo BrightCove
description: Découvrez lʼextension de balise de suivi vidéo BrightCove dans Adobe Experience Platform.
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 97%

---

# Présentation de l’extension de suivi vidéo BrightCove

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## Prérequis

Pour chaque propriété de balise Adobe Experience Platform, les extensions suivantes doivent être installées et configurées dans l’écran Extension :

* Adobe Analytics
* du service d’identification des visiteurs Experience Cloud
* Extensions Core installées

Utilisez le fragment de code « Code incorporé sur la page (avancé) » dans le code HTML de chaque page web sur laquelle un lecteur vidéo doit apparaître. Le fragment de code HTML « Code incorporé sur la page (avancé) » se trouve dans la [documentation Brightcove](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Le lien suivant fournit des informations supplémentaires sur [la manière de générer du code incorporé pour les lecteurs vidéo d’aperçu et de vidéos publiées](https://fr.studio.support.brightcove.com/players/generating-player-embed-code.html).

Cette extension version 1.1.0 prend en charge l’incorporation de plusieurs vidéos BrightCove sur une seule page web. S’il existe plusieurs propriétés `id` dans les balises incorporées avancées, assurez-vous qu’elles possèdent chacune des valeurs uniques. Par exemple, `player1`, `player2`, etc.

>[!NOTE]
>
>Sur les pages comportant plusieurs vidéos, chaque vidéo utilise le même jeu de configuration défini dans la règle de balise qui s’exécute sur cette page. Par exemple, si vous créez une règle avec un événement qui se déclenche lorsque la vidéo est terminée à 50 %, chaque vidéo de la page déclenche la règle au point de repère de 50 %.

Si la page web qui utilise cette extension interagit avec la vidéo avant que le script approprié ne soit complètement chargé, vous pouvez prendre deux mesures pour résoudre le problème. Vous pouvez tout d’abord charger la bibliothèque de balises de manière synchrone, puis placer l’élément `<script type="text/javascript">\_satellite.pageBottom();\</script\>` avant l’intégration de la vidéo dans la page.

Voir la [documentation de l’API BrightCove](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) pour plus d’informations sur les méthodes de composants et les événements utilisés dans cette extension.

## Éléments de données

L’extension contient sept éléments de données. Aucun ne nécessite d’être configuré.

* **Position de la tête de lecture :** lorsque cet élément de données est appelé dans une règle de balise, il enregistre en secondes la position de la tête de lecture sur le montage vidéo.
* **Identifiant du compte de la vidéo :** cet élément de données enregistre l’identifiant du compte Brightcove qui a publié la vidéo.
* **Durée de la vidéo :** cet élément de données enregistre la durée totale, en secondes, du contenu vidéo. De plus, une mesure calculée peut être créée dans Analytics pour convertir cette valeur en minutes ou en heures.
* **Prise en charge des publicités vidéo :** cet élément de données indique si les publicités sont prises en charge dans la vidéo.
* **Identifiant de la vidéo :** cet élément de données indique l’identifiant BrightCove associé à la vidéo.
* **Nom de la vidéo :** cet élément de données indique le nom descriptif ou convivial de la vidéo.
* **Balises vidéo :** cet élément de données indique les scripts spécifiques associés à la vidéo.

## Événements

L’extension comprend sept événements et seul le suivi personnalisé par points de repère requiert une configuration.

* **Suivi personnalisé par points de repère :** cet événement se déclenche lorsque la vidéo atteint le pourcentage de vidéo indiqué. Par exemple, si une vidéo dure 60 secondes et que la valeur indiquée est de 50 %, l’événement se déclenche à 30 secondes de vidéo. 

>[!NOTE]
>
>Veuillez noter que cet événement se déclenche à chaque fois que ce point de repère est atteint. Par exemple, si l’utilisateur atteint le repère des 50 %, retourne à un point antérieur de la vidéo, puis atteint à nouveau le repère, l’événement se déclenche à nouveau.

* **Vidéo terminée :** cet événement se déclenche lorsqu’une vidéo est entièrement terminée.
* **Métadonnées de vidéo chargées :** cet événement est déclenché lorsque le lecteur a reçu les informations initiales de durée et de dimension.
* **Vidéo mise en pause :** cet événement se déclenche lorsque la vidéo est mise en pause.
* **Vidéo reprise :** cet événement se déclenche lorsque la vidéo reprend après avoir été mise en pause.
* **Modification de l’affichage vidéo :** cet événement se déclenche lorsque la vidéo passe en mode Plein écran et le quitte.
* **Vidéo lancée :** cet événement se déclenche lorsque la vidéo est lancée pour la première fois.

## Utilisation

Une règle de balise peut être définie pour chaque événement vidéo (les sept événements répertoriés ci-dessus). Créez une règle de balise spécifique pour chaque événement dont vous souhaitez effectuer le suivi. Si vous ne souhaitez pas effectuer le suivi dʼun événement, ne créez pas de règle pour celui-ci.

Les règles comportent trois actions :

1. Définir les variables Adobe Analytics. (Créer des éléments de données pour tous ou certains des éléments de données répertoriés ci-dessus.)
1. Envoyer la balise Adobe Analytics.
1. Effacer les variables Adobe Analytics.

## Exemple de règle de balise pour « Vidéo lancée »

Les objets d’extension vidéo suivants doivent être inclus :

* **Événements**

   1. « Vidéo lancée » : cet événement déclenche la règle lorsque le visiteur lance une vidéo BrightCove.

* **Condition**

   1. Aucun

* **Actions**

   1. Dans une action Analytics « Définir des variables », définissez :

      * L’événement pour **Vidéo lancée** (exemple : event17)
      * Une valeur prop/eVar pour l’élément de données **Nom de la vidéo** (exemple : eVar10)
      * Une valeur prop/eVar pour l&#39;élément de données **Durée de la vidéo** (exemple : eVar11)
      * Une valeur prop/eVar pour l’élément de données **Emplacement actuel de la vidéo** (exemple : eVar12)

   1. L’action Analytics « Envoyer la balise » (`s.tl`)
   1. L’action Analytics « Effacer les variables »

>[!TIP]
>
>Pour ceux qui ne souhaitent pas configurer plusieurs eVars ou props pour chaque élément vidéo, les valeurs des éléments de données sont concaténées en tant que méthode alternative. Ils sont ensuite analysés dans les rapports de classification à l’aide de l’outil Créateur de règles de classification. Pour plus d’informations, voir la documentation [Outil Créateur de règles de classification](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=fr). Enfin, elles sont appliquées en tant que segment dans Analysis Workspace.
>
>Pour ce faire, créez un nouvel élément de données appelé par exemple « Métadonnées vidéo » et programmez-le pour extraire tous les éléments de données vidéo (répertoriés ci-dessus) et les concaténer.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
