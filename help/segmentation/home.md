---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Segmentation Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 4%

---


# Présentation du service de segmentation

Adobe Experience Platform Segmentation Service fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données de Profil client en temps réel. Ces segments sont configurés et maintenus de manière centralisée sur Platform et sont facilement accessibles par toute solution Adobe.

Ce document présente un aperçu du service de segmentation et du rôle qu’il joue dans l’Adobe Experience Platform.

## Prise en main de Segmentation Service

Il est important de comprendre les termes clés suivants utilisés tout au long de ce document :

- **Segmentation**: Diviser un grand groupe d’individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits qui partagent des caractéristiques similaires et réagissent de la même manière aux stratégies marketing.
- **Définition** de segment : Jeu de règles utilisé pour décrire les principales caractéristiques ou le comportement d’une audience de cible. Une fois conceptualisée, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres d’audience admissibles pour un segment.
- **Audience**: Ensemble de profils résultant qui répond aux critères d’une définition de segment.

## Fonctionnement de la segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat.

Une fois qu’un segment a été conceptuellement défini, il est créé en Experience Platform. En règle générale, les segments sont créés par le spécialiste du marketing ou de l’audience, bien que certaines organisations préfèrent les créer par leur service marketing, en collaboration avec leurs analystes de données. Après avoir examiné les données envoyées à Platform, l’analyste de données compose la définition de segment en sélectionnant les champs et les valeurs qui seront utilisés pour créer les règles ou conditions du segment. Cette opération est effectuée à l’aide de l’interface utilisateur ou de l’API.

## Création de segments

Qu’ils soient créés à l’aide de l’API ou du créateur de segments, les segments sont en fin de compte définis à l’aide du langage PQL (Profil Requête Language). C’est ici que la définition de segment conceptuel est décrite dans le langage créé pour récupérer les profils répondant aux critères. Pour plus d’informations, voir la présentation [de](./pql/overview.md)PQL.

