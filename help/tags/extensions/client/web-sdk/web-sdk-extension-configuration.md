---
title: Configuration de l’extension de balise du SDK Web
description: Découvrez comment configurer l’extension de balise SDK Web Experience Platform dans l’interface utilisateur des balises.
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: f2f61c8e68fa794317e3b4f845f1950cebc59ec7
workflow-type: tm+mt
source-wordcount: '2525'
ht-degree: 4%

---

# Configuration de l’extension de balise du SDK Web

L’extension de balise [!DNL Web SDK] envoie des données à Adobe Experience Cloud à partir de propriétés web via l’Edge Network Experience Platform.

L’extension vous permet de diffuser des données dans Platform, de synchroniser les identités, de traiter les signaux de consentement du client et de collecter automatiquement des données contextuelles.

Ce document explique comment configurer l’extension de balise dans l’interface utilisateur de balises.

## Installation de l’extension de balise du SDK Web {#install}

Une propriété doit être installée sur l’extension de balise SDK Web. Si vous ne l’avez pas déjà fait, consultez la documentation sur la [création d’une propriété de balise](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=fr).

Après avoir créé une propriété, ouvrez-la et sélectionnez l’onglet **[!UICONTROL Extensions]** sur la barre de gauche.

Sélectionnez l’onglet **[!UICONTROL Catalogue]** . Dans la liste des extensions disponibles, recherchez l’extension [!DNL Web SDK] et sélectionnez **[!UICONTROL Install]**.

![Image présentant l’interface utilisateur des balises avec l’extension SDK Web sélectionnée](assets/web-sdk-install.png)

Après avoir sélectionné **[!UICONTROL Install]**, vous devez configurer l’extension de balise du SDK Web et enregistrer la configuration.

>[!NOTE]
>
>L’extension de balise n’est installée qu’après l’enregistrement de la configuration. Reportez-vous aux sections suivantes pour savoir comment configurer l’extension de balise.

## Configuration des paramètres d’instance {#general}

Les options de configuration en haut de la page indiquent à Adobe Experience Platform où acheminer les données et quelles configurations utiliser sur le serveur.

![Image présentant les paramètres généraux de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-general.png)

* **[!UICONTROL Nom]** : l’extension SDK Web de Adobe Experience Platform prend en charge plusieurs instances sur la page. Le nom est utilisé pour envoyer des données à plusieurs organisations avec une configuration de balise. Par défaut, le nom de l’instance est `alloy`. Vous pouvez toutefois remplacer le nom de l’instance par n’importe quel nom d’objet JavaScript valide.
* **[!UICONTROL Identifiant de l’organisation IMS]** : identifiant de l’organisation à laquelle vous souhaitez envoyer les données à l’Adobe. La plupart du temps, utilisez la valeur par défaut qui est renseignée automatiquement. Si la page contient plusieurs instances, renseignez ce champ avec la valeur de la deuxième organisation à laquelle vous souhaitez envoyer des données.
* **[!UICONTROL Domaine Edge]** : domaine à partir duquel l’extension envoie et reçoit des données. Adobe recommande d’utiliser un domaine propriétaire (CNAME) pour cette extension. Le domaine tiers par défaut fonctionne pour les environnements de développement, mais ne convient pas aux environnements de production. Les instructions de configuration d’un CNAME propriétaire sont répertoriées [ici](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=fr).

## Configuration des paramètres du flux de données {#datastreams}

Cette section vous permet de sélectionner les flux de données à utiliser pour chacun des trois environnements disponibles (production, évaluation et développement).

Lorsqu’une demande est envoyée à l’Edge Network, un identifiant de flux de données est utilisé pour référencer la configuration côté serveur. Vous pouvez mettre à jour la configuration sans avoir à apporter de modifications au code sur votre site web.

Consultez le guide sur [datastreams](../../../../datastreams/overview.md) pour savoir comment configurer un flux de données.

Vous pouvez choisir un flux de données dans les menus déroulants disponibles ou sélectionner **[!UICONTROL Entrer les valeurs]** et saisir un identifiant de flux de données personnalisé pour chaque environnement.

![Image montrant les paramètres de la branche de données de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-datastreams.png)

## Configuration des paramètres de confidentialité {#privacy}

