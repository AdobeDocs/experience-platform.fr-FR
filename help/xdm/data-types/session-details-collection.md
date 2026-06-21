---
title: Type de données de collection des détails de session
description: Découvrez le type de données Modèle de données d’expérience (XDM) de la collecte de détails de session .
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
TQID: https://experienceleague.adobe.com/w2EYDZMD7deZm-pkdsNDtMSm3E3YwyNrVXBGpqTG6pc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 1258
ht-degree: 8%

---

# [!UICONTROL Détails de la session] Type de données de collection

La collecte de [!UICONTROL Détails de session] est un type de données standard du modèle de données d’expérience (XDM) qui effectue le suivi des données liées aux sessions de lecture de média. Ce schéma englobe un large éventail de propriétés qui peuvent être utilisées pour fournir des informations sur le comportement des utilisateurs et les modèles de consommation de contenu. Utilisez le type de données de collection [!UICONTROL Détails de session] pour capturer l’interaction client en consignant les événements de lecture, les interactions publicitaires, les marqueurs de progression, les pauses et d’autres mesures.

+++Sélectionnez cette option pour afficher un diagramme du type de données Collecte des détails de la session .
![Diagramme du type de données de collecte Détails de la session.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, à savoir les champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données et génère les champs de `mediaReporting` correspondants, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

Chaque nom d’affichage contient un lien vers des informations supplémentaires sur sa variable d’implémentation. Les pages liées contiennent des détails sur les données collectées par Adobe, les valeurs d’implémentation, les paramètres réseau et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|---|---|---|---|---|
| [[!UICONTROL Type de chargement des annonces]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/ad-load-type) | `adLoad` | Chaîne | Non | Type de publicité chargée tel que défini par la représentation interne de chaque client. |
| [[!UICONTROL album]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/album) | `album` | Chaîne | Non | Nom de l’album auquel appartient la vidéo ou l’enregistrement musical. |
| [[!UICONTROL Artiste]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/artist) | `artist` | Chaîne | Non | Nom de l’artiste ou du groupe qui effectue l’enregistrement musical ou la vidéo. |
| [[!UICONTROL ID de ressource]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/asset-id) | `assetID` | Chaîne | Non | L’[!UICONTROL ID de ressource] est l’identifiant unique du contenu de la ressource multimédia, tel que l’identifiant de l’épisode de la série télévisée, l’identifiant de la ressource vidéo ou l’identifiant de l’événement en direct. En règle générale, ces identifiants sont dérivés d’autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes. |
| [[!UICONTROL Auteur]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/author) | `author` | Chaîne | Non | Nom de l’auteur du média. |
| [[!UICONTROL Type de contenu de diffusion]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/content-type) | `contentType` | Chaîne | Oui | Le [!UICONTROL type de contenu de diffusion] de la diffusion en continu. Les valeurs disponibles par [!UICONTROL Type de flux] incluent :<br>Audio : « song », « podcast », « audiobook » et « radio » ; <br>Vidéo : « VoD », « Live », « Linear », « UGC » et « DVoD ».<br>Les clients peuvent fournir des valeurs personnalisées pour ce paramètre. |
| [[!UICONTROL Réseau de diffusion]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/network) | `network` | Chaîne | Non | Nom du réseau/canal. |
| [[!UICONTROL &#x200B; Canal de contenu &#x200B;]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/content-channel) | `channel` | Chaîne | Oui | Le [!UICONTROL canal de contenu] est le canal de distribution à partir duquel le contenu a été lu. |
| [!UICONTROL Réseau de diffusion de contenu] | `cdn` | Chaîne | Non | Le [!UICONTROL réseau de diffusion de contenu] du contenu lu. |
| [[!UICONTROL Identifiant du contenu]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/content-id) | `name` | string | Oui | L’[!UICONTROL ID de contenu] est un identifiant unique du contenu. Il peut être utilisé pour établir un lien vers d’autres ID de secteur ou de CMS. |
| [[!UICONTROL Nom du contenu]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/content-name) | `friendlyName` | Chaîne | Non | Le [!UICONTROL &#x200B; Nom du contenu &#x200B;] est le nom « convivial » (lisible par l’utilisateur) du contenu. |
| [[!UICONTROL Nom du lecteur de contenu]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/content-player-name) | `playerName` | Chaîne | Oui | Nom du lecteur de contenu. |
| [[!UICONTROL Nom du créateur]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/originator) | `originator` | Chaîne | Non | Nom du créateur du contenu. |
| [[!UICONTROL Jour]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/day-part) | `dayPart` | Chaîne | Non | Une propriété qui définit l’heure de diffusion ou de lecture du contenu. Les clients et clientes peuvent définir n’importe quelle valeur, si nécessaire. |
| [[!UICONTROL Numéro de l’épisode]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/episode) | `episode` | Chaîne | Non | Numéro de l’épisode. |
| [[!UICONTROL Type de flux]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/media-feed-type) | `feed` | Chaîne | Non | Type de flux. Peut soit représenter les données liées au flux, telles que EAST HD ou SD, soit la source du flux, telle qu’une URL. |
| [[!UICONTROL Date de première diffusion]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/first-air-date) | `firstAirDate` | Chaîne | Non | Date à laquelle le contenu a été diffusé à la télévision pour la première fois. Tout format de date est acceptable, mais Adobe recommande : AAAA-MM-JJ. |
| [[!UICONTROL Première date numérique]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/first-digital-date) | `firstDigitalDate` | Chaîne | Non | Date à laquelle le contenu a été diffusé pour la première fois sur un canal ou une plateforme numérique. Tout format de date est acceptable, mais Adobe recommande le format suivant : AAAA-MM-JJ. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/genre) | `genre` | Chaîne | Non | Type ou groupement de contenu, tel que défini par le producteur du contenu. Les valeurs doivent être délimitées par des virgules dans l’implémentation des variables. |
| [[!UICONTROL Média autorisé]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/authorized) | `authorized` | Chaîne | Non | Confirme si l&#39;utilisateur a obtenu une autorisation via l&#39;authentification Adobe. |
| [[!UICONTROL Longueur du contenu multimédia]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/content-length) | `length` | Entier | Oui | La [!UICONTROL Longueur du contenu multimédia] contient la longueur/l’exécution de l’élément. Il s’agit de la longueur maximale (ou durée) du contenu utilisé (en secondes). |
| [[!UICONTROL Identifiant &#x200B;]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/mvpd) | `mvpd` | Chaîne | Non | Identifiant du distributeur de programmation vidéo multicanal (MVPD) fourni via l’authentification Adobe. |
| [[!UICONTROL Éditeur]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/publisher) | `publisher` | Chaîne | Non | Nom de l’éditeur du contenu audio. |
| [[!UICONTROL Station radio]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/station) | `station` | Chaîne | Non | Nom de la station radio sur laquelle le contenu audio est lu. |
| [[!UICONTROL Valeur d’évaluation]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/content-rating) | `rating` | Chaîne | Non | Évaluation telle que définie par les directives parentales TV. |
| [[!UICONTROL Libellé d’enregistrement]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/label) | `label` | Chaîne | Non | Nom de la maison de disques. |
| [[!UICONTROL Reprendre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/content-resumes) | `hasResume` | Booléen | Non | Marque chaque lecture qui a été reprise après plus de 30 minutes de mise en mémoire tampon, de mise en pause ou de blocage. |
| [[!UICONTROL Numéro de saison]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/season) | `season` | Chaîne | Non | Le [!UICONTROL numéro de saison] auquel appartient l’émission. La série Saison n’est obligatoire que si l’émission fait partie d’une série. |
| [[!UICONTROL Nom de la série]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/show) | `show` | Chaîne | Non | Nom Du Programme/De La Série. Le Nom du programme n’est requis que si l’émission fait partie d’une série. |
| [[!UICONTROL Afficher le type]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/show-type) | `showType` | Chaîne | Non | Type de contenu. Par exemple, une bande-annonce ou un épisode complet. Le type de contenu est exprimé sous la forme d’un nombre entier compris entre 0 et 3. Par exemple, « 0 » = Épisode complet ; « 1 » = Aperçu/bande-annonce ; « 2 » = Clip ; « 3 » = Autre. |
| [[!UICONTROL Format de flux]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/standard-metadata/stream-format) | `streamFormat` | Chaîne | Non | Format du flux (HD, SD). |
| [[!UICONTROL Type de flux]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/stream-type) | `streamType` | Chaîne | Non | Type du flux de médias. |
| [[!UICONTROL Version &#x200B;]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/core/app-version) | `appVersion` | Chaîne | Non | Version de l’application du lecteur multimédia. Cela peut avoir n’importe quelle valeur personnalisée adaptée à votre lecteur. |
