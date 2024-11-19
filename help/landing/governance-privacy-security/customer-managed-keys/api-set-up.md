---
title: Configuration et configuration des clés gérées par le client à l’aide de l’API
description: Découvrez comment configurer votre application CMK avec votre client Azure et envoyer votre ID de clé de chiffrement à Adobe Experience Platform.
role: Developer
feature: API, Privacy
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 49%

---

# Configuration et configuration des clés gérées par le client à l’aide de l’API

Ce document couvre le processus d’activation de la fonction de clés gérées par le client (CMK) dans Adobe Experience Platform à l’aide de l’API. Pour plus d’informations sur la façon d’effectuer ce processus à l’aide de l’interface utilisateur, reportez-vous au [document de configuration du CMK de l’interface utilisateur](./ui-set-up.md).

## Conditions préalables

Pour afficher et consulter la section [!UICONTROL Chiffrement] dans Adobe Experience Platform, vous devez avoir créé un rôle et lui avoir attribué l’autorisation [!UICONTROL Gérer la clé gérée par le client]. Tout utilisateur disposant de l’autorisation [!UICONTROL Gérer la clé gérée par le client] peut activer le CMK pour son organisation.

Pour plus d&#39;informations sur l&#39;attribution des rôles et des autorisations en Experience Platform, consultez la [documentation sur la configuration des autorisations](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Pour activer le CMK, votre [[!DNL Azure] Key Vault doit être configuré](./azure-key-vault-config.md) avec les paramètres suivants :

* [Activer la protection contre le vidage](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Activer soft-delete](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurer l’accès à l’aide du  [!DNL Azure] contrôle d’accès basé sur les rôles](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configuration d’un Key Vault  [!DNL Azure] ](./azure-key-vault-config.md)

## Configurer l’application CMK {#register-app}

Une fois que votre coffre-fort de clé est configuré, l’étape suivante consiste à s’enregistrer pour l’application CMK qui se connectera à votre client [!DNL Azure].

### Commencer

L’enregistrement de l’application CMK nécessite que vous exécutiez des appels vers les API Platform. Pour plus d’informations sur la collecte des en-têtes d’authentification requis pour effectuer ces appels, consultez le [guide d’authentification des API Platform](../../api-authentication.md).

Le guide d’authentification fournit des instructions sur la génération de votre propre valeur unique pour l’en-tête de requête `x-api-key`, toutes les opérations API de ce guide utilisent plutôt la valeur statique `acp_provisioning`. Cependant, vous devez toujours fournir vos propres valeurs pour `{ACCESS_TOKEN}` et `{ORG_ID}`.

Dans tous les appels API présentés dans ce guide, `platform.adobe.io` est utilisé comme chemin racine, qui correspond par défaut à la région VA7. Si votre organisation utilise une autre région, `platform` doit être suivi d’un tiret et du code de région affecté à votre organisation : `nld2` pour NLD2 ou `aus5` pour AUS5 (par exemple : `platform-aus5.adobe.io`). Si vous ne connaissez pas la région de votre entreprise, contactez votre administrateur système.

### Récupérer une URL d’authentification {#fetch-authentication-url}

Pour démarrer le processus d’enregistrement, envoyez une requête GET au point d’entrée d’enregistrement de l’application afin de récupérer l’URL d’authentification requise pour votre organisation.

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie une propriété `applicationRedirectUrl` contenant l’URL d’authentification.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Copiez et collez l’adresse `applicationRedirectUrl` dans un navigateur pour ouvrir une boîte de dialogue d’authentification. Sélectionnez **[!DNL Accept]** pour ajouter le principal de service de l’application CMK à votre client [!DNL Azure].

