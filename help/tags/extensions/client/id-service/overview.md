---
title: Présentation de lʼextension Service d’identités d’Adobe Experience Cloud
description: Découvrez lʼextension de balises du service d’identités d’Adobe Experience Cloud dans Adobe Experience Platform.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
TQID: https://experienceleague.adobe.com/p0fm5HTNKzXVXYxi2mvAhAIHG46WdcWApvuQ0eGnFLo
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2: id: c975b431-530e-4c29-9216-0301b9e204c1id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 761
ht-degree: 87%

---

# Présentation de lʼextension Service d’identités d’Adobe Experience Cloud

Cette référence vous permet dʼobtenir plus dʼinformations sur la configuration de lʼextension du service Experience Cloud ID dʼAdobe et sur les options disponibles lors de lʼutilisation de cette extension afin de créer une règle.

Utilisez cette extension pour intégrer le service d’identités d’Experience Cloud à votre propriété. Grâce au service d’identités d’Experience Cloud, vous pouvez créer et stocker des identifiants uniques et persistants pour les personnes qui visitent votre site.

## Configuration de l’extension Experience Cloud ID

Cette section fournit des informations relatives aux options disponibles lors de la configuration de l’extension Experience Cloud ID.

Si l’extension Experience Cloud ID n’est pas encore installée, ouvrez votre propriété, puis cliquez sur **[!UICONTROL Extensions > Catalogue]**, placez le curseur sur l’extension Experience Cloud ID et cliquez sur **[!UICONTROL Installer]**.

Pour configurer l’extension, ouvrez l’onglet Extensions , placez le curseur sur l’extension, puis cliquez sur **[!UICONTROL Configurer]**.

![](../../../images/optin.jpg)

Les options de configuration disponibles sont les suivantes :

### Experience Cloud Organization ID (ID d’organisation d’Experience Cloud)

ID de votre organisation Experience Cloud.

Votre ID est une chaîne alphanumérique de 24 caractères suivie par `@AdobeOrg`. Si vous ne connaissez pas votre ID, contactez l’Assistance clientèle.

### Exclusion de chemins d’accès spécifiques

L’ID Experience Cloud ID ne se charge pas si l’URL correspond à l’un des chemins spécifiés.

(Facultatif) Activez les Regex s’il s’agit d’une expression régulière.

Sélectionnez **[!UICONTROL Ajouter]** pour exclure un autre chemin.

### Opt-in (Accord préalable)

Utilisez les options Opt-in (Accord préalable) pour déterminer si les visiteurs doivent accepter les services Adobe sur votre site, ainsi que pour savoir si des cookies peuvent être créés pour suivre l’activité des visiteurs.

L’Opt-in est le point de référence centralisé pour toutes les bibliothèques côté client de la solution Experience Platform afin de déterminer si des cookies peuvent être créés sur l’appareil ou le navigateur d’un utilisateur ou d’une utilisatrice lors de sa visite sur votre site. L’opt-in ne prend pas en charge la collecte ou le stockage des préférences d’autorisation des utilisateurs.

**Activer Opt-in (Accord préalable) ?**

L’option sélectionnée détermine si votre site web attend le consentement pour suivre les activités d’un visiteur sur votre site web.

Il existe trois options :

* **No** (Non) : n’attend pas le consentement pour suivre le visiteur. Il s’agit du comportement par défaut si vous ne sélectionnez pas d’option.
* **Yes** (Oui) : attend le consentement pour suivre le visiteur.
* **Determined at runtime using function** (Déterminé lors de l’exécution à l’aide de la fonction) : déterminer par programmation si la valeur est true (vrai) ou false (faux) lors de l’exécution. Si vous sélectionnez cette option, le champ Select Data Element (Sélectionner l’élément de données) devient disponible. Sélectionnez un élément de données pouvant déterminer si le consentement doit être attendu. Cet élément de données correspond à une valeur booléenne. Vous pouvez, par exemple, sélectionner un élément de données qui fournit le consentement en fonction du pays du visiteur, s’il se trouve ou non dans l’UE.

**L’Opt-in (Accord préalable) de stockage est-il Enabled (Activé) ?**

S’il est activé, le consentement est stocké dans un cookie propriétaire sur votre domaine. S’il n’est pas activé, les paramètres de consentement sont conservés dans votre CMP ou dans un cookie que vous gérez.

**Opt In Cookie Domain?** (Domaine du cookie Opt-in ?)

Utilisez ce paramètre facultatif pour spécifier le domaine dans lequel le cookie Opt-in (Accord préalable) est stocké si le stockage est activé. Vous pouvez entrer un domaine ou sélectionner un élément de données contenant le domaine.

**Opt In Storage Expiry?** (Expiration du stockage Opt-in ?)

Indiquez quand le cookie Opt-in (Accord préalable) expire si le stockage est activé, en secondes.

Saisissez un nombre, puis sélectionnez une unité de temps dans la liste déroulante. Par exemple, saisissez 2 et sélectionnez **[!UICONTROL Semaines]**. La valeur par défaut est de 13 mois.

**Permissions?** (Autorisations ?)

Transmettez le consentement précédent à la bibliothèque Opt-in (Accord préalable). Sélectionnez un élément de données contenant le consentement. Le type d’élément doit être un objet ou une chaîne JSON. Remplace les accords Opt-in (Accord préalable) dans les approbations.

Exemple :

`"{"aa":true,"aam":true,"ecid":true}"`

**Pre Opt In Approvals?** (Opt-in dans les approbations ?)

Définissez les catégories qui sont approuvées ou refusées lorsqu’aucune préférence n’a été définie par le visiteur. Le consentement est supposé pour les solutions sélectionnées à partir du moment où la page est chargée. Le type d’élément doit être un objet ou une chaîne JSON (exemple : `{aam: true}`).

### Variables

Définissez les paires nom-valeur comme propriétés d’instance Experience Cloud ID. Utilisez la liste déroulante pour sélectionner une variable, puis saisissez ou sélectionnez une valeur. Pour plus dʼinformations sur chaque variable, reportez-vous à la [documentation sur le service d’identités d’Experience Cloud](https://experiencecloud.adobe.com/resources/help/fr_FR/mcvid/mcvid-overview.html).

## Types d’actions de l’extension Experience Cloud ID

Cette section décrit les types d’actions disponibles dans l’extension Experience Cloud ID.

### Types d’actions

#### Set Customer IDs (Définition des ID de client)

Définissez un ou plusieurs ID de client.

1. Saisissez le code d’intégration.

   Le code d’intégration doit contenir la valeur configurée en tant que source de données dans Audience Manager ou dans Customer Attributes (Attributs du client).

1. Sélectionnez une valeur.

   La valeur doit être un ID d’utilisateur. Les éléments de données sont mieux adaptés aux valeurs dynamiques, tels que les identifiants du système interne d’un client spécifique.

1. Sélectionnez un état d’authentification.

   Les options disponibles sont les suivantes :

   * Unknown (Inconnu)
   * Authenticated (Authentifié)
   * Logged out (Déconnecté)

1. (Facultatif) Sélectionnez **[!UICONTROL Ajouter]** pour définir d’autres ID de client.
1. Sélectionnez **[!UICONTROL Conserver les modifications]**.
