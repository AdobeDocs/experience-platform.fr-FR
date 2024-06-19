---
solution: Experience Platform
title: Groupe de champs de schéma de contenu et de préférences
description: Découvrez le groupe de champs de schéma Contenus et Préférences .
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL Consentements et préférences] groupe de champs

[!UICONTROL Consentements et préférences] est un groupe de champs standard pour la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) qui capture les informations de consentement et de préférence pour un client individuel.

>[!NOTE]
>
>Ce groupe de champs n’étant compatible qu’avec [!DNL XDM Individual Profile], il ne peut pas être utilisé pour [!DNL XDM ExperienceEvent] schémas. Si vous souhaitez inclure des données de consentement et de préférence dans votre schéma d’événement d’expérience, ajoutez la variable [[!UICONTROL Consentement pour la confidentialité, la personnalisation et les préférences marketing] type de données](../../data-types/consents.md) au schéma via l’utilisation d’une [groupe de champs personnalisés](../../ui/resources/field-groups.md#create) au lieu de .

## Structure du groupe de champs {#structure}

La variable [!UICONTROL Consentements et préférences] Le groupe de champs fournit un champ de type objet unique, `consents`, pour capturer les informations sur le consentement et les préférences. Ce champ étend la propriété [[!UICONTROL Consentement pour la confidentialité, la personnalisation et les préférences marketing] type de données](../../data-types/consents.md), suppression de la variable `adID` et ajouter un `idSpecific` champ map .

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consultez le guide sur la [exploration des ressources XDM](../../ui/explore.md) pour savoir comment rechercher une ressource XDM et examiner sa structure dans l’interface utilisateur de Platform.

Le fichier JSON suivant illustre un exemple du type de données que la variable [!UICONTROL Consentements et préférences] groupe de champs peut traiter. Pour plus d’informations sur l’utilisation de la plupart des champs fournis par le groupe de champs, consultez le guide sur la [Type de données Consentements et Préférences](../../data-types/consents.md). Les sous-sections ci-dessous portent sur les attributs uniques que le groupe de champs ajoute au type de données.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Vous pouvez générer des exemples de données JSON pour tout schéma XDM que vous définissez dans Experience Platform afin de mieux visualiser la manière dont vos données de consentement et de préférence client doivent être mappées. Pour plus d’informations, consultez la documentation suivante :
>
>* [Génération d’exemples de données dans l’interface utilisateur](../../ui/sample.md)
>* [Génération d’exemples de données dans l’API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` peut être utilisé lorsqu’un consentement ou une préférence spécifique ne s’applique pas de manière universelle à un client, mais qu’il est limité à un seul appareil ou à un seul identifiant. Par exemple, un client peut refuser de recevoir des emails à une adresse, tout en autorisant éventuellement l’envoi d’emails à une autre.

>[!IMPORTANT]
>
>Consentements et préférences au niveau du canal (c.-à-d. ceux fournis sous `consents` en dehors de `idSpecific`) s’appliquent à tous les identifiants de ce canal. Par conséquent, tous les consentements et préférences au niveau du canal influent directement sur le respect des paramètres équivalents d’ID ou spécifiques à l’appareil :
>
>* Si le client s’est désabonné au niveau du canal, tous les consentements ou préférences équivalents dans `idSpecific` sont ignorées.
>* Si le consentement ou la préférence au niveau du canal n’est pas définie ou si le client s’est inscrit, alors les consentements ou préférences équivalents dans `idSpecific` sont honorés.

Chaque clé dans la variable `idSpecific` représente un espace de noms d’identité spécifique reconnu par le service Adobe Experience Platform Identity. Bien que vous puissiez définir vos propres espaces de noms personnalisés pour classer différents identifiants, il est recommandé d’utiliser l’un des espaces de noms standard fournis par Identity Service pour réduire les tailles de stockage pour Real-Time Customer Profile. Pour plus d’informations sur les espaces de noms d’identité, voir [présentation de l’espace de noms d’identité](../../../identity-service/features/namespaces.md) dans la documentation d’Identity Service.

Les clés de chaque objet d’espace de noms représentent les valeurs d’identité uniques pour lesquelles le client a défini des préférences. Chaque valeur d’identité peut contenir un ensemble complet de consentements et de préférences, formatés de la même manière que `consents`.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

Within `marketing` objets fournis dans la variable `idSpecific` , `any` et `preferred` ne sont pas pris en charge. Ces champs ne peuvent être configurés qu’au niveau de l’utilisateur. En outre, la variable `idSpecific` préférences marketing pour `email`, `sms`, et `push` ne pas prendre en charge `subscriptions` des champs.

Il existe également un consentement qui ne peut être fourni que dans la variable `idSpecific` section : `adID`. Ce champ est traité dans la sous-section ci-dessous.

#### `adID`

La variable `adID` le consentement représente le consentement du client pour savoir si un ID d’annonceur (IDFA ou GAID) peut être utilisé pour lier le client à l’ensemble des applications de cet appareil. Cette valeur ne peut être configurée que sous le `ECID` espace de noms d’identité dans la variable `idSpecific` et ne peuvent pas être définies pour d’autres espaces de noms ou au niveau de l’utilisateur pour ce groupe de champs.

```json
"idSpecific": {
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Vous ne devez pas définir cette valeur directement, car le SDK Adobe Experience Platform Mobile la définit automatiquement le cas échéant.

## Ingestion de données à l’aide du groupe de champs {#ingest}

Pour utiliser la variable [!UICONTROL Consentements et préférences] pour ingérer des données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma qui contient ce groupe de champs.

Voir le tutoriel sur [création d’un schéma dans l’interface utilisateur](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment affecter des groupes de champs à des champs. Une fois que vous avez créé un schéma contenant un champ avec la propriété [!UICONTROL Consentements et préférences] groupe de champs, voir la section sur [création d’un jeu de données](../../../catalog/datasets/user-guide.md#create) dans le guide d’utilisation du jeu de données, en suivant les étapes de création d’un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-Time Customer Profile], vous devez créer une [!DNL Profile]Schéma activé en fonction de la variable [!DNL XDM Individual Profile] qui contient la classe [!UICONTROL Consentements et préférences] groupe de champs. Le jeu de données que vous créez à partir de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux tutoriels liés ci-dessus pour connaître les étapes spécifiques liées à [!DNL Real-Time Customer Profile] conditions requises pour les schémas et les jeux de données.
>
>En outre, vous devez également vous assurer que vos stratégies de fusion sont configurées pour prioriser le ou les jeux de données qui contiennent les dernières données de consentement et de préférence, afin que les profils client soient correctement mis à jour. Consultez la présentation sur [stratégies de fusion](../../../rtcdp/profile/merge-policies.md) pour plus d’informations.

## Gestion des modifications du consentement et des préférences

Lorsqu’un client modifie ses consentements ou ses préférences sur votre site web, ces modifications doivent être collectées et appliquées immédiatement à l’aide de la variable [SDK Web Adobe Experience Platform](../../../web-sdk/commands/setconsent.md). Si un client choisit de ne pas participer à la collecte de données, toute collecte de données doit immédiatement cesser. Si un client s’exclut de la personnalisation, aucune personnalisation ne doit être présente sur la page suivante qu’il consulte.

## Étapes suivantes

Ce document couvrait la structure et l’utilisation de la fonction [!UICONTROL Consentements et préférences] groupe de champs. Pour plus d’informations sur les autres champs fournis par le groupe de champs, consultez le document sur la [[!UICONTROL Consentement pour la confidentialité, la personnalisation et les préférences marketing] type de données](../../data-types/consents.md).
