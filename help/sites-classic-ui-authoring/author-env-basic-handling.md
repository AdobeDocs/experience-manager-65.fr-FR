---
title: Gestion de base
description: Présentation de la gestion de base lors de l’utilisation de l’environnement de création Adobe Experience Manager. Il s’appuie sur la console Sites.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 48%

---

# Manipulation de base{#basic-handling}

>[!NOTE]
>
>* Cette page est conçue pour donner un aperçu des opérations de gestion de base lors de l’utilisation de l’environnement de création Adobe Experience Manager (AEM). Il s’appuie sur la console **Sites**.
>
>* Certaines fonctionnalités ne sont pas disponibles dans toutes les consoles et d’autres sont disponibles dans certaines consoles. Des informations spécifiques sur les consoles individuelles et leurs fonctionnalités associées sont traitées plus en détail sur d’autres pages.
>* Des raccourcis clavier sont disponibles dans toute l’application AEM, notamment lors de l’[utilisation des consoles](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) et de la [modification de pages](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>

## L’écran de bienvenue {#the-welcome-screen}

L’IU classique propose une sélection de consoles, qui utilisent des mécanismes connus pour parcourir et initier des actions, notamment cliquer, double-cliquer et [menus contextuels](#context-menus).

Après la connexion, l’écran de bienvenue s’affiche. Il fournit une liste de liens vers les consoles et services :

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## Consoles {#consoles}

Les principales consoles sont les suivantes :

<table>
 <tbody>
  <tr>
   <td><strong>Console</strong></td>
   <td><strong>Objectif</strong></td>
  </tr>
  <tr>
   <td><strong>Bienvenue</strong></td>
   <td>Fournit un aperçu et un accès direct (au moyen de liens) vers les principales fonctions d’AEM.</td>
  </tr>
  <tr>
   <td><strong>Ressources numériques</strong><br /> </td>
   <td>Ces consoles vous permettent d’importer et de <a href="/help/sites-classic-ui-authoring/classicui-assets.md">gestion des ressources numériques</a> tels que des images, des vidéos, des documents et des fichiers audio. Ces ressources peuvent ensuite être utilisées par n’importe quel site web s’exécutant sur la même instance AEM. </td>
  </tr>
  <tr>
   <td><strong>Lancements</strong></td>
   <td>Avec cette console, vous pouvez gérer vos <a href="/help/sites-classic-ui-authoring/classic-launches.md">lancements</a> et élaborer ainsi le contenu pour une prochaine version d’une ou de plusieurs pages Web activées.<br /> <i>Remarque : dans l’IU activée pour les écrans tactiles, la plupart des fonctionnalités sont également disponibles dans la console Sites, avec le rail Références.</i> <i>Si nécessaire, cette console est disponible à partir de la console Outils ; sélectionnez Opérations, puis Lancements.</i></td>
  </tr>
  <tr>
   <td><strong>Boîte de réception </strong></td>
   <td>Souvent, différentes personnes sont impliquées dans les sous-tâches d’un workflow et chaque personne doit accomplir son étape avant de remettre le travail à la personne suivante. La boîte de réception vous permet d’afficher les notifications liées à ces tâches. Reportez-vous à la section <a href="/help/sites-administering/workflows.md">Utilisation des processus</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Balisage</strong></td>
   <td>Les consoles Balisage vous permettent d’administrer des balises. Les balises sont des noms courts ou des expressions que vous pouvez utiliser pour classer et annoter des éléments de contenu afin de faciliter leur recherche et leur organisation. Pour plus d’informations, voir <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Utilisation et gestion des balises</a>.</td>
  </tr>
  <tr>
   <td><strong>Outils</strong></td>
   <td>La variable <a href="/help/sites-administering/tools-consoles.md">Consoles Outils</a> vous donner accès à plusieurs outils et consoles spécialisés pour la gestion des sites web, des ressources numériques et d’autres aspects du référentiel de contenu.</td>
  </tr>
  <tr>
   <td><strong>Utilisateurs</strong></td>
   <td>Ces consoles vous permettent de gérer les droits d’accès des utilisateurs et des groupes. Pour plus d’informations, voir <a href="/help/sites-administering/security.md">Administration et sécurité des utilisateurs</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Sites Web</strong></td>
   <td>Les consoles Sites/Sites web vous permettent de <a href="/help/sites-classic-ui-authoring/classic-page-author.md">créer, afficher et gérer des sites web ;</a> s’exécutant sur votre instance AEM. Grâce à ces consoles, vous pouvez créer, copier, déplacer et supprimer des pages de site web, démarrer des workflows et activer (publier) des pages. Vous pouvez également ouvrir une page pour la modifier.<br /> </td>
  </tr>
  <tr>
   <td><strong>Workflows</strong></td>
   <td>Un processus est une série d’étapes définies décrivant la procédure à suivre pour accomplir certaines tâches. Souvent, plusieurs personnes sont impliquées dans une tâche et chaque personne doit accomplir son étape avant de remettre le travail à la personne suivante. La console Workflow vous permet d’élaborer des modèles de workflows et de gérer l’exécution des instances de workflow. Reportez-vous à la section <a href="/help/sites-administering/workflows.md">Utilisation des workflows</a>.<br /> </td>
  </tr>
 </tbody>
</table>

La console **Sites web** propose deux volets grâce auxquels vous pouvez parcourir et gérer vos pages :

* Volet de gauche

  Présente l’arborescence de vos sites Web et les pages dans ces sites Web.

  Il affiche également des informations sur d’autres aspects ou AEM, y compris les projets, les plans directeurs et les ressources.

* Volet de droite

  Les pages s’affichent alors (à l’emplacement sélectionné dans le volet de gauche) et peuvent être utilisées pour agir.

À partir de là, vous pouvez [gérer vos pages](/help/sites-authoring/managing-pages.md) à l’aide de la barre d’outils ou d’un menu contextuel, ou encore en ouvrant une page afin de réaliser d’autres actions.

>[!NOTE]
>
>Dans toutes les consoles, la gestion de base est la même. Cette section traite de la console **Sites web**, car il s’agit de la principale console utilisée lors de la création.

![chlimage_1-9](assets/chlimage_1-9a.png)

## Accès à l’Aide {#accessing-help}

Sur diverses consoles (par exemple, Sites web), une **Aide** est disponible. Cliquer **Aide** ouvre Package Share ou le site de documentation.

![chlimage_1-10](assets/chlimage_1-10a.png)

Lors de la modification d’une page, la variable [sidekick comporte également un bouton d’accès à l’aide](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Naviguer dans la console Sites web {#navigating-with-the-websites-console}

La variable **Sites web** La console répertorie vos pages de contenu dans une arborescence (volet de gauche). Pour faciliter la navigation, les sections de l’arborescence peuvent être développées (+) ou réduites (-), selon les besoins :

* Cliquez sur le nom de la page dans le volet de gauche pour effectuer les opérations suivantes :

   * Répertorie les pages enfants dans le volet de droite
   * Développe la structure dans le volet de gauche.

     Pour des raisons de performances, cette action dépend du nombre de noeuds enfants. Avec une installation standard, cette méthode d’extension fonctionne lorsqu’il existe `30` ou moins de noeuds enfants.

* Double-cliquez sur le nom de la page (volet de gauche) pour développer l’arborescence, mais comme la page est ouverte en même temps, cet effet n’est pas si évident.

>[!NOTE]
>
>Cette valeur par défaut ( `30`) peut être modifié par console dans les configurations spécifiques à l’application du widget siteadmin :
>
>Sur le nœud siteadmin :
>
>définissez la valeur de la propriété :
>`treeAutoExpandMax`
>Sur :
>`/apps/wcm/core/content/siteadmin`
>
>ou globalement dans le thème :
>définissez la valeur de :
>`TREE_AUTOEXPAND_MAX`
>dans :
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>Voir [SiteAdmin dans l’API Widget CQ](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin) pour plus d’informations.

## Informations sur la page dans la console Sites web {#page-information-on-the-websites-console}

Le volet de droite de la console **Sites web** fournit une vue de liste avec des informations sur les pages :

![page-info](assets/page-info.png)

Les informations suivantes sont disponibles ; un sous-ensemble de ces champs s’affiche par défaut :

<table>
 <tbody>
  <tr>
   <td><strong>Colonne</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Miniature</td>
   <td>Affiche une miniature de la page.</td>
  </tr>
  <tr>
   <td>Titre</td>
   <td>Le titre qui s’affiche sur la page.</td>
  </tr>
  <tr>
   <td>Nom</td>
   <td>Le nom qu’AEM attribue à la page.</td>
  </tr>
  <tr>
   <td>Publié</td>
   <td>Indique si la page a été publiée et donne la date et l’heure de publication.</td>
  </tr>
  <tr>
   <td>Modifié</td>
   <td>Indique si la page a été modifiée et donne la date et l’heure de modification. Pour enregistrer toute modification, vous devez activer la page.</td>
  </tr>
  <tr>
   <td>Publication Scene7</td>
   <td>Indique si la page a été publiée sur Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Statut</td>
   <td>Indique l’état de la page, par exemple si la page fait partie d’un workflow ou d’une Live Copy, ou si une page est verrouillée.</td>
  </tr>
  <tr>
   <td>Impressions</td>
   <td>Affiche l’activité sur une page en nombre d’accès.</td>
  </tr>
  <tr>
   <td>Modèle</td>
   <td>Indique le modèle sur lequel repose une page.</td>
  </tr>
  <tr>
   <td>Dans le processus</td>
   <td>Indique le moment où la page se trouve dans un workflow.</td>
  </tr>
  <tr>
   <td>Verrouillé par</td>
   <td>Indique lorsqu’une page a été verrouillée et le compte utilisateur qui l’a verrouillée.</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>Indique si la page fait partie d’une Live Copy.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Pour sélectionner les colonnes visibles, placez le pointeur de la souris sur le titre d’une colonne. Un menu déroulant s’affiche et vous pouvez utiliser la variable **Colonnes** .

Les couleurs en regard des pages dans les colonnes **Publié** et **Modifié** indiquent le statut de la publication :

| **Colonne** | **Couleur** | **Description** |
|---|---|---|
| Publié | Vert | Publication réussie. Le contenu est publié. |
| Publié | Jaune | Publication en attente. Le système n’a pas encore reçu la confirmation de la publication. |
| Publié | Rouge | Échec de la publication. Il n’existe aucune connexion avec l’instance de publication. Cela peut également signifier que le contenu a été désactivé. |
| Publié | *blank* | La page n’a jamais été publiée. |
| Modifié | Bleu | La page a été modifiée depuis la dernière publication. |
| Modifié | *blank* | Cette page n’a jamais été modifiée ou n’a pas été modifiée depuis la dernière publication. |

## Menus contextuels {#context-menus}

L’IU classique applique des mécanismes courants pour la navigation et le déclenchement des opérations, notamment clic et double-clic. En fonction de la situation actuelle, divers menus contextuels (ouverts avec le bouton droit de la souris) sont également disponibles :

![chlimage_1-11](assets/chlimage_1-11a.png)
