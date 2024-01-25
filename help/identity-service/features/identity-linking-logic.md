---
title: Logique de liaison d’Identity Service
description: Découvrez comment Identity Service relie des identités disparates pour créer une vue d’ensemble complète d’un client.
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 45170c78b9d15c7cc9d71f2d0dab606ea988a783
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# Logique de liaison d’Identity Service

Un lien entre deux identités est établi lorsque l’espace de noms de l’identité et les valeurs d’identité correspondent.

Deux types d’identités sont liés :

* **Enregistrements de profil**: ces identités proviennent généralement de systèmes CRM.
* **Événements d’expérience**: ces identités proviennent généralement de la mise en oeuvre de WebSDK ou de la source Adobe Analytics.

## Présentation de la logique de liaison d’Identity Service

Une identité se compose d’un espace de noms d’identité et d’une valeur d’identité.

* Un espace de noms d’identité est le contexte d’une valeur d’identité donnée à . Les exemples d’espaces de noms d’identité courants incluent l’ID CRM, le courrier électronique et le téléphone.
* Une valeur d’identité est la chaîne qui représente une entité du monde réel. Par exemple : &quot;julien&quot;<span>@acme.com&quot; peut être une valeur d’identité pour un espace de noms Email et 555-555-1234 peut être une valeur d’identité correspondante pour un espace de noms Phone.

>[!TIP]
>
>L’espace de noms d’identité est important, car sans lui, la valeur d’identité perd son contexte et ne dispose pas d’informations suffisantes pour correspondre correctement aux identités.

Consultez les diagrammes suivants pour une représentation visuelle du fonctionnement de la logique de liaison d’Identity Service :

>[!BEGINTABS]

>[!TAB Graphique existant]

Supposons que vous ayez un graphique d’identités existant avec trois identités liées :

* PHONE : (555)-555-1234
* EMAIL : julien<span>@acme.com
* Identifiant CRM : 60013ABC

![graphique existant](../images/identity-settings/existing-graph.png)

>[!TAB Données entrantes]

Une paire d’identités est ingérée dans votre graphique et cette paire contient :

* Identifiant CRM : 60013ABC
* ECID:100066526

![données entrantes](../images/identity-settings/incoming-data.png)

>[!TAB Graphique mis à jour]

Identity Service reconnaît que l’ID CRM : 60013ABC existe déjà dans votre graphique. Il lie donc uniquement le nouvel ECID.

![graphique mis à jour](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Scénario client

Vous êtes ingénieur en données et vous ingérez le jeu de données CRM suivant (enregistrement de profil) à Experience Platform.

| Identifiant CRM** | Téléphone* | Adresse e-mail* | Prénom | Nom |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` - Indique le champ marqué comme identité principale.
>* `*` - Indique le champ marqué comme identité secondaire.
>
>Identity Service ne fait pas la distinction entre l’identité principale et l’identité secondaire. Tant qu’un champ est marqué comme identité, il sera ingéré dans Identity Service.

Vous avez également implémenté WebSDK et ingéré un jeu de données WebSDK (Experience Event) avec les tableaux de données suivants :

| Date et heure | Identités dans l’événement* | Événement |
| --- | --- | --- |
| `t=1` | ECID:38652 | Afficher la page d’accueil |
| `t=2` | ECID:38652, ID CRM:31260XYZ | Rechercher des chaussures |
| `t=3` | ECID:44675 | Afficher la page d’accueil |
| `t=4` | ECID : 44675, ID CRM : 31260XYZ | Afficher l’historique des achats |

>[!NOTE]
>
>* `*` - Indique le champ marqué comme identité, avec ECID marqué comme principal.
>* Par défaut, l’identifiant de personne (dans ce cas, l’identifiant CRM) est désigné comme identité principale. Si l’identifiant de personne n’existe pas, l’identifiant du cookie (dans ce cas, l’ECID) devient l’identité principale.

Dans cet exemple :

* `t=1`, utilisait un ordinateur de bureau (ECID:38652) et pour afficher le navigateur de la page d’accueil de manière anonyme.
* `t=2`, utilisait le même ordinateur de bureau, se connectait (ID CRM : 31260XYZ), puis recherchait des chaussures.
   * Une fois qu’un utilisateur est connecté, l’événement envoie à la fois l’identifiant ECID et l’identifiant CRM à Identity Service.
* `t=3`, utilisait un ordinateur portable (ECID:44675) et naviguait de manière anonyme.
* `t=4`, a utilisé le même ordinateur portable, s’est connecté (ID CRM : 31260XYZ), puis a consulté l’historique des achats.


>[!BEGINTABS]

>[!TAB timestamp=0]

At `timestamp=0`, vous disposez de deux graphiques d’identités pour deux clients différents. Tous deux sont représentés par trois identités liées.

| | Identifiant CRM | E-mail | Téléphone |
| --- | --- | --- | --- |
| Customer One | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Client deux | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-zero](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

At `timestamp=1`, un client utilise un ordinateur portable pour visiter votre site web de commerce électronique, afficher votre page d’accueil et naviguer de manière anonyme. Cet événement de navigation anonyme est identifié comme ECID:38652. Comme Identity Service ne stocke que les événements avec au moins deux identités, ces informations ne sont pas stockées.

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

At `timestamp=2`, un client utilise le même ordinateur portable pour visiter votre site web d’e-commerce. Ils se connectent avec leur nom d’utilisateur et leur mot de passe, et ils recherchent des chaussures. Identity Service identifie le compte du client lorsqu’il se connecte, car il correspond à son identifiant CRM : 31260XYZ. En outre, Identity Service associe ECID:38562 à l’ID CRM:31260XYZ, car ils utilisent tous deux le même navigateur sur le même appareil.

![timestamp-two](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

At `timestamp=3` un client utilise une tablette pour visiter votre site web d’e-commerce et naviguer de manière anonyme. Cet événement de navigation anonyme est identifié comme ECID:44675. Comme Identity Service ne stocke que les événements avec au moins deux identités, ces informations ne sont pas stockées.

![timestamp-trois](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

At `timestamp=4`, un client utilise la même tablette, se connecte à son compte (ID CRM : 31260XYZ) et affiche son historique des achats. Cet événement lie leur ID CRM : 31260XYZ à l’identifiant de cookie affecté à l’activité de navigation anonyme, ECID : 44675, et relie ECID : 44675 au graphique d’identités de customer two.

![timestamp-quatre](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]
