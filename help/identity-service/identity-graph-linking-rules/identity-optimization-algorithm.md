---
title: Algorithme d’optimisation des identités
description: Découvrez l’algorithme d’optimisation des identités dans Identity Service.
hide: true
hidefromtoc: true
badge: Alpha
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 2%

---

# Algorithme d’optimisation des identités

>[!IMPORTANT]
>
>L’algorithme d’optimisation des identités est en Alpha. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

L’algorithme d’optimisation des identités est une règle qui permet de s’assurer qu’un graphique d’identités est représentatif d’une seule personne et, par conséquent, empêche la fusion indésirable d’identités sur Real-time Customer Profile.

## Paramètres d&#39;entrée

Un profil fusionné unique et son graphique d’identités correspondant doivent représenter une seule personne (entité de personne). Une seule personne est généralement représentée par des identifiants de gestion de la relation client et/ou des identifiants de connexion. On s’attend à ce qu’aucun deux individus (ID CRM) ne soient fusionnés dans un seul profil ou graphique.

Vous devez spécifier les espaces de noms qui représentent une entité de personne dans Identity Service à l’aide de l’algorithme d’optimisation des identités. Par exemple, si une base de données CRM définit un compte utilisateur à associer à un identifiant CRM unique et à une seule adresse email, les paramètres d’identité de cet environnement de test se présentent comme suit :

* Espace de noms de l’ID de gestion de la relation client = unique
* Espace de noms de courriel = unique

Un espace de noms que vous déclarez unique est automatiquement configuré pour avoir une limite maximale d’un dans un graphique d’identités donné. Par exemple, si vous déclarez un espace de noms d’identifiant CRM unique, un graphique d’identités ne peut avoir qu’une seule identité contenant un espace de noms d’identifiant CRM.

>[!NOTE]
>
>* Actuellement, l’algorithme ne prend en charge que l’utilisation d’un seul identifiant de connexion (un espace de noms de connexion). Pour le moment, il n’est pas possible de prendre en charge plusieurs identifiants de connexion (plusieurs espaces de noms d’identité utilisés pour la connexion), des graphiques d’entités domestiques et des structures de graphiques hiérarchiques.
>
>* Tous les espaces de noms qui sont des identifiants de personne et utilisés dans l’environnement de test pour générer des graphiques d’identité doivent être marqués comme un espace de noms unique. Dans le cas contraire, il se peut que des résultats de liaison indésirables s’affichent.

## Processus

Lors de l’ingestion de nouvelles identités, Identity Service vérifie si les nouvelles identités et leurs espaces de noms correspondants se traduiront par le dépassement des limites configurées. Si les limites ne sont pas dépassées, l’ingestion de nouvelles identités se poursuit et ces identités sont liées au graphique. Toutefois, si les limites sont dépassées, l’algorithme d’optimisation des identités met à jour le graphique de sorte que l’horodatage le plus récent soit respecté et que les liens les plus anciens avec les espaces de noms de priorité inférieure soient supprimés.

## Exemples de scénarios pour l’algorithme d’optimisation des identités

La section suivante décrit le comportement de l’algorithme d’optimisation des identités dans des scénarios tels que l’appareil partagé ou l’ingestion de données avec le même horodatage.

### Appareil partagé

Un appareil partagé fait référence à un appareil utilisé par plusieurs individus. Par exemple, un appareil partagé peut être un ordinateur portable ou une tablette que vous partagez avec un partenaire ou un membre de votre famille, un ordinateur de bibliothèque ou un kiosque public.

>[!BEGINTABS]

>[!TAB Exemple 1]

| Espace de noms | Limite |
| --- | --- |
| Identifiant CRM | 1 |
| E-mail | 1 |
| ECID | S/O |

Dans cet exemple, l’identifiant CRM et le courrier électronique sont désignés comme espaces de noms uniques. At `timestamp=0`, un jeu de données d’enregistrement CRM est ingéré et crée deux graphiques différents en raison de la configuration de limite. Chaque graphique contient un identifiant CRM et un espace de noms Email.

* `timestamp=1`: Jane se connecte à votre site web de commerce électronique à l’aide d’un ordinateur portable. Jane est représentée par son identifiant CRM et son e-mail, tandis que le navigateur web sur son ordinateur portable qu’elle utilise est représenté par un ECID.
* `timestamp=2`: John se connecte à votre site web de commerce électronique à l’aide du même ordinateur portable. John est représenté par son identifiant CRM et son e-mail, tandis que le navigateur web qu’il a utilisé est déjà représenté par un ECID. Comme le même ECID est lié à deux graphiques différents, Identity Service peut savoir que cet appareil (ordinateur portable) est un appareil partagé.
* Cependant, en raison de la configuration de limite qui définit un maximum d’un espace de noms d’identifiant CRM et d’un espace de noms d’email par graphique, l’algorithme d’optimisation de l’identité divise le graphique en deux.
   * Enfin, puisque John est le dernier utilisateur authentifié, l’ECID qui représente l’ordinateur portable reste lié à son graphique au lieu de celui de Jane.

![cas d’appareil partagé 1](../images/identity-settings/shared-device-case-one.png)

>[!TAB Exemple 2]

| Espace de noms | Limite |
| --- | --- |
| Identifiant CRM | 1 |
| ECID | S/O |

Dans cet exemple, l’espace de noms de l’identifiant CRM est désigné comme un espace de noms unique.

