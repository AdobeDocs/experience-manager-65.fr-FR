---
title: Texte (Markdown)
seo-title: Texte (Markdown)
description: Lors du processus de création, l’éditeur de fragments de contenu utilise la syntaxe markdown pour vous permettre d’écrire aisément du contenu.
seo-description: Lors du processus de création, l’éditeur de fragments de contenu utilise la syntaxe markdown pour vous permettre d’écrire aisément du contenu.
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 100%

---


# Texte (Markdown) {#markdown}

Lors du processus de [création](content-fragments-variations.md#authoring-your-content), l’éditeur de fragments de contenu utilise la syntaxe *markdown* pour vous permettre d’écrire aisément du contenu :

![Éditeur de balisage](/help/assets/content-fragments/assets/cfm-6420-08.png)

Vous pouvez définir :

* [Notation d’en-tête](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Paragraphes et sauts de ligne](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Liens](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Images](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Blocs de citations](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Listes](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Accent](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Blocs de code](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Échappements par barre oblique inverse](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notation d’en-tête {#heading-notation}

Pour créer un en-tête en plaçant un hashtag (#) devant le titre. Un hashtag (#) est utilisé pour un H1, deux hashtags (##) pour un H2, etc. Vous pouvez utiliser jusqu’à 6 hashtags. Par exemple :

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

Si vous le souhaitez, vous pouvez créer une balise H1 en soulignant le texte par des signes égal et créer une balise H2 en soulignant le texte par des signes moins. Par exemple :

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Paragraphes et sauts de ligne {#paragraphs-and-line-breaks}

Un paragraphe est simplement une ou plusieurs lignes de texte consécutives, séparées par une ou plusieurs lignes vierges. Une ligne vierge est une ligne ne contenant que des espaces ou des tabulations. Les paragraphes normaux ne doivent pas être mis en retrait avec des espaces ou des tabulations.

Un saut de ligne est créé en terminant une ligne par deux espaces ou plus puis un retour.

## Liens {#links}

Vous pouvez créer des liens intégrés et de référence.

Dans les deux styles, le texte du lien est délimité par des crochets `[]`.

Voici des exemples de liens intégrés :

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

Les liens de référence présentent la syntaxe suivante :

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Images {#images}

La syntaxe des images est similaire à celle des liens. Vous pouvez créer des images intégrées et référencées.

Par exemple, les images intégrées présentent la syntaxe suivante :

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

La syntaxe comprend :

* Un point d’exclamation : !;
* suivi d’un ensemble de crochets, contenant le texte d’attribut alternatif de l’image ;
* suivi d’un ensemble de parenthèses, contenant l’URL ou le chemin d’accès de l’image, et un attribut de titre facultatif inclus dans des guillemets doubles ou simples.

Les images de style de référence présentent la syntaxe suivante :

    `![Alt text][id]`

Où « id » est le nom d’une référence d’image définie. Les références d’image sont définies à l’aide d’une syntaxe identique à celle des références de lien :

    `[id]: url/to/image "Optional title attribute"`

## Blocs de citations {#block-quotes}

Vous pouvez inclure des citations en ajoutant le symbole > avant le texte. Par exemple :

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

Vous pouvez utiliser des blocs de citations imbriqués. Par exemple :

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Listes {#lists}

Vous pouvez créer des listes ordonnées et non ordonnées.

Pour créer une liste non ordonnée, insérez le symbole &amp;ast; avant les éléments de la liste. Par exemple :

    `* item in list`

    `* item in list`

    `* item in list`

Pour créer une liste ordonnée, ajoutez les chiffres, suivis d’un point, avant chaque élément de la liste. Par exemple :

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Accent {#emphasis}

Vous pouvez ajouter un style italique ou gras à votre texte.

Vous pouvez ajouter des italiques comme suit :

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Vous pouvez mettre du texte en gras comme suit :

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Pour désigner une plage de code, entourez-la de guillemets obliques (`). Contrairement à un bloc de code préformaté, une plage de code indique du code dans un paragraphe normal.

Par exemple :

    ``Use the `printf()` function.``

## Blocs de code {#code-blocks}

Les blocs de code sont généralement utilisés pour illustrer le code source. Vous pouvez créer des blocs de code en mettant le code en retrait à l’aide d’une tabulation ou d’au moins 4 espaces. Par exemple :

    `This is a normal paragraph.`

        `This is a code block.`

## Échappements par barre oblique inverse {#backslash-escapes}

Vous pouvez utiliser des caractères d’échappement par barre oblique inverse pour générer des caractères littéraux ayant une signification spéciale dans la syntaxe de formatage. Par exemple, pour entourer un mot par des astérisques littéraux (au lieu d’une balise &lt;em> HTML), vous pouvez utiliser des barres obliques inverses avant les astérisques, comme suit :

    `\\*literal asterisks\\*`

Les échappements par barre oblique inverse sont disponibles pour les caractères suivants :

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`

