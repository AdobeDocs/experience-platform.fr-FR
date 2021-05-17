---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; registre de schémas ; compatibilité ; compatibilité ; mode de compatibilité ; mode de compatibilité ; type de champ ; types de champ ;
solution: Experience Platform
title: Annexe du Guide de l'API du registre des schémas
description: Ce document fournit des informations supplémentaires relatives au travail avec l’API Schema Registry.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: dcfdc9c479e8a77296f7cb0bf9f5bb36e9261b75
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 47%

---

# Annexe du guide de l&#39;API du registre de schémas

Ce document fournit des informations supplémentaires sur l&#39;utilisation de l&#39;API [!DNL Schema Registry].

## Utilisation des paramètres de requête {#query}

[!DNL Schema Registry] prend en charge l&#39;utilisation de paramètres de requête pour la page et le filtrage des résultats lors de la mise en vente des ressources.

>[!NOTE]
>
>Lorsque vous combinez plusieurs paramètres de requête, ceux-ci doivent être séparés par des esperluettes (`&`).

### Pagination {#paging}

Les paramètres de requête les plus courants pour la pagination sont les suivants :

| Paramètre | Description |
| --- | --- |
| `start` | Indiquez où doivent commencer les résultats répertoriés. Cette valeur peut être obtenue à partir de l&#39;attribut `_page.next` d&#39;une réponse de liste et utilisée pour accéder à la page de résultats suivante. Si la valeur `_page.next` est nulle, aucune page supplémentaire n’est disponible. |
| `limit` | Limite le nombre de ressources renvoyé. Exemple : `limit=5` renverra une liste de cinq ressources. |
| `orderby` | Triez les résultats en fonction d’une propriété spécifique. Exemple : `orderby=title` triera les résultats par titre dans l’ordre croissant (A-Z). Si vous Ajoutez un `-` avant la valeur du paramètre (`orderby=-title`), les éléments sont triés par titre dans l’ordre décroissant (Z-A). |

### Filtrage {#filtering}

Vous pouvez filtrer les résultats en utilisant le paramètre `property`, qui est utilisé pour appliquer un opérateur spécifique à une propriété JSON donnée dans les ressources récupérées. Les opérateurs pris en charge sont les suivants :

| Opérateur | Description | Exemple |
| --- | --- | --- |
| `==` | Filtres selon si la propriété est égale à la valeur fournie. | `property=title==test` |
| `!=` | Filtres selon si la propriété n’est pas égale à la valeur fournie. | `property=title!=test` |
| `<` | Filtres selon si la propriété est inférieure à la valeur fournie. | `property=version<5` |
| `>` | Filtres selon si la propriété est supérieure à la valeur fournie. | `property=version>5` |
| `<=` | Filtres selon si la propriété est inférieure ou égale à la valeur fournie. | `property=version<=5` |
| `>=` | Filtres selon si la propriété est supérieure ou égale à la valeur fournie. | `property=version>=5` |
| `~` | Filtres selon si la propriété correspond à une expression régulière fournie. | `property=title~test$` |
| (Aucun) | Le fait de spécifier uniquement le nom de la propriété renvoie uniquement les entrées où la propriété existe. | `property=title` |

>[!TIP]
>
>Vous pouvez utiliser le paramètre `property` pour filtrer les groupes de champs de schéma selon leur classe compatible. Par exemple, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` renvoie uniquement les groupes de champs compatibles avec la classe [!DNL XDM Individual Profile].

## Mode de compatibilité {#compatibility}

[!DNL Experience Data Model] (XDM) est une spécification documentée publiquement, pilotée par l&#39;Adobe pour améliorer l&#39;interopérabilité, l&#39;expressivité et la puissance des expériences numériques. Adobe conserve le code source et les définitions formelles XDM dans un [projet open source sur GitHub](https://github.com/adobe/xdm/). Ces définitions sont écrites dans la notation standard XDM, et utilisent JSON-LD (JavaScript Object Notation for Linked Data) et le schéma JSON comme grammaire de définition des schémas XDM.

Lorsque vous examinez les définitions XDM formelles dans le référentiel public, vous pouvez voir que le XDM standard est différent de ce que vous voyez dans Adobe Experience Platform. Ce que vous voyez dans [!DNL Experience Platform] s&#39;appelle Mode de compatibilité et fournit un mappage simple entre XDM standard et la façon dont il est utilisé dans [!DNL Platform].

### Fonctionnement du mode de compatibilité

Le mode de compatibilité permet au modèle XDM JSON-LD de fonctionner avec une infrastructure de données existante en modifiant les valeurs du XDM standard tout en conservant la même sémantique. Il utilise une structure JSON imbriquée en affichant les schémas dans un format de type arbre.

La principale différence que vous noterez entre le XDM standard et le mode de compatibilité est la suppression du préfixe « xdm: » devant les noms des champs.

Le tableau ci-dessous contient une comparaison côte à côte affichant les champs associés à la date de naissance (dont les attributs « description » ont été supprimés) aux formats XDM standard et Mode de compatibilité. Notez que les champs Mode de compatibilité incluent une référence au champ XDM et à son type de données dans les attributs « meta:xdmField » et « meta:xdmType ».

<table>
  <th>XDM standard</th>
  <th>Mode de compatibilité</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
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
  <pre class="JSON language-JSON hljs">
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

La plupart des services [!DNL Experience Platform], y compris [!DNL Catalog], [!DNL Data Lake] et [!DNL Real-time Customer Profile] utilisent [!DNL Compatibility Mode] au lieu de XDM standard. L&#39;API [!DNL Schema Registry] utilise également [!DNL Compatibility Mode] et les exemples de ce document sont tous affichés à l&#39;aide de [!DNL Compatibility Mode].

Il est intéressant de savoir qu&#39;un mappage a lieu entre XDM standard et la façon dont il est opérationnel dans [!DNL Experience Platform], mais il ne devrait pas affecter votre utilisation des services [!DNL Platform].

Le projet open source est à votre disposition, mais lorsqu&#39;il s&#39;agit d&#39;interagir avec des ressources par le biais de [!DNL Schema Registry], les exemples d&#39;API de ce document fournissent les meilleures pratiques que vous devez connaître et suivre.
