---
title: Configuration des alertes et de la place sur la liste autorisée IP pour Azure CMK
description: Découvrez comment placer sur la liste autorisée l’adresse IP statique d’Adobe dans Azure Key Vault et comment les alertes Experience Platform permettent de détecter et de résoudre les problèmes d’accès aux clés gérées par le client.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Configuration des alertes et de la place sur la liste autorisée IP pour [!DNL Azure] CMK

Pour améliorer la transparence, Adobe fournit un [service de surveillance](../../../../observability/alerts/ui.md){target="_blank"} qui vérifie le statut d’accès à votre coffre de clés et déclenche des alertes en cas de problème. Ces alertes vous aident à répondre rapidement et à éviter les interruptions de service. Pour activer ce service, placez sur la liste autorisée l’adresse IP statique d’Adobe.

>[!IMPORTANT]
>
>Si vous avez désactivé l’accès au réseau public ou configuré votre coffre de clés [!DNL Azure] pour autoriser uniquement les réseaux sélectionnés, vous devez ajouter l’adresse IP statique d’Adobe à votre place sur la liste autorisée. Sans cela, vous ne serez peut-être pas averti des problèmes d’accès qui pourraient avoir un impact sur votre instance Experience Platform.

## Placer sur la liste autorisée l’adresse IP statique d’Adobe dans [!DNL Azure] Key Vault {#add-adobe-static-ip}

Pour activer ces alertes tout en conservant vos restrictions réseau, accédez à votre **[!DNL Azure Key Vault]** > **[!DNL Networking settings]**. Dans l’onglet **[!DNL Firewalls and virtual networks]** , sélectionnez **[!DNL Allow public access from specific virtual networks and IP addresses]**.

![[!DNL Azure] écran des paramètres réseau du coffre de clés indiquant où ajouter l’adresse IP statique d’Adobe et avec l’option Autoriser l’accès depuis mise en surbrillance.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Adresse IP statique d’Adobe

>[!IMPORTANT]
>
>L’adresse IP statique fournie par Adobe est : `20.88.123.53`.

Ensuite, dans la section **[!DNL Firewall]** , sélectionnez **[!DNL Add your current IP address]** et remplacez-la par l’adresse IP statique d’Adobe. Toutes les connexions sortantes sont traitées comme des environnements de production. Par conséquent, cette adresse IP statique doit être placée sur la liste autorisée pour garantir un accès ininterrompu à votre coffre de clés dans les configurations réseau restreintes.

>[!NOTE]
>
>Après avoir ajouté ou mis à jour l’adresse IP statique dans vos paramètres de coffre de clés [!DNL Azure], patientez jusqu’à 10 minutes pour que la modification prenne effet. Une fois l’adresse IP ajoutée, l’application CMK accède au coffre de clés pour vérifier les autorisations.

Après avoir placé sur la liste autorisée l’adresse IP statique d’Adobe, Experience Platform peut surveiller l’accès à votre coffre de clés et déclencher des alertes en cas de problème. Ces alertes fournissent des avertissements précoces afin que vous puissiez agir avant que le service ne soit affecté. La section suivante détaille les types d’alertes que vous pouvez recevoir et la manière de répondre.

## Surveiller les alertes {#monitor-alerts}

Les alertes de Platform vous informent des problèmes susceptibles d’interrompre l’accès aux clés, tels que **[!UICONTROL Échec de l’accès à la clé]** ou **[!UICONTROL Désactivation de la clé]**. Ces alertes vous aident à identifier rapidement des problèmes tels qu’une adresse IP statique supprimée ou un pare-feu mal configuré. Pour restaurer l’accès, vérifiez les paramètres de votre pare-feu [!DNL Azure] et ajoutez à nouveau l’adresse IP requise.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Abonnez-vous aux notifications d’événement d’Adobe I/O pour recevoir des alertes en temps réel dans vos outils de surveillance. Pour obtenir des instructions de configuration, voir [Abonnement aux notifications d’événement Adobe I/O](../../../../observability/alerts/subscribe.md). Vous pouvez également consulter le [guide de l’interface utilisateur des alertes](../../../../observability/alerts/ui.md) pour savoir comment afficher et gérer les alertes dans Experience Platform.

## Étapes suivantes

Vous avez maintenant configuré la surveillance des alertes et des listes autorisées IP pour votre coffre de clés [!DNL Azure]. Pour terminer la configuration des clés gérées par le client dans [!DNL Azure], suivez ces guides de configuration.

- [Configurer un coffre  [!DNL Azure]  clés](./azure-key-vault-config.md)
- [Utiliser l’API pour configurer la fonction CMK](./api-set-up.md)
- [Utilisation de l’interface utilisateur pour configurer CMK](./ui-set-up.md)
