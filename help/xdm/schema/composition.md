---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;énumération;mixin;groupe de champs;groupes de champs;mixins;type de données;types de données;types de données;type de données;identité Principale;profil individuel XDM;champs XDM;énumérer le type de données;événement d’expérience;événement d’expérience XDM;événement d’expérience XDM;événement d’expérience;événement d’expérience;événement d’expérience;événement d’expérience classe;classe;classes;classes;classe;type de données;type de données;type de données;type de données;schémas;schémas;identityMap;carte d’identité;carte d’identité;conception de schéma;carte;carte;schéma d’union;union
solution: Experience Platform
title: Principes de base de la composition des schémas
topic-legacy: overview
description: Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques de la composition de schémas à utiliser dans Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '3726'
ht-degree: 32%

---

# Principes de base de la composition des schémas

Ce document présente les schémas [!DNL Experience Data Model] (XDM) ainsi que les blocs de création, les principes et les bonnes pratiques pour la composition de schémas à utiliser dans Adobe Experience Platform. Pour obtenir des informations générales sur XDM et son utilisation dans [!DNL Platform], consultez la [présentation du système XDM](../home.md).

## Compréhension des schémas

Un schéma est un jeu de règles qui représente et valide la structure et le format des données. À un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (comme le prénom, le nom, l’anniversaire, etc.).

Outre la description de la structure des données, les schémas appliquent des contraintes et des attentes aux données de manière à ce qu’elles puissent être validées lorsqu’elles sont déplacées d’un système à l’autre. Ces définitions standard permettent d’interpréter les données de manière cohérente, quelle que soit leur origine, et éliminent la nécessité d’une traduction entre les applications.

[!DNL Experience Platform] conserve cette normalisation sémantique à l’aide de schémas. Les schémas sont la manière standard de décrire les données dans [!DNL Experience Platform], ce qui permet à toutes les données conformes aux schémas d’être réutilisées dans une organisation sans conflit, voire partagées entre plusieurs organisations.

Les schémas XDM sont idéaux pour stocker de grandes quantités de données complexes dans un format autonome. Pour plus d’informations sur la manière dont XDM effectue cette opération, reportez-vous aux sections [objet incorporé](#embedded) et [Big Data](#big-data) de l’annexe du présent document.

### Workflows basés sur des schémas dans [!DNL Experience Platform]

La normalisation est un concept clé de [!DNL Experience Platform]. XDM, piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas standard pour la gestion de l’expérience client.

L’infrastructure sur laquelle [!DNL Experience Platform] est construit, appelée [!DNL XDM System], facilite les workflows basés sur des schémas et inclut les [!DNL Schema Registry], [!DNL Schema Editor], les métadonnées de schéma et les modèles de consommation de service. Pour plus d’informations, consultez la [présentation du système XDM](../home.md).

L’utilisation des schémas dans [!DNL Experience Platform] présente plusieurs avantages clés. First, schemas allow for better data governance and data minimization, which is especially important with privacy regulations. Ensuite, la création de schémas avec les composants standard d’Adobe permet d’obtenir des informations d’usine et d’utiliser les services AI/ML avec un minimum de personnalisations. Enfin, les schémas fournissent une infrastructure pour le partage de données et une orchestration efficace.

## Planification de votre schéma

La première étape de la conception d’un schéma consiste à déterminer le concept ou l’objet dans le monde réel que vous essayez de capturer au sein du schéma. Une fois que vous avez identifié le concept que vous essayez de décrire, vous pouvez commencer à planifier votre schéma en réfléchissant à des éléments comme le type de données, les champs d’identité potentiels et la manière dont le schéma peut évoluer dans le futur.

### Comportements de données dans [!DNL Experience Platform]

Data intended for use in [!DNL Experience Platform] is grouped into two behavior types:

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de série temporelle** : fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM sont décrites en détail par la suite dans ce document.

Les schémas d’enregistrement et de série temporelle contiennent tous deux une carte des identités (`xdm:identityMap`). Ce champ contient la représentation de l’identité d’un sujet tiré des champs marqués comme « Identité » décrit à la section suivante.

### [!UICONTROL Identité] {#identity}

Les schémas sont utilisés pour ingérer des données dans [!DNL Experience Platform]. Ces données sont finalement utilisées par plusieurs services pour créer une vue unique et unifiée d’une entité individuelle. Il est donc important, lors de la réflexion sur les schémas, de réfléchir aux identités des clients et aux champs qui peuvent être utilisés pour identifier un sujet, quel que soit l’origine des données.

Pour faciliter ce processus, les champs clés de vos schémas peuvent être marqués comme identités. Lors de l’ingestion des données, les données de ces champs sont insérées dans le &quot;[!UICONTROL graphique d’identités]&quot; de cette personne. Les données du graphique peuvent ensuite être consultées par [[!DNL Real-time Customer Profile]](../../profile/home.md) et d’autres services [!DNL Experience Platform] afin de fournir une vue d’ensemble de chaque client.

Les champs généralement marqués comme &quot;[!UICONTROL Identité]&quot; incluent : adresse électronique, numéro de téléphone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr), identifiant CRM ou d’autres champs d’identifiant uniques. Vous devez également tenir compte de tous les identifiants uniques propres à votre organisation, car ils peuvent également représenter de bons champs &quot;[!UICONTROL Identité]&quot;.

