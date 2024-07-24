---
audience: user
user-guide-title: Service d’identités d’Adobe Experience Platform
breadcrumb-title: Guide de Platform Identity Service
user-guide-description: Associez les identités des clients, quel que soit l’appareil ou le système utilisé, afin d’offrir des expériences digitales personnalisées.
feature: Identities
role: Admin,Developer
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 73%

---


# Service d’identités d’Adobe Experience Platform {#identity}

- [Présentation du service d’identités](home.md)
- [Identity Service et Real-time Customer Profile](identity-and-profile.md)
- Fonctionnalités {#features}
   - [Espace de noms d’identité](./features/namespaces.md)
   - [Logique de liaison d’identités](./features/identity-linking-logic.md)
   - [Visionneuse de graphique d’identités](./features/identity-graph-viewer.md)
   - [Suppressions dans le service d’identités](./features/deletion.md)
   - Règles de liaison de graphiques d’identités {#identity-graph-linking-rules}
      - [Présentation des fonctionnalités](./identity-graph-linking-rules/overview.md)
      - [Guide de configuration](./identity-graph-linking-rules/configuration.md)
      - [Algorithme d’optimisation des identités](./identity-graph-linking-rules/identity-optimization-algorithm.md)
      - [Priorité d’espace de noms](./identity-graph-linking-rules/namespace-priority.md)
      - [Interface utilisateur de la simulation graphique](./identity-graph-linking-rules/graph-simulation.md)
      - [Paramètres des identités](./identity-graph-linking-rules/identity-settings-ui.md)
      - [Exemples de scénarios client](./identity-graph-linking-rules/example-scenarios.md)
      - [Exemples de configurations de graphique](./identity-graph-linking-rules/example-configurations.md)
   - [Présentation d’ECID](./features/ecid.md)
- [Guide de mise en oeuvre](implementation.md)
- [Barrières de sécurité pour les données Identity ](guardrails.md)
- API Service d’identités {#api}
   - [Prise en main](api/getting-started.md)
   - [Étiquetage d’un champ comme identité](api/label-identities.md)
   - [Répertorier les identités d’un cluster](api/list-cluster-identites.md)
   - [Répertorier l’historique des clusters d’une identité](api/list-cluster-history.md)
   - [Répertorier les mappages d’une identité](api/list-identity-mappings.md)
   - [Répertorier les espaces de noms disponibles](api/list-namespaces.md)
   - [Création d’un espace de noms personnalisé](api/create-custom-namespace.md)
   - [Répertorier l’identifiant natif d’une identité](api/list-native-id.md)
   - [Référence d’API](https://www.adobe.io/experience-platform-apis/references/identity-service)
- [Détection des appareils partagés](shared-device-detection.md)
- [Définir des champs d’identité dans l’interface utilisateur](label-identities.md)
- [Traitement des demandes d’accès à des informations personnelles](privacy.md)
- [Guide de dépannage](troubleshooting-guide.md)
- [Notes de mise à jour de Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/release-notes/latest)