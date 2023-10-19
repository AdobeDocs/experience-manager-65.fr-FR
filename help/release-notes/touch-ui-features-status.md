---
title: Statut des fonctionnalités de l’IU tactile
description: Notes de mise à jour spécifiques à l’IU tactile d’ [!DNL Adobe Experience Manager]
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: ht
source-wordcount: '1067'
ht-degree: 100%

---

# Statut des fonctionnalités de l’IU tactile {#touch-ui-feature-status}

L’interface utilisateur classique d’Adobe Experience Manager (AEM) 6.4 et versions ultérieures [est obsolète.](../release-notes/deprecated-removed-features.md) Adobe n’apporte pas d’autres améliorations à l’interface utilisateur classique et recommande d’utiliser les nouvelles fonctionnalités puissantes disponibles dans l’interface utilisateur tactile.

Depuis la version 6.0, AEM est doté d’une nouvelle interface appelée Interface utilisateur optimisée pour les écrans tactiles (ou IU tactile) qui s’aligne sur [!DNL Adobe Experience Cloud] et sur les instructions générales concernant les interfaces utilisateur Adobe. Avec la mise en œuvre quasi totale de la parité des fonctionnalités, cette interface est devenue l’interface utilisateur standard d’AEM. L’ancienne interface orientée bureau est dénommée « IU classique ».

Bien que la plupart des fonctionnalités soient déjà présentes dans l’interface utilisateur optimisée pour les écrans tactiles, il en reste certaines à intégrer, qui le seront dans les prochaines mises à jour.

La liste ci-dessous indique le statut des fonctionnalités implémentées dans AEM 6.5.

Pour obtenir des recommandations destinées aux utilisateurs qui effectuent une mise à niveau vers AEM 6.5, consultez les [recommandations relatives à l’interface utilisateur pour les clients](/help/sites-deploying/ui-recommendations.md)..

>[!NOTE]
>
>Cette page traite uniquement de la parité des fonctionnalités avec l’IU classique. Les fonctionnalités qui ont été ajoutées à l’IU optimisée pour les écrans tactiles et qui sont absentes de l’IU classique ne sont pas répertoriées.

>[!NOTE]
>
>Cette liste a pour objectif d’être la plus complète possible, mais ne doit pas être considérée comme exhaustive.

## Légende {#legend}

* **Complète** : la fonctionnalité est pleinement disponible dans l’IU tactile.
* **Principalement** : la fonctionnalité est principalement disponible dans l’IU optimisée pour les écrans tactiles.
* **Absente** : la fonctionnalité n’est pas présente dans l’IU tactile. L’IU classique doit être utilisée pour effectuer cette action.
* **Remplacée** : la fonctionnalité a été remplacée par une nouvelle implémentation qui fonctionne différemment.
* **Supprimée :** la fonctionnalité n’existe plus dans l’IU optimisée pour les écrans tactiles et elle ne sera pas remplacée.

## Statut des fonctionnalités : administration de sites {#feature-status-sites-admin}

Vous trouverez ci-dessous la liste des fonctionnalités de l’Administration de sites de l’IU classique (`/siteadmin`) et leur statut dans l’IU optimisée pour les écrans tactiles (`/sites.html`).

