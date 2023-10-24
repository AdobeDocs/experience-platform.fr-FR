---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2023 pour Adobe Experience Platform.
source-git-commit: d024596c7d85139721ef370f9e081911a217d9ba
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 53%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 octobre 2023**

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Sources](#sources)

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mise à jour de l’authentification pour la zone d’entrée des données | Vous pouvez désormais voir la date d’expiration désignée de votre zone d’entrée de données lors de l’affichage de vos informations d’identification. Vous devez actualiser votre jeton avant la date d’expiration afin de continuer à l’utiliser dans votre application. Si vous n’actualisez pas manuellement votre jeton avant la date d’expiration indiquée, celui-ci s’actualisera automatiquement et vous fournira un nouveau jeton la prochaine fois que vous récupérerez vos informations d’identification. Pour plus d’informations, consultez la documentation relative à [utilisation de la zone d’entrée des données](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [vue d’ensemble des sources](../../sources/home.md).
