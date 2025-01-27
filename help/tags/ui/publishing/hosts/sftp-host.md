---
title: Hôtes SFTP
description: Découvrez comment configurer les balises dans Adobe Experience Platform pour diffuser des versions de bibliothèque sur un serveur SFTP sécurisé et auto-hébergé.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: b3c3bf0a39a30e8c9baf81ec20945497acef5465
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 39%

---

# Hôtes SFTP

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Experience Platform vous permet de diffuser les versions de bibliothèque de balises sur un serveur SFTP sécurisé que vous hébergez, ce qui vous permet de mieux contrôler le stockage et la gestion de vos versions. Ce guide explique comment configurer un hôte SFTP pour une propriété de balise dans l’interface utilisateur de l’Experience Platform ou dans l’interface utilisateur de la collecte de données.

>[!NOTE]
>
>Vous pouvez également choisir d’utiliser un hôte géré par Adobe à la place. Pour plus d’informations, consultez le guide sur les [hôtes gérés par l’Adobe ](./managed-by-adobe-host.md).
>
>Pour plus d’informations sur les avantages et les limites des bibliothèques d’auto-hébergement, consultez le [ guide d’auto-hébergement ](./self-hosting-libraries.md).

## Configurer une clé d’accès pour votre serveur {#access-key}

Platform se connecte à votre serveur SFTP à l’aide d’une clé chiffrée. Pour configurer cette méthode correctement, quelques manipulations sont nécessaires :

### Création d’une paire de clés publique/privée

Une paire de clés publique/privée doit être installée sur votre serveur SFTP. Vous pouvez générer ces clés sur votre serveur ou les générer ailleurs et les installer sur votre serveur. Pour plus d’informations, consultez la documentation GitHub concernant la [génération de clés SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key).

### Chiffrer vos clés

La clé privée est utilisée pour chiffrer la clé publique. Vous devrez fournir votre clé privée pendant le processus de création de l’hôte SFTP. Consultez la section sur le [chiffrement des valeurs](../../../api/guides/encrypting-values.md) dans le guide de l’API Reactor pour obtenir des instructions sur le chiffrement des clés publiques. Utilisez la clé GPG de l’environnement de production, sauf si vous savez que vous avez besoin d’une clé spécifique. Enfin, vous pouvez chiffrer votre clé privée depuis n’importe quel ordinateur. Il n’est donc pas nécessaire d’installer GPG sur votre serveur pour réaliser cette manipulation.

### Placer sur la liste autorisée Adresses IP de Platform

Vous devrez peut-être approuver un ensemble d’adresses IP à utiliser dans le pare-feu de votre entreprise pour permettre à Platform d’atteindre votre serveur SFTP et de s’y connecter. Ces adresses IP sont les suivantes :

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>La structure des versions de balises a changé au fil du temps. Elles utilisent des liens symboliques (symlinks) en interne pour maintenir la rétrocompatibilité afin que les codes incorporés précédents continuent à fonctionner avec la dernière structure de version. Votre serveur SFTP doit prendre en charge l’utilisation des liens symboliques pour servir de destination valide aux versions de balises.

Pour plus d’informations détaillées, reportez-vous à l’article Medium suivant sur la [configuration de serveurs SFTP pour la diffusion d’une version](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Création d’un hôte SFTP {#create}

Sélectionnez **[!UICONTROL Hôtes]** dans le volet de navigation de gauche, puis **[!UICONTROL Ajouter un hôte]**.

![Image illustrant le bouton Ajouter l’hôte sélectionné dans l’interface utilisateur](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

La boîte de dialogue de création de l’hôte s’affiche. Attribuez un nom à l’hôte et sous **[!UICONTROL Type]**, sélectionnez **[!UICONTROL SFTP]**.

![Image illustrant l’option d’hébergement SFTP sélectionnée](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### Configuration de l’hôte SFTP {#configure}

La boîte de dialogue se développe pour inclure des options de configuration supplémentaires pour l’hôte SFTP. Elles sont expliquées ci-dessous.

![Image montrant les détails requis pour une connexion d’hôte SFTP](../../../images/ui/publishing/sftp-hosts/host-details.png)

| Champ de configuration | Description |
| --- | --- |
| [!UICONTROL Ne pas utiliser de liens symboliques] | Par défaut, tous les hôtes SFTP utilisent des liens symboliques (symlinks) pour référencer la bibliothèque [versions](../builds.md) qui sont enregistrés sur le serveur. Cependant, tous les serveurs ne prennent pas en charge l’utilisation de liens symboliques. Lorsque cette option est sélectionnée, l’hôte utilise une opération de copie pour mettre à jour directement les ressources de build au lieu d’utiliser des liens symboliques. |
| [!UICONTROL  URL du serveur SFTP ] | Chemin d’accès de base de l’URL de votre serveur . |
| [!UICONTROL Chemin] | Chemin d’accès à ajouter à l’URL du serveur de base pour cet hôte. |
| [!UICONTROL Port] | Le port doit être l’un des ports suivants :<ul><li>`21`</li><li>`22`</li><li>`201`</li><li>`200`</li><li>`2002`</li><li>`2018`</li><li>`2022`</li><li>`2200`</li><li>`2222`</li><li>`2333`</li><li>`2939`</li><li>`443`</li><li>`4343`</li><li>`80`</li><li>`8080`</li><li>`8888`</li></ul>En règle générale, Adobe limite le nombre de ports pouvant être utilisés pour le trafic sortant. Les ports sélectionnés sont généralement autorisés à passer par les pare-feu d’entreprise et incluent certaines plages pour plus de flexibilité. |
| [!UICONTROL Nom d’utilisateur] | Nom d’utilisateur à utiliser lors de l’accès au serveur. |
| [!UICONTROL Clé privée chiffrée] | La clé privée chiffrée que vous avez créée lors d’une [étape précédente](#access-key). |

Sélectionnez **[!UICONTROL Enregistrer]** pour créer l’hôte avec la configuration sélectionnée.

![Image montrant l’hôte SFTP en cours d’enregistrement](../../../images/ui/publishing/sftp-hosts/save-host.png)

Cliquer sur **[!UICONTROL Enregistrer]** entraîne le test de la connexion et de la capacité de diffusion des fichiers sur votre serveur SFTP. Platform crée un dossier, écrit un fichier dans ce dossier, vérifie que le fichier est bien là, puis supprime le tout. Si le compte utilisateur de votre serveur SFTP (celui associé au certificat sécurisé que vous avez fourni à Platform) ne dispose pas des autorisations nécessaires pour effectuer cette action, l’hôte passe en état « Failed » (Échec).

## Étapes suivantes

Ce guide explique comment configurer un serveur SFTP auto-hébergé à utiliser dans les balises. Une fois l’hôte établi, vous pouvez l’associer à un ou plusieurs de vos [environnements](../environments.md) pour publier des bibliothèques de balises. Pour plus d’informations sur le processus général d’activation des fonctionnalités de balises sur vos propriétés web ou mobiles, consultez la [présentation de la publication](../overview.md).
