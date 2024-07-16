---
title: Hôtes SFTP
description: Découvrez comment configurer les balises dans Adobe Experience Platform pour diffuser des versions de bibliothèque sur un serveur SFTP sécurisé et auto-hébergé.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 38%

---

# Hôtes SFTP

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Adobe Experience Platform vous permet de fournir des versions de bibliothèque de balises à un serveur SFTP sécurisé que vous hébergez, ce qui vous permet de mieux contrôler la manière dont vos versions sont stockées et gérées. Ce guide explique comment configurer un hôte SFTP pour une propriété de balise dans l’interface utilisateur Experience Platform ou l’interface utilisateur de collecte de données.

>[!NOTE]
>
>Vous pouvez également choisir d’utiliser un hôte géré par Adobe à la place. Pour plus d’informations, consultez le guide sur les [hôtes gérés par Adobe](./managed-by-adobe-host.md) .
>
>Pour plus d’informations sur les avantages et les limites des bibliothèques d’auto-hébergement, consultez le [guide d’auto-hébergement](./self-hosting-libraries.md).

## Configuration d’une clé d’accès pour votre serveur {#access-key}

Platform se connecte à votre serveur SFTP à l’aide d’une clé chiffrée. Pour configurer cette méthode correctement, quelques manipulations sont nécessaires :

### Création d’une paire de clés publique/privée

Une paire de clés publique/privée doit être installée sur votre serveur SFTP. Vous pouvez générer ces clés sur votre serveur ou les générer ailleurs et les installer sur votre serveur. Pour plus d’informations, consultez la documentation GitHub concernant la [génération de clés SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key).

### Chiffrer vos clés

La clé privée est utilisée pour chiffrer la clé publique. Vous devrez fournir votre clé privée pendant le processus de création de l’hôte SFTP. Pour obtenir des instructions sur le cryptage de clés publiques, reportez-vous à la section sur le [chiffrement de valeurs](../../../api/guides/encrypting-values.md) du guide de l’API Reactor. Utilisez la clé GPG de l’environnement de production, sauf si vous savez que vous avez besoin d’une clé spécifique. Enfin, vous pouvez chiffrer votre clé privée depuis n’importe quel ordinateur. Il n’est donc pas nécessaire d’installer GPG sur votre serveur pour réaliser cette manipulation.

### Placer sur la liste autorisée les adresses IP de la plateforme

Vous devrez peut-être approuver un ensemble d’adresses IP à utiliser dans le pare-feu de votre entreprise pour permettre à Platform d’atteindre votre serveur SFTP et de s’y connecter. Ces adresses IP sont les suivantes :

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>La structure des versions de balises a changé au fil du temps. Elles utilisent des liens symboliques (symlinks) en interne pour maintenir la rétrocompatibilité afin que les codes incorporés précédents continuent à fonctionner avec la dernière structure de version. Votre serveur SFTP doit prendre en charge l’utilisation des liens symboliques pour servir de destination valide aux versions de balises.

Pour plus d’informations détaillées, reportez-vous à l’article Medium suivant sur la [configuration de serveurs SFTP pour la diffusion d’une version](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Création d’un hôte SFTP {#create}

Sélectionnez **[!UICONTROL Hôtes]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Ajouter un hôte]**.

![Image montrant le bouton Ajouter l’hôte sélectionné dans l’interface utilisateur](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

La boîte de dialogue de création d’hôte s’affiche. Attribuez un nom à l’hôte et, sous **[!UICONTROL Type]**, sélectionnez **[!UICONTROL SFTP]**.

![Image montrant l&#39;option d&#39;hébergement SFTP sélectionnée](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### Configuration de l’hôte SFTP {#configure}

La boîte de dialogue se développe afin d’inclure des options de configuration supplémentaires pour l’hôte SFTP. Ces informations sont expliquées ci-dessous.

![Image montrant les détails requis pour une connexion d’hôte SFTP](../../../images/ui/publishing/sftp-hosts/host-details.png)

| Champ de configuration | Description |
| --- | --- |
| [!UICONTROL Ne pas utiliser de liens symboliques] | Par défaut, tous les hôtes SFTP utilisent des liens symboliques (symlinks) pour référencer la bibliothèque [builds](../builds.md) qui sont enregistrés sur le serveur. Cependant, tous les serveurs ne prennent pas en charge l’utilisation de liens symboliques. Lorsque cette option est sélectionnée, l’hôte utilise une opération de copie pour mettre à jour les ressources de création directement au lieu d’utiliser des liens symboliques. |
| [!UICONTROL URL du serveur SFTP] | Chemin d’accès de base de l’URL pour votre serveur. |
| [!UICONTROL Chemin] | Chemin d’accès à l’URL du serveur de base pour cet hôte. |
| [!UICONTROL Port] | Le port doit être l’un des ports suivants :<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>En règle générale, Adobe limite le nombre de ports pouvant être utilisés pour le trafic sortant. Les ports sélectionnés sont généralement autorisés par le biais des pare-feu d’entreprise et incluent certaines plages pour plus de flexibilité. |
| [!UICONTROL Nom d’utilisateur] | Nom d’utilisateur à utiliser lors de l’accès au serveur. |
| [!UICONTROL Clé privée chiffrée] | Clé privée chiffrée que vous avez créée lors d’une [étape précédente](#access-key). |

Sélectionnez **[!UICONTROL Enregistrer]** pour créer l’hôte avec la configuration sélectionnée.

![Image montrant l&#39;hôte SFTP en cours d&#39;enregistrement](../../../images/ui/publishing/sftp-hosts/save-host.png)

Cliquer sur **[!UICONTROL Enregistrer]** entraîne le test de la connexion et de la capacité de diffusion des fichiers sur votre serveur SFTP. Platform crée un dossier, écrit un fichier dans ce dossier, vérifie que le fichier est bien là, puis procède au nettoyage. Si le compte utilisateur de votre serveur SFTP (celui associé au certificat sécurisé que vous avez fourni à Platform) ne dispose pas des autorisations nécessaires pour effectuer cette action, l’hôte passe en état &quot;Échec&quot;.

## Étapes suivantes

Ce guide explique comment configurer un serveur SFTP auto-hébergé à utiliser dans des balises . Une fois l’hôte établi, vous pouvez l’associer à un ou plusieurs de vos [environnements](../environments.md) pour publier des bibliothèques de balises. Pour plus d’informations sur le processus d’activation des fonctionnalités de balises de haut niveau sur vos propriétés web ou mobiles, consultez la [présentation de la publication](../overview.md).
