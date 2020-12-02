---
title: Modification de l’aspect
seo-title: Modification de l’aspect
description: Modification du script
seo-description: Modification du script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Modifier l&#39;apparence {#alter-the-appearance}

## Modifier le script {#modify-the-script}

Le script comment.hbs est responsable de la création du code HTML global pour chaque commentaire.

Pour ne pas afficher l’avatar en regard de chaque commentaire publié :

1. Copier `comment.hbs`de `libs`dans `apps`

   1. Sélectionner `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Sélectionner **[!UICONTROL Copier]**
   1. Sélectionner `/apps/social/commons/components/hbs/comments/comment`
   1. Sélectionner **[!UICONTROL Coller]**

1. Ouvrez le `comment.hbs` superposé

   * Doublon-clic sur le noeud `comment.hbs` dans `/apps/social/commons/components/hbs/comments/comment folder`

1. Recherchez les lignes suivantes et supprimez-les ou placez-les en commentaire :

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Supprimez les lignes ou entourez-les de `<!--` et `-->` pour les commenter. En outre, les caractères &#39;xxx&#39; sont ajoutés comme indicateur visuel de l&#39;endroit où l&#39;avatar aurait été.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Réplication de l’incrustation {#replicate-the-overlay}

Poussez le composant de commentaires superposés sur l’instance de publication à l’aide de l’outil de réplication.

>[!NOTE]
>
>Une forme de réplication plus robuste consisterait à créer un package dans Package Manager et à l&#39;[activer](/help/sites-administering/package-manager.md#replicating-packages). Un package peut être exporté et archivé.

Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]** et cliquez sur **[!UICONTROL Activer l&#39;arborescence]**.

Pour le chemin de Début, saisissez `/apps/social/commons` et sélectionnez **[!UICONTROL Activer]**.

![verify-content-template](assets/verify-content-template.png)

### Résultats de la vue {#view-results}

Si vous vous connectez à l’instance de publication en tant qu’administrateur (https://localhost:4503/crx/de en tant qu’administrateur/administrateur, par exemple), vous pouvez vérifier que les composants superposés sont bien présents.

Si vous vous déconnectez et vous vous reconnectez en tant que `aaron.mcdonald@mailinator.com/password` et actualisez la page, vous constaterez que le commentaire publié ne s’affiche plus avec un avatar, mais un simple &quot;xxx&quot; s’affiche.

![create-template-component](assets/create-template-component.png)

