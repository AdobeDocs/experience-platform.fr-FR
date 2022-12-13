---
title: Guide de bout en bout de la gouvernance des données
description: Suivez le processus complet pour appliquer des contraintes d’utilisation des données pour les champs et les jeux de données dans Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 2%

---

# Guide de bout en bout sur la gouvernance des données

Pour contrôler quelles actions marketing peuvent être effectuées sur certains jeux de données et champs dans Adobe Experience Platform, vous devez configurer les éléments suivants :

1. [Application de libellés](#labels) aux jeux de données et aux champs dont vous souhaitez restreindre l’utilisation.
1. [Configuration et activation des stratégies de gouvernance des données](#policy) qui déterminent quels types de données étiquetées peuvent être utilisés pour certaines actions marketing.
1. [Application d’actions marketing à vos destinations](#destinations) pour indiquer les stratégies qui s’appliquent aux données envoyées vers ces destinations.

Une fois la configuration des libellés, des stratégies de gouvernance et des actions marketing terminée, vous pouvez [test de l’application de la stratégie](#test) pour s’assurer qu’il fonctionne comme prévu.

Ce guide décrit l’ensemble du processus de configuration et d’application d’une stratégie de gouvernance des données dans l’interface utilisateur de Platform. Pour des informations plus détaillées sur les fonctionnalités utilisées dans ce guide, consultez la documentation de présentation sur les rubriques suivantes :

* [Gouvernance des données d’Adobe Experience Platform](./home.md)
* [Libellés d’utilisation des données](./labels/overview.md)
* [Stratégies d’utilisation des données](./policies/overview.md)
* [Application des stratégies](./enforcement/overview.md)

>[!NOTE]
>
>Ce guide se concentre sur la configuration et l’application des stratégies pour la manière dont les données sont utilisées ou activées dans Experience Platform. Si vous essayez de restreindre **access** Pour accéder aux données proprement dites de certains utilisateurs de Platform au sein de votre organisation, consultez le guide de bout en bout sur la [contrôle d’accès basé sur les attributs](../access-control/abac/end-to-end-guide.md) au lieu de . Le contrôle d’accès basé sur les attributs utilise également des étiquettes et des stratégies, mais pour un cas d’utilisation différent de celui de la gouvernance des données.

## Application de libellés {#labels}

Si vous souhaitez imposer des contraintes d’utilisation des données à un jeu de données spécifique, vous pouvez [appliquer des libellés directement à ce jeu de données ;](#dataset-labels) ou des champs spécifiques de ce jeu de données.

Vous pouvez également [appliquer des libellés à un schéma ;](#schema-labels) afin que tous les jeux de données basés sur ce schéma héritent des mêmes libellés.

>[!NOTE]
>
>Pour plus d’informations sur les différents libellés d’utilisation des données et leur utilisation prévue, voir la section [référence des libellés d’utilisation des données](./labels/reference.md). Si les libellés principaux disponibles ne couvrent pas tous les cas d’utilisation souhaités, vous pouvez [définir vos propres étiquettes personnalisées ;](./labels/user-guide.md#manage-custom-labels) ainsi que .

### Application dʼétiquettes à un jeu de données {#dataset-labels}

Sélectionner **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, sélectionnez le nom du jeu de données auquel vous souhaitez appliquer des libellés. Vous pouvez éventuellement utiliser le champ de recherche pour réduire la liste des jeux de données affichés.

![Image montrant un jeu de données sélectionné dans l’interface utilisateur de Platform](./images/e2e/select-dataset.png)

La vue Détails du jeu de données s’affiche. Sélectionnez la **[!UICONTROL Gouvernance des données]** pour afficher la liste des champs du jeu de données et des libellés qui y ont déjà été appliqués. Cochez les cases en regard des champs auxquels vous souhaitez ajouter des libellés, puis sélectionnez **[!UICONTROL Modification des étiquettes de gouvernance]** dans le rail de droite.

![Image montrant plusieurs champs de jeu de données sélectionnés pour l’étiquetage](./images/e2e/dataset-field-label.png)

>[!NOTE]
>
>Si vous souhaitez ajouter des libellés au jeu de données entier, cochez la case en regard de **[!UICONTROL Nom du champ]** pour mettre en surbrillance tous les champs avant de sélectionner **[!UICONTROL Modification des étiquettes de gouvernance]**.
>
>![Image présentant tous les champs mis en surbrillance pour un jeu de données](./images/e2e/label-whole-dataset.png)

Dans la boîte de dialogue suivante, sélectionnez les libellés à appliquer aux champs du jeu de données que vous avez choisis précédemment. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer les modifications]**.

![Image présentant tous les champs mis en surbrillance pour un jeu de données](./images/e2e/save-dataset-labels.png)

Continuez à suivre les étapes ci-dessus pour appliquer des libellés à différents champs (ou à différents jeux de données) si nécessaire. Lorsque vous avez terminé, vous pouvez passer à l’étape suivante de [activation des stratégies de gouvernance des données](#policy).

### Application de libellés à un schéma {#schema-labels}

Sélectionner **[!UICONTROL Schémas]** dans le volet de navigation de gauche, sélectionnez le schéma auquel vous souhaitez ajouter des libellés dans la liste.

>[!TIP]
>
>Si vous ne savez pas quel schéma s’applique à un jeu de données spécifique, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, puis sélectionnez le lien situé sous le **[!UICONTROL Schéma]** pour le jeu de données souhaité. Sélectionnez le nom du schéma dans la fenêtre contextuelle qui s’affiche pour ouvrir le schéma dans l’éditeur de schémas.
>
>![Image montrant un lien vers le schéma d’un jeu de données](./images/e2e/schema-from-dataset.png)

La structure du schéma apparaît dans l’éditeur de schémas. À partir de là, sélectionnez le **[!UICONTROL Étiquettes]** pour afficher une vue de liste des champs du schéma et des libellés qui y ont déjà été appliqués. Cochez les cases en regard des champs auxquels vous souhaitez ajouter des libellés, puis sélectionnez **[!UICONTROL Modification des étiquettes de gouvernance]** dans le rail de droite.

![Image montrant un champ de schéma unique sélectionné pour les étiquettes de gouvernance](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Si vous souhaitez ajouter des libellés à tous les champs du schéma, sélectionnez l’icône en forme de crayon sur la ligne supérieure.
>
>![Image montrant l’icône en forme de crayon sélectionnée dans la vue des libellés de schéma](./images/e2e/label-whole-schema.png)

Dans la boîte de dialogue suivante, sélectionnez les libellés à appliquer aux champs de schéma que vous avez choisis précédemment. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Image montrant plusieurs libellés ajoutés à un champ de schéma](./images/e2e/save-schema-labels.png)

Continuez à suivre les étapes ci-dessus pour appliquer des libellés à différents champs (ou à différents schémas) si nécessaire. Lorsque vous avez terminé, vous pouvez passer à l’étape suivante de [activation des stratégies de gouvernance des données](#policy).

## Activation des stratégies de gouvernance des données {#policy}

Après avoir appliqué des libellés à vos schémas et/ou jeux de données, vous pouvez créer des stratégies de gouvernance des données qui limitent les actions marketing pour lesquelles certains libellés peuvent être utilisés.

Sélectionner **[!UICONTROL Stratégies]** dans le volet de navigation de gauche pour afficher la liste des stratégies principales définies par Adobe, ainsi que les stratégies personnalisées créées précédemment par votre organisation.

Chaque étiquette principale est associée à une stratégie de base qui, lorsqu’elle est activée, impose les contraintes d’activation appropriées sur les données qui contiennent cette étiquette. Pour activer une stratégie de base, sélectionnez-la dans la liste, puis sélectionnez l’option **[!UICONTROL État de la stratégie]** bascule vers **[!UICONTROL Activé]**.

![Image montrant une stratégie principale activée dans l’interface utilisateur](./images/e2e/enable-core-policy.png)

Si les stratégies principales disponibles ne couvrent pas tous vos cas d’utilisation (par exemple, lorsque vous utilisez des étiquettes personnalisées que vous avez définies sous votre organisation), vous pouvez définir une stratégie personnalisée à la place. Dans la **[!UICONTROL Stratégies]** espace de travail, sélectionnez **[!UICONTROL Création d’une stratégie]**.

![Image montrant le [!UICONTROL Création d’une stratégie] en cours de sélection dans l’interface utilisateur](./images/e2e/create-policy.png)

Une fenêtre contextuelle s’affiche, vous invitant à sélectionner le type de stratégie à créer. Sélectionner **[!UICONTROL Politique de gouvernance des données]**, puis sélectionnez **[!UICONTROL Continuer]**.

![Image montrant le [!UICONTROL Politique de gouvernance des données] option sélectionnée](./images/e2e/governance-policy.png)

Dans l’écran suivant, fournissez un **[!UICONTROL Nom]** et facultatif **[!UICONTROL Description]** pour la stratégie. Dans le tableau ci-dessous, sélectionnez les libellés que cette stratégie doit rechercher. En d’autres termes, il s’agit des libellés que la stratégie empêchera d’utiliser pour les actions marketing que vous spécifiez à l’étape suivante.

Si vous sélectionnez plusieurs libellés, vous pouvez utiliser les options du rail de droite pour déterminer si tous les libellés doivent être présents pour que la stratégie applique des restrictions d’utilisation, ou si un seul d’entre eux doit être présent. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Image montrant la configuration de base de la stratégie terminée dans l’interface utilisateur](./images/e2e/configure-policy.png)

Dans l’écran suivant, sélectionnez les actions marketing pour lesquelles cette stratégie limitera l’utilisation des libellés sélectionnés précédemment. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Image montrant une action marketing affectée à une stratégie dans l’interface utilisateur](./images/e2e/select-marketing-action.png)

Le dernier écran affiche un résumé des détails de la stratégie et des actions qu’elle restreint pour les libellés. Sélectionner **[!UICONTROL Terminer]** pour créer la stratégie.

![Image montrant la confirmation de la configuration de la stratégie dans l’interface utilisateur](./images/e2e/confirm-policy.png)

La stratégie est créée, mais est définie sur [!UICONTROL Désactivé] par défaut. Sélectionnez la stratégie dans la liste et définissez la variable **[!UICONTROL État de la stratégie]** bascule vers **[!UICONTROL Activé]** pour activer la stratégie.

![Image montrant la stratégie créée activée dans l’interface utilisateur](./images/e2e/enable-created-policy.png)

Continuez à suivre les étapes ci-dessus pour créer et activer les stratégies dont vous avez besoin avant de passer à l’étape suivante.

## Gestion des actions marketing pour les destinations {#destinations}

Pour que vos stratégies activées déterminent avec précision les données qui peuvent être activées vers une destination, vous devez affecter des actions marketing spécifiques à cette destination.

Prenons l’exemple d’une stratégie activée qui empêche toute donnée contenant une `C2` du libellé utilisé pour l’action marketing &quot;[!UICONTROL Exporter vers un tiers]&quot;. Lors de l’activation de données vers une destination, la stratégie vérifie les actions marketing présentes sur la destination. Si &quot;[!UICONTROL Exporter vers un tiers]&quot; est présent, lors de la tentative d’activation de données avec un `C2` se traduit par une violation de la politique. Si &quot;[!UICONTROL Exporter vers un tiers]&quot; n’est pas présent, la stratégie n’est pas appliquée pour la destination et les données avec `C2` les libellés peuvent être librement activés.

When [connexion d’une destination dans l’interface utilisateur](../destinations/ui/connect-destination.md), la variable **[!UICONTROL Gouvernance]** dans le workflow, vous pouvez sélectionner les actions marketing qui s’appliquent à cette destination, ce qui détermine finalement les stratégies de gouvernance des données appliquées à la destination.

![Image montrant les actions marketing sélectionnées pour une destination](./images/e2e/destination-marketing-actions.png)

## Test de l’application des stratégies {#test}

Une fois que vous avez étiqueté vos données, activé les stratégies de gouvernance des données et affecté des actions marketing à vos destinations, vous pouvez tester si vos stratégies sont appliquées comme prévu.

Si vous configurez les éléments correctement, lorsque vous tentez d’activer des données qui sont restreintes par vos stratégies, l’activation est automatiquement refusée et un message de violation de la politique s’affiche, présentant des informations détaillées sur la traçabilité des données sur les causes de la violation.

Consultez le document sur [application automatique des stratégies](./enforcement/auto-enforcement.md) pour plus d’informations sur la manière d’interpréter les messages de violation de stratégie.

## Étapes suivantes

Ce guide décrit les étapes requises pour configurer et appliquer des stratégies de gouvernance des données dans vos workflows d’activation. Pour plus d’informations sur les composants de gouvernance des données impliqués dans ce guide, consultez la documentation suivante :

* [Libellés d’utilisation des données](./labels/overview.md)
* [Stratégies d’utilisation des données](./policies/overview.md)
* [Application des stratégies](./enforcement/overview.md)
