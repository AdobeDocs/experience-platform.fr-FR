---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;énumération;identité principale;identité principale;profil individuel XDM;Événement d’expérience;Événement d’expérience XDM;ExperienceEvent XDM;experienceEvent;experienceevent;Experienceevenet XDM;conception de schéma;bonnes pratiques
solution: Experience Platform
title: Bonnes pratiques de modélisation des données
description: Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques de la composition de schémas à utiliser dans Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 7a763a978443c0a074e6368448320056759f72bb
workflow-type: tm+mt
source-wordcount: '3429'
ht-degree: 49%

---

# Bonnes pratiques de modélisation des données

[!DNL Experience Data Model] (XDM) est le cadre de base qui normalise les données d’expérience client en fournissant des structures et des définitions communes à utiliser dans les services Adobe Experience Platform en aval. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées à une représentation commune et utilisées pour obtenir des informations précieuses à partir des actions des clients, définir des audiences de clients et exprimer les attributs des clients à des fins de personnalisation.

XDM étant extrêmement polyvalent et personnalisable par sa conception, il est important de suivre les bonnes pratiques de modélisation des données lors de la conception de vos schémas. Ce document couvre les principales décisions et considérations à prendre lors du mappage de vos données d’expérience client à XDM.

## Commencer

Avant de lire ce guide, consultez la [présentation du système XDM](../home.md) pour une présentation détaillée de XDM et de son rôle dans Experience Platform.

Comme ce guide se concentre exclusivement sur les considérations clés concernant la conception de schémas, nous vous recommandons vivement de lire le [principes de base de la composition des schémas](./composition.md) pour des explications détaillées des éléments de schéma individuels mentionnés tout au long de ce guide.

## Résumé des bonnes pratiques {#summary}

L’approche recommandée pour concevoir votre modèle de données à utiliser dans Experience Platform peut être résumée comme suit :

1. Comprendre les cas d’utilisation professionnels pour vos données.
1. Identifiez les sources de données principales qui doivent être introduites dans Experience Platform pour répondre à ces cas d’utilisation.
1. Identifier toutes les sources de données secondaires susceptibles d’être intéressantes. Par exemple, si actuellement une seule unité commerciale de votre organisation souhaite transférer ses données vers Experience Platform, une unité commerciale similaire pourrait également souhaiter transférer des données similaires à l’avenir. En prenant en compte ces sources secondaires, vous pouvez normaliser le modèle de données dans l’ensemble de votre organisation.
1. Créez un diagramme de relation d’entité détaillé (ERD) pour les sources de données qui ont été identifiées.
1. Convertissez l’ERD détaillé en un ERD centré sur Experience Platform (y compris les profils, les événements d’expérience et les entités de recherche).

Les étapes relatives à l’identification des sources de données applicables requises pour exécuter vos cas d’utilisation professionnels varient d’une organisation à l’autre. Bien que le reste des sections de ce document se concentre sur les dernières étapes d’organisation et de construction d’un ERD une fois les sources de données identifiées, les explications des différents composants du diagramme peuvent vous éclairer sur les décisions à prendre concernant les sources de données qui doivent être migrées vers Experience Platform.

## Créer un ERD détaillé {#create-an-erd}

Une fois que vous avez déterminé les sources de données que vous souhaitez importer dans Experience Platform, créez un ERD détaillé pour vous aider à orienter le processus de mappage de vos données vers les schémas XDM.

L’exemple ci-dessous représente un ERD simplifié pour une société qui souhaite importer des données dans Experience Platform. Le diagramme présente les entités essentielles qui doivent être triées en classes XDM, notamment les comptes clients, les hôtels et plusieurs événements d’e-commerce courants.

![Diagramme relationnel d’entité qui met en évidence les entités essentielles qui doivent être triées en classes XDM pour l’ingestion de données.](../images/best-practices/erd.png)

