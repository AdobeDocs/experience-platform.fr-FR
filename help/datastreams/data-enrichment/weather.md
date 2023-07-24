---
title: Utilisation des données météorologiques de DNL Le canal météorologique
description: Utilisez les données météorologiques du DNL Weather Channel pour améliorer les données que vous collectez par le biais des flux de données.
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 4c9abcefb279c6e8a90744b692d86746a4896d0a
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 4%

---

# Utiliser les données météorologiques de [!DNL The Weather Channel]

Adobe s’est associé à [!DNL [The Weather Company]](https://www.ibm.com/weather) afin d’apporter le contexte supplémentaire de la météo des États-Unis aux données collectées via les flux de données. Vous pouvez utiliser ces données pour les analyses, le ciblage et la création de segments dans Experience Platform.

Il existe trois types de données disponibles à partir de [!DNL The Weather Channel]:

* **[!UICONTROL Météo actuelle]**: Conditions météorologiques actuelles de l’utilisateur, selon sa localisation. Il s’agit notamment de la température actuelle, de la fréquentation, de la couverture du cloud, etc.
* **[!UICONTROL Météo prévue]**: La prévision comprend les prévisions de 1, 2, 3, 5, 7 et 10 jours pour l’emplacement de l’utilisateur.
* **[!UICONTROL Triggers]**: Les déclencheurs sont des combinaisons spécifiques qui correspondent à différentes conditions météorologiques sémantiques. Il existe trois types de déclencheurs météorologiques différents :

   * **[!UICONTROL Déclencheurs météo]**: Des conditions sémantiquement significatives, comme le temps froid ou pluvieux. Il peut y avoir des différences dans leurs définitions entre les différents climats.
   * **[!UICONTROL Déclencheurs de produits]**: Conditions qui conduiraient à l’achat de différents types de produits. Par exemple : les prévisions météorologiques froides pourraient signifier que les achats de manteaux de pluie sont plus probables.
   * **[!UICONTROL Déclencheurs météorologiques graves]**: Des avertissements météorologiques graves, comme des avertissements d&#39;ouragan ou d&#39;tempête d&#39;hiver.

## Conditions préalables {#prerequisites}

Avant d’utiliser les données météorologiques, assurez-vous de respecter les conditions préalables suivantes :

* Vous devez acquérir sous licence les données météorologiques que vous utiliserez, à partir de [!DNL The Weather Channel]. Il l’activera alors sur votre compte.
* Les données météorologiques ne sont disponibles que par le biais de flux de données. Pour utiliser les données météorologiques, vous devez utiliser [!DNL Web SDK], [!DNL Mobile Edge Extension] ou le [API du serveur](../../server-api/overview.md) pour exploiter ces données.
* Votre flux de données doit comporter [[!UICONTROL Emplacement géographique]](../configure.md#advanced-options) activée.
* Ajoutez la variable [groupe de champs météo](#schema-configuration) au schéma que vous utilisez.

## Configuration {#provisioning}

Une fois que vous avez autorisé les données de [!DNL The Weather Channel], votre compte pourra alors accéder aux données. Ensuite, vous devez contacter le service à la clientèle pour Adobe l’activation des données dans votre flux de données. Une fois activées, les données sont automatiquement ajoutées.

Vous pouvez vérifier qu’il est ajouté en exécutant une trace de périphérie avec le débogueur ou en utilisant Assurance pour suivre un accès via la variable [!DNL Edge Network].

### Configuration du schéma {#schema-configuration}

Vous devez ajouter les groupes de champs météorologiques à votre schéma Experience Platform correspondant au jeu de données d’événement que vous utilisez dans votre flux de données. Cinq groupes de champs sont disponibles :

* [!UICONTROL Prévisions météo]
* [!UICONTROL Météo actuelle]
* [!UICONTROL Déclencheurs de produits]
* [!UICONTROL Déclencheurs relatifs]
* [!UICONTROL Déclencheurs météorologiques graves]

## Accès aux données météorologiques {#access-weather-data}

Une fois vos données sous licence et disponibles, vous pouvez y accéder de différentes manières dans l’ensemble des services Adobe.

### Adobe Analytics {#analytics}

Dans [!DNL Adobe Analytics], les données météorologiques peuvent être mappées par le biais de règles de traitement, avec le reste de vos [!DNL XDM] schéma.

Vous trouverez la liste des champs que vous pouvez mapper dans le [référence météo](weather-reference.md) page. Comme pour tout [!DNL XDM] schémas, les clés sont précédées du préfixe `a.x`. Par exemple, un champ nommé `weather.current.temperature.farenheit` s’afficherait dans [!DNL Analytics] as `a.x.weather.current.temperature.farenheit`.

![Interface des règles de traitement](../assets/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

Dans [!DNL Adobe Customer Journey Analytics], les données météorologiques sont disponibles dans le jeu de données spécifié dans la banque de données. Tant que les attributs météorologiques sont [ajouté à votre schéma ;](#prerequisites-prerequisites), ils seront disponibles pour [ajouter à une vue de données](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=fr) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

Les données météorologiques sont disponibles dans la variable [Real-time Customer Data Platform](../../rtcdp/overview.md), à utiliser dans les segments. Les données météorologiques sont associées aux événements.

![Créateur de segments affichant les événements météo](../assets/data-enrichment/weather/schema-builder.png)

Comme les conditions météorologiques changent souvent, Adobe vous recommande de définir des contraintes de temps sur les segments, comme illustré dans l’exemple ci-dessus. Avoir une journée froide dans le dernier jour ou deux est beaucoup plus important qu&#39;avoir une journée froide il y a 6 mois.

Voir [référence météo](weather-reference.md) pour les champs disponibles.

### Adobe Target {#target}

Dans [!DNL Adobe Target], vous pouvez utiliser les données météorologiques pour générer de la personnalisation en temps réel. Les données météorologiques sont transmises à [!DNL Target] as [!UICONTROL mBox] et vous pouvez y accéder via un [!UICONTROL mBox] .

![Target Audience Builder](../assets/data-enrichment/weather/target-audience-builder.png)

Le paramètre est la valeur [!DNL XDM] chemin d’accès à un champ spécifique. Voir [référence météo](weather-reference.md) pour les champs disponibles et leurs chemins d’accès correspondants.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous comprenez mieux comment utiliser les données météorologiques dans différentes solutions d’Adobe. Pour en savoir plus sur le mappage des champs de données météorologiques, voir [référence de mappage de champs](weather-reference.md).
