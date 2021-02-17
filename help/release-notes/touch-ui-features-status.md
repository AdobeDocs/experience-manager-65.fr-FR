---
title: État des fonctionnalités de l’IU tactile
description: Notes de mise à jour spécifiques à  [!DNL Adobe Experience Manager] IU tactile.
translation-type: tm+mt
source-git-commit: d938f52766154b68df2f6db2c8c49a0ad97e7e6d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 49%

---


# État des fonctionnalités de l’IU tactile {#touch-ui-feature-status}

AEM version 6.4 ou ultérieure [L’interface utilisateur classique est obsolète](../release-notes/deprecated-removed-features.md). L’Adobe n’apporte pas d’autres améliorations à l’interface utilisateur classique et les utilisateurs sont invités à tirer parti des nouvelles fonctionnalités puissantes disponibles dans l’interface utilisateur tactile.

À partir de la version 6.0, AEM a introduit une nouvelle interface utilisateur appelée &quot;interface utilisateur tactile&quot; (simplement appelée &quot;interface utilisateur tactile&quot;) qui est alignée sur [!DNL Adobe Experience Cloud] et sur les directives générales relatives à l’interface utilisateur de l’Adobe. Avec la quasi parité des fonctionnalités atteinte, cette interface est devenue l’interface standard en AEM avec l’interface héritée et orientée sur les ordinateurs de bureau, appelée &quot;interface utilisateur classique&quot;.

Bien que la plupart des fonctionnalités soient déjà présentes dans l’interface utilisateur optimisée pour les écrans tactiles, il en reste certaines à intégrer, qui le seront dans les prochaines mises à jour.

La liste suivante présente l&#39;état actuel des capacités mises en oeuvre dans l&#39;AEM 6.5.

