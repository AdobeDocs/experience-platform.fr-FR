---
title: Présentation de l’assistant AI (hérité) dans Adobe Experience Platform
description: Découvrez l’assistant d’IA (hérité), ses nuances et cas d’utilisation, ainsi que son utilisation pour accélérer votre workflow avec Adobe Experience Platform et Real-Time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: 68c55e370cab58ce5c93359520bf4ce671282a1b
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 5%

---

# Assistant d’IA (hérité) dans Adobe Experience Platform

>[!IMPORTANT]
>
>Ce document s’applique à l’assistant d’IA (hérité). Pour plus d’informations sur l’assistant AI (Next-Gen), consultez le guide de l’interface utilisateur de l’assistant [AI](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) dans la documentation [AI dans Experience Cloud](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/home).

Reportez-vous au tableau suivant pour une comparaison de l’assistant AI (hérité) et de l’assistant AI (nouvelle génération) :

| Domaine de fonctionnalités | Assistant AI (hérité) | Assistant IA (nouvelle génération) |
| --- | --- | --- |
| Expérience utilisateur | L’assistant d’IA (hérité) est disponible dans un panneau du rail de droite uniquement. | L’assistant d’IA (version suivante) est disponible dans le panneau du rail droit et dans une expérience immersive en plein écran. |
| Portée des fonctionnalités | Vous pouvez utiliser l’assistant d’IA (hérité) pour obtenir des connaissances sur les produits et des informations opérationnelles. | Vous pouvez utiliser l’assistant d’IA (nouvelle génération) pour acquérir des connaissances sur les produits, obtenir des informations opérationnelles, ainsi que des compétences avancées en matière d’agentisme et exécuter des tâches en plusieurs étapes. |
| Architecture de Platform | L’assistant AI (hérité) n’est pas créé sur la pile Agent Orchestrator. | L’assistant d’IA (nouvelle génération) est optimisé par [Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator), ce qui permet l’extensibilité et une coordination avancée entre les fonctionnalités. |
| Couverture de l’application | L’assistant d’IA (hérité) est une implémentation spécifique à l’application. | Vous pouvez utiliser l’assistant d’IA (version suivante) pour une expérience d’assistant d’IA unifiée dans toutes les applications Adobe Experience Cloud. |
| Modèle d’accès et d’autorisation | Modèle d’accès au niveau de l’application aligné sur les limites de chaque produit. | Tous les utilisateurs ont accès à l’assistant AI (version suivante) et aux agents Experience Platform associés. **Remarque** : <ul><li>**Adobe Experience Manager** : votre administrateur doit vous accorder l’autorisation d’accéder à l’assistant AI (Next-Gen) via [Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).</li><li>**Customer Journey Analytics** : votre administrateur doit vous accorder l’autorisation d’accéder à l’assistant AI par le biais du contrôle d’accès de [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/technotes/access-control?lang=en). Cela vous permet de poser des questions sur la connaissance des produits et les informations sur les données. |

La vidéo suivante est destinée à vous aider à comprendre l’assistant AI.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Lisez ce document pour en savoir plus sur l’assistant AI (hérité) dans Adobe Experience Platform.

L’assistant d’IA (hérité) dans Adobe Experience Platform est une expérience de conversation que vous pouvez utiliser pour accélérer vos workflows dans les applications Adobe. Vous pouvez utiliser l’assistant d’IA (hérité) pour mieux comprendre la connaissance des produits, résoudre les problèmes ou rechercher des informations et des informations opérationnelles. L’assistant AI (hérité) prend en charge Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

