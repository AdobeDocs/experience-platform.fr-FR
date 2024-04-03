---
title: Type de données de collection Détails de la session
description: Découvrez le type de données XDM (Session Details Collection Experience Data Model).
source-git-commit: fb000d45d828c01fdb08d7555512f07ab52e1f7b
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 15%

---

# [!UICONTROL Détails de la session] Type de données de collecte

[!UICONTROL Détails de la session] La collecte est un type de données XDM (Experience Data Model) standard qui effectue le suivi des données liées aux sessions de lecture multimédia. Les champs de collecte de médias sont utilisés pour capturer des données envoyées à d’autres services Adobe en vue d’un traitement ultérieur. Ce schéma englobe un large éventail de propriétés qui peuvent être utilisées pour fournir des informations sur le comportement des utilisateurs et les schémas de consommation de contenu. Utilisez la variable [!UICONTROL Détails de la session] Type de données de collecte permettant de capturer l’engagement des utilisateurs en enregistrant les événements de lecture, les interactions publicitaires, les marqueurs de progression, les pauses et d’autres mesures.

+++Sélectionnez cette option pour afficher un diagramme du type de données Collection de détails de la session.
![Schéma du type de données Collection de détails de la session.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Type de chargement de publicité] | `adLoad` | Chaîne | Non | Type de publicité chargée tel que défini par la représentation interne de chaque client. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | Chaîne | Non | Nom de l’album auquel appartient l’enregistrement musical ou la vidéo. |
| [[!UICONTROL Artiste]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | Chaîne | Non | Nom de l’artiste ou du groupe qui effectue l’enregistrement musical ou vidéo. |
| [[!UICONTROL ID de ressource]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | Chaîne | Non | La variable [!UICONTROL ID de ressource] est l’identifiant unique du contenu de la ressource multimédia, tel que l’identifiant d’épisode de la série télévisée, l’identifiant de la ressource de film ou l’identifiant d’événement en direct. En règle générale, ces identifiants sont issus des autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes. |
| [[!UICONTROL Auteur]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | Chaîne | Non | Nom de l’auteur du média. |
| [[!UICONTROL Type de contenu diffusé]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | Chaîne | Oui | La variable [!UICONTROL Type de contenu diffusé] de la diffusion de flux. Valeurs disponibles par [!UICONTROL Type de diffusion] inclure :<br>Audio : &quot;chanson&quot;, &quot;podcast&quot;, &quot;audiobook&quot; et &quot;radio&quot;;<br>Vidéo : &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; et &quot;DVoD&quot;.<br>Les clients peuvent fournir des valeurs personnalisées pour ce paramètre. |
| [[!UICONTROL Réseau de diffusion]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | Chaîne | Non | Nom du réseau/canal. |
| [[!UICONTROL Canal de contenu]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | Chaîne | Oui | La variable [!UICONTROL Canal de contenu] est le canal de distribution à partir duquel le contenu a été lu. |
| [[!UICONTROL Le contenu se termine]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | Booléen | Non | [!UICONTROL Le contenu se termine] indique si une ressource multimédia minutée a été visionnée jusqu’à la fin. Cet événement ne signifie pas nécessairement que le spectateur a visionné toute la vidéo ; il aurait pu sauter devant. |
| [!UICONTROL Réseau de diffusion de contenu] | `cdn` | Chaîne | Non | La variable [!UICONTROL Réseau de diffusion de contenu] du contenu lu. |
| [[!UICONTROL Identifiant de contenu]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | Chaîne | Oui | La variable [!UICONTROL Identifiant de contenu] est un identifiant unique du contenu. Il peut être utilisé pour renvoyer vers d’autres ID d’industrie ou CMS. |
| [[!UICONTROL Nom du contenu]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | Chaîne | Non | La variable [!UICONTROL Nom du contenu] est le nom &quot;convivial&quot; (lisible par l’utilisateur) du contenu. |
| [[!UICONTROL Nom du lecteur de contenu]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | Chaîne | Oui | Nom du lecteur de contenu. |
| [[!UICONTROL Nom du créateur]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | Chaîne | Non | Nom du créateur de contenu. |
| [[!UICONTROL Partie de la journée]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | Chaîne | Non | Propriété qui définit l’heure de la journée à laquelle le contenu a été diffusé ou lu. Cela peut avoir une valeur définie selon les besoins par les clients. |
| [[!UICONTROL Numéro d’épisode]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | Chaîne | Non | Numéro de l’épisode. |
| [[!UICONTROL Type de flux]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | Chaîne | Non | Le type de flux, qui peut représenter des données liées au flux réel telles que EAST HD ou SD, ou la source du flux telle qu’une URL. |
| [[!UICONTROL Date de première diffusion]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | Chaîne | Non | Date à laquelle le contenu a été diffusé à la télévision pour la première fois. Tout format de date est acceptable, mais Adobe recommande : AAAA-MM-JJ. |
| [[!UICONTROL Date de première distribution numérique]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | Chaîne | Non | Date à laquelle le contenu a été diffusé pour la première fois sur une chaîne ou une plateforme numérique. Tout format de date est acceptable, mais Adobe recommande : AAAA-MM-JJ. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | Chaîne | Non | Type ou regroupement de contenu tel que défini par le producteur de contenu. Les valeurs doivent être délimitées par des virgules dans l’implémentation de la variable. |
| [[!UICONTROL Média autorisé]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | Chaîne | Non | Confirme si l’utilisateur a été autorisé via l’authentification Adobe. |
| [[!UICONTROL Longueur du contenu multimédia]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Nombre entier | Oui | La variable [!UICONTROL Longueur du contenu multimédia] contient la durée/l’exécution de l’élément : il s’agit de la durée maximale (ou durée) du contenu en cours de consommation (en secondes). |
| [[!UICONTROL Démarrages de média]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | Booléen | Non | Événement de chargement pour le média. Cela se produit lorsque la visionneuse sélectionne le bouton de lecture. Cela compte même s’il existe des publicités preroll, des mises en mémoire tampon, des erreurs, etc. |
| [[!UICONTROL Identifiant MVPD]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | Chaîne | Non | Identifiant MVPD (Multi-channel Video Programming Distributor) fourni via l’authentification Adobe. |
| [[!UICONTROL Éditeur]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | Chaîne | Non | Nom de l’éditeur de contenu audio. |
| [[!UICONTROL Radio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | Chaîne | Non | Nom de la station de radio sur laquelle le son est lu. |
| [[!UICONTROL Valeur de notation]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | Chaîne | Non | Évaluation telle que définie par les directives parentales de la télévision. |
| [[!UICONTROL Libellé d’enregistrement]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | Chaîne | Non | Nom du libellé de l’enregistrement. |
| [[!UICONTROL Reprendre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Booléen | Non | Marque chaque lecture qui a été reprise après plus de 30 minutes de mise en mémoire tampon, de mise en pause ou de blocage. |
| [[!UICONTROL Numéro de saison]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | Chaîne | Non | La variable [!UICONTROL Numéro de saison] à laquelle le programme appartient. La Saison n’est requise que si le programme fait partie d’une série. |
| [[!UICONTROL Nom de la série]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | Chaîne | Non | Nom du programme/de la série. Le nom du programme n’est requis que si le programme fait partie d’une série. |
| [[!UICONTROL Type de programme]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | Chaîne | Non | Type de contenu. Par exemple, une bande-annonce ou un épisode complet. Le type de contenu est exprimé sous la forme d’un nombre entier compris entre 0 et 3. Par exemple, &quot;0&quot; = Épisode complet ; &quot;1&quot; = Aperçu/Bande-annonce ; &quot;2&quot; = Clip ; &quot;3&quot; = Autre. |
| [[!UICONTROL Format de diffusion]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | Chaîne | Non | Format du flux (HD, SD). |
| [[!UICONTROL Type de diffusion]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | Chaîne | Non | Type de flux multimédia. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | Chaîne | Non | Version du SDK utilisée par le lecteur. Cela peut avoir toute valeur personnalisée qui convient à votre lecteur. |

{style="table-layout:auto"}

<!-- This is required for sessionStart. 
Q) How do I indicate that?
Q) Do you know where to link for:
Ad Load Type
Content Delivery Network
 -->
