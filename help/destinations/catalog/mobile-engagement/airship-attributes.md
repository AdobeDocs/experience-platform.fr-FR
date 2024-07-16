---
keywords: attributs de navire d’aviation;destination du navire d’aviation
title: Connexion Attributs Airship
description: Transférez en toute transparence les données d’audience Adobe à Airship en tant qu’attributs d’audience pour le ciblage au sein de Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 31%

---

# Connexion [!DNL Airship Attributes] {#airship-attributes-destination}

## Présentation {#overview}

[!DNL Airship] est la principale plateforme d’engagement client, qui vous aide à diffuser des messages omnicanaux personnalisés et significatifs à vos utilisateurs à chaque étape du cycle de vie des clients.

Cette intégration transmet les données de profil d’Adobe dans [!DNL Airship] en tant que [Attributs](https://docs.airship.com/guides/audience/attributes/) pour le ciblage ou le déclenchement.

Pour en savoir plus sur [!DNL Airship], consultez les [Airship Docs](https://docs.airship.com).

>[!TIP]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe [!DNL Airship]. Pour toute demande de mise à jour ou de demande de mise à jour, contactez-les directement à l’adresse [support.airship.com](https://support.airship.com/).

## Conditions préalables {#prerequisites}

Avant de pouvoir envoyer vos audiences à [!DNL Airship], vous devez :

* Activez les attributs dans votre projet [!DNL Airship].
* Générez un jeton porteur pour l’authentification.

>[!TIP]
>
>Créez un compte [!DNL Airship] via [ce lien d&#39;inscription](https://go.airship.eu/accounts/register/plan/starter/) si ce n&#39;est déjà fait.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse email, numéro de téléphone, nom) et/ou les identités, en fonction du mapping de vos champs. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Activation des attributs {#enable-attributes}

Les attributs de profil Adobe Experience Platform sont similaires aux attributs [!DNL Airship] et peuvent être facilement mappés les uns aux autres dans Platform à l’aide de l’outil de mappage présenté ci-dessous sur cette page.

Les projets [!DNL Airship] ont plusieurs attributs prédéfinis et par défaut. Si vous disposez d’un attribut personnalisé, vous devez d’abord le définir dans [!DNL Airship]. Pour plus d’informations, voir [Configuration et gestion des attributs](https://docs.airship.com/tutorials/audience/attributes/) .

## Générer un jeton porteur {#bearer-token}

Accédez à **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs &amp; Integrations]** dans le [tableau de bord Airship](https://go.airship.com) et sélectionnez **[!UICONTROL Tokens]** dans le menu de gauche.

Cliquez sur **[!UICONTROL Créer un jeton]**.

Attribuez un nom convivial à votre jeton, par exemple &quot;Destination des attributs d’Adobe&quot;, puis sélectionnez &quot;Accès complet&quot; pour le rôle.

Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les détails comme confidentiels.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Airship Attributes], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1

Tirez parti des données de profil collectées dans Adobe Experience Platform pour personnaliser le message et le contenu riche dans l’un des canaux de [!DNL Airship]. Par exemple, utilisez les données de profil [!DNL Experience Platform] pour définir les attributs d’emplacement dans [!DNL Airship]. Cela permet à une marque d’hôtel d’afficher une image pour l’emplacement d’hôtel le plus proche pour chaque utilisateur.

### Cas d’utilisation #2

Tirez parti des attributs de Adobe Experience Platform pour enrichir davantage les profils [!DNL Airship] et les combiner avec des données prédictives SDK ou [!DNL Airship]. Par exemple, un détaillant peut créer une audience avec le statut de fidélité et les données de localisation (attributs de Platform) et [!DNL Airship] prévus pour générer des données pour envoyer des messages très ciblés aux utilisateurs ayant le statut de fidélité à l’or qui vivent à Las Vegas, NV, et ont une forte probabilité d’attrition.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Jeton de porteur]** : le jeton de porteur que vous avez généré à partir du tableau de bord [!DNL Airship].

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : saisissez une description pour cette destination.
* **[!UICONTROL Domaine]** : sélectionnez un centre de données des États-Unis ou de l’UE, selon le centre de données [!DNL Airship] qui s’applique à cette destination.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

Les attributs [!DNL Airship] peuvent être définis sur un canal, qui représente une instance de l’appareil, par exemple iPhone, ou un utilisateur nommé, qui mappe tous les appareils d’un utilisateur à un identifiant commun, tel qu’un ID de client. Si votre schéma contient des adresses électroniques en texte brut (non hachées) comme identité principale, sélectionnez le champ d’adresse électronique dans vos **[!UICONTROL attributs Source]** et mappez-le à l’utilisateur [!DNL Airship] nommé dans la colonne de droite sous **[!UICONTROL identités cibles]**, comme illustré ci-dessous.

![Mappage d’utilisateur nommé](../../assets/catalog/mobile-engagement/airship/mapping.png)

Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire un appareil, mappez-les au canal approprié en fonction de la source. Les images suivantes montrent comment deux mappages sont créés :

* IDFA iOS Advertising ID sur un canal iOS [!DNL Airship]
* Adobe de l’attribut `fullName` à l’attribut [!DNL Airship] &quot;Nom complet&quot;

>[!NOTE]
>
>Utilisez le nom convivial qui apparaît dans le tableau de bord [!DNL Airship] lors de la sélection du champ cible pour votre mappage d’attributs.

**Mapper l’identité**

Sélectionner le champ source :

![Se connecter aux attributs des navires](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Sélectionnez le champ cible :

![Se connecter aux attributs des navires](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Attribut de carte**

Sélectionner l’attribut source :

![Sélectionner le champ source](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Sélectionnez l’attribut cible :

![Sélectionner un champ cible](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Vérification du mappage :

![Mapping des canaux](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](../../../data-governance/home.md).
