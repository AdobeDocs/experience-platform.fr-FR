---
title: Configurer AWS KMS pour les clés gérées par le client
description: Découvrez comment configurer le service de gestion des clés (KMS) de Amazon Web Services à utiliser avec les clés gérées par le client dans Adobe Experience Platform.
exl-id: 0cf0deab-dc30-412f-b511-dee5504c3953
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 0%

---

# Configurer AWS KMS pour les clés gérées par le client

>[!AVAILABILITY]
>
>Ce document s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>[Les clés gérées par le client](../overview.md) (CMK) sur AWS sont prises en charge pour Privacy and Security Shield, mais ne sont pas disponibles pour Healthcare Shield. Les CMK sur Azure sont prises en charge pour Privacy and Security Shield ainsi que pour Healthcare Shield.

Utilisez ce guide pour sécuriser vos données avec Amazon Web Services (AWS) Key Management Service (KMS) en créant, gérant et contrôlant des clés de chiffrement pour Adobe Experience Platform. Cette intégration simplifie la conformité, rationalise les opérations grâce à l&#39;automatisation et élimine le besoin de gérer votre propre infrastructure de gestion clé.

Pour obtenir des instructions spécifiques à Customer Journey Analytics, reportez-vous à la documentation du CMK Customer Journey Analytics [&#128279;](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-privacy/cmk)

>[!IMPORTANT]
>
>Adobe Experience Platform chiffre les données inactives par défaut à l’aide de clés gérées par le système. En activant les clés gérées par le client (CMK), vous prenez le contrôle total de la sécurité de vos données. Toutefois, cette modification est irréversible. Une fois la fonction CMK activée, vous ne pouvez pas revenir aux clés gérées par le système. Il vous incombe de gérer vos clés en toute sécurité afin d’assurer un accès ininterrompu à vos données et d’éviter toute inaccessibilité potentielle.

Utilisez AWS KMS pour améliorer la sécurité des données avec la gestion intégrée des clés de chiffrement pour Adobe Experience Platform. Suivez ce guide pour créer et gérer des clés de chiffrement, en veillant à ce que vos données restent protégées.

## Conditions préalables {#prerequisites}

Avant de poursuivre avec ce document, vous devez avoir une bonne compréhension des concepts et fonctionnalités clés suivants :

- **Service de gestion des clés AWS (KMS)** : comprendre les principes de base du service de gestion des clés AWS, notamment comment créer, gérer et faire pivoter des clés de chiffrement. Consultez la [documentation officielle de KMS](https://docs.aws.amazon.com/kms/) pour en savoir plus.
- **Politiques de gestion des identités et des accès (IAM) dans AWS** : IAM est un service qui vous permet de gérer l’accès aux services et ressources AWS en toute sécurité. Utilisez IAM pour :
   - Définissez les utilisateurs, groupes et rôles qui ont accès à des ressources spécifiques.
   - Spécifiez les actions que les utilisateurs et utilisatrices sont autorisés ou non à effectuer.
   - Mettez en œuvre un contrôle d’accès affiné en attribuant des autorisations à l’aide de politiques IAM.
Pour plus d’informations, consultez la documentation officielle [Politiques IAM pour AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- **Sécurité des données dans Experience Platform** : découvrez comment Experience Platform assure la sécurité des données et s’intègre à des services externes tels qu’AWS KMS pour le chiffrement. Experience Platform protège les données avec HTTPS TLS v1.2 pour le transit, le chiffrement du fournisseur de cloud au repos, le stockage isolé et les options d’authentification et de chiffrement personnalisables. Consultez la [présentation de la gouvernance, de la confidentialité et de la sécurité](../overview.md) ou le document sur le [chiffrement des données dans Experience Platform](../../encryption.md) pour plus d’informations sur la manière dont vos données sont protégées.
- **AWS Management Console** : hub central où vous pouvez accéder à tous vos services AWS et les gérer à partir d’une application web. Utilisez la barre de recherche pour rechercher rapidement des outils, vérifier les notifications, gérer votre compte et la facturation et personnaliser vos paramètres. Pour plus d’informations, consultez la documentation [officielle de la console de gestion AWS](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html).

## Commencer {#get-started}

Ce guide nécessite que vous ayez déjà accès à un compte Amazon Web Services et à la console de gestion. Pour commencer, procédez comme suit :

### Sélectionner une région prise en charge {#select-supported-region}

AWS KMS est disponible dans des régions spécifiques. Assurez-vous d’opérer dans une région où KMS est pris en charge. Vous pouvez afficher une liste complète des régions prises en charge dans la liste des points d’entrée et quotas AWS KMS [&#128279;](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

Assurez-vous que votre clé de chiffrement AWS KMS se trouve dans la même région que votre instance Adobe Experience Platform afin de maintenir la conformité aux exigences de résidence des données, d’optimiser les performances et d’éviter des coûts supplémentaires inter-régions. Les régions mal alignées peuvent entraîner des problèmes d’accessibilité et d’intégration des données.

### Vérifier les autorisations {#verify-permissions}

Assurez-vous de disposer des autorisations AWS Identity and Access Management (IAM) nécessaires pour créer, gérer et utiliser des clés de chiffrement dans KMS. Pour vérifier vos autorisations :

1. Accédez au [simulateur de politiques IAM](https://policysim.aws.amazon.com/).
2. Sélectionnez votre compte utilisateur ou votre rôle.
3. Simuler des actions KMS telles que `kms:CreateKey` ou `kms:Encrypt`.

Si la simulation renvoie une erreur ou si vous n’êtes pas sûr de vos autorisations, contactez votre administrateur ou administratrice AWS pour obtenir de l’aide.

### Vérifier la configuration de votre compte AWS

Vérifiez que votre compte AWS est activé pour utiliser les services AWS KMS. L&#39;accès KMS est activé par défaut pour la plupart des comptes, mais vous pouvez vérifier la configuration de votre compte en consultant la [console de gestion AWS](https://aws.amazon.com/console/). Pour plus d’informations, consultez le [guide du développeur du service de gestion des clés AWS](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html).

### Accédez à AWS KMS pour commencer la configuration des clés

Pour commencer à configurer et gérer votre clé de chiffrement, connectez-vous à votre compte AWS et accédez à AWS Key Management Service (KMS). Dans la console de gestion AWS, sélectionnez **Service de gestion des clés (KMS)** dans le menu des services.

![Menu déroulant de recherche de la console de gestion AWS avec le service Key Management mis en surbrillance.](../../../images/governance-privacy-security/key-management-service/navigate-to-kms.png)

## Créer une clé {#create-a-key}

>[!IMPORTANT]
>
>Garantissez le stockage sécurisé, l’accès et la disponibilité des clés de chiffrement. Il vous incombe de gérer vos clés et d’éviter toute perturbation des opérations d’Experience Platform.

Dans l’espace de travail [!DNL Key Management Service (KMS)], sélectionnez **[!DNL Create a key]**.

![L’espace de travail Service Key Management avec l’option Créer une clé mise en surbrillance.](../../../images/governance-privacy-security/key-management-service/create-a-key.png)

## Configurer les paramètres clés {#configure-key}

Le workflow [!DNL Configure Key] s’affiche. Par défaut, le type de clé est défini sur **[!DNL Symmetric]** et l’utilisation de la clé sur **[!DNL Encrypt and Decrypt]**. Assurez-vous que ces options sont sélectionnées avant de continuer.

![La première étape du workflow Configurer les clés avec les options de base Symétrique et Chiffrer et déchiffrer est mise en surbrillance.](../../../images/governance-privacy-security/key-management-service/configure-key-basic-options.png)

Développez le menu déroulant **[!DNL Advanced options]** . Il est recommandé d’utiliser l’option **[!DNL KMS]**, qui permet à AWS de créer et de gérer les ressources clés. L’option **[!DNL KMS]** est sélectionnée par défaut.

>[!NOTE]
>
>Si vous disposez déjà d’une clé, vous pouvez importer du matériel de clé externe ou utiliser le Key Store d’AWS [!DNL CloudHSM]. Ces options ne sont pas couvertes dans le cadre de ce document.

Sélectionnez ensuite le paramètre [!DNL Regionality], qui spécifie la portée de la région de la clé. Sélectionnez **[!DNL Single-Region key]**, puis **[!DNL Next]** pour passer à l’étape 2.

>[!IMPORTANT]
>
>AWS applique des restrictions de région pour les clés KMS. Cette restriction de zone géographique signifie que la clé doit se trouver dans la même zone géographique que votre compte Adobe. Adobe ne peut accéder qu’aux clés KMS situées dans la région de votre compte. Assurez-vous que la région sélectionnée correspond à la région de votre compte à client unique Adobe.

![Étape 1 du workflow Configurer les clés avec les options avancées Région AWS, KMS et Région unique mises en surbrillance.](../../../images/governance-privacy-security/key-management-service/configure-key-advanced-options.png)

## Étiqueter et baliser votre clé {#add-labels-and-tags-to-key}

La deuxième étape [!DNL Add labels] du workflow s’affiche. Ici, vous configurez les champs [!DNL Alias] et [!DNL Tags] pour vous aider à gérer et à localiser votre clé de chiffrement à partir de la console AWS KMS.

Saisissez un libellé descriptif pour votre clé dans le champ de saisie **[!DNL Alias]**. L’alias agit comme un identifiant convivial, permettant de localiser rapidement la clé à l’aide de la barre de recherche de la console AWS KMS. Pour éviter toute confusion, choisissez un nom significatif qui reflète l’objectif de la clé, tel que « Adobe-Experience-Platform-Key » ou « Customer-Encryption-Key ». Vous pouvez également inclure une description de la clé si l’alias de la clé est insuffisant pour décrire son objectif.

Enfin, attribuez des métadonnées à votre clé en ajoutant des paires clé-valeur dans la section [!DNL Tags] . Cette étape est facultative, mais vous devez ajouter des balises pour catégoriser et filtrer les ressources AWS afin d’en faciliter la gestion. Par exemple, si votre organisation utilise plusieurs ressources Adobe, vous pouvez les baliser avec « Adobe » ou « Experience-Platform ». Cette étape supplémentaire facilite la recherche et la gestion de toutes les ressources associées dans la console de gestion AWS. Sélectionnez **[!DNL Add tag]** pour lancer le processus.

<!-- I do not have an AWS account with which to document the Add tag process as yet. -->

Lorsque vos paramètres vous conviennent, sélectionnez **[!DNL Next]** pour poursuivre le workflow.

![Étape 2 du workflow Configurer les clés avec l’alias, la description, les balises et le suivant mis en surbrillance.](../../../images/governance-privacy-security/key-management-service/add-labels.png)

## Définition des principales autorisations administratives {#define-key-admins}

La troisième étape du workflow de création de clé s’affiche. Pour garantir un accès sécurisé et contrôlé, vous pouvez choisir parmi les utilisateurs et rôles IAM ceux qui peuvent gérer la clé. Il existe deux options à ce stade : [!DNL Key administrators] et [!DNL Key deletion]. Dans la section **[!DNL Key administrators]** , cochez une ou plusieurs cases en regard du nom d’un utilisateur ou d’un rôle auquel vous souhaitez accorder des autorisations d’administrateur pour cette clé.

>[!NOTE]
>
>Vous ne pouvez pas créer d’administrateurs à cette étape du workflow.

Dans la section **[!DNL Key deletion]** , cochez la case pour accorder aux administrateurs de clés le droit de supprimer cette clé. Si vous ne cochez pas cette case, les utilisateurs administrateurs ne sont pas autorisés à effectuer cette opération.

Sélectionnez **[!DNL Next]** pour continuer le workflow.

![ L’étape Définir les autorisations administratives clés du workflow, avec les cases à cocher et l’option suivante en surbrillance.](../../../images/governance-privacy-security/key-management-service/define-key-admins.png)

## Octroi de l’accès aux utilisateurs clés {#assign-key-users}

Dans la quatrième étape du workflow, vous pouvez [!DNL Define key usage permissions]. Dans la liste **[!DNL Key users]**, cochez les cases de tous les utilisateurs et rôles IAM qui doivent être autorisés à utiliser cette clé.

De ce point de vue, vous pouvez également [!DNL Add another AWS account] ; toutefois, l’ajout d’autres comptes AWS est fortement déconseillé. L’ajout d’un autre compte peut introduire des risques et compliquer la gestion des autorisations pour les opérations de chiffrement et de déchiffrement. En conservant la clé associée à un seul compte AWS, Adobe garantit une intégration sécurisée avec AWS KMS, ce qui réduit les risques et garantit un fonctionnement fiable.

Sélectionnez **[!DNL Next]** pour continuer le workflow.

![ L’étape Définir les autorisations d’utilisation des clés du workflow, avec les cases à cocher et l’option suivante en surbrillance.](../../../images/governance-privacy-security/key-management-service/define-key-users.png)

## Vérifier la configuration des clés {#review}

L’étape de révision de la configuration de clé s’affiche. Vérifiez les détails clés dans les sections [!DNL Key configuration] et [!DNL Alias and description].

>[!NOTE]
>
>Assurez-vous que la région de clé est identique au compte AWS.

![Étape de révision du workflow avec les sections Configuration de clé et Alias et description mises en surbrillance.](../../../images/governance-privacy-security/key-management-service/review-key-configuration-details.png)

Sélectionnez **[!DNL Confirm]** pour terminer le processus. Vous revenez sur l’espace de travail Clés gérées par le client KMS qui répertorie toutes les clés disponibles.

## Étapes suivantes

Une fois AWS KMS configuré, commencez à configurer l’intégration à l’aide de l’interface utilisateur [!UICONTROL &#x200B; Configuration du chiffrement de plateforme &#x200B;] ou de l’API Adobe Experience Platform. Pour poursuivre le processus unique de configuration de la fonctionnalité Clés gérées par le client, reportez-vous au guide de configuration de l’interface utilisateur [UI](./ui-set-up.md).
