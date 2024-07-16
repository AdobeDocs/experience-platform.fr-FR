---
keywords: Experience Platform;accueil;rubriques les plus consultées;RGPD;rgpd;CCPA;ccpa;PDPA;pdpa;LGPD;lgpd;faq;FAQ;réglementation;réglementation;réglementations;réglementation;confidentialité;confidentialité;confidentialité
solution: Experience Platform
title: FAQ sur les réglementations de confidentialité
description: Ce document répond aux questions les plus fréquemment posées sur les réglementations de confidentialité légales prises en charge et leur mise en oeuvre dans Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 32%

---

# FAQ sur les réglementations relatives à la confidentialité

Ce document répond aux questions les plus fréquemment posées sur les réglementations de confidentialité légales prises en charge et leur mise en oeuvre dans Adobe Experience Cloud.

>[!NOTE]
>
>Les définitions des différents termes utilisés dans ce document se trouvent dans le guide [terminologie de la réglementation de la confidentialité](terminology.md).

## Questions générales

Les questions suivantes concernent toutes les réglementations de confidentialité prises en charge par Experience Cloud.

### Quelles sont les répercussions des réglementations de confidentialité prises en charge ?

Les [réglementations de confidentialité prises en charge par Experience Cloud](./overview.md) s’appliquent à toutes les organisations qui stockent et traitent les données personnelles des citoyens dans les juridictions respectives des réglementations, quel que soit l’emplacement géographique de l’organisation.

### Que signifie la notion de données personnelles ?

Les données personnelles constituent toute information relative à une personne physique ou à un titulaire de données qui peut être utilisée pour identifier directement ou indirectement la personne. Il peut s’agir d’un nom, d’une photo, d’une adresse e-mail, de détails bancaires, de publications sur les réseaux sociaux, d’informations médicales ou de l’adresse IP d’un ordinateur.

Les identifiants suivants sont couramment utilisés dans des applications Experience Cloud et peuvent être soumis à des exigences de réglementation en matière de confidentialité :

* Nom
* Adresse postale
* Identifiant personnel unique
* Identifiant en ligne
* Adresse IP
* Adresse e-mail
* Nom du compte

Les informations personnelles peuvent aussi inclure les renseignements liés à l’activité sur Internet ou sur d’autres réseaux électroniques. Cela inclut, entre autres :

* L’historique de navigation
* L’historique des recherches
* Les informations relatives à l’interaction d’un client avec un site web, une application ou une publicité

Même si les réglementations de confidentialité couvrent un large éventail d&#39;informations personnelles, les termes du contrat standard de l&#39;Adobe stipulent que les informations personnelles sensibles (telles que le numéro de sécurité sociale, les informations de permis de conduire, les informations de compte financier et les données biométriques) sont généralement interdites d&#39;importation et d&#39;utilisation dans les applications Experience Cloud.

### Quelle est la différence entre le contrôleur des données et le responsable du traitement des données ?

Le **contrôleur des données** est l’entité qui détermine les finalités, conditions et moyens du traitement des données personnelles, tandis que l’**entité de traitement des données** est une entité qui traite les données personnelles pour le compte du contrôleur des données.

Un **contrôleur des données** est la personne ou l’organisation qui a le pouvoir et la responsabilité de prendre des décisions concernant la collecte, l’utilisation ou la divulgation de données personnelles. Un **responsable du traitement des données** est la personne ou l’organisation qui fonctionne en relation avec la collecte, l’utilisation ou la divulgation des données personnelles et la direction du contrôleur des données.

### Quelle est la différence entre le consentement explicite et le consentement univoque du titulaire de données ?

**Consentement explicite** fait référence à une norme de consentement qui implique une indication spécifique, éclairée et sans ambiguïté des souhaits du sujet de données sous forme orale ou écrite. En d’autres termes, le sujet des données doit littéralement et explicitement dire &quot;J’accepte&quot; ou &quot;Je suis d’accord&quot; pour que le consentement soit considéré comme explicite. En outre, il doit être aussi facile de retirer le consentement que de le donner.

**Consentement non ambigu (implicite)** fait référence au consentement qui n’a pas été explicitement donné par le sujet des données, mais qui n’en est pas moins de nature non ambiguë. Par exemple, lors du processus d’inscription à un site web d’entreprise, un avis est donné qu’en fournissant une adresse électronique, le sujet des données accepte de recevoir des emails sur des offres spéciales. Si le sujet des données lit l&#39;avis, la discrimination positive consistant à entrer dans son email est suffisante pour être considérée comme un consentement univoque.

