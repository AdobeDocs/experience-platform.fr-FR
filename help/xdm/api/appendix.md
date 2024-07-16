---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;compatibilité;compatibilité;mode de compatibilité;mode de compatibilité;type de champ;types de champ;type de champ;registre des schémas;compatibilité
solution: Experience Platform
title: Annexe du guide de l’API Schema Registry
description: Ce document fournit des informations supplémentaires relatives au travail avec l’API Schema Registry.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 28891cf37dc9ffcc548f4c0565a77f62432c0b44
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 28%

---

# Annexe du guide de l’API Schema Registry

Ce document fournit des informations supplémentaires sur l’utilisation de l’API [!DNL Schema Registry].

## Utilisation des paramètres de requête {#query}

[!DNL Schema Registry] prend en charge l’utilisation de paramètres de requête pour la page et le filtrage des résultats lors de la liste des ressources.

>[!NOTE]
>
>Lorsque vous combinez plusieurs paramètres de requête, ceux-ci doivent être séparés par des esperluettes (`&`).

### Pagination {#paging}

Les paramètres de requête les plus courants pour la pagination sont les suivants :

| Paramètre | Description |
| --- | --- |
| `orderby` | Triez les résultats en fonction d&#39;une propriété spécifique. Exemple : `orderby=title` triera les résultats par titre dans l’ordre croissant (A-Z). L’ajout de `-` avant la valeur du paramètre (`orderby=-title`) triera les éléments par titre dans l’ordre décroissant (Z-A). |
| `limit` | Lorsqu’il est utilisé conjointement avec un paramètre `orderby` , `limit` limite le nombre maximal d’éléments à renvoyer pour une requête donnée. Ce paramètre ne peut pas être utilisé sans paramètre `orderby` présent.<br><br>Le paramètre `limit` spécifie un entier positif (entre `0` et `500`) sous la forme d’un *indice* quant au nombre maximal d’éléments à renvoyer. Par exemple, `limit=5` renvoie uniquement cinq ressources dans la liste. Cependant, cette valeur n’est pas strictement respectée. La taille réelle de la réponse peut être plus petite ou plus grande, en raison de la nécessité de fournir l’opération fiable du paramètre `start`, le cas échéant. |
| `start` | Lorsqu&#39;il est utilisé conjointement avec un paramètre `orderby`, `start` indique où la liste sous-définie d&#39;éléments doit commencer. Ce paramètre ne peut pas être utilisé sans paramètre `orderby` présent. Cette valeur peut être obtenue à partir de l’attribut `_page.next` d’une réponse de liste et utilisée pour accéder à la page de résultats suivante. Si la valeur `_page.next` est nulle, aucune page supplémentaire n’est disponible.<br><br>En règle générale, ce paramètre est omis afin d’obtenir la première page de résultats. Ensuite, `start` doit être défini sur la valeur maximale de la propriété de tri principale du champ `orderby` reçu dans la page précédente. La réponse de l’API renvoie ensuite des entrées commençant par celles dont la propriété de tri principale est `orderby` strictement supérieure (pour l’ordre ascendant) ou strictement inférieure (pour l’ordre descendant) à la valeur spécifiée.<br><br>Par exemple, si le paramètre `orderby` est défini sur `orderby=name,firstname`, le paramètre `start` contiendra une valeur pour la propriété `name`. Dans ce cas, si vous souhaitez afficher les 20 entrées suivantes d’une ressource immédiatement après le nom &quot;Miller&quot;, vous utiliserez : `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filtrage {#filtering}

Vous pouvez filtrer les résultats à l’aide du paramètre `property` utilisé pour appliquer un opérateur spécifique à une propriété JSON donnée dans les ressources récupérées. Les opérateurs pris en charge sont les suivants :

