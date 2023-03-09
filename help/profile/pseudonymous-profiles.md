---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;jeu de données;temps de vie;ttl;temps de vie;pseudonyme;profils pseudonymes;expiration des données;expiration;
solution: Experience Platform
title: Expiration des données de profil pseudonyme
description: Ce document fournit des conseils généraux sur la configuration de l’expiration des données pour les profils pseudonymes dans Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 3f776255ca858a86f501fd587c44fe176c45e103
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---


# Expiration des données de profils pseudonymes [!BADGE Version limitée]

Dans Adobe Experience Platform, un profil est pris en compte pour l’expiration des données pseudonymes s’il répond aux conditions suivantes :

- Les types d’identité du profil assemblé correspondent à ce que le client a spécifié comme type d’identité pseudonyme ou inconnu.
   - Par exemple, si le type d’identité du profil est `ECID`, `GAID`ou `AAID`. Le profil assemblé ne comporte aucun identifiant provenant d’un autre type d’identité. Dans cet exemple, un profil assemblé effectue les opérations suivantes : **not** posséder une identité de courrier électronique ou de gestion de la relation client.
- Aucune activité n’a eu lieu au cours d’une période définie par l’utilisateur. L’activité est définie par les événements d’expérience ingérés ou les mises à jour des attributs de profil initiées par le client.
   - Par exemple, un nouvel événement de page vue ou une nouvelle mise à jour d’attribut de page est considéré comme une activité. Cependant, une mise à jour de l’adhésion au segment non initiée par l’utilisateur est **not** considérée comme une activité. Actuellement, pour calculer l’expiration des données, le suivi au niveau du profil est basé sur le moment de l’ingestion.

## Accéder à {#access}

L’expiration des données de profil pseudonyme ne peut pas être configurée via l’interface utilisateur de Platform ou les API. Pour activer cette fonctionnalité, vous devez plutôt contacter l’assistance technique. Lorsque vous contactez l’assistance, incluez les informations suivantes :

- Les types d&#39;identité à prendre en compte pour les suppressions de profil Pseudonyme.
   - Par exemple : `ECID` uniquement, `AAID` uniquement ou une combinaison de `ECID` et `AAID`.
- Le temps d’attente avant la suppression d’un profil pseudonyme. La recommandation par défaut pour les clients est de 30 jours. Cependant, cette valeur peut varier en fonction de votre cas d’utilisation.
- Nombre de profils actuels par rapport au nombre de profils de licence.

## Questions fréquentes {#faq}

La section suivante répertorie les questions fréquentes sur l’expiration des données de profils pseudonymes :

### Quels utilisateurs doivent utiliser l’expiration des données de profils pseudonymes ?

- Si vous utilisez un connecteur qui envoie directement des données de leur source vers Platform.
- Si vous disposez d’un site web qui diffuse en masse des clients non authentifiés.
- Si vos jeux de données contiennent un nombre de profils excessif et que vous avez confirmé que ce nombre excessif de profils est dû à un type d’identité basé sur des cookies anonymes.
   - Pour le déterminer, vous devez utiliser le rapport de chevauchement des types d’identité. Vous trouverez plus d’informations sur ce rapport sous LIEN

### Quels sont les avertissements que vous devez connaître avant d’utiliser l’expiration des données de profils pseudonymes ?

- L’expiration des données de profil anonymes s’exécutera sur la variable **production** sandbox.
- Une fois cette fonction activée, la suppression des profils est **permanent**. Il y a **non** méthode de restauration des profils supprimés.
- Ceci est **not** une tâche de nettoyage unique. L’expiration des données de profil anonymes s’exécutera en permanence une fois par jour et supprimera les profils qui correspondent aux entrées du client.
- **Tous** les profils définis comme profils pseudonymes seront affectés par l&#39;expiration des données de profil pseudonyme. C’est le cas **not** Peu importe si le profil est un événement d’expérience uniquement ou s’il contient uniquement des attributs de profil.
- Ce nettoyage va **only** se produit dans Profile. Identity Service peut continuer à afficher les identités supprimées dans le graphique après le nettoyage dans les cas où le profil a plusieurs identités pseudonymes associées (telles que `AAID` et `ECID`). Cette divergence sera corrigée dans un avenir proche.

### En quoi l’expiration des données de profil pseudonyme diffère-t-elle de l’expiration des données d’événement d’expérience existantes ?

L’expiration des données de profil anonyme et l’expiration des données d’événement d’expérience sont des fonctionnalités complémentaires.

#### Granularité

L’expiration des données d’événement d’expérience fonctionne sur un **dataset** niveau. Par conséquent, chaque jeu de données peut avoir un paramètre d’expiration de données différent.

L’expiration des données de profil anonyme fonctionne sur un **sandbox** niveau. Par conséquent, l’expiration des données affectera tous les profils de l’environnement de test.

#### Types d’identité

L’expiration des données d’événement d’expérience supprime les événements **only** selon l’horodatage de l’enregistrement d’événement. Les types d’identité inclus sont les suivants : **ignored** à des fins d’expiration.

Expiration des données de profil pseudonyme **only** prend en compte les profils qui comportent des graphiques d’identités qui contiennent des types d’identités sélectionnés par le client, tels que `ECID`, `AAID`ou d’autres types de cookies. Si le profil contient **any** type d’identité supplémentaire qui était **not** dans la liste sélectionnée du client, le profil effectue les opérations suivantes : **not** être supprimées.

#### Éléments supprimés

Expiration des données d’événement d’expérience **only** supprime les événements et supprime **not** supprimez les données de classe de profil. Les données de classe de profil ne sont supprimées que lorsque toutes les données sont supprimées dans **all** jeux de données et il existe **non** enregistrements de classe de profil restants pour le profil.

Suppression de l’expiration des données de profil anonyme **both** enregistrements d’événement et de profil. Par conséquent, les données de classe de profil seront également supprimées.

### Comment l’expiration des données de profil pseudonyme peut-elle être utilisée conjointement avec l’expiration des données d’événement d’expérience ?

L’expiration des données de profil anonymes et l’expiration des données d’événement d’expérience peuvent être utilisées pour se compléter.

Vous devriez **always** configurez l’expiration des données d’événement d’expérience dans vos jeux de données en fonction de vos besoins de conservation des données concernant vos clients connus. Une fois que l’expiration des données d’événement d’expérience est configurée, vous pouvez utiliser l’expiration des données de profil pseudonyme pour supprimer automatiquement les profils pseudonymes. En règle générale, le délai d’expiration des données pour les profils pseudonymes est inférieur au délai d’expiration des données pour les événements d’expérience.

Dans un cas d’utilisation standard, vous pouvez définir l’expiration de vos données d’événement d’expérience en fonction des valeurs de vos données utilisateur connues et vous pouvez définir l’expiration de vos données de profil anonyme sur une durée beaucoup plus courte afin de limiter l’impact des profils anonymes sur la conformité de votre licence Platform.
