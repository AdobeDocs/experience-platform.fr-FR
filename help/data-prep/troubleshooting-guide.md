---
keywords: Experience Platform;accueil;rubriques populaires;
title: Guide de dépannage de la préparation des données
description: Ce document fournit des réponses aux questions fréquentes sur la préparation des données Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 28%

---

# Guide de dépannage de [!DNL Data Prep]

Ce document fournit des réponses aux questions fréquentes sur la [!DNL Data Prep] Adobe Experience Platform ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou pour obtenir des informations de dépannage concernant les API d’Experience Platform en général, consultez le [guide de dépannage des API de Adobe Experience Platform](../landing/troubleshooting.md).

## FAQ

Vous trouverez ci-dessous une liste des questions fréquentes sur [!DNL Data Prep] et leurs réponses.

### Comment les erreurs de transformation sont-elles résolues ?

[!DNL Data Prep] localise toutes les erreurs de transformation dans la colonne dans laquelle elles se sont produites. Par conséquent, cette colonne devient nulle et le reste de la ligne continue à être traité. Ces problèmes de transformation sont consignés comme **Avertissements**. Il est recommandé de consulter régulièrement les avertissements et d’ajuster la logique de transformation pour tenir compte des problèmes de transformation. Cela augmentera la qualité des données ingérées dans Experience Platform.

Si les colonnes marquées comme **Obligatoires** deviennent nulles en raison de problèmes de transformation, la ligne ne sera pas ingérée. Lorsque l’ingestion de données partielle est activée, vous pouvez définir le seuil de ces rejets avant que le flux entier échoue. Si l’attribut devenu nul n’a eu aucune incidence sur les validations au niveau du schéma, la ligne continuera à être ingérée.

Toutes les lignes non valides, même sans erreur de transformation, seront également rejetées. Par exemple, un flux d’ingestion de données peut avoir un mappage passthrough (sans logique de transformation) vers un champ obligatoire et il n’y a pas de valeur entrante pour cet attribut. Cette ligne sera rejetée.

### Comment échapper des caractères spéciaux dans un champ ?