Cette section vous permet de configurer la manière dont le SDK Web traite les signaux de consentement des utilisateurs de votre site Web. Plus précisément, il vous permet de sélectionner le niveau de consentement par défaut supposé d’un utilisateur si aucune autre préférence de consentement explicite n’a été fournie.

Le niveau de consentement par défaut n’est pas enregistré dans le profil utilisateur.

![Image montrant les paramètres de confidentialité de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-privacy.png)

| [!UICONTROL Niveau de consentement par défaut] | Description |
| --- | --- |
| [!UICONTROL In] | Collectez les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL Out] | Ignorer les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL En attente] | Événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. Lorsque les préférences de consentement sont fournies, les événements sont collectés ou ignorés en fonction des préférences fournies. |
| [!UICONTROL Fourni par l’élément de données] | Le niveau de consentement par défaut est déterminé par un élément de données distinct que vous définissez. Lorsque vous utilisez cette option, vous devez spécifier l’élément de données à l’aide du menu déroulant fourni. |

>[!TIP]
>
>Utilisez **[!UICONTROL Out]** ou **[!UICONTROL Pending]** si vous avez besoin du consentement explicite de l’utilisateur pour vos activités commerciales.

## Configuration des paramètres d’identité {#identity}

Cette section vous permet de définir le comportement du SDK Web lorsqu’il s’agit de gérer l’identification des utilisateurs.

![Image montrant les paramètres d’identité de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-identity.png)

* **[!UICONTROL Migrer l’ECID depuis VisitorAPI]** : cette option est activée par défaut. Lorsque cette fonction est activée, le SDK peut lire les cookies `AMCV` et `s_ecid` et définir le cookie `AMCV` utilisé par [!DNL Visitor.js]. Cette fonctionnalité est importante lors de la migration vers le SDK Web, car certaines pages utilisent toujours [!DNL Visitor.js]. Cette option permet au SDK de continuer à utiliser le même [!DNL ECID] afin que les utilisateurs ne soient pas identifiés comme deux utilisateurs distincts.
* **[!UICONTROL Utiliser des cookies tiers]** : lorsque cette option est activée, le SDK Web tente de stocker un identifiant d’utilisateur dans un cookie tiers. En cas de réussite, l’utilisateur est identifié comme un utilisateur unique lorsqu’il navigue sur plusieurs domaines, plutôt que comme un utilisateur distinct sur chaque domaine. Si cette option est activée, le SDK peut toujours ne pas pouvoir stocker l’identifiant de l’utilisateur dans un cookie tiers si le navigateur ne prend pas en charge les cookies tiers ou s’il a été configuré par l’utilisateur pour ne pas autoriser les cookies tiers. Dans ce cas, le SDK stocke uniquement l’identifiant dans le domaine propriétaire.

  >[!IMPORTANT]
  >>Les cookies tiers ne sont pas compatibles avec la fonctionnalité [ d’identifiant d’appareil propriétaire](../../../../web-sdk/identity/first-party-device-ids.md) du SDK Web.
Vous pouvez utiliser des identifiants d’appareil propriétaires ou des cookies tiers, mais vous ne pouvez pas utiliser les deux fonctionnalités simultanément.
  >
## Configuration des paramètres de personnalisation {#personalization}

Cette section vous permet de configurer le mode de masquage de certaines parties d’une page lors du chargement du contenu personnalisé. Cela garantit que vos visiteurs ne voient que la page personnalisée.

![Image montrant les paramètres de personnalisation de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL Migrer Target d’at.js vers le SDK Web]** : utilisez cette option pour permettre à [!DNL Web SDK] de lire et d’écrire les cookies `mbox` et `mboxEdgeCluster` hérités utilisés par les bibliothèques at.js `1.x` ou `2.x`. Vous pouvez ainsi conserver le profil du visiteur lors du passage d’une page qui utilise le SDK Web à une page qui utilise les bibliothèques at.js `1.x` ou `2.x` et vice versa.

### Style de prémasquage {#prehiding-style}

L’éditeur de style de prémasquage vous permet de définir des règles CSS personnalisées pour masquer des sections spécifiques d’une page. Lorsque la page est chargée, le SDK Web utilise ce style pour masquer les sections à personnaliser, récupère la personnalisation, puis annule le masquage des sections de page personnalisées. Ainsi, vos visiteurs voient les pages déjà personnalisées, sans voir le processus de récupération de personnalisation.

### Prémasquer le fragment de code {#prehiding-snippet}

