---
title: Catégories d’intérêt Mailchimp
description: Mailchimp (également appelé Intuit Mailchimp) est une plateforme de marketing automatisé populaire et un service de marketing par e-mail utilisé par les entreprises pour gérer et communiquer avec des contacts (clients, clients ou autres personnes intéressées) à l’aide de listes de diffusion et de campagnes de marketing par e-mail. Utilisez ce connecteur pour trier vos contacts en fonction de leurs centres d’intérêt et de leurs préférences.
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: a293df660a9b959d12bdc170d1cb69f3543a30f1
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 22%

---

# Connexion [!DNL Mailchimp Interest Categories]

[[!DNL Mailchimp]](https://mailchimp.com) est une plateforme d’automatisation du marketing et un service de marketing par e-mail très utilisé par les entreprises pour gérer et communiquer avec les contacts. *(clients, clients ou autres parties intéressées)* utilisation de listes de diffusion et de campagnes de marketing par e-mail. Utilisez ce connecteur pour trier vos contacts en fonction de leurs centres d’intérêt et de leurs préférences.

[!DNL Mailchimp Interest Categories] uses [audiences](https://mailchimp.com/help/getting-started-audience/), [groups](https://mailchimp.com/help/getting-started-with-groups/), et les catégories d’intérêt *(également appelés noms de groupe ou titres de groupe)*. Chaque [!DNL Mailchimp] groupe est une liste de catégories d’intérêt. Les contacts sont associés à une catégorie d&#39;intérêt lorsqu&#39;ils s&#39;abonnent à une ou plusieurs catégories d&#39;intérêt par le biais d&#39;un formulaire d&#39;inscription sur votre site web. Au sein d’une audience, vous pouvez également organiser les contacts en groupes et les associer à des catégories d’intérêt. Ces catégories peuvent ensuite être utilisées pour créer des segments. Vous pouvez utiliser ces audiences pour diffuser des emails de campagne ciblés vers les contacts abonnés.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) utilise la variable [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API à créer [catégories d&#39;intérêt](https://mailchimp.com/developer/marketing/api/interest-categories/) puis ajouter des contacts de chacune des audiences Platform sélectionnées dans une catégorie d’intérêt correspondante. Vous pouvez **ajouter de nouveaux contacts** ou **mettre à jour les informations des [!DNL Mailchimp] contacts**, puis **les ajouter ou les supprimer des groupes de votre choix** dans un [!DNL Mailchimp] après les avoir activés dans un nouveau segment. [!DNL Mailchimp Interest Groups] utilise les noms d’audience sélectionnés de Platform comme catégories d’intérêt dans [!DNL Mailchimp].

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Mailchimp Interest Categories], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Envoyer des emails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service des ventes d&#39;un site web de sport souhaite diffuser une campagne marketing par email à une liste de contacts qui se sont identifiés comme intéressés par le football. Les listes de contacts sont séparées en tant que lots dans l’exportation des données reçue de l’équipe de développement du site web et doivent donc être suivies. L’équipe identifie une [!DNL Mailchimp] et commence à créer les audiences Experience Platform dans lesquelles sont ajoutés les contacts de chaque liste. Après avoir envoyé ces audiences à [!DNL Mailchimp Interest Categories], si des contacts n’existent pas dans le [!DNL Mailchimp] audience à laquelle ils sont ajoutés à un groupe avec le nom de l’audience auquel le contact appartient. Si des contacts existent déjà dans la variable [!DNL Mailchimp] audience ou groupe, puis leurs informations sont mises à jour. Une fois les données envoyées à [!DNL Mailchimp Interest Categories], l’équipe des ventes peut sélectionner et envoyer le courrier électronique de la campagne marketing au groupe d’intérêt football au sein de la [!DNL Mailchimp] audience.

## Conditions préalables {#prerequisites}

Reportez-vous aux sections ci-dessous pour connaître les conditions préalables à configurer dans Experience Platform et [!DNL Mailchimp] et pour les informations que vous devez rassembler avant de travailler avec la variable [!DNL Mailchimp Interest Categories] destination.

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL Mailchimp Interest Categories], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=fr) créés dans [!DNL Experience Platform].

### Conditions préalables pour l’ [!DNL Mailchimp Interest Categories] destination {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données de Platform vers votre [!DNL Mailchimp] compte :

#### Vous devez disposer d’un [!DNL Mailchimp] account {#prerequisites-account}

