---
keywords: Experience Platform;accueil;rubriques populaires;service d’identité;service d’identité;appareils partagés;appareils partagés
solution: Experience Platform
title: Présentation des périphériques partagés (bêta)
topic-legacy: tutorial
description: La détection des appareils partagés identifie les différents utilisateurs authentifiés du même appareil, ce qui permet une représentation plus précise des données client dans les graphiques d’identités.
hide: true
hidefromtoc: true
source-git-commit: 9c0d360b39bf69a44ac6298724dbab0f8456dc90
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 8%

---

# Présentation de la détection des périphériques partagés (bêta)

>[!IMPORTANT]
>
>La fonction [!DNL Shared Device Detection] est en version bêta. Ses fonctionnalités et sa documentation peuvent faire l’objet de modifications.

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

[!DNL Shared Device] fait référence aux appareils utilisés par plusieurs individus. Les tablettes, les ordinateurs de bibliothèque et les kiosques sont des exemples d’appareils partagés. Grâce à la fonction [!DNL Shared Device Detection], il est possible d’empêcher la fusion de différents utilisateurs d’un même appareil en une seule identité, ce qui permet une représentation plus précise.

Avec [!DNL Shared Device Detection] vous pouvez :

* créer des graphiques d’identités distincts pour différents utilisateurs d’un même appareil ;
* empêcher le mélange de données provenant de différentes personnes utilisant le même appareil ;
* Générer une vue plus propre et plus précise de vos clients.

>[!TIP]
>
>Les configurations de [!DNL Shared Device Detection] doivent être terminées avant d’activer [!DNL Profile] pour le jeu de données, car vous ne pouvez plus modifier les paramètres, une fois les graphiques générés dans [!DNL Identity Service].

## Prise en main

L’utilisation de [!DNL Shared Device Detection] nécessite une compréhension des différents services Platform impliqués. Avant de commencer à travailler avec [!DNL Shared Device Detection], veuillez consulter la documentation relative aux services suivants :

* [[!DNL Identity Service]](../home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
   * [Visionneuse de graphique d’identités](./identity-graph-viewer.md) : Visualisez et interagissez avec la visionneuse de graphiques d’identités pour mieux comprendre comment les identités client sont regroupées et de quelles façons.
   * [Espaces de noms d’identité](../namespaces.md) : Découvrez les composants d’une identité complète et comment les espaces de noms d’identité vous permettent de distinguer le contexte et le type d’identité.

### Terminologie

Le tableau suivant contient la liste des termes essentiels à la compréhension de [!DNL Shared Device Detection] :

| Termes | Définition |
| --- | --- |
| Appareil partagé | Un appareil partagé est un appareil utilisé par plusieurs individus. Les tablettes, les ordinateurs de bibliothèque et les kiosques sont des exemples de périphériques partagés. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] fait référence à un paramètre de configuration qui permet aux données de différents utilisateurs d’un même appareil d’être séparées les unes des autres. |
| [!UICONTROL Espace de noms d’identité partagée] | Un [!UICONTROL espace de noms d’identité partagée] est utilisé pour représenter un seul appareil partagé par plusieurs utilisateurs différents. |
| [!UICONTROL Espace de noms d’identité utilisateur] | Un [!UICONTROL espace de noms d’identité utilisateur] est utilisé pour représenter l’utilisateur authentifié ou connecté d’un appareil partagé. |

## Interface utilisateur des périphériques partagés

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis **[!UICONTROL Paramètres d’identité]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

La page [!UICONTROL Paramètres d’appareil partagé] s’affiche, vous fournissant une interface pour configurer les paramètres d’appareil partagé pour vos données. Les paramètres des appareils partagés sont désactivés par défaut.

Lorsqu’ils sont activés, les paramètres d’appareil partagés permettent de séparer les données de différents utilisateurs d’un même appareil les uns des autres. Ce paramètre de configuration permet une représentation plus précise et plus précise des graphiques d’identités, où les identités utilisateur du même appareil ne sont pas combinées.

Sélectionnez **[!UICONTROL Activer]** pour commencer à modifier les paramètres de votre appareil partagé.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

Les options de configuration [!UICONTROL Espace de noms d’identité partagé] et [!UICONTROL Espace de noms d’identité utilisateur] s’affichent, ce qui vous permet de modifier les espaces de noms d’identité que vous souhaitez utiliser.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Shared Identity ] Namespace représente un appareil unique utilisé par plusieurs utilisateurs différents. Cet espace de noms est toujours défini sur **[!UICONTROL ECID]**, car tous les utilisateurs de Platform utilisent **[!UICONTROL ECID]** comme identifiant du navigateur web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

L’ [!UICONTROL espace de noms d’identité utilisateur] vous permet d’identifier différents utilisateurs du même appareil et d’empêcher la combinaison des données dans le même graphique d’identités.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Sélectionnez la barre de recherche **[!UICONTROL Espace de noms d’identité utilisateur]** et saisissez un espace de noms d’identité ou sélectionnez un espace de noms d’identité dans le menu déroulant.

>[!TIP]
>
>L’ [!UICONTROL espace de noms d’identité utilisateur] doit être mappé à l’espace de noms d’identité qui correspond à l’identifiant de connexion de l’utilisateur final. Les options incluent l’ID de client, le courrier électronique et le courrier électronique haché.

![emails](../images/shared-device/emails.png)

Une fois que vous avez configuré vos [!UICONTROL paramètres de périphérique partagé], sélectionnez **[!UICONTROL Enregistrer]**.

![save](../images/shared-device/save.png)

Une fenêtre contextuelle s’affiche, vous invitant à confirmer votre sélection. Sélectionnez **[!UICONTROL Oui]** pour terminer le paramètre de configuration.

![confirm](../images/shared-device/confirm.png)
