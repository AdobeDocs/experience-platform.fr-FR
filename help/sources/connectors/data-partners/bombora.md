---
title: Intention de Bombora
description: Découvrez la source d’intention Bombora sur Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 8a5fdcfcf503df1b9d5aa338ff530181a2d03b5d
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 10%

---

# [!DNL Bombora Intent]

[!DNL Bombora] est une solution d’audience complète spécialisée dans les données d’intention B2B. [!DNL Bombora Intent] est une source Adobe Experience Platform que vous pouvez utiliser pour connecter votre compte [!DNL Bombora] à Experience Platform et intégrer les données d’intention de votre compte.

Avec la source de [!DNL Bombora Intent], vous pouvez intégrer [!DNL Bombora's] données d’intention de montée en puissance rapide de l’entreprise pour identifier les comptes recherchant activement vos produits ou services. Utilisez [!DNL Bombora] pour donner la priorité aux comptes de marché afin de créer des segments précis et d’exécuter des campagnes ABM hyper-ciblées. Vos efforts marketing se concentrent alors sur les comptes les plus susceptibles d’être convertis. De plus, vous pouvez tirer parti de stratégies axées sur les intentions pour optimiser les dépenses publicitaires, stimuler l’engagement et maximiser le retour sur investissement.

Lisez ce document pour obtenir les informations préalables sur la source de [!DNL Bombora].

## Cas d’utilisation {#use-cases}

Lisez les exemples de cas d’utilisation suivants que vous pouvez appliquer à la source de [!DNL Bombora].

### Intégration de Demand-Side Platform (DSP)

En tant que spécialiste marketing B2B, vous pouvez créer une liste de comptes dans Real-Time CDP, identifier les sociétés qui affichent une forte intention pour vos produits, puis activer cette liste dans [!DNL Bombora], qui s’intègre directement aux DSP, ce qui vous permet d’exécuter des campagnes publicitaires programmatiques ciblées à l’aide de données [!DNL Bombora's]. Cela garantit que vos dépenses publicitaires sont axées sur les entreprises les plus susceptibles de convertir leur contenu.

### Account-Based Marketing (ABM) Fonctionnalités

En tant que spécialiste marketing B2B, vous pouvez créer une liste de comptes basée sur des signaux d’intention propriétaires et tiers. Vous pouvez ensuite activer cette liste en [!DNL Bombora], où les fonctionnalités d’ABM vous permettent de cibler les employés de ces comptes en particulier, en veillant à ce que vos publicités atteignent les décideurs plutôt qu’une large audience.

### Activation ABM multicanal

En tant que spécialiste marketing B2B, vous pouvez créer une liste de comptes dans Real-Time CDP, identifier les sociétés à forte intention et l’activer dans le [!DNL Bombora] d’exécuter des campagnes ciblées sur plusieurs canaux. Sur les médias sociaux payants, vous pouvez diffuser des annonces personnalisées aux professionnels sur les comptes cibles de plateformes telles que [!DNL Linkedin] et [!DNL Facebook].

Grâce aux plateformes publicitaires natives, vous pouvez vous assurer que votre contenu parvient aux décideurs dans des contextes pertinents. Vous pouvez également étendre les campagnes à la télévision avancée, en diffusant des annonces sur des comptes clés. Cette approche multicanal garantit la cohérence des messages sur toutes les plateformes, en maximisant les taux d’engagement et de conversion.

## Conditions préalables {#prerequisites}

Lisez les sections suivantes pour connaître les étapes préalables requises avant de connecter [!DNL Bombora] à Experience Platform.

### Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à un place sur la liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre place sur la liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [place sur la liste autorisée d’adresse IP](../../ip-address-allow-list.md) pour plus d’informations.

### Configuration des autorisations sur Experience Platform

Pour connecter votre compte **[!UICONTROL à Experience Platform]** les autorisations **[!UICONTROL Afficher les sources et]** Gérer les sources[!DNL Bombora] doivent être activées. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/abac/ui/permissions.md).

### Contraintes de dénomination pour fichiers et répertoires

Les restrictions répertoriées ci-dessous doivent être prises en compte lors de l’attribution d’un nom à votre fichier ou répertoire d’espace de stockage :

* Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
* Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
* Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
* Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
* Les caractères de chemin d’URL non autorisés ne sont pas autorisés. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

### Collecter les informations d’identification requises

[!DNL Bombora] sur Experience Platform est hébergé par [!DNL Google Cloud Storage]. Pour authentifier correctement votre compte [!DNL Bombora], vous devez fournir les valeurs appropriées pour les informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| Identifiant de la clé d’accès | Identifiant de la clé d’accès [!DNL Bombora]. Il s’agit d’une chaîne alphanumérique de 61 caractères requise pour authentifier votre compte auprès d’Experience Platform. |
| Clé d’accès secrète | La clé d’accès secrète [!DNL Bombora]. Il s’agit d’une chaîne codée en base 64 de 40 caractères requise pour authentifier votre compte auprès d’Experience Platform. |
| Nom du compartiment | Compartiment [!DNL Bombora] à partir duquel les données seront extraites. |

Pour plus d’informations sur ces informations d’identification, consultez le [[!DNL Google Cloud Storage] guide des clés HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre clé d’accès, lisez le guide [prérequis [!DNL Google Cloud Storage]  dans la présentation de la source](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## [!DNL Bombora] le schéma {#schema}

Lisez cette section pour plus d’informations sur le schéma [!DNL Bombora] et la structure des données.

Le schéma [!DNL Bombora] est appelé **B2B Bombora Account Intent**. Il s’agit des informations d’intention hebdomadaires (recherche d’acheteur B2B anonyme et consommation de contenu) sur des comptes et des sujets spécifiés. Les données sont au format parquet.

* Classe - [!DNL Bombora Account Intent] XDM
* Espace de noms - [!DNL Bombora Account Intent] B2B
* Identité du Principal - `intentID`
* Relations - Compte B2B

| Nom du champ | Type de données | Description |
|------------------------|-----------|----------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OBJET | Ce champ est utilisé par le système pour le contrôle du système source. |
| `_id` | CHAÎNE | Ce champ est utilisé par le système comme identifiant unique. |
| `accountDomain` | CHAÎNE | Ce champ contient le domaine du compte. |
| `accountID` | CHAÎNE | Ce champ contient l’identifiant de compte B2B auquel cet enregistrement d’intention est associé. |
| `bomboraAccountName` | CHAÎNE | Ce champ contient l’ID de la société dans Bombora. |
| `clusterID` | CHAÎNE | Ce champ contient l’ID du cluster. |
| `clusterName` | CHAÎNE | Ce champ contient le nom du cluster. |
| `compositeScore` | ENTIER | Ce champ contient le score composite d’intention. |
| `intentID` | CHAÎNE | Ce champ contient une valeur unique générée par le système. |
| `partitionDate` | DATE | Ce champ contient la date de partition. Cette opération s’effectue toutes les semaines, en fin de semaine, au format `mm/dd/yyyy`. |
| `topicID` | CHAÎNE | Ce champ contient l’ID de rubrique d’intention de Bombora. |
| `topicName` | CHAÎNE | Ce champ contient le nom de la rubrique d’intention de Bombora. |

{style="table-layout:auto"}

>[!TIP]
>
>Toute modification du schéma sera communiquée à l’avance à Adobe. Pour prendre en charge une évolution transparente des schémas, le maintien de la rétrocompatibilité est essentiel. Experience Platform applique une approche de contrôle de version additif uniquement, en s’assurant que toutes les mises à jour du schéma sont non destructives. Cela signifie que les modifications avec rupture sont strictement interdites et que seules les modifications qui améliorent ou étendent le schéma existant sont autorisées.

## Connecter votre compte [!DNL Bombora] à Experience Platform dans l’interface utilisateur

Une fois la configuration requise terminée, consultez le tutoriel [connexion de votre compte  [!DNL Bombora]  Experience Platform](../../tutorials/ui/create/data-partners/bombora.md) pour démarrer votre intégration.

## Questions fréquentes {#faq}

Lisez cette section pour obtenir des réponses aux questions fréquentes sur la source de [!DNL Bombora].

### Ai-je besoin d’avoir un contrat existant avec [!DNL Bombora] pour utiliser ses données d’intention de compte dans Real-Time CDP B2B edition ?

+++Réponse

Oui, vous devez avoir un contrat actif avec [!DNL Bombora] pour accéder et utiliser leurs données d’intention dans Experience Platform et Real-Time CDP B2B edition. L’intégration tire parti de votre accord existant avec le [!DNL Bombora] pour ingérer et activer des signaux d’intention de compte dans Experience Platform et Real-Time CDP.

+++

### Les champs personnalisés de [!DNL Bombora] sont-ils pris en charge dans cette intégration ?

+++Réponse

Actuellement, vous ne pouvez utiliser que des champs de [!DNL Bombora] standard pour l’ingestion et l’activation. Pour afficher la liste des champs pris en charge, consultez le [[!DNL Bombora] guide des schémas](#schema) pour plus d’informations sur la disponibilité des champs.

+++

### Puis-je ingérer des données de [!DNL Bombora] vers Experience Platform de manière ad hoc ?

+++Réponse

Oui, vous pouvez ingérer des données à partir de [!DNL Bombora] sur une base ad hoc. Vous pouvez créer un flux de données pour ingérer les dernières données d’intention, à condition qu’il y ait de nouvelles données provenant de l’adresse [!DNL Bombora]. Cependant, vous ne pouvez avoir qu’un seul flux de données actif à la fois. Par conséquent, assurez-vous de supprimer le flux de données existant, avant d’en créer un nouveau.

+++

### Quel est le processus de validation des données d’intention et comment puis-je vérifier quelles données d’intention sont liées à un compte spécifique ?

+++Réponse

Pour valider les données d&#39;intention et déterminer quels signaux d&#39;intention sont liés à des comptes spécifiques, utilisez [Adobe Experience Platform Query Service](../../../query-service/home.md) par ID de compte.

+++

### Comment puis-je rechercher une intention pour une entreprise spécifique ?

+++Réponse

Exécutez une requête SQL dans [Query Service](../../../query-service/home.md) pour rechercher des données d’intention à l’aide du nom de la société ou de l’ID de compte. Pour afficher toutes les données d’intention pour une société spécifique, vous pouvez exécuter une requête SQL dans Query Service à l’aide du nom de la société ou de l’ID de compte pour récupérer tous les signaux d’intention associés.

+++


### J’ai détecté un problème lié au processus de correspondance de compte dans Experience Platform. Que dois-je faire ?

+++Réponse

La résolution dépend du problème spécifique :

* **Domaine de société incorrect ou manquant dans Experience Platform** : si le problème provient d’une valeur de domaine de société incorrecte dans les données de compte, mettez à jour le champ domaine de société dans Experience Platform pour assurer une correspondance précise.
* **Mappage de champ incorrect dans le flux de données** : si le problème est dû à un chemin de champ de domaine d’entreprise incorrect dans le flux de données, mettez à jour la configuration du flux de données pour référencer le chemin de champ correct.

+++

### Comment supprimer des données d’intention dans Experience Platform ?

+++Réponse

Vous devez [supprimer le jeu de données](../../../catalog/datasets/user-guide.md#delete-a-dataset) pour supprimer les données d’intention dans Experience Platform.

+++

### Quel champ est utilisé pour faire correspondre les comptes de [!DNL Bombora] à Experience Platform ?

+++Réponse

Le champ `accountOrganization.domain` est utilisé pour les comptes correspondants. Si votre organisation utilise un autre champ personnalisé pour stocker le nom du site web, assurez-vous de fournir le chemin d’accès au champ correct pour un mappage précis.

+++

### Que se passe-t-il lorsqu’un domaine d’entreprise est mis à jour dans Experience Platform ?

+++Réponse

Lorsqu’un domaine d’entreprise est mis à jour, la nouvelle valeur de domaine est appliquée lors de la prochaine exécution du flux de données. Cela permet de s’assurer que :

* L’ingestion des données de future intention utilise le domaine mis à jour pour la correspondance de compte.
* Tous les signaux d’intention précédemment incohérents peuvent désormais s’aligner correctement sur le compte prévu.
* Aucune modification rétroactive n’est apportée aux données précédemment ingérées. Seules les nouvelles données et les données entrantes refléteront la mise à jour.

+++

### Qu’est-ce que le processus de correspondance de domaine ?

+++Réponse

La correspondance de domaines dans Experience Platform est basée sur une correspondance exacte de la valeur du champ de domaine nettoyé. Experience Platform supprime automatiquement les préfixes (par exemple https:/<span>/www.) et conserve le domaine de niveau supérieur (par exemple adobe.com). La correspondance nécessite une valeur de domaine exacte, sans prise en charge de la correspondance approximative pour les sous-domaines.

+++

### Où puis-je utiliser les données d’intention ?

+++Réponse

Les données d’intention peuvent être utilisées dans [Audiences de compte](../../../segmentation/types/account-audiences.md) pour améliorer le ciblage, la segmentation et la personnalisation. En tirant parti des signaux d’intention, les entreprises peuvent identifier et interagir avec les comptes qui manifestent un grand intérêt pour des sujets spécifiques, ce qui optimise la portée du marketing et des ventes.

+++
