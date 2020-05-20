---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Présentation d’Adobe Experience Platform Privacy Service

Pour offrir de meilleures expériences client, vous devez collecter et stocker les données personnelles de vos clients. Lors de l’utilisation de ces données, il est important de comprendre et de respecter la confidentialité de vos clients. Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d&#39;accéder à vos données personnelles ou de les supprimer de vos entrepôts de données sur demande.

Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui vous permet de respecter automatiquement les règles de confidentialité légales et organisationnelles.

## Pourquoi Privacy Service ?

Privacy Service a été développé en réponse à un changement fondamental dans la façon dont les entreprises sont tenues de gérer les données personnelles de leurs clients. Le principal objectif de Privacy Service est d&#39;automatiser la conformité aux règlements sur la confidentialité des données qui, en cas de violation, peuvent entraîner des amendes importantes et perturber les opérations de données de votre entreprise.

### Privacy Service et GDPR

Le règlement [](https://eugdpr.org/) général sur la protection des données (RGPD) a introduit plusieurs nouveaux droits à la vie privée des données pour les membres de l&#39;Union européenne, notamment le **droit d&#39;accès** et le **droit d&#39;être oublié**. Cela signifie que tout citoyen de l&#39;UE dont les données personnelles ont été collectées par votre entreprise peut demander d&#39;accéder à ses données ou de les supprimer à tout moment. Le non-respect de ces demandes dans les 30 jours peut entraîner des amendes de plusieurs millions de dollars pour votre organisation.

Le Service de la protection de la vie privée appuie les demandes d&#39;accès et de suppression de RGMD et les surveille séparément des demandes en vertu du règlement de l&#39;ACPCP. Pour plus d&#39;informations, consultez la FAQ [](gdpr/faq.md) RMMD et les documents [terminologiques](gdpr/terminology.md) .

### Privacy Service et CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. L&#39;ACCP accorde de nouveaux droits à la confidentialité des données aux résidents californiens, y compris le droit d&#39;accéder et de supprimer leurs données personnelles, de savoir si leurs données personnelles sont vendues ou divulguées (et à qui), et le droit de opt-out leurs données d&#39;être vendues à des tiers.

Le Service de la protection de la vie privée appuie les demandes d&#39;accès et de suppression de la réglementation de l&#39;ACCP et les suit séparément des demandes du RPMD. Privacy Service prend également en charge l’envoi de demandes d’exclusion de la vente pour les applications Experience Cloud qui les prennent en charge. Consultez la FAQ [de l&#39;](ccpa/faq.md) ACCP pour en savoir plus.

## Comment utiliser Privacy Service pour gérer les demandes de travaux de confidentialité

Privacy Service fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les demandes de vos clients pour accéder à leurs données privées ou les supprimer, ou pour ne pas les vendre (également connues sous le nom de tâches **de** confidentialité). Le service fournit également un mécanisme central d’audit et de consignation qui vous permet de vue de l’état et des résultats des tâches de confidentialité impliquant des applications Experience Cloud.

>[!NOTE] Actuellement, les demandes d’exclusion ne sont prises en charge que par l’API de Privacy Service.

### Utilisation de l’API

L’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service vous permet de créer et de gérer des tâches de confidentialité à l’aide des appels d’API RESTful, ce qui vous permet d’approcher par programmation la conformité à la réglementation de confidentialité pour vos applications Experience Cloud. Pour obtenir des instructions détaillées sur l’utilisation de l’API, consultez le guide [du développeur de l’API](api/getting-started.md)Privacy Service.

### Utilisation de l’interface utilisateur

L’interface utilisateur de Privacy Service vous permet de créer et de surveiller des tâches de confidentialité à l’aide d’une interface graphique. L’interface utilisateur comprend un widget de rapport **d’** état qui fournit une représentation visuelle de l’état de toutes les requêtes actives et vous permet de créer de nouvelles requêtes à l’aide du créateur **de** requêtes intégré ou en téléchargeant des fichiers JSON. Pour plus d’informations sur l’utilisation de l’interface utilisateur, voir le guide [d’utilisation de](ui/overview.md)Privacy Service.