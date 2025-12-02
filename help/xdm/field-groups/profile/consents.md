---
solution: Experience Platform
title: Groupe de champs de schéma Consentements et préférences
description: En savoir plus sur le groupe de champs de schéma Consentements et Préférences .
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] le groupe de champs

[!UICONTROL Consents and Preferences] est un groupe de champs standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) qui recueille les informations de consentement et de préférence d’un client individuel.

>[!NOTE]
>
>Ce groupe de champs n’étant compatible qu’avec [!DNL XDM Individual Profile], il ne peut pas être utilisé pour les schémas [!DNL XDM ExperienceEvent]. Si vous souhaitez inclure des données de consentement et de préférence dans votre schéma d’événement d’expérience, ajoutez le type de données [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] au schéma](../../data-types/consents.md) à l’aide d’un [groupe de champs personnalisé](../../ui/resources/field-groups.md#create) à la place.

## Structure du groupe de champs {#structure}

Le groupe de champs [!UICONTROL Consents and Preferences] fournit un champ de type objet unique, `consents`, pour capturer les informations de consentement et de préférence. Ce champ étend le type de données [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]](../../data-types/consents.md) en supprimant le champ `adID` et en ajoutant un champ de mappage `idSpecific`.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consultez le guide sur l’[exploration des ressources XDM](../../ui/explore.md) vers pour savoir comment rechercher n’importe quelle ressource XDM et inspecter sa structure dans l’interface utilisateur d’Experience Platform.

Le fichier JSON suivant illustre un exemple du type de données que le groupe de champs [!UICONTROL Consents and Preferences] peut traiter. Pour plus d’informations sur l’utilisation de la plupart des champs fournis par le groupe de champs, reportez-vous au guide sur le [type de données Consentements et Préférences](../../data-types/consents.md). Les sous-sections ci-dessous portent sur les attributs uniques que le groupe de champs ajoute au type de données.

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
>Vous pouvez générer des exemples de données JSON pour tout schéma XDM défini dans Experience Platform afin de visualiser plus facilement la manière dont vos données de consentement et de préférence client doivent être mappées. Pour plus d’informations, consultez la documentation suivante :
>
>* [Générer des exemples de données dans l’interface utilisateur](../../ui/sample.md)
>* [Générer des exemples de données dans l’API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` peut être utilisé lorsqu’un consentement ou une préférence spécifique ne s’applique pas universellement à un client ou une cliente, mais se limite à un seul appareil ou ID. Par exemple, un client peut refuser de recevoir des e-mails à une adresse, tout en autorisant potentiellement la réception d’e-mails à une autre adresse.

>[!IMPORTANT]
>
>Les consentements et préférences au niveau du canal (c’est-à-dire ceux fournis sous `consents` en dehors de `idSpecific`) s’appliquent à tous les identifiants de ce canal. Par conséquent, tous les consentements et préférences au niveau du canal affectent directement le respect de paramètres équivalents spécifiques à l’ID ou à l’appareil :
>
>* Si le client s’est désabonné au niveau du canal, tous les consentements ou préférences équivalents dans `idSpecific` sont ignorés.
>* Si le consentement ou la préférence au niveau du canal n’est pas défini, ou si le client a choisi, les consentements ou préférences équivalents dans `idSpecific` sont respectés.

Chaque clé de l’objet `idSpecific` représente un espace de noms d’identité spécifique reconnu par le service d’identités Adobe Experience Platform. Bien que vous puissiez définir vos propres espaces de noms personnalisés pour classer différents identifiants, il est recommandé d’utiliser l’un des espaces de noms standard fournis par Identity Service pour réduire les tailles de stockage pour le profil client en temps réel. Pour plus d’informations sur les espaces de noms d’identité, consultez la [&#x200B; présentation des espaces de noms d’identité &#x200B;](/help/identity-service/features/namespaces.md) dans la documentation d’Identity Service.

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

Dans `marketing` objets fournis dans la section `idSpecific` , les champs `any` et `preferred` ne sont pas pris en charge. Ces champs ne peuvent être configurés qu’au niveau de l’utilisateur. En outre, les préférences marketing `idSpecific` pour `email`, `sms` et `push` ne prennent pas en charge les champs `subscriptions`.

Un consentement ne peut également être fourni que dans la section `idSpecific` : `adID`. Ce champ est traité dans la sous-section ci-dessous.

#### `adID`

Le consentement `adID` représente le consentement du client pour savoir si un ID d’annonceur (IDFA ou GAID) peut être utilisé pour lier le client dans les applications sur cet appareil. Cette valeur peut uniquement être configurée sous l’espace de noms d’identité `ECID` dans la section `idSpecific` et ne peut pas être définie pour d’autres espaces de noms ou au niveau de l’utilisateur pour ce groupe de champs.

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
>Il n’est pas prévu que vous définissiez directement cette valeur, car Adobe Experience Platform Mobile SDK la définit automatiquement le cas échéant.

## Ingestion de données à l’aide du groupe de champs {#ingest}

Pour utiliser le groupe de champs [!UICONTROL Consents and Preferences] afin d’ingérer les données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma contenant ce groupe de champs.

Consultez le tutoriel sur la [création d’un schéma dans l’interface utilisateur](https://www.adobe.com/go/xdm-schema-editor-tutorial-en_fr) pour savoir comment affecter des groupes de champs à des champs. Une fois que vous avez créé un schéma contenant un champ avec le groupe de champs [!UICONTROL Consents and Preferences], reportez-vous à la section sur la [création d’un jeu de données](/help/catalog/datasets/user-guide.md#create) dans le guide d’utilisation des jeux de données, en suivant les étapes de création d’un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-Time Customer Profile], vous devez créer un schéma activé pour [!DNL Profile] basé sur la classe [!DNL XDM Individual Profile] qui contient le groupe de champs [!UICONTROL Consents and Preferences]. Le jeu de données que vous créez à partir de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux tutoriels liés ci-dessus pour obtenir des instructions spécifiques relatives aux exigences en matière de [!DNL Real-Time Customer Profile] pour les schémas et les jeux de données.
>
>En outre, vous devez également vous assurer que vos politiques de fusion sont configurées pour donner la priorité au(x) jeu(x) de données contenant les dernières données de consentement et de préférence, afin que les profils clients soient correctement mis à jour. Pour plus d’informations, consultez la présentation des [politiques de fusion](/help/rtcdp/profile/merge-policies.md).

## Gérer les modifications de consentement et de préférence

Lorsqu’un client modifie ses consentements ou ses préférences sur votre site web, ces modifications doivent être collectées et immédiatement appliquées en définissant le consentement dans la bibliothèque de collecte de données utilisée. Si un client se désinscrit de la collecte de données, toute collecte de données doit immédiatement cesser. Si un client ou une cliente désactive la personnalisation, aucune personnalisation ne devrait être présente sur la page suivante qu’il ou elle charge. Voir [`setConsent`](/help/collection/js/commands/setconsent.md) à l’aide de la bibliothèque JavaScript ou l’action [[!UICONTROL Set consent]](/help/tags/extensions/client/web-sdk/actions/set-consent.md) à l’aide de l’extension de balise Web SDK.

## Étapes suivantes

Ce document couvrait la structure et l’utilisation du groupe de champs [!UICONTROL Consents and Preferences]. Pour plus d’informations sur les autres champs fournis par le groupe de champs , consultez le document sur le type de données [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] &#x200B;](../../data-types/consents.md) .
