---
title: Réinitialiser l’ID de fusion
description: Action obsolète permettant de séparer des événements appelés sur la même page.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Réinitialiser l’ID de fusion

>[!IMPORTANT]
>
>Cette action est obsolète. Utilisez plutôt les paramètres [Collecter les clics sur les liens internes](../configure/data-collection.md#collect-internal-link-clicks) .

Le type d’action **[!UICONTROL Reset merge ID]** vous permet de séparer des événements appelés sur la même page. Il est généralement utilisé dans les scénarios de lien interne où vous pouvez avoir plusieurs payloads à envoyer à Adobe. Cette action vous permet de réinitialiser l’ID de fusion d’un événement afin qu’il ne soit pas considéré comme faisant partie du même événement après son arrivée dans Edge Network.

Si vous souhaitez contrôler la manière dont plusieurs événements d’une même page sont séparés ou fusionnés, utilisez l’option [Collecter les clics sur les liens internes](../configure/data-collection.md#collect-internal-link-clicks) lors de la configuration de l’extension de balise.
