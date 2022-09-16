---
keywords: Experience Platform;profil;profil client en temps réel;profil unifié;profil unifié;unifié;profil;unifié;profil;rtcp;activer le profil;activer le profil;schéma d’union;PROFIL D’UNION;profil d’union
title: Guide de l’interface utilisateur des schémas d’union
topic-legacy: guide
type: Documentation
description: Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez facilement afficher n’importe quel schéma d’union au sein de votre organisation et prévisualiser les champs, les identités, les relations et les schémas de contribution d’une classe spécifique. Ce guide fournit des informations détaillées sur la manière d’afficher et d’explorer les schémas d’union à l’aide de l’interface utilisateur de Platform.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 6%

---

# [!UICONTROL Guide de l’interface utilisateur du schéma d’union]

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez facilement afficher n’importe quel schéma d’union au sein de votre organisation et prévisualiser les champs, les identités, les relations et les schémas de contribution d’une classe spécifique. Ce guide fournit des informations détaillées sur la manière d’afficher et d’explorer les schémas d’union à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce guide de l’interface utilisateur nécessite une compréhension des différentes [!DNL Experience Platform] services impliqués dans la gestion des données de Real-time Customer Profile. Avant de lire ce guide ou de travailler dans l’interface utilisateur, consultez la documentation relative aux services suivants :

* [[!DNL Real-time Customer Profile]](../home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Identity Service]](../../identity-service/home.md): Active [!DNL Real-time Customer Profile] en rapprochant des identités de sources de données disparates lors de leur ingestion dans [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

## Présentation des schémas d’union

Real-time Customer Profile vous permet de créer des profils robustes et centralisés contenant des attributs du client et des événements horodatés pour chaque interaction client sur les systèmes intégrés à Adobe Experience Platform. Le format et la structure de ces données sont fournis par les schémas du modèle de données d’expérience (XDM), chaque schéma étant basé sur une classe XDM et contenant des champs compatibles avec cette classe.

Les schémas peuvent être créés pour plusieurs cas d’utilisation, référençant la même classe mais contenant des champs spécifiques à leur utilisation. Lorsqu’un schéma est activé pour Profile, il fait partie d’un schéma d’union. En d’autres termes, les schémas d’union sont composés de plusieurs schémas qui partagent la même classe et qui ont été activés pour Profile. Le schéma d’union permet de visualiser une fusion de tous les champs contenus dans les schémas partageant la même classe. Real-time Customer Profile utilise le schéma d’union pour créer une vue d’ensemble de chaque client.

L’utilisation des schémas d’union nécessite une compréhension approfondie des schémas XDM. Pour plus d’informations, veuillez commencer par lire la [principes de base de la composition des schémas](../../xdm/schema/composition.md).

## Affichage des schémas d’union

Pour accéder aux schémas d’union dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Schéma d’union]** . Le [!UICONTROL Schéma d’union] s’ouvre pour afficher le schéma d’union pour la classe actuellement sélectionnée.

![](../images/union-schema/union-schema-landing.png)

## Sélectionner une classe

Pour afficher le schéma d’union pour une classe XDM spécifique, sélectionnez la classe dans la **[!UICONTROL Classe]** menu déroulant. En raison du fait que toutes les classes n’ont pas de schémas d’union, seules les classes avec des schémas d’union (c’est-à-dire des classes avec des schémas qui ont été activés pour Profile) sont disponibles dans la liste déroulante.

Une fois qu’une classe a été sélectionnée, le schéma affiché est mis à jour pour refléter le schéma d’union de la classe sélectionnée. Par exemple, vous pouvez sélectionner **[!UICONTROL XDM Individual Profile]** pour afficher le schéma d’union de cette classe.

![](../images/union-schema/union-schema-class.png)

## Exploration des schémas d’union

Vous pouvez explorer le schéma d’union en faisant défiler vers le haut ou vers le bas pour afficher la structure complète du schéma et en sélectionnant un crochet angulaire à droite (`>`) pour développer les champs imbriqués.

![](../images/union-schema/union-schema-explore.png)

