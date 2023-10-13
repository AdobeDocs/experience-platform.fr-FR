---
title: Configuration d’Azure Key Vault
description: Découvrez comment créer un compte d’entreprise avec Azure ou utiliser un compte d’entreprise existant et créer le Key Vault.
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: 4ec87482c5a38404217ecd910b6a27ee2d0e00eb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 36%

---

# Configurer un coffre [!DNL Azure] Key Vault

Les clés gérées par le client (CMK) ne prennent en charge que les clés d’une [!DNL Microsoft Azure] Key Vault. Pour commencer, vous devez utiliser [!DNL Azure] pour créer un compte d’entreprise ou utiliser un compte d’entreprise existant, puis suivre les étapes ci-dessous pour créer le coffre de clés.

>[!IMPORTANT]
>
>Seuls les niveaux de service Premium et Standard d’[!DNL Azure] Key Vault sont pris en charge. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] et [!DNL Azure Payments HSM] ne sont pas pris en charge. Reportez-vous à la documentation d’[[!DNL Azure] ](https://learn.microsoft.com/fr-fr/azure/security/fundamentals/key-management#azure-key-management-services) pour plus d’informations sur les services de gestion de clés proposés.

>[!NOTE]
>
>La documentation ci-dessous ne couvre que les étapes de base pour créer le Key Vault. En dehors de ces instructions, vous devez configurer le Key Vault conformément aux politiques de votre entreprise.

Connectez-vous au portail [!DNL Azure] et utilisez la barre de recherche pour accéder à **[!DNL Key vaults]** sous la liste des services.

![La fonction de recherche de [!DNL Microsoft Azure] avec [!DNL Key vaults] surlignée dans les résultats de la recherche.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

La page **[!DNL Key vaults]** s’affiche après avoir sélectionné le service. À partir de là, sélectionnez **[!DNL Create]**.

![La variable [!DNL Key vaults] tableau de bord dans [!DNL Microsoft Azure] avec [!DNL Create] surlignée.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

À l’aide du formulaire fourni, renseignez les détails de base du Key Vault, y compris un nom et un groupe de ressources affecté.

>[!WARNING]
>
>Bien que la plupart des options puissent rester sur leurs valeurs par défaut, **assurez-vous d’activer les options de suppression réversible et de protection contre le vidage**. Si vous n’activez pas ces fonctionnalités, vous risquez de perdre l’accès à vos données si le Key Vault est supprimé.
>
>![La variable [!DNL Microsoft Azure] [!DNL Create a Key Vault] workflow avec protection de suppression et purge souples mise en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

À partir de là, continuez à parcourir le workflow de création de Key Vault et configurez les différentes options en fonction des stratégies de votre entreprise.

Une fois que vous êtes parvenu au **[!DNL Review + create]** vous pouvez consulter les détails de KeyVault pendant la validation. Une fois la validation acceptée, sélectionnez **[!DNL Create]** pour terminer le processus.

![La Microsoft Azure Key valide la révision et la création d’une page avec l’option Créer mise en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configurer l’accès {#configure-access}

Ensuite, activez le contrôle d’accès basé sur les rôles Azure pour votre coffre-fort de clé. Sélectionner **[!DNL Access configuration]** dans le [!DNL Settings] dans la barre de navigation de gauche, puis sélectionnez **[!DNL Azure role-based access control]** pour activer le paramètre. Cette étape est essentielle, car l’application CMK doit être associée ultérieurement à un rôle Azure. L’attribution d’un rôle est présentée dans la section [API](./api-set-up.md#assign-to-role) et [Interface utilisateur](./ui-set-up.md#assign-to-role) workflows.

![La variable [!DNL Microsoft Azure] tableau de bord avec [!DNL Access configuration] et [!DNL Azure role-based access control] surlignée.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Configurer les options de mise en réseau {#configure-network-options}

Si votre Key Vault est configuré pour restreindre l’accès public à certains réseaux virtuels ou désactiver entièrement l’accès public, vous devez accorder [!DNL Microsoft] une exception de pare-feu.

Sélectionnez **[!DNL Networking]** dans le volet de navigation de gauche. Sous **[!DNL Firewalls and virtual networks]**, cochez la case **[!DNL Allow trusted Microsoft services to bypass this firewall]**, puis sélectionnez **[!DNL Apply]**.

![La variable [!DNL Networking] de [!DNL Microsoft Azure] avec [!DNL Networking] et [!DNL Allow trusted Microsoft surfaces to bypass this firewall] exception mise en évidence.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Générer une clé {#generate-a-key}

Une fois que vous avez créé un KeyVault, vous pouvez en générer une nouvelle. Accédez à l’onglet **[!DNL Keys]** et sélectionnez **[!DNL Generate/Import]**.

![La variable [!DNL Keys] de [!DNL Azure] avec [!DNL Generate import] surlignée.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilisez le formulaire fourni pour attribuer un nom à la clé, puis sélectionnez **RSA** pour le type de clé. Au minimum, la variable **[!DNL RSA key size]** doit être au moins **3072** bits requis par [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] est également compatible avec RSA 3027.

>[!NOTE]
>
>N’oubliez pas le nom que vous indiquez pour la clé, car vous devez envoyer la clé à Adobe.

Utilisez les commandes restantes pour configurer la clé que vous souhaitez générer ou importer selon vos besoins. Lorsque vous avez terminé, sélectionnez **[!DNL Create]**.

![Créez un tableau de bord de clés avec [!DNL 3072] bits surlignés.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La clé configurée apparaît dans la liste des clés du coffre.

![La variable [!DNL Keys] espace de travail avec le nom de clé en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Étapes suivantes

Pour poursuivre le processus unique de configuration de la fonctionnalité de clés gérées par le client, continuez avec la variable [API](./api-set-up.md) ou [Interface utilisateur](./ui-set-up.md) guides de configuration des clés gérées par le client.
