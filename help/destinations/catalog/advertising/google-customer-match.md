---
keywords: correspondance client Google ; correspondance client Google ; correspondance client Google ; correspondance client Google
title: Connexion Google Customer Match
description: Google Customer Match vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées par Google, telles que Search, Shopping, Gmail et YouTube.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 3%

---


# [!DNL Google Customer Match] connexion

[Les ](https://support.google.com/google-ads/answer/6379332?hl=en) correspondances clients de Google vous permettent d&#39;utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées de Google, par exemple :  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail] et  [!DNL YouTube].

![Destination de correspondance client Google dans l’interface utilisateur Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la destination [!DNL Google Customer Match], voici des exemples d&#39;utilisation que les clients Adobe Experience Platform peuvent résoudre en utilisant cette fonctionnalité.

### Cas d’utilisation 1

Une marque de vêtements d’athlétisme souhaite atteindre les clients existants par [!DNL Google Search] et [!DNL Google Shopping] pour personnaliser les offres et les articles en fonction de leurs achats passés et de leur historique de navigation. La marque d’habillement peut assimiler des adresses électroniques de son propre service de gestion de la relation client à un Experience Platform et créer des segments à partir de ses propres données hors ligne. Ensuite, ils peuvent envoyer ces segments à [!DNL Google Customer Match] pour les utiliser dans [!DNL Search] et [!DNL Shopping], en optimisant leurs dépenses publicitaires.

### Cas d’utilisation no 2

Une importante société technologique a lancé un nouveau téléphone. Pour promouvoir ce nouveau modèle de téléphone, ils cherchent à sensibiliser les clients qui possèdent déjà des modèles de leurs téléphones aux nouvelles fonctionnalités et fonctionnalités du téléphone.

Pour promouvoir cette version, ils téléchargent les adresses électroniques de leur base de données de gestion de la relation client vers l’Experience Platform, en utilisant les adresses électroniques comme identifiants. Les segments sont créés en fonction des clients qui possèdent des modèles de téléphone plus anciens. Ensuite, les segments sont envoyés à [!DNL Google Customer Match], afin que la société puisse cible les clients actuels, les clients qui possèdent des modèles de téléphone anciens et les clients similaires sur [!DNL YouTube].

## Gouvernance des données pour les destinations [!DNL Google Customer Match] {#data-governance}

Certaines destinations dans l’Experience Platform ont certaines règles et obligations pour les données envoyées à la plateforme de destination ou reçues de celle-ci. Il vous incombe de comprendre les limites et les obligations de vos données et de comprendre comment vous les utilisez dans Adobe Experience Platform et la plateforme de destination. Adobe Experience Platform fournit des outils de gouvernance des données pour vous aider à gérer certaines de ces obligations d’utilisation des données. [En savoir ](../../..//data-governance/labels/overview.md) plus sur les outils et les stratégies de gouvernance des données.

## Identités prises en charge {#supported-identities}

[!DNL Google Customer Match] prend en charge l&#39;activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité de cible | Description | Considérations |
|---|---|---|
| GAID | Identifiant Google Advertising | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage IDFA. |
| phone_sha256_e.164 | Numéros de téléphone au format E164, hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Suivez les instructions de la section [Exigences de correspondance d&#39;ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de nommage appropriés pour les numéros de téléphone en texte brut et hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hachage automatiquement les données sur l’activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section [Exigences de correspondance d&#39;ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de nommage appropriés pour les adresses électroniques en texte brut et hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hachage automatiquement les données sur l’activation. |
| user_id | ID utilisateur personnalisés | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage personnalisé. |

## Type d&#39;exportation {#export-type}

**Exportation**  de segment : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone et autres) utilisés dans la  [!DNL Google Customer Match] destination.

## [!DNL Google Customer Match] conditions préalables du compte  {#google-account-prerequisites}

Avant de configurer une destination [!DNL Google Customer Match] dans l&#39;Experience Platform, veillez à lire et à respecter la politique de Google concernant l&#39;utilisation de [!DNL Customer Match], décrite dans la [documentation d&#39;assistance de Google](https://support.google.com/google-ads/answer/6299717).

### Liste autorisée {#allowlist}

>[!NOTE]
>
>Il est obligatoire d’être ajouté à la liste autorisée de Google avant de configurer votre première destination [!DNL Google Customer Match] en Experience Platform. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été effectué par Google avant de créer une destination.

Avant de créer la destination [!DNL Google Customer Match] en Experience Platform, vous devez contacter Google et suivre les instructions de liste autorisée de [Utiliser les partenaires de correspondance client pour télécharger vos données](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) dans la documentation de Google.

Il existe également une seconde liste autorisée Google à laquelle vous devez ajouter votre compte si vous prévoyez de télécharger des données à l’aide de [User_ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id) de Google. Pour ajouter votre compte à la liste autorisée, contactez votre gestionnaire de compte Google.

## Exigences de correspondance d&#39;ID {#id-matching-requirements}

[!DNL Google] exige qu’aucune information d’identification personnelle (identification personnelle) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Google Customer Match] peuvent être masquées par des identifiants *hachés*, tels que des adresses électroniques ou des numéros de téléphone.

En fonction du type d’ID que vous saisissez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Google Customer Match] :

* **Incorporation de numéros** de téléphone bruts : vous pouvez assimiler des numéros de téléphone bruts au  [!DNL E.164] format  [!DNL Platform], et ils sont automatiquement hachés à l&#39;activation. Si vous choisissez cette option, veillez à toujours intégrer vos numéros de téléphone bruts dans l&#39;espace de nommage `Phone_E.164`.
* **Invitation de numéros** de téléphone hachés : vous pouvez pré-hacher vos numéros de téléphone avant l&#39;assimilation dans  [!DNL Platform]. Si vous choisissez cette option, veillez à toujours intégrer vos numéros de téléphone hachés dans l&#39;espace de nommage `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Les numéros de téléphone saisis dans l&#39;espace de nommage `Phone` ne peuvent pas être activés dans [!DNL Google Customer Match].

## Conditions requises pour le hachage des courriels {#hashing-requirements}

Vous pouvez hacher des adresses électroniques avant de les importer dans Adobe Experience Platform ou utiliser des adresses électroniques en clair dans l’Experience Platform et les faire [!DNL Platform] hacher sur l’activation.

Pour plus d&#39;informations sur les exigences de hachage de Google et d&#39;autres restrictions à l&#39;activation, consultez les sections suivantes de la documentation de Google :

* [[!DNL Customer Match] avec adresse électronique, adresse ou ID utilisateur](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considérations](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Correspondance client avec numéro de téléphone](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Correspondance client avec les ID de périphérique mobile](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Pour en savoir plus sur l’assimilation d’adresses électroniques dans l’Experience Platform, consultez les sections [présentation de l’assimilation par lots](../../../ingestion/batch-ingestion/overview.md) et [présentation de l’assimilation en flux continu](../../../ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences de Google, décrites dans les liens ci-dessus.

## Utilisation d’espaces de nommage personnalisés {#custom-namespaces}

Avant de pouvoir utiliser l&#39;espace de nommage `User_ID` pour envoyer des données à Google, veillez à synchroniser vos propres identifiants à l&#39;aide de [!DNL gTag]. Consultez la [documentation officielle de Google](https://support.google.com/google-ads/answer/9199250) pour obtenir des informations détaillées.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## Se connecter à la destination {#connect-destination}

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, faites défiler la catégorie **[!UICONTROL Publicité]**. Sélectionnez [!DNL Google Customer Match], puis **[!UICONTROL Configurer]**.

![Se connecter à la destination de correspondance client de Google](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Si une connexion à cette destination existe, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l&#39;étape **Compte**, si vous aviez précédemment configuré une connexion à votre destination [!DNL Google Customer Match], sélectionnez **[!UICONTROL Compte existant]** et sélectionnez votre connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à [!DNL Google Customer Match]. Pour vous connecter et connecter Adobe Experience Cloud à votre compte [!DNL Google Ad], sélectionnez **[!UICONTROL Se connecter à destination]**.

>[!NOTE]
>
>L’Experience Platform prend en charge la validation des informations d’identification dans le processus d’authentification. Il affiche un message d’erreur si vous saisissez des informations d’identification incorrectes dans votre compte [!DNL Google Ad], afin de vous assurer que vous ne terminez pas le flux de travail avec des informations d’identification incorrectes.

![Se connecter à la destination de correspondance client de Google - étape d&#39;authentification](../../assets/catalog/advertising/google-customer-match/connection.png)

Une fois vos informations d’identification confirmées et que Adobe Experience Cloud est connecté à votre compte Google, vous pouvez sélectionner **[!UICONTROL Suivant]** pour passer à l’étape **[!UICONTROL Authentification]**.

![Informations d’identification confirmées](../../assets/catalog/advertising/google-customer-match/connection-success.png)

À l’étape **[!UICONTROL Authentification]**, saisissez **[!UICONTROL Nom]** et **[!UICONTROL Description]** pour votre flux d’activation et renseignez votre **[!UICONTROL ID de compte]** Google.

Au cours de cette étape, vous pouvez également sélectionner toute **[!UICONTROL action marketing]** qui s’applique à cette destination. Les actions marketing indiquent l’intention pour laquelle les données sont exportées vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer votre propre action marketing. Pour plus d&#39;informations sur les actions marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

>[!IMPORTANT]
>
> * L&#39;action marketing **[!UICONTROL Combiner avec les informations d&#39;identification personnelle]** est sélectionnée par défaut pour la destination [!DNL Google Customer Match] et ne peut pas être supprimée.
> * Pour les destinations [!DNL Google Customer Match]. **[!UICONTROL L’]** ID de compte correspond à l’ID client de votre client avec Google. Le format de l’ID est xxx-xxx-xxxx.


![Connexion à la correspondance client Google - étape d’authentification](../../assets/catalog/advertising/google-customer-match/authentication.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, consultez la section suivante, [Activer les segments à [!DNL Google Customer Match]](#activate-segments), pour le reste du flux de travail.

## Activer les segments dans [!DNL Google Customer Match] {#activate-segments}

Pour savoir comment activer des segments dans [!DNL Google Customer Match], voir [Activer les données vers les destinations](../../ui/activate-destinations.md).


À l’étape **[!UICONTROL Calendrier de segment]**, vous devez fournir l’[!UICONTROL ID d’application] lors de l’envoi de segments [!DNL IDFA] ou [!DNL GAID] à [!DNL Google Customer Match].

![Identifiant de l’application de correspondance client Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Pour plus d&#39;informations sur la façon de trouver le [!DNL App ID], consultez la [documentation officielle de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

## Vérification de la réussite de l’activation du segment {#verify-activation}

Une fois le flux d’activation terminé, basculez sur votre compte **[!UICONTROL Publicités Google]**. Les segments activés s’affichent dans votre compte Google en tant que listes client. Notez que selon la taille du segment, certaines audiences ne sont pas renseignées à moins qu’il y ait plus de 100 utilisateurs principaux à diffuser.

Lors du mappage d’un segment avec les identifiants mobiles [!DNL IDFA] et [!DNL GAID], [!DNL Google Customer Match] crée un segment distinct pour chaque mappage d’ID. Votre compte [!DNL Google Ads] présente deux segments différents, l&#39;un pour [!DNL IDFA] et l&#39;autre pour le mappage [!DNL GAID].

## Ressources supplémentaires {#additional-resources}

* [Intégration de la correspondance client Google - Didacticiel vidéo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)