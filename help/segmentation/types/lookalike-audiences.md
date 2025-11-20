---
solution: Experience Platform
title: Audiences Similaires
description: Découvrez comment cibler de nouvelles audiences à forte valeur ajoutée dans Adobe Experience Platform à l’aide d’audiences semblables.
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: 03f8124f0fc750efa9b7bca0ff80de4c9263915d
workflow-type: tm+mt
source-wordcount: '2250'
ht-degree: 10%

---

# Guide des audiences semblables

>[!IMPORTANT]
>
>Les informations semblables et les audiences semblables sont automatiquement désactivées pour les environnements qui affichent une faible utilisation. Une faible utilisation est définie comme le fait de ne pas afficher d’informations semblables au cours des trois derniers mois ou de ne pas créer d’audience semblable au cours des six derniers mois.
>
>Si les informations semblables sont désactivées pour votre environnement, vous pouvez demander l’accès en envoyant un e-mail à l’équipe d’assistance clientèle d’Adobe, y compris votre identifiant d’organisation et les détails de l’environnement dans votre message.
>
>Après réception de la confirmation de l’assistance clientèle d’Adobe, les informations et audiences semblables seront activées dans tous les sandbox de votre environnement.

Dans Adobe Experience Platform, les audiences semblables fournissent des informations intelligentes sur chacune de vos audiences, en s’appuyant sur des informations basées sur le machine learning pour identifier et cibler les clients à forte valeur ajoutée avec vos campagnes marketing.

Les audiences semblables vous permettent de créer des audiences étendues qui ciblent des clients similaires à vos audiences hautement performantes ou des clients similaires à des audiences converties précédemment.

## Terminologie {#terminology}

Avant de commencer à utiliser des audiences semblables, veillez à bien comprendre les concepts suivants :

- **Audience de base** : l’audience de base est l’audience sur laquelle vous souhaitez en savoir plus. Il s’agit de l’audience sur laquelle le modèle similaire est **basé**.
- **Modèle similaire** : un modèle similaire est un modèle de machine learning entraîné sur chaque audience de base éligible sans aucune entrée client. Chaque modèle similaire crée les facteurs d’influence et les graphiques de similarité. Un modèle similaire n’est **noté**
- **Audience semblable** : une audience semblable est l’audience créée lorsqu’un modèle semblable avec un seuil de similarité sélectionné est appliqué à l’audience de base. Vous pouvez créer plusieurs audiences semblables à l’aide du même modèle de similaire. L’audience semblable est celle qui est notée.
- **Taille totale de l’audience adressable** : la taille totale de l’audience adressable est le nombre total de profils au cours des 30 derniers jours, moins la population de l’audience de base au cours des 30 derniers jours. Par exemple, si un client possède 10 millions de profils au cours des 30 derniers jours et que l’audience de base en possède 1 million au cours des 30 derniers jours, la taille totale de l’audience adressable est de 9 millions de profils.

## Admissibilité {#eligibility}

Pour utiliser des informations semblables, l’audience de base **doit** doit répondre aux critères d’éligibilité suivants :

- L’audience de base **doit** doit être créée dans Experience Platform.
   - Les audiences générées de manière externe ne sont **pas** éligibles aux informations semblables.
- L’audience de base **doit** se trouve dans la politique de fusion par défaut.
- L’audience de base **ne doit** pas utiliser de champs limités par la gouvernance des données.

## Détails du modèle analogue {#details}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_notEligible"
>title="Non éligible"
>abstract="Cette audience n’est actuellement pas éligible aux informations analogues, car elle peut avoir moins que le nombre minimum de profils requis pour la formation, ou l’exportation de profils n’a pas encore été déclenchée."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_processing"
>title="En cours de traitement"
>abstract="Cette audience est en cours de traitement. Le traitement du modèle peut prendre jusqu’à 24 heures. Veuillez réessayer plus tard."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_error"
>title="Erreur"
>abstract="Une erreur s’est produite lors du traitement de ce modèle. Supprimez et recréez ce modèle ou réessayez plus tard."

Dans Adobe Experience Platform, le modèle similaire utilise trois types de points de données différents :

- Appartenance à l’audience au cours des 30 derniers jours
- Événements d’expérience des 30 derniers jours qui ont été ingérés dans le profil client en temps réel
- Attributs de profil ingérés dans le profil client en temps réel au cours des 30 derniers jours

Tous ces points de données sont transformés en paires clé-valeur qui sont intégrées au modèle similaire. Seules les paires clé-valeur avec un pourcentage significatif de profils correspondant seront conservées.

