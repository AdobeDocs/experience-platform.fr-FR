---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord du profil;tableau de bord
title: Tableau de bord des profils
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les données Real-time Customer Profile de votre entreprise.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 3%

---

# (Version bêta) [!UICONTROL Tableau de bord Profils]

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord décrite dans ce document est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos données [!DNL Real-time Customer Profile], telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord [!UICONTROL Profils] et l’utiliser dans l’interface utilisateur. Il fournit également des informations sur les mesures affichées dans le tableau de bord.

Pour une présentation de toutes les fonctionnalités de Profile dans l’interface utilisateur de l’Experience Platform, consultez le [guide de l’interface utilisateur de Real-time Customer Profile](../../profile/ui/user-guide.md).

## Données du tableau de bord du profil

Le tableau de bord [!UICONTROL Profils] affiche un instantané des données d’attribut (enregistrement) dont votre organisation dispose dans la banque de profils dans Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données d’attribut de l’instantané affichent les données exactement telles qu’elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord Profil n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord [!UICONTROL Profils]

Pour accéder au tableau de bord [!UICONTROL Profils] dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Aperçu]** pour afficher le tableau de bord.

![](../images/profiles/dashboard-overview.png)

### Sélection de stratégies de fusion

Les mesures affichées dans le tableau de bord [!UICONTROL Profils] reposent sur les stratégies de fusion appliquées à vos données Real-time Customer Profile. Lorsque les données sont rassemblées à partir de plusieurs sources, il est possible que les données contiennent des valeurs en conflit (par exemple, un jeu de données peut répertorier un client comme &quot;unique&quot;, tandis qu’un autre jeu de données peut répertorier le client comme &quot;marié&quot;). C’est la tâche de la stratégie de fusion de déterminer les données à prioriser et à afficher dans le cadre du profil.

Le tableau de bord sélectionne automatiquement une stratégie de fusion à afficher, mais vous pouvez modifier la stratégie de fusion sélectionnée à l’aide du menu déroulant. Pour choisir une autre stratégie de fusion, sélectionnez la liste déroulante en regard du nom de la stratégie de fusion, puis sélectionnez la stratégie de fusion que vous souhaitez afficher.

>[!NOTE]
>
>Le menu déroulant affiche uniquement les stratégies de fusion liées à la classe XDM Individual Profile. Toutefois, si votre organisation a créé plusieurs stratégies de fusion, vous devrez peut-être faire défiler la liste complète des stratégies de fusion disponibles.

Pour plus d’informations sur les stratégies de fusion, notamment sur la création, la modification et la déclaration d’une stratégie de fusion par défaut pour votre organisation, commencez par lire la [présentation des stratégies de fusion](../../profile/merge-policies/overview.md).

![](../images/profiles/select-merge-policy.png)

### Widgets et mesures

Le tableau de bord est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur vos données de profil. La date et l’heure de la &quot;dernière mise à jour&quot; d’un widget indique le moment où le dernier instantané des données a été pris.

![](../images/profiles/dashboard-timestamp.png)

## Widgets disponibles

Experience Platform fournit plusieurs widgets que vous pouvez utiliser pour visualiser différentes mesures liées à vos données de profil. Pour en savoir plus, sélectionnez le nom d’un widget ci-dessous :

* [[!UICONTROL Taille de l’audience]](#audience-size)
* [[!UICONTROL Profils ajoutés]](#profiles-added)
* [[!UICONTROL Profils ajoutés au fil du temps]](#profiles-added-over-time)
* [[!UICONTROL Profils par espace de noms]](#profiles-by-namespace)
* [[!UICONTROL Superposition des espaces de noms]](#namespace-overlap)

### [!UICONTROL Taille de l’audience] {#audience-size}

Le widget **[!UICONTROL Taille de l’audience]** affiche le nombre total de profils fusionnés dans l’entrepôt de données Profile au moment de la prise de l’instantané. Ce nombre est le résultat de l’application de la stratégie de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

Pour plus d’informations sur les fragments et les profils fusionnés, commencez par lire la section *Fragments de profil par rapport aux profils fusionnés* de la [présentation de Real-time Customer Profile](../../profile/home.md).

>[!NOTE]
>
>La stratégie de fusion utilisée pour calculer cette mesure n’est pas la même que la stratégie de fusion générée par le système utilisée pour calculer les [!UICONTROL audiences adressables] dans le tableau de bord [!UICONTROL Utilisation de la licence]. Par conséquent, le nombre d’audiences dans les tableaux de bord [!UICONTROL Profils] et [!UICONTROL Utilisation de la licence] ne sera probablement pas identique.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profils ajoutés] {#profiles-added}

Le widget **[!UICONTROL Profils ajoutés]** affiche le nombre total de profils fusionnés qui ont été ajoutés à l’entrepôt de données Profile depuis la dernière prise d’instantané. Ce nombre est le résultat de l’application de la stratégie de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profils ajoutés au fil du temps] {#profiles-added-over-time}

Le widget **[!UICONTROL Profils ajoutés au fil du temps]** affiche le nombre total de profils fusionnés qui ont été ajoutés quotidiennement à la banque de données de profil au cours des 30 derniers jours. Ce nombre est mis à jour chaque jour lorsque l’instantané est pris. Par conséquent, si vous deviez ingérer des profils dans Platform, le nombre de profils ne serait pas reflété tant que l’instantané suivant n’a pas été pris.

Le nombre de profils ajoutés est le résultat de l’application de la stratégie de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profils par espace de noms] {#profiles-by-namespace}

Le widget **[!UICONTROL Profils par espace de noms]** affiche la ventilation des espaces de noms d’identité entre tous les profils fusionnés de votre banque de profils. Le nombre total de profils par [!UICONTROL espace de noms ID] (en d’autres termes, l’ajout de toutes les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils de fusion, car plusieurs espaces de noms peuvent y être associés pour un profil. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

Pour en savoir plus sur les espaces de noms d’identité, consultez la [documentation de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Superposition des espaces de noms] {#namespace-overlap}

Le widget **[!UICONTROL chevauchement des espaces de noms]** affiche un diagramme de Venn, ou un diagramme de définition, qui montre le chevauchement des profils dans votre banque de profils contenant plusieurs espaces de noms d’identité.

Après avoir utilisé les menus déroulants du widget pour sélectionner les espaces de noms d’identité à comparer, les cercles s’affichent avec la taille relative de chaque espace de noms, le nombre de profils contenant les deux espaces de noms étant représenté par la taille du chevauchement entre les cercles.

Si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel. Par conséquent, il est probable que votre organisation comporte plusieurs profils contenant des fragments provenant de plusieurs espaces de noms d’identité.

Pour en savoir plus sur les espaces de noms d’identité, consultez la [documentation de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord Profils et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des données [!DNL Profile] dans l’interface utilisateur de l’Experience Platform, consultez le [guide de l’interface utilisateur de profil client en temps réel](../../profile/ui/user-guide.md).
