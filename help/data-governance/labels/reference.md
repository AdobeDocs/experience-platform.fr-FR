---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Etiquettes d’utilisation des données prises en charge
topic: labels
translation-type: tm+mt
source-git-commit: 5aa0325a051d9e6e6dd65234db27ab251cfb2d9e

---


# Etiquettes d’utilisation des données prises en charge

Adobe Experience Platform inclut une infrastructure de gouvernance des données avec l’application DULE (Data Usage Labeling and Enforcement) à son coeur.  Les fonctionnalités DULE permettent d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs afin de classer les données en fonction du type de stratégies d’utilisation qui s’appliquent à ces données.

Le suivant  décrit tous les libellés d’utilisation des données actuellement pris en charge par la plateforme d’expérience.

Vous trouverez plus d’informations sur la gouvernance des données et le DULE dans l’aperçu [de la gouvernance des](../home.md)données.

## Étiquettes de contrat

Les étiquettes &quot;C&quot; du contrat sont utilisées pour classer les données qui ont des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre entreprise.

| Étiquette | Définition |
|---|---|
| **C1** | Les données peuvent uniquement être exportées à partir d’Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants de périphérique ou individuels. [Plus d’informations...](#c1) |
| **C2** | Les données ne peuvent pas être exportées vers un tiers. [Plus d’informations...](#c2) |
| **C3** | Les données ne peuvent être combinées ni utilisées d&#39;une autre manière avec des informations directement identifiables. [Plus d’informations...](#c3) |
| **C4** | Les données ne peuvent pas être utilisées pour cibler des publicités ou du contenu, que ce soit sur site ou entre sites. [Plus d’informations...](#c4) |
| **C5** | Les données ne peuvent pas être utilisées pour le ciblage inter-sites basé sur l’intérêt du contenu ou des publicités. [Plus d’informations...](#c5) |
| **C6** | Les données ne peuvent pas être utilisées pour le ciblage publicitaire sur site. [Plus d’informations...](#c6) |
| **C7** | Les données ne peuvent pas être utilisées pour le ciblage sur site du contenu. [Plus d’informations...](#c7) |
| **C8** | Les données ne peuvent pas être utilisées pour mesurer les sites Web ou les applications de votre entreprise. [Plus d’informations...](#c8) |
| **C9** | Les données ne peuvent pas être utilisées dans le Data Science. [Plus d’informations...](#c9) |

## Étiquettes d’identité

Les étiquettes &quot;I&quot; d’identité sont utilisées pour classer les données qui peuvent identifier ou contacter une personne spécifique.

| Étiquette | Définition |
|---|---|
| **I1** | Données directement identifiables qui peuvent identifier ou contacter une personne spécifique, plutôt qu’un appareil. |
| **I2** | Données indirectes identifiables pouvant être utilisées en combinaison avec toute autre donnée pour identifier ou contacter une personne spécifique. |

## Étiquettes sensibles

Les libellés &quot;S&quot; sensibles sont utilisés pour classer les données que vous, et votre entreprise, considérez comme sensibles.

Un type de données que vous jugerez peut-être sensible peut être un type différent de données géographiques; toutefois, ce  ne se limite pas aux données géographiques.

| Étiquette | Définition |
|---|---|
| **S1** | Données spécifiant la latitude et la longitude qui peuvent être utilisées pour déterminer l’emplacement précis d’un périphérique. |
| **S2** | Données pouvant être utilisées pour déterminer une zone de géofence définie de manière générale. |


## Plus d’informations

La section suivante fournit des informations détaillées sur l’implémentation de libellés spécifiques.

### C1 {#c1}

Certaines données peuvent uniquement être exportées à partir d’Adobe Experience Cloud dans un formulaire agrégé sans inclure d’identifiants de périphérique ou individuels. Par exemple, les données provenant des réseaux sociaux.

### C2 {#c2}

Certains fournisseurs de données ont des termes dans leurs contrats qui interdisent l&#39;exportation des données d&#39;où elles ont été collectées à l&#39;origine. Par exemple, les contrats de réseau social limitent souvent le transfert des données que vous recevez d’eux. Le libellé C2 est plus restrictif que [C1](#c1), ce qui ne nécessite que l’agrégation et des données anonymes.

### C3 {#c3}

Certains fournisseurs de données ont des termes dans leurs contrats qui interdisent la combinaison ou l&#39;utilisation de ces données avec des informations directement identifiables. Par exemple, les contrats pour les données provenant des réseaux publicitaires, des serveurs d’annonces et des fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques sur l’utilisation de ces données avec des données directement identifiables.

### C4 {#c4}

C4 est l&#39;étiquette la plus restrictive - elle englobe les étiquettes [C5](#c5), [C6](#c6)et [C7](#c7).

### C5 {#c5}

Le ciblage basé sur l’intérêt, ou personnalisation, se produit si les trois conditions suivantes sont remplies : Les données collectées sur le site sont (1) utilisées pour faire des inférences sur les intérêts des utilisateurs, (2) utilisées dans un autre contexte, comme sur un autre site ou une autre application (hors site) ET (3) utilisées pour sélectionner le contenu ou les publicités diffusées en fonction de ces inférences.

La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Différents sites représentent des différents de sorte que l’utilisation de données intersites dans un contexte quelconque diffère de l’original. Les données intersites sont généralement collectées et traitées afin de faire des inférences sur les intérêts des utilisateurs. Par conséquent, l’utilisation de données intersites pour le ciblage des publicités ou du contenu est généralement qualifiée de ciblage basé sur l’intérêt, que la publicité ou le contenu s’affiche sur site ou hors site. Si, par exemple, les données sur site étaient utilisées en combinaison avec les données hors site pour sélectionner la publicité à afficher sur le site d’une entreprise, cette utilisation serait considérée comme un ciblage basé sur les intérêts. Autre exemple : le reciblage des publicités vers des utilisateurs hors site serait probablement considéré comme un ciblage basé sur les intérêts.

L’utilisation de données hors site à elle seule pour le ciblage pourrait également être considérée comme un ciblage basé sur l’intérêt, puisque les données hors site sont généralement collectées et traitées pour faire des inférences sur les intérêts des utilisateurs.

Cependant, le ciblage du contenu ou des publicités utilisant uniquement des données sur site ne peut généralement pas être considéré comme un ciblage basé sur les intérêts. Le ciblage sur site qui n’est pas considéré comme un ciblage basé sur les intérêts est traité comme deux étiquettes distinctes. Plus précisément, l’étiquette C6 traite du ciblage et des  des publicités sur site et s’adresse spécifiquement à la sélection des publicités, aux et aux, et l’étiquette C7 traite de la sélection du contenu sur site, de l’analyse de l’et duciblage du contenu sur site.

En fin de compte, c&#39;est à vous d&#39;interpréter l&#39;étiquette et de savoir comment l&#39;utilisation des données avec cette étiquette est appliquée. À titre de référence, les cadres du CCI et de la DAA sont présentés ci-dessous :

IAB : Personnalisation. Collecte et traitement d&#39;informations sur votre utilisation de ce service pour personnaliser par la suite la publicité et/ou le contenu pour vous dans d&#39;autres , comme sur d&#39;autres sites Web ou applications, au fil du temps. En règle générale, le contenu du site ou de l’application est utilisé pour faire des inférences sur vos intérêts qui éclairent la sélection future de la publicité et/ou du contenu.

DAA : Publicité comportementale en ligne. Collecte de données à partir d’un ordinateur ou d’un périphérique particulier concernant les comportements de consultation Web au fil du temps et sur des sites Web non affiliés afin de prédire les préférences ou les intérêts des utilisateurs pour diffuser de la publicité sur cet ordinateur ou cet appareil en fonction de préférences ou d’intérêts déduits de ces comportements de consultation Web.

### C6 {#c6}

Les publicités sont des messages ou des notifications, y compris du texte et des images, qui apparaissent sur un site Web ou une application et qui sont principalement destinés à promouvoir la vente de biens ou de services. Il vous appartient de déterminer l&#39;objectif de tels messages ou notifications. Les publicités sont distinctes du contenu sur site, couvert par l’étiquette [C7](#c7). Les données avec une étiquette C6 ne peuvent pas être utilisées pour le ciblage des publicités sur site, y compris la sélection et le des publicités sur les sites Web ou les applications de votre entreprise, ni pour mesurer la et l&#39;efficacité de ces publicités. Cela inclut l’utilisation des données précédemment collectées sur le site sur les intérêts des utilisateurs pour sélectionner des publicités, traiter les données sur les publicités affichées, le moment et l’endroit où elles ont été affichées, et savoir si les utilisateurs ont pris des mesures en rapport avec la publicité, comme cliquer sur une publicité ou faire un achat. En règle générale, l’utilisation des préférences d’un utilisateur en fonction de son  sur site, puis de ces préférences dans le ciblage des publicités sur site ne serait pas considérée comme un ciblage basé sur les intérêts (également appelé personnalisation), car elle ne répondait pas aux trois exigences nécessaires au ciblage basé sur les intérêts. _[Voir le libellé C5 pour ces exigences.](#c5)_

En fin de compte, c&#39;est à vous d&#39;interpréter l&#39;étiquette et de savoir comment l&#39;utilisation des données avec cette étiquette est appliquée. À titre de référence, les cadres du CCI et de la DAA sont présentés ci-dessous :

IAB : 3. Sélection de publicité, ,  : La collecte d&#39;informations, combinée avec des informations collectées précédemment, pour sélectionner et diffuser des publicités pour vous, et pour mesurer le et l&#39;efficacité de ces publicités. Cela inclut l&#39;utilisation d&#39;informations collectées précédemment sur vos centres d&#39;intérêt pour sélectionner des publicités, le traitement des données sur les publicités affichées, leur fréquence d&#39;affichage, leur date et leur lieu d&#39;affichage, et si vous avez pris des mesures en rapport avec la publicité, par exemple en cliquant sur une publicité ou en faisant un achat. Cela n’inclut pas la personnalisation, qui est la collecte et le traitement d’informations sur votre utilisation de ce service pour personnaliser ultérieurement la publicité et/ou le contenu pour vous dans d’autres  de, tels que des sites Web ou des applications, au fil du temps.

DAA : La publicité comportementale en ligne n’inclut pas le  de la  des premières parties, les publicitaires ou lesannonces publicitaires, ni la publicité contextuelle (c.-à-d. la publicité basée sur le contenu de la page Web visitée, la visite actuelle d’un consommateur sur une page Web ou un de recherche).

### C7 {#c7}

Le contenu sur site est du texte et des images qui sont conçus pour informer, éduquer ou divertir, et qui ne sont pas créés pour promouvoir la vente de biens ou de services. C’est à vous de déterminer l’objectif du contenu, y compris si le contenu serait considéré comme une publicité native. L’étiquette C7 n’est pas destinée à couvrir les publicités sur site, qui sont couvertes par l’étiquette [C6](#c6). Les données avec une étiquette C7 ne peuvent pas être utilisées pour le ciblage du contenu sur site, y compris la sélection et l&#39; de contenu sur les sites Web ou les applications de votre entreprise, ni pour mesurer l&#39;et l&#39;efficacité de ce contenu. Cela inclut les informations précédemment collectées sur les intérêts des utilisateurs dans un contenu sélectionné, le traitement des données sur le contenu affiché, la fréquence ou la durée d’affichage, le moment et l’emplacement d’affichage, et si les utilisateurs ont pris des mesures relatives au contenu, notamment en cliquant sur le contenu. En règle générale, l’utilisation des préférences d’un utilisateur en fonction de son  sur site, puis de ces préférences dans le ciblage du contenu sur site ne peut pas être considérée comme un ciblage basé sur des intérêts (également appelé personnalisation), puisqu’elle ne répond pas aux trois conditions nécessaires pour un ciblage basé sur des intérêts. _[Voir le libellé C5 pour ces exigences.](#c5)_

En fin de compte, c&#39;est à vous d&#39;interpréter l&#39;étiquette et de savoir comment l&#39;utilisation des données avec cette étiquette est appliquée. À titre de référence, les cadres du CCI et de la DAA sont présentés ci-dessous :

IAB : 4. Sélection de contenu, ,  : Collecte d’informations et combinaison avec des informations collectées précédemment, pour sélectionner et diffuser du contenu pour vous, et pour mesurer l’ et l’efficacité de ce contenu. Cela inclut l’utilisation d’informations collectées précédemment sur vos centres d’intérêt pour sélectionner le contenu, le traitement des données sur le contenu affiché, la fréquence ou la durée d’affichage, le moment et l’emplacement d’affichage du contenu, ainsi que l’action que vous avez entreprise en rapport avec le contenu, par exemple en cliquant sur le contenu. Cela n’inclut pas la personnalisation, c’est-à-dire la collecte et le traitement d’informations sur votre utilisation de ce service pour personnaliser par la suite le contenu et/ou la publicité pour vous dans d’autres  de, tels que des sites Web ou des applications, au fil du temps.

DAA : La publicité comportementale en ligne n’inclut pas le  de la  des premières parties, les publicitaires ou lesannonces publicitaires, ni la publicité contextuelle (c.-à-d. la publicité basée sur le contenu de la page Web visitée, la visite actuelle d’un consommateur sur une page Web ou un de recherche).

### C8 {#c8}

Les données ne peuvent pas être utilisées pour mesurer, comprendre et générer des rapports sur l’utilisation par les utilisateurs des sites ou applications de votre entreprise. Cela n’inclut pas le ciblage basé sur l’intérêt (ciblage inter-sites), qui est la collecte d’informations sur votre utilisation de ce service pour ensuite personnaliser le contenu et/ou la publicité pour vous dans d’autres , c’est-à-dire sur d’autres services, tels que des sites Web ou des applications, au fil du temps.

### C9 {#c9}

Certains contrats prévoient des interdictions explicites sur l&#39;utilisation des données pour la science des données. Parfois, ces termes sont rédigés en des termes qui interdisent l’utilisation de données pour l’intelligence artificielle (AI), l’apprentissage automatique (ML) ou la modélisation.