---
title: Présentation De L’Extension Transfert D’Événements Algolia
description: Découvrez comment configurer et utiliser l’extension de transfert d’événement Algolia dans Adobe Experience Platform. Transférez les données de comportement des utilisateurs via l’API Insights, configurez des règles, mappez des champs XDM et vérifiez la diffusion des événements.
last-substantial-update: 2025-05-09T00:00:00Z
source-git-commit: d1b641ed0b48357a2f4b78d6829ccab52e4889ca
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 1%

---


# Présentation de l’extension de transfert d’événement [!DNL Algolia] {#overview}

>[!NOTE]
>
>Adobe Experience Platform Launch fait désormais partie des technologies de collecte de données de Adobe Experience Platform. Par conséquent, des mises à jour terminologiques ont été apportées à la documentation du produit. Pour obtenir la liste complète de ces modifications, reportez-vous au [guide des mises à jour terminologiques](../../../../tags/term-updates.md).

Utilisez [!DNL Algolia] pour offrir des expériences de recherche rapides, pertinentes et personnalisées. Grâce à l’optimisation optimisée par l’IA, vous pouvez améliorer les résultats de recherche et les recommandations afin d’aider les utilisateurs et les utilisatrices à trouver rapidement les produits, le contenu ou les informations dont ils ont besoin.

Utilisez l’extension de transfert d’événement [!DNL Algolia] pour envoyer des événements de comportement utilisateur à [!DNL Algolia] via le [!DNL Insights API]. Ces données comportementales permettent d’obtenir des recommandations optimisées par l’IA, des expériences personnalisées et des fonctionnalités de recherche intelligentes.

## Conditions préalables {#prerequisites}

