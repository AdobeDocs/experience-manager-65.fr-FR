---
title: Incrustation des composants des communautés
seo-title: Incrustation des composants des communautés
description: Incrustation des composants des communautés
seo-description: Incrustation des composants des communautés
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Composants de communautés de superposition {#overlay-communities-components}

L’intention de [superposer](/help/communities/client-customize.md#overlays) un composant par défaut est de modifier l’aspect ou le comportement d’un composant globalement, pour toutes les références relatives au composant. Il repose sur la nature de sling à résoudre dans le dossier /apps avant de rechercher dans le dossier /libs . Par conséquent, le chemin d’accès au composant est identique à celui du composant par défaut, sauf qu’il se trouve dans le dossier /apps et non dans le dossier /libs .

## Exemple {#example}

**Composant des commentaires de superposition**

Supposons que vous souhaitiez modifier la fonction de commentaire afin qu’elle corresponde à la conception de votre site web, en modifiant l’en-tête du commentaire afin qu’il n’affiche plus l’avatar pour un commentaire. Les solutions pour masquer l’avatar utilisent soit CSS, soit, comme décrit ici, le recouvrement du fichier header.jsp dans le dossier des applications afin que le code HTML contenant l’avatar ne soit jamais envoyé au client.

Pour superposer des commentaires, vous devez :

1. [Page Commentaires](/help/communities/overlay-create-comments-page.md)
1. [Création de noeuds](/help/communities/overlay-create-nodes.md)
1. [Modification de l’aspect](/help/communities/overlay-alter-appearance.md)

**Incrustation d’emails de notifications**

Supposons que vous souhaitiez personnaliser le message des notifications par e-mail, vous pouvez le faire en [superposant](/help/communities/client-customize.md#overlays) les modèles à l’adresse **/libs/settings/community/templates/email/html**.

Par exemple, pour modifier les notifications par courrier électronique de mentions (pour un composant de communautés spécifique où ugc est créé), ajoutez une condition **if** pour verb **mention** dans les modèles des composants pour lesquels vous avez activé la prise en charge de **@mentions**.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Pour modifier le modèle de notification électronique pour @mention dans les commentaires de blog, placez le modèle prêt à l’emploi à l’adresse : `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