Actuellement, le modèle similaire est exécuté toutes les 24 heures, créant et recréant les facteurs d’influence et les graphiques de similarité pour les audiences de base. La notation des audiences semblables est également exécutée fréquemment.

## Droits {#entitlements}

Les droits suivants s’appliquent à l’utilisation des audiences semblables :

- Les clients Real-Time CDP Prime ont droit à des audiences **5** actives dans les sandbox de production
- Les clients Real-Time CDP Ultimate ont droit à des audiences semblables actives de **20** dans les sandbox de production
- Les sandbox de développement sont limités à des audiences semblables **5** pour tous les clients Real-Time CDP

Les packs de modules complémentaires, qui seront disponibles à une date ultérieure, augmentent les droits pour les sandbox de production de 20 audiences semblables par pack.

## Accès {#access}

Pour confirmer si vous avez accès à des audiences semblables, sélectionnez une audience dans le portail d’audiences et vérifiez si l’onglet **[!UICONTROL Look-alike insights]** est visible.

## Affichage d’informations semblables {#view}

Les informations semblables sont intégrées à la page des détails de l’audience. Pour afficher les informations semblables pour une audience, sélectionnez **[!UICONTROL Audiences]** dans la barre de navigation de gauche, suivi de **[!UICONTROL Browse]**, et de l’audience pour laquelle vous souhaitez afficher les informations.

![Le bouton Audiences est mis en surbrillance, ainsi que l’audience de base utilisée pour la modélisation similaire.](../images/types/lookalike/browse.png)

La page Détails de l’audience s’affiche. Sélectionnez **[!UICONTROL Look-alike insights]** onglet pour afficher les informations semblables de l’audience. La page **[!UICONTROL Look-alike insights]** s’affiche. Cette page comporte trois éléments principaux : le graphique de similarité et de portée, les audiences semblables et les facteurs d’influence.

![L’onglet Informations semblables est mis en surbrillance, affichant les informations semblables pour l’audience de base.](../images/types/lookalike/look-alike-insights.png)

### Similarité et portée {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Similarité et portée"
>abstract="Le graphique de similarité et de portée trace la portée attendue d’une audience analogue composée de profils au-dessus d’un score de similarité donné. Vous pouvez pointer sur un point spécifique du graphique pour afficher le pourcentage de similarité et le nombre de profils attendu pour le point actuellement surligné."

La section Similarité et portée affiche un graphique qui trace la portée attendue d’une audience semblable composée de profils au-dessus d’un score de similarité donné. Le score de similarité représente la **distance** de similarité entre le profil de l’audience de base et le profil insight similaire.

![Le graphique de similarité et de portée est mis en surbrillance.](../images/types/lookalike/similarity-and-reach.png)

Sur ce graphique, l’axe X mesure le pourcentage de similarité entre un profil et les membres de l’audience sélectionnée. Le score de similarité s’étend de 0 % à 100 %, un score de similarité plus élevé indiquant qu’un profil est plus proche des membres de l’audience sélectionnée en termes de valeurs de facteur d’influence.

L’axe des ordonnées affiche le nombre attendu de profils avec le pourcentage de similarité qui correspond à la valeur correspondante de l’axe des abscisses. Ce nombre attendu de profils va de 0 à la taille totale de l’audience adressable ou à 25 millions de profils, selon la valeur la plus faible. Cet axe est mesuré sur une **échelle logarithmique** pour améliorer la lisibilité du graphe.

Notez que le graphique est **cumulatif** de droite à gauche. Cela signifie qu’en tout point du graphique, la valeur de l’axe des ordonnées est le nombre de profils ayant une similarité **supérieure** au seuil de similarité. Par exemple, si l’axe X est à 60 % et l’axe Y à 10 millions, cela signifie qu’il y a 10 millions de profils qui ont une similarité égale ou supérieure à 60 % avec l’audience de base.

Vous pouvez pointer sur un point spécifique du graphique pour afficher le pourcentage de similarité et le nombre de profils attendu pour le point actuellement surligné.

### Audiences similaires {#list}

La section Audiences semblables affiche une liste de toutes les audiences semblables qui ont été créées précédemment pour l’audience de base sélectionnée.

![La section Audiences semblables est mise en surbrillance.](../images/types/lookalike/select-laa.png)

