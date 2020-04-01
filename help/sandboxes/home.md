---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des sandbox
topic: overview
translation-type: tm+mt
source-git-commit: 564940f37b66159c84ca7402bd3648010232182b

---


# Présentation des sandbox

Adobe Experience Platform est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

In order to address this need, Experience Platform provides **sandboxes** which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

Ce présente un aperçu général des sandbox dans la plateforme d’expérience.

## Présentation des sandbox

Les sandbox sont des partitions virtuelles au sein d’une seule instance d’Experience Platform, qui permettent une intégration transparente au processus de développement de vos applications d’expérience numérique. Une instance de plateforme d’expérience prend en charge un sandbox de production et plusieurs sandbox hors production, chaque sandbox conservant sa propre bibliothèque indépendante de ressources de plateforme (y compris les , les jeux de données, les, les , etc.).  Tout le contenu et les actions entreprises dans un sandbox sont limités à ce sandbox et n’affectent aucun autre sandbox.

Les sandbox hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre sandbox de production. En outre, les sandbox hors production disposent d’une fonction de réinitialisation qui supprime toutes les ressources créées par les clients du sandbox. Les sandbox hors production ne peuvent pas être convertis en sandbox de production.

>[!NOTE] Lorsqu’un sandbox est créé pour la première fois, il ne contient aucune donnée. Chaque sandbox conservant sa propre banque de données isolée, ils doivent également importer leurs données indépendamment.

En résumé, les sandbox offrent les avantages suivants :

* **Gestion** du cycle de vie des applications : Créez des de  virtuels distincts pour développer et développer des applications d’expérience numérique.
* **Gestion** de projet et de marque : Permettre à plusieurs projets de fonctionner en parallèle au sein de la même organisation IMS, tout en offrant isolement et . Les prochaines versions prendront en charge le déploiement dans plusieurs régions.
* **Un écosystème** de développement flexible : Fournissez des sandbox de manière transparente, évolutive et économique pour l’exploration, l’activation et la démonstration.

##  pour sandbox

Par défaut, tous les utilisateurs d’une organisation ont accès à un sandbox de production. L’accès aux sandbox hors production doit être accordé par un administrateur système, un administrateur de produit ou un administrateur de  de produits via la console d’administration [Adobe](https://adminconsole.adobe.com).

Pour pouvoir , créer, mettre à jour ou supprimer des sandbox hors production, les utilisateurs doivent également disposer des autorisations d’administration de sandbox.

Pour plus d’informations sur la gestion des rôles et des autorisations pour les sandbox, reportez-vous à la présentation [du](../access-control/home.md).

## Sandbox dans l’interface utilisateur de la plateforme d’expérience

Dans l’interface [utilisateur de la plateforme](https://platform.adobe.com)d’expérience, les utilisateurs peuvent basculer entre les sandbox auxquels ils ont accès en utilisant le contrôle de commutation **de** sandbox en haut à gauche de l’écran.  Les utilisateurs disposant de droits d’administration Sandbox ont également accès à l’onglet **Sandbox** dans le volet de navigation de gauche, où ils peuvent  et gérer des sandbox pour leur entreprise. Pour plus d’informations sur l’utilisation des sandbox dans l’interface utilisateur, voir le guide [de l’utilisateur](ui/overview.md)sandbox.

## Sandbox dans les API de plateformes d’expérience

Lors d’appels aux API de plateforme d’expérience, un nom de sandbox doit être fourni sous l’en-tête `x-sandbox-name`. Par exemple, lors d’un appel à l’API [du service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catalogue pour de tous les jeux de données dans le sandbox de production, le nom du sandbox (&quot;prod&quot;) est fourni comme en-tête dans la demande d’API :

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Si `x-sandbox-name` n’est pas inclus dans un appel d’API, le système utilise un sandbox par défaut à la place. Toutefois, la meilleure pratique consiste à toujours inclure cet en-tête dans tous les appels d’API, même lorsque vous utilisez le sandbox par défaut. C’est pourquoi la documentation de l’API pour la plateforme d’expérience traite `x-sandbox-name` comme un en-tête obligatoire.

### API Sandbox

L’API Sandbox vous permet de gérer les sandbox à l’aide des opérations de l’API RESTful. Consultez le guide [du développeur](api/getting-started.md) sandbox pour obtenir des informations détaillées sur l’utilisation de l’API, notamment des requêtes correctement formatées et des exemples de réponses.

## Étapes suivantes

En lisant ce , vous avez été initié aux concepts essentiels concernant les sandbox dans Experience Platform. Pour obtenir des instructions détaillées sur la gestion des sandbox, reportez-vous au guide [de l’](ui/overview.md) utilisateur pour l’interface utilisateur ou au guide [du](./api/getting-started.md) développeur pour l’API.

Bien que les sandbox constituent un outil précieux pour isoler les de plateformes  pour votre équipe de développement, vous pouvez également gérer des plus détaillés à l’aide de la console d’administration Adobe. See the [access control overview](../access-control/home.md) for more information.