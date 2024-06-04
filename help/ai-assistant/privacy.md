---
title: Confidentialité, sécurité et gouvernance dans l’assistant d’IA
description: Découvrez les pratiques en matière de confidentialité, de sécurité et de gouvernance de l’assistant d’IA.
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: 1762fcbcc730ccb08340a71383c90404c3fea614
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Confidentialité, sécurité et gouvernance dans l’assistant d’IA

L’assistant d’IA dans Adobe Experience Platform est placé au premier plan de la confidentialité, de la sécurité et de la gouvernance.

Lisez ce document pour en savoir plus sur les fonctionnalités axées sur la confiance des clients que vous pouvez attendre de l’assistant d’IA :

* Aucune donnée personnelle n’est utilisée aujourd’hui par l’assistant d’IA, même à des fins de formation.
* L’assistant d’IA ne connaît pas les données des consommateurs.
* Toutes les [contrôle d&#39;accès](../access-control/home.md) Les politiques seront honorées par l’assistant d’IA.
   * Toutes les nouvelles stratégies de contrôle d’accès basées sur des attributs sont répercutées dans l’assistant d’IA après un maximum de 24 heures*
* Vous devez disposer d’une autorisation explicite pour interagir avec l’assistant d’IA.
   * Vous pouvez définir des autorisations différentes pour Experience Platform et Journey Optimizer à l’aide de la variable [Interface utilisateur des autorisations](../access-control/abac/ui/permissions.md) et vous pouvez utiliser la variable [Admin Console](../access-control/ui/browse.md) pour attribuer des autorisations au Customer Journey Analytics.
   * Les autorisations sont granulaires et votre administrateur d’environnement de test peut configurer lequel de vos utilisateurs peut poser différentes catégories de questions (questions basées sur les connaissances du produit avec l’assistant d’IA ou questions relatives aux informations opérationnelles).
* L’assistant d’IA est une fonctionnalité prête pour les HIPAA qui répond aux exigences de cette dernière en matière de traitement et d’utilisation des informations sur la santé protégées (IAP).
* Vous pouvez afficher un journal de vos interactions précédentes avec l’assistant d’IA avec une politique de conservation des données de 30 jours.
* L’assistant d’IA est associé à des données spécifiques à un environnement de test et à la documentation des Adobes publics lorsque vous répondez aux invites utilisateur. Les données ne sont pas partagées entre les environnements de test.
* Les invites que vous fournissez à l’assistant d’IA ne sont pas partagées avec d’autres clients.


**Cela signifie que si de nouvelles étiquettes sont ajoutées aux champs et aux objets ou si de nouvelles stratégies sont créées, l’assistant d’IA peut prendre jusqu’à 24 heures pour les honorer. Pendant ces 24 heures, les utilisateurs ayant un accès nouvellement restreint peuvent toujours accéder à ces champs et objets.*
