---
title: Gestion des événements d’affichage dans le SDK Web
description: Décrit ce que sont les événements d’affichage et comment les utiliser dans le SDK Web.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Gestion des événements d’affichage dans le SDK Web

Les événements d’affichage sont utilisés par Web SDK pour informer votre service de personnalisation ou d’analyse lorsqu’un contenu de personnalisation spécifique est affiché sur une page. L’envoi d’événements d’affichage améliore la précision des mesures de personnalisation et vous donne un aperçu précis de ce que les utilisateurs voient sur votre page.

>[!NOTE]
>
>Les événements d’affichage ne sont pas envoyés automatiquement lors de l’appel de la fonction `applyPropositions`.

## Envoyer automatiquement des événements d’affichage

L’envoi d’événements d’affichage fournit automatiquement des mesures d’analyse plus précises, puisque l’événement est envoyé immédiatement après le chargement de la personnalisation. Cette implémentation présente également une méthode d’implémentation plus rationalisée.

Pour envoyer automatiquement des événements d’affichage après le rendu du contenu personnalisé sur la page, vous devez configurer les paramètres suivants :

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` ou non spécifié

Web SDK envoie les événements d’affichage immédiatement après le rendu d’une personnalisation suite à un appel `sendEvent`.

## Envoi d’événements d’affichage dans les appels sendEvent suivants

Par rapport à l’envoi automatique d’événements d’affichage , lorsque vous les incluez dans les appels d’`sendEvent` suivants, vous avez également la possibilité d’inclure plus d’informations sur le chargement de la page dans l’appel. Il peut s’agir d’informations supplémentaires, qui n’étaient pas disponibles lors de la demande du contenu personnalisé.

En outre, l’envoi d’événements d’affichage dans les appels `sendEvent` réduit les erreurs de taux de rebond lors de l’utilisation d’Adobe Analytics.

>[!IMPORTANT]
>
>Lors de l’utilisation de propositions générées manuellement, les événements d’affichage ne sont pris en charge que par le biais d’appels `sendEvent`. Dans ce cas, vous ne pouvez pas envoyer automatiquement des événements d’affichage.

### Envoyer des événements d’affichage pour les propositions générées automatiquement

Pour envoyer des événements d’affichage pour les propositions générées automatiquement, vous devez configurer les paramètres suivants dans l’appel `sendEvent` :

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` pour le haut de la page visitée

Pour envoyer les événements d’affichage, appelez `sendEvent` avec `personalization.includeRenderedPropositions: true`

### Envoi d’événements d’affichage pour les propositions générées manuellement

Pour envoyer des événements d’affichage pour les propositions générées manuellement, vous devez les inclure dans le champ XDM `_experience.decisioning.propositions`, y compris les champs `id`, `scope` et `scopeDetails` des propositions.

En outre, définissez le champ `include _experience.decisioning.propositionEventType.display` sur `1`.