## Trier les entités en catégories de profil, de recherche et d’événement {#sort-entities}

Une fois que vous avez créé un ERD pour identifier les entités essentielles que vous souhaitez importer dans Experience Platform, ces entités doivent être triées en catégories de profil, de recherche et d’événement :

| Catégorie | Description |
| --- | --- |
| Entités de profil | Les entités de profil représentent les attributs relatifs à une personne, généralement un client ou une cliente. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la classe **[!DNL XDM Individual Profile]**. |
| Entités de recherche | Les entités de recherche représentent des concepts qui peuvent être associés à une personne, mais qui ne peuvent pas être directement utilisés pour identifier la personne. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur des **classes personnalisées**, et sont liées à des profils et des événements au moyen de [relations de schéma](../tutorials/relationship-ui.md). |
| Entités d’événement | Les entités d’événement représentent des concepts liés aux actions qu’un client peut entreprendre, aux événements système ou à tout autre concept dans lequel vous souhaitez peut-être suivre les modifications au fil du temps. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la classe **[!DNL XDM ExperienceEvent]**. |

{style="table-layout:auto"}

### Considérations pour le tri des entités {#considerations}

Les sections ci-dessous fournissent des conseils supplémentaires sur la manière de trier vos entités dans les catégories ci-dessus.

#### Données mutables et immuables {#mutable-and-immutable-data}

Une principale méthode de tri entre les catégories d’entités consiste à déterminer si les données capturées sont mutables ou non.

Les attributs appartenant aux profils ou aux entités de recherche sont généralement mutables. Par exemple, les préférences d’un client ou d’une cliente peuvent changer au fil du temps et les paramètres d’une formule d’abonnement peuvent être mis à jour en fonction des tendances du marché.

En revanche, les données d’événement sont généralement immuables. Puisque les événements sont associés à une date et à une heure spécifique, l’« instantané système » fourni par un événement ne change pas. Par exemple, un événement peut capturer les préférences d’un client ou d’une cliente lors d’un passage en caisse d’un panier, et ne change pas même si les préférences finissent par changer ultérieurement. Les données d’événement ne peuvent pas être modifiées après leur enregistrement.

En résumé, les profils et les entités de recherche contiennent des attributs mutables et représentent les informations les plus récentes sur les objets qu’ils capturent, tandis que les événements sont des enregistrements non modifiables du système à un moment spécifique.

#### Attributs du client {#customer-attributes}

Si une entité contient des attributs liés à un client ou une cliente en particulier, il s’agit probablement d’une entité de profil. Voici quelques exemples d’attributs :

* Informations personnelles telles que le nom, la date de naissance, le sexe et le ou les identifiants de compte.
* Informations de localisation telles que les adresses et les informations GPS.
* Coordonnées telles que les numéros de téléphone et les adresses e-mail.

#### Suivi des données au fil du temps {#track-data}

Si vous souhaitez analyser la manière dont certains attributs au sein d’une entité changent au fil du temps, il s’agit probablement d’une entité d’événement. Par exemple, l’ajout d’articles à un panier peut être suivi en tant qu’événement ajouter-au-panier dans Experience Platform :

| Identifiant client | Type | ID de produit | Quantité | Date et heure |
| --- | --- | --- | --- | --- |
| 1234567 | Ajouter | 275098 | 2 | 1er octobre 10:32 |
| 1234567 | Supprimer | 275098 | 1 | 1er octobre 10:33 |
| 1234567 | Ajouter | 486502 | 1 | 1er octobre 10:41 |
| 1234567 | Ajouter | 910482 | 5 | 3 octobre, 14:15 |

{style="table-layout:auto"}

#### Cas d’utilisation de segmentation {#segmentation-use-cases}

Lors de la catégorisation de vos entités, il est important de réfléchir aux audiences que vous pourriez vouloir créer pour répondre aux cas d’utilisation particuliers de votre entreprise.

