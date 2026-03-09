---
title: Accéder à l’assistant AI (hérité) dans Experience Platform
description: Découvrez comment accéder à l’assistant AI dans l’interface utilisateur d’Experience Cloud.
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: 077c42f2190316a00168bbeca685c08677c2b13a
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# Accéder à l’assistant AI (hérité) dans Experience Platform

>[!IMPORTANT]
>
>Ce document s’applique à l’assistant d’IA (hérité). Pour plus d’informations sur l’assistant AI (Next-Gen), consultez le guide de l’interface utilisateur de l’assistant [AI](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) dans la documentation [AI dans Experience Cloud](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/home).

Reportez-vous au tableau suivant pour une comparaison de l’assistant AI (hérité) et de l’assistant AI (nouvelle génération) :

| Domaine de fonctionnalités | Assistant AI (hérité) | Assistant IA (nouvelle génération) |
| --- | --- | --- |
| Expérience utilisateur | L’assistant d’IA (hérité) est disponible dans un panneau du rail de droite uniquement. | L’assistant d’IA (version suivante) est disponible dans le panneau du rail droit et dans une expérience immersive en plein écran. |
| Portée des fonctionnalités | Vous pouvez utiliser l’assistant d’IA (hérité) pour obtenir des connaissances sur les produits et des informations opérationnelles. | Vous pouvez utiliser l’assistant d’IA (nouvelle génération) pour acquérir des connaissances sur les produits, obtenir des informations opérationnelles, ainsi que des compétences avancées en matière d’agentisme et exécuter des tâches en plusieurs étapes. |
| Architecture de Platform | L’assistant AI (hérité) n’est pas créé sur la pile Agent Orchestrator. | L’assistant d’IA (nouvelle génération) est optimisé par [Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator), ce qui permet l’extensibilité et une coordination avancée entre les fonctionnalités. |
| Couverture de l’application | L’assistant d’IA (hérité) est une implémentation spécifique à l’application. | Vous pouvez utiliser l’assistant d’IA (version suivante) pour une expérience d’assistant d’IA unifiée dans toutes les applications Adobe Experience Cloud. |
| Modèle d’accès et d’autorisation | Modèle d’accès au niveau de l’application aligné sur les limites de chaque produit. | Tous les utilisateurs ont accès à l’assistant AI (version suivante) et aux agents Experience Platform associés. **Remarque** : <ul><li>**Adobe Experience Manager** : votre administrateur doit vous accorder l’autorisation d’accéder à l’assistant AI (Next-Gen) via [Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).</li><li>**Customer Journey Analytics** : votre administrateur doit vous accorder l’autorisation d’accéder à l’assistant AI par le biais du contrôle d’accès de [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/technotes/access-control?lang=en). Cela vous permet de poser des questions sur la connaissance des produits et les informations sur les données. |

Vous pouvez accéder à l’assistant d’IA (hérité) dans plusieurs applications de Adobe Experience Cloud.

>[!NOTE]
>
>Si vous recevez un message contextuel dans l’interface utilisateur des autorisations qui vous informe que votre organisation doit d’abord accepter des termes juridiques supplémentaires afin d’accéder à l’assistant d’IA (hérité), contactez votre équipe de compte Adobe pour obtenir des conseils sur ces termes.

## Commencer {#get-started}

Vous devez effectuer deux étapes préalables avant de pouvoir accéder à l’assistant AI (hérité).

1. Votre entreprise doit d’abord accepter les conditions juridiques. Pour plus d’informations, contactez l’équipe chargée de votre compte Adobe.
2. Vos administrateurs doivent vous accorder les autorisations suffisantes pour accéder à l’assistant AI (hérité).

Si l’une de ces deux étapes préalables n’est pas terminée, les messages suivants s’affichent lorsque vous sélectionnez l’icône de conversation de l’assistant d’IA (hérité) dans l’interface utilisateur d’Experience Platform.

>[!BEGINTABS]

>[!TAB Votre entreprise ne peut pas utiliser l’assistant AI (hérité)]

