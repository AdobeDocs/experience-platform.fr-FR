---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Étiquettes d’utilisation des données prises en charge
topic: labels
translation-type: tm+mt
source-git-commit: 5aa0325a051d9e6e6dd65234db27ab251cfb2d9e
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 2%

---


# Étiquettes d’utilisation des données prises en charge

Adobe Experience Platform inclut une infrastructure de gouvernance des données, avec l’application DULE (Data Usage Labeling and Enforcement) en tête.  Les fonctions DULE permettent d&#39;appliquer des étiquettes d&#39;utilisation de données aux jeux de données et aux champs afin de classer les données en fonction du type de stratégies d&#39;utilisation qui s&#39;appliquent à ces données.

La liste suivante présente tous les libellés d’utilisation des données actuellement pris en charge par la plateforme d’expérience.

Vous trouverez plus d&#39;informations sur la gouvernance des données et le DULE dans l&#39;aperçu [de la gouvernance des](../home.md)données.

## Étiquettes des contrats

Les étiquettes de contrat &quot;C&quot; sont utilisées pour classer les données qui ont des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre entreprise.

| Étiquette | Définition |
|---|---|
| **C1** | Les données peuvent uniquement être exportées à partir d’Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants de périphérique ou de particulier. [Plus d’informations...](#c1) |
| **C2** | Les données ne peuvent pas être exportées vers un tiers. [Plus d’informations...](#c2) |
| **C3** | Les données ne peuvent pas être combinées ou utilisées d&#39;une autre manière avec des informations directement identifiables. [Plus d’informations...](#c3) |
| **C4** | Les données ne peuvent pas être utilisées pour cibler des publicités ou du contenu, sur site ou sur plusieurs sites. [Plus d’informations...](#c4) |
| **C5** | Les données ne peuvent pas être utilisées pour le ciblage intersite du contenu ou des publicités basé sur l’intérêt. [Plus d’informations...](#c5) |
| **C6** | Les données ne peuvent pas être utilisées pour le ciblage publicitaire sur site. [Plus d’informations...](#c6) |
| **C7** | Les données ne peuvent pas être utilisées pour le ciblage sur site du contenu. [Plus d’informations...](#c7) |
| **C8** | Les données ne peuvent pas être utilisées pour mesurer les sites Web ou les applications de votre entreprise. [Plus d’informations...](#c8) |
| **C9** | Les données ne peuvent pas être utilisées dans les workflows Data Science. [Plus d’informations...](#c9) |

## Étiquettes d&#39;identité

Les étiquettes &quot;I&quot; d’identité sont utilisées pour classer les données qui peuvent identifier ou contacter une personne spécifique.

| Étiquette | Définition |
|---|---|
| **I1** | Données directement identifiables qui peuvent identifier ou contacter une personne spécifique, plutôt qu’un dispositif. |
| **I2** | Données indirectes identifiables pouvant être utilisées en combinaison avec toute autre donnée pour identifier ou contacter une personne spécifique. |

## Étiquettes sensibles

Les étiquettes &quot;S&quot; sensibles sont utilisées pour classer les données que vous, et votre entreprise, considérez comme sensibles.

Un type de données que vous jugerez peut-être sensible peut être différent de types de données géographiques ; cependant, cette catégorie ne se limite pas aux données géographiques.

| Étiquette | Définition |
|---|---|
| **S1** | Données spécifiant la latitude et la longitude qui peuvent être utilisées pour déterminer l’emplacement précis d’un périphérique. |
| **S2** | Données pouvant être utilisées pour déterminer une zone de géofence définie de manière générale. |


## Plus d’informations

La section suivante fournit des informations détaillées sur la mise en oeuvre de libellés spécifiques.

### C1 {#c1}

Certaines données ne peuvent être exportées qu’à partir d’Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants de périphérique ou de particulier. Par exemple, les données provenant des réseaux sociaux.

### C2 {#c2}

Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent l&#39;exportation de données d&#39;où elles ont été collectées à l&#39;origine. Par exemple, les contrats de réseaux sociaux limitent souvent le transfert des données que vous recevez d&#39;eux. L&#39;étiquette C2 est plus restrictive que [C1](#c1), ce qui ne nécessite que l&#39;agrégation et les données anonymes.

### C3 {#c3}

Certains fournisseurs de données ont des clauses dans leurs contrats qui interdisent la combinaison ou l&#39;utilisation de ces données avec des informations directement identifiables. Par exemple, les contrats portant sur des données provenant de réseaux publicitaires, de serveurs d’annonces et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données à l’aide de données directement identifiables.

### C4 {#c4}

C4 est l&#39;étiquette la plus restrictive - elle englobe les étiquettes [C5](#c5), [C6](#c6)et [C7](#c7).

### C5 {#c5}

Le ciblage basé sur l’intérêt, ou la personnalisation, se produit si les trois conditions suivantes sont remplies : Les données collectées sur le site sont (1) utilisées pour faire des déductions sur les intérêts des utilisateurs, (2) utilisées dans un autre contexte, par exemple sur un autre site ou une autre application (hors site) ET (3) utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces déductions.

La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les différents sites représentent des contextes différents, de sorte que l’utilisation de données intersites dans un contexte différent de l’original. Les données intersites sont généralement collectées et traitées afin d’en déduire les intérêts des utilisateurs. En conséquence, l’utilisation de données intersites pour le ciblage des publicités ou du contenu est généralement qualifiée de ciblage axé sur les intérêts, que la publicité ou le contenu s’affiche sur site ou hors site. Par exemple, si des données sur site étaient utilisées en combinaison avec des données hors site pour sélectionner la publicité à afficher à l’utilisateur sur le site d’une organisation, cette utilisation serait considérée comme un ciblage basé sur les intérêts. Autre exemple, le reciblage des publicités vers des utilisateurs hors site serait également considéré comme un ciblage basé sur les intérêts.

L’utilisation de données hors site uniquement pour le ciblage pourrait également être considérée comme un ciblage fondé sur l’intérêt, puisque les données hors site sont généralement collectées et traitées pour faire des inférences sur les intérêts des utilisateurs.

Cependant, le ciblage du contenu ou des publicités utilisant uniquement des données sur le site ne peut généralement pas être considéré comme un ciblage axé sur les intérêts. Le ciblage sur site qui n’est pas par ailleurs considéré comme un ciblage basé sur les intérêts est traité comme deux étiquettes distinctes. En particulier, l’étiquette C6 traite du ciblage et du rapports des annonces sur site et traite spécifiquement de la sélection des annonces, de la diffusion et du rapports, et l’étiquette C7 traite de la sélection, de la diffusion et du rapports du contenu sur site (ciblage du contenu sur site).

En fin de compte, l&#39;interprétation de l&#39;étiquette et la façon dont les données associées à cette étiquette sont appliquées dépend de vous. À titre de référence, les cadres du CCI et de la DAA sont présentés ci-dessous :

IAB : Personnalisation. Collecte et traitement d&#39;informations sur votre utilisation de ce service pour personnaliser ultérieurement la publicité et/ou le contenu pour vous dans d&#39;autres contextes, comme sur d&#39;autres sites Web ou applications, au fil du temps. En règle générale, le contenu du site ou de l’application est utilisé pour faire des inférences sur vos intérêts, ce qui explique la sélection future de la publicité et/ou du contenu.

DAA : Publicité comportementale en ligne. Collecte de données à partir d’un ordinateur ou d’un périphérique particulier concernant les comportements de consultation Web au fil du temps et sur des sites Web non affiliés afin d’utiliser ces données pour prédire les préférences ou les intérêts des utilisateurs pour diffuser de la publicité sur cet ordinateur ou appareil en fonction des préférences ou des intérêts induits par ces comportements de consultation Web.

### C6 {#c6}

Les publicités sont des messages ou des notifications, y compris des textes et des images, qui apparaissent sur un site Web ou une application et qui sont principalement destinés à promouvoir la vente de biens ou de services. Il vous appartient de déterminer l&#39;objectif de tels messages ou notifications. Les publicités sont distinctes du contenu sur site, couvert par l&#39;étiquette [C7](#c7). Les données avec une étiquette C6 ne peuvent pas être utilisées pour le ciblage des publicités sur site, y compris la sélection et la diffusion des publicités sur les sites Web ou les applications de votre entreprise, ni pour mesurer la diffusion et l’efficacité de ces publicités. Cela inclut l’utilisation des données collectées sur site concernant les intérêts des utilisateurs pour sélectionner des publicités, traiter les données sur les publicités affichées, leur moment et leur emplacement d’affichage et déterminer si les utilisateurs ont pris des mesures en rapport avec la publicité, comme cliquer sur une publicité ou faire un achat. En règle générale, l’utilisation des préférences d’un utilisateur en fonction de ses activités sur site, puis l’utilisation de ces préférences dans le ciblage des publicités sur site, ne sont pas considérées comme un ciblage fondé sur des intérêts (également appelé personnalisation), puisqu’elles ne répondent pas aux trois exigences nécessaires pour le ciblage fondé sur des intérêts. _[Voir l&#39;étiquette C5 pour ces exigences.](#c5)_

En fin de compte, l&#39;interprétation de l&#39;étiquette et la façon dont les données associées à cette étiquette sont appliquées dépend de vous. À titre de référence, les cadres du CCI et de la DAA sont présentés ci-dessous :

IAB : 3. Sélection de la publicité, diffusion, rapports : La collecte d&#39;informations, combinée à des informations collectées précédemment, pour sélectionner et diffuser des publicités pour vous, et pour mesurer la diffusion et l&#39;efficacité de ces publicités. Cela comprend l&#39;utilisation d&#39;informations collectées précédemment sur vos centres d&#39;intérêt pour sélectionner des publicités, le traitement de données sur les publicités affichées, leur fréquence, leur moment et leur emplacement d&#39;affichage, ainsi que le fait que vous ayez pris des mesures relatives à la publicité, notamment en cliquant sur une publicité ou en faisant un achat. Cela n’inclut pas la personnalisation, qui est la collecte et le traitement d’informations sur votre utilisation de ce service pour personnaliser ultérieurement la publicité et/ou le contenu pour vous dans d’autres contextes, tels que des sites Web ou des applications, au fil du temps.

DAA : La publicité comportementale en ligne n&#39;inclut pas les activités des premières parties, les Diffusions publicitaires ou les Rapports publicitaires, ni la publicité contextuelle (c&#39;est-à-dire la publicité basée sur le contenu de la page Web visitée, la visite actuelle d&#39;un consommateur sur une page Web ou une requête de recherche).

### C7 {#c7}

Le contenu sur site est un texte et des images conçus pour informer, éduquer ou divertir, et qui ne sont pas créés pour promouvoir la vente de biens ou de services. Il vous appartient de déterminer l’objectif du contenu, y compris si celui-ci peut être considéré comme une publicité native. L&#39;étiquette C7 n&#39;est pas destinée à couvrir les publicités sur site, qui sont couvertes par l&#39;étiquette [C6](#c6). Les données avec une étiquette C7 ne peuvent pas être utilisées pour le ciblage du contenu sur site, y compris la sélection et la diffusion de contenu sur les sites Web ou les applications de votre entreprise, ni pour mesurer la diffusion et l’efficacité de ce contenu. Cela inclut les informations collectées précédemment sur les intérêts des utilisateurs dans un contenu sélectionné, le traitement des données sur le contenu affiché, la fréquence ou la durée d’affichage, le moment et l’emplacement d’affichage, et si les utilisateurs ont pris des mesures relatives au contenu, notamment en cliquant sur le contenu. En règle générale, l’utilisation des préférences d’un utilisateur en fonction de ses activités sur site, puis l’utilisation de ces préférences dans le ciblage du contenu sur site, ne sont pas considérées comme un ciblage axé sur les intérêts (également appelé personnalisation), puisqu’elles ne répondent pas aux trois exigences nécessaires pour le ciblage basé sur les intérêts. _[Voir l&#39;étiquette C5 pour ces exigences.](#c5)_

En fin de compte, l&#39;interprétation de l&#39;étiquette et la façon dont les données associées à cette étiquette sont appliquées dépend de vous. À titre de référence, les cadres du CCI et de la DAA sont présentés ci-dessous :

IAB : 4. Sélection du contenu, diffusion, rapports : Collecte d’informations et combinaison avec des informations collectées précédemment, pour sélectionner et diffuser du contenu pour vous, et pour mesurer la diffusion et l’efficacité de ce contenu. Cela comprend l&#39;utilisation d&#39;informations collectées précédemment sur vos centres d&#39;intérêt pour sélectionner le contenu, le traitement des données sur le contenu affiché, la fréquence ou la durée d&#39;affichage, le moment et l&#39;endroit où il a été affiché, ainsi que le fait que vous ayez pris des mesures concernant le contenu, notamment en cliquant sur le contenu. Cela n’inclut pas la personnalisation, qui est la collecte et le traitement d’informations sur votre utilisation de ce service pour personnaliser ultérieurement le contenu et/ou la publicité pour vous dans d’autres contextes, tels que des sites Web ou des applications, au fil du temps.

DAA : La publicité comportementale en ligne n&#39;inclut pas les activités des premières parties, les Diffusions publicitaires ou les Rapports publicitaires, ni la publicité contextuelle (c&#39;est-à-dire la publicité basée sur le contenu de la page Web visitée, la visite actuelle d&#39;un consommateur sur une page Web ou une requête de recherche).

### C8 {#c8}

Les données ne peuvent pas être utilisées pour mesurer, comprendre et générer des rapports sur l’utilisation par les utilisateurs des sites ou applications de votre entreprise. Cela n’inclut pas le ciblage basé sur l’intérêt (ciblage intersite), qui est la collecte d’informations sur votre utilisation de ce service pour personnaliser ultérieurement le contenu et/ou la publicité pour vous dans d’autres contextes, c’est-à-dire sur d’autres services, tels que des sites Web ou des applications, au fil du temps.

### C9 {#c9}

Certains contrats comportent des interdictions explicites d&#39;utilisation des données pour la science des données. Parfois, ces termes sont rédigés en des termes qui interdisent l&#39;utilisation de données pour l&#39;intelligence artificielle (IA), l&#39;apprentissage automatique (ML) ou la modélisation.