Sélectionnez un champ pour en afficher les détails, notamment le nom d’affichage, le type de données, la description, le chemin, la date de création et la date de dernière modification. Vous pouvez également afficher une liste des schémas de contribution contenant le champ que vous avez sélectionné.

![](../images/union-schema/union-schema-explore-field.png)

La sélection du nom d’un schéma de contribution révèle les noms des jeux de données associés à ce schéma qui ingèrent des données dans le champ sélectionné. Chaque nom de jeu de données s’affiche sous la forme d’un lien. La sélection d’un nom de jeu de données ouvre l’onglet d’activité de ce jeu de données dans une nouvelle fenêtre.

Pour plus d’informations sur les jeux de données, y compris l’affichage de l’activité des jeux de données et l’aperçu des données des jeux de données dans l’interface utilisateur, consultez le [guide de l’interface utilisateur des jeux de données](../../catalog/datasets/user-guide.md).

![](../images/union-schema/union-schema-field-datasets.png)

## Affichage des schémas de contribution

Vous pouvez également afficher les schémas spécifiques qui contribuent au schéma d’union en sélectionnant **[!UICONTROL Tous les schémas de contribution]** pour développer la liste des schémas. Selon la classe que vous avez sélectionnée et le nombre de schémas que votre organisation a créés dans Platform, il peut s’agir d’une liste courte contenant un seul schéma ou une liste longue contenant de nombreux schémas.

![](../images/union-schema/union-schema-contributing-schemas.png)

La sélection du nom d’un schéma spécifique met en évidence les champs du schéma d’union qui font partie du schéma que vous avez sélectionné. Une fois qu’un schéma est sélectionné, le schéma d’union apparaît grisé avec des barres noires indiquant les champs qui font partie du schéma de contribution.

![](../images/union-schema/union-schema-select-schema.png)

## Affichage des identités

L’interface utilisateur vous permet d’afficher la liste des identités incluses dans le schéma d’union en sélectionnant **[!UICONTROL Identités]** pour développer la liste.

![](../images/union-schema/union-schema-identities.png)

La sélection d’une identité individuelle dans la liste entraîne la mise à jour automatique du schéma affiché afin d’afficher le champ d’identité. Cela peut inclure le développement de plusieurs champs si le champ d’identité est imbriqué.

Le champ d’identité est mis en surbrillance dans le schéma d’union et les détails de l’identité s’affichent dans la partie droite de l’écran. Les détails incluent une liste des schémas de contribution contenant le champ d’identité. Vous pouvez descendre dans la hiérarchie pour trouver des liens vers les jeux de données associés à ce schéma qui ingèrent des données dans le champ d’identité sélectionné.

![](../images/union-schema/union-schema-select-identity.png)

## Afficher les relations

L’interface utilisateur de schéma d’union vous permet également d’afficher les relations définies pour les schémas en fonction de la classe de schéma sélectionnée. La définition d’une relation est un moyen de connecter deux schémas appartenant à différentes classes afin d’obtenir des informations plus complexes sur les données client.

Si des relations ont été établies pour la classe sélectionnée, sélectionnez **[!UICONTROL Relations]** affiche une liste des champs utilisés pour créer des relations. Tous les schémas n’utilisent pas ou ne nécessitent pas de relations définies. Il est donc courant que la section Relations ne contienne aucun champ.

Pour en savoir plus sur les relations de schéma, y compris sur la manière de les définir à l’aide de l’interface utilisateur, consultez la page [ce document sur les relations de schémas](../../xdm/tutorials/relationship-ui.md).

![](../images/union-schema/union-schema-relationships.png)

La sélection d’un champ de relation dans la liste entraîne la mise à jour du schéma affiché afin d’afficher le champ de relation mis en surbrillance. Cela peut inclure le développement de plusieurs champs si le champ de relation est imbriqué.

![](../images/union-schema/union-schema-select-relationship.png)

## Étapes suivantes

En lisant ce guide, vous savez maintenant comment afficher et parcourir les schémas d’union à l’aide de la variable [!DNL Experience Platform] Interface utilisateur. Pour plus d’informations sur les schémas, y compris sur leur utilisation dans Platform, veuillez commencer par lire le [Présentation du système XDM](../../xdm/home.md).
