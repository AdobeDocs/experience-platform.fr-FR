---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord du profil;tableau de bord
title: Tableau de bord des profils
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les données Real-time Customer Profile de votre entreprise.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 7590c24baae669ebe3214985088a7135a69ff8bc
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 5%

---

# [!UICONTROL Profils] tableau de bord

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur votre [!DNL Real-time Customer Profile] données, telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder à et utiliser le [!UICONTROL Profils] tableau de bord dans l’interface utilisateur et fournit des informations sur les mesures affichées dans le tableau de bord.

Pour une présentation de toutes les fonctionnalités de profil de l’interface utilisateur de l’Experience Platform, consultez la page [Guide de l’interface utilisateur de Real-time Customer Profile](../../profile/ui/user-guide.md).

## Données du tableau de bord du profil

Le [!UICONTROL Profils] Le tableau de bord affiche un instantané des données d’attribut (enregistrement) dont votre organisation dispose dans la banque de profils dans Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données d’attribut de l’instantané affichent les données exactement telles qu’elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord Profil n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration de la [!UICONTROL Profils] tableau de bord

Pour accéder au [!UICONTROL Profils] Tableau de bord dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** dans le rail de gauche, puis sélectionnez l’option **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre entreprise est une nouvelle entreprise de Platform et qu’elle ne dispose pas encore de jeux de données Profile principaux ni de stratégies de fusion créés, la variable [!UICONTROL Profils] tableau de bord n’est pas visible. Au lieu de cela, la variable [!UICONTROL Présentation] Cet onglet affiche des liens et de la documentation pour vous aider à prendre en main Real-time Customer Profile.

![](../images/profiles/dashboard-overview.png)

### Modification de la variable [!UICONTROL Profils] tableau de bord

