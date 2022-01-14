---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord du profil;tableau de bord
title: Tableau de bord des profils
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les données Real-time Customer Profile de votre entreprise.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: cea94fef9751aca5e17db7d61d66a70962060d9b
workflow-type: tm+mt
source-wordcount: '1618'
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

## Stratégies de fusion {#merge-policies}

Les mesures affichées dans la [!UICONTROL Profils] Les tableaux de bord sont basés sur les stratégies de fusion appliquées à vos données Real-time Customer Profile. Lorsque les données sont rassemblées à partir de plusieurs sources pour créer le profil client, il est possible que les données contiennent des valeurs en conflit (par exemple, un jeu de données peut répertorier un client comme &quot;unique&quot;, tandis qu’un autre jeu de données peut le répertorier comme &quot;marié&quot;). La tâche de la stratégie de fusion consiste à déterminer les données à prioriser et à afficher dans le cadre du profil.

Pour plus d’informations sur les stratégies de fusion, notamment sur la création, la modification et la déclaration d’une stratégie de fusion par défaut pour votre organisation, commencez par lire la section [présentation des stratégies de fusion](../../profile/merge-policies/overview.md).

Le tableau de bord sélectionne automatiquement une stratégie de fusion à afficher, mais vous pouvez modifier la stratégie de fusion sélectionnée à l’aide du menu déroulant. Pour choisir une autre stratégie de fusion, sélectionnez la liste déroulante en regard du nom de la stratégie de fusion, puis sélectionnez la stratégie de fusion que vous souhaitez afficher.

>[!NOTE]
>
>Le menu déroulant affiche uniquement les stratégies de fusion liées à la classe XDM Individual Profile. Toutefois, si votre organisation a créé plusieurs stratégies de fusion, vous devrez peut-être faire défiler la liste complète des stratégies de fusion disponibles.

![](../images/profiles/select-merge-policy.png)

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

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord Profils et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation de [!DNL Profile] données de l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur de Real-time Customer Profile](../../profile/ui/user-guide.md).
