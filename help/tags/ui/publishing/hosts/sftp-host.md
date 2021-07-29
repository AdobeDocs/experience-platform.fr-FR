---
title: Hôtes SFTP
description: Découvrez comment configurer des balises dans Adobe Experience Platform pour diffuser des versions de bibliothèque sur un serveur SFTP sécurisé auto-hébergé.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 44%

---

# Hôtes SFTP

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Si vous ne souhaitez pas qu’Adobe gère vos bibliothèques hébergées, vous avez la possibilité de laisser Adobe Experience Platform  placer les versions sur un serveur SFTP sécurisé que vous hébergez.

Platform  se connecte à votre serveur SFTP à l’aide d’une clé chiffrée. Pour configurer cette méthode correctement, quelques manipulations sont nécessaires :

1. Une paire de clés publique/privée doit être installée sur votre serveur SFTP. Vous pouvez générer ces clés sur votre serveur ou les générer ailleurs et les installer sur votre serveur. Pour plus d’informations, consultez la documentation GitHub concernant la [génération de clés SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) .
1. La clé privée est utilisée pour chiffrer la clé GPG publique. Vous devrez fournir votre clé privée pendant le processus de création de l’hôte SFTP. Voir la section [Chiffrer les valeurs](https://developer.adobelaunch.com/api/guides/encrypting_values/) de la documentation de l’API Reactor pour obtenir des instructions sur le chiffrement des clés GPG publiques. Utilisez la clé GPG de l’environnement de production, sauf si vous savez que vous avez besoin d’une clé spécifique. Enfin, vous pouvez chiffrer votre clé privée depuis n’importe quel ordinateur. Il n’est donc pas nécessaire d’installer GPG sur votre serveur pour réaliser cette manipulation.
1. Vous devrez peut-être approuver les adresses IP utilisées avec le pare-feu de votre entreprise pour permettre à Platform d’atteindre votre serveur SFTP et de s’y connecter. Ces adresses IP sont les suivantes :
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>La structure des versions de balises a changé au fil du temps. Elles utilisent des liens symboliques (symlinks) en interne pour maintenir la rétrocompatibilité afin que les codes incorporés précédents continuent à fonctionner avec la dernière structure de version. Votre serveur SFTP doit prendre en charge l’utilisation des liens symboliques pour servir de destination valide aux versions de balises.

Pour plus d’informations, reportez-vous à l’article Medium suivant sur la [configuration des serveurs SFTP pour envoyer une version](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Création d’un hôte SFTP

1. Ouvrez l’onglet [!UICONTROL Hôtes].
1. Créez l’hôte.
1. Donnez un nom à votre hôte.
1. Choisissez **[!UICONTROL SFTP]** comme type d’hôte.
1. Saisissez l’hôte, le chemin, le port, le nom d’utilisateur et la clé privée chiffrée.

   Le port doit être l’un des ports suivants :

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >En règle générale, Adobe limite le nombre de ports pouvant être utilisés pour le trafic sortant. Les ports sélectionnés sont généralement autorisés par le biais des pare-feu d’entreprise, en plus d’inclure certaines plages pour la flexibilité.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

Lorsque vous sélectionnez **[!UICONTROL Enregistrer]**, la connexion et la capacité de diffuser les fichiers sur votre serveur SFTP sont testées. Platform crée un dossier, écrit un fichier dans ce dossier, vérifie que le fichier est bien là, puis procède à son nettoyage. Si le compte utilisateur de votre serveur SFTP (celui associé au certificat sécurisé que vous avez fourni à Platform) ne dispose pas des autorisations nécessaires pour effectuer cette action, l’hôte passe en état &quot;Failed&quot; (Échec).
