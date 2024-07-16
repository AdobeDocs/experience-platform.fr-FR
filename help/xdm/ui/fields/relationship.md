---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;relation;champ;
solution: Experience Platform
title: Définition des champs de relation dans l’interface utilisateur
description: Découvrez comment définir un champ de relation dans l’interface utilisateur Experience Platform.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Définition des champs de relation dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un [schéma d’union](../../schema/composition.md#union) est une vue unifiée de tous les schémas appartenant à la même classe qui ont également été activés pour [Real-time Customer Profile](../../../profile/home.md). Le schéma d’union est exploité par Profile afin de construire une représentation complète d’un client à partir de données d’expérience disparates.

Dans certains cas, vous ingérez peut-être des données qui ne font pas nécessairement partie d’un profil, mais qui sont néanmoins liées au profil. Un exemple de ce type de données serait un champ &quot;hôtel préféré&quot; pour un client. Puisque les attributs de l’hôtel préféré d’une personne ne sont pas les attributs de la personne elle-même, un hôtel est mieux représenté par un schéma distinct basé sur une classe personnalisée plutôt que [!DNL XDM Individual Profile].

Les schémas d’union étant basés uniquement sur des schémas qui partagent la même classe, l’activation simple du schéma &quot;Hotels&quot; à utiliser dans Profile n’inclura pas son schéma d’union de champs pour [!DNL XDM Individual Profile]. Vous devez plutôt définir une relation entre &quot;Hotels&quot; et un autre schéma appartenant à l’union. Cela implique de définir un **champ de relation** dans un schéma source qui référence l’identité principale d’un schéma de référence.

Pour obtenir des instructions détaillées sur la définition d’une relation entre deux schémas dans l’interface utilisateur de Adobe Experience Platform, consultez le [tutoriel sur l’interface utilisateur des relations](../../tutorials/relationship-ui.md).
