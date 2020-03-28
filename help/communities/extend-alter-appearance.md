---
title: Modification de l’aspect (HBS)
seo-title: Modifier l’aspect
description: Modification des scripts HBS
seo-description: Modification des scripts HBS
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Modification de l’aspect (HBS) {#alter-the-appearance-hbs}

Maintenant que les composants du système de commentaires personnalisé dans le répertoire de l’application (/apps) sont en place, avec une ressourceSuperType référençant le système de commentaires par défaut et le modèle/ personnalisé(e) enregistré(e), il est possible de modifier l’implémentation.

Pour une démonstration simple, une fonction visuelle, l’avatar de l’utilisateur connecté qui publie un commentaire, est supprimé.

>[!NOTE]
>
>Pour utiliser l’extension, l’instance du système de commentaires d’un site Web à affecter (/content) doit définir resourceType comme système de commentaires personnalisé.

## Modification des scripts HBS {#modify-the-hbs-scripts}

Using [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Ouvrir [/applications/custom/components/commentaires/comment/**comment.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * commentez la balise qui inclut l’avatar pour un commentaire (~ ligne 21) :

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* Ouvrir [/applications/custom/components/commentaires/**commentaires.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * commentez la balise qui inclut l&#39;avatar pour la prochaine entrée de commentaire (~ ligne 44) :

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* Select **Save All**

### Répliquer l’application personnalisée {#replicate-custom-app}

Une fois l’application modifiée, il est nécessaire de reproduire à nouveau le composant personnalisé.

Une manière de le faire est

* Dans le menu principal

   * sélectionnez **Outils > Opérations > Réplication**
   * select `Activate Tree`
   * set `Start Path`: to `/apps/custom`
   * deselect `Only Modified`
   * select `Activate`button

### Commentaire  modifié sur l&#39;exemple de page publié {#view-modified-comment-on-published-sample-page}

[En poursuivant l’expérience](/help/communities/extend-sample-page.md#publish-sample-page) sur l’instance de publication, toujours connecté en tant que même utilisateur, il est maintenant possible d’actualiser la page dans le  de publication  de de de la modification pour supprimer l’avatar :

![chlimage_1-136](assets/chlimage_1-136.png)

### Exemple de package d’extension de commentaire {#sample-comment-extension-package}

Vous trouverez ci-joint un package de l’application de commentaires personnalisée créée dans ce didacticiel.

[Obtenir le fichier](assets/sample-comment-extension-6-1-fp3.zip)
