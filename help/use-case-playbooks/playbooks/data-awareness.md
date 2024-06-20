---
solution: Experience Platform
title: Présentation de la prise en compte des données dans les classeurs de cas d’utilisation
description: Découvrez comment accélérer le temps de valorisation en copiant les ressources générées dans l’environnement de test d’inspiration finale vers d’autres environnements de test.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Ressources générées par le lecteur Publish dans d’autres environnements de test {#publish-to-other-sandboxes}

Les scénarios d’utilisation sont des modèles marketing conçus pour générer des ressources telles que des audiences, des schémas ou des parcours pour des cas d’utilisation marketing courants. Vous pouvez tester les ressources créées par des livres de jeu dans l’environnement de test inspirant. Lorsque vous êtes prêt, vous pouvez importer les ressources dans d’autres environnements de test de développement pour effectuer d’autres tests avec les données disponibles dans ces environnements de test. Lorsque vous êtes satisfait des tests, vous pouvez ensuite déplacer les ressources des environnements de test de développement vers les environnements de test de production.

Cependant, dans certains cas, vous avez peut-être déjà configuré vos propres schémas, champs et groupes de champs dans d’autres environnements de test de développement. Cela peut rendre certaines des ressources générées par les modèles de cas d’utilisation, comme les parcours, incompatibles avec vos données. Pour comprendre comment utiliser la fonctionnalité de sensibilisation aux données pour mieux aligner et compléter les ressources générées avec vos ressources existantes, lisez ce tutoriel.

## Conditions préalables {#prerequisites}

Avant de lire ce tutoriel, parcourez les [modèles de manuel d’utilisation disponibles](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) et [création d’une instance](/help/use-case-playbooks/playbooks/create-share-reuse.md) d’un playbook préféré.

La création d’une instance génère un ensemble de ressources telles que des parcours, des segments, des schémas et des messages dans l’environnement de test d’inspiration. Lisez la suite pour découvrir comment copier ces ressources dans d’autres environnements de test.

### Création et publication d’un module {#create-publish-package}

>[!NOTE]
>
> Vous ne pouvez importer des packages que dans d’autres environnements de développement. Une fois que vous avez apporté toutes les modifications ou mises à jour nécessaires, vous pouvez importer en production les ressources ou les modules de ces environnements de test de développement. Vous ne pouvez pas importer directement depuis les environnements de test des cahiers de travail du cas d’utilisation en production.

1. Pour importer des objets de l’environnement de test d’inspiration dans un autre environnement de test, accédez à l’instance souhaitée d’un manuel de cas d’utilisation, puis sélectionnez **[!UICONTROL Publish sur un autre environnement de test]** pour exporter les artefacts sous la forme d’un package.

   ![GIF montrant les différentes instances de cas d’utilisation](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Une fois que vous avez sélectionné le **[!UICONTROL Publish sur un autre environnement de test]** , un modal s’affiche. Renseignez le nom et la description facultative, puis sélectionnez **[!UICONTROL Créer]**. Cette étape regroupe les ressources générées dans un package qui peut être importé dans un autre environnement de test.

   ![Un modal pour créer un package](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Accédez au **Environnements de test** dans le volet de navigation de gauche, puis sélectionnez l’option **Packages** , recherchez votre package et publiez-le. Pour publier un module dont l’état est en version préliminaire, procédez comme suit : [outil sandbox](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) document.

   ![Module dans un état de brouillon ou non publié](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Publier le package](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Une fois la publication terminée, un message s’affiche sur la page de navigation des modules. **+** activée en regard du nom.

   ![Onglet Modules dans la page Sandbox](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Le package ne peut pas être importé tant qu’il est toujours en mode préliminaire. Ouvrez donc la page des détails du package et publiez le package.

5. Sélectionnez la variable **+** contrôler et démarrer le workflow pour importer les ressources générées par le manuel du cas d’utilisation dans la **[!UICONTROL Environnement de test Target]**. Sélectionnez un environnement de test cible et confirmez le nom du module à importer à l’aide de la liste déroulante. Ajoutez les détails de la tâche, tels que le nom et la description de la tâche, avant de passer à l’étape suivante.

   ![Lancez le workflow d&#39;import, sélectionnez target, confirmez le package, ajoutez les détails de la tâche.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. Dans le **[!UICONTROL Afficher les dépendances]** vous pouvez mapper des schémas et copier d’autres ressources à partir de l’environnement de test d’inspiration dans l’environnement de test cible. La variable **[!UICONTROL Terminer]** est désactivé tant que vous n’avez pas mappé chaque schéma.

   ![Mappez les schémas à l’étape &quot;Afficher les dépendances&quot;, en activant le bouton Terminer .](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Mappage des schémas {#map-schemas}

1. Mappez le premier schéma. La boîte de dialogue de mappage de schéma affiche une liste déroulante pour sélectionner le schéma cible. Si le schéma source est un schéma de profil, il n’existe aucune autre option de schéma cible en dehors de la variable [schéma de profil d’union individuel](/help/xdm/classes/individual-profile.md). Vous pouvez voir les recommandations de mappage générées automatiquement entre les données source et les champs cibles lors du premier affichage de la page. Vous pouvez éditer les mappages en sélectionnant le champ cible, puis en sélectionnant un nouveau champ. Si vous modifiez les mappages proposés, utilisez la méthode **Valider** pour valider les nouveaux mappages et afficher les erreurs pouvant être liées aux nouveaux mappages. Sélectionner **Enregistrer** une fois le mappage terminé.

   ![Boîte de dialogue de mappage de schéma avec une liste déroulante pour sélectionner un schéma cible.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Poursuivez le mappage de tous les champs des schémas. Si le schéma est un [schéma d&#39;événement](/help/xdm/classes/experienceevent.md), la boîte de dialogue affiche une liste déroulante dans laquelle vous pouvez afficher tous les schémas d’événement dans l’environnement de test cible.

   ![Sélectionner un schéma cible dans la liste déroulante](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Sélectionnez un schéma parmi les schémas disponibles dans la **Environnement de test Target**.

   ![Sélection d’un schéma](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Effectuez le mappage et sélectionnez **Enregistrer**.

   ![Enregistrement du mapping](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Une fois que vous avez effectué le mappage de tous les champs des schémas, sélectionnez **Terminer** pour terminer le workflow d&#39;import.

   ![Terminer le flux](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Vous ne pouvez modifier aucune ressource, à l’exception des schémas, car il s’agit d’un environnement de test inspirant, mais ils s’affichent car il s’agit de dépendances du module.

### Statut de l’importation {#import-status}

1. Vous êtes automatiquement redirigé vers le [**Imports**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) où vous pouvez voir la progression de votre importation.

   ![Page affichant la progression de l&#39;import](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Pendant l’importation du package, les actifs du package sont créés dans l’environnement de test cible. Une fois l’importation terminée, ils font référence aux champs que vous avez mappés pendant le processus d’importation. Le processus est maintenant terminé et les ressources de l’environnement de test inspirant sont désormais également présentes dans votre environnement de test cible pour que vous puissiez le tester.

   ![Ressources générées dans l’environnement de test cible](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment utiliser les classeurs de cas d’utilisation avec [outil sandbox](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) pour créer des parcours exécutables qui référencent vos schémas. En savoir plus sur les [Cas d’utilisation Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
