---
title: Clés gérées par le client dans Adobe Experience Platform
description: Découvrez comment configurer vos propres clés de chiffrement pour les données stockées dans Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 2564c0cc817362536f1a8291e1c733d9efbf5a78
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 75%

---

# Clés gérées par le client dans Adobe Experience Platform

Les données stockées sur Adobe Experience Platform sont chiffrées au repos à l’aide de clés au niveau du système. Si vous utilisez une application reposant sur Platform, vous pouvez choisir d’utiliser vos propres clés de chiffrement pour mieux contrôler la sécurité de vos données.

>[!NOTE]
>
>Les données du lac de données Adobe Experience Platform et de la banque de profils sont chiffrées à l’aide de CMK. Ils sont considérés comme vos principaux entrepôts de données.

Ce document décrit le processus d’activation de la fonctionnalité des clés gérées par le client (CMK) dans Platform.

## Conditions préalables

Pour accéder aux API de CMK, vous devez affecter la variable [!UICONTROL Gestion de la clé gérée par le client] l’autorisation et l’accès à un environnement de test de production à un rôle nouveau ou existant associé aux informations d’identification de l’API. Si vous souhaitez fournir ces informations d’identification d’API avec uniquement un accès CMK, il est recommandé de créer un nouveau rôle d’administrateur CMK avec les autorisations nécessaires mentionnées précédemment.

