---
title: Chiffrement des valeurs
description: Découvrez comment chiffrer des valeurs sensibles lors de l’utilisation de l’API Reactor.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
TQID: https://experienceleague.adobe.com/Ui3AuOGd9Pr5CoM1kNo6oddr-gVT9Xh2PWkDV7E6bm8
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 396
ht-degree: 91%

---

# Chiffrement des valeurs

Lorsque vous utilisez des balises dans Adobe Experience Platform, certains workflows nécessitent de fournir des valeurs sensibles (par exemple, en fournissant une clé privée lors de la diffusion de bibliothèques vers des environnements via des hôtes). La nature sensible de ces informations d’identification nécessite
transfert et stockage sécurisés.

Ce document décrit comment chiffrer des valeurs sensibles à l’aide du [chiffrement GnuPG](https://www.gnupg.org/gph/en/manual/x110.html) (également appelé GPG) afin que seul le système de balises puisse les lire.

## Obtention de la clé GPG publique et de la somme de contrôle

Après avoir [téléchargé](https://gnupg.org/download/) et installé la dernière version de GPG, vous devez obtenir la clé GPG publique pour l’environnement de production des balises :

* [Clé GPG](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Somme de contrôle](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## Importer la clé dans votre trousseau

Une fois que vous avez enregistré la clé sur votre ordinateur, l’étape suivante consiste à l’ajouter à votre trousseau GPG.

**Syntaxe**

```shell
gpg --import {KEY_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{KEY_NAME}` | Nom du fichier de clé publique. |

{style="table-layout:auto"}

**Exemple**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Chiffrer les valeurs

Après avoir ajouté la clé à votre trousseau, vous pouvez commencer à chiffrer les valeurs à l’aide de l’indicateur `--encrypt`. Le script suivant illustre le fonctionnement de cette commande :

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Cette commande peut être répartie comme suit :

* L&#39;entrée est fournie à la commande `gpg`.
* `--armor` crée une sortie ASCII (texte) au lieu de binaire. Cela simplifie le transfert de la valeur via JSON.
* `--encrypt` indique à GPG de chiffrer les données.
* `-r` définit le destinataire des données. Seul le destinataire (titulaire de la clé privée correspondant à la clé publique) peut déchiffrer les données. Le nom du destinataire de la clé souhaitée peut être trouvé en examinant la sortie de `gpg --list-keys`.

La commande ci-dessus utilise la clé publique de `Tags Data Encryption <launch@adobe.com>` pour chiffrer la valeur, `Example value`, au format ASCII.

La sortie de la commande ressemblerait à ce qui suit :

```shell
|-----BEGIN PGP MESSAGE-----

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
|-----END PGP MESSAGE-----
```

Cette sortie ne peut être déchiffrée que par les systèmes disposant de la clé privée qui
correspond à la clé publique `Tags Data Encryption <launch@adobe.com>`.

Cette sortie est la valeur qui doit être fournie lors de l’envoi de données à l’API Reactor. Le système stocke cette sortie chiffrée et la déchiffre temporairement selon les besoins. Par exemple, le système déchiffre les informations d’identification de l’hôte suffisamment longtemps pour lancer une connexion au serveur, puis supprime immédiatement toutes les traces de la valeur déchiffrée.

>[!NOTE]
>
>Le format de la valeur texte et chiffrée est important. Assurez-vous que les retours de ligne sont correctement placés dans une séquence d’échappement dans la valeur fournie dans la requête.
