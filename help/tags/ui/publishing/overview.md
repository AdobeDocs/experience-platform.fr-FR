---
title: Présentation de la publication
description: Découvrez le processus de publication des modifications apportées à vos bibliothèques de code de gestion des balises dans Adobe Experience Platform.
exl-id: 32eaad87-d7dc-4812-b546-a136511512fe
TQID: https://experienceleague.adobe.com/wVtU5W3rKpDY4aWKzzLHqCccO55cBkvLiFghxObwqEw
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: abc02dd6-664f-446a-9aaa-675bc0f2fe4aid: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 570
ht-degree: 95%

---

# Présentation de la publication

Adobe Experience Platform vous permet d’encapsuler les modifications apportées à votre code de gestion des balises dans des bibliothèques individuelles. Plusieurs bibliothèques pouvant désormais être développées en parallèle par différentes équipes, ces bibliothèques doivent suivre un processus délibéré et autorisé afin de fusionner les modifications avant le transfert vers votre environnement de production.

Au niveau de base, chaque bibliothèque passe par le processus de publication suivant :

1. Créez une nouvelle bibliothèque (ou modifiez une bibliothèque existante) dans un environnement de développement.
1. Testez la fonctionnalité de la bibliothèque dans un environnement d’évaluation si nécessaire.
1. Déployez la bibliothèque dans votre environnement de production.

Supposons que vous créiez un nouvel événement de « passage en caisse » ainsi qu’un nouvel élément de données de chiffre d’affaires associé à cet événement, et que vous apportiez une modification à la configuration de l’extension Adobe Analytics pour la prise en charge de ce nouvel événement et de ce nouvel élément de données. Vous pouvez inclure toutes ces modifications dans une nouvelle bibliothèque et utiliser le processus de publication afin de les tester, de les approuver et de les publier sous la forme d’une seule unité.

Pour une présentation générale du processus de publication des bibliothèques, notamment des détails sur la manière dont les bibliothèques héritent des ressources des versions en amont en fonction de leur état de publication, consultez le [guide des flux de publication](./publishing-flow.md).

Outre le flux de publication, il est important de comprendre le fonctionnement de plusieurs composants et relations afin de développer et de publier efficacement vos bibliothèques. Le tableau suivant décrit chacun de ces concepts clés et fournit des liens vers leur documentation pour vous aider à en savoir plus sur chacun d’entre eux :

| Composant | Description |
| --- | --- |
| Bibliothèques | Une bibliothèque est un ensemble d’instructions qui définit la façon dont les extensions, les éléments de données et les règles interagissent les uns avec les autres, ainsi qu’avec votre site web. Lorsqu’une bibliothèque est compilée pour être déployée dans un environnement, elle devient une version.<br><br>Reportez-vous à la présentation des [bibliothèques](./libraries.md) pour plus d’informations sur la création, la gestion et l’activation de bibliothèques dans l’interface utilisateur. |
| Versions | Une version est une bibliothèque compilée. Lorsqu’elle est déployée dans un environnement, une version fournit l’ensemble réel des fichiers contenant le code qui est distribué au navigateur de chaque utilisateur lorsque ce dernier consulte votre site.<br><br>Reportez-vous à la présentation des [versions](./builds.md) pour plus d’informations sur le contenu et le format des versions. |
| Environnements | Un environnement de balises est un ensemble d’instructions de déploiement qui indique à Experience Platform le format souhaité de votre version et l’emplacement où vous souhaitez qu’elle soit livrée.<br><br>Reportez-vous à la présentation des [environnements](./environments.md) pour plus d’informations sur les différents types d’environnements ainsi que sur la manière d’installer et de configurer des environnements existants ou d’en créer de nouveaux. |
| Hôtes | Un hôte représente les détails de la connexion permettant à un environnement de distribuer une version à votre site web. Vous pouvez laisser Adobe gérer l’hébergement de votre version ou bien fournir des informations sur vos propres serveurs hôtes.<br><br>Reportez-vous à la présentation des [hôtes](./hosts/hosts-overview.md) pour plus d’informations sur chaque option d’hébergement. |
| Code côté client | Le code côté client est l’ensemble des scripts que vous placez dans le code source de votre site ou application et qui indique à chaque appareil client où récupérer la version. Le code est associé à un environnement et peut changer lorsque vous apportez des modifications à la configuration de votre environnement.<br><br>Pour en savoir plus, consultez la section portant sur les [codes intégrés](./environments.md#embed-code) dans la présentation des environnements. |

## Étapes suivantes

Ce document présente un aperçu des différents composants impliqués dans la publication de bibliothèques de balises dans Adobe Experience Platform. Reportez-vous à la documentation à laquelle renvoie les différentes sections de ce guide pour en savoir plus sur les détails du processus de publication.
