---
title: Création d’un contenu accessible (conformité WCAG 2.0)
seo-title: Création d’un contenu accessible (conformité WCAG 2.0)
description: Instructions pour rendre les contenus web plus accessibles aux personnes en situation de handicap
seo-description: Instructions pour rendre les contenus web plus accessibles aux personnes en situation de handicap
uuid: e2653a46-fd55-407b-b331-8a684fbfd041
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 0aa18f7d-76a8-4c51-9e17-da50ae065fe8
docset: aem65
translation-type: tm+mt
source-git-commit: aaabef9d51e333003385709045e2249a10eb34aa

---


# Création d’un contenu accessible (conformité WCAG 2.0){#creating-accessible-content-wcag-conformance}

WCAG 2.0 regroupe un ensemble de règles et de critères de réussite qui ne se rattachent pas à une technologie particulière visant à rendre les contenus web plus accessibles aux personnes en situation de handicap.

>[!NOTE]
>
>Voir également:
>
>* Notre [guide rapide à propos de WCAG 2.0](/help/managing/qg-wcag.md) pour en savoir plus
>* [Configuration de l’Éditeur de texte enrichi pour produire du contenu accessible](/help/sites-administering/rte-accessible-content.md)
>



Les contenus sont classés selon trois niveaux de conformité : Niveau A (le plus bas), Niveau AA et Niveau AAA (le plus élevé). Brièvement, les niveaux se définissent comme suit :

* **Niveau A :** votre site atteint un niveau d’accessibilité minimum de base. Pour atteindre ce niveau, tous les critères de réussite du niveau A doivent être satisfaits.
* **** Niveau A : Il s&#39;agit d&#39;un niveau d&#39;accessibilité idéal à rechercher, dans lequel votre site atteint un niveau d&#39;accessibilité amélioré, de sorte qu&#39;il soit accessible à la plupart des personnes dans la plupart des situations utilisant la plupart des technologies. Pour atteindre ce niveau, tous les critères de réussite de niveau A et de niveau A sont satisfaits.
* **Niveau AAA :** votre site atteint un très haut niveau d’accessibilité. Pour atteindre ce niveau, tous les critères de réussite des niveaux A, AA et AAA doivent être satisfaits.

Lors de sa création, vous devez déterminer à quel niveau général votre site doit se conformer.

La section suivante présente les [règles WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) ainsi que les critères de réussite associés liés aux [niveaux de conformité](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) A et AA.

>[!NOTE]
>
>Il n’est pas possible, pour certains types de contenu, de satisfaire à tous les critères de réussite du niveau de conformité AAA ; celui-ci n’est donc pas recommandé à titre de politique générale.

>[!NOTE]
>
>Dans ce document, nous utilisons :
>
>* les noms courts des [règles WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) ;
>* la numérotation utilisée dans les [règles WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) afin de simplifier les références croisées avec le site web WCAG.
>



## Principe 1 : perceptible {#principle-perceivable}

