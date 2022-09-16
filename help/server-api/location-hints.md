---
title: Conseils de localisation
description: Cet article explique le fonctionnement des indicateurs d’emplacement dans l’API Edge Network Server, de sorte que les demandes des utilisateurs finaux puissent toujours être acheminées vers le même serveur.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 80c527ab3c82e01fe19e5003e224d63e79b23bdc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Conseils de localisation

## Présentation {#overview}

Le [!DNL Adobe Experience Platform Edge Network] utilise plusieurs serveurs répartis dans le monde pour garantir des temps de réponse rapides, quel que soit l’emplacement de l’utilisateur final. Il utilise également le routage basé sur DNS pour s’assurer que les demandes sont toujours acheminées vers l’emplacement réseau Edge le plus proche des utilisateurs finaux.

Si les utilisateurs finaux se connectent à un VPN ou changent de type de réseau sur leurs appareils mobiles au cours d’une session, les demandes Edge Network peuvent souvent être acheminées vers un autre emplacement. Le routage de mi-session entre les serveurs peut s’avérer problématique, car les solutions Adobe Experience Platform et Adobe Experience Cloud stockent les informations de profil utilisateur final sur le réseau Edge.

C&#39;est là que les indices de localisation entrent en jeu.

Pour garantir que les utilisateurs finaux interagissent toujours avec le serveur régional Edge Network qui contient les données de profil actuelles, la fonctionnalité d’indicateurs d’emplacement garantit que toutes les requêtes envoyées au réseau Edge sont envoyées au même serveur que celui où a été effectuée la première requête d’une session. Cela permet aux utilisateurs d’avoir une expérience cohérente, quelles que soient les modifications réseau qu’ils peuvent subir au cours d’une session.

## Utilisation des conseils d’emplacement

Les indicateurs d’emplacement sont inclus dans la réponse de la requête réseau Edge initiale et dans toutes les requêtes suivantes, comme illustré dans l’exemple ci-dessous :

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

Le `EdgeNetwork` La portée contient toutes les informations pertinentes dont le réseau Edge a besoin pour acheminer les requêtes suivantes en conséquence. Dans la réponse de la requête initiale et de chaque requête ultérieure au réseau Edge, il y aura une section dans la gestion avec un type de `locationHint:result`.

L’indice associé au `EdgeNetwork` scope peut contenir l’une des valeurs suivantes :

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Format d’API**

Pour garantir que les requêtes suivantes sont correctement acheminées, insérez l’indicateur d’emplacement dans le chemin d’URL des appels API suivants entre le chemin de base, généralement `ee`, et `v2` Version de l’API.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Stockage des indicateurs d’emplacement dans les cookies {#storing-hints-in-cookies}

Pour vous assurer que l’indicateur d’emplacement renvoyé par le réseau Edge persiste pendant la durée de la session, vous pouvez stocker la valeur de l’indicateur d’emplacement dans un cookie, ainsi que la durée de vie du cookie, qui est contenue dans la variable `ttlSeconds` (généralement 1 800 secondes).

Comme pour la plupart des cookies, vous devez prolonger la durée de vie de ce cookie chaque fois qu’une réponse est apportée par le réseau Edge. Pour garantir une compatibilité maximale avec le SDK Web, utilisez le nom du cookie. `kndctr_{IMSORG}_AdobeOrg_cluster`. Les identifiants de l’organisation IMS se terminent généralement par `@AdobeOrg`. Le `@` doit être convertie en trait de soulignement pour que le cookie soit au bon format.
