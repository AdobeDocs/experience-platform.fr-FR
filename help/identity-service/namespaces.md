---
keywords: Experience Platform;accueil;rubriques populaires;espace de noms;espaces de noms;espaces de noms;espace de noms;espace de noms d’identité;espace de noms d’identité;identité;identité;service d’identité
solution: Experience Platform
title: Présentation d’Identity Namespace
topic-legacy: overview
description: Les espaces de noms d’identité sont des composants du Service d’identités qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur de "name@email.com" comme adresse électronique ou "443522" comme identifiant CRM numérique.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 5373b8fcd84cee749a85bdb755a23eb7292cf352
workflow-type: tm+mt
source-wordcount: '1598'
ht-degree: 20%

---

# Présentation des espaces de noms d’identité

Les espaces de noms d’identité sont des composants d’[[!DNL Identity Service]](./home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur « name<span>@email.com » comme adresse électronique ou « 443522 » comme identifiant CRM numérique.

## Prise en main

L’utilisation des espaces de noms d’identité nécessite une compréhension des différents services d’Adobe Experience Platform impliqués. Avant de commencer à travailler avec les espaces de noms d’identité, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Identity Service]](./home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
- [[!DNL Privacy Service]](../privacy-service/home.md) : les espaces de noms d’identité sont utilisés pour se conformer au Règlement général sur la protection des données (RGPD), les demandes de RGPD peuvent être faites par rapport à un espace de noms d’identité.

## Compréhension des espaces de noms d’identité

Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. Lors de la mise en correspondance de données d’enregistrement entre des fragments de profil, comme lorsque [!DNL Real-time Customer Profile] fusionne des données de profil, la valeur d’identité et l’espace de noms doivent correspondre.

Par exemple, deux fragments de profil peuvent contenir des identifiants Principaux différents, mais ils partagent la même valeur pour l’espace de noms &quot;Email&quot;. Par conséquent, [!DNL Platform] peut voir que ces fragments sont en fait la même personne et rassemble les données dans le graphique d’identités de la personne.

![](images/identity-service-stitching.png)

### Types d’identité

Les données peuvent être identifiées par plusieurs types d’identité différents. Le type d’identité est spécifié au moment de la création de l’espace de noms d’identité et contrôle la conservation ou non des données dans le graphique d’identités, ainsi que toutes les instructions spéciales concernant la manière dont ces données doivent être traitées. Tous les types d’identité, à l’exception de **Identifiant de non-personne**, suivent le même comportement que le regroupement d’un espace de noms et de sa valeur d’identifiant correspondante dans un cluster de graphiques d’identités. Les données ne sont pas regroupées lors de l’utilisation de **Identifiant de non-personne**.

Les types d’identité suivants sont disponibles dans [!DNL Platform]:

| Type d’identité | Description |
| --- | --- |
| Cookie Identifiant | Les ID de cookie identifient les navigateurs Web. Ces identités sont essentielles à l’expansion et constituent la majorité du graphique d’identités. Cependant, par nature, elles se désintègrent rapidement et perdent leur valeur au fil du temps. |
| Identifiant multi-appareils | Les identifiants multi-appareils identifient un individu et lient généralement d’autres identifiants ensemble. Par exemple, un identifiant de connexion, un identifiant CRM et un identifiant de fidélité. Ceci indique à [!DNL Identity Service] de gérer la valeur avec précaution. |
| ID de périphérique | Les identifiants d’appareil identifient les appareils matériels, tels qu’IDFA (iPhone et iPad), GAID (Android) et RIDA (Roku), et peuvent être partagés par plusieurs personnes dans des foyers. |
| Adresse électronique | Les adresses électroniques sont souvent associées à une seule personne et peuvent donc être utilisées pour identifier cette personne sur différents canaux. Les identités de ce type comprennent des informations d’identification personnelle (PII). Ceci indique à [!DNL Identity Service] de gérer la valeur avec précaution. |
| Identifiant de non-personne | Les identifiants non-personnes sont utilisés pour stocker les identifiants qui nécessitent des espaces de noms, mais ne sont pas connectés à un cluster de personnes. Par exemple, un SKU de produit, des données liées aux produits, aux organisations ou aux magasins. |
| Numéro de téléphone | Les numéros de téléphone sont souvent associés à une seule personne et peuvent donc être utilisés pour identifier cette personne sur différents canaux. Les identités de ce type incluent des informations d’identification personnelle. Ceci indique à [!DNL Identity Service] de gérer la valeur avec précaution. |

### Espaces de noms standard

Experience Platform fournit plusieurs espaces de noms d’identité disponibles pour toutes les organisations. Ils sont appelés espaces de noms standard et sont visibles à l’aide de l’API [!DNL Identity Service] ou via l’interface utilisateur de Platform.

Les espaces de noms standard suivants sont fournis pour être utilisés par toutes les organisations au sein de Platform :

| Nom d’affichage | Description |
| ------------ | ----------- |
| AdCloud | Espace de noms qui représente l’Adobe d’AdCloud. |
| Adobe Analytics (identifiant hérité) | Espace de noms représentant Adobe Analytics. Pour plus d’informations, consultez le document suivant sur les [espaces de noms Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces). |
| IDFA Apple (ID pour les annonceurs) | Espace de noms qui représente l’Apple ID pour les annonceurs. Pour plus d’informations, consultez le document suivant sur les [annonces basées sur les intérêts](https://support.apple.com/fr-fr/HT202074). |
| Service de notification push Apple | Espace de noms représentant les identités collectées à l’aide du service de notification push Apple. Pour plus d’informations, consultez le document suivant sur [Service de notification push Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) . |
| CORE | Espace de noms représentant Adobe Audience Manager. Cet espace de noms peut également être référencé par son nom hérité : &quot;Adobe AudienceManager&quot;. Pour plus d’informations, consultez le document suivant sur les [ID d’Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids). |
| ECID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consultez le document suivant sur [ECID](./ecid.md) pour plus d’informations. |
| Email | Espace de noms représentant une adresse électronique. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |
| Emails (SHA256, avec mise en minuscules) | Espace de noms pour l’adresse électronique préhachée. Les valeurs fournies dans cet espace de noms sont converties en minuscules avant le hachage avec SHA256. Les espaces de début et de fin doivent être supprimés avant qu’une adresse email ne soit normalisée. Ce paramètre ne peut pas être modifié rétroactivement. Pour plus d’informations, consultez le document suivant sur la [prise en charge du hachage SHA-256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) . |
| Firebase Cloud Messaging | Espace de noms représentant les identités collectées à l’aide de Google Firebase Cloud Messaging pour les notifications push. Pour plus d’informations, consultez le document suivant sur [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) . |
| Identifiant Google Ad (GAID) | Espace de noms qui représente un identifiant Google Advertising. Consultez le document suivant sur [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) pour plus d’informations. |
| ID de clic Google | Espace de noms représentant un ID de clic Google. Pour plus d’informations, consultez le document suivant sur [Suivi des clics dans Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking). |
| Téléphone | Espace de noms qui représente un numéro de téléphone. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |
| Téléphone (E.164) | Espace de noms qui représente les numéros de téléphone bruts qui doivent être hachés au format E.164. Le format E.164 comprend un signe plus (`+`), un code d&#39;appel international, un code local et un numéro de téléphone. Par exemple : `(+)(country code)(area code)(phone number)`. |
| Téléphone (SHA256) | Espace de noms qui représente les numéros de téléphone qui doivent être hachés à l’aide de SHA256. Vous devez supprimer les symboles, les lettres et les zéros de début. Vous devez également ajouter le code d’appel de pays comme préfixe. |
| Téléphone (SHA256_E.164) | Espace de noms qui représente les numéros de téléphone bruts qui doivent être hachés au format SHA256 et E.164. |
| TNTID | Espace de noms représentant Adobe Target. Pour plus d’informations, voir le document suivant sur [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en). |
| Windows AID | Espace de noms qui représente un identifiant Windows Advertising. Pour plus d’informations, consultez le document suivant sur [ID de publicité Windows](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041). |

### Affichage des espaces de noms d’identité

Pour afficher les espaces de noms d’identité dans l’interface utilisateur, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Parcourir]**.

![parcourir](./images/browse.png)

Une liste d’espaces de noms d’identité s’affiche dans l’interface principale de la page, affichant des informations sur leur nom, les symboles d’identité, la date de dernière mise à jour et s’il s’agit d’un espace de noms standard ou personnalisé. Le rail de droite contient des informations sur la [!UICONTROL force du graphique d’identités].

![identités](./images/identities.png)

Platform fournit également des espaces de noms à des fins d’intégration. Ces espaces de noms sont masqués par défaut, car ils sont utilisés pour se connecter à d’autres systèmes et non pour assembler des identités. Pour afficher les espaces de noms d’intégration, sélectionnez **[!UICONTROL Afficher les identités d’intégration]**.

![view-integration-identities](./images/view-integration-identities.png)

Sélectionnez un espace de noms d’identité dans la liste pour afficher des informations sur un espace de noms spécifique. La sélection d’un espace de noms d’identité met à jour l’affichage sur le rail de droite afin d’afficher les métadonnées concernant l’espace de noms d’identité que vous avez sélectionné, y compris le nombre d’identités ingérées et le nombre d’enregistrements ayant échoué et ignorés.

![select-namespace](./images/select-namespace.png)

## Gestion des espaces de noms personnalisés {#manage-namespaces}

Selon les données de votre organisation et les cas d’utilisation, vous pouvez avoir besoin d’espaces de noms personnalisés. Les espaces de noms personnalisés peuvent être créés à l’aide de l’API [[!DNL Identity Service]](./api/create-custom-namespace.md) ou via l’interface utilisateur.

Pour créer un espace de noms personnalisé à l’aide de l’interface utilisateur, accédez à l’espace de travail **[!UICONTROL Identités]**, sélectionnez **[!UICONTROL Parcourir]**, puis sélectionnez **[!UICONTROL Créer un espace de noms d’identité]**.

![select-create](./images/select-create.png)

La boîte de dialogue **[!UICONTROL Créer un espace de noms d’identité]** s’affiche. Indiquez un **[!UICONTROL nom d’affichage]** et **[!UICONTROL symbole d’identité]** unique, puis sélectionnez le type d’identité que vous souhaitez créer. Vous pouvez également ajouter une description facultative pour ajouter des informations supplémentaires sur l’espace de noms. Tous les types d’identité, à l’exception de **Identifiant de non-personne**, suivent le même comportement de regroupement. Si vous sélectionnez **Identifiant de non-personne** comme type d’identité lors de la création d’un espace de noms, l’assemblage ne se produit pas. Pour plus d’informations sur chaque type d’identité, reportez-vous au tableau sur les [types d’identité](#identity-types).

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

>[!IMPORTANT]
>
>Les espaces de noms que vous définissez sont propres à votre organisation et nécessitent un symbole d’identité unique pour être créés avec succès.

![create-identity-namespace](./images/create-identity-namespace.png)

Comme pour les espaces de noms standard, vous pouvez sélectionner un espace de noms personnalisé dans l’onglet **[!UICONTROL Parcourir]** pour en afficher les détails. Cependant, avec un espace de noms personnalisé, vous pouvez également modifier son nom d’affichage et sa description à partir de la zone de détails.

>[!NOTE]
>
>Une fois qu’un espace de noms a été créé, il ne peut plus être supprimé et son symbole d’identité et son type ne peuvent plus être modifiés.

## Espaces de noms dans les données d’identité

La délivrance de l’espace de noms pour une identité dépend de la méthode que vous utilisez pour fournir les données d’identité. Pour plus d’informations sur la délivrance de données d’identité, reportez-vous à la section [fournissant des données d’identité](./home.md#supplying-identity-data-to-identity-service) dans la [!DNL Identity Service] présentation.

## Étapes suivantes

Maintenant que vous comprenez les concepts clés des espaces de noms d’identité, vous pouvez commencer à apprendre à utiliser votre graphique d’identités à l’aide de la [visionneuse de graphiques d’identités](./ui/identity-graph-viewer.md).
