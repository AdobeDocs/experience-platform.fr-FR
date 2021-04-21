---
keywords: Experience Platform ; profil ; profil client en temps réel ; interface utilisateur ; interface utilisateur ; personnalisation ; tableau de bord profil ; tableau de bord
title: Tableau de bord profils
description: Adobe Experience Platform fournit un tableau de bord par lequel vous pouvez vue des informations importantes sur les données du Profil client en temps réel de votre entreprise.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---

# (Bêta) [!UICONTROL tableau de bord Profils]

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord décrite dans ce document est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord par lequel vous pouvez vue des informations importantes sur vos données [!DNL Real-time Customer Profile], telles qu’elles sont capturées au cours d’un instantané quotidien. Ce guide décrit comment accéder au tableau de bord [!UICONTROL Profils] de l’interface utilisateur et comment l’utiliser. Il fournit également des informations sur les mesures affichées dans le tableau de bord.

Pour un aperçu de toutes les fonctionnalités de Profil de l’interface utilisateur de l’Experience Platform, consultez le [Guide de l’interface utilisateur du Profil client en temps réel](../../profile/ui/user-guide.md).

## Données du tableau de bord profil

Le tableau de bord [!UICONTROL Profils] affiche un instantané des données d&#39;attribut (enregistrement) de votre organisation dans le magasin de Profils dans l&#39;Experience Platform. L&#39;instantané n&#39;inclut aucune donnée de événement (série chronologique).

Les données d&#39;attribut de l&#39;instantané affichent les données exactement telles qu&#39;elles apparaissent au moment précis où l&#39;instantané a été pris. En d&#39;autres termes, l&#39;instantané n&#39;est pas une approximation ou un échantillon des données et le tableau de bord de Profil n&#39;est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis l&#39;instantané ne seront pas répercutées dans le tableau de bord tant que l&#39;instantané suivant n&#39;aura pas été pris.

## Exploration du tableau de bord [!UICONTROL Profils]

Pour accéder au tableau de bord [!UICONTROL Profils] dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Profils]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Aperçu]** pour afficher le tableau de bord.

![](../images/profiles/dashboard-overview.png)

### Sélection de stratégies de fusion

Les mesures affichées dans le tableau de bord [!UICONTROL Profils] reposent sur les stratégies de fusion appliquées à vos données de Profil client en temps réel. Lorsque les données sont rassemblées à partir de plusieurs sources, il est possible que les données contiennent des valeurs conflictuelles (par exemple, un jeu de données peut liste un client comme &quot;unique&quot; tandis qu’un autre jeu de données peut liste le client comme &quot;marié&quot;) et il appartient à la stratégie de fusion de déterminer les données à classer par priorité et à afficher dans le profil.

Le tableau de bord sélectionne automatiquement une stratégie de fusion à afficher, mais vous pouvez modifier la stratégie de fusion sélectionnée à l&#39;aide du menu déroulant. Pour choisir une autre stratégie de fusion, sélectionnez la liste déroulante en regard du nom de la stratégie de fusion, puis sélectionnez la stratégie de fusion à vue.

>[!NOTE]
>
>Le menu déroulant affiche uniquement les stratégies de fusion liées à la classe de Profil XDM. Toutefois, si votre entreprise a créé plusieurs stratégies de fusion, il peut s&#39;avérer nécessaire de faire défiler les stratégies pour vue la liste complète des stratégies de fusion disponibles.

Pour plus d&#39;informations sur les stratégies de fusion, y compris sur la création, la modification et la déclaration d&#39;une stratégie de fusion par défaut pour votre organisation, consultez le [guide d&#39;interface utilisateur des stratégies de fusion](../../profile/ui/merge-policies.md).

![](../images/profiles/select-merge-policy.png)

### Widgets et mesures

Le tableau de bord est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur vos données de Profil. La date et l’heure de la &quot;dernière mise à jour&quot; d’un widget indiquent le moment où le dernier instantané des données a été effectué.

![](../images/profiles/dashboard-timestamp.png)

## Widgets disponibles

Experience Platform fournit plusieurs widgets que vous pouvez utiliser pour visualiser différentes mesures liées à vos données de Profil. Sélectionnez le nom d’un widget ci-dessous pour en savoir plus :