Vous pouvez modifier l’aspect de la variable [!UICONTROL Profils] tableau de bord en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord, ainsi que d’accéder au **[!UICONTROL Bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Reportez-vous à la section [modification des tableaux de bord](../customize/modify.md) et [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

## (Version bêta) Informations sur l’efficacité des profils {#profile-efficiency-insights}

>[!IMPORTANT]
>
>La fonctionnalité d’aperçu de l’efficacité des profils est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Le [!UICONTROL Efficacité] cet onglet fournit des mesures sur la qualité et l’exhaustivité des données de votre profil. Il détaille l’utilisation des widgets d’efficacité de profil. Ces widgets illustrent en un coup d’oeil la composition de vos profils, les tendances d’exhaustivité au fil du temps et les évaluations de la qualité des données de votre profil.

[Le tableau de bord de l’efficacité des profils.](../images/profiles/attributes-quality-assessment.png)

Voir [section widgets d’efficacité du profil](#profile-efficacy-widgets) pour plus d’informations sur les widgets actuellement disponibles.

La mise en page de ce tableau de bord peut également être personnalisée en sélectionnant [**[!UICONTROL Modifier le tableau de bord]**](../customize/modify.md) de la [!UICONTROL Présentation] .

## Parcourir les profils {#browse-profiles}

Le [!UICONTROL Parcourir] Cet onglet vous permet de rechercher et d’afficher les profils en lecture seule ingérés dans votre organisation IMS. Vous y trouverez des informations importantes appartenant au profil concernant leurs préférences, les événements passés, les interactions et les segments.

Pour en savoir plus sur les fonctionnalités d’affichage des profils fournies dans l’interface utilisateur de Platform, consultez la documentation sur [navigation dans les profils dans Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Stratégies de fusion {#merge-policies}

Les mesures affichées dans la [!UICONTROL Profils] Les tableaux de bord sont basés sur les stratégies de fusion appliquées à vos données Real-time Customer Profile. Lorsque les données sont rassemblées à partir de plusieurs sources pour créer le profil client, il est possible que les données contiennent des valeurs en conflit (par exemple, un jeu de données peut répertorier un client comme &quot;unique&quot;, tandis qu’un autre jeu de données peut le répertorier comme &quot;marié&quot;). La tâche de la stratégie de fusion consiste à déterminer les données à prioriser et à afficher dans le cadre du profil.

Pour plus d’informations sur les stratégies de fusion, notamment sur la création, la modification et la déclaration d’une stratégie de fusion par défaut pour votre organisation, commencez par lire la section [présentation des stratégies de fusion](../../profile/merge-policies/overview.md).

Le tableau de bord sélectionne automatiquement une stratégie de fusion à afficher, mais vous pouvez modifier la stratégie de fusion sélectionnée à l’aide du menu déroulant. Pour choisir une autre stratégie de fusion, sélectionnez la liste déroulante en regard du nom de la stratégie de fusion, puis sélectionnez la stratégie de fusion que vous souhaitez afficher.

>[!NOTE]
>
>Le menu déroulant affiche uniquement les stratégies de fusion liées à la classe XDM Individual Profile. Toutefois, si votre organisation a créé plusieurs stratégies de fusion, vous devrez peut-être faire défiler la liste complète des stratégies de fusion disponibles.

![](../images/profiles/select-merge-policy.png)

## Schémas d’union

Le [!UICONTROL Schéma d’union] Le tableau de bord affiche le schéma d’union pour une classe XDM spécifique. En sélectionnant la variable [!UICONTROL **Classe**] dans la liste déroulante, vous pouvez afficher les schémas d’union pour différentes classes XDM.

Les schémas d’union sont composés de plusieurs schémas qui partagent la même classe et qui ont été activés pour Profile. Ils vous permettent de voir en une seule vue, une fusion de chaque champ contenu dans chaque schéma qui partage la même classe.

Pour en savoir plus sur l’interface utilisateur du schéma d’union, consultez le guide de l’interface utilisateur du schéma d’union . [affichage des schémas d’union dans l’interface utilisateur de Platform](../../profile/ui/union-schema.md#view-union-schemas).

## Widgets et mesures

Le tableau de bord est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur vos données de profil.

La date et l’heure de la &quot;dernière mise à jour&quot; d’un widget indique le moment où le dernier instantané des données a été pris. La date et l’heure de l’instantané sont indiquées en UTC ; il ne se trouve pas dans le fuseau horaire de l’utilisateur individuel ou de l’organisation IMS.

## Widgets standard

Adobe fournit plusieurs widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos données de profil. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation à l’aide de la variable [!UICONTROL Bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, commencez par lire le [Présentation de la bibliothèque de widgets](../customize/widget-library.md).

Pour en savoir plus sur chacun des widgets standard disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Nombre de profils]](#profile-count)
* [[!UICONTROL Profils ajoutés]](#profiles-added)
* [[!UICONTROL Tendance du nombre de profils]](#profiles-count-trend)
* [[!UICONTROL Profils par identité]](#profiles-by-identity)
* [[!UICONTROL Superposition des identités]](#identity-overlap)

### [!UICONTROL Nombre de profils] {#profile-count}

Le **[!UICONTROL Nombre de profils]** widget affiche le nombre total de profils fusionnés dans la banque de profils au moment de la prise de vue instantanée. Ce nombre est le résultat de l’application de la stratégie de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

Voir [section sur les stratégies de fusion plus tôt dans ce document](#merge-policies) pour en savoir plus.

>[!NOTE]
>
>Le [!UICONTROL Nombre de profils] Le widget peut afficher un nombre différent du nombre de profils affiché dans la variable [!UICONTROL Parcourir] dans le [!UICONTROL Profils] pour plusieurs raisons. La raison la plus courante est que la variable [!UICONTROL Parcourir] L’onglet référence le nombre total de profils fusionnés en fonction de la stratégie de fusion par défaut de votre organisation, tandis que la variable [!UICONTROL Nombre de profils] Le widget référence le nombre total de profils fusionnés en fonction de la stratégie de fusion que vous avez sélectionnée pour afficher dans le tableau de bord.
>
>Une autre raison courante est due aux différences entre le moment où l’instantané du tableau de bord est pris et le moment où l’exemple de tâche est exécuté pour la fonction [!UICONTROL Parcourir] . Vous pouvez voir quand la variable [!UICONTROL Nombre de profils] Le widget a été mis à jour pour la dernière fois en examinant l’horodatage du widget et pour en savoir plus sur la manière dont l’exemple de tâche est déclenché sur la page [!UICONTROL Parcourir] , voir [section sur le nombre de profils dans le guide de l’interface utilisateur de Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Profils ajoutés] {#profiles-added}

Le **[!UICONTROL Profils ajoutés]** widget affiche le nombre total de profils fusionnés qui ont été ajoutés à la banque de profils à partir du dernier instantané pris. Ce nombre est le résultat de l’application de la stratégie de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu. Vous pouvez utiliser le sélecteur de liste déroulante pour afficher les profils ajoutés au cours des 30, 90 ou 12 derniers jours.

>[!NOTE]
>
>Le [!UICONTROL Profils ajoutés] widget reflète le nombre de profils ajoutés après la configuration de la banque de profils et l’ingestion des profils. En d’autres termes, si votre entreprise a configuré la banque de profils et ingéré 4 000 000 le jour 1, le tableau de bord sera disponible dans les 24 heures, mais la variable [!UICONTROL Profils ajoutés] est défini sur 0. Cela permet d’éviter un pic associé à l’ingestion initiale des profils dans le système. Au cours des 30 prochains jours, votre entreprise assimilera 1 000 000 profils supplémentaires dans la banque de profils. Une fois l’instantané suivant pris, la variable [!UICONTROL Profils ajoutés] Le widget affiche un total de 1 000 000 profils ajoutés, tandis que la variable [!UICONTROL Nombre de profils] le widget afficherait 5 000 000 profils au total.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Tendance du nombre de profils] {#profiles-count-trend}

Le **[!UICONTROL Tendance du nombre de profils]** widget affiche le nombre total de profils fusionnés qui ont été ajoutés quotidiennement à la banque de profils au cours des 30, 90 ou 12 derniers jours. Ce nombre est mis à jour chaque jour lorsque l’instantané est pris. Par conséquent, si vous deviez ingérer des profils dans Platform, le nombre de profils ne serait pas reflété tant que l’instantané suivant n’a pas été pris. Le nombre de profils ajoutés est le résultat de l’application de la stratégie de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

Voir [section sur les stratégies de fusion plus tôt dans ce document](#merge-policies) pour en savoir plus.

Le **[!UICONTROL Tendance du nombre de profils]** widget affiche un bouton &quot;légendes&quot; en haut à droite du widget. Sélectionner **[!UICONTROL Sous-titres]** pour ouvrir la boîte de dialogue des sous-titres automatiques.

![Onglet Aperçu du profil affichant le widget de tendance du nombre de profils avec le bouton de sous-titres en surbrillance.](../images/profiles/profile-count-trend-captions.png)

Un modèle d’apprentissage automatique génère automatiquement des sous-titres pour décrire les tendances clés et les événements importants en analysant le graphique et les données.

![Boîte de dialogue de sous-titres automatiques pour le widget de tendance de comptage des profils .](../images/profiles/profiles-count-trends-automatic-captions-dialog.png)

### [!UICONTROL Profils par identité] {#profiles-by-identity}

Le **[!UICONTROL Profils par identité]** widget affiche la ventilation des identités pour tous les profils fusionnés de votre banque de profils. Le nombre total de profils par identité (c’est-à-dire en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils fusionnés, car plusieurs espaces de noms peuvent être associés à un profil. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

Voir [section sur les stratégies de fusion plus tôt dans ce document](#merge-policies) pour en savoir plus.

Pour en savoir plus sur les identités, rendez-vous sur la page [Documentation du service Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Superposition des identités] {#identity-overlap}

Le **[!UICONTROL Superposition des identités]** Ce widget affiche un diagramme de Venn, ou un diagramme de jeu, qui montre le chevauchement des profils de votre banque de profils contenant plusieurs identités.

Après avoir utilisé les menus déroulants du widget pour sélectionner les identités à comparer, les cercles s’affichent avec la taille relative de chaque identité, le nombre de profils contenant les deux espaces de noms étant représenté par la taille du chevauchement entre les cercles. Si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités seront associées à ce client individuel. Par conséquent, il est probable que votre organisation dispose de plusieurs profils contenant des fragments provenant de plusieurs identités.

Pour plus d’informations sur les fragments de profil, commencez par lire la section sur [fragments de profil par rapport aux profils fusionnés](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) dans la présentation de Real-time Customer Profile.

Pour en savoir plus sur les identités, rendez-vous sur la page [Documentation du service Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

## (Version bêta) Widgets d’efficacité des profils {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>Les widgets d’efficacité du profil sont actuellement en version bêta et ne sont pas disponibles pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Adobe fournit plusieurs widgets pour évaluer l’exhaustivité des profils ingérés disponibles pour votre analyse de données. Chacun des widgets d’efficacité de profil peut être filtré par stratégie de fusion. Pour modifier le filtre de stratégie de fusion, sélectionnez la variable[!UICONTROL Profils utilisant une stratégie de fusion] et sélectionnez la stratégie appropriée dans la liste disponible.

Pour en savoir plus sur chacun des widgets d’efficacité de profil, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Évaluation de la qualité des attributs]](#attribute-quality-assessment)
* [[!UICONTROL Complétude du profil]](#profile-completeness)
* [[!UICONTROL Tendance d’achèvement du profil]](#profile-completeness-trend)

### (Version bêta) [!UICONTROL Évaluation de la qualité des attributs] {#attribute-quality-assessment}

Ce widget affiche l’exhaustivité et la cardinalité de chaque attribut de profil depuis la date du dernier traitement. Ces informations sont présentées sous la forme d’un tableau de quatre colonnes où chaque ligne du tableau représente un attribut unique.

| Colonne | Description |
|---|---|
| Attribut | Nom de l’attribut. |
| Profils | Le nombre de profils qui possèdent cet attribut et qui sont remplis par des valeurs non nulles. |
| Complétude | Ce pourcentage est déterminé par le nombre total de profils qui possèdent cet attribut et qui sont renseignés avec des valeurs non nulles. Le nombre est calculé en divisant le nombre total de profils par le nombre total de valeurs non vides dans les profils pour cet attribut. |
| Cardinalité | Le nombre total de **unique** valeurs non nulles de cet attribut. Elle est mesurée sur tous les profils. |

![Le widget d’évaluation de la qualité des attributs](../images/profiles/attributes-quality-assessment.png)

### (Version bêta) [!UICONTROL Profils par exhaustivité] {#profile-completeness}

Ce widget crée un graphique circulaire d’exhaustivité du profil depuis la date du dernier traitement. L’exhaustivité d’un profil est mesurée par le pourcentage d’attributs remplis avec des valeurs non nulles parmi tous les attributs observés.

Ce widget affiche la proportion de profils présentant une exhaustivité élevée, moyenne ou faible. Par défaut, trois niveaux d’exhaustivité sont configurés :

* Haute exhaustivité : Les profils comportent plus de 70 % d’attributs renseignés.
* Paramètre d’exhaustivité moyenne : Les profils comportent moins de 70 % et plus de 30 % d’attributs renseignés.
* Faible exhaustivité : Les attributs des profils sont remplis à moins de 30 %.

![Les profils par widget d’exhaustivité](../images/profiles/profiles-by-completeness.png)

### (Version bêta) [!UICONTROL Tendance d’achèvement du profil] {#profile-completeness-trend}

Ce widget crée un graphique en colonnes empilé afin de représenter la tendance de l’exhaustivité des profils au fil du temps. La complexité est mesurée par le pourcentage d’attributs qui sont remplis avec des valeurs non nulles parmi tous les attributs observés. Elle classe l’exhaustivité du profil comme une exhaustivité élevée, moyenne ou faible depuis la date du dernier traitement.

L’axe X représente le temps, l’axe Y le nombre de profils et les couleurs les trois niveaux d’exhaustivité du profil.

Les trois niveaux d&#39;exhaustivité sont les suivants :

* Haute exhaustivité : Les profils comportent plus de 70 % d’attributs renseignés.
* Paramètre d’exhaustivité moyenne : Les profils comportent moins de 70 % et plus de 30 % d’attributs renseignés.
* Faible exhaustivité : Les attributs des profils sont remplis à moins de 30 %.

![Widget de tendance d’achèvement des profils](../images/profiles/profiles-completeness-trend.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord Profils et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation de [!DNL Profile] données de l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur de Real-time Customer Profile](../../profile/ui/user-guide.md).