Pour plus d’informations sur l’affectation de rôles et d’autorisations dans Experience Platform, reportez-vous à la section [configuration de la documentation sur les autorisations](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Pour activer le CMK, votre [!DNL Azure] Key Vault doit être configuré avec les paramètres suivants :

* [Activer la protection contre le vidage](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Activation de la suppression progressive](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurer l’accès à l’aide de [!DNL Azure] contrôle d’accès en fonction du rôle](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

## Résumé du processus

La fonction CMK est incluse dans les offres Adobe Healthcare Shield et Privacy and Security Shield. Une fois que votre entreprise a acheté une licence pour l’une de ces offres, vous pouvez lancer un processus unique de configuration de la fonctionnalité.

>[!WARNING]
>
>Après avoir configuré la fonction CMK, vous ne pouvez pas revenir aux clés gérées par le système. Il vous incombe de gérer vos clés en toute sécurité et de fournir l’accès à votre coffre de clés, à votre clé et à votre application CMK dans [!DNL Azure] pour éviter de perdre l’accès à vos données.

Le processus se présente comme suit :

1. [Configurez un coffre  [!DNL Azure]  Key Vault](#create-key-vault) en fonction des politiques de votre entreprise, puis [générez une clé de chiffrement](#generate-a-key) qui sera à la fin partagée avec Adobe.
1. Utilisez les appels d’API pour [configurer l’application CMK](#register-app) avec votre client [!DNL Azure].
1. Utilisez les appels d’API pour [envoyer votre ID de clé de chiffrement à Adobe](#send-to-adobe) et lancez le processus d’activation de la fonctionnalité.
1. [Vérifiez le statut de la configuration](#check-status) pour vous assurer que la fonction CMK a été activée.

Une fois le processus de configuration terminé, toutes les données intégrées à Platform dans l’ensemble des sandbox seront chiffrées à l’aide de votre configuration de clé [!DNL Azure]. Pour vous servir de la fonction CMK, vous utiliserez la fonctionnalité [!DNL Microsoft Azure] pouvant faire partie de leur [programme de préversion publique](https://azure.microsoft.com/fr-fr/support/legal/preview-supplemental-terms/).

## Configurer un coffre [!DNL Azure] Key Vault {#create-key-vault}

La fonction CMK ne prend en charge que les clés d’un coffre [!DNL Microsoft Azure] Key Vault. Pour commencer, vous devez utiliser [!DNL Azure] pour créer un compte d’entreprise ou utiliser un compte d’entreprise existant, puis suivre les étapes ci-dessous pour créer le coffre de clés.

>[!IMPORTANT]
>
>Seuls les niveaux de service Premium et Standard d’[!DNL Azure] Key Vault sont pris en charge. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] et [!DNL Azure Payments HSM] ne sont pas pris en charge. Reportez-vous à la documentation d’[[!DNL Azure] ](https://learn.microsoft.com/fr-fr/azure/security/fundamentals/key-management#azure-key-management-services) pour plus d’informations sur les services de gestion de clés proposés.

>[!NOTE]
>
>La documentation ci-dessous ne couvre que les étapes de base pour créer le coffre de clés. En dehors de ces instructions, vous devez configurer le coffre de clés en fonction des politiques de votre entreprise.

Connectez-vous au portail [!DNL Azure] et utilisez la barre de recherche pour accéder à **[!DNL Key vaults]** sous la liste des services.

![Rechercher et sélectionner des coffres de clés](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

La page **[!DNL Key vaults]** s’affiche après avoir sélectionné le service. À partir de là, sélectionnez **[!DNL Create]**.

![Créer un coffre de clés](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

À l’aide du formulaire fourni, renseignez les détails de base du coffre de clés, y compris un nom et un groupe de ressources affecté.

>[!WARNING]
>
>Bien que la plupart des options puissent rester sur leurs valeurs par défaut, **assurez-vous d’activer les options de suppression réversible et de protection contre le vidage**. Si vous n’activez pas ces fonctionnalités, vous risquez de perdre l’accès à vos données si le coffre de clés est supprimé.
>
>![Activer la protection contre le vidage](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

À partir de là, continuez à parcourir le processus de création de coffre de clés et configurez les différentes options en fonction des politiques de votre entreprise.

Une fois l’étape **[!DNL Review + create]** atteinte, vous pouvez vérifier les détails du coffre de clés pendant la validation. Une fois la validation acceptée, sélectionnez **[!DNL Create]** pour terminer le processus.

![Configuration de base pour le coffre de clés](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

### Configurer les options de mise en réseau

Si votre coffre de clés est configuré pour restreindre l’accès public à certains réseaux virtuels ou pour désactiver entièrement l’accès public, vous devez accorder à Microsoft une exception de pare-feu.

Sélectionnez **[!DNL Networking]** dans le volet de navigation de gauche. Sous **[!DNL Firewalls and virtual networks]**, cochez la case **[!DNL Allow trusted Microsoft services to bypass this firewall]**, puis sélectionnez **[!DNL Apply]**.

![Configuration de base pour le coffre de clés](../images/governance-privacy-security/customer-managed-keys/networking.png)

### Générer une clé {#generate-a-key}

Une fois que vous avez créé un coffre de clés, vous pouvez générer une nouvelle clé. Accédez à l’onglet **[!DNL Keys]** et sélectionnez **[!DNL Generate/Import]**.

![Générer une clé](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilisez le formulaire fourni pour attribuer un nom à la clé, puis sélectionnez **RSA** pour le type de clé. Au minimum, la variable **[!DNL RSA key size]** doit être au moins **3072** bits requis par [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] est également compatible avec RSA 3027.

>[!NOTE]
>
>Mémorisez le nom que vous indiquez pour la clé, car il sera utilisé à une étape ultérieure lors de l’[envoi de la clé à Adobe](#send-to-adobe).

Utilisez les commandes restantes pour configurer la clé que vous souhaitez générer ou importer selon vos besoins. Lorsque vous avez terminé, sélectionnez **[!DNL Create]**.

![Configurer la clé](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La clé configurée apparaît dans la liste des clés du coffre.

![Clé ajoutée](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Configurer l’application CMK {#register-app}

Une fois que votre coffre de clés est configuré, l’étape suivante consiste à enregistrer l’application CMK qui se connectera à votre client [!DNL Azure].

### Prise en main

L’enregistrement de l’application CMK nécessite que vous exécutiez des appels vers les API Platform. Pour plus d’informations sur la collecte des en-têtes d’authentification requis pour effectuer ces appels, consultez le [guide d’authentification des API Platform](../../landing/api-authentication.md).

Le guide d’authentification fournit des instructions sur la génération de votre propre valeur unique pour l’en-tête de requête `x-api-key`, toutes les opérations API de ce guide utilisent plutôt la valeur statique `acp_provisioning`. Cependant, vous devez toujours fournir vos propres valeurs pour `{ACCESS_TOKEN}` et `{ORG_ID}`.

Dans tous les appels API présentés dans ce guide, `platform.adobe.io` est utilisé comme chemin racine, qui correspond par défaut à la région VA7. Si votre entreprise utilise une autre région, `platform` doit être suivie d’un tiret et du code de région affecté à votre organisation : `nld2` pour NLD2 ou `aus5` pour AUS5 (par exemple : `platform-aus5.adobe.io`). Si vous ne connaissez pas la région de votre entreprise, contactez votre administrateur système.

### Récupérer une URL d’authentification

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

![Accepter la requête d’autorisation](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Attribuer l’application CMK à un rôle {#assign-to-role}

Une fois le processus d’authentification terminé, revenez au coffre de clés [!DNL Azure] et sélectionnez **[!DNL Access control]** dans le volet de navigation de gauche. À partir de là, sélectionnez **[!DNL Add]**, puis **[!DNL Add role assignment]**.

![Ajouter une affectation de rôle](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

L’écran suivant vous invite à choisir un rôle pour cette affectation. Sélectionnez **[!DNL Key Vault Crypto Service Encryption User]** avant de sélectionner **[!DNL Next]** pour continuer.

![Sélectionner un rôle](../images/governance-privacy-security/customer-managed-keys/select-role.png)

Dans l’écran suivant, choisissez **[!DNL Select members]** pour ouvrir une boîte de dialogue dans le rail de droite. Utilisez la barre de recherche pour localiser le principal de service de l’application CMK et sélectionnez-le dans la liste. Lorsque vous avez terminé, sélectionnez **[!DNL Save]**.

>[!NOTE]
>
>Si vous ne trouvez pas votre application dans la liste, votre principal de service n’a pas été accepté dans votre client. Veuillez travailler avec votre administrateur ou représentant [!DNL Azure] pour vous assurer que vous disposez des privilèges appropriés.

## Activer la configuration de la clé de chiffrement sur Experience Platform {#send-to-adobe}

Après l’installation de l’application CMK sur [!DNL Azure], vous pouvez envoyer votre identifiant de la clé de chiffrement à Adobe. Sélectionnez **[!DNL Keys]** dans le volet de navigation de gauche, suivi du nom de la clé à envoyer.

![Sélectionner la clé](../images/governance-privacy-security/customer-managed-keys/select-key.png)

Sélectionnez la dernière version de la clé et sa page de détails s’affiche. À partir de là, vous pouvez éventuellement configurer les opérations autorisées pour la clé. Au moins, la clé doit être accordée aux autorisations **[!DNL Wrap Key]** et **[!DNL Unwrap Key]**.

Le champ **[!UICONTROL Identifiant de clé]** affiche l’identifiant d’URI de la clé. Copiez cette valeur d’URI à utiliser à l’étape suivante.

![Copier l’URL de clé](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Une fois que vous avez obtenu l’URI du coffre de clés, vous pouvez l’envoyer à l’aide d’une requête POST au point d’entrée de configuration du CMK.

>[!NOTE]
>
>Seul le coffre de clés et le nom de la clé sont stockés dans Adobe, et pas la version de la clé.

**Requête**

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
| `name` | Un nom pour la configuration. Veillez à mémoriser cette valeur, car il sera nécessaire de vérifier le statut de la configuration à une [étape ultérieure](#check-status). La valeur respecte la casse. |
| `type` | Le type de configuration. Cette propriété doit être définie sur `BYOK_CONFIG`. |
| `imsOrgId` | Votre identifiant d’organisation. Il doit s’agir de la même valeur que celle fournie sous l’en-tête `x-gw-ims-org-id`. |
| `configData` | Contient les détails suivants sur la configuration :<ul><li>`providerType` : Cette propriété doit être définie sur `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier` : URI de coffre de clés que vous avez copié [précédemment](#send-to-adobe).</li></ul> |

**Réponse**

Une réponse réussie renvoie les détails du traitement de la configuration.

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
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

Le traitement doit être terminé dans les minutes qui suivent.

## Vérifiez le statut de la configuration {#check-status}

Pour vérifier le statut de la demande de configuration, vous pouvez effectuer une requête GET.

**Requête**

Vous devez ajouter le `name` de la configuration que vous souhaitez vérifier au chemin d’accès (`config1` dans l’exemple ci-dessous) et inclure un paramètre de requête `configType` défini sur `BYOK_CONFIG`.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie le statut du traitement.

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
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

L’attribut `status` peut avoir l’une des quatre valeurs ayant la signification suivante :

1. `RUNNING` : vérifie que Platform a la possibilité d’accéder à la clé et au coffre de clés.
1. `UPDATE_EXISTING_RESOURCES` : le système ajoute le coffre de clés et le nom des clés aux magasins de données de tous les sandbox de votre entreprise.
1. `COMPLETED` : le coffre de clés et le nom des clés ont été ajoutés aux magasins de données.
1. `FAILED` : un problème s’est produit, principalement lié à la configuration de la clé, du coffre de clés ou de l’application multi-utilisateur.

## Révoquer l’accès {#revoke-access}

Si vous souhaitez révoquer l’accès de Platform à vos données, vous pouvez supprimer le rôle d’utilisateur associé à l’application du coffre de clés dans [!DNL Azure].

>[!WARNING]
>
>La désactivation du coffre de clés, de la clé ou de l’application CMK peut entraîner une modification entraînant une rupture. Une fois que l’application Key Vault, Key ou CMK est désactivée et que les données ne sont plus accessibles dans Platform, les opérations en aval liées à ces données ne seront plus possibles. Assurez-vous de comprendre les impacts en aval de la révocation de l’accès à Platform à votre clé avant d’apporter des modifications à votre configuration.

Après avoir supprimé l’accès à la clé ou désactivé/supprimé la clé de votre [!DNL Azure] Vault clé, qui peut prendre entre quelques minutes et 24 heures pour que cette configuration se propage aux entrepôts de données principaux. Les workflows Platform incluent également les entrepôts de données en mémoire cache et transitoires requis pour les performances et les fonctionnalités de base des applications. La propagation de la révocation du CMK via ces magasins mis en cache et transitoires peut prendre jusqu’à sept jours, comme déterminé par leurs workflows de traitement des données. Par exemple, cela signifie que le tableau de bord Profil conserve et affiche les données de son entrepôt de données de cache et met sept jours à expiration pour que les données conservées dans les entrepôts de données du cache fassent l’objet d’un cycle d’actualisation. Le même délai s’applique pour que les données soient à nouveau disponibles lors de la réactivation de l’accès à l’application.

>[!NOTE]
>
>Il existe deux exceptions spécifiques au cas d’utilisation à l’expiration du jeu de données de sept jours sur les données non primaires (mises en cache/transitoires). Pour plus d’informations sur ces fonctionnalités, consultez leur documentation respective.<ul><li>[Réducteur d’URL Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=fr#message-preset-sms)</li><li>[Projections Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Étapes suivantes

En suivant les étapes ci-dessus, vous avez activé le CMK pour votre entreprise. Les données ingérées dans les entrepôts de données principaux seront désormais chiffrées et déchiffrées à l’aide des clés de votre [!DNL Azure] Key Vault.

