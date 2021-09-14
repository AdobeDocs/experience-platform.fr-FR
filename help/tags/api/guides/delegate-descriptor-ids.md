---
title: ID de descripteur de délégué
description: Découvrez les identifiants de descripteur délégué dans l’API Reactor et comment ils relient des ressources à des extensions.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: ht
source-wordcount: '501'
ht-degree: 100%

---

# ID de descripteur de délégué

Lors de l’utilisation des balises dans Adobe Experience Platform, toutes les fonctionnalités que vous pouvez déployer sur votre site sont fournies par des extensions. Les fonctionnalités fournies par chaque extension sont définies par le développeur de l’extension. Lorsqu’une extension est déployée, elle est regroupée avec ses différentes fonctionnalités sous la forme d’un [module d’extension](../endpoints/extension-packages.md). Les fonctionnalités que les développeurs ajoutent à un module d’extension sont considérées comme des « délégués » de ce module.

Chaque délégué d’un module d’extension reçoit un identifiant de descripteur délégué unique. L’identifiant de descripteur délégué pour une ressource spécifique indique au système le type de ressource dont il s’agit et à quel module d’extension il appartient.

## Syntaxe

Un identifiant de descripteur délégué se compose de trois chaînes unies par des caractères à deux points (`::`) représentant respectivement le nom du module d’extension, le type de délégué et le nom du délégué. Ces chaînes sont composées pour être lisibles par l’utilisateur. Elles sont automatiquement générées et affectées par le système lorsqu’un module d’extension est ingéré.

Par exemple, si un module d’extension nommé `example-package` comporte une action nommée `custom-code`, cette action aura l’identifiant de descripteur délégué suivant : `example-package::actions::custom-code`.

## Utilisation des identifiants de descripteur délégué sur les ressources applicables

Les identifiants de descripteur délégué sont importants pour comprendre à quel moment définir des composants de règle (événements, conditions et actions) et des éléments de données dans l’API. Les sections ci-dessous décrivent comment ces identifiants entrent en jeu pour chaque ressource.

### Composants de   règle

Un [composant de règle](../endpoints/rule-components.md) doit être associé à un événement, une condition ou une action appartenant à un module d’extension. Cela représente le « type » du composant de règle, car il se rapporte à la logique de la règle globale (un événement, une condition ou une action). Par conséquent, lors de la création d’un composant de règle, un identifiant de descripteur délégué doit être fourni pour indiquer à quel événement, condition ou action le composant de règle doit être associé.

Par exemple, pour créer un composant de règle d’événement basé sur un événement `click` dans un module d’extension `example-package`, le composant de règle utilisera la valeur `delegate_descriptor_id` suivante : `example-package::events::click`.

Pour plus d’informations, voir la section [Création d’un composant de règle](../endpoints/rule-components.md#create).

### Éléments de données

Un [élément de données](../endpoints/data-elements.md) doit être associé à un module d’extension lors de sa création, car chaque module d’extension définit les types compatibles pour ses éléments de données délégués, ainsi que leur comportement prévu.

Par exemple, pour créer un élément de données qui utilise le type `cookie` comme défini par un module d’extension `example-package`, l’élément de données utilise la valeur `delegate_descriptor_id` suivante : `example-package::dataElements::cookie`.

Voir la section [Création d’un élément de données](../endpoints/data-elements.md#create) pour plus d’informations.

### Extensions

Une [extension](../endpoints/extensions.md) est automatiquement associée à un module d’extension lors de sa création initiale et est représentée dans l’objet `relationships` de l’extension. Si votre extension nécessite des paramètres personnalisés, elle nécessite également un identifiant de descripteur délégué.

>[!NOTE]
>
>Les extensions qui ne nécessitent pas de paramètres personnalisés n’ont pas besoin d’un identifiant de descripteur délégué.

Par exemple, pour ajouter un identifiant de descripteur délégué à une extension appartenant au module d’extension `example-package`, l’extension utilisera la valeur `delegate_descriptor_id` suivante : `example-package::extensionConfiguration::config`.

Pour plus d’informations, consultez le guide sur la [création d’une extension](../endpoints/extensions.md#create).