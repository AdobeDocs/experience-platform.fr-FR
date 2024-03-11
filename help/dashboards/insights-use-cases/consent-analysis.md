---
title: Analyse et suivi du consentement
description: Découvrez comment créer un tableau de bord d’analyse du consentement pour suivre les tendances du consentement des utilisateurs au fil du temps.
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: 454f485a327233ca1a5b37ea58f16b7b53255ba6
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Analyse et suivi du consentement

Dans le contexte marketing actuel, vous devez comprendre et respecter les préférences de consentement des clients. Adobe Real-time Customer Data Platform permet aux marketeurs d’analyser le consentement des clients afin de créer des rapports de confiance, de se conformer aux réglementations de confidentialité et de proposer des expériences plus personnalisées.

Ce document explique comment créer un tableau de bord de consentement pour divers cas d’utilisation marketing pour les données Real-Time CDP. Plus précisément, il se concentre sur la création d’une audience avec les attributs appropriés pour vos besoins professionnels, puis sur l’utilisation de widgets préconfigurés dans l’interface utilisateur de Adobe Experience Platform. Une autre méthode de création de votre propre widget personnalisé avec la fonction de tableaux de bord définis par l’utilisateur est également présentée.

## Cas d’utilisation {#use-cases}

Les cas d’utilisation couverts dans ce guide sont les tendances de consentement et le chevauchement des consentements.

- **Tendance du consentement** effectue le suivi des tendances au fil du temps du consentement de l’utilisateur. L’analyse des modifications des préférences de consentement aide les marketeurs à planifier et à exécuter des campagnes qui s’adaptent à ces modifications. Par exemple, vous pouvez exécuter des campagnes éducatives ciblées, des campagnes de transparence et de confiance ou des campagnes d’incitation pour orienter les choix de consentement. Vous pouvez également mettre en corrélation les campagnes qui ont pu avoir un impact négatif sur le consentement pour réduire de manière proactive la fréquence de ces campagnes.
- **Superposition du consentement** utilise le chevauchement entre les canaux de consentement pour diffuser des messages personnalisés cohérents sur plusieurs canaux pour vos clients qui ont consenti à plusieurs canaux. Les marketeurs peuvent hiérarchiser et allouer des ressources à certains canaux pour lesquels un plus haut degré de consentement et des messages personnalisés peuvent interagir avec les clients et générer des taux de réponse plus élevés.

## Créer des audiences consentantes {#create-consent-audiences}

Pour créer un tableau de bord de consentement, vous devez d’abord créer une audience de tous les profils qui ont accepté de contacter. Pour accéder au créateur de segments de Real-time Customer Data Platform, sélectionnez **[!UICONTROL Audiences]** dans le volet de navigation de gauche de l’interface utilisateur de Platform. Dans le [!UICONTROL Client] de la [!UICONTROL Audiences] tableau de bord, sélectionnez **[!UICONTROL Créer une audience]** en haut à droite de la vue, puis **[!UICONTROL Créer des règles]**.

![La variable [!UICONTROL Audiences] tableau de bord avec [!UICONTROL Client], [!UICONTROL Audiences], et [!UICONTROL Créer un segment] surlignée.](../images/insights-use-cases/consent-analysis/create-audience.png)