Le fragment de code de masquage préalable est utile lorsque la bibliothèque SDK Web est chargée de manière asynchrone. Dans ce cas, pour éviter le scintillement, nous vous recommandons de masquer le contenu avant le chargement de la bibliothèque SDK Web.

Pour utiliser le fragment de code de masquage préalable, copiez-le et collez-le dans l’élément `<head>` de votre page.

>[!IMPORTANT]
>
Lors de l’utilisation du fragment de code de masquage préalable, Adobe recommande d’utiliser la même règle [!DNL CSS] que celle utilisée par le [style de masquage préalable](#prehiding-style).

## Configuration des paramètres de collecte de données {#data-collection}

Gérer les paramètres de configuration de la collecte de données. Des paramètres similaires dans la bibliothèque JavaScript sont disponibles à l’aide de la commande [`configure`](/help/web-sdk/commands/configure/overview.md).

![Image présentant les paramètres de collecte de données de l’extension de balise du SDK Web dans l’interface utilisateur des balises.](assets/web-sdk-ext-collection.png)

* **[!UICONTROL Activé avant le rappel d’envoi d’événement]** : fonction de rappel permettant d’évaluer et de modifier la charge utile envoyée à Adobe. Utilisez la variable `content` dans la fonction de rappel pour modifier la charge utile. Ce rappel est la balise équivalente à [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) dans la bibliothèque JavaScript.
* **[!UICONTROL Collecter les clics sur les liens internes]** : une case à cocher qui permet la collecte des données de suivi des liens internes à votre site ou propriété. Lorsque vous activez cette case à cocher, les options de regroupement d’événements s’affichent :
   * **[!UICONTROL Aucun regroupement d’événements]** : les données de suivi des liens sont envoyées à l’Adobe dans des événements distincts. Les clics sur les liens envoyés dans des événements distincts peuvent augmenter l’utilisation contractuelle des données envoyées à Adobe Experience Platform.
   * **[!UICONTROL Groupement d’événements à l’aide de l’enregistrement de session]** : stockez les données de suivi des liens dans l’enregistrement de session jusqu’à l’événement de page suivant. Sur la page suivante, les données de suivi des liens stockées et les données de pages vues sont envoyées à Adobe en même temps. Adobe recommande d’activer ce paramètre lors du suivi des liens internes.
   * **[!UICONTROL Groupement d’événements à l’aide de l’objet local]** : stockez les données de suivi des liens dans un objet local jusqu’à l’événement de page suivant. Si un visiteur accède à une nouvelle page, les données de suivi des liens sont perdues. Ce paramètre est plus bénéfique dans le contexte des applications d’une seule page.
* **[!UICONTROL Collecter les clics sur les liens externes]** : une case à cocher qui permet la collecte de liens externes.
* **[!UICONTROL Collecter les clics sur les liens de téléchargement]** : une case à cocher qui active la collecte des liens de téléchargement.
* **[!UICONTROL Qualificateur de lien de téléchargement]** : expression régulière qui qualifie une URL de lien en tant que lien de téléchargement.
* **[!UICONTROL Propriétés de clic de filtre]** : fonction de rappel permettant d’évaluer et de modifier les propriétés liées aux clics avant la collection. Cette fonction s’exécute avant le rappel [!UICONTROL On avant l’envoi d’événement].
* **Paramètres contextuels** : collecte automatiquement les informations sur les visiteurs, ce qui renseigne des champs XDM spécifiques pour vous. Vous pouvez choisir **[!UICONTROL Toutes les informations contextuelles par défaut]** ou **[!UICONTROL Informations contextuelles spécifiques]**. Il s’agit de la balise équivalente à [`context`](/help/web-sdk/commands/configure/context.md) dans la bibliothèque JavaScript.
   * **[!UICONTROL Web]** : collecte des informations sur la page active.
   * **[!UICONTROL Appareil]** : collecte des informations sur l’appareil de l’utilisateur.
   * **[!UICONTROL Environnement]** : collecte des informations sur le navigateur de l’utilisateur.
   * **[!UICONTROL Placer le contexte]** : collecte des informations sur l’emplacement de l’utilisateur.
   * **[!UICONTROL Conseils de l’agent utilisateur à forte entropie]** : collecte des informations plus détaillées sur l’appareil de l’utilisateur.

>[!TIP]
>
Le champ **[!UICONTROL Avant le clic sur les liens envoyer]** est un rappel obsolète qui n’est visible que pour les propriétés qui l’ont déjà configuré. Il s’agit de la balise équivalente à [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) dans la bibliothèque JavaScript. Utilisez le rappel **[!UICONTROL Filtrer les propriétés de clic]** pour filtrer ou ajuster les données de clic, ou utilisez le **[!UICONTROL rappel d’envoi d’événement]** pour filtrer ou ajuster la charge utile globale envoyée à Adobe. Si le rappel **[!UICONTROL Filter click properties]** et le rappel **[!UICONTROL On before link send]** sont définis tous les deux, seul le rappel **[!UICONTROL Filter click properties]** s’exécute.

## Configuration des paramètres de la collection multimédia {#media-collection}

La fonctionnalité de collecte de médias vous aide à collecter des données liées aux sessions multimédia sur votre site web.

Les données collectées peuvent inclure des informations sur les lectures multimédia, les pauses, les fins et d’autres événements connexes. Une fois ces données collectées, vous pouvez les envoyer à Adobe Experience Platform et/ou Adobe Analytics pour générer des rapports. Cette fonctionnalité offre une solution complète pour effectuer le suivi et comprendre le comportement de consommation des médias sur votre site web.

![ Image montrant les paramètres de collecte des médias de l’extension de balise SDK Web dans l’interface utilisateur des balises ](assets/media-collection.png)


* **[!UICONTROL Canal]** : nom du canal sur lequel se produit la collecte de médias. Exemple : `Video channel`.
* **[!UICONTROL Nom du lecteur]** : nom du lecteur multimédia.
* **[!UICONTROL Version de l’application]** : version de l’application du lecteur multimédia.
* **[!UICONTROL Intervalle de ping principal]** : fréquence des pings pour le contenu principal, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `10` à `50` secondes.  Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](../../../../web-sdk/commands/createmediasession.md#automatic).
* **[!UICONTROL Intervalle de ping de publicité]** : fréquence des pings pour le contenu de la publicité, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `1` à `10` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](../../../../web-sdk/commands/createmediasession.md#automatic)

## Configurer les remplacements de trains de données {#datastream-overrides}

Les remplacements de trains de données vous permettent de définir des configurations supplémentaires pour vos trains de données, qui sont transmises au réseau Edge via le SDK Web.

Vous pouvez ainsi déclencher des comportements de trains de données différents de ceux par défaut, sans créer de train de données ni modifier vos paramètres existants.

Le remplacement de la configuration du train de données comporte deux étapes :

1. Tout d’abord, vous devez définir vos remplacements de configuration de trains de données sur la page de [configuration des trains de données](/help/datastreams/configure.md).
2. Ensuite, vous devez envoyer les remplacements à l’Edge Network soit par le biais d’une commande SDK Web, soit à l’aide de l’extension de balise SDK Web.

Pour obtenir des instructions détaillées sur la façon de remplacer les configurations du flux de données, reportez-vous à la documentation [sur le remplacement de la documentation](/help/datastreams/overrides.md).

Au lieu de transmettre les remplacements par le biais d’une commande SDK Web, vous pouvez configurer les remplacements dans l’écran d’extension de balise illustré ci-dessous.

>[!IMPORTANT]
>
Les remplacements de flux de données doivent être configurés par environnement. Les environnements de développement, d’évaluation et de production ont tous des remplacements distincts. Vous pouvez copier les paramètres entre eux à l’aide des options dédiées affichées dans l’écran ci-dessous.

![Image montrant le remplacement de la configuration du flux de données à l’aide de la page d’extension de balise du SDK Web.](assets/datastream-overrides.png)

Par défaut, le remplacement de la configuration du flux de données est désactivé. L’option **[!UICONTROL Correspondance de la configuration de la banque de données]** est sélectionnée par défaut.

![ L’interface utilisateur de l’extension de balise SDK Web présentant la configuration de la chaîne de données remplace le paramètre par défaut.](assets/datastream-override-default.png)

Pour activer les remplacements de flux de données dans l’extension de balise, sélectionnez **[!UICONTROL Enabled]** dans le menu déroulant.

![ L’interface utilisateur de l’extension de balise SDK Web affiche la configuration du flux de données remplace le paramètre Activé.](assets/datastream-override-enabled.png)

Une fois que vous avez activé les remplacements de configuration du flux de données, vous pouvez configurer les remplacements pour chaque service décrit ci-dessous.

Les paramètres de remplacement de la banque de données ci-dessous remplacent toutes les configurations et règles de flux de données côté serveur pour l’environnement sélectionné.

### Adobe Analytics {#analytics}

Utilisez les paramètres de cette section pour remplacer le routage des données vers le service Adobe Analytics.

![Image de l’interface utilisateur de l’extension de balise SDK Web montrant les paramètres de remplacement de la banque de données Adobe Analytics.](assets/datastream-override-analytics.png)

* **[!UICONTROL Activé]** / **[!UICONTROL Désactivé]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service Adobe Analytics.
* **[!UICONTROL Suites de rapports]** : identifiants des suites de rapports de destination dans Adobe Analytics. La valeur doit être une suite de rapports de remplacement préconfigurée (ou une liste de suites de rapports séparées par des virgules) de votre configuration de flux de données. Ce paramètre remplace les suites de rapports principales.
* **[!UICONTROL Ajouter une suite de rapports]** : sélectionnez cette option pour ajouter d’autres suites de rapports.

### Adobe Audience Manager {#audience-manager}

Utilisez les paramètres de cette section pour remplacer le routage des données vers le service Adobe Audience Manager.

![Image de l’interface utilisateur de l’extension de balise SDK Web montrant les paramètres de remplacement de la banque de données Adobe Audience Manager.](assets/datastream-override-audience-manager.png)

* **[!UICONTROL Activé]** / **[!UICONTROL Désactivé]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service Adobe Audience Manager.
* **[!UICONTROL Conteneur de synchronisation des identifiants tiers]** : identifiant du conteneur de synchronisation des identifiants tiers de destination dans Audience Manager. La valeur doit être un conteneur secondaire préconfiguré de votre configuration de flux de données et remplace le conteneur principal.

### Adobe Experience Platform {#experience-platform}

Utilisez les paramètres de cette section pour remplacer le routage des données vers le service Adobe Experience Platform.

![Image de l’interface utilisateur de l’extension de balise SDK Web montrant les paramètres de remplacement de la banque de données Adobe Experience Platform.](assets/datastream-override-experience-platform.png)

* **[!UICONTROL Activé]** / **[!UICONTROL Désactivé]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service Adobe Experience Platform.
* **[!UICONTROL Jeu de données d’événement]** : identifiant du jeu de données d’événement de destination dans Adobe Experience Platform. La valeur doit être un jeu de données secondaire préconfiguré de votre configuration de flux de données.
* **[!UICONTROL Offer decisioning]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service [!DNL Offer Decisioning].
* **[!UICONTROL Segmentation Edge]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service [!DNL Edge Segmentation].
* **[!UICONTROL Destinations Personalization]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers les destinations de personnalisation.
* **[!UICONTROL Adobe Journey Optimizer]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service [!DNL Adobe Journey Optimizer].

### Transfert des événements côté serveur d’Adobe {#ssf}

Utilisez les paramètres de cette section pour remplacer le routage des données par le service de transfert des événements côté serveur Adobe.

![Image de l’interface utilisateur de l’extension de balise SDK Web montrant les paramètres de remplacement de la bande de données de transfert d’événement côté serveur Adobe.](assets/datastream-override-ssf.png)

* **[!UICONTROL Activé]** / **[!UICONTROL Désactivé]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service de transfert des événements côté serveur Adobe.

### Adobe Target {#target}

Utilisez les paramètres de cette section pour remplacer le routage des données vers le service Adobe Target.

![Image de l’interface utilisateur de l’extension de balise SDK Web montrant les paramètres de remplacement de la banque de données Adobe Target.](assets/datastream-override-target.png)

* **[!UICONTROL Activé]** / **[!UICONTROL Désactivé]** : utilisez ce menu déroulant pour activer ou désactiver le routage des données vers le service Adobe Target.

## Configuration des paramètres avancés

Utilisez le champ **[!UICONTROL Chemin d’accès de base Edge]** si vous devez modifier le chemin de base utilisé pour interagir avec l’Edge Network. Cela ne doit pas nécessiter de mise à jour, mais dans le cas où vous participez à une version bêta ou alpha, l’Adobe peut vous demander de modifier ce champ.

![Image présentant les paramètres avancés à l&#39;aide de la page d&#39;extension de balise du SDK Web.](assets/advanced-settings.png)
