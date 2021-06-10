---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;compatibilité;compatibilité;mode de compatibilité;mode de compatibilité;type de champ;types de champ;type de champ;registre des schémas;compatibilité
solution: Experience Platform
title: Annexe du guide de l’API Schema Registry
description: Ce document fournit des informations supplémentaires relatives au travail avec l’API Schema Registry.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: d70f297130ec04dd799d60c70b95777ee79bbfef
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 48%

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
| `start` | Spécifiez où commencer les résultats répertoriés. Cette valeur peut être obtenue à partir de l’attribut `_page.next` d’une réponse de liste et utilisée pour accéder à la page de résultats suivante. Si la valeur `_page.next` est nulle, aucune page supplémentaire n’est disponible. |
| `limit` | Limite le nombre de ressources renvoyé. Exemple : `limit=5` renverra une liste de cinq ressources. |
| `orderby` | Triez les résultats en fonction d’une propriété spécifique. Exemple : `orderby=title` triera les résultats par titre dans l’ordre croissant (A-Z). L’ajout d’un `-` devant la valeur du paramètre (`orderby=-title`) triera les éléments par titre dans l’ordre décroissant (Z-A). |

{style=&quot;table-layout:auto&quot;}

### Filtrage {#filtering}

Vous pouvez filtrer les résultats à l’aide du paramètre `property`, utilisé pour appliquer un opérateur spécifique à une propriété JSON donnée dans les ressources récupérées. Les opérateurs pris en charge sont les suivants :

| Opérateur | Description | Exemple |
| --- | --- | --- |
| `==` | Filtre selon si la propriété est égale à la valeur fournie. | `property=title==test` |
| `!=` | Filtre selon si la propriété n’est pas égale à la valeur fournie. | `property=title!=test` |
| `<` | Filtre selon si la propriété est inférieure à la valeur fournie. | `property=version<5` |
| `>` | Filtre selon si la propriété est supérieure ou non à la valeur fournie. | `property=version>5` |
| `<=` | Filtre selon si la propriété est inférieure ou égale à la valeur fournie. | `property=version<=5` |
| `>=` | Filtre selon si la propriété est supérieure ou égale à la valeur fournie. | `property=version>=5` |
| `~` | Filtre selon si la propriété correspond à une expression régulière fournie. | `property=title~test$` |
| (Aucun) | Le fait de spécifier uniquement le nom de la propriété renvoie uniquement les entrées où la propriété existe. | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Vous pouvez utiliser le paramètre `property` pour filtrer les groupes de champs de schéma selon leur classe compatible. Par exemple, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` renvoie uniquement les groupes de champs compatibles avec la classe [!DNL XDM Individual Profile].

## Mode de compatibilité {#compatibility}

[!DNL Experience Data Model] (XDM) est une spécification documentée publiquement, conçue par Adobe pour améliorer l’interopérabilité, l’expressivité et la puissance des expériences numériques. Adobe conserve le code source et les définitions formelles XDM dans un [projet open source sur GitHub](https://github.com/adobe/xdm/). Ces définitions sont écrites dans la notation standard XDM, et utilisent JSON-LD (JavaScript Object Notation for Linked Data) et le schéma JSON comme grammaire de définition des schémas XDM.

Lorsque vous examinez les définitions XDM formelles dans le référentiel public, vous pouvez voir que le XDM standard est différent de ce que vous voyez dans Adobe Experience Platform. Ce que vous voyez dans [!DNL Experience Platform] s’appelle Mode de compatibilité et fournit un mappage simple entre le XDM standard et la manière dont il est utilisé dans [!DNL Platform].

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
              "title": "Birth Date",
              "type": "string",
              "format": "date",
          },
          "xdm:birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767
        }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
        {
          "birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
              "meta:xdmField": "xdm:birthDate",
              "meta:xdmType": "date"
          },
          "birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField": "xdm:birthDayAndMonth",
              "meta:xdmType": "string"
          },
          "birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767,
              "meta:xdmField": "xdm:birthYear",
              "meta:xdmType": "short"
        }
      </pre>
  </td>
  </tr>
</table>

### Pourquoi le mode de compatibilité est-il nécessaire ?

Adobe Experience Platform est conçu de manière à fonctionner avec plusieurs solutions et services possédant chacun leurs propres défis et limitations techniques (par exemple, la manière dont certaines technologies traitent les caractères spéciaux). Le mode de compatibilité a été développé dans le but de surpasser ces limites.

La plupart des [!DNL Experience Platform] services, y compris [!DNL Catalog], [!DNL Data Lake] et [!DNL Real-time Customer Profile] utilisent [!DNL Compatibility Mode] au lieu de XDM standard. L’API [!DNL Schema Registry] utilise également [!DNL Compatibility Mode] et les exemples de ce document sont tous affichés à l’aide de [!DNL Compatibility Mode].

Il est intéressant de savoir qu’un mappage a lieu entre le XDM standard et la manière dont il est opérationnalisé dans [!DNL Experience Platform], mais il ne devrait pas affecter votre utilisation des services [!DNL Platform].

Le projet open source est à votre disposition, mais lorsqu’il s’agit d’interagir avec des ressources via [!DNL Schema Registry], les exemples d’API de ce document fournissent les bonnes pratiques que vous devez connaître et suivre.
