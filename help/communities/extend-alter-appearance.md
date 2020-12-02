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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Modifier l&#39;apparence (HBS) {#alter-the-appearance-hbs}

Maintenant que les composants du système de commentaires personnalisés dans le répertoire de l&#39;application (/apps) sont en place, avec un resourceSuperType référençant le système de commentaires par défaut et le modèle/Vue personnalisé enregistré, il est possible de modifier l&#39;implémentation.

Pour une simple démonstration, une fonction visuelle, l’avatar affiché par l’utilisateur connecté qui publie un commentaire, est supprimée.

>[!NOTE]
>
>Pour utiliser l&#39;extension, l&#39;instance du système de commentaires d&#39;un site Web à affecter (/content) doit définir resourceType comme système de commentaires personnalisé.

## Modification des scripts HBS {#modify-the-hbs-scripts}

Utilisation de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Ouvrez [/apps/custom/components/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Mettez en commentaire la balise qui contient l’avatar pour un commentaire (~ ligne 21) :

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Ouvrez [/apps/custom/components/commentaires/**commentaires.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Mettez en commentaire la balise qui contient l’avatar pour la prochaine entrée de commentaire (~ ligne 44) :

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* Sélectionner **Enregistrer tout**

### Répliquer l’application personnalisée {#replicate-custom-app}

Une fois l’application modifiée, il est nécessaire de reproduire à nouveau le composant personnalisé.

L&#39;une des façons de le faire est :

* Dans le menu principal

   * Sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]**.
   * Sélectionnez **[!UICONTROL Activer l&#39;arbre]**.
   * Définissez `Start Path` sur `/apps/custom`.
   * Désélectionnez **[!UICONTROL Uniquement modifié]**.
   * Sélectionnez le bouton **[!UICONTROL Activer]**.

### Commentaire modifié de la vue sur l’exemple de page publié {#view-modified-comment-on-published-sample-page}

[En poursuivant l’](/help/communities/extend-sample-page.md#publish-sample-page) expérience de l’instance de publication, toujours connectée en tant que même utilisateur, il est maintenant possible d’actualiser la page dans l’environnement de publication afin de vue la modification de suppression de l’avatar :

![Contenu modifié par vue](assets/view-modified-content.png)

### Exemple de package d&#39;extension de commentaire {#sample-comment-extension-package}

Vous trouverez ci-joint un package de l&#39;application de commentaires personnalisés créée dans ce didacticiel.

[Obtenir le fichier](assets/sample-comment-extension-6-1-fp3.zip)
