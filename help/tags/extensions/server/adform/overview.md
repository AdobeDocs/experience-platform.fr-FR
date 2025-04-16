---
keywords: intégration d’adform ; adform ;
title: Intégration Adform pour le reciblage non authentifié
description: Cette intégration de Adobe Experience Platform vous permet de recibler les utilisateurs en fonction de l’ECID.
last-substantial-update: 2025-03-26T00:00:00Z
source-git-commit: 23da6e12b1f5bdc37240d7aa11a44e040b29e3f7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# Présentation de l’extension [!DNL Adform]

L’extension [[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud) permet le transfert d’événement côté serveur dans Adobe Experience Platform, ce qui permet aux annonceurs, aux agences de médias et aux éditeurs de synchroniser directement les données avec le système ID Fusion d’Adform. Cette intégration permet aux entreprises d’impliquer les audiences sur plusieurs canaux, d’améliorer les performances des campagnes et de fournir des solutions personnalisées pour affiner les stratégies de publicité numérique et maximiser l’efficacité des dépenses publicitaires.

Contrairement au suivi côté client traditionnel, cette extension rend inutiles les cookies tiers en utilisant des identifiants propriétaires, en particulier l’ECID (Experience Cloud ID), qui est synchronisé avec Adform. Cela permet un reciblage transparent des audiences sans avoir à déployer JavaScript côté client.

Ce guide explique comment installer, configurer et déployer l’extension pour transférer des événements des propriétés numériques d’une marque via le réseau Edge d’Adobe vers Adform afin de permettre un reciblage transparent des visiteurs.

## Reciblage hors site

Grâce au reciblage hors site, vous pouvez réengager les clients potentiels qui ont visité votre site web mais qui ne l’ont pas converti. Adform vous aide à atteindre ces audiences sur différentes plateformes, à renforcer la présence de la marque et à augmenter les opportunités de conversion. Utilisez cette intégration pour :

* Réengagez des visiteurs inconnus sans utiliser de cookies tiers.
* Activez les audiences directement sur les ECID sans utiliser d’identifiants tiers de substitution de cookies ou de balises supplémentaires sur vos propriétés numériques.

Adform vous aide à :

* Transformez facilement vos audiences de premier niveau indiquées sur les ECID en identifiants adressables pour les campagnes publicitaires numériques.
* Liez les ECID à 40+ solutions d’identification enchérissables pour optimiser votre portée, votre fréquence et vos performances par rapport à vos audiences cibles.

### Activation de l’audience côté serveur avec [!DNL Adform] {#server-side-activation}

Contrairement aux déploiements d’ID côté client traditionnels, cette intégration ne nécessite pas que vous déployiez la solution d’un fournisseur d’ID sur vos propriétés numériques. Au lieu de cela, il active l’activation d’audience côté serveur en utilisant les ECID déjà synchronisés avec Adform. Les principaux avantages sont les suivants :

* **Aucun déploiement JavaScript côté client** : vous n’avez pas besoin de gérer la logique de reconnaissance des visiteurs côté client ou de déchiffrer les identifiants côté client en versions stables de plus longue durée.
* **Synchronisation transparente des audiences** : les ECID sont mappés au graphique d’identifiant interne d’Adform, ce qui permet un reciblage efficace sur toutes les plateformes.
* **Amélioration de la portée et de la déduplication** : le graphique ID Fusion connecte les ECID à plusieurs identifiants, ce qui garantit une correspondance d’audience de haute qualité.

## Conditions préalables {#prerequisites}

Avant d’intégrer Adform à Adobe, assurez-vous que les conditions préalables suivantes sont remplies :

1. **Configuration d’Adobe Web SDK** : Adobe Web SDK doit être mis en œuvre pour faciliter la collecte de données et le transfert d’événement.

2. **CDP ou SKU de connexion** : vous devez disposer du SKU Prime ou Ultimate de la plateforme de données client (CDP) Adobe, ou du SKU de connexion, pour permettre une communication transparente côté client et côté serveur.

3. **Configuration Adobe Experience Platform Edge Network**:
   * Assurez-vous qu’Edge Network est configuré pour prendre en charge le transfert d’événement en temps réel pour le reciblage hors site. Pour plus d’informations, consultez le guide de prise en main du transfert d’événement [Adobe](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started).
   * Cette étape est essentielle pour transmettre efficacement des données au point d’entrée côté serveur d’Adobe.

Une fois ces conditions préalables réunies, vous pouvez continuer à configurer et déployer l’extension [!DNL Adform] .

## Configuration de l’extension [!DNL Adform] {#configure-adform-extension}

Pour configurer l’extension [!DNL Adform], suivez les étapes décrites dans les sections ci-dessous.

### Installation et configuration de l’extension 

Accédez à la [!DNL Adform extension] dans l’interface utilisateur de transfert d’événement et saisissez les valeurs requises :

| Entrée | Description |
| --- | --- |
| ID de configuration du suivi | Identifiant unique fourni par Adform pour le suivi des événements. |
| Domaine global | Utilisez `a1.adform.net` cette option pour optimiser les performances et éviter les problèmes de latence régionale. |

Enregistrez la configuration après avoir saisi ces détails.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### Définition des paramètres de tracking

L’action « track » est la règle d’événement principal. Il se déclenche en fonction d’actions prédéfinies, généralement `page load.` inclure les paramètres suivants :

**Paramètres requis :**

| Paramètres | Description |
| --- | --- |
| `Page Name` | Identifie la page ou l’action de l’utilisateur. |
| `User Agent` | Capture les informations pour la correspondance d’audience. |
| `IP Address` | Crucial pour un ciblage précis et un reciblage. |

**Paramètres recommandés :**

| Paramètres | Description |
| --- | --- |
| `Page URL` | Identifie la page ou l’action de l’utilisateur. |
| `Referral URL` | Capture des informations pour la correspondance d’audience. |
| `ECID` | Essentiel pour un ciblage et un reciblage précis. |
| `Source Domain` | Essentiel pour un ciblage et un reciblage précis. |

<!-- ![Tracking parameters for Adform]() -->

### Joindre une règle

L’extension doit être associée à une règle pour fonctionner correctement. Si aucune condition n’est définie, créez une règle globale pour vous assurer qu’elle s’exécute toujours.

>[!NOTE]
>
>Si l’extension ne se déclenche pas, vérifiez qu’elle est associée à une règle valide dans la collecte de données Adobe Experience Platform.

<!-- ![Attach a rule to the Adform extension]() -->

## Validation et déploiement

Assurez-vous que l’extension est installée et configurée correctement et que tous les éléments de données requis sont mappés, notamment :
* [ECID](/help/identity-service/features/ecid.md)
* Nom de la page
* URL de référence
* Agent utilisateur
* Adresse IP

Une fois que vous avez entré tous les champs obligatoires et terminé les tests, sélectionnez **Build** pour déployer l’extension.

## Étapes suivantes

Vous devez maintenant comprendre comment Adform s’intègre aux fonctionnalités côté serveur d’Adobe et évaluer la faisabilité de l’intégration au sein de votre infrastructure existante. Pour plus d’informations, consultez la [documentation officielle d’Adform](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud).