---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;énumération;mixin;groupe de champs;groupes de champs;mixins;type de données;types de données;types de données;type de données;identité principale;profil individuel XDM;champs XDM;énumérer le type de données;événement d’expérience;événement d’expérience XDM;événement d’expérience XDM;événement d’expérience;événement d’expérience;événement d’événement d’expérience XDM;événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement d’événement Classe;classes;classes;type de données;type de données;type de données;type de données;schémas;schémas;identityMap;carte d’identité;carte d’identité;conception de schémas;carte;mappage;schéma d’union;union
solution: Experience Platform
title: Principes de base de la composition des schémas
description: Découvrez les schémas de modèle de données d’expérience (XDM) et les blocs de création, les principes et les bonnes pratiques pour la composition de schémas dans Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 595d9bd6a0aa0c9f1059e485c54e89ce02b7ec68
workflow-type: tm+mt
source-wordcount: '4365'
ht-degree: 26%

---

# Principes de base de la composition des schémas

Découvrez les schémas de modèle de données d’expérience (XDM) et les blocs de création, les principes et les bonnes pratiques pour la composition de schémas dans Adobe Experience Platform. Pour obtenir des informations générales sur XDM et son utilisation dans [!DNL Platform], consultez la [présentation du système XDM](../home.md).

## Compréhension des schémas {#understanding-schemas}

Un schéma est un jeu de règles qui représente et valide la structure et le format des données. À un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (comme le prénom, le nom, l’anniversaire, etc.).

Outre la description de la structure des données, les schémas appliquent des contraintes et des attentes aux données de manière à ce qu’elles puissent être validées lorsqu’elles sont déplacées d’un système à l’autre. Ces définitions standard permettent d’interpréter les données de manière cohérente, quelle que soit leur origine, et éliminent la nécessité d’une traduction entre les applications.

Experience Platform conserve cette normalisation sémantique à l’aide de schémas. Les schémas sont la manière standard de décrire les données dans Experience Platform. Ils permettent à toutes les données conformes aux schémas d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations.

Les schémas XDM sont idéaux pour stocker de grandes quantités de données complexes dans un format autonome. Pour plus d’informations sur la façon dont XDM effectue cette opération, reportez-vous aux sections relatives aux [objets incorporés](#embedded) et aux [données massives](#big-data) de l’annexe de ce document.

### Workflows basés sur des schémas dans Experience Platform {#schema-based-workflows}

La normalisation est un concept clé d’Experience Platform. XDM, piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas standard pour la gestion de l’expérience client.

L’infrastructure sur laquelle l’Experience Platform est créé, appelée [!DNL XDM System], facilite les workflows basés sur des schémas et inclut les [!DNL Schema Registry], [!DNL Schema Editor], les métadonnées de schéma et les modèles de consommation de service. Pour plus d’informations, consultez la [présentation du système XDM](../home.md).

L’utilisation des schémas dans Experience Platform présente plusieurs avantages clés. Tout d’abord, les schémas permettent une meilleure gouvernance des données et une réduction au minimum des données, ce qui est particulièrement important avec les réglementations de confidentialité. Ensuite, la création de schémas avec les composants standard d’Adobe permet d’obtenir des informations d’usine et d’utiliser les services AI/ML avec un minimum de personnalisations. Enfin, les schémas fournissent une infrastructure pour le partage de données et une orchestration efficace.

## Planification de votre schéma {#planning}

La première étape de la conception d’un schéma consiste à déterminer le concept ou l’objet dans le monde réel que vous essayez de capturer au sein du schéma. Une fois que vous avez identifié le concept que vous essayez de décrire, commencez à planifier votre schéma en réfléchissant à des éléments tels que le type de données, les champs d’identité potentiels et la manière dont le schéma pourrait évoluer à l’avenir.

### Comportements de données dans Experience Platform {#data-behaviors}

Les données pouvant être utilisées dans Experience Platform sont regroupées selon deux types de comportements :

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de série temporelle** : fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM sont décrites en détail par la suite dans ce document.

Les schémas d’enregistrement et de série temporelle contiennent tous deux une carte des identités (`xdm:identityMap`). Ce champ contient la représentation de l’identité d’un objet tiré des champs marqués comme « Identité » décrit à la section suivante.

### [!UICONTROL Identité] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identités dans les schémas"
>abstract="Les identités sont des champs clés d&#39;un schéma pouvant être utilisés pour identifier un objet, comme une adresse e-mail ou un identifiant marketing. Ces champs sont utilisés pour créer le graphique d&#39;identité de chaque individu ainsi que les profils client. Pour plus d&#39;informations sur les identités dans les schémas, consultez la documentation."

Les schémas sont utilisés pour ingérer des données dans Experience Platform. Ces données sont finalement utilisées par plusieurs services pour créer une vue unique et unifiée d’une entité individuelle. Il est donc important, lors de la conception de schémas pour les identités client, de prendre en compte les champs qui peuvent être utilisés pour identifier un sujet, quel que soit l’origine des données.

Pour faciliter ce processus, les champs clés de vos schémas peuvent être marqués comme identités. Lors de l’ingestion des données, les données de ces champs sont insérées dans le &quot;[!UICONTROL graphique d’identités]&quot; de cette personne. Les données du graphique peuvent ensuite être consultées par [[!DNL Real-Time Customer Profile]](../../profile/home.md) et d’autres services Experience Platform afin de fournir une vue d’ensemble de chaque client.

Les champs généralement marqués comme &quot;[!UICONTROL Identité]&quot; sont les suivants : adresse électronique, numéro de téléphone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr), identifiant CRM ou autres champs d’identification uniques. Tenez compte de tous les identifiants uniques propres à votre organisation, car ils peuvent également représenter de bons champs &quot;[!UICONTROL Identité]&quot;.

