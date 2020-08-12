---
title: Rich Text Editor Essentials
seo-title: Rich Text Editor Essentials
description: Présentation de la fonction Editeur de texte enrichi
seo-description: Présentation de la fonction Editeur de texte enrichi
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
translation-type: tm+mt
source-git-commit: 4b6311cbfe11a61b74f68bf5a25ad1f5faef5358
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---


# Rich Text Editor Essentials {#rich-text-editor-essentials}

## Présentation {#overview}

Un éditeur de texte enrichi (RTE) permet de saisir du texte avec des annotations.

Pour les composants Communities, bien que semblables à l’éditeur de texte [enrichi dans l’environnement](../../help/sites-authoring/rich-text-editor.md)d’auteur, elles affectent le texte saisi dans l’environnement de publication.

![éditeur de texte enrichi](assets/rich-text-editor.png)

## Activation de l’éditeur de texte enrichi {#enabling-rich-text-editor}

Les composants de communautés qui autorisent le contenu généré par l’utilisateur (UGC) peuvent être activés pour autoriser RTE. Selon que le composant a été ajouté à une page ou inclus dans une [fonction](functions.md), RTE peut être activé ou non par défaut.

Si elle n’est pas activée, il vous suffit de passer en mode [d’édition](sites-console.md#authoring-site-content)Auteur, de sélectionner le composant à modifier et de cocher la `Rich Text Editor` case.

RTE est disponible pour les composants de communautés suivants :

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Commentaires](comments.md)
* [Filélibraire](file-library.md)
* [Forum](forum.md)
* [Message](configure-messaging.md)
* [Q&amp;R](working-with-qna.md)
* [Révisions](reviews.md)

## Personnalisation {#customization}

La personnalisation de l&#39;éditeur de texte enrichi est possible car l&#39;implémentation est basée sur [CKEEditor](https://www.ckeditor.com/).

La configuration actuelle pour les composants Communautés se trouve dans le `cq.social.  scf   clientlib`, situé dans le référentiel à l’emplacement

`/libs/clientlibs/social/commons/scf/ckrte.js`

La modification de cq.social.scf clientlib n’est pas recommandée car les mises à niveau ultérieures peuvent remplacer les modifications.

### Exemple de personnalisation : Liens intégrés {#example-customization-inline-links}

Pour des raisons de sécurité, les options d’hyperlien ne sont pas incluses dans l’ensemble d’icônes de texte enrichi présenté par défaut aux membres. La possibilité de faire des erreurs est considérable lorsque les trois types sont autorisés dans l&#39;UGC.

Pour ajouter les options d’hyperlien à la barre d’outils :

* ajouter une barre d&#39;outils nommée &quot; `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* Select **[!UICONTROL Save All]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```

