---
title: Type de données de collection des détails de session
description: Découvrez le type de données Modèle de données d’expérience (XDM) de la collecte de détails de session .
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 13%

---

# Type de données de la collecte de [!UICONTROL Session Details]

La collecte de [!UICONTROL Session Details] est un type de données standard du modèle de données d’expérience (XDM) qui effectue le suivi des données liées aux sessions de lecture multimédia. Les champs de collecte de médias sont utilisés pour capturer des données envoyées à d’autres services Adobe en vue d’un traitement ultérieur. Ce schéma englobe un large éventail de propriétés qui peuvent être utilisées pour fournir des informations sur le comportement des utilisateurs et les modèles de consommation de contenu. Utilisez le type de données Collecte de [!UICONTROL Session Details] pour capturer l’interaction client en consignant les événements de lecture, les interactions publicitaires, les marqueurs de progression, les pauses et d’autres mesures.

+++Sélectionnez cette option pour afficher un diagramme du type de données Collecte des détails de la session .
![Diagramme du type de données de collecte Détails de la session.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur la vidéo et les données collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, les rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Ad Load Type] | `adLoad` | Chaîne | Non | Type de publicité chargée tel que défini par la représentation interne de chaque client. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | Chaîne | Non | Nom de l’album auquel appartient la vidéo ou l’enregistrement musical. |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | Chaîne | Non | Nom de l’artiste ou du groupe qui effectue l’enregistrement musical ou la vidéo. |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | Chaîne | Non | Le [!UICONTROL Asset ID] est l’identifiant unique du contenu de la ressource multimédia, tel que l’identifiant de l’épisode de la série télévisée, l’identifiant de la ressource vidéo ou l’identifiant de l’événement en direct. En règle générale, ces identifiants sont dérivés d’autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes. |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | Chaîne | Non | Nom de l’auteur du média. |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | Chaîne | Oui | [!UICONTROL Broadcast Content Type] de la diffusion du flux. Les valeurs disponibles par [!UICONTROL Stream Type] sont les suivantes : <br> Audio : « song », « podcast », « audiobook » et « radio » ; <br> Vidéo : « VoD », « Live », « Linear », « UGC » et « DVoD ».<br>Les clients peuvent fournir des valeurs personnalisées pour ce paramètre. |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | Chaîne | Non | Nom du réseau/canal. |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | Chaîne | Oui | Le [!UICONTROL Content Channel] est le canal de distribution à partir duquel le contenu a été lu. |
| [!UICONTROL Content Delivery Network] | `cdn` | Chaîne | Non | [!UICONTROL Content Delivery Network] du contenu lu. |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | chaîne | Oui | Le [!UICONTROL Content ID] est un identifiant unique du contenu. Il peut être utilisé pour établir un lien vers d’autres ID de secteur ou de CMS. |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | Chaîne | Non | Le [!UICONTROL Content Name] est le nom « convivial » (lisible par l’utilisateur) du contenu. |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | Chaîne | Oui | Nom du lecteur de contenu. |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | Chaîne | Non | Nom du créateur du contenu. |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | Chaîne | Non | Une propriété qui définit l’heure de diffusion ou de lecture du contenu. Les clients et clientes peuvent définir n’importe quelle valeur si nécessaire |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | Chaîne | Non | Numéro de l’épisode. |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | Chaîne | Non | Type de flux. Peut soit représenter les données liées au flux, telles que EAST HD ou SD, soit la source du flux, telle qu’une URL. |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | Chaîne | Non | Date à laquelle le contenu a été diffusé à la télévision pour la première fois. Tout format de date est acceptable, mais Adobe recommande : AAAA-MM-JJ. |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | Chaîne | Non | Date à laquelle le contenu a été diffusé pour la première fois sur un canal ou une plateforme numérique. Tout format de date est acceptable, mais Adobe recommande le format suivant : AAAA-MM-JJ. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | Chaîne | Non | Type ou groupement de contenu, tel que défini par le producteur du contenu. Les valeurs doivent être délimitées par des virgules dans l’implémentation des variables. |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | Chaîne | Non | Confirme si l&#39;utilisateur a obtenu une autorisation via l&#39;authentification Adobe. |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Entier | Oui | Le [!UICONTROL Media Content Length] contient la longueur/exécution de l’élément. Il s’agit de la longueur maximale (ou durée) du contenu consommé (en secondes). |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | Chaîne | Non | Identifiant du distributeur de programmation vidéo multicanal (MVPD) fourni via l’authentification Adobe. |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | Chaîne | Non | Nom de l’éditeur du contenu audio. |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | Chaîne | Non | Nom de la station radio sur laquelle le contenu audio est lu. |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | Chaîne | Non | Évaluation telle que définie par les directives parentales TV. |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | Chaîne | Non | Nom de la maison de disques. |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Booléen | Non | Marque chaque lecture qui a été reprise après plus de 30 minutes de mise en mémoire tampon, de mise en pause ou de blocage. |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | Chaîne | Non | [!UICONTROL Season Number] auquel appartient l’émission. La série Saison n’est obligatoire que si l’émission fait partie d’une série. |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | Chaîne | Non | Nom Du Programme/De La Série. Le Nom du programme n’est requis que si l’émission fait partie d’une série. |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | Chaîne | Non | Type de contenu. Par exemple, une bande-annonce ou un épisode complet. Le type de contenu est exprimé sous la forme d’un nombre entier compris entre 0 et 3. Par exemple, « 0 » = Épisode complet ; « 1 » = Aperçu/bande-annonce ; « 2 » = Clip ; « 3 » = Autre. |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | Chaîne | Non | Format du flux (HD, SD). |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | Chaîne | Non | Type du flux de médias. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | Chaîne | Non | Version du SDK utilisée par le lecteur. Cela peut avoir n’importe quelle valeur personnalisée adaptée à votre lecteur. |

{style="table-layout:auto"}
