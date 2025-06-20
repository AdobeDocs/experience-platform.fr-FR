---
title: Référence de résolution des alertes CMK
description: Identifiez, résolvez les problèmes et résolvez les alertes courantes déclenchées par les configurations incorrectes de Customer Managed Key (CMK) dans Adobe Experience Platform. Utilisez ce guide pour suivre des instructions claires et détaillées et restaurer un accès sécurisé aux clés.
source-git-commit: 0d9cc046956dd380bb8816f0d8bf497bbad6140b
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 1%

---

# Référence de résolution des alertes CMK

Utilisez ce guide pour résoudre les problèmes et les alertes déclenchées par des paramètres de clé gérée par le client (CMK) mal configurés dans Adobe Experience Platform. Il permet aux administrateurs système et aux spécialistes de l’implémentation d’identifier les causes et d’appliquer des résolutions pour restaurer un accès sécurisé.

## Catégories d’alerte {#categories}

Les sections suivantes décrivent les types d’alertes qui peuvent être déclenchées par des problèmes de clés gérées par le client (CMK) dans Adobe Experience Platform :

- [Accès à la clé désactivé](#key-access-disabled)
- [Échec d’accès à la clé](#key-access-failure)
- [Notification d’alerte](#alert-notification)

## Accès à la clé désactivé {#key-access-disabled}

Cette alerte indique que Adobe Experience Platform ne peut pas accéder au CMK configuré en raison de la désactivation de la clé ou de son inaccessibilité en raison de problèmes de configuration des clés associés.

>[!IMPORTANT]
>
>Dans ce cas, la fonction CMK d’Adobe traite l’échec d’accès comme une suppression délibérée et purge toutes les données associées à votre organisation, en fonction de votre SLA.

### Quand cela se produit

Cette alerte est déclenchée lorsque la clé de chiffrement du coffre de clés Azure Key Vault est désactivée, supprimée ou mal configurée d’une manière qui empêche l’accès pendant les opérations de la plateforme.

### Causes possibles

Les raisons courantes pour lesquelles cette alerte peut se produire sont les suivantes :

- La clé a été désactivée manuellement.
- Les opérations clés (wrapKey/unwrapKey) ont été supprimées.
- La date d’activation de la clé est définie dans le futur.
- La date d’expiration de la clé est dans le passé.
- La clé a été supprimée.
- Les autorisations de l’application MultiTenant ont été supprimées ou modifiées.
- L’application MultiTenant a été supprimée.
- Les propriétés de l’application MultiTenant ont été modifiées.
- Le coffre de clés a été supprimé ou n’est plus accessible.

### Résolution

+++Si la clé est désactivée

1. Accédez au [coffre de clés Azure](https://portal.azure.com/) qui contient la fonction CMK.
2. Sélectionnez la clé associée à Adobe Experience Platform.
3. Vérifiez que le statut de la clé est défini sur **Activé**.
4. Si la clé est désactivée, activez-la à l’aide du portail Azure ou de la `az keyvault key enable` de commande de l’interface de ligne de commande.

>[!NOTE]
>
>Personnalisez cette commande pour votre environnement Azure.

+++

+++Si les opérations clés ont été modifiées

1. Ajoutez à nouveau les autorisations `wrapKey` et `unwrapKey` à la clé .

>[!NOTE]
>
>Tous les paramètres de la clé, y compris les dates d’activation et d’expiration, doivent être valides pour que la clé fonctionne.

+++

+++Si la date d’activation ou d’expiration est mal configurée

1. Définissez la date d’activation sur le passé ou le présent.
2. Définissez la date d’expiration sur une date ultérieure.

+++

+++Si la clé a été supprimée

1. Assurez-vous que la suppression réversible est activée dans Azure Key Vault.
2. Accédez à « Gérer les clés supprimées » dans le portail Azure ou l’interface de ligne de commande.
3. Sélectionnez la clé supprimée dans la liste des éléments supprimés de manière réversible.
4. Cliquez sur **Récupérer** pour restaurer la clé.

+++

+++Si les autorisations de l’application MultiTenant ont été supprimées ou modifiées

1. Restaurez les autorisations appropriées pour l’application MultiTenant.
2. Vérifiez que l’autorisation suivante est accordée : `Key Vault Crypto Service Encryption User`

+++

+++Si l’application MultiTenant a été supprimée

C&#39;est un changement radical. Vous devez contacter Adobe pour restaurer ou régénérer l’application MultiTenant.

+++

+++Si les paramètres de l’application MultiTenant ont été modifiés

1. Annulez les modifications apportées aux propriétés associées à l’application MultiTenant.

+++

+++Si le coffre de clés a été supprimé

1. Vérifiez que la suppression réversible est activée dans Azure.
2. Accédez à « Gérer les coffres supprimés » dans le portail ou l’interface de ligne de commande.
3. Récupérez le coffre supprimé pendant votre période de conservation (7-90 jours).
4. Si la protection contre le vidage est désactivée, vous pourrez peut-être tout de même récupérer le coffre.

>[!NOTE]
>
>Si la protection par suppression réversible ou par purge n’est pas configurée correctement, il se peut que la clé ou le coffre ne soit pas récupérable.

+++

## Échec d’accès à la clé {#key-access-failure}

Cette alerte indique que Adobe Experience Platform n’a pas pu accéder au CMK en raison d’un refus d’accès au niveau du réseau ou basé sur la configuration.

>[!IMPORTANT]
>
>Ceci est traité comme une erreur récupérable. Dans ce cas **les données ne sont** pas purgées sous SLA.

### Quand cela se produit

Cette alerte est généralement déclenchée lorsque le pare-feu du coffre de clés n’est pas configuré pour autoriser l’accès au CMK d’Adobe ou lorsque l’accès basé sur les identités échoue.

### Causes possibles

- Le pare-feu de Key Vault bloque l’adresse IP statique d’Adobe (`20.88.123.53`)
- La clé n’existe plus à l’emplacement prévu
- Les autorisations pour l’application Adobe MultiTenant sont manquantes
- Le coffre de clés a été supprimé ou mal configuré
- L&#39;ID d&#39;objet de l&#39;application MultiTenant a changé

### Résolution

+++Si le coffre de clés ou la clé n’existe plus

1. Vérifiez que le coffre de clés et la clé de chiffrement existent toujours.
2. Si la clé a été supprimée, suivez les étapes de récupération de suppression réversible sous « Accès aux clés désactivé ».

+++

+++Si les autorisations de l’application MultiTenant sont manquantes ou modifiées

1. Vérifiez que l’application Adobe MultiTenant dispose des autorisations suivantes :
   - `get`, `wrapKey` et `unwrapKey` sur la clé.
2. Vérifiez que l’ID d’objet de l’application MultiTenant est correct. S’il a été modifié, réappliquez les autorisations.

+++

+++Si le pare-feu bloque Adobe

1. Consultez les règles de pare-feu dans Azure Key Vault.
2. Assurez-vous qu’ils autorisent l’accès depuis l’adresse IP statique Adobe : `20.88.123.53`.

>[!NOTE]
>
>Même avec les autorisations appropriées, une adresse IP bloquée empêche l’accès aux clés.

+++

## Notification d’alerte {#alert-notification}

Cette alerte sert de notification générale pour la configuration du CMK ou les anomalies d’accès qui ne correspondent pas à un type d’échec connu.

>[!NOTE]
>
>Cette alerte peut refléter une erreur interne, une nouvelle configuration incorrecte ou une condition inattendue.

### Quand cela se produit

Cette alerte s’affiche lorsqu’Adobe CMK détecte un problème inconnu, non pris en charge ou nouveau lors de l’accès aux clés ou de la surveillance.

### Causes possibles

- Conditions de pare-feu/réseau imprévues
- Modifications de clés ou de coffre non couvertes par les types d’alerte prédéfinis
- Perturbations internes du réseau Adobe
- Mauvaise configuration qu’Adobe n’a jamais vue auparavant

### Résolution

+++Si la cause est inconnue ou ambiguë

1. Vérifiez le message d’alerte pour tout détail contextuel.
2. Vérifiez les paramètres du pare-feu, du coffre-fort et des clés pour connaître les modifications récentes.
3. Si aucune cause claire n’est trouvée, contactez l’assistance Adobe pour obtenir des conseils.
4. Surveillez les journaux et le comportement du système pour identifier les modèles.

+++

## Étapes suivantes

Pour comprendre comment les alertes sont déclenchées et comment configurer le placé sur la liste autorisée IP pour [!DNL Azure] CMK, consultez le guide [Configurer des alertes et une liste autorisée IP pour Azure CMK](./azure/alerts-and-ip-access.md).
