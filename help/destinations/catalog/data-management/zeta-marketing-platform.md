---
title: Plateforme marketing Zeta
description: La plateforme Zeta Marketing (ZMP) est un système basé sur le cloud qui vous permet d’acquérir, de développer et de fidéliser vos clients plus efficacement, optimisé par l’intelligence (données propriétaires et IA).
hide: true
hidefromtoc: true
exl-id: 291ee60c-aa81-4f1e-9df2-9905a8eeb612
source-git-commit: 0c3c192105146dd949e9b11f8925bf4f9d7c15c0
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 28%

---

# Plateforme marketing Zeta {#zeta-marketing-platform}

## Vue d’ensemble {#overview}

La plateforme Zeta Marketing (ZMP) est un système basé sur le cloud qui vous permet d’acquérir, de développer et de fidéliser vos clients plus efficacement, optimisé par l’intelligence (données propriétaires et IA). Pour plus d&#39;informations, reportez-vous à la section [Zeta Global](https://zetaglobal.com/).

Avec le connecteur Zeta Marketing Platform disponible dans Adobe Experience Platform, vous pouvez synchroniser facilement vos audiences de l’Experience Platform vers le ZMP.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et conservés par l’équipe *Zeta Global*. Pour toute question ou demande de mise à jour, contactez l’équipe à l’adresse [Contactez-nous](https://zetaglobal.com/about/contact-us/).

## Cas d’utilisation {#use-cases}

### Création de segments d’audience {#use-case-build-audiences}

Un marketeur souhaite créer des profils d’audience uniques, identifier les segments les plus précieux et les utiliser sur tous les canaux numériques pris en charge par la plateforme Zeta Marketing. Ils veulent créer une véritable vue 360 d’un profil de consommateur, créer et activer des audiences significatives. Vous trouverez plus d&#39;informations sur les canaux pris en charge par Zeta Marketing Platform [ici](https://zetaglobal.com/platform/integrations/).

### Cibler les utilisateurs avec des publicités {#use-case-target-users}

Un annonceur a pour but de cibler des utilisateurs dans des audiences spécifiques par le biais du Demand Side Platform Zeta (DSP), car ces utilisateurs interagissent avec leurs marques. Pour plus d&#39;informations sur le DSP Zeta, cliquez [ici](https://knowledgebase.zetaglobal.com/pug/).

## Conditions préalables {#prerequisites}

### Conditions préalables de la plateforme marketing Zeta

* Avant de configurer une nouvelle connexion à la destination Zeta Marketing Platform, vous devez créer une liste de clients vide dans votre compte Zeta Marketing Platform. Vous devez choisir l’une de ces listes de clients comme cible désignée pour recevoir l’audience Adobe Experience Platform que vous prévoyez d’envoyer. Vous pouvez créer une liste de clients vide dans le fichier ZMP en suivant les instructions [ici](https://knowledgebase.zetaglobal.com/kb/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Bien que Adobe Experience Platform permette l’activation de plusieurs audiences vers une instance de destination ZMP spécifique, il est obligatoire que chaque instance de destination ZMP ne reçoive qu’une seule audience Experience Platform. Pour gérer plusieurs audiences de l’Experience Platform, créez des instances de destination ZMP supplémentaires pour chaque audience et sélectionnez une liste de clients différente dans la liste déroulante. Cette approche permet de s’assurer que les audiences ZMP cibles ne sont pas écrasées. Voir [Renseignement des détails de destination](#destination-details) pour plus d’informations.
* Utilisez les informations d’identification suivantes pour configurer la destination :
   * Nom d’utilisateur : **api**
   * Mot de passe : votre clé d’API REST ZMP. Vous pouvez trouver votre clé API REST en vous connectant à votre compte ZMP et en accédant à la section **Paramètres** > **Intégrations** > **Clés et applications** . Pour plus d’informations, consultez la [documentation ZMP](https://knowledgebase.zetaglobal.com/kb/integrations) .

## Identités prises en charge {#supported-identities}

[!DNL Zeta Marketing Platform] prend en charge l’activation des ID utilisateur personnalisés décrits dans le tableau ci-dessous. Pour plus d’informations, voir [identities](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> La destination Zeta Marketing Platform exige que vous mappiez un espace de noms d’identité source à l’identité cible ZMP `uid`. Cela permet à la plateforme de marketing Zeta de différencier de manière unique chaque profil.

| Identité cible | Description | Considérations | Notes |
---------|----------|----------|----------|
| uid | Identifiant unique utilisé par ZMP pour différencier les profils de clients | Obligatoire | Choisissez l’espace de noms d’identité standard `Email` si vous souhaitez identifier des profils uniques à l’aide de leurs adresses électroniques. Vous pouvez également choisir de mapper votre espace de noms personnalisé à `uid` si les profils client n’ont pas d’adresse électronique. |
| email_md5_id | Courriel MD5 qui représente chaque profil client | Facultatif | Choisissez cette identité cible lorsque vous souhaitez identifier de manière unique les profils client à l’aide de valeurs MD5 d’email. Il est essentiel que les adresses électroniques soient déjà au format MD5 dans l’Experience Platform, car Platform ne convertit pas le texte brut en MD5. Dans ce scénario, définissez `uid` (obligatoire) sur les mêmes valeurs MD5 d&#39;email ou un autre espace de noms d&#39;identité approprié. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

>[!NOTE]
> À mesure que des membres individuels sont ajoutés ou supprimés de l’audience Platform, des mises à jour sont envoyées au fichier ZMP pour s’assurer que la liste des clients de destination est synchronisée en conséquence.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Nom d’utilisateur]** : `api`
* **[!UICONTROL Mot de passe]** : votre clé d’API REST ZMP. Vous pouvez trouver votre clé API REST en vous connectant à votre compte ZMP et en accédant à la section **Paramètres** > **Intégrations** > **Clés et applications** . Pour plus d’informations, consultez la [documentation ZMP](https://knowledgebase.zetaglobal.com/kb/integrations) .

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Image montrant la configuration ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant du site du compte ZMP]** : votre **identifiant du site** ZMP auquel vous souhaitez envoyer vos audiences. Vous pouvez afficher votre ID de site en accédant à la section **Paramètres** > **Intégrations** > **Clés et applications** . Vous trouverez plus d&#39;informations [ici](https://knowledgebase.zetaglobal.com/kb/integrations).
* **[!UICONTROL Segment ZMP]** : segment de liste de clients dans votre compte d’ID de site ZMP que vous souhaitez mettre à jour avec l’audience Platform.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’exportation de profils vers [!DNL Zeta Marketing Platform].

Sélection des champs sources :
* Sélectionnez un espace de noms d’identité source (personnalisé ou standard, tel que `Email`) qui identifie de manière unique un profil dans Adobe Experience Platform et [!DNL Zeta Marketing Platform].
* Sélectionnez tous les attributs de profil source XDM qui doivent être exportés vers et mis à jour dans le [!DNL Zeta Marketing Platform].

Sélection des champs cibles :
* (Obligatoire) Sélectionnez `uid` comme identité cible à laquelle vous mappez un espace de noms d’identité source.
* (Facultatif) Sélectionnez `email_md5_id` comme identité cible à laquelle vous avez mappé l’espace de noms de l’identité source qui représente les valeurs md5 du courrier électronique. Il est essentiel que les adresses électroniques soient déjà au format MD5 dans l’Experience Platform, car Platform ne convertit pas le texte brut en MD5.
* Sélectionnez d’autres mappings de ciblage si nécessaire.

![Mappage d’identités](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Une activation réussie de l’audience de l’Experience Platform vers la plateforme Zeta Marketing met à jour la liste des clients cible dans le fichier ZMP. Le nombre et les exemples de profils dans la liste des clients cibles seront égaux au nombre d’identités qui ont été activées avec succès.

![Liste des clients dans ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Chaque membre de l’audience qui a été activé à partir de l’Experience Platform est également visible sous **Audiences** > **Personnes** dans le fichier ZMP. Vous pourrez également afficher le segment **Liste de clients** auquel un profil appartient dans la vue Client unique, comme illustré ci-dessous.

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

* [Base de connaissances Zeta](https://knowledgebase.zetaglobal.com/kb/)