Pour savoir comment créer et utiliser des segments dans le créateur de segments (l’implémentation de l’interface utilisateur de Segmentation Service), consultez le guide [du créateur de](./ui/overview.md)segments.

Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, voir le didacticiel sur la [création de segments d’audience à l’aide de l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Dans le événement d’une extension d’un schéma, tous les téléchargements futurs doivent mettre à jour les champs nouvellement ajoutés en conséquence. Pour plus d’informations sur la personnalisation du modèle de données d’expérience (XDM), consultez le didacticiel [de l’éditeur de](../xdm/tutorials/create-schema-ui.md)Schéma.

## Évaluer les segments

### Segmentation par flux

Segmentation par flux est un processus continu de sélection des données qui met à jour vos segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données entrantes sur le Profil client en temps réel. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui garantit que votre audience de cible reste pertinente.

Pour en savoir plus sur la segmentation en flux continu, consultez la documentation [sur la segmentation en](./api/streaming-segmentation.md)flux continu.

### Segmentation par lots

En lieu et place d’un processus continu de sélection des données, la segmentation par lots déplace toutes les données de profil à la fois par le biais de définitions de segment afin de produire les audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin que vous puissiez l’exporter pour l’utiliser.

Pour savoir comment évaluer les segments, consultez le didacticiel [d’évaluation des](./tutorials/evaluate-a-segment.md)segments.

## Accès aux résultats de la segmentation

Pour savoir comment accéder à un segment exporté, consultez le didacticiel [d’évaluation des](./tutorials/evaluate-a-segment.md)segments.

## Métadonnées de segment

Les métadonnées de segment facilitent l’indexation dans le événement de l’un de vos segments à réutiliser et/ou à combiner.

La composition de vos segments (via l’API ou le créateur de segments) nécessite de définir un nom de segment et de fusionner la stratégie.

### Noms de segment

Lors de la création d’un segment, vous devez fournir un nom de segment. Le nom du segment permet d’identifier un segment particulier dans la collection créée par le service de segmentation. Les noms de segment doivent donc être descriptifs, concis et uniques.

>[!NOTE]
>
>Lors de la planification d’un segment, n’oubliez pas que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec celui-ci. Lors de la sélection d’un nom, pensez à la possibilité que votre segment contienne des portions réutilisables.

### Stratégies de fusion

Les stratégies de fusion sont des règles utilisées par le Profil pour déterminer comment les données seront hiérarchisées et combinées en une vue unifiée dans certaines conditions.
Si aucune stratégie de fusion n’est définie, la stratégie de fusion Platform par défaut est utilisée. Si vous préférez utiliser une stratégie de fusion propre à votre organisation, vous pouvez créer la vôtre et la marquer comme valeur par défaut de votre organisation.

>[!NOTE]
>
>L&#39;estimation des tailles d&#39;audiences est basée sur la stratégie de fusion de profils par défaut de l&#39;entreprise.

### Autres métadonnées de segment

Outre le nom du segment et la stratégie de fusion, le créateur de segments vous offre un champ de métadonnées &quot;description du segment&quot; supplémentaire dans lequel vous pouvez résumer l’objectif de votre définition de segment.

## Fonctionnalités de segmentation avancées

Les segments peuvent être configurés pour générer continuellement une audience en combinant l’assimilation [de données](../ingestion/streaming-ingestion/overview.md) en flux continu à l’une des fonctionnalités de segmentation avancées suivantes :
- [Segmentation séquentielle](#sequential)
- [Segmentation dynamique](#dynamic)
- [Segmentation multientité](#multi-entity)

Ces fonctions avancées sont décrites plus en détail dans les sections suivantes.

## Segmentation séquentielle {#sequential}

Un parcours utilisateur standard est séquentiel par nature.  L’Adobe Experience Platform vous permet de définir une série ordonnée de segments pour refléter ce parcours, capturant ainsi des séquences de événements au fur et à mesure de leur apparition. Vous pouvez classer les événements dans l’ordre souhaité en utilisant la chronologie du événement visuel dans le créateur de segments.

Un exemple de parcours client qui nécessiterait une segmentation séquentielle serait la vue de produit > produit ajouté > passage en caisse > Aucun achat.

## Segmentation dynamique {#dynamic}

La segmentation dynamique résout les problèmes d’évolutivité auxquels les spécialistes du marketing sont généralement confrontés lors de la création de segments pour les campagnes marketing.

Contrairement à la segmentation statique qui nécessite de capturer de manière explicite et répétée chaque cas d’utilisation possible, la segmentation dynamique utilise des variables pour construire la logique de règle et exprimer de manière dynamique les relations.

### Cas d’utilisation : Recherche de clients qui effectuent des achats en dehors de leur état d’origine

Pour illustrer la valeur de cette fonction de segmentation avancée, imaginez un architecte de données collaborant avec un spécialiste du marketing afin d’identifier les clients qui ont effectué des achats en dehors de leur état d’origine.

**Le problème**

La segmentation statique nécessite de définir des segments individuels avec un attribut d’état d’accueil unique, avant de filtrer les événements d’achat qui ne sont pas égaux à l’état d’origine. Un segment explicite de ce type se lirait comme suit : &quot;Je cherche des gens de l&#39;Utah où l&#39;état de leur achat n&#39;est pas Utah&quot;. Pour créer une audience à l’aide de cette méthode, vous devez définir un segment pour chaque état des États-Unis, pour un total de 50 segments.

En raison des différentes combinaisons de segments qui surviennent inévitablement au fur et à mesure de l’échelle, le processus manuel requis pour la segmentation statique prend plus de temps, ce qui réduit votre efficacité globale.

**La solution**

En attribuant une variable à l’attribut d’état d’achat, votre segment dynamique simplifie la recherche d’un achat pour lequel l’état de cet achat n’est pas égal à l’état d’origine du client. Cela vous permet ensuite de consolider 50 segments statiques en un seul segment dynamique.

## Segmentation multientité {#multi-entity}

Grâce à la fonction avancée de segmentation multientité, vous pouvez créer des segments à l’aide de plusieurs classes XDM, ajoutant ainsi des extensions aux schémas de personnes. En conséquence, le service de segmentation peut accéder à d’autres champs pendant la définition de segment comme s’ils étaient natifs du magasin de données de profil.

La segmentation multientité offre la souplesse nécessaire pour identifier les audiences en fonction des données pertinentes pour vos besoins commerciaux. Ce processus peut être réalisé rapidement et facilement sans avoir besoin d&#39;expertise pour interroger les bases de données. Cela vous permet d’ajouter des données clés à vos segments sans avoir à apporter des modifications coûteuses aux flux de données ou attendre une fusion de données dorsales.

### Cas d’utilisation : Promotion axée sur les prix

Pour illustrer la valeur de cette fonction de segmentation avancée, imaginez qu’un architecte de données collabore avec un spécialiste du marketing.

Dans cet exemple, l’architecte de données associe les données d’un individu (composé de schémas avec un Profil individuel XDM et XDM ExperienceEvent comme classes de base) à une autre classe utilisant une clé. Une fois joint, l’architecte de données ou le spécialiste du marketing peut utiliser ces nouveaux champs lors de la définition de segment comme s’ils étaient natifs du schéma de classe de base.

**Le problème**

L&#39;architecte de données et le spécialiste du marketing travaillent tous deux pour le même détaillant de vêtements. Le détaillant compte plus de 1 000 magasins en Amérique du Nord et réduit périodiquement les prix des produits tout au long de leur cycle de vie. En conséquence, le spécialiste du marketing souhaite lancer une campagne spéciale pour donner aux acheteurs qui ont acheté ces articles la possibilité de les acheter au prix réduit.

Les ressources de l&#39;architecte de données incluent l&#39;accès aux données Web issues de la navigation des clients ainsi que les données d&#39;ajout de paniers contenant des identifiants SKU de produit. Ils ont également accès à une classe de &quot;produits&quot; distincte, où sont stockées des informations supplémentaires sur les produits (y compris le prix du produit). Leur conseil est de se concentrer sur les clients qui ont ajouté un produit à leur panier au cours des 14 derniers jours, mais qui n&#39;ont pas acheté l&#39;article, dont le prix a maintenant baissé.

**La solution**

>[!NOTE]
>
>Dans cet exemple, nous supposerons que l&#39;architecte de données a déjà établi un Espace de nommage d&#39;identification.

A l’aide de l’API, l’architecte de données associe la clé du schéma ExperienceEvent à la classe &quot;products&quot;. Cela permet à l’architecte de données d’utiliser les champs supplémentaires de la classe &quot;products&quot; comme s’ils étaient natifs du schéma ExperienceEvent. En guise de dernière étape du travail de configuration, l’architecte de données doit importer les données appropriées dans le Profil client en temps réel. Pour ce faire, vous devez activer le jeu de données &quot;products&quot; en vue de l’utiliser avec le Profil. Une fois la configuration terminée, l’architecte de données ou le spécialiste du marketing peuvent créer le segment de cible dans le créateur de segments.

Consultez la présentation [de la composition de](../xdm/schema/composition.md#union) schéma pour savoir comment définir les relations entre les classes XDM.

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Cas d’utilisation

Pour illustrer la valeur de cette fonctionnalité de segmentation avancée, considérez trois cas d’utilisation standard qui illustrent les défis qui se posaient dans les applications marketing avant l’amélioration de la charge utile de segment :
- Personnalisation du courrier électronique
- Reciblage des courriels
- Reciblage publicitaire

**Personnalisation du courrier électronique**

Un spécialiste du marketing qui a créé une campagne par courriel a peut-être tenté de créer un segment pour une audience de cible en utilisant les achats récents de la boutique de clients au cours des trois derniers mois. Idéalement, ce segment nécessiterait à la fois le nom de l’article et celui de la boutique où l’achat a été effectué. Avant l’amélioration, le défi consistait à capturer l’identifiant de magasin à partir du événement d’achat et à l’affecter au profil de ce client.

**Reciblage des courriels**

Il est souvent complexe de créer et de qualifier des segments pour les campagnes par courrier électronique ciblant &quot;l’abandon de panier&quot;. Avant l&#39;amélioration, il était difficile de savoir quels produits inclure dans un message personnalisé en raison de la disponibilité des données requises. Les données pour lesquelles les produits ont été abandonnés sont liées à des événements d&#39;expérience qui étaient auparavant difficiles à surveiller et à extraire des données.

**Reciblage publicitaire**

Un autre défi traditionnel pour les spécialistes du marketing a été de créer des publicités pour recibler les clients avec des articles abandonnés du panier. Bien que les définitions de segments aient abordé ce problème, avant l&#39;amélioration, il n&#39;existait pas de méthode formelle pour différencier les produits achetés des produits abandonnés. Vous pouvez désormais cible de jeux de données spécifiques lors de la définition de segment.

## Types de données du service de segmentation

Tous les types de données XDM sont pris en charge dans le service de segmentation. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivants.

### Données de chaîne

Les définitions de segment utilisent des données de chaîne pour définir des contraintes non numériques pour les audiences de segment, telles que &quot;nom du pays&quot; ou &quot;niveau de programme de fidélité&quot;.

Les données de chaîne sont incluses dans les définitions de segment à l’aide d’instructions logiques, inclusives/exclusives et de comparaisons. Une fois qu’un attribut de chaîne est ajouté à votre définition de segment, vous pouvez utiliser des instructions appropriées à la chaîne pour l’évaluer par rapport à d’autres champs de chaîne.

| Type de relevé | Exemples |
| -------------- | -------- |
| Logique | et, ou non |
| Inclusif/exclusif | inclure, doit exister, exclure, ne doit pas exister |
| Comparaison | est égal à, n’est pas égal à, contient, débuts avec |


### Données de date

Les données de date vous permettent d’attribuer un contexte temporel à vos définitions de segment, soit en utilisant des dates de début/fin spécifiques, soit en utilisant des instructions pertinentes à la date, comme le montre le tableau ci-dessous. Une implémentation peut consister à créer une audience de clients qui ont interagi avec votre marque à tout moment *cette année* et qui ont également été actifs ** au cours des derniers jours.

| Exemple de champ | Déclarations pertinentes | Chronologie |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | aujourd&#39;hui, hier, ce mois-ci, cette année | Pertinent au jour où le segment a été créé. |
| person.lastPurchase | en dernier lieu, avant, après, | Pertinent dans une semaine ou un mois donné. |

### Événements d’expérience

En tant que schéma d’Adobe Experience Platform, XDM ExperienceEvents enregistre les interactions client explicites et implicites avec les applications intégrées Platform, y compris un instantané du système au moment où l’interaction a eu lieu. ExperienceEvents sont des enregistrements de faits. Il s’agit donc d’une source de données disponible lors de la définition de segment.

Comme le montre le tableau ci-dessous, les données de événement sont rendues à l’aide de mots-clés qui aident à affiner le comportement des événements et à spécifier les attributs de événement.

| Mot-clé | Utilisez   |
| ------- | --- |
| Inclure/exclure | Décrit le comportement du événement par l’inclusion ou l’omission de données. |
| Tout/tout | Permet de déterminer le nombre de segments qualifiants. |
| Bouton bascule &quot;Appliquer la règle de temps&quot; | Incorpore les données de date. |
| Est égal à, n’est pas égal, débuts avec, n’est pas début avec, se termine par, ne se termine pas par, contient, ne contient pas, n’existe pas, n’existe pas | Incorpore des données de chaîne. |

### Segments

Les définitions de segment existantes peuvent également être utilisées comme composants d’une nouvelle définition de segment, en ajoutant leurs attributs et règles basées sur le événement au nouveau segment.

### Audiences

Les audiences externes peuvent également être utilisées comme composants d’une nouvelle définition de segment, en ajoutant leurs règles d’attribut au nouveau segment.

Actuellement, seul l’Adobe Audience Manager est pris en charge en tant qu’audience. D’autres sources seront activées à l’avenir.

### Autres types de données

Outre celles mentionnées ci-dessus, la liste des types de données pris en charge inclut également :
- Chaîne
- Identificateur de ressource unique
- Enum
- Nombre
- Long
- Entier
- Court
- Octet
- Booléen
- Date
- Date-heure
- Tableau
- objet
- Carte
- Événements

## Étapes suivantes

Le service de segmentation fournit un processus consolidé pour créer des segments à partir des données du Profil client en temps réel. En résumé :

- La segmentation est le processus de définition d&#39;un sous-ensemble de profils à partir de votre banque de profils, ce qui vous permet de caractériser le comportement ou les attributs d&#39;un groupe vendable souhaité. Le service de segmentation rend ce processus possible.
- Lors de la planification d’un segment, gardez à l’esprit qu’un segment peut être référencé à partir de tout autre segment et combiné avec celui-ci.
- Un segment peut être créé à partir de règles basées sur des données de profil, des données de série chronologique associées, ou les deux.
- Les segments peuvent être évalués à la demande ou de manière continue. Lors de l’évaluation à la demande, toutes les données de profil sont transmises simultanément par le biais des définitions de segment. Lorsqu’elles sont évaluées en continu, les données sont diffusées par le biais des définitions de segment lorsqu’elles entrent dans Platform.

Pour savoir comment définir des segments dans l’interface utilisateur, consultez le guide [du créateur de](./ui/overview.md)segments. Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, voir le didacticiel sur la [création de segments à l’aide de l’API](./tutorials/create-a-segment.md).