### Facteurs d’influence {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Facteurs d’influence"
>abstract="Les facteurs d’influence sont les attributs, les événements et les appartenances à une audience qui sont importants pour expliquer la similarité d’un profil aux profils membres de l’audience de base.Les libellés et politiques d’utilisation des données peuvent être utilisés pour exclure certaines données en tant que facteurs d’influence dans les modèles analogues."
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/segmentation/types/lookalike-audiences#exclude" text="Exclure des données"

La section Facteurs d’influence affiche les 100 principaux facteurs qui influencent le modèle similaire pour l’audience de base sélectionnée. Ces facteurs d’influence sont les attributs de profil, les événements d’expérience et les appartenances à l’audience qui sont les plus importants pour expliquer les similitudes dans l’audience de base. Comprendre les facteurs d’influence principaux vous permet de mieux personnaliser votre contenu marketing pour cette audience et pour toute audience semblable que vous créez à partir de celle-ci. Notez que tous les facteurs d’influence qui affectent le modèle similaire ne s’affichent pas.

Pour les facteurs d’influence numériques, les paires clé-valeur peuvent être placées dans des intervalles, en fonction du nombre de valeurs différentes de la clé. Par exemple, si vous disposez d’une clé de `income`, il y aura probablement de nombreuses valeurs uniques. Par conséquent, les paires clé-valeur seront placées dans des compartiments pouvant ressembler à `income=[0 -> 30000]`, `income=[30000 -> 50000]` et `income=[50000 -> 100000]`.

Ces intervalles sont régulièrement recalculés pour s’assurer que les données sont tenues à jour.

![La section facteurs d’influence est mise en surbrillance.](../images/types/lookalike/influential-factors.png)

>[!NOTE]
>
>Les facteurs d’influence sont triés par ordre d’importance et sont indépendants les uns des autres.

| Champ | Description |
| ----- | ----------- |
| Type | Type de données à partir duquel le facteur d’influence est dérivé. Il peut s’agir d’un attribut de profil, d’un événement d’expérience ou d’une appartenance à une audience. |
| Clé | Nom du champ de données. Pour les clés du type d’appartenance à l’audience, cette valeur représente l’**espace de noms** de l’audience d’où proviennent les données. Les valeurs possibles sont `ups` (Segmentation Service) et `AO` (Audience Orchestration). Pour les clés d’autres types, cette valeur représente le chemin du champ XDM. Par exemple, si la société Luma dispose d’un champ personnalisé appelé revenu, la clé est `_luma.income` |
| Valeur | La valeur varie en fonction du facteur d’influence qu’elle représente. Pour les attributs de profil ou les événements d’expérience, ce champ représente la valeur ou la plage de valeurs du champ de données qui indique la similitude avec les membres de l’audience de base. La plage de valeurs est écrite sous la forme `[A -> B]`, où `A` représente la plage inférieure tandis que `B` représente la plage supérieure. Pour les appartenances à l’audience, ce champ correspond au nom de l’audience. |
| Importance | Niveau relatif d’importance du facteur d’influence. Elle peut être élevée, moyenne ou faible. |

## Créer une audience semblable {#create}

>[!IMPORTANT]
>
>Vous **ne pouvez pas** utiliser une audience semblable comme audience de base pour une autre audience semblable. En d’autres termes, vous **pouvez pas** créer des audiences semblables chaînées.

Pour créer une audience semblable, vous devez sélectionner l’audience sur laquelle vous souhaitez baser l’audience semblable. Pour accéder à la liste des audiences disponibles, sélectionnez **[!UICONTROL Audiences]** dans la barre de navigation de gauche, puis **[!UICONTROL Browse]**. La liste des audiences s’affiche. Sur cette page, vous pouvez sélectionner l’audience que vous souhaitez utiliser comme audience de base.

![Le bouton Audiences est mis en surbrillance, ainsi que l’audience de base utilisée pour la modélisation similaire.](../images/types/lookalike/browse.png)

Sur la page des détails de l’audience, sélectionnez **[!UICONTROL Create look-alike audience]** pour lancer le processus de création d’une audience semblable.

![Le bouton [!UICONTROL Create look-alike audience] est mis en surbrillance.](../images/types/lookalike/create-look-alike-audience.png)

La fenêtre contextuelle **[!UICONTROL Create a look-alike audience]** s’affiche. Sur cette page, vous pouvez définir le pourcentage de similarité de l’audience semblable.

![La fenêtre contextuelle [!UICONTROL Create a look-alike audience] s’affiche.](../images/types/lookalike/create-audience.png)

Vous pouvez définir ce pourcentage de similarité de trois manières différentes :

