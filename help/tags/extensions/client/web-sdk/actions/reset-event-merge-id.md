---
title: Réinitialiser l’ID de fusion
description: Action obsolète permettant de séparer des événements appelés sur la même page.
exl-id: a11a9b7c-2751-46f9-86cf-2869b56ff481
source-git-commit: 2d7ba15f918c314fe219212df82aec6d7ac1fc77
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Réinitialiser l’ID de fusion

>[!IMPORTANT]
>
>Cette action est obsolète. Utilisez plutôt les paramètres [Collecter les clics sur les liens internes](../configure/data-collection.md#collect-internal-link-clicks) .

Le type d’action **[!UICONTROL Réinitialiser l’ID de fusion]** permet de séparer les événements appelés sur la même page. Il est généralement utilisé dans les scénarios de lien interne où vous pouvez avoir plusieurs payloads à envoyer à Adobe. Cette action vous permet de réinitialiser l’ID de fusion d’un événement afin qu’il ne soit pas considéré comme faisant partie du même événement après son arrivée dans Edge Network.

Si vous souhaitez contrôler la manière dont plusieurs événements d’une même page sont séparés ou fusionnés, utilisez l’option [Collecter les clics sur les liens internes](../configure/data-collection.md#collect-internal-link-clicks) lors de la configuration de l’extension de balise.
