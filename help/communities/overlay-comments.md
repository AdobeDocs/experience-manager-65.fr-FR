---
title: Incrustation des composants de communautés
seo-title: Incrustation des composants de communautés
description: Incrustation des composants de communautés
seo-description: Incrustation des composants de communautés
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# Incrustation des composants de communautés {#overlay-communities-components}

L’intention de [superposer](/help/communities/client-customize.md#overlays) un composant par défaut est de modifier globalement l’aspect ou le comportement d’un composant, pour toutes les références relatives au composant. Il s’appuie sur la nature de sling pour résoudre le problème dans le dossier /apps avant de rechercher dans le dossier /libs. Le chemin d’accès au composant est donc identique au chemin d’accès au composant par défaut, sauf qu’il se trouve dans le dossier /apps et non dans le dossier /libs.

## Exemple {#example}

**Composant de commentaires d’incrustation**

Supposons que vous souhaitiez modifier la fonction de commentaire afin qu’elle corresponde à la conception de votre site Web, en modifiant l’en-tête du commentaire afin qu’il n’affiche plus l’avatar d’un commentaire. Les solutions de masquage de l’avatar utilisent CSS ou, comme décrit ici, superposent le fichier header.jsp dans le dossier des applications afin que le code HTML contenant l’avatar ne soit jamais envoyé au client.

Pour superposer des commentaires, vous devez effectuer les opérations suivantes :

1. [Page Commentaires](/help/communities/overlay-create-comments-page.md)
1. [Création de noeuds](/help/communities/overlay-create-nodes.md)
1. [Modifier l’aspect](/help/communities/overlay-alter-appearance.md)

**Courriers électroniques de notifications d’incrustation**

Supposons que vous souhaitiez personnaliser le message des notifications par courrier électronique, vous pouvez le faire en [superposant](/help/communities/client-customize.md#overlays) les modèles dans **/libs/settings/community/templates/email/html**.

Par exemple, pour modifier les notifications par courrier électronique de mentions (pour un composant de communautés spécifique dans lequel ugc est créé), ajoutez une condition **if** pour la **mentionde verbe** dans les modèles des composants pour lesquels vous avez activé la prise en charge de **@mentions** .

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Pour modifier le modèle de notifications par courrier électronique pour @mentions dans les commentaires de blog, placez le modèle prêt à l’emploi à l’adresse suivante : `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
