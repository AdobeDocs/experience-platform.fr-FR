---
title: Stripe
description: Découvrez comment ingérer des données de paiement de votre compte Stripe vers Adobe Experience Platform
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# [!DNL Stripe]

Des milliers d’entreprises de toutes tailles utilisent [!DNL Stripe] à la fois en ligne et en personne pour accepter les paiements, générer de nouvelles sources de revenus et se développer à l’échelle mondiale avec l’aide de Adobe Experience Platform, Adobe Commerce et [!DNL Magento Open Source].

Utilisez la source de [!DNL Stripe] dans Experience Platform pour ingérer les données capturées par vos clients lors du flux d’achat. Une fois ingérées, utilisez ces données pour créer des offres personnalisées et déverrouiller des informations commerciales plus riches.

>[!TIP]
>
>Pour toute question sur la source de [!DNL Stripe] sur Experience Platform, contactez [!DNL Stripe] à l’adresse adobe-partner<span>@stripe.com.

>[!BEGINSHADEBOX]

**Exemple de cas d’utilisation pour la source de [!DNL Stripe]**

Votre entreprise permet aux clients d&#39;acheter des articles dans votre boutique en ligne avec la possibilité d&#39;**acheter maintenant** et **payer plus tard** (à l&#39;aide de [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] ou [!DNL Zip]).

Utilisez la source de données [!DNL Stripe] pour analyser l’utilisation des options **acheter maintenant** et **payer plus tard** et tester des offres personnalisées auprès de ces clients. Par exemple, pensez à recommander des articles de module complémentaire pour augmenter le nombre d’articles dans leur panier avant de passer en caisse.

>[!ENDSHADEBOX]

Lisez le document ci-dessous pour plus d’informations sur la configuration de votre compte source [!DNL Stripe], la récupération des informations d’identification nécessaires et la création de vos schémas.

## Conditions préalables {#prerequisites}

Les sections suivantes apportent des informations sur la configuration requise avant de connecter votre compte [!DNL Stripe] à Experience Platform.

### Récupérer votre jeton d’accès

* Connectez-vous au [[!DNL Stripe] tableau de bord](https://dashboard.stripe.com/login) en utilisant votre adresse e-mail [!DNL Stripe] et votre mot de passe.
* Dans le tableau de bord de la [!DNL Developers], sélectionnez **[!DNL API keys for developers]**.
* Sous l’onglet **Clés API**, sélectionnez **[!DNL Reveal test key]** pour afficher votre jeton d’accès.
* Vous pouvez désormais utiliser ce jeton comme jeton d’accès lors de la connexion de votre compte [!DNL Stripe] à Experience Platform, à l’aide de l’API [!DNL Flow Service] ou de l’interface utilisateur d’Experience Platform.

### Collecter les informations d’identification requises

Pour connecter votre compte [!DNL Stripe] à Experience Platform, vous devez fournir des valeurs pour les informations d’authentification suivantes :

>[!BEGINTABS]

>[!TAB  API ]

Vous devez fournir les informations d’identification suivantes lors de la connexion de votre compte [!DNL Stripe] à l’aide de l’API [!DNL Flow Service].

| Informations d’identification | Description |
| --- | --- |
| `accessToken` | Jeton d’authentification du code d’actualisation OAuth 2 [!DNL Stripe]. |
| `connectionSpec.id` | Identifiant de spécification de connexion de la source de [!DNL Stripe]. Cet identifiant est corrigé comme suit : `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB UI]

Vous devez fournir les informations d’identification suivantes lors de la connexion de votre compte [!DNL Stripe] à l’aide de l’interface utilisateur d’Experience Platform.

| Informations d’identification | Description |
| --- | --- |
| Jeton d’accès | Jeton d’authentification du code d’actualisation OAuth 2 [!DNL Stripe]. |

>[!ENDTABS]

Pour plus d’informations sur l’utilisation des API [!DNL Stripe], consultez la [[!DNL Stripe] documentation sur les clés API](https://docs.stripe.com/keys).

### Créer un schéma de modèle de données d’expérience (XDM)

La source de [!DNL Stripe] prend en charge l’ingestion des données des chemins d’accès aux ressources suivants :

* Frais
* Abonnements
* Remboursements
* Transactions de solde
* Clientes et clients
* Prix

Vous devez créer un schéma XDM pour décrire un jeu de données, qui peut stocker les champs et les types de données qui seront envoyés de [!DNL Stripe] à Experience Platform.

>[!BEGINTABS]

>[!TAB Frais ]

En [!DNL Stripe], les **frais** représentent des tentatives de transfert d’argent dans votre [!DNL Stripe]. Lisez le [[!DNL Stripe]  Guide de l’API sur les frais &#x200B;](https://docs.stripe.com/api/charges) pour plus d’informations sur les attributs de frais spécifiques.

+++Sélectionnez pour afficher l’objet Stripe Charge  

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Abonnements]

Dans [!DNL Stripe], vous pouvez utiliser **abonnements** pour facturer un client sur une base récurrente. Lisez le guide [[!DNL Stripe] API sur les abonnements](https://docs.stripe.com/api/subscriptions) pour plus d’informations sur les attributs d’abonnement spécifiques.

+++Sélectionnez pour afficher l’objet Abonnement Stripe .

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Remboursements]

En [!DNL Stripe], vous pouvez utiliser **remboursements** pour rembourser des frais créés précédemment. Lisez le [[!DNL Stripe]  Guide de l’API sur les remboursements](https://docs.stripe.com/api/refunds) pour plus d’informations sur les attributs de remboursement spécifiques.

+++Sélectionnez cette option pour afficher l’objet Remboursement Stripe

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Transactions de solde]

En [!DNL Stripe], les **mouvements de solde** représentent le mouvement de fonds entre vos comptes [!DNL Stripe]. Lisez le guide [[!DNL Stripe] API sur les transactions de solde](https://docs.stripe.com/api/balance_transactions) pour plus d&#39;informations sur les attributs spécifiques des transactions de solde.

+++Sélectionnez cette option pour afficher l&#39;objet Transaction solde Stripe

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Clients]

En [!DNL Stripe], les **clients** représentent un client donné de votre entreprise. Pour plus d’informations sur les attributs spécifiques des clients, consultez le guide [[!DNL Stripe] API relatif aux clients](https://docs.stripe.com/api/customers) pour plus d’informations sur les attributs spécifiques des clients.

+++Sélectionner pour afficher l’objet client Stripe

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Prix]

En [!DNL Stripe], les **prix** représentent le coût unitaire, la devise et le cycle de facturation facultatif pour les achats récurrents et uniques de produits. Lisez le guide [[!DNL Stripe] API sur les prix](https://docs.stripe.com/api/prices) pour plus d’informations sur les attributs de prix spécifiques.

+++Sélectionnez pour afficher l’objet Prix Stripe

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

### Configuration des autorisations sur Experience Platform

Les autorisations **[!UICONTROL View Sources]** et **[!UICONTROL Manage Sources]** doivent être activées pour votre compte afin de connecter votre compte [!DNL Stripe] à Experience Platform. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

## Étapes suivantes

Une fois la configuration requise terminée, vous pouvez procéder à la connexion et à l’ingestion de vos données [!DNL Stripe] vers Experience Platform. Lisez les guides suivants pour savoir comment ingérer des données de paiements [!DNL Stripe] vers Experience Platform à l’aide d’API ou de l’interface utilisateur :

* [Ingérez des données de paiements de votre compte Stripe vers Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/payments/stripe.md).
* [Ingérez des données de paiement de votre compte Stripe vers Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/payments/stripe.md).
