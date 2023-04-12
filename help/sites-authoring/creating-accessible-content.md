---
title: Création de contenu accessible pour Adobe Experience Manager (conformité au WCAG 2.1)
description: Utilisez AEM pour rendre le contenu Web accessible et utilisable par les personnes en situation de handicap
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '13818'
ht-degree: 63%

---

# Création d’un contenu accessible (conformité WCAG 2.1) {#creating-accessible-content-wcag-conformance}

Le [Consignes relatives à l’accessibilité du contenu web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), établi par [un groupe de travail du World Wide Web Consortium ;](https://www.w3.org/groups/#Accessibility_Guidelines_Working_Group), se compose d’un ensemble de consignes et de critères de réussite, indépendants de la technologie, qui permettent de rendre le contenu web accessible et utilisable par les personnes en situation de handicap.

En introduction, le consortium propose une série de sections et de documents annexes :

* [Nouvelles fonctionnalités de WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Conformité à WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Présentation de WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Techniques relatives à WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Documents WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

En outre, voir :
* Le [Guide rapide relatif à WCAG 2.1](/help/managing/qg-wcag.md).
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
>Dans ce document, les éléments suivants sont utilisés :
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

Les informations d’une page web peuvent être fournies dans différents formats non textuels, tels que des images, des vidéos, des animations, des graphiques et des graphiques. Les personnes aveugles ou ayant de graves déficiences visuelles ne peuvent pas voir de contenu non textuel. Cependant, ils peuvent accéder au contenu textuel en le faisant lire par un lecteur d&#39;écran ou en le présentant sous forme tactile à l&#39;aide d&#39;un dispositif d&#39;affichage en braille. Ainsi, en proposant des équivalents textuels au contenu au format graphique, les personnes qui ne peuvent pas voir le contenu graphique peuvent accéder à une version équivalente de l’information fournie par le contenu.

Un autre avantage utile est que les équivalents textuels permettent l’indexation du contenu non textuel par la technologie des moteurs de recherche.

#### Comment procéder – Contenu non textuel (1.1.1) {#how-to-meet-non-text-content}

Pour les images statiques, la règle de base consiste à fournir un équivalent textuel. Vous pouvez le faire dans la variable **Texte de remplacement** champ . Voir, par exemple, le composant principal **[Image](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=fr)**.

>[!NOTE]
>
>Certains composants principaux prêts à l’emploi, tels que **[Carrousel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html)**, ne fournissent pas de champ **Texte de remplacement** pour ajouter des descriptions de texte de remplacement à des images individuelles. Il existe cependant le champ **Libellé** (onglet **[Accessibilité](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html#accessibility-tab)**) pour l’ensemble du composant.
>
>Lors de l’implémentation de ces versions pour votre instance AEM, votre équipe de développement devra configurer ces composants pour prendre en charge l’attribut `alt` afin que les auteurs et autrices puissent l’ajouter au contenu (voir [Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

Dans AEM, le champ **Texte de remplacement** doit être renseigné par défaut. Si votre image est purement décorative et que le texte secondaire est superflu, l’option **L’image est décorative** peut être sélectionnée.

#### Création d’un texte secondaire adapté {#creating-good-text-alternatives}

Il existe diverses formes de contenu non textuel. Par conséquent, la valeur du texte secondaire dépend du rôle du graphique dans la page web. Voici quelques-unes des règles de base à respecter :

* Les textes secondaires doivent être succincts, tout en communiquant clairement l’information essentielle du contenu non textuel.
* Il est préférable d’éviter les descriptions trop longues (plus de 100 caractères). Si un texte secondaire doit être plus détaillé :
   * donnez une brève description dans le texte secondaire ;
   * et avoir une description plus longue dans le texte ailleurs sur la même page ou dans une page web distincte. Lien vers cette description distincte en faisant de l’image un lien ou en plaçant un lien texte en regard de l’image.
* Le texte de remplacement ne doit pas répliquer le contenu fourni sous forme de texte à proximité sur la même page. N’oubliez pas que de nombreuses images sont des illustrations de points déjà couverts dans le texte d’une page. Il peut donc y avoir une alternative textuelle détaillée.
* Si le contenu non textuel est un lien vers une autre page ou un autre document et qu’il n’existe aucun autre texte faisant partie d’un même lien, le texte secondaire de l’image doit indiquer la destination du lien. Il ne doit pas décrire l’image.
* Si le contenu non textuel est contenu dans un élément de bouton et qu’il n’y a pas de texte faisant partie du même bouton, le texte secondaire de l’image doit indiquer la fonctionnalité du bouton. Il ne doit pas décrire l’image.
* Il est tout à fait acceptable de spécifier un texte de remplacement vide (nul) pour une image, mais seulement si l’image n’a pas besoin de texte de remplacement. Par exemple, il s’agit d’une image purement décorative ou si le texte équivalent existe dans le texte de la page.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Voici quelques-uns des types spécifiques de contenu non textuel auquel un texte secondaire doit être associé :

* Illustrations : Ce sont des images de personnes, d&#39;objets ou de lieux. Il est important de réfléchir au rôle de la photo dans la page et de décrire le contenu de l’image, car la technologie d’assistance annonce le type d’élément (par exemple, `graphic` ou `image`); il peut améliorer la clarté d’utilisation `screenshot` ou `illustration` dans les descriptions de texte de remplacement, mais cela dépend du contexte. La cohérence est un facteur important. Une décision doit être prise pour l’ensemble de l’équipe de création et elle doit être appliquée tout au long de l’expérience utilisateur.
* Icônes : certains petits pictogrammes (images) communiquent parfois des informations spécifiques. Ils doivent être utilisés de manière uniforme sur une page et un site. Toutes les instances de l’icône sur une page ou un site doivent avoir le même texte secondaire bref et succinct, sauf si cela duplique de manière superflue le texte adjacent.
* Graphiques et graphiques : Elles représentent généralement des données numériques. Ainsi, une option permettant de fournir un texte secondaire peut être d’inclure un bref résumé des principales tendances affichées dans le graphique ou le graphique. Si nécessaire, fournissez également une description plus détaillée dans le texte à l’aide de la variable **Description** dans le champ **Avancé** propriétés de l’image. Vous pouvez également fournir les données source sous forme tabulaire ailleurs dans la page ou le site.
* Cartes, diagrammes, organigrammes : pour les graphiques produisant des données spatiales (par exemple, pour la description des relations entre des objets ou un processus), assurez-vous que le message clé est fourni au format texte et que ces informations textuelles sont placées à proximité de chaque point de données associé. Dans le cas des cartes, il est probable que l’utilisation d’un équivalent en texte intégral ne soit pas adaptée. Toutefois, si la carte est fournie pour aider les gens à trouver leur chemin vers un emplacement donné, alors le texte secondaire de l’image de la carte peut indiquer brièvement *Carte de X*, puis donner des indications vers cet emplacement en texte à un autre endroit, dans la page ou dans le champ **Description** de l’onglet **Avancé** du composant **Image**.
* CAPTCHA : Un CAPTCHA est un *Test public de Turing entièrement automatisé pour informer les ordinateurs et les humains de leur éparpillement*. Il s’agit d’un contrôle de sécurité utilisé sur les pages web pour distinguer les humains des logiciels malveillants, mais qui peut entraîner des barrières à l’accessibilité. Il s’agit d’images qui demandent aux utilisateurs de décrire ce qu’ils voient pour réussir un test de sécurité. Il n’est pas possible de fournir un texte de remplacement à l’image. Vous devez donc envisager des solutions non graphiques alternatives. Le W3C propose quelques suggestions, telles que :
   * Puzzles logiques
   * Utilisation de la sortie son au lieu des images
   * Comptes d’utilisateur limités et filtres de courrier indésirable
* Images d’arrière-plan : elles impliquent l’utilisation de feuilles de style en cascade CSS (Cascading Style Sheet) plutôt que de code HTML. Il est donc impossible de spécifier une valeur de texte secondaire. Par conséquent, les images d’arrière-plan ne doivent pas communiquer d’informations textuelles importantes. Sinon, ces informations doivent aussi être spécifiées dans le texte de la page. Cependant, il est important qu’un arrière-plan secondaire s’affiche si l’image ne peut pas s’afficher.

>[!NOTE]
>
>Le niveau de contraste entre l’arrière-plan et le texte au premier plan doit être suffisant. Cela est décrit de manière plus détaillée à la section [Contraste (minimum) (1.4.3)](#contrast-minimum).

#### En savoir plus – Contenu non textuel (1.1.1) {#more-information-non-text-content}

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
* Contenu seulement audio ou vidéo (pré-enregistré) : Pour les médias pré-enregistrés audio uniquement et pré-enregistrés vidéo uniquement, les faits suivants sont vrais, sauf lorsque l’audio ou la vidéo est un média de remplacement pour le texte et est clairement étiqueté comme tel :
   * Contenu audio pré-enregistré uniquement : Une alternative pour les médias temporels est fournie, qui présente des informations équivalentes pour le contenu audio pré-enregistré uniquement.
   * Vidéo pré-enregistrée uniquement : Il existe une alternative aux médias temporels ou une piste audio qui présente des informations équivalentes pour le contenu vidéo pré-enregistré uniquement.

#### Objectif – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Les problèmes d’accessibilité pour la vidéo et l’audio peuvent être rencontrés par :

* Les personnes malvoyantes lorsqu’il n’y a pas de bande sonore, ou que la bande sonore n’est pas suffisante pour les informer de ce qui se passe dans la vidéo ou l’animation ;
* les personnes malentendantes ou sourdes, qui ne peuvent pas entendre la bande sonore ;
* Les personnes qui peuvent entendre la bande sonore, mais ne comprennent pas ce qui est parlé (par exemple, parce qu&#39;elle est dans une langue qu&#39;elles ne comprennent pas).

Les utilisateurs de navigateurs ou d’appareils qui ne prennent pas en charge la lecture de contenu dans des formats multimédias spécifiques, tels que le Flash des Adobes, peuvent également ne pas avoir accès aux vidéos ou au contenu audio.

Fournir ces informations dans un format différent, tel que du texte (ou de l’audio pour une vidéo sans audio), peut les rendre accessibles aux personnes qui ne peuvent pas accéder au contenu d’origine.

#### Comment procéder – Contenu seulement audio ou vidéo (pré-enregistré) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Si le contenu est un contenu audio pré-enregistré sans vidéo (podcast par exemple) :
   * Fournissez un lien juste avant ou après le contenu vers une transcription textuelle du contenu audio. La transcription doit être une page de HTML avec un équivalent textuel de tout le contenu non parlé important et parlé, plus une indication de qui parle, une description du décor, des expressions vocales et une description de tout autre contenu audio significatif.
* Si le contenu est une animation ou une vidéo pré-enregistrée sans audio :
   * Fournissez un lien juste avant ou après le contenu vers une description textuelle équivalente des informations fournies par la vidéo.
   * Ou une audio-description équivalente dans un format audio couramment utilisé, tel que MP3.

>[!NOTE]
>
>Si le contenu audio ou vidéo est fourni comme alternative au contenu existant dans un autre format sur la même page web, une alternative supplémentaire peut ne pas être nécessaire.
>
>Les règles, décrites par la section [Présentation de WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html), fournissent d’autres informations.

L’insertion d’un contenu multimédia dans vos pages web AEM est similaire à celle d’une image. Cependant, comme le contenu multimédia est bien plus qu’une image fixe, il existe différents paramètres et options pour contrôler la lecture du contenu multimédia.

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

Dans la mesure du possible, utilisez le sous-titrage codé, car cela permet aux utilisateurs de choisir d’afficher ou non les sous-titres.

Pour les sous-titres non intégrés, créez et fournissez un fichier de sous-titres synchronisés dans un format approprié (par exemple : [SMIL](https://www.w3.org/AudioVideo/)) avec le fichier vidéo (les détails sur la façon de procéder ne sont pas compris dans ce guide, mais nous avons fourni des liens vers certains tutoriels sous [En savoir plus - Sous-titres (pré-enregistrés) (1.2.2)](#more-information-captions-prerecorded)). Pensez à inclure une note avisant les utilisateurs que des sous-titres sont disponibles pour la vidéo, ou à activer la fonctionnalité de sous-titres.

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
* Audio-description ou version de remplacement pour un média temporel (pré-enregistré) : Une alternative pour un média temporel ou une audio-description du contenu vidéo pré-enregistré est fournie pour un média synchronisé, sauf lorsque le média est un média de remplacement pour un texte et qu’il est clairement étiqueté comme tel.

#### Objectif – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Les personnes aveugles ou malvoyantes ne pourront pas accéder au contenu si les informations contenues dans une vidéo ou une animation sont fournies sous forme visuelle seulement ou si la piste audio ne fournit pas suffisamment d’informations pour comprendre ce qui se passe visuellement.

#### Comment procéder – Audio-description ou version de remplacement pour un média temporel (pré-enregistré) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Deux méthodes peuvent être adoptées pour remplir ce critère de réussite. N’importe lequel est acceptable :

1. Incluez une audio-description supplémentaire pour le contenu vidéo. Cela peut se faire de trois façons :
   * Pendant les pauses dans la boîte de dialogue existante, fournissez des informations sur les modifications de la scène qui ne sont pas présentées dans le cadre de la piste audio existante ;
   * Fournissez une nouvelle piste audio supplémentaire et facultative contenant la piste audio d’origine, mais également des informations audio supplémentaires sur les modifications dans la scène.
      * Les utilisateurs peuvent basculer entre la piste audio existante (qui *ne fait pas* contiennent une description audio) et la nouvelle piste audio (qui *does* contient une description audio).
      * Cela évite toute perturbation des utilisateurs qui n’ont pas besoin de la description supplémentaire.
   * Créez une deuxième version du contenu vidéo pour permettre des descriptions audio étendues. Cela permet de réduire les difficultés liées à la fourniture de descriptions audio détaillées dans les espaces entre les dialogues existants, en mettant temporairement le contenu audio et vidéo en pause aux moments appropriés. Par conséquent, une audio-description beaucoup plus longue peut être fournie avant que l’action ne recommence. Comme dans l’exemple précédent, il est préférable de le fournir en tant que piste audio supplémentaire en option afin d’éviter toute perturbation des utilisateurs qui n’ont pas besoin de la description supplémentaire.
1. Fournissez une transcription textuelle formant un équivalent textuel adapté des éléments audio et visuels de la vidéo ou de l’animation. Cela devrait inclure, le cas échéant, une indication sur qui parle, une description du décor, tout événement ou information présentée visuellement, et les expressions vocales. Selon sa durée, vous pouvez placer la transcription sur la même page que la vidéo ou l’animation, ou sur une page distincte ; si vous choisissez cette option, fournissez un lien vers la transcription en regard de la vidéo ou de l’animation.

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

Suivez les instructions de la section [Sous-titres (pré-enregistrés)](#captions-prerecorded) ci-dessus. Cependant, en raison de la nature du média en direct, les sous-titres doivent être créés aussi rapidement que possible et en fonction de ce qui se passe. Par conséquent, vous devez envisager d’utiliser des outils de sous-titrage en temps réel ou de transcription voix-texte.

Ce document ne vise pas à fournir des instructions détaillées à ce sujet, mais vous trouverez des renseignements utiles en suivant les liens ci-après :

* [WebAIM : Real Time Captioning (sous-titrage en temps réel ; en anglais)](https://webaim.org/techniques/captions/realtime)

* [Projet AccessComputing (University of Washington) : est-il possible de générer des sous-titres automatiquement à l’aide de la reconnaissance vocale ?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### En savoir plus – Sous-titres (en direct) (1.2.4) {#more-information-captions-live}

* [Compréhension du critère de réussite 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Comment remplir le critère de réussite 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Audio-description (préenregistrée) (1.2.5)   {#audio-description-prerecorded}

* Critère de réussite 1.2.5
* Niveau AA
* Audio-description (pré-enregistrée) : Une description audio est fournie pour tout le contenu vidéo pré-enregistré dans les médias synchronisés.

#### Objectif – Audio-description (pré-enregistrée) (1.2.5) {#purpose-audio-description-prerecorded}

Ce critère de réussite est identique au critère [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audio-description-or-media-alternative-prerecorded), excepté que les auteurs doivent fournir une audio-description beaucoup plus détaillée, conforme au niveau AA.

#### Comment procéder – Audio-description (pré-enregistrée) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Suivez les instructions de la section [Audio-description ou version de remplacement pour un média temporel (pré-enregistré)](#audio-description-or-media-alternative-prerecorded).

#### En savoir plus – Audio-description (pré-enregistrée) (1.2.5) {#more-information-audio-description-prerecorded}

* [Compréhension du critère de réussite 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Comment remplir le critère de réussite 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adaptable (1.3) {#adaptable}

[Règle 1.3 - Adaptable : Créez un contenu qui peut être présenté de différentes manières (par exemple de manière plus simple) sans perdre d’informations ni de structure.](https://www.w3.org/TR/WCAG/#adaptable)

Cette ligne directrice couvre les exigences nécessaires pour soutenir les personnes qui :

* peuvent ne pas être en mesure d’accéder aux informations présentées par un auteur dans la présentation par défaut de ce contenu (par exemple, une mise en page à plusieurs colonnes ou une page utilisant intensivement des couleurs et/ou des images).

* utilisent peut-être un contenu audio uniquement ou un affichage visuel de remplacement, par exemple un contraste élevé ou une grande taille de texte.

### Informations et relations (1.3.1)  {#info-and-relationships}

* Critère de réussite 1.3.1
* Niveau A
* Informations et relations : Les informations, la structure et les relations véhiculées par la présentation peuvent être déterminées par programmation ou sont disponibles dans le texte.

#### Objectif – Informations et relations (1.3.1) {#purpose-info-and-relationships}

De nombreuses technologies d’assistance utilisées par les personnes en situation de handicap reposent sur des informations structurelles pour s’afficher de manière efficace ou *comprendre* contenu. Ces informations structurelles peuvent prendre la forme d’en-têtes de page, d’en-têtes de ligne et de colonne de tableau et de types de liste. Par exemple, un utilisateur peut recourir à un lecteur d’écran pour parcourir une page d’un titre à un autre. Cependant, si le contenu d’une page semble s’appuyer exclusivement sur une structure de style visuel plutôt que sur le code HTML sous-jacent, aucune information structurelle n’est disponible pour les technologies d’assistance, ce qui limite leur capacité à faciliter la navigation.

Ce critère de réussite vise à garantir que de telles informations structurelles sont fournies par programmation dans le code HTML, ou d’autres techniques de codage, de sorte que les navigateurs et les technologies d’assistance puissent y accéder pour les exploiter.

#### Comment procéder – Informations et relations (1.3.1) {#how-to-meet-info-and-relationships}

AEM facilite la construction de pages web significatives au sens sémantique à l’aide des éléments HTML appropriés. Ouvrez le contenu de votre page dans l’éditeur de texte enrichi (un composant Texte) et utilisez la variable **Paraformat** (symbole du paragraphe) pour spécifier l’élément structurel approprié (paragraphe et en-tête, par exemple).

Vous pouvez vous assurer que vos pages web disposent de la structure appropriée en utilisant, le cas échéant, les éléments suivants :

* **Titres :** Tant que les fonctions d’accessibilité de l’éditeur de texte enrichi sont activées, AEM offre trois niveaux d’en-tête de page. Vous pouvez les utiliser pour identifier les sections et sous-sections de contenu. En-tête 1 est le plus haut niveau d’en-tête, En-tête 3 le plus bas. L’administrateur système peut configurer le système pour autoriser l’utilisation d’un plus grand nombre de niveaux d’en-tête.

* **Listes** : vous pouvez spécifier trois types de listes différents en HTML :
   * L’élément `<ul>` est utilisé pour les listes *non triées* (à puces). Les éléments de liste individuels sont identifiés à l’aide de l’élément `<li>`. Dans l’éditeur de texte enrichi, utilisez la variable **Liste à puces** icône .
   * L’élément `<ol>` est utilisé pour les listes *numérotées*. Les éléments de liste individuels sont identifiés à l’aide de l’élément `<li>`. Dans l’éditeur de texte enrichi, cliquez sur l’icône **Liste numérotée**.

   Si vous souhaitez modifier le contenu existant en un type de liste spécifique, mettez en surbrillance le texte approprié et sélectionnez le type de liste approprié. Comme dans l’exemple précédent qui illustre la saisie du texte de paragraphe, les éléments de liste appropriés sont automatiquement ajoutés à votre HTML.

   En mode Plein écran, les icônes **Liste à puces** et **Liste numérotée** sont visibles. Lorsque vous n’êtes pas en mode Plein écran, les deux options sont disponibles derrière l’icône **Listes** unique.

* **Tableaux** : les tableaux de données doivent être identifiés à l’aide des éléments de tableau HTML :
   * un élément `<table>` ;
   * un élément `<tr>` pour chaque ligne du tableau ;
   * un élément `<th>` pour chaque en-tête de ligne et de colonne ;
   * un élément `<td>` pour chaque cellule de données.

   En outre, les tableaux accessibles utilisent les éléments et attributs suivants :

   * L’élément `<caption>` sert à fournir une légende visible pour le tableau. Par défaut, les légendes apparaissent centrées au-dessus du tableau, mais peuvent être positionnées de manière appropriée à l’aide de CSS. La légende est associée au tableau par programmation, ce qui en fait une méthode utile pour fournir une introduction au contenu.
   * L’élément `<summary>` aide les utilisateurs non voyants à comprendre plus facilement les informations présentées dans un tableau, en fournissant une synthèse de ce qu’un utilisateur voyant peut voir. Cela s’avère utile lorsque des mises en page de tableau complexes ou non conventionnelles sont utilisées (cet attribut n’est pas affiché dans le navigateur, il est uniquement lu pour les technologies d’assistance).
   * L’attribut `scope` de l’élément `<th>` sert à indiquer si une cellule représente un en-tête pour une ligne ou une colonne particulière. Une approche similaire consiste à utiliser les attributs header et id dans des tableaux complexes, où les cellules de données peuvent être associées à un ou plusieurs en-têtes.

   >[!NOTE]
   >
   >Par défaut, ces éléments et attributs ne sont pas directement disponibles, mais l’administrateur du système peut ajouter la prise en charge de ces valeurs dans la boîte de dialogue **Propriétés du tableau[ (voir** Ajout de la prise en charge des éléments et attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

   Pour ouvrir la **Tableau** dans laquelle vous pouvez sélectionner la **Propriétés du tableau** tab :

   * Définissez une **légende** appropriée.
   * Idéalement, supprimez toutes les valeurs par défaut pour **Largeur**, **Hauteur**, **Bordure**, **Marge intérieure des cellules** et **Espacement des cellules**. En effet, ces propriétés peuvent être définies dans une feuille de style globale.

   Vous pouvez ensuite utiliser les **propriétés de cellule** pour définir si la cellule est une cellule de données ou d’en-tête :

* **Mise en évidence** : utilisez l’élément `<strong>` ou `<em>` pour indiquer la mise en évidence. N’utilisez pas d’en-têtes pour mettre le texte en évidence au sein des paragraphes.
   * Mettez en surbrillance le texte à mettre en évidence ;
   * Cliquez sur le bouton **B** Icône (pour `<strong>`) ou le **I** Icône (pour `<em>`) affichés dans la variable **Propriétés** (assurez-vous que HTML est sélectionné).

      >[!NOTE]
      >
      >Dans une installation AEM standard, l’éditeur de texte enrichi est configuré pour utiliser :
      >
      >* `<b>` pour `<strong>`
      >* `<i>` pour `<em>`

      >
      >Ils sont identiques dans la pratique, mais `<strong>` et `<em>` sont préférables, car il s’agit de code HTML correct sémantiquement. Votre équipe de développement peut configurer l’éditeur de texte enrichi pour qu’il utilise `<strong>` et `<em>` (au lieu de `<b>` et `<i>`) lors du développement de votre instance de projet.

* **Tableaux de données complexes**: Parfois, lorsqu’il existe des tableaux complexes comportant deux niveaux ou plus d’en-têtes, les propriétés de tableau de base peuvent ne pas suffire à fournir toutes les informations structurelles nécessaires. Pour ce type de tableaux complexes, des relations directes doivent être créées entre les en-têtes et leurs cellules associées à l’aide de la fonction **header** et **id** attributs.

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

   Pour ce faire dans AEM, ajoutez les balises directement à l’aide du mode d’édition de la source.

   >[!NOTE]
   >
   >Cette fonctionnalité n’est pas disponible immédiatement dans une installation standard. Elle nécessite la configuration de l’éditeur de texte enrichi, des règles de HTML et du sérialiseur.

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

### Caractéristiques sensorielles (1.3.3)  {#sensory-characteristics}

* Critère de réussite 1.3.3
* Niveau A
* Caractéristiques sensorielles : les instructions données pour la compréhension et l’utilisation du contenu ne doivent pas reposer uniquement sur les caractéristiques sensorielles des éléments comme la forme, la taille, l’emplacement visuel, l’orientation ou le son.

#### Objectif – Caractéristiques sensorielles (1.3.3) {#purpose-sensory-characteristics}

Les concepteurs et conceptrices concentrent généralement leurs efforts sur le côté visuel (couleur, forme, style du texte, ou position absolue ou relative d’un élément du contenu) de la présentation des informations. Il peut s’agir de puissantes techniques de conception pour véhiculer l’information (et améliorer l’accessibilité globale pour les utilisateurs voyants ayant des besoins d’accessibilité cognitive), mais les personnes aveugles ou malvoyantes peuvent ne pas être en mesure d’accéder à des informations qui nécessitent l’identification visuelle d’attributs tels que la position, la couleur ou la forme.

De même, les informations qui nécessitent de distinguer différents sons (par exemple, du contenu parlé masculin ou féminin) présentent des obstacles à l’accessibilité pour les personnes malentendantes, si elles ne sont reflétées dans aucun texte secondaire pour le contenu audio.

>[!NOTE]
>
>Pour connaître les conditions requises en rapport avec les alternatives aux couleurs, voir [Utilisation de la couleur](#use-of-color).

#### Comment procéder – Caractéristiques sensorielles (1.3.3) {#how-to-meet-sensory-characteristics}

Assurez-vous que toutes les informations qui reposent sur les caractéristiques visuelles du contenu de la page sont également présentées dans un autre format.

* Ne vous fiez pas à la position visuelle pour donner des informations. Par exemple, si vous souhaitez renvoyer les utilisateurs vers un menu sur le côté droit de la page pour accéder à des informations supplémentaires, ne reportez-vous pas à la section *le menu de droite ;*; au lieu de cela, nommez le menu (par exemple au moyen d’un en-tête) et faites référence à ce nom dans le texte.
* Ne vous limitez pas au style de texte (texte en gras ou en italique, par exemple) comme seul moyen de transmettre l’information.

>[!NOTE]
>
>L’utilisation de termes descriptifs est acceptable s’ils ont une signification dans un contexte non visuel. Par exemple, en utilisant *above* et *below* serait généralement acceptable, car ils impliquent respectivement du contenu avant et après un élément de contenu particulier ; cela aurait encore du sens lorsque le contenu est parlé à haute voix.

#### En savoir plus – Caractéristiques sensorielles (1.3.3) {#more-information-sensory-characteristics}

* [Compréhension du critère de réussite 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Comment remplir le critère de réussite 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Perceptible (1.4) {#distinguishable}

[Règle 1.4 – Perceptible : faciliter la perception visuelle et auditive du contenu par l’utilisateur, notamment en séparant le premier plan de l’arrière-plan.](https://www.w3.org/TR/WCAG/#distinguishable)

### Utilisation de la couleur (1.4.1)  {#use-of-color}

* Critère de réussite 1.4.1
* Niveau A
* Utilisation de la couleur : La couleur n’est pas utilisée comme seul moyen visuel de transmettre des informations, d’indiquer une action, de demander une réponse ou de distinguer un élément visuel.

>[!NOTE]
>
>Ce critère de réussite traite spécifiquement de la perception des couleurs. Les autres formes de perception sont traitées à la règle [Adaptable (1.3)](#adaptable), comme l’accès à la couleur par programme informatique et les autres formes de codage de la présentation visuelle.

#### Objectif – Utilisation de la couleur (1.4.1) {#purpose-use-of-color}

La couleur est un moyen efficace d’améliorer l’aspect esthétique des pages web et est également utile pour véhiculer l’information. Cependant, il existe une gamme de déficiences visuelles, de la cécité à la déficience visuelle en matière de couleurs, ce qui signifie que certaines personnes sont incapables de distinguer certaines couleurs. Cela fait du codage par couleur un moyen peu fiable de fournir des informations.

Par exemple, une personne ayant une déficience visuelle de couleur rouge-vert ne pourra pas distinguer les nuances de vert et les nuances de rouge. Elles peuvent voir les deux couleurs comme une troisième couleur (marron, par exemple), auquel cas elles ne peuvent pas distinguer le rouge, le vert et le marron.

En outre, les personnes qui utilisent des navigateurs exclusivement textuels, des appareils d’affichage monochromes ou qui visualisent une impression en noir et blanc de la page ne peuvent pas percevoir les couleurs.

Il faut aussi tenir compte de la *selected* pour un élément d’interface (par exemple, les onglets, les boutons de bascule, etc.), qui doit être transmis d’une autre manière que par la couleur et au-delà d’une simple présentation visuelle. Pour ces éléments, l’utilisation supplémentaire de modèles, de formes et d’informations de programmation est utile pour créer une expérience utilisateur pleinement inclusive non limitée à un sens spécifique.

#### Comment procéder – Utilisation de la couleur (1.4.1) {#how-to-meet-use-of-color}

Si la couleur sert à véhiculer l’information, veillez à ce que cette information soit accessible sans recourir à la couleur.

Par exemple, assurez-vous que les informations fournies par couleur sont également fournies explicitement dans le texte.

Si la couleur est utilisée comme indice pour fournir des informations, vous devez fournir un indice visuel supplémentaire, tel que la modification du style (gras, italique, par exemple) ou de la police. Les utilisateurs et utilisatrices daltoniens ou souffrant d’une déficience visuelle peuvent alors distinguer les informations à l’écran. Cependant, il ne peut pas être entièrement fiable, car il n’aidera pas les personnes qui ne peuvent pas voir du tout la page. Il est donc (parfois) utile de fournir du texte caché ou d’utiliser des solutions programmatiques, comme la [suite de normes web ARIA (Accessible Rich Internet Applications)](https://www.w3.org/WAI/standards-guidelines/aria/) pour transmettre cette information à des utilisateurs non voyants.

#### En savoir plus – Utilisation de la couleur (1.4.1) {#more-information-use-of-color}

* [Compréhension du critère de réussite 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Comment remplir le critère de réussite 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Commande audio (1.4.2)  {#audio-control}

* Critère de réussite 1.4.2
* Niveau A
* Commande audio : si un contenu audio d’une page web est lu automatiquement pendant plus de 3 secondes, il existe, au choix, un mécanisme pour interrompre ou arrêter le contenu audio, ou un mécanisme pour commander le volume audio indépendamment du niveau de volume global du système.

#### Objectifs – Commande audio (1.4.2) {#purpose-audio-control}

Les personnes qui utilisent un logiciel de lecture d’écran peuvent avoir du mal à entendre la sortie vocale si d’autres fichiers audio sont lus en même temps. Cette difficulté est exacerbée lorsque la sortie vocale du lecteur d’écran est basée sur un logiciel (comme la plupart aujourd’hui) et contrôlée par la même commande de volume que le son. En outre, certaines personnes atteintes de déficiences cognitives et les personnes qui sont neurodivergent peuvent avoir une sensibilité sonore. Ces personnes ne parviennent pas à modifier le niveau de volume sur le contenu audio, ce qui les perturbe.

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
* Contraste (minimum) : La présentation visuelle du texte et des images du texte présente un rapport de contraste d’au moins 4,5:1, sauf pour ce qui suit :
   * Texte grand format : Le texte à grande échelle et les images de texte à grande échelle ont un rapport de contraste d’au moins 3:1.
   * Incident : Texte ou images de texte faisant partie d’un composant d’interface utilisateur inactif, [pure décoration](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), ne sont visibles par personne ou font partie d’une image qui contient un autre contenu visuel important, n’ont aucune exigence de contraste.
   * Logotypes : aucune exigence de contraste pour le texte faisant partie d’un logo ou d’un nom de marque.

   >[!NOTE]
   >
   >Voir [Présentation du contraste non textuel](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) pour plus d’informations, afin de vous assurer que les auteurs de contenu comprennent les exigences supplémentaires concernant les éléments non textuels (notamment les icônes, les éléments d’interface).

#### Objectif – Contraste (minimum) (1.4.3) {#purpose-contrast-minimum}

Les personnes avec certaines déficiences visuelles peuvent ne pas être en mesure de distinguer certaines paires de couleurs à faible contraste. Elles peuvent être confrontées à des obstacles à l’accessibilité si :

* Le texte est faiblement contrasté avec sa couleur d’arrière-plan.
* Le codage colorimétrique du texte (tel que le texte du lien et le texte hors lien) est important pour distinguer les informations.

>[!NOTE]
>
>Le texte utilisé uniquement à des fins décoratives est exclu de ce critère de réussite.

#### Comment procéder – Contraste (minimum) (1.4.3) {#how-to-meet-contrast-minimum}

Veillez à ce que le texte soit suffisamment contrasté par rapport à son arrière-plan. Les rapports de contraste dépendent de la taille et du style du texte en question :

* Pour le texte de moins de 18 points (ou 14 points en gras), le rapport de contraste entre le texte/les images de texte et l’arrière-plan doit être d’au moins 4.5:1.
* Pour le texte d’au moins 18 points (ou 14 points en gras), le rapport de contraste doit être d’au moins 3:1.
* Si un arrière-plan a un motif, l’arrière-plan autour du texte doit être ombré, de sorte que le rapport de 4.5:1 ou 3:1 soit préservé.

>[!NOTE]
>
>N’oubliez pas que les polices peuvent différer de la manière dont elles effectuent le rendu du dimensionnement PT/PX/EM équivalent.
>
>Faites preuve de bon sens et déposez le problème du côté lisible et convivial lorsque vous sélectionnez les polices et le dimensionnement appropriés au contenu web.

>[!NOTE]
>
>Les sites suivants peuvent vous aider à effectuer des conversions dans d’autres unités :
>
>* [Calculateur Px vers Em - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* Voir &quot;Conversion de la taille de la police : pixel-point-em-rem-percent&quot; à l’adresse `https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/`
>* Voir PMtoEM.com : Conversion PX/EM simplifiée à l’adresse `http://pxtoem.com/`


Pour vérifier les rapports de contraste, utilisez un outil de contraste des couleurs, tel que le [Analyseur de contraste des couleurs du groupe Paciello](https://www.paciellogroup.com/resources/contrast-analyser.html) ou le [Vérificateur de contraste des couleurs WebAIM](https://webaim.org/resources/contrastchecker/). Ces outils vous permettent de vérifier des paires de couleurs et de signaler tout problème de contraste.

Si vous êtes moins intéressé par l’aspect de votre page, vous pouvez également choisir de ne pas spécifier de couleurs de texte d’arrière-plan et de premier plan. Aucune vérification du contraste n’est requise, car le navigateur de l’utilisateur détermine les couleurs du texte et de l’arrière-plan.

S’il n’est pas possible de respecter les niveaux de contraste recommandés, fournissez un lien vers une version équivalente alternative de la page (qui ne présente aucun problème de contraste des couleurs). Vous pouvez également laisser l’utilisateur régler le contraste du modèle de couleurs de la page selon ses besoins.

#### En savoir plus – Contraste (minimum) (1.4.3) {#more-information-contrast-minimum}

* [Compréhension du critère de réussite 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Comment remplir le critère de réussite 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Redimensionner le texte (1.4.4)  {#resize-text}

* Critère de réussite 1.4.4
* Niveau A
* Redimensionner le texte : à l’exception des sous-titres et des images du texte, il est possible d’effectuer, sans technologie d’assistance, un redimensionnement atteignant 200 %, sans perte de contenu ou de fonctionnalité.

#### Objectif – Redimensionner le texte (1.4.4) {#purpose-resize-text}

Ce critère de réussite a pour but de s’assurer que le texte rendu visuellement, y compris les contrôles basés sur le texte (caractères de texte affichés pour être visibles [par rapport aux caractères de texte encore sous forme de données, en ASCII par exemple]), puisse être mis à l’échelle avec succès. Il pourra ainsi être lu directement par les personnes atteintes de déficiences visuelles légères, qui n’auront pas besoin d’une technologie d’assistance, par exemple d’une loupe. Les utilisateurs peuvent bénéficier de la mise à l’échelle de tout le contenu de la page web, mais l’élément le plus crucial est le texte.

#### Comment procéder – Redimensionner le texte (1.4.4) {#how-to-meet-resize-text}

En plus de suivre les instructions de la section [Comment remplir le critère de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) vous pouvez encourager les auteurs de contenu à utiliser des largeurs et hauteurs fluides et flexibles dans leurs conceptions de page et tailles de police (par exemple, conception web réactive) pour permettre aux lecteurs de redimensionner le texte.

#### En savoir plus – Redimensionner le texte (1.4.4) {#more-information-resize-text}

* [Compréhension du critère de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Comment remplir le critère de réussite 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Texte sous forme d’image (1.4.5) {#images-of-text}

* Critère de réussite 1.4.5
* Niveau AA
* Texte sous forme d’image : si les technologies utilisées peuvent réaliser la présentation visuelle, du texte est utilisé pour véhiculer l’information plutôt que du texte sous forme d’image sauf dans les cas suivants :
   * Personnalisable : L’image du texte peut être visuellement personnalisée en fonction des besoins de l’utilisateur.
   * Essentiel : Une présentation particulière du texte est essentielle à la transmission de l&#39;information.

>[!NOTE]
>
>Les logotypes (texte faisant partie d’un logo ou d’un nom de marque) sont considérés comme essentiels.

#### Objectif – Texte sous forme d’image (1.4.5) {#purpose-images-of-text}

Les images de texte sont souvent utilisées lorsqu’un style de texte particulier est privilégié, par exemple, un logotype ou si le texte a été généré à partir d’une autre source (la numérisation d’un document papier, par exemple). Cependant, par rapport au texte présenté au format HTML dans le style CSS, les images de texte n’offrent pas la possibilité de modifier leur taille ou leur apparence, des fonctionnalités parfois nécessaires pour les personnes avec des déficiences visuelles ou présentant des difficultés de lecture.

#### Comment procéder – Texte sous forme d’image (1.4.5) {#how-to-meet-images-of-text}

Si des images de texte doivent être utilisées, utilisez CSS pour remplacer les images de texte par du texte équivalent en HTML afin que le texte soit disponible de manière personnalisable. Pour consulter un exemple, reportez-vous à la section [C30 : Utilisation de CSS pour remplacer le texte par des images de texte et fourniture de commandes d’interface utilisateur pour basculer](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

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
* Clavier : toutes les fonctionnalités du contenu sont exploitables à l’aide d’une interface clavier, sans nécessiter de minutage spécifique pour les touches individuelles, sauf lorsque la fonction sous-jacente nécessite une entrée dépendant du chemin du mouvement de l’utilisateur et pas seulement des points de terminaison.

#### Objectif - Clavier (2.1.1) {#purpose-keyboard}

Ce critère de réussite a pour but de permettre, dans la mesure du possible, d’utiliser le contenu à l’aide d’un clavier ou d’une interface de clavier (pour pouvoir utiliser un clavier supplémentaire). Lorsque le contenu peut être utilisé à l’aide d’un clavier ou d’un clavier alternatif, il est exploitable pour les personnes sans vision (qui ne peuvent pas utiliser d’appareils tels que les souris qui nécessitent une coordination oculaire) et pour les personnes qui doivent utiliser des claviers alternatifs ou des périphériques d’entrée qui agissent comme émulateurs de clavier. Les émulateurs de clavier comprennent des logiciels d’entrée vocale, des logiciels d’aperçu, des claviers à l’écran, des logiciels de numérisation, ainsi que divers claviers alternatifs et technologies d’assistance. Les personnes malvoyantes peuvent également avoir des difficultés à suivre un pointeur et trouver l’utilisation d’un logiciel beaucoup plus facile (ou seulement possible) si elles peuvent le contrôler à partir du clavier.

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

Ce critère de réussite a pour but de s’assurer que les utilisateurs en situation de handicap disposent, chaque fois que possible, du temps nécessaire pour interagir avec le contenu web. Les personnes atteintes de déficiences visuelles (cécité, malvoyance, troubles de la dextérité) et de limitations cognitives peuvent avoir besoin d’un temps supplémentaire pour lire le contenu ou pour mettre en œuvre certaines fonctions, comme compléter des formulaires en ligne. Si les fonctions web dépendent du temps, il sera difficile pour certains utilisateurs d’effectuer l’action requise avant qu’une limite de temps soit atteinte. Dans ce cas, le service leur est inaccessible. La conception de fonctions qui ne dépendent pas du temps aide les personnes en situation de handicap à accomplir ces fonctions. Le fait de fournir des options pour désactiver les limites de temps, personnaliser la durée ou demander plus de temps avant qu’une limite de temps ne se produise permet aux utilisateurs qui ont besoin de plus de temps que prévu pour effectuer les tâches avec succès. Ces options sont répertoriées dans l’ordre le plus pratique pour l’utilisateur. Désactiver les limites de temps est préférable à la personnalisation de la durée, elle-même préférable à l’octroi d’un temps supplémentaire avant d’atteindre une limite de temps.

#### Comment procéder – Réglage du minutage (2.2.1) {#how-to-meet-timing-adjustable}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### En savoir plus – Réglage du minutage (2.2.1) {#more-information-timing-adjustable}

* [Compréhension du critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Comment remplir le critère de réussite 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Mettre en pause, arrêter, masquer (2.2.2)  {#pause-stop-hide}

* Critère de réussite 2.2.2
* Niveau A
* Mettre en pause, arrêter, masquer : pour toute information en mouvement, clignotante, défilante ou mise à jour automatiquement, tous les points suivants sont vrais :
   * Déplacement, clignotement, défilement : Pour toute information en mouvement, clignotante ou défilante qui (a) démarre automatiquement, (b) dure plus de cinq secondes, et (c) est présentée en parallèle à d’autres contenus, il existe un mécanisme permettant à l’utilisateur de la suspendre, de l’arrêter ou de la masquer à moins que le mouvement, la clignotante ou le défilement ne fassent partie d’une activité où il est essentiel ;
   * Mise à jour automatique : Pour toute information mise à jour automatiquement qui (a) démarre automatiquement et (b) est présentée en parallèle avec d’autres contenus, il existe un mécanisme permettant à l’utilisateur de la mettre en pause, de l’arrêter ou de la masquer, ou de contrôler la fréquence de la mise à jour, sauf si la mise à jour automatique fait partie d’une activité où elle est essentielle.

Les points à noter sont les suivants :

1. Pour les exigences relatives au contenu scintillant ou flashant, se référer à la règle Ne pas concevoir de contenu susceptible de provoquer des crises (2.3).
1. Puisque tout contenu ne satisfaisant pas ce critère de réussite peut interférer avec la capacité de l’utilisateur à exploiter la page entière, tout le contenu présent dans la page web (qu’il soit utilisé pour satisfaire d’autres critères de réussite ou non) doit satisfaire ce critère de réussite. Voir [Exigence de conformité 5 : Non-interférence](https://www.w3.org/TR/WCAG20/#cc5).
1. Le contenu mis à jour régulièrement par un logiciel ou diffusé en continu à l’agent utilisateur n’est pas nécessaire pour conserver ou présenter des informations générées ou reçues entre le lancement de la mise en pause et la reprise de la présentation, car cela peut ne pas être techniquement possible et dans de nombreuses situations peut induire en erreur.
1. Une animation qui se produit dans le cadre d’une phase de préchargement ou d’une situation similaire peut être considérée comme essentielle si l’interaction ne peut pas se produire au cours de cette phase pour tous les utilisateurs et si ne pas indiquer la progression, cela peut dérouter les utilisateurs ou les faire croire que le contenu a été figé ou cassé.

#### Objectif – Mettre en pause, arrêter, masquer (2.2.2) {#purpose-pause-stop-hide}

Certains utilisateurs peuvent trouver les contenus mobiles gênants, voire douloureux physiquement, ce qui crée pour eux des difficultés à se concentrer sur d’autres parties de la page. En outre, un tel contenu peut s’avérer difficile à lire pour les personnes qui ont du mal à suivre le texte en mouvement.

#### Comment procéder – Mettre en pause, arrêter, masquer (2.2.2) {#how-to-meet-pause-stop-hide}

Selon la nature du contenu, vous pouvez appliquer une ou plusieurs des suggestions suivantes lors de la création de pages web contenant du contenu mobile, clignotant ou clignotant :

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
* Trois Flashs ou sous le seuil critique : Les pages Web ne contiennent rien qui clignote plus de trois fois au cours d’une période d’une seconde, ou le flash est inférieur aux seuils Flash généraux et rouges.

>[!NOTE]
>
>Étant donné que tout contenu qui ne répond pas à ce critère de réussite peut interférer avec la capacité d’un utilisateur à utiliser la page entière, tout le contenu de la page web (qu’il soit utilisé pour satisfaire d’autres critères de réussite ou non) doit satisfaire à ce critère de réussite. Voir [Exigence de conformité 5 : Non-interférence](https://www.w3.org/TR/WCAG/#cc5).

#### Objectif – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#purpose-three-flashes-or-below-threshold}

Il arrive que le contenu qui flashe provoque des crises de photosensibilité. En appliquant ce critère de réussite, les utilisateurs concernés peuvent accéder au contenu et en prendre connaissance sans inquiétude quant au contenu qui flashe.

#### Comment procéder – Pas plus de trois flashs ou sous le seuil critique (2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

Prenez des mesures pour vous assurer que les techniques suivantes sont appliquées :

* Assurez-vous que les composants ne clignotent pas plus de trois fois au cours d’une période d’une seconde ;
* Si la condition ci-dessus ne peut pas être remplie, affichez le contenu clignotant dans une *petite zone sécurisée* en pixels sur l’écran. Cette zone est calculée à l&#39;aide d&#39;une formule complexe, couverte par la section [G176 : Maintenir la zone de clignotement suffisamment petite](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), cette technique ne doit donc être suivie que si le contenu clignotant est *nécessaire.

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

Ce critère de réussite a pour but de permettre aux personnes qui naviguent de manière séquentielle dans le contenu d’accéder plus directement au contenu principal de la page web. Les pages web et les applications contiennent souvent du contenu qui s’affiche sur d’autres pages ou écrans. Parmi les exemples de blocs de contenu répétés, citons, entre autres, les liens de navigation, les graphiques de titres et les encadrés publicitaires. Les petites sections répétées, telles que des mots individuels, des expressions ou des liens uniques, ne sont pas considérées comme des blocs aux fins de cette disposition.

#### Comment procéder – Contournement de blocs (2.4.1) {#how-to-meet-bypass-blocks}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### En savoir plus – Contournement de blocs (2.4.1) {#more-information-bypass-blocks}

* [Compréhension du critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Comment remplir le critère de réussite 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Titre de page (2.4.2)  {#page-titled}

* Critère de réussite 2.4.2
* Niveau A
* Titre de page : Les pages web comportent des titres qui décrivent la rubrique ou l’objectif.

#### Objectif – Titre de page (2.4.2) {#purpose-page-titled}

Ce critère de réussite permet à chacun, indépendamment d’une déficience particulière, d’identifier rapidement le contenu d’une page web sans lire la page dans son intégralité. Cela s’avère utile lorsque plusieurs pages web sont ouvertes dans des onglets de navigateur, car le titre de la page s’affiche dans l’onglet et peut donc être localisé rapidement.

#### Comment procéder – Titre de page (2.4.2) {#how-to-meet-page-titled}

Lorsqu’une nouvelle page HTML est créée dans AEM, vous pouvez spécifier son titre. Assurez-vous que le titre décrit correctement le contenu et l’objectif de la page, en particulier tous les aspects uniques, afin que les visiteurs puissent rapidement identifier si le contenu correspond à leurs besoins.

Vous pouvez également changer le titre d’une page que vous modifiez en sélectionnant : **Informations sur la page** – **Propriétés.**

#### En savoir plus – Titre de page (2.4.2) {#more-information-page-titled}

* [Compréhension du critère de réussite 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Comment remplir le critère de réussite 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Ordre de focus (2.4.3)  {#focus-order}

* Critère de réussite 2.4.3
* Niveau A
* Ordre de focus : s’il est possible de naviguer de manière séquentielle dans une page web et que les séquences de navigation affectent la signification ou le fonctionnement, l’attribution du focus aux composants concernés obéit à un ordre préservant la signification et la maniabilité.

#### Objectif – Ordre de focus (2.4.3) {#purpose-focus-order}

Ce critère de réussite a pour but de s’assurer que, lorsque les utilisateurs naviguent de manière séquentielle dans le contenu, ils rencontrent des informations dans un ordre compatible avec la signification de ce contenu et qu’il puisse être utilisé à l’aide du clavier. Ce critère diminue la confusion en permettant aux utilisateurs de former un modèle mental cohérent du contenu. Différents ordres correspondant aux relations logiques au sein du contenu peuvent coexister. Il peut s’agir, par exemple, de parcourir des composants dans un formulaire en ligne composé de différents champs et/ou étapes, en correspondance avec les relations logiques au sein du contenu.

#### Comment procéder – Ordre de focus (2.4.3) {#how-to-meet-focus-order}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### En savoir plus – Ordre de focus (2.4.3) {#more-information-focus-order}

* [Compréhension du critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Comment remplir le critère de réussite 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Fonction du lien (selon le contexte) (2.4.4)  {#link-purpose-in-context}

* Critère de réussite 2.4.4
* Niveau A
* Fonction du lien (selon le contexte) : la fonction de chaque lien est déterminée par le texte du lien seul ou par le texte du lien associé à un contexte du lien déterminé par un programme informatique, sauf si la fonction du lien est ambiguë pour tout utilisateur.

#### Objectif – Fonction du lien (selon le contexte) (2.4.4) {#purpose-link-purpose-in-context}

Pour tous les utilisateurs, qu’ils aient une déficience ou non, il est essentiel d’indiquer clairement la direction d’un lien par le biais du texte du lien approprié. Cela permet aux utilisateurs de décider s’ils souhaitent réellement suivre un lien. Pour les utilisateurs voyants, un texte de lien significatif est utile lorsqu’il existe plusieurs liens sur une page (en particulier si la page contient beaucoup de texte), car un texte de lien significatif fournit une indication plus claire de la fonctionnalité de la page cible. D’un autre côté, les utilisateurs de technologies d’assistance peuvent générer une liste de tous les liens sur une seule page, et ainsi comprendre plus facilement le texte du lien hors contexte, s’il est à la fois unique et informatif. Cependant, les personnes voyantes souffrant d’un handicap cognitif peuvent être perturbées si un lien ne fournit pas suffisamment d’informations pour décrire précisément où le lien les mène.

#### Comment procéder – Fonction du lien (selon le contexte) (2.4.4) {#how-to-meet-link-purpose-in-context}

Avant tout, veillez à ce que l’objectif d’un lien soit clairement décrit dans le texte du lien.

* Mauvais exemple :
   * Texte : Pour plus de détails sur nos cours du soir de l’automne 2010, cliquez ici.
   * Motif : le lien est ambigu et n’indique pas clairement sa destination.
* Bon exemple :
   * Texte : Cours du soir de l’automne 2010 – Détails.
   * Motif : il est possible d’améliorer le texte du lien en adaptant légèrement le texte et sa position.

Les liens doivent être formulés de manière cohérente sur toutes les pages, en particulier pour les barres de navigation. Si, par exemple, un lien vers une page spécifique est nommé **Publications** sur une page, il doit être nommé de la même façon sur toutes les autres pages.

Au moment de la rédaction de cet article, l’utilisation des attributs de titre pose certains problèmes. Ils ne permettent pas de s’assurer que des liens similaires présentés sur une page donnent des informations uniques sur la destination (par exemple, la mention « en savoir plus » se rapporte souvent à un ensemble de destinations différentes) :

* Le texte contenu dans l’attribut title n’est disponible que sous la forme d’une info-bulle contextuelle pour les utilisateurs de souris. Il n’est pas possible d’y accéder de manière cohérente à l’aide du clavier ou pour les utilisateurs mobiles.
* Les lecteurs d’écran peuvent lire les attributs de titre, mais cette fonctionnalité peut ne pas être activée par défaut. par conséquent, les utilisateurs peuvent ne pas connaître l’existence d’un attribut de titre.
* Il est difficile de changer l&#39;aspect du texte du titre, ce qui signifie qu&#39;il peut être difficile ou impossible à lire pour certaines personnes.

Ainsi, bien que l’attribut de titre puisse être utilisé pour fournir un contexte supplémentaire à un lien, gardez à l’esprit ses limites et ne l’utilisez pas comme alternative au texte du lien approprié.

Si le lien est composé d’une image, veillez à ce que le texte secondaire de l’image décrive la destination du lien. Par exemple, si une image de bibliothèque est définie comme lien vers les publications d’une personne, le texte secondaire doit indiquer **Publications de Jean Dupont** et non **Bibliothèque**.

Si l’ancre de lien contient du texte qui décrit l’objet du lien en plus de l’élément image (et donc que le texte apparaît à côté de l’image), utilisez un attribut alt vide pour l’image :

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
>
>Le fragment de code ci-dessus est une illustration. Il est recommandé d’utiliser la variable **Image** composant.

Bien qu’il soit conseillé de spécifier un texte du lien qui identifie l’objectif du lien sans avoir besoin de contexte supplémentaire, il est admis que cela n’est pas toujours possible. Il est possible d’utiliser des liens dépourvus de contexte dans les cas suivants. Un certain nombre d’exemples HTML figurent dans la section [Comment remplir le critère de réussite 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Le texte du lien fait partie d’une liste de liens étroitement liés et lorsque l’élément de liste encadrant le lien fournit suffisamment de contexte.
* L’objet d’un lien peut être clairement identifié à partir de la fonction *previous* texte du paragraphe (et non le texte suivant).
* Le lien est contenu dans un tableau de données et l’objectif peut donc être clairement identifié à partir des en-têtes associés.
* Une liste de liens est contenue dans un ensemble d’en-têtes et l’en-tête lui-même fournit un contexte approprié.
* Une liste de liens est contenue dans un lien imbriqué et l’élément de liste parent situé au-dessus du lien imbriqué fournit un contexte approprié.

Parfois, lorsqu’il existe plusieurs liens sur une page (chacun d’eux fournit la direction d’un lien avec des détails complexes mais nécessaires), il peut être approprié de fournir une version alternative de la page web qui affiche exactement le même contenu, mais lorsque le texte du lien n’est pas aussi détaillé.

Vous pouvez également utiliser des scripts de sorte qu’une quantité minimale de texte soit fournie dans le lien lui-même. Lors de l’activation d’un contrôle approprié positionné en haut de la page, le texte du lien est *expand* plus de détails. Une approche similaire consiste à utiliser CSS pour *masquer* le lien complet des utilisateurs voyants, mais il est toujours affiché en plein écran pour les utilisateurs de lecteurs d’écran. Cela ne relève pas du présent document, mais vous trouverez plus d&#39;informations sur la façon d&#39;y parvenir dans la section [En savoir plus - Fonction du lien (selon le contexte) (2.4.4)](#more-information-link-purpose-in-context) .

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

Lorsque le critère de réussite indique « mode de fonctionnement », cela sert à prendre en compte des plateformes qui n’affichent pas toujours un indicateur de focus. En règle générale, il n’existe qu’un seul mode de fonctionnement. Ce critère de réussite s’applique donc.

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
* Langue de la page : La langue humaine par défaut de chaque page web peut être déterminée par programmation.

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
>AEM permet d’affiner davantage les variations d’une langue racine ; par exemple, l’anglais américain - en-us, l’anglais britannique - en-gb et l’anglais canadien - en-ca. Ce niveau de détail est souvent superflu pour les technologies d’assistance, même s’il est utile pour les variantes régionales du contenu des pages.

#### En savoir plus – Langue de la page (3.1.1) {#more-information-language-of-page}

* [Compréhension du critère de réussite 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Comment remplir le critère de réussite 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Les codes reposent sur la norme ISO 639-1. Vous trouverez une liste de codes plus complète pour chaque langue sur le site [W3Schools.com](https://www.w3schools.com/tags/ref_language_codes.asp).

### Langue d’un passage (3.1.2)  {#language-of-parts}

* Critère de réussite 3.1.2
* Niveau AA
* Langue d’un passage : La langue humaine de chaque passage ou expression dans le contenu peut être déterminée par programmation. Les exceptions sont les noms propres, les termes techniques, les mots d&#39;une langue indéterminée, ainsi que les mots ou expressions qui sont devenus partie intégrante du langage courant du texte qui l&#39;entoure immédiatement.

#### Objectif – Langue d’un passage (3.1.2) {#purpose-language-of-parts}

L’objectif de ce critère de réussite est similaire au critère de réussite. [Langue de la page](#language-of-page), sauf qu’il s’applique aux pages web comportant du contenu dans plusieurs langues sur une seule page (en raison, par exemple, de citations ou de mots empruntés peu courants).

Les pages appliquant ce critère de réussite permettent :

* Logiciel de transition en braille pour insérer des caractères accentués.
* Les lecteurs d’écran peuvent prononcer correctement les mots contenant des caractères spéciaux ou délivrés dans une autre langue que celle par défaut, identifiée sur la page.
* Les outils de traduction du type Google Translate peuvent correctement traduire les mots d’une langue à une autre.

#### Comment procéder – Langue d’un passage (3.1.2) {#how-to-meet-language-of-parts}

Le `lang` peut être utilisé pour identifier les modifications dans la langue du contenu. Par exemple, une citation en allemand (code ISO 639-1 « de ») peut s’afficher comme suit :

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
>Il n’est pas nécessaire de suivre ce critère de réussite lors de l’inclusion de noms ou de villes dans différentes langues. Ou, lorsque vous utilisez des mots ou expressions empruntés qui sont devenus courants dans la langue par défaut, comme *schadenfreude* en anglais.

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

Le focus peut être déplacé vers un contrôle à l’aide du clavier (par exemple, en accédant à un contrôle à l’aide de la touche de tabulation) ou à l’aide de la souris (par exemple, en cliquant sur un champ de texte). Le déplacement de la souris au-dessus d’un contrôle n’a aucun effet sur le focus, sauf si un script implémente ce comportement. Pour certains types de contrôles, cliquer sur un contrôle peut également activer le contrôle (par exemple, un bouton), ce qui peut, à son tour, déclencher une modification de contexte.

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

Ce critère de réussite a pour but de s’assurer que la saisie de données ou la sélection d’un contrôle de formulaire a des effets prévisibles. La modification du paramètre d’un composant de l’interface utilisateur modifie un aspect du contrôle qui persiste lorsque l’utilisateur n’interagit plus avec celui-ci. Ainsi, cocher une case, saisir du texte dans un champ ou modifier l’option sélectionnée dans un contrôle de liste modifie le paramétrage, alors que l’activation d’un lien ou d’un bouton le laisse inchangé. Les changements de contexte peuvent dérouter les utilisateurs s’ils ne les perçoivent pas aisément ou s’ils sont facilement déconcentrés par la modification. Les changements de contexte ne sont appropriés que lorsqu’il est clair qu’un tel changement se produit en réponse à l’action de l’utilisateur.

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

Ce critère de réussite a pour but d’encourager l’utilisation d’une présentation et d’une mise en page cohérentes pour les utilisateurs qui interagissent avec du contenu répété dans un ensemble de pages web et qui doivent rechercher plusieurs fois des informations ou des fonctionnalités spécifiques. Les personnes malvoyantes qui utilisent la loupe pour agrandir une petite partie de l’écran utilisent souvent des repères visuels et des limites de pages pour localiser rapidement un contenu répété. De même, la présentation d’un contenu répété dans le même ordre est importante pour les utilisateurs visuels qui font appel à leur mémoire spatiale ou à des repères visuels dans la représentation graphique pour localiser ce contenu.

Il est important de noter que l’expression « dans le même ordre » de cette section ne signifie pas l’impossibilité d’utiliser des menus connexes, des blocs de navigation secondaires ou une structure de page complémentaire. Ce critère de réussite est plutôt destiné à aider les utilisateurs qui interagissent avec du contenu répété sur plusieurs pages web à prédire l’emplacement du contenu qu’ils recherchent. Et de le trouver plus rapidement quand ils le redécouvrent.

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

Ce critère de réussite a pour but d’assurer une identification cohérente des composants fonctionnels qui apparaissent à plusieurs reprises dans un ensemble de pages web. L’une des stratégies des utilisateurs de lecteurs d’écran pour parcourir un site web consiste à s’appuyer abondamment sur leur connaissance des fonctions présentées sur différentes pages. Si des fonctions identiques comportent des libellés différents (ou, plus généralement, un nom accessible différent) sur différentes pages Web, le site est beaucoup plus difficile à utiliser. La situation peut en outre dérouter les personnes atteintes de limitations cognitives et accroître la charge en la matière. Par conséquent, l’étiquetage cohérent aide.

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

Ce critère de réussite a pour but de s’assurer que les utilisateurs sont conscients qu’une erreur s’est produite et qu’ils peuvent déterminer ce qui ne va pas. Le message d’erreur doit être aussi précis que possible. Dans le cas d’un envoi de formulaire infructueux, le fait de réafficher le formulaire et d’indiquer les champs erronés ne suffit pas pour que certains utilisateurs puissent percevoir qu’une erreur s’est produite. Les utilisateurs de lecteurs d’écran, par exemple, ne savent pas qu’une erreur s’est produite tant qu’ils n’ont pas rencontré l’un des indicateurs. Il est possible qu’ils abandonnent complètement le formulaire avant d’identifier l’indicateur d’erreur, en pensant que la page n’est tout simplement pas fonctionnelle. Selon la définition des règles WCAG, une [erreur de saisie](https://www.w3.org/TR/WCAG/#dfn-input-error) correspond à une information fournie par l’utilisateur et qui n’est pas acceptée. Cela inclut les éléments suivants.

Informations requises par la page web, mais omises par l’utilisateur, ou informations fournies par l’utilisateur, mais non conformes au format de données requis ou aux valeurs autorisées.
Par exemple :

* l’utilisateur ne saisit pas l’abréviation appropriée dans le champ état, province ou région ;
* l’utilisateur saisit une abréviation d’État non valide ;
* l’utilisateur saisit un code postal inexistant ;
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
* Étiquettes ou instructions : Des libellés ou des instructions sont fournis lorsque le contenu nécessite une saisie de l’utilisateur.

#### Objectif – Étiquettes ou instructions (3.3.2) {#purpose-labels-or-instructions}

Fournir des instructions pour aider les personnes à remplir des formulaires est une partie essentielle des bonnes pratiques en matière d’utilisation de l’interface. Cela s’avère utile pour les personnes ayant des déficiences visuelles ou cognitives qui auraient autrement des difficultés à comprendre la disposition d’un formulaire et le type de données à fournir dans un champ de formulaire particulier.

##### Formulaires

Dans le projet de démonstration AEM WKND, une étiquette par défaut est ajoutée lorsque vous ajoutez un composant de formulaire à la page, par exemple un **champ de texte**. Ce titre par défaut dépend du type de composant. Vous pouvez ajouter votre propre titre dans le **Titre et texte** de la boîte de dialogue de modification de ce champ. Il est important de s’assurer que les étiquettes aident les utilisateurs à comprendre les données associées à chaque composant de formulaire.

Utilisez ce champ **Titre** pour les éléments de champ, car il fournit une étiquette accessible par les technologies d’assistance. Le simple fait d’écrire une étiquette dans le texte en regard du champ ne suffit pas.

Pour certains composants de formulaire, il est également possible de masquer visuellement les libellés à l’aide de la fonction **Masquer le titre** . Les libellés masqués de cette manière sont toujours disponibles pour les dispositifs d’assistance, mais ne s’affichent pas à l’écran. Bien qu’il s’agisse d’une bonne approche dans certaines situations, il est préférable d’inclure un libellé visuel dans la mesure du possible, car certains utilisateurs peuvent consulter une petite section de l’écran (un champ à la fois) et avoir besoin des libellés pour identifier correctement le champ.

###### Boutons Image {#image-buttons}

Lorsque des boutons d’image sont utilisés (par exemple, **Bouton Image** composant du projet WKND), la variable **Titre** dans le champ **Titre et texte** de la boîte de dialogue de modification fournit en fait le texte de remplacement de l’image, plutôt que le libellé. Ainsi, dans l’exemple ci-dessous, l’image avec le texte `Submit` comporte le texte secondaire `Submit`, ajouté à l’aide du champ **Titre** dans la boîte de dialogue de modification.

###### Groupes de champs de formulaire {#groups-of-form-fields}

Dans le projet WKND, où il existe un groupe de contrôles connexes, tels que **Groupe de cases d’option**, un titre peut être nécessaire pour le groupe et des contrôles individuels. Lors de l’ajout d’un ensemble de boutons radio dans AEM, le champ **Titre** fournit le titre de ce groupe, tandis que les titres individuels sont spécifiés lors de la création des boutons radio (**Éléments**).

Cependant, il n’existe aucune association par programmation entre le titre du groupe et les boutons radio eux-mêmes. Les éditeurs de modèles doivent placer le titre dans le champ nécessaire `fieldset` et `legend` pour créer cette association, vous ne pouvez le faire qu’en modifiant le code source de la page. Un administrateur système peut également ajouter la prise en charge de ces éléments afin qu’ils apparaissent dans la boîte de dialogue **Propriétés du champ** (voir [Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

###### Considérations supplémentaires pour les formulaires {#additional-considerations-for-forms}

Si les données doivent être saisies dans un format spécifique, précisez-le dans le texte du libellé. Par exemple, si une date doit être saisie au format `DD-MM-YYYY`, indiquez-le spécifiquement dans le libellé. Cela signifie que lorsque les utilisateurs de lecteurs d’écran rencontrent le champ, le libellé est automatiquement annoncé, ainsi que les informations supplémentaires sur le format.

Si la saisie d’un champ de formulaire est obligatoire, indiquez-le en utilisant le mot « obligatoire » dans le libellé. AEM ajoute un astérisque lorsqu’un champ est obligatoire, mais il serait idéal d’inclure le mot `required` dans le libellé lui-même (dans le champ **Titre** de la boîte de dialogue de modification).

Le positionnement des libellés est également important, car ils permettent de localiser les champs appropriés. Cela est tout particulièrement important lorsque l’utilisateur est confronté à un formulaire complexe. Suivez les conventions ci-dessous :

* Cases à cocher ou cases d’option :
Les libellés sont positionnés immédiatement à droite du champ.
* Tous les autres composants de formulaire (par exemple, zones de texte, zones de liste modifiable) :
les libellés sont positionnés immédiatement au-dessus ou à gauche du champ.

Dans les formulaires simples avec des fonctionnalités limitées, étiquetez correctement une `Submit` peut agir comme libellé pour le champ adjacent (par exemple `Search`). Cela s’avère utile dans les cas où il peut être difficile de trouver de l’espace pour le texte du libellé.

#### En savoir plus – Étiquettes ou instructions (3.3.2) {#more-information-labels-or-instructions}

* [Compréhension du critère de réussite 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Comment remplir le critère de réussite 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Suggestion d’erreur (3.3.3)  {#error-suggestion}

* Critère de réussite 3.3.3
* Niveau AA
* Clavier : si une erreur de saisie est automatiquement détectée et que des suggestions de correction sont connues, ces suggestions sont proposées à l’utilisateur, sauf si elles compromettent la sécurité ou l’objectif du contenu.

#### Objectif – Suggestion d’erreur (3.3.3) {#purpose-error-suggestion}

Ce critère de réussite a pour but de s’assurer que les utilisateurs reçoivent des suggestions appropriées pour corriger, si possible, une erreur de saisie. Selon les règles WCAG, une [erreur de saisie](https://www.w3.org/TR/WCAG/#dfn-input-error) indique que « l’information fournie par l’utilisateur n’est pas acceptée » par le système. À titre d’exemples de saisies non acceptées, figurent les informations requises, mais omises par l’utilisateur, et celles fournies par l’utilisateur, mais non conformes au format de données requis ou aux valeurs autorisées.

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

Ce critère de réussite a pour but d’aider les utilisateurs en situation de handicap à éviter les conséquences graves d’une erreur lorsqu’ils effectuent une action qui ne peut pas être annulée. Par exemple, l’achat de billets d’avion non remboursables ou le lancement d’un ordre d’achat d’actions par le biais d’un compte de courtage sont des transactions financières assorties de graves conséquences. Si un utilisateur a commis une erreur sur la date du voyage en avion, il peut se retrouver avec un billet pour le mauvais jour qui ne peut pas être échangé. Si l&#39;utilisateur a commis une erreur sur le nombre de parts d&#39;actions à acheter, il pourrait acheter plus d&#39;actions que prévu. Ces deux types d&#39;erreurs coûteuses impliquent des transactions qui ont lieu immédiatement et qui ne peuvent pas être modifiées par la suite. De même, il peut s’agir d’une erreur irrécupérable si les utilisateurs modifient ou suppriment involontairement des données stockées dans une base de données à laquelle ils doivent accéder ultérieurement, par exemple l’intégralité de leur profil de voyage sur un site web de services de voyage. En ce qui concerne la modification ou la suppression de données « contrôlables par l’utilisateur », l’objectif est d’empêcher la perte massive de données, par exemple la suppression d’un fichier ou d’un enregistrement. L’objectif ne consiste pas à exiger une confirmation pour chaque commande d’enregistrement ou les opérations de création ou de modification simple de documents, d’enregistrements ou d’autres données.

Les utilisateurs en situation de handicap sont plus enclins à commettre des erreurs. Les personnes atteintes de difficultés de lecture peuvent avoir tendance à transposer les chiffres et les lettres, et celles souffrant de troubles moteurs à actionner des touches par erreur. La possibilité d’annuler des actions permet aux utilisateurs de corriger une erreur pouvant avoir de graves conséquences. Pouvoir vérifier et corriger des informations donne à l’utilisateur la possibilité de détecter une erreur avant d’effectuer une action d’une portée considérable.

Les données contrôlables par l’utilisateur sont des données visibles pour lui, et qu’il peut modifier ou supprimer de manière intentionnelle. À titre d’exemple, le contrôle de ces données par un utilisateur peut consister à mettre à jour le numéro de téléphone et l’adresse indiqués dans son compte ou à supprimer d’anciennes factures enregistrées sur un site web. Il ne s’agit pas d’éléments comme les données relatives à la surveillance de moteurs de recherche et de journaux Internet que l’utilisateur ne peut pas voir ni utiliser directement.

#### Comment procéder – Prévention des erreurs (juridiques, financières, données) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### En savoir plus – Prévention des erreurs (juridiques, financières, données) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Compréhension du critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Comment remplir le critère de réussite 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Principe 4 : robuste {#principle-robust}

[Principe 4 : Robuste : le contenu doit être suffisamment robuste pour pouvoir être interprété par un large éventail d’agents utilisateur, y compris les technologies d’assistance.](https://www.w3.org/TR/WCAG/#robust)

### Compatible (4.1) {#compatible}

[Règle 4.1 – Compatible : optimiser la compatibilité avec les agents utilisateur actuels et futurs, y compris les technologies d’assistance.](https://www.w3.org/TR/WCAG/#compatible)

Optimiser la compatibilité avec les agents utilisateur actuels et futurs, y compris les technologies d’assistance.

### Analyse (4.1.1)  {#parsing}

* Critère de réussite 4.1.1
* Niveau A
* Analyse : dans le contenu implémenté à l’aide de langages de balisage, les éléments ont des balises de début et de fin complètes, sont imbriqués selon leurs spécifications, ne contiennent pas d’attributs de duplicata et les identifiants sont uniques, sauf si les spécifications autorisent ces fonctionnalités.

#### Objectif – Analyse (4.1.1) {#purpose-parsing}

Ce critère de réussite a pour but de s’assurer que les agents utilisateurs, y compris les technologies d’assistance, peuvent interpréter et analyser le contenu avec précision. Si le contenu ne peut pas être analysé dans une structure de données, différents agents utilisateurs peuvent le présenter différemment ou ne pas pouvoir l’analyser. Certains agents utilisateurs utilisent des « techniques de réparation » pour restituer un contenu mal codé.

Comme les techniques de réparation varient d’un agent utilisateur à l’autre, les auteurs ne peuvent pas présumer que le contenu est analysé avec précision dans une structure de données ou qu’il sera rendu correctement par des agents utilisateurs spécialisés, y compris les technologies d’assistance, à moins que le contenu ne soit créé selon les règles définies dans la grammaire formelle de cette technologie. Dans les langages de balisage, les erreurs de syntaxe d’éléments et d’attributs, ainsi que l’impossibilité de fournir des balises de début et de fin correctement imbriquées, entraînent des erreurs qui empêchent les agents utilisateurs d’analyser le contenu de manière fiable. Ainsi, le critère de réussite impose que le contenu puisse être analysé en utilisant uniquement les règles de la grammaire formelle.

#### Comment procéder – Analyse (4.1.1) {#how-to-meet-parsing}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### En savoir plus – Analyse (4.1.1) {#more-information-parsing}

* [Compréhension du critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Comment remplir le critère de réussite 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nom, rôle, valeur (4.1.2)  {#name-role-value}

* Critère de réussite 4.1.2
* Niveau A
* Nom, rôle, valeur : Pour tous les composants de l’interface utilisateur (y compris, mais sans s’y limiter : éléments de formulaire, liens et composants générés par les scripts), le nom et le rôle peuvent être déterminés par programmation. les états, propriétés et valeurs qui peuvent être définis par l’utilisateur peuvent être définis par programmation ; Les agents utilisateurs peuvent être informés des modifications apportées à ces éléments, y compris les technologies d’assistance.

#### Objectif – Nom, rôle, valeur (4.1.2) {#purpose-ame-role-value}

Ce critère de réussite a pour but de s’assurer que les technologies d’assistance peuvent recueillir des informations sur le contenu, l’activer (ou le définir) et actualiser l’état des contrôles de l’interface utilisateur.

Si l’interface utilise des contrôles standard issus de technologies d’accessibilité, ce processus est simple. Si les éléments de l’interface utilisateur sont utilisés conformément aux spécifications, les conditions de cette disposition sont remplies. (Voir les exemples relatifs au critère de réussite 4.1.2 ci-dessous)

Toutefois, si des contrôles personnalisés sont créés ou si des éléments d’interface sont programmés (dans le code ou le script) pour avoir un rôle et/ou une fonction différents de ceux habituels, des mesures supplémentaires doivent être prises pour s’assurer que les contrôles fournissent des informations importantes aux technologies d’assistance et se permettent d’être contrôlés par ces technologies.

L’état important d’un contrôle d’interface utilisateur est de savoir s’il est ciblé. Il est possible de déterminer cet état par programmation, et des notifications concernant le changement de focus sont envoyées aux agents utilisateurs de même qu’aux dispositifs d’assistance. Un autre exemple d’état de contrôle de l’interface utilisateur est de savoir si une case à cocher ou un bouton radio a été sélectionné. Ou si une arborescence ou un noeud de liste réductible est développé ou réduit.

#### Comment procéder – Nom, rôle, valeur (4.1.2) {#how-to-meet-ame-role-value}

Appliquez les règles indiquées dans la section [Comment remplir le critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### En savoir plus – Nom, rôle, valeur (4.1.2)  {#more-information-ame-role-value}

* [Compréhension du critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Comment remplir le critère de réussite 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
