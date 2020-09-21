---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: Annexe de développement du registre des schémas
description: Ce document fournit des informations supplémentaires relatives au travail avec l’API Schema Registry.
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 69%

---


# Annexe

This document provides supplemental information related to working with the [!DNL Schema Registry] API.

## Mode de compatibilité

[!DNL Experience Data Model] (XDM) est une spécification documentée publiquement, pilotée par l&#39;Adobe pour améliorer l&#39;interopérabilité, l&#39;expressivité et la puissance des expériences numériques. Adobe conserve le code source et les définitions formelles XDM dans un [projet open source sur GitHub](https://github.com/adobe/xdm/). Ces définitions sont écrites dans la notation standard XDM, et utilisent JSON-LD (JavaScript Object Notation for Linked Data) et le schéma JSON comme grammaire de définition des schémas XDM.

Lorsque vous examinez les définitions XDM formelles dans le référentiel public, vous pouvez voir que le XDM standard est différent de ce que vous voyez dans Adobe Experience Platform. What you are seeing in [!DNL Experience Platform] is called Compatibility Mode, and it provides a simple mapping between standard XDM and the way it is used within [!DNL Platform].

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

La plupart des [!DNL Experience Platform] services, y compris [!DNL Catalog]les services, [!DNL Data Lake]et [!DNL Real-time Customer Profile] , sont utilisés [!DNL Compatibility Mode] à la place de XDM standard. L’ [!DNL Schema Registry] API utilise également [!DNL Compatibility Mode]et les exemples de ce document s’affichent tous à l’aide [!DNL Compatibility Mode].

It is worthwhile to know that a mapping takes place between standard XDM and the way it is operationalized in [!DNL Experience Platform], but it should not affect your use of [!DNL Platform] services.

The open source project is available to you, but when it comes to interacting with resources through the [!DNL Schema Registry], the API examples in this document provide the best practices you should know and follow.