Il est important de réfléchir aux identités client lors de la phase de planification du schéma afin de vous assurer que les données sont rassemblées pour créer le profil le plus robuste possible. Consultez la présentation de [Adobe Experience Platform Identity Service](../../identity-service/home.md) pour en savoir plus sur la manière dont les informations d’identité peuvent vous aider à fournir des expériences numériques à vos clients.

Il existe deux manières d’envoyer des données d’identité à Platform :

1. Ajout de descripteurs d’identité à des champs individuels, soit par l’intermédiaire de l’[interface utilisateur de l’éditeur de schémas](../ui/fields/identity.md), soit à l’aide de l’[API Schema Registry](../api/descriptors.md#create)
1. Using an [`identityMap` field](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` is a map-type field that describes the various identity values for an individual, along with their associated namespaces. Ce champ peut être utilisé pour fournir des informations d’identité pour vos schémas, au lieu de définir des valeurs d’identité dans la structure du schéma lui-même.

The main drawback of using `identityMap` is that identities become embedded in the data and become less visible as a result. Si vous ingérez des données brutes, vous devez définir des champs d’identité individuels dans la structure réelle du schéma à la place. Les schémas qui utilisent `identityMap` ne peuvent pas non plus participer aux relations.

Cependant, les mappages d’identité peuvent s’avérer particulièrement utiles si vous rentrez des données provenant de sources qui stockent les identités ensemble (comme [!DNL Airship] ou Adobe Audience Manager), ou s’il existe un nombre variable d’identités pour un schéma. En outre, les mappages d’identité sont requis si vous utilisez le [SDK Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/).

Voici un exemple de carte d’identité simple :

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Comme l’exemple ci-dessus le montre, chaque clé de l’objet `identityMap` représente un espace de noms d’identité. La valeur de chaque clé est un tableau d’objets, représentant les valeurs d’identité (`id`) pour l’espace de noms respectif. Consultez la [!DNL Identity Service] documentation pour obtenir la [liste des espaces de noms d’identité standard](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconnus par les applications Adobe.

>[!NOTE]
>
>Une valeur booléenne indique si la valeur est une identité Principale (`primary`) peut également être fournie pour chaque valeur d’identité. Les identités Principal ne doivent être définies que pour les schémas destinés à être utilisés dans [!DNL Real-time Customer Profile]. Pour plus d’informations, consultez la section [schémas d’union](#union) .

### Principes d’évolution des schémas {#evolution}

Étant donné que la nature des expériences numériques continue à évoluer, les schémas utilisés pour les représenter le doivent aussi. Un schéma bien conçu est donc capable de s’adapter et d’évoluer si nécessaire sans provoquer des modifications destructives aux versions précédentes du schéma.

Le maintien de la compatibilité descendante étant essentiel pour l’évolution du schéma, [!DNL Experience Platform] applique un principe de contrôle de version purement additif. Ce principe garantit que toute révision du schéma n’entraîne que des mises à jour et des modifications non destructives. En d’autres termes, **les modifications entraînant des ruptures ne sont pas prises en charge.**

>[!NOTE]
>
>Si un schéma n’a pas encore été utilisé pour ingérer des données dans [!DNL Experience Platform] et n’a pas été activé pour une utilisation dans Real-time Customer Profile, vous pouvez introduire une modification entraînant une rupture dans ce schéma. Cependant, une fois que le schéma a été utilisé dans [!DNL Platform], il doit respecter la politique de contrôle de version additif.

Le tableau suivant répertorie les modifications prises en charge lors de la modification des schémas, des groupes de champs et des types de données :

| Modifications prises en charge | Modifications entraînant une rupture (non prises en charge) |
| --- | --- |
| <ul><li>Adding new fields to the resource</li><li>Rendre un champ obligatoire facultatif</li><li>Modification du nom d’affichage et de la description de la ressource</li><li>Activation du schéma pour participer à Profile</li></ul> | <ul><li>Supprimer des champs définis précédemment</li><li>Introduire de nouveaux champs obligatoires</li><li>Renommer ou redéfinir des champs existants</li><li>Supprimer ou limiter des valeurs de champ précédemment prises en charge</li><li>Déplacement de champs existants vers un autre emplacement de l’arborescence</li><li>Suppression du schéma</li><li>Désactivation de la participation du schéma dans Profile</li></ul> |

### Schémas et ingestion de données

In order to ingest data into [!DNL Experience Platform], a dataset must first be created. Les jeux de données sont les blocs de construction de la transformation et du suivi des données pour [[!DNL Catalog Service]](../../catalog/home.md) et représentent généralement des tableaux ou des fichiers qui contiennent des données ingérées. Tous les jeux de données sont basés sur des schémas XDM existants qui fournissent des contraintes sur ce que les données ingérées doivent contenir et sur la manière dont elles doivent être structurées. Pour plus d’informations, consultez la présentation d’[Adobe Experience Platform Data Ingestion](../../ingestion/home.md).

## Blocs de création d’un schéma

[!DNL Experience Platform] utilise une approche de composition dans laquelle des blocs de création standard sont associés pour créer des schémas. Cette approche favorise la réutilisation de composants existants et conditionne la normalisation dans le secteur pour soutenir les schémas et les composants fournisseurs dans [!DNL Platform].

Les schémas sont composés à l’aide de la formule suivante :

**Class + Schema Field Group&amp;ast; = XDM Schema**

&amp;ast;A schema is composed of a class and zero or more schema field groups. Cela signifie que vous pouvez composer un schéma de jeu de données sans utiliser de groupes de champs.

### Classe {#class}

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

A schema&#39;s class determines which field groups will be eligible for use in that schema. Ceci est discuté plus en détail dans la [section suivante](#field-group).

Adobe fournit plusieurs classes XDM standard (&quot;core&quot;). Deux de ces classes, [!DNL XDM Individual Profile] et [!DNL XDM ExperienceEvent], sont requises pour la plupart des processus Platform en aval. Outre ces classes principales, vous pouvez également créer vos propres classes personnalisées afin de décrire des cas d’utilisation plus spécifiques à votre organisation. Les classes personnalisées sont définies par une organisation lorsqu’aucune classe principale définie par l’Adobe n’est disponible pour décrire un cas d’utilisation unique.

La capture d’écran suivante montre comment les classes sont représentées dans l’interface utilisateur de Platform. Comme l’exemple de schéma présenté ne contient aucun groupe de champs, tous les champs affichés sont fournis par la classe du schéma ([!UICONTROL XDM Individual Profile]).

![](../images/schema-composition/class.png)

Pour obtenir la liste la plus récente des classes XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/classes). Vous pouvez également vous reporter au guide sur l’[exploration des composants XDM](../ui/explore.md) si vous préférez afficher les ressources dans l’interface utilisateur.

### Groupe de champs {#field-group}

Un groupe de champs est un composant réutilisable qui définit un ou plusieurs champs qui implémentent certaines fonctions telles que les détails personnels, les préférences d’hôtel ou l’adresse. Les groupes de champs sont destinés à être inclus dans le cadre d’un schéma qui met en oeuvre une classe compatible.

Les groupes de champs définissent la ou les classes avec lesquelles ils sont compatibles en fonction du comportement des données qu’ils représentent (enregistrement ou série temporelle). Cela signifie que tous les groupes de champs ne sont pas disponibles pour toutes les classes.

[!DNL Experience Platform] inclut de nombreux groupes de champs d’Adobe standard tout en permettant aux fournisseurs de définir des groupes de champs pour leurs utilisateurs et aux utilisateurs individuels de définir des groupes de champs pour leurs propres concepts spécifiques.

For example, to capture details such as &quot;[!UICONTROL First Name]&quot; and &quot;[!UICONTROL Home Address]&quot; for your &quot;[!UICONTROL Loyalty Members]&quot; schema, you would be able to use standard field groups that define those common concepts. Cependant, les concepts spécifiques à des cas d’utilisation moins courants (tels que &quot;[!UICONTROL Loyalty Program Level]&quot;) ne comportent souvent pas de groupe de champs prédéfini. Dans ce cas, vous devez définir votre propre groupe de champs pour capturer ces informations.

Remember that schemas are composed of &quot;zero or more&quot; field groups, so this means that you could compose a valid schema without using any field groups at all.

La capture d’écran suivante montre comment les groupes de champs sont représentés dans l’interface utilisateur de Platform. Un seul groupe de champs ([!UICONTROL Détails démographiques]) est ajouté à un schéma dans cet exemple, qui fournit un regroupement de champs à la structure du schéma.

![](../images/schema-composition/field-group.png)

For the most up-to-date list of available standard XDM field groups, refer to the [official XDM repository](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Alternatively, you can refer to the guide on [exploring XDM components](../ui/explore.md) if you prefer to view resources in the UI.

### Type de données {#data-type}

Les types de données sont utilisés comme types de champ de référence dans des classes ou des schémas de la même manière que des champs littéraux de base. La principale différence réside dans le fait que les types de données peuvent définir plusieurs sous-champs. Tout comme un groupe de champs, un type de données permet l’utilisation cohérente d’une structure à plusieurs champs, mais offre plus de flexibilité qu’un groupe de champs, car un type de données peut être inclus n’importe où dans un schéma en l’ajoutant en tant que &quot;type de données&quot; d’un champ.

[!DNL Experience Platform] fournit un certain nombre de types de données courants dans le  [!DNL Schema Registry] pour prendre en charge l’utilisation de modèles standard pour décrire des structures de données communes. Ceci est expliqué plus en détail dans les tutoriels [!DNL Schema Registry], où il devient plus clair lorsque vous parcourez les étapes de définition des types de données.

La capture d’écran suivante montre comment les types de données sont représentés dans l’interface utilisateur de Platform. L’un des champs fournis par le groupe de champs [!UICONTROL Détails démographiques] utilise le type de données &quot;[!UICONTROL Nom de personne]&quot;, comme indiqué par le texte qui suit la barre verticale (`|`) en regard du nom du champ. Ce type de données particulier fournit plusieurs sous-champs relatifs au nom d’une personne, un concept qui peut être réutilisé pour d’autres champs où le nom d’une personne doit être capturé.

![](../images/schema-composition/data-type.png)

Pour obtenir la liste la plus récente des types de données XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/datatypes). Vous pouvez également vous reporter au guide sur l’[exploration des composants XDM](../ui/explore.md) si vous préférez afficher les ressources dans l’interface utilisateur.

### Champ

Un champ est le bloc de création le plus basique d’un schéma. Les champs apportent des contraintes concernant le type de données qu’ils peuvent contenir en définissant un type de données spécifique. Ces types de données de base définissent un champ unique, tandis que les [types de données](#data-type) mentionnés précédemment vous permettent de définir plusieurs sous-champs et de réutiliser la même structure à champs multiples sur plusieurs schémas. Ainsi, en plus de définir le &quot;type de données&quot; d’un champ comme l’un des types de données définis dans le registre, [!DNL Experience Platform] prend en charge les types scalaires de base tels que :

* Chaîne
* Entier
* Double
* Booléen
* Tableau
* Objet

>[!TIP]
>
>Voir l’ [annexe](#objects-v-freeform) pour plus d’informations sur les avantages et les inconvénients de l’utilisation de champs de forme libre par rapport aux champs de type objet.

Les plages valides de ces types scalaires peuvent être limitées davantage à certains motifs, formats, minimums/maximums ou valeurs prédéfinies. Grâce à ces contraintes, il est possible de représenter une large plage de types de champ spécifiques, notamment :

* Enum
* Long
* Short
* Byte
* Date
* Date-time
* Map

>[!NOTE]
>
>Le type de champ « map » permet des données de paires clé-valeur, y compris plusieurs valeurs pour une clé unique. Les cartes ne peuvent être définies qu’au niveau du système, ce qui signifie que vous pouvez rencontrer une carte dans un schéma de secteur ou de fournisseur, mais celle-ci ne peut pas être utilisée dans les champs que vous définissez. Le [guide de développement de l’API Schema Registry](../api/getting-started.md) contient plus d’informations sur la définition des types de champ.

Certaines opérations de données utilisées par des services et des applications en aval imposent des contraintes sur certains types de champs. Les services concernés incluent, sans s’y limiter :

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Avant de créer un schéma à utiliser dans les services en aval, veuillez consulter la documentation appropriée de ces services afin de mieux comprendre les exigences et les contraintes de champ pour les opérations de données auxquelles le schéma est destiné.

### Champs XDM

En plus des champs de base et de la possibilité de définir vos propres types de données, XDM fournit un ensemble standard de champs et de types de données qui sont implicitement compris par les services [!DNL Experience Platform] et fournissent une plus grande cohérence lorsqu’ils sont utilisés dans les composants [!DNL Platform].

Ces champs, tels que &quot;Prénom&quot; et &quot;Adresse électronique&quot;, contiennent des connotations ajoutées au-delà des types de champs scalaires de base, indiquant à [!DNL Platform] que tous les champs partageant le même type de données XDM se comportent de la même manière. Ce comportement peut être considéré comme cohérent, quel que soit l’endroit d’où proviennent les données ou le service [!DNL Platform] dans lequel les données sont utilisées.

Consultez le [dictionnaire des champs XDM](field-dictionary.md) pour obtenir une liste complète des champs XDM disponibles. Nous vous recommandons d’utiliser les champs XDM et les types de données dès que possible pour aider à la cohérence et à la standardisation dans [!DNL Experience Platform].

## Exemple de composition

Les schémas représentent le format et la structure des données qui seront ingérés dans [!DNL Platform] et qui sont créés à l’aide d’un modèle de composition. As previously mentioned, these schemas are composed of a class and zero or more field groups that are compatible with that class.

Par exemple, un schéma décrivant les achats effectués dans un magasin de détail peut être appelé &quot;[!UICONTROL Transactions de magasin]&quot;. Le schéma met en oeuvre la classe [!DNL XDM ExperienceEvent] associée au groupe de champs standard [!UICONTROL Commerce] et un groupe de champs [!UICONTROL Informations sur le produit] défini par l’utilisateur.

Another schema which tracks website traffic might be called &quot;[!UICONTROL Web Visits]&quot;. Il met également en oeuvre la classe [!DNL XDM ExperienceEvent], mais combine cette fois le groupe de champs [!UICONTROL Web] standard.

The diagram below shows these schemas and the fields contributed by each field group. Il contient également deux schémas basés sur la classe [!DNL XDM Individual Profile], y compris le schéma &quot;[!UICONTROL Loyalty Members]&quot; mentionné précédemment dans ce guide.

![](../images/schema-composition/composition.png)

### Union {#union}

Bien que [!DNL Experience Platform] vous permette de composer des schémas pour des cas d’utilisation particuliers, il permet également d’afficher une &quot;union&quot; de schémas pour un type de classe spécifique. Le diagramme précédent présente deux schémas basés sur la classe XDM ExperienceEvent et deux schémas basés sur la classe [!DNL XDM Individual Profile]. L’union, illustrée ci-dessous, regroupe les champs de tous les schémas qui partagent la même classe ([!DNL XDM ExperienceEvent] et [!DNL XDM Individual Profile], respectivement).

![](../images/schema-composition/union.png)

En activant un schéma à utiliser avec [!DNL Real-time Customer Profile], il sera inclus dans l’union pour ce type de classe. [!DNL Profile] fournit des profils robustes et centralisés des attributs du client ainsi qu’un compte horodaté de chaque événement que le client a eu sur n’importe quel système intégré à  [!DNL Platform]. [!DNL Profile] utilise la vue d’union pour représenter ces données et fournir une vue d’ensemble de chaque client.

Pour plus d’informations sur l’utilisation de [!DNL Profile], consultez la [présentation de Real-time Customer Profile](../../profile/home.md).

## Mappage des fichiers de données à des schémas XDM

Tous les fichiers de données ingérés dans [!DNL Experience Platform] doivent être conformes à la structure d’un schéma XDM. Pour plus d’informations sur la manière de formater les fichiers de données pour se conformer aux hiérarchies XDM (ainsi que des fichiers d’exemple), consultez le document sur les [exemples de transformations ETL](../../etl/transformations.md). Pour obtenir des informations générales sur l’ingestion de fichiers de données dans [!DNL Experience Platform], consultez la [présentation de l’ingestion par lots](../../ingestion/batch-ingestion/overview.md).

## Schémas pour les segments externes

Si vous intégrez des segments provenant de systèmes externes dans Platform, vous devez utiliser les composants suivants pour les capturer dans vos schémas :

* [[!UICONTROL Segment definition] class](../classes/segment-definition.md): Use this standard class to capture key attributes of an external segment definition.
* [[!UICONTROL Groupe de champs ] Détails de l’appartenance au segment](../field-groups/profile/segmentation.md) : Ajoutez ce groupe de champs à votre schéma  [!UICONTROL de profils individuels ] XDM afin d’associer des profils client à des segments spécifiques.

## Étapes suivantes

Now that you understand the basics of schema composition, you are ready to begin exploring and building schemas using the [!DNL Schema Registry].

Pour examiner la structure des deux classes XDM principales et de leurs groupes de champs compatibles couramment utilisés, consultez la documentation de référence suivante :

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

The [!DNL Schema Registry] is used to access the [!DNL Schema Library] within Adobe Experience Platform, and provides a user interface and RESTful API from which all available library resources are accessible. [!DNL Schema Library] contient les ressources du secteur définies par l’Adobe, les ressources du fournisseur définies par les partenaires [!DNL Experience Platform], ainsi que les classes, les groupes de champs, les types de données et les schémas composés par des membres de votre organisation.

Pour commencer à composer un schéma à l’aide de l’interface utilisateur, suivez le [tutoriel de l’éditeur de schémas](../tutorials/create-schema-ui.md) pour créer le schéma « Loyalty Members » mentionné tout au long de ce document.

Pour commencer à utiliser l’API [!DNL Schema Registry], commencez par lire le [guide de développement de l’API Schema Registry](../api/getting-started.md). Après avoir lu le guide de développement, suivez les étapes décrites dans le tutoriel [Création d’un schéma à l’aide de l’API Schema Registry](../tutorials/create-schema-api.md).

## Annexe

Les sections suivantes contiennent des informations supplémentaires sur les principes de la composition des schémas.

### Tableaux relationnels et objets intégrés {#embedded}

Lorsque vous travaillez avec des bases de données relationnelles, les bonnes pratiques consistent à normaliser les données ou à prendre une entité et à la diviser en éléments individuels qui sont ensuite affichés sur plusieurs tableaux. Pour pouvoir lire les données dans leur ensemble ou mettre à jour l’entité, des opérations de lecture et d’écriture doivent être effectuées sur plusieurs tableaux individuels à l’aide de la fonction REJOINDRE.

Grâce aux objets intégrés, les schémas XDM peuvent représenter directement des données complexes et les stocker dans des documents autonomes avec une structure hiérarchique. L’un des principaux avantages de cette structure est qu’elle vous permet d’effectuer des requêtes sur des données sans avoir à reconstruire l’entité par des liaisons onéreuses sur plusieurs tableaux dénormalisés. There are no hard restrictions to how many levels your schema hierarchy can be.

### Schémas et Big Data {#big-data}

Les systèmes numériques modernes génèrent une grande quantité de signaux comportementaux (données de transaction, journaux web, Internet des objets, affichage, etc.). Le Big Data offre des opportunités extraordinaires d’optimiser des expériences, mais les utiliser représente un véritable défi en raison de leur échelle et de la diversité des données. Pour tirer parti des données, vous devez normaliser leur structure, leur format et leurs définitions afin de les traiter de manière cohérente et efficace.

Les schémas permettent de résoudre ce problème en permettant l’intégration des données à partir de diverses sources, l’uniformisation au moyen de structures et de définitions communes et le partage entre les solutions. Cela permet aux processus et aux services suivants de répondre à tout type de questions posées sur les données, en s’éloignant de l’approche traditionnelle de la modélisation des données dans laquelle toutes les questions posées sur les données sont connues à l’avance et les données sont modélisées pour être conformes à ces attentes.

### Objets et champs de forme libre {#objects-v-freeform}

Lors de la conception de vos schémas, vous devez tenir compte de certains facteurs clés lors du choix d’objets plutôt que de champs de forme libre :

| Objets | Champs de forme libre |
| --- | --- |
| Augmente l’imbrication | Imbrication ou non d’imbrication |
| Crée des regroupements de champs logiques | Les champs sont placés à des emplacements ad hoc. |

{style=&quot;table-layout:auto&quot;}

#### Objets

Les avantages et inconvénients de l’utilisation d’objets sur des champs de forme libre sont répertoriés ci-dessous.

**Avantages** :

* Il est préférable d’utiliser les objets lorsque vous souhaitez créer un regroupement logique de certains champs.
* Les objets organisent le schéma de manière plus structurée.
* Les objets aident indirectement à créer une bonne structure de menus dans l’interface utilisateur du créateur de segments. Les champs regroupés dans le schéma sont directement reflétés dans la structure de dossiers fournie dans l’interface utilisateur du créateur de segments.

**Inconvénients** :

* Les champs deviennent plus imbriqués.
* Lors de l’utilisation de [Adobe Experience Platform Query Service](../../query-service/home.md), des chaînes de référence plus longues doivent être fournies pour interroger les champs imbriqués dans des objets.

#### Champs de forme libre

Les avantages et inconvénients de l’utilisation de champs de forme libre par rapport aux objets sont répertoriés ci-dessous.

**Pros**:

* Free-form fields are created directly under the root object of the schema (`_tenantId`), increasing visibility.
* Les chaînes de référence pour les champs de forme libre ont tendance à être plus courtes lors de l’utilisation de Query Service.

**Inconvénients** :

* L’emplacement des champs de forme libre dans le schéma est ad hoc, ce qui signifie qu’ils apparaissent dans l’ordre alphabétique dans l’éditeur de schémas. Cela peut rendre les schémas moins structurés, et des champs de forme libre similaires peuvent se révéler très séparés en fonction de leurs noms.
