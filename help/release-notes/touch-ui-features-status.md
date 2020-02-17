---
title: État des fonctionnalités de l’IU tactile
description: Notes de mise à jour spécifiques à l’interface utilisateur tactile d’Adobe Experience Manager.
uuid: ceb081cc-7c33-4408-8032-3ac83d461268
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: f736581d-e6ea-4ec8-bfc7-16b9aa592097
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# État des fonctionnalités de l’IU tactile{#touch-ui-feature-status}

>[!CAUTION]
>
>[L’interface utilisateur classique est obsolète](../release-notes/deprecated-removed-features.md) depuis AEM 6.4. Adobe n’envisage pas d’apporter d’autres améliorations à l’interface utilisateur classique et les utilisateurs sont encouragés à tirer parti des nouvelles fonctionnalités puissantes disponibles dans l’interface utilisateur tactile.

Depuis la version 6.0, AEM est doté d’une nouvelle interface appelée IU optimisée pour les écrans tactiles (ou IU tactile) qui est cohérente avec Adobe Marketing Cloud et les instructions générales concernant les interfaces utilisateur Adobe. Avec la mise en œuvre quasi totale de la parité des fonctionnalités, cette interface est devenue l’interface utilisateur standard d’AEM. L’ancienne interface orientée bureau est dénommée « IU classique ».

Bien que la plupart des fonctionnalités soient déjà présentes dans l’interface utilisateur optimisée pour les écrans tactiles, il en reste certaines à intégrer, qui le seront dans les prochaines mises à jour.

La liste suivante présente l’état actuel des fonctionnalités mises en oeuvre dans AEM 6.5.

For recommendations for customers that upgrade to AEM 6.5, please see [User Interface Recommendations for Customers](/help/sites-deploying/ui-recommendations.md) for details.

>[!NOTE]
>
>Veuillez noter que cette page porte uniquement sur la parité des fonctionnalités avec l’IU classique.
>
>Les fonctionnalités qui ont été ajoutées à l’IU optimisée pour les écrans tactiles et qui sont absentes de l’IU classique ne sont pas répertoriées.

>[!NOTE]
>
>Cette liste est la plus complète possible, mais ne doit pas être considérée comme exhaustive.

## Légende {#legend}

* **Complète :** la fonctionnalité est entièrement disponible dans l’IU optimisée pour les écrans tactiles.
* **Surtout**: La fonctionnalité est principalement disponible dans l’interface utilisateur tactile.
* **Absente :** la fonctionnalité n’est pas disponible dans l’IU optimisée pour les écrans tactiles. L’IU classique doit être utilisée pour exécuter cette action.
* **Remplacée :** la fonctionnalité a été remplacée par une nouvelle implémentation qui fonctionne différemment.
* **Supprimée :** la fonctionnalité n’existe plus dans l’IU optimisée pour les écrans tactiles et elle ne sera pas remplacée.

## État des fonctionnalités : Administration de sites {#feature-status-sites-admin}

This is a list of capabilities the classic UI Site Admin ( `/siteadmin`) has and the status in the touch-enabled UI ( `/sites.html`).

<table>
 <tbody>
  <tr>
   <td><strong>Fonctionnalité<br /> </strong></td>
   <td><strong>État<br /> </strong></td>
   <td><strong>Commentaire</strong></td>
  </tr>
  <tr>
   <td>Navigation dans l’arborescence du site</td>
   <td>Complète<br /> </td>
   <td>AEM 6.4 a introduit une arborescence <a href="/help/sites-authoring/basic-handling.md#content-tree">de</a>contenu.</td>
  </tr>
  <tr>
   <td>Démarrer le processus</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Créer une page</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Créer un site</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Créer un lancement</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Créer une Live Copy <br /> </td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Créer un dossier</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Afficher l’état de publication</td>
   <td>Terminer</td>
   <td>Depuis AEM 6.5, l’état du flux de travail s’affiche en mode Liste.</td>
  </tr>
  <tr>
   <td>Rechercher</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Copier/coller une page (duplication)</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Déplacer une page</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publier une page</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publier une page sans droits de réplication</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publier ultérieurement</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publier l’arborescence</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Annuler la publication de page(s)</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Annuler la publication de page(s) sans droits de réplication</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Annuler la publication ultérieurement</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Supprimer</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Verrouiller/déverrouiller</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Afficher/modifier les propriétés</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Définir les autorisations sur les pages</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Historique des versions</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Restaurer la version</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Restaurer l’arborescence et les pages supprimées</td>
   <td>Absente</td>
   <td>Utiliser l’IU classique.</td>
  </tr>
  <tr>
   <td>Afficher la différence entre l’ancienne et la nouvelle version<br /> </td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Actions Live Copy (déploiement)</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Afficher les copies de langue</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Rechercher et remplacer</td>
   <td>Absente<br /> </td>
   <td>Utiliser l’IU classique.</td>
  </tr>
  <tr>
   <td>Boîte de réception des notifications (événements JCR)</td>
   <td>Absente</td>
   <td>Utiliser l’IU classique. Sera remplacée par une autre implémentation.</td>
  </tr>
  <tr>
   <td>Références</td>
   <td>Terminer</td>
   <td>Affichage des liens de page entrants ajoutés à AEM 6.5.<br /> </td>
  </tr>
 </tbody>
