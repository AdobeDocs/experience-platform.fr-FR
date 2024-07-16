---
title: Traitement des erreurs
description: Découvrez la manière dont les erreurs sont traitées dans lʼAPI Reactor.
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 100%

---

# Traitement des erreurs

Lorsquʼun problème se produit lors dʼun appel à lʼAPI Reactor, une erreur peut être renvoyée de lʼune des façons suivantes :

* **Erreurs immédiates** : lorsquʼune requête entraîne une erreur immédiate, une réponse dʼerreur est renvoyée par lʼAPI, lʼétat HTTP reflétant le type dʼerreur général qui sʼest produit.
* **Retards dʼerreurs** : lorsquʼune requête dʼAPI entraîne un retard dʼerreur (une activité asynchrone, par exemple), une erreur peut être renvoyée par lʼAPI dans lʼélément `meta.status_details` dʼune ressource associée.

## Format dʼerreur

Les réponses dʼerreur visent à se conformer à la [spécification des erreurs JSON:API](http://jsonapi.org/format/#errors) et respectent généralement la structure suivante :

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
| `id` | Identifiant unique pour cette occurrence particulière du problème. |
| `status` | Code dʼétat HTTP applicable à ce problème, exprimé sous la forme dʼune valeur de chaîne. |
| `code` | Code dʼerreur spécifique à lʼapplication, exprimé sous la forme dʼune valeur de chaîne. |
| `title` | Résumé court et lisible par lʼutilisateur du problème qui **ne doit pas être modifié** dʼune occurrence à lʼautre, sauf à des fins de localisation. |
| `detail` | Explication lisible par lʼutilisateur spécifique à cette occurrence du problème. À lʼinstar de `title`, la valeur de ce champ peut être localisée. |
| `source` | Objet contenant des références à la source de lʼerreur, incluant éventuellement lʼun des membres suivants :<ul><li>`pointer` : chaîne [JSON Pointer (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) qui référence lʼentité associée dans le document de requête (`/data` pour un objet de données principal ou `/data/attributes/title` pour un attribut spécifique, par exemple).</li></ul> |
| `meta` | Objet contenant des métadonnées non standard sur lʼerreur. |

{style="table-layout:auto"}

## Référence dʼerreur

Le tableau suivant répertorie les différentes erreurs que l’API peut renvoyer.

| Titre de l’erreur | Description |
| --- | --- |
| `authentication-failure` | Votre jeton dʼaccès IMS est non valide. Vous pouvez obtenir un nouveau jeton dʼaccès en vous connectant à nouveau. Ou, pour les comptes techniques, en générant un nouveau JWT et en lʼéchangeant contre un jeton dʼaccès IMS. |
| `connection-refused` | Impossible dʼétablir une connexion au serveur. |
| `decrypt-bad-passphrase` | Les données nʼont pas pu être déchiffrées avec la phrase secrète fournie. |
| `decrypt-failed` | Les données n’ont pas pu être déchiffrées à l’aide de la clé privée fournie. Assurez-vous que la clé fonctionne localement et que lʼespace blanc a été supprimé. |
| `decrypt-no-data` | Les données ne peuvent pas être déchiffrées sans clé privée. Renseignez une clé privée chiffrée. |
| `delegate-descriptor-unresolved` | Lʼextension nʼa pas fourni la définition attendue de ce descripteur délégué. Il se peut que lʼextension doive être mise à jour. |
| `deleted-resources` | Les ressources que vous essayez dʼajouter à votre bibliothèque ont été supprimées. |
| `environment-in-use` | Un environnement ne peut être affecté quʼà une seule bibliothèque à la fois. Lʼoption 1 consiste à sélectionner un autre environnement. Lʼoption 2 consiste à libérer cet environnement en déplaçant la bibliothèque vers un autre environnement ou en la supprimant. |
| `environment-required` | Un environnement doit être affecté à votre bibliothèque avant de pouvoir créer une version. |
| `extension-not-found` | Lʼextension qui définit un élément de données ou un composant de règle nʼest pas incluse dans la bibliothèque. Assurez-vous que toutes les extensions requises ont été ajoutées à votre bibliothèque. |
| `extension-package-path-error` | Un chemin dʼaccès défini en extension.json a été mal construit. |
| `extension-package-transform-definition-error` | Vous avez défini une transformation non valide pour une propriété dʼobjet. Une transformation peut être définie pour chaque propriété dʼobjet. Il doit sʼagir dʼune transformation de fichier ou dʼune transformation de fonction. |
| `extension-package-zip-error` | Une erreur sʼest produite lors de la décompression du package dʼextension ou de la compression des fichiers en vue de leur distribution. |
| `host-in-use` | Un hôte ne peut pas être supprimé si un ou plusieurs environnements lʼutilisent. |
| `host-required` | Lʼenvironnement affecté à cette bibliothèque ne comporte pas dʼhôte valide. Vérifiez quel environnement est affecté à votre bibliothèque. Attribuez ensuite un hôte valide à cet environnement. |
| `host-type-error` | Seuls les hôtes SFTP doivent avoir des informations dʼidentification vérifiées avant de pouvoir être utilisés. Le prétest nʼest donc disponible que pour ce type dʼhôte. |
| `illegal-custom-code-transform` | Vous nʼêtes pas autorisé à utiliser la transformation customCode. Spécifiez une transformation de fonction ou de fichier. |
| `ims-not-authorized` | Une erreur inconnue sʼest produite lors de lʼautorisation de votre compte. Réessayez plus tard. |
| `ims-session-error` | Il y a un problème avec la session de connexion. Déconnectez-vous et reconnectez-vous. |
| `internal-error` | Une erreur interne sʼest produite. Patientez quelques minutes et réessayez. Si le problème persiste, contactez lʼassistance clientèle. |
| `invalid-data_element` | Un élément de données non valide ne peut pas être ajouté à une bibliothèque. |
| `invalid-embed_code` | Il ne sʼagit pas dʼun code incorporé valide ou vous essayez de le lier à un environnement de développement ou dʼévaluation. Les codes incorporés de la gestion dynamique des balises (Dynamic Tag Management, DTM) ne peuvent être associés quʼà des environnements de production. |
| `invalid-extension` | Une extension non valide ne peut pas être ajoutée à une bibliothèque. |
| `invalid-extension_package_id` | Vous pouvez uniquement modifier certaines des propriétés dʼobjet dʼun package dʼextension. Vous avez tenté de modifier une propriété dʼobjet non autorisée. |
| `invalid-new-owner-org-id` | LʼID dʼorganisation que vous avez tenté dʼaffecter nʼest pas un ID dʼorganisation valide. |
| `invalid-org` | Votre organisation actuelle ne dispose pas dʼun accès à lʼAPI. Vérifiez que vous utilisez lʼorganisation appropriée. |
| `invalid-rule` | Une règle non valide ne peut pas être ajoutée à une bibliothèque. |
| `invalid-settings-syntax` | Une erreur de syntaxe sʼest produite lors de lʼanalyse des paramètres JSON. |
| `library-file-not-found` | Un fichier requis défini en extension.json est introuvable dans le package zip. |
| `minification-error` | Échec de la compilation du code en raison dʼun code non valide. |
| `multiple-revisions` | Une seule révision de chaque ressource peut être incluse dans une bibliothèque. |
| `no-available-orgs` | Ce compte d’utilisateur nʼappartient pas à un profil de produit ayant accès aux balises. Utilisez Admin Console pour ajouter cet utilisateur à un profil de produit disposant de droits de balises. |
| `not-authorized` | Ce compte d’utilisateur ne dispose pas des autorisations nécessaires pour effectuer cette action. |
| `not-found` | Lʼenregistrement est introuvable. Vérifiez lʼidentifiant de lʼobjet que vous essayez de récupérer. |
| `not-unique` | Le nom que vous souhaitez utiliser est déjà attribué. Pour cette ressource, la propriété « name » doit être unique. |
| `public-release-not-authorized` | La publication publique des extensions est coordonnée par `launch-ext-dev@adobe.com`. Pour plus dʼinformations, consultez le document [Publication des extensions](../../extension-dev/submit/release.md). |
| `read-only` | Cette ressource est en lecture seule et ne peut pas être modifiée. |
| `session-timeout` | La session utilisateur a expiré. Déconnectez-vous et reconnectez-vous. |
| `sftp-authentication-failed` | Échec de lʼauthentification pour la connexion SFTP. |
| `sftp-connection-timeout` | La connexion SFTP a expiré. |
| `sftp-exception` | Une exception sʼest produite lors de lʼutilisation du protocole SFTP pour se connecter au serveur. |
| `sftp-status-exception` | Une exception SFTP sʼest produite lors de la tentative de communication avec le serveur. |
| `socket-error` | Une erreur de socket sʼest produite lors de la tentative de communication avec le serveur. |
| `ssh-disconnect` | La session SSH a été déconnectée. |
| `timeout-error` | La connexion au serveur a expiré. |
| `unknown-error` | Une erreur inattendue sʼest produite. Vous pouvez réessayer plus tard ou contacter lʼassistance clientèle et expliquer ce que vous faisiez lorsque cela sʼest produit. |
| `unsupported-custom-code-language` | Un langage de code personnalisé qui nʼest pas pris en charge a été fourni. |
| `upgraded-extension-required` | Une fois que vous avez installé une mise à niveau dʼextension, vous devez lʼinclure dans toutes les bibliothèques jusquʼà ce que la mise à niveau atteigne la production. Cela ne sʼapplique pas si lʼextension nʼa pas encore été publiée. |
| `upstream-build-required` | Une version réussie de la bibliothèque en amont est nécessaire avant de pouvoir créer celle-ci. |

{style="table-layout:auto"}