Vous pouvez échapper les caractères spéciaux d’un champ à l’aide de `${...}`. Toutefois, les fichiers JSON qui contiennent des champs avec un point (`.`) ne sont pas pris en charge par ce mécanisme. Lors de l’interaction avec des hiérarchies, si un attribut enfant comporte un point (`.`), vous devez utiliser une barre oblique inverse (`\`) pour échapper les caractères spéciaux. Par exemple, `address` est un objet qui contient l’attribut `street.name`. Il peut donc être appelé `address.street\.name` au lieu de `address.street.name`.

### Quelle est la longueur maximale des champs calculés ?

La longueur maximale des champs calculés est de 4 096 caractères.

### Mon ingestion a échoué en raison de la validation d’un attribut, mais cet attribut figure correctement dans mon fichier . Qu&#39;est-ce qui ne va pas ?

Assurez-vous que le type de données de chaque champ correspond au type défini dans le schéma. En outre, des contraintes telles que « Obligatoire », « enum » et « format » doivent être respectées.

Les données ingérées doivent être conformes au schéma du modèle de données d’expérience (XDM) défini dans Experience Platform. Si l’attribut ne correspond pas au type ou au format attendu spécifié dans le schéma, l’ingestion échoue.

Si les fonctions de préparation de données sont utilisées, assurez-vous que la transformation génère les attributs appropriés. Vous pouvez vérifier les attributs pendant le processus de configuration du workflow des sources. Lors de l’étape de mappage, sélectionnez **[!UICONTROL Nouveau type de champ]** puis **[!UICONTROL Ajouter un champ calculé]**. Ensuite, utilisez l’interface des champs calculés pour prévisualiser chaque fonction.

### Comment puis-je supprimer les valeurs de données incorrectes des enregistrements d’ingestion par lots ou en flux continu ?

Vous pouvez utiliser l’interface de mappage de la préparation des données pour effectuer un filtrage au niveau des colonnes en mappant uniquement les colonnes contenant les données requises. Vous pouvez également utiliser des champs calculés pour transformer les données à l’aide des fonctions de prise en charge.

Le filtrage au niveau des lignes est actuellement disponible uniquement pour le [connecteur source Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Après l’ingestion, vous pouvez utiliser Data Distiller pour nettoyer, mettre en forme et manipuler les données à l’aide de SQL. Cependant, ce processus nécessite la suppression du lot contenant les enregistrements incorrects et la réingestion d’un nouveau lot créé à partir du résultat du SQL.

>[!IMPORTANT]
>
>* Lac de données : vous ne pouvez supprimer des enregistrements déjà ingérés qu’en supprimant et en réingérant le lot dans lequel se trouve l’enregistrement.
>
>* Real-Time Customer Profile : vous pouvez remplacer les enregistrements basés sur les attributs en ingérant de nouveaux enregistrements, mais les enregistrements d’événement d’expérience ne peuvent pas être supprimés.
>
>* Service d’identités : vous ne pouvez pas supprimer des enregistrements directement dans le Service d’identités. Vous devrez supprimer l’ensemble du profil et charger à nouveau le profil avec les enregistrements corrects à l’aide de l’API de suppression de profil.

### Quelle est la bonne pratique pour utiliser les champs calculés dans les données GIF ?

Vous pouvez utiliser les fonctions de mappage de la préparation des données lors de l’étape de mappage des données sources au schéma XDM pour créer un champ calculé.

### Lorsque vous importez des données Adobe Analytics en tant que source, le schéma créé est-il automatiquement activé pour le profil ?

Les données Analytics ne sont pas automatiquement configurées pour le profil. Après avoir configuré le connecteur source, vous devez accéder au jeu de données et au schéma et les activer pour l’ingestion de profils.

Lorsque vous créez un flux de données source Analytics dans un sandbox de production, deux flux de données sont créés :

* Flux de données qui renvoie pendant 13 mois les données historiques de la suite de rapports dans le lac de données. Ce flux de données se termine lorsque le renvoi est terminé.
* Flux de données qui envoie des données actives au lac de données et au profil. Ce flux de données s’exécute en continu.

### Comment mettre en minuscules une valeur dans un objet map à l’aide de fonctions de préparation de données ?

Vous pouvez récupérer la valeur à l’aide de la fonction `map_get_values`, puis la mettre en minuscules à l’aide de la fonction inférieure :

```shell
lower(map_get_values(mapObject, 'keyName'))
```

Vous pouvez utiliser la même fonction pour mettre en minuscules un objet map. Cependant, vous ne pouvez pas lire en boucle une carte entière et mettre chaque élément en minuscules.

### Puis-je utiliser des fonctions de préparation de données de manière imbriquée ?

Oui, vous pouvez utiliser une fonction Préparation de données dans une autre fonction pour résoudre les problèmes liés aux fonctionnalités complexes de préparation des données lors de l’ingestion des données.

Par exemple, si vous souhaitez définir un champ comme nul en fonction d’une condition spécifique, vous pouvez utiliser la fonction « if » pour vérifier ce champ. Si la fonction renvoie `true`, vous pouvez utiliser « nullify() », et si elle renvoie `false`, vous pouvez utiliser le champ correspondant.

Si type_marketing était le champ, vous pouvez utiliser « .equals » pour vérifier la valeur dans le champ type_marketing, qui peut être imbriqué dans une fonction « if ». S’il renvoie `true`, vous pouvez utiliser la fonction « nullify() » comme illustré ci-dessous :

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Vous trouverez ci-dessous des exemples d’imbrication de fonctions de préparation de données à l’aide de si, d’égal à et de nullify :

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| --- | --- | --- | --- | --- | --- |
| iif | Évalue une expression booléenne donnée et renvoie la valeur spécifiée en fonction du résultat. | <ul><li>EXPRESSION : **obligatoire** expression booléenne en cours d’évaluation.</li><li>TRUE_VALUE : **obligatoire** valeur renvoyée si l’expression est évaluée comme vraie.</li><li>FALSE_VALUE : **obligatoire** valeur renvoyée si l’expression est évaluée comme égale à false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| est égal à | Compare deux chaînes pour vérifier si elles sont égales. Cette fonction respecte la casse. | <ul><li>STRING1 : **Obligatoire** première chaîne à comparer.</li><li>STRING2 : **Obligatoire** deuxième chaîne à comparer. | STRING1. &#x200B;égal à(&#x200B;STRING2) | « string1 ». &#x200B;equals&#x200B;(« STRING1 ») | False |
| annuler | Définit la valeur de l’attribut sur null. Utilisez-le lorsque vous ne souhaitez pas copier le champ dans le schéma cible. | | nullify() | nullify() | null |

{style="table-layout:auto"}

Voici un exemple de la manière dont les fonctions peuvent être imbriquées, en supposant que le champ évalué soit « marketing_type ».

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Ensuite, étant donné que vous disposez des trois champs suivants :

* marketing_type : (e-mail, phyMail, notification push, sms, téléphone)
* total_consentements : plage de nombres comprise entre 4 000 et 5 500
* date : de février à mars 2024

Vous pouvez utiliser et imbriquer les trois fonctions répertoriées ci-dessus pour manipuler les trois champs :

* iif(marketing_type.equals(« email »), nullify(), iif(marketing_type.equals(« push »), « push-notification », marketing_type))
* iif(marketing_type.equals(« phyMail »), nullify(), iif(marketing_type.equals(« sms »), « text-message », marketing_type))
* iif(total_consents > 5000, iif(marketing_type.equals(« phone »), nullify(), marketing_type), « insuffisamment-consentements »)
* iif(date.equals(« 3/21/24 »), iif(marketing_type.equals(« push »), nullify(), marketing_type), « not-March »)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(« sms »), « low-consent-sms », marketing_type), « high-consents »)
* iif(marketing_type.equals(« email »), iif(total_consents > 5000, nullify(), « email-low-consents »), marketing_type)
* iif(marketing_type.equals(« push »), iif(total_consents &lt; 4500, « low-consent-push », nullify()), marketing_type)
* iif(total_consents >= 5500, iif(marketing_type.equals(« phyMail »), nullify(), « high-consents »), marketing_type)