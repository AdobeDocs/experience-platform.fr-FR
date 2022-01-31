---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Correspondance de segment;correspondance de segment
solution: Experience Platform
title: FAQ sur la correspondance de segment
description: La correspondance de segment est un service de partage de segments dans Adobe Experience Platform qui permet à deux utilisateurs ou plus de Platform d’échanger des données de segment de manière sécurisée, gérée et respectueuse de la confidentialité.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 823eb549e5514a3201ba68ed395c69e202cb747f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# [!DNL Segment Match] questions fréquentes

Ce guide répond aux questions juridiques et de confidentialité souvent posées sur la correspondance de segment Adobe Experience Platform.

## Quelles données sont partagées lors des chevauchements d’estimations et comment l’Adobe peut-il m’assurer que ces mesures sont obtenues en toute sécurité ?

![duplicate.png](./images/overlap-report.png)

Aucune donnée de client ou de segment n’est déplacée dans les environnements de test pour obtenir ces mesures d’estimation de chevauchement. Les identités applicables sélectionnées par le client et préhachées dans un environnement de test donné sont ajoutées à une structure de données probabiliste dans laquelle les identifiants eux-mêmes sont représentés dans un format haché.

Il s’agit d’un processus à sens unique, ce qui signifie que les identifiants préhachés d’origine ne sont pas exposés et ne peuvent pas être modifiés à l’envers.

Ces structures de données possèdent des propriétés uniques qui permettent à l’ingénierie d’effectuer des opérations d’union et d’intersection entre elles, même si les informations codées sont considérablement compressées ou hachées. Ces opérations permettent [!DNL Segment Match] pour obtenir l’intersection estimée de deux structures de données composées d’identifiants à partir de deux environnements de test différents sans avoir à comparer les valeurs réelles. Depuis [!DNL Segment Match] utilise uniquement les structures de données, les identifiants ne conservent jamais les entrepôts de profils de leurs organisations IMS respectives à des fins d’estimation. Cela permet à l’Adobe de répondre aux exigences de confidentialité et de sécurité des clients tout en offrant des outils d’estimation très précis pour guider les accords de collaboration sur les données.

## Quel est le processus derrière la désignation des identités qui reçoivent les identités de segment partagées ?

[!DNL Segment Match] permet aux clients de configurer les espaces de noms à utiliser dans le service. Cette sélection s’applique à la fois au processus d’estimation décrit dans la question précédente et au processus de transfert de données, si le client décide de publier le flux sur un environnement de test partenaire.

Le processus de transfert de données entre les identités chiffrées de deux organisations différentes est effectué dans un environnement informatique neutre. La tâche de transfert de données appartient à Adobe, et les organisations impliquées dans le partenariat n’ont pas accès à cet environnement, et n’ont pas non plus accès aux journaux susceptibles d’être un résultat de la tâche de transfert de données.

Seul l’appartenance au segment est ingéré dans les fragments de profil se chevauchant d’une organisation IMS récepteur et aucune identité supplémentaire n’est transférée de l’organisation IMS expéditeur à l’organisation IMS récepteur. Aucune information d’identification personnelle (PII) en texte brut n’est lue par la tâche de transfert de données, car [!DNL Segment Match] permet des recouvrements uniquement sur les espaces de noms chiffrés SHA256 (email/téléphone) lorsque les données sont des informations d’identification personnelles. Les résultats ne sont jamais stockés dans l’environnement informatique.