* `timestamp=1`: Jane se connecte à votre site web de commerce électronique à l’aide d’un ordinateur portable. Elle est représentée par son identifiant CRM et le navigateur web sur l’ordinateur portable est représenté par l’ECID.
* `timestamp=2`: John se connecte à votre site web de commerce électronique à l’aide du même ordinateur portable. Il est représenté par son identifiant CRM et le navigateur web qu’il utilise est représenté par le même ECID.
   * Cet événement lie deux identifiants CRM indépendants au même ECID, qui dépasse la limite configurée d’un identifiant CRM.
   * Par conséquent, l’algorithme d’optimisation de l’identité supprime l’ancien lien, qui dans ce cas est l’identifiant CRM Jane lié à `timestamp=1`.
   * Cependant, bien que l’identifiant CRM de Jane n’existe plus sous forme de graphique sur Identity Service, il persistera toujours en tant que profil sur Real-time Customer Profile. En effet, un graphique d’identités doit contenir au moins deux identités liées. En raison de la suppression des liens, l’identifiant CRM de Jane ne dispose plus d’une autre identité à laquelle créer un lien.

![shared-device-case-deux](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Mauvais email

Dans certains cas, un utilisateur peut saisir des valeurs erronées pour son adresse électronique et/ou ses numéros de téléphone.

| Espace de noms | Limite |
| --- | --- |
| Identifiant CRM | 1 |
| E-mail | 1 |
| ECID | S/O |

Dans cet exemple, l’identifiant CRM et les espaces de noms de courrier électronique sont désignés comme uniques. Supposons que Jane et John se soient inscrits à votre site web d’e-commerce à l’aide d’une valeur d’e-mail incorrecte (test, par exemple).<span>@test.com).

* `timestamp=1`: Jane se connecte à votre site web de commerce électronique à l’aide de Safari sur son iPhone, en établissant son identifiant CRM (informations de connexion) et son ECID (navigateur).
* `timestamp=2`: John se connecte à votre site web de commerce électronique à l’aide de Google Chrome sur son iPhone, en établissant son identifiant CRM (informations de connexion) et son ECID (navigateur).
* `timestamp=3`: votre ingénieur de données ingère l’enregistrement CRM de Jane, ce qui entraîne le lien entre son identifiant CRM et le mauvais courrier électronique.
* `timestamp=4`: votre ingénieur de données ingère l’enregistrement CRM de John, ce qui entraîne l’association de son identifiant CRM au mauvais courrier électronique.
   * Cela devient alors une violation des limites configurées, car il crée un graphique unique avec deux espaces de noms d’ID de gestion de la relation client.
   * Par conséquent, l’algorithme d’optimisation des identités supprime l’ancien lien, qui dans ce cas est le lien entre l’identité de Jane avec l’espace de noms de l’ID de gestion de la relation client et l’identité avec le test.<span>@test.

Avec l’algorithme d’optimisation des identités, les valeurs d’identité erronées telles que les faux emails ou les numéros de téléphone ne sont pas propagées sur plusieurs graphiques d’identités différents.

![bad-email](../images/identity-settings/bad-email.png)

### Association d’événements anonymes

Les ECID stockent les événements non authentifiés (anonymes), tandis que l’ID de gestion de la relation client stocke les événements authentifiés. Dans le cas des appareils partagés, l’ECID (porteur d’événements non authentifiés) est associé à la variable **dernier utilisateur authentifié**.

Consultez le diagramme ci-dessous pour mieux comprendre le fonctionnement de l’association d’événements anonymes :

* Kevin et Nora partagent une tablette.
   * `timestamp=1`: Kevin se connecte à un site web de commerce électronique à l’aide de son compte, établissant ainsi son identifiant CRM (informations de connexion) et un ECID (navigateur). Au moment de la connexion, Kevin est désormais considéré comme le dernier utilisateur authentifié.
   * `timestamp=2`: Nora se connecte à un site web de commerce électronique à l’aide de son compte, établissant ainsi son identifiant CRM (informations de connexion) et le même ECID. Au moment de la connexion, Nora est désormais considérée comme le dernier utilisateur authentifié.
   * `timestamp=3`: Kevin utilise la tablette pour parcourir le site de commerce électronique, mais ne se connecte pas avec son compte. L’activité de navigation de Kevin est ensuite stockée dans l’ECID, qui, à son tour, est associé à Nora car elle est le dernier utilisateur authentifié. A ce stade, Nora possède les événements anonymes.
      * Jusqu’à ce que Kevin se reconnecte, le profil fusionné de Nora sera associé à tous les événements non authentifiés stockés par rapport à l’ECID (les événements étant l’endroit où ECID est l’identité principale).
   * `timestamp=4`: Kevin se connecte pour la seconde fois. À ce stade, il redevient le dernier utilisateur authentifié et possède désormais les événements non authentifiés :
      * Avant sa connexion initiale avant `timestamp=1`; et
      * Toute activité qu&#39;il ou Nora a effectuée en naviguant anonymement entre la première et la seconde connexion de Kevin.

![anon-event-association](../images/identity-settings/anon-event-association.png)


## Étapes suivantes

Pour plus d’informations sur les règles de liaison des graphiques d’identités, consultez la documentation suivante :

* [Présentation des règles de liaison de graphiques d’identités](./overview.md)
* [Exemples de scénarios de configuration des règles de liaison de graphiques d’identités](./example-scenarios.md)
* [Logique de liaison d’identités](../features/identity-linking-logic.md)
* [Identity Service et Real-time Customer Profile](../identity-and-profile.md)