</table>

## État des fonctionnalités : éditeur de page {#feature-status-page-editor}

This is a list of capabilities the classic UI Page Editor ( `/cf#`) has and the status in the touch-enabled ( `/editor.html`).

<table>
 <tbody>
  <tr>
   <td><strong>Fonctionnalité</strong></td>
   <td><strong>État</strong></td>
   <td><strong>Commentaire</strong></td>
  </tr>
  <tr>
   <td>Modifier les pages web</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier les pages web mobiles<br /> </td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier le contenu importé via Design Importer <br /> </td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier les courriers électroniques</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier des applications mobiles hybrides</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier les formulaires</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier les offres</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier les modèles de processus<br /> </td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>ode : Modifier et prévisualiser</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Responsive Preview<br /> </td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Mode : Modifier la conception</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Mode : Scaffolding</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Mode : État des Live Copy<br /> </td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Ajouter des annotations</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Modifier les propriétés<br /> </td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Déployer la page</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Démarrer et afficher les processus</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Présentation des packages de processus</td>
   <td>Principalement</td>
   <td>Complètement accessible dans l’interface utilisateur tactile. Plusieurs charges utiles de flux de travail sont toujours présentées dans l’interface utilisateur classique.<br /> </td>
  </tr>
  <tr>
   <td>Verrouiller/déverrouiller la page</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publier la page <br /> </td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Annuler la publication de la page</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Copier la page</td>
   <td>Supprimé<br /> </td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page">copier les pages</a>.<br /> </td>
  </tr>
  <tr>
   <td>Déplacer la page</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page">déplacer les pages</a>.<br /> </td>
  </tr>
  <tr>
   <td>Supprimer la page</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-authoring/managing-pages.md#deleting-a-page">supprimer les pages</a>.<br /> </td>
  </tr>
  <tr>
   <td>Afficher les références</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-authoring/author-environment-tools.md#references">voir la liste de référence détaillée</a>.<br /> </td>
  </tr>
  <tr>
   <td>Journal d’audit</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites et <a href="/help/sites-authoring/author-environment-tools.md#events-timeline">ouvrez le rail d’activité</a>.<br /> </td>
  </tr>
  <tr>
   <td>Créer la version</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-authoring/working-with-page-versions.md#creating-a-new-version">créer de nouvelles versions</a>.<br /> </td>
  </tr>
  <tr>
   <td>Restaurer la version</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version">restaurer des versions </a>.</td>
  </tr>
  <tr>
   <td>Passer d’un lancement à un autre</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-authoring/launches-promoting.md">basculer entre les lancements</a>.<br /> </td>
  </tr>
  <tr>
   <td>Traduire la page</td>
   <td>Supprimé</td>
   <td>Utilisez Administration de sites pour <a href="/help/sites-administering/tc-manage.md">ajouter une page aux projets de traduction</a>.<br /> </td>
  </tr>
  <tr>
   <td>Timewarp (choisissez la date/l’heure et parcourez le site tel qu’il était avant) <br /> </td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Définir les autorisations</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>IU contextuelle du client <br /> </td>
   <td>Remplacé</td>
   <td>Utilisez dorénavant l’IU <a href="/help/sites-authoring/ch-previewing.md">ContextHub</a>.</td>
  </tr>
  <tr>
   <td>Outil de recherche de contenu pour les différents types de médias<br /> </td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Liste des composants</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Copier et coller des composants <br /> </td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Liste des composants du presse-papiers</td>
   <td>Absente</td>
   <td> </td>
  </tr>
  <tr>
   <td>Annuler/rétablir</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Glisser du contenu dans un espace réservé aux composants</td>
   <td>Complète</td>
   <td> </td>
  </tr>
  <tr>
   <td>Avec la création automatique de composants, faites glisser le contenu directement dans l’espace réservé parsys<br /> </td>
   <td>Complète</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## État des fonctionnalités : éditeurs de texte, d’image et de tableau {#feature-status-text-table-and-image-editors}

Il s’agit d’une liste des fonctionnalités de l’interface utilisateur classique, à savoir l’éditeur de texte, de tableau et d’image, ainsi que l’état de l’interface utilisateur tactile.

