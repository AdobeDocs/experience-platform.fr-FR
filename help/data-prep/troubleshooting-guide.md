---
keywords: Experience Platform;accueil;rubriques populaires;
title: Guide de dépannage de la préparation des données
description: Ce document fournit des réponses aux questions fréquentes sur la préparation des données Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 29%

---

# Guide de dépannage de [!DNL Data Prep]

Ce document fournit des réponses aux questions fréquentes sur la [!DNL Data Prep] Adobe Experience Platform ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou pour obtenir des informations de dépannage concernant les API de Platform en général, reportez-vous au [guide de dépannage des API d’Adobe Experience Platform](../landing/troubleshooting.md).

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

### Mon ingestion a échoué en raison de la validation d’un attribut, mais cet attribut est correctement renseigné dans mon fichier. Qu&#39;est-ce qui ne va pas, exactement ?

Assurez-vous que le type de données de chaque champ correspond au type défini dans le schéma. En outre, des contraintes telles que &quot;Obligatoire&quot;, &quot;Énumération&quot; et &quot;format&quot; doivent être respectées.

Les données en cours d’ingestion doivent être conformes au schéma du modèle de données d’expérience (XDM) défini dans Experience Platform. Si l’attribut ne correspond pas au type ou au format attendu spécifié dans le schéma, l’ingestion échoue.

Si les fonctions de préparation de données sont utilisées, assurez-vous que la transformation génère les attributs appropriés. Vous pouvez passer en revue les attributs pendant le processus de configuration du processus des sources. Au cours de l’étape de mappage, sélectionnez **[!UICONTROL Nouveau type de champ]**, puis sélectionnez **[!UICONTROL Ajouter un champ calculé]**. Utilisez ensuite l&#39;interface des champs calculés pour prévisualiser chaque fonction.

### Comment supprimer les valeurs de données incorrectes des enregistrements de diffusion en continu ou d’ingestion par lots ?

Vous pouvez utiliser l’interface de mappage de la préparation de données pour effectuer un filtrage au niveau de la colonne en n’associant que les colonnes qui possèdent les données requises. Vous pouvez également utiliser des champs calculés pour transformer les données à l’aide des fonctions de prise en charge.

