---
title: Présentation d’Identity Namespace
description: Découvrez les espaces de noms d’identité dans Identity Service.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 98482bfdd54b70cde73c3512f8237c7862e41281
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 18%

---

# Présentation des espaces de noms d’identité

Lisez le document suivant pour en savoir plus sur ce que vous pouvez faire avec les espaces de noms d’identité dans Adobe Experience Platform Identity Service.

## Prise en main

Les espaces de noms d’identité nécessitent une compréhension des différents services Adobe Experience Platform. Avant de commencer à travailler avec les espaces de noms d’identité, veuillez consulter la documentation relative aux services suivants :

* [[!DNL Real-Time Customer Profile]](../profile/home.md): fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Identity Service]](./home.md): profitez d’une meilleure vue d’ensemble des clients et de leur comportement en rapprochant des identités entre appareils et systèmes.
* [[!DNL Privacy Service]](../privacy-service/home.md): les espaces de noms d’identité sont utilisés dans les demandes de conformité pour les réglementations de confidentialité juridiques telles que le Règlement général sur la protection des données (RGPD). Chaque demande d’accès à des informations personnelles est relative à un espace de noms afin d’identifier les données des consommateurs qui doivent être affectées.

## Compréhension des espaces de noms d’identité

![Illustration d’un processus de données avec Identity Service.](images/identity-service-stitching.png)

Une identité entièrement qualifiée comprend deux composants : une **valeur d’identité** et un **espace de noms d’identité**. Par exemple, si la valeur d’une identité est `scott@acme.com`, puis un espace de noms fournit du contexte à cette valeur en la distinguant comme adresse électronique. De même, un espace de noms peut distinguer `555-123-456` comme numéro de téléphone ; et `3126ABC` comme identifiant CRM. Essentiellement, **un espace de noms fournit un contexte à une identité donnée ;**. Lors de la mise en correspondance de données d’enregistrement entre des fragments de profil, comme lorsque [!DNL Real-Time Customer Profile] fusionne les données de profil ; la valeur d’identité et l’espace de noms doivent correspondre.

Par exemple, deux fragments de profil peuvent contenir des identifiants principaux différents, mais ils partagent la même valeur pour l’espace de noms &quot;Email&quot;. Par conséquent, l’Experience Platform peut voir que ces fragments sont en fait la même personne et rassemble les données dans le graphique d’identités de la personne.

>[!BEGINSHADEBOX]

**Identity namespace expliqué**

Une autre manière de mieux comprendre le concept d’espace de noms consiste à prendre en compte des exemples du monde réel tels que les villes et leurs états correspondants. Par exemple, Portland, Maine et Portland, Oregon, sont deux endroits différents aux États-Unis. Bien que les villes portent le même nom, l&#39;État agit comme un espace de noms et fournit le contexte nécessaire pour distinguer les deux villes l&#39;une de l&#39;autre.

Application de la même logique à Identity Service :

* En un coup d’oeil, la valeur d’identité de : `1-234-567-8900` peut ressembler à un numéro de téléphone. Cependant, du point de vue du système, cette valeur peut avoir été configurée en tant qu’identifiant CRM. Identity Service n’aurait aucun moyen d’appliquer le contexte nécessaire à cette valeur d’identité sans un espace de noms correspondant.
* Autre exemple : la valeur d’identité de : `john@gmail.com`. Bien que cette valeur d’identité puisse facilement être considérée comme un e-mail, il est tout à fait possible qu’elle soit configurée en tant qu’identifiant CRM d’espace de noms personnalisé. Avec l’espace de noms, vous pouvez distinguer `Email:john@gmail.com` de `CRM ID:john@gmail.com`.

>[!ENDSHADEBOX]

### Composants d’un espace de noms

Un espace de noms se compose des composants suivants :

* **Nom d’affichage**: nom convivial d’un espace de noms donné.
* **Symbole d’identité**: code utilisé en interne par Identity Service pour représenter un espace de noms.
* **Type d’identité**: classification d’un espace de noms donné.
* **Description**: (facultatif) toute information supplémentaire que vous pouvez fournir concernant un espace de noms donné.

### Type d’identité {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Définition du type d&#39;identité"
>abstract="Le type d&#39;identité contrôle si les données sont stockées ou non dans le graphique d&#39;identité. Les graphiques d’identités ne sont pas générés pour les types d’identités suivants : identifiants autres que de personne et identifiants de partenaire."
>text="Learn more in documentation"

Un élément d’un espace de noms d’identité est le suivant : **type d&#39;identité**. Le type d’identité détermine :

* Génération d’un graphique d’identités :
   * Les graphiques d’identités ne sont pas générés pour les types d’identités suivants : identifiants autres que de personne et identifiants de partenaire.
   * Des graphiques d’identités sont générés pour tous les autres types d’identités.
* Les identités qui sont supprimées du graphique d’identités lorsque les limites du système sont atteintes. Pour plus d’informations, consultez la section [barrières de sécurité pour les données d’identité](guardrails.md).