<table>
 <tbody>
  <tr>
   <td><strong>Fonctionnalité</strong></td>
   <td><strong>État </strong></td>
   <td><strong>Commentaire<br /> </strong></td>
  </tr>
  <tr>
   <td>Éditeur de texte enrichi</td>
   <td>Terminer</td>
   <td>Utile en place, dans la boîte de dialogue et en plein écran.</td>
  </tr>
  <tr>
   <td>Activation/désactivation des plug-ins RTE</td>
   <td>Complète<br /> </td>
   <td>Vous pouvez utiliser l’éditeur <a href="/help/sites-authoring/templates.md">de</a>modèles.</td>
  </tr>
  <tr>
   <td>Utiliser RTE pour le texte brut</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Liens et ancre</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Carte des caractères</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Copier/coller</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Coller à partir de Microsoft Word<br /> </td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Chercher et Remplacer</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Formats de texte (gras, ...)</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Sous-et exposant</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Justifier</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Listes (puces / nombres)</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Format de paragraphe</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Styles de texte</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Editeur de source (Modifier HTML)<br /> </td>
   <td>Complète<br /> </td>
   <td>Disponible uniquement dans la boîte de dialogue et en plein écran.<br /> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Vérificateur orthographique</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Tableau (éditeur de tableau intégré)</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Annuler/Rétablir<br /> </td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe RTE : Autoriser les images intégrées</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Editeur de tableau</td>
   <td>Terminer</td>
   <td>Utile en place, dans la boîte de dialogue et en plein écran.<br /> </td>
  </tr>
  <tr>
   <td>Faire glisser et déposer l’image dans la cellule du tableau<br /> </td>
   <td>Terminer</td>
   <td>En ligne utilisable</td>
  </tr>
  <tr>
   <td>Éditeur d’image<br /> </td>
   <td>Terminer</td>
   <td>Utile en place, dans la boîte de dialogue et en plein écran.<br /> </td>
  </tr>
  <tr>
   <td>Activation/désactivation des modules externes IPE</td>
   <td>Terminer</td>
   <td>AEM 6.3 a introduit une interface utilisateur dans l’éditeur <a href="/help/sites-authoring/templates.md">de</a>modèles.</td>
  </tr>
  <tr>
   <td>Module externe IPE : Recadrer</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe IPE : Retourner</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe IPE : Annuler/Rétablir</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe IPE : Zone cliquable</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe IPE : Rotation</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Module externe IPE : Zoom</td>
   <td>Complète<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## État des fonctionnalités : outils {#feature-status-tools}

La liste ci-dessous répertorie divers outils proposés dans l’IU classique et indique leur état dans l’IU optimisée pour les écrans tactiles.

<table>
 <tbody>
  <tr>
   <td><strong>Fonctionnalité<br /> </strong></td>
   <td><strong>État<br /> </strong></td>
   <td><strong>Commentaire</strong></td>
  </tr>
  <tr>
   <td>Gestion des tâches</td>
   <td>Remplacé</td>
   <td>6.0 Présentation <a href="/help/sites-authoring/projects.md">des projets et des tâches</a>.<br /> </td>
  </tr>
  <tr>
   <td>Boîte de réception du processus<br /> </td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Configuration du modèle de flux de travail vers la page (<code>/etc/workflow/wcm/templates.html</code>)</td>
   <td>Absente<br /> </td>
   <td>Utiliser l’IU classique.</td>
  </tr>
  <tr>
   <td>Interface utilisateur d’administration du balisage<br /> </td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Centre de contrôle MSM/Blueprint</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Interface utilisateur de Blueprint Manager</td>
   <td>Terminer</td>
   <td> </td>
  </tr>
  <tr>
   <td>Interface utilisateur de configuration de déploiement</td>
   <td>Absente</td>
   <td>Utiliser l’IU classique.</td>
  </tr>
  <tr>
   <td>Utilisateur, groupes et autorisations<br /> </td>
   <td>Principalement terminé<br /> </td>
   <td>Pour modifier des autorisations avancées, utilisez l’interface utilisateur classique.<br /> </td>
  </tr>
  <tr>
   <td>Versions de purge (<code>/etc/versioning/purge.html</code>)</td>
   <td>Absente</td>
   <td>Utiliser l’IU classique.</td>
  </tr>
  <tr>
   <td>Vérificateur de lien externe (<code>/etc/linkchecker.html</code>)</td>
   <td>Absente</td>
   <td>Utiliser l’IU classique.<br /> </td>
  </tr>
  <tr>
   <td>Editeur en bloc (<code>/etc/importers/bulkeditor.html</code>)</td>
   <td>Absente<br /> </td>
   <td>Utiliser l’IU classique.</td>
  </tr>
  <tr>
   <td>Télécharger des miniatures pour les ajouter ou les remplacer<br /> </td>
   <td>Absente</td>
   <td>Utiliser l’IU classique.</td>
  </tr>
 </tbody>
</table>

