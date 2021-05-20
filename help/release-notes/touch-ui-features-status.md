---
title: État des fonctionnalités de l’IU tactile
description: Notes de mise à jour spécifiques à  [!DNL Adobe Experience Manager] l’IU tactile.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 50%

---

# État des fonctionnalités de l’IU tactile {#touch-ui-feature-status}

À partir de la version 6.4, l’interface utilisateur classique est obsolète ](../release-notes/deprecated-removed-features.md). [ Adobe n’apporte pas d’autres améliorations à l’interface utilisateur classique et les utilisateurs sont encouragés à tirer parti des nouvelles fonctionnalités puissantes disponibles dans l’interface utilisateur tactile.

À compter de la version 6.0, AEM a introduit une nouvelle interface utilisateur appelée &quot;IU tactile&quot; (simplement appelée &quot;IU tactile&quot;) alignée sur les [!DNL Adobe Experience Cloud] et les directives générales de l’interface utilisateur de l’Adobe. Avec la quasi parité des fonctionnalités atteinte, cette interface est devenue l’interface standard d’AEM avec l’ancienne interface orientée bureau appelée &quot;IU classique&quot;.

Bien que la plupart des fonctionnalités soient déjà présentes dans l’interface utilisateur optimisée pour les écrans tactiles, il en reste certaines à intégrer, qui le seront dans les prochaines mises à jour.

La liste suivante présente l’état actuel des fonctionnalités mises en oeuvre dans AEM 6.5.

Pour des recommandations destinées aux clients qui effectuent une mise à niveau vers AEM 6.5, voir [Recommandations relatives à l’interface utilisateur pour les clients](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Cette page traite uniquement de la parité des fonctionnalités avec l’IU classique. Les fonctionnalités ajoutées à l’IU tactile et uniques qui ne sont pas présentes dans l’IU classique ne sont pas répertoriées.

>[!NOTE]
>
>Cette liste s’efforce d’être complète, mais n’est pas exhaustive.

## Légende {#legend}

* **Complète :** la fonctionnalité est entièrement disponible dans l’IU optimisée pour les écrans tactiles..
* **Principalement** : Cette fonctionnalité est principalement disponible dans l’IU tactile.
* **Absente :** la fonctionnalité n’est pas disponible dans l’IU optimisée pour les écrans tactiles. L’IU classique doit être utilisée pour exécuter cette action.
* **Remplacée :** la fonctionnalité a été remplacée par une nouvelle implémentation qui fonctionne différemment.
* **Supprimée :** la fonctionnalité n’existe plus dans l’IU optimisée pour les écrans tactiles et elle ne sera pas remplacée.

## État des fonctionnalités : Administration de sites {#feature-status-sites-admin}

Il s’agit d’une liste des fonctionnalités de l’administrateur de site de l’IU classique (`/siteadmin`) et de l’état dans l’IU tactile (`/sites.html`).

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Navigation dans l’arborescence du site | Terminer | AEM 6.4 a introduit une [arborescence de contenu](/help/sites-authoring/basic-handling.md#content-tree). |
| Démarrer le processus | Terminer |  |
| Créer une page | Complète |  |
| Créer un site | Complète |  |
| Créer un lancement | Complète |  |
| Créer une Live Copy | Terminer |  |
| Créer un dossier | Complète |  |
| Afficher l’état de publication | Terminer | À compter de AEM version 6.5, l’état du workflow s’affiche en mode Liste. |
| Rechercher | Terminer |  |
| Copier et coller la page (Dupliquer) | Terminer |  |
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
| Boîte de réception de notifications (événements JCR) | Absente | Utiliser l’IU classique. Sera remplacée par une autre implémentation. |
| Références | Terminer | Affichage des liens de page entrants ajoutés à AEM 6.5. |

## État des fonctionnalités : éditeur de page {#feature-status-page-editor}

Il s’agit d’une liste des fonctionnalités de l’éditeur de page de l’IU classique (`/cf#`) et de l’état dans l’IU optimisée pour les écrans tactiles (`/editor.html`).

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
| Mode : Modifier et prévisualiser | Terminer |  |
| Aperçu réactif | Terminer |  |
| Mode : Modifier la conception | Complète |  |
| Mode : Scaffolding | Complète |  |
| Mode : État des Live Copy | Terminer |  |
| Ajouter des annotations | Complète |  |
| Modification des propriétés | Terminer |  |
| Déployer la page | Terminer |  |
| Démarrer et afficher le workflow | Terminer |  |
| Gestion des packages de workflow | Principalement | Complètement accessible dans l’interface utilisateur tactile. Plusieurs payload de workflow sont toujours présentés dans l’IU classique. |
| Verrouiller/déverrouiller la page | Complète |  |
| Publier la page | Terminer |  |
| Annuler la publication de la page | Complète |  |
| Copie de la page | Supprimé | Utilisez Administration de sites pour [copier les pages](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Déplacer la page | Supprimé | Utilisez Administration de sites pour [déplacer les pages](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Supprimer la page | Supprimé | Utilisez Administration de sites pour [supprimer les pages](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Afficher les références | Supprimé | Utilisez Administration de sites pour afficher la [liste de référence détaillée](/help/sites-authoring/author-environment-tools.md#references). |
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
| Faire glisser du contenu dans l’espace réservé du composant | Terminer |  |
| Faire glisser directement le contenu dans l’espace réservé parsys avec la création automatique de composant | Terminer |  |

## État des fonctionnalités : éditeurs de texte, d’image et de tableau {#feature-status-text-table-and-image-editors}

Il s’agit d’une liste des fonctionnalités de l’IU classique Texte, Tableau et Éditeur d’image et de l’état de l’IU tactile.

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Éditeur de texte enrichi | Terminer | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes de l’éditeur de texte enrichi | Terminer | Vous pouvez utiliser l’[éditeur de modèles](/help/sites-authoring/templates.md). |
| Utilisation de l’éditeur de texte enrichi pour le texte brut | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Liens et ancre | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Table de caractères | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Copier/coller | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Coller à partir de Microsoft Word | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Rechercher et remplacer | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Formats de texte (gras, ...) | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Indice et exposant | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Justifier | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Listes (puce/nombres) | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Format de paragraphe | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Styles de texte | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Éditeur de source (Modifier HTML) | Terminer | Disponible uniquement dans la boîte de dialogue et en plein écran. |
| Module externe de l’éditeur de texte enrichi : Vérificateur orthographique | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Tableau (éditeur de tableau incorporé) | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Annuler/rétablir | Terminer |  |
| Module externe de l’éditeur de texte enrichi : Autorisation des images en ligne | Terminer |  |
| Éditeur de tableau | Terminer | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Faire glisser l’image dans la cellule du tableau | Terminer | Utilisable en ligne |
| Éditeur d’image | Terminer | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes IPE | Terminer | AEM 6.3 a introduit une interface utilisateur dans l’ [éditeur de modèles](/help/sites-authoring/templates.md). |
| Module externe IPE : Recadrer | Terminer |  |
| Module externe IPE : Retourner | Terminer |  |
| Module externe IPE : Annuler/rétablir | Terminer |  |
| Module externe IPE : Zone cliquable | Terminer |  |
| Module externe IPE : Rotation | Terminer |  |
| Module externe IPE : Zoom | Terminer |  |

## État des fonctionnalités : outils {#feature-status-tools}

La liste ci-dessous répertorie divers outils proposés dans l’IU classique et indique leur état dans l’IU optimisée pour les écrans tactiles.

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Gestion des tâches | Remplacé | La version 6.0 introduit les projets et les tâches. |
| Boîte de réception des workflows | Terminer |  |
| Configuration du modèle de workflow vers page (`/etc/workflow/wcm/templates.html`) | Absente | Utiliser l’IU classique. |
| Interface utilisateur d’administration du balisage | Terminer |  |
| MSM/Centre de contrôle des plans directeurs | Terminer |  |
| Interface utilisateur de Blueprint Manager | Terminer |  |
| Interface utilisateur de configuration du déploiement | Absente | Utiliser l’IU classique. |
| Interface utilisateur des utilisateurs, groupes et autorisations | Principalement terminé | Pour la modification avancée d’autorisations, utilisez l’interface utilisateur classique. |
| Purge des versions (`/etc/versioning/purge.html`) | Absente | Utiliser l’IU classique. |
| Vérificateur de lien externe (`/etc/linkchecker.html`) | Absente | Utiliser l’IU classique. |
| Éditeur en bloc (`/etc/importers/bulkeditor.html`) | Absente | Utiliser l’IU classique. |
| Chargement de miniatures pour ajouter ou remplacer celles-ci | Absente | Utiliser l’IU classique. |
