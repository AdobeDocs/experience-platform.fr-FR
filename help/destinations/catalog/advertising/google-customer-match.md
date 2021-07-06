---
keywords: correspondance client Google;correspondance client Google;correspondance client Google
title: Connexion à la correspondance client Google
description: Google Customer Match vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées par Google, telles que Search, Shopping, Gmail et YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 4fed44edb3e201422f765493c9019be1cddffccc
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 4%

---

# [!DNL Google Customer Match] connection

## Présentation {#overview}

[Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Matchlets vous permet d’utiliser vos données en ligne et hors ligne pour atteindre et réengager vos clients dans les propriétés détenues et exploitées de Google, comme :  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail] et  [!DNL YouTube].

![Destination de correspondance client Google dans l’interface utilisateur de Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Google Customer Match], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette fonctionnalité.

### Cas d’utilisation #1

Une marque de vêtements de sport souhaite atteindre ses clients existants par [!DNL Google Search] et [!DNL Google Shopping] afin de personnaliser les offres et les articles en fonction de leurs achats passés et de leur historique de navigation. La marque de vêtements peut ingérer des adresses électroniques de son propre CRM vers l’Experience Platform et créer des segments à partir de ses propres données hors ligne. Ensuite, ils peuvent envoyer ces segments à [!DNL Google Customer Match] afin qu’ils soient utilisés dans [!DNL Search] et [!DNL Shopping], optimisant ainsi leurs dépenses publicitaires.

### Cas d’utilisation #2

Une importante entreprise technologique a lancé un nouveau téléphone. Pour promouvoir ce nouveau modèle de téléphone, ils cherchent à faire connaitre les nouvelles fonctionnalités du téléphone aux clients qui possèdent des modèles précédents de leurs téléphones.

Pour promouvoir cette version, ils téléchargent les adresses électroniques de leur base de données CRM dans Experience Platform, en utilisant les adresses électroniques comme identifiants. Les segments sont créés en fonction des clients qui possèdent des modèles de téléphone plus anciens. Ensuite, les segments sont envoyés à [!DNL Google Customer Match] afin que l’entreprise puisse cibler les clients actuels, les clients qui possèdent des modèles de téléphone anciens et des clients similaires sur [!DNL YouTube].

## Gouvernance des données pour les destinations [!DNL Google Customer Match] {#data-governance}

Certaines destinations en Experience Platform ont certaines règles et obligations pour les données envoyées ou reçues de la plateforme de destination. Il vous incombe de comprendre les limites et les obligations de vos données, ainsi que la manière dont vous utilisez ces données dans Adobe Experience Platform et la plateforme de destination. Adobe Experience Platform fournit des outils de gouvernance des données pour vous aider à gérer certaines de ces obligations en matière d’utilisation des données. [En savoir ](../../../data-governance/labels/overview.md) plus sur les outils et les politiques de gouvernance des données.

## Identités prises en charge {#supported-identities}

