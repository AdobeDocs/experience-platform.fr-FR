---
title: Test et validation des configurations de flux de données dynamiques
description: Découvrez comment utiliser Adobe Experience Platform Assurance pour tester  [!DNL Dynamic Datastream Configuration]  règles et confirmer le routage des événements entre les jeux de données et les services.
source-git-commit: 19e297602d67a360a3b6bcdd6d5403fb6090de7f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Tester et valider des [!DNL Dynamic Datastream Configurations]

Utilisez [!DNL Adobe Experience Platform] Assurance pour obtenir une visibilité en temps réel sur la manière dont les règles de [!DNL Dynamic Datastream Configuration] évaluent et acheminent les événements. En faire votre principal outil de test après la configuration des règles.

>[!IMPORTANT]
>
>Les modifications de configuration des flux de données prennent jusqu’à 15 minutes pour se propager dans Edge Network. Patientez dans la fenêtre de propagation complète avant de démarrer une session Assurance ou de vérifier les volumes d’ingestion du jeu de données.

## Configuration d’une session Assurance {#assurance-setup}

1. Dans l’interface utilisateur de [!DNL Adobe Experience Platform], accédez à **[!UICONTROL Assurance]** puis sélectionnez **[!UICONTROL Créer une session]**.
2. Connectez votre implémentation de Web SDK ou de Mobile SDK à la session à l’aide de l’extension de navigateur Assurance (pour le web) ou d’Assurance SDK (pour le mobile).
3. Générez des événements sur votre site ou application qui doivent déclencher différentes règles de [!DNL Dynamic Datastream Configuration].

Pour obtenir des instructions complètes sur la configuration d’Assurance, consultez la [documentation Adobe Experience Platform Assurance](/help/assurance/home.md).

## Éléments à rechercher dans les traces Assurance {#assurance-traces}

Pour chaque événement traité par Edge Network, Assurance affiche :

- **Quelle règle correspondait :** le nom de règle et les conditions spécifiques pour lesquelles l’événement remplissait les critères.
- **Résultat du routage :** quels services ont reçu l’événement et à quel jeu de données Edge Network l’a acheminé.
- **Si les remplacements côté [!DNL Dynamic Datastream Configuration] ou côté client étaient actifs :** cela permet de diagnostiquer les cas où les règles sont contournées de manière inattendue. Lorsqu’un remplacement côté client est présent, l’Edge Network ignore [!DNL Dynamic Datastream Configuration] règles relatives à cet événement. Pour plus d’informations, voir [remplacements de la configuration des trains de données](/help/datastreams/overrides.md).

## Liste de contrôle de test {#testing-checklist}

Validez chaque chemin d’accès à l’événement dans Assurance avant de passer à la validation au niveau de la plateforme.

| Test | Éléments à vérifier | How |
| ------ | --------------- | ----- |
| **Routage d’événement exploitable** | Les événements d’achat arrivent dans le jeu de données activé pour le profil | Déclenchez un événement d’achat ; vérifiez dans Assurance que la règle appropriée correspond et Assurance affiche le jeu de données attendu comme destination de routage |
| **Routage analytique des événements** | Les pages vues accèdent au jeu de données ne concernant pas les profils | Parcourez les pages ; vérifiez dans Assurance et confirmez que les événements apparaissent dans le jeu de données attendu dans [!DNL Adobe Experience Platform] |
| **Suppression d’événement système** | Edge Network achemine les événements `decisioning.propositionFetch` vers le jeu de données de quarantaine, et non vers le jeu de données de profil principal | Chargez une page avec une personnalisation [!DNL Adobe Target] ou [!DNL Adobe Journey Optimizer] ; vérifiez que l’événement `decisioning.propositionFetch` correspond à la règle [de suppression des événements système](/help/datastreams/dynamic-configurations/use-cases.md#uc3) |
| **Filtrage des robots** | Les événements notés par les robots sont mis en quarantaine ou ignorés | Utilisez une adresse IP ou un user-agent de robot connu qui correspond à vos règles de détection de robot ; vérifiez les `botDetection.score = 1` dans Assurance et confirmez les correspondances [règle de filtrage de robot](/help/datastreams/dynamic-configurations/use-cases.md#uc4) |
| **Secours par défaut** | Les événements qui ne correspondent à aucune règle suivent la configuration par défaut du flux de données | Envoyer un type d’événement non couvert par une règle ; vérifier qu’il est acheminé vers le jeu de données principal |
| **Ordre des règles** | Le comportement « First-match-wins » est correct | Envoyez un événement qui peut correspondre à plusieurs règles. Vérifiez qu’Assurance affiche uniquement la première règle correspondante s’appliquant. |
| **Conflit de remplacement côté client** | Les événements avec remplacement de SDK contournent les règles de [!DNL Dynamic Datastream Configuration] | Envoyer un événement avec `edgeConfigOverrides` dans `sendEvent` ; vérifier dans Assurance que l’Edge Network a ignoré [!DNL Dynamic Datastream Configuration] règles pour cet événement |

## Étapes suivantes

- Examiner les [bonnes pratiques pour [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/best-practices.md) pour obtenir des conseils opérationnels continus.
- Voir la [FAQ](/help/datastreams/dynamic-configurations/faq.md) si vous rencontrez un comportement de routage inattendu.
- Revenez à [Créer des configurations de flux de données dynamiques](/help/datastreams/dynamic-configurations/configure.md) pour ajuster les conditions des règles ou l’ordre des règles.
