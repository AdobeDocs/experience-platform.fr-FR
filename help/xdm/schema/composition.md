---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;Schéma;énumération;mixin;Groupe de champs;Groupes de champs;mixins;type de données;types de données;type de données;identité principale;identité principale;profil individuel XDM;champs XDM;type de données d’énumération;Événement d’expérience;Événement d’expérience XDM;ExperienceEvent XDM;experienceEvent;experienceevent;conception de schéma;classe;classe;classes;classes;type de données;Type de données;Type de données;Type de données;Schémas;Schémas;identityMap;mappage d’identités;Mappage d’identités;conception de schéma;mappage;mappage;mappage;union schéma;union
solution: Experience Platform
title: Principes de base de la composition des schémas
description: Découvrez les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques pour la composition de schémas dans Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 5b59d491834854829a89a240ccd612367cf558d4
workflow-type: tm+mt
source-wordcount: '4291'
ht-degree: 24%

---

# Principes de base de la composition des schémas

Découvrez les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques pour la composition de schémas dans Adobe Experience Platform. Pour obtenir des informations générales sur XDM et son utilisation dans Experience Platform, consultez la [&#x200B; présentation du système XDM &#x200B;](../home.md).

## Compréhension des schémas {#understanding-schemas}

Un schéma est un jeu de règles qui représente et valide la structure et le format des données. À un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (comme le prénom, le nom, l’anniversaire, etc.).

Outre la description de la structure des données, les schémas appliquent des contraintes et des attentes aux données de manière à ce qu’elles puissent être validées lorsqu’elles sont déplacées d’un système à l’autre. Ces définitions standard permettent d’interpréter les données de manière cohérente, quelle que soit leur origine, et éliminent la nécessité d’une traduction entre les applications.

Experience Platform maintient cette normalisation sémantique à l’aide de schémas. Les schémas sont la manière standard de décrire les données dans Experience Platform. Ils permettent à toutes les données conformes aux schémas d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations.

Les schémas XDM sont parfaits pour stocker de grandes quantités de données complexes dans un format autonome. Pour plus d’informations sur les [objets incorporés](#embedded) et [données volumineuses](#big-data) de XDM, reportez-vous aux sections de l’annexe de ce document.

### Workflows basés sur des schémas dans Experience Platform {#schema-based-workflows}

La normalisation est un concept clé d’Experience Platform. XDM, piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas standard pour la gestion de l’expérience client.

L’infrastructure sur laquelle Experience Platform est conçu, connue sous le nom de [!DNL XDM System], facilite les workflows basés sur des schémas et inclut les modèles de [!DNL Schema Registry], de [!DNL Schema Editor], de métadonnées de schéma et de consommation de services. Pour plus d’informations, consultez la [présentation du système XDM](../home.md).

L’utilisation de schémas dans Experience Platform présente plusieurs avantages majeurs. Tout d’abord, les schémas permettent une meilleure gouvernance des données et une minimisation des données, ce qui est particulièrement important avec les réglementations de confidentialité. Ensuite, la création de schémas avec des composants standard d’Adobe permet d’obtenir des informations prêtes à l’emploi et d’utiliser des services d’IA/ML avec un minimum de personnalisations. Enfin, les schémas fournissent une infrastructure pour le partage d’informations sur les données et une orchestration efficace.

## Planification de votre schéma {#planning}

La première étape de la conception d’un schéma consiste à déterminer le concept ou l’objet dans le monde réel que vous essayez de capturer au sein du schéma. Une fois que vous avez identifié le concept que vous essayez de décrire, commencez à planifier votre schéma en réfléchissant à des éléments tels que le type de données, les champs d’identité potentiels et la manière dont le schéma peut évoluer dans le futur.

### Comportements de données dans Experience Platform {#data-behaviors}

Les données pouvant être utilisées dans Experience Platform sont regroupées selon deux types de comportements :

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de série temporelle** : fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un objet d’enregistrement.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à ce dernier lors de sa création initiale.

Les schémas d’enregistrement et de série temporelle contiennent tous deux une carte des identités (`xdm:identityMap`). Ce champ contient la représentation de l’identité d’un objet tiré des champs marqués comme « Identité » décrit à la section suivante.

### [!UICONTROL Identity] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identités dans les schémas"
>abstract="Les identités sont des champs clés d&#39;un schéma pouvant être utilisés pour identifier un objet, comme une adresse e-mail ou un identifiant marketing. Ces champs sont utilisés pour créer le graphique d&#39;identité de chaque individu ainsi que les profils client. Pour plus d&#39;informations sur les identités dans les schémas, consultez la documentation."

Les schémas définissent la structure des données ingérées dans Experience Platform. Ces données alimentent plusieurs services au sein de Platform et permettent de créer une vue unique et unifiée de chaque individu. Ainsi, lors de la conception de schémas, réfléchissez soigneusement aux champs à marquer comme identités, car ils contrôlent la manière dont les profils sont regroupés dans les jeux de données.

Pour faciliter ce processus, les champs clés de vos schémas peuvent être marqués comme identités. Lors de l’ingestion des données, les données de ces champs sont insérées dans le « [!UICONTROL Identity Graph] » de cet individu. Les données du graphique peuvent ensuite être consultées par [[!DNL Real-Time Customer Profile]](../../profile/home.md) et d’autres services Experience Platform afin de fournir une vue d’ensemble de chaque client individuel.

Les champs généralement désignés comme champs « [!UICONTROL Identity] » sont les suivants : adresse e-mail, numéro de téléphone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr), identifiant CRM ou d’autres champs d’identification uniques. Tenez compte des identifiants uniques spécifiques à votre organisation, car il peut également s’agir de bons champs « [!UICONTROL Identity] ».

Pour en savoir plus sur la manière dont les informations d’identité peuvent vous aider à proposer des expériences digitales à vos clients, consultez la [&#x200B; présentation d’Identity Service](../../identity-service/home.md). Consultez le document des bonnes pratiques de modélisation des données pour obtenir des [&#x200B; sur l’utilisation des identités lors de la création d’un schéma](./best-practices.md#data-validation-fields).

Il existe deux manières d’envoyer des données d’identité à Experience Platform :

1. Ajouter des descripteurs d’identité à des champs individuels, par le biais de l’interface utilisateur [Éditeur de schémas](../ui/fields/identity.md) ou à l’aide de l’API [Schema Registry](../api/descriptors.md#create)
2. En utilisant un champ de [`identityMap`](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` est un champ de type map qui décrit les différentes valeurs d’identité d’un individu, ainsi que les espaces de noms qui lui sont associés. Ce champ peut être utilisé pour fournir des informations d’identité à vos schémas, au lieu de définir des valeurs d’identité dans la structure du schéma lui-même.

L’inconvénient principal de l’utilisation de `identityMap` est que les valeurs d’identité sont imbriquées et peuvent être plus difficiles à utiliser dans les outils qui prévoient des champs d’identité de niveau supérieur, tels que le créateur de segments ou certaines intégrations tierces.

>[!NOTE]
>
>Un schéma qui utilise `identityMap` peut être utilisé comme schéma source dans une relation, mais ne peut pas être utilisé comme schéma de référence. En effet, tous les schémas de référence doivent avoir une identité visible qui peut être mappée dans un champ de référence au sein du schéma source. Reportez-vous au guide de l’interface utilisateur sur [les relations](../tutorials/relationship-ui.md) pour plus d’informations sur les exigences des schémas source et de référence.

Cependant, les mappages d’identités peuvent s’avérer utiles s’il existe un nombre variable d’identités pour un schéma ou si vous importez des données provenant de sources qui stockent des identités ensemble (telles que [!DNL Airship] ou Adobe Audience Manager). En outre, des mappages d’identité sont requis si vous utilisez [Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/).

Voici un exemple de mappage d’identités simple :

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

Comme le montre l’exemple ci-dessus, chaque clé de l’objet `identityMap` représente un espace de noms d’identité. La valeur de chaque clé est un tableau d’objets représentant les valeurs d’identité (`id`) de l’espace de noms correspondant. Reportez-vous à la documentation [!DNL Identity Service] pour obtenir une [&#x200B; liste des espaces de noms d’identité standard](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconnus par les applications Adobe.

>[!NOTE]
>
>Une valeur booléenne indiquant si la valeur est une identité principale (`primary`) peut également être fournie pour chaque valeur d’identité. Il vous suffit de définir des identités principales pour les schémas destinés à être utilisés dans [!DNL Real-Time Customer Profile].

### Principes d’évolution des schémas {#evolution}

Étant donné que la nature des expériences digitales continue à évoluer, les schémas utilisés pour les représenter le doivent aussi. Un schéma bien conçu est donc capable de s’adapter et d’évoluer si nécessaire sans provoquer des modifications destructives aux versions précédentes du schéma.

Le maintien de la rétrocompatibilité étant essentiel à l’évolution des schémas, Experience Platform applique un principe de contrôle des versions purement additif. Ce principe garantit que toute révision du schéma n’entraîne que des mises à jour et des modifications non destructives. En d’autres termes, **les modifications entraînant des ruptures ne sont pas prises en charge.**

>[!NOTE]
>
>Vous ne pouvez introduire une modification avec rupture dans un schéma que s’il n’a pas encore été utilisé pour ingérer des données dans Experience Platform et n’a pas été activé pour une utilisation dans le profil client en temps réel. Cependant, une fois le schéma utilisé dans Experience Platform, il doit respecter la politique de contrôle de version additif.

Le tableau suivant détaille les modifications prises en charge lors de la modification de schémas, de groupes de champs et de types de données :

| Modifications prises en charge | Modifications entraînant une rupture (non prises en charge) |
| --- | --- |
| <ul><li>Ajouter de nouveaux champs à la ressource</li><li>Rendre un champ obligatoire facultatif</li><li>Introduction de nouveaux champs obligatoires*</li><li>Modification du nom d’affichage et de la description de la ressource</li><li>Activation du schéma pour participer au profil</li></ul> | <ul><li>Supprimer des champs définis précédemment</li><li>Renommer ou redéfinir des champs existants</li><li>Supprimer ou limiter des valeurs de champ précédemment prises en charge</li><li>Déplacement de champs existants vers un autre emplacement de l’arborescence</li><li>Suppression du schéma</li><li>Désactivation du schéma de la participation au profil</li><li>Modification du champ d’identité principale sur un schéma activé pour Profil et contenant des données ingérées</li></ul> |

\**Reportez-vous à la section ci-dessous pour des considérations importantes concernant [la définition de nouveaux champs obligatoires](#post-ingestion-required-fields).*

### Champs obligatoires

Les champs de schéma individuels peuvent être [marqués comme requis](../ui/fields/required.md), ce qui signifie que tous les enregistrements ingérés doivent contenir des données dans ces champs pour passer la validation. Par exemple, la définition, si nécessaire, du champ d’identité principale d’un schéma peut garantir que tous les enregistrements ingérés participeront au profil client en temps réel. De même, la définition d’un champ d’horodatage selon les besoins garantit que tous les événements de série temporelle sont conservés chronologiquement.

>[!IMPORTANT]
>
>Qu’un champ de schéma soit obligatoire ou non, Experience Platform n’accepte pas les valeurs `null` ou vides pour les champs ingérés. S’il n’existe aucune valeur pour un champ particulier dans un enregistrement ou un événement, la clé de ce champ doit être exclue de la payload d’ingestion.

#### Définition des champs selon les besoins après l’ingestion {#post-ingestion-required-fields}

Si un champ a été utilisé pour ingérer des données et n’a pas été défini à l’origine comme requis, ce champ peut avoir une valeur nulle pour certains enregistrements. Si vous définissez ce champ comme obligatoire après l’ingestion, tous les enregistrements futurs doivent contenir une valeur pour ce champ, même si les enregistrements historiques peuvent être nuls.

Lorsque vous définissez un champ précédemment facultatif selon les besoins, tenez compte des points suivants :

1. Si vous interrogez des données historiques et que vous écrivez les résultats dans un nouveau jeu de données, certaines lignes échoueront, car elles contiennent des valeurs nulles pour le champ obligatoire.
1. Si le champ participe au profil client en temps réel et que vous exportez des données avant de le définir selon les besoins, il peut être nul pour certains profils.
1. Vous pouvez utiliser l’API Schema Registry pour afficher un journal des modifications horodaté pour toutes les ressources XDM d’Experience Platform, y compris les nouveaux champs obligatoires. Pour plus d’informations, consultez le guide sur le point d’entrée [journal d’audit](../api/audit-log.md).

### Schémas et ingestion de données

Pour ingérer des données dans Experience Platform, vous devez d’abord créer un jeu de données. Les jeux de données sont les blocs de création de la transformation des données et du suivi des [[!DNL Catalog Service]](../../catalog/home.md). Ils représentent généralement des tables ou des fichiers contenant des données ingérées. Tous les jeux de données sont basés sur des schémas XDM existants qui fournissent des contraintes sur ce que les données ingérées doivent contenir et sur la manière dont elles doivent être structurées. Pour plus d’informations, consultez la présentation d’[Experience Platform Data Ingestion](../../ingestion/home.md).

## Blocs de création d’un schéma {#schema-building-blocks}

Experience Platform utilise une approche de composition dans laquelle des blocs de création standard sont associés pour créer des schémas. Cette approche favorise la réutilisation des composants existants et stimule la normalisation dans l’ensemble du secteur afin de prendre en charge les schémas de fournisseur et les composants dans Experience Platform.

Les schémas sont composés à l’aide de la formule suivante :

**Classe + Groupe de champs de schéma&ast; = Schéma XDM**

&ast;Un schéma est composé d’une classe et de zéro ou de plusieurs groupes de champs de schéma. Cela signifie que vous pouvez composer un schéma de jeu de données sans utiliser de groupes de champs.

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

La classe d’un schéma détermine les groupes de champs éligibles à l’utilisation dans ce schéma.

Adobe fournit plusieurs classes XDM standard (« principales »). Deux de ces classes, [!DNL XDM Individual Profile] et [!DNL XDM ExperienceEvent], sont requises pour presque tous les processus Experience Platform en aval. Outre ces classes principales, vous pouvez également créer vos propres classes personnalisées pour décrire des cas d’utilisation plus spécifiques pour votre organisation. Les classes personnalisées sont définies par une organisation lorsqu’aucune classe principale définie par Adobe n’est disponible pour décrire un cas d’utilisation unique.

La capture d’écran suivante montre comment les classes sont représentées dans l’interface utilisateur d’Experience Platform. Comme l’exemple de schéma illustré ne contient aucun groupe de champs, tous les champs affichés sont fournis par la classe du schéma ([!UICONTROL XDM Individual Profile]).

![Le [!UICONTROL XDM Individual Profile] dans l’éditeur de schémas.](../images/schema-composition/class.png)

Pour obtenir la liste la plus récente des classes XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/classes). Si vous préférez afficher les ressources dans l’interface utilisateur, vous pouvez également consulter le guide sur l’[exploration des composants XDM](../ui/explore.md).

### Groupe de champs {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Groupe de champs"
>abstract="Les groupes de champs sont des composants réutilisables qui vous permettent d&#39;étendre les schémas avec des attributs supplémentaires. La plupart des groupes de champs ne sont compatibles qu&#39;avec certaines classes. Vous pouvez utiliser des groupes de champs standard définis par Adobe ou définir manuellement vos propres groupes de champs personnalisés. Pour plus d&#39;informations sur l&#39;implication des groupes de champs dans la composition des schémas, consultez la documentation."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Groupe de champs requis"
>abstract="Ce groupe de champs est requis par la source que vous utilisez. Vous ne pouvez donc pas le supprimer de votre schéma."

Un groupe de champs est un composant réutilisable qui définit un ou plusieurs champs implémentant certaines fonctions telles que des détails personnels, des préférences d’hôtel ou l’adresse. Les groupes de champs sont destinés à être inclus dans le cadre d’un schéma qui implémente une classe compatible.

Les groupes de champs définissent la ou les classes avec lesquelles ils sont compatibles, en fonction du comportement des données qu’ils représentent (enregistrement ou série temporelle). Cela signifie que tous les groupes de champs ne sont pas disponibles pour être utilisés avec toutes les classes.

Experience Platform comprend de nombreux groupes de champs Adobe standard, tout en permettant également aux fournisseurs de définir des groupes de champs pour leurs utilisateurs et aux utilisateurs individuels de définir des groupes de champs pour leurs propres concepts spécifiques.

Par exemple, pour capturer des détails tels que « [!UICONTROL First Name] » et « [!UICONTROL Home Address] » pour votre schéma « [!UICONTROL Loyalty Members] », vous pouvez utiliser des groupes de champs standard qui définissent ces concepts courants. Toutefois, les concepts plus spécifiques à votre organisation (tels que les détails du programme de fidélité personnalisé ou les attributs de produit) qui peuvent ne pas être couverts par les groupes de champs standard. Dans ce cas, vous devez définir votre propre groupe de champs pour capturer ces informations.

>[!NOTE]
>
>Il est vivement recommandé d’utiliser des groupes de champs standard chaque fois que cela est possible dans vos schémas, car ces champs sont compris implicitement par les services Experience Platform et fournissent une meilleure cohérence lorsqu’ils sont utilisés sur les composants Experience Platform.
>
>Les champs fournis par les composants standard (tels que « Prénom » et « Adresse e-mail ») contiennent des connotations ajoutées au-delà des types de champs scalaires de base. Ils indiquent à Experience Platform que tous les champs partageant le même type de données se comporteront de la même manière. Ce comportement peut s’avérer cohérent quelle que soit la provenance des données ou le service Experience Platform dans lequel les données sont utilisées.

N’oubliez pas que les schémas sont composés de groupes de champs « zéro ou plus ». Cela signifie que vous pouvez composer un schéma valide sans utiliser de groupes de champs.

La capture d’écran suivante montre comment les groupes de champs sont représentés dans l’interface utilisateur d’Experience Platform. Dans cet exemple, un seul groupe de champs ([!UICONTROL Demographic Details]) est ajouté à un schéma, ce qui fournit un regroupement de champs à la structure du schéma.

![Éditeur de schémas avec le groupe de champs [!UICONTROL Demographic Details] mis en surbrillance dans un exemple de schéma.](../images/schema-composition/field-group.png)

Pour obtenir la liste la plus récente des groupes de champs XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Si vous préférez afficher les ressources dans l’interface utilisateur, vous pouvez également consulter le guide sur l’[exploration des composants XDM](../ui/explore.md).

>[!NOTE]
>
> Les groupes de champs XDM standard évoluent constamment et certains groupes de champs sont obsolètes. Pour obtenir la liste la plus récente des groupes de champs obsolètes, reportez-vous à la section [groupes de champs obsolètes](https://github.com/adobe/xdm/tree/master/components/fieldgroups/deprecated) dans le référentiel XDM officiel.

### Type de données {#data-type}

Les types de données sont utilisés comme types de champ de référence dans des classes ou des schémas de la même manière que des champs littéraux de base. La principale différence réside dans le fait que les types de données peuvent définir plusieurs sous-champs de la même manière que les groupes de champs. La principale différence entre les deux est que les types de données peuvent être inclus n’importe où dans un schéma en l’ajoutant en tant que « type de données » d’un champ. Bien que les groupes de champs ne soient compatibles qu’avec certaines classes, les types de données peuvent être inclus dans n’importe quelle classe ou groupe de champs parent.

>[!NOTE]
>
>Si un champ est défini comme un type de données spécifique, vous ne pouvez pas créer le même champ avec un type de données différent dans un autre schéma. Cette contrainte s’applique à l’ensemble du client de votre organisation.

Experience Platform fournit un certain nombre de types de données courants dans le cadre de la [!DNL Schema Registry] pour prendre en charge l’utilisation de modèles standard pour décrire des structures de données courantes. Cela est expliqué plus en détail dans les tutoriels [registre des schémas](../tutorials/create-schema-api.md) et sera plus clair lorsque vous parcourrez les étapes de définition des types de données.

La capture d’écran suivante montre comment les types de données sont représentés dans l’interface utilisateur d’Experience Platform. L’un des champs fournis par le groupe de champs [!UICONTROL Demographic Details] utilise le type de données « [!UICONTROL Object] », comme indiqué par le texte suivant le caractère de barre verticale (`|`) en regard du nom du champ. Ce type de données spécifique fournit plusieurs sous-champs liés au nom d’une personne, un concept qui peut être réutilisé pour d’autres champs dans lesquels le nom d’une personne doit être capturé.

![Diagramme dans l’éditeur de schémas pour une personne individuelle avec l’objet Nom complet et les attributs mis en surbrillance.](../images/schema-composition/data-type.png)

Pour obtenir la liste la plus récente des types de données XDM standard disponibles, reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/datatypes). Si vous préférez afficher les ressources dans l’interface utilisateur, vous pouvez également consulter le guide sur l’[exploration des composants XDM](../ui/explore.md).

>[!NOTE]
>
> Les types de données XDM standard évoluent constamment et certains types de données ont été abandonnés. Pour obtenir la liste la plus mise à jour des types de données obsolètes, reportez-vous à la section [types de données obsolètes](https://github.com/adobe/xdm/tree/master/components/datatypes/deprecated) dans le référentiel XDM officiel.

### Champ {#field}

Un champ est le bloc de création le plus basique d’un schéma. Les champs fournissent des contraintes concernant le type de données qu’ils peuvent contenir en définissant un type de données spécifique. Ces types de données de base définissent un seul champ, tandis que les types de données mentionnés précédemment vous permettent de définir plusieurs sous-champs et de réutiliser la même structure à champs multiples dans différents schémas. Donc, en plus de définir le « type de données » d’un champ comme l’un des types de données défini dans le registre, Experience Platform prend en charge des types scalaires de base comme :

* Chaîne
* Entier
* Double
* Booléen
* Tableau
* Objet

>[!TIP]
>
>Voir [annexe](#objects-v-freeform) pour plus d’informations sur les avantages et inconvénients de l’utilisation de champs à structure libre par rapport aux champs de type objet.

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
>Le type de champ « mappage » permet d’obtenir des données de paire clé-valeur, y compris plusieurs valeurs pour une seule clé. Les mappages se trouvent dans les classes XDM et les groupes de champs standard, mais vous pouvez également définir des mappages personnalisés. Pour plus d’informations, consultez le tutoriel de l’API sur [définition de champs de mappage personnalisés](../tutorials/custom-fields-api.md#custom-maps) ou le guide sur [définition de champs de mappage dans l’interface utilisateur](../ui/fields/map.md).

## Exemple de composition {#composition-example}

Les schémas sont créés à l’aide d’un modèle de composition et représentent le format et la structure des données à ingérer dans Experience Platform. Comme mentionné précédemment, ces schémas sont composés d’une classe et de zéro ou plusieurs groupes de champs compatibles avec cette classe.

Par exemple, un schéma décrivant les achats effectués dans un magasin de vente au détail peut être appelé « [!UICONTROL Store Transactions] ». Le schéma implémente la classe [!DNL XDM ExperienceEvent] combinée avec le groupe de champs [!UICONTROL Commerce] standard et un groupe de champs [!UICONTROL Product Info] défini par l’utilisateur.

Un autre schéma qui suit le trafic du site web peut être appelé « [!UICONTROL Web Visits] ». Il implémente également la classe [!DNL XDM ExperienceEvent], mais cette fois combine le groupe de champs [!UICONTROL Web] standard.

Le diagramme ci-dessous présente ces schémas et les champs fournis par chaque groupe de champs. Il contient également deux schémas basés sur la classe [!DNL XDM Individual Profile], y compris le schéma « [!UICONTROL Loyalty Members] » mentionné précédemment dans ce guide.

![Diagramme de flux de quatre schémas et des groupes de champs qui y contribuent.](../images/schema-composition/composition.png)

### Union {#union}

Experience Platform vous permet non seulement de composer des schémas pour des cas d’utilisation spécifiques, mais aussi de voir une « union » des schémas pour un type de classe spécifique. Le diagramme précédent montre deux schémas basés sur la classe XDM ExperienceEvent et deux schémas basés sur la classe [!DNL XDM Individual Profile]. L’union, illustrée ci-dessous, agrège les champs de tous les schémas qui partagent la même classe ([!DNL XDM ExperienceEvent] et [!DNL XDM Individual Profile], respectivement).

![Diagramme de flux de schéma d’union qui décrit les champs qui les composent.](../images/schema-composition/union.png)

En activant un schéma à utiliser avec [!DNL Real-Time Customer Profile], il est inclus dans l’union pour ce type de classe. [!DNL Profile] fournit des profils robustes et centralisés des attributs du client ainsi qu’un compte horodaté de chaque événement que le client a eu sur un système intégré à Experience Platform. [!DNL Profile] utilise la vue union pour représenter ces données et fournir une vue holistique de chaque client individuel.

Pour plus d’informations sur l’utilisation de [!DNL Profile], consultez la [présentation du profil client en temps réel](../../profile/home.md).

## Mappage des fichiers de données à des schémas XDM {#mapping-datafiles}

Tous les fichiers de données ingérés dans Experience Platform doivent être conformes à la structure d’un schéma XDM. Pour plus d’informations sur la manière de formater les fichiers de données pour se conformer aux hiérarchies XDM (ainsi que des fichiers d’exemple), consultez le document sur les [exemples de transformations ETL](../../etl/transformations.md). Pour obtenir des informations générales sur l’ingestion de fichiers de données dans Experience Platform, consultez la [présentation de l’ingestion par lots](../../ingestion/batch-ingestion/overview.md).

## Schémas pour les audiences externes

Si vous importez des audiences de systèmes externes dans Experience Platform, vous devez utiliser les composants suivants pour les capturer dans vos schémas :

* [[!UICONTROL Segment definition] class &#x200B;](../classes/segment-definition.md) : utilisez cette classe standard pour capturer les attributs clés d’une définition de segment externe.
* [[!UICONTROL Segment Membership Details] le groupe de champs &#x200B;](../field-groups/profile/segmentation.md) : ajoutez ce groupe de champs à votre schéma [!UICONTROL XDM Individual Profile] pour associer des profils client à des audiences spécifiques.

## Étapes suivantes

Maintenant que vous comprenez les principes de base de la composition des schémas, vous êtes prêt à commencer à explorer et à créer des schémas à l’aide de l’[!DNL Schema Registry] .

Pour passer en revue la structure des deux classes XDM principales et leurs groupes de champs compatibles couramment utilisés, consultez la documentation de référence suivante :

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Le [!DNL Schema Registry] permet d’accéder au [!DNL Schema Library] dans Experience Platform et fournit une interface utilisateur et une API RESTful à partir desquelles toutes les ressources de bibliothèque disponibles sont accessibles. Le [!DNL Schema Library] contient les ressources du secteur définies par Adobe, les ressources du fournisseur définies par les partenaires Experience Platform, ainsi que les classes, groupes de champs, types de données et schémas composés par des membres de votre organisation.

Pour commencer à composer un schéma à l’aide de l’interface d’utilisation, suivez le [tutoriel de l’éditeur de schémas](../tutorials/create-schema-ui.md) pour créer le schéma « Loyalty Members » mentionné tout au long de ce document.

Pour commencer à utiliser l’API [!DNL Schema Registry], consultez tout d’abord le guide de développement de l’API [Schema Registry](../api/getting-started.md). Après avoir lu le guide de développement, suivez les étapes décrites dans le tutoriel [Création d’un schéma à l’aide de l’API Schema Registry](../tutorials/create-schema-api.md).

## Annexe

Les sections suivantes contiennent des informations supplémentaires sur les principes de la composition des schémas.

### Tableaux relationnels et objets intégrés {#embedded}

Lorsque vous travaillez avec des bases de données relationnelles, les bonnes pratiques consistent à normaliser les données ou à prendre une entité et à la diviser en éléments individuels qui sont ensuite affichés sur plusieurs tableaux. Pour lire les données dans leur ensemble ou mettre à jour l&#39;entité, des opérations de lecture et d&#39;écriture doivent être effectuées sur de nombreuses tables individuelles à l&#39;aide de JOIN.

En utilisant des objets incorporés, les schémas XDM peuvent représenter directement des données complexes et les stocker dans des documents autonomes avec une structure hiérarchique. L&#39;un des principaux avantages de cette structure est qu&#39;elle vous permet d&#39;interroger les données sans avoir à reconstruire l&#39;entité par des jointures coûteuses à plusieurs tables dénormalisées. Il n’existe aucune restriction stricte quant au nombre de niveaux que peut contenir votre hiérarchie de schéma.

### Schémas et Big Data {#big-data}

Les systèmes numériques modernes génèrent une grande quantité de signaux comportementaux (données de transaction, journaux web, Internet des objets, affichage, etc.). Le Big Data offre des opportunités extraordinaires d’optimiser des expériences, mais les utiliser représente un véritable défi en raison de leur échelle et de la diversité des données. Pour tirer parti des données, leur structure, leur format et leurs définitions doivent être normalisés afin qu’elles puissent être traitées de manière cohérente et efficace.

Les schémas permettent de résoudre ce problème en permettant l’intégration des données à partir de diverses sources, l’uniformisation au moyen de structures et de définitions communes et le partage entre les solutions. Cela permet aux processus et services ultérieurs de répondre à tout type de question posée sur les données. Il s&#39;éloigne de l&#39;approche traditionnelle de la modélisation des données, où toutes les questions à poser aux données sont connues à l&#39;avance et où les données sont modélisées pour se conformer à ces attentes.

### Objets par rapport aux champs à structure libre {#objects-v-freeform}

Certains facteurs clés doivent être pris en compte lors du choix des objets par rapport aux champs de forme libre lors de la conception de vos schémas :

| Objets | Champs à structure libre |
| --- | --- |
| Augmente l’imbrication | Moins ou pas d’imbrication |
| Crée des regroupements logiques de champs | Les champs sont placés à des emplacements ad hoc |

{style="table-layout:auto"}

#### Objets

Les avantages et inconvénients de l’utilisation d’objets sur des champs à structure libre sont répertoriés ci-dessous.

**Avantages** :

* Il est préférable d’utiliser les objets lorsque vous souhaitez créer un regroupement logique de certains champs.
* Les objets organisent le schéma de manière plus structurée.
* Les objets aident indirectement à créer une bonne structure de menu dans l’interface utilisateur du créateur de segments. Les champs regroupés dans le schéma sont directement répercutés dans la structure de dossiers fournie dans l’interface utilisateur du créateur de segments.

**Inconvénients** :

* Les champs deviennent plus imbriqués.
* Lors de l’utilisation d’Experience Platform Query Service [&#128279;](../../query-service/home.md), des chaînes de référence plus longues doivent être fournies aux champs de requête imbriqués dans des objets.

#### Champs à structure libre

Les avantages et inconvénients de l’utilisation de champs à structure libre sur des objets sont répertoriés ci-dessous.

**Avantages** :

* Les champs de forme libre sont créés directement sous l’objet racine du schéma (`_tenantId`), ce qui accroît la visibilité.
* Les chaînes de référence des champs à structure libre ont tendance à être plus courtes lors de l’utilisation de Query Service.

**Inconvénients** :

* L’emplacement des champs de forme libre dans le schéma est ad hoc, ce qui signifie qu’ils apparaissent dans l’ordre alphabétique dans l’éditeur de schémas. Cela peut rendre les schémas moins structurés et les champs de forme libre similaires peuvent finir par être très séparés en fonction de leur nom.
