---
title: Configuration de l’extension de balise du SDK Web
description: Découvrez comment configurer l’extension de balise SDK Web Experience Platform dans l’interface utilisateur des balises.
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 6%

---

# Configuration de l’extension de balise du SDK Web

La variable [!DNL Web SDK] l’extension de balise envoie des données à Adobe Experience Cloud à partir de propriétés web via l’Edge Network Experience Platform.

L’extension vous permet de diffuser des données dans Platform, de synchroniser les identités, de traiter les signaux de consentement du client et de collecter automatiquement des données contextuelles.

Ce document explique comment configurer l’extension de balise dans l’interface utilisateur de balises.

## Installation de l’extension de balise du SDK Web {#install}

Une propriété doit être installée sur l’extension de balise SDK Web. Si vous ne l’avez pas déjà fait, consultez la documentation sur [création d’une propriété de balise](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=fr).

Après avoir créé une propriété, ouvrez-la et sélectionnez l’option **[!UICONTROL Extensions]** de la barre de gauche.

Sélectionnez la variable **[!UICONTROL Catalogue]** . Recherchez le composant [!DNL Web SDK] extension et sélectionner **[!UICONTROL Installer]**.

![Image présentant l’interface utilisateur des balises avec l’extension SDK Web sélectionnée](assets/web-sdk-install.png)

Après avoir sélectionné **[!UICONTROL Installer]**, vous devez configurer l’extension de balise du SDK Web et enregistrer la configuration.

>[!NOTE]
>
>L’extension de balise n’est installée qu’après l’enregistrement de la configuration. Reportez-vous aux sections suivantes pour savoir comment configurer l’extension de balise.

## Configuration des paramètres d’instance {#general}

Les options de configuration en haut de la page indiquent à Adobe Experience Platform où acheminer les données et quelles configurations utiliser sur le serveur.

![Image présentant les paramètres généraux de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-general.png)

* **[!UICONTROL Nom]**: l’extension SDK Web de Adobe Experience Platform prend en charge plusieurs instances sur la page. Le nom est utilisé pour envoyer des données à plusieurs organisations avec une configuration de balise. Le nom de l’instance est défini par défaut sur `alloy`. Vous pouvez toutefois remplacer le nom de l’instance par n’importe quel nom d’objet JavaScript valide.
* **[!UICONTROL Identifiant de l’organisation IMS]**: identifiant de l’organisation à laquelle vous souhaitez envoyer les données dans Adobe. La plupart du temps, utilisez la valeur par défaut qui est renseignée automatiquement. Si la page contient plusieurs instances, renseignez ce champ avec la valeur de la deuxième organisation à laquelle vous souhaitez envoyer des données.
* **[!UICONTROL Domaine Edge]**: domaine à partir duquel l’extension envoie et reçoit des données. Adobe recommande d’utiliser un domaine propriétaire (CNAME) pour cette extension. Le domaine tiers par défaut fonctionne pour les environnements de développement, mais ne convient pas aux environnements de production. Les instructions de configuration d’un CNAME propriétaire sont répertoriées [ici](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=fr).

## Configuration des paramètres du flux de données {#datastreams}

Cette section vous permet de sélectionner les flux de données à utiliser pour chacun des trois environnements disponibles (production, évaluation et développement).

Lorsqu’une demande est envoyée à l’Edge Network, un identifiant de flux de données est utilisé pour référencer la configuration côté serveur. Vous pouvez mettre à jour la configuration sans avoir à apporter de modifications au code sur votre site web.

Consultez le guide sur la [datastreams](../../../../datastreams/overview.md) pour savoir comment configurer un flux de données.

Vous pouvez choisir un flux de données dans les menus déroulants disponibles ou sélectionner **[!UICONTROL Saisir des valeurs]** et saisissez un identifiant de flux de données personnalisé pour chaque environnement.

![Image montrant les paramètres de flux de données de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-datastreams.png)

## Configuration des paramètres de confidentialité {#privacy}

Cette section vous permet de configurer la manière dont le SDK Web traite les signaux de consentement des utilisateurs de votre site Web. Plus précisément, il vous permet de sélectionner le niveau de consentement par défaut supposé d’un utilisateur si aucune autre préférence de consentement explicite n’a été fournie.

Le niveau de consentement par défaut n’est pas enregistré dans le profil utilisateur.

![Image montrant les paramètres de confidentialité de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-privacy.png)

| [!UICONTROL Niveau de consentement par défaut] | Description |
| --- | --- |
| [!UICONTROL Dans] | Collectez les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL Out] | Ignorer les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL En attente] | Événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. Lorsque les préférences de consentement sont fournies, les événements sont collectés ou ignorés en fonction des préférences fournies. |
| [!UICONTROL Fourni par l’élément de données] | Le niveau de consentement par défaut est déterminé par un élément de données distinct que vous définissez. Lorsque vous utilisez cette option, vous devez spécifier l’élément de données à l’aide du menu déroulant fourni. |