[Principe 1 : perceptible – Les informations et les composants de l’interface utilisateur doivent être présentés aux utilisateurs sous des formes qu’ils peuvent percevoir.](https://www.w3.org/TR/WCAG20/#perceivable)

### Équivalents textuels (1.1) {#text-alternatives}

[Règle 1.1 – Les équivalents textuels : proposer des équivalents textuels à tout contenu non textuel qui pourra alors être présenté sous d’autres formes selon les besoins de l’utilisateur : grands caractères, braille, synthèse vocale, symboles ou langage simplifié.](https://www.w3.org/TR/WCAG20/#text-equiv)

### Contenu non textuel (1.1.1) {#non-text-content}

* Critère de réussite 1.1.1
* Niveau A
* Contenu non textuel : tout contenu non-textuel présenté à l’utilisateur a un équivalent textuel qui remplit une fonction équivalente sauf dans les situations énumérées ci-dessous.

#### Objectif – Contenu non textuel (1.1.1) {#purpose-non-text-content}

Le contenu d’une page web peut être proposé dans différents formats non textuels (photos, vidéos, animations, tableaux et graphiques). Les personnes aveugles ou malvoyantes ne sont pas en mesure de voir le contenu non textuel, mais elles peuvent accéder au contenu textuel en le faisant lire par un lecteur d’écran ou sous forme tactile dans un appareil d’affichage en braille. Ainsi, en proposant des équivalents textuels pour le contenu graphique, les personnes qui ne voient pas le contenu graphique peuvent accéder à une version équivalente des informations véhiculées par le contenu.

Autre avantage utile : les équivalents textuels permettent aux moteurs de recherche d’indexer le contenu non textuel.

#### Comment procéder – Contenu non textuel (1.1.1) {#how-to-meet-non-text-content}

Pour les images statiques, la règle de base consiste à fournir un équivalent textuel. Vous pouvez pour ce faire utiliser le champ **Texte de remplacement** :

>[!NOTE]
>
>Certains composants prêts à l’emploi, tels que **Carrousel** et **Diaporama** , ne permettent pas d’ajouter des descriptions de texte de remplacement aux images. Lors de l’implémentation de ces versions pour votre instance AEM, votre équipe de développement devra configurer ces composants pour prendre en charge l’ `alt` attribut afin que les auteurs puissent l’ajouter au contenu (voir [Ajout de la prise en charge d’éléments et d’attributs](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)HTML supplémentaires).

Le champ **Texte de remplacement** est disponible dans la boîte de dialogue du composant **Image** sous l’onglet **Métadonnées** :

![Boîte de dialogue de modification du composant Image dans l’interface utilisateur optimisée pour les écrans tactiles ; présente le champ Texte de remplacement.](assets/screen_shot_2018-03-21at165045.png)

Dans AEM, le champ **Texte de remplacement** doit être renseigné par défaut. Si votre image est purement décorative et que le texte de remplacement est dénué de sens, l’option **L’image est décorative** peut être sélectionnée.

#### Creating Good Text Alternatives {#creating-good-text-alternatives}

Il existe diverses formes de contenu non textuel. Par conséquent, la valeur de l’équivalent textuel dépend du rôle du graphique dans la page web. Voici quelques-unes des règles de base à respecter :

* Les équivalents textuels doivent être succincts, tout en communiquant clairement l’information essentielle du contenu non textuel.
* Il est préférable d’éviter les descriptions trop longues (plus de 100 caractères). Si un équivalent textuel doit être plus détaillé :

   * donnez une brève description dans l’équivalent textuel ;
   * proposez une description plus longue dans le texte ailleurs sur la même page ou dans une page web distincte. Renvoyez vers cette description individuelle en transformant l’image en lien ou en plaçant un lien textuel près de l’image.

* L’équivalent textuel ne doit pas répliquer le contenu fourni sous forme de texte à proximité sur la même page. N’oubliez pas que nombre d’images sont des illustrations de points déjà traités dans le texte d’une page ; un équivalent textuel détaillé existe donc peut-être déjà.
* Si le contenu non textuel est un lien vers une autre page ou un autre document et qu’il n’existe pas de texte faisant partie dudit lien, l’équivalent textuel de l’image doit indiquer la destination du lien, et non décrire l’image.
* Si le contenu non textuel est contenu dans un bouton et qu’il n’existe pas de texte faisant partie dudit bouton, l’équivalent textuel de l’image doit indiquer la fonction du bouton, et non décrire l’image.
* Il est tout à fait acceptable de donner à une image un texte de remplacement vide (nul), mais seulement si l’image n’a pas de texte de remplacement (par exemple, c’est un graphique purement décoratif) ou si le texte équivalent existe déjà dans le texte de la page.

L’ébauche du document [W3C: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) (techniques pour spécifier des équivalents textuels utiles ; en anglais) répertorie des détails et des exemples d’équivalents textuels appropriés pour différents types d’images.

Voici quelques-uns des types spécifiques de contenu non textuel auquel un équivalent textuel doit être associé :

* Illustrative photos:
These are images of people, objects or places. Think about the role of the photo in the page; an appropriate text equivalent is likely to be *Photo of[object ]*, but may be dependent on the surrounding text.
* Icônes :
Certains petits pictogrammes (images) communiquent parfois des informations spécifiques. Ils doivent être utilisés de manière uniforme sur une page et un site. Toutes les instances de l’icône sur une page ou un site doivent avoir le même équivalent textuel bref et succinct, sauf si cela duplique de manière superflue le texte adjacent.
* Charts and graphs:
These typically represent numerical data. So one option for providing a text alternative might be to include a brief summary of the main trends shown in the chart or graphic. If necessary, also provide a more detailed description in text using the **Description** field in the **Advanced** image properties tab. Additionally, you could provide the source data in tabular form elsewhere in the page or site.

   ![Exemple d’un graphique. La meilleure approche pour fournir un équivalent est présentée ci-dessous.](assets/chlimage_1.jpeg)

   Pour spécifier un équivalent textuel pour cet exemple de graphique, ajoutez un texte `alt` concis à l’image, puis un équivalent textuel complet juste après l’image.

   ```xml
   <p><img src="figure1.gif" alt="Figure 1" ></p>
   <p> Figure 1. Distribution of Articles by Journal Category.
   Pie chart: Language=68%, Education=14% and Science=18%.</p>
   ```

   >[!NOTE]
   >
   >Le fragment de code ci-dessus est uniquement utilisé pour illustrer l’ordre. Il est recommandé d’utiliser le composant **Image** (plutôt que la `img src` référence utilisée ci-dessus).

   Dans AEM, ce résultat peut être obtenu à l’aide d’une combinaison des champs **Texte de remplacement** et **Description** de la boîte de dialogue de configuration de l’image, comme dans [Compatibilité - Contenu non textuel (1.1.1)](#how-to-meet-non-text-content).

* Maps, diagrams, flowcharts:
For graphics providing spatial data (for example. to support describing relationships between objects or a process), ensure that the key message is provided in text format. For maps, providing a full text equivalent is likely to be impractical, but if the map is provided as a way of helping people find their way to a particular location, then the map image’s alternative text can briefly indicate *Map of X*, then provide directions to that location in text elsewhere in the page or through the **Description** field in the **Advanced** tab of the **Image** component.
* CAPTCHA :
L’acronyme anglais CAPTCHA (*Completely Automated Public Turing test to tell Computers and Humans Apart*) désigne un test servant à déterminer si le contenu est consulté par une personne plutôt que par un ordinateur. Ce contrôle de sécurité utilisé sur les pages web pour distinguer les humains des logiciels malveillants peut constituer un obstacle à l’accessibilité. Il s’agit d’images obligeant les utilisateurs à décrire ce qu’ils voient pour pouvoir réussir le test de sécurité. Il n’est évidemment pas possible de fournir un équivalent textuel pour l’image. Vous devez par conséquent envisager des alternatives non graphiques.
Le W3C émet plusieurs suggestions, comme celles énumérées ci-dessous. Chacune de ces approches a ses propres avantages et inconvénients.

   * Énigmes logiques
   * Utilisation d’une sortie audio plutôt que d’images
   * Comptes d’utilisateur limités et filtres de courrier indésirable

* Images d’arrière-plan : Elles sont réalisées à l’aide de feuilles de style en cascade (CSS) plutôt qu’en HTML. Cela signifie qu’il n’est pas possible de spécifier une autre valeur de texte. Par conséquent, les images d’arrière-plan ne doivent pas fournir d’informations textuelles importantes. Si tel est le cas, ces informations doivent également être fournies dans le texte de la page. Cependant, il est important qu’un autre arrière-plan s’affiche lorsque l’image ne peut pas être affichée.

   >[!NOTE]
   >
   >Le niveau de contraste entre l’arrière-plan et le texte au premier plan doit être suffisant. Ceci est décrit de manière plus détaillée à la section [Contraste (minimum) (1.4.3)](#contrast-minimum).

#### En savoir plus – Contenu non textuel (1.1.1) {#more-information-non-text-content}

* [Compréhension du critère de réussite 1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [Comment remplir le critère de réussite 1.1.1](https://www.w3.org/WAI/WCAG20/quickref/#text-equiv)
* [W3C: HTML5 Techniques for providing useful text alternatives (techniques pour spécifier des équivalents textuels utiles ; ébauche, en anglais)](https://dev.w3.org/html5/alt-techniques/)
* [Explication des CAPTCHA et alternatives par le W3C](https://www.w3.org/TR/turingtest/)

### Média temporel (1.2) {#time-based-media}

[Règle 1.2 – Média temporel : proposer des versions de remplacement aux médias temporels.](https://www.w3.org/TR/WCAG20/#text-equiv)

Cette section traite du contenu web *temporel*, notamment le contenu que l’utilisateur peut lire (contenu vidéo, audio et animé, par exemple) et qui peut être pré-enregistré ou en direct.

### Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#audio-only-and-video-only-pre-recorded}

* Critère de réussite 1.2.1
* Niveau A
* Contenu seulement audio ou vidéo (pré-enregistré) : pour des médias pré-enregistrés seulement audio et pré-enregistrés seulement vidéo, sauf si l’audio ou la vidéo est un média de remplacement pour un texte et qu’ils sont clairement identifiés comme tels, ce qui suit s’applique :

   * Contenu pré-enregistré seulement audio : fournir une version de remplacement pour un média temporel, présentant une information équivalente au contenu seulement audio.
   * Contenu pré-enregistré seulement vidéo : fournir, soit une version de remplacement pour un média temporel, soit une piste audio (présentant une information équivalente) pour un contenu pré-enregistré seulement vidéo.

#### Objectif – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#purpose-audio-only-and-video-only-pre-recorded}

Les personnes suivantes peuvent éprouver des problèmes à accéder au contenu vidéo et audio :

* Les personnes malvoyantes lorsqu’il n’y a aucune piste audio ou si la piste audio ne suffit pas à les informer de ce qui se passe dans la vidéo ou l’animation.
* Les personnes malentendantes ou sourdes, qui ne peuvent pas écouter la piste audio.
* Les personnes qui peuvent écouter la piste audio, mais qui ne la comprennent pas (si par exemple elle est dans une langue qu’elles ne comprennent pas).

Les personnes qui utilisent des navigateurs ou des périphériques qui ne prennent pas en charge la lecture du contenu dans des formats multimédias spécifiques (Adobe Flash par exemple) peuvent aussi ne pas avoir accès au contenu vidéo ou audio.

En proposant ces informations dans un autre format (texte par exemple, ou audio pour un contenu vidéo sans audio), elles seront accessibles par les personnes qui ne sont pas en mesure d’accéder au contenu original.

#### Comment procéder – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#how-to-meet-audio-only-and-video-only-pre-recorded}

* Si le contenu est un contenu audio pré-enregistré sans vidéo (podcast par exemple) :

   * Fournissez un lien immédiatement avant ou après le contenu vers une transcription textuelle du contenu audio.
La transcription doit être une page HTML avec un équivalent textuel de tout le contenu non parlé important et parlé, et indiquer en outre qui parle, avec les expressions vocales et une description du décor et de tout autre contenu audio significatif.

* Si le contenu est une animation ou une vidéo pré-enregistrée sans audio :

   * Fournissez un lien immédiatement avant ou après le contenu vers une description textuelle équivalente des informations communiquées par la vidéo.
   * Ou fournissez une audio-description équivalente dans un format audio fréquemment utilisé (MP3 par exemple).

>[!NOTE]
>
>Si le contenu audio ou vidéo est fourni comme alternative au contenu qui existe déjà dans un autre format sur une page web, il n’est pas nécessaire d’adhérer aux exigences ci-dessus. Si, par exemple, une vidéo illustre une liste d’instructions textuelles, il n’est pas nécessaire d’ajouter un équivalent puisque les instructions textuelles agissent comme équivalent de la vidéo.

L’ajout de contenu multimédia (Flash notamment) dans vos pages web AEM revient à ajouter une image. Toutefois, puisque le contenu multimédia représente bien davantage qu’une image fixe, il existe différents paramètres et options pour contrôler la lecture du multimédia.

>[!NOTE]
>
>Lorsque vous utilisez du contenu multimédia avec du contenu informatif, vous devez également créer des liens vers des alternatives. Par exemple, pour inclure une transcription de texte, créez une page HTML pour afficher la transcription, puis ajoutez un lien en regard ou en dessous du contenu audio.

#### En savoir plus – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#more-information-audio-only-and-video-only-pre-recorded}

* [Compréhension du critère de réussite 1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [Comment remplir le critère de réussite 1.2.1](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)

### Sous-titres (pré-enregistrés) (1.2.2) {#captions-pre-recorded}

* Critère de réussite 1.2.2
* Niveau A
* Sous-titres (pré-enregistrés) : fournir des sous-titres pour tout contenu audio pré-enregistré dans un média synchronisé, excepté lorsque le média est un média de remplacement pour un texte et qu’il est clairement identifié comme tel.

#### Objectif – Sous-titres (pré-enregistrés) (1.2.2) {#purpose-captions-pre-recorded}

Les personnes sourdes ou malentendantes n’auront pas accès au contenu audio, ou y auront accès avec de grandes difficultés. Les sous-titres sont des équivalents textuels au contenu audio parlé et non parlé ; ils s’affichent à l’écran au moment approprié durant la vidéo. Ils permettent aux personnes qui ne peuvent pas écouter le contenu audio de comprendre ce qui se passe.

>[!NOTE]
>
>Les sous-titres ne sont pas obligatoires s’il existe déjà des équivalents textuels ou non textuels adaptés (qui fournissent directement des informations équivalentes) sur la même page que la vidéo ou l’animation.

#### Comment procéder – Sous-titres (pré-enregistrés) (1.2.2) {#how-to-meet-captions-pre-recorded}

Les sous-titres peuvent être :

* Intégrés : toujours visibles pendant la lecture de la vidéo.
* Fermé :* *les légendes peuvent être activées ou désactivées par l’utilisateur.

Ajoutez des sous-titres non intégrés chaque fois que cela est possible, car les utilisateurs peuvent ainsi décider s’ils souhaitent les afficher.

Pour les sous-titres non intégrés, vous devez créer et fournir un fichier de sous-titrage synchronisé dans un format approprié ([SMIL](https://www.w3.org/AudioVideo/) par exemple) avec le fichier vidéo (la procédure à suivre pour ce faire ne fait pas l’objet de ce guide, mais vous trouverez des liens vers des didacticiels sous [En savoir plus – Sous-titres (pré-enregistrés) (1.2.2)](#more-information-captions-pre-recorded)). Pensez à inclure une note avisant les utilisateurs que des sous-titres sont disponibles pour la vidéo.

Si vous devez utiliser des sous-titres intégrés, incorporez le texte à la piste vidéo. Pour ce faire, utilisez des applications de montage vidéo qui permettent de superposer du texte sur la vidéo.

#### En savoir plus – Sous-titres (pré-enregistrés) (1.2.2) {#more-information-captions-pre-recorded}

* [Compréhension du critère de réussite 1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) :
* [Comment remplir le critère de réussite 1.2.2](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)
* [W3C: Synchronized Multimedia (Multimédia synchronisé ; en anglais)](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions (Sous-titres, transcriptions et descriptions audio), par webAIM (en anglais)](https://webaim.org/techniques/captions/)

### Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#audio-description-or-media-alternative-pre-recorded}

* Critère de réussite 1.2.3
* Niveau A
* Audio-description ou version de remplacement pour un média temporel (pré-enregistré) : fournir une version de remplacement pour un média temporel ou une audio-description du contenu vidéo pré-enregistré pour un média synchronisé, excepté quand le média est un média de remplacement pour un texte et qu’il est clairement identifié comme tel.

#### Objectif – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#purpose-audio-description-or-media-alternative-pre-recorded}

Les personnes aveugles ou malvoyantes ne pourront pas accéder au contenu si les informations dans une vidéo ou une animation sont fournies sous forme visuelle seulement ou si la piste audio ne fournit pas suffisamment d’informations pour comprendre ce qui se passe visuellement.

#### Comment procéder – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-pre-recorded}

Deux approches peuvent être adoptées pour remplir ce critère de réussite. Les deux sont acceptables :

1. Inclure une audio-description supplémentaire pour le contenu vidéo. Vous pouvez y parvenir de trois façons :

   * Durant les pauses dans le dialogue existant, fournissez des informations sur les modifications dans la scène qui ne sont pas présentées dans la piste audio existante.
   * Fournissez une nouvelle piste audio supplémentaire et facultative contenant la piste audio originale, mais aussi des informations audio supplémentaires sur les modifications dans la scène.

      * Les utilisateurs peuvent ainsi permuter entre la piste audio existante (qui ne contient *pas* d’audio-description) et la nouvelle piste audio (qui *comprend* une audio-description).

      * De cette façon, les utilisateurs qui n’ont pas besoin de la description supplémentaire ne sont pas interrompus.
   * Créez une deuxième version du contenu vidéo afin d’y inclure des audio-descriptions plus détaillées. Ceci réduit les difficultés associées à la spécification d’audio-descriptions détaillées dans les intervalles au sein du dialogue existant, en interrompant temporairement l’audio et la vidéo à des points appropriés. Vous pouvez ainsi ajouter une audio-description beaucoup plus longue avant que l’action ne recommence. Comme dans l’exemple précédent, il est préférable de proposer une piste audio supplémentaire facultative afin d’éviter toute interruption pour les utilisateurs qui n’ont pas besoin du contenu supplémentaire.


1. Fournissez une transcription textuelle qui est un équivalent textuel adapté des éléments audio et visuels de la vidéo ou de l’animation. Il peut s’agir, si cela est approprié, d’une indication précisant qui parle, d’une description du décor ou d’expressions vocales. Selon sa durée, vous pouvez placer la transcription sur la même page que la vidéo ou animation, ou sur une autre page ; dans le deuxième cas, fournissez un lien vers la transcription près de la vidéo ou de l’animation.

Les détails exacts de la création de vidéos décrites en audio ne sont pas compris dans ce guide. La création de descriptions vidéo et audio peut prendre du temps, mais d’autres produits Adobe peuvent vous aider à accomplir ces tâches. Si vous créez du contenu dans Adobe Flash Professional, vous devez également créer un script pour inviter l’utilisateur à télécharger le module externe approprié et fournir une alternative de texte via l’ `<noscript>` élément.

#### En savoir plus – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#more-information-audio-description-or-media-alternative-pre-recorded}

* [Compréhension du critère de réussite 1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) :
* [Comment remplir le critère de réussite 1.2.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://www.adobe.com/products/premiere/encore/)

### Sous-titres (en direct) (1.2.4)  {#captions-live}

* Critère de réussite 1.2.4
* Niveau AA
* Sous-titres (en direct) : fournir des sous-titres pour tout contenu audio en direct, sous forme de média synchronisé.

#### Objectif – Sous-titres (en direct) (1.2.4) {#purpose-captions-live}

This success criterion is identical to [Captions (Pre-Recorded)](#captionsprerecorded) in that it addresses accessibility barriers experienced by people who are deaf or hearing-impaired, except that this success criterion deals with live presentations such as webcasts.

#### Comment procéder – Sous-titres (en direct) (1.2.4) {#how-to-meet-captions-live}

Follow the guidance provided for [Captions (Pre-Recorded)](#captionsprerecorded) above. However, due to the live nature of the media, caption provision has to be created as quickly as possible and in response to what is happening. Therefore, you should consider using real time captioning or speech-to-text tools.

Ce document ne vise pas à fournir des instructions détaillées à ce sujet, mais vous trouverez des renseignements utiles en suivant les liens ci-après :

* [webAIM : Real Time Captioning (sous-titrage en temps réel ; en anglais)](https://www.webaim.org/techniques/captions/realtime.php)
* [AccessIT (University of Washington) : Est-il possible de générer des sous-titres automatiquement à l’aide de la reconnaissance vocale ?](https://www.washington.edu/accessit/articles?1209)

#### En savoir plus – Sous-titres (en direct) (1.2.4) {#more-information-captions-live}

* [Compréhension du critère de réussite 1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [Comment remplir le critère de réussite 1.2.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-real-time-captions)

### Audio-description (pré-enregistrée) (1.2.5)  {#audio-description-pre-recorded}

* Critère de réussite 1.2.5
* Niveau AA
* Audio-description (pré-enregistrée) : fournir une audio-description pour tout contenu vidéo pré-enregistré, sous forme de média synchronisé.

#### Objectif – Audio-description (pré-enregistrée) (1.2.5) {#purpose-audio-description-pre-recorded}

Ce critère de réussite est identique au critère [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audiodescriptionormediaalternativeprerecorded), excepté que les auteurs doivent fournir une audio-description beaucoup plus détaillée, conforme au niveau AA.

#### Comment procéder – Audio-description (pré-enregistrée) (1.2.5) {#how-to-meet-audio-description-pre-recorded}

Suivez les instructions de la section [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audiodescriptionormediaalternativeprerecorded).

#### En savoir plus – Audio-description (pré-enregistrée) (1.2.5) {#more-information-audio-description-pre-recorded}

* [Compréhension du critère de réussite 1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [Comment remplir le critère de réussite 1.2.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc-only)

### Adaptable (1.3) {#adaptable}

[Règle 1.3 – Adaptable : créer un contenu qui puisse être présenté de différentes manières sans perte d’information ni de structure (par exemple avec une mise en page simplifiée).](https://www.w3.org/TR/WCAG20/#content-structure-separation)

Cette règle couvre les exigences nécessaires pour aider les personnes qui :

* peut ne pas être en mesure d&#39;accéder aux informations présentées par un auteur dans une mise en page de page Web en deux dimensions, en plusieurs colonnes et en couleur *standard

* utilisent peut-être un contenu audio uniquement ou un affichage visuel de remplacement, par exemple un contraste élevé ou une grande taille de texte.

### Informations et relations (1.3.1)  {#info-and-relationships}

* Critère de réussite 1.3.1
* Niveau A
* Informations et relations : l’information, la structure et les relations véhiculées par la présentation peuvent être déterminées par un programme informatique ou sont disponibles sous forme de texte.

#### Objectif – Informations et relations (1.3.1) {#purpose-info-and-relationships}

Nombre des technologies d’assistance auxquelles ont recours les personnes en situation de handicap ont recours à des informations structurelles pour afficher ou restituer efficacement le contenu. Ces informations structurelles peuvent se présenter sous forme de titres de page, de titres de lignes et de colonnes de tableau et de types de liste. Par exemple, un utilisateur peut recourir à un lecteur d’écran pour parcourir une page d’un titre à un autre. Si, toutefois, le contenu d’une page semble avoir une structure de style visuel uniquement, plutôt qu’un code HTML sous-jacent, aucune information structurelle n’est disponible pour les technologies d’assistance, ce qui limite leur capacité à faciliter la navigation.

Ce critère de réussite vise à garantir que de telles informations structurelles sont fournies dans le code HTML, de sorte que les navigateurs et les technologies d’assistance puissent accéder à l’information et l’exploiter.

#### Comment procéder – Informations et relations (1.3.1) {#how-to-meet-info-and-relationships}

AEM facilite la construction de pages web à l’aide des éléments HTML appropriés. Ouvrez le contenu de la page dans l’éditeur de texte enrichi (un composant Texte) et, à l’aide du menu **Paraformat** (symbole du paragraphe), spécifiez l’élément structurel approprié (paragraphe, en-tête, etc.).

L’image suivante présente du texte stylisé comme texte de paragraphe.

![Exemple de l’élément Paragraphe affiché en mode d’édition de la source (IU classique).](assets/screen_shot_2018-03-21at165623.png)

Veillez à ce que vos pages web aient la structure appropriée comme suit :

* **Utilisation de titres :**

   As long as you have the accessibility features of the RTE enabled (see [AEM and Accessibility](#adobeexperiencemanagerandaccessibility)), AEM offers 3 levels of page heading. You can use these to identify sections and subsections of content. Heading 1 is the highest level of heading, Heading 3 the lowest. The system administrator can configure the system to allow the use of more heading levels.

   L’image suivante illustre un exemple des différents types de titres.

   ![Titres 1 à 3 affichés dans le sélecteur déroulant (IU classique).](assets/screen_shot_2018-03-21at165719.png)

* **Texte mis en évidence** :

   Mettez le texte en évidence à l’aide des éléments &lt;strong> ou &lt;em>. N’utilisez pas de titres au sein des paragraphes.

   * Surlignez le texte à mettre en évidence.
   * Click on the **B** icon (for &lt;strong>) or the **I** icon (for &lt;em>) shown within the **Properties** panel (make sure that HTML is selected).
   >[!NOTE]
   >
   >Dans une installation AEM standard, l’éditeur de texte enrichi est configuré pour utiliser :
   >
   >    * &lt;b> au lieu de &lt;strong>
   * &lt;i> au lieu de &lt;em>
   Même s’ils sont en réalité identiques, &lt;strong> et &lt;em> sont préférables car ils constituent un code html sémantiquement correct. Votre équipe de développement peut configurer l’éditeur de texte enrichi pour utiliser &lt;strong> et &lt;em> (au lieu de &lt;b> et &lt;i>) lors de l’élaboration de votre instance de projet.

* **Listes** : vous pouvez spécifier trois différents types de listes en HTML :

   * L’ `<ul>` élément est utilisé pour les listes *non triées* (à puces). Les éléments de liste individuels sont identifiés à l’aide de l’ `<li>` élément.
Dans l’éditeur de texte enrichi, cliquez sur l’icône **Liste à puces**.

   * L’ `<ol>` élément est utilisé pour les listes *numérotées* *. *Les éléments de liste individuels sont identifiés à l’aide de l’ `<li>` élément.
In the RTE, use the **Numbered List** icon.
   Pour modifier un contenu existant en un type de liste particulier, sélectionnez-le, puis choisissez le type de liste approprié. Comme dans l’exemple précédent illustrant la saisie du texte du paragraphe, les éléments de liste appropriés sont automatiquement ajoutés au fichier HTML.

   En mode plein écran, les icônes **Liste de puces** et **Liste numérotée** sont visibles. Lorsqu’un autre mode est activé, les deux options sont regroupées derrière l’icône **Listes**.

   ![](do-not-localize/screen_shot_2018-03-21at165756.png)

   >[!NOTE]
   `<dl>` n’est pas pris en charge par l’éditeur de texte enrichi.

* **Tableaux** :

   Les tableaux de données doivent être identifiés à l’aide des éléments de tableau HTML :

   * one `<table>` element
   * a `<tr>` element for each row of the table
   * a `<th>` element for each row and column heading
   * a `<td>` element for every data cell
   >[!NOTE]
   Dans l’IU classique, les tables doivent être réalisées avec le composant **Table.**

   En outre, les tableaux accessibles utilisent les éléments et attributs suivants :

   * L’ `<caption>` élément sert à fournir une légende visible pour le tableau. Les légendes apparaissent par défaut centrées au-dessus du tableau, mais peuvent être positionnées de manière appropriée à l’aide de CSS. La légende est associée au tableau par programmation, ce qui en fait une méthode utile pour fournir une introduction au contenu.
   * L’ `<summary>` élément aide les utilisateurs non voyants à comprendre plus facilement les informations présentées dans un tableau, en fournissant une synthèse de ce qu’un utilisateur voyant peut voir. Cela s’avère particulièrement utile lorsque des dispositions de tableau complexes ou non conventionnelles sont utilisées (cet attribut n’est pas affiché dans le navigateur, il est uniquement lu pour les technologies d’assistance).
   * L’ `scope` attribut de l’ `<th>` élément sert à indiquer si une cellule représente un en-tête pour une rangée particulière ou pour une colonne particulière. Une approche similaire consiste à utiliser les attributs d’en-tête et d’ID dans des tableaux complexes, où les cellules de données peuvent être associées à un ou plusieurs en-têtes.
   >[!NOTE]
   By default, these elements and attributes are not directly available, though it is possible for the system administrator to add support for these values in the **Table properties** dialog box (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

   Lorsque vous ajoutez un **Tableau**, vous pouvez configurer ses propriétés dans la boîte de dialogue **Propriétés du tableau** :

   ![cac-02](assets/cac-02.png)

   Pour ouvrir la boîte de dialogue **Tableau** dans laquelle vous pouvez sélectionner l’onglet **Propriétés** du tableau :

   * Définissez une **légende** appropriée.
   * Idéalement, supprimez les valeurs par défaut des propriétés **Largeur**, **Hauteur**, **Bordure**, **Marge intérieure des cellules** et **Espacement des cellules** car ces propriétés peuvent être définies dans une feuille de style globale.
   ![cac-01](assets/cac-01.png)

   Vous pouvez ensuite utiliser les **propriétés de cellule** pour définir si la cellule est une cellule de données ou d’en-tête :

   ![cac-03](assets/cac-03.png)

* **Tableaux** de données complexes :

   In some cases, where there are complex tables with two or more levels of headers, then the basic Table Properties may not be enough to provide all the structural information necessary. For these kinds of complex tables, direct relationships need to be created between the headers and their related cells using the **header** and **id** attributes. For example, in the table below headers and ids are matched to make a programmatic association for assistive technology users.

   >[!NOTE]
   L’attribut id n’est pas disponible dans une installation prête à l’emploi. Il peut être activé en configurant les règles HTML et le sérialiseur dans l’éditeur de texte enrichi.

   >[!NOTE]
   Dans l’IU classique, les tables doivent être réalisées avec le composant **Table.**

   ```xml
   <table>
      <tr>
        <th rowspan="2" id="h">Homework</th>
        <th colspan="3" id="e">Exams</th>
        <th colspan="3" id="p">Projects</th>
      </tr>
      <tr>
        <th id="e1" headers="e">1</th>
        <th id="e2" headers="e">2</th>
        <th id="ef" headers="e">Final</th>
        <th id="p1" headers="p">1</th>
        <th id="p2" headers="p">2</th>
        <th id="pf" headers="p">Final</th>
      </tr>
      <tr>
       <td headers="h">15%</td>
       <td headers="e e1">15%</td>
       <td headers="e e2">15%</td>
       <td headers="e ef">20%</td>
       <td headers="p p1">10%</td>
       <td headers="p p2">10%</td>
       <td headers="p pf">15%</td>
      </tr>
     </table>
   ```

   Pour y parvenir dans AEM, vous devez ajouter la balise directement en mode d’édition de la source.

   >[!NOTE]
   Cette fonctionnalité n’est pas immédiatement disponible dans une installation standard. Vous devez configurer les règles HTML et le sérialiseur dans l’éditeur de texte enrichi.

#### En savoir plus – Informations et relations (1.3.1) {#more-information-info-and-relationships}

* [Compréhension du critère de réussite 1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [Comment remplir le critère de réussite 1.3.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-programmatic)

### Caractéristiques sensorielles (1.3.3)  {#sensory-characteristics}

* Critère de réussite 1.3.3
* Niveau A
* Caractéristiques sensorielles : les instructions données pour la compréhension et l’utilisation du contenu ne doivent pas reposer uniquement sur les caractéristiques sensorielles des éléments comme la forme, la taille, l’emplacement visuel, l’orientation ou le son.

#### Objectif – Caractéristiques sensorielles (1.3.3) {#purpose-sensory-characteristics}

Les concepteurs concentrent généralement leurs efforts sur le côté visuel (couleur, forme, style du texte ou position absolue ou relative d’un élément du contenu) de la présentation des informations. Même s’il peut s’agir de techniques de conception très efficaces pour véhiculer l’information, les personnes aveugles ou malvoyantes peuvent ne pas être en mesure d’accéder à l’information nécessitant une identification visuelle des attributs (position, couleur ou forme, par exemple).

De même, les informations qui impliquent de distinguer différents sons (contenu verbalisé par un homme ou une femme, par exemple) présentent un obstacle à l’accessibilité pour les personnes malentendantes si elles ne sont pas reproduites dans un équivalent textuel du contenu audio.

>[!NOTE]
Pour connaître les conditions requises en rapport avec les alternatives aux couleurs, voir [Utilisation de la couleur](#use-of-color).

#### Comment procéder – Caractéristiques sensorielles (1.3.3) {#how-to-meet-sensory-characteristics}

Veillez à ce que les informations qui reposent sur des caractéristiques visuelles du contenu de la page soient également présentées dans un autre format.

* Ne vous fiez pas à la seule position visuelle pour transmettre une information. Si, par exemple, vous souhaitez renvoyer les utilisateurs à un menu sur le côté droit de la page pour accéder à d’autres informations, ne renvoyez pas au *menu à droite* ; nommez plutôt le menu (par exemple au moyen d’un titre) et faites référence à ce nom dans le texte.
* Ne vous fiez pas au style de texte (gras ou italique par exemple) comme seul moyen de transmettre l’information.

>[!NOTE]
L’utilisation de termes descriptifs est acceptable s’ils ont une signification dans un contexte non visuel. Par exemple, les termes *ci-dessus* et *ci-dessous* sont généralement acceptables, puisqu’ils impliquent respectivement le contenu juste avant ou après un élément de contenu particulier ; ils resteront donc significatifs si le contenu est lu à haute voix.

#### En savoir plus – Caractéristiques sensorielles (1.3.3) {#more-information-sensory-characteristics}

* [Compréhension du critère de réussite 1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [Comment remplir le critère de réussite 1.3.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-understanding)

### Distinguable (1.4) {#distinguishable}

[Règle 1.4 – Distinguable : faciliter la perception visuelle et auditive du contenu par l’utilisateur, notamment en séparant le premier plan de l’arrière-plan.](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### Utilisation de la couleur (1.4.1)  {#use-of-color}

* Critère de réussite 1.4.1
* Niveau A
* Utilisation de la couleur : la couleur n’est pas utilisée comme la seule façon de véhiculer de l’information, d’indiquer une action, de solliciter une réponse ou de distinguer un élément visuel.

>[!NOTE]
Ce critère de réussite traite spécifiquement de la perception des couleurs. Les autres formes de perception sont traitées à la règle [Adaptable (1.3)](#adaptable), comme l’accès à la couleur par programme informatique et les autres formes de codage de la présentation visuelle.

#### Objectif – Utilisation de la couleur (1.4.1) {#purpose-use-of-color}

La couleur est un moyen évidemment efficace d’améliorer l’aspect esthétique des pages web ; elle est également utile pour véhiculer l’information. Toutefois, en raison de différentes déficiences visuelles (de la cécité au daltonisme), certaines personnes ne sont pas capables de distinguer certaines couleurs. Par conséquent, le codage en couleurs ne constitue pas un moyen fiable de véhiculer l’information.

Par exemple, une personne qui ne distingue pas le vert du rouge ne sera pas en mesure de distinguer différentes nuances de ces couleurs. Si elle voit ces couleurs comme une troisième couleur (marron par exemple), elle ne sera pas non plus en mesure de distinguer le rouge du vert et du marron.

En outre, les personnes qui utilisent des navigateurs qui ne reconnaissent que le texte, des périphériques d’affichage monochromes ou un imprimé en noir et blanc de la page ne verront pas les couleurs.

#### Comment procéder – Utilisation de la couleur (1.4.1) {#how-to-meet-use-of-color}

Si la couleur sert à véhiculer l’information, veillez à ce que cette information soit accessible sans recourir à la couleur.

Par exemple, veillez à ce que l’information véhiculée par la couleur le soit aussi explicitement dans le texte. L’illustration ci-dessous présente de quelle façon le texte et la couleur identifient les sièges vacants à un spectacle :

<table>
 <tbody>
  <tr>
   <td><p><strong>Performance</strong></p> </td>
   <td><p><strong>Disponibilité</strong></p> </td>
  </tr>
  <tr>
   <td><p>Mardi 16<sup></sup> mars</p> </td>
   <td><p>SIÈGES VACANTS</p> </td>
  </tr>
  <tr>
   <td><p>Mercredi 17 mars</p> </td>
   <td><p>SIÈGES VACANTS</p> </td>
  </tr>
  <tr>
   <td><p>Jeudi 18<sup></sup> mars</p> </td>
   <td><p>COMPLET</p> </td>
  </tr>
 </tbody>
</table>

Si la couleur sert de repère pour fournir l’information, ajoutez un repère visuel supplémentaire, notamment en changeant le style (gras ou italique, par exemple) ou la police. Les personnes malvoyantes ou ayant une déficience visuelle seront ainsi en mesure d’identifier l’information. Toutefois, cette méthode seule ne suffit pas, car elle n’est d’aucune utilité pour les personnes qui ne voient pas du tout la page.

#### En savoir plus – Utilisation de la couleur (1.4.1) {#more-information-use-of-color}

* [Compréhension du critère de réussite 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Comment remplir le critère de réussite 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Conseils pour obtenir un rapport de contraste de 3:1, avec une liste de couleurs adaptées au web](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### Contraste (minimum) (1.4.3) {#contrast-minimum}

* Critère de réussite 1.4.3
* Niveau AA
* Contraste (minimum) : la présentation visuelle du texte et du texte sous forme d’image a un rapport de contraste d’au moins 4,5:1, sauf dans les cas suivants :

   * Texte agrandi : le texte agrandi et le texte agrandi sous forme d’image ont un rapport de contraste d’au moins 3:1.
   * Texte décoratif : aucune exigence de contraste pour le texte ou le texte sous forme d’image qui fait partie d’un composant d’interface utilisateur inactif, qui est purement décoratif, qui est invisible pour tous ou qui est une partie d’une image contenant un autre contenu significatif.
   * Logotypes : aucune exigence de contraste pour le texte faisant partie d’un logo ou d’un nom de marque.

#### Objectif – Contraste (minimum) (1.4.3) {#purpose-contrast-minimum}

Les personnes avec certaines déficiences visuelles peuvent ne pas être en mesure de distinguer certaines paires de couleurs à faible contraste. Elles peuvent être confrontées à des obstacles à l’accessibilité si :

* Le texte est faiblement contrasté avec sa couleur d’arrière-plan.
* Le codage en couleurs du texte (par exemple entre le texte du lien et le texte en dehors du lien) joue un rôle pour distinguer l’information.

>[!NOTE]
Le texte simplement décoratif est exclu de ce critère de réussite.

#### Comment procéder – Contraste (minimum) (1.4.3) {#how-to-meet-contrast-minimum}

Veillez à ce que le texte soit suffisamment contrasté par rapport à son arrière-plan. Les rapports de contraste dépendent de la taille et du style du texte en question :

* Pour le texte de moins de 18 points (ou 14 points en gras), le rapport de contraste entre le texte et les images de texte et l’arrière-plan doit être d’au moins 4,5:1.
* Pour le texte de 18 points (ou 14 points en gras) au moins, le rapport de contraste doit être d’au moins 3:1.
* Si un arrière-plan a un motif, l’arrière-plan autour du texte doit être ombré, de sorte que le rapport de 4,5:1 ou 3:1 soit préservé.

Pour vérifier les rapports de contraste, utilisez un outil de contraste des couleurs, tel que l’[analyseur de contraste des couleurs du groupe Paciello](https://www.paciellogroup.com/resources/contrast-analyser.html) ou l’[outil de vérification du contraste des couleurs de webAIM](https://www.webaim.org/resources/contrastchecker/), afin de vérifier les paires de couleurs et de signaler les éventuels problèmes de contraste.

Par ailleurs, si l’aspect de votre page n’est pas un souci majeur, vous avez la possibilité de ne spécifier aucune couleur de texte de premier plan ou d’arrière-plan. Dans ce cas, il n’est pas nécessaire de vérifier le contraste, puisque le navigateur de l’utilisateur déterminera les couleurs du texte et de l’arrière-plan.

S’il n’est pas possible d’obtenir les niveaux de contraste recommandés, vous devez fournir un lien vers une version équivalente alternative de la page (qui ne présente aucun problème de contraste des couleurs) ou permettre à l’utilisateur de régler le contraste du jeu de couleurs de la page selon ses besoins.

#### En savoir plus – Contraste (minimum) (1.4.3) {#more-information-contrast-minimum}

* [Compréhension du critère de réussite 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [Comment remplir le critère de réussite 1.4.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-contrast)

### Texte sous forme d’image (1.4.5) {#images-of-text}

* Critère de réussite 1.4.5
* Niveau AA
* Texte sous forme d’image : si les technologies utilisées peuvent réaliser la présentation visuelle, du texte est utilisé pour véhiculer l’information plutôt que du texte sous forme d’image sauf dans les cas suivants :

   * Personnalisable : le texte sous forme d’image peut être personnalisé visuellement selon les exigences de l’utilisateur.
   * Essentielle : une présentation spécifique du texte est essentielle à l’information véhiculée.

>[!NOTE]
Les logotypes (le texte qui fait partie d’un logo ou d’un nom de marque) sont considérés comme essentiels.

#### Objectif – Texte sous forme d’image (1.4.5) {#purpose-images-of-text}

Le texte sous forme d’image est souvent utilisé lorsqu’un style particulier de texte est nécessaire, tel un logotype ou si le texte a été généré à partir d’une autre source (par exemple la copie numérisée d’un document papier). Toutefois, par rapport au texte présenté en code HTML ou stylisé à l’aide d’une feuille de style CSS, il n’est pas possible de modifier la taille ou l’aspect du texte sous forme d’image, ce qui peut être nécessaire pour les personnes malvoyantes ou ayant des difficultés de lecture.

#### Comment procéder – Texte sous forme d’image (1.4.5) {#how-to-meet-images-of-text}

Si vous devez utiliser du texte sous forme d’image, utilisez une feuille de style CSS pour remplacer le texte sous forme d’image par un équivalent textuel HTML, de sorte que le texte puisse être personnalisé. Pour en savoir plus à ce sujet, voir [C30: Using CSS to replace text with images of text and providing user interface controls to switch](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30) (Utilisation d’une feuille de style CSS pour remplacer du texte par du texte sous forme d’image et fournir des commandes d’interface utilisateur à permuter ; en anglais).

#### En savoir plus – Texte sous forme d’image (1.4.5) {#more-information-images-of-text}

* [Compréhension du critère de réussite 1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [Comment remplir le critère de réussite 1.4.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-text-presentation)

## Principe 2 : utilisable {#principle-operable}

[Principe 2 : utilisable – Les composants de l’interface utilisateur et de navigation doivent être utilisables.](https://www.w3.org/TR/WCAG20/#operable)

### Mettre en pause, arrêter, masquer (2.2.2)  {#pause-stop-hide}

* Critère de réussite 2.2.2
* Niveau A
* Mettre en pause, arrêter, masquer : pour toute information en mouvement, clignotante, défilante ou mise à jour automatiquement, tous les points suivants sont vrais : 

   * déplacement, clignotement, défilement : pour toute information en mouvement, clignotante ou défilante qui (a) démarre automatiquement, (b) dure plus de cinq secondes et (c) est présentée conjointement avec un autre contenu, il y a un mécanisme à la disposition de l’utilisateur pour la mettre en pause, l’arrêter ou la masquer, à moins que le mouvement, le clignotement ou le défilement s’avère un élément essentiel au bon déroulement de l’activité ; et
   * mise à jour automatique : pour toute information mise à jour automatiquement qui (a) démarre automatiquement et (b) est présentée conjointement avec un autre contenu, il y a un mécanisme à la disposition de l’utilisateur pour la mettre en pause, l’arrêter ou pour en contrôler la fréquence des mises à jour à moins que la mise à jour automatique s’avère essentielle au bon déroulement de l’activité.

Remarques :

1. Pour les exigences relatives au contenu scintillant ou flashant, se référer à la règle [Ne pas concevoir de contenu susceptible de provoquer des crises (2.3)](#donotdesigncontentinawaythatisknowntocauseseizures23).
1. Puisque tout contenu ne satisfaisant pas à ce critère de réussite peut interférer avec la capacité de l’utilisateur à exploiter la page entière, tout le contenu présent dans la page web (qu’il soit utilisé pour satisfaire à d’autres critères de réussite ou non) doit satisfaire à ce critère de réussite. Voir [Exigence de conformité 5 : Non-interférence](https://www.w3.org/TR/WCAG20/#cc5).
1. Il n’est pas exigé que le contenu mis à jour périodiquement par logiciel ou diffusé en flux à l’agent utilisateur conserve ou présente l’information générée ou reçue entre la mise en pause et la reprise de la présentation, puisque cela peut ne pas être techniquement possible et s’avérer trompeur dans beaucoup de situations.
1. Une animation survenant dans une phase de pré-chargement ou dans une situation similaire peut être considérée comme essentielle si aucune interaction n’est permise à tous les utilisateurs durant cette phase et si l’absence d’indication de progression est susceptible de perturber les utilisateurs ou de leur faire croire que le contenu est figé ou défectueux.

#### Objectif – Mettre en pause, arrêter, masquer (2.2.2) {#purpose-pause-stop-hide}

Certains utilisateurs peuvent être distraits par le contenu en mouvement et avoir du mal à se concentrer sur d’autres parties de la page. En outre, un tel contenu peut s’avérer difficile à lire par les personnes qui ont du mal à suivre le texte en mouvement.

#### Comment procéder – Mettre en pause, arrêter, masquer (2.2.2) {#how-to-meet-pause-stop-hide}

Selon la nature du contenu, appliquez une ou plusieurs des suggestions ci-après lorsque vous créez des pages web qui contiennent du mouvement, flashant ou clignotant :

* Fournissez un moyen de mettre en pause le contenu défilant afin que l’utilisateur dispose de suffisamment de temps pour le lire. Par exemple, des téléscripteurs de nouvelles ou du texte automatiquement mis à jour.
* Veillez à ce que le contenu qui clignote s’arrête de clignoter après cinq secondes.
* Utilisez des technologies appropriées pour afficher le contenu clignotant pouvant être désactivé par le navigateur. Par exemple, des fichiers GIF (Graphics Interchange Format) ou APNG (Animated Portable Network Graphics).
* Fournissez un contrôle de formulaire sur la page web permettant à l’utilisateur de désactiver tout le contenu clignotant sur la page.
* Si aucune des solutions ci-dessus n’est possible, fournissez un lien vers une page avec tout le contenu mais sans aucun clignotement.

#### En savoir plus – Mettre en pause, arrêter, masquer (2.2.2) {#more-information-pause-stop-hide}

* [Compréhension du critère de réussite 2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [Comment remplir le critère de réussite 2.2.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-time-limits-pause)

### Crises (2.3) {#seizures}

[Règle 2.3 – Crises : ne pas concevoir de contenu susceptible de provoquer des crises.](https://www.w3.org/TR/WCAG20/#seizure)

### Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#three-flashes-or-below-threshold}

* Critère de réussite 2.3.1
* Niveau A
* Pas plus de trois flashs ou sous le seuil critique (2.3.1) : une page web doit être exempte de tout élément qui flashe plus de trois fois dans n’importe quel intervalle d’une seconde ou ce flash doit se situer sous le seuil de flash générique et le seuil de flash rouge.

>[!NOTE]
Puisque tout contenu ne satisfaisant pas à ce critère de réussite peut interférer avec la capacité de l’utilisateur à exploiter la page entière, tout le contenu présent dans la page web (qu’il soit utilisé pour satisfaire à d’autres critères de réussite ou non) doit satisfaire à ce critère de réussite. Voir [Exigence de conformité 5 : Non-interférence](https://www.w3.org/TR/WCAG20/#cc5).

#### Objectif – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#purpose-three-flashes-or-below-threshold}

Il arrive que le contenu qui flashe provoque des crises de photosensibilité. En appliquant ce critère de réussite, les utilisateurs concernés peuvent accéder au contenu et en prendre connaissance sans inquiétude quant au contenu qui flashe.

#### Comment procéder – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

Veillez à ce que les techniques ci-après soient appliquées :

* Veillez à ce que les composants ne flashent pas plus de trois fois dans n’importe quel intervalle d’une seconde.
* If the above condition cannot be met, then display flashing content within a *small safe area* in pixels on the screen. This area is calculated using a complex formula, covered in [G176: Keeping the flashing area small enough](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), so this technique should only be followed if flashing content is *absolutely* necessary.

#### En savoir plus – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Compréhension du critère de réussite 2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [Comment remplir le critère de réussite 2.3.1](https://www.w3.org/WAI/WCAG20/quickref/#seizure)

### Titre de page (2.4.2)  {#page-titled}

* Critère de réussite 2.4.2
* Niveau A
* Titre de page : les pages web présentent un titre qui décrit leur sujet ou leur but.

#### Objectif – Titre de page (2.4.2) {#purpose-page-titled}

Ce critère de réussite aide quiconque, en situation de handicap ou non, à identifier rapidement le contenu d’une page web sans avoir à lire la page entière. Ceci s’avère particulièrement utile lorsque plusieurs pages web sont ouvertes dans des onglets de navigateur, puisque le titre de la page s’affiche dans l’onglet et est donc facile à trouver.

#### Comment procéder – Titre de page (2.4.2) {#how-to-meet-page-titled}

Si une nouvelle page HTML est créée dans AEM, vous pouvez en spécifier le titre. Veillez à ce que le titre décrive adéquatement le contenu de la page, de sorte que les visiteurs puissent rapidement identifier si le contenu est réellement adapté à leurs besoins.

You can also edit the page title when editing a page, which is accessible by **Page Information** - **Properties.**

#### En savoir plus – Titre de page (2.4.2) {#more-information-page-titled}

* [Compréhension du critère de réussite 2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [Comment remplir le critère de réussite 2.4.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-title)

### Fonction du lien (selon le contexte) (2.4.4)  {#link-purpose-in-context}

* Critère de réussite 2.4.4
* Niveau A
* Fonction du lien (selon le contexte) (2.4.4) : la fonction de chaque lien est déterminée par le texte du lien seul ou par le texte du lien associé à un contexte du lien déterminé par un programme informatique, sauf si la fonction du lien est ambiguë pour tout utilisateur.

#### Objectif – Fonction du lien (selon le contexte) (2.4.4) {#purpose-link-purpose-in-context}

Pour tous les utilisateurs, en situation de handicap ou non, il est essentiel d’indiquer clairement la destination d’un lien par l’intermédiaire d’un texte de lien approprié. Les utilisateurs peuvent ainsi décider s’ils souhaitent suivre ce lien. Pour les utilisateurs voyants, un texte de lien significatif est extrêmement utile s’il existe plusieurs liens sur une page (en particulier si la page contient énormément de texte), car il indique clairement la fonctionnalité de la page cible. D’un autre côté, les utilisateurs de technologies d’assistance peuvent générer une liste de tous les liens sur une seule page, et ainsi comprendre plus facilement le texte du lien hors contexte.

#### Comment procéder – Fonction du lien (selon le contexte) (2.4.4) {#how-to-meet-link-purpose-in-context}

Avant tout, veillez à ce que l’objectif d’un lien soit clairement décrit dans le texte du lien.

* Mauvais exemple : 

   * Texte : Pour plus de détails sur nos cours du soir de l’automne 2010, cliquez ici.
   * Motif : le lien est ambigu et n’indique pas clairement sa destination.

* Bon exemple : 

   * Texte : Cours du soir pour l&#39;automne 2010 - détails.
   * Motif : il est possible d’améliorer le texte du lien en adaptant légèrement le texte et sa position.

Links should be phrased consistently across pages, especially for navigation bars. For example, if a link to a specific page is named **Publications** on one page, use that text on other pages to ensure consistency.

Au moment de la rédaction toutefois, certains problèmes peuvent se présenter quant à l’utilisation des titres :

* Habituellement, seuls les utilisateurs d’une souris ont accès au texte contenu dans l’attribut de titre, sous forme d’info-bulle contextuelle ; ce texte n’est pas accessible par clavier.
* Les lecteurs d’écran peuvent lire à haute voix les attributs de titre, mais cette fonctionnalité peut ne pas être activée par défaut ; les utilisateurs peuvent donc ne pas savoir qu’il existe un attribut de titre.
* Il est difficile de modifier l’aspect du texte d’un titre, ce qui signifie qu’il peut être difficile ou impossible de le lire pour certains utilisateurs.

Par conséquent, même si vous pouvez utiliser l’attribut de titre pour fournir plus de contexte sur un lien, vous devez connaître ses limites et ne pas l’utiliser comme alternative à un texte de lien approprié.

Where the link is made up of an image, make sure that the alternative text for the image describes the destination of the link. For example, if an image of a bookshelf is set as a link to a person’s publications, the alternative text should read **John Smith’s publications** and not **Bookshelf**.

Par ailleurs, si l’ancre du lien contient du texte qui décrit l’objet du lien en sus de l’image (et par conséquent que le texte apparaît le long de l’image), utilisez un attribut alt vide pour l’image :

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
L’extrait de code ci-dessus est une illustration ; il est recommandé d’utiliser le composant **Image**.

While it’s advisable to provide link text that identifies the purpose of the link without needing additional context, it is recognized that this is not always possible. Context free links can be used in the following cases, HTML examples of which can be found in [How to Meet Success Criterion 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs).

* si le texte du lien fait partie d’une liste de liens étroitement liés et si l’élément de liste encadrant le lien fournit suffisamment de contexte.
* Where the purpose of a link can be clearly identified from the *preceding* (not the following) paragraph text.
* si le lien est contenu dans un tableau de données et par conséquent que l’objet du lien peut être clairement identifié dans les titres associés.
* si une liste de liens est contenue dans un jeu de titres et que le titre lui-même fournit suffisamment de contexte.
* si une liste de liens est contenue dans un lien imbriqué et que la liste parente elle-même au-dessus du lien imbriqué fournit suffisamment de contexte.

Dans certains cas, s’il existe plusieurs liens sur une page (chacun d’eux fournit la destination d’un lien avec des détails complexes mais nécessaires), il peut être nécessaire de fournir une version alternative de la page web qui affiche exactement le même contenu, mais où le texte du lien n’est pas aussi détaillé.

Alternatively, scripts can be used so that a minimal amount of text is provided within the link itself, but on activating an appropriate control positioned towards the top of the page, the link text is *expanded* into further detail. A similar approach is to use CSS to *hide* the full link from sighted users, but still output it in full to screen reader users. This falls outside the scope of this document, but more information on how this can be achieved can be found in the [More Information - Link Purpose (In Context) (2.4.4)](#more-information-link-purpose-in-context) section.

#### More Information - Link Purpose (In Context) (2.4.4) {#more-information-link-purpose-in-context}

* [Compréhension du critère de réussite 2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [Comment remplir le critère de réussite 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs)
* [C7: Utilisation d’une feuille de style CSS pour masquer une portion du texte du lien](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## Principe 3 : compréhensible {#principle-understandable}

[Principe 3 : compréhensible – Les informations et l’utilisation de l’interface utilisateur doivent être compréhensibles.](https://www.w3.org/TR/WCAG20/#understandable)

### Rendre le contenu textuel lisible et compréhensible (3.1) {#make-text-content-readable-and-understandable}

[Règle 3.1 – Lisible : rendre le contenu textuel lisible et compréhensible (3.1)](https://www.w3.org/TR/WCAG20/#meaning)

### Langue de la page (3.1.1) {#language-of-page}

* Critère de réussite 3.1.1
* Niveau A
* Langue de la page : la langue par défaut de chaque page web peut être déterminée par un programme informatique.

#### Objectif – Langue de la page (3.1.1) {#purpose-language-of-page}

Ce critère de réussite garantit que ce texte et tout autre contenu linguistique est correctement restitué. Pour les utilisateurs de lecteur d’écran, il garantit que le contenu est correctement prononcé, tandis que les navigateurs visuels sont plus susceptibles d’afficher correctement certains jeux de caractères.

#### Comment procéder – Langue de la page (3.1.1) {#how-to-meet-language-of-page}

To meet this success criterion, the default language of a web page can be identified using the `lang` attribute within the `<html>` element at the top of the page. Par exemple :

* If a page is written in British English, the `<html>` element should read:
   `<html lang = “en-gb”>`

* Alors qu&#39;une page à rendre en anglais américain devrait adopter la norme suivante :
   `<html lang = “en-us”>`

**Dans AEM, la langue par défaut de votre page est définie lors de la création de la page, mais peut également être modifiée lors de la modification d’une page, accessible par** Sidekick **-** onglet Page **- Propriétés de** la page... - **onglet Avancé** .

#### En savoir plus – Langue de la page (3.1.1) {#more-information-language-of-page}

* [Compréhension du critère de réussite 3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [Comment remplir le critère de réussite 3.1.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-doc-lang-id)
* Les codes reposent sur la norme ISO 639-1. Vous trouverez une liste de codes plus complète pour chaque langue sur le site [W3Schools.com](https://www.w3schools.com/tags/ref_language_codes.asp).

### Langue d’un passage (3.1.2)  {#language-of-parts}

* Critère de réussite 3.1.2
* Niveau AA
* Langue d’un passage : la langue de chaque passage ou expression du contenu peut être déterminée par un programme informatique sauf pour un nom propre, pour un terme technique, pour un mot dont la langue est indéterminée ou pour un mot ou une expression faisant partie du langage courant de la langue utilisée dans le contexte immédiat.

#### Objectif – Langue d’un passage (3.1.2) {#purpose-language-of-parts}

Ce critère de réussite vise le même objectif que le critère de réussite [Langue de la page](#languageofpage), mais il s’applique aux pages web avec du contenu en plusieurs langues sur une seule page (par exemple, en raison de citations ou de mots empruntés peu courants).

Si une page applique ce critère de réussite, alors :

* Le logiciel de transition en braille peut insérer des caractères accentués.
* Les lecteurs d’écran peuvent prononcer correctement les mots qui sont dans une autre langue que la langue par défaut.
* Les outils de traduction du type Google Translate peuvent correctement traduire les mots d’une langue à une autre.

#### Comment procéder – Langue d’un passage (3.1.2) {#how-to-meet-language-of-parts}

L’ `lang` attribut peut être utilisé pour identifier les modifications dans la langue du contenu. Par exemple, une citation en allemand (code ISO 639-1 &quot;de&quot;) peut s’afficher comme suit :

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
Les attributs blockquote ne sont pas pris en charge dans une instance prête à l’emploi. Il est toutefois possible de développer un composant personnalisé pour prendre cette fonction en charge.

De même, le navigateur peut restituer correctement un mot ou une expression emprunté peu courant si l’élément `span` est utilisé comme suit :

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
Il n’est pas nécessaire d’adhérer à ce critère de réussite pour les noms ou villes dans différentes langues ou lors de l’utilisation de mots ou d’expressions empruntés qui sont devenus courants dans la langue par défaut (tel que *diktat* en français).

Pour ajouter l’élément span, avec un langage approprié, vous pouvez modifier manuellement votre balisage HTML en mode d’édition source du RTE afin qu’il se lise comme ci-dessus. Vous pouvez également inclure l’ `lang` attribut dans RTE par un administrateur système (voir [Ajout de la prise en charge d’éléments et d’attributs](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)HTML supplémentaires).

#### En savoir plus – Langue d’un passage (3.1.2) {#more-information-language-of-parts}

* [Compréhension du critère de réussite 3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.htm)
* [Comment remplir le critère de réussite 3.1.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-other-lang-id)

### Aider l’utilisateur à éviter et à corriger les erreurs de saisie (3.3) {#help-users-avoid-and-correct-mistakes}

[Règle 3.3 – Assistance à la saisie : aider l’utilisateur à éviter et à corriger les erreurs de saisie (3.3)](https://www.w3.org/TR/WCAG20/#minimize-error)

### Étiquettes ou instructions (3.3.2) {#labels-or-instructions}

* Critère de réussite 3.3.2
* Niveau A
* Étiquettes ou instructions : des étiquettes sont présentées ou des instructions sont fournies quand un contenu requiert une saisie utilisateur.

#### Objectif – Étiquettes ou instructions (3.3.2) {#purpose-labels-or-instructions}

La fourniture d’instructions pour aider les utilisateurs à remplir des formulaires est l’un des éléments essentiels pour rendre une interface conviviale. Ceci s’avère particulièrement utile pour les personnes ayant des déficiences visuelles ou cognitives qui risquent autrement d’avoir du mal à comprendre la mise en page d’un formulaire et le tri des données à fournir dans un champ particulier du formulaire.

Dans AEM, une étiquette est ajoutée par défaut lorsque vous ajoutez un composant de formulaire, tel que **Champ de texte**, à la page. Ce titre par défaut dépend du type de composant. Vous pouvez ajouter votre propre titre pour ce champ dans l’onglet **Titre et texte** de la boîte de dialogue d’édition. Veillez à ce que les étiquettes aident les utilisateurs à comprendre les données associées à chaque composant de formulaire.

![cac-04](assets/cac-04.png)

Utilisez ce champ **Titre** pour les éléments de champ, car il fournit une étiquette accessible par les technologies d’assistance. Le simple fait d’écrire une étiquette dans le texte en regard du champ ne suffit pas.

For some form components it is also possible to visually hide labels using the **Hide Title** checkbox. Labels hidden in this way are still available to assistive technology, but not displayed on the screen. While this can be a good approach in some situations it is usually best to include a visual label wherever possible, as some users may be looking at a very small section of the screen (one field at a time) and need the labels to identify the field correctly.

#### Boutons Image {#image-buttons}

Lorsque des boutons d’image sont utilisés (par exemple, le composant Bouton **de l’** image), le champ **Titre** de l’onglet **Titre et Texte** de la boîte de dialogue Modifier fournit en fait le texte de remplacement de l’image, plutôt que le libellé. Ainsi, dans l’exemple ci-dessous, l’image avec le texte `Submit` comporte un texte alternatif de `Submit`, ajouté à l’aide du champ **Titre** de la boîte de dialogue de modification.

![cac-05](assets/cac-05.png)

#### Groupes de champs de formulaire {#groups-of-form-fields}

Lorsqu’il existe un groupe de commandes associées, comme **Groupe de cases d’option**, il peut être nécessaire de donner un titre au groupe, ainsi qu’aux commandes individuelles. Lors de l’ajout d’un jeu de cases d’option dans AEM, le champ **Titre** fournit le titre de ce groupe et des titres individuels sont spécifiés alors que les cases d’option (**Éléments**) sont créées.

![cac-06](assets/cac-06.png)

Cependant, il n&#39;existe aucune association programmatique entre le titre du groupe et les boutons radio eux-mêmes. Les éditeurs de modèles doivent placer le titre dans les balises nécessaires `fieldset` et `legend` pour créer cette association. Pour ce faire, il suffit de modifier le code source de la page. Un administrateur système peut également ajouter la prise en charge de ces éléments afin qu’ils apparaissent dans la boîte de dialogue Propriétés **du** champ (voir [Ajout de la prise en charge d’éléments et d’attributs](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)HTML supplémentaires).

#### Considérations supplémentaires pour les formulaires {#additional-considerations-for-forms}

Si les données doivent être saisies dans un format spécifique, précisez-le dans le texte de l’étiquette. Par exemple, si une date doit être entrée dans le `DD-MM-YYYY` format, indiquez-la spécifiquement dans le libellé. Cela signifie que lorsque les utilisateurs de lecteurs d’écran rencontrent le champ, le libellé est automatiquement annoncé, ainsi que les informations supplémentaires sur le format.

Si la saisie d’un champ de formulaire est obligatoire, renseignez-la en utilisant le mot requis dans le libellé. AEM ajoute un astérisque lorsqu’un champ est requis, mais il serait idéal d’inclure le mot `required`dans le libellé lui-même (dans le champ **Titre** de la boîte de dialogue de modification).

![cac-07](assets/cac-07.png)

Le positionnement des libellés est également important car ils permettent de localiser les champs appropriés. Ceci est tout particulièrement important lorsque l’utilisateur est confronté à un formulaire complexe. Suivez les conventions ci-dessous :

* Cases à cocher ou cases d’option : 
Les libellés sont positionnés immédiatement à droite du champ.
* Tous les autres composants de formulaire (par ex., zones de texte, zones de liste modifiable) : 
Les libellés sont positionnés immédiatement au-dessus ou à gauche du champ.

Dans les formulaires simples avec des fonctionnalités très limitées, un `Submit` bouton approprié peut servir d’étiquette pour le champ adjacent (par exemple `Search`). Cela s’avère utile dans les cas où il peut être difficile de trouver de l’espace pour le texte de l’étiquette.

#### En savoir plus – Étiquettes ou instructions (3.3.2) {#more-information-labels-or-instructions}

* [Compréhension du critère de réussite 3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [Comment remplir le critère de réussite 3.3.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-minimize-error-cues)

