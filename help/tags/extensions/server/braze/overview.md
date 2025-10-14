---
keywords: extension de transfert d’événement;ventilation;extension de transfert d’événement de ventilation
title: Extension de transfert d’événement de braze
description: Cette extension de transfert d’événement Adobe Experience Platform envoie les événements Edge Network à Brand.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 3%

---

# Extension de transfert d’événement [!DNL Braze Track Events API]

[[!DNL Braze]](https://www.braze.com) est une plateforme d’engagement client qui alimente les interactions centrées sur les clients entre les consommateurs et les marques en temps réel. En utilisant [!DNL Braze], vous pouvez effectuer les opérations suivantes :

- Diffusez des données (comme des messages marketing) à des utilisateurs ciblés en fonction de leurs préférences linguistiques, de leurs préférences d’emplacement, etc., afin d’augmenter les taux de conversion et de prendre en charge les principaux objectifs de l’entreprise.
- Envoyez aux clients des messages personnalisés sur plusieurs canaux, y compris des e-mails, des notifications push et des messages in-app, au bon moment et dans les langues de leur choix.
- Ciblez des utilisateurs spécifiques pour les campagnes marketing et promotionnelles afin d’augmenter le nombre de clients réguliers.
- Étudiez le comportement et les schémas des utilisateurs pour cibler des audiences spécifiques avec des messages personnalisés, ce qui peut contribuer à augmenter les recettes.

L’extension [!DNL Braze Track Events API] [de transfert d’événement](../../../ui/event-forwarding/overview.md) vous permet d’exploiter les données capturées dans l’Edge Network Adobe Experience Platform et de les envoyer à [!DNL Braze] sous la forme d’événements côté serveur à l’aide de l’API [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track).

Ce document couvre les cas d’utilisation de l’extension, comment l’installer dans vos bibliothèques de transfert d’événement et comment utiliser ses fonctionnalités dans un transfert d’événement [rule](../../../ui/managing-resources/rules.md).

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données de l’Edge Network dans [!DNL Braze] pour tirer parti de ses fonctionnalités d’analyse et de ciblage des clients.

Prenons l’exemple d’une entreprise de vente au détail présente sur plusieurs canaux (site web et mobile) et qui capture des entrées transactionnelles ou conversationnelles en tant que données d’événement de son site web et de ses plateformes mobiles. En utilisant diverses règles [tag](../../../home.md), ces données sont envoyées à l’Edge Network en temps réel. À partir de là, l’extension de transfert d’événement [!DNL Braze] envoie automatiquement les événements pertinents à [!DNL Braze] du côté serveur.

Une fois les données envoyées, les équipes d’analyse de l’entreprise peuvent alors exploiter les fonctionnalités [!DNL Braze's] pour traiter les jeux de données et obtenir des informations sur l’entreprise afin de générer des graphiques, des tableaux de bord ou d’autres visualisations pour informer les parties prenantes de l’entreprise. Consultez la page [[!DNL Braze] clients](https://www.braze.com/customers) pour plus d’informations sur les différents cas d’utilisation de la plateforme.

## [!DNL Braze] conditions préalables et barrières de sécurité {#prerequisites}

Vous devez disposer d’un compte [!DNL Braze] pour pouvoir utiliser ses technologies. Si vous ne disposez pas d’un compte, accédez à la [page de prise en main](https://www.braze.com/get-started/) sur [!DNL Braze] pour vous connecter à [!DNL Braze Sales] et lancer le processus de création de compte.

### Protections des API

L’extension utilise deux des API de [!DNL Braze] et leurs limites sont décrites ci-dessous :

| API | Limites de taux |
| --- | --- |
| [!DNL User Track] | 50 000 demandes par minute. <br> Pour plus d’informations, consultez la [[!DNL User Track] documentation de l’API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit). |
| [!DNL User Identify] | 20 000 demandes par minute. <br> Pour plus d’informations, consultez la [[!DNL User Identify] documentation de l’API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit). |

>[!NOTE]
>
> Pour plus d’informations sur les limites qu’elles imposent, consultez le guide sur les [[!DNL Braze] limites de l’API](https://www.braze.com/docs/api/api_limits/) .

### Points de données facturables

L’envoi d’attributs personnalisés supplémentaires à [!DNL Braze] peut augmenter la consommation de vos points de données [!DNL Braze]. Consultez votre gestionnaire de compte [!DNL Braze] avant d’envoyer des attributs personnalisés supplémentaires. Pour plus d’informations, consultez la documentation [!DNL Braze] sur les [&#x200B; points de données facturables](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable).

### Collecte des détails de configuration requis {#configuration-details}

Pour connecter l’Edge Network à [!DNL Braze], les entrées suivantes sont requises :

| Type de clé | Description | Exemple |
| --- | --- | --- |
| [!DNL Braze] Instance | Point de terminaison REST associé au compte [!DNL Braze]. Pour plus d&#39;informations, reportez-vous à la documentation [!DNL Braze] sur [instances](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) . | `https://rest.iad-03.braze.com` |
| Clé API | La clé d’API [!DNL Braze] associée au compte [!DNL Braze]. <br/>Reportez-vous à la documentation [!DNL Braze] sur la [clé API REST](https://www.braze.com/docs/api/basics/#rest-api-key) pour obtenir des conseils. | `YOUR-BRAZE-REST-API-KEY` |

### Créer un secret

Créez un nouveau secret de transfert d&#39;événement [&#128279;](../../../ui/event-forwarding/secrets.md)et définissez la valeur sur votre [[!DNL Braze] clé API](#configuration-details).  Elle sera utilisée pour authentifier la connexion à votre compte tout en conservant la valeur en sécurité.

## Installation et configuration de l’extension [!DNL Braze] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier à la place.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]** , sélectionnez **[!UICONTROL Installer]** sur la carte de l’extension [!DNL Braze].

![Installez l’extension [!DNL Braze].](../../../images/extensions/server/braze/install-extension.png)

Sur l’écran suivant, saisissez les [valeurs de configuration](#configuration-details) suivantes que vous avez précédemment collectées à partir de [!DNL Braze] :

- **[!UICONTROL Braze Rest Endpoint URL]** : vous pouvez saisir la valeur de votre URL de point d’entrée rest [!DNL Braze] en tant que texte brut dans l’entrée fournie.
- **[!UICONTROL Clé API]** : sélectionnez l’ [élément de données secret](#create-a-secret) que vous avez créé précédemment, qui contient votre clé d’API [!DNL Braze].

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![La page de configuration de l’extension [!DNL Braze].](../../../images/extensions/server/braze/configure-extension.png)

## Création d’une règle [!DNL Send Event] {#tracking-rule}

Après avoir installé l’extension, créez un transfert d’événement [rule](../../../ui/managing-resources/rules.md) et configurez ses conditions selon vos besoins. Lors de la configuration des actions pour la règle, sélectionnez l’extension **[!UICONTROL Braze]**, puis sélectionnez **[!UICONTROL Envoyer l’événement]** pour le type d’action.

![Ajoutez une configuration d&#39;action de règle de transfert d&#39;événement.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identification de l’utilisateur]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Identifiant utilisateur externe] | UUID ou GUID longs, aléatoires et bien répartis. Si vous choisissez une autre méthode pour nommer vos ID utilisateur, ceux-ci doivent également être longs, aléatoires et bien répartis. En savoir plus sur la [convention d’affectation de nom d’utilisateur suggérée](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze User ID] | Identifiant de l’utilisateur de Braze. |
| [!UICONTROL Alias utilisateur] | Un alias sert d’autre identifiant d’utilisateur unique. Utilisez des alias pour identifier les utilisateurs selon différentes dimensions que votre ID utilisateur principal. <br><br> L’objet user alias se compose de deux parties : un nom_alias pour l’identifiant lui-même et un libellé_alias indiquant le type d’alias. Les utilisateurs peuvent avoir plusieurs alias avec des libellés différents, mais un seul alias par alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Pour lier l’événement à un utilisateur, vous devez renseigner le champ [!UICONTROL Identifiant utilisateur externe], le champ [!UICONTROL Identifiant utilisateur de braze] ou la section [!UICONTROL Alias utilisateur].

**[!UICONTROL Event Data]**

| Entrée | Description | Obligatoire |
| --- | --- | --- |
| [!UICONTROL Nom de l’événement &#x200B;] | Nom de l’événement. | Oui |
| [!UICONTROL Heure de l’événement] | Date-time sous la forme d’une chaîne au format ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Oui |
| [!UICONTROL Identifiant d’application] | L’identifiant d’application ou <strong>app_id</strong> est un paramètre qui associe une activité à une application spécifique de votre groupe d’applications. Il désigne l’application dans le groupe d’applications avec lequel vous interagissez. En savoir plus sur les [types d’identifiants d’API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propriétés de l’événement &#x200B;] | Objet JSON contenant des propriétés personnalisées de l’événement. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> L’action **[!UICONTROL Braze Send Event]** ne nécessite qu’un **[!UICONTROL Event Name]** et une **[!UICONTROL Event Time]** à spécifier, mais vous devez inclure autant d’informations que possible dans le champ des propriétés personnalisées. Pour plus d’informations sur l’objet d’événement [!DNL Braze], reportez-vous à la [documentation officielle](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributs de l’utilisateur]**

Les attributs utilisateur peuvent être un objet JSON contenant des champs qui créeront ou mettront à jour un attribut avec le nom et la valeur fournis sur le profil utilisateur spécifié. Les propriétés suivantes sont prises en charge :

| Attribut utilisateur | Description |
| --- | --- |
| [!UICONTROL Prénom] | |
| [!UICONTROL Nom] | |
| [!UICONTROL Phone] | |
| [!UICONTROL E-mail.] | |
| [!UICONTROL Genre] | Une des chaînes suivantes : &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (autre), &quot;N&quot; (non applicable), &quot;P&quot; (préférez ne pas dire). |
| [!UICONTROL Ville] | |
| [!UICONTROL Country] | Pays sous forme de chaîne au format [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Langue] | Langue sous forme de chaîne au format [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Date de naissance] | Chaîne au format &quot;AAAA-MM-JJ&quot; (par exemple, 1980-12-21). |
| [!UICONTROL Fuseau horaire] | Nom du fuseau horaire de la [base de données du fuseau horaire IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (par exemple, &quot;Amérique/New_York&quot; ou &quot;Heure de l’Est (États-Unis et Canada)&quot;). |
| [!UICONTROL Facebook] | Hachage contenant n’importe quel identifiant (chaîne), mentions &quot;J’aime&quot; (tableau de chaînes), num_friend (entier). |
| [!UICONTROL Twitter] | Hachage contenant n’importe quel ID (entier), screen_name (chaîne, nom du Twitter), followers_count (entier), friend_count (entier), statuses_count(entier). |

{style="table-layout:auto"}

## Création d’une règle [!DNL Send Purchase Event] {#purchase-rule}

Après avoir installé l’extension, créez un transfert d’événement [rule](../../../ui/managing-resources/rules.md) et configurez ses conditions selon vos besoins. Lors de la configuration des actions pour la règle, sélectionnez l’extension **[!UICONTROL Braze]**, puis sélectionnez **[!UICONTROL Envoyer l’événement d’achat]** pour le type d’action.

![Ajoutez une configuration d&#39;action de type Action de transfert d&#39;événement de type Achat de braze.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identification de l’utilisateur]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Identifiant utilisateur externe] | UUID ou GUID longs, aléatoires et bien répartis. Si vous choisissez une autre méthode pour nommer vos ID utilisateur, ceux-ci doivent également être longs, aléatoires et bien répartis. En savoir plus sur la [convention d’affectation de nom d’utilisateur suggérée](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze User ID] | Identifiant de l’utilisateur de Braze. |
| [!UICONTROL Alias utilisateur] | Un alias sert d’autre identifiant d’utilisateur unique. Utilisez des alias pour identifier les utilisateurs selon différentes dimensions que votre ID utilisateur principal. <br><br> L’objet user alias se compose de deux parties : un nom_alias pour l’identifiant lui-même et un libellé_alias indiquant le type d’alias. Les utilisateurs peuvent avoir plusieurs alias avec des libellés différents, mais un seul alias par alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Pour lier l’événement à un utilisateur, vous devez renseigner le champ [!UICONTROL External User ID], le champ [!UICONTROL Braze User Identifier] ou la section [!UICONTROL User Alias] .

**[!UICONTROL Données d’achat]**

| Entrée | Description | Obligatoire |
| --- | --- | --- |
| [!UICONTROL ID de produit &#x200B;] | Identifiant de l’achat. (par exemple, Nom du produit ou Catégorie de produit) | Oui |
| [!UICONTROL Temps d’achat] | Date-time sous la forme d’une chaîne au format ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Oui |
| [!UICONTROL &#x200B; de devise] | Devise en tant que chaîne au format [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) Alphabétique du code de devise. | Oui |
| [!UICONTROL Prix &#x200B;] | Prix. | Oui |
| [!UICONTROL Quantité &#x200B;] | Si elle n’est pas fournie, la valeur par défaut est 1. La valeur maximale doit être inférieure à 100. | |
| [!UICONTROL Identifiant d’application] | L’identifiant d’application ou <strong>app_id</strong> est un paramètre qui associe une activité à une application spécifique de votre groupe d’applications. Il désigne l’application dans le groupe d’applications avec lequel vous interagissez. En savoir plus sur les [types d’identifiants d’API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propriétés d’achat &#x200B;] | Objet JSON contenant les propriétés personnalisées de l’achat. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> L’action **[!UICONTROL Braze Send Event]** ne nécessite qu’un **[!UICONTROL Event Name]** et une **[!UICONTROL Event Time]** à spécifier, mais vous devez inclure autant d’informations que possible dans le champ des propriétés personnalisées. Pour plus d’informations sur l’objet d’événement [!DNL Braze], reportez-vous à la [documentation officielle](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributs de l’utilisateur]**

Les attributs utilisateur peuvent être un objet JSON contenant des champs qui créeront ou mettront à jour un attribut avec le nom et la valeur fournis sur le profil utilisateur spécifié. Les propriétés suivantes sont prises en charge :

| Attribut utilisateur | Description |
| --- | --- |
| [!UICONTROL Prénom] | |
| [!UICONTROL Nom] | |
| [!UICONTROL Phone] | |
| [!UICONTROL E-mail.] | |
| [!UICONTROL Genre] | Une des chaînes suivantes : &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (autre), &quot;N&quot; (non applicable), &quot;P&quot; (préférez ne pas dire). |
| [!UICONTROL Ville] | |
| [!UICONTROL Country] | Pays sous forme de chaîne au format [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Langue] | Langue sous forme de chaîne au format [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Date de naissance] | Chaîne au format &quot;AAAA-MM-JJ&quot; (par exemple, 1980-12-21). |
| [!UICONTROL Fuseau horaire] | Nom du fuseau horaire de la [base de données du fuseau horaire IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (par exemple, &quot;Amérique/New_York&quot; ou &quot;Heure de l’Est (États-Unis et Canada)&quot;). |
| [!UICONTROL Facebook] | Hachage contenant n’importe quel identifiant (chaîne), mentions &quot;J’aime&quot; (tableau de chaînes), num_friend (entier). |
| [!UICONTROL Twitter] | Hachage contenant n’importe quel ID (entier), screen_name (chaîne, nom du Twitter), followers_count (entier), friend_count (entier), statuses_count(entier). |

{style="table-layout:auto"}

## Validation des données dans [!DNL Braze] {#validate}

Si la collecte d’événements et l’intégration de [!DNL Adobe Experience Platform] ont réussi, des événements s’affichent dans la console [!DNL Braze] lors de l’ [&#x200B; affichage des profils utilisateur](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Plus précisément, les nouvelles données d’événement envoyées à [!DNL Braze] sont reflétées dans la section [!DNL Purchases] de l’onglet [aperçu](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab) d’un utilisateur particulier.

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion vers [!DNL Braze] à l’aide du transfert d’événement. Pour plus d&#39;informations sur les applications en aval pour les données d&#39;événement envoyées à [!DNL Braze], consultez la [documentation officielle](https://www.braze.com/docs).

Pour plus d’informations sur les fonctionnalités de transfert d’événement en Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
