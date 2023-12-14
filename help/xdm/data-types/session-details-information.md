---
title: Type de données Informations sur les détails de la session
description: Découvrez le type de données XDM (Experience Data Model) Informations sur les détails de la session.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 20%

---

# [!UICONTROL Informations sur la session] type de données

[!UICONTROL Informations sur la session] est un type de données XDM (Experience Data Model) standard qui effectue le suivi des données liées aux sessions de lecture multimédia. Le schéma englobe un large éventail de propriétés qui fournissent des informations sur la manière dont le contenu multimédia est utilisé. Utilisez la variable [!UICONTROL Informations sur la session] type de données pour capturer l’engagement des utilisateurs en enregistrant les événements de lecture, les interactions publicitaires, les marqueurs de progression, les pauses et d’autres mesures. Cela offre des informations précieuses sur le comportement des utilisateurs et les schémas de consommation de contenu.

+++Sélectionnez cette option pour afficher un diagramme du type de données Informations sur les détails de la session.
![Schéma du type de données Informations sur les détails de la session.](../images/data-types/session-details-information.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL ID de session multimédia] | `ID` | chaîne | La variable [!UICONTROL ID de session multimédia] identifie une instance d’une diffusion de contenu unique à une lecture individuelle. |
| [!UICONTROL Identifiant de contenu] | `name` | chaîne | **Obligatoire** La variable [!UICONTROL Identifiant de contenu] est un identifiant unique du contenu. Il peut être utilisé pour renvoyer vers d’autres ID d’industrie ou CMS. |
| [!UICONTROL Nom du contenu] | `friendlyName` | Chaîne | La variable [!UICONTROL Nom du contenu] est le nom &quot;convivial&quot; (lisible par l’utilisateur) du contenu. |
| [!UICONTROL Longueur du contenu multimédia] | `length` | Nombre entier | **Obligatoire** La variable [!UICONTROL Longueur du contenu multimédia] contient la durée/l’exécution de l’élément : il s’agit de la durée maximale (ou durée) du contenu en cours de consommation (en secondes). |
| [!UICONTROL Type de contenu diffusé] | `contentType` | Chaîne | **Obligatoire** La variable [!UICONTROL Type de contenu diffusé] de la diffusion de flux. Valeurs disponibles par [!UICONTROL Type de diffusion] inclure :<br>Audio : &quot;chanson&quot;, &quot;podcast&quot;, &quot;audiobook&quot; et &quot;radio&quot;;<br>Vidéo : &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; et &quot;DVoD&quot;.<br>Les clients peuvent fournir des valeurs personnalisées pour ce paramètre. |
| [!UICONTROL Nom du lecteur de contenu] | `playerName` | Chaîne | **Obligatoire** Nom du lecteur de contenu. |
| [!UICONTROL Canal de contenu] | `channel` | Chaîne | **Obligatoire** La variable [!UICONTROL Canal de contenu] est le canal de distribution à partir duquel le contenu a été lu. |
| [!UICONTROL Version] | `appVersion` | Chaîne | Version du SDK utilisée par le lecteur. Cela peut avoir toute valeur personnalisée qui convient à votre lecteur. |
| [!UICONTROL Nom de la série] | `show` | Chaîne | Nom du programme/de la série. Le nom du programme n’est requis que si le programme fait partie d’une série. |
| [!UICONTROL Numéro de saison] | `season` | Chaîne | La variable [!UICONTROL Numéro de saison] à laquelle le programme appartient. La Saison n’est requise que si le programme fait partie d’une série. |
| [!UICONTROL Numéro d’épisode] | `episode` | Chaîne | Numéro de l’épisode. |
| [!UICONTROL ID de ressource] | `assetID` | Chaîne | La variable [!UICONTROL ID de ressource] est l’identifiant unique du contenu de la ressource multimédia, tel que l’identifiant d’épisode de la série télévisée, l’identifiant de la ressource de film ou l’identifiant d’événement en direct. En règle générale, ces identifiants sont issus des autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes. |
| [!UICONTROL Genre] | `genre` | Chaîne | Type ou regroupement de contenu tel que défini par le producteur de contenu. Les valeurs doivent être délimitées par des virgules dans l’implémentation de la variable. |
| [!UICONTROL Date de première diffusion] | `firstAirDate` | Chaîne | Date à laquelle le contenu a été diffusé à la télévision pour la première fois. Tout format de date est acceptable, mais Adobe recommande : AAAA-MM-JJ. |
| [!UICONTROL Date de première distribution numérique] | `firstDigitalDate` | Chaîne | Date à laquelle le contenu a été diffusé pour la première fois sur une chaîne ou une plateforme numérique. Tout format de date est acceptable, mais Adobe recommande : AAAA-MM-JJ. |
| [!UICONTROL Valeur de notation] | `rating` | Chaîne | Évaluation telle que définie par les directives parentales de la télévision. |
| [!UICONTROL  Nom du créateur] | `originator` | Chaîne | Nom du créateur de contenu. |
| [!UICONTROL Réseau de diffusion] | `network` | Chaîne | Nom du réseau/canal. |
| [!UICONTROL Type de programme] | `showType` | Chaîne | Type de contenu, par exemple, bande-annonce ou épisode complet. |
| [!UICONTROL Type de chargement de publicité] | `adLoad` | Chaîne | Type de publicité chargée tel que défini par la représentation interne de chaque client. |
| [!UICONTROL Identifiant MVPD] | `mvpd` | Chaîne | La variable [!UICONTROL Identifiant MVPD] qui a été fourni via l’authentification par Adobe. |
| [!UICONTROL Média autorisé] | `authorized` | Chaîne | Confirme si l’utilisateur a été autorisé via l’authentification Adobe. |
| [!UICONTROL Partie de la journée] | `dayPart` | Chaîne | Propriété qui définit l’heure de la journée à laquelle le contenu a été diffusé ou lu. Cela peut avoir une valeur définie selon les besoins par les clients. |
| [!UICONTROL Type de flux] | `feed` | Chaîne | Le type de flux, qui peut représenter des données liées au flux réel telles que EAST HD ou SD, ou la source du flux telle qu’une URL. |
| [!UICONTROL Format de diffusion] | `streamFormat` | Chaîne | Format du flux (HD, SD). |
| [!UICONTROL Reprendre] | `hasResume` | Booléen | Marque chaque lecture qui a été reprise après plus de 30 minutes de mise en mémoire tampon, de mise en pause ou de blocage. |
| [!UICONTROL Type de diffusion] | `streamType` | Chaîne | Type de flux multimédia. |
| [!UICONTROL Artiste] | `artist` | Chaîne | Nom de l’artiste ou du groupe qui effectue l’enregistrement musical ou vidéo. |
| [!UICONTROL Album] | `album` | Chaîne | Nom de l’album auquel appartient l’enregistrement musical ou la vidéo. |
| [!UICONTROL Libellé d’enregistrement] | `label` | Chaîne | Nom du libellé de l’enregistrement. |
| [!UICONTROL Auteur] | `author` | Chaîne | Nom de l’auteur du média. |
| [!UICONTROL Radio] | `station` | Chaîne | Nom de la station de radio sur laquelle le son est lu. |
| [!UICONTROL Éditeur] | `publisher` | Chaîne | Nom de l’éditeur de contenu audio. |
| [!UICONTROL Segment de vidéo] | `segment` | Chaîne | Intervalle qui décrit la partie du contenu visualisée en minutes. |
| [!UICONTROL Indicateur de média téléchargé] | `isDownloaded` | Booléen | La diffusion a été lue localement sur l’appareil après avoir été téléchargée. |
| [!UICONTROL Données fédérées] | `isFederated` | Booléen | [!UICONTROL Données fédérées] est définie sur true lorsque l’accès est fédéré (c’est-à-dire qu’il est reçu par le client dans le cadre d’un partage de données fédérée, plutôt que dans le cadre de sa propre mise en oeuvre). |
| [!UICONTROL Démarrages de média] | `isViewed` | Booléen | Événement de chargement pour le média. Cela se produit lorsque la visionneuse sélectionne le bouton de lecture. Cela compte même s’il existe des publicités preroll, des mises en mémoire tampon, des erreurs, etc. |
| [!UICONTROL Démarrages de contenu] | `isPlayed` | Booléen | [!UICONTROL Démarrages de contenu] devient true lorsque la première image du média est visionnée. Si l’utilisateur abandonne au cours d’une publicité, d’une mise en mémoire tampon, etc., aucune [!UICONTROL Démarrages de contenu] . |
| [!UICONTROL Le contenu se termine] | `isCompleted` | Booléen | [!UICONTROL Le contenu se termine] indique si une ressource multimédia minutée a été visionnée jusqu’à la fin. Cet événement ne signifie pas nécessairement que le spectateur a visionné toute la vidéo ; il aurait pu sauter devant. |
| [!UICONTROL Temps passé sur le contenu] | `timePlayed` | Nombre entier | [!UICONTROL Temps passé sur le contenu] additionne la durée de l’événement (en secondes) pour tous les événements de type LECTURE sur le contenu principal. |
| [!UICONTROL Temps passé sur le média] | `totalTimePlayed` | Nombre entier | Décrit le temps total passé par un utilisateur sur un fichier multimédia minuté spécifique, qui inclut le temps passé à regarder les publicités. |
| [!UICONTROL Durée de lecture unique] | `uniqueTimePlayed` | Nombre entier | Décrit la somme des intervalles uniques affichés par un utilisateur sur une ressource multimédia minutée, c’est-à-dire que les intervalles de lecture affichés plusieurs fois ne sont comptabilisés qu’une seule fois. |
| [!UICONTROL Audience moyenne par minute] | `averageMinuteAudience` | Nombre | Décrit la durée moyenne de visionnage du contenu pour un élément multimédia spécifique, c’est-à-dire la durée totale de visionnage du contenu divisée par la durée de toutes les sessions de lecture. |
| [!UICONTROL Nombre de publicités] | `adCount` | Nombre entier | Nombre de publicités démarrées au cours de la lecture. |
| [!UICONTROL Nombre de chapitres] | `chapterCount` | Nombre entier | Nombre de chapitres démarrés au cours de la lecture. |
| [!UICONTROL Marqueur de progression de 10 %] | `hasProgress10` | Booléen | Indique que le curseur de lecture a passé le marqueur des 10 % du média en fonction de la longueur du flux. Le marqueur n’est compté qu’une seule fois, même si vous effectuez une recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.   |
| [!UICONTROL Marqueur de progression de 25 %] | `hasProgress25` | Booléen | Indique que le curseur de lecture a passé le marqueur des 25 % du média en fonction de la longueur du flux. Le marqueur n’est compté qu’une seule fois, même si vous effectuez une recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.   |
| [!UICONTROL Marqueur de progression de 50 %] | `hasProgress50` | Booléen | Indique que le curseur de lecture a passé le marqueur des 50 % du média en fonction de la longueur du flux. Le marqueur n’est compté qu’une seule fois, même si vous effectuez une recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.   |
| [!UICONTROL Marqueur de progression de 75 %] | `hasProgress75` | Booléen | Indique que le curseur de lecture a passé le marqueur des 75 % du média en fonction de la longueur du flux. Le marqueur n’est compté qu’une seule fois, même si vous effectuez une recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.   |
| [!UICONTROL Marqueur de progression de 95 %] | `hasProgress95` | Booléen | Indique que le curseur de lecture a passé le marqueur des 95 % du média en fonction de la longueur du flux. Le marqueur n’est compté qu’une seule fois, même si vous effectuez une recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.   |
| [!UICONTROL Diffusions estimées] | `estimatedStreams` | Nombre | Nombre estimé de diffusions vidéo ou audio pour chaque élément de contenu individuel. |
| [!UICONTROL Diffusions touchées par la pause] | `hasPauseImpactedStreams` | Booléen | Indique si une ou plusieurs pauses ont eu lieu au cours de la lecture d’un seul élément multimédia. |
| [!UICONTROL Événements de mise en pause] | `pauseCount` | Nombre entier | [!UICONTROL Événements de mise en pause] comptabilise le nombre de mises en pause qui se sont produites pendant la lecture. |
| [!UICONTROL Durée totale de pause] | `pauseTime` | Nombre entier | [!UICONTROL Durée totale de pause] décrit la durée en secondes pendant laquelle la lecture a été interrompue par l’utilisateur. |
| [!UICONTROL Affichages de segments du média] | `hasSegmentView` | Booléen | [!UICONTROL Affichages de segments du média] indique lorsqu’au moins une image, pas nécessairement la première, a été visionnée. |
| [!UICONTROL Délai d’expiration du serveur de session multimédia] | `secondsSinceLastCall` | Nombre | La variable [!UICONTROL Délai d’expiration du serveur de session multimédia] indique le temps, en secondes, qui s’est écoulé entre la dernière interaction connue de l’utilisateur et le moment où la session a été fermée. |
| [!UICONTROL Réseau de diffusion de contenu] | `cdn` | Chaîne | La variable [!UICONTROL Réseau de diffusion de contenu] du contenu lu. |
| [!UICONTROL Pev3] | `pev3` | Chaîne | [!UICONTROL Pev3] est le type de flux média utilisé pour la création de rapports. |
| [!UICONTROL Pccr] | `pccr` | Booléen | [!UICONTROL Pccr] indique qu’une redirection a eu lieu. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
