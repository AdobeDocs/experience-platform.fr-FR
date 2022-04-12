---
title: Référence de test de configuration
description: Découvrez comment l’Auditor teste les configurations dans Adobe Experience Platform Debugger.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 65%

---

# Référence des tests de configuration

Cette référence fournit des informations supplémentaires sur la manière dont la fonction Auditor de Adobe Experience Platform Debugger exécute des tests de configuration.

>[!NOTE]
>
>Pour plus d’informations sur les tests d’Auditor dans Platform Debugger, voir la section [présentation de la fonctionnalité auditor](./overview.md).

Les tests de configuration recherchent des paramètres, des valeurs ou des conflits potentiels spécifiques dans votre implémentation. Platform Auditor évalue les balises en fonction d’autres règles et des bonnes pratiques recommandées.

| Test | Poids | Critères | Recommandation |
| --- | --- | --- | --- |
| Advertising Cloud : les noms de conversion utilisent uniquement des caractères alphanumériques | 3 | Le `ev_conversion_property_name` ne doit contenir que des valeurs numériques et décimales SAUF pour le paramètre `ev_transid` qui peut contenir du texte ou des valeurs numériques. Recherchez les pixels `everesttech.net`   qui contiennent un paramètre d’URL commençant par  `ev_`. | Assurez-vous que les paramètres de propriété de transaction contiennent uniquement des valeurs numériques et décimales.<br><br>Avertissement : tout autre type de valeur peut entraîner une perte de données. |
| Advertising Cloud : les noms de conversion utilisent uniquement des caractères autorisés pour les URL | 3 | Les noms des propriétés de conversion ne doivent pas contenir d’esperluette ni de point d’interrogation. | Assurez-vous que les paramètres de propriété de transaction ne contiennent pas d’esperluette ni de point d’interrogation non codé. Ces caractères rompent le format d’URL.<br><br>Avertissement : Paramètres de propriété contenant une esperluette ou un point d’interrogation non codé (par exemple :  `ev_formComplete?=1` ou  `ev_formComplete&Submit=1`), peut entraîner une perte de données. |
| Advertising Cloud : ID de transaction correctement implémentée | 1 | Nom de la propriété  `ev_transid=` ne doit pas être vide. | Nom de la propriété  `ev_transid=` ne doit pas être laissé sans valeur. En l’absence de valeur, vous pourriez subir des pertes de données de transaction. Attribuer une valeur à `ev_transid=` ou supprimez le paramètre du pixel. |
| Analytics : instancié dans DOM | 5 | Le code Adobe Analytics n’est pas installé ou ne s’exécute pas. Renvoie 0 lorsqu’aucun code Analytics n’est trouvé sur la page web. | Vérifiez que la balise Analytics est implémentée sur la page et n’est pas bloquée par les activités de script suivantes.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr) |
| Analytics : instancié une fois | 5 | Le code Adobe Analytics a été détecté plusieurs fois sur la page. Renvoie 0 lorsqu’aucun code Analytics n’est trouvé sur la page web. | Assurez-vous qu’il n’y a qu’une seule balise Analytics sur la page.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics : version la plus récente | 3 | Vos pages n’exécutent pas la dernière version de la bibliothèque de codes Analytics. Les bibliothèques de codes qui alimentent les technologies Experience Cloud sont constamment mises à jour et modifiées afin de tirer parti des améliorations de performances et de fournir les dernières fonctionnalités. Renvoie 0 lorsqu’aucun code Analytics n’est trouvé sur la page web. | Installez la dernière version de la bibliothèque Analytics.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=fr) |
| Launch : les balises tierces se chargent de manière asynchrone une fois le modèle DOM prêt | 3 | Pour trouver un équilibre entre une bonne expérience utilisateur et la collecte de données précises, les balises tierces doivent être déclenchées dès que le modèle DOM est prêt. Cela permet de s’assurer que ces scripts de suivi s’exécutent sans affecter la fonctionnalité du site. | Résolvez ce problème en ajustant toutes les règles qui exécutent des pixels tiers pour qu’ils se déclenchent à l’aide de DOM Ready (Prêt pour DOM).<br><br>[Informations supplémentaires](../../tags/ui/managing-resources/rules.md) |
| Service Experience Cloud ID : dernière version | 2 | Vos pages n’exécutent pas la dernière version de la bibliothèque de codes du service d’identification des visiteurs,  visitorAPI.js. Les bibliothèques de codes qui alimentent les technologies Experience Cloud sont constamment mises à jour et modifiées afin de tirer parti des améliorations de performances et de fournir les dernières fonctionnalités. | Installez la dernière version de la bibliothèque du service d’identification des visiteurs.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch : version la plus récente | 2 | Ces pages n’exécutent pas la dernière version de la bibliothèque de codes de balises (Turbine). Les bibliothèques de codes qui alimentent les technologies Experience Cloud sont constamment mises à jour et modifiées afin de tirer parti des améliorations de performances et de fournir les dernières fonctionnalités. | Recréez et publiez la bibliothèque de balises.<br><br>[Informations supplémentaires](../../tags/quick-start/quick-start.md) |
| Target : version la plus récente | 2 | Vos pages n’exécutent pas la dernière version de la bibliothèque de codes Target. Les bibliothèques de codes qui alimentent les technologies Experience Cloud sont constamment mises à jour et modifiées afin de tirer parti des améliorations de performances et de fournir les dernières fonctionnalités. | Installez la dernière version de la bibliothèque Target.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html) |
| Target : mboxDefault précède mboxCreate | 5 | L’utilisation correcte de  mboxCreate ressemble à ceci :<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Veillez à inclure une  `<div class="mboxDefault"></div>` avant d’appeler mboxCreate(). at.js ne le fera pas à votre place.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html) |
| Target : DOCTYPE valide | 5 | Un DOCTYPE non valide a été détecté. Aucune mbox ne sera déclenchée dans ce scénario.  Pour at.js, le DOCTYPE doit être en mode standard, sinon Target ne fonctionnera pas. | Mettez à jour le DOCTYPE sur la page.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/faq-at-js/target-atjs-faq.html) |

{style=&quot;table-layout:auto&quot;}
