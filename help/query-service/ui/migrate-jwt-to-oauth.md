---
title: Migration des informations d’identification de serveur à serveur JWT vers OAuth
description: Découvrez comment migrer les informations d’identification JWT non expirantes vers les informations d’identification de serveur à serveur OAuth dans Adobe Experience Platform afin de conserver un accès sécurisé et ininterrompu à Query Service avant la fin de la prise en charge de JWT le 30 juin 2025. Ce guide fournit des instructions détaillées, explique le comportement post-migration et répond aux questions courantes.
source-git-commit: 264d3b12d8fd3bd100018513af1576b3de1cbb33
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---

# Migration des informations d’identification de serveur à serveur JWT vers OAuth

>[!IMPORTANT]
>
>Adobe rend obsolète la prise en charge des identifiants du compte de service (JWT) utilisés par Query Service. Après le 30 juin 2025, les informations d’identification non expirantes basées sur JWT n’actualiseront ni n’authentifieront plus les requêtes d’API. Pour éviter les interruptions de service, vous devez migrer chaque information d’identification éligible vers l’authentification de serveur à serveur OAuth.

Ce guide vous explique comment migrer des informations d’identification JWT non expirantes vers des informations d’identification OAuth de serveur à serveur dans Adobe Experience Platform. L’achèvement de ce processus garantit un accès ininterrompu à Query Service avant la fin de la prise en charge des informations d’identification JWT le 30 juin 2025.

Ce document fournit des instructions détaillées pour effectuer la migration, comprendre son impact et vérifier vos informations d’identification mises à jour.

## Qui doit migrer ? {#who-needs-to-migrate}

Si vous utilisez des informations d’identification non expirantes dans Query Service, vous devez migrer chacune d’elles. Cela s’applique aux informations d’identification utilisées dans les workflows automatisés, les requêtes planifiées ou les intégrations d’API personnalisées.

Si les informations d’identification sont répertoriées sous la section **[!UICONTROL Informations d’identification non expirantes]** de l’onglet **[!UICONTROL Informations d’identification]**, elles sont affectées.

## Comment migrer des informations d’identification {#how-to-migrate}

Vous pouvez migrer les informations d’identification directement dans l’interface utilisateur d’Experience Platform. Pour ce faire, accédez à **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Informations d’identification]**. Dans la section **[!UICONTROL Informations d’identification non expirantes]**, identifiez des informations d’identification marquées comme éligibles à la migration et sélectionnez **[!UICONTROL Migrer]** en regard de celles-ci.

>[!NOTE]
>
>La migration prend 8 à 10 secondes et ne peut pas être annulée une fois démarrée.

![Espace de travail Informations d’identification de Query Service avec les options Requêtes, Informations d’identification et Migrer mises en surbrillance.](../images/ui/migrate-jwt-to-oauth/migrate.png)

Après la migration, le système met à jour les informations d’identification pour utiliser l’authentification de serveur à serveur OAuth. La méthode basée sur JWT est automatiquement retirée et le statut est mis à jour sur **[!UICONTROL Migré]**.

Aucune reconfiguration n’est requise. Les traitements et intégrations existants continuent à fonctionner sans interruption.

## Que se passe-t-il après la migration {#after-migration}

Une fois la migration terminée :

- Vos informations d’identification continuent à fonctionner de manière transparente, de sorte qu’aucune modification n’est nécessaire dans vos tâches ou intégrations.
- Query Service utilise automatiquement l’authentification de serveur à serveur OAuth.
- La méthode d’authentification basée sur JWT a été abandonnée et n’est plus utilisée.

>[!IMPORTANT]
>
>Vous ne pouvez pas annuler cette modification. Une fois migrées, les informations d’identification ne peuvent pas être rétablies dans JWT.

## Questions fréquentes {#faq}

Ces questions répondent à des préoccupations courantes et vous aident à assurer une migration fluide et sans interruption.

### Pourquoi Adobe rend-il les informations d’identification JWT obsolètes ?

OAuth de serveur à serveur est une méthode d’authentification plus sécurisée et normalisée. Il offre une meilleure gestion du cycle de vie et prend en charge une plus grande cohérence de la plateforme.

### Que se passe-t-il si je ne migre pas d’ici le 30 juin 2025 ?

Les informations d’identification JWT ne s’actualiseront plus et les intégrations qui en dépendent échoueront. Adobe ne peut pas migrer les informations d’identification en votre nom à moins de lancer le processus.

### Comment savoir si je dois migrer ?

Si des informations d’identification apparaissent sous la section **[!UICONTROL Informations d’identification non expirantes]** de l’onglet Informations d’identification , ces informations d’identification doivent être migrées.

### Dois-je mettre à jour mes intégrations ou reconfigurer quoi que ce soit ?

Non. Après la migration, les informations d’identification OAuth prennent automatiquement le relais. Aucune modification manuelle n’est nécessaire dans vos tâches ou intégrations.

### Puis-je migrer toutes les informations d’identification en même temps ?

Non. Vous devez migrer chaque information d’identification individuellement à l’aide du bouton **[!UICONTROL Migrer]**.

### Puis-je continuer à utiliser les informations d’identification arrivant à expiration ?

Oui. Les informations d’identification arrivant à expiration ne sont pas affectées par cette modification. Seules les informations d’identification JWT non expirantes doivent être migrées.

### Un message indiquant « [!UICONTROL Aucune information d’identification sans date d’expiration n’a été trouvée.] » Qu&#39;est-ce que ça veut dire ? Dois-je prendre des mesures ?

Ce message signifie que vous n’avez pas encore créé d’informations d’identification non expirantes. Vous n’avez donc rien à faire.

### Je vois un message indiquant « [!UICONTROL La vérification de l’administrateur AEP a échoué]... » Qu&#39;est-ce que cela signifie ? Dois-je prendre des mesures ?

Ce message indique que vous n’êtes pas un administrateur ou que vous ne disposez pas des autorisations nécessaires pour créer des informations d’identification sans date d’expiration.

- Si vos autorisations n’ont pas été modifiées récemment, cela signifie que vous n’avez jamais eu accès à la création d’informations d’identification. Aucune action n’est donc nécessaire.
- Si vos autorisations ont été modifiées récemment, contactez l’administrateur de votre organisation et demandez-lui de migrer les informations d’identification pour vous.

### Puis-je migrer des informations d’identification non expirantes pour quelqu’un d’autre ?

Oui, mais seulement si vous êtes un administrateur. Seuls les administrateurs disposent des autorisations nécessaires pour créer et migrer des informations d’identification non expirantes pour d’autres utilisateurs, afin de pouvoir continuer à travailler sans interruption.

## Étapes suivantes {#next-steps}

Passez en revue chaque information d’identification non expirante dans l’onglet [!UICONTROL &#x200B; Informations d’identification &#x200B;] et migrez-la individuellement avant le 30 juin 2025. Pour toute question ou assistance, contactez votre représentant de compte Adobe.
