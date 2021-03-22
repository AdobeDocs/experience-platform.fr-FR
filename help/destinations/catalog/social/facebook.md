---
keywords: connexion facebook;connexion facebook;destinations facebook;facebook;instagram;messenger;facebook messenger Messenger
title: Connexion Facebook
description: Activez des profils pour vos campagnes Facebook pour le ciblage, la personnalisation et la suppression des audiences en fonction des courriers électroniques hachés.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 8%

---


# [!DNL Facebook] connexion

Activez des profils pour vos campagnes [!DNL Facebook] pour le ciblage, la personnalisation et la suppression des audiences en fonction des courriers électroniques hachés.

Vous pouvez utiliser cette destination pour le ciblage des audiences dans la famille [!DNL Facebook’s] d’applications prises en charge par [!DNL Custom Audiences], y compris [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] et [!DNL Messenger]. La sélection de l’application sur laquelle vous souhaitez exécuter la campagne est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].

![Destination Facebook dans l’interface utilisateur Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la destination [!DNL Facebook], voici deux exemples d&#39;utilisation que les clients de Adobe Experience Platform peuvent résoudre en utilisant cette fonctionnalité.

### Cas d’utilisation 1

Un détaillant en ligne souhaite atteindre les clients existants par le biais de plateformes sociales et leur montrer des offres personnalisées en fonction de leurs commandes précédentes. Le détaillant en ligne peut ingérer des adresses électroniques de sa propre gestion de la relation client vers Adobe Experience Platform, créer des segments à partir de ses propres données hors ligne et envoyer ces segments à la [!DNL Facebook] plate-forme sociale, en optimisant les dépenses publicitaires.

### Cas d’utilisation no 2

Une compagnie aérienne a différents niveaux de clients (Bronze, Argent et Or) et veut fournir à chacun des niveaux des offres personnalisées via des plateformes sociales. Cependant, tous les clients n’utilisent pas l’application mobile de la compagnie aérienne et certains d’entre eux ne se sont pas connectés au site Web de la société. Les seuls identifiants dont dispose la société à propos de ces clients sont les identifiants d’adhésion et les adresses électroniques.

Pour les cible sur les réseaux sociaux, ils peuvent intégrer les données client de leur gestion de la relation client dans Adobe Experience Platform, en utilisant les adresses électroniques comme identifiants.

Ensuite, ils peuvent utiliser leurs données hors ligne, y compris les ID d&#39;adhésion et les niveaux de clients associés, pour créer de nouveaux segments d&#39;audience qu&#39;ils peuvent cible via la destination [!DNL Facebook].

## Gouvernance des données pour les destinations [!DNL Facebook] {#data-governance}

>[!IMPORTANT]
>
>Les données envoyées à [!DNL Facebook] ne peuvent pas inclure d’identités assemblées. Vous êtes responsable du respect de cette obligation et pouvez le faire en vous assurant que les segments sélectionnés pour l’activation n’utilisent pas d’option de raccordement dans leur stratégie de fusion. En savoir plus sur [les stratégies de fusion](/help/profile/ui/merge-policies.md).

## Identités prises en charge {#supported-identities}

[!DNL Facebook Custom Audiences] prend en charge l&#39;activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité de cible | Description | Considérations |
|---|---|---|
| GAID | Identifiant Google Advertising | Sélectionnez l&#39;identité de la cible GAID lorsque votre identité source est un espace de nommage GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité de la cible IDFA lorsque votre identité source est un espace de nommage IDFA. |
| phone_sha256 | Numéros de téléphone hachés avec l&#39;algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Suivez les instructions de la section [Exigences de correspondance d&#39;ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de nommage appropriés pour les numéros de téléphone en texte brut et hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hachage automatiquement les données sur l’activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section [Exigences de correspondance d&#39;ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de nommage appropriés pour les adresses électroniques en texte brut et hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hachage automatiquement les données sur l’activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage personnalisé. |

## Type d&#39;exportation {#export-type}

**Exportation**  de segment : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination Facebook.

## Conditions préalables du compte Facebook {#facebook-account-prerequisites}

Avant d’envoyer vos segments ciblés à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

- L&#39;autorisation **[!DNL Manage campaigns]** doit être activée pour votre compte d&#39;utilisateur [!DNL Facebook] pour le compte d&#39;annonce que vous prévoyez d&#39;utiliser.
- Le compte commercial **Adobe Experience Cloud** doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Pour plus d&#39;informations, consultez [Ajouter des partenaires à votre gestionnaire d&#39;entreprise](https://www.facebook.com/business/help/1717412048538897) dans la documentation Facebook.
   >[!IMPORTANT]
   >
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. L&#39;autorisation est requise pour l&#39;intégration [!DNL Adobe Experience Platform].
- Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` correspond à votre [!DNL Facebook Ad Account ID].

## Exigences de correspondance d&#39;ID {#id-matching-requirements}

[!DNL Facebook] exige qu’aucune information d’identification personnelle (identification personnelle) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Facebook] peuvent être masquées par des identifiants *hachés*, tels que des adresses électroniques ou des numéros de téléphone.

En fonction du type d’ID que vous saisissez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Facebook] :

- **Incorporation de numéros** de téléphone bruts : vous pouvez ingérer des numéros de téléphone bruts au  [!DNL E.164] format  [!DNL Platform]. Ils se sont automatiquement heurtés à l&#39;activation. Si vous choisissez cette option, veillez à toujours intégrer vos numéros de téléphone bruts dans l&#39;espace de nommage `Phone_E.164`.
- **Invitation de numéros** de téléphone hachés : vous pouvez pré-hacher vos numéros de téléphone avant l&#39;assimilation dans  [!DNL Platform]. Si vous choisissez cette option, veillez à toujours intégrer vos numéros de téléphone hachés dans l&#39;espace de nommage `Phone_SHA256`.

>[!NOTE]
>
>Les numéros de téléphone saisis dans l&#39;espace de nommage `Phone` ne peuvent pas être activés dans [!DNL Facebook].


## Conditions requises pour le hachage des courriels {#email-hashing-requirements}

Vous pouvez hacher des adresses électroniques avant de les importer dans Adobe Experience Platform ou utiliser des adresses électroniques en clair dans l’Experience Platform et les faire [!DNL Platform] hacher sur l’activation.

Pour en savoir plus sur l’assimilation d’adresses électroniques dans l’Experience Platform, consultez les sections [présentation de l’assimilation par lots](/help/ingestion/batch-ingestion/overview.md) et [présentation de l’assimilation en flux continu](/help/ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

- Rogner tous les espaces de début et de fin de la chaîne de courriel ; exemple : `johndoe@example.com`, et non `<space>johndoe@example.com<space>`;
- Lors du hachage des chaînes de courrier électronique, veillez à mettre la chaîne en minuscules en hachage ;
   - Exemple : `example@email.com`, et non `EXAMPLE@EMAIL.COM`;
- Assurez-vous que la chaîne hachée est en minuscules.
   - Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, et non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Ne salez pas la chaîne.

>[!NOTE]
>
>Les données des espaces de nommage non hachés sont automatiquement hachées par [!DNL Platform] à l&#39;activation.
> Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hachage automatiquement les données sur l’activation.
> L&#39;option **[!UICONTROL Appliquer la transformation]** s&#39;affiche uniquement lorsque vous sélectionnez des attributs comme champs source. Elle ne s’affiche pas lorsque vous choisissez des espaces de nommage.

![Transformation du mappage des identités](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilisation d’espaces de nommage personnalisés {#custom-namespaces}

Avant de pouvoir utiliser l&#39;espace de nommage `Extern_ID` pour envoyer des données à [!DNL Facebook], veillez à synchroniser vos propres identifiants à l&#39;aide de [!DNL Facebook Pixel]. Consultez la [documentation officielle](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) pour obtenir des informations détaillées.

## Se connecter à la destination {#connect-destination}

Pour vous connecter à la destination [!DNL Facebook], voir le [Processus d’authentification des destinations de réseau social](./workflow.md).

## Activer les segments dans [!DNL Facebook] {#activate-segments}

Pour savoir comment activer des segments dans [!DNL Facebook], voir [Activer les données vers les destinations](../../ui/activate-destinations.md).

À l&#39;étape **[!UICONTROL Planification des segments]**, vous devez fournir l&#39;[!UICONTROL Origine d&#39;audience] lors de l&#39;envoi de segments à [!DNL Facebook Custom Audiences].

![Origine Facebook de l&#39;Audience](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Données exportées {#exported-data}

Pour [!DNL Facebook], une activation réussie signifie qu&#39;une audience personnalisée [!DNL Facebook] serait créée par programmation dans [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’adhésion au segment dans l’audience est ajoutée ou supprimée selon que les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL Facebook] prend en charge les remplissages d’audiences historiques. Toutes les qualifications des segments historiques sont envoyées à [!DNL Facebook] lorsque vous activez les segments vers la destination.