---
title: Modification de l’aspect (HBS)
seo-title: Modification de l’aspect
description: Modification des scripts HBS
seo-description: Modification des scripts HBS
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Modifier l’aspect (HBS) {#alter-the-appearance-hbs}

Maintenant que les composants du système de commentaires personnalisé dans le répertoire de l’application (/apps) sont en place, avec un resourceSuperType référençant le système de commentaires par défaut et le modèle/affichage personnalisé enregistré, il est possible de modifier l’implémentation.

Pour une démonstration simple, l’avatar affiché pour l’utilisateur connecté qui publie un commentaire est supprimé.

>[!NOTE]
>
>Pour utiliser l’extension , l’instance du système de commentaires d’un site web à affecter (/content) doit définir son resourceType comme système de commentaires personnalisé.

## Modification des scripts HBS {#modify-the-hbs-scripts}

Utilisation de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Ouvrez [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Commentez la balise qui contient l’avatar d’une publication de commentaire (~ ligne 21) :

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Ouvrez [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Mettez en commentaire la balise qui contient l’avatar pour la prochaine entrée de commentaire (~ ligne 44) :

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* Sélectionnez **Enregistrer tout**.

### Répliquer l’application personnalisée {#replicate-custom-app}

Une fois l’application modifiée, il est nécessaire de répliquer à nouveau le composant personnalisé.

Pour ce faire, procédez comme suit :

* À partir du menu principal

   * Sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]**.
   * Sélectionnez **[!UICONTROL Activer l’arborescence]**.
   * Définissez `Start Path` sur `/apps/custom`.
   * Désélectionnez **[!UICONTROL Uniquement Modifié]**.
   * Sélectionnez le bouton **[!UICONTROL Activer]** .

### Afficher le commentaire modifié sur l’exemple de page publié {#view-modified-comment-on-published-sample-page}

[En poursuivant l’](/help/communities/extend-sample-page.md#publish-sample-page) expérience sur l’instance de publication, toujours connecté en tant qu’utilisateur identique, il est désormais possible d’actualiser la page dans l’environnement de publication pour afficher la modification afin de supprimer l’avatar :

![view-modified-content](assets/view-modified-content.png)

### Exemple de module d’extension de commentaire {#sample-comment-extension-package}

Vous trouverez ci-joint un package de l’application de commentaires personnalisés créée dans ce tutoriel.

[Obtenir le fichier](assets/sample-comment-extension-6-1-fp3.zip)
