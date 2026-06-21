---
title: Présentation de l’extension de suivi vidéo BrightCove
description: Découvrez lʼextension de balise de suivi vidéo BrightCove dans Adobe Experience Platform.
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
TQID: https://experienceleague.adobe.com/C1JZ1MziVRvUeDbCRaS-BURurIAcr904-rfdHS9Qks4
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: c153fd90-23e1-4614-81d3-3cc7571227f7id: e08599ea-8888-4294-ba74-3ba0a7762a46id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: b0a1f9d5-5795-42a3-a6d0-bd0e2748fd06id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 887
ht-degree: 97%

---

# Présentation de l’extension de suivi vidéo BrightCove

## Prérequis

Pour chaque propriété de balise Adobe Experience Platform, les extensions suivantes doivent être installées et configurées dans l’écran Extension :

* Adobe Analytics
* du service d’identification des visiteurs Experience Cloud
* Extensions Core installées

Utilisez le fragment de code « code intégré sur la page (avancé) » dans le code HTML de chaque page web sur laquelle un lecteur vidéo doit apparaître. Lʼextrait de code HTML « code intégré sur la page (avancé) » se trouve dans la [documentation Brightcove](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Le lien suivant fournit des informations supplémentaires sur [la manière de générer du code incorporé pour les lecteurs vidéo d’aperçu et de vidéos publiées](https://fr.studio.support.brightcove.com/players/generating-player-embed-code.html).

Cette extension version 1.1.0 prend en charge l’incorporation de plusieurs vidéos BrightCove sur une seule page web. Sʼil existe plusieurs propriétés `id` parmi les balises d’incorporation avancées, assurez-vous quʼelles possèdent toutes des valeurs uniques. Par exemple, `player1`, `player2`, etc.

>[!NOTE]
>
>Sur les pages comportant plusieurs vidéos, chaque vidéo utilise le même jeu de configuration défini dans la règle de balise qui s’exécute sur cette page. Par exemple, si vous créez une règle avec un événement qui se déclenche lorsque la vidéo est terminée à 50 %, chaque vidéo de la page déclenche la règle au point de repère de 50 %.

Si la page web qui utilise cette extension interagit avec la vidéo avant que le script approprié ne soit complètement chargé, vous pouvez prendre deux mesures pour résoudre le problème. Vous pouvez tout d’abord charger la bibliothèque de balises de manière synchrone, puis placer l’élément `<script type="text/javascript">\_satellite.pageBottom();\</script\>` avant l’incorporation de la vidéo dans la page.

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

   1. None

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
>Pour ceux qui ne souhaitent pas configurer plusieurs eVars ou props pour chaque élément vidéo, les valeurs des éléments de données sont concaténées comme méthode alternative. Ils sont ensuite analysés dans les rapports de classification à l’aide de l’outil Créateur de règles de classification. Pour plus d’informations, voir la documentation [Outil Créateur de règles de classification](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=fr). Enfin, elles sont appliquées en tant que segment dans Analysis Workspace.
>
>Pour ce faire, créez un nouvel élément de données appelé par exemple « Métadonnées vidéo » et programmez-le pour extraire tous les éléments de données vidéo (répertoriés ci-dessus) et les concaténer.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
