---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;api étiquette dʼutilisation des données;api service de stratégie;étiquettes dʼutilisation des données prises en charge;étiquettes contrat;étiquettes identité;étiquettes sensibles
solution: Experience Platform
title: Glossaire des étiquettes dʼutilisation des données
topic-legacy: labels
description: Ce document décrit toutes les étiquettes dʼutilisation des données actuellement prises en charge par Adobe Experience Platform.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: c29b6c7dc061ea910ebedcae1fa4beaa6def10b1
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 67%

---

# Glossaire des étiquettes dʼutilisation des données {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Types d’étiquettes"
>abstract="Il existe plusieurs catégories de libellés d’utilisation des données. Les étiquettes définies par l’Adobe comprennent les étiquettes de contrat, les étiquettes d’identité et les étiquettes sensibles. Les libellés définis par votre organisation sont classés comme des libellés personnalisés."
>text="See the data usage labels glossary for more information on these label types."

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Adobe Experience Platform Data Governance fournit de multiples étiquettes dʼutilisation des données de base prêtes à lʼemploi que vous pouvez utiliser pour commencer à classer vos données.

Ce document décrit les étiquettes dʼutilisation des données de base actuellement fournies par [!DNL Experience Platform]. Vous trouverez plus d’informations sur la gouvernance des données dans la [présentation de la gouvernance des données](../home.md).

## Étiquettes Contrat

Les étiquettes Contrat « C » sont utilisées pour catégoriser des données qui possèdent des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre organisation.

