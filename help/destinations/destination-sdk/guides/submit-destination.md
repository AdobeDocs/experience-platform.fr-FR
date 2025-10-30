---
description: Cette page fournit toutes les informations dont vous avez besoin pour envoyer une destination personnalisée pour révision lorsqu’elle est créée à l’aide de Destination SDK.
title: Envoyer une destination personnalisée pour révision
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 35%

---

# Envoyer une destination personnalisée pour révision

## Vue d’ensemble {#overview}

>[!IMPORTANT]
>
>* Le processus documenté ici n’est nécessaire que pour les partenaires qui soumettent des destinations standardisées (publiques). Si vous créez une destination privée pour votre propre usage, vous n’avez pas besoin de produire et de partager ces ressources avec Adobe.
>
>* Le temps de réponse standard d’Adobe pour examiner les demandes de publication de destination est de cinq jours ouvrables.
>
>* Si l’équipe d’Adobe vous demande d’apporter des mises à jour à vos configurations après votre envoi initial, vous devez envoyer une autre demande de publication de destination après avoir effectué les mises à jour.
>
>* Même après la mise en ligne de la destination dans le catalogue Experience Platform, si vous devez apporter des mises à jour à vos configurations, vous devez envoyer une nouvelle demande de publication de destination pour que les mises à jour soient répercutées dans les configurations.
>
>* La chronologie de révision et les artefacts requis sont les mêmes pour les nouvelles destinations et les destinations existantes que vous mettez à jour.

Pour que votre destination puisse être publiée dans le [catalogue des destinations Experience Platform](/help/destinations/catalog/overview.md), vous devez fournir à Adobe certaines informations sur la destination et les tests effectués. Cela permet de sʼassurer que les utilisateurs bénéficient de la meilleure expérience possible lors de l’activation des données vers votre plateforme.

Cette page répertorie toutes les informations dont vous avez besoin pour envoyer ou mettre à jour une destination créée à l’aide dʼAdobe Experience Platform Destination SDK. Pour envoyer une destination dans Adobe Experience Platform, adressez un e-mail à <aepdestsdk@adobe.com> et précisez les informations suivantes :