![Interface de l’assistant d’IA avec la première expérience utilisateur déclenchée.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Vous devez accepter un [contrat utilisateur](https://www.adobe.com/fr/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) avant de pouvoir utiliser l’assistant d’IA (hérité). Le contrat utilisateur contient également le contrat bêta public. Cela vous permet d’utiliser des fonctionnalités supplémentaires de l’assistant d’IA (hérité) lors de leur déploiement en version bêta.

+++Sélectionner pour afficher l’interface du contrat utilisateur

![Première page du contrat d’utilisation.](./images/user-agreement-1.png)

![Dernière page du contrat d’utilisation.](./images/user-agreement-2.png)

+++

## Présentation de l’assistant AI {#understanding-ai-assistant}

L’assistant d’IA (hérité) répond à vos questions envoyées en interrogeant une base de données, puis en traduisant les données de la base de données en une réponse lisible par l’utilisateur.

Cette représentation interne des données sous-jacentes est également appelée **[!DNL Knowledge Graph]**. Il s’agit d’un réseau complet de concepts, de données et de métadonnées pour une réponse donnée.

Le [!DNL Knowledge Graph] se compose de sous-graphiques qui sont référencés chaque fois que les requêtes sont envoyées :

* Informations opérationnelles sur le client.
* Informations opérationnelles sur les clients dans divers méta-magasins.
* Documentation Experience League.

Il existe deux catégories de questions à prendre en compte avant d’interroger l’assistant d’IA (hérité) :

### Connaissances du produit {#product-knowledge}

La connaissance des produits fait référence aux concepts et aux sujets reposant sur la documentation d’Experience League. Les questions relatives à la connaissance des produits peuvent être spécifiées de manière plus détaillée dans les sous-groupes suivants :

| Connaissances du produit | Exemples |
| --- | --- |
| Apprentissage par points | <ul><li>Quelle est la différence entre une identité et une clé primaire ou étrangère ?</li><li>Que sont les audiences semblables ?</li></ul> |
| Ouvrir la découverte | <ul><li>Comment exporter ce jeu de données ?</li><li>Existe-t-il des schémas pour les clients du secteur de la santé ?</li></ul> |
| Résolution des problèmes | <ul><li>Pourquoi ne puis-je pas activer un schéma détenu par Adobe pour le profil ?</li><li>Pourquoi ne puis-je pas supprimer un segment ?</li></ul> |

{style="table-layout:auto"}

Regardez la vidéo suivante pour plus d’informations sur les connaissances des produits de l’assistant AI (hérité) :

>[!VIDEO](https://video.tv.adobe.com/v/3438032/?learn=on)

### Informations opérationnelles {#operational-insights}

Les informations opérationnelles se rapportent aux réponses que l’assistant AI (hérité) génère sur vos objets de métadonnées (attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources), y compris les nombres, les recherches et l’impact de la parenté. Il n’examine aucune donnée du sandbox.

* De combien de jeux de données dispose-t-on ?
* Combien d’attributs de schéma n’ont jamais été utilisés ?
* Quelles audiences ont été activées ?

Vous pouvez poser des questions à l’assistant d’IA (hérité) sur vos informations opérationnelles dans les domaines suivants :

| Domaine | Métadonnées prises en charge | Métadonnées non prises en charge |
| --- | --- | --- |
| Attributs | <ul><li>Recherche de nom d’attribut</li><li>Attribut - relation de schéma</li><li>Attribut - relation du jeu de données</li><li>Attribut - Relation d’audience</li><li>Attribut - relation de destination</li></ul> | <ul><li>Classe d’attribut</li><li>Journal</li><li>Statut d’obsolescence</li><li>Étiquettes</li><li>Valeur stockée dans les attributs</li></ul> |
| Audiences | <ul><li>Taille de l’audience</li><li>Type d’audience (diffusion en continu ou par lots)</li><li>Dates de création/modification</li><li>Statut d’activation</li><li>Nombre de profils</li><li>Dupliquer les audiences</li><li>Recherche de définition d’audience</li><li>Audience - Relation d’audience</li><li>Audience - Relation d’attributs</li><li>Audience - Relation du jeu de données</li><li>Audience - Relation de destination</li><li>Recherche de nom</li><li>Recherche par nom et ID | <ul><li>Chevauchements des audiences</li><li>Activation de l’audience</li><li>Audience - relations de campagne</li><li>Journal</li><li>Créer/modifier</li><li>Étiquettes</li><li>Tendances de qualification des profils</li></ul> |
| Flux de données | <ul><li>Nombre de flux de données</li><li>Statut du flux de données</li><li>Flux de données - Relation du jeu de données</li><li>Flux de données - Relation source</li></ul> | <ul><li>Création/modification</li><li>Relations flux de données-lot</li><li>Ingérer le nombre de profils</li></ul> |
| Jeux de données | <ul><li>Nombre de jeux de données</li><li>Statut d’activation du profil</li><li>Date de création/modification</li><li>Jeu de données - Relation de schéma</li><li>Jeu de données - Relation d’audience</li><li>Relation jeu de données - attribut</li><li>Jeu de données - Relation de flux de données</li><li>Taille du jeu de données</li><li>Nombre de lignes</li><li>Recherche de nom </li><li>Recherche par nom et ID</li></ul> | <ul><li>Journal</li><li>Créé par</li><li>Jeu de données - Relation par lots</li><li>Création/modification de jeu de données</li><li>Nombre de profils</li><li>Recherche de valeur</li></ul> |
| Destinations | <ul><li>Nombre de destinations configurées</li><li>Relation destination-audience</li><li>Relation d’attributs de destination</li></ul> | <ul><li>Configuration du compte</li><li>Informations d’identification du compte</li><li>Profils uniques activés</li></ul> |
| Parcours | <ul><li>Comptages</li><li>Recherche de nom</li><li>Recherche par nom et ID</li><li>Statut du parcours</li><li>Statut de déclenchement (audience ou événements)</li><li>Dates de création/modification</li><li>Fréquence récurrente</li></ul> | <ul><li>Attributs - Relations de parcours</li><li>Journal</li><li>Création/modification</li><li>Créé par</li><li>Événements</li><li>Parcours - jeu de données</li><li>Parcours - schéma</li><li>Offres</li><li>Tendances de qualification des profils</li><li>Événements d’étape</li></ul> |
| Schémas | <ul><li>Nombre de schémas</li><li>Date de création/modification</li><li>Schéma - Relation des attributs</li><li>Schéma - Relation du jeu de données</li><li>Schéma - Relation d’audience</li><li>Statut d’activation du profil</li><li>Recherche de nom</li><li>Recherche par nom et ID</li></ul> | <ul><li>Journal</li><li>Création/modification</li><li>Créé par</li><li>Groupes de champs</li><li>Identités</li><li>Espaces de noms d’identité</li><li>Étiquettes</li><li>Nombre de profils</li></ul> |
| Sources | <ul><li>Comptes</li><li>Statut du compte</li><li>Flux de données actifs/inactifs pour chaque compte</li><li>Connecteur Source - Relation de flux de données</li><li>Compte Source - relation du flux de données</li></ul> | <ul><li>Informations d’identification du compte</li><li>Configuration du compte</li><li>Mesures d’ingestion de données</li><li>Nombre de profils</li><li>Source - relations par lots</li></ul> |

{style="table-layout:auto"}

Pour les questions relatives aux informations opérationnelles, les réponses peuvent ne pas refléter l’état actuel de l’interface utilisateur. Les données sur lesquelles reposent ces questions sont mises à jour toutes les 24 heures. Par exemple, les modifications apportées par les utilisateurs et utilisatrices dans Real-Time CDP pendant la journée sont synchronisées avec les entrepôts de données la nuit, puis répondent aux questions des utilisateurs et utilisatrices le matin. Vous devrez vous connecter à un sandbox pour vous renseigner sur des données spécifiques liées à des objets.

Regardez la vidéo suivante pour plus d’informations sur les insights opérationnels de l’assistant d’IA (hérité) :

>[!VIDEO](https://video.tv.adobe.com/v/3444031?learn=on&enablevpops)

### Périmètre de la fonctionnalité {#feature-scope}

Actuellement, la portée de l’assistant d’IA (hérité) est la suivante :

* [Connaissance des produits](./home.md#product-knowledge) : l’assistant AI (hérité) peut répondre aux questions sur la connaissance des produits pour Experience Platform, Real-Time Customer Data Platform et Adobe Journey Optimizer. Vous pouvez également approfondir les rubriques de connaissance des produits Customer Journey Analytics, mais uniquement via l’interface utilisateur de Customer Journey Analytics.
* [Informations opérationnelles &#x200B;](./home.md#operational-insights) : vous pouvez poser des questions à l’assistant d’IA (hérité) sur les informations opérationnelles des objets de données suivants : attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources.

## Étapes suivantes

Maintenant que vous avez une compréhension générale de l’assistant AI (hérité), vous pouvez procéder à l’utilisation de l’assistant AI (hérité) pendant vos workflows. Pour plus d’informations, reportez-vous à la documentation suivante :

* [Guide de l’interface utilisateur de l’assistant AI (hérité)](./ui-guide.md)
* [Accès aux fonctionnalités](./access.md)
* [Guide des questions](./questions.md)
* [Assistant Confidentialité, sécurité et gouvernance dans l’IA (hérité)](./privacy.md)
* [Questions fréquentes](./faq.md)
