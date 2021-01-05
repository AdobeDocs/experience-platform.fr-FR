---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;relationship;field;
solution: Experience Platform
title: Définir un champ de relation dans l’interface utilisateur
description: Découvrez comment définir un champ de relation dans l’interface utilisateur de l’Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Définir un champ de relation dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un [schéma d’union](../../schema/composition.md#union) est une vue unifiée de tous les schémas appartenant à la même classe qui ont également été activés pour [Profil client en temps réel](../../../profile/home.md). Le schéma d’union est exploité par Profil afin de construire une représentation complète d’un client à partir de données d’expérience disparates.

Dans certains cas, vous importez des données qui ne font pas nécessairement partie d’un profil, mais qui sont néanmoins liées au profil. Un exemple de ce type de données serait un champ &quot;hôtel préféré&quot; pour un client. Comme les attributs d&#39;un hôtel favori ne sont pas ceux de la personne elle-même, un hôtel est mieux représenté par un schéma séparé basé sur une classe personnalisée plutôt que [!DNL XDM Individual Profile].

Étant donné que les schémas d&#39;union ne sont basés que sur des schémas partageant la même classe, la simple activation du schéma &quot;Hôtels&quot; pour utilisation dans le Profil n&#39;inclut pas ses champs schéma d&#39;union pour [!DNL XDM Individual Profile]. Vous devez plutôt définir une relation entre &quot;Hôtels&quot; et un autre schéma appartenant à l&#39;union. Cela implique de définir un champ de relation **** dans un schéma source qui référence l&#39;identité Principale d&#39;un schéma de destination.

Pour obtenir des instructions détaillées sur la définition d’une relation entre deux schémas dans l’interface utilisateur Adobe Experience Platform, consultez le [didacticiel sur l’interface utilisateur des relations](../../tutorials/relationship-ui.md).