* Une description des cas d’utilisation que votre destination résout. Cela n’est nécessaire que si vous envoyez une nouvelle configuration de destination.
* Une description du motif de l’envoi de la destination. Cela n’est nécessaire que si vous mettez à jour une configuration de destination existante.
* Des résultats de test après avoir utilisé le point dʼentrée de l’API de destination de test pour effectuer un appel HTTP vers votre destination. Veuillez partager avec Adobe un appel API effectué vers votre point d’entrée de destination et la réponse API reçue de votre point d’entrée de destination.
* Enregistrement d’écran qui affiche l’expérience utilisateur d’une personne qui se connecte à votre destination et qui passe par les étapes d’activation.
* Exigences supplémentaires pour les destinations basées sur des fichiers :
   * Partagez une requête et un exemple de réponse après avoir utilisé l’API de test pour [tester la destination basée sur des fichiers avec des profils types](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Joignez un exemple de fichier généré par la destination et exporté vers l’emplacement de stockage .
   * Envoyez une preuve que vous avez correctement ingéré le fichier exporté de l’emplacement de stockage vers votre système.
* La preuve que vous avez envoyé une demande de publication de destination pour votre destination à l’aide de l’[API de publication de destination](../publishing-api/create-publishing-request.md).
* Une documentation PR (demande de tirage), suivant les instructions décrites dans le [processus de documentation en libre-service](../docs-framework/documentation-instructions.md).
* Un fichier image qui s’affichera sous forme de logo sur votre carte de destination dans le catalogue des destinations dʼExperience Platform.

Vous trouverez des informations détaillées sur chaque élément dans les sections ci-dessous :

## Description du cas d’utilisation {#use-case-description}

Fournissez une description des cas d’utilisation que votre destination résout pour les clients Experience Platform. Vos descriptions peuvent être similaires aux cas d’utilisation des partenaires existants :

* [Pinterest &#x200B;](/help/destinations/catalog/advertising/pinterest.md) : créez des audiences à partir de vos listes de clients, des personnes qui ont visité votre site ou de celles qui ont déjà interagi avec votre contenu sur Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases) : les API DataX sont disponibles pour les annonceurs qui souhaitent cibler un groupe d’audiences spécifique dont les adresses e-mail sont désactivées dans Verizon Media (VMG). Ils peuvent rapidement créer une nouvelle audience et envoyer le groupe d’audiences souhaité à l’aide de l’API en temps quasi réel de VMG.

## Motif de la mise à jour {#reason-for-update}

>[!NOTE]
>
>Cette section n’est nécessaire que lorsque vous mettez à jour une configuration existante.

Fournissez une brève description du problème que votre envoi résout pour la destination existante. Par exemple, votre envoi peut mettre à jour le nom, la description et le logo de votre destination lorsque vous passez de la version bêta à la disponibilité générale. Votre envoi peut également corriger un bogue détecté dans votre configuration de destination.

## Résultats du test après l’utilisation de l’API de destination du test {#testing-api-response}

Fournissez les résultats du test après avoir utilisé le point dʼentrée de l’[API de destination du test](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) pour effectuer un appel HTTP vers votre destination. Cela inclut :

* La requête API complète (en-têtes et corps) effectuée sur votre point dʼentrée de destination, à l’aide de l’API de test.
* La réponse de l’API reçue de votre point dʼentrée de destination.

Par exemple, votre requête et votre réponse peuvent ressembler aux exemples ci-dessous :

**Requête**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Réponse**

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

## Exigences supplémentaires pour les destinations basées sur des fichiers {#additional-file-based-destination-requirements}

Pour les destinations basées sur des fichiers, vous devez fournir une preuve supplémentaire que vous avez correctement configuré la destination. Veillez à inclure les éléments suivants :

### Test de la réponse de l’API {#testing-api-response-file-based}

Incluez une requête et un exemple de réponse après avoir utilisé l’API de test pour [tester la destination basée sur des fichiers avec des profils types](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Joindre le fichier exporté {#attach-exported-file}

Dans votre [e-mail de soumission](#download-sample-email), joignez un fichier CSV qui a été exporté vers votre emplacement de stockage par la destination que vous avez configurée.

### Preuve d’ingestion réussie {#proof-of-successful-ingestion}

Enfin, vous devez fournir une forme de preuve que les données ont bien été ingérées dans votre système après avoir été exportées vers l’emplacement de stockage que vous avez fourni. Veuillez fournir l’un des éléments ci-dessous :

* Captures d’écran ou brève vidéo de capture d’écran dans laquelle vous prenez le fichier manuellement à l’emplacement de stockage et l’ingérez dans votre système.
* Captures d’écran ou brève vidéo de capture d’écran dans laquelle l’interface utilisateur de votre système confirme que le nom de fichier généré par Experience Platform a bien été ingéré dans votre système.
* Enregistrez les lignes de votre système qu’Adobe peut corréler au nom de fichier ou aux données générées à partir d’Experience Platform.

## Preuve dʼenvoi dʼune demande de publication de destination {#destination-publishing-request-proof}

Une fois votre destination testée, vous devez utiliser l’[API de publication de destination](../publishing-api/create-publishing-request.md) pour envoyer la destination à Adobe pour examen et publication.

Indiquez l’identifiant de la demande de publication pour votre destination. Pour plus d’informations sur la manière de récupérer l’identifiant de requête de publication, consultez la section [Récupération des requêtes de publication de destination](../publishing-api/retrieve-publishing-request.md).

## Documentation de destination PR (demande de tirage) pour les intégrations personnalisées {#documentation-pr}

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une [intégration personnalisée](../overview.md#productized-custom-integrations), vous devez utiliser le [processus de documentation en libre-service](../docs-framework/documentation-instructions.md) pour créer une page de documentation du produit pour la destination. Dans le cadre du processus d’envoi, indiquez la demande de tirage (PR) pour votre documentation de destination.

## Logo de votre destination {#logo}

Le catalogue des destinations comprend un logo pour chaque carte de destination. Incluez dans votre e-mail une image avec le logo de votre destination.

Les exigences relatives aux images sont les suivantes :

* **Format** : `SVG`
* **Taille** : moins de 2 Mo

## Télécharger un exemple d’e-mail {#download-sample-email}

[Téléchargez](../assets/guides/sample-email-submit-destination.rtf) un exemple d’e-mail contenant toutes les informations que vous devez fournir à Adobe.