| Opérateur | Description | Exemple |
| --- | --- | --- |
| `==` | Filtre selon si la propriété est égale à la valeur fournie. | `property=title==test` |
| `!=` | Filtre selon si la propriété n’est pas égale à la valeur fournie. | `property=title!=test` |
| `<` | Filtre selon si la propriété est inférieure à la valeur fournie. | `property=version<5` |
| `>` | Filtre selon si la propriété est supérieure ou non à la valeur fournie. | `property=version>5` |
| `<=` | Filtre selon si la propriété est inférieure ou égale à la valeur fournie. | `property=version<=5` |
| `>=` | Filtre selon si la propriété est supérieure ou égale à la valeur fournie. | `property=version>=5` |
| (Aucun) | Le fait de spécifier uniquement le nom de la propriété renvoie uniquement les entrées où la propriété existe. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>Vous pouvez utiliser le paramètre `property` pour filtrer les groupes de champs de schéma selon leur classe compatible. Par exemple, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` renvoie uniquement les groupes de champs compatibles avec la classe [!DNL XDM Individual Profile].

## Mode de compatibilité {#compatibility}

[!DNL Experience Data Model] (XDM) est une spécification documentée publiquement, pilotée par l’Adobe pour améliorer l’interopérabilité, l’expressivité et la puissance des expériences numériques. Adobe conserve le code source et les définitions formelles XDM dans un [projet open source sur GitHub](https://github.com/adobe/xdm/). Ces définitions sont écrites dans la notation standard XDM, et utilisent JSON-LD (JavaScript Object Notation for Linked Data) et le schéma JSON comme grammaire de définition des schémas XDM.

Lorsque vous examinez les définitions XDM formelles dans le référentiel public, vous pouvez voir que le XDM standard est différent de ce que vous voyez dans Adobe Experience Platform. Ce que vous voyez dans [!DNL Experience Platform] s’appelle Mode de compatibilité et fournit un mappage simple entre le XDM standard et la manière dont il est utilisé dans [!DNL Platform].

### Fonctionnement du mode de compatibilité

Le mode de compatibilité permet au modèle XDM JSON-LD de fonctionner avec une infrastructure de données existante en modifiant les valeurs du XDM standard tout en conservant la même sémantique. Il utilise une structure JSON imbriquée en affichant les schémas dans un format de type arbre.

La principale différence que vous noterez entre le XDM standard et le mode de compatibilité est la suppression du préfixe « xdm: » devant les noms des champs.

Le tableau ci-dessous contient une comparaison côte à côte affichant les champs associés à la date de naissance (dont les attributs « description » ont été supprimés) aux formats XDM standard et Mode de compatibilité. Notez que les champs Mode de compatibilité incluent une référence au champ XDM et à son type de données dans les attributs « meta:xdmField » et « meta:xdmType ».

<table style="table-layout:auto">
  <th>XDM standard</th>
  <th>Mode de compatibilité</th>
  <tr>
  <td>
  <pre class=" language-json">
{
  "xdm:birthDate": {
    "title" : "Date de naissance",
    "type": "string",
    "format": "date"
  },
  "xdm:birthDayAndMonth": {
    "title" : "Date de naissance",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9][0-9]"
  },
  "xdm:birthYear": {
    "title" : "Année de naissance",
    "type": "integer",
    "minimum" : 1,
    "maximum" : 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "birthDate": {
    "title" : "Date de naissance",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:birthDate",
    "meta:xdmType": "date"
  },
  "birthDayAndMonth": {
    "title" : "Date de naissance",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9][0-9]",
    "meta:xdmField": "xdm:birthDayAndMonth",
    "meta:xdmType": "string"
  },
  "birthYear": {
    "title" : "Année de naissance",
    "type": "integer",
    "minimum" : 1,
    "maximum" : 32767,
    "meta:xdmField": "xdm:birthYear",
    "meta:xdmType": "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### Pourquoi le mode de compatibilité est-il nécessaire ?

Adobe Experience Platform est conçu de manière à fonctionner avec plusieurs solutions et services possédant chacun leurs propres défis et limitations techniques (par exemple, la manière dont certaines technologies traitent les caractères spéciaux). Le mode de compatibilité a été développé dans le but de surpasser ces limites.

La plupart des services [!DNL Experience Platform], y compris [!DNL Catalog], [!DNL Data Lake] et [!DNL Real-Time Customer Profile] utilisent [!DNL Compatibility Mode] au lieu de XDM standard. L’API [!DNL Schema Registry] utilise également [!DNL Compatibility Mode] et les exemples de ce document s’affichent tous à l’aide de [!DNL Compatibility Mode].

Il est intéressant de savoir qu’un mappage a lieu entre le XDM standard et la manière dont il est opérationnalisé dans [!DNL Experience Platform], mais il ne doit pas affecter votre utilisation des services [!DNL Platform].

Le projet open source est à votre disposition, mais lorsqu’il s’agit d’interagir avec des ressources via [!DNL Schema Registry], les exemples d’API de ce document fournissent les bonnes pratiques que vous devez connaître et suivre.