Pour de nombreuses réglementations comme le RGPD, un consentement explicite est requis pour le traitement de données personnelles sensibles, où rien d’autre que &quot;opt-in&quot; ne suffira. Toutefois, pour les données non sensibles, le consentement univoque (implicite) est acceptable.

### Les sujets des données de moins d’un certain âge peuvent-ils donner leur consentement ?

De nombreuses réglementations de confidentialité stipulent que si un sujet des données est âgé de moins d’un certain âge, il ne peut légalement fournir de consentement pour la collecte de ses données personnelles. Dans ces cas-ci, certaines réglementations autorisent le consentement du détenteur de la responsabilité parentale pour ce sujet de données, mais pas tous. Le tableau suivant répertorie l’âge minimum pour que les sujets des données puissent fournir leur propre consentement pour chaque réglementation, avec des notes pour plus d’informations :

| Réglementation | Age du consentement | Notes |
| --- | --- | --- |
| CCPA (Californie) | 16 | <ul><li>Le consentement parental ne peut être fourni que pour les sujets de données de 13 ans ou plus.</li><li>La collecte de données à caractère personnel auprès de personnes de moins de 13 ans est strictement interdite.</li></ul> |
| RGPD (Union européenne) | 16 | <ul><li>Certains États membres de l&#39;UE peuvent fournir une loi à un âge inférieur à cette fin, mais pas moins de 13 ans.</li><li>Le consentement parental doit être fourni pour tous les sujets des données dont l’âge est inférieur à la limite d’âge.</li></ul> |
| LGPD (Brésil) | 13 | <ul><li>Le consentement parental doit être fourni pour tous les sujets des données dont l’âge est inférieur à la limite d’âge.</li><li>Le consentement peut être donné par une personne physique âgée de 13 à 18 ans, à condition que le traitement de ses données personnelles soit effectué dans leur meilleur intérêt.</li></ul> |
| PDPA (Thaïlande) | 10 | <ul><li>Le consentement parental doit être fourni pour tous les sujets des données dont l’âge est inférieur à la limite d’âge.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Combien de jours une entreprise a-t-elle pour répondre à la demande d’un client souhaitant consulter ou supprimer des informations personnelles ?

En supposant que l’entreprise ait collecté des informations personnelles et qu’elle puisse authentifier ou vérifier l’identité d’un consommateur particulier, les réglementations de confidentialité permettent de remplir un délai spécifique pour une demande de consommateur. Le tableau suivant ventile les délais applicables pour chaque réglementation, avec des notes sur certaines exceptions :

>[!NOTE]
>
>Le délai de réponse en &quot;jours&quot; est le reflet des délais prescrits par chaque loi pour répondre à une demande des consommateurs.

| Réglementation | Période de réponse | Notes |
| --- | --- | --- |
| CCPA (Californie) | 45 jours | |
| RGPD (Union européenne) | 30 jours | Si la demande est complexe ou si de nombreuses demandes ont été effectuées par le même sujet de données, la demande peut être étendue à 60 jours. |
| LGPD (Brésil) | 15 jours | |
| PDPA (Thaïlande) | 30 jours | Si une société ne peut pas répondre à la demande d’un sujet de données dans le délai de conformité, elle disposera de 30 jours supplémentaires à compter de la date à laquelle elle n’a pas été en mesure de répondre par écrit à la personne concernée. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Mon entreprise doit-elle nommer un délégué à la protection des données ?

Si les opérations de données de votre entreprise relèvent des juridictions légales du RGPD, LGPD ou PDPA, vous devez nommer un délégué à la protection des données (DPO) dans les cas suivants :

* Votre organisation est une autorité publique
* Votre entreprise s’engage dans une surveillance systématique à grande échelle.
* Votre entreprise s’engage dans le traitement à grande échelle de données personnelles sensibles.

>[!IMPORTANT]
>
>Contrairement à d&#39;autres réglementations, la CCPA en fait une obligation. Cependant, il est généralement recommandé que, pour maintenir la conformité en matière de confidentialité, une entreprise dispose d’une activité de collecte de données de surveillance individuelle qualifiée et du stockage des données des consommateurs, ainsi que de répondre aux demandes des clients.

