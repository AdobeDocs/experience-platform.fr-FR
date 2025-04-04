---
title: Présentation de SAP Commerce Source
description: Découvrez comment connecter SAP Commerce à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 14%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>La source [!DNL SAP Commerce] est en version Beta. Voir la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), une solution de plateforme d’e-commerce cloud pour les entreprises B2B et B2C, est disponible dans le cadre du portefeuille d’expériences client SAP. [[!DNL SAP] Facturation des abonnements](https://www.sap.com/products/financial-management/subscription-billing.html) est un produit du portefeuille qui permet une gestion complète du cycle de vie des abonnements avec des expériences de vente et de paiement simplifiées grâce à des intégrations normalisées.

La source [!DNL SAP Commerce] vous permet d’ingérer des informations sur les clients et les contacts dans Experience Platform à partir des points d’entrée de l’API [[!DNL SAP] Facturation des abonnements](https://www.sap.com/products/financial-management/subscription-billing.html) Partenaires commerciaux ci-dessous :

* [Clients](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contacts](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

En outre, si [!DNL SAP Commerce] est exécuté pour récupérer les données client, l’API [ Relations client-contact ](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) est également appelée pour récupérer les informations de contact du client.

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée de données avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant de pouvoir importer vos données [!DNL SAP Commerce] dans Experience Platform, vous devez d’abord vous assurer que vous disposez des éléments suivants :

* Un compte [!DNL SAP Subscription Billing]. Si vous ne disposez pas d’un compte de facturation valide, contactez votre gestionnaire de compte [!DNL SAP]. Reportez-vous au document [[!DNL SAP] Configuration de Platform](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) pour plus d’informations.

* Clé de service [!DNL SAP]. La clé de service [!DNL SAP] vous permet d’accéder à l’API [!DNL SAP Subscription Billing] via Experience Platform. [!DNL SAP Commerce] requiert ce qui suit :
   * Identifiant client
   * Secret client
   * URL. Le modèle d’URL est le suivant : `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Cette valeur sera utilisée ultérieurement pour obtenir des valeurs pour `region` et `tokenEndpoint` lorsque vous [Créez une connexion de base](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) à l’aide de l’API ou lorsque vous [Connectez votre [!DNL SAP Commerce] compte](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) via l’interface utilisateur d’Experience Platform.

+++Sélectionner pour voir un exemple de clé de service

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Étapes suivantes

La documentation ci-dessous fournit des informations sur la connexion de [!DNL SAP Commerce] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

* [Créez une connexion source et un flux de données pour importer  [!DNL SAP Commerce]  données dans Experience Platform à l’aide d’API](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Connectez votre compte  [!DNL SAP Commerce]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Créer un flux de données pour une source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/ecommerce.md)
