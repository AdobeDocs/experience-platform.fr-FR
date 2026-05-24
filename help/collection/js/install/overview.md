---
title: Présentation de l’installation de Web SDK
description: Découvrez comment installer Experience Platform Web SDK.
keywords: installation du sdk web;installer le sdk web;internet explorer;promesse;package npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
TQID: https://experienceleague.adobe.com/C8-LOh7sINppoBOGZP9YUuRnhj7-qxXb8c2Gmziecdw
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: b64298cc-90cc-46b7-8917-ee391f1c7516id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: de9975b2-c43a-4287-9698-4f4cad92b83f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 232
ht-degree: 0%

---

# Présentation de l’installation de Web SDK

Il existe trois manières prises en charge d’utiliser Adobe Experience Platform Web SDK :

1. **[Extension de balise Web SDK](/help/tags/extensions/client/web-sdk/overview.md)** : Adobe recommande d’utiliser cette méthode. Installez une balise de chargement sur votre site, puis utilisez l’interface utilisateur de la collecte de données de Adobe Experience Platform pour configurer votre implémentation.
1. **[Bibliothèque JavaScript Web SDK](library.md)** : référencez un fichier de bibliothèque hébergé sur un réseau CDN ou hébergez le fichier de bibliothèque à l’aide de votre propre infrastructure. Effectuez des appels à la bibliothèque dans le code de votre site.
1. **[NPM](npm.md)** : installez le SDK Web sur votre site à l’aide du gestionnaire de packages NPM.

## Conditions préalables

Avant d’utiliser ou d’installer le SDK Web, vous devez respecter les conditions suivantes :

* L’architecture dans Adobe Experience Platform doit d’abord être configurée. Ces paramètres comprennent tous les schémas, identités et flux de données nécessaires.
* Vous devez disposer des autorisations appropriées configurées pour accéder aux outils appropriés. Par exemple, si votre organisation décide d’utiliser l’extension de balise, vous devez disposer des autorisations appropriées pour accéder à l’interface utilisateur de la collecte de données. Pour plus d’informations, voir [Autorisations de collecte de données](../../permissions.md).
* Il est recommandé d’avoir un domaine propriétaire (CNAME). Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous pouvez l’utiliser. Les tests en développement fonctionnent sans CNAME, mais Adobe recommande d’en avoir un avant la publication en production. Voir [Identifiants d’appareils propriétaires](../../identity/fpid.md) pour plus d’informations.
