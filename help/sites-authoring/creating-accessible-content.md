---
title: Création de contenu accessible pour la conformité à Adobe Experience Manager (WCAG 2.1)
description: Utiliser AEM pour aider à rendre le contenu Web accessible et utilisable par les personnes handicapées
translation-type: tm+mt
source-git-commit: cb7df7301364eb1ce3a1ca376256d2cd5afcb2c8
workflow-type: tm+mt
source-wordcount: '13956'
ht-degree: 83%

---


# Création de contenu accessible (conformité WCAG 2.1) {#creating-accessible-content-wcag-conformance}

Les règles [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/), établies par [un groupe de travail du consortium World Wide Web](https://www.w3.org/Consortium/activities#Accessibility_Guidelines_Working_Group), constituent un ensemble de règles et de critères de réussite, indépendants de la technologie, permettant d’obtenir des contenus web accessibles et utilisables par les personnes en situation de handicap.

En introduction, le consortium propose une série de sections et de documents annexes :

* [Nouvelles fonctionnalités de WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Conformité à WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Présentation de WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Techniques relatives à WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Documents WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

En outre, voir :
* Our [Quick Guide to WCAG 2.1](/help/managing/qg-wcag.md).
* Rapports de conformité [à l’accessibilité pour les solutions](https://www.adobe.com/accessibility/compliance.html)Adobe.
* [Configuration de l’éditeur de texte enrichi pour la production de contenu accessible](/help/sites-administering/rte-accessible-content.md)

Les règles sont classées selon trois niveaux de conformité : niveau A (le plus bas), niveau AA et niveau AAA (le plus élevé). Pour résumer, les niveaux sont définis comme suit :

* **Niveau A :** votre site atteint un niveau minimum d’accessibilité. Pour atteindre ce niveau, tous les critères de réussite de niveau A sont satisfaits.
* **Niveau A :** Il s&#39;agit d&#39;un niveau d&#39;accessibilité idéal à rechercher, dans lequel votre site atteint un niveau fondamental d&#39;accessibilité, de sorte qu&#39;il soit accessible à la plupart des personnes dans la plupart des situations utilisant la plupart des technologies. Pour atteindre ce niveau, tous les critères de réussite de niveau A et de niveau AA sont satisfaits.
* **Niveau AAA :** votre site atteint un très haut niveau d’accessibilité. Pour atteindre ce niveau, tous les critères de réussite des niveaux A, AA et AAA sont satisfaits.

Lors de la création de votre site, vous devez déterminer à quel niveau général il doit se conformer.

The following section presents [layers of the WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) with related success criteria for Level A and Level AA [conformance levels](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1).

>[!NOTE]
>
>Dans ce document, nous utilisons :
>
>* The [short names for the WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* The [numbering used in the WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) to aid cross-referencing with the WCAG website.


## Principe 1 : perceptible  {#principle-perceivable}

[Principe 1 : perceptible – Les informations et les composants de l’interface utilisateur doivent être présentés aux utilisateurs sous des formes qu’ils peuvent percevoir.](https://www.w3.org/TR/WCAG/#perceivable)

### Équivalents textuels (1.1)  {#text-alternatives}

[Règle 1.1 – Les équivalents textuels : proposer des équivalents textuels à tout contenu non textuel qui pourra alors être présenté sous d’autres formes selon les besoins de l’utilisateur : grands caractères, braille, synthèse vocale, symboles ou langage simplifié.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Contenu non textuel (1.1.1)  {#non-text-content}

* Critère de réussite 1.1.1
* Niveau A
* Contenu non textuel : tout contenu non textuel présenté à l’utilisateur possède un texte secondaire qui remplit une fonction équivalente sauf dans les situations énumérées ci-dessous.

#### Objectif – Contenu non textuel (1.1.1) {#purpose-non-text-content}

Le contenu d’une page web peut être proposé dans différents formats non textuels (photos, vidéos, animations, tableaux et graphiques). Les personnes aveugles ou malvoyantes ne sont pas en mesure de voir le contenu non textuel, mais elles peuvent accéder au contenu textuel en le faisant lire par un lecteur d’écran ou sous forme tactile dans un appareil d’affichage en braille. Ainsi, en proposant des équivalents textuels pour le contenu graphique, les personnes qui ne voient pas le contenu graphique peuvent accéder à une version équivalente des informations véhiculées par le contenu.

Autre avantage utile : les équivalents textuels permettent aux moteurs de recherche d’indexer le contenu non textuel.

#### Comment procéder – Contenu non textuel (1.1.1)  {#how-to-meet-non-text-content}

Pour les graphiques statiques, l&#39;exigence de base est de fournir une alternative de texte équivalente pour le graphique. Vous pouvez le faire dans le champ Texte **** de remplacement ; voir par exemple, l’ **[image](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/components/image.html)**du composant principal.

>[!NOTE]
>
>Certains composants principaux prêts à l’emploi, tels que le **[carrousel](https://docs.adobe.com/content/help/fr/experience-manager-core-components/using/components/carousel.html)**, ne fournissent pas de champ de texte**de remplacement pour ajouter des descriptions de texte de remplacement à des images individuelles, bien qu’il existe le champ **Etiquette**(onglet ****[Accessibilité) pour l’ensemble du composant.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)**
>
>Lors de l’implémentation de ces versions pour votre instance AEM, votre équipe de développement devra configurer ces composants pour prendre en charge l’attribut `alt`[ afin que les auteurs puissent l’ajouter au contenu (voir Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

Dans AEM, le champ **Texte secondaire** doit être renseigné par défaut. If the image is purely decorative and alternative text would be unnecessary, the **Image is decorative** option can be checked.

#### Création d’un texte secondaire adapté {#creating-good-text-alternatives}

Il existe diverses formes de contenu non textuel. Par conséquent, la valeur du texte secondaire dépend du rôle du graphique dans la page web. Voici quelques-unes des règles de base à respecter :

* Les textes secondaires doivent être succincts, tout en communiquant clairement l’information essentielle du contenu non textuel.
* Il est préférable d’éviter les descriptions trop longues (plus de 100 caractères). Si un texte secondaire doit être plus détaillé :
   * donnez une brève description dans le texte secondaire ;
   * proposez une description plus longue dans le texte ailleurs sur la même page ou dans une page web distincte. Renvoyez vers cette description individuelle en transformant l’image en lien ou en plaçant un lien textuel près de l’image.
* Le texte secondaire ne doit pas répliquer le contenu fourni sous forme de texte à proximité sur la même page. N’oubliez pas que nombre d’images sont des illustrations de points déjà traités dans le texte d’une page ; il existe peut-être déjà un texte secondaire.
* Si le contenu non textuel est un lien vers une autre page ou un autre document et qu’il n’existe pas de texte faisant partie dudit lien, le texte secondaire de l’image doit indiquer la destination du lien, et non décrire l’image.
* Si le contenu non textuel est contenu dans un bouton et qu’il n’existe pas de texte faisant partie dudit bouton, le texte secondaire de l’image doit indiquer la fonction du bouton, et non décrire l’image.
* Il est parfaitement acceptable qu’une image se voit attribuer un texte de remplacement vide (nul), mais seulement si l’image n’a pas besoin d’un autre texte (par exemple, il s’agit d’un graphique purement décoratif) ou si le texte équivalent existe déjà dans le texte de la page.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Voici quelques-uns des types spécifiques de contenu non textuel auquel un texte secondaire doit être associé :

* Photos illustratives : il s’agit de photos de personnes, d’objets ou de lieux. Il est important de réfléchir au rôle de la photo dans la page et de généralement recommander de décrire le contenu de l&#39;image, car la technologie d&#39;assistance annoncera le type d&#39;élément (par exemple, `graphic` ou `image`); il peut être plus clair à utiliser `screenshot` ou `illustration` dans les descriptions textuelles de rechange, mais cela dépend du contexte. La cohérence est un facteur important, une décision doit être prise pour l’ensemble de l’équipe de création et elle doit être appliquée tout au long de l’expérience utilisateur.
* Icônes : certains petits pictogrammes (images) communiquent parfois des informations spécifiques. Ils doivent être utilisés de manière uniforme sur une page et un site. Toutes les instances de l’icône sur une page ou un site doivent avoir le même texte secondaire bref et succinct, sauf si cela duplique de manière superflue le texte adjacent.
* Tableaux et graphiques : ils représentent généralement des données numériques. Pour proposer un texte secondaire, vous pouvez par exemple inclure un bref résumé des principales tendances affichées dans le graphique ou diagramme. Si nécessaire, fournissez une description plus détaillée du texte dans le champ **Description** de l’onglet des propriétés d’image **Avancées**. En outre, vous pouvez fournir les données sources sous forme tabulaire ailleurs dans la page ou le site.
* Cartes, diagrammes, organigrammes : Pour les graphiques fournissant des données spatiales (par exemple, pour prendre en charge la description des relations entre des objets ou un processus), assurez-vous que le message clé est fourni au format texte et que ces informations textuelles sont placées près de chaque point de données associé. Dans le cas des cartes, il est probable que l’utilisation d’un équivalent en texte intégral ne soit pas pratique, mais si la carte est fournie pour aider les gens à trouver leur chemin vers un emplacement donné, le texte de remplacement de l’image de carte peut indiquer brièvement la *carte X*, puis fournir des indications vers cet emplacement dans le texte à un autre endroit, dans la page ou dans le champ **Description** de l’onglet **Avancé** du composant **Image**.
* CAPTCHA :
L’acronyme anglais CAPTCHA (*Completely Automated Public Turing test to tell Computers and Humans Apart*) désigne un test servant à déterminer si le contenu est consulté par une personne plutôt que par un ordinateur. Ce contrôle de sécurité utilisé sur les pages web pour distinguer les humains des logiciels malveillants peut constituer un obstacle à l’accessibilité. Il s’agit d’images obligeant les utilisateurs à décrire ce qu’ils voient pour pouvoir réussir le test de sécurité. Il n’est évidemment pas possible de fournir un équivalent textuel pour l’image. Vous devez par conséquent envisager des alternatives non graphiques.
Le W3C émet plusieurs suggestions, comme celles énumérées ci-dessous. Chacune de ces approches a ses propres avantages et inconvénients.
   * Énigmes logiques
   * Utilisation d’une sortie audio plutôt que d’images
   * Comptes d’utilisateur limités et filtres de courrier indésirable
* Images d’arrière-plan : elles impliquent l’utilisation de feuilles de style en cascade CSS (Cascading Style Sheet) plutôt que de code HTML. Il n’est donc pas possible de spécifier une valeur de texte secondaire. Par conséquent, les images d’arrière-plan ne doivent pas communiquer d’informations textuelles importantes. Sinon, ces informations doivent aussi être spécifiées dans le texte de la page. Cependant, il est important qu’un arrière-plan alternatif s’affiche si l’image ne peut pas s’afficher.

>[!NOTE]
>
>Le niveau de contraste entre l’arrière-plan et le texte au premier plan doit être suffisant. Cela est décrit de manière plus détaillée à la section [Contraste (minimum) (1.4.3)](#contrast-minimum).

#### En savoir plus – Contenu non textuel (1.1.1)  {#more-information-non-text-content}

* [Compréhension du critère de réussite 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Comment remplir le critère de réussite 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Explication des CAPTCHA et alternatives par le W3C](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Média temporel (1.2)  {#time-based-media}

[Règle 1.2 – Média temporel : proposer des versions de remplacement aux médias temporels.](https://www.w3.org/TR/WCAG/#time-based-media)

This deals with web content that is *time-based*. This covers content that the user can play (such as video, audio, and animated content) and may be prerecorded or a live stream.

### Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Critère de réussite 1.2.1
* Niveau A
* Contenu seulement audio ou vidéo (pré-enregistré) : pour des médias pré-enregistrés seulement audio et pré-enregistrés seulement vidéo, sauf si l’audio ou la vidéo est un média de remplacement pour un texte et qu’ils sont clairement identifiés comme tels, ce qui suit s’applique :
   * Contenu pré-enregistré seulement audio : fournir une version de remplacement pour un média temporel, présentant une information équivalente au contenu seulement audio.
   * Contenu pré-enregistré seulement vidéo : fournir, soit une version de remplacement pour un média temporel, soit une piste audio (présentant une information équivalente) pour un contenu pré-enregistré seulement vidéo.

#### Objectif – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Les personnes suivantes peuvent éprouver des problèmes à accéder au contenu vidéo et audio :

* Les personnes malvoyantes lorsqu’il n’y a aucune piste audio ou si la piste audio ne suffit pas à les informer de ce qui se passe dans la vidéo ou l’animation.
* Les personnes malentendantes ou sourdes, qui ne peuvent pas écouter la piste audio.
* Les personnes qui peuvent écouter la piste audio, mais qui ne la comprennent pas (si par exemple elle est dans une langue qu’elles ne comprennent pas).

Les personnes qui utilisent des navigateurs ou des périphériques qui ne prennent pas en charge la lecture du contenu dans des formats multimédias spécifiques (Adobe Flash par exemple) peuvent aussi ne pas avoir accès au contenu vidéo ou audio.

En proposant ces informations dans un autre format (texte par exemple, ou audio pour un contenu vidéo sans audio), elles seront accessibles par les personnes qui ne sont pas en mesure d’accéder au contenu original.

#### Comment procéder – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Si le contenu est enregistré au préalable avec un fichier audio sans vidéo (tel qu’un podcast) :
   * Fournissez un lien immédiatement avant ou après le contenu vers une transcription textuelle du contenu audio.
La transcription doit être une page HTML avec un équivalent textuel de tout le contenu non parlé important et parlé, et indiquer en outre qui parle, avec les expressions vocales et une description du décor et de tout autre contenu audio significatif.
* Si le contenu est une animation ou une vidéo préenregistrée sans audio :
   * Fournissez un lien immédiatement avant ou après le contenu vers une description textuelle équivalente des informations communiquées par la vidéo.
   * Ou fournissez une audio-description équivalente dans un format audio fréquemment utilisé (MP3 par exemple).

>[!NOTE]
>
>Si le contenu audio ou vidéo est fourni comme une alternative au contenu qui existe déjà dans un autre format sur la même page Web, une alternative supplémentaire peut ne pas être nécessaire.
>
>Les lignes directrices, [Comprendre WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html), fournissent des informations complémentaires.

L’insertion de contenu multimédia dans vos pages Web AEM est similaire à l’insertion d’une image. Cependant, comme le contenu multimédia est bien plus qu&#39;une image fixe, il existe une variété de paramètres et d&#39;options pour contrôler la façon dont le multimédia est lu.

>[!NOTE]
>
>Si vous utilisez un contenu multimédia informatif, vous devez également créer des liens vers les équivalents. Par exemple, pour inclure une transcription textuelle, créez une page HTML où afficher la transcription, puis ajoutez un lien en regard ou en dessous du contenu audio.

#### En savoir plus – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [Compréhension du critère de réussite 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### Sous-titres (pré-enregistrés) (1.2.2) {#captions-prerecorded}

* Critère de réussite 1.2.2
* Niveau A
* Sous-titres (pré-enregistrés) : fournir des sous-titres pour tout contenu audio pré-enregistré dans un média synchronisé, excepté lorsque le média est un média de remplacement pour un texte et qu’il est clairement identifié comme tel.

#### Objectif – Sous-titres (pré-enregistrés) (1.2.2) {#purpose-captions-prerecorded}

Les personnes sourdes ou malentendantes seront incapables ou auront de grandes difficultés à accéder au contenu audio. Les légendes sont des équivalents textuels pour les sons parlés et non parlés, affichés à l’écran au moment approprié pendant la vidéo. Ils permettent aux gens qui ne peuvent pas entendre le son de comprendre ce qui se passe.

#### Comment procéder – Sous-titres (pré-enregistrés) (1.2.2) {#how-to-meet-captions-prerecorded}

Les sous-titres peuvent être :

* intégrés : toujours visibles pendant la lecture de la vidéo ;
* non intégrés : activés ou désactivés par l’utilisateur.

Ajoutez des sous-titres non intégrés chaque fois que cela est possible, car les utilisateurs peuvent ainsi décider s’ils souhaitent les afficher.

Pour les légendes fermées, vous devez créer et fournir un fichier de sous-titrage synchronisé dans un format approprié (tel que [SMIL](https://www.w3.org/AudioVideo/)) en même temps que le fichier vidéo (les détails sur la façon de procéder dépassent la portée de ce guide, mais nous avons fourni des liens vers certains didacticiels sous [Plus d’informations - Légendes (préenregistré) (1.2.2)](#more-information-captions-prerecorded). Veillez à fournir une note ou à activer la fonction de sous-titrage dans le lecteur vidéo pour informer les utilisateurs que les sous-titrages sont disponibles pour la vidéo.

Si vous devez utiliser des sous-titres intégrés, incorporez le texte à la piste vidéo. Pour ce faire, utilisez des applications de montage vidéo qui permettent de superposer du texte sur la vidéo.

#### More Information - Captions (Prerecorded) (1.2.2) {#more-information-captions-prerecorded}

* [Compréhension du critère de réussite 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Critère de réussite 1.2.3
* Niveau A
* Audio-description ou version de remplacement pour un média temporel (pré-enregistré) : fournir une version de remplacement pour un média temporel ou une audio-description du contenu vidéo pré-enregistré pour un média synchronisé, excepté quand le média est un média de remplacement pour un texte et qu’il est clairement identifié comme tel.

#### Objectif – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Les personnes aveugles ou malvoyantes ne pourront pas accéder au contenu si les informations contenues dans une vidéo ou une animation sont fournies sous forme visuelle seulement ou si la piste audio ne fournit pas suffisamment d’informations pour comprendre ce qui se passe visuellement.

#### Comment procéder – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Deux approches peuvent être adoptées pour remplir ce critère de réussite. Les deux sont acceptables :

1. Inclure une audio-description supplémentaire pour le contenu vidéo. Vous pouvez y parvenir de trois façons :
   * Durant les pauses dans le dialogue existant, fournissez des informations sur les modifications dans la scène qui ne sont pas présentées dans la piste audio existante.
   * Fournissez une nouvelle piste audio supplémentaire et facultative contenant la piste audio originale, mais aussi des informations audio supplémentaires sur les modifications dans la scène.
      * Les utilisateurs peuvent ainsi permuter entre la piste audio existante (qui ne contient *pas* de description audio) et la nouvelle piste audio (qui *comprend* une description audio).
      * De cette façon, les utilisateurs qui n’ont pas besoin de la description supplémentaire ne sont pas interrompus.
   * Créez une deuxième version du contenu vidéo afin d’y inclure des audio-descriptions plus détaillées. Ceci réduit les difficultés associées à la spécification d’audio-descriptions détaillées dans les intervalles au sein du dialogue existant, en interrompant temporairement l’audio et la vidéo à des points appropriés. Vous pouvez ainsi ajouter une audio-description beaucoup plus longue avant que l’action ne recommence. Comme dans l’exemple précédent, il est préférable de proposer une piste audio supplémentaire facultative afin d’éviter toute interruption pour les utilisateurs qui n’ont pas besoin du contenu supplémentaire.
1. Fournir une transcription de texte qui est un texte approprié équivalent aux éléments audio et visuels de la vidéo ou de l&#39;animation. Cela devrait inclure, le cas échéant, une indication de la personne qui parle, une description du cadre, tout événement ou information présenté visuellement et toute expression vocale. Selon sa longueur, vous pouvez placer la transcription sur la même page que la vidéo ou l’animation, ou sur une page distincte ; si vous choisissez cette dernière option, fournissez un lien vers la transcription adjacente à la vidéo ou à l&#39;animation.

Les détails exacts de la création de vidéos avec description audio ne sont pas compris dans ce guide. La création de descriptions vidéo et audio peut prendre du temps, mais d’autres produits Adobe peuvent vous aider à accomplir ces tâches.

#### En savoir plus – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Compréhension du critère de réussite 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### Sous-titres (en direct) (1.2.4)    {#captions-live}

* Critère de réussite 1.2.4
* Niveau AA
* Sous-titres (en direct) : fournir des sous-titres pour tout contenu audio en direct, sous forme de média synchronisé.

#### Objectif – Sous-titres (en direct) (1.2.4)  {#purpose-captions-live}

This success criterion is identical to [Captions (Prerecorded)](#captions-prerecorded) in that it addresses accessibility barriers experienced by people who are deaf or hearing-impaired, except that this success criterion deals with live presentations such as webcasts.

#### Comment procéder – Sous-titres (en direct) (1.2.4) {#how-to-meet-captions-live}

Suivez les instructions de la section [Sous-titres (pré-enregistrés)](#captions-prerecorded) ci-dessus. Toutefois, en raison de la nature du média (direct), les sous-titres doivent être créés aussi rapidement que possible, en fonction de ce qui se passe dans la vidéo. Par conséquent, envisagez d’utiliser des outils de sous-titrage en temps réel ou de transcription voix-texte.

Ce document ne vise pas à fournir des instructions détaillées à ce sujet, mais vous trouverez des renseignements utiles en suivant les liens ci-après :

* [WebAIM : Real Time Captioning (sous-titrage en temps réel ; en anglais)](https://www.webaim.org/techniques/captions/realtime.php)

* [Projet AccessComputing (Université de Washington) : Les légendes peuvent-elles être générées automatiquement à l’aide de la reconnaissance vocale ?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### En savoir plus – Sous-titres (en direct) (1.2.4)  {#more-information-captions-live}

* [Compréhension du critère de réussite 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Comment remplir le critère de réussite 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Audio-description (préenregistrée) (1.2.5) {#audio-description-prerecorded}

* Critère de réussite 1.2.5
* Niveau AA
* Audio-description (pré-enregistrée) : fournir une audio-description pour tout contenu vidéo pré-enregistré, sous forme de média synchronisé.

#### Objectif – Audio-description (pré-enregistrée) (1.2.5) {#purpose-audio-description-prerecorded}

Ce critère de réussite est identique au critère [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audio-description-or-media-alternative-prerecorded), excepté que les auteurs doivent fournir une audio-description beaucoup plus détaillée, conforme au niveau AA.

#### Comment procéder – Audio-description (pré-enregistrée) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Suivez les instructions de la section [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audio-description-or-media-alternative-prerecorded).

#### En savoir plus – Audio-description (pré-enregistrée) (1.2.5) {#more-information-audio-description-prerecorded}

* [Compréhension du critère de réussite 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adaptable (1.3)  {#adaptable}

[Règle 1.3 – Adaptable : créer un contenu qui puisse être présenté de différentes manières sans perte d’information ni de structure (par exemple avec une mise en page simplifiée).](https://www.w3.org/TR/WCAG/#adaptable)

Cette règle couvre les exigences nécessaires pour aider les personnes qui :

* peut ne pas être en mesure d&#39;accéder aux informations présentées par un auteur dans la présentation par défaut de ce contenu (par exemple, une mise en page à plusieurs colonnes ou une page avec une utilisation intensive des couleurs et/ou des images).

* peut utiliser un affichage audio uniquement ou un affichage visuel alternatif tel qu’un texte volumineux ou un contraste élevé.

### Informations et relations (1.3.1)    {#info-and-relationships}

* Critère de réussite 1.3.1
* Niveau A
* Informations et relations : l’information, la structure et les relations véhiculées par la présentation peuvent être déterminées par un programme informatique ou sont disponibles sous forme de texte.

#### Objectif – Informations et relations (1.3.1)  {#purpose-info-and-relationships}

De nombreuses technologies d&#39;assistance utilisées par les personnes handicapées s&#39;appuient sur l&#39;information structurelle pour afficher ou *comprendre* efficacement le contenu. Ces informations structurelles peuvent prendre la forme d’en-têtes de page, de lignes et de colonnes de tableau et de types de listes. Par exemple, un lecteur d’écran peut permettre à un utilisateur de naviguer dans une page d’un titre à l’autre. Cependant, lorsque le contenu de la page semble avoir une structure uniquement par le biais de la mise en forme visuelle, plutôt que le code HTML sous-jacent, aucune information structurelle n’est disponible pour les technologies d’assistance, ce qui limite leur capacité à prendre en charge une navigation plus facile.

Ce critère de réussite existe pour s&#39;assurer que ces informations structurelles sont fournies par programmation au moyen de code HTML ou d&#39;autres techniques de codage, de sorte que les navigateurs et les technologies d&#39;assistance puissent accéder à ces informations et en tirer parti.

#### Comment procéder – Informations et relations (1.3.1)  {#how-to-meet-info-and-relationships}

AEM facilite la création de contenu Web sémantiquement significatif à l’aide des éléments HTML appropriés. Ouvrez le contenu de la page dans l’éditeur de texte enrichi (un composant Texte) et, à l’aide du menu **Paraformat** (symbole du paragraphe), spécifiez l’élément structurel approprié (paragraphe, en-tête, etc.).

Vous pouvez vous assurer que vos pages Web disposent de la structure appropriée en utilisant les éléments suivants, le cas échéant :

* **En-têtes :** Tant que les fonctions d’accessibilité du RTE sont activées, AEM offre 3 niveaux d’en-tête de page. Vous pouvez les utiliser pour identifier les sections et sous-sections de contenu. En-tête 1 est le plus haut niveau d’en-tête, En-tête 3 le plus bas. L’administrateur système peut configurer le système pour autoriser l’utilisation d’un plus grand nombre de niveaux d’en-tête.

* **Listes**: Vous pouvez utiliser du code HTML pour spécifier trois types de listes différents :
   * L’élément `<ul>` est utilisé pour les listes *non triées* (à puces). Les éléments de liste individuels sont identifiés à l’aide de l’élément `<li>`. Dans l’éditeur de texte enrichi, utilisez l’icône **Liste à puces**.
   * L’élément `<ol>` est utilisé pour les listes *numérotées*. Les éléments de liste individuels sont identifiés à l’aide de l’élément `<li>`. Dans l’éditeur de texte enrichi, cliquez sur l’icône **Liste numérotée**.
   Pour modifier un contenu existant en un type de liste particulier, sélectionnez-le, puis choisissez le type de liste approprié. Comme dans l’exemple précédent illustrant la saisie du texte du paragraphe, les éléments de liste appropriés sont automatiquement ajoutés au fichier HTML.

   En mode Plein écran, les icônes **Liste à puces** et **Liste numérotée** sont visibles. Lorsque vous n’êtes pas en mode Plein écran, les deux options sont disponibles derrière l’icône **Listes** unique.

* **Tableaux**: Les tableaux de données doivent être identifiés à l’aide d’éléments de tableau HTML :
   * un élément `<table>` ;
   * un élément `<tr>` pour chaque ligne du tableau ;
   * un élément `<th>` pour chaque en-tête de ligne et de colonne ;
   * un élément `<td>` pour chaque cellule de données.
   En outre, les tableaux accessibles utilisent les éléments et attributs suivants :

   * L’élément `<caption>` sert à fournir une légende visible pour le tableau. Les légendes apparaissent par défaut centrées au-dessus du tableau, mais peuvent être positionnées de manière appropriée à l’aide de CSS. La légende est associée au tableau par programmation, ce qui en fait une méthode utile pour fournir une introduction au contenu.
   * L’élément `<summary>` aide les utilisateurs non voyants à comprendre plus facilement les informations présentées dans un tableau, en fournissant une synthèse de ce qu’un utilisateur voyant peut voir. Cela s’avère particulièrement utile lorsque des mises en page de tableau complexes ou non conventionnelles sont utilisées (cet attribut n’est pas affiché dans le navigateur, il est uniquement lu pour les technologies d’assistance).
   * L’attribut `scope` de l’élément `<th>` sert à indiquer si une cellule représente un en-tête pour une ligne ou une colonne particulière. Une approche similaire consiste à utiliser les attributs header et id dans des tableaux complexes, où les cellules de données peuvent être associées à un ou plusieurs en-têtes.
   >[!NOTE]
   >
   >Par défaut, ces éléments et attributs ne sont pas directement disponibles, mais l’administrateur du système peut ajouter la prise en charge de ces valeurs dans la boîte de dialogue **Propriétés du tableau**[ (voir Ajout de la prise en charge des éléments et attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes).

   Pour ouvrir la boîte de dialogue **Tableau** dans laquelle vous pouvez sélectionner l’onglet **Propriétés** du tableau :

   * Définissez une **légende** appropriée.
   * Idéalement, supprimez toutes les valeurs par défaut pour **Largeur**, **Hauteur**, **Bordure**, **Marge intérieure des cellules** et **Espacement des cellules**. En effet, ces propriétés peuvent être définies dans une feuille de style globale.
   Vous pouvez ensuite utiliser les **propriétés de cellule** pour définir si la cellule est une cellule de données ou d’en-tête :

* **Accent**: Utilisez l’ `<strong>` élément ou `<em>` l’élément pour indiquer l’accent. N’utilisez pas d’en-têtes pour mettre le texte en évidence au sein des paragraphes.
   * Surlignez le texte à mettre en évidence.
   * Cliquez sur l’icône **B** (pour `<strong>`) ou **I** (pour `<em>`) du panneau **Propriétés** (HTML doit être sélectionné).

      >[!NOTE]
      >
      >Dans une installation AEM standard, l’éditeur de texte enrichi est configuré pour utiliser :
      >
      >* `<b>` pour `<strong>`
      >* `<i>` pour `<em>`
      >
      >Ils sont identiques dans la pratique, mais `<strong>` et `<em>` sont préférables, car il s’agit de code HTML correct sémantiquement. Votre équipe de développement peut configurer l’éditeur de texte enrichi pour qu’il utilise `<strong>` et `<em>` (au lieu de `<b>` et `<i>`) lors du développement de votre instance de projet.


* **Tableaux de données complexes** : dans certains cas, lorsqu’il existe des tableaux complexes comportant deux niveaux d’en-tête ou plus, les propriétés de tableau de base peuvent ne pas suffire à fournir toutes les informations structurelles nécessaires. Pour ce type de tableaux complexes, il est nécessaire de créer des relations directes entre les en-têtes et leurs cellules associées à l’aide des attributs **header** et **id.**

   >[!NOTE]
   >
   >L’attribut id n’est pas disponible dans une installation prête à l’emploi. Il peut être activé en configurant les règles HTML et le sérialiseur dans l’éditeur de texte enrichi.

   Par exemple, dans le tableau ci-dessous, les attributs header et id correspondent pour créer une association de programmation pour les utilisateurs de technologies d’assistance.

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
   >
   >Cette fonctionnalité n’est pas immédiatement disponible dans une installation standard. Vous devez configurer les règles HTML et le sérialiseur dans l’éditeur de texte enrichi.

#### En savoir plus – Informations et relations (1.3.1) {#more-information-info-and-relationships}

* [Compréhension du critère de réussite 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Comment remplir le critère de réussite 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Séquence significative (1.3.2)  {#meaningful-sequence}

* Critère de réussite 1.3.2
* Niveau A
* Séquence significative : lorsque la séquence dans laquelle le contenu est présenté influe sur sa signification, il est possible de déterminer par programmation une séquence de lecture correcte.

#### Objectif – Séquence significative (1.3.2) {#purpose-meaningful-sequence}

Ce critère de réussite a pour but de permettre à un agent utilisateur de proposer une autre présentation du contenu tout en préservant l’ordre de lecture nécessaire pour comprendre sa signification. Il est important de pouvoir déterminer par programmation au moins une séquence de contenu compréhensible. Si le contenu ne répond pas à ce critère de réussite, il est possible que les utilisateurs soient troublés ou désorientés dans le cas où la technologie d’assistance lit le contenu dans le désordre ou si d’autres feuilles de style ou modifications de mise en forme sont appliquées.

#### Comment procéder – Séquence significative (1.3.2) {#how-to-meet-meaningful-sequence}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### En savoir plus - Séquence significative (1.3.2) {#more-information-meaningful-sequence}

* [Compréhension du critère de réussite 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Comment remplir le critère de réussite 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Caractéristiques sensorielles (1.3.3)    {#sensory-characteristics}

* Critère de réussite 1.3.3
* Niveau A
* Caractéristiques sensorielles : les instructions données pour la compréhension et l’utilisation du contenu ne doivent pas reposer uniquement sur les caractéristiques sensorielles des éléments comme la forme, la taille, l’emplacement visuel, l’orientation ou le son.

#### Objectif – Caractéristiques sensorielles (1.3.3)  {#purpose-sensory-characteristics}

Les concepteurs se concentrent souvent sur les fonctions de conception visuelle, telles que la couleur, la forme, le style de texte ou la position absolue ou relative d’un élément de contenu lors de la présentation des informations. Il peut s&#39;agir de techniques de conception très puissantes pour transmettre de l&#39;information (et peuvent améliorer l&#39;accessibilité globale pour les utilisateurs voyants ayant des besoins d&#39;accessibilité cognitive), mais les personnes aveugles ou malvoyantes peuvent être incapables d&#39;accéder à l&#39;information qui nécessite une identification visuelle des attributs tels que la position, la couleur ou la forme.

De même, les informations qui impliquent de distinguer différents sons (contenu verbalisé par un homme ou une femme, par exemple) présentent un obstacle à l’accessibilité pour les personnes malentendantes si elles ne sont pas reproduites dans un équivalent textuel du contenu audio.

>[!NOTE]
>
>Pour connaître les conditions requises en rapport avec les alternatives aux couleurs, voir [Utilisation de la couleur](#use-of-color).

#### Comment procéder – Caractéristiques sensorielles (1.3.3)  {#how-to-meet-sensory-characteristics}

Veillez à ce que les informations qui reposent sur des caractéristiques visuelles du contenu de la page soient également présentées dans un autre format.

* Ne vous fiez pas à la seule position visuelle pour transmettre une information. Si, par exemple, vous souhaitez renvoyer les utilisateurs à un menu sur le côté droit de la page pour accéder à d’autres informations, ne renvoyez pas au *menu à droite* ; nommez plutôt le menu (par exemple au moyen d’un titre) et faites référence à ce nom dans le texte.
* Ne vous fiez pas au style de texte (gras ou italique par exemple) comme seul moyen de transmettre l’information.

>[!NOTE]
>
>L’utilisation de termes descriptifs est acceptable s’ils ont une signification dans un contexte non visuel. Par exemple, les termes *ci-dessus* et *ci-dessous* sont généralement acceptables, puisqu’ils impliquent respectivement le contenu juste avant ou après un élément de contenu particulier ; ils resteront donc significatifs si le contenu est lu à haute voix.

#### En savoir plus – Caractéristiques sensorielles (1.3.3) {#more-information-sensory-characteristics}

* [Compréhension du critère de réussite 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Comment remplir le critère de réussite 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Distinguable (1.4)  {#distinguishable}

[Règle 1.4 – Distinguable : faciliter la perception visuelle et auditive du contenu par l’utilisateur, notamment en séparant le premier plan de l’arrière-plan.](https://www.w3.org/TR/WCAG/#distinguishable)

### Utilisation de la couleur (1.4.1)    {#use-of-color}

* Critère de réussite 1.4.1
* Niveau A
* Utilisation de la couleur : la couleur n’est pas utilisée comme la seule façon de véhiculer de l’information, d’indiquer une action, de solliciter une réponse ou de distinguer un élément visuel.

>[!NOTE]
>
>Ce critère de réussite traite spécifiquement de la perception des couleurs. Les autres formes de perception sont traitées à la règle [Adaptable (1.3)](#adaptable), comme l’accès à la couleur par programme informatique et les autres formes de codage de la présentation visuelle.

#### Objectif – Utilisation de la couleur (1.4.1)  {#purpose-use-of-color}

La couleur est un moyen évidemment efficace d’améliorer l’aspect esthétique des pages web ; elle est également utile pour véhiculer l’information. Toutefois, en raison de différentes déficiences visuelles (de la cécité au daltonisme), certaines personnes ne sont pas capables de distinguer certaines couleurs. Par conséquent, le codage en couleurs ne constitue pas un moyen fiable de véhiculer l’information.

Par exemple, une personne qui ne distingue pas le vert du rouge ne sera pas en mesure de distinguer différentes nuances de ces couleurs. Si elle voit ces couleurs comme une troisième couleur (marron par exemple), elle ne sera pas non plus en mesure de distinguer le rouge du vert et du marron.

En outre, les personnes qui utilisent des navigateurs qui ne reconnaissent que le texte, des périphériques d’affichage monochromes ou un imprimé en noir et blanc de la page ne verront pas les couleurs.

L’état *sélectionné* pour un élément d’interface (par exemple, les onglets, les boutons de bascule, etc.) doit également être transmis d’une manière autre que la couleur et au-delà d’une simple présentation visuelle. Pour ces éléments, l&#39;utilisation supplémentaire de modèles, de formes et d&#39;informations de programmation est utile lors de la création d&#39;une expérience utilisateur pleinement inclusive qui ne repose pas sur un sens spécifique.

#### Comment procéder – Utilisation de la couleur (1.4.1)  {#how-to-meet-use-of-color}

Si la couleur sert à véhiculer l’information, veillez à ce que cette information soit accessible sans recourir à la couleur.

Par exemple, assurez-vous que les informations fournies par couleur sont également fournies explicitement dans le texte.

Si la couleur est utilisée comme indice pour fournir des informations, vous devez fournir un indice visuel supplémentaire, tel que la modification du style (gras ou italique, par exemple) ou de la police. Cela aide les personnes malvoyantes ou ne percevant pas bien les couleurs à identifier l’information. Cependant, il ne peut pas être entièrement fiable, car il n’aidera pas les personnes qui ne peuvent pas voir du tout la page. Par conséquent, il est (parfois) utile de fournir du texte caché ou d&#39;utiliser des solutions programmatiques, comme la suite de normes [Web pour les applications Internet enrichies](https://www.w3.org/WAI/standards-guidelines/aria/)accessibles (ARIA), pour transmettre cette information à des utilisateurs non voyants.

#### En savoir plus – Utilisation de la couleur (1.4.1) {#more-information-use-of-color}

* [Compréhension du critère de réussite 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Comment remplir le critère de réussite 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Commande audio (1.4.2)  {#audio-control}

* Critère de réussite 1.4.2
* Niveau A
* Commande audio : si un contenu audio d’une page web est lu automatiquement pendant plus de 3 secondes, il existe, au choix, un mécanisme pour interrompre ou arrêter le contenu audio, ou un mécanisme pour commander le volume audio indépendamment du niveau de volume global du système.

#### Objectifs – Commande audio (1.4.2) {#purpose-audio-control}

Les personnes qui utilisent un logiciel de lecture d’écran peuvent avoir du mal à entendre la sortie vocale si d’autres fichiers audio sont lus en même temps. Cette difficulté est aggravée lorsque la sortie vocale du lecteur d’écran est basée sur un logiciel (comme la plupart aujourd’hui) et contrôlée par la même commande de volume que le son. De plus, certaines personnes ayant des déficiences cognitives et des personnes neurodivergentes peuvent avoir une sensibilité solide. Ces personnes ne pourront pas modifier le niveau de volume du contenu audio, ce qui sera très perturbant.

Il est donc important que l’utilisateur puisse désactiver le son en arrière-plan.

>[!NOTE]
>
>Le contrôle du volume permet de réduire son volume à zéro.

#### Comment procéder – Commande audio (1.4.2) {#how-to-meet-audio-control}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### En savoir plus – Commande audio (1.4.2) {#more-information-audio-control}

* [Compréhension du critère de réussite 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Comment remplir le critère de réussite 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contraste (minimum) (1.4.3)  {#contrast-minimum}

* Critère de réussite 1.4.3
* Niveau AA
* Contraste (minimum) : la présentation visuelle du texte et du texte sous forme d’image a un rapport de contraste d’au moins 4,5:1, sauf dans les cas suivants :
   * Texte agrandi : le texte agrandi et le texte agrandi sous forme d’image ont un rapport de contraste d’au moins 3:1.
   * Incidental: Text or images of text that are part of an inactive user interface component, that are [pure decoration](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), that are not visible to anyone, or that are part of a picture that contains significant other visual content, have no contrast requirement.
   * Logotypes : aucune exigence de contraste pour le texte faisant partie d’un logo ou d’un nom de marque.
   >[!NOTE]
   >
   >Pour plus d’informations, voir [Comprendre le contraste](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) non textuel afin de vous assurer que les auteurs de contenu comprennent les exigences supplémentaires relatives aux éléments non textuels (notamment les icônes, les éléments d’interface).

#### Objectif – Contraste (minimum) (1.4.3)  {#purpose-contrast-minimum}

Les personnes avec certaines déficiences visuelles peuvent ne pas être en mesure de distinguer certaines paires de couleurs à faible contraste. Elles peuvent être confrontées à des obstacles à l’accessibilité si :

* Le texte est faiblement contrasté avec sa couleur d’arrière-plan.
* Le codage en couleurs du texte (par exemple entre le texte du lien et le texte en dehors du lien) joue un rôle pour distinguer l’information.

>[!NOTE]
>
>Le texte simplement décoratif est exclu de ce critère de réussite.

#### Comment procéder – Contraste (minimum) (1.4.3)  {#how-to-meet-contrast-minimum}

Veillez à ce que le texte soit suffisamment contrasté par rapport à son arrière-plan. Les rapports de contraste dépendent de la taille et du style du texte en question :

* Pour le texte de moins de 18 points (ou 14 points en gras), le rapport de contraste entre le texte/les images de texte et l’arrière-plan doit être d’au moins 4.5:1.
* Pour le texte de 18 points (ou 14 points en gras) au moins, le rapport de contraste doit être d’au moins 3:1.
* Si un arrière-plan a un motif, l’arrière-plan autour du texte doit être ombré, de sorte que le rapport de 4,5:1 ou 3:1 soit préservé.

>[!NOTE]
>
>N’oubliez pas que les polices peuvent différer dans la manière dont elles restituent le dimensionnement PT/PX/EM équivalent.
>
>Il est recommandé d’utiliser un bon jugement et une erreur de lisibilité et d’utilisation lors de la sélection des polices et du dimensionnement appropriés pour le contenu Web.

>[!NOTE]
>
>Les sites suivants peuvent vous aider à convertir d’autres unités :
>
>* [Calculatrice Px to Em - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [Conversion de la taille de la police : pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com : Conversion PX/EM rendue simple](http://pxtoem.com)


Pour vérifier les rapports de contraste, utilisez un outil de contraste des couleurs, tel que l’[analyseur de contraste des couleurs du groupe Paciello](https://www.paciellogroup.com/resources/contrast-analyser.html) ou l’[outil de vérification du contraste des couleurs de webAIM](https://www.webaim.org/resources/contrastchecker/), afin de vérifier les paires de couleurs et de signaler les éventuels problèmes de contraste.

Par ailleurs, si l’aspect de votre page n’est pas un souci majeur, vous avez la possibilité de ne spécifier aucune couleur de texte de premier plan ou d’arrière-plan. Dans ce cas, il n’est pas nécessaire de vérifier le contraste, puisque le navigateur de l’utilisateur déterminera les couleurs du texte et de l’arrière-plan.

S’il n’est pas possible d’obtenir les niveaux de contraste recommandés, vous devez fournir un lien vers une version équivalente alternative de la page (qui ne présente aucun problème de contraste des couleurs) ou permettre à l’utilisateur de régler le contraste du jeu de couleurs de la page selon ses besoins.

#### En savoir plus – Contraste (minimum) (1.4.3)  {#more-information-contrast-minimum}

* [Compréhension du critère de réussite 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Comment remplir le critère de réussite 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Redimensionner le texte (1.4.4)  {#resize-text}

* Critère de réussite 1.4.4
* Niveau A
* Redimensionner le texte : à l’exception des sous-titres et des images du texte, il est possible d’effectuer, sans technologie d’assistance, un redimensionnement atteignant 200 %, sans perte de contenu ou de fonctionnalité.

#### Objectif – Redimensionner le texte (1.4.4) {#purpose-resize-text}

Ce critère de réussite a pour but de s’assurer que le texte rendu visuellement, y compris les contrôles basés sur le texte (caractères de texte affichés pour être visibles [par rapport aux caractères de texte encore sous forme de données, en ASCII par exemple]), puisse être mis à l’échelle avec succès. Il pourra ainsi être lu directement par les personnes atteintes de déficiences visuelles légères, qui n’auront pas besoin d’une technologie d’assistance, par exemple d’une loupe. Les utilisateurs peuvent bénéficier de la mise à l’échelle de tout le contenu de la page web, mais l’élément le plus crucial est le texte.

#### Comment procéder – Redimensionner le texte (1.4.4) {#how-to-meet-resize-text}

En plus de suivre les directives sous [Comment répondre aux critères de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) , vous pouvez encourager les auteurs de contenu à utiliser des largeurs et hauteurs fluides et flexibles dans leurs conceptions de page et tailles de police (par exemple, Conception Web réactive) pour permettre aux lecteurs de redimensionner le texte.

#### En savoir plus – Redimensionner le texte (1.4.4) {#more-information-resize-text}

* [Compréhension du critère de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Comment remplir le critère de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Texte sous forme d’image (1.4.5)  {#images-of-text}

* Critère de réussite 1.4.5
* Niveau AA
* Texte sous forme d’image : si les technologies utilisées peuvent réaliser la présentation visuelle, du texte est utilisé pour véhiculer l’information plutôt que du texte sous forme d’image sauf dans les cas suivants :
   * Personnalisable : le texte sous forme d’image peut être personnalisé visuellement selon les exigences de l’utilisateur.
   * Essentielle : une présentation spécifique du texte est essentielle à l’information véhiculée.

>[!NOTE]
>
>Les logotypes (le texte qui fait partie d’un logo ou d’un nom de marque) sont considérés comme essentiels.

#### Objectif – Texte sous forme d’image (1.4.5)  {#purpose-images-of-text}

Le texte sous forme d’image est souvent utilisé lorsqu’un style particulier de texte est nécessaire, tel un logotype ou si le texte a été généré à partir d’une autre source (par exemple la copie numérisée d’un document papier). Toutefois, par rapport au texte présenté en code HTML ou stylisé à l’aide d’une feuille de style CSS, il n’est pas possible de modifier la taille ou l’aspect du texte sous forme d’image, ce qui peut être nécessaire pour les personnes malvoyantes ou ayant des difficultés de lecture.

#### Comment procéder – Texte sous forme d’image (1.4.5)  {#how-to-meet-images-of-text}

Si des images de texte doivent être utilisées, utilisez CSS pour remplacer les images de texte par du texte équivalent en HTML afin que le texte soit disponible de manière personnalisable. Pour un exemple sur la manière d’y parvenir, reportez-vous à [C30: Using CSS to replace text with images of text and providing user interface controls to switch](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### En savoir plus – Texte sous forme d’image (1.4.5) {#more-information-images-of-text}

* [Compréhension du critère de réussite 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Comment remplir le critère de réussite 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Principe 2 : utilisable  {#principle-operable}

[Principe 2 : utilisable – Les composants de l’interface utilisateur et de navigation doivent être utilisables.](https://www.w3.org/TR/WCAG/#operable)

### Accessibilité au clavier (2.1) {#keyboard-accessible}

[Règle 2.1 – Accessibilité au clavier : rendre toutes les fonctionnalités disponibles à partir du clavier.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

Il s’agit de veiller à ce que les utilisateurs puissent accéder à toutes les fonctionnalités à l’aide du clavier.

### Clavier (2.1.1)  {#keyboard}

* Critère de réussite 2.1.1
* Niveau A
* Clavier : toutes les fonctionnalités du contenu sont exploitables à l’aide d’une interface clavier, sans nécessiter de minutage spécifique pour les touches individuelles, sauf lorsque la fonction sous-jacente nécessite une entrée dépendant du chemin du mouvement de l’utilisateur et pas seulement des points de terminaison.

#### Objectif - Clavier (2.1.1) {#purpose-keyboard}

Ce critère de réussite a pour but de permettre, dans la mesure du possible, d’utiliser le contenu à l’aide d’un clavier ou d’une interface de clavier (pour pouvoir utiliser un clavier supplémentaire). Si le contenu est accessible à l’aide d’un clavier ou d’un clavier alternatif, il peut être utilisé par les personnes atteintes de déficience visuelle (qui ne peuvent pas utiliser des appareils comme les souris, qui nécessitent une coordination oculaire) ou celles qui doivent utiliser des claviers alternatifs ou des périphériques d’entrée jouant le rôle d’émulateurs de clavier. Les émulateurs de clavier comprennent des logiciels de reconnaissance vocale, des logiciels de commande par le souffle, des claviers sur écran, des logiciels de numérisation, ainsi que différents claviers alternatifs et technologies d’assistance. Les personnes malvoyantes peuvent également avoir des difficultés à suivre un pointeur et trouver son contrôle bien plus facile, voir même uniquement possible, à partir du clavier.

#### Comment procéder – Clavier (2.1.1) {#how-to-meet-keyboard}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### En savoir plus – Clavier (2.1.1) {#more-information-keyboard}

* [Compréhension du critère de réussite 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Comment remplir le critère de réussite 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### Aucun piège de clavier (2.1.2)  {#no-keyboard-trap}

* Critère de réussite 2.1.2
* Niveau A
* Aucun piège de clavier : s’il est possible de déplacer le focus vers un élément de la page à l’aide d’une interface clavier, il peut être transféré ailleurs exclusivement à l’aide de l’interface clavier. Si la sélection nécessite d’autres fonctions que les touches de direction ou de tabulation non modifiées, ou d’autres méthodes de sortie standard, l’utilisateur est informé de la méthode nécessaire pour changer de focus.

#### Objectif – Aucun piège de clavier (2.1.2) {#purpose-no-keyboard-trap}

Ce critère de réussite a pour but de s’assurer que le contenu ne *piège* pas le focus au clavier dans les sous-sections du contenu d’une page web. Il s’agit d’un problème courant lorsque plusieurs formats sont combinés dans une page et générés à l’aide de plug-ins ou d’applications intégrées.

Il peut arriver que la fonctionnalité de la page Web limite la cible d’action à une sous-section du contenu (par exemple, une boîte de dialogue modale). Dans ce cas, vous devez fournir une méthode permettant à un utilisateur de quitter cette sous-section de contenu (par exemple, la touche Echap ferme la boîte de dialogue modale ou un bouton Fermer ferme la boîte de dialogue modale).

#### Comment procéder – Aucun piège de clavier (2.1.2) {#how-to-meet-no-keyboard-trap}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### En savoir plus – Aucun piège de clavier (2.1.2) {#more-information-no-keyboard-trap}

* [Compréhension du critère de réussite 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Comment remplir le critère de réussite 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### Accorder un temps suffisant (2.2) {#enough-time}

[Règle 2.2 – Accorder un temps suffisant : donner aux utilisateurs suffisamment de temps pour lire et utiliser le contenu.](https://www.w3.org/TR/WCAG/#enough-time)

Il s’agit de s’assurer que les utilisateurs disposent d’un temps suffisant pour lire et agir.

### Réglage du minutage (2.2.1)  {#timing-adjustable}

* Critère de réussite 2.2.1
* Niveau A
* Clavier : accorder aux utilisateurs un temps suffisant pour lire et utiliser le contenu.

#### Objectif – Réglage du minutage (2.2.1) {#purpose-timing-adjustable}

Ce critère de réussite a pour but de s’assurer que les utilisateurs en situation de handicap disposent, chaque fois que possible, du temps nécessaire pour interagir avec le contenu web. Les personnes atteintes de déficiences visuelles (cécité, malvoyance, troubles de la dextérité) et de limitations cognitives peuvent avoir besoin d’un temps supplémentaire pour lire le contenu ou pour mettre en œuvre certaines fonctions, comme compléter des formulaires en ligne. Si les fonctions web dépendent du temps, il sera difficile pour certains utilisateurs d’effectuer l’action requise avant qu’une limite de temps soit atteinte. Dans ce cas, le service leur est inaccessible. La conception de fonctions indépendantes du temps aidera les personnes en situation de handicap à accomplir ces fonctions. La disponibilité d’options permettant de désactiver les limites de temps, de personnaliser la durée ou de demander du temps supplémentaire avant d’atteindre une limite de temps aide les utilisateurs qui en ont besoin à accomplir leurs tâches avec succès. Ces options sont répertoriées dans l’ordre le plus pratique pour l’utilisateur. Désactiver les limites de temps est préférable à la personnalisation de la durée, elle-même préférable à l’octroi d’un temps supplémentaire avant d’atteindre une limite de temps.

#### Comment procéder – Réglage du minutage (2.2.1) {#how-to-meet-timing-adjustable}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### En savoir plus – Réglage du minutage (2.2.1) {#more-information-timing-adjustable}

* [Compréhension du critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Comment remplir le critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Mettre en pause, arrêter, masquer (2.2.2)    {#pause-stop-hide}

* Critère de réussite 2.2.2
* Niveau A
* Mettre en pause, arrêter, masquer : pour toute information en mouvement, clignotante, défilante ou mise à jour automatiquement, tous les points suivants sont vrais :
   * déplacement, clignotement, défilement : pour toute information en mouvement, clignotante ou défilante qui (a) démarre automatiquement, (b) dure plus de cinq secondes et (c) est présentée conjointement avec un autre contenu, il y a un mécanisme à la disposition de l’utilisateur pour la mettre en pause, l’arrêter ou la masquer, à moins que le mouvement, le clignotement ou le défilement s’avère un élément essentiel au bon déroulement de l’activité ; et
   * mise à jour automatique : pour toute information mise à jour automatiquement qui (a) démarre automatiquement et (b) est présentée conjointement avec un autre contenu, il y a un mécanisme à la disposition de l’utilisateur pour la mettre en pause, l’arrêter ou pour en contrôler la fréquence des mises à jour à moins que la mise à jour automatique s’avère essentielle au bon déroulement de l’activité.

Remarques :

1. Pour les exigences relatives au contenu scintillant ou flashant, se référer à la règle Ne pas concevoir de contenu susceptible de provoquer des crises (2.3).
1. Puisque tout contenu ne satisfaisant pas ce critère de réussite peut interférer avec la capacité de l’utilisateur à exploiter la page entière, tout le contenu présent dans la page web (qu’il soit utilisé pour satisfaire d’autres critères de réussite ou non) doit satisfaire ce critère de réussite. Voir [Exigence de conformité 5 : Non-interférence](https://www.w3.org/TR/WCAG20/#cc5).
1. Il n’est pas exigé que le contenu mis à jour périodiquement par logiciel ou diffusé en flux à l’agent utilisateur conserve ou présente l’information générée ou reçue entre la mise en pause et la reprise de la présentation, puisque cela peut ne pas être techniquement possible et s’avérer trompeur dans beaucoup de situations.
1. Une animation survenant dans une phase de pré-chargement ou dans une situation similaire peut être considérée comme essentielle si aucune interaction n’est permise à tous les utilisateurs durant cette phase et si l’absence d’indication de progression est susceptible de perturber les utilisateurs ou de leur faire croire que le contenu est figé ou défectueux.

#### Objectif – Mettre en pause, arrêter, masquer (2.2.2)  {#purpose-pause-stop-hide}

Certains utilisateurs peuvent trouver le contenu qui bouge gênant, voire douloureux physiquement, ce qui rend difficile de se concentrer sur d&#39;autres parties de la page. De plus, un tel contenu peut s&#39;avérer difficile à lire pour les personnes qui ont du mal à suivre le mouvement du texte.

#### Comment procéder – Mettre en pause, arrêter, masquer (2.2.2)  {#how-to-meet-pause-stop-hide}

Selon la nature du contenu, appliquez une ou plusieurs des suggestions ci-après lorsque vous créez des pages web qui contiennent du mouvement, flashant ou clignotant :

* Fournissez un moyen de suspendre le contenu défilant pour donner aux utilisateurs suffisamment de temps pour le lire. Par exemple, les titres d’actualité, le texte mis à jour automatiquement et les carrousels d’images qui avancent automatiquement.
* Veillez à ce que le contenu qui clignote s’arrête de clignoter après cinq secondes.
* Utilisez les technologies appropriées pour afficher du contenu mobile ou clignotant qui peut être désactivé par le navigateur. Par exemple, des fichiers GIF (Graphics Interchange Format) ou APNG (Animated Portable Network Graphics).
* Fournissez un contrôle de formulaire sur la page Web pour permettre à l’utilisateur de désactiver tout le contenu mobile ou clignotant de la page.
* Si l’une des options ci-dessus n’est pas possible, fournissez un lien vers une page contenant tout le contenu, mais sans déplacement ni clignotement.

#### En savoir plus – Mettre en pause, arrêter, masquer (2.2.2)  {#more-information-pause-stop-hide}

* [Compréhension du critère de réussite 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Comment remplir le critère de réussite 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Crises et réactions physiques (2.3) {#seizures-and-physcial-reactions}

[Règle 2.3 – Crises : ne pas concevoir de contenu susceptible de provoquer des crises ou des réactions physiques.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Pas plus de trois flashs ou sous le seuil critique (2.3.1)  {#three-flashes-or-below-threshold}

* Critère de réussite 2.3.1
* Niveau A
* Pas plus de trois flashs ou sous le seuil critique : une page web doit être exempte de tout élément qui flashe plus de trois fois dans n’importe quel intervalle d’une seconde ou ce flash doit se situer sous le seuil de flash générique et le seuil de flash rouge.

>[!NOTE]
>
>Puisque tout contenu ne satisfaisant pas ce critère de réussite peut interférer avec la capacité de l’utilisateur à exploiter la page entière, tout le contenu présent dans la page web (qu’il soit utilisé pour satisfaire d’autres critères de réussite ou non) doit satisfaire ce critère de réussite. Voir [Exigence de conformité 5 : Non-interférence](https://www.w3.org/TR/WCAG/#cc5).

#### Objectif – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#purpose-three-flashes-or-below-threshold}

Il arrive que le contenu qui flashe provoque des crises de photosensibilité. En appliquant ce critère de réussite, les utilisateurs concernés peuvent accéder au contenu et en prendre connaissance sans inquiétude quant au contenu qui flashe.

#### Comment procéder – Pas plus de trois flashs ou sous le seuil critique (2.3.1)  {#how-to-meet-three-flashes-or-below-threshold}

Veillez à ce que les techniques ci-après soient appliquées :

* Veillez à ce que les composants ne flashent pas plus de trois fois dans n’importe quel intervalle d’une seconde.
* S’il n’est pas possible de remplir la condition ci-dessus, présentez le contenu qui clignote dans un *petit espace sécurisé* en pixels à l’écran. Cet espace est calculé selon une formule complexe, abordée dans la section [G176: Keeping the flashing area small enough](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176) (faire en sorte que la zone qui clignote soit suffisamment petite ; en anglais). Cette technique doit être appliquée uniquement si le contenu qui clignote est *absolument* nécessaire.

#### En savoir plus – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Compréhension du critère de réussite 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Comment remplir le critère de réussite 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navigabilité (2.4) {#navigable}

[Règle 2.4 – Navigabilité : mettre à disposition les moyens nécessaires pour aider les utilisateurs à naviguer, trouver du contenu et déterminer leur localisation.](https://www.w3.org/TR/WCAG/#navigable)

Cette règle permet de s’assurer que la navigation pour accéder au contenu soit simple et facile pour les utilisateurs.

### Contournement de blocs (2.4.1)  {#bypass-blocks}

* Critère de réussite 2.4.1
* Niveau A
* Contournement de blocs : un mécanisme permet de contourner des blocs de contenu répétés sur plusieurs pages web.

#### Objectif – Contournement de blocs (2.4.1) {#purpose-bypass-blocks}

Ce critère de réussite a pour but de permettre aux personnes qui naviguent de manière séquentielle dans le contenu d’accéder plus directement au contenu principal de la page web. Les pages web et les applications contiennent souvent du contenu qui s’affiche sur d’autres pages ou écrans. Les exemples de blocs de contenu répétés incluent, entre autres, les liens de navigation, les graphiques d’en-tête, les menus et les cadres publicitaires. Concernant cette disposition, les petites sections répétées (mots individuels, expressions, liens uniques) ne sont pas considérées comme des blocs.

#### Comment procéder – Contournement de blocs (2.4.1) {#how-to-meet-bypass-blocks}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### En savoir plus – Contournement de blocs (2.4.1) {#more-information-bypass-blocks}

* [Compréhension du critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Comment remplir le critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Titre de page (2.4.2)    {#page-titled}

* Critère de réussite 2.4.2
* Niveau A
* Titre de page : les pages web présentent un titre qui décrit leur sujet ou leur but.

#### Objectif – Titre de page (2.4.2)  {#purpose-page-titled}

Ce critère de réussite aide quiconque, en situation de handicap ou non, à identifier rapidement le contenu d’une page web sans avoir à lire la page entière. Cela s’avère particulièrement utile lorsque plusieurs pages web sont ouvertes dans des onglets de navigateur, puisque le titre de la page s’affiche dans l’onglet et est donc facile à trouver.

#### Comment procéder – Titre de page (2.4.2)  {#how-to-meet-page-titled}

Lorsqu’une nouvelle page HTML est créée dans AEM, vous pouvez spécifier le titre de la page. Assurez-vous que le titre décrit correctement le contenu et l’objectif de la page, en particulier les aspects uniques, afin que les visiteurs puissent rapidement déterminer si le contenu correspond réellement à leurs besoins.

Vous pouvez également changer le titre d’une page que vous modifiez en sélectionnant : **Informations sur la page** - **Propriétés.**

#### En savoir plus – Titre de page (2.4.2) {#more-information-page-titled}

* [Compréhension du critère de réussite 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Comment remplir le critère de réussite 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Ordre de focus (2.4.3)  {#focus-order}

* Critère de réussite 2.4.3
* Niveau A
* Ordre de focus : s’il est possible de naviguer de manière séquentielle dans une page web et que les séquences de navigation affectent la signification ou le fonctionnement, l’attribution du focus aux composants concernés obéit à un ordre préservant la signification et la maniabilité.

#### Objectif – Ordre de focus (2.4.3) {#purpose-focus-order}

Ce critère de réussite a pour but de s’assurer que, lorsque les utilisateurs naviguent de manière séquentielle dans le contenu, ils rencontrent des informations dans un ordre compatible avec la signification de ce contenu et qu’il puisse être utilisé à l’aide du clavier. Ce critère diminue la confusion en permettant aux utilisateurs de former un modèle mental cohérent du contenu. Différents ordres correspondant aux relations logiques au sein du contenu peuvent coexister. Par exemple, passer d’un composant à un formulaire en ligne composé de plusieurs champs et/ou étapes reflète les relations logiques dans le contenu.

#### Comment procéder – Ordre de focus (2.4.3) {#how-to-meet-focus-order}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### En savoir plus – Ordre de focus (2.4.3) {#more-information-focus-order}

* [Compréhension du critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Comment remplir le critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Fonction du lien (selon le contexte) (2.4.4)    {#link-purpose-in-context}

* Critère de réussite 2.4.4
* Niveau A
* Fonction du lien (selon le contexte) : la fonction de chaque lien est déterminée par le texte du lien seul ou par le texte du lien associé à un contexte du lien déterminé par un programme informatique, sauf si la fonction du lien est ambiguë pour tout utilisateur.

#### Objectif – Fonction du lien (selon le contexte) (2.4.4)  {#purpose-link-purpose-in-context}

Pour tous les utilisateurs, indépendamment de la déficience, il est essentiel d&#39;indiquer clairement la direction d&#39;un lien par le biais d&#39;un texte de lien approprié. Cela permet aux utilisateurs de décider s’ils souhaitent ou non suivre un lien. Pour les utilisateurs voyants, un texte de lien significatif est extrêmement utile lorsqu’il y a plusieurs liens sur une page (en particulier si la page est lourde de texte), car un texte de lien significatif fournit une indication plus claire de la fonctionnalité de la page de cible. Les utilisateurs de certaines technologies d’assistance, qui peuvent générer une liste de tous les liens sur une seule page, peuvent comprendre plus facilement le texte du lien hors contexte si ce texte de lien est à la fois unique et informatif. Cependant, les personnes voyantes souffrant d&#39;un handicap cognitif peuvent être perturbées si un lien ne fournit pas suffisamment d&#39;information pour décrire précisément où le lien les mènera.

#### Comment procéder – Fonction du lien (selon le contexte) (2.4.4)  {#how-to-meet-link-purpose-in-context}

Avant tout, veillez à ce que l’objectif d’un lien soit clairement décrit dans le texte du lien.

* Mauvais exemple :
   * Texte : Pour plus de détails sur nos cours du soir de l’automne 2010, cliquez ici.
   * Motif : le lien est ambigu et n’indique pas clairement sa destination.
* Bon exemple :
   * Texte : Cours du soir de l’automne 2010 – Détails.
   * Motif : il est possible d’améliorer le texte du lien en adaptant légèrement le texte et sa position.

Les liens doivent être formulés de manière cohérente sur toutes les pages, en particulier pour les barres de navigation. Si, par exemple, un lien vers une page spécifique est nommé **Publications** sur une page, il doit être nommé de la même façon sur toutes les autres pages.

Au moment de la rédaction de cet article, l&#39;utilisation des attributs de titre pose certains problèmes afin de s&#39;assurer que des liens similaires présentés sur une page fournissent des informations uniques sur la destination (par exemple, &quot;lire plus&quot; se rapporte souvent à un éventail de destinations différentes) :

* En règle générale, le texte contenu dans l’attribut de titre n’est disponible que pour les utilisateurs de la souris sous la forme d’une fenêtre contextuelle d’info-bulle et n’est pas accessible de manière cohérente à l’aide du clavier ou par les utilisateurs mobiles.
* Les lecteurs d’écran peuvent lire à haute voix les attributs de titre, mais cette fonctionnalité peut ne pas être activée par défaut ; les utilisateurs peuvent donc ne pas savoir qu’il existe un attribut de titre.
* Il est difficile de modifier l’aspect du texte d’un titre, ce qui signifie qu’il peut être difficile ou impossible de le lire pour certains utilisateurs.

Par conséquent, même si vous pouvez utiliser l’attribut de titre pour fournir plus de contexte sur un lien, vous devez connaître ses limites et ne pas l’utiliser comme alternative à un texte de lien approprié.

Si le lien est composé d’une image, veillez à ce que le texte secondaire de l’image décrive la destination du lien. Si, par exemple, une image de bibliothèque est définie comme lien vers les publications d’une personne, le texte secondaire doit indiquer **Publications de Jean Dupont** et non **Bibliothèque**.

Par ailleurs, si l’ancre du lien contient du texte qui décrit l’objet du lien en sus de l’image (et par conséquent que le texte apparaît le long de l’image), utilisez un attribut alt vide pour l’image :

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>L’extrait de code ci-dessus est une illustration ; il est recommandé d’utiliser le composant **Image**.

Bien qu&#39;il soit conseillé de fournir un texte de lien qui identifie l&#39;objectif du lien sans avoir besoin d&#39;un contexte supplémentaire, il est reconnu que ce n&#39;est pas toujours possible. Des liens sans contexte peuvent être utilisés dans les cas suivants, dont des exemples HTML se trouvent dans [Comment répondre au critère de réussite 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Si le texte du lien fait partie d’une liste de liens étroitement liés et si l’élément de liste encadrant le lien fournit suffisamment de contexte.
* Si l’objet d’un lien peut être clairement identifié dans le texte du paragraphe *précédent* (et non suivant).
* si le lien est contenu dans un tableau de données et par conséquent que l’objet du lien peut être clairement identifié dans les titres associés.
* si une liste de liens est contenue dans un jeu de titres et que le titre lui-même fournit suffisamment de contexte.
* si une liste de liens est contenue dans un lien imbriqué et que la liste parente elle-même au-dessus du lien imbriqué fournit suffisamment de contexte.

Dans certains cas, s’il existe plusieurs liens sur une page (chacun d’eux fournit la destination d’un lien avec des détails complexes mais nécessaires), il peut être nécessaire de fournir une version alternative de la page web qui affiche exactement le même contenu, mais où le texte du lien n’est pas aussi détaillé.

Toutefois, il est possible d’utiliser des scripts de sorte qu’un texte minimal soit fourni avec le lien lui-même, mais, à l’activation d’une commande appropriée placée vers le haut de la page, que le texte du lien soit *développé* afin d’afficher davantage de détails. Une approche similaire consiste à utiliser une feuille de style CSS afin de *masquer* le lien complet pour les utilisateurs voyants, tout en l’affichant dans son intégralité pour les utilisateurs d’un lecteur d’écran. Cela ne fait pas partie du sujet de ce document ; toutefois, vous en apprendrez davantage dans la section [En savoir plus – Fonction du lien (selon le contexte) (2.4.4)](#more-information-link-purpose-in-context).

#### En savoir plus – Fonction du lien (selon le contexte) (2.4.4) {#more-information-link-purpose-in-context}

* [Compréhension du critère de réussite 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [Comment remplir le critère de réussite 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### Plusieurs méthodes (2.4.5)  {#multiple-ways}

* Critère de réussite 2.4.5
* Niveau AA
* Plusieurs méthodes : différentes méthodes sont possibles pour localiser une page web dans un ensemble de pages, sauf lorsque cette page résulte d’un processus ou d’une étape de processus.

#### Objectif – Plusieurs méthodes (2.4.5) {#purpose-multiple-ways}

Ce critère de réussite a pour but de permettre aux utilisateurs de localiser le contenu de la manière la mieux adaptée à leurs besoins. Ils peuvent considérer qu’une technique est plus facile à utiliser ou plus compréhensible qu’une autre.

Même les petits sites devraient offrir aux utilisateurs un moyen de s’orienter. Pour un site comportant trois ou quatre pages, toutes liées à la page d’accueil, il peut suffire d’indiquer des liens depuis et vers la page d’accueil. Ces liens peuvent ainsi servir de carte du site.

#### Comment procéder – Multiplicité des méthodes (2.4.5) {#how-to-meet-multiple-ways}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### En savoir plus – Plusieurs méthodes (2.4.5) {#more-information-multiple-ways}

* [Compréhension du critère de réussite 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [Comment remplir le critère de réussite 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### Titres et libellés (2.4.6)  {#headings-and-labels}

* Critère de réussite 2.4.6
* Niveau AA
* Titres et libellés : les titres et les libellés décrivent le sujet ou l’objectif.

#### Objectif – Titres et libellés (2.4.6) {#purpose-headings-and-labels}

Ce critère de réussite a pour but d’aider les utilisateurs à comprendre les informations contenues dans les pages web et leur organisation. Si les titres sont clairs et descriptifs, les utilisateurs peuvent trouver plus facilement les informations qu’ils recherchent et comprendre plus aisément les relations entre les différentes parties du contenu. Les libellés descriptifs aident les utilisateurs à identifier des composants spécifiques dans le contenu.

#### Comment procéder – Titres et libellés (2.4.6) {#how-to-meet-headings-and-labels}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### En savoir plus – Titres et libellés (2.4.6) {#more-information-headings-and-labels}

* [Compréhension du critère de réussite 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [Comment remplir le critère de réussite 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### Focus visible (2.4.7)  {#focus-visible}

* Critère de réussite 2.4.7
* Niveau AA
* Focus visible : toute interface utilisateur par commande au clavier possède un mode de fonctionnement où l’indicateur de focus au clavier est visible.

#### Objectif – Focus visible (2.4.7) {#purpose-focus-visible}

Ce critère de réussite a pour but d’aider une personne à identifier l’élément auquel correspond le focus au clavier.

Il doit être possible pour une personne d’identifier, parmi plusieurs, l’élément ayant reçu le focus au clavier. S’il n’apparaît à l’écran qu’un seul contrôle activable au clavier, le critère de réussite est satisfait, car la conception visuelle ne présente qu’un seul élément activable à l’aide du clavier.

L’indication « mode de fonctionnement » du critère de réussite concerne la prise en compte des plates-formes qui n’affichent pas toujours un indicateur de focus. Ce critère de réussite s’applique, car, dans la plupart des cas, il n’existe qu’un seul mode de fonctionnement.

#### Comment procéder – Focus visible (2.4.7) {#how-to-meet-focus-visible}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### En savoir plus – Focus visible (2.4.7) {#more-information-focus-visible}

* [Compréhension du critère de réussite 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Comment remplir le critère de réussite 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Principe 3 : compréhensible  {#principle-understandable}

[Principe 3 : compréhensible – Les informations et l’utilisation de l’interface utilisateur doivent être compréhensibles.](https://www.w3.org/TR/WCAG/#understandable)

### Rendre le contenu textuel lisible et compréhensible (3.1)  {#make-text-content-readable-and-understandable}

[Règle 3.1 – Lisible : rendre le contenu textuel lisible et compréhensible](https://www.w3.org/TR/WCAG/#readable)

### Langue de la page (3.1.1)  {#language-of-page}

* Critère de réussite 3.1.1
* Niveau A
* Langue de la page : la langue par défaut de chaque page web peut être déterminée par un programme informatique.

#### Objectif – Langue de la page (3.1.1)  {#purpose-language-of-page}

Ce critère de réussite garantit que ce texte et tout autre contenu linguistique est correctement restitué. Pour les utilisateurs de lecteur d’écran, il garantit que le contenu est correctement prononcé, tandis que les navigateurs visuels sont plus susceptibles d’afficher correctement certains jeux de caractères.

#### Comment procéder – Langue de la page (3.1.1)  {#how-to-meet-language-of-page}

Pour que ce critère de réussite soit satisfait, la langue par défaut d’une page web peut être identifiée à l’aide de l’attribut `lang` dans l’élément `<html>` en haut de la page. Par exemple :

* If a page is written in English, the `<html>` element should read:
   `<html lang = “en”>`

* considérant qu&#39;une page à rendre en espagnol devrait adopter la norme suivante :
   `<html lang = “es”>`

In AEM, the default language of your page is set when creating the page, but may also be changed when editing [Page Properties](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>AEM fournit des ajustements supplémentaires pour les variations d’une langue racine ; par exemple, l&#39;anglais américain - en-us, l&#39;anglais britannique - en-gb et l&#39;anglais canadien - en-ca. Ce niveau de détail est souvent superflu pour les technologies d’assistance, mais peut être utilisé pour les variations régionales du contenu des pages.

#### En savoir plus – Langue de la page (3.1.1) {#more-information-language-of-page}

* [Compréhension du critère de réussite 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Comment remplir le critère de réussite 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Les codes reposent sur la norme ISO 639-1. Vous trouverez une liste de codes plus complète pour chaque langue sur le site [W3Schools.com](https://www.w3schools.com/tags/ref_language_codes.asp).

### Langue d’un passage (3.1.2)    {#language-of-parts}

* Critère de réussite 3.1.2
* Niveau AA
* Langue d’un passage : la langue de chaque passage ou expression du contenu peut être déterminée par un programme informatique sauf pour un nom propre, pour un terme technique, pour un mot dont la langue est indéterminée ou pour un mot ou une expression faisant partie du langage courant de la langue utilisée dans le contexte immédiat.

#### Objectif – Langue d’un passage (3.1.2)  {#purpose-language-of-parts}

Ce critère de réussite vise le même objectif que le critère de réussite [Langue de la page](#language-of-page), mais il s’applique aux pages web avec du contenu en plusieurs langues sur une seule page (par exemple, en raison de citations ou de mots empruntés peu courants).

Si une page applique ce critère de réussite, alors :

* Le logiciel de transition en braille peut insérer des caractères accentués.
* Les lecteurs d’écran prononcent les mots qui comportent des caractères spéciaux ou qui ne sont pas dans la langue par défaut identifiée au niveau de la page.
* Les outils de traduction du type Google Translate peuvent correctement traduire les mots d’une langue à une autre.

#### Comment procéder – Langue d’un passage (3.1.2)  {#how-to-meet-language-of-parts}

L’attribut `lang` peut être utilisé pour identifier les modifications dans la langue du contenu. Par exemple, une citation en allemand (code ISO 639-1 &quot;de&quot;) peut s’afficher comme suit :

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Les attributs blockquote ne sont pas pris en charge dans une instance prête à l’emploi. Il est toutefois possible de développer un composant personnalisé pour prendre cette fonction en charge.

De même, le navigateur peut restituer correctement un mot ou une expression emprunté peu courant si l’élément `span` est utilisé comme suit :

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>Il n’est pas nécessaire d’adhérer à ce critère de réussite pour les noms ou villes dans différentes langues ou lors de l’utilisation de mots ou d’expressions empruntés qui sont devenus courants dans la langue par défaut (tel que *diktat* en français).

Pour ajouter l’élément span, avec un langage approprié, vous pouvez modifier manuellement votre balisage HTML en mode d’édition source de l’éditeur de texte enrichi afin qu’il se lise comme ci-dessus. Vous pouvez également inclure l’attribut `lang`[ dans l’éditeur de texte enrichi par un administrateur système (voir Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

#### En savoir plus – Langue d’un passage (3.1.2) {#more-information-language-of-parts}

* [Compréhension du critère de réussite 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [Comment remplir le critère de réussite 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### Prévisible (3.2) {#predictable}

[Règle 3.2 – Prévisible : faire apparaître les pages web et les exploiter de manière prévisible.](https://www.w3.org/TR/WCAG/#predictable)

Il s’agit de s’assurer que les pages web sont cohérentes en termes d’aspect et de fonctionnement.

### Sur focus (3.2.1)  {#on-focus}

* Critère de réussite 3.2.1
* Niveau A
* Sur focus : lorsqu’un composant de l’interface utilisateur reçoit le focus, il ne déclenche pas de changement de contexte.

#### Objectif – Sur focus (3.2.1) {#purpose-on-focus}

Ce critère de réussite a pour but de s’assurer que les fonctionnalités sont prévisibles lorsque les visiteurs parcourent un document. Un composant capable de déclencher un événement lorsqu’il reçoit le focus ne doit pas modifier le contexte. Voici quelques exemples, non limitatifs, de changements de contextes lorsqu’un composant reçoit le focus :

* envoi automatique de formulaires lorsqu’un composant reçoit le focus ;
* lancement de nouvelles fenêtres lorsqu’un composant reçoit le focus ;
* changement de focus pour un autre composant lorsque ce composant reçoit le focus ;

Il est possible de déplacer le focus vers un contrôle à l’aide du clavier (par exemple, en accédant à un contrôle grâce à la touche de tabulation) ou à l’aide de la souris (par exemple, en cliquant sur un champ de texte). Le déplacement de la souris au-dessus d’un contrôle n’a aucun effet sur le focus, sauf si un script implémente ce comportement. Notez que pour certains types de contrôles, cliquer sur un contrôle revient à l’activer (par exemple, un bouton). Cette action peut, en retour, déclencher un changement de contexte.

#### Comment procéder – Sur focus (3.2.1) {#how-to-meet-on-focus}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### En savoir plus – Sur focus (3.2.1) {#more-information-on-focus}

* [Compréhension du critère de réussite 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [Comment remplir le critère de réussite 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### Sur entrée (3.2.2)  {#on-input}

* Critère de réussite 3.2.2
* Niveau A
* Sur entrée : la modification d’un paramètre de composant de l’interface utilisateur n’entraîne pas automatiquement un changement de contexte, sauf si l’utilisateur a été informé du comportement avant d’utiliser ce composant.

#### Objectif – Sur entrée (3.2.2) {#purpose-on-input}

Ce critère de réussite a pour but de s’assurer que la saisie de données ou la sélection d’un contrôle de formulaire a des effets prévisibles. La modification d’un paramètre de composant de l’interface utilisateur modifie l’un des aspects du contrôle, de manière persistante lorsque l’utilisateur n’interagit plus avec celui-ci. Ainsi, cocher une case, saisir du texte dans un champ ou modifier l’option sélectionnée dans un contrôle de liste modifie le paramétrage, alors que l’activation d’un lien ou d’un bouton le laisse inchangé. Les changements de contexte peuvent dérouter les utilisateurs s’ils ne les perçoivent pas aisément ou s’ils sont facilement déconcentrés par la modification. Un changement de contexte n’est approprié que s’il est évident qu’il se produit en réponse à l’action de l’utilisateur.

#### Comment procéder – Sur entrée (3.2.2) {#how-to-meet-on-input}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### En savoir plus – Sur entrée (3.2.2) {#more-information-on-input}

* [Compréhension du critère de réussite 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [Comment remplir le critère de réussite 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### Navigation cohérente (3.2.3)  {#consistent-navigation}

* Critère de réussite 3.2.3
* Niveau AA
* Navigation cohérente : les mécanismes de navigation répétés sur plusieurs pages web regroupées s’enchaînent selon le même ordre relatif à chaque répétition, sauf si l’utilisateur effectue une modification.

#### Objectif – Navigation cohérente (3.2.3) {#purpose-consistent-navigation}

Ce critère de réussite a pour but d’encourager l’utilisation d’une présentation et d’une disposition cohérentes pour les utilisateurs qui interagissent avec du contenu répété dans un ensemble de pages web et qui ont besoin de trouver à plusieurs reprises des informations ou des fonctionnalités spécifiques. Les personnes malvoyantes qui utilisent la loupe pour agrandir une petite partie de l’écran utilisent souvent des repères visuels et des limites de pages pour localiser rapidement un contenu répété. De même, la présentation d’un contenu répété dans le même ordre est importante pour les utilisateurs visuels qui font appel à leur mémoire spatiale ou à des repères visuels dans la représentation graphique pour localiser ce contenu.

Il est important de noter que l’expression « dans le même ordre » de cette section ne signifie pas l’impossibilité d’utiliser des menus connexes, des blocs de navigation secondaires ou une structure de page complémentaire. Ce critère de réussite vise plutôt à aider les utilisateurs qui interagissent avec du contenu répété sur plusieurs pages web à prévoir l’emplacement du contenu qu’ils recherchent et à le trouver plus rapidement lorsqu’ils y reviennent.

Les utilisateurs peuvent effectuer une modification de l’ordre en faisant appel à des agents utilisateur adaptatifs ou en définissant des préférences pour que les informations soient présentées de la manière la plus utile pour eux.

#### Comment procéder – Navigation cohérente (3.2.3) {#how-to-meet-consistent-navigation}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### En savoir plus – Navigation cohérente (3.2.3) {#more-information-consistent-navigation}

* [Compréhension du critère de réussite 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [Comment remplir le critère de réussite 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### Identification homogène (3.2.4)  {#consistent-identification}

* Critère de réussite 3.2.4
* Niveau A
* Identification cohérente : les composants possédant la même fonctionnalité dans un ensemble de pages web sont identifiés de manière homogène.

#### Objectif – Identification cohérente (3.2.4) {#purpose-consistent-identification}

Ce critère de réussite a pour but d’assurer une identification cohérente des composants fonctionnels qui apparaissent à plusieurs reprises dans un ensemble de pages web. L’une des stratégies des utilisateurs de lecteurs d’écran pour parcourir un site web consiste à s’appuyer abondamment sur leur connaissance des fonctions présentées sur différentes pages. Si des fonctions identiques comportent des libellés différents (ou, plus généralement, un nom accessible différent) selon les pages web, le site sera beaucoup plus difficile à utiliser. La situation peut en outre dérouter les personnes atteintes de limitations cognitives et accroître la charge en la matière. La définition de libellés cohérents facilitera le processus,

Cette homogénéité s’applique aussi aux alternatives textuelles. Si des icônes ou d’autres éléments non textuels ont la même fonctionnalité, leurs alternatives textuelles doivent également être cohérentes.

Si deux composants d’une page web possèdent la même fonctionnalité qu’un troisième composant d’une autre page appartenant à un ensemble de pages, ces trois composants doivent être cohérents. Ainsi, les deux composants présents sur la même page seront cohérents.

Bien qu’il soit souhaitable et recommandé de toujours garantir la cohérence pour une page web spécifique, le critère 3.2.4 ne traite que la cohérence d’un ensemble de pages web où un élément est répété dans plusieurs pages.

#### Comment procéder – Identification cohérente (3.2.4) {#how-to-meet-consistent-identification}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### En savoir plus – Identification cohérente (3.2.4) {#more-information-consistent-identification}

* [Compréhension du critère de réussite 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [Comment remplir le critère de réussite 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### Assistance à la saisie (3.3) {#input-assistance}

[Règle 3.3 – Assistance à la saisie : aider l’utilisateur à éviter et à corriger les erreurs de saisie.](https://www.w3.org/TR/WCAG/#input-assistance)

### Identification des erreurs (3.3.1)  {#error-identification}

* Critère de réussite 3.3.1
* Niveau A
* Identification des erreurs : si une erreur de saisie est automatiquement détectée, l’élément erroné est identifié et l’erreur est décrite à l’utilisateur dans le texte.

#### Objectif – Identification des erreurs (3.3.1) {#purpose-error-identification}

Ce critère de réussite a pour but de s’assurer que les utilisateurs sont conscients qu’une erreur s’est produite et qu’ils peuvent déterminer ce qui ne va pas. Le message d’erreur doit être aussi précis que possible. Dans le cas d’un envoi de formulaire infructueux, le réaffichage du formulaire et l’indication des champs erronés ne suffisent pas, pour certains utilisateurs, à percevoir qu’une erreur s’est produite. Les utilisateurs de lecteurs d’écran, par exemple, ne savent pas qu’une erreur s’est produite tant qu’ils n’ont pas identifié l’un des indicateurs. Il est possible qu’ils abandonnent complètement le formulaire avant d’identifier l’indicateur d’erreur, en pensant que la page n’est tout simplement pas fonctionnelle. Per the definition in WCAG, an [input error](https://www.w3.org/TR/WCAG/#dfn-input-error) is information provided by the user that is not accepted. Cela inclut :

les informations requises par la page web, mais omises par l’utilisateur, ou les informations fournies par l’utilisateur, mais non conformes au format de données requis ou aux valeurs autorisées.
Par exemple :

* l’utilisateur ne saisit pas l’abréviation appropriée dans le champ État, Région, etc.  ;
* l’utilisateur saisit une abréviation d’État non valide ;
* l’utilisateur saisit un code postal inexistant ;
* l’utilisateur saisit une date de naissance fixée à 2 ans après la date présente ;
* l’utilisateur saisit des caractères alphabétiques ou des parenthèses dans le champ de son numéro de téléphone alors que seuls les chiffres sont acceptés ;
* l’utilisateur saisit une offre inférieure à l’offre précédente ou à l’augmentation minimale pour une offre.

#### Comment procéder – Identification des erreurs (3.3.1) {#how-to-meet-error-identification}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### En savoir plus – Identification des erreurs (3.3.1) {#more-information-error-identification}

* [Compréhension du critère de réussite 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Comment remplir le critère de réussite 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Étiquettes ou instructions (3.3.2)  {#labels-or-instructions}

* Critère de réussite 3.3.2
* Niveau A
* Étiquettes ou instructions : des étiquettes sont présentées ou des instructions sont fournies quand un contenu requiert une saisie utilisateur.

#### Objectif – Étiquettes ou instructions (3.3.2)  {#purpose-labels-or-instructions}

La fourniture d’instructions pour aider les utilisateurs à remplir des formulaires est l’un des éléments essentiels pour rendre une interface conviviale. Ceci s’avère particulièrement utile pour les personnes ayant des déficiences visuelles ou cognitives qui risquent autrement d’avoir du mal à comprendre la mise en page d’un formulaire et le tri des données à fournir dans un champ particulier du formulaire.

##### Forms

Dans le projet de démonstration AEM WKND, une étiquette par défaut est ajoutée lorsque vous ajoutez un composant de formulaire, tel qu’un champ **de** texte, à la page. Ce titre par défaut dépend du type de composant. Vous pouvez ajouter votre propre titre dans les onglets **Titre et Texte** de la boîte de dialogue Modifier pour ce champ. Il est important de s’assurer que les étiquettes aident les utilisateurs à comprendre les données associées à chaque composant de formulaire.

Utilisez ce champ **Titre** pour les éléments de champ, car il fournit une étiquette accessible par les technologies d’assistance. Le simple fait d’écrire une étiquette dans le texte en regard du champ ne suffit pas.

Pour certains composants, il est également possible de masquer visuellement les étiquettes en cochant la case **Masquer le titre**. Les étiquettes masquées de cette façon restent accessibles aux technologies d’assistance, mais ne s’affichent pas à l’écran. Si cette approche est adaptée à certaines situations, il est généralement préférable d’inclure une étiquette visuelle chaque fois que cela est possible, car certains utilisateurs qui ne regardent qu’une très petite portion de l’écran (un champ à la fois) ont besoin des étiquettes pour identifier correctement le champ.

###### Boutons Image {#image-buttons}

Where image buttons are used (for example, the **Image Button** component of the WKND project) the **Title** field in the **Title and Text** tab of the edit dialog actually provides the alt text for the image, rather than the label. Ainsi, dans l’exemple ci-dessous, l’image avec le texte `Submit` comporte le texte secondaire `Submit`, ajouté à l’aide du champ **Titre** dans la boîte de dialogue de modification.

###### Groupes de champs de formulaire {#groups-of-form-fields}

In the WKND project, where there is a group of related controls, such as **Radio Group**, a title may be needed for the group, as well as individual controls. Lors de l’ajout d’un ensemble de boutons radio dans AEM, le champ **Titre** fournit le titre de ce groupe, tandis que les titres individuels sont spécifiés lors de la création des boutons radio (**Éléments**).

Cependant, il n’existe aucune association par programmation entre le titre du groupe et les boutons radio eux-mêmes. Les éditeurs de modèles doivent placer le titre dans les balises `fieldset` et `legend` nécessaires afin de créer cette association. Pour ce faire, il suffit de modifier le code source de la page. Un administrateur système peut également ajouter la prise en charge de ces éléments afin qu’ils apparaissent dans la boîte de dialogue **Propriétés du champ**[ (voir Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

###### Considérations supplémentaires pour les formulaires {#additional-considerations-for-forms}

Si les données doivent être saisies dans un format spécifique, précisez-le dans le texte du libellé. Par exemple, si une date doit être saisie au format `DD-MM-YYYY`, indiquez-le spécifiquement dans le libellé. Cela signifie que lorsque les utilisateurs de lecteurs d’écran rencontrent le champ, le libellé est automatiquement annoncé, ainsi que les informations supplémentaires sur le format.

Si la saisie d’un champ de formulaire est obligatoire, indiquez-le en utilisant le mot « obligatoire » dans le libellé. AEM ajoute un astérisque lorsqu’un champ est obligatoire, mais il serait idéal d’inclure le mot `required` dans le libellé lui-même (dans le champ **Titre** de la boîte de dialogue de modification).

Le positionnement des libellés est également important, car ils permettent de localiser les champs appropriés. Cela est tout particulièrement important lorsque l’utilisateur est confronté à un formulaire complexe. Suivez les conventions ci-dessous :

* Cases à cocher ou cases d’option :
Les libellés sont positionnés immédiatement à droite du champ.
* Tous les autres composants de formulaire (par ex., zones de texte, zones de liste modifiable) :
Les libellés sont positionnés immédiatement au-dessus ou à gauche du champ.

Dans les formulaires simples avec des fonctionnalités très limitées, un bouton `Submit` approprié peut servir de libellé pour le champ adjacent (par exemple `Search`). Cela s’avère utile dans les cas où il peut être difficile de trouver de l’espace pour le texte du libellé.

#### En savoir plus – Étiquettes ou instructions (3.3.2) {#more-information-labels-or-instructions}

* [Compréhension du critère de réussite 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Comment remplir le critère de réussite 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Suggestion d’erreur (3.3.3)  {#error-suggestion}

* Critère de réussite 3.3.3
* Niveau AA
* Clavier : si une erreur de saisie est automatiquement détectée et que des suggestions de correction sont connues, ces suggestions sont proposées à l’utilisateur, sauf si elles compromettent la sécurité ou l’objectif du contenu.

#### Objectif – Suggestion d’erreur (3.3.3) {#purpose-error-suggestion}

Ce critère de réussite a pour but de s’assurer que les utilisateurs reçoivent des suggestions appropriées pour corriger, si possible, une erreur de saisie. The WCAG definition of [input error](https://www.w3.org/TR/WCAG/#dfn-input-error) says that it is &quot;information provided by the user that is not accepted&quot; by the system. À titre d’exemples de saisies non acceptées, figurent les informations requises, mais omises par l’utilisateur, et celles fournies par l’utilisateur, mais non conformes au format de données requis ou aux valeurs autorisées.

Le critère de réussite 3.3.1 prévoit la notification des erreurs. Cependant, les personnes atteintes de limitations cognitives peuvent avoir du mal à comprendre comment corriger les erreurs. Celles atteintes de déficiences visuelles ne seront peut-être pas en mesure de déterminer exactement comment corriger l’erreur. Dans le cas d’un envoi de formulaire infructueux, les utilisateurs risquent d’abandonner faute de savoir comment corriger l’erreur, même s’ils savent qu’elle s’est produite.

L’auteur du contenu peut donner la description de l’erreur ou l’agent utilisateur peut fournir la description de l’erreur en fonction d’informations spécifiques à la technologie et déterminées par programmation.

#### Comment procéder – Suggestion d’erreur (3.3.3) {#how-to-meet-error-suggestion}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### En savoir plus – Suggestion d’erreur (3.3.3) {#more-information-error-suggestion}

* [Compréhension du critère de réussite 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [Comment remplir le critère de réussite 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### Prévention des erreurs (juridiques, financières, données) (3.3.4)  {#error-prevention-legal-financial-data}

* Critère de réussite 3.3.4
* Niveau AA
* Prévention des erreurs (juridiques, financières, données) : concernant les pages web entraînant des engagements juridiques ou des transactions financières pour l’utilisateur, qui modifient ou suppriment des données contrôlables par l’utilisateur dans les systèmes de stockage de données ou qui envoient des réponses de test de l’utilisateur, au moins l’une des conditions suivantes est vraie :

   * Réversible
Les envois sont réversibles.
   * Vérifié
Les données entrées par l’utilisateur sont analysées pour détecter les erreurs de saisie et l’utilisateur a la possibilité de les corriger.
   * Confirmé
Il existe un mécanisme pour examiner, confirmer et corriger les informations avant de finaliser l’envoi.

#### Objectif – Prévention des erreurs (juridiques, financières, données) (3.3.4) {#purpose-error-prevention-legal-financial-data}

Ce critère de réussite a pour but d’aider les utilisateurs en situation de handicap à éviter les conséquences graves d’une erreur lorsqu’ils effectuent une action qui ne peut pas être annulée. Par exemple, l’achat de billets d’avion non remboursables ou le lancement d’un ordre d’achat d’actions par le biais d’un compte de courtage sont des transactions financières assorties de graves conséquences. Si un utilisateur a commis une erreur de date pour un voyage en avion, il disposera d’un billet pour le mauvais jour, sans pouvoir l’échanger. Si l’erreur concerne un nombre d’actions à acheter, l’achat concernera davantage d’actions que prévu. Ces deux types d’erreurs impliquent des transactions immédiates, non modifiables par la suite, et qui peuvent être très coûteuses. De même, il peut s’agir d’une erreur irrémédiable si les utilisateurs modifient ou suppriment involontairement des données stockées dans une base de données, à laquelle ils auront par la suite besoin d’accéder (par exemple, leur profil de voyage complet sur un site web de voyagiste). En ce qui concerne la modification ou la suppression de données « contrôlables par l’utilisateur », l’objectif est d’empêcher la perte massive de données, par exemple la suppression d’un fichier ou d’un enregistrement. L’objectif ne consiste pas à exiger une confirmation pour chaque commande d’enregistrement ou les opérations de création ou de modification simple de documents, d’enregistrements ou d’autres données.

Les utilisateurs en situation de handicap sont plus enclins à commettre des erreurs. Les personnes atteintes de difficultés de lecture peuvent avoir tendance à transposer les chiffres et les lettres, et celles souffrant de troubles moteurs à actionner des touches par erreur. La possibilité d’annuler des actions permet aux utilisateurs de corriger une erreur pouvant avoir de graves conséquences. Pouvoir vérifier et corriger des informations donne à l’utilisateur la possibilité de détecter une erreur avant d’effectuer une action d’une portée considérable.

Les données contrôlables par l’utilisateur sont des données visibles pour lui, et qu’il peut modifier ou supprimer de manière intentionnelle. À titre d’exemple, le contrôle de ces données par un utilisateur peut consister à mettre à jour le numéro de téléphone et l’adresse indiqués dans son compte ou à supprimer d’anciennes factures enregistrées sur un site web. Il ne s’agit pas d’éléments comme les données relatives à la surveillance de moteurs de recherche et de journaux Internet que l’utilisateur ne peut pas voir ni utiliser directement.

#### Comment procéder – Prévention des erreurs (juridiques, financières, données) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### En savoir plus – Prévention des erreurs (juridiques, financières, données) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Compréhension du critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Comment remplir le critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Principe 4 : robuste {#principle-robust}

[Principe 4 : robuste – Le contenu doit être suffisamment robuste pour être interprétable par un large éventail d’agents utilisateur, y compris les technologies d’assistance.](https://www.w3.org/TR/WCAG/#robust)

### Compatible (4.1) {#compatible}

[Règle 4.1 – Compatible : optimiser la compatibilité avec les agents utilisateur actuels et futurs, y compris les technologies d’assistance.](https://www.w3.org/TR/WCAG/#compatible)

Optimiser la compatibilité avec les agents utilisateur actuels et futurs, y compris les technologies d’assistance.

### Analyse (4.1.1)  {#parsing}

* Critère de réussite 4.1.1
* Niveau A
* Analyse : dans le contenu implémenté à l’aide de langages de balisage, les éléments ont des balises de début et de fin complètes, sont imbriqués selon leurs spécifications, ne contiennent pas d’attributs de duplicata et les identifiants sont uniques, sauf si les spécifications autorisent ces fonctionnalités.

#### Objectif – Analyse (4.1.1) {#purpose-parsing}

Ce critère de réussite a pour but de s’assurer que les agents utilisateurs, y compris les technologies d’assistance, peuvent interpréter et analyser le contenu avec précision. Si le contenu ne peut pas être analysé dans une structure de données, différents agents utilisateurs pourraient le présenter différemment ou être complètement incapables de l’analyser. Certains agents utilisateurs utilisent des « techniques de réparation » pour restituer un contenu mal codé.

Comme les techniques de réparation varient d’un agent utilisateur à l’autre, les auteurs ne peuvent pas présumer que le contenu sera analysé avec précision dans une structure de données ou qu’il sera restitué correctement par des agents utilisateurs spécialisés, y compris les technologies d’assistance, à moins que le contenu ne soit créé selon les règles définies dans la grammaire formelle de cette technologie. Dans les langages de balisage, les erreurs de syntaxe d’éléments et d’attributs, ainsi que l’impossibilité de fournir des balises de début et de fin correctement imbriquées, entraînent des erreurs qui empêchent les agents utilisateurs d’analyser le contenu de manière fiable. Ainsi, le critère de réussite impose que le contenu puisse être analysé en utilisant uniquement les règles de la grammaire formelle.

#### Comment procéder – Analyse (4.1.1) {#how-to-meet-parsing}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### En savoir plus – Analyse (4.1.1) {#more-information-parsing}

* [Compréhension du critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Comment remplir le critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nom, rôle, valeur (4.1.2)  {#name-role-value}

* Critère de réussite 4.1.2
* Niveau A
* Nom, rôle, valeur : pour tous les composants de l’interface utilisateur (y compris, mais pas uniquement : éléments de formulaire, liens et composants générés par les scripts), le nom et le rôle peuvent être déterminés par programmation ; les états, propriétés et valeurs définissables par l’utilisateur peuvent être fixés par programmation ; et les agents utilisateurs peuvent être informés des modifications apportées à ces éléments, y compris les technologies d’assistance.

#### Objectif – Nom, rôle, valeur (4.1.2) {#purpose-ame-role-value}

Ce critère de réussite a pour but de s’assurer que les technologies d’assistance peuvent recueillir des informations sur le contenu, l’activer (ou le définir) et actualiser l’état des contrôles de l’interface utilisateur.

Si l’interface utilise des contrôles standard issus de technologies d’accessibilité, ce processus est simple. Si l’utilisation des éléments de l’interface utilisateur est conforme aux spécifications, les conditions de cette disposition seront remplies. (Voir les exemples relatifs au critère de réussite 4.1.2 ci-dessous)

Cependant, si des contrôles personnalisés sont créés ou si des éléments d’interface sont programmés (dans le code ou le script) avec un rôle et/ou une fonction différents de leurs caractéristiques usuelles, des mesures supplémentaires doivent être prises pour garantir que les contrôles fournissent des informations importantes aux technologies d’assistance et autorisent eux-mêmes leur contrôle par ces technologies.

L’état du focus d’un contrôle d’interface utilisateur est particulièrement important. Il est possible de déterminer cet état par programmation, et des notifications concernant le changement de focus sont envoyées aux agents utilisateurs de même qu’aux dispositifs d’assistance. Savoir si une case à cocher ou un bouton radio a été sélectionné, ou si une arborescence ou un nœud de liste réductible a été développé ou réduit, constituent d’autres exemples d’état d’un contrôle de l’interface utilisateur.

#### Comment procéder – Nom, rôle, valeur (4.1.2) {#how-to-meet-ame-role-value}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### En savoir plus – Nom, rôle, valeur (4.1.2) {#more-information-ame-role-value}

* [Compréhension du critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Comment remplir le critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
