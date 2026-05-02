---
title: Présentation des trains de données
description: Découvrez comment les flux de données vous aident à connecter votre intégration Experience Platform SDK côté client aux produits Adobe et aux destinations tierces.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 79d724eec4903b8a3eee6f717d94fcd70a4ffcb7
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 48%

---

# Présentation des trains de données

Un flux de données représente la configuration côté serveur pour les SDK Web et Mobile [!DNL Adobe Experience Platform]. Alors que la commande [`configure`](/help/collection/js/commands/configure/overview.md) dans le SDK gère les paramètres côté client (tels que le `edgeDomain`), les flux de données gèrent toutes les autres configurations.

Lorsque vous envoyez une requête au [!DNL Edge Network], le `datastreamId` référence le flux de données où les données sont envoyées. Vous pouvez mettre à jour la configuration côté serveur sans modifier le code de votre site web.

Vous pouvez créer et gérer des flux de données en sélectionnant **[!UICONTROL Datastreams]** dans le volet de navigation de gauche de l’interface utilisateur de [!DNL Adobe Experience Platform] ou de la collecte de données.

![Copie d’écran de l’onglet Flux de données dans l’interface utilisateur de Adobe Experience Platform.](assets/overview/datastreams-tab.png)

Pour plus d’informations sur la configuration d’un train de données dans l’interface utilisateur, voir le [guide de configuration](/help/datastreams/configure.md).

## Gérer des données sensibles dans les trains de données {#sensitive}

>[!IMPORTANT]
>
>Le contenu de ce document ne constitue pas un avis juridique et n’est pas destiné à s’y substituer. Consultez le service juridique de votre entreprise pour obtenir des conseils sur le traitement des données sensibles.

Les politiques de gestion des données d’entreprise et les exigences réglementaires augmentent les restrictions quant à la manière dont les données sensibles des clientes et des clients peuvent être collectées, traitées et utilisées. Cela inclut la collecte, le traitement et l’utilisation des données de santé protégées (ISP), qui sont soumises à des réglementations telles que le Health Insurance Portability and Accountability Act (HIPAA).

Les flux de données fournissent trois méthodes pour vous aider à gérer en toute sécurité vos données sensibles :

* [Chiffrement amélioré](#encryption)
* [Gouvernance des données](#governance)
* [Journaux d’audit](#audit-logs)

### Chiffrement amélioré {#encryption}

Toutes les données transitant par le [!DNL Edge Network] sont acheminées par le biais de connexions sécurisées et chiffrées à l’aide du protocole [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Si le train de données introduit des données dans Experience Platform, les données sont alors chiffrées au repos dans le lac de données d’Experience Platform. Pour plus d’informations, consultez le document sur le [chiffrement des données dans Experience Platform](/help/landing/governance-privacy-security/encryption.md).

### Gouvernance des données {#governance}

Les flux de données utilisent les fonctionnalités de gouvernance des données intégrées d’Experience Platform pour empêcher l’envoi de données sensibles vers des services non conformes à la loi HIPAA. En étiquetant des champs spécifiques qui contiennent des données sensibles dans vos schémas de trains de données, vous pouvez contrôler de manière granulaire quels champs de données peuvent être utilisés à des fins spécifiques.

La vidéo suivante présente une brève vue d’ensemble de la manière dont les restrictions d’utilisation des données sont configurées et appliquées pour les trains de données dans l’interface utilisateur :

>[!VIDEO](https://video.tv.adobe.com/v/3413102/?captions=fre_fr&quality=12&learn=on&speedcontrol=on)

Dans Experience Platform, vous pouvez appliquer des [libellés d’utilisation des données sensibles](/help/data-governance/labels/reference.md#sensitive) aux schémas et aux champs contenant des données que votre organisation juge sensibles. Par exemple, le libellé `RHD` est utilisé pour désigner les informations protégées sur la santé ; le libellé `S1` représente les données de géolocalisation.

>[!NOTE]
>
>Pour plus d’informations sur l’application des libellés d’utilisation des données dans l’onglet [!UICONTROL Schemas] de l’interface utilisateur d’Experience Platform ou de la collecte de données, consultez le tutoriel [étiquetage des schémas](/help/xdm/tutorials/labels.md).

Lorsque vous créez un flux de données, si le schéma sélectionné contient des libellés d’utilisation de données sensibles, vous pouvez uniquement configurer le flux de données pour envoyer ces données vers des destinations conformes à la loi HIPAA. Actuellement, la seule destination conforme à la norme HIPAA prise en charge par les flux de données est [!DNL Adobe Experience Platform]. D’autres services de destination, notamment les destinations [!DNL Adobe Target], [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], de transfert d’événement et Edge, sont désactivés pour les flux de données contenant des libellés d’utilisation de données sensibles.

Si un schéma est utilisé dans un train de données existant avec des services non conformes à la loi HIPAA, la tentative d’ajout d’un libellé d’utilisation des données sensibles au schéma génère un message de violation de politique et empêche l’action. Le message spécifie le flux de données qui a déclenché la violation et suggère de supprimer du flux de données tout service non conforme à la loi HIPAA pour résoudre le problème.

### Journaux d’audit {#audit-logs}

Dans Experience Platform, les activités du train de données peuvent être surveillées sous la forme de journaux d’audit. Les journaux d’audit indiquent **qui** a effectué **quoi** action et **quand**, ainsi que d’autres données contextuelles qui peuvent vous aider à résoudre les problèmes liés aux flux de données afin d’aider votre entreprise à se conformer aux politiques de gestion des données d’entreprise et aux exigences réglementaires.

Chaque fois qu’un utilisateur ou une utilisatrice crée, met à jour ou supprime un train de données, un journal d’audit est créé pour enregistrer l’action. Il en va de même lorsqu’un utilisateur ou une utilisatrice crée, met à jour ou supprime un mappage par le biais de la [Préparation de données pour la collecte de données](/help/datastreams/data-prep.md). Qu’il s’agisse d’un flux de données ou d’un mappage mis à jour, le journal d’audit obtenu est classé sous le type de ressource [!UICONTROL Datastreams].

Consultez la documentation relative aux [journaux d’audit](/help/landing/governance-privacy-security/audit-logs/overview.md) pour plus d’informations sur la manière d’interpréter les journaux des trains de données et autres services pris en charge.

## Étapes suivantes {#next-steps}

Ce guide fournit une vue d’ensemble complète des trains de données et de leur utilisation dans le cadre de la collecte de données et du traitement des données sensibles. Pour obtenir des instructions sur la configuration d’un nouveau train de données, voir le [guide de configuration des trains de données](/help/datastreams/configure.md).
