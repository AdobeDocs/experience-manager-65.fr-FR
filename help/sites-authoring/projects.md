---
title: Projets
seo-title: Projets
description: Les projets vous permettent de regrouper des ressources dans une seule entité dont l’environnement commun et partagé facilite la gestion de vos projets.
seo-description: Les projets vous permettent de regrouper des ressources dans une seule entité dont l’environnement commun et partagé facilite la gestion de vos projets.
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Projets{#projects}

Les projets permettent de regrouper des ressources dans une seule entité. Un environnement commun et partagé permet de gérer facilement vos projets. Dans AEM, les types de ressources que vous pouvez associer à un projet s’appellent des mosaïques. Tiles may include project and team information, assets, workflows, and other types of information, as described in detail in [Project Tiles.](#project-tiles)

>[!CAUTION]
>
>For users in projects to see other users/groups while using Projects functionality like creating projects, creating tasks/workflows, seeing and managing the team, those users need to have read access on **/home/users** and **/home/groups**. The easiest way to implement this is to give the **projects-users** group read access to **/home/users** and**/home/groups**.

En tant qu’utilisateur, vous pouvez effectuer les opérations suivantes :

* Créer des projets
* Associer du contenu et des dossiers de ressources à un projet
* Supprimer des projets
* Supprimer les liens de contenu d’un projet

Reportez-vous aux rubriques supplémentaires suivantes :

* [Gestion de projets
   ](/help/sites-authoring/touch-ui-managing-projects.md)
* [Utilisation de tâches](/help/sites-authoring/task-content.md)
* [Utilisation des workflows de projet](/help/sites-authoring/projects-with-workflows.md)
* [Projet de création et intégration à PIM](/help/sites-authoring/managing-product-information.md)

## Console Projets {#projects-console}

Dans AEM, la console Projets permet d’accéder à vos projets et de les gérer.

![screen-shot_2019-03-05at125110](assets/screen-shot_2019-03-05at125110.png)

* Sélectionnez **Chronologie**, puis un projet pour afficher sa chronologie.
* Cliquez/appuyez sur **Sélectionner** pour passer en mode de sélection.
* Cliquez sur **Créer** pour ajouter des projets.
* L’option **Activer/désactiver les projets actifs** vous permet de basculer entre tous les projets et uniquement ceux qui sont actifs.
* L’option **Afficher la vue Statistiques** permet d’afficher les statistiques de projet relatives à la réalisation de tâches.

## Mosaïques de projet {#project-tiles}

Dans la console Projets, vous devez associer différents types d’informations à vos projets. Elles sont connues sous le nom de **mosaïques**. Toutes les mosaïques, ainsi que le type d’informations qu’elles contiennent, sont décrites dans cette section.

Vous pouvez associer les mosaïques suivantes à votre projet. Chacune d’elles est décrite dans les sections ci-après :

* Ressources et collections de ressources
* Expériences
* Liens
* Informations sur le projet
* Equipe
* Pages d’entrée
* Courriels
* Workflows
* Lancements
* Tâches

### Ressources {#assets}

Dans la mosaïque **Ressources**, vous pouvez regrouper tous les éléments dont vous avez besoin pour un projet particulier.

![chlimage_1-70](assets/chlimage_1-70.png)

Vous chargez des ressources directement dans la mosaïque. En outre, vous pouvez créer des visionneuses d’images, des visionneuses à 360° ou des visionneuses de médias mixtes si vous avez installé le complément Médias dynamiques.

![chlimage_1-71](assets/chlimage_1-71.png)

### Collections de ressources {#asset-collections}

Comme avec les ressources, vous pouvez ajouter des [collections de ressources](/help/assets/managing-collections-touch-ui.md) directement à votre projet. Vous définissez les collections dans AEM Assets.

![chlimage_1-72](assets/chlimage_1-72.png)

Ajoutez une collection en cliquant sur **Ajouter une collection** et en sélectionnant une collection dans la liste.

### Expériences {#experiences}

La mosaïque **Expériences** permet d’ajouter au projet une application mobile, un site web ou une publication.

![chlimage_1-73](assets/chlimage_1-73.png)

Les icônes indiquent le type d’expérience qui est représenté : site web, application mobile ou publication. Ajoutez des expériences en cliquant sur le signe + ou en cliquant sur **Ajouter une expérience** et en sélectionnant le type d’expérience.

![chlimage_1-74](assets/chlimage_1-74.png)

Sélectionnez le chemin des miniatures, et le cas échéant, modifiez la miniature de l’expérience. Les expériences sont regroupées dans la mosaïque **Expériences.**

### Liens {#links}

La mosaïque Liens permet d’associer des liens externes à votre projet.

![chlimage_1-75](assets/chlimage_1-75.png)

Vous pouvez donner au lien un nom facile à reconnaître et changer de miniature.

![chlimage_1-76](assets/chlimage_1-76.png)

### Informations sur le projet {#project-info}

La mosaïque Informations sur le projet fournit des informations générales sur le projet, notamment sa description, son état (actif ou inactif), son échéance et ses membres. En outre, vous pouvez ajouter une miniature de projet qui sera visible dans la page principale Projets.

![chlimage_1-77](assets/chlimage_1-77.png)

Des membres d’équipe peuvent être attribués et supprimés de cette mosaïque (ou leurs rôles peuvent être modifiés) et de la mosaïque Equipe.

![chlimage_1-78](assets/chlimage_1-78.png)

### Tâche de traduction {#translation-job}

La mosaïque Tâche de traduction est l’endroit où vous commencez une traduction et où vous pouvez voir l’état de toutes vos traductions. Pour configurer votre traduction, consultez [Création de projets de traduction](/help/assets/translation-projects.md).

![chlimage_1-79](assets/chlimage_1-79.png)

Click the ellipsis at the bottom of the **Translation Job** card to view the assets in the translation workflow. La liste des tâches de traduction contient également des entrées pour les balises et les métadonnées des ressources. Ces entrées indiquent que les métadonnées et les balises des ressources sont également traduites.

![chlimage_1-80](assets/chlimage_1-80.png)

### Equipe {#team}

Dans cette page, vous pouvez définir les membres de l’équipe de projet. En mode d’édition, vous pouvez saisir le nom des membres d’équipe et attribuer des rôles utilisateur.

![chlimage_1-81](assets/chlimage_1-81.png)

Vous pouvez ajouter et supprimer des membres de l’équipe. De plus, vous pouvez modifier le [rôle utilisateur](#userroles) attribué à chaque membre de l’équipe.

![chlimage_1-82](assets/chlimage_1-82.png)

### Pages d’entrée {#landing-pages}

La mosaïque **Pages d’entrée** vous permet de demander une nouvelle page d’entrée.

![chlimage_1-83](assets/chlimage_1-83.png)

Ce workflow est décrit à la section [Création d’un workflow de page d’entrée](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow).

### Courriels {#emails}

La mosaïque **Courriels** permet de gérer les demandes de courrier électronique. Elle lance le workflow de demande de courrier électronique.

![chlimage_1-84](assets/chlimage_1-84.png)

Pour plus d’informations, se reporter à [Worfklow de demande de courrier électronique.](/help/sites-authoring/projects-with-workflows.md#request-email-workflow) 

### Workflows {#workflows}

Vous pouvez configurer votre projet pour qu’il suive certains workflow. Si des workflows sont actifs, leur état s’affiche dans la mosaïque **Workflows** de la console Projets.

![chlimage_1-85](assets/chlimage_1-85.png)

Vous pouvez configurer votre projet pour qu’il suive certains workflows. Selon le type de projet que vous sélectionnez, différents workflows sont disponibles.

Ils sont décrits à la section [Utilisation des workflows de projet.](/help/sites-authoring/projects-with-workflows.md) 

### Lancements {#launches}

La mosaïque Lancements présente tous les programmes qui ont été demandés avec un workflow [de demande de lancement.](/help/sites-authoring/projects-with-workflows.md) 

![chlimage_1-86](assets/chlimage_1-86.png)

### Tâches {#tasks}

Les tâches vous permettent de surveiller l’état de toutes les activités associées à un projet, y compris des workflows. Tasks are covered in detail at [Working with Tasks](/help/sites-authoring/task-content.md).

![chlimage_1-87](assets/chlimage_1-87.png)

## Modèles de projet {#project-templates}

AEM est livré avec trois modèles différents prêts à l’emploi :

* Un projet simple - Un échantillon de référence pour tout projet qui ne correspond pas à d&#39;autres catégories (un fourre-tout). Il comprend trois rôles de base (propriétaires, éditeurs et observateurs) et quatre workflows (Approbation de projet, Demander un lancement, Demander la page d’entrée et Demander un courrier électronique).
* Un projet média - Un exemple de projet de référence pour les activités liées aux médias. Il comprend plusieurs rôles de projet relatifs aux médias (photographes, éditeurs, rédacteurs, concepteurs, propriétaires et observateurs). Il comprend également deux processus liés au contenu multimédia : Demande de copie (pour demander et examiner du texte) et Photo du produit (pour gérer la photographie liée aux produits).
* [Produit Photo Shoot Project](/help/sites-authoring/managing-product-information.md) - Exemple de référence pour la gestion de la photographie de produit liée au commerce électronique. Il comprend les rôles suivants : photographes, éditeurs, retoucheurs de photos, propriétaires, directeurs créatifs, marketeurs de réseaux sociaux, directeurs marketing, réviseurs et observateurs.
* [Un projet de traduction](/help/sites-administering/translation.md) : modèle de référence pour gérer des activités liées à la traduction. Il prévoit trois rôles de base (propriétaires, éditeurs et observateurs). Il comprend deux workflows accessibles dans l’interface utilisateur Workflows.

En fonction du modèle sélectionné, plusieurs options s’offrent à vous, notamment en termes de rôles utilisateur et de workflows.

## Rôles utilisateur dans un projet {#user-roles-in-a-project}

Différents rôles utilisateur sont définis dans un modèle de projet et utilisés pour deux principales raisons :

1. Permissions. Les rôles utilisateur peuvent faire partie de l’une des trois catégories répertoriées : Observateur, Editeur, Propriétaire. Par exemple, un photographe ou un rédacteur aura les mêmes privilèges qu’un éditeur. Les autorisations déterminent ce que les utilisateurs peuvent faire avec le contenu d’un projet.
1. Workflows. Les workflows déterminent l’utilisateur associé à telles ou telles tâches d’un projet. Les tâches peuvent être associées à un rôle de projet. Par exemple, une tâche peut être attribuée à des photographes, de sorte que tous les membres de l’équipe disposant du rôle Photographe se la voient attribuer.

Pour vous permettre de gérer les autorisations de sécurité et de contrôle, tous les projets prennent en charge les rôles par défaut suivants :

<table>
 <tbody>
  <tr>
   <td><p><strong>Rôle</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
   <td><p><strong>Permissions</strong></p> </td>
   <td><p><strong>Appartenance à un groupe</strong></p> </td>
  </tr>
  <tr>
   <td><p>Observateur</p> </td>
   <td><p>Un utilisateur disposant de ce rôle peut afficher les détails du projet, y compris son état.</p> </td>
   <td><p>Droits en lecture seule sur un projet</p> </td>
   <td><p>groupe workflow-users</p> </td>
  </tr>
  <tr>
   <td><p>Éditeur</p> </td>
   <td><p>Un utilisateur disposant de ce rôle peut télécharger et modifier le contenu d’un projet.</p> <p> </p> </td>
   <td>
    <ul>
     <li>Accès en lecture et écriture sur un projet, les métadonnées correspondantes et les ressources connexes.</li>
     <li>Droits permettant à l’utilisateur de transférer une liste de plans ou une séance photo et de réviser et approuver des ressources</li>
     <li>Droits en écriture sur /etc/commerce</li>
     <li>Droits de modification sur un projet spécifique</li>
    </ul> </td>
   <td><p>groupe workflow-users</p> </td>
  </tr>
  <tr>
   <td><p>Propriétaire</p> </td>
   <td><p>Un utilisateur disposant de ce rôle peut lancer un projet. Le propriétaire peut créer un projet, lancer une tâche pour un projet et déplacer les ressources approuvées vers le dossier Production. Toutes les autres tâches de projet peuvent également être visualisées et implémentées par le propriétaire.</p> </td>
   <td>
    <ul>
     <li>Droits en écriture sur /etc/commerce</li>
    </ul> </td>
   <td>
    <ul>
     <li>Groupe d’utilisateurs DAM (pour pouvoir créer un projet)</li>
     <li>groupe d’administrateurs de projet (pour pouvoir déplacer des ressources)</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Pour des projets créatifs, des rôles supplémentaires, par exemple, de photographe, sont également proposés. Vous pouvez utiliser ces rôles pour créer des rôles personnalisés liés à un projet spécifique.

>[!NOTE]
>
>Lorsque vous créez un projet et ajoutez des utilisateurs pour les différents rôles, des groupes liés au projet sont automatiquement créés pour gérer les autorisations correspondantes. Par exemple, un projet nommé Monprojet serait associé à trois groupes **Propriétaires Monprojet**, **Editeurs Monprojet**, **Observateurs Monprojet**. Cependant, si le projet est supprimé, ces groupes ne le sont pas automatiquement. Un administrateur doit supprimer manuellement les groupes dans **Outils** > **Sécurité** > **Groupes**.
