---
title: État des fonctionnalités de l’IU tactile
description: Notes de mise à jour spécifiques à [!DNL Adobe Experience Manager] IU tactile.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 50%

---

# État des fonctionnalités de l’IU tactile {#touch-ui-feature-status}

AEM version 6.4 et ultérieure [L’interface utilisateur classique est obsolète.](../release-notes/deprecated-removed-features.md). Adobe n’apporte pas d’autres améliorations à l’interface utilisateur classique et les utilisateurs sont encouragés à tirer parti des nouvelles fonctionnalités puissantes disponibles dans l’interface utilisateur tactile.

À compter de la version 6.0, AEM a introduit une nouvelle interface utilisateur appelée &quot;IU tactile&quot; (simplement appelée &quot;IU tactile&quot;) alignée sur la [!DNL Adobe Experience Cloud] et aux directives générales de l’interface utilisateur d’Adobe. Avec la quasi parité des fonctionnalités atteinte, cette interface est devenue l’interface standard d’AEM avec l’ancienne interface orientée bureau appelée &quot;IU classique&quot;.

Bien que la plupart des fonctionnalités soient déjà présentes dans l’interface utilisateur optimisée pour les écrans tactiles, il en reste certaines à intégrer, qui le seront dans les prochaines mises à jour.

La liste suivante présente l’état actuel des fonctionnalités mises en oeuvre dans AEM 6.5.