Les types d’identité suivants sont disponibles dans Experience Platform :

| Type d’identité | Description |
| --- | --- |
| ID de cookie | Les ID de cookie identifient les navigateurs Web. Ces identités sont essentielles à l’expansion et constituent la majorité du graphique d’identités. Cependant, par nature, ils se désintègrent rapidement et perdent leur valeur au fil du temps. |
| Identifiant multi-appareils | Les identifiants multi-appareils identifient un individu et lient généralement d’autres identifiants ensemble. Par exemple, un identifiant de connexion, un identifiant CRM et un identifiant de fidélité. Cela indique que [!DNL Identity Service] pour gérer la valeur avec précaution. |
| ID d’appareil | Les identifiants d’appareil identifient les appareils matériels, tels qu’IDFA (iPhone et iPad), GAID (Android) et RIDA (Roku), et peuvent être partagés par plusieurs personnes dans des foyers. |
| Adresse e-mail | Les adresses électroniques sont souvent associées à une seule personne et peuvent donc être utilisées pour identifier cette personne sur différents canaux. Les identités de ce type comprennent des informations d’identification personnelle (PII). Cela indique que [!DNL Identity Service] pour gérer la valeur avec précaution. |
| Identifiant de non-personne | Les identifiants non-personnes sont utilisés pour stocker les identifiants qui nécessitent des espaces de noms, mais ne sont pas connectés à un cluster de personnes. Par exemple, un SKU de produit, des données liées aux produits, aux organisations ou aux magasins. |
| Identifiant du partenaire | <ul><li>Les identifiants de partenaire sont des identifiants utilisés par les partenaires de données pour représenter des personnes. Les identifiants de partenaire sont souvent pseudonymes afin de ne pas révéler la véritable identité d&#39;une personne, et peuvent être probabilistes. Dans Real-time Customer Data Platform, les identifiants de partenaire sont principalement utilisés pour l’activation étendue de l’audience et l’enrichissement des données, et non pour la création de liens entre graphiques d’identités.</li><li>Les graphiques d’identités ne sont pas générés lors de l’ingestion d’une identité contenant un espace de noms d’identité spécifié comme type d’identifiant de partenaire.</li><li>Si vous n’ingérez pas de données de partenaire à l’aide du type d’identité de l’identifiant de partenaire, vous risquez d’atteindre les limites des graphiques système sur Identity Service, ainsi que de fusionner des profils indésirables.</li><ul> |
| Numéro de téléphone | Les numéros de téléphone sont souvent associés à une seule personne et peuvent donc être utilisés pour identifier cette personne sur différents canaux. Les identités de ce type incluent des informations d’identification personnelle. Cela indique que [!DNL Identity Service] pour gérer la valeur avec précaution. |

{style="table-layout:auto"}

### Espaces de noms standard {#standard}

Experience Platform fournit plusieurs espaces de noms d’identité disponibles pour toutes les organisations. Ils sont appelés espaces de noms standard et sont visibles à l’aide de la variable [!DNL Identity Service] API ou via l’interface utilisateur de Platform.

Les espaces de noms standard suivants sont fournis pour être utilisés par toutes les organisations au sein de Platform :

