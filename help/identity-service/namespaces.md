---
keywords: Experience Platform ; accueil ; sujets populaires ; espace de nommage ; Espace de nommage ; Espaces de nommage ; espaces de nommage ; espace de nommage d'identité ; espace de nommage d'identité ; identité ; identité ; service d'identité ; service d'identité
solution: Experience Platform
title: Présentation de l'Espace de nommage d'identité
topic: aperçu
description: 'Les espaces de noms d’identité sont des composants d’Identity Service qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent la valeur "name@email.com" en tant qu’adresse électronique ou "443522" en tant qu’identifiant CRM numérique. '
translation-type: tm+mt
source-git-commit: fc493a207e305887e798238ba6883f4934c5cba5
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 22%

---


# Présentation des espaces de noms d’identité

Les espaces de noms d’identité sont des composants d’[[!DNL Identity Service]](./home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur « name<span>@email.com » comme adresse électronique ou « 443522 » comme identifiant CRM numérique.

## Prise en main

L’utilisation des espaces de noms d’identité nécessite une compréhension des différents services d’Adobe Experience Platform impliqués. Avant de commencer à travailler avec les espaces de noms d’identité, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Identity Service]](./home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
- [[!DNL Privacy Service]](../privacy-service/home.md) : les espaces de noms d’identité sont utilisés pour se conformer au Règlement général sur la protection des données (RGPD), les demandes de RGPD peuvent être faites par rapport à un espace de noms d’identité.

## Compréhension des espaces de noms d’identité

Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. Lors de la correspondance de données d’enregistrement entre des fragments de profil, comme lorsque [!DNL Real-time Customer Profile] fusionne des données de profil, la valeur d’identité et l’espace de nommage doivent correspondre.

Par exemple, deux fragments de profil peuvent contenir des identifiants Principaux différents mais ils partagent la même valeur pour l’espace de nommage &quot;E-mail&quot;. Par conséquent, [!DNL Platform] peut voir que ces fragments sont en fait la même personne et rassemble les données dans le graphique d’identité de la personne.

![](images/identity-service-stitching.png)

### Types d’identité

Les données peuvent être identifiées par plusieurs types d’identité différents. Le type d’identité est spécifié au moment de la création de l’espace de noms d’identité et contrôle la conservation ou non des données dans le graphique d’identités, ainsi que toutes les instructions spéciales concernant la manière dont ces données doivent être traitées.

Les types d’identité suivants sont disponibles dans [!DNL Platform]:

| Type d’identité | Description |
| --- | --- |
| Cookie Identifiant | Les ID de cookie identifient les navigateurs Web. Ces identités sont essentielles à l’expansion et constituent la majorité du graphique d’identités. Cependant, par nature, elles se désintègrent rapidement et perdent leur valeur au fil du temps. |
| ID sur plusieurs périphériques | Les identifiants sur plusieurs périphériques identifient une personne et lient généralement d’autres identifiants ensemble. Par exemple, un ID de connexion, un ID de gestion de la relation client et un ID de fidélité. Il s&#39;agit d&#39;une indication à [!DNL Identity Service] pour gérer la valeur de façon sensible. |
| ID de périphérique | Les ID de périphérique identifient les périphériques matériels, tels que IDFA (iPhone et iPad), GAID (Android) et RIDA (Roku), et peuvent être partagés par plusieurs personnes au sein des ménages. |
| Adresse électronique | Les adresses électroniques sont souvent associées à une seule personne et peuvent donc être utilisées pour identifier cette personne sur différents canaux. Les identités de ce type comprennent des informations d’identification personnelle (PII). Il s&#39;agit d&#39;une indication à [!DNL Identity Service] pour gérer la valeur de façon sensible. |
| Identificateur des personnes autres que les personnes | Les identifiants non-personnes sont utilisés pour stocker les identifiants qui nécessitent des espaces de nommage mais qui ne sont pas connectés à une grappe de personnes. Par exemple, un SKU de produit, des données liées à des produits, des organisations ou des magasins. |
| Numéro de téléphone | Les numéros de téléphone sont souvent associés à une seule personne et peuvent donc être utilisés pour identifier cette personne sur différents canaux. Les identités de ce type incluent des informations d’identification personnelle. Il s&#39;agit d&#39;une indication à [!DNL Identity Service] pour gérer la valeur de façon sensible. |

### Espaces de noms standard

Experience Platform fournit plusieurs espaces de noms d’identité disponibles pour toutes les organisations. Ces espaces de nommage sont connus sous le nom d’ standard et sont visibles à l’aide de l’API [!DNL Identity Service] ou via l’interface utilisateur de la plate-forme.

Les espaces de nommage standard suivants sont fournis pour être utilisés par toutes les organisations au sein de Plateforme :

| Nom d’affichage | Description |
| ------------ | ----------- |
| AdCloud | Espace de nommage représentant l’Adobe AdCloud. |
| Adobe Analytics (ID hérité) | Espace de nommage qui représente Adobe Analytics. Pour plus d&#39;informations, consultez le document suivant sur [espaces de nommage Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces). |
| Apple IDFA (ID pour les annonceurs) | Espace de nommage qui représente un ID Apple pour les annonceurs. Pour plus d&#39;informations, consultez le document suivant sur [les publicités basées sur des intérêts](https://support.apple.com/en-us/HT202074). |
| Service de notifications Push Apple | Espace de nommage qui représente les identités collectées à l’aide du service de notifications Push Apple. Pour plus d’informations, consultez le document suivant sur [service de notifications Push Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1). |
| CORE | Espace de nommage qui représente Adobe Audience Manager. Cet espace de nommage peut également être référencé par son nom hérité : &quot;Adobe AudienceManager&quot;. Pour plus d’informations, consultez le document suivant sur [ID d’Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids). |
| ECID | Espace de nommage qui représente l’ECID. Cet espace de nommage peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Pour plus d&#39;informations, consultez le document suivant sur [ECID](./ecid.md). |
| E-mail | Espace de nommage qui représente une adresse électronique. Ce type d&#39;espace de nommage est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne dans différents canaux. |
| Courriers électroniques (SHA256, avec un caractère minuscule) | Espace de nommage d’adresse électronique préhachée. Les valeurs fournies dans cet espace de nommage sont converties en minuscules avant le hachage avec SHA256. Les espaces de début et de fin doivent être supprimés avant qu’une adresse électronique ne soit normalisée. Ce paramètre ne peut pas être modifié rétroactivement. Pour plus d’informations, consultez le document suivant sur [Prise en charge du hachage SHA256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support). |
| Messagerie Firebase Cloud | Espace de nommage qui représente les identités collectées à l’aide de Google Firebase Cloud Messaging pour les notifications Push. Pour plus d’informations, consultez le document suivant sur [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging). |
| Identifiant de publicité Google (GAID) | Espace de nommage qui représente un identifiant Google Advertising ID. Pour plus d&#39;informations, consultez le document suivant sur [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en). |
| ID de clic Google | Espace de nommage qui représente un identifiant de clic Google. Pour plus d&#39;informations, consultez le document suivant sur le [suivi des clics dans les publicités Google](https://developers.google.com/adwords/api/docs/guides/click-tracking). |
| Téléphone | Espace de nommage qui représente un numéro de téléphone. Ce type d&#39;espace de nommage est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne dans différents canaux. |
| Téléphone (E.164) | Espace de nommage qui représente les numéros de téléphone bruts qui doivent être hachés au format E.164. Le format E.164 comprend un signe plus (`+`), un code d&#39;appel international pour le pays, un code local et un numéro de téléphone. Par exemple: `(+)(country code)(area code)(phone number)`. |
| Téléphone (SHA256) | Espace de nommage qui représente les numéros de téléphone qui doivent être hachés à l&#39;aide de SHA256. Vous devez supprimer les symboles, les lettres et les zéros de début. Vous devez également ajouter le code d’appel du pays comme préfixe. |
| Téléphone (SHA256_E.164) | Espace de nommage qui représente les numéros de téléphone bruts qui doivent être hachés au format SHA256 et E.164. |
| TNTID | Espace de nommage qui représente Adobe Target. Pour plus d’informations, consultez le document suivant sur [Cible](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en). |
| Windows AID | Espace de nommage qui représente un identifiant de publicité Windows. Pour plus d&#39;informations, consultez le document suivant sur [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041). |

Pour vue des espaces de nommage standard dans l&#39;interface utilisateur, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez l&#39;onglet **[!UICONTROL Parcourir]** pour afficher une liste d&#39;espaces de nommage d&#39;identité standard accessibles à votre organisation. Vous pouvez trier les espaces de nommage par ordre alphabétique selon leur **[!UICONTROL nom d’affichage]**, **[!UICONTROL symbole d’identité]** ou **[!UICONTROL propriétaire]**. Vous pouvez également trier les espaces de nommage par ordre chronologique en fonction de leur date de mise à jour la plus récente.

Sélectionnez un espace de nommage pour afficher des informations plus spécifiques sur le rail de droite.

>[!NOTE]
>
>Platform fournit également des espaces de nommage à des fins d’intégration. Ces espaces de nommage sont masqués par défaut car ils servent à se connecter à d&#39;autres systèmes et non à recouper des identités. Pour vue des espaces de nommage d&#39;intégration, sélectionnez **[!UICONTROL identités d&#39;intégration de Vue]**.

![](./images/browse-namespaces.png)

## Gestion des espaces de nommage personnalisés {#manage-namespaces}

Selon les données de votre organisation et les cas d’utilisation, vous pouvez avoir besoin d’espaces de noms personnalisés. Les espaces de nommage personnalisés peuvent être créés à l’aide de l’API [[!DNL Identity Service]](./api/create-custom-namespace.md) ou via l’interface utilisateur.

Pour créer un espace de nommage personnalisé à l’aide de l’interface utilisateur, accédez à l’espace de travail **[!UICONTROL Identités]**, sélectionnez **[!UICONTROL Parcourir]**, puis **[!UICONTROL Créer un espace de nommage d’identité]**.

![](./images/create.png)

La boîte de dialogue **[!UICONTROL Créer un espace de nommage d&#39;identité]** s&#39;affiche. Indiquez un **[!UICONTROL nom d’affichage]** unique et **[!UICONTROL symbole d’identité]**, puis sélectionnez le type d’identité que vous souhaitez créer. Vous pouvez également ajouter une description facultative à d’autres informations sur l’espace de nommage. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer]**.

>[!IMPORTANT]
>
>Les Espaces de nommage que vous définissez sont privés à votre entreprise et nécessitent un symbole d’identité unique pour être créés avec succès.

![](./images/create-namespace.png)

Comme pour les espaces de nommage standard, vous pouvez sélectionner un espace de nommage personnalisé dans l&#39;onglet **[!UICONTROL Parcourir]** pour en vue les détails. Cependant, avec un espace de nommage personnalisé, vous pouvez également modifier son nom d’affichage et sa description à partir de la zone de détails.

>[!NOTE]
>
>Une fois un espace de nommage créé, il ne peut plus être supprimé et son symbole d&#39;identité et son type ne peuvent plus être modifiés.

## Espaces de noms dans les données d’identité

La délivrance de l’espace de noms pour une identité dépend de la méthode que vous utilisez pour fournir les données d’identité. Pour plus d&#39;informations sur la fourniture de données d&#39;identité, consultez la section [la fourniture de données d&#39;identité](./home.md#supplying-identity-data-to-identity-service) dans l&#39;[!DNL Identity Service] présentation.

## Étapes suivantes

Maintenant que vous connaissez les concepts clés des espaces de nommage d&#39;identité, vous pouvez commencer à apprendre à utiliser votre graphique d&#39;identité à l&#39;aide de la [visionneuse de graphiques d&#39;identité](./ui/identity-graph-viewer.md).
