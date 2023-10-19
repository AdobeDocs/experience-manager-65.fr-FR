---
title: Incrustation de composants Communities
description: Découvrez comment superposer un composant par défaut afin de pouvoir modifier globalement l’aspect ou le comportement d’un composant pour toutes les références relatives au composant.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Incrustation de composants Communities {#overlay-communities-components}

L’intention de [superposition](/help/communities/client-customize.md#overlays) un composant par défaut consiste à modifier globalement l’aspect ou le comportement d’un composant, pour toutes les références relatives au composant. Il repose sur la nature de sling à résoudre dans le dossier /apps avant de rechercher dans le dossier /libs . Par conséquent, le chemin d’accès au composant est identique à celui du composant par défaut, sauf qu’il se trouve dans le dossier /apps et non dans le dossier /libs .

## Exemple {#example}

**Composant des commentaires de superposition**

Supposons que vous souhaitiez modifier la fonction de commentaire afin qu’elle corresponde à la conception de votre site web, en modifiant l’en-tête du commentaire afin qu’il n’affiche plus l’avatar pour un commentaire. Les solutions pour masquer l’avatar utilisent soit CSS, soit, comme décrit ici, le recouvrement du fichier header.jsp dans le dossier des applications afin que le HTML contenant l’avatar ne soit jamais envoyé au client.

Pour superposer des commentaires, vous devez :

1. [Page Créer un commentaire](/help/communities/overlay-create-comments-page.md)
1. [Création de noeuds](/help/communities/overlay-create-nodes.md)
1. [Modification de l’aspect](/help/communities/overlay-alter-appearance.md)

**Incrustation d’emails de notifications**

Supposons que vous souhaitiez personnaliser le message des notifications par e-mail, vous pouvez le faire en [superposition](/help/communities/client-customize.md#overlays) les modèles à l’adresse `/libs/settings/community/templates/email/html`.

Supposons, par exemple, que vous souhaitiez modifier les notifications par courrier électronique relatives aux mentions (pour un composant Communities spécifique dans lequel le contenu créé par l’utilisateur est). Dans ce cas, ajoutez une **if** condition pour verbe **mentions** dans les modèles des composants pour lesquels vous avez activé la fonction **@mentions** la prise en charge.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Pour modifier le modèle de notification électronique pour @mention dans les commentaires de blog, placez le modèle prêt à l’emploi à l’adresse : `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