Prenons l’exemple d’une entreprise qui souhaite connaître toutes les personnes membres « Gold » ou « Platinum » de son programme de fidélité ayant effectué plus de cinq achats au cours de l’année dernière. Sur la base de cette logique de segmentation, vous pouvez tirer les conclusions suivantes concernant la manière dont les entités pertinentes doivent être représentées :

* « Gold » et « Platinum » représentent des statuts de fidélité applicables à une personne cliente particulière. Puisque la logique de segmentation ne concerne que le statut de fidélité actuel de la clientèle, ces données peuvent être modélisées dans le cadre d’un schéma de profil. Si vous souhaitez suivre les modifications du statut de fidélité au fil du temps, vous pouvez également créer un schéma d’événement supplémentaire pour les modifications du statut de fidélité.
* Les achats sont des événements qui se produisent à un moment donné et la logique de segmentation concerne les événements d’achat dans une fenêtre temporelle spécifiée. Ces données doivent donc être modélisées en tant que schéma d’événement.

#### Cas d’utilisation d’activation {#activation-use-cases}

Outre les considérations relatives aux cas d’utilisation de segmentation, vous devez également consulter les cas d’utilisation d’activation pour ces audiences afin d’identifier d’autres attributs pertinents.

Par exemple, une entreprise a créé une audience basée sur la règle stipulant que `country = US`. Ensuite, lors de l’activation de cette audience vers certaines cibles en aval, l’entreprise souhaite filtrer tous les profils exportés en fonction de l’État d’origine. Par conséquent, un attribut `state` doit également être capturé dans l’entité de profil applicable.

#### Valeurs agrégées {#aggregated-values}

En fonction du cas d’utilisation et de la granularité de vos données, vous devez décider si certaines valeurs doivent être pré-agrégées avant d’être incluses dans un profil ou une entité d’événement.

Par exemple, une entreprise souhaite créer une audience en fonction du nombre d’achats. Vous pouvez choisir d’incorporer ces données avec la granularité la plus faible en incluant chaque événement d’achat horodaté comme une entité à part entière. Cependant, cela peut parfois augmenter de façon exponentielle le nombre d’événements enregistrés. Pour réduire le nombre d’événements ingérés, vous pouvez choisir de créer une valeur agrégée `numberOfPurchases` sur une période d’une semaine ou d’un mois. D’autres fonctions d’agrégation telles que MIN et MAX peuvent également s’appliquer à ces situations.

>[!CAUTION]
>
>Experience Platform n’effectue actuellement pas d’agrégation automatique de valeurs, bien que cela soit prévu pour les prochaines versions. Si vous choisissez d’utiliser des valeurs agrégées, vous devez effectuer les calculs en externe avant d’envoyer les données à Experience Platform.

#### Cardinalité {#cardinality}

Les cardinalités établies dans votre ERD peuvent également fournir des indices sur la manière de classer vos entités. S’il existe une relation un-à-plusieurs entre deux entités, l’entité qui représente le « plusieurs » est susceptible d’être une entité d’événement. Cependant, il existe également des cas où le « plusieurs » est un ensemble d’entités de recherche fournies sous forme de tableau dans une entité de profil.