![Boîte de dialogue de demande d’autorisation Microsoft avec [!UICONTROL Accept] surlignée.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Attribuer l’application CMK à un rôle {#assign-to-role}

Une fois le processus d’authentification terminé, revenez au coffre de clés [!DNL Azure] et sélectionnez **[!DNL Access control]** dans le volet de navigation de gauche. À partir de là, sélectionnez **[!DNL Add]**, puis **[!DNL Add role assignment]**.

![ Le tableau de bord Azure Microsoft avec [!DNL Add] et [!DNL Add role assignment] surlignés.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

L’écran suivant vous invite à choisir un rôle pour cette affectation. Sélectionnez **[!DNL Key Vault Crypto Service Encryption User]** avant de sélectionner **[!DNL Next]** pour continuer.

>[!NOTE]
>
>Si vous disposez du niveau [!DNL Managed-HSM Key Vault], vous devez sélectionner le rôle d’utilisateur **[!DNL Managed HSM Crypto Service Encryption User]**.

![Le tableau de bord Azure Microsoft avec [!DNL Key Vault Crypto Service Encryption User] en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Dans l’écran suivant, choisissez **[!DNL Select members]** pour ouvrir une boîte de dialogue dans le rail de droite. Utilisez la barre de recherche pour localiser le principal de service de l’application CMK et sélectionnez-le dans la liste. Lorsque vous avez terminé, sélectionnez **[!DNL Save]**.

>[!NOTE]
>
>Si vous ne trouvez pas votre application dans la liste, votre principal de service n’a pas été accepté dans votre client. Pour vous assurer que vous disposez des privilèges appropriés, contactez votre administrateur ou représentant [!DNL Azure].

## Activer la configuration de la clé de chiffrement sur Experience Platform {#send-to-adobe}

Après l’installation de l’application CMK sur [!DNL Azure], vous pouvez envoyer votre identifiant de la clé de chiffrement à Adobe. Sélectionnez **[!DNL Keys]** dans le volet de navigation de gauche, suivi du nom de la clé à envoyer.

![Le tableau de bord Azure Microsoft avec l’objet [!DNL Keys] et le nom de clé mis en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Sélectionnez la dernière version de la clé et sa page de détails s’affiche. À partir de là, vous pouvez éventuellement configurer les opérations autorisées pour la clé.

>[!IMPORTANT]
>
>Les opérations minimales requises autorisées pour la clé sont les autorisations **[!DNL Wrap Key]** et **[!DNL Unwrap Key]**. Vous pouvez inclure [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] et [!DNL Verify] si vous le souhaitez.

Le champ **[!UICONTROL Identifiant de clé]** affiche l’identifiant d’URI de la clé. Copiez cette valeur d’URI à utiliser à l’étape suivante.

![Détails de la clé de tableau de bord Azure Microsoft avec [!DNL Permitted operations] et les sections Copier la clé URL mises en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Une fois que vous avez obtenu l’URI du coffre de clés, vous pouvez l’envoyer à l’aide d’une requête POST au point d’entrée de configuration du CMK.

>[!NOTE]
>
>Seul le coffre de clés et le nom de la clé sont stockés dans Adobe, et pas la version de la clé.

**Requête**

+++ Exemple de requête pour envoyer un URI de coffre-fort clé au point de terminaison de configuration du CMK.

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `name` | Un nom pour la configuration. Veillez à mémoriser cette valeur, car il est nécessaire de vérifier l’état de la configuration à une [étape ultérieure](#check-status). La valeur respecte la casse. |
| `type` | Le type de configuration. Cette propriété doit être définie sur `BYOK_CONFIG`. |
| `imsOrgId` | ID d’organisation. Cet identifiant doit être la même valeur que celle fournie sous l’en-tête `x-gw-ims-org-id`. |
| `configData` | Cette propriété contient les détails suivants sur la configuration :<ul><li>`providerType` : Cette propriété doit être définie sur `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier` : URI de coffre de clés que vous avez copié [précédemment](#send-to-adobe).</li></ul> |

+++

**Réponse**

+++ La réponse réussie renvoie les détails de la tâche de configuration.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

Le traitement de la tâche doit être terminé dans les minutes qui suivent.

## Vérifiez le statut de la configuration {#check-status}

Pour vérifier le statut de la demande de configuration, vous pouvez effectuer une requête GET.

**Requête**

Vous devez ajouter le `name` de la configuration que vous souhaitez vérifier au chemin d’accès (`config1` dans l’exemple ci-dessous) et inclure un paramètre de requête `configType` défini sur `BYOK_CONFIG`.

+++ Exemple de requête pour vérifier le statut de la requête de configuration.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Réponse**

+++ La réponse réussie renvoie l’état de la tâche.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

L’attribut `status` peut avoir l’une des quatre valeurs ayant la signification suivante :

1. `RUNNING` : vérifie que Platform peut accéder à la clé et à la clé Vault.
1. `UPDATE_EXISTING_RESOURCES` : le système ajoute le coffre de clés et le nom des clés aux magasins de données de tous les sandbox de votre entreprise.
1. `COMPLETED` : le coffre-fort de la clé et le nom de la clé ont été ajoutés avec succès aux banques de données.
1. `FAILED` : un problème s’est produit, principalement lié à la configuration de la clé, du coffre de clés ou de l’application multi-utilisateur.

## Étapes suivantes

En suivant les étapes ci-dessus, vous avez activé le CMK pour votre entreprise. Les données ingérées dans les entrepôts de données principaux seront désormais chiffrées et déchiffrées à l’aide des clés de votre Key Vault [!DNL Azure]. Pour en savoir plus sur le cryptage des données dans Adobe Experience Platform, consultez la [documentation sur le cryptage](../encryption.md).
