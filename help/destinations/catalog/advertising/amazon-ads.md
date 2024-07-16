---
title: Amazon Ads
description: Amazon Ads offre toute une gamme de solutions pour vous aider à atteindre vos objectifs publicitaires. Les partenaires de vente enregistrés, les vendeurs et vendeuses, les marchands de livres, les auteures et auteurs Kindle Direct Publishing (KDP), les personnes développant des applications et/ou les agences peuvent tirer parti du connecteur. L’intégration d’Amazon Ads à Adobe Experience Platform offre une intégration clé en main aux produits Amazon Ads, y compris Amazon DSP (ADSP). À l’aide de la destination Amazon Ads dans Adobe Experience Platform, les utilisateurs et utilisatrices peuvent définir des audiences d’annonceurs pour le ciblage et l’activation sur Amazon DSP.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 8e34e5488ab80cd1f3c8086bf7c16d3f22527540
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 55%

---

# Connexion Amazon Ads (Beta) {#amazon-ads}

## Présentation {#overview}

[!DNL Amazon Ads] offre toute une gamme d’options pour vous aider à atteindre vos objectifs publicitaires pour les vendeurs enregistrés, les vendeurs, les vendeurs de livres, les auteurs de publication directe Kindle (KDP), les développeurs d’applications et/ou les agences.

L’intégration [!DNL Amazon Ads] à Adobe Experience Platform permet l’intégration clé en main des produits [!DNL Amazon Ads], y compris Amazon DSP (ADSP) et Amazon Marketing Cloud (AMC).

En utilisant la destination [!DNL Amazon Ads] dans Adobe Experience Platform, les utilisateurs peuvent définir des audiences d’annonceurs pour le ciblage et l’activation sur la DSP Amazon.  En outre, les utilisateurs peuvent charger leurs données vers [!DNL Amazon Marketing Cloud] pour comprendre les performances par audience, les dimensions fournies par l’annonceur, l’appartenance à des segments Amazon ou d’autres signaux disponibles dans AMC. Après avoir téléchargé les audiences de l’annonceur vers AMC, les utilisateurs peuvent utiliser [!DNL Amazon Marketing Cloud] pour modifier, améliorer ou ajouter des audiences aux membres de l’audience à l’aide de signaux Amazon depuis [!DNL Amazon Marketing Cloud].

