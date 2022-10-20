---
title: Présentation De L’Extension Splunk
description: Découvrez l’extension Splunk pour le transfert d’événement dans Adobe Experience Platform.
source-git-commit: cad6d78868ac89be325faa58f567b89869bfff02
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 2%

---

# Présentation de l’extension Splunk

[Splunk](https://www.splunk.com) est une plateforme d’observabilité qui fournit des fonctions de recherche, d’analyse et de visualisation pour obtenir des informations exploitables sur vos données. Le Splunk [transfert d’événement](../../../ui/event-forwarding/overview.md) tire parti de l’extension [API REST du collecteur d’événements HTTP Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) pour envoyer des événements du réseau Adobe Experience Platform Edge au [Collecteur d’événements HTTP Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

Splunk utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec l’API Splunk Event Collector.

## Cas d&#39;utilisation {#use-cases}

Les équipes marketing peuvent utiliser l’extension pour les cas d’utilisation suivants :

| Cas d’utilisation | Description |
| --- | --- |
| Analyse du comportement des clients | Les entreprises peuvent capturer les données d’événement d’interaction client de leur site web et transférer les événements pertinents vers Splunk. Les équipes de marketing et d’analyse peuvent alors effectuer des analyses ultérieures dans la plateforme Splunk afin de comprendre les interactions et les comportements clés des utilisateurs. La plateforme Splunk peut être utilisée pour générer des graphiques, des tableaux de bord ou d’autres visualisations afin d’informer les parties prenantes de l’entreprise. |
| Recherche évolutive sur des jeux de données volumineux | Les entreprises peuvent capturer des entrées transactionnelles ou conversationnelles en tant que données d’événement du site web et transférer des événements vers Splunk. Les équipes d’Analytics peuvent ensuite tirer parti des fonctionnalités d’indexation évolutive de Splunk pour filtrer et traiter les jeux de données volumineux afin d’obtenir des informations sur l’entreprise et de prendre des décisions éclairées. |

{style=&quot;table-layout:auto&quot;}

## Conditions préalables {#prerequisites}

Vous devez disposer d’un compte Splunk pour utiliser cette extension. Vous pouvez vous inscrire à un compte Splunk sur la page [Page d’accueil de Splunk](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> L’extension Splunk prend en charge les instances d’entreprise Splunk Cloud et Splunk. Ce guide documente une mise en oeuvre à l’aide de [Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) comme référence. Le processus de configuration pour [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) est similaire, mais nécessite des conseils spécifiques de votre administrateur Splunk Enterprise.

Pour configurer l’extension, vous devez également disposer des valeurs techniques suivantes :

* Un [Jeton de collecteur d’événements](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). Les jetons sont généralement au format UUIDv4, comme suit : `12345678-1234-1234-1234-1234567890AB`.
* Adresse et port de l’instance de plateforme Splunk pour votre organisation. L’adresse et le port d’une instance de plateforme ont généralement le format suivant : `mysplunkserver.example.com:443`.
   >[!IMPORTANT]
   >
   > Les points de terminaison Splunk référencés dans le transfert d’événement ne doivent utiliser que le port `443`. Les ports non standard ne sont actuellement pas pris en charge dans les implémentations de transfert d’événement.

## Installation de l’extension Splunk {#install}

Pour installer l’extension Splunk Event Collector dans l’interface utilisateur, accédez à **Transfert d’événement** et sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, accédez à **Extensions** > **Catalogue**. Recherchez &quot;[!DNL Splunk]&quot;, puis sélectionnez **[!DNL Install]** sur l’extension Splunk.

![Bouton Installer pour l’extension Splunk sélectionnée dans l’interface utilisateur](../../../images/extensions/splunk/install.png)

## Configuration de l’extension Splunk {#configure_extension}

>[!IMPORTANT]
>
>En fonction des besoins de mise en oeuvre, vous devrez peut-être créer un schéma, des éléments de données et un jeu de données avant de configurer l’extension. Avant de commencer, consultez toutes les étapes de configuration afin de déterminer les entités à configurer pour votre cas d’utilisation.

Sélectionner **Extensions** dans le volet de navigation de gauche. Sous **Installé**, sélectionnez **Configurer** sur l’extension Splunk.

![Bouton Configurer pour l’extension Splunk sélectionnée dans l’interface utilisateur](../../../images/extensions/splunk/configure.png)

Pour **[!UICONTROL URL du collecteur d’événements HTTP]**, saisissez l’adresse et le port de votre instance de plateforme Splunk. Sous **[!UICONTROL Jeton d’accès]**, saisissez votre [!DNL Event Collector Token] . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Options de configuration renseignées dans l’interface utilisateur](../../../images/extensions/splunk/input.png)

## Configuration d’une règle de transfert d’événement {#config_rule}

Commencer à créer une règle de transfert d’événement [règle](../../../ui/managing-resources/rules.md) et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez l’événement [!UICONTROL Splunk] , puis sélectionnez la variable [!UICONTROL Créer un événement] type d’action. D’autres contrôles s’affichent pour configurer davantage l’événement Splunk.

![Définition de la configuration d’une action](../../../images/extensions/splunk/action-configurations.png)

L’étape suivante consiste à mapper les propriétés d’événement Splunk aux éléments de données que vous avez précédemment créés. Les mappages facultatifs pris en charge en fonction des données d’événement d’entrée pouvant être configurés sont présentés ci-dessous. Reportez-vous à la section [Documentation Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) pour plus de détails.

| Nom du champ | Description |
| --- | --- |
| [!UICONTROL Événement ]<br><br>**(OBLIGATOIRE)** | Indiquez comment vous souhaitez fournir les données d’événement. Les données d’événement peuvent être affectées à la variable `event` clé dans l’objet JSON dans la requête HTTP ou il peut s’agir de texte brut. Le `event` se trouve au même niveau dans le paquet d’événement JSON que les clés de métadonnées. Dans le `event` accolades clé-valeur, les données peuvent se trouver sous n’importe quel formulaire (chaîne, nombre, autre objet JSON, etc.). |
| [!UICONTROL Hôte] | Nom d’hôte du client à partir duquel vous envoyez des données. |
| [!UICONTROL Type de source] | Type de source à affecter aux données d’événement. |
| [!UICONTROL Source] | La valeur source à affecter aux données d’événement. Par exemple, si vous envoyez des données à partir d’une application que vous développez, définissez cette clé sur le nom de l’application. |
| [!UICONTROL Index] | Nom de l’index des données d’événement. L’index que vous spécifiez ici doit se trouver dans la liste des index autorisés si le paramètre index est défini pour le jeton. |
| [!UICONTROL Heure] | Heure de l’événement. Le format d’heure par défaut est UNIX (au format `<sec>.<ms>`) et dépend du fuseau horaire local. Par exemple : `1433188255.500` indique 1433188255 secondes et 500 millisecondes après l’époque, ou lundi 1er juin 2015 à 7:50:17 h GMT. |
| [!UICONTROL Champs] | Spécifiez un objet JSON brut ou un ensemble de paires clé-valeur contenant des champs personnalisés explicites à définir au moment de l’index.  Le `fields` ne s’applique pas aux données brutes.<br><br>Requêtes contenant les `fields` doit être envoyée à la propriété `/collector/event` point de terminaison , sinon ils ne seront pas indexés. Pour plus d’informations, voir la documentation Splunk sur [extraction de champs indexés](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### Validation des données dans Splunk {#validate}

Après avoir créé et exécuté la règle de transfert d’événement, vérifiez si l’événement envoyé à l’API Splunk s’affiche comme prévu dans l’interface utilisateur de Splunk. Si la collecte d’événements et l’intégration de l’Experience Platform ont réussi, des événements s’affichent dans la console Splunk comme suit :

![Données d’événement apparaissant dans l’interface utilisateur Splunk lors de la validation](../../../images/extensions/splunk/splunk-data.png)

## Étapes suivantes

Ce document explique comment installer et configurer l’extension de transfert d’événement Splunk dans l’interface utilisateur. Pour plus d’informations sur la collecte de données d’événement dans Splunk, consultez la documentation officielle :

* [Configuration et utilisation du collecteur d’événements HTTP dans Splunk Web ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [Configuration de l’authentification avec des jetons](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [Dépannage du collecteur d’événements HTTP](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (répertorie également un compendium de [codes d’erreur possibles](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
