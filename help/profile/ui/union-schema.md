---
keywords: Experience Platform ; profil ; profil client en temps réel ; profil unifié ; Profil unifié ; unifié ; Profil ; rtcp ; activer le profil ; Activer le profil ; schéma d' ; Union d' ;  d' ;  d'
title: Guide de l'interface utilisateur du Schéma Union
topic-legacy: guide
type: Documentation
description: Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez facilement vue n’importe quel schéma d’union au sein de votre organisation et prévisualisation les champs, identités, relations et schémas de contribution pour une classe spécifique. Ce guide fournit des informations détaillées sur la manière de vue et d’explorer les schémas d’union à l’aide de l’interface utilisateur de la plate-forme.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 2%

---

# [!UICONTROL Union ] schemaUI guide

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez facilement vue n’importe quel schéma d’union au sein de votre organisation et prévisualisation les champs, identités, relations et schémas de contribution pour une classe spécifique. Ce guide fournit des informations détaillées sur la manière de vue et d’explorer les schémas d’union à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce guide d&#39;interface utilisateur nécessite une compréhension des différents services [!DNL Experience Platform] impliqués dans la gestion des données de Profil client en temps réel. Avant de lire ce guide ou de travailler dans l’interface utilisateur, consultez la documentation relative aux services suivants :

* [[!DNL Real-time Customer Profile]](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Identity Service]](../../identity-service/home.md): Permet  [!DNL Real-time Customer Profile] de relier les identités à partir de sources de données disparates au fur et à mesure de leur assimilation  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

## Présentation des schémas d&#39;union

Le Profil client en temps réel vous permet de créer des profils robustes et centralisés contenant des attributs du client et des événements horodatés pour chaque interaction du client entre des systèmes intégrés à Adobe Experience Platform. Le format et la structure de ces données sont fournis par les schémas du modèle de données d’expérience (XDM), chaque schéma étant basé sur une classe XDM et contenant des champs compatibles avec cette classe.

Il est possible de créer des schémas pour plusieurs cas d&#39;utilisation, référençant la même classe mais contenant des champs spécifiques à leur utilisation. Lorsqu’un schéma est activé pour le Profil, il devient partie intégrante d’un schéma d’union. En d’autres termes, les schémas d’union sont composés de plusieurs schémas partageant la même classe et ayant été activés pour le Profil. Le schéma d&#39;union vous permet de voir une fusion de tous les champs contenus dans les schémas partageant la même classe. Le Profil client en temps réel utilise le schéma d’union pour créer une vue holistique pour chaque client.

Travailler avec des schémas d&#39;union nécessite une compréhension approfondie des schémas XDM. Pour plus d&#39;informations, veuillez commencer par lire les [bases de la composition des schémas](../../xdm/schema/composition.md).

## Schémas d&#39;union vue

Pour accéder aux schémas d&#39;union dans l&#39;interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche, puis sélectionnez l&#39;onglet **[!UICONTROL Schéma d&#39;Union]**. L&#39;onglet [!UICONTROL Schéma d&#39;Union] s&#39;ouvre pour afficher le schéma d&#39;union pour la classe actuellement sélectionnée.

![](../images/union-schema/union-schema-landing.png)

## Sélectionner une classe

Pour afficher le schéma d&#39;union pour une classe XDM spécifique, sélectionnez la classe dans la liste déroulante **[!UICONTROL Classe]**. Étant donné que toutes les classes n&#39;ont pas de schémas d&#39;union, seules les classes avec schémas d&#39;union (c&#39;est-à-dire les classes avec schémas activés pour le Profil) sont disponibles dans la liste déroulante.

Une fois qu&#39;une classe a été sélectionnée, le schéma affiché se met à jour pour refléter le schéma d&#39;union de la classe sélectionnée. Par exemple, vous pouvez sélectionner **[!UICONTROL Profil individuel XDM]** pour vue le schéma d&#39;union de cette classe.

![](../images/union-schema/union-schema-class.png)

## Explorer les schémas d’union

Vous pouvez explorer le schéma d’union en faisant défiler la page vers le haut et vers le bas jusqu’à la vue de la structure complète du schéma et en sélectionnant un crochet droit (`>`) pour développer les champs imbriqués.

![](../images/union-schema/union-schema-explore.png)