AMC rassemble des signaux uniques provenant de propriétés détenues et exploitées par Amazon, qui s’étendent sur plusieurs médias, y compris l’affichage, la vidéo, la diffusion en continu de la télévision, l’audio et les publicités sponsorisées. Les utilisateurs peuvent facilement envoyer des segments traités de Adobe Experience Platform à AMC afin d’améliorer l’apprentissage, tels que les groupes sur le marché des audiences, les cohortes de style de vie et les schémas d’engagement de la marque. Les segments augmentés peuvent ensuite être utilisés pour optimiser les activations multimédia dans Amazon DSP.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe *[!DNL Amazon Ads]*. Il s’agit actuellement d’un produit en version Beta qui peut faire l’objet de modifications. Pour toute demande ou information, contactez directement l’équipe d’Amazon Ads à l’adresse *`amc-support@amazon.com`.*

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination *[!DNL Amazon Ads]*, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Activation et ciblage {#activation-and-targeting}

Cette intégration avec Amazon DSP permet à [!DNL Amazon Ads] annonceurs de transmettre des audiences CDP de l’annonceur de Adobe Experience Platform à Amazon DSP de créer des audiences de l’annonceur pour le ciblage publicitaire. Configurez Amazon DSP pour effectuer un ciblage positif ou négatif (suppression) des audiences.

### Analytics et mesure {#analytics-and-measurement}

Cette intégration à [!DNL Amazon Marketing Cloud] (AMC) permet aux annonceurs [!DNL Amazon Ads] de transmettre des segments CDP du formulaire Adobe Experience Platform à AMC. Les annonceurs peuvent alors joindre les entrées CDP avec des signaux [!DNL Amazon Ads] et effectuer des analyses personnalisées sur des sujets tels que l’impact multimédia, les segments d’audience et les parcours client dans un format conforme à la confidentialité. Par exemple, un annonceur peut charger une liste de ses clients existants pour comprendre les performances agrégées des campagnes publicitaires ou des statistiques agrégées d’événements de conversion on-Amazon, telles que l’affichage d’une page des détails d’un produit, l’ajout d’un produit à un panier ou l’achat d’un produit.

### Optimisation d’Advertising

Cette intégration à [!DNL Amazon Marketing Cloud] (AMC) permet aux annonceurs de charger leurs propres listes de clients et d’utiliser [!DNL Amazon Marketing Cloud] SQL, d’exécuter de manière récurrente des analyses de chevauchement, des suppressions, des ajouts ou des optimisations sur les audiences avant de créer une audience prête pour l’activation dans Amazon DSP pour le ciblage.

## Conditions préalables {#prerequisites}

Pour utiliser la connexion [!DNL Amazon Ads] avec Adobe Experience Platform, les utilisateurs doivent d’abord avoir accès à un compte Amazon DSP Advertiser ou à une instance [!DNL Amazon Marketing Cloud]. Pour configurer ces instances, consultez la page suivante du site web [!DNL Amazon Ads] :

* [Commencer avec Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Prise en main du Marketing Cloud Amazon](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identités prises en charge {#supported-identities}

La connexion *[!DNL Amazon Ads]* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service//features/namespaces.md). Pour plus d’informations sur les identités prises en charge par [!DNL Amazon Ads], consultez le [Centre de support Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identité cible | Description | Considérations |
|---|---|---|
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation d’audience]** | Vous exportez tous les profils membres d’une audience ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination *[!DNL Amazon Ads]*. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

Vous accédez à l’interface de connexion [!DNL Amazon Ads] où vous sélectionnez pour la première fois les comptes d’annonceurs auxquels vous souhaitez vous connecter. Lors de la connexion, on vous redirige vers Adobe Experience Platform avec une nouvelle connexion fournie avec l’ID du compte publicitaire que vous avez sélectionné. Sélectionnez le compte publicitaire approprié dans l’écran de configuration de destination pour continuer.

* **[!UICONTROL Jeton porteur]** : renseignez le jeton porteur pour vous authentifier sur la destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Connexion Amazon Ads]** : sélectionnez l’identifiant du compte [!DNL Amazon Ads] cible utilisé pour la destination.

>[!NOTE]
>
>Après avoir enregistré la configuration de destination, vous ne pourrez pas modifier l’identifiant publicitaire [!DNL Amazon Ads], même si vous vous authentifiez à nouveau via votre compte Amazon. Pour utiliser un autre identifiant publicitaire [!DNL Amazon Ads], vous devez créer une nouvelle connexion de destination.

* **[!UICONTROL Zone géographique des annonceurs]** : sélectionnez la zone géographique dans laquelle votre annonceur est hébergé. Pour plus d’informations sur les marchés pris en charge par chaque zone géographique, consultez la [documentation Amazon Ads](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Configurer une nouvelle destination](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

La connexion [!DNL Amazon Ads] prend en charge les adresses électroniques hachées et les numéros de téléphone hachés à des fins de correspondance d’identité. La capture d’écran ci-dessous fournit un exemple de correspondance compatible avec la connexion [!DNL Amazon Ads] :

![Mappage Adobe vers Amazon Ads.](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Pour mapper des adresses e-mail hachées, sélectionnez l’espace de noms d’identité `Email_LC_SHA256` comme champ source.
* Pour mapper des numéros de téléphone hachés, sélectionnez l’espace de noms d’identité `Phone_SHA256` comme champ source.
* Pour mapper des adresses e-mail ou des numéros de téléphone non hachés, sélectionnez les espaces de noms d’identité correspondants comme champs source, puis cochez la case `Apply Transformation` pour que Platform hache les identités lors de l’activation.

Vous ne sélectionnez un champ cible donné qu’une seule fois dans une configuration de destination du connecteur [!DNL Amazon Ads].  Par exemple, si vous envoyez des courriers électroniques professionnels, vous ne pouvez pas mapper les courriers électroniques personnels dans la même configuration de destination.

Il est vivement recommandé de mapper autant de champs que possible. Si un seul attribut source est disponible, vous pouvez mapper un seul champ. La destination [!DNL Amazon Ads] utilise tous les champs mappés à des fins de mappage, produisant des taux de correspondance plus élevés si d’autres champs sont fournis. Pour plus d’informations sur les identifiants acceptés, consultez la [page d’aide sur les audiences hachées Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois votre audience chargée, vous pouvez vérifier qu’elle a été créée et chargée correctement en procédant comme suit :

**Pour Amazon DSP**

Accédez à votre **[!UICONTROL identifiant publicitaire]** > **[!UICONTROL Audiences]** > **[!UICONTROL Publicités publicitaires]**. Si votre audience a été créée avec succès et qu’elle contient le nombre minimum de membres, le statut `Active` s’affiche. Vous trouverez plus d’informations sur la taille et la portée de votre audience dans le panneau Portée prévue sur le côté droit de l’interface utilisateur d’Amazon DSP.

![Validation de la création d’audiences Amazon DSP.](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Pour[!DNL Amazon Marketing Cloud]**

Dans le navigateur de schéma de gauche, recherchez votre audience sous **[!UICONTROL Annonceur téléchargé]** > **[!UICONTROL aep_audiences]**. Vous pouvez ensuite interroger votre audience dans l’éditeur AMC SQL avec la clause suivante :

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![Validation de la création d’audience de Marketing Cloud Amazon](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour accéder à une documentation d’aide supplémentaire, consultez les ressources d’aide [!DNL Amazon Ads] suivantes :

* [Centre d’aide Amazon DSP](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Journal des modifications {#changelog}

Cette section répertorie les nouvelles fonctionnalités et les mises à jour importantes de la documentation consacrée au connecteur de destination.

+++ Afficher le journal des modifications

| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Mars 2024 | Nouvelles fonctionnalités et mise à jour de la documentation | Ajout de l’option permettant d’exporter les audiences à utiliser dans [!DNL Amazon Marketing Cloud] (AMC). |
| Mai 2023 | Nouvelles fonctionnalités et mise à jour de la documentation | <ul><li>Ajout de la prise en charge de la sélection de la zone géographique de l’annonceur dans le [workflow de connexion de destination](#destination-details).</li><li>Nouvelle documentation sur la fonctionnalité de sélection de la zone géographique de l’annonceur. Pour plus d’informations sur la sélection de la zone géographique de l’annonceur appropriée, consultez la [documentation d’Amazon](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Mars 2023 | Version initiale | Publication de la destination initiale et de la documentation. |

{style="table-layout:auto"}

+++