| Fonctionnalité | Statut | Commentaire |
|--- |--- |--- |
| Navigation dans l’arborescence du site | Complète | AEM 6.4 a introduit un [aperçu d’arborescence de contenu](/help/sites-authoring/basic-handling.md#content-tree). |
| Démarrer le workflow | Complète |  |
| Créer une page | Complète |  |
| Créer un nouveau site | Complète |  |
| Créer un lancement | Complète |  |
| Créer une Live Copy | Complète |  |
| Créer un dossier | Complète |  |
| Afficher le statut de publication | Complète | À compter d’AEM version 6.5, le statut du workflow s’affiche dans la vue Liste. |
| Rechercher | Complète |  |
| Copier/coller une page (duplication) | Complète |  |
| Déplacer des pages | Terminé |  |
| Publier des pages | Terminé |  |
| Publier des pages sans droits de réplication | Complète |  |
| Publier ultérieurement | Complète |  |
| Publier l’arborescence | Complète |  |
| Annuler la publication de pages | Terminé |  |
| Annuler la publication de pages sans droits de réplication | Complète |  |
| Dépublier ultérieurement | Complète |  |
| Supprimer | Complète |  |
| Verrouiller/déverrouiller | Complète |  |
| Afficher/modifier les propriétés | Complète |  |
| Définir les autorisations sur les pages | Complète |  |
| Historique des versions | Complète |  |
| Restaurer la version | Complète |  |
| Restaurer l’arborescence et les pages supprimées | Absente | Utiliser l’IU classique. |
| Afficher la différence entre l’ancienne et la nouvelle version | Complète |  |
| Actions Live Copy (déploiement) | Complète |  |
| Voir Copies de langue | Complète |  |
| Rechercher et remplacer | Absente | Utiliser l’IU classique. |
| Boîte de réception des notifications (événements JCR) | Absente | Utiliser l’IU classique. Remplacée par une autre implémentation à venir. |
| Références | Complète | Affichage des liens de page entrants ajoutés à AEM 6.5. |

## Statut des fonctionnalités : éditeur de page {#feature-status-page-editor}

Vous trouverez ci-dessous la liste des fonctionnalités de l’éditeur de page de l’interface utilisateur classique (`/cf#`) et leur statut dans l’IU optimisée pour les écrans tactiles (`/editor.html`).

| Fonctionnalité | Statut | Commentaire |
|--- |--- |--- |
| Modifier les pages web | Complète |  |
| Modifier les pages web mobiles | Complète |  |
| Modifier le contenu importé via Design Importer  | Complète |  |
| Modifier les e-mails | Complète |  |
| Modifier les applications mobiles hybrides | Complète |  |
| Modifier les formulaires | Complète |  |
| Modifier les offres | Complète |  |
| Modifier les modèles de workflows | Complète |  |
| Mode : Modifier et Prévisualiser | Complète |  |
| Aperçu réactif | Complète |  |
| Mode : modifier la conception | Complète |  |
| Mode : génération de modèles automatique | Complète |  |
| Mode : Statut des Live Copy | Complète |  |
| Ajouter des annotations | Complète |  |
| Modification des propriétés | Complète |  |
| Déployer la page | Complète |  |
| Démarrer et afficher le workflow | Complète |  |
| Présentation des packages de workflows | Principalement | Accessible dans l’interface utilisateur tactile. Plusieurs payloads de workflow sont toujours présentées dans l’IU classique. |
| Verrouiller/déverrouiller la page | Complète |  |
| Publier la page | Complète |  |
| Dépublication de la page | Complète |  |
| Copie de la page | Supprimé | Utilisez l’Administration de sites pour [copier les pages](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Déplacer la page | Supprimé | Utilisez l’Administration de sites pour [déplacer les pages](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Supprimer la page | Supprimé | Utilisez l’Administration de sites pour [supprimer les pages](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Afficher les références | Supprimé | Utilisez l’Administration de sites pour voir la [liste de référence détaillée](/help/sites-authoring/author-environment-tools.md#references). |
| Journal d’audit | Supprimé | Utilisez l’Administration de sites et [ouvrez le rail d’activité](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Créer la version | Supprimé | Utilisez l’Administration de sites pour [créer de nouvelles versions](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurer la version | Supprimé | Utilisez Administration de sites pour [restaurer des versions](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Changer les lancements | Supprimé | Utilisez l’Administration de sites pour [basculer entre les lancements](/help/sites-authoring/launches-promoting.md). |
| Traduire la page | Supprimé | Utilisez l’Administration de sites pour [ajouter une page aux projets de traduction](/help/sites-administering/tc-manage.md). |
| Distorsion du temps (choisissez la date/l’heure et parcourez le site tel qu’il était avant) | Complète |  |
| Définir les autorisations | Complète |  |
| IU contextuelle du client  | Remplacé | Utilisez dorénavant l’interface utilisateur [ContextHub](/help/sites-authoring/ch-previewing.md). |
| Outil de recherche de contenu pour les différents types de médias | Complète |  |
| Liste des composants | Complète |  |
| Copier/coller de composants | Complète |  |
| Liste des composants dans le presse-papiers | Absente |  |
| Annuler/rétablir | Complète |  |
| Glisser du contenu dans un espace réservé aux composants | Complète |  |
| Avec la création automatique de composants, faites glisser le contenu directement dans l’espace réservé de parsys. | Complète |  |

## Statut des fonctionnalités : éditeurs de texte, d’image et de tableau {#feature-status-text-table-and-image-editors}

Vous trouverez ci-dessous la liste des fonctionnalités des éditeurs de texte, d’image et de tableau de l’interface utilisateur classique et leur statut dans l’IU optimisée pour les écrans tactiles.

| Fonctionnalité | Statut | Commentaire |
|--- |--- |--- |
| Éditeur de texte enrichi | Complète | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes de l’éditeur de texte enrichi | Complète | Cette opération peut être effectuée à l’aide de l’[Éditeur de modèles](/help/sites-authoring/templates.md). |
| Utilisation de l’éditeur de texte enrichi pour le texte brut | Complète |  |
| Module externe de l’éditeur de texte enrichi : liens et ancre | Complète |  |
| Module externe de l’éditeur de texte enrichi : table de caractères | Complète |  |
| Module externe de l’éditeur de texte enrichi : copier/coller | Complète |  |
| Plug-in de l’éditeur de texte enrichi : coller à partir de Microsoft® Word | Complète |  |
| Module externe de l’éditeur de texte enrichi : rechercher et remplacer | Complète |  |
| Module externe de l’éditeur de texte enrichi : formats de texte (gras, ...) | Complète |  |
| Module externe de l’éditeur de texte enrichi : indice et exposant | Complète |  |
| Module externe de l’éditeur de texte enrichi : justifier | Complète |  |
| Plug-in de l’éditeur de texte enrichi : listes (puces/nombres) | Complète |  |
| Module externe de l’éditeur de texte enrichi : format de paragraphe | Complète |  |
| Module externe de l’éditeur de texte enrichi : styles de texte | Complète |  |
| Module externe de l’éditeur de texte enrichi : Éditeur de source (Modifier le HTML) | Complète | Disponible uniquement dans la boîte de dialogue et en plein écran. |
| Module externe de l’éditeur de texte enrichi : vérificateur orthographique | Complète |  |
| Module externe de l’éditeur de texte enrichi : tableau (éditeur de tableau incorporé) | Complète |  |
| Module externe de l’éditeur de texte enrichi : annuler/rétablir | Complète |  |
| Module externe de l’éditeur de texte enrichi : autorisation des images en ligne | Complète |  |
| Éditeur de tableau | Complète | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Faire glisser l’image dans la cellule du tableau | Complète | Utilisable en ligne |
| Éditeur d’image | Complète | Utilisable sur place, dans une boîte de dialogue et en plein écran. |
| Activation/désactivation des modules externes IPE | Complète | AEM version 6.3 a introduit une interface utilisateur dans l’[Éditeur de modèles](/help/sites-authoring/templates.md). |
| Module externe IPE : recadrer | Complète |  |
| Module externe IPE : retourner | Complète |  |
| Module externe IPE : annuler/rétablir | Complète |  |
| Module externe IPE : zone cliquable | Complète |  |
| Module externe IPE : rotation | Complète |  |
| Module externe IPE : zoom | Complète |  |

## Statut des fonctionnalités : outils {#feature-status-tools}

Vous trouverez ci-dessous la liste des divers outils de l’IU classique et leur statut dans l’IU tactile.

| Fonctionnalité | Statut | Commentaire |
|--- |--- |--- |
| Gestion des tâches | Remplacé | La version 6.0 introduit les projets et les tâches. |
| Boîte de réception des workflows | Complète |  |
| Configuration de modèle de workflow en page (`/etc/workflow/wcm/templates.html`) | Absente | Utiliser l’IU classique. |
| Interface utilisateur d’administration du balisage | Complète |  |
| Centre de contrôle des plans directeurs / MSM | Complète |  |
| Interface utilisateur du gestionnaire de plans directeurs | Complète |  |
| Interface utilisateur de configuration du déploiement | Absente | Utiliser l’IU classique. |
| Interface utilisateur des utilisateurs/utilisatrices, groupes et autorisations | Principalement complète | Pour la modification avancée d’autorisations, utilisez l’interface utilisateur classique. |
| Purge des versions (`/etc/versioning/purge.html`) | Absente | Utiliser l’IU classique. |
| Vérificateur de lien externe (`/etc/linkchecker.html`) | Absente | Utiliser l’IU classique. |
| Éditeur en bloc (`/etc/importers/bulkeditor.html`) | Absente | Utiliser l’IU classique. |
| Chargement de miniatures pour en ajouter ou les remplacer | Absente | Utiliser l’IU classique. |
