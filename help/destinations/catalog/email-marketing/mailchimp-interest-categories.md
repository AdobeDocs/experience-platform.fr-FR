---
title: Catégories d’intérêt Mailchimp
description: Mailchimp (également appelé Intuit Mailchimp) est une plateforme de marketing automatisé populaire et un service de marketing par e-mail utilisé par les entreprises pour gérer et communiquer avec des contacts (clients, clients ou autres personnes intéressées) à l’aide de listes de diffusion et de campagnes de marketing par e-mail. Utilisez ce connecteur pour trier vos contacts en fonction de leurs centres d’intérêt et de leurs préférences.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 20%

---

# Connexion [!DNL Mailchimp Interest Categories]

[[!DNL Mailchimp]](https://mailchimp.com) est une plateforme d’automatisation du marketing populaire et un service de marketing par e-mail utilisé par les entreprises pour gérer et communiquer avec des contacts *(clients, clients ou autres parties intéressées)* à l’aide de listes de diffusion et de campagnes de marketing par e-mail. Utilisez ce connecteur pour trier vos contacts en fonction de leurs centres d’intérêt et de leurs préférences.

[!DNL Mailchimp Interest Categories] utilise [audiences](https://mailchimp.com/help/getting-started-audience/), [groupes](https://mailchimp.com/help/getting-started-with-groups/) et catégories d’intérêt *(également appelées noms de groupe ou titres de groupe)*. Chaque groupe [!DNL Mailchimp] est une liste de catégories d’intérêt. Les contacts sont associés à une catégorie d&#39;intérêt lorsqu&#39;ils s&#39;abonnent à une ou plusieurs catégories d&#39;intérêt par le biais d&#39;un formulaire d&#39;inscription sur votre site web. Au sein d’une audience, vous pouvez également organiser les contacts en groupes et les associer à des catégories d’intérêt. Ces catégories peuvent ensuite être utilisées pour créer des segments. Vous pouvez utiliser ces audiences pour diffuser des emails de campagne ciblés vers les contacts abonnés.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) utilise l’API [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) pour créer des [catégories d’intérêt](https://mailchimp.com/developer/marketing/api/interest-categories/), puis ajouter des contacts de chacune des audiences Platform sélectionnées dans une catégorie d’intérêt correspondante. Vous pouvez **ajouter de nouveaux contacts** ou **mettre à jour les informations des [!DNL Mailchimp] contacts** existants, puis **les ajouter ou les supprimer de leurs groupes souhaités** dans une audience [!DNL Mailchimp] existante après les avoir activés dans un nouveau segment. [!DNL Mailchimp Interest Groups] utilise les noms d’audience sélectionnés de Platform comme catégories d’intérêt dans [!DNL Mailchimp].

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Mailchimp Interest Categories], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Envoyer des emails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service des ventes d&#39;un site web de sport souhaite diffuser une campagne marketing par email à une liste de contacts qui se sont identifiés comme intéressés par le football. Les listes de contacts sont séparées en tant que lots dans l’exportation des données reçue de l’équipe de développement du site web et doivent donc être suivies. L’équipe identifie une audience [!DNL Mailchimp] existante et commence à créer les audiences Experience Platform dans lesquelles les contacts de chaque liste sont ajoutés. Après l’envoi de ces audiences à [!DNL Mailchimp Interest Categories], si des contacts n’existent pas dans l’audience sélectionnée [!DNL Mailchimp], ils sont ajoutés à un groupe avec le nom de l’audience auquel le contact appartient. Si des contacts existent déjà dans l&#39;audience ou le groupe [!DNL Mailchimp], leurs informations sont mises à jour. Une fois les données envoyées à [!DNL Mailchimp Interest Categories], l’équipe des ventes peut sélectionner et envoyer le courrier électronique de campagne marketing au groupe d’intérêt de football au sein de l’audience [!DNL Mailchimp].

## Conditions préalables {#prerequisites}

Reportez-vous aux sections ci-dessous pour connaître les conditions préalables à configurer dans Experience Platform et [!DNL Mailchimp], ainsi que pour obtenir des informations que vous devez rassembler avant de travailler avec la destination [!DNL Mailchimp Interest Categories].

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL Mailchimp Interest Categories], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créés dans [!DNL Experience Platform].

### Conditions préalables pour la destination [!DNL Mailchimp Interest Categories] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données de Platform vers votre compte [!DNL Mailchimp] :

