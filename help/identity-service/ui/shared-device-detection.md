---
keywords: Experience Platform;accueil;rubriques populaires;service d’identité;service d’identité;appareils partagés;appareils partagés
title: Présentation des périphériques partagés (bêta)
description: La détection des appareils partagés identifie les différents utilisateurs authentifiés du même appareil, ce qui permet une représentation plus précise des données client dans les graphiques d’identités.
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 10%

---

# Présentation de la détection des périphériques partagés (bêta)

>[!IMPORTANT]
>
>Le [!DNL Shared Device Detection] est en version bêta. Les fonctionnalités et la documentation peuvent faire l’objet de changements.

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

[!DNL Shared Device] fait référence aux appareils utilisés par plusieurs individus. Les tablettes, les ordinateurs de bibliothèque et les kiosques sont des exemples d’appareils partagés. Par le biais de la [!DNL Shared Device Detection] , il est possible d’empêcher la fusion de différents utilisateurs d’un même appareil en une seule identité, ce qui permet une représentation plus précise d’un individu.

Avec [!DNL Shared Device Detection], vous pouvez :

* créer des graphiques d’identités distincts pour différents utilisateurs d’un même appareil ;
* empêcher le mélange de données provenant de différentes personnes utilisant le même appareil ;
* Générer une vue plus propre et plus précise de vos clients.

>[!TIP]
>
>Configurations pour [!DNL Shared Device Detection] doit être renseigné avant d’activer Profile pour le jeu de données, car vous ne pouvez plus modifier les paramètres une fois les graphiques générés dans [!DNL Identity Service].

## Prise en main de [!DNL Shared Device Detection]

Utilisation de [!DNL Shared Device Detection] nécessite une compréhension des différents services Platform impliqués. Avant de commencer à utiliser [!DNL Shared Device Detection], veuillez consulter la documentation relative aux services suivants :

* [[!DNL Identity Service]](../home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
   * [Visionneuse de graphique d’identités](./identity-graph-viewer.md): Visualisez et interagissez avec la visionneuse de graphiques d’identités pour mieux comprendre comment les identités client sont regroupées et de quelles façons.
   * [Espaces de noms d’identité](../namespaces.md): Découvrez les composants d’une identité complète et comment les espaces de noms d’identité vous permettent de distinguer le contexte et le type d’identité.

## Comprendre [!DNL Shared Device Detection]

Il est important de comprendre la terminologie suivante lorsque vous utilisez
[!DNL Shared Device Detection]. Consultez le tableau ci-dessous pour obtenir la liste des termes essentiels à la compréhension [!DNL Shared Device Detection].

### Terminologie

| Termes | Définition |
| --- | --- |
| Appareil partagé | Un appareil partagé est un appareil utilisé par plusieurs individus. Les tablettes, les ordinateurs de bibliothèque et les kiosques sont des exemples de périphériques partagés. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] fait référence à un paramètre de configuration qui permet aux données de différents utilisateurs d’un même appareil d’être séparées les unes des autres. |
| Espace de noms d’identité partagée | L’espace de noms d’identité partagée représente l’appareil qui peut être utilisé par plusieurs utilisateurs. L’espace de noms d’identité partagée est généralement l’ECID, mais il peut être défini sur d’autres identifiants d’appareil. |
| Espace de noms d’identité utilisateur | L’espace de noms d’identité de l’utilisateur représente l’utilisateur authentifié (connecté) d’un appareil partagé. |
| Dernier utilisateur authentifié | Le dernier utilisateur authentifié représente l’utilisateur qui a été connecté pour la dernière fois à un appareil, si un appareil est connecté par plusieurs comptes. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] fonctionne en établissant deux espaces de noms : la valeur **Espace de noms d’identité partagée** et le **Espace de noms d’identité utilisateur**.

* L’espace de noms d’identité partagée représente l’appareil qui peut être utilisé par plusieurs utilisateurs. Adobe recommande aux clients d’utiliser ECID comme identifiant d’appareil partagé.
* L’espace de noms d’identité de l’utilisateur est mappé à l’espace de noms d’identité qui correspond à l’identifiant de connexion d’un utilisateur. Il peut s’agir de l’identifiant CRM, de l’adresse électronique, du courrier électronique haché ou du numéro de téléphone d’un utilisateur.

Un appareil partagé, comme une tablette, possède une seule **Espace de noms d’identité partagée**. D’un autre côté, chaque utilisateur d’un appareil partagé a sa propre désignation. **Espace de noms d’identité utilisateur** qui correspond à leurs identifiants de connexion respectifs. Par exemple, une tablette que Kevin et Nora partagent pour l’utilisation du commerce électronique possède son propre ECID de `1234`, tandis que Kevin possède son propre espace de noms d’identité utilisateur mappé à son `kevin@email.com` compte et Nora a son propre espace de noms d’identité utilisateur mappé à `nora@email.com` compte .

[!DNL Shared Device Detection] peut faire des distinctions entre plusieurs utilisateurs d’un même appareil en liant l’espace de noms d’identité partagée (par exemple, ECID) avec l’espace de noms d’identité du dernier utilisateur authentifié (identifiant de connexion).

### Envoi des données d’identité à un graphique d’identités

Examinez l’exemple suivant pour mieux comprendre comment [!DNL Shared Device Detection] fonctionne :

>[!NOTE]
>
>Dans ce diagramme, l’espace de noms d’identité partagée est configuré sur ECID et l’espace de noms d’identité utilisateur est configuré sur l’identifiant CRM.