>[!TIP]
>
>Utilisation **[!UICONTROL Out]** ou **[!UICONTROL En attente]** si vous avez besoin d’un consentement explicite de l’utilisateur pour vos activités commerciales.

## Configuration des paramètres d’identité {#identity}

Cette section vous permet de définir le comportement du SDK Web lorsqu’il s’agit de gérer l’identification des utilisateurs.

![Image présentant les paramètres d’identité de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-identity.png)

* **[!UICONTROL Migration de l’ECID depuis VisitorAPI]**: cette option est activée par défaut. Lorsque cette fonction est activée, le SDK peut lire la variable `AMCV` et `s_ecid` et définissez la variable `AMCV` cookie utilisé par [!DNL Visitor.js]. Cette fonctionnalité est importante lors de la migration vers le SDK Web, car certaines pages utilisent toujours [!DNL Visitor.js]. Cette option permet au SDK de continuer à utiliser la même [!DNL ECID] afin que les utilisateurs ne soient pas identifiés comme deux utilisateurs distincts.
* **[!UICONTROL Utilisation de cookies tiers]**: lorsque cette option est activée, le SDK Web tente de stocker un identifiant d’utilisateur dans un cookie tiers. En cas de réussite, l’utilisateur est identifié comme un utilisateur unique lorsqu’il navigue sur plusieurs domaines, plutôt que comme un utilisateur distinct sur chaque domaine. Si cette option est activée, le SDK peut toujours ne pas pouvoir stocker l’identifiant de l’utilisateur dans un cookie tiers si le navigateur ne prend pas en charge les cookies tiers ou s’il a été configuré par l’utilisateur pour ne pas autoriser les cookies tiers. Dans ce cas, le SDK stocke uniquement l’identifiant dans le domaine propriétaire.

  >[!IMPORTANT]
  >>Les cookies tiers ne sont pas compatibles avec la variable [identifiant d’appareil propriétaire](../../../../web-sdk/identity/first-party-device-ids.md) dans le SDK Web.
Vous pouvez utiliser des identifiants d’appareil propriétaires ou des cookies tiers, mais vous ne pouvez pas utiliser les deux fonctionnalités simultanément.
  >
## Configuration des paramètres de personnalisation {#personalization}

Cette section vous permet de configurer le mode de masquage de certaines parties d’une page lors du chargement du contenu personnalisé. Cela garantit que vos visiteurs ne voient que la page personnalisée.

![Image montrant les paramètres de personnalisation de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL Migration de Target depuis at.js vers le SDK Web]**: utilisez cette option pour activer [!DNL Web SDK] pour lire et écrire l’héritage `mbox` et `mboxEdgeCluster` cookies utilisés par at.js `1.x` ou `2.x` bibliothèques. Vous pouvez ainsi conserver le profil du visiteur lors du passage d’une page qui utilise le SDK Web à une page qui utilise at.js. `1.x` ou `2.x` et vice versa.

### Style de prémasquage {#prehiding-style}

L’éditeur de style de prémasquage vous permet de définir des règles CSS personnalisées pour masquer des sections spécifiques d’une page. Lorsque la page est chargée, le SDK Web utilise ce style pour masquer les sections à personnaliser, récupère la personnalisation, puis annule le masquage des sections de page personnalisées. Ainsi, vos visiteurs voient les pages déjà personnalisées, sans voir le processus de récupération de personnalisation.

### Prémasquer le fragment de code {#prehiding-snippet}

Le fragment de code de masquage préalable est utile lorsque la bibliothèque SDK Web est chargée de manière asynchrone. Dans ce cas, pour éviter le scintillement, nous vous recommandons de masquer le contenu avant le chargement de la bibliothèque SDK Web.

Pour utiliser le fragment de code de masquage préalable, copiez-le et collez-le dans le `<head>` de votre page.