#### Vous devez avoir un compte [!DNL Mailchimp] {#prerequisites-account}

Avant de pouvoir créer une destination [!DNL Mailchimp Interest Categories], vous devez vous assurer d’avoir un compte [!DNL Mailchimp]. Si vous n&#39;en avez pas encore, consultez la [[!DNL Mailchimp] page d&#39;inscription](https://login.mailchimp.com/signup/) pour vous enregistrer et créer votre compte.

#### Collecte de la clé d’API [!DNL Mailchimp] {#gather-credentials}

Vous avez besoin de votre [!DNL Mailchimp] **clé API** pour authentifier la destination [!DNL Mailchimp Interest Categories] sur votre compte [!DNL Mailchimp]. La **clé API** sert de **mot de passe** lorsque vous [authentifiez la destination](#authenticate).

Si vous ne disposez pas de votre **clé API**, connectez-vous à votre compte et reportez-vous à la documentation [[!DNL Mailchimp] Générer votre clé API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) pour en créer une.

`0123456789abcdef0123456789abcde-us14` est un exemple de clé API.

>[!IMPORTANT]
>
>Si vous générez la **clé API**, écrivez-la car vous ne pourrez pas y accéder après la génération.

#### Identifier le centre de données [!DNL Mailchimp] {#identify-data-center}

Ensuite, vous devez identifier votre centre de données [!DNL Mailchimp]. Pour ce faire, connectez-vous à votre compte [!DNL Mailchimp] et accédez à la **section Clés API** de votre compte.

La valeur correspond à la première partie de l’URL que vous voyez dans votre navigateur. Si l’URL est *https://`us14`.mailchimp.com/account/api/*, le centre de données est `us14`.

Elle est également ajoutée à votre clé API sous la forme *key-dc* ; si votre clé API est `0123456789abcdef0123456789abcde-us14`, alors le centre de données est `us14`.

Notez la valeur de centre de données *(`us14` dans cet exemple)*, vous avez besoin de cette valeur lorsque vous [renseignez les détails de destination](#destination-details).

Si vous avez besoin d’autres conseils, reportez-vous à la [[!DNL Mailchimp] documentation de base](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Mécanismes de sécurisation {#guardrails}

Chacune de vos audiences [!DNL Mailchimp] peut contenir jusqu’à 60 noms de groupe (ou catégories d’intérêt) dans un seul groupe ou entre plusieurs groupes au sein d’une même audience. Reportez-vous à [!DNL Mailchimp] [groups](https://mailchimp.com/help/getting-started-with-groups/) pour toute clarification requise. Lorsque vous atteignez cette limite, vous obtenez un message `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` en tant que réponse d’erreur de l’API [!DNL Mailchimp].

Consultez également les [!DNL Mailchimp] [limites de taux](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) pour obtenir des informations détaillées sur les limites imposées par l’API [!DNL Mailchimp].

## Identités prises en charge {#supported-identities}

[!DNL Mailchimp] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresse électronique du contact | Obligatoire |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Pour chaque audience sélectionnée dans Platform, l’état du segment [!DNL Mailchimp Interest Categories] correspondant est mis à jour avec son état d’audience de Platform.</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour en Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Mailchimp Interest Categories]. Vous pouvez également la localiser sous la catégorie **[!UICONTROL Marketing par e-mail]**.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, remplissez les champs requis ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**.

| Champ | Description |
| --- | --- |
| **[!UICONTROL Nom d’utilisateur]** | Votre nom d’utilisateur [!DNL Mailchimp Interest Categories]. |
| **[!UICONTROL Mot de passe]** | Votre [!DNL Mailchimp] **clé d&#39;API**, que vous avez noté dans la section [Rassembler [!DNL Mailchimp] informations d&#39;identification](#gather-credentials).<br> Votre clé API prend la forme `{KEY}-{DC}`, où la partie `{KEY}` fait référence à la valeur indiquée dans la section [[!DNL Mailchimp] clé API](#gather-credentials) et la partie `{DC}` fait référence au [[!DNL Mailchimp] centre de données](#identify-data-center). <br>Vous pouvez fournir la partie `{KEY}` ou l’intégralité du formulaire.<br> Par exemple, si votre clé API est <br>*`0123456789abcdef0123456789abcde-us14`*,<br>, vous pouvez fournir *`0123456789abcdef0123456789abcde`*ou *`0123456789abcdef0123456789abcde-us14`*comme valeur. |

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
| **[!UICONTROL Centre de données]** | Votre compte [!DNL Mailchimp] `data center`. Pour obtenir des conseils, reportez-vous à la section [Identifier [!DNL Mailchimp] le centre de données](#identify-data-center) . |
| **[!UICONTROL Nom de l’audience (veuillez d’abord sélectionner le centre de données)]** | Après avoir sélectionné votre **[!UICONTROL centre de données]**, cette liste déroulante est automatiquement renseignée avec les noms d’audience de votre compte [!DNL Mailchimp]. Sélectionnez l’audience que vous souhaitez mettre à jour avec les données de Platform. |
| **[!UICONTROL Catégorie d’intérêts (veuillez d’abord sélectionner le centre de données et le nom d’audience)]** | Une fois que vous avez sélectionné votre **[!UICONTROL nom d’audience]**, cette liste déroulante est automatiquement renseignée avec les noms de catégorie de groupes d’intérêt de votre compte [!DNL Mailchimp]. Sélectionnez le nom de la catégorie que vous souhaitez mettre à jour avec les données de Platform. |

{style="table-layout:auto"}

>[!TIP]
>
> Si la clé d&#39;API que vous avez fournie dans le champ **[!UICONTROL Mot de passe]** ou la valeur **[!UICONTROL du centre de données]** est incorrecte, l&#39;interface utilisateur affiche une réponse d&#39;erreur d&#39;API [!DNL Mailchimp] : *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* comme illustré ci-dessous. Dans ce cas, vous ne pouvez pas sélectionner de valeur dans le champ **[!UICONTROL Nom d’audience (veuillez sélectionner le centre de données en premier)]** . Pour corriger cette erreur, indiquez les valeurs correctes.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement les données d’audience de Adobe Experience Platform vers la destination [!DNL Mailchimp Interest Categories], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL Mailchimp Interest Categories], procédez comme suit :

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Vous pouvez désormais voir une nouvelle ligne de mappage sur l’écran.
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]**, choisissez la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez l’attribut XDM ou l’attribut **[!UICONTROL Sélectionner l’espace de noms d’identité]** et sélectionnez une identité.
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]** , choisissez l’ **[!UICONTROL espace de noms d’identité]** et sélectionnez une identité ou la catégorie **[!UICONTROL Sélectionner des attributs]** et sélectionnez dans la liste des attributs renseignés dans l’API [!DNL Mailchimp]. *Tous les attributs personnalisés que vous avez ajoutés à l’audience [!DNL Mailchimp] sélectionnée seront également disponibles pour la sélection en tant que champs cibles.*

   Les mappages disponibles entre votre schéma de profil XDM et [!DNL Mailchimp Interest Categories] sont les suivants :

   | Champ source | Champ cible | Notes |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: email` | Obligatoire : Oui |
   | `xdm: person.name.firstName` | `Attribute: FNAME` | |
   | `xdm: person.name.lastName` | `Attribute: LNAME` | |
   | `xdm: person.birthDayAndMonth` | `Attribute: BIRTHDAY` | |

   En outre, `ADDRESS` est un champ cible spécial appelé `merge field` dans votre audience [!DNL Mailchimp]. La [[!DNL Mailchimp] documentation](https://mailchimp.com/developer/marketing/docs/merge-fields/) définit les clés requises comme `addr1`, `city`, `state` et `zip`, ainsi que les clés facultatives `addr2` et `country`. Les valeurs de ces champs doivent être des chaînes. Si l’un des mappages de champ `ADDRESS` est présent, la destination transmet l’objet `ADDRESS` à l’API [!DNL Mailchimp] pour mise à jour. La valeur par défaut de tous les champs `ADDRESS` qui ne sont pas mappés est `NULL`, à l’exception du pays dont la valeur par défaut est `US`.

   Les mappages disponibles pour le champ `ADDRESS` sont les suivants :

   | Champ source | Champ cible |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   Par exemple, vous souhaitez mettre à jour la valeur de `country` avec le champ d’adresse existant du contact `addr1`, `city`, `state` et les valeurs `zip` comme `132, My Street, Kingston`, `New York`, `New York` et `12401`. Pour mettre à jour `country`, vous devez transmettre les valeurs existantes avec les modifications *(le cas échéant)* et la nouvelle valeur pour le pays. Par conséquent, les valeurs de votre jeu de données doivent être `132, My Street, Kingston`, `New York`, `New York`, `12401` et `US`. En résumé, si vous transmettez uniquement `country` et ne fournissez pas de valeurs pour `addr1`, `city`, `state` et `zip`, ils seront remplacés par `NULL`.

   Un exemple avec les mappages terminés est illustré ci-dessous :
   ![ Exemple de capture d’écran de l’interface utilisateur de Platform montrant les mappages de champs.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

* Connectez-vous à votre compte [[!DNL Mailchimp]](https://login.mailchimp.com/). Ensuite, accédez à la page **[!DNL Audience]**. Développez ensuite le menu **[!DNL Manage Contacts]** et sélectionnez **[!DNL Groups]**.

![Capture d’écran de l’interface utilisateur de Mailchimp montrant la page du groupe d’audiences.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Sélectionnez le Groupe et vérifiez si les audiences sélectionnées sont créées en tant que catégories avec le nom de l’audience de Platform, qui peut être suivi d’un suffixe généré automatiquement.
   * Cette destination utilise les noms des segments sélectionnés pour créer la catégorie d’intérêt à l’aide de l’API [[!DNL Mailchimp] Ajouter une catégorie d’intérêt](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/). Si vous créez une destination et réactivez les mêmes audiences, [!DNL Mailchimp] ajoute un suffixe pour faire la distinction entre les segments existants et les nouveaux segments.
* Les contacts dont les emails n&#39;existaient pas dans le groupe sont ajoutés à la catégorie nouvellement créée.
* Pour les contacts déjà présents dans le groupe, les données du champ d&#39;attribut sont mises à jour et le contact est ajouté à la catégorie nouvellement créée.

![Copie d’écran de l’interface utilisateur de Mailchimp montrant les catégories de groupes d’audiences.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreur rencontrée si la clé d’API ou les valeurs du centre de données [!DNL Mailchimp] sont incorrectes {#incorrect-credentials-error}

Si la clé d&#39;API que vous avez fournie dans le champ **[!UICONTROL Mot de passe]** ou la valeur **[!UICONTROL du centre de données]** est incorrecte, l&#39;interface utilisateur affiche une réponse d&#39;erreur d&#39;API [!DNL Mailchimp] : *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* comme illustré ci-dessous. Dans ce cas, vous ne pouvez pas sélectionner de valeur dans le champ **[!UICONTROL Nom d’audience (veuillez sélectionner le centre de données en premier)]** .

![ Copie d’écran de l’interface utilisateur de Platform indiquant une erreur si la clé de l’API Mailchimp ou les valeurs du centre de données sont incorrectes.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Pour corriger cette erreur et passer à l’étape suivante, vous devez fournir les valeurs correctes. Reportez-vous au [centre de données  [!DNL Mailchimp]  d’identification](#identify-data-center) et
[Rassemblez les sections  [!DNL Mailchimp] Clé API](#gather-credentials) si vous avez besoin d’instructions.

### Erreur rencontrée si la limite de nom de groupe [!DNL Mailchimp] est dépassée {#group-name-limits-error}

Lors de la création de la destination, vous pouvez recevoir les messages d’erreur suivants : *`Cannot have more than 60 interests per list (Across all categories)`* ou *`400 BAD_REQUEST`*. Cela se produit lorsque vous dépassez les 60 noms de groupe (ou catégories d’intérêt) d’un seul groupe ou de plusieurs groupes dans la même limite d’audience, comme décrit dans la section [Barrières de sécurité](#guardrails) . Pour corriger cette erreur, veillez à ne pas dépasser la limite du nom du groupe dans [!DNL Mailchimp].

### [!DNL Mailchimp] Codes d’état et d’erreur

Consultez la [[!DNL Mailchimp] page erreurs](https://mailchimp.com/developer/marketing/docs/errors/) pour obtenir une liste complète des codes d’état et d’erreur avec des explications.

## Ressources supplémentaires {#additional-resources}

Vous trouverez ci-dessous d’autres informations utiles à partir de la documentation [!DNL Mailchimp] :
* [Prise en main de [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Prise en main des audiences](https://mailchimp.com/help/getting-started-audience/)
* [Créer une audience](https://mailchimp.com/help/create-audience/)
* [Prise en main des groupes](https://mailchimp.com/help/getting-started-with-groups/)
* [Créer un groupe d’audiences](https://mailchimp.com/help/create-new-audience-group/)
* [Catégories d’intérêts](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [API marketing](https://mailchimp.com/developer/marketing/api/)