>[!NOTE]
>
>Comme il n’existe pas d’approche universelle pour tous les cas d’utilisation, il est important de tenir compte des avantages et des inconvénients de chaque situation lors de la classification des entités en fonction de leur cardinalité. Consultez la [section suivante](#pros-and-cons) pour plus d’informations.

Le tableau suivant décrit certaines relations d’entité courantes et les catégories qui peuvent en découler :

| Relation | Cardinalité | Catégories d’entité |
| --- | --- | --- |
| Passage en caisse du client et du panier | Un à plusieurs | Une même personne peut avoir plusieurs passages en caisse, c’est-à-dire des événements qui peuvent être suivis au fil du temps. Le client serait donc une entité de profil, tandis que le passage en caisse serait une entité d’événement. |
| Compte client et de fidélité | Un à un | Un seul client ne peut avoir qu’un seul compte de fidélité, et un compte de fidélité ne peut appartenir qu’à un seul client. Comme il s’agit d’une relation un-à-un, les comptes client et de fidélité représentent tous deux des entités de profil. |
| Client et abonnement | Un à plusieurs | Un seul client peut avoir plusieurs abonnements. Puisque l’entreprise ne s’intéresse qu’aux abonnements actuels d’un client, le client est une entité de profil, tandis que l’abonnement est une entité de recherche. |

{style="table-layout:auto"}

### Avantages et inconvénients de différentes classes d’entités {#pros-and-cons}

Bien que la section précédente ait fourni quelques instructions générales pour déterminer comment classer vos entités, il est important de comprendre que choisir une catégorie d’entités plutôt qu’une autre comporte souvent des avantages et des inconvénients. L’étude de cas suivante a pour but d’illustrer la manière dont vous pouvez envisager vos options dans ces situations.

Une entreprise effectue le suivi des abonnements actifs de ses clients, un même client pouvant disposer de nombreux abonnements. L’entreprise souhaite également inclure des abonnements pour les cas d’utilisation de segmentation, comme la recherche de tous les utilisateurs avec des abonnements actifs.

Dans ce scénario, l’entreprise dispose de deux options potentielles pour représenter les abonnements d’un client dans son modèle de données :

1. [l’utilisation des attributs de profil](#profile-approach)
1. [l’utilisation des entités d’événement](#event-approach)

#### Approche 1 : utilisation des attributs de profil {#profile-approach}

La première approche consiste à inclure un tableau de `subscriptionID` dans l’entité de profil pour le client.

![Schéma du client dans l’éditeur de schémas avec la classe et la structure mises en surbrillance](../images/best-practices/profile-schema.png)

**Avantages**

* La segmentation est possible dans le cas d’utilisation prévu.
* Le schéma conserve uniquement les derniers enregistrements d’abonnement pour un client.

**Inconvénients**

* Le tableau entier doit être redémarré chaque fois que des modifications sont apportées à un champ du tableau.
* Si différentes sources de données ou unités opérationnelles alimentent le tableau en données, il devient difficile de garder le dernier tableau mis à jour synchronisé sur tous les canaux.

#### Approche 2 : utilisation des entités d’événement {#event-approach}

La deuxième approche consiste à utiliser des schémas d’événement pour représenter un événement d’abonnement. Cela inclut l’ID d’abonnement avec un ID de client et un horodatage du moment où l’événement d’abonnement s’est produit.

![Diagramme du schéma Événement d’abonnement avec la classe Événement d’expérience XDM et la structure d’abonnements mises en surbrillance.](../images/best-practices/event-schema.png)

**Avantages**

* Les règles de segmentation peuvent être plus flexibles (par exemple, la recherche de tous les clients qui ont modifié leurs abonnements au cours des 30 derniers jours).
* Lorsque le statut d’abonnement d’un client change, vous n’avez plus à mettre à jour un tableau long et potentiellement complexe dans les attributs de profil du client. Cela s’avère particulièrement utile si des modifications simultanées de la liste d’abonnements du client proviennent de plusieurs sources.

**Inconvénients**

* La segmentation devient plus complexe pour le cas d’utilisation original prévu (identification du statut des abonnements les plus récents des clients). L’audience a désormais besoin d’une logique supplémentaire pour indiquer le dernier événement d’abonnement pour qu’un client vérifie son statut.
* Les événements risquent davantage d’expirer automatiquement et d’être purgés de la banque de profils. Pour plus d’informations, consultez le guide sur les [expirations des événements d’expérience](../../profile/event-expirations.md).

## Créer des schémas en fonction de vos entités classées {#schemas-for-categorized-entities}

Une fois que vous avez trié vos entités en catégories de profil, de recherche et d’événement, vous pouvez commencer à convertir votre modèle de données en schémas XDM. À des fins de démonstration, l’exemple de modèle de données illustré précédemment a été trié en catégories appropriées dans le diagramme suivant :

![Diagramme des schémas contenus dans les entités de profil, de recherche et d’événement](../images/best-practices/erd-sorted.png)

La catégorie sous laquelle une entité a été triée doit déterminer la classe XDM sur laquelle baser son schéma. Réitération :

* Les entités de profil doivent utiliser la classe [!DNL XDM Individual Profile].
* Les entités d’événement doivent utiliser la classe [!DNL XDM ExperienceEvent].
* Les entités de recherche doivent utiliser des classes XDM personnalisées définies par votre organisation. Les entités de profil et d’événement peuvent ensuite référencer ces entités de recherche par le biais de relations de schéma.

>[!NOTE]
>
>Bien que les entités d’événement soient presque toujours représentées par des schémas distincts, les entités des catégories de profil ou de recherche peuvent être combinées dans un seul schéma XDM, selon leur cardinalité.
>
>Par exemple, l’entité Client ayant une relation un-à-un avec l’entité LoyaltyAccount, le schéma de l’entité Client peut également inclure un objet `LoyaltyAccount` pour contenir les champs de fidélité appropriés pour chaque client. Cependant, en cas de relation un-à-plusieurs, l’entité qui représente le « plusieurs » peut être représentée par un schéma distinct ou un tableau d’attributs de profil, selon sa complexité.

Les sections ci-dessous fournissent des conseils généraux sur la création de schémas basés sur votre ERD.

### Adopter une approche de modélisation itérative {#iterative-modeling}

Les [règles d’évolution des schémas](./composition.md#evolution) dictent que seules les modifications non destructives peuvent être apportées aux schémas une fois qu’ils ont été implémentés. En d’autres termes, une fois que vous avez ajouté un champ à un schéma et que les données ont été ingérées par rapport à ce champ, le champ ne peut plus être supprimé. Il est donc essentiel d’adopter une approche de modélisation itérative lorsque vous créez vos schémas pour la première fois, en commençant par une mise en oeuvre simplifiée qui gagne progressivement en complexité au fil du temps.

Si vous ne savez pas si un champ particulier est nécessaire pour l’inclure dans un schéma, la bonne pratique consiste à l’exclure. S’il est déterminé par la suite que le champ est nécessaire, il peut toujours être ajouté à l’itération suivante du schéma.

### Champs d’identité {#identity-fields}

Dans Experience Platform, les champs XDM marqués comme identités sont utilisés pour rassembler des informations sur les clients individuels provenant de plusieurs sources de données. Bien qu’un schéma puisse comporter plusieurs champs marqués comme identités, une seule identité principale doit être définie pour que le schéma soit activé pour une utilisation dans [!DNL Real-Time Customer Profile]. Voir la section sur les [champs d’identité](./composition.md#identity) dans les principes de base de la composition des schémas pour plus d’informations sur le cas d’utilisation de ces champs.

Lors de la conception de vos schémas, toute clé primaire dans vos tables de base de données relationnelle est probablement candidate pour des identités primaires. Les autres exemples de champs d’identité applicables sont les adresses électroniques du client, les numéros de téléphone, les ID de compte et les [ECID](../../identity-service/features/ecid.md).

### Groupes de champs de schéma d’application Adobe {#adobe-application-schema-field-groups}

Experience Platform fournit plusieurs groupes de champs de schéma XDM prêts à l’emploi pour la capture de données liées aux applications Adobe suivantes :

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Par exemple, vous pouvez utiliser le groupe de champs [[!UICONTROL Adobe Analytics ExperienceEvent Template] pour mapper &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) schémas XDM des champs spécifiques à [!DNL Analytics]. Selon les applications d’Adobe que vous utilisez, vous devez utiliser ces groupes de champs fournis par Adobe dans vos schémas.

![Schéma du [!UICONTROL Adobe Analytics ExperienceEvent Template].](../images/best-practices/analytics-field-group.png)

Les groupes de champs d’application Adobe attribuent automatiquement une identité principale par défaut grâce à l’utilisation du champ `identityMap`, qui est un objet généré par le système et en lecture seule qui mappe les valeurs d’identité standard pour un client individuel.

Pour Adobe Analytics, ECID est l’identité principale par défaut. Si une valeur ECID n’est pas fournie par un client, l’identité principale est définie par défaut sur AAID.

>[!IMPORTANT]
>
>Lors de l’utilisation de groupes de champs d’application Adobe, aucun autre champ ne doit être marqué comme identité principale. Si d’autres propriétés doivent être marquées comme identités, ces champs doivent être attribués en tant qu’identités secondaires à la place.

## Champs de validation des données {#data-validation-fields}

Lorsque vous ingérez des données dans le lac de données, la validation des données n’est appliquée que pour les champs limités. Pour valider un champ particulier lors de l’ingestion par lots, vous devez marquer le champ comme étant contraint dans le schéma XDM. Pour empêcher les données incorrectes d’entrer dans Experience Platform, définissez vos exigences de validation lors de la création de vos schémas.

>[!IMPORTANT]
>
>La validation ne s’applique pas aux colonnes imbriquées. Si le format du champ se trouve dans une colonne de tableau, les données ne sont pas validées.

Pour définir des contraintes sur un champ, sélectionnez le champ dans l’éditeur de schémas afin d’ouvrir la barre latérale **[!UICONTROL Field properties]**. Consultez la documentation sur les [propriétés de champ spécifiques à un type](../ui/fields/overview.md#type-specific-properties) pour obtenir une description exacte des champs disponibles.

![Éditeur de schémas avec les champs de contrainte mis en surbrillance dans la barre latérale [!UICONTROL Field properties].](../images/best-practices/data-validation-fields.png)

### Conseils pour maintenir l’intégrité des données {#data-integrity-tips}

Les suggestions suivantes vous aident à maintenir l’intégrité des données lors de la création d’un schéma.

* **Tenez compte des identités principales** : pour les produits Adobe tels que SDK web, Mobile SDK, Adobe Analytics et Adobe Journey Optimizer, le champ `identityMap` sert souvent d’identité principale. Évitez de désigner des champs supplémentaires en tant qu’identités principales pour ce schéma.
* **Assurez-vous que `_id` n’est pas utilisé comme identité** : le champ `_id` dans les schémas Événement d’expérience ne peut pas être utilisé comme identité, car il est destiné à l’unicité des enregistrements.
* **Définir des contraintes de longueur** : il est recommandé de définir des longueurs minimale et maximale sur les champs marqués comme identités. Un avertissement se déclenche si vous essayez d’attribuer un espace de noms personnalisé à un champ d’identité sans respecter les contraintes de longueur minimale et maximale. Ces limitations permettent de maintenir la cohérence et la qualité des données.
* **Appliquer des modèles pour des valeurs cohérentes** : si vos valeurs d’identité suivent un modèle spécifique, utilisez le paramètre **[!UICONTROL Pattern]** pour appliquer des contraintes. Ce paramètre peut inclure des règles telles que les chiffres uniquement, les majuscules ou les minuscules, ou des combinaisons de caractères spécifiques. Utilisez des expressions régulières pour faire correspondre des modèles dans vos chaînes.
* **Limiter les eVars dans les schémas Analytics** : en règle générale, un schéma Analytics ne doit comporter qu’une seule eVar désignée comme identité. Si vous envisagez d’utiliser plusieurs eVar en tant qu’identité, vous devez vérifier si la structure des données peut être optimisée.
* **Garantir l’unicité d’un champ sélectionné** : le champ sélectionné doit être unique par rapport à l’identité principale dans le schéma. Si ce n’est pas le cas, ne le marquez pas comme identité. Par exemple, si plusieurs clients peuvent fournir la même adresse e-mail, cet espace de noms n’est pas une identité appropriée. Ce principe s’applique également aux autres espaces de noms d’identité tels que les numéros de téléphone. Le marquage d’un champ non unique en tant qu’identité peut entraîner une réduction indésirable du profil.
* **Vérifier les longueurs de chaîne minimales** : tous les champs de chaîne doivent comporter au moins un caractère, car les valeurs de chaîne ne doivent jamais être vides. Les valeurs nulles pour les champs non obligatoires sont toutefois acceptables. Par défaut, les nouveaux champs de chaîne ont une longueur minimale d’un.

## Gestion des schémas activés pour Profile {#managing-profile-enabled-schemas}

Cette section explique comment gérer les schémas déjà activés pour le profil client en temps réel. Une fois qu’un schéma est activé, vous ne pouvez pas le désactiver ni le supprimer. Vous devez déterminer comment empêcher toute utilisation ultérieure et comment gérer les jeux de données que vous ne pouvez pas supprimer.

Une fois qu’un schéma est activé pour Profile, la configuration ne peut pas être inversée. Si un schéma ne doit plus être utilisé, renommez-le pour clarifier son statut et créer un schéma de remplacement avec la structure et la configuration d’identité correctes. Cela permet d’éviter la réutilisation accidentelle du schéma obsolète lorsque les utilisateurs créent de nouveaux jeux de données ou configurent des workflows d’ingestion.

Les jeux de données système apparaissent parfois avec les schémas activés pour Real-Time Customer Profile. Vous ne pouvez pas supprimer des jeux de données système, même si le schéma associé est obsolète. Pour éviter toute utilisation involontaire, renommez le schéma obsolète activé pour Profile et confirmez qu’aucun workflow d’ingestion ne pointe vers le jeu de données système qui reste en place.

Appliquez les bonnes pratiques suivantes pour éviter la réutilisation accidentelle de schémas activés pour Profile obsolètes :

* Utilisez une convention de nommage claire lorsque vous rendez un schéma obsolète. Incluez des libellés tels que « Obsolète », « Ne pas utiliser » ou une balise de version.
* Arrêtez d’ingérer des données dans un jeu de données en fonction du schéma que vous souhaitez supprimer.
* Créez un schéma avec la structure, la configuration d’identité et le modèle de dénomination corrects.
* Passez en revue les jeux de données système qui ne peuvent pas être supprimés et vérifiez qu’aucun workflow d’ingestion ne les référence.
* Documentez la modification en interne afin que d’autres utilisateurs comprennent pourquoi le schéma est obsolète.

>[!TIP]
>
>Consultez le [guide de dépannage XDM](../troubleshooting-guide.md#delete-profile-enabled) pour plus d’informations sur les schémas activés pour Profile et les limites associées.

## Étapes suivantes

Ce document présente les instructions générales et les bonnes pratiques pour la conception de votre modèle de données pour Experience Platform. Pour résumer :

* Triez vos tableaux de données en catégories de profil, de recherche et d’événement avant de créer vos schémas.
* Évaluez plusieurs approches lorsque vous concevez des schémas pour différents cas d’utilisation.
* Assurez-vous que votre modèle de données prend en charge votre segmentation ou les objectifs du parcours client.
* Veillez à ce que les schémas restent aussi simples que possible. Ajoutez de nouveaux champs uniquement lorsque cela est nécessaire.

Lorsque vous êtes prêt, consultez le tutoriel sur la [création d’un schéma dans l’interface utilisateur](../tutorials/create-schema-ui.md) pour obtenir des instructions détaillées sur la création de schémas, l’affectation de classe et le mappage de champs.