>[!IMPORTANT]
>
Lors de l’utilisation du fragment de code de masquage préalable, Adobe recommande d’utiliser le même [!DNL CSS] comme celle utilisée par la variable [style de prémasquage](#prehiding-style).

## Configuration des paramètres de collecte de données {#data-collection}

![Image présentant les paramètres de collecte de données de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/web-sdk-ext-collection.png)

* **[!UICONTROL Fonction de rappel]**: la fonction de rappel fournie dans l’extension est également appelée [`onBeforeEventSend` function](/help/web-sdk/commands/configure/onbeforeeventsend.md) dans la bibliothèque. Cette fonction vous permet de modifier les événements de manière globale avant qu’ils ne soient envoyés à l’Edge Network.
* **[!UICONTROL Activer la collecte de données de clic]**: le SDK Web peut automatiquement collecter des informations sur les clics sur les liens. Cette fonctionnalité est activée par défaut, mais elle peut être désactivée à l’aide de cette option. Les liens sont également étiquetés comme liens de téléchargement s’ils contiennent l’une des expressions de téléchargement répertoriées dans la variable [!UICONTROL Télécharger le qualificateur de lien] textbox. Adobe vous fournit quelques qualificateurs de lien de téléchargement par défaut. Vous pouvez les modifier en fonction de vos besoins.
* **[!UICONTROL Données contextuelles collectées automatiquement]**: par défaut, le SDK Web collecte certaines données contextuelles concernant l’appareil, le web, l’environnement et le contexte de lieu. Si vous ne souhaitez pas que ces données soient collectées ou que certaines catégories de données soient uniquement collectées, sélectionnez **[!UICONTROL Informations contextuelles spécifiques]** et sélectionnez les données à collecter. Voir [`context`](/help/web-sdk/commands/configure/context.md) pour plus d’informations.

## Configuration des paramètres de la collection multimédia {#media-collection}

La fonctionnalité de collecte de médias vous aide à collecter des données liées aux sessions multimédia sur votre site web.

Les données collectées peuvent inclure des informations sur les lectures multimédia, les pauses, les fins et d’autres événements connexes. Une fois ces données collectées, vous pouvez les envoyer à Adobe Experience Platform et/ou Adobe Analytics pour générer des rapports. Cette fonctionnalité offre une solution complète pour effectuer le suivi et comprendre le comportement de consommation des médias sur votre site web.

![Image montrant les paramètres de collecte de médias de l’extension de balise SDK Web dans l’interface utilisateur des balises](assets/media-collection.png)


* **[!UICONTROL Canal]**: nom du canal sur lequel se produit la collecte de médias. Exemple : `Video channel`.
* **[!UICONTROL Nom du lecteur]**: nom du lecteur multimédia.
* **[!UICONTROL Version de l’application]**: version de l’application du lecteur multimédia.
* **[!UICONTROL Intervalle de ping principal]**: fréquence des pings pour le contenu principal, en secondes. La valeur par défaut est `10`. Les valeurs peuvent être comprises entre `10` to `50` secondes.  Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de la variable [sessions suivies automatiquement](../../../../web-sdk/commands/createmediasession.md#automatic).
* **[!UICONTROL Intervalle de ping publicitaire]**: fréquence des pings pour le contenu de la publicité, en secondes. La valeur par défaut est `10`. Les valeurs peuvent être comprises entre `1` to `10` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de la variable [sessions suivies automatiquement](../../../../web-sdk/commands/createmediasession.md#automatic)

## Configurer les remplacements de trains de données {#datastream-overrides}

Les remplacements de trains de données vous permettent de définir des configurations supplémentaires pour vos trains de données, qui sont transmises au réseau Edge via le SDK Web.

Vous pouvez ainsi déclencher des comportements de trains de données différents de ceux par défaut, sans créer de train de données ni modifier vos paramètres existants.

Le remplacement de la configuration du train de données comporte deux étapes :

1. Tout d’abord, vous devez définir vos remplacements de configuration de trains de données sur la page de [configuration des trains de données](/help/datastreams/configure.md).
2. Ensuite, vous devez envoyer les remplacements à l’Edge Network soit par le biais d’une commande SDK Web, soit à l’aide de l’extension de balise SDK Web.

Voir la structure de données [la documentation de remplacement de configuration](/help/datastreams/overrides.md) pour obtenir des instructions détaillées sur la façon de remplacer les configurations datastream.

Au lieu de transmettre les remplacements par le biais d’une commande SDK Web, vous pouvez configurer les remplacements dans l’écran d’extension de balise illustré ci-dessous.

>[!IMPORTANT]
>
Les remplacements de flux de données doivent être configurés par environnement. Les environnements de développement, d’évaluation et de production ont tous des remplacements distincts. Vous pouvez copier les paramètres entre eux à l’aide des options dédiées affichées dans l’écran ci-dessous.

![Image montrant le remplacement de la configuration de la banque de données à l’aide de la page de l’extension de balise SDK Web.](assets/datastream-overrides.png)

## Configuration des paramètres avancés

Utilisez la variable **[!UICONTROL Chemin de base Edge]** si vous devez modifier le chemin de base utilisé pour interagir avec l’Edge Network. Cela ne doit pas nécessiter de mise à jour, mais dans le cas où vous participez à une version bêta ou alpha, l’Adobe peut vous demander de modifier ce champ.

![Image présentant les paramètres avancés à l’aide de la page de l’extension de balise SDK Web.](assets/advanced-settings.png)
