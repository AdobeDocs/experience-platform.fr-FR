---
keywords: google customer match;Google customer match;Google Customer Match
title: Destination de la correspondance client Google
seo-title: Destination de la correspondance client Google
description: Google Customer Match vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées par Google, telles que Search, Shopping, Gmail et YouTube.
seo-description: Google Customer Match vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées par Google, telles que Search, Shopping, Gmail et YouTube.
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 11%

---


# Destination de la correspondance client Google

## Présentation {#overview}

[La Correspondance](https://support.google.com/google-ads/answer/6379332?hl=en) client de Google vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées de Google, comme : [!DNL Search], [!DNL Shopping], [!DNL Gmail]et [!DNL YouTube].

![Destination Google Customer Match dans l’interface utilisateur CDP en temps réel](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la [!DNL Google Customer Match] destination, voici des exemples d’utilisation que les clients de la plate-forme de données clientes en temps réel peuvent résoudre à l’aide de cette fonctionnalité.

### Cas d’utilisation 1

Une marque de vêtements d’athlétisme veut atteindre les clients existants par le biais [!DNL Google Search] et [!DNL Google Shopping] pour personnaliser les offres et les articles en fonction de leurs achats passés et de leur historique de navigation. La marque d’habillement peut assimiler des adresses électroniques de sa propre gestion de la relation client au CDP en temps réel, créer des segments à partir de ses propres données hors ligne et envoyer ces segments à des fins [!DNL Google Customer Match] d’utilisation à l’échelle [!DNL Search] et [!DNL Shopping]en optimisant ses dépenses publicitaires.

### Cas d’utilisation no 2

Une importante société technologique vient de sortir un nouveau téléphone. Afin de promouvoir ce nouveau modèle téléphonique, ils cherchent à sensibiliser les clients qui possèdent déjà des modèles de leurs téléphones aux nouvelles fonctionnalités et fonctionnalités du téléphone.

Pour promouvoir cette version, ils téléchargent les adresses électroniques de leur base de données de gestion de la relation client dans le CDP en temps réel, en utilisant les adresses électroniques comme identifiants. Les segments sont créés en fonction des clients qui possèdent des modèles de téléphone plus anciens et qui les envoient à [!DNL Google Customer Match] des clients actuels, des clients qui possèdent des modèles de téléphone plus anciens, ainsi que des clients similaires sur [!DNL YouTube].

## Gouvernance des données pour les [!DNL Google Customer Match] destinations {#data-governance}

Les destinations dans le CDP en temps réel peuvent avoir certaines règles et obligations pour les données envoyées à la plateforme de destination ou reçues de celle-ci. Il vous incombe de comprendre les limites et les obligations de vos données et de comprendre comment vous les utilisez dans Adobe Experience Platform et la plateforme de destination. Adobe Experience Platform fournit des outils de gouvernance des données pour vous aider à gérer certaines de ces obligations d’utilisation des données. [En savoir plus](../../..//data-governance/labels/overview.md) sur les outils et les stratégies de gouvernance des données.

## Type et identités d’exportation {#export-type}

**Exportation** de segment : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone, etc.) used in the [!DNL Google Customer Match] destination.

**Identités** : vous pouvez utiliser des courriers électroniques bruts ou hachés comme ID de client dans Google

## [!DNL Google Customer Match] conditions préalables du compte {#google-account-prerequisites}

Avant de configurer une [!DNL Google Customer Match] destination dans le CDP en temps réel, veillez à lire et à respecter la politique d’utilisation de Google [!DNL Customer Match], décrite dans la documentation [d’assistance de](https://support.google.com/google-ads/answer/6299717)Google.

### Liste autorisée {#allowlist}

>[!NOTE]
>
>Il est obligatoire d’être ajouté à la liste autorisée de Google avant de configurer votre première [!DNL Google Customer Match] destination dans le CDP en temps réel. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été effectué par Google avant de créer une destination.

Avant de créer la destination dans le CDP en temps réel, vous devez contacter Google et suivre les instructions de liste autorisée de la section [!DNL Google Customer Match] Utiliser les partenaires de correspondance client pour télécharger vos données [](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) dans la documentation Google.


### Conditions requises pour le hachage des courriels {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google exige qu’aucune information d’identification personnelle (PII) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Google Customer Match] doivent être masquées des adresses électroniques *hachées* . Vous pouvez choisir de hacher les adresses électroniques avant de les importer dans Adobe Experience Platform, ou vous pouvez choisir de travailler avec les adresses électroniques en clair dans l&#39;Experience Platform et de faire en sorte que notre algorithme les hache sur l&#39;activation.

Pour plus d&#39;informations sur les exigences de hachage de Google et d&#39;autres restrictions à l&#39;activation, consultez les sections suivantes de la documentation de Google :

* [[!DNL Customer Match] avec adresse électronique, adresse ou ID utilisateur](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considérations](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

Pour en savoir plus sur l&#39;assimilation d&#39;adresses électroniques dans l&#39;Experience Platform, consultez la présentation [de l&#39;assimilation par](../../../ingestion/batch-ingestion/overview.md) lot et la présentation [de l&#39;assimilation par](../../../ingestion/streaming-ingestion/overview.md)flux continu.

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences de Google, décrites dans les liens ci-dessus.


>[!IMPORTANT]
>
>Si vous choisissez de ne pas hacher les adresses électroniques, le CDP en temps réel le fera pour vous lorsque vous activerez des segments vers [!DNL Google Customer Match]. Dans le processus [d’](#activate-segments) activation (voir étape 5), sélectionnez l’ `Email` option comme illustré ci-dessous pour les adresses *de courriel en texte brut et* pour les adresses de courriel `Email_LC_SHA256` *hachées.*

![Hachage sur l’activation](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

## Se connecter à la destination {#connect-destination}

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, faites défiler l’écran jusqu’à la catégorie **[!UICONTROL Publicité]** . Sélectionnez [!DNL Google Customer Match], puis **[!UICONTROL Configurer]**.

![Se connecter à la destination de correspondance client de Google](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

In the **Account** step, if you had previously set up a connection to your [!DNL Google Customer Match] destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to [!DNL Google Customer Match]. Sélectionnez **[!UICONTROL Se connecter à la destination]** pour vous connecter et connecter Adobe Experience Cloud à votre [!DNL Google Ad] compte.

>[!NOTE]
>
>Real-time CDP supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your [!DNL Google Ad] account. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

![Se connecter à la destination de correspondance client de Google - étape d&#39;authentification](../../assets/catalog/advertising/google-customer-match/connection.png)

Once your credentials are confirmed and Adobe Experience Cloud is connected to your Google account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

![Informations d’identification confirmées](../../assets/catalog/advertising/google-customer-match/connection-success.png)

Dans l’étape **[!UICONTROL Authentification]** , saisissez un [!UICONTROL Nom] et une [!UICONTROL Description] pour votre flux d’activation et indiquez à Google l’identifiant de [!UICONTROL compte.]

Cette étape vous permet également de sélectionner tout cas **[!UICONTROL d’utilisation]** marketing à appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](../../../data-governance/policies/overview.md#core-actions)données.

Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

>[!IMPORTANT]
>
> * Le cas d’utilisation **[!UICONTROL Combiner avec les informations d’identification personnelle]** pour le marketing est sélectionné par défaut pour la [!DNL Google Customer Match] destination et ne peut pas être supprimé.
> * Pour [!DNL Google Customer Match] les destinations. **[!UICONTROL L’ID]** de compte correspond à l’ID client de votre client avec Google. Le format de l’ID est xxx-xxx-xxxx.


![Connexion à la correspondance client Google - étape d’authentification](../../assets/catalog/advertising/google-customer-match/authentication.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. In either case, see the next section, [Activate segments to [!DNL Google Customer Match]](#activate-segments), for the rest of the workflow.

## Activate segments to [!DNL Google Customer Match] {#activate-segments}

Pour activer des segments dans [!DNL Google Customer Match], procédez comme suit :

Dans **[!UICONTROL Destinations > Parcourir]**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments.[!DNL Google Customer Match]

Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].

![segments-to-destination](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

À l’étape de mappage **** d’identité, sélectionnez les attributs à inclure en tant qu’identité dans cette destination. Sélectionnez **[!UICONTROL Ajouter un nouveau mappage]** et parcourez votre schéma, sélectionnez Courriel et/ou Courriel haché, puis mappez-les à l’identité de cible correspondante.

![écran initial de mappage d&#39;identité](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

**Adresse électronique en texte ordinaire en tant qu&#39;identité** Principale : Si votre schéma contient des adresses électroniques en texte brut (non hachées) comme identité Principale, sélectionnez le champ de courriel dans vos attributs **** source et faites correspondre au champ Courriel dans la colonne de droite sous Identités **[!UICONTROL de]** Cible, comme indiqué ci-dessous :

![sélectionner l&#39;identité des courriers électroniques en texte brut](../../assets/catalog/advertising/google-customer-match/raw-email.gif)

**Adresse électronique hachée en tant qu&#39;identité** Principale : Si vous avez haché des adresses électroniques en tant qu&#39;identité Principale dans votre schéma, sélectionnez le champ de courriel haché dans vos attributs **** source et faites correspondre au champ Email_LC_SHA256 dans la colonne de droite sous Identités **[!UICONTROL de la]** Cible, comme indiqué ci-dessous :

![sélectionner l&#39;identité des courriels hachés](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

Sur la page de planification **[!UICONTROL des]** segments, vous pouvez définir la date de début pour l’envoi des données vers la destination.

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, le CDP en temps réel recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le processus d’activation de segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir Application [de la](../../../rtcdp/privacy/data-governance-overview.md#enforcement) stratégie dans la section de documentation sur la gouvernance des données.

![confirm-selection](../../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et début d&#39;envoi des données vers la destination.

![confirm-selection](../../assets/catalog/advertising/google-customer-match/review.png)


<!--

Insert in Step 6 when mobile device ID activation is available

    >[!IMPORTANT]
    >
    >If you select mobile device IDs (GAID or IDFA) as primary identity in the Identity mapping step, you must also provide an Application Id in this step. If you selected GAID as identity, see [Set the Application ID](https://developer.android.com/studio/build/application-id) in the Android developer documentation. IF you selected IDFA as identity, see [App ID](https://developer.android.com/studio/build/application-id) in the Apple developer documentation.

    ![segment schedule page](/help/rtcdp/destinations/assets/gcm-segment-schedule.png) 

-->

## Vérification de la réussite de l’activation du segment {#verify-activation}

Une fois le flux d’activation terminé, basculez sur votre compte Publicités **** Google. Les segments activés s’affichent désormais dans votre compte Google en tant que listes client. Notez que selon la taille du segment, certaines audiences ne seront pas renseignées à moins qu’il y ait plus de 100 utilisateurs principaux à diffuser.

## Ressources supplémentaires {#additional-resources}

* [Intégration de la correspondance client Google - Didacticiel vidéo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)