Il est important de réfléchir aux identités client au cours de la phase de planification du schéma afin de vous assurer que les données sont rassemblées pour créer le profil le plus robuste possible. Pour en savoir plus sur la manière dont les informations d’identité peuvent vous aider à fournir des expériences numériques à vos clients, consultez la [présentation d’Identity Service](../../identity-service/home.md). Consultez le document des bonnes pratiques de modélisation des données pour obtenir [ conseils sur l’utilisation des identités lors de la création d’un schéma](./best-practices.md#data-validation-fields).

Il existe deux manières d’envoyer des données d’identité à Platform :

1. Ajout de descripteurs d’identité à des champs individuels, soit par l’[interface utilisateur de l’éditeur de schémas](../ui/fields/identity.md), soit à l’aide de l’ [ API Schema Registry](../api/descriptors.md#create)
1. Utilisation d’un champ [`identityMap`](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` est un champ de type map qui décrit les différentes valeurs d’identité d’un individu, ainsi que les espaces de noms qui lui sont associés. Ce champ peut être utilisé pour fournir des informations d’identité pour vos schémas, au lieu de définir des valeurs d’identité dans la structure du schéma lui-même.

L’inconvénient principal de l’utilisation de `identityMap` est que les identités sont incorporées dans les données et deviennent par conséquent moins visibles. Si vous ingérez des données brutes, vous devez définir des champs d’identité individuels dans la structure réelle du schéma à la place.

>[!NOTE]
>
>Un schéma qui utilise `identityMap` peut être utilisé comme schéma source dans une relation, mais ne peut pas être utilisé comme schéma de référence. Cela est dû au fait que tous les schémas de référence doivent avoir une identité visible qui peut être mappée dans un champ de référence dans le schéma source. Pour plus d’informations sur les exigences des schémas source et de référence, consultez le guide de l’interface utilisateur sur les [relations](../tutorials/relationship-ui.md) .

Cependant, les mappages d’identité peuvent s’avérer utiles s’il existe un nombre variable d’identités pour un schéma, ou si vous ramenez des données provenant de sources qui stockent les identités ensemble (telles que [!DNL Airship] ou Adobe Audience Manager). En outre, les mappages d’identité sont requis si vous utilisez le [SDK Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/home/).

Voici un exemple de carte d’identité simple :

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
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
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

Comme l’exemple ci-dessus le montre, chaque clé de l’objet `identityMap` représente un espace de noms d’identité. La valeur de chaque clé est un tableau d’objets, représentant les valeurs d’identité (`id`) pour l’espace de noms respectif. Reportez-vous à la documentation [!DNL Identity Service] pour obtenir la [ liste des espaces de noms d’identité standard ](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconnus par les applications Adobe.

>[!NOTE]
>
>Une valeur boolean indiquant si la valeur est une identité principale (`primary`) peut également être fournie pour chaque valeur d’identité. Il vous suffit de définir les identités primaires pour les schémas destinés à être utilisés dans [!DNL Real-Time Customer Profile]. Pour plus d’informations, consultez la section sur les [schémas d’union](#union) .

### Principes d’évolution des schémas {#evolution}

Étant donné que la nature des expériences digitales continue à évoluer, les schémas utilisés pour les représenter le doivent aussi. Un schéma bien conçu est donc capable de s’adapter et d’évoluer si nécessaire sans provoquer des modifications destructives aux versions précédentes du schéma.

Le maintien de la compatibilité descendante étant essentiel pour l’évolution du schéma, Experience Platform applique un principe de contrôle de version purement additif. Ce principe garantit que toute révision du schéma n’entraîne que des mises à jour et des modifications non destructives. En d’autres termes, **les modifications entraînant des ruptures ne sont pas prises en charge.**

>[!NOTE]
>
>Vous ne pouvez introduire une modification entraînant une rupture dans un schéma que s’il n’a pas encore été utilisé pour ingérer des données dans Experience Platform et qu’il n’a pas été activé pour une utilisation dans Real-time Customer Profile. Cependant, une fois que le schéma a été utilisé dans [!DNL Platform], il doit respecter la politique de contrôle de version additif.

Le tableau suivant répertorie les modifications prises en charge lors de la modification des schémas, des groupes de champs et des types de données :

| Modifications prises en charge | Modifications entraînant une rupture (non prises en charge) |
| --- | --- |
| <ul><li>Ajouter de nouveaux champs à la ressource</li><li>Rendre un champ obligatoire facultatif</li><li>Présentation des nouveaux champs obligatoires*</li><li>Modification du nom d’affichage et de la description de la ressource</li><li>Activation du schéma pour participer à Profile</li></ul> | <ul><li>Supprimer des champs définis précédemment</li><li>Renommer ou redéfinir des champs existants</li><li>Supprimer ou limiter des valeurs de champ précédemment prises en charge</li><li>Déplacement de champs existants vers un autre emplacement de l’arborescence</li><li>Suppression du schéma</li><li>Désactivation de la participation du schéma dans Profile</li></ul> |

\**Reportez-vous à la section ci-dessous pour des considérations importantes concernant la [définition de nouveaux champs obligatoires](#post-ingestion-required-fields).*

### Champs obligatoires

Les champs de schéma individuels peuvent être [marqués comme obligatoires](../ui/fields/required.md), ce qui signifie que tout enregistrement ingéré doit contenir des données dans ces champs pour passer la validation. Par exemple, la définition du champ d’identité principal d’un schéma selon les besoins peut vous aider à vous assurer que tous les enregistrements ingérés participeront à Real-time Customer Profile. De même, la définition d’un champ d’horodatage selon les besoins garantit que tous les événements de série temporelle sont préservés chronologiquement.

>[!IMPORTANT]
>
>Qu’un champ de schéma soit obligatoire ou non, Platform n’accepte pas `null` ou les valeurs vides pour un champ ingéré. S’il n’existe aucune valeur pour un champ particulier dans un enregistrement ou un événement, la clé de ce champ doit être exclue de la charge utile d’ingestion.

#### Définition des champs requis après l’ingestion {#post-ingestion-required-fields}

Si un champ a été utilisé pour ingérer des données et qu’il n’a pas été initialement défini comme requis, il peut avoir une valeur nulle pour certains enregistrements. Si vous définissez ce champ comme étant obligatoire après l’ingestion, tous les enregistrements ultérieurs doivent contenir une valeur pour ce champ, même si les enregistrements historiques peuvent être nuls.

Lorsque vous définissez un champ précédemment facultatif selon les besoins, gardez à l’esprit les points suivants :

1. Si vous interrogez des données historiques et écrivez les résultats dans un nouveau jeu de données, certaines lignes échouent car elles contiennent des valeurs nulles pour le champ requis.
1. Si le champ participe à [Real-time Customer Profile](../../profile/home.md) et que vous exportez des données avant de les définir selon les besoins, il peut être nul pour certains profils.
1. Vous pouvez utiliser l’API Schema Registry pour afficher un journal des modifications horodaté pour toutes les ressources XDM dans Platform, y compris les nouveaux champs obligatoires. Pour plus d’informations, consultez le guide sur le [point d’entrée du journal d’audit](../api/audit-log.md) .

### Schémas et ingestion de données

Pour ingérer des données dans Experience Platform, vous devez d’abord créer un jeu de données. Les jeux de données sont les blocs de construction de la transformation et du suivi des données pour [[!DNL Catalog Service]](../../catalog/home.md) et représentent généralement des tableaux ou des fichiers qui contiennent des données ingérées. Tous les jeux de données sont basés sur des schémas XDM existants qui fournissent des contraintes sur ce que les données ingérées doivent contenir et sur la manière dont elles doivent être structurées. Pour plus d’informations, consultez la présentation d’[Adobe Experience Platform Data Ingestion](../../ingestion/home.md).

## Blocs de création d’un schéma {#schema-building-blocks}

Experience Platform utilise une approche de composition dans laquelle des blocs de création standard sont associés pour créer des schémas. Cette approche favorise la réutilisation des composants existants et entraîne la normalisation dans l’ensemble du secteur pour prendre en charge les schémas et composants fournisseurs dans [!DNL Platform].

Les schémas sont composés à l’aide de la formule suivante :

**Classe + Groupe de champs de schéma&amp;ast; = Schéma XDM**

&amp;ast;Un schéma est composé d’une classe et de zéro ou plusieurs groupes de champs de schéma. Cela signifie que vous pouvez composer un schéma de jeu de données sans utiliser de groupes de champs.

### Classe {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Classe"
>abstract="Chaque schéma est basé sur une seule classe. La classe définit le comportement du schéma et les propriétés communes que tous les schémas basés sur cette classe doivent avoir. Pour plus d&#39;informations sur l&#39;implication des classes dans la composition des schémas, consultez la documentation."

>[!CONTEXTUALHELP]
>id="platform_schemas_class_industries"
>title="Type de secteur"
>abstract="Si vous sélectionnez un secteur industriel pertinent pour votre entreprise, le modèle de machine learning peut fournir une meilleure organisation des données en mappant plus précisément les champs source avec les groupes de champs standard conformes aux normes du secteur. Cela permet de s’assurer que l’intégration des données est adaptée aux besoins spécifiques de votre secteur d’activité et donne lieu à des informations plus précises et plus pertinentes."

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrement ou série temporelle). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

La classe d’un schéma détermine les groupes de champs pouvant être utilisés dans ce schéma. Ceci est abordé plus en détail dans la [prochaine section](#field-group).

Adobe fournit plusieurs classes XDM standard (&quot;core&quot;). Deux de ces classes, [!DNL XDM Individual Profile] et [!DNL XDM ExperienceEvent], sont requises pour la plupart des processus Platform en aval. En plus de ces classes de base, vous pouvez créer vos propres classes personnalisées afin de décrire des cas d’utilisation plus spécifiques à votre organisation. Les classes personnalisées sont définies par une organisation lorsqu’aucune classe principale définie par l’Adobe n’est disponible pour décrire un cas d’utilisation unique.

La capture d’écran suivante montre comment les classes sont représentées dans l’interface utilisateur de Platform. Comme l’exemple de schéma présenté ne contient aucun groupe de champs, tous les champs affichés sont fournis par la classe du schéma ([!UICONTROL XDM Individual Profile]).

![ [!UICONTROL XDM Individual Profile] dans l’éditeur de schémas.](../images/schema-composition/class.png)

Pour obtenir la liste la plus récente des classes XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/classes). Vous pouvez également vous reporter au guide sur l’ [exploration des composants XDM](../ui/explore.md) si vous préférez afficher des ressources dans l’interface utilisateur.

### Groupe de champs {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Groupe de champs"
>abstract="Les groupes de champs sont des composants réutilisables qui vous permettent d&#39;étendre les schémas avec des attributs supplémentaires. La plupart des groupes de champs ne sont compatibles qu&#39;avec certaines classes. Vous pouvez utiliser des groupes de champs standard définis par Adobe ou définir manuellement vos propres groupes de champs personnalisés. Pour plus d&#39;informations sur l&#39;implication des groupes de champs dans la composition des schémas, consultez la documentation."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Groupe de champs requis"
>abstract="Ce groupe de champs est requis par la source que vous utilisez. Vous ne pouvez donc pas le supprimer de votre schéma."

Un groupe de champs est un composant réutilisable qui définit un ou plusieurs champs qui implémentent certaines fonctions telles que les détails personnels, les préférences d’hôtel ou l’adresse. Les groupes de champs sont destinés à être inclus dans le cadre d’un schéma qui met en oeuvre une classe compatible.

Les groupes de champs définissent la ou les classes avec lesquelles ils sont compatibles, en fonction du comportement des données qu’ils représentent (enregistrement ou série temporelle). Cela signifie que tous les groupes de champs ne sont pas disponibles pour toutes les classes.

Experience Platform inclut de nombreux groupes de champs d’Adobe standard tout en permettant aux fournisseurs de définir des groupes de champs pour leurs utilisateurs et aux utilisateurs individuels de définir des groupes de champs pour leurs propres concepts spécifiques.

Par exemple, pour capturer des détails tels que &quot;[!UICONTROL Prénom]&quot; et &quot;[!UICONTROL Adresse du domicile]&quot; pour votre schéma &quot;[!UICONTROL Loyalty Members]&quot;, vous pouvez utiliser des groupes de champs standard qui définissent ces concepts communs. Toutefois, les concepts plus spécifiques à votre organisation (tels que les détails du programme de fidélité personnalisés ou les attributs de produit) qui peuvent ne pas être couverts par les groupes de champs standard. Dans ce cas, vous devez définir votre propre groupe de champs pour capturer ces informations.

>[!NOTE]
>
>Il est vivement recommandé d’utiliser des groupes de champs standard chaque fois que cela est possible dans vos schémas, car ces champs sont implicitement compris par les services Experience Platform et offrent une plus grande cohérence lorsqu’ils sont utilisés sur l’ensemble des composants [!DNL Platform].
>
>Les champs fournis par les composants standard (tels que &quot;Prénom&quot; et &quot;Adresse électronique&quot;) contiennent des connotations ajoutées au-delà des types de champs scalaires de base. Ils indiquent à [!DNL Platform] que tous les champs partageant le même type de données se comportent de la même manière. Ce comportement peut être considéré comme cohérent, quel que soit l’endroit d’où proviennent les données ou le service [!DNL Platform] dans lequel les données sont utilisées.

N’oubliez pas que les schémas sont composés de groupes de champs &quot;zéro ou plus&quot;, ce qui signifie que vous pouvez composer un schéma valide sans utiliser aucun groupe de champs.

La capture d’écran suivante montre comment les groupes de champs sont représentés dans l’interface utilisateur de Platform. Un seul groupe de champs ([!UICONTROL Détails démographiques]) est ajouté à un schéma dans cet exemple, qui fournit un regroupement de champs à la structure du schéma.

![L’éditeur de schémas avec le groupe de champs [!UICONTROL Détails démographiques] mis en surbrillance dans un exemple de schéma.](../images/schema-composition/field-group.png)

Pour obtenir la liste la plus récente des groupes de champs XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Vous pouvez également vous reporter au guide sur l’ [exploration des composants XDM](../ui/explore.md) si vous préférez afficher des ressources dans l’interface utilisateur.

>[!NOTE]
>
> Les groupes de champs XDM standard évoluent toujours et certains groupes de champs ont été abandonnés. Pour obtenir la liste des groupes de champs obsolètes la plus récente, reportez-vous à la [section des groupes de champs obsolètes](https://github.com/adobe/xdm/tree/master/components/fieldgroups/deprecated) du référentiel XDM officiel.

### Type de données {#data-type}

Les types de données sont utilisés comme types de champ de référence dans des classes ou des schémas de la même manière que des champs littéraux de base. La principale différence réside dans le fait que les types de données peuvent définir plusieurs sous-champs de la même manière que les groupes de champs. La principale différence entre eux est que les types de données peuvent être inclus n’importe où dans un schéma en l’ajoutant comme &quot;type de données&quot; d’un champ. Bien que les groupes de champs ne soient compatibles qu’avec certaines classes, les types de données peuvent être inclus dans n’importe quelle classe parent ou groupe de champs.

>[!NOTE]
>
>Si un champ est défini comme un type de données spécifique, vous ne pouvez pas créer le même champ avec un type de données différent dans un autre schéma. Cette contrainte s’applique à l’ensemble du client de votre entreprise.

Experience Platform fournit un certain nombre de types de données courants dans le cadre de [!DNL Schema Registry] pour prendre en charge l’utilisation de modèles standard pour la description de structures de données communes. Ceci est expliqué plus en détail dans les [tutoriels du registre des schémas](../tutorials/create-schema-api.md) et devient plus clair lorsque vous parcourez les étapes de définition des types de données.

La capture d’écran suivante montre comment les types de données sont représentés dans l’interface utilisateur de Platform. L’un des champs fournis par le groupe de champs [!UICONTROL Demographic Details] utilise le type de données &quot;[!UICONTROL Object]&quot;, comme indiqué par le texte suivant la barre verticale (`|`) en regard du nom du champ. Ce type de données particulier fournit plusieurs sous-champs relatifs au nom d’une personne, un concept qui peut être réutilisé pour d’autres champs où le nom d’une personne doit être capturé.

![Diagramme de l’éditeur de schémas pour une personne individuelle avec l’objet Nom complet et les attributs mis en surbrillance.](../images/schema-composition/data-type.png)

Pour obtenir la liste la plus récente des types de données XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/datatypes). Vous pouvez également vous reporter au guide sur l’ [exploration des composants XDM](../ui/explore.md) si vous préférez afficher des ressources dans l’interface utilisateur.

>[!NOTE]
>
> Les types de données XDM standard évoluent toujours et certains types de données ont été abandonnés. Pour obtenir la liste des types de données obsolètes la plus récente, reportez-vous à la [section sur les types de données obsolètes](https://github.com/adobe/xdm/tree/master/components/datatypes/deprecated) du référentiel XDM officiel.

### Champ {#field}

Un champ est le bloc de création le plus basique d’un schéma. Les champs fournissent des contraintes concernant le type de données qu’ils peuvent contenir en définissant un type de données spécifique. Ces types de données de base définissent un champ unique, tandis que les [types de données](#data-type) mentionnés précédemment vous permettent de définir plusieurs sous-champs et de réutiliser la même structure à champs multiples sur différents schémas. Donc, en plus de définir le « type de données » d’un champ comme l’un des types de données défini dans le registre, Experience Platform prend en charge des types scalaires de base comme :

* Chaîne
* Entier
* Double
* Booléen
* Tableau
* Objet

>[!TIP]
>
>Pour plus d’informations sur les avantages et les inconvénients de l’utilisation de champs de forme libre par rapport aux champs de type objet, reportez-vous à l’ [annexe](#objects-v-freeform) .

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
>Le type de champ &quot;map&quot; permet des données de paires clé-valeur, y compris plusieurs valeurs pour une clé unique. Les mappages se trouvent dans les classes XDM standard et les groupes de champs, mais vous pouvez également définir des mappages personnalisés. Pour plus d’informations, consultez le tutoriel de l’API sur la [ définition des champs de mappage personnalisés](../tutorials/custom-fields-api.md#custom-maps) ou le guide sur la [ définition des champs de mappage dans l’interface utilisateur](../ui/fields/map.md).

## Exemple de composition {#composition-example}

Les schémas sont créés à l’aide d’un modèle de composition et représentent le format et la structure des données à ingérer dans [!DNL Platform]. Comme mentionné précédemment, ces schémas sont composés d’une classe et de zéro ou plusieurs groupes de champs compatibles avec cette classe.

Par exemple, un schéma décrivant les achats effectués dans un magasin de détail peut être appelé &quot;[!UICONTROL Transactions de magasin]&quot;. Le schéma met en oeuvre la classe [!DNL XDM ExperienceEvent] associée au groupe de champs [!UICONTROL Commerce] standard et à un groupe de champs [!UICONTROL Informations sur le produit] défini par l’utilisateur.

Un autre schéma qui suit le trafic du site web peut être appelé &quot;[!UICONTROL Visites web]&quot;. Il met également en oeuvre la classe [!DNL XDM ExperienceEvent], mais cette fois-ci combine le groupe de champs [!UICONTROL Web] standard.

Le diagramme ci-dessous montre ces schémas et les champs fournis par chaque groupe de champs. Il contient également deux schémas basés sur la classe [!DNL XDM Individual Profile], y compris le schéma &quot;[!UICONTROL Loyalty Members]&quot; mentionné précédemment dans ce guide.

![Schéma de flux de quatre schémas et groupes de champs qui y contribuent.](../images/schema-composition/composition.png)

### Union {#union}

Experience Platform vous permet non seulement de composer des schémas pour des cas d’utilisation spécifiques, mais aussi de voir une « union » des schémas pour un type de classe spécifique. Le diagramme précédent présente deux schémas basés sur la classe XDM ExperienceEvent et deux schémas basés sur la classe [!DNL XDM Individual Profile]. L’union, illustrée ci-dessous, agrège les champs de tous les schémas qui partagent la même classe ([!DNL XDM ExperienceEvent] et [!DNL XDM Individual Profile], respectivement).

![Schéma de flux de schéma d’union qui représente les champs qui les composent.](../images/schema-composition/union.png)

En activant un schéma à utiliser avec [!DNL Real-Time Customer Profile], il est inclus dans l’union pour ce type de classe. [!DNL Profile] fournit des profils robustes et centralisés des attributs du client ainsi qu’un compte horodaté de chaque événement que le client a eu dans n’importe quel système intégré à [!DNL Platform]. [!DNL Profile] utilise la vue d’union pour représenter ces données et fournir une vue holistique de chaque client individuel.

Pour plus d’informations sur l’utilisation de [!DNL Profile], consultez la [présentation de Real-Time Customer Profile](../../profile/home.md).

## Mappage des fichiers de données à des schémas XDM {#mapping-datafiles}

Tous les fichiers de données ingérés dans Experience Platform doivent être conformes à la structure d’un schéma XDM. Pour plus d’informations sur la manière de formater les fichiers de données pour se conformer aux hiérarchies XDM (ainsi que des fichiers d’exemple), consultez le document sur les [exemples de transformations ETL](../../etl/transformations.md). Pour obtenir des informations générales sur l’ingestion de fichiers de données dans Experience Platform, consultez la [présentation de l’ingestion par lots](../../ingestion/batch-ingestion/overview.md).

## Schémas pour les audiences externes

Si vous intégrez des audiences provenant de systèmes externes dans Platform, vous devez utiliser les composants suivants pour les capturer dans vos schémas :

* [[!UICONTROL Définition de segment] class](../classes/segment-definition.md) : utilisez cette classe standard pour capturer les attributs clés d’une définition de segment externe.
* [[!UICONTROL Détails de l’appartenance à un segment] groupe de champs](../field-groups/profile/segmentation.md) : ajoutez ce groupe de champs à votre schéma [!UICONTROL XDM Individual Profile] pour associer des profils client à des audiences spécifiques.

## Étapes suivantes

Maintenant que vous comprenez les principes de base de la composition des schémas, vous êtes prêt à commencer à explorer et à créer des schémas à l’aide de [!DNL Schema Registry].

Pour examiner la structure des deux classes XDM principales et de leurs groupes de champs compatibles couramment utilisés, consultez la documentation de référence suivante :

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry] est utilisé pour accéder à [!DNL Schema Library] dans Adobe Experience Platform et fournit une interface utilisateur et une API RESTful à partir desquelles toutes les ressources de bibliothèque disponibles sont accessibles. [!DNL Schema Library] contient des ressources du secteur définies par l’Adobe, des ressources du fournisseur définies par des partenaires Experience Platform, ainsi que des classes, des groupes de champs, des types de données et des schémas composés par des membres de votre organisation.

Pour commencer à composer un schéma à l’aide de l’interface utilisateur, suivez le [tutoriel de l’éditeur de schémas](../tutorials/create-schema-ui.md) pour créer le schéma « Loyalty Members » mentionné tout au long de ce document.

Pour commencer à utiliser l’API [!DNL Schema Registry], commencez par lire le [guide de développement de l’API Schema Registry](../api/getting-started.md). Après avoir lu le guide de développement, suivez les étapes décrites dans le tutoriel [Création d’un schéma à l’aide de l’API Schema Registry](../tutorials/create-schema-api.md).

## Annexe

Les sections suivantes contiennent des informations supplémentaires sur les principes de la composition des schémas.

### Tableaux relationnels et objets intégrés {#embedded}

Lorsque vous travaillez avec des bases de données relationnelles, les bonnes pratiques consistent à normaliser les données ou à prendre une entité et à la diviser en éléments individuels qui sont ensuite affichés sur plusieurs tableaux. Pour lire les données dans leur ensemble ou mettre à jour l’entité, les opérations de lecture et d’écriture doivent être effectuées sur de nombreuses tables individuelles à l’aide de la fonction JOIN.

En utilisant des objets intégrés, les schémas XDM peuvent représenter directement des données complexes et les stocker dans des documents autonomes avec une structure hiérarchique. L’un des principaux avantages de cette structure est qu’elle vous permet d’interroger les données sans avoir à reconstruire l’entité par des jointures onéreuses sur plusieurs tables dénormalisées. Il n’existe aucune restriction stricte quant au nombre de niveaux pouvant être autorisés dans votre hiérarchie de schémas.

### Schémas et Big Data {#big-data}

Les systèmes numériques modernes génèrent une grande quantité de signaux comportementaux (données de transaction, journaux web, Internet des objets, affichage, etc.). Le Big Data offre des opportunités extraordinaires d’optimiser des expériences, mais les utiliser représente un véritable défi en raison de leur échelle et de la diversité des données. Pour tirer parti des données, la structure, le format et les définitions de ces données doivent être normalisés afin qu’elles puissent être traitées de manière cohérente et efficace.

Les schémas permettent de résoudre ce problème en permettant l’intégration des données à partir de diverses sources, l’uniformisation au moyen de structures et de définitions communes et le partage entre les solutions. Cela permet aux processus et services suivants de répondre à tout type de question posée sur les données. Il s’éloigne de l’approche traditionnelle de la modélisation des données où toutes les questions à poser sur les données sont connues à l’avance et les données sont modélisées pour se conformer à ces attentes.

### Objets et champs de forme libre {#objects-v-freeform}

Lors de la conception de vos schémas, vous devez tenir compte de certains facteurs clés lors du choix d’objets plutôt que de champs de forme libre :

| Objets | Champs de forme libre |
| --- | --- |
| Augmente l’imbrication | Imbrication ou non d’imbrication |
| Crée des regroupements de champs logiques | Les champs sont placés à des emplacements ad hoc. |

{style="table-layout:auto"}

#### Objets

Les avantages et inconvénients de l’utilisation d’objets sur des champs de forme libre sont répertoriés ci-dessous.

**Pros** :

* Il est préférable d’utiliser les objets lorsque vous souhaitez créer un regroupement logique de certains champs.
* Les objets organisent le schéma de manière plus structurée.
* Les objets aident indirectement à créer une bonne structure de menus dans l’interface utilisateur du créateur de segments. Les champs regroupés dans le schéma sont directement reflétés dans la structure de dossiers fournie dans l’interface utilisateur du créateur de segments.

**Cons** :

* Les champs deviennent plus imbriqués.
* Lors de l’utilisation de [Adobe Experience Platform Query Service](../../query-service/home.md), des chaînes de référence plus longues doivent être fournies aux champs de requête imbriqués dans des objets.

#### Champs de forme libre

Les avantages et inconvénients de l’utilisation de champs de forme libre par rapport aux objets sont répertoriés ci-dessous.

**Pros** :

* Les champs de forme libre sont créés directement sous l’objet racine du schéma (`_tenantId`), ce qui augmente la visibilité.
* Les chaînes de référence pour les champs de forme libre ont tendance à être plus courtes lors de l’utilisation de Query Service.

**Cons** :

* L’emplacement des champs de forme libre dans le schéma est ad hoc, ce qui signifie qu’ils apparaissent dans l’ordre alphabétique dans l’éditeur de schémas. Cela peut rendre les schémas moins structurés, et des champs de forme libre similaires peuvent se révéler très séparés en fonction de leurs noms.