Avant de pouvoir créer un [!DNL Mailchimp Interest Categories] destination, vous devez d’abord vous assurer que vous disposez d’une [!DNL Mailchimp] compte . Si vous n’en avez pas déjà un, rendez-vous sur la page [[!DNL Mailchimp] page d’inscription](https://login.mailchimp.com/signup/) pour enregistrer et créer votre compte.

#### Collecte [!DNL Mailchimp] Clé API {#gather-credentials}

Vous avez besoin de votre [!DNL Mailchimp] **Clé API** pour authentifier la variable [!DNL Mailchimp Interest Categories] destination par rapport à votre [!DNL Mailchimp] compte . Le **Clé API** sert de **Mot de passe** lorsque vous [authentifier la destination](#authenticate).

Si vous n’avez pas votre **Clé API**, connectez-vous à votre compte et reportez-vous à la section [[!DNL Mailchimp] Génération de votre clé API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) pour en créer une.

Exemple de clé API : `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Si vous générez la variable **Clé API**, écrivez-le car vous ne pourrez pas y accéder après une génération.

#### Identifier [!DNL Mailchimp] centre de données {#identify-data-center}

Ensuite, vous devez identifier votre [!DNL Mailchimp] centre de données. Pour ce faire, connectez-vous à [!DNL Mailchimp] et accédez au **Section Clés API** de votre compte.

La valeur correspond à la première partie de l’URL que vous voyez dans votre navigateur. Si l’URL est *https://`us14`.mailchimp.com/account/api/*, le centre de données est `us14`.

Il est également ajouté à votre clé API dans le formulaire. *key-dc*; si votre clé API est `0123456789abcdef0123456789abcde-us14`, le centre de données est `us14`.

Écrire la valeur du centre de données *(`us14` dans cet exemple)*, cette valeur est nécessaire lorsque vous [remplir les détails de destination](#destination-details).

Si vous avez besoin d’autres conseils, reportez-vous à la section [[!DNL Mailchimp] Documentation de base](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Mécanismes de sécurisation {#guardrails}

Chacune de vos [!DNL Mailchimp] Les audiences peuvent contenir jusqu’à 60 noms de groupe (ou catégories d’intérêt) au sein d’un seul groupe ou de plusieurs groupes au sein d’une même audience. Voir [!DNL Mailchimp] [groups](https://mailchimp.com/help/getting-started-with-groups/) pour toute clarification requise. Lorsque vous atteignez cette limite, vous obtenez une `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` message en tant que réponse d’erreur de la fonction [!DNL Mailchimp] API.

En outre, reportez-vous à la section [!DNL Mailchimp] [limites de taux](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) pour obtenir des informations détaillées sur les limites imposées par la variable [!DNL Mailchimp] API.

## Identités prises en charge {#supported-identities}

[!DNL Mailchimp] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresse électronique du contact | Obligatoire |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Pour chaque audience sélectionnée dans Platform, la valeur [!DNL Mailchimp Interest Categories] l’état du segment est mis à jour avec son état d’audience de Platform.</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour en Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Mailchimp Interest Categories]. Vous pouvez également la localiser sous le **[!UICONTROL Marketing par e-mail]** catégorie.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs obligatoires ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**.

| Champ | Description |
| --- | --- |
| **[!UICONTROL Nom d’utilisateur]** | Votre [!DNL Mailchimp Interest Categories] nom d’utilisateur. |
| **[!UICONTROL Mot de passe]** | Votre [!DNL Mailchimp] **Clé API**, que vous avez noté dans la variable [Collecte [!DNL Mailchimp] informations](#gather-credentials) .<br> Votre clé API prend la forme `{KEY}-{DC}`, où la variable `{KEY}` fait référence à la valeur indiquée dans la variable [[!DNL Mailchimp] Clé API](#gather-credentials) et le `{DC}` fait référence à la [[!DNL Mailchimp] centre de données](#identify-data-center). <br>Vous pouvez fournir le `{KEY}` ou l’intégralité du formulaire.<br> Par exemple, si votre clé API est <br>*`0123456789abcdef0123456789abcde-us14`*,<br> vous pouvez fournir *`0123456789abcdef0123456789abcde`*ou *`0123456789abcdef0123456789abcde-us14`*comme valeur. |

{style="table-layout:auto"}

![Capture d’écran montrant comment s’authentifier sur l’interface utilisateur de Platform.](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un statut **[!UICONTROL Connecté]** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| Champ | Description |
| --- | --- |
| **[!UICONTROL Nom]** | Un nom par lequel vous reconnaîtrez cette destination à l’avenir. |
| **[!UICONTROL Description]** | Description qui vous aidera à identifier cette destination ultérieurement. |
| **[!UICONTROL Centre de données]** | Votre [!DNL Mailchimp] account `data center`. Reportez-vous à la section [Identifier [!DNL Mailchimp] centre de données](#identify-data-center) pour obtenir des conseils. |
| **[!UICONTROL Nom de l’audience (veuillez d’abord sélectionner le centre de données)]** | Après avoir sélectionné **[!UICONTROL Centre de données]**, cette liste déroulante est automatiquement renseignée avec les noms d’audience de votre [!DNL Mailchimp] compte . Sélectionnez l’audience que vous souhaitez mettre à jour avec les données de Platform. |
| **[!UICONTROL Catégorie d’intérêts (veuillez d’abord sélectionner le centre de données et le nom d’audience)]** | Après avoir sélectionné **[!UICONTROL Nom de l’audience]**, cette liste déroulante est automatiquement renseignée avec les noms de catégorie de groupes d’intérêt de votre [!DNL Mailchimp] compte . Sélectionnez le nom de la catégorie que vous souhaitez mettre à jour avec les données de Platform. |

{style="table-layout:auto"}

>[!TIP]
>
> Si la clé d’API que vous avez fournie dans la variable **[!UICONTROL Mot de passe]** ou le champ **[!UICONTROL Centre de données]** est incorrecte, l’interface affiche une [!DNL Mailchimp] Réponse d’erreur de l’API : *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* comme illustré ci-dessous. Dans ce cas, vous ne pouvez pas sélectionner de valeur dans la variable **[!UICONTROL Nom de l’audience (veuillez d’abord sélectionner le centre de données)]** champ . Pour corriger cette erreur, indiquez les valeurs correctes.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer les audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des audiences vers les destinations d’exportation d’audiences par flux](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience de Adobe Experience Platform vers le [!DNL Mailchimp Interest Categories] destination, vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents issus de la destination cible.

Pour mapper correctement vos champs XDM à [!DNL Mailchimp Interest Categories] champs de destination, procédez comme suit :

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Vous pouvez désormais voir une nouvelle ligne de mappage sur l’écran.
1. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’attribut XDM ou choisissez l’option **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité.
1. Dans le **[!UICONTROL Sélectionner le champ cible]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité ou choisissez **[!UICONTROL Sélectionner des attributs]** et sélectionnez dans la liste des attributs renseignés à partir du [!DNL Mailchimp] API. *Tous les attributs personnalisés que vous avez ajoutés au [!DNL Mailchimp] L’audience pourra également être sélectionnée comme champ cible.*

   Mappages disponibles entre votre schéma de profil XDM et [!DNL Mailchimp Interest Categories] sont les suivants : | Champ source | Champ cible | Notes | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Obligatoire : Oui | |`xdm: person.name.firstName`|`Attribute: FNAME`| | |`xdm: person.name.lastName`|`Attribute: LNAME`| | |`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   En outre, `ADDRESS` est un champ cible spécial appelé `merge field` dans votre [!DNL Mailchimp] audience. Le [[!DNL Mailchimp] documentation](https://mailchimp.com/developer/marketing/docs/merge-fields/) définit les clés requises comme `addr1`, `city`, `state`, et `zip`et les clés facultatives `addr2` et `country`. Les valeurs de ces champs doivent être des chaînes. Si l’une des variables `ADDRESS` les mappages de champs sont présents, la destination transfère la variable `ADDRESS` vers l’objet [!DNL Mailchimp] API pour la mise à jour. Quelconque `ADDRESS` les champs qui ne sont pas mappés ont une valeur par défaut de `NULL` sauf pour le pays par défaut `US`.

   Les mappages disponibles pour la variable `ADDRESS` sont les suivants :

   | Champ source | Champ cible |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   Par exemple, vous souhaitez mettre à jour la valeur de `country` avec le champ d&#39;adresse existant du contact `addr1`, `city`, `state`, et `zip` valeurs en tant que `132, My Street, Kingston`, `New York`, `New York` et `12401`. Pour mettre à jour la variable `country` vous devez transmettre les valeurs existantes avec des modifications. *(le cas échéant)* et la nouvelle valeur du pays. Par conséquent, les valeurs de votre jeu de données doivent être `132, My Street, Kingston`, `New York`, `New York`, `12401`, et `US`. Réitérer, si vous ne réussissez que `country` et ne fournissent pas de valeurs pour `addr1`, `city`, `state`, et `zip` Ils seront remplacés par `NULL`.

   Vous trouverez ci-dessous un exemple de mappages terminés :
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les mappages de champs.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Une fois les mappages fournis pour la connexion à la destination, sélectionnez **[!UICONTROL Suivant]**.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

* Connectez-vous à [[!DNL Mailchimp]](https://login.mailchimp.com/) compte . Ensuite, accédez au **[!DNL Audience]** page. Ensuite, développez la variable **[!DNL Manage Contacts]** et sélectionnez **[!DNL Groups]**.

![Capture d’écran de l’interface utilisateur de Mailchimp montrant la page du groupe Audience.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Sélectionnez le Groupe et vérifiez si les audiences sélectionnées sont créées en tant que catégories avec le nom de l’audience de Platform, qui peut être suivi d’un suffixe généré automatiquement.
   * Cette destination utilise les noms des segments sélectionnés pour créer la catégorie d’intérêt en utilisant la variable [[!DNL Mailchimp] Ajout d’une API de catégorie d’intérêt](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/). Si vous créez une destination et réactivez les mêmes audiences, [!DNL Mailchimp] ajoute un suffixe pour distinguer les segments existants des nouveaux segments.
* Les contacts dont les emails n&#39;existaient pas dans le groupe sont ajoutés à la catégorie nouvellement créée.
* Pour les contacts déjà présents dans le groupe, les données du champ d&#39;attribut sont mises à jour et le contact est ajouté à la catégorie nouvellement créée.

![Capture d’écran de l’interface utilisateur de Mailchimp montrant les catégories de groupes d’audiences.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreur rencontrée si [!DNL Mailchimp] Les valeurs de clé d’API ou de centre de données sont incorrectes {#incorrect-credentials-error}

Si la clé d’API que vous avez fournie dans la variable **[!UICONTROL Mot de passe]** ou le champ **[!UICONTROL Centre de données]** est incorrecte, l’interface affiche une [!DNL Mailchimp] Réponse d’erreur de l’API : *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* comme illustré ci-dessous. Dans ce cas, vous ne pouvez pas sélectionner de valeur dans la variable **[!UICONTROL Nom de l’audience (veuillez d’abord sélectionner le centre de données)]** champ .

![Copie d’écran de l’interface utilisateur de Platform affichant une erreur si les valeurs de votre clé API ou de votre centre de données Mailchimp sont incorrectes.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Pour corriger cette erreur et passer à l’étape suivante, vous devez fournir les valeurs correctes. Reportez-vous à la section [Identifier [!DNL Mailchimp] centre de données](#identify-data-center) et
[Collecte [!DNL Mailchimp] Clé API](#gather-credentials) si vous avez besoin d’instructions.

### Erreur rencontrée si [!DNL Mailchimp] la limite du nom de groupe est dépassée. {#group-name-limits-error}

Lors de la création de la destination, vous pouvez recevoir les messages d’erreur suivants : *`Cannot have more than 60 interests per list (Across all categories)`* ou *`400 BAD_REQUEST`*. Cela se produit lorsque vous dépassez les 60 noms de groupe (ou catégories d’intérêt) d’un seul groupe ou de plusieurs groupes dans la même limite d’audience, comme décrit dans la section [barrières de sécurité](#guardrails) . Pour corriger cette erreur, veillez à ne pas dépasser la limite du nom du groupe dans [!DNL Mailchimp].

### [!DNL Mailchimp] Codes d’état et d’erreur

Reportez-vous à la section [[!DNL Mailchimp] page erreurs](https://mailchimp.com/developer/marketing/docs/errors/) pour obtenir une liste complète des codes d’état et d’erreur avec des explications.

## Ressources supplémentaires {#additional-resources}

Retrouvez d’autres informations utiles de la documentation de [!DNL Mailchimp] ci-dessous :
* [Prise en main de [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Prise en main d’Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Création d’un public](https://mailchimp.com/help/create-audience/)
* [Prise en main des groupes](https://mailchimp.com/help/getting-started-with-groups/)
* [Création d’un groupe d’audiences](https://mailchimp.com/help/create-new-audience-group/)
* [Catégories d’intérêts](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [API marketing](https://mailchimp.com/developer/marketing/api/)