Le créateur de segments s’affiche. Ensuite, sélectionnez **[!UICONTROL XDM Individual Profile]** dans les options disponibles. Pour plus d’informations sur la variable [canevas du créateur de règles](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![Le créateur de segments avec le [!UICONTROL XDM Individual Profile] dossier d’attributs mis en surbrillance.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Recherchez les attributs de consentement parmi les options disponibles. Sélectionner **[!UICONTROL Consentements et préférences]**.

>[!NOTE]
>
>Si vous avez conservé votre consentement de l’utilisateur dans un attribut différent du groupe de champs recommandé par l’Adobe, vous devez sélectionner ces attributs au lieu de ceux affichés ci-dessous.

Vous trouverez plus d’informations sur la [gestion du consentement dans la segmentation](../../segmentation/consents.md#handling-consent-in-segmentation) la documentation.

![Le créateur de segments avec le [!UICONTROL Consentement et préférences] dossier d’attributs mis en surbrillance.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

Les différentes options de consentement et de préférence s’affichent. Comme cette démonstration se concentre sur le consentement à contacter sur divers canaux marketing, sélectionnez **[!UICONTROL Préférences marketing]**.

![Le créateur de segments avec le [!UICONTROL Préférences marketing] en surbrillance.](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

La liste des préférences marketing s&#39;affiche. Bien que cet exemple de cas d’utilisation se concentre sur les emails, les SMS et les appels, vous pouvez créer des insights pour toute autre combinaison ou l’ensemble des options également. Pour chacun des canaux, suivez les étapes ci-dessous pour créer une audience.

Pour commencer à configurer une audience, sélectionnez **[!UICONTROL Recevoir un SMS]** / **[!UICONTROL Recevoir un courrier électronique]** / **[!UICONTROL Réception d’appels]**.

![Les canaux de contact disponibles pour le marketing sont mis en surbrillance dans le créateur d’audiences.](../images/insights-use-cases/consent-analysis/channels.png)

La variable [!UICONTROL Abonnements] s’affiche. Dans les options disponibles, sélectionnez et faites glisser le **[!UICONTROL Valeur de choix]** dans le volet central, puis sélectionnez la valeur souhaitée dans la liste déroulante. Dans ce cas, sélectionnez **Oui (inclusion)**. Attribuez ensuite un nom à l’audience en fonction des besoins de votre entreprise et fournissez une description conviviale.

>[!NOTE]
>
>Le nombre d’audiences que vous êtes invité à créer est limité. Vous trouverez plus d’informations dans la section [documentation sur les barrières de segmentation](../../profile/guardrails.md#segmentation-guardrails).

![La variable [!UICONTROL Valeur de choix] avec l’attribut [!UICONTROL Oui (inclusion)] en surbrillance dans le créateur de segments. Le nom et la description de l’audience sont également mis en surbrillance.](../images/insights-use-cases/consent-analysis/choice-value.png)

Une fois les audiences nécessaires créées, elles sont répertoriées dans la [!UICONTROL Audiences] [!UICONTROL Parcourir] .

>[!NOTE]
>
>Lors de la création d’une audience, vous devez attendre la fin de la tâche de segmentation par lots avant que les données ne soient disponibles pour commencer à créer votre tableau de bord de consentement. La segmentation par lots décrit le processus de déplacement simultané de toutes vos données de profil à travers vos définitions de segment pour produire les audiences correspondantes. Une fois créée, cette audience est enregistrée et stockée afin que vous puissiez l&#39;exporter et l&#39;utiliser. Les segments par lot sont automatiquement évalués toutes les 24 heures.

## Consommer des insights {#consume-insights}

Adobe a créé différentes informations qui sont automatiquement disponibles pour vous dans les tableaux de bord Profils, Audiences et Destinations . Toutes les audiences que vous créez sont alors automatiquement utilisables avec ces informations préconfigurées. Consultez la documentation standard du widget pour obtenir la liste des insights disponibles dans la section [Profils](../guides/profiles.md#standard-widgets), [Audiences](../guides/audiences.md#standard-widgets), et [Destinations](../guides/destinations.md) tableaux de bord.

## Supervision de l’audience {#audience-overlap}

Pour examiner le chevauchement entre deux audiences de consentement, ajoutez le [!UICONTROL Superposition des audiences par stratégie de fusion] dans le tableau de bord Profils et sélectionnez les audiences de votre choix dans les menus déroulants. Consultez la documentation pour obtenir des instructions sur l’ajout d’un widget à votre tableau de bord. [*Superposition des audiences par stratégie de fusion*](../guides/profiles.md#audience-overlap-by-merge-policy) pour plus d’informations sur les informations.

<!-- Image needs updating to night mode -->

![Le tableau de bord Profils avec le chevauchement Audience par le widget de stratégie de fusion mis en surbrillance. Le widget visualise les chevauchements entre deux audiences de consentement.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

Vous pouvez afficher le chevauchement de toutes les audiences où les utilisateurs ont consenti à recevoir des appels à l’échelle de toutes les autres audiences, avec le rapport sur le chevauchement des audiences dans le tableau de bord Audiences . Pour afficher le chevauchement des audiences de consentement, accédez d’abord à la [!UICONTROL Audiences] [!UICONTROL Présentation] . À partir de là, vous pouvez ajouter le [!UICONTROL Rapport de chevauchement d’audiences] du tableau de bord Audiences . Une fois le widget créé, sélectionnez la variable **[!UICONTROL L’utilisateur a consenti aux appels]** audience depuis le menu déroulant aperçu de l’audience en haut de la page. Ensuite, sélectionnez **[!UICONTROL En savoir plus]** dans le widget Rapport de chevauchement d’audiences pour afficher jusqu’à 50 des principales superpositions et jusqu’à 50 des moins superpositions concernant le segment sélectionné.

<!-- Image needs updating to night mode -->

![Le tableau de bord Audiences avec le widget Rapport de chevauchement d’audiences s’affiche. L’utilisateur a consenti à ce que l’audience d’appels soit une audience de comparaison et le lien Afficher plus est mis en surbrillance.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

La boîte de dialogue Rapport de chevauchement d’audiences se développe pour afficher des données de chevauchement d’audiences supplémentaires.

<!-- Image needs updating to night mode -->

![Le rapport sur le chevauchement des audiences, avec l’option Utilisateurs autorisés à mettre en surbrillance l’audience par courrier électronique.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Tendances de la taille de l’audience {#audience-size-trends}

Lorsque vous créez une audience basée sur le consentement, celle-ci évolue automatiquement jusqu’à 12 mois à compter de la date de création de l’audience. Pour afficher une tendance entièrement fonctionnelle du consentement de votre client, ajoutez les widgets suivants au [!UICONTROL Segments] [!UICONTROL Présentation] page. Ces informations offrent un moyen puissant de suivre l’évolution de votre consentement au fil du temps. Ils sont même corrélés avec toute campagne que vous exécutez en parallèle qui peut avoir un impact positif ou négatif sur le consentement. Les descriptions proposées pour ces widgets s’appliquent à un cas d’utilisation du consentement.

- [Tendance de la taille de l’audience](../guides/audiences.md#audience-size-trend): ce widget permet de suivre la modification de votre consentement respectif au fil du temps.
- [Tendance de changement de la taille de l’audience](../guides/audiences.md#audience-size-change-trend): ce widget surveille la manière dont votre consentement client a changé quotidiennement. Par exemple, si le nombre de vos consentements client a chuté de 100 000, vous pouvez voir comment cette modification s’est produite sur une base quotidienne.
- [Tendance de la taille de l’audience par identité](../guides/audiences.md#audience-size-trend-by-identity): avec ce widget, vous pouvez suivre l’évolution de votre consentement respectif au fil du temps, mais davantage filtré par une identité spécifique telle qu’un email.

<!-- Image needs updating to night mode -->

![Le tableau de bord Audiences avec la tendance Taille de l’audience, la tendance de la taille de l’audience par identité et le widget de tendance de changement de la taille de l’audience s’affichent. L’option Utilisateurs autorisés à envoyer des emails à l’audience est mise en surbrillance.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Tableau de bord Aperçu des audiences {#audiences-overview-dashboard}

Après avoir créé une audience liée au consentement, telle que &quot;Utilisateurs consentés à des SMS&quot;, vous pouvez afficher les informations clés de consentement personnalisé concernant votre audience en ajoutant les widgets appropriés à votre tableau de bord Aperçu des audiences . Accédez au [!UICONTROL Audiences] [!UICONTROL Présentation] et ajoutez les widgets de votre choix dans la bibliothèque de widgets. Tout widget ajouté à votre vue du tableau de bord peut être redimensionné et déplacé à l’aide de la fonction [!UICONTROL Modifier le tableau de bord] fonction . Votre vue personnalisée peut contenir des informations telles que la tendance au fil du temps (jusqu’à 12 mois), les chevauchements avec d’autres audiences et la composition de l’identité de l’audience. Un exemple de vue est présenté ci-dessous.

![Le tableau de bord des audiences avec le consentement des utilisateurs pour l’audience SMS mis en surbrillance dans le menu déroulant de l’audience globale.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Tableaux de bord définis par l’utilisateur ou l’utilisatrice {#usr-defined-dashboards}

Vous pouvez également créer vos propres widgets avec des tableaux de bord définis par l’utilisateur. La création de votre propre widget vous permet de contrôler entièrement le type de widget, ainsi que de vous offrir la possibilité d’ajouter des filtres et bien plus encore, directement dans Adobe Real-Time CDP.

Par exemple, si vous souhaitez afficher la tendance de plusieurs audiences de consentement dans le même graphique afin que vous puissiez voir au fil du temps comment chacune de vos préférences de consentement a changé. Ce type de visualisation est possible avec des tableaux de bord définis par l’utilisateur en quelques étapes et une configuration unique. Sélectionnez d’abord **[!UICONTROL Tableaux de bord]** dans le volet de navigation de gauche. La variable [!UICONTROL Tableaux de bord] workspace s’affiche. Sélectionnez **[!UICONTROL Créer un tableau de bord]**. Instructions complètes sur la manière de procéder [création d’un tableau de bord et d’un widget personnalisé](../user-defined-dashboards.md) se trouve dans le guide des tableaux de bord définis par l’utilisateur.

![L’espace de travail des tableaux de bord avec les tableaux de bord et l’option Créer un tableau de bord est mise en surbrillance.](../images/user-defined-dashboards/create-dashboard.png)

Lorsque vous [sélectionner votre modèle de données ;](../user-defined-dashboards.md#select-data-model) dans le compositeur de widgets, sélectionnez `CDPInsights` suivie de **[!UICONTROL Suivant]**. La variable [!UICONTROL Sélectionner un tableau] s’affiche.

![La boîte de dialogue Sélectionner le modèle de données avec le modèle CDPInsights mis en surbrillance.](../images/user-defined-dashboards/select-data-model-dialog.png)

La vue suivante affiche la liste des tableaux disponibles dans le rail de gauche. Sélectionnez le `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![La boîte de dialogue Sélectionner le tableau avec la table &#39;adwh_fact_profile_by_segment_and_namespace_trendlines&#39; mise en surbrillance.](../images/insights-use-cases/consent-analysis/select-table.png)

Une fois que le compositeur de widget est renseigné avec les données du tableau de votre choix, procédez comme suit :

- [Rechercher [!UICONTROL Attributs]](../user-defined-dashboards.md#add-filter-attributes) pour `[!UICONTROL date]`, puis utilisez l’icône + pour ajouter le `[!UICONTROL date]` sur l’axe X depuis le menu déroulant.
  ![Le compositeur de widgets avec l’icône de module complémentaire et le menu déroulant sont mis en surbrillance.](../images/user-defined-dashboards/attributes-dropdown.png)
- Rechercher [!UICONTROL Attributs] pour `[!UICONTROL count_of_profiles]`, puis utilisez l’icône + pour ajouter le `[!UICONTROL count_of_profiles]` sur l’axe Y depuis le menu déroulant.
- Sélectionnez la variable `...` (ellipses) dans la variable [!UICONTROL Axe Y] , puis sélectionnez la variable [!UICONTROL SUM] fonction d’agrégat dans le menu déroulant.
  ![Le widget Compositeur de widget Consentement se développe avec le modèle de données, le tableau, le menu déroulant de l’axe Y et la fonction SUM mise en surbrillance. ](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Sélectionnez la variable [!UICONTROL Marques] menu déroulant, puis définissez le type de graphique sur [!UICONTROL Ligne].
- Rechercher [!UICONTROL Attributs] pour le `[!UICONTROL segment_name]`, puis utilisez l’icône + pour ajouter le `segment_name` as a [!UICONTROL Filtrer] dans le menu déroulant. La variable [!UICONTROL Filtre : Segment_name] s’affiche. Sélectionnez les audiences créées précédemment et liées au consentement. Pour cet exemple, sélectionnez **[!UICONTROL Utilisateurs consentants aux appels]**, **[!UICONTROL Utilisateurs consentants aux SMS]**, et **[!UICONTROL Utilisateurs consentants au courrier électronique]**, suivie de **[!UICONTROL Appliquer]**.
- Rechercher [!UICONTROL Attributs] pour `[!UICONTROL segment_name]`, puis sélectionnez l’icône + à ajouter. `segment_name` as a [!UICONTROL Couleur] dans le menu déroulant.
- Ouvrir [la valeur [!UICONTROL Propriétés] panel](../user-defined-dashboards.md#widget-properties) et fournir les [!UICONTROL Titre du widget] et [!UICONTROL Libellé de l&#39;axe].
  ![Le compositeur de widgets avec l’icône de propriétés et le titre du widget mis en surbrillance.](../images/user-defined-dashboards/properties-panel.png)
- Sélectionner **[!UICONTROL Enregistrer et fermer]** pour confirmer vos paramètres.

>[!TIP]
>
>Vous pouvez maintenant redimensionner ou déplacer le widget à la taille et à la position souhaitées avant d’enregistrer le tableau de bord.


L’image ci-dessous montre l’affichage de votre widget terminé et d’autres informations personnalisées potentielles. Pour plus d’informations sur les types de widgets qui peuvent être créés, reportez-vous à la section [documentation du modèle de données](../cdp-insights-data-model.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![Le widget de tendances de consentement personnalisé terminé.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Suivi des stratégies de consentement {#consent-policies}

Les tableaux de bord de consentement que vous créez capturent la variable **distribution des attributs de consentement et de préférence uniquement**.

>[!NOTE]
>
>Pour les clients de **Adobe Health Care Shield** ou **Adobe de la confidentialité et de la sécurité**, ces tableaux de bord **ne pas** reflète tout suivi des stratégies de consentement. Le suivi disponible inclut le nombre de stratégies créées, activées et l’impact sur l’appartenance à l’audience.

## Étapes suivantes

En lisant ce document, vous avez appris à créer des tableaux de bord pour obtenir une vue d’ensemble complète de vos préférences de consentement des clients à l’aide d’informations Real-Time CDP. Ce document explique comment Real-Time CDP offre une solution robuste au paysage actuel axé sur la confidentialité dans lequel la collecte, la segmentation, l’analyse et les campagnes marketing personnalisées basées sur les données de consentement sont essentielles pour les marketeurs.
