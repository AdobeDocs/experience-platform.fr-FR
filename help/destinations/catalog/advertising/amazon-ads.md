---
title: Publicités Amazon
description: Amazon Ads offre toute une gamme d’options pour vous aider à atteindre vos objectifs publicitaires pour les vendeurs enregistrés, les vendeurs, les vendeurs de livres, les auteurs de publication directe Kindle (KDP), les développeurs d’applications et/ou les agences. L’intégration d’Amazon Ads à Adobe Experience Platform offre une intégration clé en main aux produits Amazon Ads, y compris le DSP Amazon (ADSP). À l’aide de la destination Amazon Ads dans Adobe Experience Platform, les utilisateurs peuvent définir des audiences d’annonceurs pour le ciblage et l’activation sur la DSP Amazon.
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 29%

---


# (Version bêta) Connexion Amazon Ads {#amazon-ads}

## Aperçu {#overview}

Amazon Ads offre toute une gamme d’options pour vous aider à atteindre vos objectifs publicitaires pour les vendeurs enregistrés, les vendeurs, les vendeurs de livres, les auteurs de publication directe Kindle (KDP), les développeurs d’applications et/ou les agences.

L’intégration d’Amazon Ads à Adobe Experience Platform offre une intégration clé en main aux produits Amazon Ads, y compris le DSP Amazon (ADSP). À l’aide de la destination Amazon Ads dans Adobe Experience Platform, les utilisateurs peuvent définir des audiences d’annonceurs pour le ciblage et l’activation sur la DSP Amazon.

Cette connexion prend en charge la création d’audiences dans les Amazon Marketplaces suivants : `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>Cette page de documentation a été créée par la fonction *Publicités Amazon* l&#39;équipe. Il s’agit actuellement d’un produit bêta qui peut faire l’objet de modifications. Pour toute demande de mise à jour ou de renseignements, contactez-les directement à l’adresse *`amc-support@amazon.com`.*

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable *Publicités Amazon* destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Activation et ciblage {#activation-and-targeting}

Cette intégration avec Amazon DSP permet aux annonceurs d’Amazon Ads de transmettre des segments CDP des annonceurs de Adobe Experience Platform à Amazon DSP afin de créer des audiences des annonceurs pour le ciblage publicitaire. Les audiences peuvent être sélectionnées dans Amazon DSP pour un ciblage positif, ainsi qu’un ciblage négatif (suppression). En outre, en utilisant des signaux générés par le Marketing Cloud Amazon, les annonceurs peuvent optimiser leurs audiences qui synchronisent les modifications d’audience avec les DSP Amazon.

## Conditions préalables {#prerequisites}

Pour utiliser la connexion Amazon Ads avec Adobe Experience Platform, les utilisateurs doivent d’abord avoir accès à un compte Amazon DSP Advertiser.  Pour configurer ces instances, consultez la page suivante du site web Amazon Ads :

* [Prise en main d’Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Identités prises en charge {#supported-identities}

Le *Publicités Amazon* La connexion prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md). Pour plus d’informations sur les identités prises en charge par Amazon Ads, consultez la page [Centre de support Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identité cible | Description | Considérations |
|---|---|---|
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la variable *Publicités Amazon* destination. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

Vous accédez à l’interface de connexion d’Amazon Ads où vous allez d’abord sélectionner les comptes publicitaires auxquels vous souhaitez vous connecter.  Lors de la connexion, vous serez redirigé vers Adobe Experience Platform avec une nouvelle connexion, fournie avec l’identifiant du compte publicitaire que vous avez sélectionné. Sélectionnez le compte Advertiser approprié dans l’écran de configuration de destination pour continuer.

* **[!UICONTROL Jeton de porteur]**: Renseignez le jeton porteur pour vous authentifier à la destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant publicitaire Amazon Ads]**: Sélectionnez l’identifiant du compte Amazon Ads cible utilisé pour la destination.

Remarque : une fois que vous aurez sélectionné cet identifiant publicitaire Amazon Ads, vous devrez créer une nouvelle destination pour modifier ce paramètre. Si vous réauthentifiez les informations d’identification OAuth et sélectionnez un nouvel identifiant publicitaire, vos modifications ne s’appliqueront pas.

![Configuration d’une nouvelle destination](../../assets/catalog/advertising/amazon_ads_image_1.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

La connexion Amazon Ads prend en charge les adresses électroniques hachées et les numéros de téléphone hachés à des fins de correspondance d’identité.  La capture d’écran ci-dessous fournit un exemple de correspondance compatible avec la connexion Amazon Ads :

![Mappage Adobe vers Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Pour mapper des adresses électroniques hachées, sélectionnez la variable `Email_LC_SHA256` espace de noms d’identité en tant que champ source.
* Pour mapper des numéros de téléphone hachés, sélectionnez l’option `Phone_SHA256` espace de noms d’identité en tant que champ source.
* Pour mapper des adresses électroniques ou des numéros de téléphone non hachés, sélectionnez les espaces de noms d’identité correspondants comme champs source, puis cochez la case `Apply Transformation` pour que Platform hache les identités lors de l’activation.

Il est vivement recommandé de mapper autant de champs que possible. Si un seul attribut source est disponible, vous pouvez mapper un seul champ.  La destination Publicités Amazon utilisera tous les champs mappés à des fins de mappage, produisant des taux de correspondance plus élevés si d’autres champs sont fournis. Pour plus d’informations sur les identifiants acceptés, consultez la [Page d’aide d’une audience hachée Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Données exportées / Validation de l’exportation des données {#exported-data}

Une fois votre audience chargée, vous pouvez vérifier que votre audience a été créée et chargée correctement en procédant comme suit :

**Pour Amazon DSP**

Accédez à votre identifiant publicitaire → Audiences → Publicitaires. Si votre audience a été créée avec succès et répond au nombre minimum de membres de l’audience, un état de `Active`.  Vous trouverez plus d’informations sur la taille et la portée de votre audience dans le panneau Portée prévue sur le côté droit de l’interface utilisateur d’Amazon DSP.

![Validation de la création d’audiences Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour accéder à une documentation d’aide supplémentaire, consultez les ressources d’aide Amazon Ads suivantes :

* [Centre d’aide Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
