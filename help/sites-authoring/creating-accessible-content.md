---
title: Création de contenu accessible pour Adobe Experience Manager (conformité au WCAG 2.1)
description: Utilisez AEM pour rendre le contenu Web accessible et utilisable par les personnes en situation de handicap
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '13636'
ht-degree: 100%

---

# Créer du contenu accessible (conformité WCAG 2.1) {#creating-accessible-content-wcag-conformance}

Les [Règles pour l’accessibilité des contenus web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), établies par un [groupe de travail du consortium World Wide Web](https://www.w3.org/groups/#Accessibility_Guidelines_Working_Group), constituent un ensemble de règles et de critères de réussite, indépendants de la technologie, permettant d’obtenir des contenus web accessibles et utilisables par les personnes en situation de handicap.

En introduction, le consortium propose une série de sections et de documents annexes :

* [Nouvelles fonctionnalités de WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Conformité à WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Présentation de WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Techniques relatives à WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Documents WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

En outre, voir :
* [Guide rapide relatif à WCAG 2.1](/help/managing/qg-wcag.md).
* Les [rapports de conformité à l’accessibilité pour les solutions Adobe](https://www.adobe.com/accessibility/compliance.html).
* [Configuration de l’éditeur de texte enrichi pour produire du contenu accessible](/help/sites-administering/rte-accessible-content.md)

Les règles sont classées selon trois niveaux de conformité : niveau A (le plus bas), niveau AA, et niveau AAA (le plus élevé). Pour résumer, les niveaux sont définis comme suit :

* **Niveau A :** votre site atteint un niveau minimum d’accessibilité. Pour atteindre ce niveau, tous les critères de réussite de niveau A sont satisfaits.
* **Niveau AA :** il s’agit d’un niveau d’accessibilité idéal à rechercher, dans lequel votre site atteint un niveau d’accessibilité fondamental, de sorte qu’il soit accessible à la plupart des personnes dans la plupart des situations utilisant la plupart des technologies. Pour atteindre ce niveau, tous les critères de réussite de niveau A et de niveau AA sont satisfaits.
* **Niveau AAA :** votre site atteint un très haut niveau d’accessibilité. Pour atteindre ce niveau, tous les critères de succès des niveaux A, AA, et AAA sont satisfaits.

Lors de la création de votre site, vous devez déterminer à quel niveau général il doit se conformer.

La section suivante présente les [différents aspects des règles WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) ainsi que les critères de réussite associés aux [niveaux de conformité](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) A et AA.

>[!NOTE]
>
>Dans ce document, les éléments suivants sont utilisés :
>
>* les [noms courts des règles WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) ;
>* la [numérotation utilisée dans les règles WCAG 2.1](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) afin de simplifier les références croisées avec le site web WCAG.

## Principe 1 : perceptible {#principle-perceivable}

[Principe 1 : perceptible – Les informations et les composants de l’interface utilisateur doivent être présentés aux utilisateurs sous des formes qu’ils peuvent percevoir.](https://www.w3.org/TR/WCAG/#perceivable)

### Équivalents textuels (1.1) {#text-alternatives}

[Règle 1.1 – Les équivalents textuels : ils proposent des équivalents textuels à tout contenu non textuel qui pourra alors être présenté sous d’autres formes selon les besoins de l’utilisateur ou de l’utilisatrice : grands caractères, braille, synthèse vocale, symboles ou langage simplifié.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Contenu non textuel (1.1.1) {#non-text-content}

* Critère de réussite 1.1.1
* Niveau A
* Contenu non textuel : tout contenu non textuel présenté à l’utilisateur possède un texte secondaire qui remplit une fonction équivalente sauf dans les situations énumérées ci-dessous.

#### Objectif – Contenu non textuel (1.1.1) {#purpose-non-text-content}

Les informations d’une page web peuvent être fournies dans différents formats non textuels, tels que des images, des vidéos, des animations, des tableaux et des graphiques. Les personnes non-voyantes ou ayant de graves déficiences visuelles ne peuvent pas voir les contenus non textuels. Cependant, elles peuvent accéder au contenu textuel en le faisant lire par un lecteur d’écran ou encore sous forme tactile, à l’aide d’un dispositif d’affichage en braille. Ainsi, en proposant des alternatives textuelles aux contenus graphiques, les personnes qui ne peuvent pas voir le contenu graphique peuvent accéder à une version équivalente de l’information fournie par le contenu.

Par ailleurs, les alternatives textuelles ont l’avantage de permettre l’indexation du contenu non textuel par la technologie des moteurs de recherche.

#### Comment procéder – Contenu non textuel (1.1.1) {#how-to-meet-non-text-content}

Pour les images statiques, la règle de base consiste à fournir un équivalent textuel. Cela est possible dans le champ **Texte alternatif**. Observez par exemple, le composant principal **[Image](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=fr)**.

>[!NOTE]
>
>Certains composants principaux prêts à l’emploi, tels que **[Carrousel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=fr)**, ne fournissent pas de champ **Texte de remplacement** pour ajouter des descriptions de texte de remplacement à des images individuelles. Il existe cependant le champ **Libellé** (onglet **[Accessibilité](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=fr#accessibility-tab)**) pour l’ensemble du composant.
>
>Lors de l’implémentation de ces versions pour votre instance AEM, votre équipe de développement devra configurer ces composants pour prendre en charge l’attribut `alt` afin que les auteurs et autrices puissent l’ajouter au contenu (voir [Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

Dans AEM, le champ **Texte de remplacement** doit être renseigné par défaut. Si votre image est purement décorative et que le texte secondaire est superflu, l’option **L’image est décorative** peut être sélectionnée.

#### Création d’un texte secondaire adapté {#creating-good-text-alternatives}

Il existe diverses formes de contenu non textuel. Par conséquent, la valeur du texte secondaire dépend du rôle du graphique dans la page web. Voici quelques-unes des règles de base à respecter :

* Les textes secondaires doivent être succincts, tout en communiquant clairement l’information essentielle du contenu non textuel.
* Il est préférable d’éviter les descriptions trop longues (plus de 100 caractères). Si un texte secondaire doit être plus détaillé :
   * fournissez une brève description dans le texte secondaire ;
   * proposez une description plus longue, ailleurs sur la même page ou dans une page web distincte. Créez un lien vers cette description distincte en faisant de l’image un lien ou en plaçant un lien textuel en regard de l’image.
* Le texte secondaire ne doit pas répliquer le contenu fourni sous forme de texte à proximité sur la même page. N’oubliez pas que de nombreuses images sont des illustrations de points déjà couverts dans le texte d’une page. Il existe donc peut-être un texte secondaire détaillé.
* Si le contenu non textuel est un lien vers une autre page ou un autre document et qu’il n’existe pas de texte faisant partie dudit lien, le texte secondaire de l’image doit indiquer la destination du lien. Il ne doit pas décrire l’image.
* Si le contenu non textuel est contenu dans un bouton et qu’il n’existe pas de texte faisant partie dudit bouton, le texte secondaire de l’image doit indiquer la fonctionnalité du bouton. Il ne doit pas décrire l’image.
* Il est tout à fait acceptable de spécifier un texte secondaire vide (nul) pour une image, mais uniquement si l’image n’a pas besoin de texte secondaire. Par exemple, il s’agit d’une image purement décorative ou le texte équivalent existe dans le texte de la page.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Voici quelques-uns des types spécifiques de contenu non textuel auquel un texte secondaire doit être associé :

* Photos illustratives : il s’agit de photos de personnes, d’objets ou de lieux. Il est important de réfléchir au rôle de la photo dans la page. En général, il est recommandé de décrire le contenu de l’image, car la technologie d’assistance annonce le type d’élément (par exemple, `graphic` ou `image`) ; l’utilisation d’éléments `screenshot` ou `illustration` peut clarifier les descriptions des textes secondaires, mais cela dépend du contexte. La cohérence est un facteur important. Il faut prendre la même décision pour l’ensemble de l’équipe de création et l’appliquer tout au long de l’expérience du client ou de la cliente.
* Icônes : certains petits pictogrammes (images) communiquent parfois des informations spécifiques. Ils doivent être utilisés de manière uniforme sur une page et un site. Toutes les instances de l’icône sur une page ou un site doivent avoir le même texte secondaire bref et succinct, sauf si cela duplique de manière superflue le texte adjacent.
* Graphiques et diagrammes : il représentent habituellement des données numériques. Il est donc possible de fournir un texte alternatif en fournissant, par exemple, un bref résumé des principales tendances affichées dans le graphique ou le diagramme. Si nécessaire, fournissez également une description plus détaillée dans le texte à l’aide du champ **Description** dans l’onglet des propriétés d’image **Avancées**. En outre, vous pouvez fournir les données sources sous forme tabulaire ailleurs dans la page ou le site.
* Cartes, diagrammes, organigrammes : pour les graphiques produisant des données spatiales (par exemple, pour la description des relations entre des objets ou un processus), assurez-vous que le message clé est fourni au format texte et que ces informations textuelles sont placées à proximité de chaque point de données associé. Dans le cas des cartes, il est probable que l’utilisation d’un équivalent en texte intégral ne soit pas adaptée. Toutefois, si la carte est fournie pour aider les gens à trouver leur chemin vers un emplacement donné, alors le texte secondaire de l’image de la carte peut indiquer brièvement *Carte de X*, puis donner des indications vers cet emplacement en texte à un autre endroit, dans la page ou dans le champ **Description** de l’onglet **Avancé** du composant **Image**.
* CAPTCHA : un CAPTCHA est un *test public de Turing entièrement automatisé destiné à distinguer les ordinateurs des humains*. Ce contrôle de sécurité utilisé sur les pages web pour distinguer les humains des logiciels malveillants peut toutefois entraîner des barrières à l’accessibilité. Le CAPTCHA, sous forme d’images, nécessite que les utilisateurs et utilisatrices décrivent ce qu’ils voient pour réussir le test de sécurité. Il n’est évidemment pas possible de fournir un texte secondaire à l’image. Vous devrez donc envisager d’autres solutions non graphiques. Le W3C propose quelques suggestions, telles que les suivantes :
   * Puzzles logiques
   * Utilisation de la sortie son au lieu des images
   * Comptes d’utilisateur limités et filtres de courrier indésirable
* Images d’arrière-plan : elles impliquent l’utilisation de feuilles de style en cascade CSS (Cascading Style Sheet) plutôt que de code HTML. Il est donc impossible de spécifier une valeur de texte secondaire. Par conséquent, les images d’arrière-plan ne doivent pas communiquer d’informations textuelles importantes. Sinon, ces informations doivent aussi être spécifiées dans le texte de la page. Cependant, il est important qu’un arrière-plan secondaire s’affiche si l’image ne peut pas s’afficher.

>[!NOTE]
>
>Le niveau de contraste entre l’arrière-plan et le texte au premier plan doit être suffisant. Cela est décrit de manière plus détaillée à la section [Contraste (minimum) (1.4.3)](#contrast-minimum).

#### En savoir plus – Contenu non textuel (1.1.1) {#more-information-non-text-content}

* [Compréhension du critère de réussite 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Comment remplir le critère de réussite 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Explication des CAPTCHA et alternatives par le W3C](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Média temporel (1.2) {#time-based-media}

[Règle 1.2 – Média temporel : propose des versions de remplacement aux médias temporels.](https://www.w3.org/TR/WCAG/#time-based-media)

Cette section traite du contenu web *temporel*, notamment le contenu que l’utilisateur peut lire (contenu vidéo, audio et animé, par exemple) et qui peut être pré-enregistré ou en direct.

### Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Critère de réussite 1.2.1
* Niveau A
* Contenu audio ou vidéo uniquement (pré-enregistré) : pour les médias pré-enregistrés audio uniquement et les médias pré-enregistrés vidéo uniquement, les faits suivants sont vrais, sauf lorsque l’audio ou la vidéo est un média secondaire pour le texte et qu’il est clairement marqué comme tel :
   * Contenu pré-enregistré audio uniquement : une alternative pour les médias temporels qui présentent des informations équivalentes pour le contenu pré-enregistré audio uniquement.
   * Contenu pré-enregistré vidéo uniquement : une alternative pour les médias temporels ou une piste audio qui présente des informations équivalentes pour le contenu pré-enregistré vidéo uniquement.

#### Objectif – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Les personnes suivantes peuvent rencontrer des problèmes d’accessibilité à la vidéo et à l’audio :

* les personnes malvoyantes lorsqu’il n’y a pas de bande sonore, ou que la bande sonore n’est pas suffisante pour les informer de ce qui se passe dans la vidéo ou l’animation ;
* les personnes malentendantes ou sourdes, qui ne peuvent pas entendre la bande sonore ;
* les personnes qui peuvent entendre la bande sonore, mais ne comprennent pas ce qui est dit (par exemple, parce qu’elle est dans une langue qu’elles ne comprennent pas).

Les utilisateurs et utilisatrices de navigateurs ou d’appareils qui ne prennent pas en charge la lecture de contenu dans des formats multimédias spécifiques, tels qu’Adobe Flash, peuvent également ne pas avoir accès aux contenus vidéo ou audio.

Fournir ces informations dans un format différent, tel que du texte (ou de l’audio pour une vidéo sans audio), peut les rendre accessibles aux personnes qui ne peuvent pas accéder au contenu d’origine.

#### Comment procéder – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Si le contenu est un contenu audio pré-enregistré sans vidéo (podcast par exemple) :
   * Fournissez un lien immédiatement avant ou après le contenu vers une transcription textuelle du contenu audio. La transcription doit être une page HTML avec un équivalent textuel de tout le contenu parlé et du contenu non parlé important, et indiquer en outre qui parle, avec les expressions vocales et une description du décor et de tout autre contenu audio significatif.
* Si le contenu est une animation ou une vidéo pré-enregistrée sans audio :
   * Fournissez un lien juste avant ou après le contenu vers une description textuelle équivalente des informations fournies par la vidéo
   * ou une audio-description équivalente dans un format audio couramment utilisé, tel que MP3.

>[!NOTE]
>
>Si le contenu audio ou vidéo est fourni comme alternative à un contenu existant, mais dans un autre format, sur la même page web, une autre alternative peut ne pas s’avérer nécessaire.
>
>Les règles, décrites par la section [Présentation de WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html), fournissent d’autres informations.

L’insertion d’un contenu multimédia dans vos pages web AEM est similaire à celle d’une image. Cependant, le contenu multimédia étant plus complexe qu’une image fixe, il y a de nombreux paramètres et options pour contrôler sa lecture.

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

Les personnes sourdes ou malentendantes n’auront pas accès au contenu audio, ou y auront accès avec de grandes difficultés. Les sous-titres sont des équivalents textuels au contenu audio parlé et non parlé ; ils s’affichent à l’écran au moment approprié durant la vidéo. Ils permettent aux personnes qui ne peuvent pas écouter le contenu audio de comprendre ce qui se passe.

#### Comment procéder – Sous-titres (pré-enregistrés) (1.2.2) {#how-to-meet-captions-prerecorded}

Les sous-titres peuvent être :

* intégrés : toujours visibles pendant la lecture de la vidéo ;
* non intégrés : activés ou désactivés par l’utilisateur.

Utilisez des sous-titres non intégrés chaque fois que cela est possible, car les utilisateurs et utilisatrices peuvent ainsi décider s’ils souhaitent les afficher.

Pour les sous-titres non intégrés, créez et fournissez un fichier de sous-titrage synchronisé dans un format approprié ([SMIL](https://www.w3.org/AudioVideo/), par exemple) avec le fichier vidéo. Ce guide ne décrit pas la procédure à suivre pour ce faire, mais vous trouverez des liens vers des tutoriels dans [En savoir plus – Sous-titres (pré-enregistrés) (1.2.2)](#more-information-captions-prerecorded). Pensez à inclure une note avisant les utilisateurs que des sous-titres sont disponibles pour la vidéo, ou à activer la fonctionnalité de sous-titres.

Si vous devez utiliser des sous-titres intégrés, incorporez le texte à la piste vidéo. Pour ce faire, utilisez des applications de montage vidéo qui permettent de superposer du texte sur la vidéo.

#### En savoir plus – Sous-titres (pré-enregistrés) (1.2.2) {#more-information-captions-prerecorded}

* [Compréhension du critère de réussite 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Critère de réussite 1.2.3
* Niveau A
* Audio-description ou version de remplacement pour un média temporel (pré-enregistré) : une alternative pour un média temporel ou une audio-description du contenu vidéo pré-enregistré est fournie pour un média synchronisé, sauf lorsque le média est un média secondaire pour un texte et qu’il est clairement étiqueté comme tel.

#### Objectif – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Les personnes aveugles ou malvoyantes ne pourront pas accéder au contenu si les informations contenues dans une vidéo ou une animation sont fournies sous forme visuelle seulement ou si la piste audio ne fournit pas suffisamment d’informations pour comprendre ce qui se passe visuellement.

#### Comment procéder – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Deux méthodes peuvent être adoptées pour satisfaire ce critère de réussite. Les deux sont acceptables :

1. Incluez une audio-description supplémentaire pour le contenu vidéo. Vous pouvez le faire de trois façons :
   * Pendant les pauses dans la boîte de dialogue existante, fournissez des informations sur les modifications de la scène qui ne sont pas présentées dans la piste audio existante.
   * Fournissez une nouvelle piste audio supplémentaire et facultative contenant la piste audio originale, mais aussi des informations audio supplémentaires sur les modifications dans la scène.
      * Les utilisateurs et utilisatrices peuvent permuter entre la piste audio existante (qui *ne contient pas* de description audio) et la nouvelle (qui *en comprend une*).
      * Cela évite de perturber les utilisateurs et utilisatrices qui n’ont pas besoin de la description supplémentaire.
   * Créez une deuxième version du contenu vidéo pour pouvoir ajouter des audio-descriptions plus longues. Cela permet de réduire les difficultés liées à l’ajout d’audio-descriptions détaillées entre les dialogues existants, en mettant temporairement le contenu audio et vidéo en pause aux moments appropriés. Une audio-description beaucoup plus longue peut ainsi être fournie avant que l’action ne reprenne. Comme dans l’exemple précédent, il est préférable de la fournir en tant que piste audio supplémentaire en option, afin d’éviter de perturber les utilisateurs et utilisatrices qui n’ont pas besoin de la description supplémentaire.
1. Fournissez une transcription textuelle formant un équivalent textuel adapté des éléments audio et visuels de la vidéo ou de l’animation. Il peut s’agir, si cela est approprié, d’une indication précisant qui parle, d’une description du décor, des événements, d’informations présentées visuellement ou d’expressions orales. Selon sa durée, vous pouvez placer la transcription sur la même page que la vidéo ou l’animation, ou sur une autre. Dans le deuxième cas, fournissez un lien vers la transcription à proximité de la vidéo ou de l’animation.

Les détails exacts de la création de vidéos avec description audio ne font pas partie de ce guide. La création de descriptions vidéo et audio peut prendre du temps, mais d’autres produits Adobe peuvent vous aider à accomplir ces tâches.

#### En savoir plus – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Compréhension du critère de réussite 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### Sous-titres (en direct) (1.2.4)  {#captions-live}

* Critère de réussite 1.2.4
* Niveau AA
* Sous-titres (en direct) : fournir des sous-titres pour tout contenu audio en direct, sous forme de média synchronisé.

#### Objectif – Sous-titres (en direct) (1.2.4) {#purpose-captions-live}

Ce critère de réussite est identique aux [Sous-titres (pré-enregistrés)](#captions-prerecorded), du fait qu’il résout les obstacles à l’accessibilité pour les personnes sourdes ou malentendantes ; toutefois, il traite des présentations en direct du type webcast.

#### Comment procéder – Sous-titres (en direct) (1.2.4) {#how-to-meet-captions-live}

Suivez les instructions de la section [Sous-titres (pré-enregistrés)](#captions-prerecorded) ci-dessus. Toutefois, étant donné qu’il s’agit de média en direct, les sous-titres doivent être créés aussi vite que possible et en fonction de ce qui se passe dans la vidéo. Par conséquent, vous devez envisager d’utiliser des outils de sous-titrage en temps réel ou de transcription audio en texte.

Ce document ne vise pas à fournir des instructions détaillées à ce sujet, mais vous trouverez des renseignements utiles en suivant les liens ci-après :

* [WebAIM : Real Time Captioning (sous-titrage en temps réel ; en anglais)](https://webaim.org/techniques/captions/realtime)

* [Projet AccessComputing (University of Washington) : est-il possible de générer des sous-titres automatiquement à l’aide de la reconnaissance vocale ?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### En savoir plus – Sous-titres (en direct) (1.2.4) {#more-information-captions-live}

* [Compréhension du critère de réussite 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Comment remplir le critère de réussite 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Audio-description (préenregistrée) (1.2.5)   {#audio-description-prerecorded}

* Critère de réussite 1.2.5
* Niveau AA
* Audio-description (pré-enregistrée) : une description audio est fournie pour tout le contenu vidéo pré-enregistré dans les médias synchronisés.

#### Objectif – Audio-description (pré-enregistrée) (1.2.5) {#purpose-audio-description-prerecorded}

Ce critère de réussite est identique au critère [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audio-description-or-media-alternative-prerecorded), excepté que les auteurs doivent fournir une audio-description beaucoup plus détaillée, conforme au niveau AA.

#### Comment procéder – Audio-description (pré-enregistrée) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Suivez les instructions de la section [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audio-description-or-media-alternative-prerecorded).

#### En savoir plus – Audio-description (pré-enregistrée) (1.2.5) {#more-information-audio-description-prerecorded}

* [Compréhension du critère de réussite 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adaptable (1.3) {#adaptable}

[Règle 1.3 - Adaptable : créer un contenu qui puisse être présenté de différentes manières sans perte d’information ni de structure (par exemple avec une mise en page simplifiée).](https://www.w3.org/TR/WCAG/#adaptable)

Cette règle couvre les exigences nécessaires pour proposer un contenu adapté aux personnes qui :

* peuvent ne pas être en mesure d’accéder aux informations présentées par un auteur dans la présentation par défaut de ce contenu (par exemple, une mise en page à plusieurs colonnes ou une page utilisant intensivement des couleurs et/ou des images).

* utilisent peut-être un contenu audio uniquement ou un affichage visuel de remplacement, par exemple un contraste élevé ou une grande taille de texte.

### Informations et relations (1.3.1)  {#info-and-relationships}

* Critère de réussite 1.3.1
* Niveau A
* Informations et relations : les informations, la structure et les relations de la présentation peuvent être déterminées par programmation ou sont disponibles dans le texte.

#### Objectif – Informations et relations (1.3.1) {#purpose-info-and-relationships}

Nombre des technologies d’assistance auxquelles ont recours les personnes en situation de handicap s’appuient sur des informations structurelles pour afficher efficacement le contenu ou le rendre plus *intelligible*. Ces informations structurelles peuvent se présenter sous forme de titres de page, de lignes de tableau, de titres de colonne et de types de liste. Par exemple, un utilisateur peut recourir à un lecteur d’écran pour parcourir une page d’un titre à un autre. Cependant, si le contenu d’une page semble s’appuyer exclusivement sur une structure de style visuel plutôt que sur le code HTML sous-jacent, aucune information structurelle n’est disponible pour les technologies d’assistance, ce qui limite leur capacité à faciliter la navigation.

Ce critère de réussite vise à garantir que de telles informations structurelles sont fournies par programmation dans le code HTML, ou d’autres techniques de codage, de sorte que les navigateurs et les technologies d’assistance puissent y accéder pour les exploiter.

#### Comment procéder – Informations et relations (1.3.1) {#how-to-meet-info-and-relationships}

AEM facilite la construction de pages web significatives au sens sémantique à l’aide des éléments HTML appropriés. Ouvrez le contenu de la page dans l’éditeur de texte enrichi (un composant de texte) et, à l’aide du menu **Paraformat** (symbole du paragraphe), spécifiez l’élément structurel approprié (paragraphe et en-tête, par exemple).

Vous pouvez veiller à ce que vos pages web aient la structure appropriée en utilisant, si besoin, les éléments suivants :

* **En-têtes :** tant que les fonctionnalités d’accessibilité de l’éditeur de texte enrichi sont activées, AEM offre trois niveaux d’en-tête de page. Vous pouvez les utiliser pour identifier les sections et sous-sections de contenu. En-tête 1 est le plus haut niveau d’en-tête, En-tête 3 le plus bas. L’administrateur système peut configurer le système pour autoriser l’utilisation d’un plus grand nombre de niveaux d’en-tête.

* **Listes** : vous pouvez spécifier trois types de listes différents en HTML :
   * L’élément `<ul>` est utilisé pour les listes *non triées* (à puces). Les éléments de liste individuels sont identifiés à l’aide de l’élément `<li>`. Dans l’éditeur de texte enrichi, cliquez sur l’icône **Liste à puces**.
   * L’élément `<ol>` est utilisé pour les listes *numérotées*. Les éléments de liste individuels sont identifiés à l’aide de l’élément `<li>`. Dans l’éditeur de texte enrichi, cliquez sur l’icône **Liste numérotée**.

  Pour modifier le contenu existant d’un type de liste particulier, surlignez le texte concerné, puis sélectionnez le type de liste approprié. Comme dans l’exemple précédent illustrant la saisie du texte du paragraphe, les éléments de liste appropriés sont automatiquement ajoutés au fichier HTML.

  En mode Plein écran, les icônes **Liste à puces** et **Liste numérotée** sont visibles. Lorsque vous n’êtes pas en mode Plein écran, les deux options sont disponibles derrière l’icône **Listes** unique.

* **Tableaux** : les tableaux de données doivent être identifiés à l’aide des éléments de tableau HTML :
   * un élément `<table>` ;
   * un élément `<tr>` pour chaque ligne du tableau ;
   * un élément `<th>` pour chaque en-tête de ligne et de colonne ;
   * un élément `<td>` pour chaque cellule de données.

  En outre, les tableaux accessibles utilisent les éléments et attributs suivants :

   * L’élément `<caption>` sert à fournir un sous-titre visible pour le tableau. Les légendes apparaissent par défaut centrées au-dessus du tableau, mais peuvent être positionnées de manière appropriée à l’aide de CSS. La légende est associée au tableau par programmation, ce qui en fait une méthode utile pour fournir une introduction au contenu.
   * L’élément `<summary>` aide les utilisateurs non voyants à comprendre plus facilement les informations présentées dans un tableau, en fournissant une synthèse de ce qu’un utilisateur voyant peut voir. Cela s’avère particulièrement utile lors de l’utilisation de mises en page de tableau complexes ou non conventionnelles (cet attribut n’est pas affiché dans le navigateur, il est uniquement lu pour les technologies d’assistance).
   * L’attribut `scope` de l’élément `<th>` sert à indiquer si une cellule représente un en-tête pour une ligne ou une colonne particulière. Une approche similaire consiste à utiliser les attributs header et id dans des tableaux complexes, où les cellules de données peuvent être associées à un ou plusieurs en-têtes.

  >[!NOTE]
  >
  >Par défaut, ces éléments et attributs ne sont pas directement disponibles, mais l’administrateur du système peut ajouter la prise en charge de ces valeurs dans la boîte de dialogue **Propriétés du tableau[ (voir** Ajout de la prise en charge des éléments et attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

  Pour ouvrir la boîte de dialogue **Tableau** dans laquelle vous pouvez sélectionner l’onglet **Propriétés du tableau** :

   * Définissez une **légende** appropriée.
   * Idéalement, supprimez toutes les valeurs par défaut pour **Largeur**, **Hauteur**, **Bordure**, **Marge intérieure des cellules** et **Espacement des cellules**. En effet, ces propriétés peuvent être définies dans une feuille de style globale.

  Vous pouvez ensuite utiliser les **propriétés de cellule** pour définir si la cellule est une cellule de données ou d’en-tête :

* **Mise en évidence** : utilisez l’élément `<strong>` ou `<em>` pour indiquer la mise en évidence. N’utilisez pas d’en-têtes pour mettre le texte en évidence au sein des paragraphes.
   * Surlignez le texte à mettre en évidence ;
   * Cliquez sur l’icône **B** (pour `<strong>`) ou l’icône **I** (pour `<em>`) affichée dans le panneau **Propriétés** (assurez-vous que HTML est sélectionné).

     >[!NOTE]
     >
     >Dans une installation AEM standard, l’éditeur de texte enrichi est configuré pour utiliser :
     >
     >* `<b>` pour `<strong>`
     >* `<i>` pour `<em>`
     >
     >Ils sont identiques dans la pratique, mais `<strong>` et `<em>` sont préférables, car il s’agit de code HTML correct sémantiquement. Votre équipe de développement peut configurer l’éditeur de texte enrichi pour qu’il utilise `<strong>` et `<em>` (au lieu de `<b>` et `<i>`) lors du développement de votre instance de projet.

* **Tableaux de données complexes** : dans certains cas, lorsqu’il existe des tableaux complexes comportant deux niveaux ou plus d’en-têtes, les propriétés de base du tableau peuvent ne pas suffire à fournir toutes les informations structurelles nécessaires. Pour ce type de tableaux complexes, il est nécessaire de créer des relations directes entre les en-têtes et leurs cellules associées à l’aide des attributs **en-tête** et **ID**.

  >[!NOTE]
  >
  >L’attribut id n’est pas disponible dans une installation prête à l’emploi. Il peut être activé en configurant les règles HTML et le sérialiseur dans l’éditeur de texte enrichi.

  Par exemple, dans le tableau ci-dessous, les attributs header et id correspondent de façon à créer une association de programmation pour les utilisateurs de technologies d’assistance.

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

  Dans AEM, ajoutez les balises directement à l’aide du mode d’édition de la source.

  >[!NOTE]
  >
  >Cette fonctionnalité n’est pas disponible immédiatement dans une installation standard. Il faut pour cela configurer l’éditeur de texte enrichi, les règles de HTML et le sérialiseur.

#### En savoir plus – Informations et relations (1.3.1) {#more-information-info-and-relationships}

* [Compréhension du critère de réussite 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Comment remplir le critère de réussite 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Séquence significative (1.3.2)  {#meaningful-sequence}

* Critère de réussite 1.3.2
* Niveau A
* Séquence significative : lorsque la séquence dans laquelle le contenu est présenté influe sur sa signification, il est possible de déterminer par programmation une séquence de lecture correcte.

#### Objectif – Séquence significative (1.3.2) {#purpose-meaningful-sequence}

Ce critère de succès a pour but de permettre à un agent utilisateur de proposer une autre présentation du contenu tout en préservant l’ordre de lecture nécessaire pour comprendre sa signification. Il est important de pouvoir déterminer par programmation au moins une séquence de contenu compréhensible. Si le contenu ne répond pas à ce critère de succès, il est possible que les utilisatrices et les utilisateurs soient troublés ou désorientés dans le cas où la technologie d’assistance lit le contenu dans le désordre ou si d’autres feuilles de style ou modifications de mise en forme sont appliquées.

#### Comment procéder – Séquence significative (1.3.2) {#how-to-meet-meaningful-sequence}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### En savoir plus - Séquence significative (1.3.2) {#more-information-meaningful-sequence}

* [Compréhension du critère de réussite 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Comment remplir le critère de réussite 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Caractéristiques sensorielles (1.3.3)  {#sensory-characteristics}

* Critère de réussite 1.3.3
* Niveau A
* Caractéristiques sensorielles : les instructions données pour la compréhension et l’utilisation du contenu ne doivent pas reposer uniquement sur les caractéristiques sensorielles des éléments comme la forme, la taille, l’emplacement visuel, l’orientation ou le son.

#### Objectif – Caractéristiques sensorielles (1.3.3) {#purpose-sensory-characteristics}

Les concepteurs et conceptrices concentrent généralement leurs efforts sur le côté visuel (couleur, forme, style du texte, ou position absolue ou relative d’un élément du contenu) de la présentation des informations. Même s’il peut s’agir de techniques de conception très efficaces pour véhiculer l’information (et améliorer l’accessibilité générale pour les utilisateurs et utilisatrices sans handicap visuel, mais ayant besoin d’une meilleure accessibilité cognitive), les personnes aveugles ou malvoyantes peuvent ne pas être en mesure d’accéder à l’information nécessitant une identification visuelle des attributs (position, couleur ou forme, par exemple).

De la même manière, les informations qui impliquent de distinguer différents sons (contenu verbalisé par un homme ou une femme, par exemple) présentent un obstacle à l’accessibilité pour les personnes malentendantes si elles ne sont pas reproduites dans un équivalent textuel du contenu audio.

>[!NOTE]
>
>Pour connaître les conditions requises en rapport avec les alternatives aux couleurs, voir [Utilisation de la couleur](#use-of-color).

#### Comment procéder – Caractéristiques sensorielles (1.3.3) {#how-to-meet-sensory-characteristics}

Assurez-vous que toutes les informations qui reposent sur les caractéristiques visuelles du contenu de la page sont également présentées dans un autre format.

* Ne vous fiez pas à la position visuelle pour donner des informations. Par exemple, si vous souhaitez renvoyer les utilisateurs et les utilisatrices vers un menu sur le côté droit de la page pour accéder à des informations supplémentaires, ne faites pas référence au *menu de droite* ; au lieu de cela, nommez le menu (par exemple au moyen d’un en-tête) et faites référence à ce nom dans le texte.
* Ne vous limitez pas au style de texte (texte en gras ou en italique, par exemple) comme seul moyen de transmettre l’information.

>[!NOTE]
>
>L’utilisation de termes descriptifs est acceptable s’ils ont une signification dans un contexte non visuel. Par exemple, les termes *ci-dessus* et *ci-dessous* sont généralement acceptables, puisqu’ils impliquent respectivement le contenu juste avant ou après un élément de contenu particulier ; ils restent donc significatifs si le contenu est lu à haute voix.

#### En savoir plus – Caractéristiques sensorielles (1.3.3) {#more-information-sensory-characteristics}

* [Compréhension du critère de réussite 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Comment remplir le critère de réussite 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Perceptible (1.4) {#distinguishable}

[Règle 1.4 – Perceptible : faciliter la perception visuelle et auditive du contenu par l’utilisateur, notamment en séparant le premier plan de l’arrière-plan.](https://www.w3.org/TR/WCAG/#distinguishable)

### Utilisation de la couleur (1.4.1)  {#use-of-color}

* Critère de réussite 1.4.1
* Niveau A
* Utilisation de la couleur : la couleur n’est pas utilisée comme seul moyen visuel de transmettre des informations, d’indiquer une action, de demander une réponse ou de distinguer un élément visuel.

>[!NOTE]
>
>Ce critère de réussite traite spécifiquement de la perception des couleurs. Les autres formes de perception sont traitées dans la règle [Adaptable (1.3)](#adaptable), incluant l’accès à la couleur via un programme informatique et les autres formes de codage de la présentation visuelle.

#### Objectif - Utilisation de la couleur (1.4.1) {#purpose-use-of-color}

La couleur est un moyen efficace d’améliorer l’aspect esthétique des pages web et est également utile pour véhiculer l’information. Cependant, il existe une plage de déficiences visuelles, de la cécité au daltonisme, ce qui signifie que certaines personnes sont incapables de distinguer certaines couleurs. Cela fait du codage par couleur un moyen peu fiable de fournir des informations.

Par exemple, une personne ayant un daltonisme rouge-vert ne peut pas distinguer les nuances de vert et les nuances de rouge. Elle peut voir les deux couleurs comme une troisième couleur (marron, par exemple). Dans ce cas, elle ne peut pas distinguer le rouge, le vert et le marron.

En outre, les personnes qui utilisent des navigateurs de texte seul, des appareils d’affichage monochromes ou qui visualisent une impression en noir et blanc de la page ne peuvent pas percevoir les couleurs.

De plus, l’état *sélectionné* d’un élément d’interface (par exemple, les onglets, boutons (bascule), etc.) doit également être transmis d’une autre manière que par la couleur, et au-delà de la seule présentation visuelle. Pour ces éléments, l’utilisation supplémentaire de modèles, de formes et d’informations de programmation est utile pour créer une expérience utilisateur pleinement inclusive non limitée à un sens spécifique.

#### Comment procéder – Utilisation de la couleur (1.4.1) {#how-to-meet-use-of-color}

Si la couleur sert à véhiculer l’information, veillez à ce que cette information soit accessible sans recourir à la couleur.

Par exemple, assurez-vous que les informations fournies par couleur sont également fournies explicitement dans le texte.

Si vous utilisez la couleur comme vecteur d’information, vous devez fournir un indice visuel supplémentaire, par exemple, en modifiant le style (gras ou italique, par exemple) ou la police. Les utilisateurs et utilisatrices daltoniens ou souffrant d’une déficience visuelle peuvent alors distinguer les informations à l’écran. Cependant, il ne peut pas être entièrement fiable, car il n’aidera pas les personnes qui ne peuvent pas voir du tout la page. Il est donc (parfois) utile de fournir du texte caché ou d’utiliser des solutions programmatiques, comme la [suite de normes web ARIA (Accessible Rich Internet Applications)](https://www.w3.org/WAI/standards-guidelines/aria/) pour transmettre cette information à des utilisateurs non voyants.

#### En savoir plus – Utilisation de la couleur (1.4.1) {#more-information-use-of-color}

* [Compréhension du critère de réussite 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Comment remplir le critère de réussite 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Commande audio (1.4.2)  {#audio-control}

* Critère de réussite 1.4.2
* Niveau A
* Commande audio : si un contenu audio d’une page web est lu automatiquement pendant plus de 3 secondes, il existe, au choix, un mécanisme pour interrompre ou arrêter le contenu audio, ou un mécanisme pour commander le volume audio indépendamment du niveau de volume global du système.

#### Objectifs – Commande audio (1.4.2) {#purpose-audio-control}

Les personnes qui utilisent un logiciel de lecture d’écran peuvent avoir du mal à entendre la sortie vocale si d’autres fichiers audio sont lus en même temps. Cette difficulté est aggravée lorsque la sortie vocale du lecteur d’écran est basée sur un logiciel (comme la plupart aujourd’hui) et contrôlée par la même commande de volume que le son. De plus, certaines personnes atteintes de déficiences cognitives ou montrant des signes de neurodivergence peuvent être sensibles au son. Ces personnes ne pourront pas modifier le niveau de volume du contenu audio, ce qui sera très perturbant.

Il est donc important que l’utilisateur puisse désactiver le son en arrière-plan.

>[!NOTE]
>
>La maîtrise du volume englobe la possibilité de réduire le son à zéro.

#### Comment procéder – Commande audio (1.4.2) {#how-to-meet-audio-control}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### En savoir plus – Commande audio (1.4.2) {#more-information-audio-control}

* [Compréhension du critère de réussite 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Comment remplir le critère de réussite 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contraste (minimum) (1.4.3) {#contrast-minimum}

* Critère de réussite 1.4.3
* Niveau AA
* Contraste (minimum) : la présentation visuelle du texte et des images du texte présente un rapport de contraste d’au moins 4,5:1, sauf dans les cas suivants :
   * Texte grand format : le texte à grande échelle et les images de texte à grande échelle ont un rapport de contraste d’au moins 3:1.
   * Texte décoratif : aucune exigence de contraste pour le texte ou le texte sous forme d’image intégré à un composant d’interface utilisateur inactif. Il s’agit d’un élément [purement décoratif](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), invisible de tous et toutes ou intégré à une partie d’une image contenant un autre contenu significatif.
   * Logotypes : aucune exigence de contraste pour le texte faisant partie d’un logo ou d’un nom de marque.

  >[!NOTE]
  >
  >Pour plus d’informations, consultez [Présentation du contraste non textuel](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) afin de vous assurer que les personnes chargées de la création de contenu comprennent les autres exigences relatives aux éléments non textuels (notamment les icônes et les éléments d’interface).

#### Objectif – Contraste (minimum) (1.4.3) {#purpose-contrast-minimum}

Les personnes avec certaines déficiences visuelles peuvent ne pas être en mesure de distinguer certaines paires de couleurs à faible contraste. Elles peuvent être confrontées à des obstacles à l’accessibilité si :

* Le texte est faiblement contrasté avec sa couleur d’arrière-plan.
* Le codage de la couleur du texte (tel que le texte du lien et le texte hors lien) est important pour distinguer les informations.

>[!NOTE]
>
>Le texte utilisé uniquement à des fins décoratives est exclu de ce critère de succès.

#### Comment procéder – Contraste (minimum) (1.4.3) {#how-to-meet-contrast-minimum}

Veillez à ce que le texte soit suffisamment contrasté par rapport à son arrière-plan. Les rapports de contraste dépendent de la taille et du style du texte en question :

* Pour le texte de moins de 18 points (ou 14 points en gras), le rapport de contraste entre le texte/les images de texte et l’arrière-plan doit être d’au moins 4.5:1.
* Pour un texte d’au moins 18 points (ou 14 points en gras), le rapport de contraste doit être d’au moins 3:1.
* Si un arrière-plan a un motif, l’arrière-plan autour du texte doit être ombré, de sorte que le rapport de 4.5:1 ou 3:1 soit préservé.

>[!NOTE]
>
>N’oubliez pas que les polices peuvent différer en matière de rendu du dimensionnement PT/PX/EM équivalent.
>
>Pour la sélection des polices et du dimensionnement appropriés du contenu web, il est recommandé de faire preuve de bon sens et de privilégier la lisibilité et la convivialité.

>[!NOTE]
>
>Les sites suivants peuvent vous aider à effectuer des conversions dans d’autres unités :
>
>* [Calculateur de Px à Em – Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* Consultez « Conversion des tailles de polices : pixel-point-em-rem-percent » à l’adresse `https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/`.
>* Consultez PMtoEM.com : conversion PX/EM simplifiée à l’adresse `http://pxtoem.com/`.

Pour vérifier les rapports de contraste, utilisez un outil de contraste des couleurs, tel que l’[analyseur de contraste des couleurs du groupe Paciello](https://www.paciellogroup.com/resources/contrast-analyser.html) ou le [vérificateur de contraste des couleurs WebAIM](https://webaim.org/resources/contrastchecker/). Ces outils vous permettent de vérifier des paires de couleurs et de signaler tout problème de contraste.

Si vous accordez moins d’importance à l’apparence de votre page, vous pouvez choisir de ne pas spécifier de couleurs de texte d’arrière-plan et de premier plan. Aucune vérification du contraste n’est requise, car le navigateur de l’utilisateur ou de l’utilisatrice détermine les couleurs du texte et de l’arrière-plan.

S’il est impossible de respecter les niveaux de contraste recommandés, fournissez un lien vers une version équivalente alternative de la page (qui ne présente aucun problème de contraste des couleurs). Vous pouvez également laisser l’utilisateur ou l’utilisatrice régler le contraste du modèle de couleurs de la page selon ses besoins.

#### En savoir plus – Contraste (minimum) (1.4.3) {#more-information-contrast-minimum}

* [Compréhension du critère de réussite 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Comment remplir le critère de réussite 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Redimensionner le texte (1.4.4)  {#resize-text}

* Critère de réussite 1.4.4
* Niveau A
* Redimensionner le texte : à l’exception des sous-titres et des images du texte, il est possible d’effectuer, sans technologie d’assistance, un redimensionnement atteignant 200 %, sans perte de contenu ou de fonctionnalité.

#### Objectif – Redimensionner le texte (1.4.4) {#purpose-resize-text}

Ce critère de réussite a pour but de s’assurer que le texte rendu visuellement, y compris les contrôles basés sur le texte (caractères de texte affichés pour être visibles [par rapport aux caractères de texte encore sous forme de données, en ASCII par exemple]), puisse être mis à l’échelle avec succès. Il pourra ainsi être lu directement par les personnes atteintes de déficiences visuelles légères, qui n’auront pas besoin d’une technologie d’assistance, par exemple d’une loupe. Les utilisateurs peuvent bénéficier de la mise à l’échelle de tout le contenu de la page web, mais l’élément le plus crucial est le texte.

#### Comment procéder – Redimensionner le texte (1.4.4) {#how-to-meet-resize-text}

En plus de suivre les directives données dans la section [Comment satisfaire le critère de succès 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text), vous pouvez encourager les personnes chargées de la création de contenu à utiliser des largeurs et hauteurs fluides et flexibles dans la conception des pages et des tailles de police (par exemple, en design web réactif) pour permettre aux lecteurs et lectrices de redimensionner le texte.

#### En savoir plus – Redimensionner le texte (1.4.4) {#more-information-resize-text}

* [Compréhension du critère de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Comment remplir le critère de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Texte sous forme d’image (1.4.5) {#images-of-text}

* Critère de réussite 1.4.5
* Niveau AA
* Texte sous forme d’image : si les technologies utilisées peuvent réaliser la présentation visuelle, du texte est utilisé pour véhiculer l’information plutôt que du texte sous forme d’image sauf dans les cas suivants :
   * Personnalisable : l’image du texte peut être personnalisée visuellement en fonction des besoins de l’utilisateur ou de l’utilisatrice.
   * Essentiel : une présentation particulière du texte est essentielle à la transmission de l’information.

>[!NOTE]
>
>Les logotypes (texte faisant partie d’un logo ou d’un nom de marque) sont considérés comme essentiels.

#### Objectif – Texte sous forme d’image (1.4.5) {#purpose-images-of-text}

Les images de texte sont souvent utilisées lorsqu’un style de texte particulier est privilégié, par exemple, un logotype ou si le texte a été généré à partir d’une autre source (la numérisation d’un document papier, par exemple). Cependant, par rapport au texte présenté au format HTML dans le style CSS, les images de texte n’offrent pas la possibilité de modifier leur taille ou leur apparence, des fonctionnalités parfois nécessaires pour les personnes avec des déficiences visuelles ou présentant des difficultés de lecture.

#### Comment procéder – Texte sous forme d’image (1.4.5) {#how-to-meet-images-of-text}

Si des images de texte doivent être utilisées, utilisez le CSS pour remplacer les images de texte par du texte équivalent en HTML afin que le texte soit disponible de manière personnalisable. Pour un exemple, consultez [C30: Using CSS to replace text with images of text and providing user interface controls to switch](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30) (C30 : utiliser le CSS pour remplacer le texte par des images de texte et fournir des commandes dans l’UI pour basculer).

#### En savoir plus – Texte sous forme d’image (1.4.5) {#more-information-images-of-text}

* [Compréhension du critère de réussite 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Comment remplir le critère de réussite 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Principe 2 : utilisable {#principle-operable}

[Principe 2 : utilisable – Les composants de l’interface utilisateur et de navigation doivent être utilisables.](https://www.w3.org/TR/WCAG/#operable)

### Accessibilité au clavier (2.1) {#keyboard-accessible}

[Règle 2.1 – Accessibilité au clavier : rendre toutes les fonctionnalités disponibles à partir du clavier.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

Il s’agit de veiller à ce que les utilisateurs puissent accéder à toutes les fonctionnalités à l’aide du clavier.

### Clavier (2.1.1)  {#keyboard}

* Critère de réussite 2.1.1
* Niveau A
* Clavier : toutes les fonctionnalités du contenu sont exploitables à l’aide d’une interface clavier, sans nécessiter de minutage spécifique pour les touches individuelles, sauf lorsque la fonction sous-jacente nécessite une entrée dépendant du chemin du mouvement de l’utilisateur et pas seulement des points d’entrée.

#### Objectif - Clavier (2.1.1) {#purpose-keyboard}

Ce critère de réussite a pour but de permettre, dans la mesure du possible, d’utiliser le contenu à l’aide d’un clavier ou d’une interface de clavier (pour pouvoir utiliser un clavier supplémentaire). Si le contenu est accessible à l’aide d’un clavier ou d’un clavier alternatif, il devient accessible aux personnes atteintes de déficience visuelle (qui ne peuvent pas utiliser des appareils comme les souris, qui nécessitent une coordination oculaire) ou celles qui doivent utiliser des claviers alternatifs ou des appareils de saisie jouant le rôle d’émulateurs de clavier. Les émulateurs de clavier comprennent des logiciels de reconnaissance vocale, des logiciels de commande par le souffle, des claviers sur écran, des logiciels de numérisation, ainsi que différents claviers alternatifs et technologies d’assistance. Les personnes malvoyantes peuvent également avoir des difficultés à suivre un pointeur et trouver l’utilisation du logiciel bien plus facile, voire simplement possible, à partir du clavier.

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

Il peut arriver que la fonctionnalité de la page web limite la cible du focus à une sous-section du contenu (par exemple, une boîte de dialogue modale). Dans ce cas, vous devez fournir une méthode permettant à un utilisateur de quitter cette sous-section de contenu (par exemple, la touche Échap ferme la boîte de dialogue modale ou un bouton Fermer ferme la boîte de dialogue modale).

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

Ce critère de réussite a pour but de s’assurer que les utilisateurs en situation de handicap disposent, chaque fois que possible, du temps nécessaire pour interagir avec le contenu web. Les personnes atteintes de déficiences visuelles (cécité, malvoyance, troubles de la dextérité) et de limitations cognitives peuvent avoir besoin d’un temps supplémentaire pour lire le contenu ou pour mettre en œuvre certaines fonctions, comme compléter des formulaires en ligne. Si les fonctions web dépendent du temps, il sera difficile pour certains utilisateurs d’effectuer l’action requise avant qu’une limite de temps soit atteinte. Dans ce cas, le service leur est inaccessible. La conception de fonctions indépendantes du temps aide les personnes en situation de handicap à accomplir ces fonctions. La disponibilité d’options permettant de désactiver les limites de temps, de personnaliser la durée ou de demander du temps supplémentaire avant d’atteindre une limite de temps aide les utilisateurs et les utilisatrices qui en ont besoin à accomplir leurs tâches. Ces options sont répertoriées dans l’ordre le plus pratique pour l’utilisateur. Désactiver les limites de temps est préférable à la personnalisation de la durée, elle-même préférable à l’octroi d’un temps supplémentaire avant d’atteindre une limite de temps.

#### Comment procéder – Réglage du minutage (2.2.1) {#how-to-meet-timing-adjustable}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### En savoir plus – Réglage du minutage (2.2.1) {#more-information-timing-adjustable}

* [Compréhension du critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Comment remplir le critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Mettre en pause, arrêter, masquer (2.2.2)  {#pause-stop-hide}

* Critère de réussite 2.2.2
* Niveau A
* Mettre en pause, arrêter, masquer : pour toute information en mouvement, clignotante, défilante ou mise à jour automatiquement, tous les points suivants sont vrais :
   * Déplacement, clignotement, défilement : pour toute information en mouvement, clignotante ou défilante qui
      * (a) démarre automatiquement,
      * (b) dure plus de cinq secondes, et
      * (c) est présentée en parallèle à d’autres contenus,
il existe un mécanisme permettant à l’utilisateur ou à l’utilisatrice de la suspendre, de l’arrêter ou de la masquer, sauf si le mouvement, le clignotement ou le défilement fait partie intégrante de l’activité.
   * Mise à jour automatique : pour toute information mise à jour automatiquement qui
      * (a) démarre automatiquement, et
      * (b) est présentée en parallèle à d’autres contenus,
il existe un mécanisme permettant à l’utilisateur ou à l’utilisatrice de la suspendre, de l’arrêter ou de la masquer, ou de contrôler la fréquence de la mise à jour, sauf si la mise à jour automatique fait partie intégrante de l’activité.

Remarques :

1. Pour les exigences relatives au contenu scintillant ou clignotant, se référer à la règle Ne pas concevoir de contenu susceptible de provoquer des crises d’épilepsie (2.3).
1. Comme tout contenu qui ne remplit pas ce critère de réussite peut interférer avec la capacité de l’utilisateur ou de l’utilisatrice à exploiter la page entière, tout le contenu présent dans la page web (qu’il soit utilisé pour remplir d’autres critères de réussite ou non) doit remplir ce critère de réussite. Consultez [Exigence de conformité 5 : non interférence](https://www.w3.org/TR/WCAG20/#cc5).
1. Le contenu mis à jour régulièrement par un logiciel ou diffusé en continu à l’utilisateur ou l’utilisatrice n’est pas tenu de conserver ou présenter des informations générées ou reçues entre la mise en pause et la reprise de la présentation. En effet, cela peut être techniquement impossible et peut induire en erreur dans de nombreuses situations.
1. Une animation dans le cadre d’une phase de préchargement ou d’une situation similaire peut être considérée comme essentielle si l’interaction ne peut pas se produire au cours de cette phase pour tous les utilisateurs et utilisatrices, et si le fait de ne pas indiquer la progression risque de dérouter les utilisateurs et les utilisatrices ou de leur faire croire que le contenu a été figé ou interrompu.

#### Objectif – Mettre en pause, arrêter, masquer (2.2.2) {#purpose-pause-stop-hide}

Certains utilisateurs et utilisatrices peuvent trouver les contenus mobiles gênants, voire douloureux physiquement, ce qui crée pour eux des difficultés à se concentrer sur d’autres parties de la page. De plus, un tel contenu peut se révéler difficile à lire pour les personnes qui ont des difficultés à suivre un texte mobile.

#### Comment procéder – Mettre en pause, arrêter, masquer (2.2.2) {#how-to-meet-pause-stop-hide}

Selon la nature du contenu, vous pouvez appliquer une ou plusieurs des suggestions suivantes lorsque vous créez des pages web qui contiennent du mouvement, des flashs ou des clignotements :

* Prévoyez un moyen de suspendre le défilement du contenu afin de donner aux utilisateurs suffisamment de temps pour le lire, par exemple, sous la forme de fils d’actualité, de texte mis à jour automatiquement et de carrousels d’images avec progression automatique.
* Veillez à ce qu’un contenu clignotant cesse de clignoter après cinq secondes.
* Utilisez les technologies appropriées pour afficher des contenus mobiles ou clignotants, désactivables par le biais du navigateur, notamment des fichiers GIF (Graphics Interchange Format) ou APNG (Animated Portable Network Graphics).
* Fournissez un contrôle de formulaire sur la page web permettant à l’utilisateur de désactiver les contenus mobiles ou clignotants sur la page.
* Si aucune des solutions ci-dessus n’est possible, fournissez un lien vers une page avec tout le contenu, mais sans mouvement ni clignotement.

#### En savoir plus – Mettre en pause, arrêter, masquer (2.2.2) {#more-information-pause-stop-hide}

* [Compréhension du critère de réussite 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Comment remplir le critère de réussite 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Crises et réactions physiques (2.3) {#seizures-and-physcial-reactions}

[Règle 2.3 – Crises : ne pas concevoir de contenu susceptible de provoquer des crises ou des réactions physiques.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#three-flashes-or-below-threshold}

* Critère de réussite 2.3.1
* Niveau A
* Pas plus de trois flashs ou sous le seuil critique : une page web doit être exempte de tout élément qui flashe plus de trois fois dans un intervalle d’une seconde ou ce flash doit se situer sous le seuil de flash générique et le seuil de flash rouge.

>[!NOTE]
>
>Comme tout contenu qui ne remplit pas ce critère de succès peut interférer avec la capacité de l’utilisateur ou de l’utilisatrice à exploiter la page entière, tout le contenu présent dans la page web (qu’il soit utilisé pour remplir d’autres critères de réussite ou non) doit remplir ce critère de succès. Consultez [Exigence de conformité 5 : non interférence](https://www.w3.org/TR/WCAG/#cc5).

#### Objectif – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#purpose-three-flashes-or-below-threshold}

Il arrive que le contenu qui flashe provoque des crises de photosensibilité. En appliquant ce critère de réussite, les utilisateurs concernés peuvent accéder au contenu et en prendre connaissance sans inquiétude quant au contenu qui flashe.

#### Comment procéder – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

Assurez-vous d’appliquer les techniques suivantes :

* assurez-vous que les composants ne flashent pas plus de trois fois au cours d’une période d’une seconde ;
* si vous ne pouvez pas remplir la condition ci-dessus, affichez le contenu clignotant dans une *petite zone sécurisée* en pixels sur l’écran. Cette zone est calculée à l’aide d’une formule complexe, couverte par la section [G176 : garder la zone de flash suffisamment petite (en anglais)](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176). Utilisez cette technique uniquement si l’utilisation de flashs est nécessaire.

#### En savoir plus – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Compréhension du critère de réussite 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Comment remplir le critère de réussite 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navigabilité (2.4) {#navigable}

[Règle 2.4 – Navigable : fournir à l’utilisateur des éléments d’orientation pour naviguer, trouver le contenu et se situer dans le site.](https://www.w3.org/TR/WCAG/#navigable)

Cette règle permet de s’assurer que la navigation pour accéder au contenu soit simple et facile pour les utilisateurs.

### Contournement de blocs (2.4.1)  {#bypass-blocks}

* Critère de réussite 2.4.1
* Niveau A
* Contournement de blocs : un mécanisme permet de contourner des blocs de contenu répétés sur plusieurs pages web.

#### Objectif – Contournement de blocs (2.4.1) {#purpose-bypass-blocks}

Ce critère de réussite a pour but de permettre aux personnes qui naviguent de manière séquentielle dans le contenu d’accéder plus directement au contenu principal de la page web. Les pages web et les applications contiennent souvent du contenu qui s’affiche sur d’autres pages ou écrans. Parmi les exemples de blocs de contenu répétés, citons, entre autres, les liens de navigation, les graphiques de titres et les encadrés publicitaires. Concernant cette disposition, les petites sections répétées (mots seuls, expressions, liens uniques) ne sont pas considérées comme des blocs.

#### Comment procéder – Contournement de blocs (2.4.1) {#how-to-meet-bypass-blocks}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### En savoir plus – Contournement de blocs (2.4.1) {#more-information-bypass-blocks}

* [Compréhension du critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Comment remplir le critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Titre de page (2.4.2)  {#page-titled}

* Critère de réussite 2.4.2
* Niveau A
* Titre de page : les pages web comportent des titres qui décrivent la rubrique ou l’objectif.

#### Objectif – Titre de page (2.4.2) {#purpose-page-titled}

Ce critère de succès permet à chacun, indépendamment d’une déficience particulière, d’identifier rapidement le contenu d’une page web sans lire la page dans son intégralité. Cela se révèle utile lorsque plusieurs pages web sont ouvertes dans des onglets de navigateur, car le titre de la page s’affiche dans l’onglet et peut donc être localisé rapidement.

#### Comment procéder – Titre de page (2.4.2) {#how-to-meet-page-titled}

Lorsqu’une nouvelle page HTML est créée dans AEM, vous pouvez spécifier son titre. Assurez-vous que le titre décrit le contenu et l’objectif de la page de manière adéquate, en particulier les aspects uniques, afin que les visiteurs et les visiteuses puissent rapidement déterminer si le contenu correspond réellement à leurs besoins.

Vous pouvez également changer le titre d’une page que vous modifiez en sélectionnant : **Informations sur la page** – **Propriétés.**

#### En savoir plus – Titre de page (2.4.2) {#more-information-page-titled}

* [Compréhension du critère de réussite 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Comment remplir le critère de réussite 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Ordre de focus (2.4.3)  {#focus-order}

* Critère de réussite 2.4.3
* Niveau A
* Ordre de focus : s’il est possible de naviguer de manière séquentielle dans une page web et que les séquences de navigation affectent la signification ou le fonctionnement, l’attribution du focus aux composants concernés obéit à un ordre préservant la signification et la maniabilité.

#### Objectif – Ordre de focus (2.4.3) {#purpose-focus-order}

Ce critère de succès a pour but de s’assurer que, lorsque les utilisateurs et les utilisatrices naviguent de manière séquentielle dans le contenu, ils rencontrent des informations dans un ordre compatible avec la signification de ce contenu et qu’il puisse être utilisé à l’aide du clavier. Ce critère diminue la confusion en permettant aux utilisateurs de former un modèle mental cohérent du contenu. Différents ordres correspondant aux relations logiques au sein du contenu peuvent coexister. Il peut s’agir, par exemple, de parcourir des composants dans un formulaire en ligne composé de différents champs et/ou étapes, en correspondance avec les relations logiques au sein du contenu.

#### Comment procéder – Ordre de focus (2.4.3) {#how-to-meet-focus-order}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### En savoir plus – Ordre de focus (2.4.3) {#more-information-focus-order}

* [Compréhension du critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Comment remplir le critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Fonction du lien (selon le contexte) (2.4.4)  {#link-purpose-in-context}

* Critère de réussite 2.4.4
* Niveau A
* Fonction du lien (selon le contexte) : la fonction de chaque lien est déterminée par le texte du lien seul ou par le texte du lien associé à un contexte du lien déterminé par un programme informatique, sauf si la fonction du lien est ambiguë pour tout utilisateur.

#### Objectif – Fonction du lien (selon le contexte) (2.4.4) {#purpose-link-purpose-in-context}

Pour tous les utilisateurs et utilisatrices, qu’ils aient une déficience ou non, il est essentiel d’indiquer clairement la direction d’un lien avec le texte du lien approprié. Cela permet aux utilisateurs et aux utilisatrices de décider s’ils souhaitent réellement suivre un lien. Pour les utilisateurs et utilisatrices voyants, un texte de lien significatif est utile lorsqu’il existe plusieurs liens sur une page (en particulier si la page contient beaucoup de texte), car il fournit une indication plus claire de la fonctionnalité de la page cible. D’un autre côté, les utilisateurs et utilisatrices de technologies d’assistance peuvent générer une liste de tous les liens sur une seule page, et ainsi comprendre plus facilement le texte du lien hors contexte, s’il est à la fois unique et informatif. Les personnes voyantes souffrant d’un handicap cognitif peuvent être perturbées si un lien ne donne pas suffisamment d’informations sur sa destination.

#### Comment procéder – Fonction du lien (selon le contexte) (2.4.4) {#how-to-meet-link-purpose-in-context}

Avant tout, veillez à ce que l’objectif d’un lien soit clairement décrit dans le texte du lien.

* Mauvais exemple :
   * Texte : Pour plus de détails sur nos cours du soir de l’automne 2010, cliquez ici.
   * Motif : le lien est ambigu et n’indique pas clairement sa destination.
* Bon exemple :
   * Texte : Cours du soir de l’automne 2010 – Détails.
   * Motif : il est possible d’améliorer le texte du lien en adaptant légèrement le texte et sa position.

Les liens doivent être formulés de manière cohérente sur toutes les pages, en particulier pour les barres de navigation. Par exemple, si un lien vers une page spécifique est nommé **Publications** sur une page, utilisez ce texte sur les autres pages pour garantir la cohérence.

Au moment de la rédaction de cet article, l’utilisation des attributs de titre pose certains problèmes. Ils ne permettent pas de s’assurer que des liens similaires présentés sur une page donnent des informations uniques sur la destination (par exemple, la mention « en savoir plus » se rapporte souvent à plusieurs destinations différentes) :

* Seuls les utilisateurs et utilisatrices d’une souris ont accès au texte contenu dans l’attribut de titre grâce à une info-bulle contextuelle ; ce texte n’est pas accessible en permanence à l’aide du clavier ou sur un téléphone mobile.
* Les lecteurs d’écran peuvent lire les attributs de titre, mais cette fonctionnalité peut ne pas être activée par défaut. Par conséquent, les utilisateurs et utilisatrices peuvent ne pas connaître l’existence d’un attribut de titre.
* Il est compliqué de changer l’aspect du texte du titre, ce qui signifie qu’il peut être difficile, voire impossible à lire pour certaines personnes.

Ainsi, bien que l’attribut de titre puisse fournir un contexte supplémentaire à un lien, gardez à l’esprit ses limites et ne l’utilisez pas comme alternative au texte du lien approprié.

Lorsque le lien est composé d’une image, assurez-vous que le texte de remplacement de l’image décrit la destination du lien. Par exemple, si une image représentant une bibliothèque est définie comme lien vers les publications d’une personne, le texte alternatif doit stipuler : **Publications de John Smith** et non **Bibliothèque**.

Si l’ancre de lien contient du texte qui décrit la destination du lien en plus de l’élément image (et donc que le texte apparaît à côté de l’image), utilisez un attribut de remplacement vide pour l’image :

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
>
>L’extrait de code ci-dessus est une illustration. Il est recommandé d’utiliser le composant d’**image**.

Bien qu’il soit conseillé de fournir un texte de lien qui identifie l’objectif du lien sans avoir besoin de contexte supplémentaire, il est à noter que ce n’est pas toujours possible. Il est possible d’utiliser des liens dépourvus de contexte dans les cas suivants. Un certain nombre d’exemples HTML figurent dans la section [Comment remplir le critère de réussite 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Le texte du lien fait partie d’une liste de liens étroitement liés et l’élément de liste encadrant le lien fournit suffisamment de contexte.
* L’objet d’un lien peut être clairement identifié dans le texte du paragraphe *précédent* (et non suivant).
* Le lien est contenu dans un tableau de données et l’objectif peut donc être clairement identifié à partir des en-têtes associés.
* Une liste de liens est contenue dans un ensemble d’en-têtes et l’en-tête lui-même fournit un contexte approprié.
* Une liste de liens est contenue dans un lien imbriqué et l’élément de liste parent situé au-dessus du lien imbriqué fournit un contexte approprié.

Parfois, lorsqu’il existe plusieurs liens sur une page (chacun d’eux fournissant la direction d’un lien avec des détails complexes mais nécessaires), il peut être approprié de fournir une version alternative de la page web qui affiche exactement le même contenu, mais avec un texte de lien moins détaillé.

Vous pouvez également utiliser des scripts, de sorte qu’une quantité minimale de texte soit fournie dans le lien lui-même. Lors de l’activation d’une commande appropriée positionnée en haut de la page, le texte du lien est *étendu* pour afficher plus de détails. Une approche similaire consiste à utiliser CSS pour *masquer* le lien complet aux utilisateurs et utilisatrices voyants, mais il est toujours affiché en plein écran pour les utilisateurs et utilisatrices de lecteurs d’écran. Bien que cette information ne relève pas du présent document, vous trouverez plus de détails sur la façon d’y parvenir dans la section [Comprendre – Fonction du lien (selon le contexte) (2.4.4)](#more-information-link-purpose-in-context).

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

Lorsque le critère de réussite indique « mode de fonctionnement », cela sert à prendre en compte des plateformes qui n’affichent pas toujours un indicateur de focus. Ce critère de succès s’applique, car, dans la plupart des cas, il n’existe qu’un seul mode de fonctionnement.

#### Comment procéder – Focus visible (2.4.7) {#how-to-meet-focus-visible}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### En savoir plus – Focus visible (2.4.7) {#more-information-focus-visible}

* [Compréhension du critère de réussite 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Comment remplir le critère de réussite 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Principe 3 : compréhensible {#principle-understandable}

[Principe 3 : compréhensible – Les informations et l’utilisation de l’interface utilisateur doivent être compréhensibles.](https://www.w3.org/TR/WCAG/#understandable)

### Rendre le contenu textuel lisible et compréhensible (3.1) {#make-text-content-readable-and-understandable}

[Règle 3.1 – Lisible : rendre le contenu textuel lisible et compréhensible](https://www.w3.org/TR/WCAG/#readable)

### Langue de la page (3.1.1) {#language-of-page}

* Critère de réussite 3.1.1
* Niveau A
* Langue de la page : la langue humaine par défaut de chaque page web peut être définie par programmation.

#### Objectif – Langue de la page (3.1.1) {#purpose-language-of-page}

Ce critère de réussite garantit que ce texte et tout autre contenu linguistique est correctement restitué. Pour les utilisateurs de lecteur d’écran, il garantit que le contenu est correctement prononcé, tandis que les navigateurs visuels sont plus susceptibles d’afficher correctement certains jeux de caractères.

#### Comment procéder – Langue de la page (3.1.1) {#how-to-meet-language-of-page}

Pour que ce critère de réussite soit satisfait, la langue par défaut d’une page web peut être identifiée à l’aide de l’attribut `lang` dans l’élément `<html>` en haut de la page. Par exemple :

* Si une page est écrite en anglais, l’élément `<html>` doit être :
  `<html lang = "en">`

* En revanche, pour une page à restituer en espagnol, l’attribut doit être défini comme suit :
  `<html lang = "es">`

Dans AEM, la langue par défaut de la page est définie lors de la création de la page. Elle peut aussi être redéfinie en modifiant les [propriétés de la page](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>AEM offre des fonctions de réglage supplémentaires pour les variations d’une langue racine ; par exemple, l’anglais américain (en-us), l’anglais britannique (en-gb) et l’anglais canadien (en-ca). Ce niveau de détail est souvent superflu pour les technologies d’assistance, même s’il est utile pour les variantes régionales du contenu des pages.

#### En savoir plus – Langue de la page (3.1.1) {#more-information-language-of-page}

* [Compréhension du critère de réussite 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Comment remplir le critère de réussite 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Les codes sont basés sur la norme ISO 639-1. Une liste plus exhaustive des codes pour chaque langue est disponible sur le [Site W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Langue des parties (3.1.2)  {#language-of-parts}

* Critère de réussite 3.1.2
* Niveau AA
* Langue d’un passage : la langue humaine de chaque passage ou expression dans le contenu peut être définie par programmation. Les exceptions sont les noms propres, les termes techniques, les mots d’une langue indéterminée, ainsi que les mots ou expressions qui sont devenus partie intégrante du langage courant du texte qui l’entoure immédiatement.

#### Objectif – Langue d’un passage (3.1.2) {#purpose-language-of-parts}

L’objectif de ce critère de succès est similaire au critère de succès [Langue de la page](#language-of-page), sauf qu’il s’applique aux pages web comportant du contenu dans plusieurs langues sur une seule page (par exemple, en cas de citations ou de mots empruntés peu courants).

Les pages qui appliquent ce critère de succès ont les avantages suivants :

* Un logiciel de transition en braille pour insérer des caractères accentués.
* Les lecteurs d’écran peuvent prononcer correctement les mots contenant des caractères spéciaux ou délivrés dans une autre langue que celle par défaut, identifiée sur la page.
* Les outils de traduction du type Google Translate peuvent correctement traduire les mots d’une langue à une autre.

#### Comment procéder – Langue d’un passage (3.1.2) {#how-to-meet-language-of-parts}

L’attribut `lang` peut être utilisé pour identifier les changements de langue du contenu. Par exemple, une citation en allemand (code ISO 639-1 « de ») peut s’afficher comme suit :

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
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>Il n’est pas nécessaire de respecter ce critère de réussite lors de l’inclusion de noms ou de villes dans différentes langues. Ou bien, lorsque vous utilisez des mots ou expressions empruntés devenus courants dans la langue par défaut, tels que *schadenfreude* en anglais.

Pour ajouter l’élément span, avec un langage approprié, vous pouvez modifier manuellement votre balisage HTML en mode d’édition source de l’éditeur de texte enrichi afin qu’il se lise comme ci-dessus. Vous pouvez également inclure l’attribut `lang` dans l’éditeur de texte enrichi par un administrateur système (voir [Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

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

Il est possible de déplacer le focus vers une commande à l’aide du clavier (par exemple, en accédant à une commande par tabulation) ou à l’aide de la souris (par exemple, en cliquant sur un champ de texte). Le déplacement de la souris au-dessus d’une commande n’a aucun effet sur le focus, sauf si un script implémente ce comportement. Notez que pour certains types de commandes, cliquer sur une commande revient à l’activer (par exemple, un bouton). Cette action peut, en retour, entraîner un changement de contexte.

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

Ce critère de réussite a pour but de s’assurer que la saisie de données ou la sélection d’une commande de formulaire a des effets prévisibles. La modification d’un paramètre de n’importe quel composant de l’interface utilisateur modifie l’un des aspects de la commande, de manière persistante lorsque l’utilisateur ou l’utilisatrice n’interagit plus avec celle-ci. Ainsi, cocher une case, saisir du texte dans un champ ou modifier l’option sélectionnée dans un contrôle de liste modifie le paramétrage, alors que l’activation d’un lien ou d’un bouton le laisse inchangé. Les changements de contexte peuvent dérouter les utilisateurs s’ils ne les perçoivent pas aisément ou s’ils sont facilement déconcentrés par la modification. Un changement de contexte n’est approprié que s’il est évident qu’il se produit en réponse à l’action de l’utilisateur ou de l’utilisatrice.

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

Ce critère de succès a pour but d’encourager l’utilisation d’une présentation et d’une mise en page cohérentes pour les utilisateurs et utilisatrices qui interagissent avec du contenu répété dans un ensemble de pages web et qui ont besoin de trouver à plusieurs reprises des informations ou des fonctionnalités spécifiques. Les personnes malvoyantes qui utilisent la loupe pour agrandir une petite partie de l’écran utilisent souvent des repères visuels et des limites de pages pour localiser rapidement un contenu répété. De même, la présentation d’un contenu répété dans le même ordre est importante pour les utilisateurs visuels qui font appel à leur mémoire spatiale ou à des repères visuels dans la représentation graphique pour localiser ce contenu.

L’expression « dans le même ordre » de cette section ne signifie pas qu’il est impossible d’utiliser des sous-menus, des blocs de navigation secondaires ou une structure de page complémentaire. Ce critère de succès vise plutôt à aider les utilisateurs et utilisatrices qui interagissent avec du contenu répété sur plusieurs pages web à prévoir l’emplacement du contenu qu’ils recherchent. Il leur permet également de le trouver plus rapidement quand ils le redécouvrent.

Les utilisateurs et utilisatrices peuvent effectuer une modification de l’ordre en faisant appel à des agents utilisateur adaptatifs ou en définissant des préférences pour que les informations soient présentées de la manière la plus utile pour eux.

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

Ce critère de réussite a pour but d’assurer une identification cohérente des composants fonctionnels qui apparaissent à plusieurs reprises dans un ensemble de pages web. L’une des stratégies des utilisateurs de lecteurs d’écran pour parcourir un site web consiste à s’appuyer abondamment sur leur connaissance des fonctions présentées sur différentes pages. Si des fonctions identiques comportent des libellés différents (ou, plus généralement, un nom accessible différent) selon les pages web, le site sera beaucoup plus difficile à utiliser. La situation peut en outre dérouter les personnes atteintes de limitations cognitives et accroître la charge en la matière. Par conséquent, l’étiquetage cohérent aide.

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

Ce critère de réussite a pour but de s’assurer que les utilisateurs sont conscients qu’une erreur s’est produite et qu’ils peuvent déterminer ce qui ne va pas. Le message d’erreur doit être aussi précis que possible. Dans le cas d’un échec d’envoi de formulaire, le réaffichage du formulaire avec les champs erronés indiqués ne suffit pas, pour certains utilisateurs et utilisatrices, à constater qu’une erreur s’est produite. Les utilisateurs et utilisatrices de lecteurs d’écran, par exemple, ne savent pas qu’une erreur s’est produite tant qu’ils ou elles n’ont pas identifié l’un des indicateurs. Il est possible qu’ils abandonnent complètement le formulaire avant d’identifier l’indicateur d’erreur, en pensant que la page n’est tout simplement pas fonctionnelle. Selon la définition des règles WCAG, une [erreur de saisie](https://www.w3.org/TR/WCAG/#dfn-input-error) correspond à une information fournie par l’utilisateur et qui n’est pas acceptée. Cela inclut les éléments suivants :

Les informations requises par la page web, mais omises par l’utilisateur ou l’utilisatrice, ou les informations fournies par l’utilisateur ou l’utilisatrice, mais non conformes au format de données requis ou aux valeurs autorisées.
Par exemple :

* l’utilisateur ou l’utilisatrice ne saisit pas l’abréviation appropriée dans le champ état, province ou région ;
* l’utilisateur ou l’utilisatrice saisit une abréviation d’état non valide ;
* l’utilisateur ou l’utilisatrice saisit un code postal inexistant ;
* l’utilisateur saisit une date de naissance fixée à 2 ans après la date présente ;
* l’utilisateur saisit des caractères alphabétiques ou des parenthèses dans le champ de son numéro de téléphone alors que seuls les chiffres sont acceptés ;
* l’utilisateur saisit une offre inférieure à l’offre précédente ou à l’augmentation minimale pour une offre.

#### Comment procéder – Identification des erreurs (3.3.1) {#how-to-meet-error-identification}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### En savoir plus – Identification des erreurs (3.3.1) {#more-information-error-identification}

* [Compréhension du critère de réussite 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Comment remplir le critère de réussite 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Étiquettes ou instructions (3.3.2) {#labels-or-instructions}

* Critère de réussite 3.3.2
* Niveau A
* Libellés ou instructions : des libellés ou des instructions sont fournis lorsque le contenu nécessite une saisie de l’utilisateur ou de l’utilisatrice.

#### Objectif – Étiquettes ou instructions (3.3.2) {#purpose-labels-or-instructions}

Fournir des instructions pour aider les personnes à remplir des formulaires est une partie essentielle des bonnes pratiques en matière d’utilisation de l’interface. Cela s’avère utile pour les personnes ayant des déficiences visuelles ou cognitives qui auraient autrement des difficultés à comprendre la mise en page d’un formulaire et le type de données à fournir dans un champ de formulaire particulier.

##### Forms

Dans le projet de démonstration AEM WKND, une étiquette par défaut est ajoutée lorsque vous ajoutez un composant de formulaire à la page, par exemple un **champ de texte**. Ce titre par défaut dépend du type de composant. Vous pouvez ajouter votre propre titre dans l’onglet **Titre et Texte** de la boîte de dialogue de modification de ce champ. Il est important de s’assurer que les libellés aident les utilisateurs et les utilisatrices à comprendre les données associées à chaque composant de formulaire.

Utilisez ce champ **Titre** pour les éléments de champ, car il fournit un libellé accessible par les technologies d’assistance. Le simple fait d’écrire un libellé dans le texte en regard du champ ne suffit pas.

Pour certains composants de formulaire, il est également possible de masquer visuellement les libellés à l’aide de la case à cocher **Masquer le titre**. Les libellés masqués de cette manière sont toujours disponibles pour les dispositifs d’assistance, mais ne s’affichent pas à l’écran. Bien qu’il s’agisse d’une bonne approche dans certaines situations, il est généralement préférable d’inclure un libellé visuel dans la mesure du possible, car certains utilisateurs et utilisatrices sont susceptibles de consulter une très petite section de l’écran (un champ à la fois) et d’avoir besoin des libellés pour identifier correctement le champ.

###### Boutons Image {#image-buttons}

Lorsque des boutons d’image sont utilisés (par exemple, le composant **Bouton Image** du projet WKND), le champ **Titre** de l’onglet **Titre et texte** de la boîte de dialogue de modification fournit en fait le texte secondaire de l’image, plutôt que le libellé. Ainsi, dans l’exemple ci-dessous, l’image avec le texte `Submit` comporte le texte secondaire `Submit`, ajouté à l’aide du champ **Titre** dans la boîte de dialogue de modification.

###### Groupes de champs de formulaire {#groups-of-form-fields}

Dans le projet WKND, lorsqu’il existe un groupe de commandes associées, comme **Groupe de boutons radio**, il peut s’avérer nécessaire d’ajouter un titre au groupe et des commandes individuelles. Lors de l’ajout d’un ensemble de boutons radio dans AEM, le champ **Titre** fournit le titre de ce groupe, tandis que les titres individuels sont spécifiés lors de la création des boutons radio (**Éléments**).

Cependant, il n’existe aucune association par programmation entre le titre du groupe et les boutons radio eux-mêmes. Les éditeurs de modèles doivent placer le titre dans les balises `fieldset` et `legend` nécessaires afin de créer cette association. Ceci ne peut être effectué qu’en modifiant le code source de la page. L’administration système peut également ajouter la prise en charge de ces éléments afin qu’ils apparaissent dans la boîte de dialogue **Propriétés du champ** (voir [Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

###### Considérations supplémentaires pour les formulaires {#additional-considerations-for-forms}

Si les données doivent être saisies dans un format spécifique, précisez-le dans le texte du libellé. Par exemple, si une date doit être saisie au format `DD-MM-YYYY`, indiquez-le spécifiquement dans le libellé. Cela signifie que lorsque les utilisateurs de lecteurs d’écran rencontrent le champ, le libellé est automatiquement annoncé, ainsi que les informations supplémentaires sur le format.

Si la saisie d’un champ de formulaire est obligatoire, indiquez-le en utilisant le mot « obligatoire » dans le libellé. AEM ajoute un astérisque lorsqu’un champ est obligatoire, mais il serait idéal d’inclure le mot `required` dans le libellé lui-même (dans le champ **Titre** de la boîte de dialogue de modification).

Le positionnement des libellés est également important, car ils permettent de localiser les champs appropriés. Cela est tout particulièrement important lorsque l’utilisateur est confronté à un formulaire complexe. Suivez les conventions ci-dessous :

* Cases à cocher ou cases d’option :
Les libellés sont positionnés immédiatement à droite du champ.
* Tous les autres composants de formulaire (par exemple, zones de texte, zones de liste modifiable) :
les libellés sont positionnés immédiatement au-dessus ou à gauche du champ.

Dans les formulaires simples aux fonctionnalités limitées, l’ajout d’un libellé approprié pour un bouton `Submit` peut servir de libellé pour le champ adjacent (par exemple, `Search`). Cela s’avère utile dans les cas où il peut être difficile de trouver de l’espace pour le texte du libellé.

#### En savoir plus – Étiquettes ou instructions (3.3.2) {#more-information-labels-or-instructions}

* [Compréhension du critère de réussite 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Comment remplir le critère de réussite 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Suggestion d’erreur (3.3.3)  {#error-suggestion}

* Critère de réussite 3.3.3
* Niveau AA
* Clavier : si une erreur de saisie est automatiquement détectée et que des suggestions de correction sont connues, ces suggestions sont proposées à l’utilisateur, sauf si elles compromettent la sécurité ou l’objectif du contenu.

#### Objectif – Suggestion d’erreur (3.3.3) {#purpose-error-suggestion}

Ce critère de réussite a pour but de s’assurer que les utilisateurs reçoivent des suggestions appropriées pour corriger, si possible, une erreur de saisie. Selon les règles WCAG, une [erreur de saisie](https://www.w3.org/TR/WCAG/#dfn-input-error) indique que « l’information fournie par l’utilisateur n’est pas acceptée » par le système. À titre d’exemples de saisies non acceptées, figurent les informations requises, mais omises par l’utilisateur, et celles fournies par l’utilisateur, mais non conformes au format de données requis ou aux valeurs autorisées.

Le critère de réussite 3.3.1 prévoit la notification des erreurs. Cependant, les personnes atteintes de limitations cognitives peuvent avoir du mal à comprendre comment corriger les erreurs. Celles atteintes de déficiences visuelles ne seront peut-être pas en mesure de déterminer exactement comment corriger l’erreur. Dans le cas d’un envoi de formulaire infructueux, les utilisateurs et utilisatrices risquent d’abandonner faute de savoir comment corriger l’erreur, même s’ils savent qu’elle s’est produite.

La personne en charge de la création du contenu peut donner la description de l’erreur ou l’agent utilisateur peut fournir la description de l’erreur en fonction d’informations spécifiques à la technologie et déterminées par programmation.

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

Ce critère de réussite a pour but d’aider les utilisateurs en situation de handicap à éviter les conséquences graves d’une erreur lorsqu’ils effectuent une action qui ne peut pas être annulée. Par exemple, l’achat de billets d’avion non remboursables ou le lancement d’un ordre d’achat d’actions par le biais d’un compte de courtage sont des transactions financières assorties de graves conséquences. Si une personne a commis une erreur de date pour un voyage en avion, elle risque d’avoir un billet pour le mauvais jour, sans pouvoir l’échanger. Si l’erreur concerne un nombre d’actions à acheter, l’achat pourrait concerner davantage d’actions que prévu. Ces deux types d’erreurs coûteuses concernent des transactions qui ont lieu immédiatement et qui ne peuvent pas être modifiées par la suite. De même, il peut s’agir d’une erreur irrémédiable si les utilisateurs et utilisatrices modifient ou suppriment involontairement des données stockées dans une base de données, à laquelle ils auront par la suite besoin d’accéder (par exemple, leur profil de voyage complet sur un site web de voyagiste). En ce qui concerne la modification ou la suppression de données « contrôlables par l’utilisateur », l’objectif est d’empêcher la perte massive de données, par exemple la suppression d’un fichier ou d’un enregistrement. L’objectif ne consiste pas à exiger une confirmation pour chaque commande d’enregistrement ou les opérations de création ou de modification simple de documents, d’enregistrements ou d’autres données.

Les utilisateurs en situation de handicap sont plus enclins à commettre des erreurs. Les personnes atteintes de difficultés de lecture peuvent avoir tendance à transposer les chiffres et les lettres, et celles souffrant de troubles moteurs à actionner des touches par erreur. La possibilité d’annuler des actions permet aux utilisateurs de corriger une erreur pouvant avoir de graves conséquences. Pouvoir vérifier et corriger des informations donne à l’utilisateur la possibilité de détecter une erreur avant d’effectuer une action d’une portée considérable.

Les données contrôlables par l’utilisateur sont des données visibles pour lui, et qu’il peut modifier ou supprimer de manière intentionnelle. À titre d’exemple, le contrôle de ces données par un utilisateur peut consister à mettre à jour le numéro de téléphone et l’adresse indiqués dans son compte ou à supprimer d’anciennes factures enregistrées sur un site web. Il ne s’agit pas d’éléments comme les données relatives à la surveillance de moteurs de recherche et de journaux Internet que l’utilisateur ou l’utilisatrice ne peut pas voir ni utiliser directement.

#### Comment procéder – Prévention des erreurs (juridiques, financières, données) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### En savoir plus – Prévention des erreurs (juridiques, financières, données) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Compréhension du critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Comment remplir le critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Principe 4 : robuste {#principle-robust}

[Principe 4 : robuste – Le contenu doit être suffisamment robuste pour être interprétable par un large éventail d’agents utilisateurs, y compris les technologies d’assistance.](https://www.w3.org/TR/WCAG/#robust)

### Compatible (4.1) {#compatible}

[Règle 4.1 – Compatible : optimiser la compatibilité avec les agents utilisateur actuels et futurs, y compris les technologies d’assistance.](https://www.w3.org/TR/WCAG/#compatible)

Optimiser la compatibilité avec les agents utilisateur actuels et futurs, y compris les technologies d’assistance.

### Analyse (4.1.1)  {#parsing}

* Critère de réussite 4.1.1
* Niveau A
* Analyse : dans le contenu implémenté à l’aide de langages de balisage, les éléments ont des balises de début et de fin complètes, sont imbriqués selon leurs spécifications, ne contiennent pas d’attributs de duplicata et les identifiants sont uniques, sauf si les spécifications autorisent ces fonctionnalités.

#### Objectif – Analyse (4.1.1) {#purpose-parsing}

Ce critère de réussite a pour but de s’assurer que les agents utilisateurs, y compris les technologies d’assistance, peuvent interpréter et analyser le contenu avec précision. Si le contenu ne peut pas être analysé dans une structure de données, différents agents utilisateurs pourraient le présenter différemment ou être incapables de l’analyser. Certains agents utilisateurs utilisent des « techniques de réparation » pour restituer un contenu mal codé.

Les techniques de réparation variant d’un agent utilisateur à l’autre, les personnes créant du contenu ne peuvent pas supposer que le contenu sera analysé avec précision dans une structure de données ou qu’il sera restitué correctement par des agents utilisateurs spécialisés, y compris les technologies d’assistance, à moins que le contenu ne soit créé selon les règles définies dans la grammaire formelle de cette technologie. Dans les langages de balisage, les erreurs de syntaxe d’éléments et d’attributs, ainsi que l’impossibilité de fournir des balises de début et de fin correctement imbriquées, entraînent des erreurs qui empêchent les agents utilisateurs d’analyser le contenu de manière fiable. Ainsi, le critère de réussite impose que le contenu puisse être analysé en utilisant uniquement les règles de la grammaire formelle.

#### Comment procéder – Analyse (4.1.1) {#how-to-meet-parsing}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### En savoir plus – Analyse (4.1.1) {#more-information-parsing}

* [Compréhension du critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Comment remplir le critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nom, rôle, valeur (4.1.2)  {#name-role-value}

* Critère de réussite 4.1.2
* Niveau A
* Nom, rôle, valeur : pour tous les composants de l’interface utilisateur (y compris, mais pas uniquement, les éléments de formulaire, les liens et les composants générés par des scripts), le nom et le rôle peuvent être déterminés par programmation ; les états, propriétés et valeurs définissables par l’utilisateur ou l’utilisatrice peuvent être définis par programmation ; et les agents utilisateurs peuvent être informés des modifications apportées à ces éléments, y compris les technologies d’assistance.

#### Objectif – Nom, rôle, valeur (4.1.2) {#purpose-ame-role-value}

Ce critère de réussite a pour but de s’assurer que les technologies d’assistance peuvent recueillir des informations sur le contenu, l’activer (ou le définir) et actualiser l’état des contrôles de l’interface utilisateur.

Si l’interface utilise des contrôles standard issus de technologies d’accessibilité, ce processus est simple. Si les éléments de l’interface utilisateur sont utilisés conformément à la spécification, les conditions de cette disposition sont remplies. (Voir les exemples relatifs au critère de réussite 4.1.2 ci-dessous)

Cependant, si des commandes personnalisées sont créées ou si des éléments d’interface sont programmés (dans le code ou le script) avec un rôle et/ou une fonction différents de leurs caractéristiques habituelles, des dispositions supplémentaires doivent être prises pour garantir que les commandes fournissent des informations importantes aux technologies d’assistance et autorisent d’être contrôlées par ces technologies.

L’état du focus d’une commande d’interface utilisateur est particulièrement important. Il est possible de déterminer cet état par programmation, et des notifications concernant le changement de focus sont envoyées aux agents utilisateurs de même qu’aux dispositifs d’assistance. Parmi les autres exemples d’état des commandes de l’interface utilisateur, on peut citer la sélection ou la non sélection d’une case à cocher ou d’un bouton radio. Ou si une arborescence ou un nœud de liste réductible est développé ou réduit.

#### Comment procéder – Nom, rôle, valeur (4.1.2) {#how-to-meet-ame-role-value}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### En savoir plus – Nom, rôle, valeur (4.1.2)  {#more-information-ame-role-value}

* [Compréhension du critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Comment remplir le critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
