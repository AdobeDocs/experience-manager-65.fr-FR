---
title: Incrustations de composants de communautés
seo-title: Incrustations de composants de communautés
description: Incrustations de composants de communautés
seo-description: Incrustations de composants de communautés
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Incrustations de composants de communautés {#overlay-communities-components}

L’intention de [superposer](/help/communities/client-customize.md#overlays) un composant par défaut est de modifier globalement l’aspect ou le comportement d’un composant, pour toutes les références relatives au composant. Il dépend de la nature de sling à résoudre dans le dossier /apps avant de rechercher dans le dossier /libs. Par conséquent, le chemin d’accès au composant est identique à celui du composant par défaut, sauf qu’il se trouve dans le dossier /apps et non dans le dossier /libs.

## Exemple {#example}

**Composant de commentaires d’incrustation**

Supposons que vous souhaitez modifier la fonction de commentaire afin qu’elle corresponde à la conception de votre site Web, en modifiant l’en-tête du commentaire afin qu’il n’affiche plus l’avatar pour un commentaire. Les solutions permettant de masquer l’avatar utilisent le format CSS ou, comme décrit ici, superposent le fichier header.jsp dans le dossier des applications afin que le code HTML contenant l’avatar ne soit jamais envoyé au client.

Pour superposer des commentaires, vous devez :

1. [Page Commentaires](/help/communities/overlay-create-comments-page.md)
1. [Créer des noeuds](/help/communities/overlay-create-nodes.md)
1. [Modification de l’aspect](/help/communities/overlay-alter-appearance.md)

**Courriers électroniques de notifications d’incrustation**

Supposons que vous souhaitiez personnaliser le message des notifications par courrier électronique, vous pouvez le faire en [superposant](/help/communities/client-customize.md#overlays) les modèles dans **/libs/settings/community/templates/email/html**.

Par exemple, pour modifier les notifications de mentions par courriel (pour un composant de communautés spécifique où ugc est créé), ajoutez une condition **if** pour la **mention** de verbe dans les modèles des composants pour lesquels vous avez activé la prise en charge de **@mentions** .

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Pour modifier le modèle de notifications électroniques pour @mentions dans les commentaires de blog, placez le modèle prêt à l&#39;emploi à l&#39;adresse suivante : `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
