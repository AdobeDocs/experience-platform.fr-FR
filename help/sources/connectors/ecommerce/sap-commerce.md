---
title: Présentation de SAP Commerce Source
description: Découvrez comment connecter SAP Commerce à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Version bêta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 19%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>La source [!DNL SAP Commerce] est en version Beta. Pour plus d’informations sur l’utilisation de sources étiquetées bêta, consultez la [présentation des sources](../../home.md#terms-and-conditions) .

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), une solution de plateforme de commerce électronique basée sur le cloud pour les entreprises B2B et B2C est disponible dans le cadre du portefeuille d’expérience client SAP. [[!DNL SAP] La facturation des abonnements](https://www.sap.com/products/financial-management/subscription-billing.html) est un produit du portefeuille qui permet une gestion complète du cycle de vie des abonnements avec des expériences de vente et de paiement simplifiées grâce à des intégrations normalisées.

La source [!DNL SAP Commerce] vous permet d’ingérer des informations sur les clients et les contacts dans Platform à partir des points d’entrée de l’API [[!DNL SAP]  Subscription Billing](https://www.sap.com/products/financial-management/subscription-billing.html) Business Partners ci-dessous :

* [Clients](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contacts](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

De plus, si [!DNL SAP Commerce] est exécuté pour récupérer les données client, l’API [Customer-Contact Relationships](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) est également appelée pour récupérer les informations de contact du client.

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant de pouvoir importer vos données [!DNL SAP Commerce] dans Experience Platform, vous devez d’abord vous assurer que vous disposez des éléments suivants :

* Un compte [!DNL SAP Subscription Billing]. Si vous ne disposez pas déjà d’un compte de facturation valide, contactez votre gestionnaire de compte [!DNL SAP]. Pour plus d’informations, consultez le document [[!DNL SAP] Configuration de la plateforme](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) .

* Clé de service [!DNL SAP]. La clé de service [!DNL SAP] vous permet d’accéder à l’API [!DNL SAP Subscription Billing] via Experience Platform. [!DNL SAP Commerce] requiert ce qui suit :
   * Identifiant client
   * Secret client
   * URL. Le modèle d’URL est le suivant : `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Cette valeur sera utilisée ultérieurement pour obtenir des valeurs pour `region` et `tokenEndpoint` lorsque vous [ créez une connexion de base ](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) à l’aide de l’API ou lorsque vous [connectez votre  [!DNL SAP Commerce] compte](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) via l’interface utilisateur de Platform.

+++Sélectionnez cette option pour afficher un exemple de clé de service.

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

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL SAP Commerce] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Créez une connexion source et un flux de données pour importer [!DNL SAP Commerce] des données vers Platform à l’aide d’API](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Connectez votre compte  [!DNL SAP Commerce] à l’Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Créer un flux de données pour une source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/ecommerce.md)
