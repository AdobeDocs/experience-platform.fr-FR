---
title: Envoyer l’événement multimédia
description: Envoyez les données multimédia à Adobe Experience Platform Edge Network.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Envoyer l’événement multimédia

L’action **[!UICONTROL Send media event]** envoie un événement multimédia à un flux de données, qui peut ensuite être utilisé par des applications et des services tels que Adobe Experience Platform ou Adobe Analytics. Cette action est utile lorsque vous effectuez le suivi du contenu multimédia en flux continu sur votre propriété.

![Image de l’interface utilisateur d’Experience Platform affichant l’écran d’événement multimédia d’envoi.](../assets/send-media-event.png)

Les options disponibles dépendent du **[!UICONTROL Media event type]** que vous sélectionnez. Tous les types d’événements multimédias nécessitent un **[!UICONTROL Player ID]**, qui est le nom du lecteur de contenu.

Certains types d’événements permettent de configurer d’autres champs. Si un type d’événement multimédia n’est pas répertorié ici, le seul champ disponible est [!UICONTROL Player ID]. Les types d’événements multimédias suivants incluent d’autres champs :

## [!UICONTROL Ad break start]

Permet de configurer les détails d’un pod publicitaire.

* **[!UICONTROL Ad break name]** : nom convivial de la coupure publicitaire.
* **[!UICONTROL Ad break offset (seconds)]** : décalage de la coupure publicitaire dans le contenu, en secondes.
* **[!UICONTROL Ad break index]** : index de la coupure publicitaire dans le contenu, commençant à 1.

## [!UICONTROL Ad start]

Permet de configurer les détails de la publicité.

* **[!UICONTROL Ad name]** : nom convivial de la publicité.
* **[!UICONTROL Ad ID]** : ID de l’annonce publicitaire. Toute valeur alphanumérique est prise en charge.
* **[!UICONTROL Ad length (seconds)]** : durée de la publicité vidéo, en secondes.
* **[!UICONTROL Advertiser]** : société ou marque dont le produit apparaît dans la publicité.
* **[!UICONTROL Campaign ID]** : identifiant de la campagne publicitaire.
* **[!UICONTROL Creative ID]** : ID du contenu publicitaire.
* **[!UICONTROL Creative URL]** : URL du contenu publicitaire.
* **[!UICONTROL Placement ID]** : ID d’emplacement de l’annonce publicitaire.
* **[!UICONTROL Site ID]** : ID du site publicitaire.
* **[!UICONTROL Pod position]** : index de la publicité à l’intérieur de la coupure publicitaire parent, commençant à 0.

Ce type d’événement prend également en charge la possibilité de fournir des métadonnées personnalisées dans le cadre de la payload d’événement multimédia.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]** : objet [Qualité d’expérience](/help/xdm/data-types/qoe-data-details-collection.md) qui spécifie le débit, les images perdues, les images par seconde et l’heure de début.

## [!UICONTROL Chapter start]

Permet de configurer les détails du chapitre.

* **[!UICONTROL Chapter name]** : nom du chapitre ou du segment.
* **[!UICONTROL Chapter length]** : longueur du chapitre, en secondes.
* **[!UICONTROL Chapter index]** : position du chapitre à l’intérieur du contenu.
* **[!UICONTROL Chapter offset]** : décalage du chapitre par rapport au début du contenu, en secondes.

Ce type d’événement prend également en charge la possibilité de fournir des métadonnées personnalisées dans le cadre de la payload d’événement multimédia.

## [!UICONTROL Error]

Permet de configurer les détails des erreurs.

* **[!UICONTROL Error name]** : nom de l’erreur.
* **[!UICONTROL Source]** : source de l’erreur.

## [!UICONTROL Session start]

Permet de configurer les détails de session multimédia.