[!DNL Google Customer Match] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | Identifiant Google Advertising | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| phone_sha256_e.164 | Numéros de téléphone au format E164, hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Suivez les instructions de la section [Exigences de correspondance des ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section [Exigences de correspondance des ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. |
| user_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

## Type d&#39;export {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone et autres) utilisés dans la  [!DNL Google Customer Match] destination.

## [!DNL Google Customer Match] conditions préalables du compte {#google-account-prerequisites}

Avant de configurer une destination [!DNL Google Customer Match] en Experience Platform, veillez à lire et à respecter la politique d’utilisation de [!DNL Customer Match] de Google, décrite dans la [documentation du support Google](https://support.google.com/google-ads/answer/6299717).

Ensuite, assurez-vous que votre compte [!DNL Google] est configuré pour un niveau d’accès [!DNL Standard] ou supérieur. Pour plus d’informations, voir la [documentation Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) .

### Liste autorisée {#allowlist}

Avant de créer la destination [!DNL Google Customer Match] en Experience Platform, assurez-vous que votre compte [!DNL Google Ads] est conforme à la [politique de correspondance client de Google](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Les clients disposant de comptes conformes sont automatiquement autorisés par Google.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Google] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences activées vers [!DNL Google Customer Match] peuvent être masquées à partir des identifiants *hachés*, tels que les adresses électroniques ou les numéros de téléphone.

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Google Customer Match] :

* **Ingestion de numéros** de téléphone bruts : vous pouvez ingérer des numéros de téléphone bruts au  [!DNL E.164] format  [!DNL Platform], qui sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans l’espace de noms `Phone_E.164`.
* **Ingestion de numéros** de téléphone hachés : vous pouvez pré-hacher vos numéros de téléphone avant l’ingestion dans  [!DNL Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans l’espace de noms `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Les numéros de téléphone ingérés dans l’espace de noms `Phone` ne peuvent pas être activés dans [!DNL Google Customer Match].

## Exigences en matière de hachage des emails {#hashing-requirements}

Vous pouvez hacher les adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser les adresses électroniques en clair dans Experience Platform et les [!DNL Platform] hacher lors de l’activation.

Pour plus d’informations sur les exigences de hachage de Google et d’autres restrictions sur l’activation, consultez les sections suivantes de la documentation de Google :

* [[!DNL Customer Match] avec adresse électronique, adresse ou identifiant utilisateur](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considérations](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Correspondance client avec numéro de téléphone](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Correspondance client avec les identifiants d’appareil mobile](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, consultez la [présentation de l’ingestion par lots](../../../ingestion/batch-ingestion/overview.md) et la [présentation de l’ingestion par flux](../../../ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences de Google, décrites dans les liens ci-dessus.

## Utilisation d’espaces de noms personnalisés {#custom-namespaces}

Avant de pouvoir utiliser l’espace de noms `User_ID` pour envoyer des données à Google, veillez à synchroniser vos propres identifiants à l’aide de [!DNL gTag]. Consultez la [documentation officielle de Google](https://support.google.com/google-ads/answer/9199250) pour plus d’informations.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## Configuration de la destination : présentation vidéo {#video}

La vidéo ci-dessous présente les étapes de configuration d’une destination [!DNL Google Customer Match] et d’activation de segments. Les étapes sont également présentées de manière séquentielle dans les sections suivantes.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Se connecter à la destination {#connect-destination}

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, faites défiler l’écran jusqu’à la catégorie **[!UICONTROL Publicité]**. Sélectionnez [!DNL Google Customer Match], puis **[!UICONTROL Configurer]**.

![Connexion à la destination de correspondance client Google](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d’informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l’espace de travail de destination.

À l’étape **Compte**, si vous aviez auparavant configuré une connexion à votre destination [!DNL Google Customer Match], sélectionnez **[!UICONTROL Compte existant]** et sélectionnez votre connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à [!DNL Google Customer Match]. Pour vous connecter et connecter Adobe Experience Cloud à votre compte [!DNL Google Ad], sélectionnez **[!UICONTROL Se connecter à la destination]**.

>[!NOTE]
>
>Experience Platform prend en charge la validation des informations d’identification dans le processus d’authentification. Il affiche un message d’erreur si vous saisissez des informations d’identification incorrectes pour votre compte [!DNL Google Ad], afin de vous assurer que vous ne complétez pas le workflow avec des informations d’identification incorrectes.

![Connexion à la destination de correspondance client Google - étape d’authentification](../../assets/catalog/advertising/google-customer-match/connection.png)

Une fois vos informations d’identification confirmées et que Adobe Experience Cloud est connecté à votre compte Google, vous pouvez sélectionner **[!UICONTROL Suivant]** pour passer à l’étape **[!UICONTROL Authentification]** .

![Informations d’identification confirmées](../../assets/catalog/advertising/google-customer-match/connection-success.png)

À l’étape **[!UICONTROL Authentification]**, saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activation et renseignez votre **[!UICONTROL ID de compte Google]**.

Au cours de cette étape, vous pouvez également sélectionner toute **[!UICONTROL action marketing]** qui s’applique à cette destination. Les actions marketing indiquent l’intention pour laquelle les données sont exportées vers la destination. Vous pouvez effectuer un choix parmi des actions marketing définies par l’Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, consultez la [Présentation des stratégies d’utilisation des données](../../../data-governance/policies/overview.md).

Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

>[!IMPORTANT]
>
> * L’action marketing **[!UICONTROL Combiner avec les PII]** est sélectionnée par défaut pour la destination [!DNL Google Customer Match] et ne peut pas être supprimée.
> * Pour les destinations [!DNL Google Customer Match]. **[!UICONTROL L’]** ID de compte est votre ID client avec Google. Le format de l’ID est xxx-xxx-xxxx.


![Connexion à la correspondance client Google - étape d’authentification](../../assets/catalog/advertising/google-customer-match/authentication.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, reportez-vous à la section suivante, [Activation des segments vers [!DNL Google Customer Match]](#activate-segments), pour le reste du workflow.

## Activation des segments vers [!DNL Google Customer Match] {#activate-segments}

Pour plus d’informations sur l’activation des segments vers [!DNL Google Customer Match], voir [Activation des données vers les destinations](../../ui/activate-destinations.md).


À l’étape **[!UICONTROL Planification du segment]** , vous devez fournir l’ [!UICONTROL ID d’application] lors de l’envoi de segments [!DNL IDFA] ou [!DNL GAID] à [!DNL Google Customer Match].

![ID de l’application de correspondance client Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Pour plus d&#39;informations sur la façon de trouver la [!DNL App ID], consultez la [documentation officielle de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

## Vérification de la réussite de l’activation du segment {#verify-activation}

Une fois le flux d’activation terminé, basculez vers votre compte **[!UICONTROL Google Ads]**. Les segments activés s’affichent dans votre compte Google sous forme de listes de clients. En fonction de la taille du segment, certaines audiences ne sont pas renseignées, sauf s’il y a plus de 100 principaux utilisateurs à diffuser.

Lors du mappage d’un segment sur les [!DNL IDFA] et [!DNL GAID] identifiants mobiles, [!DNL Google Customer Match] crée un segment distinct pour chaque mappage d’identifiant. Votre compte [!DNL Google Ads] affiche deux segments différents, l’un pour [!DNL IDFA] et l’autre pour le mappage [!DNL GAID].

## Ressources supplémentaires {#additional-resources}

* [Intégration de la correspondance client Google - Tutoriel vidéo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
