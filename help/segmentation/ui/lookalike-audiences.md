---
solution: Experience Platform
title: Audiences similaires
description: Découvrez comment cibler de nouvelles audiences à forte valeur ajoutée dans Adobe Experience Platform à l’aide d’audiences look-alike.
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 10%

---

# Guide des audiences semblables

>[!IMPORTANT]
>
>Les insights semblables et les audiences semblables ne sont disponibles que dans la variable **Modification B2C**.

Dans Adobe Experience Platform, les audiences look-alike fournissent des insights intelligents sur chacune de vos audiences, en exploitant les insights basés sur l’apprentissage automatique pour identifier et cibler les clients à forte valeur ajoutée dans vos campagnes marketing.

Avec les audiences look-alike, vous pouvez créer des audiences étendues qui ciblent des clients similaires à vos audiences hautement performantes ou des clients ciblés similaires aux audiences converties précédemment.

## Terminologie {#terminology}

Avant de commencer avec les audiences look-alike, veillez à comprendre les concepts suivants :

- **Audience de base**: l’audience de base est l’audience dont vous souhaitez obtenir plus d’informations. Il s’agit de l’audience que le modèle analogue est **based** sur .
- **Modèle analogue**: un modèle analogue est un modèle d’apprentissage automatique formé sur chaque audience de base éligible sans aucune entrée client. Chaque modèle analogue crée des facteurs d’influence et des graphiques de similarité. Un modèle analogue fait **not** on obtient un score.
- **Audience analogue**: une audience analogue est l’audience créée lorsqu’un modèle analogue avec un seuil de similarité sélectionné est appliqué à l’audience de base. Vous pouvez créer plusieurs audiences look-alike à l’aide du même modèle look-alike. L&#39;audience analogue est ce qui obtient un score.
- **Taille totale de l’audience adressable**: la taille totale de l’audience adressable est le nombre total de profils au cours des 30 derniers jours, moins la population de base de l’audience au cours des 30 derniers jours. Par exemple, si un client a 10 millions de profils au cours des 30 derniers jours et que l’audience de base a 1 million de profils au cours des 30 derniers jours, la taille totale de l’audience adressable est de 9 millions de profils.

## Admissibilité {#eligibility}

Pour utiliser des insights semblables, l’audience de base **must** répondent aux critères d&#39;éligibilité suivants :

- L’audience de base **must** être créé dans Platform.
   - Les audiences générées de l’extérieur sont **not** éligible aux insights semblables.
- L’audience de base **must** se trouve sur la stratégie de fusion par défaut.
- L’audience de base **must** n’utilisez pas de champs qui sont limités par la gouvernance des données.

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

Dans Adobe Experience Platform, le modèle analogue utilise trois types de points de données différents :

- Appartenance à l’audience au cours des 30 derniers jours
- Événements d’expérience des 30 derniers jours ingérés dans le profil client en temps réel
- Attributs de profil des 30 derniers jours ingérés dans le profil client en temps réel

Tous ces points de données sont transformés en paires valeur-clé qui sont transmises au modèle analogue. Seules les paires clé-valeur avec un pourcentage significatif de correspondance de profils seront conservées.

Actuellement, le modèle look-alike est exécuté toutes les 24 heures, créant et recréant les facteurs d’influence et les graphiques de similitudes pour les audiences de base. La notation pour les audiences look-alike est également exécutée fréquemment.

## Droits {#entitlements}

Les droits suivants s’appliquent pour l’utilisation d’audiences look-alike :

- Les clients Real-Time CDP Prime ont le droit de **5** Audiences look-alike de production actives
- Les clients Real-Time CDP Ultimate ont le droit de **20** Audiences look-alike de production actives
- Les environnements de test de développement sont limités à **5** Audiences semblables pour tous les clients Real-Time CDP

Les modules complémentaires, qui seront disponibles ultérieurement, augmenteront les droits pour les environnements de test de production de 20 audiences semblables par pack.

Pour confirmer que vous avez accès aux audiences look-alike, contactez votre représentant d’Adobe.

## Affichage des insights semblables {#view}