Le filtrage au niveau des lignes est actuellement disponible uniquement pour le [connecteur source Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Après l’ingestion, vous pouvez utiliser le Distiller de données pour nettoyer, former et manipuler les données à l’aide de SQL. Toutefois, ce processus nécessite la suppression du lot contenant les enregistrements erronés et la réingestion d’un nouveau lot créé à partir du résultat du SQL.

>[!IMPORTANT]
>
>* Lac de données : vous pouvez uniquement supprimer les enregistrements qui ont déjà été ingérés en supprimant et en réingérant le lot dans lequel se trouve l’enregistrement.
>
>* Real-Time Customer Profile : vous pouvez remplacer des enregistrements basés sur des attributs en ingérant de nouveaux enregistrements, mais les enregistrements d’événement d’expérience ne peuvent pas être supprimés.
>
>* Identity Service : vous ne pouvez pas supprimer les enregistrements directement dans Identity Service. Vous devrez supprimer l’intégralité du profil et le charger à nouveau avec les enregistrements corrects à l’aide de l’API de suppression de profil.

### Quelles sont les bonnes pratiques pour utiliser des champs calculés dans les données de GIF ?

Vous pouvez utiliser les fonctions de mappage de la préparation de données lors de l’étape de mappage des données sources sur le schéma XDM pour créer un nouveau champ calculé.

### Lorsque vous importez des données Adobe Analytics en tant que source, le schéma créé automatiquement est-il activé pour profile ?

Les données Analytics ne sont pas automatiquement configurées pour Profile. Après avoir configuré le connecteur source, vous devez accéder au jeu de données et au schéma et les activer pour l’ingestion par Profile.

Lorsque vous créez un flux de données source Analytics dans un environnement de test de production, deux flux de données sont créés :

* Flux de données qui effectue un renvoi de 13 mois des données de suite de rapports historiques dans le lac de données. Ce flux de données se termine une fois le renvoi terminé.
* Flux de données qui envoie des données actives au lac de données et à Profile. Ce flux de données s’exécute en continu.

### Comment puis-je mettre en minuscules une valeur dans un objet map à l’aide des fonctions de préparation de données ?

Vous pouvez récupérer la valeur à l’aide de la fonction `map_get_values`, puis la mettre en minuscules à l’aide de la fonction lower :

```shell
lower(map_get_values(mapObject, 'keyName'))
```

Vous pouvez utiliser la même fonction pour mettre en minuscules un objet map. Cependant, vous ne pouvez pas parcourir une carte entière en boucle et faire en sorte que chaque élément soit en minuscules.

### Puis-je utiliser les fonctions de préparation de données de manière imbriquée ?

Oui, vous pouvez utiliser une fonction de préparation des données au sein d’une autre fonction pour résoudre les problèmes liés aux fonctionnalités complexes de préparation des données lors de l’ingestion des données.

Par exemple, si vous souhaitez définir un champ comme nul en fonction d’une condition spécifique, vous pouvez utiliser la fonction &quot;iif&quot; pour vérifier ce champ. Si la fonction renvoie `true`, vous pouvez utiliser &quot;nullify()&quot;, et si elle renvoie `false`, vous pouvez utiliser le champ correspondant.

Si marketing_type était le champ , vous pouvez utiliser &quot;.equals&quot; pour vérifier la valeur du champ marketing_type et l’imbriquer dans une fonction &quot;iif&quot;. Si elle renvoie `true`, vous pouvez utiliser la fonction &quot;nullify()&quot; comme illustré ci-dessous :

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Vous trouverez ci-dessous des exemples d’imbrication de fonctions de préparation de données à l’aide de if, equals et null :

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| --- | --- | --- | --- | --- | --- |
| iif | Évalue une expression booléenne donnée et renvoie la valeur spécifiée en fonction du résultat. | <ul><li>EXPRESSION : **Obligatoire** Expression booléenne en cours d’évaluation.</li><li>TRUE_VALUE : **Required** La valeur renvoyée si l’expression renvoie true (vrai).</li><li>FALSE_VALUE : **Required** La valeur renvoyée si l’expression est évaluée comme false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| est égal à | Compare deux chaînes pour confirmer si elles sont égales. Cette fonction respecte la casse. | <ul><li>STRING1 : **Obligatoire** Première chaîne à comparer.</li><li>STRING2 : **Obligatoire** La deuxième chaîne que vous souhaitez comparer. | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;est égal à &#x200B;(&quot;STRING1&quot;) | false |
| nullify | Définit la valeur de l’attribut sur null. Vous devez l’utiliser lorsque vous ne souhaitez pas copier le champ dans le schéma cible. | | nullify() | nullify() | null |

{style="table-layout:auto"}

Vous trouverez ci-dessous un exemple d’imbrication des fonctions, en supposant que le champ évalué est &quot;marketing_type&quot;.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Ensuite, étant donné que vous disposez des trois champs suivants :

* marketing_type : (email, phyMail, push, sms, phone)
* total_consents : plage de nombres de 4 000 à 5 500
* date : de février à mars 2024

Vous pouvez utiliser et imbriquer les trois fonctions répertoriées ci-dessus pour manipuler les trois champs :

* iif(marketing_type.equals(&quot;email&quot;), null(), iif(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;), null(), iif(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type))
* iif(total_consents > 5000, iif(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;insuffisance-consentement&quot;)
* iif(date.equals(&quot;3/21/24&quot;), iif(marketing_type.equals(&quot;push&quot;), null(), marketing_type), &quot;not-March&quot;)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-consent-sms&quot;, marketing_type), &quot;high-consentement&quot;)
* iif(marketing_type.equals(&quot;email&quot;), iif(total_consent > 5000, nullify(), &quot;email-low-consentement&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_consent &lt; 4500, &quot;low-consent-push&quot;, nullify()), marketing_type)
* iif(total_consent >= 5500, iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;high-consentement&quot;), marketing_type)