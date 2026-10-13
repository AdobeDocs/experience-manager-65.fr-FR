---
title: Modifier l’apparence
description: Découvrez comment modifier le script comment.hbs responsable de la création de l’HTML globale pour chaque commentaire dans les communautés Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%
---
# Modifier l’apparence {#alter-the-appearance}

## Modifier le script {#modify-the-script}

Le script `comment.hbs` est responsable de la création de l’ensemble d’HTML pour chaque commentaire.

Pour ne pas afficher l’avatar en regard de chaque commentaire publié :

1. Copier `comment.hbs`de `libs`vers `apps`

   1. Sélectionnez `/libs/social/commons/components/hbs/comments/comment/comment.hbs`.
   1. Sélectionnez **[!UICONTROL Copier]**
   1. Sélectionnez `/apps/social/commons/components/hbs/comments/comment`.
   1. Sélectionnez **[!UICONTROL Coller]**

1. Ouvrez le `comment.hbs` recouvert

   * Double-cliquez sur le nœud `comment.hbs` dans `/apps/social/commons/components/hbs/comments/comment folder`

1. Recherchez les lignes suivantes et supprimez-les ou mettez-les en commentaire :

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Supprimez les lignes ou entourez-les de `<!--` et de `-->` pour les mettre en commentaire. De plus, les caractères &#39;xxx&#39; sont ajoutés comme indicateur visuel de l&#39;emplacement de l&#39;avatar.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Répliquer le recouvrement {#replicate-the-overlay}

Envoyez le composant Commentaires superposés à l’instance de publication à l’aide de l’outil de réplication.

>[!NOTE]
>
>Une forme de réplication plus robuste consiste à créer un package dans le gestionnaire de packages et [&#x200B; l](/help/sites-administering/package-manager.md#replicating-packages)activer. Un package peut être exporté et archivé.

Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]** et cliquez sur **[!UICONTROL Activer l’arborescence]**.

Pour le chemin de début, saisissez `/apps/social/commons` et sélectionnez **[!UICONTROL Activer]**.

![verify-content-template](assets/verify-content-template.png)

### Afficher les résultats {#view-results}

Si vous vous connectez à l’instance de publication en tant qu’administrateur, par exemple https://localhost:4503/crx/de en tant qu’administrateur/admin, vous pouvez vérifier que les composants superposés sont bien présents.

Si vous vous déconnectez, puis que vous vous connectez en tant qu’`aaron.mcdonald@mailinator.com/password` et actualisez la page, vous constatez qu’un avatar ne s’affiche pas avec le commentaire publié. Un simple « xxx » s’affiche à la place.

![create-template-component](assets/create-template-component.png)