- Déplacez le curseur pour définir le pourcentage de similarité
- Saisissez le pourcentage de similarité dans la zone de saisie numérique située en regard du curseur
- Pointez sur le graphique et sélectionnez l’emplacement souhaité pour définir le pourcentage de similarité

Vous pouvez également mettre à jour les détails de l’audience semblable, y compris son nom et sa description. Par défaut, le nom de l’audience semblable est généré en fonction du nom de l’audience de base et du pourcentage de similarité précédemment spécifiés.

![Les informations de base sont mises en surbrillance dans la fenêtre contextuelle du [!UICONTROL Create a look-alike audience].](../images/types/lookalike/basic-info.png)

Sélectionnez **[!UICONTROL Create]** pour terminer la création de votre audience semblable.

![Le bouton Créer est mis en surbrillance dans la fenêtre contextuelle de [!UICONTROL Create a look-alike audience].](../images/types/lookalike/create-audience.png)

L’audience semblable nouvellement créée est accessible dans la section **[!UICONTROL Look-alike audiences]** de la page des détails de l’audience. Elle est également disponible dans le portail d’audiences et pour d’autres utilisations en aval. Notez que la notation de l’audience semblable prendra un certain temps. Jusqu’à ce qu’il soit noté, le nombre de profils semblera être égal à 0.

## Afficher les détails de l’audience semblable {#view-details}

Pour afficher les détails d’une audience semblable, sélectionnez-la dans la section **[!UICONTROL Look-alike audiences]** de l’audience de base.

![La section Audiences semblables est mise en surbrillance.](../images/types/lookalike/select-laa.png)

La page Détails de l’audience s’affiche. Pour plus d’informations sur cette page, veuillez lire la section [détails de l’audience) de la présentation d’Audience Portal](../ui/audience-portal.md#audience-details).

![Les détails de l’audience semblable s’affichent.](../images/types/lookalike/laa-details.png)

## Exclure les champs de données de la modélisation semblable {#exclude}

>[!IMPORTANT]
>
> **Vous** êtes chargé de vous assurer que les données, y compris les données sensibles, sont étiquetées de manière appropriée et que les politiques d’utilisation des données ont été définies et activées pour se conformer aux obligations légales et réglementaires en vertu desquelles vous opérez. Vous devez également savoir que les champs de données ou les appartenances à des segments qui ne sont **pas** directement corrélés aux champs de données généralement associés à des types de données sensibles ou protégés peuvent être une source de biais potentiel. **Vous** êtes responsable de l’analyse de vos données afin d’identifier, d’étiqueter et d’appliquer les politiques d’utilisation des données appropriées à vos données, y compris tous les champs de données qui peuvent servir de proxy pour les types de données sensibles ou protégées et qui doivent être exclus de la modélisation.

Les audiences semblables peuvent être configurées pour exclure les champs de données qui sont limités à l’action marketing « Science des données » en appliquant les politiques et les libellés d’utilisation des données appropriés. Les données étiquetées comme étant interdites d’utilisation pour la science des données seront supprimées de la considération lors de l’entraînement d’un modèle d’audience semblable et lors de la génération d’une audience semblable à partir du modèle entraîné. 

>[!NOTE]
>
>Les modifications apportées aux libellés d’utilisation des données sur l’audience de base peuvent prendre jusqu’à 48 heures pour prendre effet.

Le libellé « C9 » standard peut être utilisé pour libeller les données qui ne doivent pas être utilisées pour la science des données et peut être appliqué en activant la politique « Restreindre la science des données » standard. Vous pouvez également créer des politiques supplémentaires pour restreindre l’utilisation des données avec d’autres libellés, y compris les libellés sensibles, à la science des données. Pour plus d’informations sur la gestion des politiques d’utilisation des données, consultez le guide de l’interface utilisateur [politiques d’utilisation des données](../../data-governance/policies/user-guide.md). Pour plus d’informations sur la gestion des libellés d’utilisation des données, consultez le [guide de l’interface utilisateur des libellés d’utilisation des données](../../data-governance/labels/user-guide.md).

Par défaut, si une audience de base n’a pas de libellés de contrat, le processus de modélisation des audiences semblables exclura **tout** champ, jeu de données ou audience en fonction de la politique de confidentialité activée pour votre organisation.

## Étapes suivantes

Après lecture de ce guide, vous avez appris à afficher des informations semblables et à créer des audiences semblables en fonction de ces informations. Pour plus d’informations sur les audiences dans l’interface utilisateur de Adobe Experience Platform, veuillez lire le [&#x200B; Guide de l’interface utilisateur de Segmentation Service](./overview.md).
