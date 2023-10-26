---
title: Extension de transfert d’événement de l’API Conversions liées
description: Cette extension de transfert d’événement Adobe Experience Platform vous permet de mesurer les performances de votre campagne marketing Linkedin.
last-substantial-update: 2023-10-25T00:00:00Z
source-git-commit: e1ed18aa79abae70974df1845c211a00390ecca4
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 4%

---

# Extension de l’API de conversions [!DNL LinkedIn]

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) est un outil de suivi des conversions qui crée une connexion directe entre les données marketing du serveur d’un annonceur et [!DNL LinkedIn]. Cela permet aux annonceurs d’évaluer l’efficacité de leurs [!DNL LinkedIn] campagnes marketing, quel que soit l’emplacement de la conversion, et utilisez ces informations pour optimiser les campagnes. La variable [!DNL LinkedIn Conversions API] l’extension peut contribuer à améliorer les performances et à réduire le coût par action grâce à une attribution plus complète, une meilleure fiabilité des données et une meilleure diffusion optimisée.

## Conditions préalables {#prerequisites}

Vous devez créer une règle de conversion dans votre [!DNL LinkedIn] compte publicités de campagne. [!DNL Adobe] recommande d’inclure &quot;CAPI&quot; au début du nom de la règle de conversation pour la différencier des autres types de règles de conversion que vous avez peut-être configurés.

### Créer un secret et un élément de données

Créer [!DNL LinkedIn] [secret de transfert d’événement](../../../ui/event-forwarding/secrets.md) et indiquez-lui un nom unique qui signifie membre d’authentification. Elle sera utilisée pour authentifier la connexion à votre compte tout en conservant la valeur en sécurité.

Ensuite, [créer un élément de données ;](../../../ui/managing-resources/data-elements.md#create-a-data-element) en utilisant la variable [!UICONTROL Core] et une [!UICONTROL Secret] type d’élément de données pour référencer la variable `LinkedIn` secret que vous venez de créer.

## Installez et configurez le [!DNL LinkedIn] extension {#install}

Pour installer l’extension, [création d’une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou sélectionnez une propriété existante à modifier.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans le **[!UICONTROL Catalogue]** , sélectionnez l’onglet **[!UICONTROL LinkedIn]** extension , puis sélectionnez **[!UICONTROL Installer]**.

![Le catalogue d’extensions affichant la variable [!DNL LinkedIn] installation de mise en surbrillance de la carte d’extension.](../../../images/extensions/server/linkedin/install-extension.png)

Dans l’écran suivant, saisissez le secret de l’élément de données que vous avez créé précédemment dans le champ `Access Token` champ . Le secret de l’élément de données contiendra votre [!DNL LinkedIn] Jeton OAuth 2. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![La variable [!DNL LinkedIn] page de configuration de l’extension avec la fonction [!UICONTROL Jeton d’accès] champ et [!UICONTROL Enregistrer] surlignée.](../../../images/extensions/server/linkedin/configure-extension.png)

## Créez un [!DNL Send Conversion] règle {#tracking-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL LinkedIn].

Création d’un transfert d’événement [règle](../../../ui/managing-resources/rules.md) dans la propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL LinkedIn]**. Ensuite, sélectionnez **[!UICONTROL Envoyer la conversion web]** pour le **[!UICONTROL Type d’action]**.

![La vue Règles de propriété de transfert d’événement , avec les champs requis pour ajouter une configuration d’action de règle de transfert d’événement mise en surbrillance.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Une fois la sélection effectuée, d’autres commandes s’affichent pour configurer davantage l’événement. Sélectionner **[!UICONTROL Conserver les modifications]** pour enregistrer la règle.

**[!UICONTROL Données utilisateur]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL E-mail.] | Adresse électronique du contact associé à l’événement de conversion. La valeur de l’email sera encodée par le code d’extension dans SHA256, sauf si la valeur fournie est déjà une chaîne SHA256. |
| [!UICONTROL UUID de suivi des publicités propriétaires linkedIn] | Il s’agit d’un identifiant de cookie propriétaire. Les annonceurs doivent activer le suivi de conversion amélioré à partir de [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) afin d’activer les cookies propriétaires qui ajoutent un paramètre d’identifiant de clic `li_fat_id` aux URL de clic. |
| [!UICONTROL Données sur le client] | Ce champ contient un objet JSON avec des attributs supplémentaires qui seront envoyés avec le message.<br><br>Sous , **[!UICONTROL Brut]** , vous pouvez coller l’objet JSON directement dans le champ de texte fourni ou sélectionner l’icône d’élément de données (![Icône Jeu de données](../../../images/extensions/server/aws/data-element-icon.png)) pour effectuer une sélection dans une liste d’éléments de données existants afin de représenter les données.<br><br>Vous pouvez également utiliser la variable **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur via un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. Les valeurs de clé acceptées sont les suivantes : `firstName`, `lastName`, `companyName`, `title` et `country`. |

{style="table-layout:auto"}

![La variable [!DNL User Data] section présentant des exemples de saisie de données dans les champs.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Données de conversion]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Conversion] | L’identifiant de la règle de conversion créée dans [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171) ou [!DNL LinkedIn Campaign Manager]. |
| [!UICONTROL Temps de conversion] | Horodatage en millisecondes au cours duquel l’événement de conversion s’est produit. <br><br> Remarque : Si votre source enregistre l’horodatage de conversion en secondes, insérez 000 à la fin pour le transformer en millisecondes. |
| [!UICONTROL Devise] | Code de devise au format ISO. |
| [!UICONTROL Quantité] | Valeur de la conversion dans la chaîne décimale (par exemple, &quot;100.05&quot;). |
| [!UICONTROL Identifiant d’événement] | Identifiant unique généré par les annonceurs pour indiquer chaque événement. Il s’agit d’un champ facultatif qui est utilisé pour le dédoublonnage. |

{style="table-layout:auto"}

![La variable [!DNL Conversion Data] pour afficher des exemples de données dans les champs.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Remplacements de configuration]**

>REMARQUE
>
>La variable [!UICONTROL Remplacements de configuration] permet à un utilisateur de définir une variable [!DNL LinkedIn] jeton d’accès sur chaque règle, permettant à chaque règle d’utiliser un jeton d’accès pouvant avoir accès à différents [!DNL LinkedIn] comptes publicitaires.

| Entrée | Description |
| --- | --- |
| [!UICONTROL Jeton d’accès] | La variable [!DNL LinkedIn] jeton d’accès. |

![La variable [!DNL Configuration Overrides] section présentant des exemples de saisie de données dans le champ.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL LinkedIn] en utilisant la variable [!DNL LinkedIn Conversions API] extension de transfert d’événement. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], reportez-vous au [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).
