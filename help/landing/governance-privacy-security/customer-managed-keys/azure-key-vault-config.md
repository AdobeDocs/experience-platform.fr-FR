---
title: Configuration d’Azure Key Vault
description: Découvrez comment créer un compte d’entreprise avec Azure ou utiliser un compte d’entreprise existant et créer le Key Vault.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 24%

---

# Configurer un coffre [!DNL Azure] Key Vault

Les clés gérées par le client (CMK) ne prennent en charge que les clés d’un Key Vault [!DNL Microsoft Azure]. Pour commencer, vous devez travailler avec [!DNL Azure] pour créer un compte d’entreprise ou utiliser un compte d’entreprise existant et suivre les étapes ci-dessous pour créer le Key Vault.

>[!IMPORTANT]
>
>Seuls les niveaux HSM standard, Premium et gérés pour [!DNL Azure] Key Vault sont pris en charge. [!DNL Azure Dedicated HSM] et [!DNL Azure Payments HSM] ne sont pas pris en charge. Reportez-vous à la documentation d’[[!DNL Azure] ](https://learn.microsoft.com/fr-fr/azure/security/fundamentals/key-management#azure-key-management-services) pour plus d’informations sur les services de gestion de clés proposés.

>[!NOTE]
>
>La documentation ci-dessous ne couvre que les étapes de base pour créer le Key Vault. En dehors de ces instructions, vous devez configurer le Key Vault conformément aux politiques de votre entreprise.

Connectez-vous au portail [!DNL Azure] et utilisez la barre de recherche pour accéder à **[!DNL Key vaults]** sous la liste des services.

![La fonction de recherche de [!DNL Microsoft Azure] avec [!DNL Key vaults] mise en surbrillance dans les résultats de la recherche.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

La page **[!DNL Key vaults]** s’affiche après avoir sélectionné le service. À partir de là, sélectionnez **[!DNL Create]**.

![ Le tableau de bord [!DNL Key vaults] dans [!DNL Microsoft Azure] avec [!DNL Create] surligné.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

À l’aide du formulaire fourni, renseignez les détails de base du Key Vault, y compris un nom et un groupe de ressources affecté.

>[!WARNING]
>
>Bien que la plupart des options puissent rester sur leurs valeurs par défaut, **assurez-vous d’activer les options de suppression réversible et de protection contre le vidage**. Si vous n’activez pas ces fonctionnalités, vous risquez de perdre l’accès à vos données si le Key Vault est supprimé.
>
>![Le workflow [!DNL Microsoft Azure] [!DNL Create a Key Vault] avec la protection de suppression et purge souples mise en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

À partir de là, continuez à parcourir le workflow de création de Key Vault et configurez les différentes options en fonction des stratégies de votre entreprise.

Une fois que vous êtes arrivé à l’étape **[!DNL Review + create]**, vous pouvez consulter les détails du Key Vault pendant la validation. Une fois la validation acceptée, sélectionnez **[!DNL Create]** pour terminer le processus.

![La clé Azure Microsoft valide la révision et la création d’une page avec l’option Créer mise en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configurer l’accès {#configure-access}

Ensuite, activez le contrôle d’accès basé sur les rôles Azure pour votre coffre-fort de clé. Sélectionnez **[!DNL Access configuration]** dans la section [!DNL Settings] du volet de navigation de gauche, puis sélectionnez **[!DNL Azure role-based access control]** pour activer le paramètre. Cette étape est essentielle, car l’application CMK doit être associée ultérieurement à un rôle Azure. L’affectation d’un rôle est documentée dans les workflows [API](./api-set-up.md#assign-to-role) et [UI](./ui-set-up.md#assign-to-role) .

![ Le tableau de bord [!DNL Microsoft Azure] avec [!DNL Access configuration] et [!DNL Azure role-based access control] surlignés.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Configurer les options de mise en réseau {#configure-network-options}

Si votre Key Vault est configuré pour restreindre l&#39;accès public à certains réseaux virtuels ou désactiver entièrement l&#39;accès public, vous devez accorder à [!DNL Microsoft] une exception de pare-feu.

Sélectionnez **[!DNL Networking]** dans le volet de navigation de gauche. Sous **[!DNL Firewalls and virtual networks]**, cochez la case **[!DNL Allow trusted Microsoft services to bypass this firewall]**, puis sélectionnez **[!DNL Apply]**.

![ L&#39;onglet [!DNL Networking] de [!DNL Microsoft Azure] avec l&#39;exception [!DNL Networking] et [!DNL Allow trusted Microsoft surfaces to bypass this firewall] mise en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Générer une clé {#generate-a-key}

Une fois que vous avez créé un KeyVault, vous pouvez en générer une nouvelle. Accédez à l’onglet **[!DNL Keys]** et sélectionnez **[!DNL Generate/Import]**.

![L’onglet [!DNL Keys] de [!DNL Azure] avec [!DNL Generate import] surligné.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilisez le formulaire fourni pour donner un nom à la clé et sélectionnez **RSA** ou **RSA-HSM** pour le type de clé. Au minimum, **[!DNL RSA key size]** doit être au moins **3072** bits comme requis par [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] est également compatible avec RSA 3027.

>[!NOTE]
>
>N’oubliez pas le nom que vous indiquez pour la clé, car vous devez envoyer la clé à Adobe.

Utilisez les commandes restantes pour configurer la clé que vous souhaitez générer ou importer selon vos besoins. Lorsque vous avez terminé, sélectionnez **[!DNL Create]**.

![Le tableau de bord [!DNL Create a key] avec [!DNL 3072] bits en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La clé configurée apparaît dans la liste des clés du coffre.

![Espace de travail [!DNL Keys] avec le nom de clé en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Étapes suivantes

Pour poursuivre le processus unique de configuration de la fonctionnalité de clés gérées par le client, continuez avec les guides de configuration des clés [API](./api-set-up.md) ou [IU](./ui-set-up.md) gérés par le client.