Les insights semblables sont intégrés à la page des détails de l’audience. Pour consulter les insights semblables d’une audience, sélectionnez **[!UICONTROL Audiences]** dans la barre de navigation de gauche, suivie de **[!UICONTROL Parcourir]** et l’audience pour laquelle vous souhaitez afficher les insights.

![Le bouton Audiences est mis en surbrillance, ainsi que l’audience de base utilisée pour la modélisation analogue.](../images/ui/lookalike-audiences/browse.png)

La page Détails de l’audience s’affiche. Sélectionner **[!UICONTROL Aperçu identique]** pour afficher les insights semblables de l’audience. La variable **[!UICONTROL Aperçu identique]** s’affiche. Cette page comporte trois éléments principaux : le graphique de similarité et de portée, les audiences semblables et les facteurs d’influence.

![L’onglet Aperçu identique est mis en surbrillance, affichant les insights semblables pour l’audience de base.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Similarité et portée {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Similarité et portée"
>abstract="Le graphique de similarité et de portée trace la portée attendue d’une audience analogue composée de profils au-dessus d’un score de similarité donné. Vous pouvez pointer sur un point spécifique du graphique pour afficher le pourcentage de similarité et le nombre de profils attendu pour le point actuellement surligné."

La section similarité et portée affiche un graphique qui trace la portée attendue d’une audience analogue composée de profils au-dessus d’un score de similarité donné. Le score de similarité représente la variable **distance** de similarité entre le profil de l’audience de base et le profil de l’insight analogue.

![Le graphique de similarité et de portée est mis en surbrillance.](../images/ui/lookalike-audiences/similarity-and-reach.png)

Sur ce graphique, l’axe X mesure le pourcentage de similitude entre un profil et les membres de l’audience sélectionnée. Le score de similarité est compris entre 0 % et 100 %, avec un score de similarité plus élevé indiquant qu’un profil est plus proche, en termes de valeurs de facteur d’influence, des membres de l’audience sélectionnée.

L’axe des ordonnées affiche le nombre attendu de profils avec le pourcentage de similarité correspondant à la valeur correspondante de l’axe des abscisses. Ce nombre attendu de profils est compris entre 0 et la taille totale de l’audience adressable ou 25 millions de profils, selon la valeur la plus basse. Cet axe est mesuré sur une **échelle logarithmique** pour améliorer la lisibilité du graphique.

Veuillez noter que le graphique est **cumulatif** de droite à gauche. Cela signifie qu’à tout point du graphique, la valeur de l’axe des ordonnées est le nombre de profils présentant une similarité. **above** le seuil de similarité. Par exemple, si l’axe des abscisses est de 60 % et que l’axe des abscisses est de 10 millions, cela signifie qu’il y a 10 millions de profils qui ont une similarité à 60 % ou supérieure à l’audience de base.

Vous pouvez pointer sur un point spécifique du graphique pour afficher le pourcentage de similarité et le nombre de profils attendu pour le point actuellement surligné.

### Audiences semblables {#list}

La section Audiences look-alike présente une liste de toutes les audiences look-alike qui ont été créées précédemment pour l’audience de base sélectionnée.

![La section Audiences look-alike est mise en surbrillance.](../images/ui/lookalike-audiences/select-laa.png)

### Facteurs d’influence {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Facteurs d’influence"
>abstract="Les facteurs d’influence sont les attributs, les événements et les appartenances à l’audience qui sont importants pour expliquer la similarité d’un profil aux profils membres de l’audience de base.Les libellés et politiques d’utilisation des données peuvent être utilisés pour exclure certaines données en tant que facteurs d’influence dans les modèles analogues."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=fr#exclude" text="Exclure des données"

La section facteurs d’influence présente les 100 principaux facteurs qui influencent le modèle analogue pour l’audience de base sélectionnée. Ces facteurs d’influence sont les attributs de profil, les événements d’expérience et les appartenances à l’audience qui sont les plus importants pour expliquer les similitudes dans l’audience de base. Comprendre les principaux facteurs d’influence vous permet de mieux personnaliser votre contenu marketing pour cette audience et pour toute audience analogue que vous créez à partir de celle-ci. Notez que tous les facteurs d’influence qui affectent le modèle analogue ne s’affichent pas.

Pour les facteurs d’influence qui sont numériques, les paires clé-valeur peuvent être regroupées, en fonction du nombre de valeurs différentes dont dispose la clé. Par exemple, si vous disposez d’une clé de `income`, il y aurait probablement de nombreuses valeurs uniques. Par conséquent, les paires clé-valeur seront placées dans des compartiments qui peuvent ressembler à `income=[0 -> 30000]`, `income=[30000 -> 50000]`, et `income=[50000 -> 100000]`.

Ces compartiments sont régulièrement recalculés pour s’assurer que les données sont à jour.

![La section Facteurs d’influence est mise en évidence.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>Les facteurs d’influence sont triés par ordre d’importance et sont indépendants les uns des autres.

| Champ | Description |
| ----- | ----------- |
| Type | Le type de données à partir duquel le facteur d’influence est dérivé. Il peut s’agir d’un attribut de profil, d’un événement d’expérience ou d’une appartenance à une audience. |
| Clé | Nom du champ de données. Pour les clés du type d’appartenance à l’audience, cette valeur représente la variable **namespace** de l’audience d’où proviennent les données. Les valeurs possibles incluent : `ups` (Segmentation Service) et `AO` (Audience Orchestration). Pour les clés d’autres types, cette valeur représente le chemin d’accès au champ XDM. Par exemple, si l’entreprise Luma possède un champ personnalisé appelé revenu, la clé serait `_luma.income` |
| Valeur | La valeur varie en fonction du facteur d’influence qu’elle représente. Pour les attributs de profil ou les événements d’expérience, ce champ représente la plage de valeurs du champ de données qui indique la similarité avec les membres de l’audience de base. La plage de valeurs est écrite dans le formulaire. `[A -> B]`, où `A` représente la plage inférieure tout en `B` représente la plage la plus élevée. Pour les appartenances à une audience, ce champ est le nom de l’audience. |
| Importance | Le niveau relatif d&#39;importance du facteur influent. Il peut s’agir d’une valeur élevée, moyenne ou faible. |

## Création d’une audience analogue {#create}

>[!IMPORTANT]
>
>You **cannot** utiliser une audience analogue comme audience de base pour une autre audience analogue ; C&#39;est-à-dire, vous **cannot** créer des audiences look-alike.

Pour créer une audience analogue, vous devez sélectionner l’audience dont vous souhaitez baser l’audience correspondante. Pour accéder à la liste des audiences disponibles, sélectionnez **[!UICONTROL Audiences]** dans la barre de navigation de gauche, suivie de **[!UICONTROL Parcourir]**. La liste des audiences s’affiche. Sur cette page, vous pouvez sélectionner l’audience que vous souhaitez utiliser comme audience de base.

![Le bouton Audiences est mis en surbrillance, ainsi que l’audience de base utilisée pour la modélisation analogue.](../images/ui/lookalike-audiences/browse.png)

Sur la page des détails de l’audience, sélectionnez **[!UICONTROL Création d’une audience analogue]** pour lancer le processus de création d’une audience analogue.

![La variable [!UICONTROL Création d’une audience analogue] est mise en surbrillance.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

La variable **[!UICONTROL Création d’une audience analogue]** s’affiche. Sur cette page, vous pouvez définir le pourcentage de similarité pour l’audience look-alike.

![La variable [!UICONTROL Création d’une audience analogue] s’affiche.](../images/ui/lookalike-audiences/create-audience.png)

Vous pouvez définir ce pourcentage de similarité de trois manières différentes :

- Déplacez le curseur pour définir le pourcentage de similarité.
- Saisissez le pourcentage de similarité dans la zone de saisie numérique en regard du curseur.
- Pointez sur le graphique et sélectionnez l’emplacement souhaité pour définir le pourcentage de similarité.

Vous pouvez également mettre à jour les détails sur l’audience look-alike, y compris son nom et sa description. Par défaut, le nom de l’audience analogue est généré en fonction du nom de l’audience de base et du pourcentage de similarité spécifié précédemment.

![Les informations de base sont mises en surbrillance dans la variable [!UICONTROL Création d’une audience analogue] s’affiche.](../images/ui/lookalike-audiences/basic-info.png)

Sélectionner **[!UICONTROL Créer]** pour terminer la création de votre audience analogue.

![Le bouton de création est mis en surbrillance dans la [!UICONTROL Création d’une audience analogue] s’affiche.](../images/ui/lookalike-audiences/create-audience.png)

Vous pouvez accéder à l’audience look-alike nouvellement créée. **[!UICONTROL Audiences semblables]** de la page des détails de l’audience. Elle est également disponible dans Audience Portal et pour d’autres utilisations en aval. Veuillez noter que le score de l’audience look-alike prendra un certain temps. Tant qu’il n’a pas été noté, le nombre de profils s’affiche à 0.

## Affichage des détails d’une audience analogue {#view-details}

Pour afficher les détails d’une audience analogue, sélectionnez l’audience analogue dans la **[!UICONTROL Audiences semblables]** de l’audience de base.

![La section Audiences look-alike est mise en surbrillance.](../images/ui/lookalike-audiences/select-laa.png)

La page Détails de l’audience s’affiche. Pour plus d’informations sur cette page, veuillez lire le [section détails de l’audience de la présentation d’Audience Portal](./audience-portal.md#audience-details).

![Les détails de l’audience analogue s’affichent.](../images/ui/lookalike-audiences/laa-details.png)

## Exclusion des champs de données de la modélisation analogue {#exclude}

>[!IMPORTANT]
>
> **You** sont chargés de s’assurer que les données, y compris les données sensibles, sont correctement étiquetées et que les stratégies d’utilisation des données ont été définies et activées pour se conformer aux obligations légales et réglementaires en vertu desquelles vous opérez. Vous devez également savoir que les champs de données ou les appartenances aux segments qui sont **not** la corrélation directe avec les champs de données généralement associés à des types de données sensibles ou protégés peut être une source de biais potentiel. **You** sont chargés d’analyser vos données afin d’identifier, d’étiqueter et d’appliquer les stratégies d’utilisation des données appropriées à vos données, y compris les champs de données susceptibles de représenter des types de données sensibles ou protégés et qui doivent être exclus de la modélisation.

Les audiences semblables peuvent être configurées pour exclure les champs de données qui sont restreints à l’action marketing &quot;Science des données&quot; en appliquant les libellés et stratégies d’utilisation des données appropriés. Les données étiquetées comme étant interdites d’utilisation pour la science des données seront supprimées lors de la formation d’un modèle d’audience analogue et de la génération d’une audience analogue à partir du modèle formé. 

>[!NOTE]
>
>Les modifications apportées aux libellés d’utilisation des données sur l’audience de base peuvent prendre jusqu’à 48 heures pour prendre effet.

L’étiquette &quot;C9&quot; standard peut être utilisée pour étiqueter les données qui ne doivent pas être utilisées pour la science des données et qui peuvent être appliquées en activant la politique standard &quot;Limiter la science des données&quot;. Vous pouvez également créer des stratégies supplémentaires pour limiter les données aux autres étiquettes, y compris les étiquettes sensibles, à partir de l’utilisation de la science des données. Pour plus d’informations sur la gestion des stratégies d’utilisation des données, consultez la section [Guide d’utilisation des stratégies de données](../../data-governance/policies/user-guide.md). Pour plus d’informations sur la gestion des libellés d’utilisation des données, consultez la section [Guide d’utilisation des libellés d’utilisation des données](../../data-governance/labels/user-guide.md).

Par défaut, si une audience de base ne comporte pas d’étiquettes de contrat, le processus de modélisation pour les audiences look-alike **any** champ, jeu de données ou audience en fonction de la politique de confidentialité activée pour votre entreprise.

## Étapes suivantes

Après avoir lu ce guide, vous avez appris à afficher des insights semblables et à créer des audiences semblables en fonction de ces insights. Pour plus d’informations sur les audiences dans l’interface utilisateur de Adobe Experience Platform, veuillez lire le [Guide de l’interface utilisateur de Segmentation Service](./overview.md).
