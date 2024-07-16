---
title: defaultConsent
description: Définissez la méthode de collecte du consentement par défaut pour votre propriété web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

La propriété `defaultConsent` détermine la manière dont vous gérez le consentement pour la collecte de données avant d’appeler la commande [`setConsent`](../setconsent.md). Cette propriété est utile lorsque vous ne souhaitez pas collecter accidentellement des données d’individus résidant dans des zones où le consentement est requis avant de collecter des données.

Par défaut, les utilisateurs sont inscrits à tous les usages et le SDK Web est autorisé à effectuer les tâches suivantes :

* envoyer des données vers et depuis les serveurs d’Adobe ;
* Lire et écrire des cookies ou des éléments de stockage web.

Si les utilisateurs se désinscrivent de tous les usages, le SDK Web n’effectue aucune de ces tâches.

La propriété `defaultConsent` prend en charge trois valeurs :

* **`in`** : la collecte de données se poursuit normalement, jusqu’à ce que l’utilisateur se désinscrive.
* **`out`** : les données sont définitivement ignorées jusqu’à ce que l’utilisateur se connecte.
* **`pending`** : les données sont stockées localement jusqu’à ce que l’utilisateur donne son consentement à l’aide de la commande [`setConsent`](../setconsent.md). Lorsque le consentement par défaut à des fins générales est défini sur `pending`, toute tentative d’exécution de commandes qui dépend des préférences de consentement de l’utilisateur (par exemple, la commande [`sendEvent`](../sendevent/overview.md)) entraîne la mise en file d’attente de la commande dans le SDK Web. Les commandes en file d’attente ne sont pas traitées tant que vous n’avez pas communiqué les préférences de souscription de l’utilisateur au SDK Web.

>[!NOTE]
>
> Les données de consentement ne persistent pas entre les chargements de page.

Si un visiteur ne figure pas dans la compétence du Règlement général sur la protection des données (RGPD), le consentement par défaut peut être défini sur `in`. Le consentement par défaut des visiteurs se trouvant dans la juridiction du RGPD peut être défini sur `pending`. Votre plateforme de gestion du consentement (CMP) peut détecter la région du client et fournir l’indicateur `gdprApplies` à IAB TCF 2.0. Cet indicateur peut être utilisé pour définir le consentement par défaut.

Si vous ne souhaitez pas collecter les événements qui se sont produits avant que les préférences d’inclusion de l’utilisateur ne soient définies, vous pouvez transmettre `"defaultConsent": "out"` lors de la configuration du SDK Web. Toute tentative d’exécution de commandes qui dépend des préférences de consentement de l’utilisateur n’aura aucun effet tant que vous n’aurez pas communiqué les préférences de consentement de l’utilisateur au SDK Web.

>[!NOTE]
>
>Actuellement, le SDK Web ne prend en charge qu’une seule fonction tout ou rien. Bien que nous prévoyions de créer un ensemble plus robuste d’objectifs ou de catégories qui correspondront aux différentes fonctionnalités d’Adobe et offres de produits, l’implémentation actuelle est une approche d’opt-in &quot;tout ou rien&quot;.  Cela s’applique uniquement à [!DNL Web SDK] et NON à d’autres bibliothèques JavaScript Adobe.

## Utilisation de `defaultConsent` avec `setConsent` {#using-consent}

Le SDK Web propose deux commandes de configuration de consentement complémentaires :

* [`defaultConsent`](defaultconsent.md) : cette commande est destinée à capturer les préférences de consentement des clients Adobe utilisant le SDK Web.
* [`setConsent`](../setconsent.md) : cette commande est destinée à capturer les préférences de consentement des visiteurs de votre site.

Lorsqu’ils sont utilisés ensemble, ces paramètres peuvent donner lieu à différents résultats de collecte de données et de définition des cookies, selon leurs valeurs configurées.

Consultez le tableau ci-dessous pour savoir quand se produit la collecte de données et quand les cookies sont définis, en fonction des paramètres de consentement.

| defaultConsent | setConsent | Collecte de données | Le SDK Web définit les cookies de navigateur. |
|---------|----------|---------|---------|
| `in` | `in` | Oui | Oui |
| `in` | `out` | Non | Oui |
| `in` | Non défini | Oui | Oui |
| `pending` | `in` | Oui | Oui |
| `pending` | `out` | Non | Oui |
| `pending` | Non défini | Non | Non |
| `out` | `in` | Oui | Oui |
| `out` | `out` | Non | Oui |
| `out` | Non défini | Non | Non |

Les cookies suivants sont définis lorsque la configuration du consentement permet :

| Nom | Âge max. | Description |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 jours) | Présent lorsque [`idMigrationEnabled`](../configure/idmigrationenabled.md) est activé. Cela s’avère utile lors de la transition vers le SDK Web alors que certaines parties du site utilisent toujours `visitor.js`. |
| **Cookie Demdex** | 15552000 (180 jours) | Présent si la synchronisation des identifiants est activée. L’Audience Manager définit ce cookie afin d’affecter un identifiant unique à un visiteur du site. Le cookie demdex permet à Audience Manager d’exécuter des fonctions de base, telles que l’identification des visiteurs, la synchronisation des identifiants, la segmentation, la modélisation, la création de rapports, etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutes) | Stocke la région de l’Edge Network qui sert les requêtes de l’utilisateur actuel. La région est utilisée dans le chemin de l’URL afin que l’Edge Network puisse acheminer la requête vers la région appropriée. Si un utilisateur se connecte à une autre adresse IP ou lors d’une autre session, la demande est de nouveau acheminée vers la région la plus proche. |
| **kndct_orgid_identity** | 34128000 (395 jours) | Stocke l’ECID, ainsi que d’autres informations relatives à l’ECID. |
| **kndctr_orgid_consent** | 15552000 (180 jours) | Stocke les préférences de consentement des utilisateurs pour le site web. |
| **s_ecid** | 63115200 (2 ans) | Contient une copie de l’ID Experience Cloud ([!DNL ECID]) ou MID. Le MID est stocké dans une paire clé-valeur qui suit la syntaxe suivante, `s_ecid=MCMID\|<ECID>`. |

## Définition du consentement par défaut à l’aide de l’extension de balise SDK Web

Sélectionnez le bouton radio de votre choix sous **[!UICONTROL Consentement par défaut]** lors de la [ configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Confidentialité], puis sélectionnez le **[!UICONTROL consentement par défaut]** de votre choix.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Définition du consentement par défaut à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la propriété de chaîne `defaultConsent` sur le niveau de consentement souhaité lors de l’exécution de la commande `configure`. Cette propriété est sensible à la casse et ne prend en charge que les trois valeurs suivantes : `"in"`, `"out"` et `"pending"`. Si vous tentez d’utiliser une autre valeur, la bibliothèque renvoie une erreur.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