Le message suivant s’affiche si vous utilisez une organisation qui n’est pas légalement autorisée à utiliser l’assistant AI (hérité). Dans ce scénario, vous devez contacter l’équipe de votre compte Adobe pour résoudre les problèmes d’accès.

![Message contextuel qui s’affiche dans l’interface utilisateur d’Experience Platform si l’entreprise ne peut pas utiliser l’assistant AI (hérité).](./images/access/modal-one.png)

>[!TAB Vous ne disposez pas des autorisations appropriées]

Si votre entreprise est légalement autorisée à utiliser l’assistant AI (hérité) et que vous ne pouvez toujours pas accéder à la fonctionnalité, le message suivant s’affiche dans l’interface utilisateur d’Experience Platform. Ce scénario signifie que vous ne disposez pas des autorisations suffisantes pour accéder à la fonctionnalité et que vous devez contacter vos administrateurs ou administratrices pour résoudre les problèmes liés aux autorisations.

![Message contextuel qui s’affiche sur l’interface utilisateur d’Experience Platform si vous ne disposez pas des autorisations nécessaires pour l’assistant AI (hérité).](./images/access/modal-two.png)

>[!ENDTABS]

## Accéder à l’assistant d’IA (hérité) {#get-access-to-ai-assistant}

L’accès à l’assistant d’IA (hérité) est régi par les paramètres suivants :

* **Accéder à l’application :** vous pouvez accéder à l’assistant AI (hérité) dans Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer et [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant (Legacy). Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant (Legacy).  -->
* **Autorisations :** utilisez l’[interface utilisateur des autorisations](../access-control/abac/ui/permissions.md) pour accorder ou révoquer l’accès à l’assistant d’IA (hérité) de votre organisation. Pour utiliser l’assistant d’IA (hérité), un utilisateur donné doit appartenir à un rôle disposant des autorisations **Activer l’assistant d’IA** et **Afficher les informations opérationnelles**.
   * En tant qu’administrateur ou administratrice, vous pouvez ajouter l’**Activer l’assistant AI** à un rôle donné et ajouter un utilisateur ou une utilisatrice à ce rôle, pour lui permettre d’accéder à l’assistant AI (hérité) dans votre organisation. **Remarque** : cette autorisation permet audit utilisateur d’accéder à l’assistant AI (hérité), elle ne lui accorde aucune capacité administrative pour donner ensuite à d’autres utilisateurs accès à l’assistant AI (hérité).
   * En tant qu’administrateur, vous pouvez ajouter l’**Afficher les informations opérationnelles** à un rôle donné et ajouter un utilisateur à ce rôle, pour lui permettre d’utiliser les fonctionnalités d’informations opérationnelles de l’assistant AI (hérité).

Utilisez l’[interface utilisateur des autorisations](../access-control/abac/ui/roles.md) pour accorder des autorisations d’utilisation de l’assistant AI (hérité) dans Experience Platform et Journey Optimizer. Pour plus d’informations sur l’accès à l’assistant AI (hérité) dans Customer Journey Analytics. Lisez la documentation dans [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).

![Page de l’interface utilisateur des autorisations avec les autorisations Activer l’assistant d’IA (hérité) et Afficher les informations opérationnelles incluses dans un rôle donné.](./images/access/access-permissions.png)

Une fois que vous disposez des autorisations nécessaires, vous pouvez accéder à l’assistant AI (hérité) en sélectionnant l’icône de l’assistant AI (hérité) dans l’en-tête supérieur de l’application que vous utilisez.

![Assistant AI (hérité) avec une première expérience utilisateur.](./images/access/access-home.png)

Regardez la vidéo suivante pour savoir comment configurer l’accès à l’assistant d’IA (hérité) pour vos organisations et utilisateurs.

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## Étapes suivantes

Une fois que vous disposez d’un accès complet à l’assistant AI (hérité), vous pouvez passer à l’utilisation de la fonctionnalité au cours de vos workflows. Pour plus d’informations, consultez le guide de l’interface utilisateur [Assistant AI (hérité)](./ui-guide.md) .
