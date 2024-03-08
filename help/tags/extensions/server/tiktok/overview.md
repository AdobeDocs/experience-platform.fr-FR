---
title: Intégration de l’extension de l’API des événements web Adobe TikTok
description: Cette API d’événements web Adobe Experience Platform vous permet de partager des interactions web directement avec TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 5%

---

# [!DNL TikTok] présentation de l’extension de l’API des événements web

La variable [!DNL TikTok] API events est sécurisée. [API du serveur réseau Edge](/help/server-api/overview.md) qui vous permet de partager des informations avec [!DNL TikTok] à propos directement des actions des utilisateurs sur vos sites web. Vous pouvez utiliser les règles de transfert d’événement pour envoyer des données à partir de la variable [!DNL Adobe Experience Platform Edge Network] to [!DNL TikTok] en utilisant la variable [!DNL TikTok] Extension de l’API des événements web.

## Conditions préalables de [!DNL TikTok] {#prerequisites}

Pour configurer la variable [!DNL TikTok] API d’événements web pour utiliser [!DNL TikTok] API d’événements, vous devez générer une [!DNL TikTok] code pixel et jeton d’accès.

Vous devez disposer d’un [!DNL TikTok] pour un compte professionnel afin de créer une [!DNL TikTok] en utilisant la configuration du partenaire. Accédez au [[!DNL TikTok] page d’enregistrement professionnel](https://www.tiktok.com/business/en-US/solutions/business-account) pour enregistrer et créer un compte si vous n’en avez pas déjà un.

Vous devez être connecté à votre compte d’entreprise pour configurer [!DNL TikTok] Pixel utilisant la configuration du partenaire. Pour ce faire, procédez comme suit :

1. Accédez au **[!UICONTROL Ressources]** et sélectionnez **[!UICONTROL Événement]**.
2. Sous Événements Web, sélectionnez **[!UICONTROL Gérer]**.
3. Sélectionner **[!UICONTROL Configuration d’événements web]**.
4. Sélectionner **[!UICONTROL Configuration du partenaire]** comme méthode de connexion.

Voir [Prise en main de Pixel](https://ads.tiktok.com/help/article/get-started-pixel) pour plus d’informations sur la configuration de la variable [!DNL TikTok] pixel.

Vous pouvez générer un jeton d’accès une fois que le pixel a été créé. Pour ce faire, accédez au pixel et sélectionnez la propriété **[!UICONTROL Paramètres]** . Sous API d’événements, sélectionnez **[!UICONTROL Générer un jeton d’accès]**.

Voir [[!DNL TikTok] guide de prise en main](https://business-api.tiktok.com/portal/docs?id=1739584855420929) pour plus d’informations sur la configuration du code pixel et du jeton d’accès.

## Installez et configurez le [!DNL TikTok] extension de l’API des événements web {#install}

Pour installer l’extension, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans le **[!UICONTROL Catalogue]** , sélectionnez l’onglet **[!UICONTROL Extension de l’API des événements web TikTok]** puis sélectionnez **[!UICONTROL Installer]**.

![Le catalogue d’extensions affichant la variable [!DNL TikTok] installation de mise en surbrillance de la carte d’extension.](../../../images/extensions/server/tiktok/install-extension.png)

Dans l’écran suivant, saisissez les valeurs de configuration suivantes que vous avez générées précédemment à partir de [!DNL TikTok] Gestionnaire de publicités :

* **[!UICONTROL Code pixel]**
* **[!UICONTROL Jeton d’accès]**

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![[!DNL TikTok] écran de configuration pour la [!DNL TikTok] extension de l’API des événements web.](../../../images/extensions/server/tiktok/configure.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL TikTok].

Créer [règle](../../../ui/managing-resources/rules.md) dans la propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Extension de l’API des événements web TikTok]**. Pour envoyer des événements Edge Network à [!DNL TikTok], définissez la variable **[!UICONTROL Type d’action]** to **[!UICONTROL Envoi de l’événement de l’API des événements web TikTok].**

![La variable [!UICONTROL Envoi de l’événement de l’API des événements web TikTok] type d’action sélectionné pour un [!DNL TikTok] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/tiktok/select-action.png)

Après la sélection, d’autres contrôles apparaissent pour configurer l’événement de manière plus détaillée, comme indiqué ci-dessous. Une fois terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour enregistrer la règle.

**[!UICONTROL Événements et paramètres web]**

Les événements web et les paramètres contiennent des informations générales sur l’événement. Les événements standard sont pris en charge dans les [!DNL TikTok] outils d’intégration et peuvent être utilisés pour la création de rapports , l’optimisation pour les conversions et la création d’audiences.

| Entrée | Description |
| --- | --- |
| Nom de l’événement | Nom de l’événement. Il s’agit d’actions avec des noms prédéfinis créés par [!DNL TikTok] et est un champ obligatoire. Voir [[!DNL TikTok] API marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777) documentation pour plus d’informations sur les événements pris en charge. |
| Heure de l’événement | Date-time sous forme de chaîne dans ISO 8601 ou dans `yyyy-MM-dd'T'HH:mm:ss:SSSZ` format. Il s’agit d’un champ obligatoire. |
| Identifiant d’événement | Identifiant unique généré par les annonceurs pour indiquer chaque événement. Il s’agit d’un champ facultatif qui est utilisé pour le dédoublonnage. |

{style="table-layout:auto"}

![La variable [!DNL Web Events and Parameters] section présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Paramètres de contexte utilisateur]**

Les paramètres contextuels de l’utilisateur contiennent des informations sur le client utilisées pour faire correspondre les événements de visiteur web à [!DNL TikTok] utilisateurs. L’inclusion de plusieurs types de données correspondantes vous permet d’accroître la précision des modèles de ciblage et d’optimisation.

| Entrée | Description |
| --- | --- |
| Adresse IP | Adresse IP publique du navigateur non hachée. La prise en charge des adresses IPv4 et IPv6 est assurée. Les formes complètes et compressées des adresses IPv6 sont reconnues. |
| Agent utilisateur | Agent utilisateur non haché de l’appareil de l’utilisateur. |
| E-mail | Adresse électronique du contact associé à l’événement de conversion. |
| Téléphone | Le numéro de téléphone doit être au format E164 [+][code pays][code zone][local phone number] avant le hachage. |
| ID de cookie | Si vous utilisez Pixel SDK, un identifiant unique est automatiquement enregistré dans la variable `_ttp` , si les cookies sont activés. La variable `_ttp` peut être extraite et utilisée pour ce champ. |
| Identifiant externe | Tout identifiant unique, tel que les identifiants d’utilisateur, les identifiants de cookie externe, etc., doit être haché avec SHA256. |
| TikTok Click ID | La variable `ttclid` qui est ajouté à l’URL de la landing page chaque fois qu’une publicité est sélectionnée sur [!DNL TikTok]. |
| Page URL (URL de la page) | URL de la page au moment de l’événement. |
| URL du référent de page | URL du référent de la page. |

{style="table-layout:auto"}

![La variable [!DNL User Context Parameters] section présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Paramètres des propriétés]**

Utilisez les paramètres de propriétés pour configurer d’autres propriétés prises en charge.

| Entrée | Description |
| --- | --- |
| Prix | Le coût d’un seul article. |
| Quantité | Nombre d’éléments achetés dans l’événement. Il doit s’agir d’un nombre positif supérieur à 0. |
| Type de contenu | Une valeur de `product` ou `product_group` doit être affecté à la propriété d’objet content_type , selon la manière dont vous allez configurer votre flux de données lors de la configuration de votre catalogue de produits. |
| Identifiant de contenu | Identifiant unique de l’élément de produit. |
| Catégorie de contenu | Catégorie de la page/du produit. |
| Nom du contenu | Nom de la page/du produit. |
| Devise | Devise des éléments achetés dans l’événement. Cela est exprimé dans la norme ISO-4217. |
| Valeur | Le prix total de la commande. Cette valeur sera égale au prix * quantity. |
| Description | Description de l’élément ou de la page. |
| Requête | Chaîne de texte utilisée pour rechercher un produit. |
| Statut | État d’une commande, d’un article ou d’un service. Par exemple, &quot;Envoyé&quot;. |

{style="table-layout:auto"}

![La variable [!DNL Properties Parameters] section présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Déduplication des événements {#deduplication}

[!DNL TikTok] pixel doit être configuré pour le dédoublonnage si vous utilisez les [!DNL TikTok] SDK pixel et [!DNL TikTok] extension de l’API des événements web pour envoyer les mêmes événements à [!DNL TikTok].

La déduplication n’est pas nécessaire si des types d’événements distincts sont envoyés du client et du serveur sans chevauchement. Pour vous assurer que votre rapport n’a pas d’impact négatif, vous devez vous assurer que tout événement unique partagé par la variable [!DNL TikTok] SDK pixel et [!DNL TikTok] l’extension de l’API d’événements web est dédupliquée.

Lors de l’envoi d’événements partagés, assurez-vous que chaque événement comprend un ID de pixel, un ID d’événement et un nom. Les événements dupliqués qui arrivent dans les cinq minutes seront fusionnés. Si le champ de données était absent du premier événement, il sera combiné à l’événement suivant. Les événements en double reçus sous 48 heures seront supprimés.

Voir [!DNL TikTok] documentation sur [Déduplication d’événements](https://ads.tiktok.com/help/article/event-deduplication) pour plus d’informations sur ce processus.

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL TikTok] en utilisant la variable [!DNL TikTok] extension de l’API des événements web. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], reportez-vous au [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).