Pour des recommandations destinées aux clients effectuant une mise à niveau vers AEM 6.5, voir [Recommandations relatives à l’interface utilisateur pour les clients](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Cette page traite uniquement de la parité des fonctionnalités avec l’IU classique. Les fonctionnalités ajoutées à l’IU tactile et uniques qui ne sont pas présentes dans l’IU classique ne sont pas répertoriées.

>[!NOTE]
>
>Cette liste s’efforce d’être complète, mais n’est pas exhaustive.

## Légende {#legend}

* **Complète :** la fonctionnalité est entièrement disponible dans l’IU optimisée pour les écrans tactiles..
* **Principalement**: Cette fonctionnalité est principalement disponible dans l’IU tactile.
* **Absente :** la fonctionnalité n’est pas disponible dans l’IU optimisée pour les écrans tactiles. L’IU classique doit être utilisée pour exécuter cette action.
* **Remplacée :** la fonctionnalité a été remplacée par une nouvelle implémentation qui fonctionne différemment.
* **Supprimée :** la fonctionnalité n’existe plus dans l’IU optimisée pour les écrans tactiles et elle ne sera pas remplacée.

## État des fonctionnalités : Administration de sites {#feature-status-sites-admin}

Il s’agit d’une liste des fonctionnalités de l’interface utilisateur classique de l’administrateur de site (`/siteadmin`) a et l’état dans l’interface utilisateur tactile (`/sites.html`).

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Navigation dans l’arborescence du site | Terminé | AEM 6.4 a introduit une [arborescence de contenu](/help/sites-authoring/basic-handling.md#content-tree). |
| Démarrer le processus | Terminé |  |
| Créer une page | Terminé |  |
| Créer un site | Terminé |  |
| Créer un lancement | Terminé |  |
| Créer une Live Copy | Terminé |  |
| Créer un dossier | Terminé |  |
| Afficher l’état de publication | Terminé | À compter de AEM version 6.5, l’état du workflow s’affiche en mode Liste. |
| Rechercher | Terminé |  |
| Copier et coller la page (Dupliquer) | Terminé |  |
| Déplacer une page | Terminé |  |
| Publier une page | Terminé |  |
| Publier une page sans droits de réplication | Terminé |  |
| Publier ultérieurement | Terminé |  |
| Publier l’arborescence | Terminé |  |
| Annuler la publication de page(s) | Terminé |  |
| Annuler la publication de page(s) sans droits de réplication | Terminé |  |
| Annuler la publication ultérieurement | Terminé |  |
| Supprimer | Terminé |  |
| Verrouiller/déverrouiller | Terminé |  |
| Afficher/modifier les propriétés | Terminé |  |
| Définir les autorisations sur les pages | Terminé |  |
| Historique des versions | Terminé |  |
| Restaurer la version | Terminé |  |
| Restaurer l’arborescence et les pages supprimées | Absente | Utiliser l’IU classique. |
| Afficher la différence entre l’ancienne et la nouvelle version | Terminé |  |
| Actions Live Copy (déploiement) | Terminé |  |
| Afficher les copies de langue | Terminé |  |
| Rechercher et remplacer | Absente | Utiliser l’IU classique. |
| Boîte de réception de notifications (événements JCR) | Absente | Utiliser l’IU classique. Sera remplacée par une autre implémentation. |
| Références | Terminé | Affichage des liens de page entrants ajoutés à AEM 6.5. |

## État des fonctionnalités : éditeur de page {#feature-status-page-editor}

Il s’agit d’une liste des fonctionnalités de l’éditeur de page de l’IU classique (`/cf#`) a et l’état dans la fonction tactile (`/editor.html`).

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Modifier les pages web | Terminé |  |
| Modifier les pages web mobiles | Terminé |  |
| Modifier le contenu importé via Design Importer  | Terminé |  |
| Modifier les courriers électroniques | Terminé |  |
| Modification d’applications mobiles hybrides | Terminé |  |
| Modifier les formulaires | Terminé |  |
| Modifier les offres | Terminé |  |
| Modifier les modèles de processus | Terminé |  |
| Mode : Modifier et prévisualiser | Terminé |  |
| Aperçu réactif | Terminé |  |
| Mode : Modifier la conception | Terminé |  |
| Mode : Scaffolding | Terminé |  |
| Mode : État des Live Copy | Terminé |  |
| Ajouter des annotations | Terminé |  |
| Modification des propriétés | Terminé |  |
| Déployer la page | Terminé |  |
| Démarrer et afficher le workflow | Terminé |  |
| Gestion des packages de workflow | Principalement | Complètement accessible dans l’interface utilisateur tactile. Plusieurs payload de workflow sont toujours présentés dans l’IU classique. |
| Verrouiller/déverrouiller la page | Terminé |  |
| Publier la page | Terminé |  |
| Annuler la publication de la page | Terminé |  |
| Copie de la page | Supprimé | Utilisez Administration de sites pour [copier les pages](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Déplacer la page | Supprimé | Utilisez Administration de sites pour [déplacer les pages](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Supprimer la page | Supprimé | Utilisez Administration de sites pour [supprimer les pages](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Afficher les références | Supprimé | Utilisez Administration de sites pour afficher la variable [liste de références détaillée](/help/sites-authoring/author-environment-tools.md#references). |
| Journal d’audit | Supprimé | Utilisez Administration de sites et [ouvrez le rail d’activité](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Créer la version | Supprimé | Utilisez Administration de sites pour [créer de nouvelles versions](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurer la version | Supprimé | Utilisez Administration de sites pour [restaurer des versions ](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Passer d’un lancement à un autre | Supprimé | Utilisez Administration de sites pour [basculer entre les lancements](/help/sites-authoring/launches-promoting.md). |
| Traduire la page | Supprimé | Utilisez Administration de sites pour [ajouter une page aux projets de traduction](/help/sites-administering/tc-manage.md). |
| Timewarp (choisissez la date/l’heure et parcourez le site tel qu’il était avant)  | Terminé |  |
| Définir les autorisations | Terminé |  |
| IU contextuelle du client  | Remplacé | Utilisez dorénavant l’IU [ContextHub](/help/sites-authoring/ch-previewing.md). |
| Outil de recherche de contenu pour les différents types de médias | Terminé |  |
| Liste des composants | Terminé |  |
| Copier et coller des composants | Terminé |  |
| Liste des composants du presse-papiers | Absente |  |
| Annuler/rétablir | Terminé |  |
| Faire glisser du contenu dans l’espace réservé du composant | Terminé |  |
| Faire glisser directement le contenu dans l’espace réservé parsys avec la création automatique de composant | Terminé |  |

## État des fonctionnalités : éditeurs de texte, d’image et de tableau {#feature-status-text-table-and-image-editors}

Il s’agit d’une liste des fonctionnalités de l’IU classique Texte, Tableau et Éditeur d’image et de l’état de l’IU tactile.

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Éditeur de texte enrichi | Terminé | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes de l’éditeur de texte enrichi | Terminé | Cette opération peut être effectuée à l’aide de la méthode [Éditeur de modèles](/help/sites-authoring/templates.md). |
| Utilisation de l’éditeur de texte enrichi pour le texte brut | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Liens et ancre | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Table de caractères | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Copier/coller | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Coller à partir de Microsoft Word | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Rechercher et remplacer | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Formats de texte (gras, ...) | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Indice et exposant | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Justifier | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Listes (puce/nombres) | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Format de paragraphe | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Styles de texte | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Éditeur de source (Modifier le HTML) | Terminé | Disponible uniquement dans la boîte de dialogue et en plein écran. |
| Module externe de l’éditeur de texte enrichi : Vérificateur orthographique | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Tableau (éditeur de tableau incorporé) | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Annuler/rétablir | Terminé |  |
| Module externe de l’éditeur de texte enrichi : Autorisation des images en ligne | Terminé |  |
| Éditeur de tableau | Terminé | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Faire glisser l’image dans la cellule du tableau | Terminé | Utilisable en ligne |
| Éditeur d’image | Terminé | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes IPE | Terminé | AEM version 6.3 a introduit une interface utilisateur dans [Éditeur de modèles](/help/sites-authoring/templates.md). |
| Module externe IPE : Recadrer | Terminé |  |
| Module externe IPE : Retourner | Terminé |  |
| Module externe IPE : Annuler/rétablir | Terminé |  |
| Module externe IPE : Zone cliquable | Terminé |  |
| Module externe IPE : Rotation | Terminé |  |
| Module externe IPE : Zoom | Terminé |  |

## État des fonctionnalités : outils {#feature-status-tools}

La liste ci-dessous répertorie divers outils proposés dans l’IU classique et indique leur état dans l’IU optimisée pour les écrans tactiles.

| Fonctionnalité | État | Commentaire |
|--- |--- |--- |
| Gestion des tâches | Remplacé | La version 6.0 introduit les projets et les tâches. |
| Boîte de réception des workflows | Terminé |  |
| Configuration de modèle de workflow vers page (`/etc/workflow/wcm/templates.html`) | Absente | Utiliser l’IU classique. |
| Interface utilisateur d’administration du balisage | Terminé |  |
| MSM/Centre de contrôle des plans directeurs | Terminé |  |
| Interface utilisateur de Blueprint Manager | Terminé |  |
| Interface utilisateur de configuration du déploiement | Absente | Utiliser l’IU classique. |
| Interface utilisateur des utilisateurs, groupes et autorisations | Principalement terminé | Pour la modification avancée d’autorisations, utilisez l’interface utilisateur classique. |
| Purge des versions (`/etc/versioning/purge.html`) | Absente | Utiliser l’IU classique. |
| Vérificateur de lien externe (`/etc/linkchecker.html`) | Absente | Utiliser l’IU classique. |
| Éditeur en bloc (`/etc/importers/bulkeditor.html`) | Absente | Utiliser l’IU classique. |
| Chargement de miniatures pour ajouter ou remplacer celles-ci | Absente | Utiliser l’IU classique. |
