---
title: Intégration de l’extension d’API d’événements web Adobe TikTok
description: Cette API d’événements web Adobe Experience Platform vous permet de partager des interactions de site web directement avec TikTok.
last-substantial-update: 2023-09-26T00:00:00.000Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
TQID: https://experienceleague.adobe.com/X5swX7MnFvVXFQ8AYGKWZpSOAZppvknnXPldZMOs83c
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: e43347a8-f2c5-4aa4-8623-6f13875d7e3aid: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: e08599ea-8888-4294-ba74-3ba0a7762a46id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: ae2cba0e-54f2-464b-a3b3-ad371e8a886aid: b64298cc-90cc-46b7-8917-ee391f1c7516id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1cid: f6ff4d13-7b5c-4533-8556-95e76673d4cbid: f9a2105e-7a47-4e85-9193-31a519a2cb83
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 74579d9ca311b241313a3d89b564f217cd3476c7
workflow-type: tm+mt
source-wordcount: 1147
ht-degree: 4%

---

# Présentation de l’extension d’API d’événements web [!DNL TikTok]

L’API d’événements [!DNL TikTok] est une interface sécurisée de l’[API Edge Network](https://developer.adobe.com/data-collection-apis/docs/) qui vous permet de partager des informations avec [!DNL TikTok] directement sur les actions des utilisateurs et utilisatrices sur vos sites web. Vous pouvez tirer parti des règles de transfert d’événement pour envoyer des données du [!DNL Adobe Experience Platform Edge Network] à [!DNL TikTok] à l’aide de l’extension d’API d’événements web [!DNL TikTok].

## Conditions préalables de [!DNL TikTok] {#prerequisites}

Pour configurer l’API d’événements web [!DNL TikTok] afin d’utiliser l’API d’événements [!DNL TikTok], vous devez générer un code de pixel [!DNL TikTok] et un jeton d’accès.

Vous devez disposer d’un [!DNL TikTok] valide pour le compte professionnel afin de créer un pixel d’[!DNL TikTok] à l’aide de la configuration du partenaire. Accédez à la page [[!DNL TikTok] pour l’enregistrement des entreprises](https://www.tiktok.com/business/en-US/solutions/business-account) pour vous enregistrer et créer un compte si vous n’en avez pas déjà un.

Vous devez être connecté à votre compte professionnel pour configurer [!DNL TikTok] Pixel à l’aide de la configuration du partenaire. Pour ce faire, procédez comme suit :

1. Accédez à l’onglet **** et sélectionnez **[!UICONTROL Événement]**.
2. Sous Événements web, sélectionnez **[!UICONTROL Gérer]**.
3. Sélectionnez **[!UICONTROL Configurer Des Événements Web]**.
4. Sélectionnez **[!UICONTROL Configuration du partenaire]** comme méthode de connexion.

Consultez le guide [Prise en main du pixel](https://ads.tiktok.com/help/article/get-started-pixel) pour plus d’informations sur la configuration du pixel [!DNL TikTok].

Vous pouvez générer un jeton d’accès une fois le pixel créé. Pour ce faire, accédez au pixel et sélectionnez l’onglet **[!UICONTROL Paramètres]**. Sous API d’événements, sélectionnez **[!UICONTROL Générer un jeton d’accès]**.

Pour plus d’informations sur la configuration du code de pixel et du jeton d’accès](https://business-api.tiktok.com/portal/docs?id=1739584855420929) consultez le [[!DNL TikTok]  guide de prise en main .

## Installer et configurer l’extension d’API d’événements web [!DNL TikTok] {#install}

Pour installer l’extension, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]**, sélectionnez l’extension d’API d’événements web TikTok **** puis sélectionnez **[!UICONTROL Installer]**.

![Catalogue d’extensions affichant la carte d’extension [!DNL TikTok] mettant en surbrillance install.](../../../images/extensions/server/tiktok/install-extension.png)

Dans l’écran suivant, saisissez les valeurs de configuration suivantes que vous avez précédemment générées à partir d’[!DNL TikTok] Ads Manager :

* **[!UICONTROL Code pixel]**
* **[!UICONTROL Jeton d’accès]**

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![[!DNL TikTok] de configuration de l’extension d’API d’événements web [!DNL TikTok].](../../../images/extensions/server/tiktok/configure.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL TikTok].

Créez une [règle](../../../ui/managing-resources/rules.md) dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Extension de l’API d’événements web TikTok]**. Pour envoyer des événements Edge Network à [!DNL TikTok], définissez le **[!UICONTROL Type d’action]** sur **[!UICONTROL Envoyer un événement d’API d’événements web TikTok].**

![Type d’action [!UICONTROL Envoyer un événement d’API d’événements web TikTok] sélectionné pour une règle de [!DNL TikTok] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/tiktok/select-action.png)

Après la sélection, des commandes supplémentaires apparaissent pour configurer plus en détail l’événement, comme indiqué ci-dessous. Une fois l’opération terminée, sélectionnez **[!UICONTROL Conserver les modifications]** pour enregistrer la règle.

**[!UICONTROL Événements et paramètres Web]**

Les événements et paramètres Web contiennent des informations générales sur l&#39;événement. Les événements standard sont pris en charge dans [!DNL TikTok] outils d’intégration et peuvent être utilisés pour créer des rapports , optimiser les conversions et créer des audiences.

| Entrée | Description |
| --- | --- |
| Nom de l’événement | Nom de l’événement. Il s’agit d’actions avec des noms prédéfinis créées par [!DNL TikTok] et qui constituent un champ obligatoire. Pour plus d’informations sur les événements pris en charge, consultez la documentation de l’[[!DNL TikTok] API marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777). |
| Heure de l’événement | Date et heure sous forme de chaîne au format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) ou au format `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. Ce champ est obligatoire. |
| Identifiant d’événement | Identifiant unique généré par les annonceurs pour indiquer chaque événement. Il s’agit d’un champ facultatif qui est utilisé pour la déduplication. |

{style="table-layout:auto"}

![Section [!DNL Web Events and Parameters] présentant un exemple de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Paramètres de contexte utilisateur]**

Les paramètres de contexte utilisateur contiennent des informations sur le client qui sont utilisées pour faire correspondre les événements du visiteur web aux utilisateurs [!DNL TikTok]. L’inclusion de plusieurs types de données correspondantes vous permet d’accroître la précision des modèles de ciblage et d’optimisation.

| Entrée | Description |
| --- | --- |
| Adresse IP | Adresse IP publique non hachée du navigateur. La prise en charge est fournie pour les adresses IPv4 et IPv6. Les formes complètes et compressées des adresses IPv6 sont reconnues. |
| Agent utilisateur | Agent utilisateur non haché à partir de l’appareil de l’utilisateur. |
| E-mail | Adresse e-mail du contact associé à l’événement de conversion. |
| Téléphone | Le numéro de téléphone doit être au format E164 `[+][country code][area code][local phone number]` avant hachage. |
| ID de cookie | Si vous utilisez Pixel SDK, un identifiant unique est automatiquement enregistré dans le cookie `_ttp`, si les cookies sont activés. La valeur `_ttp` peut être extraite et utilisée pour ce champ. |
| Identifiant externe | Tout identifiant unique tel que les identifiants d’utilisateur, les identifiants de cookie externe, etc. doit être haché avec SHA256. |
| ID de clic TikTok | `ttclid` qui est ajoutée à l’URL de la page de destination chaque fois qu’une publicité est sélectionnée sur [!DNL TikTok]. |
| Page URL (URL de la page) | URL de la page au moment de l’événement. |
| URL du référent de page | URL du référent de la page. |

{style="table-layout:auto"}

![Section [!DNL User Context Parameters] présentant un exemple de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Paramètres des propriétés]**

Utilisez les paramètres de propriétés pour configurer d’autres propriétés prises en charge.

| Entrée | Description |
| --- | --- |
| Price | Coût d’un seul article. |
| Quantité | Nombre d’articles achetés dans l’événement. Il doit s&#39;agir d&#39;un nombre positif supérieur à 0. |
| Type de contenu | Une valeur de `product` ou `product_group` doit être affectée à la propriété d’objet content_type, selon la manière dont vous allez configurer votre flux de données lors de la configuration de votre catalogue de produits. |
| Identifiant du contenu | Identifiant unique de l’élément de produit. |
| Catégorie de contenu | Catégorie de la page/du produit. |
| Nom du contenu | Nom de la page/du produit. |
| Devise | Devise des articles achetés dans l’événement. Cette valeur est exprimée en ISO-4217. |
| Valeur | Prix total de la commande. Cette valeur sera égale au prix * quantité. |
| Description | Description de l’élément ou de la page. |
| Requête | Chaîne de texte utilisée pour rechercher un produit. |
| Statut | Statut d&#39;une commande, d&#39;un article ou d&#39;un service. Par exemple, « envoyé ». |

{style="table-layout:auto"}

![Section [!DNL Properties Parameters] présentant un exemple de saisie de données dans les champs.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Déduplication des événements {#deduplication}

[!DNL TikTok] pixel doit être configuré pour la déduplication si vous utilisez le SDK de pixel [!DNL TikTok] et l’extension d’API d’événements web [!DNL TikTok] pour envoyer les mêmes événements à [!DNL TikTok].

La déduplication n’est pas requise si des types d’événements distincts sont envoyés depuis le client et le serveur sans chevauchement. Pour vous assurer que vos rapports ne sont pas affectés négativement, vous devez vous assurer que tout événement unique partagé par le [!DNL TikTok] pixel SDK et l’extension d’API d’événements web [!DNL TikTok] est dédupliqué.

Lors de l’envoi d’événements partagés, assurez-vous que chaque événement comprend un identifiant de pixel, un identifiant d’événement et un nom. Les événements dupliqués qui arrivent à moins de cinq minutes les uns des autres seront fusionnés. Si le champ de données était absent du premier événement, il sera combiné avec l’événement suivant. Tous les événements en double reçus dans les 48 heures seront supprimés.

Pour plus d’informations sur ce processus, consultez la documentation [!DNL TikTok] sur la [déduplication des événements](https://ads.tiktok.com/help/article/event-deduplication).

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL TikTok] à l’aide de l’extension d’API d’événements web [!DNL TikTok]. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], reportez-vous à la section [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
