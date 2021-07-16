---
title: Gestion des erreurs
description: Découvrez comment les erreurs sont gérées dans l’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---

# Traitement des erreurs

Lorsqu’un problème se produit lors d’un appel à l’API Reactor, une erreur peut être renvoyée de l’une des façons suivantes :

* **Erreurs** immédiates : Lors de l’exécution d’une requête qui entraîne une erreur immédiate, une réponse d’erreur est renvoyée par l’API, l’état HTTP reflétant le type d’erreur général qui s’est produit.
* **Erreurs** différées : Lors de l’exécution d’une requête d’API qui entraîne un retard d’erreur (une activité asynchrone, par exemple), une erreur peut être renvoyée par l’API dans l’élément  `meta.status_details` d’une ressource associée.

## Format d’erreur

Les réponses d’erreur visent à se conformer à la [spécification des erreurs JSON:API](http://jsonapi.org/format/#errors) et à respecter généralement la structure suivante :

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant unique de cette occurrence particulière du problème. |
| `status` | Code d’état HTTP applicable à ce problème, exprimé sous la forme d’une valeur string . |
| `code` | Code d’erreur spécifique à l’application, exprimé sous la forme d’une valeur string . |
| `title` | Résumé court et lisible du problème que **ne doit pas modifier** d’occurrence à occurrence, sauf à des fins de localisation. |
| `detail` | Une explication lisible et spécifique à cette occurrence du problème. Comme `title`, la valeur de ce champ peut être localisée. |
| `source` | Objet contenant des références à la source de l’erreur, incluant éventuellement l’un des membres suivants :<ul><li>`pointer`: chaîne  [JSON Pointer (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901)  qui référence l’entité associée dans le document de requête ( `/data` pour un objet de données Principal ou  `/data/attributes/title` pour un attribut spécifique, par exemple).</li></ul> |
| `meta` | Objet contenant des métadonnées non standard sur l’erreur. |

{style=&quot;table-layout:auto&quot;}

## Référence d’erreur

Le tableau suivant répertorie les différentes erreurs que l’API peut renvoyer.

| Titre de l’erreur | Description |
| --- | --- |
| `authentication-failure` | Votre jeton d’accès IMS n’est pas valide. Vous pouvez obtenir un nouveau jeton d’accès en vous connectant à nouveau. Ou pour les comptes techniques, la génération d’un nouveau JWT et la permutation pour un jeton d’accès IMS. |
| `connection-refused` | Impossible d’établir une connexion au serveur. |
| `decrypt-bad-passphrase` | Les données n’ont pas pu être déchiffrées avec la phrase secrète fournie. |
| `decrypt-failed` | Les données n’ont pas pu être déchiffrées à l’aide de la clé privée fournie. Assurez-vous que la clé fonctionne localement et que l’espace blanc a été supprimé. |
| `decrypt-no-data` | Les données ne peuvent pas être déchiffrées sans clé privée. Veuillez fournir une clé privée chiffrée. |
| `delegate-descriptor-unresolved` | L’extension n’a pas fourni la définition attendue de ce descripteur délégué. Il se peut que l’extension doive être mise à jour. |
| `deleted-resources` | Les ressources que vous essayez d’ajouter à votre bibliothèque ont été supprimées. |
| `environment-in-use` | Un environnement ne peut être affecté qu’à une seule bibliothèque à la fois. L’option 1 consiste à choisir un environnement différent. L’option 2 consiste à libérer cet environnement en déplaçant la bibliothèque vers un autre environnement ou en supprimant la bibliothèque. |
| `environment-required` | Un environnement doit être affecté à votre bibliothèque avant de pouvoir créer une version. |
| `extension-not-found` | L’extension qui définit un élément de données ou un composant de règle n’est pas incluse dans la bibliothèque . Assurez-vous que toutes les extensions requises ont été ajoutées à votre bibliothèque. |
| `extension-package-path-error` | Un chemin défini dans extension.json a été mal construit. |
| `extension-package-transform-definition-error` | Vous avez défini une transformation non valide pour une propriété d’objet. Une transformation peut être définie pour chaque propriété d’objet. Il doit s’agir d’une transformation de fichier ou d’une transformation de fonction. |
| `extension-package-zip-error` | Une erreur s’est produite lors de la décompression de l’extensionPackage ou de la compression des fichiers en vue de leur distribution. |
| `host-in-use` | Un hôte ne peut pas être supprimé si un ou plusieurs environnements l’utilisent. |
| `host-required` | L’environnement affecté à cette bibliothèque ne comporte pas d’hôte valide. Vérifiez quel environnement est affecté à votre bibliothèque. Attribuez ensuite un hôte valide à cet environnement. |
| `host-type-error` | Seuls les hôtes SFTP doivent avoir des informations d’identification vérifiées avant de pouvoir être utilisés. Le pré-test n’est donc disponible que pour ce type d’hôte. |
| `illegal-custom-code-transform` | Vous n’êtes pas autorisé à utiliser la transformation customCode. Spécifiez une fonction ou une transformation de fichier. |
| `ims-not-authorized` | Une erreur inconnue s’est produite lors de l’autorisation de votre compte. Veuillez réessayer plus tard. |
| `ims-session-error` | Il existe un problème avec la session de connexion. Veuillez vous déconnecter et vous reconnecter. |
| `internal-error` | Une erreur interne s’est produite. Veuillez patienter quelques minutes et réessayer. Si le problème persiste, contactez le service à la clientèle. |
| `invalid-data_element` | Un élément de données non valide ne peut pas être ajouté à une bibliothèque. |
| `invalid-embed_code` | Il ne s’agit pas d’un code incorporé valide ou vous essayez de le lier à un environnement de développement ou d’évaluation. Les codes incorporés de Dynamic Tag Management (DTM) ne peuvent être associés qu’à des environnements de production. |
| `invalid-extension` | Une extension non valide ne peut pas être ajoutée à une bibliothèque. |
| `invalid-extension_package_id` | Vous pouvez uniquement modifier certaines des propriétés d’objet d’un package d’extension. Vous avez tenté de modifier l’un des éléments non autorisés. |
| `invalid-new-owner-org-id` | L’ID d’organisation que vous avez tenté d’affecter n’est pas un ID d’organisation valide. |
| `invalid-org` | Votre principale organisation n’a pas accès à l’API. Vérifiez que vous utilisez l’organisation appropriée. |
| `invalid-rule` | Une règle non valide ne peut pas être ajoutée à une bibliothèque. |
| `invalid-settings-syntax` | Une erreur de syntaxe s’est produite lors de l’analyse des paramètres JSON. |
| `library-file-not-found` | Un fichier requis défini dans extension.json est introuvable dans le package zip. |
| `minification-error` | Le code n’a pas pu être compilé en raison d’un code non valide ou d’un code ES6. |
| `multiple-revisions` | Une seule révision de chaque ressource peut être incluse dans une bibliothèque. |
| `no-available-orgs` | Ce compte utilisateur n’appartient pas à un profil de produit ayant accès aux balises . Utilisez le Admin Console pour ajouter cet utilisateur à un profil de produits avec des droits de balises. |
| `not-authorized` | Ce compte utilisateur ne dispose pas des autorisations nécessaires pour effectuer cette action. |
| `not-found` | L’enregistrement est introuvable. Vérifiez l’identifiant de l’objet que vous essayez de récupérer. |
| `not-unique` | Le nom que vous essayez d’utiliser est déjà utilisé. Pour cette ressource, la propriété &#39;name&#39; doit être unique. |
| `public-release-not-authorized` | La publication publique des extensions est coordonnée par `launch-ext-dev@adobe.com`. Pour plus d’informations, consultez le document [Publication d’extensions](../../extension-dev/submit/release.md) . |
| `read-only` | Cette ressource est en lecture seule et ne peut pas être modifiée. |
| `session-timeout` | La session utilisateur a expiré. Veuillez vous déconnecter et vous reconnecter. |
| `sftp-authentication-failed` | Échec de l’authentification pour la connexion SFTP. |
| `sftp-connection-timeout` | La connexion SFTP a expiré. |
| `sftp-exception` | Une exception s’est produite lors de l’utilisation du protocole SFTP pour se connecter au serveur. |
| `sftp-status-exception` | Une exception SFTP s’est produite lors de la tentative de communication avec le serveur. |
| `socket-error` | Une erreur de socket s’est produite lors de la tentative de communication avec le serveur. |
| `ssh-disconnect` | La session SSH a été déconnectée. |
| `timeout-error` | La connexion au serveur a expiré. |
| `unknown-error` | Une erreur inattendue s’est produite. Vous pouvez réessayer plus tard ou téléphoner à l’Assistance clientèle et expliquer ce que vous faisiez lorsque cela s’est produit. |
| `unsupported-custom-code-language` | Un langage de code personnalisé qui n’est pas pris en charge a été fourni. |
| `upgraded-extension-required` | Une fois que vous avez installé une mise à niveau d’extension, vous devez l’inclure dans toutes les bibliothèques jusqu’à ce que la mise à niveau atteigne Production. La seule exception est si l’extension n’a pas encore été publiée. |
| `upstream-build-required` | Une création réussie pour la bibliothèque en amont est requise avant que vous puissiez la créer. |

{style=&quot;table-layout:auto&quot;}
