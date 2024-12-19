---
keywords: Experience Platform;accueil;rubriques populaires;RGPD;RGPD;CCPA;CCPA;PDPA;pdpa;LGPD;lgpd;faq;FAQ;réglementation;réglementations;Règlements;Confidentialité;Confidentialité;
solution: Experience Platform
title: FAQ sur les réglementations de confidentialité
description: Ce document répond aux questions fréquentes sur les réglementations légales prises en charge en matière de confidentialité et leur mise en œuvre dans Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: d643b2aeadd4080fa89d6a7b0f84a9f6882d7b89
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 32%

---

# FAQ sur les réglementations de confidentialité

Ce document répond aux questions fréquentes sur les réglementations légales prises en charge en matière de confidentialité et leur mise en œuvre dans Adobe Experience Cloud.

>[!NOTE]
>
>Les définitions des différents termes utilisés dans ce document se trouvent dans le guide [terminologie de la réglementation en matière de confidentialité](terminology.md).

## Questions générales

Les questions suivantes se rapportent à toutes les réglementations de confidentialité prises en charge par l’Experience Cloud.

### Sur qui les réglementations de confidentialité prises en charge s’appliquent-elles ?

Les [règlements sur la protection des renseignements personnels pris en charge par l&#39;Experience Cloud ](./overview.md) s&#39;appliquent à toutes les organisations qui stockent et traitent les données personnelles des citoyens dans les juridictions respectives des règlements, quel que soit l&#39;emplacement géographique de l&#39;organisation.

### Que signifie la notion de données personnelles ?

Les données personnelles constituent toute information relative à une personne physique ou à un titulaire de données qui peut être utilisée pour identifier directement ou indirectement la personne. Il peut s’agir d’un nom, d’une photo, d’une adresse e-mail, de détails bancaires, de publications sur les réseaux sociaux, d’informations médicales ou de l’adresse IP d’un ordinateur.

Les identifiants suivants sont couramment utilisés dans les applications Experience Cloud et peuvent être soumis aux exigences de la réglementation en matière de confidentialité :

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

Bien que les réglementations relatives à la confidentialité couvrent un large éventail d&#39;informations personnelles, les termes du contrat standard d&#39;Adobe stipulent que les informations personnelles sensibles (telles que le numéro de sécurité sociale, les informations figurant sur le permis de conduire, les informations de compte financier et les données biométriques) sont généralement interdites d&#39;importation et d&#39;utilisation dans les applications Experience Cloud.

### Quelle est la différence entre le contrôleur des données et le responsable du traitement des données ?

Le **contrôleur des données** est l’entité qui détermine les finalités, conditions et moyens du traitement des données personnelles, tandis que l’**entité de traitement des données** est une entité qui traite les données personnelles pour le compte du contrôleur des données.

Un **contrôleur de données** est la personne ou l&#39;organisation qui a le pouvoir et la responsabilité de prendre des décisions concernant la collecte, l&#39;utilisation ou la divulgation de données personnelles. Un **sous-traitant** est la personne ou l&#39;organisation qui opère en relation avec la collecte, l&#39;utilisation ou la divulgation des données personnelles et la direction du contrôleur de données.

### Quelle est la différence entre le consentement explicite et le consentement univoque du titulaire de données ?

**Consentement explicite** fait référence à une norme de consentement qui implique une indication spécifique, éclairée et sans ambiguïté des souhaits de la personne concernée, sous forme orale ou écrite. En d&#39;autres termes, la personne concernée doit littéralement et explicitement dire « Je consens » ou « J&#39;accepte » pour que le consentement soit considéré comme explicite. En outre, il doit être aussi facile de retirer le consentement que de le donner.

Le **consentement non ambigu (implicite)** fait référence à un consentement qui n’a pas été donné explicitement par la personne concernée, mais qui est néanmoins sans ambiguïté par nature. Par exemple, lors du processus d’inscription à un site web d’entreprise, une notification est envoyée indiquant qu’en fournissant une adresse e-mail, la personne concernée consent à recevoir des e-mails sur des offres spéciales. Si la personne concernée lit la notification, l&#39;action positive de la saisie de son e-mail suffit à être considérée comme un consentement sans ambiguïté.

Pour de nombreuses réglementations telles que le RGPD, le consentement explicite est requis pour le traitement des données personnelles sensibles, où rien de moins que l’« opt-in » suffit. Toutefois, pour les données non sensibles, un consentement sans ambiguïté (implicite) est acceptable.

### Les personnes concernées ayant moins d’un certain âge peuvent-elles donner leur consentement ?

De nombreuses réglementations relatives à la confidentialité stipulent que si une personne concernée a moins d&#39;un certain âge, elle ne peut pas légalement consentir à la collecte de ses données personnelles. Certains règlements autorisent le titulaire de la responsabilité parentale à donner son consentement pour cette personne concernée dans ces cas, mais pas tous. Le tableau suivant répertorie l’âge minimum auquel les titulaires de données doivent donner leur propre consentement pour chaque règlement, avec des notes pour plus d’informations :

| Réglementation | Âge du consentement | Notes |
| --- | --- | --- |
| CCPA (Californie) | 16 | <ul><li>Le consentement parental ne peut être fourni que pour les personnes concernées âgées de 13 ans ou plus.</li><li>La collecte de données personnelles auprès de personnes de moins de 13 ans est strictement interdite.</li></ul> |
| RGPD (Union européenne) | 16 | <ul><li>Certains États membres de l&#39;UE peuvent prévoir une loi pour un âge inférieur à cette fin, mais pas inférieur à 13 ans.</li><li>Le consentement des parents doit être fourni pour toutes les personnes concernées n’ayant pas atteint l’âge limite.</li></ul> |
| LGPD (Brésil) | 13 | <ul><li>Le consentement des parents doit être fourni pour toutes les personnes concernées n’ayant pas atteint l’âge limite.</li><li>Le consentement peut être donné par une personne physique âgée de 13 à 18 ans, pour autant que le traitement de ses données personnelles soit effectué dans son intérêt.</li></ul> |
| PDPA (Thaïlande) | 10 | <ul><li>Le consentement des parents doit être fourni pour toutes les personnes concernées n’ayant pas atteint l’âge limite.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Combien de jours une entreprise a-t-elle pour répondre à la demande d’un client souhaitant consulter ou supprimer des informations personnelles ?

En supposant que l&#39;entreprise ait recueilli des renseignements personnels et qu&#39;elle puisse authentifier ou vérifier l&#39;identité d&#39;un consommateur en particulier, les règlements sur la protection des renseignements personnels prévoient un délai précis pour qu&#39;une demande d&#39;un consommateur soit satisfaite. Le tableau suivant détaille les fenêtres temporelles applicables pour chaque règlement, avec des notes sur certaines exceptions :

>[!NOTE]
>
>Le délai de réponse en « jours » reflète les délais prescrits par chaque loi réglementaire pour répondre à une demande des consommateurs.

| Réglementation | Délai de réponse | Notes |
| --- | --- | --- |
| CCPA (Californie) | 45 jours | |
| RGPD (Union européenne) | 30 jours | |
| LGPD (Brésil) | 15 jours | |
| PDPA (Thaïlande) | 30 jours | Si une entreprise ne peut pas répondre à la demande d’un titulaire de données dans le délai imparti, elle dispose de 30 jours supplémentaires à compter de la date à laquelle elle n’a pas pu répondre à la demande pour répondre par écrit au titulaire de données. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Mon entreprise doit-elle nommer un délégué à la protection des données ?

Si les opérations de données de votre organisation relèvent de la compétence légale du RGPD, du LGPD ou de la PDPA, vous devez nommer un délégué à la protection des données (DPD) dans les cas suivants :

* Votre organisation est une autorité publique
* Votre organisation s’engage dans une surveillance systématique à grande échelle
* Votre entreprise s’engage dans le traitement à grande échelle de données personnelles sensibles.

>[!IMPORTANT]
>
>Contrairement à d&#39;autres règlements, le CCPA stipule que c&#39;est une exigence. Cependant, il est généralement recommandé que, pour respecter la confidentialité, une entreprise doive disposer d’une personne qualifiée pour collecter les données de surveillance et les stocker, ainsi que pour répondre aux demandes des clients.

### Comment puis-je prendre en charge les demandes d’accès à des informations personnelles des consommateurs si je conserve des données couvertes par les réglementations de confidentialité ?

Une fois que vous avez pris les mesures nécessaires pour authentifier les consommateurs et consommatrices qui relèvent des juridictions légales appropriées, Adobe Experience Platform Privacy Service vous permet d’envoyer les demandes d’accès à des informations personnelles de consommateurs et consommatrices vers des applications Experience Cloud compatibles. Voir la [[!DNL Privacy Service] présentation](../home.md) pour plus d’informations. Pour plus d’informations sur la manière dont vos applications Experience Cloud spécifiques peuvent répondre aux demandes de confidentialité, reportez-vous au guide sur les [applications Privacy Service et Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>L’organisme de réglementation californien doit encore fournir d’autres orientations sur les types de données éligibles aux demandes de confidentialité des consommateurs.

## Questions du CCPA

Les questions suivantes concernent spécifiquement le CCPA.

### Comment les différents rôles et responsabilités de la CCPA s’appliquent-ils à Experience Cloud ?

Selon la définition de la CCPA, s’appliquent à Adobe et à ses clients les rôles suivants :

* Les clients Adobe (la partie demandant la collecte et l’utilisation d’informations personnelles auprès des résidents de Californie) seraient considérés comme une **Entreprise**.
* Adobe, qui fournit le service, serait considéré comme un **Fournisseur de services**.

En tant que Fournisseur de services, Adobe collecte et traite des informations personnelles pour le compte de l’Entreprise. Il est contractuellement tenu d’utiliser ces informations uniquement aux finalités spécifiques définies dans le contrat.

Compte tenu de cette relation et du libellé du contrat d&#39;Adobe, les divulgations à l&#39;Adobe ne seraient probablement pas considérées comme une « vente » pour laquelle les entreprises devraient fournir un avis et demander le consentement.

Cependant, les services Adobe peuvent être utilisés pour activer certains partages et transferts de données vers des tiers. Ces transferts à des tiers pourraient être considérés comme une « vente » et exigent légalement la divulgation et le consentement. Les clients doivent se rapprocher de leur service juridique pour examiner des cas d’utilisation spécifiques afin d’évaluer les exigences applicables.

### Adobe propose-t-il d’autres outils pouvant être utiles pour répondre aux exigences de la CCPA ?

Les applications Adobe Experience Cloud fournissent des fonctionnalités de gestion et de gouvernance qui peuvent être utiles pour les besoins de confidentialité des entreprises. Parmi ces outils figurent l’étiquetage de l’utilisation des données, les contrôles d’accès basés sur les rôles, l’obscurcissement de l’adresse IP et les fonctions de hachage.

Adobe a reçu diverses certifications pour ses pratiques en matière de confidentialité et de sécurité, telles qu’une certification ISO 27001 et une validation RGPD de TrustArc.

## Questions relatives au RGPD

Les questions suivantes se rapportent spécifiquement au RGPD.

### Quelle est la différence entre un règlement et une directive ?

Un **règlement** constitue un acte législatif contraignant qui doit être appliqué dans son intégralité au sein de l’UE. Une **directive** est un acte législatif qui définit un objectif que tous les pays de l’UE doivent atteindre, mais c’est à chacun des pays de décider la manière dont ils souhaitent procéder pour y parvenir.

Il est important de noter que le RGPD est un règlement, contrairement à la législation précédente (la directive sur la protection des données), qui est une directive.

### De quelle manière le RGPD influe-t-il sur les politiques relatives aux violations des données ?

Les règlements proposés au sujet des violations des données concernent principalement les politiques de notification des entreprises qui ont été compromises. Les violations des données susceptibles de présenter un risque pour les individus doivent être notifiées à l’autorité de protection des données dans un délai de 72 heures et aux personnes concernées sans retard excessif.

## Questions PDPA

Les questions suivantes portent spécifiquement sur le PDPA.

### Qu’est-ce qu’une donnée personnelle sensible ?

La PDPA prévoit des exigences strictes pour la collecte et le stockage de données personnelles sensibles qui comprennent des données personnelles relatives à : l&#39;origine raciale ou ethnique, les opinions politiques, les croyances religieuses ou philosophiques, les casiers judiciaires, les appartenances syndicales, les données génétiques, les données biométriques, les dossiers de santé et l&#39;orientation ou les préférences sexuelles.
