---
keywords: Experience Platform ; accueil ; sujets populaires ; RGD ; RGD ; RGD ; APCCP ; APC ; APP ; APP ; Pdpa ; LGPD ; lgpd ; faq ; FAQ ; réglementation ; réglementation ; réglementation ; réglementation ; réglementation ; respect de la vie privée ; confidentialité ; confidentialité ;
solution: Experience Platform
title: FAQ sur le Règlement sur la confidentialité
topic-legacy: troubleshooting
description: Ce document fournit des réponses aux questions les plus fréquemment posées sur les réglementations en matière de protection des renseignements personnels et leur mise en oeuvre à Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 35%

---

# FAQ sur les règles de confidentialité

Ce document fournit des réponses aux questions les plus fréquemment posées sur les réglementations en matière de protection des renseignements personnels et leur mise en oeuvre à Adobe Experience Cloud.

>[!NOTE]
>
>Les définitions des différents termes utilisés dans ce document se trouvent dans le [guide de la terminologie de la réglementation de la protection des renseignements personnels](terminology.md).

## Questions générales

Les questions suivantes portent sur toutes les règles de protection des renseignements personnels appuyées par l&#39;Experience Cloud.

### Quelles sont les répercussions des réglementations prises en charge en matière de confidentialité ?

La [réglementation sur la protection de la vie privée appuyée par l&#39;Experience Cloud](./overview.md) s&#39;applique à toutes les organisations qui stockent et traitent les données personnelles des citoyens dans les juridictions respectives de la réglementation, quel que soit le lieu géographique de l&#39;organisation.

### Que signifie la notion de données personnelles ?

Les données personnelles constituent toute information relative à une personne physique ou à un sujet des données qui peut être utilisée pour identifier directement ou indirectement la personne. Il peut s’agir d’un nom, d’une photo, d’une adresse électronique, de détails bancaires, de publications sur les réseaux sociaux, d’informations médicales ou de l’adresse IP d’un ordinateur.

Les identifiants suivants sont couramment utilisés dans les applications Experience Cloud et pourraient être assujettis aux exigences de la réglementation en matière de confidentialité :

* Nom
* Adresse postale
* Identifiant personnel unique
* Identifiant en ligne
* Adresse IP
* Adresse électronique
* Nom du compte

Les informations personnelles peuvent aussi inclure les renseignements liés à l’activité sur Internet ou sur d’autres réseaux électroniques. Cela inclut, entre autres :

* L’historique de navigation
* L’historique des recherches
* Les informations relatives à l’interaction d’un client avec un site web, une application ou une publicité

Bien que les règlements sur la protection des renseignements personnels couvrent un large éventail de renseignements personnels, les termes standard du contrat de l’Adobe stipulent que les renseignements personnels sensibles (tels que les NSS, les renseignements sur le permis de conduire, les renseignements sur les comptes financiers et les données biométriques) sont généralement interdits d’importation et d’utilisation dans les applications Experience Cloud.

### Quelle est la différence entre le contrôleur des données et le responsable du traitement des données ?

Le **contrôleur des données** est l’entité qui détermine les finalités, conditions et moyens du traitement des données personnelles, tandis que l’**entité de traitement des données** est une entité qui traite les données personnelles pour le compte du contrôleur des données.

Un **contrôleur de données** est la personne ou l&#39;organisation qui a le pouvoir et la responsabilité de prendre des décisions concernant la collecte, l&#39;utilisation ou la divulgation de données à caractère personnel. Un **processeur de données** est la personne ou l&#39;organisation qui opère en relation avec la collecte, l&#39;utilisation ou la divulgation des données à caractère personnel et la direction du contrôleur de données.

### Quelle est la différence entre le consentement explicite et le consentement univoque du sujet des données ?

**Il** y a lieu de considérer explicitement une norme de consentement prévoyant une indication précise, informée et sans ambiguïté des souhaits de la personne concernée, sous forme orale ou écrite. En d&#39;autres termes, la personne concernée doit littéralement et explicitement dire &quot;je consens&quot; ou &quot;je suis d&#39;accord&quot; pour que le consentement soit considéré comme explicite. En outre, il doit être aussi facile de retirer le consentement que de le donner.

**Il** s&#39;agit d&#39;un consentement sans ambiguïté (implicite) qui n&#39;a pas été explicitement donné par la personne concernée, mais qui n&#39;en est pas moins sans ambiguïté. Par exemple, pendant le processus d&#39;inscription à un site Web de société, un avis est donné qu&#39;en fournissant une adresse électronique, la personne concernée consent à recevoir des courriels sur des offres spéciales. Si la personne concernée lit l&#39;avis, la discrimination positive à l&#39;égard de la saisie de son courriel est suffisante pour être considérée comme un consentement sans ambiguïté.

Pour de nombreuses réglementations comme le RGPD, un consentement explicite est nécessaire pour traiter des données personnelles sensibles, où rien de moins que &quot;opt-in&quot; ne suffira. Toutefois, pour les données non sensibles, le consentement explicite (implicite) est acceptable.

### Les personnes âgées de moins d&#39;un certain âge peuvent-elles donner leur consentement ?

De nombreuses réglementations sur la protection des renseignements personnels stipulent que si une personne concernée a moins d&#39;un certain âge, elle ne peut légalement consentir à la collecte de ses données personnelles. Dans certains cas, le titulaire de la responsabilité parentale peut donner son consentement à cette personne, mais pas tous. Le tableau suivant liste l&#39;âge minimum pour que les personnes concernées puissent donner leur propre consentement à chaque règlement, avec des notes pour plus d&#39;informations :

| Réglementation | Âge du consentement | Notes |
| --- | --- | --- |
| CCPA (Californie) | 16 | <ul><li>Le consentement parental ne peut être donné que pour les personnes âgées de 13 ans ou plus.</li><li>La collecte de données à caractère personnel auprès de personnes de moins de 13 ans est strictement interdite.</li></ul> |
| RGPD (Union européenne) | 16 | <ul><li>Certains États membres de l&#39;UE peuvent prévoir à cette fin une loi pour un âge inférieur, mais pas inférieur à 13 ans.</li><li>Le consentement parental doit être fourni pour toutes les personnes dont l&#39;âge est inférieur à la limite d&#39;âge.</li></ul> |
| LGPD (Brésil) | 13 | <ul><li>Le consentement parental doit être fourni pour toutes les personnes dont l&#39;âge est inférieur à la limite d&#39;âge.</li><li>Le consentement peut être donné par une personne physique âgée de 13 à 18 ans, pour autant que le traitement de ses données à caractère personnel soit effectué dans leur intérêt supérieur.</li></ul> |
| PDPA (Thaïlande) | 10 | <ul><li>Le consentement parental doit être fourni pour toutes les personnes dont l&#39;âge est inférieur à la limite d&#39;âge.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Combien de jours une entreprise a-t-elle pour répondre à la demande d’un client souhaitant consulter ou supprimer des informations personnelles ?

En supposant que l&#39;entreprise ait recueilli des renseignements personnels et qu&#39;elle puisse s&#39;authentifier ou vérifier l&#39;identité d&#39;un consommateur particulier, la réglementation sur la protection des renseignements personnels permet de respecter un délai précis pour qu&#39;une demande de consommateur soit satisfaite. Le tableau suivant ventile les délais applicables pour chaque règlement, avec des notes sur certaines exceptions :

| Réglementation | Fenêtre de conformité | Notes |
| --- | --- | --- |
| CCPA (Californie) | 45 jours |  |
| RGPD (Union européenne) | 30 jours | Si la demande est complexe ou si de nombreuses demandes ont été faites par la même personne concernée, la demande peut être prolongée à 60 jours. |
| LGPD (Brésil) | 15 jours |  |
| PDPA (Thaïlande) | 30 jours | Si une société ne peut pas répondre à la demande d&#39;une personne concernée dans le délai de conformité, la société disposera de 30 jours supplémentaires à compter de la date à laquelle elle n&#39;a pas été en mesure de répondre par écrit à la personne concernée. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Mon entreprise doit-elle nommer un délégué à la protection des données ?

Si les opérations de données de votre organisation relèvent des juridictions du RGPD, LGPD ou PDPA, vous devez nommer un agent de protection des données (DPO) dans les cas suivants :

* Votre organisation est une autorité publique
* Votre entreprise s&#39;engage dans une surveillance systématique à grande échelle
* Votre entreprise s’engage dans le traitement à grande échelle de données personnelles sensibles.

>[!IMPORTANT]
>
>Contrairement à d&#39;autres règlements, l&#39;ACFPC stipule que c&#39;est une exigence. Cependant, il est généralement recommandé que, pour maintenir la conformité à la vie privée, une société ait une activité de collecte de données de surveillance individuelle qualifiée et l&#39;enregistrement de données sur les consommateurs, ainsi que de répondre aux demandes de renseignements des clients.

### Comment puis-je prendre en charge les demandes de protection de la vie privée des consommateurs si je tiens à jour des données couvertes par la réglementation sur la protection de la vie privée ?

Une fois que vous avez pris les mesures nécessaires pour authentifier les consommateurs qui relèvent des juridictions légales appropriées, Adobe Experience Platform Privacy Service vous permet de soumettre des demandes de protection de la vie privée des consommateurs à des applications Experience Cloud compatibles. Pour plus d’informations, consultez [[!DNL Privacy Service] aperçu des ](../home.md). Pour plus d’informations sur la manière dont vos applications Experience Cloud spécifiques peuvent répondre aux demandes de confidentialité, reportez-vous au guide sur les [applications Privacy Service et Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>L’autorité de régulation californienne donnera prochainement des indications supplémentaires sur les types de données concernés par les demandes de protection de la vie privée des clients.

## Questions relatives à l&#39;ACCP

Les questions qui suivent portent spécifiquement sur l&#39;ACCP.

### Comment les différents rôles et responsabilités de la CCPA s’appliquent-ils à Experience Cloud ?

Selon la définition de la CCPA, s’appliquent à Adobe et à ses clients les rôles suivants :

* Les clients Adobe (la partie demandant la collecte et l’utilisation d’informations personnelles auprès des résidents de Californie) seraient considérés comme une **Entreprise**.
* Adobe, qui fournit le service, serait considéré comme un **Fournisseur de services**.

En tant que Fournisseur de services, Adobe collecte et traite des informations personnelles pour le compte de l’Entreprise. Il est contractuellement tenu d’utiliser ces informations uniquement aux finalités spécifiques définies dans le contrat.

Compte tenu de cette relation et du libellé du contrat de l&#39;Adobe, les divulgations à l&#39;Adobe ne seraient probablement pas considérées comme une &quot;vente&quot; pour laquelle les entreprises devraient fournir un avis et demander leur consentement.

Cependant, les services Adobe peuvent être utilisés pour activer certains partages et transferts de données vers des tiers. Ces transferts de tiers pourraient être considérés comme une &quot;vente&quot; et nécessiter légalement la divulgation et le consentement. Les clients doivent se rapprocher de leur service juridique pour examiner des cas d’utilisation spécifiques afin d’évaluer les exigences applicables.

### Adobe propose-t-il d’autres outils pouvant être utiles pour répondre aux exigences de la CCPA ?

Les applications Adobe Experience Cloud fournissent des fonctionnalités de gestion et de gouvernance qui peuvent être utiles pour les besoins de confidentialité des entreprises. Parmi ces outils figurent l’étiquetage de l’utilisation des données, les contrôles d’accès basés sur les rôles, l’obscurcissement de l’adresse IP et les fonctions de hachage.

Adobe a reçu diverses certifications pour ses pratiques en matière de confidentialité et de sécurité, telles qu’une certification ISO 27001 et une validation RGPD de TrustArc.

## Questions relatives au RDPR

Les questions qui suivent portent spécifiquement sur le RGD.

### Quelle est la différence entre un règlement et une directive ?

Un **règlement** constitue un acte législatif contraignant qui doit être appliqué dans son intégralité au sein de l’UE. Une **directive** est un acte législatif qui définit un objectif que tous les pays de l’UE doivent atteindre, mais c’est à chacun des pays de décider la manière dont ils souhaitent procéder pour y parvenir.

Il faut souligner que le RGPD est un règlement, contrairement à la législation précédente (la directive sur la protection des données personnelles), qui est une directive.

### De quelle manière le RGPD influe-t-il sur les politiques relatives aux violations des données ?

Les règlements proposés au sujet des violations des données concernent principalement les politiques de notification des entreprises qui ont été compromises. Les violations des données susceptibles de présenter un risque pour les individus doivent être notifiées à l’autorité de protection des données dans un délai de 72 heures et aux personnes concernées sans retard excessif.

## Questions relatives à PDPA

Les questions suivantes se rapportent spécifiquement à l&#39;APPE.

### Qu’est-ce que les données personnelles sensibles ?

La loi sur la protection des renseignements personnels (PDPA) prévoit des exigences strictes pour la collecte et l&#39;enregistrement de données à caractère personnel sensibles, y compris les données à caractère personnel concernant : origine raciale ou ethnique, opinions politiques, croyances religieuses ou philosophiques, casiers judiciaires, adhésion à l&#39;union commerciale, données génétiques, données biométriques, dossiers de santé et orientation ou préférences sexuelles.