### Comment puis-je prendre en charge les demandes d’accès à des informations personnelles des clients si je conserve des données couvertes par les réglementations de confidentialité ?

Une fois que vous avez pris les mesures nécessaires pour authentifier les clients qui appartiennent aux juridictions appropriées, Adobe Experience Platform Privacy Service vous permet de soumettre des demandes d’accès à des informations personnelles des clients à des applications Experience Cloud compatibles. Pour plus d’informations, consultez la [[!DNL Privacy Service] présentation](../home.md) . Pour plus d’informations sur la manière dont vos applications Experience Cloud spécifiques peuvent répondre aux demandes de confidentialité, reportez-vous au guide sur les [applications Privacy Service et Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>L’autorité de régulation californienne donnera prochainement des indications supplémentaires sur les types de données qui peuvent faire l’objet de demandes d’accès à des informations personnelles.

## Questions relatives au CCPA

Les questions suivantes se rapportent spécifiquement à la CCPA.

### Comment les différents rôles et responsabilités de la CCPA s’appliquent-ils à Experience Cloud ?

Selon la définition de la CCPA, s’appliquent à Adobe et à ses clients les rôles suivants :

* Les clients Adobe (la partie demandant la collecte et l’utilisation d’informations personnelles auprès des résidents de Californie) seraient considérés comme une **Entreprise**.
* Adobe, qui fournit le service, serait considéré comme un **Fournisseur de services**.

En tant que Fournisseur de services, Adobe collecte et traite des informations personnelles pour le compte de l’Entreprise. Il est contractuellement tenu d’utiliser ces informations uniquement aux finalités spécifiques définies dans le contrat.

Compte tenu de cette relation et du langage contractuel de l&#39;Adobe, les divulgations à l&#39;Adobe ne seraient probablement pas considérées comme une &quot;vente&quot; pour laquelle les entreprises auraient besoin de fournir un avis et de demander leur consentement.

Cependant, les services Adobe peuvent être utilisés pour activer certains partages et transferts de données vers des tiers. Ces transferts de tiers pourraient être considérés comme une &quot;vente&quot; et nécessiter légalement la divulgation et le consentement. Les clients doivent se rapprocher de leur service juridique pour examiner des cas d’utilisation spécifiques afin d’évaluer les exigences applicables.

### Adobe propose-t-il d’autres outils pouvant être utiles pour répondre aux exigences de la CCPA ?

Les applications Adobe Experience Cloud fournissent des fonctionnalités de gestion et de gouvernance qui peuvent être utiles pour les besoins de confidentialité des entreprises. Parmi ces outils figurent l’étiquetage de l’utilisation des données, les contrôles d’accès basés sur les rôles, l’obscurcissement de l’adresse IP et les fonctions de hachage.

Adobe a reçu diverses certifications pour ses pratiques en matière de confidentialité et de sécurité, telles qu’une certification ISO 27001 et une validation RGPD de TrustArc.

## Questions relatives au RGPD

Les questions suivantes concernent spécifiquement le RGPD.

### Quelle est la différence entre un règlement et une directive ?

Un **règlement** constitue un acte législatif contraignant qui doit être appliqué dans son intégralité au sein de l’UE. Une **directive** est un acte législatif qui définit un objectif que tous les pays de l’UE doivent atteindre, mais c’est à chacun des pays de décider la manière dont ils souhaitent procéder pour y parvenir.

Il est important de noter que le RGPD est un règlement, contrairement à la législation précédente (la directive sur la protection des données), qui est une directive.

### De quelle manière le RGPD influe-t-il sur les politiques relatives aux violations des données ?

Les règlements proposés au sujet des violations des données concernent principalement les politiques de notification des entreprises qui ont été compromises. Les violations des données susceptibles de présenter un risque pour les individus doivent être notifiées à l’autorité de protection des données dans un délai de 72 heures et aux personnes concernées sans retard excessif.

## Questions relatives à la PDPA

Les questions suivantes concernent spécifiquement le PDPA.

### Qu’est-ce que la notion de données personnelles sensibles ?

Le PDPA prévoit des exigences strictes pour la collecte et le stockage de données personnelles sensibles, notamment les données personnelles concernant : l’origine raciale ou ethnique, les opinions politiques, les croyances religieuses ou philosophiques, les casiers judiciaires, les adhésions syndicales, les données génétiques, les données biométriques, les dossiers de santé et l’orientation ou les préférences sexuelles.