| Nom d’affichage | Description |
| ------------ | ----------- |
| AdCloud | Espace de noms qui représente l’Adobe d’AdCloud. |
| Adobe Analytics (identifiant hérité) | Espace de noms représentant Adobe Analytics. Consultez le document suivant sur [Espaces de noms Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html#namespaces) pour plus d’informations. |
| IDFA Apple (ID pour les annonceurs) | Un espace de noms représentant l’ID Apple pour les annonceurs. Pour plus d’informations, consultez le document sur les [annonces basées sur les intérêts](https://support.apple.com/fr-fr/HT202074). |
| Service de notification push Apple | Espace de noms représentant les identités collectées à l’aide du service de notification push Apple. Consultez le document suivant sur [Service de notification push Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) pour plus d’informations. |
| CORE | Espace de noms représentant Adobe Audience Manager. Cet espace de noms peut également être mentionné par son nom hérité : &quot;Adobe AudienceManager&quot;. Consultez le document suivant sur [ID d’Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html#aam-ids) pour plus d’informations. |
| ECID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Consultez le document suivant sur [ECID](./ecid.md) pour plus d’informations. |
| E-mail | Espace de noms représentant une adresse électronique. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |
| E-mails (SHA256, en minuscules) | Un espace de noms pour adresse électronique préhachée. Les valeurs fournies dans cet espace de noms sont converties en minuscules avant le hachage en SHA-256. Les espaces de début et de fin doivent être supprimés avant qu’une adresse e-mail ne soit normalisée. Ce paramètre ne peut pas être modifié rétroactivement. Consultez le document suivant sur [Prise en charge du hachage SHA-256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support) pour plus d’informations. |
| Firebase Cloud Messaging | Espace de noms représentant les identités collectées à l’aide de Google Firebase Cloud Messaging pour les notifications push. Consultez le document suivant sur [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) pour plus d’informations. |
| Google Ad ID (GAID) | Un espace de noms représentant un ID Google Advertising. Pour plus d’informations, consultez le document suivant sur l’[ID Google Advertising](https://support.google.com/googleplay/android-developer/answer/6048248?hl=fr). |
| Google Click ID | Espace de noms représentant un identifiant de clic Google. Consultez le document suivant sur [Suivi des clics dans Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) pour plus d’informations. |
| Téléphone | Un espace de noms qui représente un numéro de téléphone. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |
| Téléphone (E.164) | Espace de noms qui représente les numéros de téléphone bruts qui doivent être hachés au format E.164. Le format E.164 comprend un signe plus (`+`), un numéro de téléphone international, un numéro de téléphone local et un numéro de téléphone. Par exemple : `(+)(country code)(area code)(phone number)`. |
| Téléphone (SHA256) | Espace de noms qui représente les numéros de téléphone qui doivent être hachés à l’aide de SHA256. Vous devez supprimer les symboles, les lettres et les zéros de début. Vous devez également ajouter le code d’appel de pays comme préfixe. |
| Téléphone (SHA256_E.164) | Un espace de noms représentant des numéros de téléphone bruts qui doivent être hachés au format SHA256 et E.164. |
| TNTID | Espace de noms représentant Adobe Target. Consultez le document suivant sur [Cible](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr) pour plus d’informations. |
| Windows AID | Espace de noms qui représente un identifiant Windows Advertising. Consultez le document suivant sur [Identifiant Windows Advertising](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) pour plus d’informations. |

### Afficher des espaces de noms d’identités {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Affichage des identités d&#39;intégration"
>abstract="Les identités d&#39;intégration sont des espaces de noms utilisés pour établir une connexion avec d&#39;autres systèmes et ne sont pas utilisés dans la résolution d&#39;identité ou pour assembler des identités. <br> Ces identités sont masquées par défaut. Utilisez le bouton pour afficher les espaces de noms d&#39;intégration."

Pour afficher les espaces de noms d’identité dans l’interface utilisateur, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Parcourir]**.

Un répertoire des espaces de noms de votre organisation s’affiche, affichant des informations sur leurs noms, symboles d’identité, dates de dernière mise à jour, types d’identité correspondants et description.

![Répertoire d’espaces de noms d’identité personnalisés dans votre organisation.](./images/namespace/browse.png)

## Créer des espaces de noms personnalisés {#create-namespaces}

Selon les données de votre organisation et les cas d’utilisation, vous pouvez avoir besoin d’espaces de noms personnalisés. Les espaces de noms personnalisés peuvent être créés à l’aide de la variable [[!DNL Identity Service]](./api/create-custom-namespace.md) API ou via l’interface utilisateur.

Pour créer un espace de noms personnalisé, sélectionnez **[!UICONTROL Créer un espace de noms d’identité]**.

![Bouton Créer un espace de noms d’identité dans l’espace de travail des identités.](./images/namespace/create-identity-namespace.png)

La variable [!UICONTROL Créer un espace de noms d’identité] s’affiche. Tout d’abord, vous devez fournir un nom d’affichage et un symbole d’identité pour l’espace de noms personnalisé que vous souhaitez créer. Vous pouvez également éventuellement fournir une description pour ajouter plus de contexte à l’espace de noms personnalisé que vous créez.

![Fenêtre contextuelle dans laquelle vous pouvez saisir des informations concernant votre espace de noms d’identité personnalisé.](./images/namespace/name-and-symbol.png)

Sélectionnez ensuite le type d’identité à affecter à l’espace de noms personnalisé. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

![Une sélection de types d’identité que vous pouvez choisir et affecter à votre espace de noms d’identité personnalisé.](./images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* Les espaces de noms que vous définissez sont propres à votre organisation et nécessitent un symbole d’identité unique pour être créés avec succès.
>
>* Une fois qu’un espace de noms a été créé, il ne peut plus être supprimé et son symbole d’identité et son type ne peuvent plus être modifiés.
>
>* Les espaces de noms en double ne sont pas pris en charge. Vous ne pouvez pas utiliser un nom d’affichage et un symbole d’identité existants lors de la création d’un espace de noms.

## Espaces de noms dans les données d’identité

La délivrance de l’espace de noms pour une identité dépend de la méthode que vous utilisez pour fournir les données d’identité. Pour plus d’informations sur la délivrance de données d’identité, consultez la section sur [fournissant des données d’identité](./home.md#supplying-identity-data-to-identity-service) dans le [!DNL Identity Service] aperçu.

## Étapes suivantes

Maintenant que vous comprenez les concepts clés des espaces de noms d’identité, vous pouvez commencer à apprendre à utiliser votre graphique d’identités à l’aide de la variable [visionneuse de graphiques d’identités](./ui/identity-graph-viewer.md).