Sélectionnez un champ pour en vue les détails, notamment le nom d’affichage, le type de données, la description, le chemin, la date de création et la date de dernière modification. Vous pouvez également vue une liste de schémas de contribution contenant le champ que vous avez sélectionné.

![](../images/union-schema/union-schema-explore-field.png)

La sélection du nom d&#39;un schéma de contribution révèle les noms des jeux de données liés à ce schéma qui importent des données dans le champ sélectionné. Chaque nom de jeu de données s’affiche sous la forme d’un lien. La sélection d&#39;un nom de jeu de données ouvre l&#39;onglet activité de ce jeu de données dans une nouvelle fenêtre.

Pour plus d&#39;informations sur les jeux de données, y compris l&#39;affichage de l&#39;activité des jeux de données et l&#39;aperçu des données des jeux de données dans l&#39;interface utilisateur, consultez le [guide de l&#39;interface utilisateur des jeux de données](../../catalog/datasets/user-guide.md).

![](../images/union-schema/union-schema-field-datasets.png)

## Schémas contributeurs de vue

Vous pouvez également vue quels schémas spécifiques contribuent au schéma d’union en sélectionnant **[!UICONTROL Tous les schémas contributeurs]** pour étendre la liste des schémas. Selon la classe que vous avez sélectionnée et le nombre de schémas que votre organisation a créés dans Platform, il peut s’agir d’une courte liste contenant un seul schéma ou d’une longue liste contenant de nombreux schémas.

![](../images/union-schema/union-schema-contributing-schemas.png)

La sélection du nom d’un schéma spécifique met en surbrillance les champs du schéma d’union qui font partie du schéma sélectionné. Une fois qu’un schéma est sélectionné, le schéma d’union apparaît grisé avec des barres noires indiquant les champs qui font partie du schéma contributeur.

![](../images/union-schema/union-schema-select-schema.png)

## Identités des vues

L’interface utilisateur vous permet de vue d’une liste d’identités incluses dans le schéma d’union en sélectionnant **[!UICONTROL Identités]** pour développer la liste.

![](../images/union-schema/union-schema-identities.png)

La sélection d&#39;une identité individuelle dans la liste entraîne la mise à jour automatique du schéma affiché en fonction des besoins pour afficher le champ d&#39;identité. Cela peut inclure l&#39;extension de plusieurs champs si le champ d&#39;identité est imbriqué.

Le champ d&#39;identité est mis en surbrillance dans le schéma d&#39;union et les détails de l&#39;identité sont affichés sur le côté droit de l&#39;écran. Les détails incluent une liste de schémas de contribution contenant le champ d&#39;identité et vous pouvez approfondir l&#39;analyse pour trouver des liens vers les jeux de données liés à ce schéma qui ingèrent des données dans le champ d&#39;identité sélectionné.

![](../images/union-schema/union-schema-select-identity.png)

## Relations de vue

L&#39;interface utilisateur du schéma d&#39;union vous permet également d&#39;afficher les relations définies pour les schémas en fonction de la classe de schéma sélectionnée. Définir une relation est un moyen de connecter deux schémas appartenant à des classes différentes afin d’obtenir des informations plus complexes sur les données client.

Si des relations ont été établies pour la classe sélectionnée, la sélection de **[!UICONTROL Relations]** affiche une liste de champs utilisés pour créer des relations. Tous les schémas n’utilisent pas ou ont besoin de relations définies. Il est donc courant que la section Relations ne contienne aucun champ.

Pour en savoir plus sur les relations de schéma, y compris sur la façon de les définir à l’aide de l’interface utilisateur, consultez [ce document sur les relations de schéma](../../xdm/tutorials/relationship-ui.md).

![](../images/union-schema/union-schema-relationships.png)

Si vous sélectionnez un champ de relation dans la liste, le schéma affiché est mis à jour selon les besoins pour afficher le champ de relation mis en surbrillance. Cela peut inclure l’extension de plusieurs champs si le champ de relation est imbriqué.

![](../images/union-schema/union-schema-select-relationship.png)

## Étapes suivantes

En lisant ce guide, vous savez maintenant comment vue et naviguer dans les schémas d&#39;union à l&#39;aide de l&#39;interface utilisateur [!DNL Experience Platform]. Pour plus d&#39;informations sur les schémas, y compris sur leur utilisation dans toute la plate-forme, veuillez commencer par lire l&#39;[Présentation du système XDM](../../xdm/home.md).
