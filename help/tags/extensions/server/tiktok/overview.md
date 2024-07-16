---
title: Intégration de l’extension de l’API des événements web Adobe TikTok
description: Cette API d’événements web Adobe Experience Platform vous permet de partager des interactions web directement avec TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 4%

---

# [!DNL TikTok] présentation de l’extension de l’API des événements web

L&#39;API d&#39;événements [!DNL TikTok] est une interface sécurisée [API de serveur Edge Network](/help/server-api/overview.md) qui vous permet de partager des informations avec [!DNL TikTok] directement sur les actions des utilisateurs sur vos sites web. Vous pouvez utiliser les règles de transfert d’événement pour envoyer des données de [!DNL Adobe Experience Platform Edge Network] vers [!DNL TikTok] à l’aide de l’extension de l’API [!DNL TikTok] d’événements web.

## Conditions préalables de [!DNL TikTok] {#prerequisites}

Pour configurer l’API d’événements web [!DNL TikTok] afin d’utiliser l’API d’événements [!DNL TikTok], vous devez générer un code de pixel et un jeton d’accès [!DNL TikTok].

Vous devez disposer d’un [!DNL TikTok] valide pour le compte professionnel afin de créer un pixel [!DNL TikTok] à l’aide de la configuration du partenaire. Accédez à la [[!DNL TikTok] page d&#39;enregistrement professionnel](https://www.tiktok.com/business/en-US/solutions/business-account) pour vous enregistrer et créer un compte si vous n&#39;en avez pas déjà un.

Vous devez être connecté à votre compte d’entreprise pour configurer [!DNL TikTok] pixel à l’aide de la configuration du partenaire. Pour ce faire, procédez comme suit :

1. Accédez à l’onglet **[!UICONTROL Assets]** et sélectionnez **[!UICONTROL Event]**.
2. Sous Événements Web, sélectionnez **[!UICONTROL Gérer]**.
3. Sélectionnez **[!UICONTROL Configurer des événements web]**.
4. Sélectionnez **[!UICONTROL Configuration de partenaire]** comme méthode de connexion.

Pour plus d’informations sur la configuration du pixel [!DNL TikTok], consultez le guide [Prise en main du pixel](https://ads.tiktok.com/help/article/get-started-pixel) .

Vous pouvez générer un jeton d’accès une fois que le pixel a été créé. Pour ce faire, accédez au pixel et sélectionnez l’onglet **[!UICONTROL Paramètres]**. Sous l’API Events, sélectionnez **[!UICONTROL Generate Access Token]**.

Consultez le [[!DNL TikTok] guide de prise en main](https://business-api.tiktok.com/portal/docs?id=1739584855420929) pour plus d’informations sur la configuration du code de pixel et du jeton d’accès.

## Installation et configuration de l’extension de l’API d’événements web [!DNL TikTok] {#install}

Pour installer l’extension, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalog]**, sélectionnez l’ **[!UICONTROL extension de l’API TikTok Web Events]** , puis sélectionnez **[!UICONTROL Install]**.

![Le catalogue d’extensions présentant l’installation de mise en surbrillance de la carte d’extension [!DNL TikTok].](../../../images/extensions/server/tiktok/install-extension.png)

Dans l’écran suivant, saisissez les valeurs de configuration suivantes que vous avez générées à partir du gestionnaire d’annonces [!DNL TikTok] :

* **[!UICONTROL Code pixel]**
* **[!UICONTROL Jeton d’accès]**

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

Écran de configuration ![[!DNL TikTok] pour l’extension de l’API [!DNL TikTok] d’événements web.](../../../images/extensions/server/tiktok/configure.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL TikTok].

Créez une [règle](../../../ui/managing-resources/rules.md) dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Extension de l’API des événements web TikTok]**. Pour envoyer des événements Edge Network à [!DNL TikTok], définissez le **[!UICONTROL Type d’action]** sur **.**

![ Le type d’action [!UICONTROL Envoyer l’événement API des événements web TikTok] sélectionné pour une règle [!DNL TikTok] dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/tiktok/select-action.png)

Après la sélection, d’autres contrôles apparaissent pour configurer l’événement de manière plus détaillée, comme indiqué ci-dessous. Une fois la règle terminée, sélectionnez **[!UICONTROL Conserver les modifications]** pour enregistrer la règle.

**[!UICONTROL Événements et paramètres web]**

Les événements web et les paramètres contiennent des informations générales sur l’événement. Les événements standard sont pris en charge dans les outils d’intégration [!DNL TikTok] et peuvent être utilisés pour la création de rapports , l’optimisation pour les conversions et la création d’audiences.

| Entrée | Description |
| --- | --- |
| Nom de l’événement | Nom de l’événement. Il s’agit d’actions avec des noms prédéfinis créés par [!DNL TikTok] et il s’agit d’un champ obligatoire. Pour plus d’informations sur les événements pris en charge, consultez la documentation [[!DNL TikTok] API marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777) . |
| Heure de l’événement | Date-time sous la forme d’une chaîne au format ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. Il s’agit d’un champ obligatoire. |
| Identifiant d’événement | Identifiant unique généré par les annonceurs pour indiquer chaque événement. Il s’agit d’un champ facultatif qui est utilisé pour le dédoublonnage. |

{style="table-layout:auto"}

![La section [!DNL Web Events and Parameters] présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Paramètres de contexte utilisateur]**

Les paramètres de contexte utilisateur contiennent des informations sur le client qui sont utilisées pour faire correspondre les événements de visiteur web avec les utilisateurs [!DNL TikTok]. L’inclusion de plusieurs types de données correspondantes vous permet d’accroître la précision des modèles de ciblage et d’optimisation.

| Entrée | Description |
| --- | --- |
| Adresse IP | Adresse IP publique du navigateur non hachée. La prise en charge des adresses IPv4 et IPv6 est assurée. Les formes complètes et compressées des adresses IPv6 sont reconnues. |
| Agent utilisateur | Agent utilisateur non haché de l’appareil de l’utilisateur. |
| E-mail | Adresse électronique du contact associé à l’événement de conversion. |
| Téléphone | Le numéro de téléphone doit être au format E164 [+][code pays][code zone][local phone number] avant le hachage. |
| ID de cookie | Si vous utilisez Pixel SDK, un identifiant unique est automatiquement enregistré dans le cookie `_ttp`, si les cookies sont activés. La valeur `_ttp` peut être extraite et utilisée pour ce champ. |
| Identifiant externe | Tout identifiant unique, tel que les identifiants d’utilisateur, les identifiants de cookie externe, etc., doit être haché avec SHA256. |
| TikTok Click ID | `ttclid` ajouté à l’URL de la page d’entrée chaque fois qu’une publicité est sélectionnée sur [!DNL TikTok]. |
| Page URL (URL de la page) | URL de la page au moment de l’événement. |
| URL du référent de page | URL du référent de la page. |

{style="table-layout:auto"}

![La section [!DNL User Context Parameters] présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Paramètres de propriétés]**

Utilisez les paramètres de propriétés pour configurer d’autres propriétés prises en charge.

| Entrée | Description |
| --- | --- |
| Price | Le coût d’un seul article. |
| Quantité | Nombre d’éléments achetés dans l’événement. Il doit s’agir d’un nombre positif supérieur à 0. |
| Type de contenu | Une valeur `product` ou `product_group` doit être affectée à la propriété d’objet content_type , selon la manière dont vous allez configurer votre flux de données lors de la configuration de votre catalogue de produits. |
| Identifiant de contenu | Identifiant unique de l’élément de produit. |
| Catégorie de contenu | Catégorie de la page/du produit. |
| Nom du contenu | Nom de la page/du produit. |
| Devise | Devise des éléments achetés dans l’événement. Cela est exprimé dans la norme ISO-4217. |
| Valeur | Le prix total de la commande. Cette valeur sera égale au prix * quantity. |
| Description | Description de l’élément ou de la page. |
| Requête | Chaîne de texte utilisée pour rechercher un produit. |
| Statut | État d’une commande, d’un article ou d’un service. Par exemple, &quot;Envoyé&quot;. |

{style="table-layout:auto"}

![La section [!DNL Properties Parameters] présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Déduplication des événements {#deduplication}

[!DNL TikTok] pixel devra être configuré pour la déduplication si vous utilisez le SDK [!DNL TikTok] pixel et l’extension d’API d’événements web [!DNL TikTok] pour envoyer les mêmes événements à [!DNL TikTok].

La déduplication n’est pas nécessaire si des types d’événements distincts sont envoyés du client et du serveur sans chevauchement. Pour vous assurer que vos rapports n’ont pas d’impact négatif, vous devez vous assurer que tout événement unique partagé par le SDK [!DNL TikTok] pixel et l’extension de l’API d’événements web [!DNL TikTok] est dédupliqué.

Lors de l’envoi d’événements partagés, assurez-vous que chaque événement comprend un ID de pixel, un ID d’événement et un nom. Les événements dupliqués qui arrivent dans les cinq minutes seront fusionnés. Si le champ de données était absent du premier événement, il sera combiné à l’événement suivant. Les événements en double reçus sous 48 heures seront supprimés.

Pour plus d’informations sur ce processus, consultez la documentation [!DNL TikTok] sur [Déduplication des événements](https://ads.tiktok.com/help/article/event-deduplication) .

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL TikTok] à l’aide de l’extension d’API d’événements web [!DNL TikTok]. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
