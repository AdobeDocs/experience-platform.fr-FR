---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;interface utilisateur;espace de travail;relation;champ;
solution: Experience Platform
title: Définir des champs de relation dans l’interface utilisateur
description: Découvrez comment définir un champ de relation dans l’interface utilisateur Experience Platform.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
TQID: https://experienceleague.adobe.com/5ojlMvkRONGd1yVuWMvv0BYMHzzw-cled0PiNX3eFo4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 250
ht-degree: 0%

---

# Définir des champs de relation dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un [schéma d’union](../../schema/composition.md#union) est une vue unifiée de tous les schémas appartenant à la même classe qui ont également été activés pour le [profil client en temps réel](../../../profile/home.md). Le schéma d’union est exploité par Profile afin de construire une représentation complète d’un client à partir de données d’expérience disparates.

Dans certains cas, il se peut que vous ingériez des données qui ne font pas nécessairement partie d’un profil, mais qui sont néanmoins liées à celui-ci. Un exemple de ce type de données serait un champ « hôtel préféré » pour un client. Comme les attributs de l’hôtel préféré d’une personne ne sont pas des attributs de la personne elle-même, il est préférable de représenter un hôtel par un schéma distinct basé sur une classe personnalisée plutôt que sur [!DNL XDM Individual Profile].

Puisque les schémas d’union sont uniquement basés sur des schémas partageant la même classe, le simple fait d’activer le schéma « Hôtels » à utiliser dans Profile n’inclut pas son schéma d’union de champs pour [!DNL XDM Individual Profile]. Vous devez plutôt définir une relation entre « Hôtels » et un autre schéma appartenant à l’union. Cela implique de définir un **champ de relation** dans un schéma source qui fait référence à l’identité principale d’un schéma de référence.

Pour obtenir des instructions détaillées sur la définition d’une relation entre deux schémas dans l’interface utilisateur de Adobe Experience Platform, consultez le tutoriel sur l’interface utilisateur [relation](../../tutorials/relationship-ui.md).
