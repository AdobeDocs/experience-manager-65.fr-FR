---
title: Composants des communautés de recouvrement
description: Découvrez comment superposer un composant par défaut afin de pouvoir modifier globalement l’aspect ou le comportement d’un composant, pour toutes les références relatives au composant.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Composants des communautés de recouvrement {#overlay-communities-components}

L’intention du [recouvrement](/help/communities/client-customize.md#overlays) d’un composant par défaut est de modifier globalement l’aspect ou le comportement d’un composant, pour toutes les références relatives au composant. Il dépend de la nature de sling pour être résolu sur le dossier /apps avant de rechercher dans le dossier /libs. Par conséquent, le chemin d’accès au composant est identique au chemin d’accès au composant par défaut, sauf qu’il se trouve dans le dossier /apps et non dans le dossier /libs.

## Exemple {#example}

**Composant Commentaires de recouvrement**

Supposons que vous souhaitiez modifier la fonction de commentaire afin qu’elle corresponde à la conception de votre site web, en modifiant l’en-tête de commentaire afin qu’elle n’affiche plus l’avatar d’un commentaire. Les solutions pour masquer l’avatar utilisent le CSS ou, comme décrit ici, le recouvrement du fichier header.jsp dans le dossier d’applications afin que l’HTML contenant l’avatar ne soit jamais envoyée au client.

Pour superposer des commentaires, vous devez :

1. [Page Créer des commentaires](/help/communities/overlay-create-comments-page.md)
1. [Créer des nœuds](/help/communities/overlay-create-nodes.md)
1. [Modifier l’apparence](/help/communities/overlay-alter-appearance.md)

**E-mails de notification de recouvrement**

Supposons que vous souhaitiez personnaliser le message de notification par e-mail en [superposant](/help/communities/client-customize.md#overlays) les modèles à l’`/libs/settings/community/templates/email/html`.

Supposons, par exemple, que vous souhaitiez modifier les notifications par e-mail de mentions (pour un composant Communities spécifique dans lequel du contenu créé par l’utilisateur est créé). Dans ce cas, ajoutez une condition **if** pour le verbe **mention** dans les modèles des composants pour lesquels vous avez activé la prise en charge de **@mentions**.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Pour modifier le modèle de notification par e-mail à @mention dans les commentaires de blog, placez le modèle prêt à l’emploi à l’emplacement suivant : `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