Avant d’installer l’extension, vérifiez que vous disposez d’un compte [!DNL Algolia] avec un accès à l’[!DNL Insights API]. Si vous ne disposez pas d’un compte , [inscrivez-vous](https://dashboard.algolia.com/users/sign_up) et activez l’accès à l’API .

Assurez-vous également de comprendre comment utiliser le [!DNL Insights API] [!DNL Algolia]. Pour obtenir un aperçu sur l’envoi d’événements, reportez-vous à la section [Envoi d’événements avec l’API Insights](https://www.algolia.com/doc/guides/sending-events/getting-started/).

Rassemblez les valeurs suivantes à partir du tableau de bord de votre compte [!DNL Algolia] :
- **[!UICONTROL ID de l’application]**
- **[!UICONTROL Clé API de recherche]**
- **[!UICONTROL Nom de l’index]**

## Installation l’extension {#install}

Pour installer l’extension [!DNL Algolia], procédez comme suit :

Accédez à **[!UICONTROL Collecte de données]** dans [!DNL Adobe Experience Platform]. Sélectionnez l’onglet **[!UICONTROL Extensions]**.

Ouvrez le **[!UICONTROL Catalogue]** et recherchez l’extension **[!UICONTROL Transfert d’événement Algolia]**, puis sélectionnez **[!UICONTROL Installer]**.

![Processus d’installation de l’extension Transfert d’événement Algolia dans Adobe Experience Platform](../../../images/extensions/server/algolia/install-extension.png)

### Configurez l’extension {#configure-extension}

Pour configurer l’extension de transfert d’événement [!DNL Algolia], accédez à l’onglet **[!UICONTROL Extensions]**, sélectionnez l’extension **[!UICONTROL Algolia]**, puis sélectionnez **[!UICONTROL Configurer]**.

![Écran de configuration de l’extension de transfert d’événement Algolia dans Adobe Experience Platform](../../../images/extensions/server/algolia/configure.png)

| Propriété | Description |
|----------|-------------|
| **[!UICONTROL ID de l&#39;application]** | Saisissez l’[!UICONTROL ID d’application] qui se trouve dans le tableau de bord Algolia sous la section [Clés API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Clé API de recherche]** | Saisissez la [!UICONTROL clé API de recherche] qui se trouve dans le tableau de bord Algolia sous la section [clés API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Nom de l’index]** | Saisissez le [!UICONTROL Nom de l’index] qui contient vos produits ou votre contenu. Cet index est utilisé comme valeur par défaut. |

{style="table-layout:auto"}

## [!DNL Algolia] types d’action d’extension de transfert d’événement {#action-types}

L’extension de transfert d’événement [!DNL Algolia] propose un type d’action unique qui peut être utilisé dans la section **[!UICONTROL Then]** d’une règle :

### Événement d’envoi {#send-event}

Configurez l’action **[!UICONTROL Envoyer l’événement]** pour transférer les événements vers [!DNL Algolia] :

Sélectionnez **[!UICONTROL Règles]** > **[!UICONTROL Ajouter une règle]** ou sélectionnez une règle existante. Dans la partie **[!UICONTROL Alors]** de la règle, ajoutez une action et sélectionnez **[!UICONTROL Extension]** : [!DNL Algolia] Transfert d’événement > **[!UICONTROL Type d’action]** : **[!UICONTROL Envoyer des événements]**.

![Configuration de l’action Envoyer l’événement dans l’extension de transfert d’événement Algolia.](../../../images/extensions/server/algolia/send-event.png)

## Implémenter le groupe de champs d’événement [!DNL Algolia] {#algolia-field-group}

Veillez à ajouter le groupe de champs d’événement [!DNL Algolia] à votre schéma avant d’utiliser l’extension de transfert d’événement [!DNL Algolia]. Il s’agit de l’un des groupes de champs standard fournis par Experience Platform.

![Configuration du groupe de champs d’événement en Algérie](../../../images/extensions/server/algolia/algolia-field-groups.png)

### Ajoutez le groupe de champs d’événement [!DNL Algolia] à votre schéma {#add-algolia-field-group}

Pour ajouter le groupe de champs d’événement [!DNL Algolia] :

Accédez à **[!UICONTROL Schémas]** et sélectionnez **[!UICONTROL Parcourir]**.

Ajoutez un nouveau schéma ou mettez à jour un schéma existant que vous utilisez pour envoyer des événements web et passez la souris sur l’icône **[!UICONTROL Ajouter]**. Saisissez *[!DNL Algolia]* dans la zone de recherche pour affiner les résultats.

Sélectionnez le bouton **[!DNL Algolia]les détails de l’événement** groupe de champs > **[!UICONTROL Ajouter un groupe de champs]** > **[!UICONTROL Enregistrer]**.

![Configuration du groupe de champs de profil Algolia dans Experience Platform](../../../images/extensions/server/algolia/algolia-profile-field-group.png)

### Mapper et envoyer des données à l’aide de la balise [!UICONTROL Collecte de données]

L’extension de transfert d’événement [!DNL Algolia] peut être utilisée avec la **[!DNL Adobe Experience Platform Web SDK]** pour envoyer des données de votre site web à [!DNL Algolia]. Pour ce faire, créez une propriété de balise, mappez les données à l’objet [!DNL XDM] et configurez des règles pour envoyer des événements.

#### Étape 1 : création d’une propriété de balise avec le SDK web

1. Créez une propriété de balise.
2. Installez l’extension [!DNL Adobe Experience Platform Web SDK].
3. Utilisez cette extension pour mapper les données d’HTML au groupe de champs **[!DNL Algolia]Event**.

![Exemple de jeu de données HTML mappé au groupe de champs d’événement Algolia](../../../images/extensions/server/algolia/html-dataset.png)

#### Étape 2 : créer un élément de données pour [!DNL XDM] mappage

1. Créez un [!UICONTROL élément de données] à l’aide du **[!DNL Adobe Experience Platform Web SDK]** .
2. Sélectionnez **[!UICONTROL objet XDM]** comme type d’élément de données.
3. Mappez vos données aux champs de [!DNL XDM] appropriés en veillant à ce que les champs spécifiques à [!DNL Algolia] soient renseignés.

![](../../../images/extensions/server/algolia/xdm-mapping.png)

#### Étape 3 : créer une règle pour envoyer des événements

1. Créez une règle dans la propriété de balise.
2. Ajoutez les déclencheurs d’événement requis tels que le chargement de page ou les événements de clic.
3. Ajoutez une action à l’aide de **[!DNL Adobe Experience Platform Web SDK]**.
4. Sélectionnez **[!UICONTROL Envoyer l’événement]** comme type d’action.
5. Configurez l’action pour utiliser l’élément de données [!DNL XDM].

![Exemple de configuration d’une action de règle dans l’extension de transfert d’événement Algolia](../../../images/extensions/server/algolia/rule-action.png)

#### Étape 4 : publier et tester

1. Publiez les règles et les modifications d’extension dans votre environnement cible.
2. Utilisez le [!DNL Adobe Experience Platform Debugger] pour vérifier que les données sont envoyées à Adobe Experience Platform et transférées à [!DNL Algolia].

![Configurer une règle pour envoyer des événements à l’aide de l’extension Algolia](../../../images/extensions/server/algolia/adobe-debugger.png)

### Vérifier les événements dans [!DNL Algolia]

Après avoir configuré l’extension de transfert d’événement [!DNL Algolia], vous pouvez vérifier que les événements sont correctement envoyés et reçus en procédant comme suit :

Accédez à votre tableau de bord [!DNL Algolia] et accédez à **[!UICONTROL Sources de données > Événements > Débogueur]**.

Sélectionnez l’événement correspondant à l’événement envoyé à partir de l’extension de transfert d’événement de [!DNL Algolia] et vérifiez que les données attendues sont présentes dans l’événement.

![Vérifier les événements dans le débogueur Algolia](../../../images/extensions/server/algolia/algolia-debugger.png)

## Scénarios d’implémentation courants

Utilisez l’extension de transfert d’événement [!DNL Algolia] pour capturer et envoyer des données d’interaction utilisateur pour divers cas d’utilisation, ce qui améliore la pertinence et la personnalisation des recherches.

### Suivi des vues de produit ou de contenu

Utilisez l’extension pour suivre le moment où les utilisateurs consultent les pages de produit ou de contenu, ce qui [!DNL Algolia] aide à comprendre les intérêts des utilisateurs.

### Suivi des événements de conversion

Effectuez le suivi des événements d’ajout au panier, des achats et d’autres événements de conversion pour optimiser les recommandations de [!DNL Algolia] optimisées par l’IA.

## Résolution des problèmes

Si vous rencontrez des problèmes lors de l’implémentation de l’extension de transfert d’événement [!DNL Algolia], tenez compte des étapes de dépannage suivantes :

### Les événements n’apparaissent pas dans les [!DNL Algolia]

Si les événements n’apparaissent pas dans [!DNL Algolia], vérifiez les points suivants :

- **Vérification des informations d’identification de l’API** : assurez-vous que le **[!UICONTROL ID d’application]** et la **[!UICONTROL Clé d’API]** correspondent aux valeurs de votre tableau de bord [!DNL Algolia].
- **Vérifier le débogueur d’événement** : utilisez le débogueur d’événement [!DNL Algolia] pour confirmer si des événements sont reçus. Dans le cas contraire, vérifiez la configuration de la règle de transfert d’événement.
- **Inspecter le mappage XDM** : assurez-vous que tous les champs obligatoires du schéma [!DNL Algolia] sont correctement mappés dans l’objet [!DNL XDM].

### Données d’événement incorrectes

- Assurez-vous que l’élément de données de l’objet de [!DNL XDM] est mappé précisément au schéma [!DNL Algolia], avec tous les champs obligatoires.
- Vérifiez que les paramètres d’événement correspondent au format et à la structure attendus décrits dans la documentation de l’API Insights d’[!DNL Algolia].

## Étapes suivantes

Ce guide explique comment envoyer des données aux [!DNL Algolia] à l’aide de l’[!DNL Algolia Event Forwarding Extension] . Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).

Pour plus d’informations sur le débogage de votre implémentation à l’aide du débogueur Experience Platform et de l’outil de surveillance du transfert d’événement, lisez la [présentation d’Adobe Experience Platform Debugger](../../../../debugger/home.md) et [Surveiller les activités dans le transfert d’événement](../../../ui/event-forwarding/monitoring.md).

## Ressources supplémentaires

- [[!DNL Algolia]  Documentation de l’API Insights &#x200B;](https://www.algolia.com/doc/rest-api/insights/)
- [[!DNL Algolia] Documentation sur les événements](https://www.algolia.com/doc/guides/sending-events/getting-started/)
- [[!DNL Adobe Experience Platform] Documentation sur le transfert d’événement](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=fr)
- [[!DNL Algolia] Présentation des fonctionnalités de l’IA](https://www.algolia.com/products/ai-search/)
