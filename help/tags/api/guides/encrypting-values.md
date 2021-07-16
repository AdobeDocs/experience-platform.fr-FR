---
title: Chiffrement des valeurs
description: Découvrez comment chiffrer des valeurs sensibles lors de l’utilisation de l’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# Chiffrement des valeurs

Lorsque vous utilisez des balises dans Adobe Experience Platform, certains workflows nécessitent de fournir des valeurs sensibles (par exemple, en fournissant une clé privée lors de la diffusion de bibliothèques vers des environnements via des hôtes). La nature délicate de ces informations d’identification nécessite
le transfert et le stockage sécurisés.

Ce document décrit comment chiffrer des valeurs sensibles à l’aide de [cryptage GnuPG](https://www.gnupg.org/gph/en/manual/x110.html) (également appelé GPG) afin que seul le système de balises puisse les lire.

## Obtention de la clé GPG publique et de la somme de contrôle

Après avoir téléchargé [et installé la dernière version de GPG, vous devez obtenir la clé GPG publique pour l’environnement de production des balises :](https://gnupg.org/download/)

* [Clé GPG](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Checksum](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## Importez la clé dans votre trousseau

Une fois que vous avez enregistré la clé sur votre ordinateur, l’étape suivante consiste à l’ajouter à votre trousseau GPG.

**Syntaxe**

```shell
gpg --import {KEY_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{KEY_NAME}` | Nom du fichier de clé publique. |

{style=&quot;table-layout:auto&quot;}

**Exemple**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Chiffrer les valeurs

Après avoir ajouté la clé à votre chaîne de clés, vous pouvez commencer à chiffrer les valeurs à l’aide de l’indicateur `--encrypt`. Le script suivant illustre le fonctionnement de cette commande :

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Cette commande peut être répartie comme suit :

* L&#39;entrée est fournie à la commande `gpg`.
* `--armor` crée une sortie encadrée ASCII au lieu de binaire. Cela simplifie le transfert de la valeur via JSON.
* `--encrypt` Indique à GPG de chiffrer les données.
* `-r` définit le destinataire des données. Seul le destinataire (titulaire de la clé privée correspondant à la clé publique) peut décrypter les données. Le nom du destinataire de la clé souhaitée peut être trouvé en examinant la sortie de `gpg --list-keys`.

La commande ci-dessus utilise la clé publique pour `Tags Data Encryption <launch@adobe.com>` pour chiffrer la valeur, `Example value`, au format ASCII.

La sortie de la commande ressemblerait à ce qui suit :

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

Cette sortie ne peut être décryptée que par les systèmes disposant de la clé privée qui
correspond à la clé publique `Tags Data Encryption <launch@adobe.com>` .

Cette sortie est la valeur qui doit être fournie dans lors de l’envoi de données à l’API Reactor. Le système stocke cette sortie chiffrée et la décrypte temporairement selon les besoins. Par exemple, le système décrypte les informations d’identification de l’hôte suffisamment longtemps pour lancer une connexion au serveur, puis supprime immédiatement toutes les traces de la valeur déchiffrée.

>[!NOTE]
>
>Le format de la valeur encadrée et chiffrée est important. Assurez-vous que les retours de ligne sont correctement précédés d’une séquence d’échappement dans la valeur fournie dans la requête.
