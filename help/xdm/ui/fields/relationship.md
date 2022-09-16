---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;relation;champ;
solution: Experience Platform
title: Définition des champs de relation dans l’interface utilisateur
description: Découvrez comment définir un champ de relation dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Définition des champs de relation dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un [schéma d’union](../../schema/composition.md#union) est une vue unifiée de tous les schémas appartenant à la même classe qui ont également été activés pour [Real-time Customer Profile](../../../profile/home.md). Le schéma d’union est exploité par Profile afin de construire une représentation complète d’un client à partir de données d’expérience disparates.

Dans certains cas, vous ingérez peut-être des données qui ne font pas nécessairement partie d’un profil, mais qui sont néanmoins liées au profil. Un exemple de ce type de données serait un champ &quot;hôtel préféré&quot; pour un client. Puisque les attributs de l’hôtel préféré d’une personne ne sont pas les attributs de la personne elle-même, un hôtel est mieux représenté par un schéma distinct basé sur une classe personnalisée plutôt que par un schéma distinct. [!DNL XDM Individual Profile].

Comme les schémas d’union ne sont basés que sur des schémas qui partagent la même classe, l’activation simple du schéma &quot;Hotels&quot; à utiliser dans Profile n’inclut pas son schéma d’union de champs pour [!DNL XDM Individual Profile]. Vous devez plutôt définir une relation entre &quot;Hotels&quot; et un autre schéma appartenant à l’union. Cela implique de définir une **champ de relation** dans un schéma source qui référence l’identité Principale d’un schéma de destination.

Pour obtenir des instructions détaillées sur la définition d’une relation entre deux schémas dans l’interface utilisateur de Adobe Experience Platform, reportez-vous à la section [tutoriel sur l’interface utilisateur de relation](../../tutorials/relationship-ui.md).