Pour obtenir des recommandations pour les clients qui effectuent la mise à niveau vers AEM 6.5, voir [Recommandations relatives à l’interface utilisateur pour les clients](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Cette page traite uniquement de la parité des fonctionnalités avec l’interface utilisateur classique. Les fonctionnalités ajoutées à l’interface utilisateur tactile et uniques qui ne sont pas présentes dans l’interface utilisateur classique ne sont pas répertoriées.

>[!NOTE]
>
>Cette liste s&#39;efforce d&#39;être complète, mais n&#39;est pas exhaustive.

## Légende {#legend}

* **Terminé** : Cette fonction est entièrement disponible dans l’interface utilisateur tactile.
* **Principalement** : Cette fonction est principalement disponible dans l’interface utilisateur tactile.
* **Absente :** la fonctionnalité n’est pas disponible dans l’IU optimisée pour les écrans tactiles. L’IU classique doit être utilisée pour exécuter cette action.
* **Remplacée :** la fonctionnalité a été remplacée par une nouvelle implémentation qui fonctionne différemment.
* **Supprimée :** la fonctionnalité n’existe plus dans l’IU optimisée pour les écrans tactiles et elle ne sera pas remplacée.

## État des fonctionnalités : Administration de sites {#feature-status-sites-admin}

Il s’agit d’une liste de fonctionnalités dont dispose l’administrateur classique du site de l’interface utilisateur (`/siteadmin`) et de l’état dans l’interface utilisateur tactile (`/sites.html`).

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Navigation dans l’arborescence du site | Terminer | AEM 6.4 a introduit une vue d&#39;arborescence de contenu [](/help/sites-authoring/basic-handling.md#content-tree). |
| Démarrer le processus | Terminer |  |
| Créer une page | Complète |  |
| Créer un site | Complète |  |
| Créer un lancement | Complète |  |
| Créer une Live Copy | Terminer |  |
| Créer un dossier | Complète |  |
| Afficher l’état de publication | Terminer | À partir de AEM 6.5, l’état du flux de travail s’affiche dans la vue de liste. |
| Rechercher | Terminer |  |
| Copier et coller la page (Duplicata) | Terminer |  |
| Déplacer une page | Complète |  |
| Publier une page | Complète |  |
| Publier une page sans droits de réplication | Complète |  |
| Publier ultérieurement | Complète |  |
| Publier l’arborescence | Complète |  |
| Annuler la publication de page(s) | Complète |  |
| Annuler la publication de page(s) sans droits de réplication | Complète |  |
| Annuler la publication ultérieurement | Terminer |  |
| Supprimer | Complète |  |
| Verrouiller/déverrouiller | Complète |  |
| Afficher/modifier les propriétés | Complète |  |
| Définir les autorisations sur les pages | Complète |  |
| Historique des versions | Complète |  |
| Restaurer la version | Terminer |  |
| Restaurer l’arborescence et les pages supprimées | Absente | Utiliser l’IU classique. |
| Afficher la différence entre l’ancienne et la nouvelle version | Terminer |  |
| Actions Live Copy (déploiement) | Complète |  |
| Afficher les copies de langue | Complète |  |
| Rechercher et remplacer | Absente | Utiliser l’IU classique. |
| Boîte de réception de notification (événements JCR) | Absente | Utiliser l’IU classique. Sera remplacée par une autre implémentation. |
| Références | Terminer | Affichage des liens de page entrants ajoutés à AEM 6.5. |

## État des fonctionnalités : éditeur de page {#feature-status-page-editor}

Il s’agit d’une liste de fonctionnalités que possède l’éditeur de page classique de l’interface utilisateur (`/cf#`) et de l’état dans l’application tactile (`/editor.html`).

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Modifier les pages web | Complète |  |
| Modifier les pages web mobiles | Terminer |  |
| Modifier le contenu importé via Design Importer  | Terminer |  |
| Modifier les courriers électroniques | Complète |  |
| Modification d’applications mobiles hybrides | Terminer |  |
| Modifier les formulaires | Terminer |  |
| Modifier les offres | Terminer |  |
| Modifier les modèles de processus | Terminer |  |
| Mode : Modifier et Prévisualisation | Terminer |  |
| Prévisualisation réactive | Terminer |  |
| Mode : Modifier la conception | Complète |  |
| Mode : Scaffolding | Complète |  |
| Mode : État des Live Copy | Terminer |  |
| Ajouter des annotations | Complète |  |
| Modification des propriétés | Terminer |  |
| Page de lancement | Terminer |  |
| Flux de travaux de début et d&#39;affichage | Terminer |  |
| Gestion des packages de processus | Principalement | Entièrement accessible dans l’interface utilisateur tactile. Plusieurs charges utiles de flux de travail sont toujours présentées dans l’interface utilisateur classique. |
| Verrouiller/déverrouiller la page | Complète |  |
| Publier la page | Terminer |  |
| Annuler la publication de la page | Complète |  |
| Copie de la page | Supprimé | Utilisez Administration de sites pour [copier les pages](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Déplacer la page | Supprimé | Utilisez Administration de sites pour [déplacer les pages](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Supprimer la page | Supprimé | Utilisez Administration de sites pour [supprimer les pages](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Afficher les références | Supprimé | Utilisez l’administrateur du site pour afficher la [liste de référence détaillée](/help/sites-authoring/author-environment-tools.md#references). |
| Journal d’audit | Supprimé | Utilisez Administration de sites et [ouvrez le rail d’activité](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Créer la version | Supprimé | Utilisez Administration de sites pour [créer de nouvelles versions](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurer la version | Supprimé | Utilisez Administration de sites pour [restaurer des versions ](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Passer d’un lancement à un autre | Supprimé | Utilisez Administration de sites pour [basculer entre les lancements](/help/sites-authoring/launches-promoting.md). |
| Traduire la page | Supprimé | Utilisez Administration de sites pour [ajouter une page aux projets de traduction](/help/sites-administering/tc-manage.md). |
| Timewarp (choisissez la date/l’heure et parcourez le site tel qu’il était avant)  | Terminer |  |
| Définir les autorisations | Complète |  |
| IU contextuelle du client  | Remplacé | Utilisez dorénavant l’IU [ContextHub](/help/sites-authoring/ch-previewing.md). |
| Outil de recherche de contenu pour les différents types de médias | Terminer |  |
| Liste des composants | Terminer |  |
| Copier et coller des composants | Terminer |  |
| Liste des composants du presse-papiers | Absente |  |
| Annuler/rétablir | Complète |  |
| Faire glisser le contenu dans l’espace réservé du composant | Terminer |  |
| Faire glisser le contenu directement dans l’espace réservé de l’analyse avec la création automatique de composant | Terminer |  |

## État des fonctionnalités : éditeurs de texte, d’image et de tableau {#feature-status-text-table-and-image-editors}

Il s’agit d’une liste des fonctionnalités de l’interface utilisateur classique Texte, Tableau et Editeur d’image et de l’état de l’interface utilisateur tactile.

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Éditeur de texte enrichi | Terminer | Cette option est utilisable en place, dans la boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes RTE | Terminer | Vous pouvez utiliser l&#39;[éditeur de modèles](/help/sites-authoring/templates.md). |
| Utiliser RTE pour le texte brut | Terminer |  |
| Module externe RTE : Liens et ancre | Terminer |  |
| Module externe RTE : Zone cliquable | Terminer |  |
| Module externe RTE : Copier/coller | Terminer |  |
| Module externe RTE : Coller à partir de Microsoft Word | Terminer |  |
| Module externe RTE : Rechercher et remplacer | Terminer |  |
| Module externe RTE : Formats de texte (gras, ...) | Terminer |  |
| Module externe RTE : Sous-et-exposant | Terminer |  |
| Module externe RTE : Justifier | Terminer |  |
| Module externe RTE : Listes (puces / numéros) | Terminer |  |
| Module externe RTE : Format de paragraphe | Terminer |  |
| Module externe RTE : Styles de texte | Terminer |  |
| Module externe RTE : Éditeur de source (Modifier HTML) | Terminer | Uniquement disponible en boîte de dialogue et en plein écran. |
| Module externe RTE : Vérificateur orthographique | Terminer |  |
| Module externe RTE : Tableau (éditeur de tableau incorporé) | Terminer |  |
| Module externe RTE : Annuler/Rétablir | Terminer |  |
| Module externe RTE : Autoriser les images en ligne | Terminer |  |
| Editeur de tableau | Terminer | Cette option est utilisable en place, dans la boîte de dialogue et en plein écran. |
| Faire glisser l’image dans la cellule du tableau | Terminer | Utilisation en ligne |
| Éditeur d’image | Terminer | Cette option est utilisable en place, dans la boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes IPE | Terminer | AEM 6.3 a introduit une interface utilisateur dans l&#39;[éditeur de modèles](/help/sites-authoring/templates.md). |
| Module externe IPE : Recadrer | Terminer |  |
| Module externe IPE : Retourner | Terminer |  |
| Module externe IPE : Annuler/Rétablir | Terminer |  |
| Module externe IPE : Zone cliquable | Terminer |  |
| Module externe IPE : Rotation | Terminer |  |
| Module externe IPE : Zoom | Terminer |  |

## État des fonctionnalités : outils {#feature-status-tools}

La liste ci-dessous répertorie divers outils proposés dans l’IU classique et indique leur état dans l’IU optimisée pour les écrans tactiles.

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Gestion des tâches | Remplacé | 6.0 Introduction de projets et de tâches. |
| Boîte de réception du processus | Terminer |  |
| Configuration du modèle de flux de travail vers la page (`/etc/workflow/wcm/templates.html`) | Absente | Utiliser l’IU classique. |
| Interface utilisateur d’administration du balisage | Terminer |  |
| Centre de contrôle MSM/Blueprint | Terminer |  |
| Interface utilisateur de Blueprint Manager | Terminer |  |
| Interface utilisateur de configuration de lancement | Absente | Utiliser l’IU classique. |
| IU des utilisateurs, groupes et autorisations | Principalement terminé | Pour modifier des autorisations avancées, utilisez l’interface utilisateur classique. |
| Purger des versions (`/etc/versioning/purge.html`) | Absente | Utiliser l’IU classique. |
| Vérificateur de lien externe (`/etc/linkchecker.html`) | Absente | Utiliser l’IU classique. |
| Éditeur en bloc (`/etc/importers/bulkeditor.html`) | Absente | Utiliser l’IU classique. |
| Télécharger des miniatures pour les ajouter ou les remplacer | Absente | Utiliser l’IU classique. |
