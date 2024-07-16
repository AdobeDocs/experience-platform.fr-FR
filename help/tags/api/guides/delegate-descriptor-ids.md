---
title: ID de descripteur de délégué
description: Découvrez les ID de descripteur de délégué dans l’API Reactor et la façon dont ils lient les ressources aux extensions.
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 99%

---

# ID de descripteur de délégué

Lors de l’utilisation des balises dans Adobe Experience Platform, toutes les fonctionnalités que vous pouvez déployer sur votre site sont fournies par des extensions. Les fonctionnalités fournies par chaque extension sont définies par le développeur de l’extension. Lorsqu’une extension est déployée, elle est groupée avec ses différentes fonctionnalités sous la forme d’un [package d’extension](../endpoints/extension-packages.md). Les fonctionnalités que les développeurs ajoutent à un package d’extension sont considérées comme des « délégués » de ce module.

Chaque délégué de package d’extension reçoit un ID de descripteur de délégué unique. L’ID de descripteur de délégué d’une ressource spécifique indique au système de quel type de ressource il s’agit, ainsi qu’à quel package d’extension elle appartient.

## Syntaxe

Un ID de descripteur de délégué se compose de trois chaînes unies par deux caractères à deux points (`::`) représentant respectivement le nom du package d’extension, le type de délégué et le nom du délégué. Ces chaînes sont composées pour être lisibles par l’utilisateur. Elles sont automatiquement générées et affectées par le système lorsqu’un package d’extension est ingéré.

Par exemple, si un package d’extension nommé `example-package`comporte une action nommée`custom-code`, cette action est dotée de l’ID de descripteur de délégué suivant : `example-package::actions::custom-code`.

## Utilisation des ID de descripteur de délégué sur les ressources applicables

La compréhension du fonctionnement des ID de descripteur de délégué est importante pour la définition des composants de règle (événements, conditions et actions) et des éléments de données dans l’API. Les sections ci-dessous décrivent le fonctionnement de ces ID pour chaque ressource.

### Composants de règle

Un [composant de règle](../endpoints/rule-components.md) doit être associé à un événement, une condition ou une action appartenant à un package d’extension. Cela représente le « type » du composant de règle, car il se rapporte à la logique de la règle globale (un événement, une condition ou une action). Par conséquent, lors de la création d’un composant de règle, un ID de descripteur de délégué doit être fourni afin d’indiquer à quel événement, à quelle condition ou à quelle action le composant de règle doit être associé.

Par exemple, pour créer un composant de règle d’événement basé sur un événement `click` dans un package d’extension `example-package`, le composant de règle utilise la valeur `delegate_descriptor_id` suivante : `example-package::events::click`.

Pour plus d’informations, consultez la section relative à la [création d’un composant de règle](../endpoints/rule-components.md#create).

### Éléments de données

Un [élément de données](../endpoints/data-elements.md) doit être associé à un package d’extension lors de sa création. En effet, chaque package d’extension définit les types compatibles pour ses éléments de données délégués, ainsi que leur comportement prévu.

Par exemple, pour créer un élément de données qui utilise le type `cookie` comme défini par le package d’extension `example-package`, l’élément de données utilise la valeur `delegate_descriptor_id` suivante : `example-package::dataElements::cookie`.

Pour plus d’informations, consultez la section relative à la [création d’un élément de données](../endpoints/data-elements.md#create).

### Extensions

Une [extension](../endpoints/extensions.md) est automatiquement associée à un package d’extension lors de sa création initiale et est représentée dans l’objet `relationships` de l’extension. Si votre extension requiert des paramètres personnalisés, elle requiert alors également un ID de descripteur de délégué.

>[!NOTE]
>
>Les extensions qui ne requièrent pas de paramètres personnalisés n’ont pas besoin d’un ID de descripteur de délégué.

Par exemple, pour ajouter un ID de descripteur de délégué à une extension appartenant au package d’extension `example-package`, l’extension utilise la valeur `delegate_descriptor_id` suivante : `example-package::extensionConfiguration::config`.

Pour plus d’informations, consultez le guide sur la [création d’une extension](../endpoints/extensions.md#create).
