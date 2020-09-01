---
keywords: Experience Platform;home;popular topics;namespace;Namespace;Namespaces;namespaces;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: 'Les espaces de noms d’identité sont des composants d’Identity Service qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur de "name<span>@email.com" en tant qu’adresse électronique ou de "443522" en tant qu’identifiant CRM numérique. '
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 63%

---


# Présentation des espaces de noms d’identité

Identity namespaces are a component of [[!DNL Identity Service]](./home.md) that serve as indicators of the context to which an identity relates. Par exemple, ils distinguent une valeur « name<span>@email.com » comme adresse électronique ou « 443522 » comme identifiant CRM numérique.

## Prise en main

L’utilisation des espaces de noms d’identité nécessite une compréhension des différents services d’Adobe Experience Platform impliqués. Avant de commencer à travailler avec les espaces de noms d’identité, veuillez consulter la documentation relative aux services suivants :

- [[ !Profil client en temps réel DNL]](../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [[ !Service d&#39;identité DNL]](./home.md): Obtenez une meilleure vue des clients individuels et de leur comportement en rapprochant les identités entre les périphériques et les systèmes.
- [[ !Privacy Service DNL]](../privacy-service/home.md): Les espaces de nommage d&#39;identité sont utilisés pour se conformer au Règlement général sur la protection des données (RGPD), où les demandes de RGPD peuvent être faites par rapport à un espace de nommage.

## Compréhension des espaces de noms d’identité

Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. When matching record data across profile fragments, as when [!DNL Real-time Customer Profile] merges profile data, both the identity value and the namespace must match.

Par exemple, deux fragments de profil peuvent contenir des identifiants principaux différents, mais partager la même valeur pour l’espace de noms « Email ». Par conséquent, Platform est en mesure de voir que ces fragments représentent en fait la même personne et peut rassembler les données dans le graphique d’identités de la personne.

![](images/identity-service-stitching.png)

### Types d’identité

Les données peuvent être identifiées par plusieurs types d’identité différents. Le type d’identité est spécifié au moment de la création de l’espace de noms d’identité et contrôle la conservation ou non des données dans le graphique d’identités, ainsi que toutes les instructions spéciales concernant la manière dont ces données doivent être traitées.

Les types d’identité suivants sont disponibles dans [!DNL Platform]:

| Type d’identité | Description |
| --- | --- |
| Cookie | Ces identités sont essentielles à l’expansion et constituent la majorité du graphique d’identités. Cependant, par nature, elles se désintègrent rapidement et perdent leur valeur au fil du temps. La suppression des cookies est traitée d’une façon spécifique dans le graphique d’identités. |
| Multi-appareils | This indicates that [!DNL Identity Service] should consider this to be a strong people identifier and hence preserve it forever. Par exemple, un identifiant de connexion, un identifiant CRM, un identifiant de fidélité, etc. |
| Appareil | Inclut les identifiants IDFA, GAID et autres identifiants IOT. Ils peuvent être partagés par les personnes d’un même foyer. |
| Adresse électronique | Les identités de ce type comprennent des informations d’identification personnelle (PII). This is an indication to [!DNL Identity Service] to handle the value sensitively. |
| Mobile | Les identités de ce type incluent des informations d’identification personnelle. This is an indication to [!DNL Identity Service] to handle the value sensitively. |
| Non-humaine | Utilisé pour stocker des identifiants qui ont besoin d’espaces de noms, mais qui ne sont pas liés à un groupe de personnes. Ces identifiants sont ensuite filtrés à partir du graphique d’identités. Les cas d’utilisation possibles incluent les données relatives aux produits, aux organisations, aux magasins, etc. (Par exemple, un SKU de produit.) |
| Téléphone | Les identités de ce type incluent des informations d’identification personnelle. This is indication to [!DNL Identity Service] to handle the value sensitively. |

### Espaces de noms standard {#standard}

Adobe Experience Platform fournit plusieurs espaces de noms d’identité disponibles pour toutes les organisations. These are known as Standard namespaces and are visible using the [!DNL Identity Service] API or through the [!DNL Platform] UI.

Pour afficher les espaces de noms standard dans l’interface utilisateur, cliquez sur **[!UICONTROL Identités]** dans le rail de gauche, puis cliquez sur l’onglet **[!UICONTROL Parcourir]**. All identity namespaces accessible to your organization will be shown, however those with &quot;[!UICONTROL Standard]&quot; as the &quot;[!UICONTROL Owner]&quot; are the Standard namespaces provided by Adobe.

Vous pouvez ensuite cliquer sur l’un des espaces de noms de la liste pour plus d’informations.

![](./images/standard-namespace-detail.png)

## Gestion des espaces de noms pour votre organisation

Selon les données de votre organisation et les cas d’utilisation, vous pouvez avoir besoin d’espaces de noms personnalisés.

These are visible in the UI as those namespaces with &quot;[!UICONTROL Custom]&quot; as the &quot;[!UICONTROL Owner]&quot;. Custom namespaces can be created using the [!DNL Identity Service] API or through the user interface.

Pour créer un espace de noms personnalisé à l’aide de l’interface utilisateur, cliquez sur **[!UICONTROL Créer un espace de noms d’identité]**, puis complétez la boîte de dialogue et cliquez sur **[!UICONTROL Créer]**.

Namespaces that you define are private to your organization and require a unique &quot;[!UICONTROL Identity Symbol]&quot; (or &quot;code&quot; if you are using the API) in order to be created successfully.

![](./images/create-identity-namespace.png)

Comme pour les espaces de noms standard, vous pouvez cliquer sur un espace de noms personnalisé à partir de l’onglet **[!UICONTROL Parcourir]** pour en afficher les détails. Toutefois, vous pouvez également modifier le nom d’affichage et la description d’un espace de noms personnalisé dans la zone de détails.

>[!NOTE]
>
>Une fois qu’un espace de noms a été créé, il ne peut plus être supprimé et son « Symbole d’identité » (ou « code » dans l’API) et son « Type » ne peuvent plus être modifiés.

## Espaces de noms dans les données d’identité

La délivrance de l’espace de noms pour une identité dépend de la méthode que vous utilisez pour fournir les données d’identité. For details on providing data identity data, please see the section on [supplying identity data](./home.md#supplying-identity-data-to-identity-service) in the [!DNL Identity Service] overview.