| Libellé | Définition |
| --- | --- |
| [C1](#c1) | Les données ne peuvent être exportées depuis Adobe Experience Cloud que sous une forme agrégée, sans inclure d’identifiants individuels ou d’appareil. |
| [C2](#c2) | Les données ne peuvent pas être exportées vers un tiers. |
| [C3](#c3) | Les données ne peuvent être combinées ou autrement utilisées avec des informations directement identifiables. |
| [C4](#c4) | Les données ne peuvent pas être utilisées pour cibler des publicités ou du contenu, que ce soit sur site ou entre sites. |
| [C5](#c5) | Les données ne peuvent pas être utilisées pour le ciblage intersite de contenu ou de publicités en fonction des intérêts. |
| [C6](#c6) | Les données ne peuvent pas être utilisées pour le ciblage de publicités sur site. |
| [C7](#c7) | Les données ne peuvent pas être utilisées pour le ciblage de contenu sur site. |
| [C8](#c8) | Les données ne peuvent pas être utilisées pour mesurer les sites web ou les applications de votre entreprise. |
| [C9](#c9) | Les données ne peuvent pas être utilisées dans les workflows Data Science. |
| [C10](#c10) | Les données ne peuvent pas être utilisées pour lʼactivation de lʼidentité assemblée. |
| [C11](#c11) | Les données ne peuvent pas être partagées avec les partenaires de correspondance de segment. |
| [C12](#c12) | Les données ne peuvent pas être exportées de quelque manière que ce soit. |

## Étiquettes Identité

Les étiquettes Identité « I » sont utilisées pour catégoriser des données pouvant identifier ou contacter une personne en particulier.

| Libellé | Définition |
| --- | --- |
| **I1** | Données directement identifiables qui permettent d’identifier ou de contacter une personne spécifique, plutôt qu’un appareil. |
| **I2** | Données indirectement identifiables pouvant être utilisées en combinaison avec toute autre donnée pour identifier ou contacter une personne spécifique. |

## Étiquettes Sensibles {#sensitive}

Les étiquettes Sensibles &quot;S&quot; sont utilisées pour catégoriser les données que vous et votre organisation considérez comme sensibles.

Différents types de données géographiques peuvent être considérés comme sensibles. Toutefois, cette catégorie ne se limite pas aux données géographiques.

| Libellé | Définition |
| --- | --- |
| **S1** | Données spécifiant la latitude et la longitude pouvant être utilisées pour déterminer l’emplacement précis d’un appareil. |
| **S2** | Données pouvant être utilisées pour déterminer une zone de géobarrière au sens large. |
| **PSPD** | Les données personnelles sensibles autorisées (PSPD) se rapportent à des données que vous êtes contractuellement autorisé par Adobe à télécharger et qui sont considérées comme &quot;sensibles&quot;, &quot;catégorie spéciale de données&quot; ou comme un terme similaire utilisé par les lois applicables. Cela exclut spécifiquement les informations sur la santé protégée (IPS) et d’autres données sur la santé réglementées. |
| **RHD** | Données qui font référence à des informations sur la santé protégée ou des informations sur un patient que vous êtes contractuellement autorisé par l’Adobe à télécharger. |

## Annexe

Les sections ci-dessous fournissent des informations supplémentaires sur les étiquettes dʼutilisation des données disponibles.

### Détails des étiquettes Contrat

Les sections suivantes contiennent des informations détaillées sur la mise en œuvre dʼétiquettes Contrat « C » spécifiques.

#### C1 {#c1}

Certaines données ne peuvent être exportées depuis Adobe Experience Cloud que sous une forme agrégée, sans inclure d’identifiants individuels ou d’appareil. Par exemple, les données provenant des réseaux sociaux.

#### C2 {#c2}

Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent l’exportation de données à partir de l’endroit où elles ont été collectées à l’origine. Par exemple, les contrats de réseau social limitent souvent le transfert des données que vous recevez de leur part. L’étiquette C2 est plus restrictive que [C1](#c1), qui ne nécessite qu’une agrégation et des données anonymes, mais qui est moins restrictif que [C12](#c12), qui empêche les exportations de données, quelle que soit la destination.

#### C3 {#c3}

Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent la combinaison ou l’utilisation de ces données avec des informations directement identifiables. Par exemple, les contrats relatifs aux données provenant de réseaux publicitaires, de serveurs de publicités et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données avec des données directement identifiables.

#### C4 {#c4}

C4 englobe les libellés [C5](#c5), [C6](#c6), et [C7](#c7). Il s’agit de l’une des étiquettes les plus restrictives, juste après la [C12](#c12).

#### C5 {#c5}

Le ciblage en fonction des intérêts, ou personnalisation, se produit si les trois conditions suivantes sont remplies : Les données collectées sur site sont (1) utilisées pour établir des inférences sur les intérêts d’un utilisateur, (2) utilisées dans un autre contexte, par exemple sur un autre site ou une autre application (hors site) ET (3) utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.

La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les différents sites représentent des contextes différents, de sorte que l’utilisation des données intersites dans n’importe quel contexte est différente de celle d’origine. Les données intersites sont généralement collectées et traitées afin d’établir des inférences sur les intérêts des utilisateurs. Par conséquent, l’utilisation de données intersites pour le ciblage de publicités ou de contenu est généralement qualifiée de ciblage en fonction des intérêts, que la publicité ou le contenu apparaisse sur le site ou hors site. Par exemple, si des données sur site étaient utilisées en combinaison avec des données hors site pour sélectionner la publicité à afficher à un utilisateur sur le site de l’entreprise, cette utilisation serait considérée comme un ciblage en fonction des intérêts. Autre exemple : le reciblage des publicités destinées aux utilisateurs hors site peut également être qualifié de ciblage en fonction des intérêts.

L’utilisation de données hors site uniquement pour le ciblage peut également être considérée comme un ciblage en fonction des intérêts, car les données hors site sont généralement collectées et traitées pour établir des inférences sur les intérêts des utilisateurs.

Cependant, le ciblage de contenu ou de publicités utilisant uniquement des données sur site ne peut généralement pas être considéré comme un ciblage en fonction des intérêts. Le ciblage sur site qui n’est pas qualifié autrement de ciblage en fonction des intérêts est traité comme deux libellés distincts. Plus précisément, l’étiquette C6 porte sur le ciblage et la création de rapports de publicités sur site et traite spécifiquement de la sélection, de la diffusion et de la création de rapports de publicités, tandis que l’étiquette C7 porte sur la sélection, la diffusion et la création de rapports de contenu sur site (ciblage de contenu sur site).

En fin de compte, l’interprétation de l’étiquette et la manière dont l’utilisation des données avec cette étiquette est appliquée dépendent de vous. À titre de référence, les cadres IAB et DAA sont fournis ci-dessous :

IAB : personnalisation. Collecte et traitement d’informations sur votre utilisation de ce service afin de personnaliser ultérieurement la publicité et/ou le contenu pour vous dans d’autres contextes, par exemple sur d’autres sites web ou applications, dans la durée. En règle générale, le contenu du site ou de l’application est utilisé pour établir des inférences sur vos intérêts, ce qui permet d’orienter la sélection future de la publicité et/ou du contenu.

DAA : publicité comportementale en ligne. Collecte de données à partir d’un ordinateur ou d’un appareil particulier concernant les comportements en matière de consultation des sites web dans le temps et sur des sites web non affiliés dans le but de prédire les préférences ou les intérêts des utilisateurs pour diffuser de la publicité sur cet ordinateur ou cet appareil en fonction des préférences ou des intérêts déduits de ces comportements.

#### C6 {#c6}

Les publicités sont des messages ou des notifications, y compris des textes et des images, apparaissant sur un site web ou une application, qui sont principalement destinés à promouvoir la vente de biens ou de services. C’est à vous de déterminer l’objectif de ces messages ou notifications. Les publicités sont séparées du contenu sur site, couvert par une étiquette [C7](#c7). Les données avec une étiquette C6 ne peuvent pas être utilisées pour le ciblage des publicités sur site, y compris la sélection et la diffusion de publicités sur les sites web ou les applications de votre organisation, ni pour mesurer la diffusion et l’efficacité de ces publicités. Cela inclut l’utilisation de données précédemment collectées sur site concernant les intérêts des utilisateurs pour sélectionner des publicités, le traitement des données concernant les publicités diffusées, le moment et le lieu de leur diffusion, et le fait de savoir si les utilisateurs ont pris des mesures en rapport avec la publicité, comme sélectionner une publicité ou effectuer un achat. En règle générale, établir des inférences sur les préférences d’un utilisateur en fonction de ses activités sur site, puis utiliser ces préférences dans le ciblage des publicités sur site, ne peut pas être considéré comme un ciblage en fonction des intérêts (également appelé personnalisation), puisqu’il ne répond pas aux trois exigences nécessaires au ciblage en fonction des intérêts. *[Voir l’étiquette C5 pour ces exigences.](#c5)*

En fin de compte, l’interprétation de l’étiquette et la manière dont l’utilisation des données avec cette étiquette est appliquée dépendent de vous. À titre de référence, les cadres IAB et DAA sont fournis ci-dessous :

IAB : 3. Sélection, diffusion, création de rapports sur les publicités : collecte d’informations, et leur combinaison avec des informations précédemment recueillies, pour sélectionner et diffuser des publicités pour vous, et pour mesurer la diffusion et l’efficacité de ces publicités. Cela inclut lʼutilisation dʼinformations précédemment collectées sur vos centres dʼintérêt pour sélectionner des publicités, le traitement de données sur les publicités diffusées, la fréquence de leur diffusion, le moment et le lieu de leur diffusion, et le fait de savoir si vous avez pris une mesure quelconque en rapport avec la publicité, par exemple en sélectionnant une publicité ou en effectuant un achat. Cela n’inclut pas la personnalisation, qui est la collecte et le traitement d’informations sur votre utilisation de ce service afin de personnaliser ultérieurement la publicité et/ou le contenu pour vous dans d’autres contextes, tels que des sites web ou des applications, dans la durée.

DAA : La publicité comportementale en ligne n’inclut pas les activités des Premières parties, la diffusion ou la création de rapports sur les publicités, ni la publicité contextuelle (c’est-à-dire la publicité basée sur le contenu de la page web visitée, la visite actuelle d’un client sur une page web ou une requête de recherche).

#### C7 {#c7}

Le contenu sur site est constitué de textes et d’images conçus pour informer, apprendre ou divertir, et non pour promouvoir la vente de biens ou de services. C’est à vous de déterminer l’objectif du contenu, notamment si celui-ci peut être qualifié de publicité native. L’étiquette C7 n’est pas destinée à couvrir les publicités sur site, qui sont couvertes par l’étiquette [C6](#c6). Les données avec une étiquette C7 ne peuvent pas être utilisées pour le ciblage de contenu sur site, y compris la sélection et la diffusion de contenu sur les sites web ou les applications de votre organisation, ni pour mesurer la diffusion et l’efficacité de ce contenu. Cela inclut les informations précédemment collectées sur les intérêts des utilisateurs dans le contenu sélectionné, le traitement des données sur le contenu affiché, la fréquence ou la durée de sa diffusion, le moment et le lieu de sa diffusion, et si les utilisateurs ont pris des mesures relatives au contenu, par exemple en sélectionnant le contenu. En règle générale, établir des inférences sur les préférences d’un utilisateur en fonction de ses activités sur site, puis utiliser ces préférences dans le ciblage de contenu sur site, ne peut pas être considéré comme un ciblage en fonction des intérêts (également appelé personnalisation), puisqu’il ne répond pas aux trois exigences nécessaires au ciblage en fonction des intérêts. *[Voir l’étiquette C5 pour ces exigences.](#c5)*

En fin de compte, l’interprétation de l’étiquette et la manière dont l’utilisation des données avec cette étiquette est appliquée dépendent de vous. À titre de référence, les cadres IAB et DAA sont fournis ci-dessous :

IAB : 4. Sélection du contenu, diffusion, création de rapports : collecte d’informations, et leur combinaison avec des informations précédemment recueillies, pour sélectionner et diffuser du contenu pour vous, et pour mesurer la diffusion et l’efficacité de ce contenu. Cela inclut lʼutilisation dʼinformations précédemment collectées sur vos intérêts pour sélectionner du contenu, le traitement des données concernant le contenu diffusé, la fréquence ou la durée de sa diffusion, le moment et le lieu de sa diffusion, et le fait de savoir si vous avez pris des mesures en rapport avec le contenu, par exemple en sélectionnant le contenu. Cela n’inclut pas la personnalisation, qui est la collecte et le traitement d’informations sur votre utilisation de ce service afin de personnaliser ultérieurement le contenu et/ou la publicité pour vous dans d’autres contextes, tels que des sites web ou des applications, dans la durée.

DAA : La publicité comportementale en ligne n’inclut pas les activités des Premières parties, la diffusion ou la création de rapports sur les publicités, ni la publicité contextuelle (c’est-à-dire la publicité basée sur le contenu de la page web visitée, la visite actuelle d’un client sur une page web ou une requête de recherche).

#### C8 {#c8}

Les données ne peuvent pas être utilisées pour mesurer, comprendre et générer des rapports sur l’utilisation des sites ou applications de votre entreprise par les utilisateurs. Cela n’inclut pas le ciblage en fonction des intérêts (ciblage intersite), qui est la collecte et le traitement d’informations sur votre utilisation de ce service afin de personnaliser ultérieurement le contenu et/ou la publicité pour vous dans d’autres contextes, notamment sur d’autres services, tels que des sites web ou des applications, dans la durée.

#### C9 {#c9}

Certains contrats prévoient des interdictions explicites sur l’utilisation des données pour la science des données. Parfois, elles sont formulées en des termes qui interdisent l’utilisation de données pour l’intelligence artificielle (AI), l’apprentissage automatique (ML) ou la modélisation.

#### C10 {#c10}

Certaines stratégies dʼutilisation des données limitent lʼutilisation de données dʼidentité assemblées pour la personnalisation. Lʼétiquette C10 est automatiquement appliquée aux segments si leurs stratégies de fusion utilisent lʼoption « graphique privé ».

#### C11 {#c11}

La correspondance de segments d’Adobe Experience Platform vous permet de faire correspondre des segments propriétaires avec des préférences de confidentialité et de consentement, ce qui facilite la création enrichie de profils utilisateurs et les insights en aval. Le libellé C11 indique les données qui ne doivent pas être utilisées dans les processus [!DNL Segment Match]. Une fois que vous avez déterminé les jeux de données et/ou les champs que vous souhaitez exclure de la correspondance de segment et que vous avez ajouté le libellé C11 en conséquence, le libellé est automatiquement appliqué par le workflow Correspondance de segment.

#### C12 {#c12}

Les données avec ce libellé ne peuvent pas être exportées depuis Platform de quelque manière que ce soit. Les champs étiquetés C12 sont exclus des téléchargements CSV, de la consommation d’API et des workflows d’activation.