* [[!UICONTROL Taille de l&#39;Audience]](#audience-size)
* [[!UICONTROL Profils ajoutés]](#profiles-added)
* [[!UICONTROL Profils ajoutés au fil du temps]](#profiles-added-over-time)
* [[!UICONTROL Profils par espace de nommage]](#profiles-by-namespace)
* [[!UICONTROL Chevauchement des Espaces de nommage]](#namespace-overlap)

### [!UICONTROL Taille de l&#39;Audience] {#audience-size}

Le widget **[!UICONTROL Taille d&#39;Audience]** affiche le nombre total de profils fusionnés dans le magasin de données du Profil au moment où l&#39;instantané a été pris. Ce nombre est le résultat de l&#39;application de la stratégie de fusion sélectionnée à vos données de Profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

Pour plus d’informations sur les fragments et les profils fusionnés, veuillez commencer par lire la section *fragments de Profil par rapport aux profils fusionnés* de la section [Présentation du Profil client en temps réel](../../profile/home.md).

>[!NOTE]
>
>La stratégie de fusion utilisée pour calculer cette mesure n&#39;est pas identique à la stratégie de fusion générée par le système utilisée pour calculer [!UICONTROL les audiences adressables] dans le tableau de bord [!UICONTROL Utilisation de la licence]. Par conséquent, il est peu probable que le nombre d&#39;audiences dans les tableaux de bord [!UICONTROL Profils] et [!UICONTROL Utilisation de la licence] soit identique.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profils ajoutés] {#profiles-added}

Le widget **[!UICONTROL Profils ajoutés]** affiche le nombre total de profils fusionnés qui ont été ajoutés au stockage de données de Profil depuis la dernière capture d&#39;écran. Ce nombre est le résultat de l&#39;application de la stratégie de fusion sélectionnée à vos données de Profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profils ajoutés au fil du temps] {#profiles-added-over-time}

Le widget **[!UICONTROL Profils ajoutés au fil du temps]** affiche le nombre total de profils fusionnés qui ont été ajoutés quotidiennement à la banque de données du Profil au cours des 30 derniers jours. Ce nombre est mis à jour chaque jour lorsque l&#39;instantané est pris. Par conséquent, si vous deviez importer des profils dans la plate-forme, le nombre de profils ne serait pas reflété tant que l&#39;instantané suivant n&#39;aurait pas été pris.

Le nombre de profils ajoutés est le résultat de l&#39;application de la stratégie de fusion sélectionnée à vos données de Profil afin de fusionner les fragments de profil pour former un profil unique pour chaque individu.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profils par espace de nommage] {#profiles-by-namespace}

Le widget **[!UICONTROL Profils par espace de nommage]** affiche la ventilation des espaces de nommage d&#39;identité sur tous les profils fusionnés de votre magasin de Profils. Le nombre total de profils par [!UICONTROL espace de nommage d&#39;ID] (en d&#39;autres termes, additionner les valeurs affichées pour chaque espace de nommage) peut être supérieur au nombre total de profils de fusion, car un profil peut être associé à plusieurs espaces de nommage. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage sont associés à ce client individuel.

Pour en savoir plus sur les espaces de nommage d&#39;identité, consultez la [documentation du service d&#39;identité Adobe Experience Platform](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Chevauchement des Espaces de nommage] {#namespace-overlap}

Le widget **[!UICONTROL chevauchement d&#39;Espaces de nommage]** affiche un diagramme de Venn, ou un diagramme de définition, qui montre le chevauchement des profils dans votre magasin de Profils contenant plusieurs espaces de nommage d&#39;identité.

Après avoir utilisé les menus déroulants du widget pour sélectionner les espaces de nommage d&#39;identité à comparer, les cercles s&#39;affichent avec la taille relative de chaque espace de nommage, le nombre de profils contenant les deux espaces de nommage étant représenté par la taille du chevauchement entre les cercles.

Si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage seront associés à ce client individuel. Il est donc probable que votre entreprise dispose de plusieurs profils contenant des fragments provenant de plusieurs espaces de nommage d’identité.

Pour en savoir plus sur les espaces de nommage d&#39;identité, consultez la [documentation du service d&#39;identité Adobe Experience Platform](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Étapes suivantes

En suivant ce document, vous devez maintenant pouvoir localiser le tableau de bord des Profils et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l&#39;utilisation des données [!DNL Profile] dans l&#39;interface utilisateur Experience Platform, consultez le [Guide d&#39;interface utilisateur du Profil client en temps réel](../../profile/ui/user-guide.md).