![Diagramme.](../images/shared-device/diagram.png)

* Kevin et Nora partagent une tablette pour visiter un site de commerce électronique. Cependant, ils disposent tous deux de leurs propres comptes indépendants qu&#39;ils utilisent chacun pour naviguer et faire des achats en ligne ;
   * En tant qu’appareil partagé, la tablette dispose d’un ECID correspondant, qui représente l’ID de cookie du navigateur web de la tablette ;
* Supposons que Kevin utilise la tablette et **se connecte** sur son compte de commerce électronique pour rechercher des écouteurs, cela signifie que l’identifiant CRM de Kevin (**Espace de noms d’identité utilisateur**) est désormais lié à l’ECID de la tablette (**Espace de noms d’identité partagée**). Les données de navigation de la tablette sont maintenant intégrées au graphique d&#39;identités de Kevin.
   * Si Kevin **déconnexion** et Nora utilise la tablette et **se connecte** à son propre compte et achète une caméra, son identifiant CRM est désormais lié à l’ECID de la tablette. Par conséquent, les données de navigation de la tablette sont désormais intégrées au graphique d’identités de Nora.
   * Si Nora **ne se déconnecte pas** et Kevin utilise la tablette, mais **ne se connecte pas**, les données de navigation de la tablette sont toujours intégrées à Nora, car elle reste en tant qu’utilisateur authentifié et son ID de gestion de la relation client est toujours lié à l’ECID de la tablette.
   * Si Nora **se déconnecte** et Kevin utilise la tablette, mais **ne se connecte pas**, les données de navigation de la tablette sont toujours intégrées au graphique d’identités de Nora, car en tant que **dernier utilisateur authentifié**, son identifiant CRM reste associé à l’ECID de la tablette.
   * Si Kevin **se connecte** encore une fois, son identifiant CRM est maintenant associé à l’ECID de la tablette, car il est désormais le dernier utilisateur authentifié et les données de navigation de la tablette sont désormais intégrées à son graphique d’identités.

### Comment [!DNL Profile Service] fusionne des fragments de profil avec [!DNL Shared Device Detection] enabled

[!DNL Profile Service] prend note des fragments de profil et des profils fusionnés. Chaque profil client est composé de plusieurs fragments de profil qui ont été fusionnés dans le but de former une vue unique pour ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client.

When [!DNL Shared Device Detection] est activé, [!DNL Profile] définit l’identité Principale du fragment de profil selon que l’événement d’expérience est authentifié ou non.

Un **événement d’expérience authentifié** est une action effectuée par un utilisateur lorsqu’il est connecté à un appareil. Pour les événements d’expérience authentifiés, l’identité Principale est **Espace de noms d’identité utilisateur** (ID de connexion). Un **événement d’expérience non authentifié** est une action effectuée par un utilisateur qui n’est pas connecté à un appareil. Pour les événements d’expérience non authentifiés, l’identité Principale est **Espace de noms d’identité partagée** (ECID).

Pour plus d’informations, consultez la [[!DNL Real-Time Customer Profile] présentation](../../profile/home.md).

## Interface utilisateur des périphériques partagés

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Paramètres d’identité]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

Le [!UICONTROL Paramètres des appareils partagés] s’affiche, vous fournissant une interface permettant de configurer les paramètres d’appareil partagé pour vos données. Les paramètres des appareils partagés sont désactivés par défaut.

Lorsqu’ils sont activés, les paramètres d’appareil partagés permettent de séparer les données de différents utilisateurs d’un même appareil les uns des autres. Ce paramètre de configuration permet une représentation plus précise et plus précise des graphiques d’identités, où les identités utilisateur du même appareil ne sont pas combinées.

Sélectionner **[!UICONTROL Activer]** pour commencer à modifier les paramètres de votre appareil partagé.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

Le [!UICONTROL Espace de noms d’identité partagée] et [!UICONTROL Espace de noms d’identité utilisateur] des options de configuration s’affichent, vous permettant de modifier les espaces de noms d’identité que vous souhaitez utiliser.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Espace de noms d’identité partagée] représente un périphérique unique utilisé par plusieurs utilisateurs différents. Cet espace de noms est toujours défini sur **[!UICONTROL ECID]** car tous les utilisateurs de Platform utilisent **[!UICONTROL ECID]** comme identifiant du navigateur web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

Le [!UICONTROL Espace de noms d’identité utilisateur] vous permet d’identifier différents utilisateurs d’un même appareil et d’empêcher la combinaison des données dans le même graphique d’identités.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Sélectionnez la **[!UICONTROL Espace de noms d’identité utilisateur]** et saisissez un espace de noms d’identité ou sélectionnez un espace de noms d’identité dans le menu déroulant.

>[!TIP]
>
>Le [!UICONTROL Espace de noms d’identité utilisateur] doit être mappé à l’espace de noms d’identité correspondant à l’identifiant de connexion de l’utilisateur final. Les options incluent l’ID de client, le courrier électronique et le courrier électronique haché.

![emails](../images/shared-device/emails.png)

Une fois que vous avez configuré votre [!UICONTROL Paramètres des périphériques partagés], sélectionnez **[!UICONTROL Enregistrer]**.

![save](../images/shared-device/save.png)

Une fenêtre contextuelle s’affiche, vous invitant à confirmer votre sélection. Sélectionner **[!UICONTROL Oui]** pour terminer le paramètre de configuration.

![confirm](../images/shared-device/confirm.png)