* **[!UICONTROL Handle media session automatically]** : case à cocher qui permet au SDK Web d’envoyer automatiquement les pings nécessaires. Vous pouvez décocher cette case si vous souhaitez envoyer manuellement des pings.
* **[!UICONTROL Playhead]** : curseur de lecture, en secondes.
* **[!UICONTROL Content type]** : type de contenu. Toute valeur de chaîne est prise en charge ; Adobe propose également les paramètres prédéfinis suivants :
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]** : durée maximale du contenu consommé, en secondes. Pour les médias en direct dont la durée est inconnue, la valeur de `86400` est la valeur par défaut.
* **[!UICONTROL Content ID]** : ID de contenu du contenu.
* **[!UICONTROL Ad load type]** : type de publicité chargée. Les deux valeurs suivantes sont prises en charge :
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]** : L&#39;album auquel appartient la chanson.
* **[!UICONTROL Artist]** : L&#39;artiste de la chanson.
* **[!UICONTROL Asset ID]** : identifiant unique du contenu de la ressource multimédia. Ces identifiants sont généralement dérivés d’autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes.
* **[!UICONTROL Author]** : nom de l’auteur du livre audio.
* **[!UICONTROL Authorized]** : indicateur qui détermine si l’utilisateur est connecté via l’authentification Adobe.
* **[!UICONTROL Day part]** : heure de diffusion ou de lecture du contenu. Toute valeur de chaîne est prise en charge.
* **[!UICONTROL Episode]** : numéro de l’épisode.
* **[!UICONTROL Feed type]** : type de flux.
* **[!UICONTROL First air date]** : date à laquelle le contenu a été diffusé pour la première fois à la télévision. Toute valeur de chaîne est prise en charge ; cependant, Adobe recommande d’utiliser le format `YYYY-MM-DD`.
* **[!UICONTROL First digital date]** : date à laquelle le contenu a été diffusé pour la première fois sur un canal ou une plateforme numérique. Toute valeur de chaîne est prise en charge ; cependant, Adobe recommande d’utiliser le format `YYYY-MM-DD`.
* **[!UICONTROL Content name]** : nom convivial du contenu.
* **[!UICONTROL Genre]** : type ou groupement de contenu défini par le producteur du contenu. Ce champ prend en charge plusieurs valeurs délimitées par une virgule.
* **[!UICONTROL Label]** : nom de la maison de disques.
* **[!UICONTROL Rating]** : évaluation telle que définie par les directives parentales de TV.
* **[!UICONTROL MVPD]** : MVPD fourni par l’authentification Adobe.
* **[!UICONTROL Network]** : nom du réseau ou du canal.
* **[!UICONTROL Originator]** : créateur du contenu.
* **[!UICONTROL Publisher]** : éditeur de contenu audio.
* **[!UICONTROL Season]** : si l’émission fait partie d’une série, il s’agit du numéro de saison de l’émission.
* **[!UICONTROL Show]** : si l’émission fait partie d’une série, le nom de la série.
* **[!UICONTROL Show type]** : type d’affichage. Toute valeur de chaîne est prise en charge ; Adobe propose également les paramètres prédéfinis suivants :
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]** : type de flux.
* **[!UICONTROL Stream format]** : format du flux, tel que HD ou SD.
* **[!UICONTROL Station]** : nom ou ID de la station radio.

Ce type d’événement prend également en charge la possibilité de fournir des métadonnées personnalisées dans le cadre de la payload d’événement multimédia. Il permet également des remplacements de la configuration du train de données, ce qui vous permet de contrôler les applications et services qui reçoivent ces données. Lorsque vous définissez un remplacement de configuration de train de données à la fois dans une commande individuelle et dans les paramètres de configuration de l’extension de balise, la commande individuelle est prioritaire. Consultez [ Remplacements de configuration de train de données ](../configure/configuration-overrides.md) pour plus d’informations.

## [!UICONTROL States update]

Permet de configurer les détails de la mise à jour de l’état. Vous pouvez démarrer ou terminer les états suivants :

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

Les champs disponibles sont les suivants :

* **[!UICONTROL States started]** : menu déroulant qui vous permet d’indiquer qu’un état a démarré. Le fait de sélectionner le bouton **[!UICONTROL Add another state that started]** vous permet de démarrer plusieurs états dans la même action.
* **[!UICONTROL States ended]** : menu déroulant qui vous permet d’indiquer qu’un état s’est terminé. Le fait de sélectionner le bouton **[!UICONTROL Add another state that ended]** vous permet de terminer plusieurs états dans la même action.
