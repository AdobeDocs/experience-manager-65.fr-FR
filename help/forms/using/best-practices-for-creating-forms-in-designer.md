---
title: Bonnes pratiques pour la création de formulaires dans le concepteur de formulaires
description: Découvrez les bonnes pratiques d’accessibilité pour la création de formulaires dans le concepteur de formulaires
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 6b86212a2b3a86b2205714c802dc1581d30e7441
workflow-type: tm+mt
source-wordcount: '11687'
ht-degree: 0%

---

# Bonnes pratiques pour la création de formulaires dans le concepteur de formulaires

LiveCycle Designer vous permet de créer du contenu de formulaire enrichi et de respecter les instructions de la section 508. Ce guide contient une vue d’ensemble des bonnes pratiques relatives à la création d’un formulaire accessible et des instructions relatives à la mise en oeuvre de ces bonnes pratiques à l’aide de LiveCycle Designer. Les bonnes pratiques suivantes sont abordées :

1. [Simplification et facilité l’utilisation des formulaires](#keep-simple)
1. [Configuration des propriétés de formulaire pour générer des informations d’accessibilité](#configure-form-properties)
1. [Choisir les contrôles adéquats](#choose-right-controls)
1. [Fournissez des équivalents textuels pour les images](#provide-text-equivalents)
1. [Fournissez des libellés appropriés pour les commandes de formulaire](#provide-proper-labels)
1. [Assurez-vous que la lecture et l’ordre de tabulation sont corrects](#ensure-reading-tab-order)
1. [S’assurer que les commandes de formulaire sont accessibles à l’aide du clavier](#ensure-keyboard-accessible)
1. [Utilisation responsable des couleurs](#use-color-responsibly)
1. [Fournir des cellules d’en-tête pour les tableaux](#provide-heading-cells)
1. [Fournir une structure de formulaire navigable](#provide-navigable-form)
1. [Éviter les perturbations dans les scripts](#avoid-disruptive-scripting)
1. [S’assurer que tout le contenu audio et vidéo est accessible](#ensure-audio-video-accessible)
1. [Identifier le langage naturel et toute modification linguistique](#identify-natural-language)

## Simplification et facilité l’utilisation des formulaires {#keep-simple}

Un formulaire n’est pas accessible s’il n’est pas facile à utiliser. Vous devez essayer de concevoir des formulaires simples et utilisables. Une disposition simple des contrôles et des champs avec des légendes et des info-bulles claires et significatives facilite l’utilisation du formulaire pour tous les utilisateurs.
La conception de formulaires organisés de manière claire et logique, qui fournissent des instructions simples et claires, aidera tous les utilisateurs à remplir les formulaires aussi facilement que possible. Les fonctions de navigation, telles que l’ordre de tabulation et les raccourcis clavier, doivent prendre en charge l’ordre logique des objets dans le formulaire.

### Éviter le contenu mobile, clignotant ou clignotant

Certaines personnes atteintes d&#39;épilepsie photosensible peuvent avoir une crise déclenchée par un mouvement dans des fréquences supérieures à 2 GHz (1 GHz, ou Hertz, égal à 1 par seconde) et inférieures à 55 GHz (55 par seconde).

Le mouvement à moins de 2 GHz est considéré comme assez lent pour être sûr pour les personnes atteintes d&#39;épilepsie photosensible. Le mouvement à plus de 55 GHz est considéré comme invisible.

Les développeurs doivent tenir compte de ces paramètres lorsqu’ils utilisent n’importe quel mouvement dans le contenu web.

D’autres utilisateurs peuvent avoir des déficiences cognitives qui rendent difficile la concentration lorsqu’il y a du contenu animé ou clignotant présent dans le formulaire.

En général, évitez d’utiliser des effets optiques insérés par des scripts, tels que du texte ou des animations flashantes, dans des formulaires interactifs. Ces effets réduisent la convivialité des formulaires pour certains utilisateurs.

Points de contrôle connexes
* Section 508 §11934.21

   * (h) Lorsque l&#39;animation est affichée, l&#39;information doit être affichée dans au moins un mode de présentation non animé, au choix de l&#39;utilisateur.
   * (k) Le logiciel ne doit pas utiliser de texte clignotant ou clignotant, d’objets ou d’autres éléments ayant une fréquence de clignotement ou de clignotement supérieure à 2 GHz et inférieure à 55 GHz.
* Section 508 §11934.22
   * (j) Les pages doivent être conçues pour éviter que l’écran scintille avec une fréquence supérieure à 2 GHz et inférieure à 55 GHz.
* WCAG 1.0
   * 7.1 Tant que les agents utilisateur ne permettent pas aux utilisateurs de contrôler le scintillement, évitez de provoquer le scintillement de l’écran. (P1)
   * 7.2 Tant que les agents utilisateur ne permettent pas aux utilisateurs de contrôler le clignotement, évitez de provoquer le clignotement du contenu (c.-à-d. modifier régulièrement la présentation, comme activer et désactiver) (P2).
   * 7.3 Tant que les agents utilisateur ne permettent pas aux utilisateurs de geler le contenu mobile, évitez les mouvements dans les pages.
   * 14.1 Utilisez le langage le plus clair et le plus simple approprié pour le contenu d’un site.
* WCAG 2.0
   * 2.2.2 Mettre en pause, arrêter, masquer : pour les informations de déplacement, de clignotement, de défilement ou de mise à jour automatique, tous les éléments suivants sont vrais : (niveau A)
   * 2.3.1 Pas plus de trois Flashs ou sous le seuil critique : les pages web ne contiennent rien qui clignote plus de trois fois au cours d’une seconde ou le flash est inférieur aux seuils Flash généraux et rouges. (Niveau A)
   * 2.3.2 Trois Flashs : les pages web ne contiennent rien qui clignote plus de trois fois au cours d’une seconde. (Niveau AAA)


## Configuration des propriétés de formulaire pour générer des informations d’accessibilité {#configure-form-properties}

Pour qu’un formulaire soit accessible, il doit être [perceptible](https://www.w3.org/TR/WCAG20/#perceivable) par technologie d’assistance. Par exemple, la plupart des lecteurs d’écran ne prennent pas en compte la disposition visuelle de votre formulaire, mais plutôt la structure sous-jacente.

Pour mettre en oeuvre cette structure sous-jacente à l’aide de LiveCycle Designer, vous devez créer un formulaire de PDF contenant des informations d’accessibilité (parfois appelées balises), afin que le lecteur d’écran ou toute autre technologie d’assistance puisse lire le texte et les composants du formulaire. Dans un formulaire contenant des informations sur l’accessibilité, chaque élément contient des informations sur sa propre structure, ainsi que des informations sur sa relation ou sa dépendance à d’autres éléments. Ce n’est que dans les fichiers de PDF contenant des informations d’accessibilité que les lecteurs d’écran peuvent identifier et décrire précisément le contenu d’un document.

Pour créer un formulaire accessible, vous devez configurer les propriétés du formulaire de sorte que LiveCycle Designer génère des informations d’accessibilité lors de l’enregistrement de la conception de formulaire en tant que fichier de PDF :
1. Choisissez Fichier > Propriétés du formulaire.
1. Cliquez sur l’onglet Enregistrer les options et, dans la zone du PDF, assurez-vous que l’option Générer les informations d’accessibilité (balises) pour Acrobat est sélectionnée.
1. Cliquez sur OK.

Dans LiveCycle Designer, cette option est sélectionnée par défaut.

>[!NOTE]
> Ces options s’appliquent uniquement lors de l’enregistrement de la conception de formulaire en tant que fichier de PDF. Elles ne s’appliquent pas aux fichiers de PDF créés avec LiveCycle Forms qui disposent d’options de configuration indépendantes de cette option dans LiveCycle Designer.

**Points de contrôle connexes**

* Section 508 §1194.21
   * (d) Des informations suffisantes sur un élément d’interface utilisateur, y compris l’identité, le fonctionnement et l’état de l’élément, doivent être disponibles pour les dispositifs d’assistance. Lorsqu’une image représente un élément de programme, les informations véhiculées par l’image doivent également être disponibles dans le texte.
   * (l) Lorsqu’un formulaire électronique est utilisé, il doit permettre aux personnes utilisant une technologie d’assistance d’accéder aux informations, aux éléments de terrain et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* Section 508 §1194.22
   * (n) Lorsque les formulaires électroniques sont conçus pour être remplis en ligne, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de terrain et aux fonctionnalités nécessaires à la remplissage et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.


## Choisir les contrôles adéquats {#choose-right-controls}

Lorsque vous concevez vos formulaires, utilisez des objets de développement issus des onglets disponibles dans la bibliothèque d’objets de LiveCycle Designer. Vous pouvez afficher ce panneau en choisissant Fenêtre > Bibliothèque d’objets ou en appuyant sur Maj+F12 (voir l’illustration 1).

![Panneau Bibliothèque d’objets](/help/forms/using/assets/image-1.png)

Figure 1 : **Panneau Bibliothèque d’objets**

Si vous utilisez d’autres objets, ils peuvent être ignorés par les dispositifs d’assistance. L’utilisation des objets standard vous évite d’avoir à définir les propriétés d’accessibilité des objets que vous avez vous-même créés. Si vous créez et utilisez vos propres objets personnalisés, veillez à utiliser la palette Accessibilité pour définir les propriétés d’accessibilité telles que Rôle, Info-bulle, Précédence du Reader d’écran et Texte de Reader d’écran personnalisé. Pour afficher la palette Accessibilité, choisissez Fenêtre > Accessibilité.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (c) Une indication bien définie à l’écran de la cible d’action actuelle doit être fournie pour que les éléments de l’interface interactive se déplacent au fur et à mesure que la cible d’action change. Le focus doit être exposé par programmation afin que la technologie d’assistance puisse suivre les changements de focus et de focus.
   * (d) Des informations suffisantes sur un élément d’interface utilisateur, y compris l’identité, le fonctionnement et l’état de l’élément, doivent être disponibles pour les dispositifs d’assistance. Lorsqu’une image représente un élément de programme, les informations véhiculées par l’image doivent également être disponibles dans le texte.
   * (l) Lorsqu’un formulaire électronique est utilisé, il doit permettre aux personnes utilisant une technologie d’assistance d’accéder aux informations, aux éléments de terrain et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* Section 508 §1194.22
   * (n) Lorsque les formulaires électroniques sont conçus pour être remplis en ligne, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de terrain et aux fonctionnalités nécessaires à la remplissage et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.

* WCAG 2.0
   * 3.2.4 Identification cohérente : les composants possédant la même fonctionnalité dans un ensemble de pages Web sont identifiés de manière cohérente. (Niveau AA).
   * 4.1.2 Nom, rôle, valeur : pour tous les composants de l’interface utilisateur (y compris, mais sans s’y limiter : éléments de formulaire, liens et composants générés par les scripts), le nom et le rôle peuvent être déterminés par programmation ; les états, propriétés et valeurs pouvant être définis par l’utilisateur peuvent être définis par programmation ; et les agents utilisateurs peuvent être informés des modifications apportées à ces éléments, y compris les technologies d’assistance. (Niveau A)


## Fournissez des équivalents textuels pour les images {#provide-text-equivalents}

Les images peuvent aider à améliorer la compréhension pour les utilisateurs présentant certains types de handicaps. Toutefois, pour les utilisateurs de lecteurs d’écran, les images diminuent l’accessibilité de votre formulaire si vous ne fournissez pas d’alternative textuelle.

Si vous choisissez d’utiliser des images, fournissez des descriptions textuelles pour tous les objets d’image et de champ d’image. Assurez-vous que le texte décrit l’objet et son objectif sur le formulaire. Lorsque vous définissez un texte secondaire, le lecteur d’écran lit cette alternative lorsqu’il rencontre l’image. Pour cette raison, une image contenant des informations doit toujours comporter un texte secondaire.

Vous fournissez des descriptions textuelles à l’aide des propriétés Info-bulle ou Texte de Reader d’écran personnalisé de la palette Accessibilité ou au moyen de champs de texte, de légendes et de noms d’objet, comme indiqué dans l’option Nom de l’onglet Liaison. Par exemple, la figure 2 illustre un exemple d’image contenant le texte &quot;Obtenir Adobe Reader&quot;. Comme un lecteur d’écran ne peut pas lire le texte qui fait partie d’une image, vous devez inclure un texte secondaire dans le champ Texte de Reader d’écran personnalisé de la palette Accessibilité pour cet objet. Dans la plupart des cas, le texte secondaire doit être identique au texte visible dans l’image (voir l’illustration 2).

![Spécification d’un texte de remplacement pour une image à l’aide de la palette Accessibilité](/help/forms/using/assets/image-2.png)

Figure 2 : **Spécification d’un texte de remplacement pour une image à l’aide de la palette Accessibilité**

Lorsque vous spécifiez un texte de remplacement, tenez compte des points suivants :
* Si l’objet image ou l’image numérisée contient des informations importantes pour le formulaire, créez du texte pour l’image dans la palette Accessibilité qui décrit l’objet et son objectif. Le texte du logo d’une société, par exemple, peut contenir les mots &quot;logo de la société&quot; et le nom de la société.
* Si l’objet image contient des informations de couleur sémantique, incluez-les également dans la description. Une description d’un feu vert de circulation, par exemple, peut être &quot;Transmission réussie&quot; et la description d’un feu rouge peut être &quot;Transmission échouée&quot;.
* Si vous utilisez des graphiques complexes, tels que des graphiques à barres, fournissez les informations dans une autre version accessible, telle qu’un tableau ou une description textuelle plus longue.
* Ne créez pas de descriptions de texte pour les images statiques qui ne sont utilisées que pour la décoration.
* N’utilisez pas les données numérisées comme informations d’arrière-plan. Cela peut se produire lorsqu’un concepteur analyse un formulaire imprimé et utilise Adobe LiveCycle Designer pour ajouter de nouveaux champs au formulaire. Les lecteurs d’écran ne peuvent pas détecter les données analysées dans cet état.

Lorsque vous incluez du contenu graphique purement décoratif dans vos formulaires, vous souhaitez vous assurer que les lecteurs d’écran n’annoncent pas la présence de l’image. Pour la plupart des lecteurs d’écran, cela est possible en définissant la propriété Texte du Reader d’écran sur Aucun dans la palette Accessibilité. Si vous ne le faites pas, certains lecteurs d’écran peuvent annoncer la présence d’un graphique, sans indiquer ce qu’il représente. Pour les images dynamiques, telles que les objets de champ d’image, assurez-vous que les équivalents textuels sont correctement mis à jour lorsque l’image est modifiée. Ne créez pas de descriptions de texte pour les objets de champ d’image qui ne sont utilisés que pour la décoration. Vous pouvez utiliser le langage de script FormCalc pour affecter dynamiquement des descriptions textuelles à un objet de champ d’image. FormCalc est le langage de script standard d’Adobe LiveCycle Designer. Prenons l’exemple d’un formulaire avec un champ d’image nommé ImageField1 et le texte associé dans le noeud imagetext des données d’exécution. Vous pouvez utiliser un script pour transmettre ce texte dans un événement approprié (tel que `form:ready`)comme suit :

`ImageField1.assist.toolTip = $record.imagetext.value`

Points de contrôle connexes
* Section 508 §1194.22
   * (a) Un équivalent textuel pour chaque élément non textuel doit être fourni (par exemple, par &quot;alt&quot;, &quot;longdesc&quot; ou dans le contenu de l’élément).
* WCAG 1.0
   * 1.1 Fournir un équivalent textuel pour chaque élément non textuel (par exemple, par &quot;alt&quot;, &quot;longdesc&quot; ou dans le contenu de l’élément). Cela inclut : les images, les représentations graphiques du texte (y compris les symboles), les zones cliquables, les animations (par exemple, les GIFs animés), les applets et les objets programmatiques, l’art ascii, les cadres, les scripts, les images utilisées comme puces de liste, les espaces, les boutons graphiques, les sons (lus avec ou sans interaction de l’utilisateur), les fichiers audio autonomes, les pistes audio de vidéo (P1).
* WCAG 2.0
   * 1.1.1 Contenu non textuel : tout contenu non textuel présenté à l’utilisateur comporte un équivalent textuel qui remplit une fonction équivalente, à l’exception des situations répertoriées ci-dessous. (Niveau A)


## Fournissez des libellés appropriés pour les commandes de formulaire{#provide-proper-labels}

Le libellé ou la légende d’un contrôle de formulaire identifie ce que le contrôle de formulaire est censé représenter. Par exemple, le texte &quot;Prénom&quot; indique aux utilisateurs de saisir leur prénom dans un champ de texte. Pour être accessible par les lecteurs d’écran, le libellé doit être associé par programmation à la commande de formulaire ou cette dernière doit être configurée avec des informations d’accessibilité supplémentaires à l’aide de la palette Accessibilité. Il ne suffit pas de placer un objet de texte à côté de la commande. Pour les utilisateurs voyants ou malvoyants, il est important que le libellé soit correctement positionné à côté du contrôle. Les deux techniques seront abordées dans les sections suivantes.

### Spécification de texte de libellé accessible à l’aide de la palette Accessibilité

Le libellé qui est perçu par les utilisateurs de lecteurs d’écran ne doit pas nécessairement être le même que la légende visuelle. Dans certains cas, vous souhaiterez peut-être être plus précis sur l’objectif du contrôle.
Pour chaque objet de champ d’un formulaire, la palette Accessibilité (voir l’illustration 3) permet de spécifier ce que le lecteur d’écran annonce pour identifier le champ de formulaire spécifique.
Pour utiliser la palette Accessibilité, procédez comme suit :
1. Pour afficher la palette Accessibilité, choisissez Fenêtre > Accessibilité ou appuyez sur les touches Maj+F6.
1. Sélectionnez un objet dans votre formulaire. La palette affiche les propriétés d’accessibilité de l’objet.

![Palette Accessibilité](/help/forms/using/assets/image-3.png)

Tableau 3 : **Palette Accessibilité**

Lorsque le formulaire est enregistré en tant que PDF, LiveCycle Designer recherche dans le formulaire les propriétés Texte personnalisé, Info-bulle, Légende et Nom, dans cet ordre, pour trouver le texte à lire par les lecteurs d’écran. Vous pouvez remplacer cet ordre par défaut à l’aide de l’option Précédence du Reader d’écran de la palette Accessibilité :

1. Sélectionnez l’objet sur la conception de formulaire.
1. Cliquez sur la palette Accessibilité.
1. Sélectionnez l’option Précédence du Reader d’écran autre que Aucun.

Les options suivantes sont disponibles :

* **Texte personnalisé**, que vous définissez dans le champ Texte de Reader d’écran personnalisé de la palette Accessibilité. Cette option vous permet de spécifier le texte que vous souhaitez utiliser pour la technologie d’assistance, comme les lecteurs d’écran. L’utilisation du paramètre Légende est préférable dans la plupart des cas. La création d’un texte de Reader d’écran personnalisé ne doit être considérée comme une option que lorsque l’utilisation de la légende ou d’une info-bulle n’est pas possible.
* **Info-bulle**, que vous définissez dans le champ Info-bulle de la palette Accessibilité. Pour la plupart des objets, les info-bulles s’affichent au moment de l’exécution lorsque l’utilisateur place le pointeur sur l’objet. Les info-bulles s’affichent pour certains objets en lecture seule, tels que l’objet Code à barres d’un formulaire pour support papier, uniquement lorsqu’un lecteur d’écran est en cours d’utilisation.
* **Légende**, ce qui entraîne LiveCycle Designer à utiliser le libellé (visuel) associé au champ de formulaire comme texte de lecteur d’écran.
* **Nom**, que vous définissez dans le champ Nom de l’onglet Liaison. Notez que ce nom ne peut pas contenir d’espaces.
* **Aucun**, ce qui entraîne l’absence de nom pour l’objet. Cela n’est jamais recommandé pour les contrôles de formulaire.

Tenez compte des points suivants lorsque vous utilisez la palette Accessibilité pour l’étiquetage des commandes de formulaire :

* Si la légende de votre contrôle de formulaire décrit correctement le contrôle, il est alors accessible aux lecteurs d’écran. Dans ce cas, laissez les champs Texte personnalisé et Info-bulle vides dans la palette Accessibilité ou remplacez la Précédence du Reader d’écran par Légende.
* Lorsque vous ciblez des lecteurs d’écran, il n’est pas utile de spécifier différentes descriptions de texte pour le même contrôle de formulaire, car un seul champ sera utilisé : le premier champ non vide dans l’ordre Précédence du Reader d’écran. Par exemple, il n’y a aucune raison de spécifier le texte personnalisé et le texte d’info-bulle pour un lecteur d’écran.
* Par défaut, le lecteur d’écran lit la légende si rien n’est spécifié dans la zone Info-bulle ou Texte par Reader d’écran personnalisé.
* N’utilisez pas la palette Accessibilité pour créer des descriptions pour les champs ou zones invisibles.
* Si vous devez créer une description à l’aide des options Info-bulle ou Texte de Reader d’écran personnalisé , incluez toujours la légende visible sur le formulaire, sauf lorsque la légende visible n’est pas significative, par exemple lorsque la légende elle-même est abrégée. Cela permet aux utilisateurs de lecteurs d’écran de communiquer efficacement avec d’autres utilisateurs au sujet des éléments de l’interface utilisateur. Ces différents groupes d’utilisateurs ont des difficultés à identifier le même élément d’IU si le texte de sa légende diffère de la info-bulle ou du texte du Reader d’écran personnalisé.
* Pour les cases à cocher et les listes déroulantes dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte de lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne pour le texte de remplacement de ces objets lorsqu’ils sont placés dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte de lecteur d’écran personnalisé.
* Si le contrôle nécessite des instructions supplémentaires, assurez-vous qu’elles sont également incluses dans l’alternative textuelle. Incluez suffisamment d’informations vocales pour que les utilisateurs sachent quelles entrées sont attendues et comment remplir correctement le champ, mais ne submergez pas les utilisateurs d’informations redondantes.
* Ne fournissez pas d’informations inutiles décrivant comment utiliser les commandes : laissez les technologies d’assistance de l’utilisateur gérer cela pour l’utilisateur. Les utilisateurs peuvent configurer la terminologie en fonction de leur niveau de confort.

La figure 4 illustre un exemple de champ de texte avec une légende visuelle qui peut être floue pour certains utilisateurs de lecteurs d’écran. Dans cet exemple, le texte de Reader d’écran personnalisé est défini sur &quot;Nombre de pages&quot; et le précédent de Reader d’écran est défini sur Texte personnalisé. Par conséquent, le texte de légende (visuel) réel (&quot;# de pages&quot;) ne sera pas utilisé par le lecteur d’écran. Une info-bulle peut également avoir été spécifiée.

![Spécification du texte de Reader d’écran personnalisé lorsque le libellé visible est inadéquat](/help/forms/using/assets/image-4.png)

Tableau 4 : **Spécification du texte de Reader d’écran personnalisé lorsque le libellé visible est inadéquat**

### Boutons radio Étiquetage

Lorsqu’un utilisateur ayant une déficience visuelle accède à un bouton radio, le lecteur d’écran doit lire deux éléments :
* Une indication de l’objectif du groupe de boutons radio
* Libellé significatif pour chaque bouton radio Pour rendre les boutons radio accessibles à l’aide des légendes du bouton :
   1. Dans la palette Hiérarchie, sélectionnez le groupe d’exclusion.
   1. Cliquez sur la palette Accessibilité, puis, dans la zone Texte par Reader sur écran personnalisé, saisissez le texte à lire pour le groupe. Par exemple, pour un groupe d’exclusion indiquant les options de paiement par différentes cartes de crédit, saisissez Sélectionner un mode de paiement.
   1. Si les légendes de chaque bouton radio fournissent du texte qui aura un sens lorsqu’il sera lu par un lecteur d’écran, sélectionnez l’onglet Liaison de la palette Objet, puis désélectionnez l’option Définir la valeur de l’élément.

  Pour rendre les boutons radio accessibles à l’aide d’une valeur d’élément spécifiée :
   1. Dans la palette Hiérarchie, sélectionnez le groupe d’exclusion.
   1. Cliquez sur la palette Accessibilité, puis, dans la zone Texte par Reader sur écran personnalisé, saisissez le texte à lire pour le groupe. Par exemple, pour un groupe d’exclusion indiquant les options de paiement par différentes cartes de crédit, saisissez Sélectionner un mode de paiement.
   1. Dans la palette Hiérarchie, sélectionnez le premier bouton radio du groupe.
   1. Dans la palette Objet, cliquez sur l’onglet Champ. Dans la zone Elément, double-cliquez sur l’élément et saisissez une valeur significative pour le bouton radio sélectionné. Par exemple, pour le premier bouton d’un groupe de méthodes de paiement, vous pouvez saisir Espèces.
   1. Répétez les étapes 3 et 4 pour chaque bouton radio du groupe d’exclusion.

### Étiquetage des contrôles personnalisés

Il est vivement recommandé d’utiliser des composants standard plutôt que des composants personnalisés, car ils fourniront par défaut à la technologie d’assistance les bons repères et informations. Toutefois, si des contrôles personnalisés sont utilisés, tenez compte des points suivants :
* Annoncez l’état des cases à cocher et des boutons radio.
* Dans les zones de liste et les listes déroulantes, annoncez l’élément par défaut sélectionné dans la liste. Assurez-vous que l’utilisateur sait utiliser les touches fléchées Haut et Bas pour parcourir les éléments de la liste. Notez qu’appuyer sur la touche de tabulation ou sur la touche Entrée ou Retour permet de sélectionner l’élément dans la liste. Avec un script, vous pouvez définir l’événement Change de l’objet pour annoncer l’élément sélectionné dans la liste.
* Annoncez aux utilisateurs les touches spéciales dont ils ont besoin pour exécuter une fonction, par exemple en appuyant sur la barre d’espace pour sélectionner un bouton ou sur la touche Flèche vers le bas pour sélectionner un élément dans une zone de liste.

### Repositionnement correct de la légende d’un contrôle

Le positionnement d’une légende est important, car les utilisateurs s’attendent à ce qu’elle se trouve à côté du contrôle. Pour les utilisateurs de l’agrandissement de l’écran, c’est encore plus important, car ils peuvent ne pas pouvoir afficher simultanément la commande et la légende s’ils sont trop éloignés.

Lorsque vous créez un objet, LiveCycle Designer positionne automatiquement la légende comme indiqué par le type d’objet. Les légendes des boutons radio, par exemple, sont placées à droite. Cet emplacement par défaut est toujours le meilleur emplacement pour une légende accessible. Si vous devez modifier la position du texte de la légende, procédez comme suit :
1. Sélectionnez l’objet en y mettant la cible d’action.
1. Dans la palette Disposition, sélectionnez la position de la légende de l’objet à partir de l’option Position de la section Légende située au bas de la palette.

L’exemple illustré dans la figure 5 illustre une zone de texte avec une légende au-dessus. La position de la palette Disposition est définie sur Haut. L’emplacement par défaut de la légende se trouve à gauche de la zone de texte.

![Modification du positionnement des légendes à l’aide de la palette Disposition](/help/forms/using/assets/image-5.png)

Figure 5 : **Modification du positionnement des légendes à l’aide de la palette Disposition**

Le tableau suivant présente un aperçu des règles de placement d’étiquettes pour les contrôles couramment utilisés.

| Type de contrôle | Règles de placement |
|--------------|-----------------|
| Entrée de texte (y compris les champs de date, d’heure et de mot de passe) | Placez la légende à gauche du contrôle (par défaut). Si cela n’est pas possible, placez-le immédiatement au-dessus ou en dessous. Les libellés doivent être positionnés à proximité du contrôle pour les utilisateurs avec un agrandissement accru afin que le libellé et le contrôle soient plus susceptibles d’être affichés ensemble dans la vue agrandie. |
| Case à cocher | Placez la légende à droite de la case à cocher (par défaut). Pour les contrôles de case à cocher dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte de lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne comme texte de remplacement pour une case à cocher dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte de lecteur d’écran personnalisé. |
| Groupe de boutons radio | Créez un titre visible pour le groupe de boutons radio en créant un élément de texte statique et en le plaçant à gauche ou au-dessus du groupe. Pour chaque bouton radio individuel, placez le libellé à droite (par défaut). |
| Liste déroulante | Placez la légende à gauche de l’objet (par défaut). Si cela n’est pas possible, placez-le immédiatement au-dessus. Pour les commandes de liste déroulante dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte de lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne comme texte de remplacement pour ces objets dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte de lecteur d’écran personnalisé. |
| Zone de liste | La légende est positionnée par défaut au-dessus de la zone de liste lors de sa création. |
| Bouton | La légende est placée automatiquement sur le bouton et ne doit pas être positionnée manuellement. Assurez-vous que l’objectif du bouton est correctement décrit par le texte de la légende. |


### Remplissage dynamique d’une info-bulle ou d’un texte de Reader d’écran personnalisé

Vous pouvez également remplir de manière dynamique l’équivalent textuel d’un contrôle de formulaire, tel que son info-bulle, avec une valeur issue d’une source de données. Par exemple, vous pouvez afficher une info-bulle personnalisée pour un objet en français.
Les éléments suivants peuvent être définis pour une info-bulle pour le schéma auquel vous vous connectez :


```html
<form>
<tooltip dp_tt="tooltip1"/>
</form>
```


Les éléments suivants peuvent être définis pour une info-bulle pour le fichier de données sur lequel vous pointez :

```html
<form>
<tooltip dp_tt="Quantité - Entrez un nombre inférieur ou égal à 100."/>
</form>
```

1. Dans la palette Bibliothèque d’objets, cliquez sur la catégorie Standard et faites glisser un objet sur la conception de formulaire. Par exemple, insérez un objet de champ de texte.
1. (Facultatif) Dans la palette Objet, cliquez sur l’onglet Champ, puis tapez la légende de l’objet dans la zone Légende. Par exemple, saisissez Quantité.
1. Dans la palette Accessibilité, cliquez sur le libellé actif Info-bulle .
1. Sélectionnez la connexion aux données.
1. Cliquez sur le triangle situé à côté de la zone Liaison et sélectionnez une liaison. Par exemple, sélectionnez info-bulle > @dp_tt.

La chaîne suivante apparaît dans la zone Liaison : $record.tooltip.dp_tt Conseil : vous pouvez saisir cette chaîne dans la zone Éléments au lieu de la sélectionner.
1. Cliquez sur OK.
1. Affichez le formulaire dans l’onglet Preview PDF ( d’aperçu).

### Fournir du texte de lien

Les utilisateurs de technologies d’assistance peuvent avoir différentes méthodes de lecture de texte lié. Par exemple, les utilisateurs de lecteurs d’écran utilisent souvent une liste de liens telle que celle illustrée à la figure 6 pour analyser rapidement les liens disponibles sur une page.

![Boîte de dialogue Liste des liens JAWS](/help/forms/using/assets/image-6.png)

Tableau 6 : **Boîte de dialogue Liste des liens JAWS**

C’est pourquoi les liens doivent être auto-décrits, c’est-à-dire que leur signification ne doit pas dépendre de leur contexte (le texte environnant). Par exemple, les mots &quot;cliquez ici&quot; peuvent former l’élément de lien réel dans l’expression &quot;cliquez ici pour télécharger notre formulaire de demande&quot;. Un tel lien serait difficile à comprendre lorsqu’il est lu dans une liste de liens, en particulier lorsqu’il existe plusieurs liens contenant le même texte.

Lorsque vous utilisez des liens dans votre formulaire, assurez-vous que chaque lien décrit correctement son objectif, sans dépendre du texte ou de la position environnant sur la page. Par exemple, au lieu d’utiliser une expression telle que &quot;Cliquez ici&quot; comme texte de lien, utilisez &quot;Télécharger le formulaire de demande&quot; comme texte de lien.

**Points de contrôle connexes**

* Section 508 §1194.21
   * (d) Des informations suffisantes sur un élément d’interface utilisateur, y compris l’identité, le fonctionnement et l’état de l’élément, doivent être disponibles pour les dispositifs d’assistance. Lorsqu’une image représente un élément de programme, les informations véhiculées par l’image doivent également être disponibles dans le texte.
   * (l) Lorsqu’un formulaire électronique est utilisé, il doit permettre aux personnes utilisant une technologie d’assistance d’accéder aux informations, aux éléments de terrain et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* Section 508 §1194.22
   * (n) Lorsque les formulaires électroniques sont conçus pour être remplis en ligne, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de terrain et aux fonctionnalités nécessaires à la remplissage et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* WCAG 1.0
   * 12.4 Associez explicitement les étiquettes à leurs contrôles (P2).
   * 13.1 Identifier clairement la cible de chaque lien (P2).
* WCAG 2.0
   * 1.1.1 Contenu non textuel : tout contenu non textuel présenté à l’utilisateur comporte un équivalent textuel qui remplit une fonction équivalente, à l’exception des situations répertoriées ci-dessous. (Niveau A)
   * 2.4.6 Titres et libellés : les titres et les libellés décrivent le sujet ou l’objectif. (Niveau AA)
   * 3.2.4 Identification cohérente : les composants possédant la même fonctionnalité dans un ensemble de pages Web sont identifiés de manière cohérente. (Niveau AA)
   * 3.3.2 Étiquettes ou instructions : des étiquettes ou des instructions sont fournies lorsque le contenu nécessite une saisie de l’utilisateur. (Niveau A)
   * 4.1.2 Nom, rôle, valeur : pour tous les composants de l’interface utilisateur (y compris, mais sans s’y limiter : éléments de formulaire, liens et composants générés par les scripts), le nom et le rôle peuvent être déterminés par programmation ; les états, propriétés et valeurs pouvant être définis par l’utilisateur peuvent être définis par programmation ; et les agents utilisateurs peuvent être informés des modifications apportées à ces éléments, y compris les technologies d’assistance. (Niveau A)


## Assurez-vous que la lecture et l’ordre de tabulation sont corrects {#ensure-reading-tab-order}

Il est très important d’assurer un ordre de lecture significatif lors de la conception de formulaires accessibles aux utilisateurs ayant une déficience visuelle ou autre. Ces utilisateurs n’utilisent généralement pas de souris pour naviguer dans un formulaire. Ils dépendent donc du clavier. L’ordre de lecture détermine la séquence utilisée par les utilisateurs de lecteurs d’écran lorsqu’ils lisent votre formulaire. En outre, l’ordre de tabulation permet aux utilisateurs de passer rapidement d’un contrôle de formulaire interactif à un autre à l’aide des touches de tabulation ou Maj+tabulation. Un ordre de tabulation logique permet de s’assurer qu’ils ont accès à tous les champs du formulaire et qu’ils peuvent parcourir le formulaire de manière raisonnable et efficace.

L’ordre de lecture du formulaire comprend tous les objets statiques (texte et images, par exemple) et les objets de champ, mais seuls les contrôles de formulaire interactifs font partie de l’ordre de tabulation.

>[!NOTE]
> Dans de nombreux cas, l’ordre de tabulation est étroitement lié à l’ordre de lecture. Pour plus de simplicité, le terme &quot;ordre de tabulation&quot; sera utilisé à la place de &quot;ordre de tabulation ou de lecture&quot; dans ce guide.

### Ordre de tabulation par défaut dans les formulaires Designer par LiveCycle

L’ordre de tabulation par défaut est automatiquement créé lorsque vous enregistrez votre formulaire en tant que PDF balisé. Dans un premier temps, l’ordre de tabulation d’un formulaire est déterminé à partir de la position locale des objets, selon les règles suivantes :

* Tous les objets sont triés de gauche à droite et de haut en bas (ordre local), en commençant par le coin supérieur gauche du formulaire.
* Tous les sous-formulaires que vous créez sont traités comme des unités autonomes et sont également navigués de gauche à droite et de haut en bas. Si deux sous-formulaires sont placés l’un à côté de l’autre, qui contiennent tous deux des objets, l’ordre de lecture parcourt tous les objets du premier sous-formulaire avant de passer au sous-formulaire suivant.

Pour les formulaires simples (c’est-à-dire les formulaires avec une disposition de gauche à droite et de haut en bas), l’ordre de tabulation par défaut est généralement correct. Pour vérifier cela, vous devez examiner l’ordre de tabulation par défaut avant de publier votre formulaire. Vous pouvez rendre l’ordre de tabulation visible à l’aide de l’une des méthodes suivantes :

* Choisissez Affichage > Afficher l’ordre de tabulation.
* Cliquez sur Afficher l’ordre dans la palette Ordre de tabulation.

Tous les objets s’affichent avec un nombre dans le coin supérieur droit, indiquant la place de l’objet dans l’ordre de tabulation par défaut. Les objets interactifs de cette séquence forment l’ordre de tabulation. La figure 7 présente la visualisation de l’ordre de lecture d’un formulaire de base.

![Visualisation de l’ordre de lecture par défaut pour un formulaire de commande type](/help/forms/using/assets/image-7.png)

Figure 7 : **Visualisation de l’ordre de lecture par défaut pour un formulaire de commande type**

Chaque numéro d’ordre de tabulation s’affiche sous une forme colorée. Les formes ont la signification suivante :
* Les cercles gris (#1 et #4) sont utilisés pour les objets de la zone de contenu.
* Les cercles verts (#6 et #7) sont utilisés pour les objets de gabarit.
* Les carrés de prêteur (#2 et #3) sont utilisés pour les objets à l’intérieur d’un fragment.

Vous pouvez choisir d’afficher uniquement les commandes de formulaire interactives (qui constituent l’ordre de tabulation) ou tous les objets de l’ordre de lecture (qui comprennent également les objets statiques tels que le texte et les images). Pour modifier cette préférence, choisissez Outils > Options > Ordre de tabulation, puis choisissez Afficher uniquement l’ordre de tabulation des champs.

Sur un formulaire complexe, il peut s’avérer difficile de voir comment le tabulation s’enchaîne d’un objet à l’autre. Vous pouvez utiliser des aides visuelles pour vous aider à voir l’ordre de tabulation sur le formulaire. Lorsque les aides visuelles sont activées, lorsque vous placez le pointeur sur l’objet, les flèches bleues indiquent l’ordre de tabulation des deux objets précédents et des deux objets suivants (voir l’illustration 8).

![Les aides visuelles mettent en surbrillance l’ordre de tabulation.](/help/forms/using/assets/image-8.png)

Figure 8 : **Les aides visuelles mettent en surbrillance l’ordre de tabulation.**

Pour activer les aides visuelles, utilisez les méthodes suivantes :
* Choisissez Outils > Options > Ordre de tabulation, puis, dans le panneau Ordre de tabulation, sélectionnez Afficher d’autres aides visuelles pour l’ordre de tabulation.
* Dans le menu de la palette Ordre de tabulation, choisissez Afficher les aides visuelles.

### Utilisation de la position pour influencer l’ordre de tabulation par défaut

Pour changer l’ordre de tabulation par défaut, vous pouvez modifier les coordonnées d’un objet en le déplaçant vers un autre emplacement. Par exemple, dans la figure 9, le champ Nom du produit apparaît dans l’ordre de tabulation avant le champ Quantité . Pour modifier cette commande, vous pouvez déplacer le champ Nom du produit afin qu’il soit placé en bas ou à droite du champ Quantité .

![L’ordre de tabulation par défaut est de gauche à droite.](/help/forms/using/assets/image-9.png)

Figure 9 : **L’ordre de tabulation par défaut est de gauche à droite.**

Vous pouvez modifier la position d’un objet en effectuant l’une des opérations suivantes :
* Faites-le glisser à l’aide de la souris
* Sélectionnez-la et déplacez-la à l’aide des touches fléchées du clavier.

>[!NOTE]
> Il peut s’avérer utile de maintenir l’alignement de l’objet en choisissant Affichage > Accrocher à la grille.

Vous pouvez modifier plus précisément les coordonnées d’un objet à l’aide de la palette Disposition (illustrée dans l’illustration 10). Cette palette permet de définir les coordonnées X et Y, ainsi que la largeur et la hauteur de l’objet.

![Utilisation des coordonnées pour positionner précisément un objet à l’aide de la palette Disposition](/help/forms/using/assets/image-10.png)

Figure 10 : **Utilisation des coordonnées pour positionner précisément un objet à l’aide de la palette Disposition**

>[!NOTE]
> Lorsque la légende et le contrôle ne sont pas fusionnés, la position de la légende d’un contrôle de formulaire est indépendante de l’ordre dans lequel les lecteurs d’écran lisent l’objet et ses éléments. Pour plus d’informations sur les légendes, voir la section 2.5 Fournir des libellés appropriés pour les commandes de formulaire dans ce guide.

### Utilisation de sous-formulaires pour influencer l’ordre de tabulation par défaut

Comme mentionné ci-dessus, les sous-formulaires vous permettent d’insérer des groupes d’objets ayant leur propre ordre de tabulation. Vous pouvez créer un sous-formulaire en effectuant l’une des opérations suivantes :
* Choisissez Insertion > Standard > Sous-formulaire.
* Sélectionnez vos objets dans la palette Hiérarchie, puis regroupez-les dans un sous-formulaire en choisissant Insertion > Placer dans un sous-formulaire.
* Sélectionnez vos objets dans le formulaire, cliquez avec le bouton droit de la souris sur la sélection, puis choisissez Placer dans un sous-formulaire.

Lorsque deux sous-formulaires contenant des objets de champ sont positionnés côte à côte, l’ordre de tabulation passe par les champs du premier sous-formulaire avant de passer au suivant. Ceci est illustré dans la figure 11, où deux sous-formulaires sont utilisés pour créer un ordre de tabulation par défaut basé sur les colonnes.

![Ordre de tabulation par défaut utilisant les sous-formulaires](/help/forms/using/assets/image-11.png)

Figure 11 : **Ordre de tabulation par défaut utilisant les sous-formulaires**

Les sous-formulaires, les cases d’option et les zones de contenu, ainsi que la position verticale des objets sur une page et sur son gabarit, influent tous sur l’ordre de tabulation.

### Création d’un ordre de tabulation personnalisé à l’aide de la palette Ordre de tabulation

Vous pouvez modifier l’ordre de tabulation par défaut lorsque vous avez besoin d’une séquence différente dans votre formulaire. La modification ne peut pas être effectuée lors du positionnement ou du regroupement dans les sous-formulaires. Pour modifier l’ordre de tabulation par défaut, vous pouvez créer un ordre de tabulation personnalisé à l’aide de la palette Ordre de tabulation.
La palette Ordre de tabulation (voir l’illustration 12) vous permet d’examiner et de modifier l’ordre dans lequel les objets de votre formulaire sont lus par les dispositifs d’assistance et parcourus par la touche de tabulation de l’utilisateur.

![Ordre de tabulation, palette](/help/forms/using/assets/image-12.png)

Figure 12 : **Ordre de tabulation, palette**

La palette Ordre de tabulation offre une autre vue de l’ordre de tabulation dans le formulaire. Il affiche tous les objets du formulaire sous forme de liste numérotée, où chaque nombre représente la position de l’objet dans l’ordre de tabulation.
Pour ouvrir la palette Ordre de tabulation, choisissez Fenêtre > Ordre de tabulation.


La palette Ordre de tabulation contient les marqueurs visuels suivants :
* Une barre grise marque chaque page du formulaire. L’ordre de tabulation de chaque page commence par le numéro 1.
* La lettre M à l’intérieur d’un cercle vert indique les objets de gabarit (elle n’est visible que lorsque vous affichez le formulaire dans le panneau Vue de conception).
* Une plage de nombres indique les objets dans un fragment.
* Un arrière-plan jaune indique l’élément sélectionné.
* Une icône de verrouillage en regard du premier objet de la page indique que l’objet ne peut pas être déplacé dans l’ordre de tabulation (visible uniquement lors de l’affichage du formulaire dans l’onglet Pages de Principal).

La liste affiche les mêmes numéros d’ordre de tabulation que les numéros affichés sur le formulaire lui-même lorsque vous choisissez Affichage > Afficher l’ordre de tabulation. Pour changer la position d’un objet dans l’ordre de tabulation, déplacez-le vers le haut ou vers le bas dans la liste de la palette Ordre de tabulation. Vous pouvez déplacer un seul objet ou un groupe d’objets. Pour ce faire, utilisez l’une des méthodes suivantes :

* Faites glisser l’objet sélectionné vers le haut ou le bas de la liste et placez-le à l’emplacement souhaité. Une poignée noire indique votre position actuelle dans la liste avant de placer l’objet.
* Dans la palette Ordre de tabulation, cliquez sur les boutons fléchés Haut ou Bas jusqu’à ce que l’objet sélectionné occupe la bonne position. Vous pouvez également appuyer sur Ctrl+Flèche Haut ou Ctrl+Flèche Bas.
* Dans le menu de la palette Ordre de tabulation, choisissez Déplacer vers le haut ou Déplacer vers le bas.
* Dans la liste de la palette Ordre de tabulation, cliquez sur l’objet sélectionné (ou sélectionnez-le et appuyez sur la touche F2) pour rendre modifiable le numéro figurant en regard du nom de l’objet. Saisissez ensuite le numéro correspondant à la nouvelle position de l’objet dans l’ordre de tabulation, puis appuyez sur Entrée.
* Sélectionnez Copier dans le menu de la palette Ordre de tabulation, sélectionnez dans la liste l’objet au-dessus duquel vous souhaitez placer l’objet que vous déplacez, puis choisissez Coller dans le menu.

Lorsque vous déplacez l’objet à un nouvel emplacement dans l’ordre, LiveCycle Designer réaffecte les numéros de l’ordre de tabulation. Bien que l’ordre de tabulation des objets situés sur un gabarit s’affiche dans le panneau Vue de conception, vous ne pouvez le modifier que dans le panneau Pages de Principal. Si vous utilisez des références à des fragments dans votre formulaire, l’ordre de tabulation à l’intérieur d’un fragment est visible lors de l’affichage de l’ordre du formulaire. Pour modifier l’ordre de tabulation dans un fragment, vous devez ouvrir le fichier source du fragment à des fins d’édition, apporter la modification et enregistrer le fichier. Toutes les formes qui utilisent ce fragment sont affectées par cette modification.

Si vous décidez de ne pas respecter l’ordre de tabulation personnalisé dans votre formulaire, vous pouvez rapidement revenir à l’ordre de tabulation automatique (par défaut) en procédant comme suit (vous perdrez toute modification apportée à l’ordre de tabulation) :
1. Dans la palette Ordre de tabulation, sélectionnez Automatique.
1. Dans la boîte de message qui s’affiche, cliquez sur Oui pour confirmer la suppression de l’ordre de tabulation personnalisé.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (a) Lorsque le logiciel est conçu pour fonctionner sur un système disposant d’un clavier, les fonctions du produit doivent être exécutables à partir d’un clavier où la fonction elle-même ou le résultat de l’exécution d’une fonction peut être détecté textuellement.
* WCAG 1.0
   * 9.2 Assurez-vous que tout élément possédant sa propre interface peut être utilisé de manière indépendante de l’appareil.
* WCAG 2.0
   * 1.3.2 Séquence significative : lorsque la séquence dans laquelle le contenu est présenté affecte sa signification, une séquence de lecture correcte peut être déterminée par programmation. (Niveau A)
   * 2.1.1 Clavier : toutes les fonctionnalités du contenu sont utilisables via une interface clavier sans nécessiter de minutage spécifique pour les touches individuelles, sauf lorsque la fonction sous-jacente nécessite une entrée qui dépend du chemin du mouvement de l’utilisateur et pas seulement des points de terminaison. (Niveau A)
   * 2.1.3 Clavier (sans exception) : toutes les fonctionnalités du contenu sont utilisables via une interface clavier sans nécessiter de minutage spécifique pour les touches individuelles. (Niveau AAA)
   * 2.4.3 Ordre de focus : si une page web peut être naviguée de manière séquentielle et que les séquences de navigation affectent la signification ou le fonctionnement, les composants pouvant être ciblés sont mis au point dans un ordre qui préserve la signification et la opérabilité. (Niveau A)


## S’assurer que les commandes de formulaire sont accessibles à l’aide du clavier{#ensure-keyboard-accessible}

Les utilisateurs doivent pouvoir remplir le formulaire entièrement à l’aide du clavier ou d’un autre appareil de saisie équivalent. Les utilisateurs ayant une mobilité réduite ou une déficience visuelle peuvent n’avoir d’autre choix que d’utiliser le clavier, et de nombreux utilisateurs qui peuvent utiliser une souris préfèrent simplement saisir leur clavier. En permettant diverses méthodes de saisie, vous créez également des formulaires accessibles qui répondent aux préférences de tous les utilisateurs.

Dans LiveCycle Designer, le moyen le plus simple de vous assurer que vos commandes sont accessibles via le clavier consiste à utiliser les commandes répertoriées sous l’onglet Commun de la palette Bibliothèque d’objets. Ces commandes répondent par défaut aux entrées de la souris et du clavier. Pour plus d’informations, voir la section 2.3 Choisir les contrôles adéquats dans ce guide.

Un autre aspect important de l’accessibilité clavier est de s’assurer que chaque élément interactif fait partie de l’ordre de tabulation du formulaire. L’utilisateur peut ainsi déplacer le curseur vers l’avant et vers l’arrière dans le formulaire à l’aide des touches Tab et Maj+Tab. Veillez à définir un ordre de tabulation logique qui inclut tous les champs et boutons. Pour plus d’informations, reportez-vous à la section 2.6. Assurez-vous que l’ordre de lecture et de tabulation est correct dans ce guide.

Enfin, il est important de s’assurer que le comportement scripté est également accessible au clavier et ne dépend pas des événements spécifiques à l’appareil. L’événement de souris MouseEnter, par exemple, ne peut pas être exécuté à l’aide du clavier. En outre, ces gestionnaires d’événements ne doivent pas interférer avec l’accessibilité clavier. Par exemple, assurez-vous que les événements de modification utilisés dans les listes déroulantes ou les zones de liste ne déclenchent pas d’actions inattendues.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (a) Lorsque le logiciel est conçu pour fonctionner sur un système disposant d’un clavier, les fonctions du produit doivent être exécutables à partir d’un clavier où la fonction elle-même ou le résultat de l’exécution d’une fonction peut être détecté textuellement.
* WCAG 1.0
   * 6.4 Pour les scripts et les applets, assurez-vous que les gestionnaires d’événements sont indépendants de l’appareil d’entrée (P2).
   * 9.2 Assurez-vous que tout élément possédant sa propre interface peut être utilisé de manière indépendante de l’appareil (P2).
   * 9.3 Pour les scripts, spécifiez des gestionnaires d’événements logiques plutôt que des gestionnaires d’événements dépendants du périphérique (P2).
* WCAG 2.0
   * 2.1.1 Clavier : toutes les fonctionnalités du contenu sont utilisables via une interface clavier sans nécessiter de minutage spécifique pour les touches individuelles, sauf lorsque la fonction sous-jacente nécessite une entrée qui dépend du chemin du mouvement de l’utilisateur et pas seulement des points de terminaison. (Niveau A)
   * 2.1.2 Aucun piège de clavier : si la sélection au clavier peut être déplacée vers un composant de la page à l’aide d’une interface clavier, la sélection peut être déplacée hors de ce composant à l’aide d’une seule interface clavier. Si elle nécessite plus que des touches de direction ou de tabulation non modifiées ou d’autres méthodes de sortie standard, l’utilisateur est informé de la méthode de déplacement de la sélection. (Niveau A)
   * 2.1.3 Clavier (sans exception) : toutes les fonctionnalités du contenu sont utilisables via une interface clavier sans nécessiter de minutage spécifique pour les touches individuelles. (Niveau AAA)


## Utilisation responsable des couleurs{#use-color-responsibly}

La conception de formulaires pour l’accessibilité implique de prendre en compte des instructions supplémentaires pour l’utilisation de la couleur. Les concepteurs utilisent des couleurs pour améliorer l’aspect des formulaires en mettant en surbrillance différents composants de formulaire. Cependant, une utilisation incorrecte de la couleur peut rendre l’information dans votre formulaire difficile ou impossible à lire pour les personnes handicapées.

### Ne pas véhiculer des informations uniquement par couleur

Les couleurs peuvent mettre en évidence et améliorer certaines parties de votre formulaire, mais vous ne devez pas véhiculer l’information uniquement par couleur.

Les informations véhiculées uniquement en couleur (couleurs ayant une signification sémantique) ne sont pas accessibles aux utilisateurs aveugles. Il en va de même pour les utilisateurs présentant des défauts de vision des couleurs ou qui utilisent différents schémas de couleurs, comme un écran couleur à contraste élevé avec du texte blanc ou un premier plan sur fond noir. N’oubliez pas que les lecteurs d’écran ne peuvent pas détecter automatiquement les informations de couleur.

Par exemple, la figure 13 présente un champ de formulaire avec une légende rouge (indiquée à l’aide de la palette Police) pour indiquer que le champ de formulaire est obligatoire. Dans cet exemple, la couleur est le seul signe de la différence entre les champs d’entrée obligatoires et facultatifs, ce qui rend impossible pour les utilisateurs aveugles ou les utilisateurs ayant certains types de daltonisme de les distinguer.

![Utiliser la couleur seule pour transmettre des informations](/help/forms/using/assets/image-13.png)

Figure 13 : **Utiliser la couleur seule pour transmettre des informations**

Pour résoudre ce problème, indiquez également l’état requis du formulaire dans le texte de remplacement du contrôle de formulaire (comme décrit dans la section 2.5 Fournir des libellés appropriés pour les contrôles de formulaire). Par exemple, vous pouvez définir le texte du lecteur d’écran sur &quot;Code postal (obligatoire)&quot;. Pour les utilisateurs qui rencontrent des difficultés à voir la couleur dans certaines combinaisons, il est recommandé de définir le type de champ de texte sur Entré par l’utilisateur - Obligatoire dans la palette Objet en plus du texte de remplacement qui indique que le champ est obligatoire. Vous pouvez également utiliser d’autres indications que la couleur, telles que le texte visuel, les styles de texte et les styles de bordure. Toutefois, pour les utilisateurs de lecteurs d’écran, vous devrez toujours transmettre les informations requises à l’aide de la palette Accessibilité.

En outre, lorsque vous fournissez des descriptions ou des instructions à l’utilisateur du formulaire, gardez à l’esprit que les instructions basées sur la seule couleur ne sont pas suffisantes pour les utilisateurs ayant une déficience visuelle. Par exemple, au lieu d’une instruction telle que &quot;Cliquez sur le bouton vert pour continuer&quot;, utilisez une description textuelle pour les actions telles que &quot;Cliquez sur le bouton suivant pour continuer&quot;.

>[!NOTE]
> Cette bonne pratique n’interdit pas l’utilisation de la couleur. Elle interdit l&#39;utilisation de la couleur comme seul moyen de transmettre des informations importantes. Si une indication visuelle est toujours souhaitée pour ce type d’informations, le concepteur peut utiliser un astérisque ou un indicateur visuel similaire pour marquer les champs requis.

### Fournissez un contraste des couleurs suffisant

De nombreux utilisateurs ayant une déficience visuelle s’appuient sur un contraste élevé entre le texte et l’arrière-plan pour lire les formulaires. Lorsque le contraste entre les couleurs d’arrière-plan et de premier plan n’est pas suffisant, un formulaire peut devenir difficile, voire impossible, à lire pour certains utilisateurs. La figure 14 présente un exemple de formulaire avec un contraste insuffisant.

![Formulaire avec contraste de couleur insuffisant](/help/forms/using/assets/image-14.png)

Figure 14 : **Formulaire avec contraste de couleur insuffisant**

Il est vivement recommandé d&#39;utiliser la police et les couleurs d&#39;arrière-plan par défaut : noir sur fond blanc. Si vous devez modifier ces couleurs par défaut, veillez à choisir une combinaison appropriée de couleurs à contraste élevé ; utilisez une couleur de premier plan foncée sur un arrière-plan clair, ou vice versa. Pour être certain, utilisez un outil (tel que l’analyseur de contraste des couleurs WAT-C) pour vérifier que le contraste est suffisant.

Adobe Reader et Adobe Acrobat permettent aux utilisateurs de spécifier si les couleurs doivent être remplacées pour répondre à leurs besoins visuels. Les utilisateurs peuvent spécifier leur propre schéma de contraste ou choisir d’utiliser un schéma fourni par le système d’exploitation. En outre, Adobe Reader et Adobe Acrobat ont leur propre modèle de contraste élevé qui peut être activé. Pour que ces options soient réussies, la meilleure approche consiste toujours à utiliser les couleurs par défaut.

Lors de la conception de votre formulaire, testez-le fréquemment à l’aide d’un paramètre de modèle de couleurs similaire à celui que beaucoup d’utilisateurs ayant une déficience visuelle utiliseront pour remplir le formulaire. Cette pratique vous permet de détecter et de corriger les problèmes dès le début du processus de conception.

Recommendations pour l’utilisation des couleurs :
* Assurez-vous qu’aucune information n’est perdue si la couleur sémantique n’est pas visible.
* Si vous ne pouvez pas utiliser les couleurs par défaut, vérifiez que les couleurs sont très contrastées, comme le noir sur fond clair (blanc). Les utilisateurs à vision partielle nécessitent généralement un contraste élevé entre le texte et son arrière-plan pour pouvoir le lire.
* Testez la lisibilité de vos formulaires en passant votre écran à un affichage à contraste élevé, à la fois sous Windows et dans Adobe Reader ou Adobe Acrobat. Mac OSX ne propose qu’un filtre en niveaux de gris simple pour un contraste élevé, ce qui n’est pas suffisant pour le test.
* Ne transmettez pas d’informations uniquement basées sur la couleur. Par exemple, n’utilisez pas uniquement la couleur pour mettre en surbrillance des éléments importants de texte. Utilisez également d’autres méthodes de mise en surbrillance et des descriptions de texte.
* N’utilisez pas trop de couleurs, car cela peut rendre difficile la lecture des informations contenues dans le contenu. Veillez toujours à ce que la lisibilité des informations reste votre priorité absolue lorsque vous décidez des couleurs à utiliser.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (i) Le codage par couleur ne doit pas être utilisé comme seul moyen de transmettre des informations, d’indiquer une action, de demander une réponse ou de distinguer un élément visuel.
* WCAG 1.0
   * 2.1 Assurez-vous que toutes les informations véhiculées par la couleur sont également disponibles sans couleur, par exemple à partir du contexte ou des balises.
   * 2.2 Assurez-vous que les combinaisons de couleurs de premier plan et d’arrière-plan offrent un contraste suffisant lorsqu’elles sont affichées par une personne ayant un déficit de couleurs ou sur un écran noir et blanc. [Priorité 2 pour les images, priorité 3 pour le texte] (P2).
* WCAG 2.0
   * 1.4.1 Utilisation de la couleur : la couleur n’est pas utilisée comme seul moyen visuel de transmettre des informations, d’indiquer une action, de demander une réponse ou de distinguer un élément visuel. (Niveau A)
   * 1.4.3 Contraste (minimum) : la présentation visuelle du texte et des images du texte présente un rapport de contraste d’au moins 4,5:1, à l’exception des éléments suivants : (niveau AA)
   * 1.4.6 Contraste (amélioré) : la présentation visuelle du texte et des images du texte présente un rapport de contraste d’au moins 7:1, sauf pour ce qui suit : (niveau AAA)


## Fournir des cellules d’en-tête pour les tableaux{#provide-heading-cells}

Les tableaux constituent un moyen efficace d’organiser et de présenter le contenu dans des formulaires accessibles. Utilisées de manière appropriée, les lignes et les colonnes d’un tableau fournissent une structure prévisible et cohérente pour le contenu du formulaire. Par exemple, lorsqu’un utilisateur de lecteur d’écran navigue dans une cellule de rangée de contenu, le lecteur d’écran indique l’emplacement de la cellule, puis lit le contenu de la cellule. Le lecteur d’écran indique l’emplacement de la cellule à l’aide d’une combinaison d’en-têtes de lignes et de colonnes ou de numéros de lignes et de colonnes. Comme les lecteurs d’écran fournissent des informations qui orientent l’utilisateur vers l’emplacement du contenu dans le tableau, sa disposition affecte directement l’accessibilité du tableau.

Vous pouvez spécifier les rôles suivants pour les éléments de tableau au fur et à mesure de la construction des tableaux. Ces rôles permettent aux lecteurs d’écran de parcourir la structure du tableau à l’aide de raccourcis spéciaux et transmettent à l’utilisateur la relation entre les cellules du tableau et les cellules d’en-tête correspondantes.
* Tableau Attribue le rôle d’un tableau au sous-formulaire sélectionné. Lorsque l’utilisateur accède à ce sous-formulaire, la plupart des lecteurs d’écran l’identifient comme un tableau et indiquent le nombre de lignes et de colonnes.
* Rangée d’en-tête Attribue le rôle d’une rangée d’en-tête au sous-formulaire ou à la rangée de tableau sélectionné. Lorsque vous parlez le contenu d’une cellule de rangée de contenu, la plupart des lecteurs d’écran identifient d’abord le contenu de la cellule correspondante dans la rangée d’en-tête.
* Rangée de contenu Attribue le rôle d’une rangée de contenu au sous-formulaire ou à la rangée de tableau sélectionné. Si une cellule contient un sous-formulaire, les lecteurs d’écran parlent généralement le contenu de la cellule correspondante dans la rangée d’en-tête, suivie des champs du sous-formulaire.
* Rangée de pied de page Attribue le rôle d’une rangée de pied de page au sous-formulaire ou à la rangée de tableau sélectionné.
* (Aucun) Indique une ligne qui contient des informations sur le tableau ou son contenu. La rangée n’est pas considérée comme faisant partie du tableau ; toutefois, le lecteur d’écran lit son contenu.

Lorsqu’ils sont utilisés correctement, les tableaux constituent un moyen efficace d’organiser et de présenter les informations tabulaires. Évitez les tableaux trop complexes, tels que ceux contenant des tableaux et des sections imbriqués.

### Définition de l’accessibilité des tableaux simples

Il est recommandé d’utiliser des tableaux avec des dispositions simples. Les tableaux simples commencent par une seule rangée d’en-tête suivie des rangées de contenu.

Lors de la conception de tableaux simples pour l’accessibilité, tenez compte des recommandations suivantes :

* L’ordre de tabulation d’un tableau est l’ordre géographique, identique à celui du formulaire. Assurez-vous que le contenu du tableau est organisé de manière à ce qu’il soit logique lorsqu’il est lu de gauche à droite et de haut en bas.
* La plupart des lecteurs d’écran interprètent la première ligne d’un tableau comme la ligne d’en-tête. Lors de la lecture du contenu d’une cellule de rangée de contenu, ces lecteurs d’écran lisent d’abord le contenu de la cellule de rangée d’en-tête associée. Assurez-vous que le contenu de chaque cellule de rangée d’en-tête décrit le contenu de la colonne de manière significative.
* Évitez les cellules qui s’étendent sur plusieurs colonnes, tableaux imbriqués ou sections de tableau. Certains lecteurs d’écran ont des difficultés à interpréter correctement ces fonctions ou peuvent ne pas les utiliser. Par exemple, si une cellule d’une rangée de contenu s’étend sur deux colonnes, les lecteurs d’écran peuvent ne pas référencer le contenu de cellule correct dans la rangée d’en-tête lors de la lecture de la cellule suivante de la rangée.

### Définition de l’accessibilité des tableaux complexes

Lors de la conception de tableaux pour l’accessibilité, assurez-vous que la disposition du tableau reste simple, avec une rangée d’en-tête suivie de rangées de contenu. Bien sûr, certains contenus peuvent nécessiter une disposition de tableau plus complexe. Par exemple, vous devrez peut-être utiliser une cellule s’étendant sur plusieurs en-têtes pour véhiculer efficacement le contenu.

Vous pouvez créer des tableaux complexes en utilisant l’objet de tableau ou en combinant des objets de sous-formulaire. L’objet de tableau permet d’utiliser des fonctionnalités destinées à faciliter la conception, telles que des options d’insertion et de redimensionnement de colonnes et de lignes.

A l’aide de la palette Accessibilité, vous pouvez définir des rôles associés à un tableau dans les sous-formulaires afin de créer un tableau complexe accessible. Selon votre expérience et vos préférences de conception, vous pouvez choisir de créer des tableaux complexes en combinant des objets de sous-formulaire. Par exemple, vous pouvez créer un sous-formulaire qui comprend deux rangées et spécifier ce sous-formulaire comme en-tête du tableau, puis spécifier un autre sous-formulaire pour les rangées de contenu du tableau.

Lors de l’utilisation d’objets de sous-formulaire au lieu d’objets de tableau pour créer des tableaux, les étapes supplémentaires suivantes sont requises :
* Dans l’onglet Sous-formulaire, définissez le type de chaque sous-formulaire sur Positionné.
* Dans la palette Accessibilité, définissez le rôle de sous-formulaire approprié pour chaque sous-formulaire composant le tableau. Par exemple, attribuez le rôle Rangée d’en-tête au sous-formulaire utilisé comme en-tête de tableau.
* Pour les rangées qui contiennent des informations sur le tableau ou son contenu, mais qui ne sont pas considérées comme faisant partie du tableau, attribuez le rôle de sous-formulaire Aucun. Le lecteur d’écran lit le contenu de la ligne.

Les fonctionnalités prises en charge par le lecteur d’écran déterminent les informations lues pour un tableau complexe. Prenons l’exemple d’un tableau contenant une rangée d’en-tête et une section contenant une rangée d’en-tête. Lorsque l’utilisateur accède à une cellule de rangée de contenu dans la section du tableau, les lecteurs d’écran lisent généralement le contenu suivant, dans l’ordre :
* Contenu de la cellule appropriée dans la rangée d’en-tête du tableau
* Contenu de la cellule appropriée dans la rangée d’en-tête de la section
* Contenu de la cellule sélectionnée Certains lecteurs d’écran, cependant, peuvent ne pas lire le contenu des deux lignes d’en-tête.

Créez des noms ou des titres visibles significatifs pour vos tableaux. Vous pouvez créer un nom de tableau sous forme de texte statique dans Adobe LiveCycle Designer et le placer devant le tableau. Vous pouvez regrouper un tableau et son nom dans un sous-formulaire. Les sous-formulaires sont particulièrement utiles lorsque vous souhaitez combiner des objets associés dans une mise en page.

Pour les contrôles dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte de lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne comme texte de remplacement d’un contrôle dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte de lecteur d’écran personnalisé. Notez toutefois que cette stratégie n’est pas toujours aussi claire pour les utilisateurs de lecteurs d’écran, car les lecteurs d’écran peuvent uniquement associer l’en-tête de colonne au contrôle lorsque l’utilisateur n’est pas en mode d’interaction de formulaire du lecteur d’écran.

**Points de contrôle connexes**
* Section 508 §1194.22
   * (g) Les en-têtes de ligne et de colonne doivent être identifiés pour les tableaux de données.
   * (h) Le balisage doit être utilisé pour associer des cellules de données et des cellules d’en-tête aux tableaux de données présentant deux niveaux logiques ou plus d’en-têtes de ligne ou de colonne.
* WCAG 1.0
   * 5.1 Pour les tableaux de données, identifiez les en-têtes de ligne et de colonne (P1).
   * 5.2 Pour les tableaux de données comportant deux niveaux logiques ou plus d’en-têtes de ligne ou de colonne, utilisez les balises pour associer les cellules de données et les cellules d’en-tête (P1).
* WCAG 2.0
   * 1.3.1 Informations et relations : les informations, la structure et les relations véhiculées par la présentation peuvent être déterminées par programmation ou sont disponibles sous forme de texte. (Niveau A)


## Fournir une structure de formulaire navigable{#provide-navigable-form}

Lorsqu’un formulaire devient long et complexe, sa facilité d’utilisation est fortement influencée par sa structure. De la même manière qu&#39;un livre est plus facile à comprendre lorsqu&#39;il est divisé en chapitres et en sections, un formulaire devient plus facile à utiliser lorsqu&#39;il est divisé en en-têtes et en sous-titres. Ce partitionnement est particulièrement utile pour les utilisateurs de lecteurs d’écran, pour les raisons suivantes :
* Chaque en-tête indique à l’utilisateur du lecteur d’écran ce qui peut être attendu dans la section qui suit l’en-tête.
* Les lecteurs d’écran fournissent des raccourcis pour passer rapidement d’un en-tête à l’autre dans le formulaire. Ils permettent également à l’utilisateur d’accéder à une liste d’en-têtes, qui fournit un aperçu de la structure du document et permet une navigation rapide.

Fournir des mécanismes qui permettent aux utilisateurs d’ignorer d’autres zones du formulaire peut faciliter le processus. Vous pouvez ajouter une structure d’en-tête à votre formulaire à l’aide de la palette Accessibilité de LiveCycle Designer.

### Fournir des mécanismes de saut

Les utilisateurs invités peuvent analyser une page dans n’importe quel ordre. Ils peuvent commencer par consulter le coin inférieur droit de la page et parcourir à l’envers le contenu. L’utilisateur de lecteur d’écran ne dispose pas de cette option, car le lecteur d’écran commence à lire la page en haut à gauche (comme présenté dans le code source) et se déplace dans un ordre linéaire. En outre, l’utilisateur voyant peut parcourir la page à la recherche de liens intéressants et les activer avec la souris. Un utilisateur de lecteur d’écran doit parcourir la page de manière séquentielle.

La méthode la plus simple et la plus efficace pour fournir une structure de formulaire navigable consiste à utiliser des en-têtes structurels et des listes correctement définies dans votre formulaire.
Vous pouvez également fournir des mécanismes qui permettent à l’utilisateur d’accéder à d’autres zones du formulaire, par exemple en ajoutant des boutons de navigation en haut et en bas du formulaire. Dans la partie supérieure d’un formulaire, vous pouvez inclure des boutons tels que Ouvrir le fichier de données, Page précédente et Page suivante. Au bas du formulaire, vous pouvez inclure des boutons tels que Enregistrer les données, Envoyer par messagerie, Haut de la page et Imprimer.

Les champs intelligents peuvent être un moyen efficace de faciliter le remplissage de certains formulaires. Par exemple, un formulaire de demande de voyage peut comporter plusieurs lignes et colonnes de champs. Si une rangée spécifique est vide, appuyer sur la touche de tabulation du dernier élément de cette rangée peut passer à la section suivante du formulaire plutôt que de continuer à parcourir plusieurs champs qui resteront vides.

### Ajout d’en-têtes à l’aide de la palette Accessibilité

Vous pouvez utiliser la palette Accessibilité pour attribuer des rôles aux objets en fonction de leur rôle. Ces rôles peuvent être appliqués pour créer des en-têtes à différents niveaux.

![Spécification d’un rôle d’en-tête dans la palette Accessibilité](/help/forms/using/assets/image-15.png)
Figure 15 : **Spécification d’un rôle d’en-tête dans la palette Accessibilité**

Pour créer un en-tête dans votre formulaire, procédez comme suit :

1. Identifiez le début de chaque segment logique de votre formulaire à l’aide d’étiquettes de texte statique,
1. Pour chaque libellé, sélectionnez l’une des options d’en-tête Rôle dans la palette Accessibilité. Les différents niveaux d’en-tête (1 à 6) vous permettent de créer une structure d’en-tête dans votre formulaire. Commencez par le niveau 1, puis utilisez le niveau 2 et ainsi de suite pour les sous-sections imbriquées.

La plupart des lecteurs d’écran permettent aux utilisateurs de naviguer rapidement entre les éléments d’en-tête en fonction de leur niveau. La figure 16 présente un formulaire divisé en segments plus petits utilisant des en-têtes. Dans cet exemple, la structure d’en-tête suivante est utilisée :

* Niveau d’en-tête 1 : Demande de produit
   * Niveau de titre 2 : détails de la commande
      * Niveau de titre 3 : options de remise
* Niveau d’en-tête 2 : informations supplémentaires
   * Niveau d’en-tête 3 : détails personnels
   * Niveau d’en-tête 3 : Adresse

![Structuration d’un formulaire à l’aide d’en-têtes](/help/forms/using/assets/image-16.png)

Figure 16 : **Structuration d’un formulaire à l’aide d’en-têtes**

Ces en-têtes sont simplement des éléments de texte statique auxquels ont été attribués une taille de police spécifique et un rôle d’en-tête au niveau approprié.

>[!NOTE]
> La simple modification de l’aspect visuel d’une étiquette de texte pour donner l’apparence d’un en-tête n’aura pas pour effet que les lecteurs d’écran le reconnaissent comme en-tête. Vous devez appliquer un rôle d’en-tête.

Assurez-vous toujours que l’ordre des niveaux d’en-tête est logique. Par exemple, une sous-section d’un en-tête de niveau 2 doit toujours être un en-tête de niveau 3 ; vous ne devez jamais ignorer les niveaux lors de la notation des sous-sections. Les utilisateurs de lecteurs d’écran utilisent les différents niveaux pour mieux comprendre la structure du formulaire. Par exemple, après avoir rencontré un en-tête de niveau 2, l’utilisateur peut utiliser un raccourci pour rechercher des en-têtes de niveau 3 et déterminer s’il existe des sous-sections. Si vous ignorez les niveaux, l’utilisateur aura des difficultés à identifier ces sous-sections.

### Listes marketing

Il peut également être utile d’ajouter du contenu de liste à votre formulaire. Les listes sont utiles pour regrouper les éléments connexes. Elles permettent aux utilisateurs de lecteurs d’écran de savoir combien d’éléments se trouvent dans une liste et de naviguer rapidement au-delà. Le marquage correct des listes rend la structure de votre formulaire plus claire pour les utilisateurs de lecteurs d’écran.

Dans LiveCycle Designer, vous créez des listes à l’aide de sous-formulaires avec les étapes suivantes :

1. Sélectionnez un sous-formulaire contenant le contenu qui sera marqué comme éléments de liste.
1. Dans la palette Accessibilité, sélectionnez Liste comme rôle.
1. Sélectionnez chaque sous-formulaire imbriqué dans le sous-formulaire Liste, puis définissez son rôle sur Elément de liste.

>[!NOTE]
> Un rôle d’élément de liste ne peut être attribué qu’à un sous-formulaire contenu dans un sous-formulaire dont le rôle de liste est spécifié. Vous ne pouvez pas définir un tableau ou une rangée de tableau en tant que liste ou élément de liste ; toutefois, un élément de liste peut contenir un tableau.

**Points de contrôle connexes**
* Section 508 §11934.22
   * (o) Une méthode permettant aux utilisateurs d’ignorer les liens de navigation répétitifs doit être fournie.
* WCAG 1.0
   * 3.5 Utilisez des éléments d’en-tête pour transmettre la structure du document et utilisez-les conformément aux spécifications (P2).
   * 3.6 Marquez correctement les listes et les éléments de liste. (P2).
   * 12.3 Divisez de grands blocs d&#39;information en groupes plus faciles à gérer, le cas échéant. (P2).
   * 13.3 Fournir des informations sur la disposition générale d’un site (par exemple, une carte du site ou une table des matières).
   * 13.4 Utiliser les mécanismes de navigation de manière cohérente (P2).
* WCAG 2.0
   * 1.3.2 Séquence significative : lorsque la séquence dans laquelle le contenu est présenté affecte sa signification, une séquence de lecture correcte peut être déterminée par programmation. (Niveau A)
   * 2.4.1 Contournement de blocs : un mécanisme est disponible pour contourner les blocs de contenu répétés sur plusieurs pages Web. (Niveau A)
   * 2.4.5 Plusieurs méthodes : plusieurs méthodes permettent de localiser une page Web dans un ensemble de pages, à l’exception de l’endroit où la page Web est le résultat d’un processus ou d’une étape dans un processus. (Niveau AA)
   * 2.4.6 Titres et libellés : les titres et les libellés décrivent le sujet ou l’objectif. (Niveau AA)
   * 2.4.10 En-têtes de section : les en-têtes de section permettent d’organiser le contenu. (Niveau AAA)
   * 3.2.3 Navigation cohérente : les mécanismes de navigation répétés sur plusieurs pages Web au sein d’un ensemble de pages Web se produisent dans le même ordre relatif chaque fois qu’elles sont répétées, à moins qu’une modification ne soit initiée par l’utilisateur. (Niveau AA)


## Éviter les perturbations dans les scripts{#avoid-disruptive-scripting}

Dans le cadre du processus de conception de formulaire, les développeurs de formulaires peuvent utiliser des scripts pour offrir une expérience utilisateur plus riche. Vous pouvez ajouter des scripts à la plupart des champs et objets de formulaire. Par exemple, vous pouvez créer des scripts simples pour mettre à jour dynamiquement les valeurs d’un formulaire interactif en réponse aux entrées de l’utilisateur.

Lors de la conception de scripts pour l’accessibilité, tenez compte des instructions générales suivantes :

* Ne pas interrompre visuellement le contenu du formulaire. Par exemple, évitez les fonctionnalités qui entraînent le scintillement, le clic ou le déplacement du contenu.
* Assurez-vous que les fenêtres contextuelles ne s’affichent que suite à des actions initiées par l’utilisateur. De même, n’autorisez pas la mise au point actuelle du formulaire (la vue actuelle de l’utilisateur) à modifier ou à réafficher le contenu, sauf si l’utilisateur l’a lancé. Par exemple, si l’utilisateur remplit des champs dans la moitié inférieure du formulaire, n’autorisez pas le changement de focus dans le coin supérieur gauche du formulaire, sauf si l’utilisateur choisit de naviguer jusqu’à cet emplacement.
* Les utilisateurs présentant un handicap peuvent avoir besoin de plus de temps pour saisir des données dans les champs. Ne spécifiez pas de réponses temporelles pour les champs de saisie.
* N’oubliez pas que les scripts côté client peuvent interférer avec les lecteurs d’écran et les claviers si le script modifie la cible d’action de l’application cliente. Par exemple, les événements change et mouseEnter, lorsqu’ils sont utilisés avec des listes déroulantes ou des zones de liste, peuvent entraîner des actions inattendues. Vérifiez que les scripts côté client n’entraînent pas de problèmes pour les utilisateurs de lecteurs d’écran et les utilisateurs utilisant uniquement le clavier.
* Les utilisateurs de technologies d’assistance ont parfois besoin de temps supplémentaire pour effectuer des tâches. Dans tous les cas où une routine minutée est sur le point d’expirer, affichez un message accessible pour autoriser une extension. Les zones d’alerte créées via JavaScript sont utilisables par les technologies d’assistance. Il est également possible de déployer une nouvelle fenêtre comportant un message pour alerter l’utilisateur d’un délai d’expiration imminent.

**Points de contrôle connexes**:
* Section 508 §1194.22
   * (l) Lorsque les pages utilisent des langages de script pour afficher du contenu ou pour créer des éléments d’interface, les informations fournies par le script doivent être identifiées par un texte fonctionnel pouvant être lu par les dispositifs d’assistance.
   * (p) Lorsqu’une réponse minutée est requise, l’utilisateur doit être alerté et disposer d’un temps suffisant pour indiquer qu’il faut plus de temps.
* WCAG 1.0
   * 1.4 Pour toute présentation multimédia basée sur le temps (par exemple, un film ou une animation), synchronisez les alternatives équivalentes (par exemple, les sous-titres ou les descriptions auditives de la piste visuelle) avec la présentation (P1).
   * 6.2 Assurez-vous que les équivalents du contenu dynamique sont mis à jour lorsque le contenu dynamique change.
   * 6.3 Assurez-vous que les pages sont utilisables lorsque les scripts, applets ou autres objets de programmation sont désactivés ou ne sont pas pris en charge. Si cela n’est pas possible, fournissez des informations équivalentes sur une autre page accessible.
   * 6.5 Assurez-vous que le contenu dynamique est accessible ou fournissez une autre présentation ou page (P2).
   * 8.1 Rendre les éléments de programmation tels que les scripts et les applets directement accessibles ou compatibles avec les technologies d’assistance [Priorité 1 si la fonctionnalité est importante et n’est pas présentée ailleurs], sinon (P2).
   * 9.3 Pour les scripts, spécifiez des gestionnaires d’événements logiques plutôt que des gestionnaires d’événements dépendants du périphérique (P2).
   * 10.1 Tant que les agents utilisateur ne permettent pas aux utilisateurs de désactiver les fenêtres générées, ne provoquez pas l’affichage de fenêtres contextuelles ou autres et ne modifiez pas la fenêtre active sans en informer l’utilisateur.
* WCAG 2.0
   * 3.2.1 Sur focus : lorsqu’un composant reçoit le focus, il ne déclenche pas de changement de contexte. (Niveau A)
   * 3.2.2 Sur entrée : la modification du paramètre d’un composant de l’interface utilisateur ne provoque pas automatiquement un changement de contexte, sauf si l’utilisateur a été informé du comportement avant d’utiliser le composant. (Niveau A)
   * 3.2.5 Modification sur la requête : les modifications de contexte sont initiées uniquement par la requête de l’utilisateur ou un mécanisme est disponible pour désactiver ces modifications. (Niveau AAA)

## S’assurer que tout le contenu audio et vidéo est accessible{#ensure-audio-video-accessible}

Si vos formulaires contiennent du contenu audio ou vidéo, y compris des clips audio et vidéo, vous devez vous assurer que ce contenu est accessible. Plus précisément, assurez-vous que les clips vidéo incorporés dans les formulaires contiennent des sous-titres (parfois appelés sous-titres) pour les utilisateurs sourds et malentendants et des descriptions vidéo pour les utilisateurs aveugles. Pour les fichiers audio qui ne sont pas synchronisés avec le contenu vidéo, une simple transcription suffit.
Pour les médias basés sur un Flash, consultez [link](/help/forms/using/best-practices-for-creating-forms-in-designer.md) pour plus d’informations sur l’apport de sous-titres.

**Points de contrôle connexes**:
* Section 508 §1194.22
   * (b) Des alternatives équivalentes à toute présentation multimédia doivent être synchronisées avec la présentation.
* WCAG 1.0
   * 1.1 Fournir un équivalent textuel pour chaque élément non textuel (par exemple, par &quot;alt&quot;, &quot;longdesc&quot; ou dans le contenu de l’élément). Cela inclut : les images, les représentations graphiques du texte (y compris les symboles), les zones cliquables, les animations (par exemple, les GIFs animés), les applets et les objets programmatiques, l’art ascii, les cadres, les scripts, les images utilisées comme puces de liste, les espaces, les boutons graphiques, les sons (lus avec ou sans interaction de l’utilisateur), les fichiers audio autonomes, les pistes audio de vidéo (P1).
   * 1.3 Tant que les agents utilisateurs ne peuvent pas lire automatiquement à voix haute l’équivalent textuel d’une piste visuelle, fournissez une description auditive des informations importantes de la piste visuelle d’une présentation multimédia (P1).
   * 1.4 Pour toute présentation multimédia basée sur le temps (par exemple, un film ou une animation), synchronisez les alternatives équivalentes (par exemple, les sous-titres ou les descriptions auditives de la piste visuelle) avec la présentation (P1).
* WCAG 2.0
   * 1.2.1 Contenu seulement audio ou vidéo (pré-enregistré) : pour un contenu seulement audio pré-enregistré et un contenu uniquement vidéo pré-enregistré, les conditions suivantes sont vraies, sauf lorsque le contenu audio ou vidéo est un média de remplacement pour le texte et est clairement identifié comme tel : (niveau A)
   * 1.2.2 Sous-titres (pré-enregistrés) : des sous-titres sont fournis pour tout contenu audio pré-enregistré dans un média synchronisé, sauf lorsque le média est un média de remplacement pour le texte et qu’il est clairement identifié comme tel. (Niveau A)
   * 1.2.3 Audio-description ou version de remplacement pour un média temporel (pré-enregistré) : une alternative pour un média temporel ou une audio-description du contenu vidéo pré-enregistré est fournie pour le média synchronisé, sauf lorsque le média est un média de remplacement pour le texte et qu’il est clairement identifié comme tel. (Niveau A)
   * 1.2.4 Sous-titres (en direct) : des sous-titres sont fournis pour tout contenu audio en direct dans un média synchronisé. (Niveau AA)
   * 1.2.5 Audio-description (pré-enregistrée) : une audio-description est fournie pour tout contenu vidéo pré-enregistré dans les médias synchronisés. (Niveau AA)
   * 1.2.6 Langue des signes (pré-enregistrée) : l’interprétation de la langue des signes est fournie pour tout contenu audio pré-enregistré dans les médias synchronisés. (Niveau AAA)
   * 1.2.7 Audio-description étendue (pré-enregistrée) : lorsque les pauses dans le son de premier plan ne suffisent pas pour permettre aux descriptions audio de transmettre le sens de la vidéo, une audio-description étendue est fournie pour tout contenu vidéo pré-enregistré dans les médias synchronisés. (Niveau AAA)
   * 1.2.8 Alternative de média (pré-enregistrée) : une alternative pour les médias temporels est fournie pour tous les médias synchronisés pré-enregistrés et pour tous les médias vidéo pré-enregistrés uniquement. (Niveau AAA)
   * 1.2.9 Contenu audio uniquement (en direct) : une alternative pour un média temporel qui présente des informations équivalentes pour le contenu audio en direct uniquement est fournie. (Niveau AAA)

## Identifier le langage naturel et toute modification linguistique{#identify-natural-language}

Le contenu du formulaire est lu par les technologies d’assistance qui utilisent des synthétiseurs vocaux spécifiques à la langue. Il est donc important d’identifier correctement la langue principale du formulaire pour s’assurer que les formulaires sont lus dans la langue prévue.

Si le texte (ou le texte de remplacement) de vos formulaires est présenté dans plusieurs langues, vous devez identifier les zones de votre formulaire dans lesquelles un changement est effectué d’une langue à l’autre.

Dans LiveCycle Designer, la définition de la langue principale est effectuée en définissant la propriété Locale du formulaire et la propriété Locale du sous-formulaire de niveau supérieur. Pour identifier les modifications apportées à la langue principale, modifiez la propriété Locale de tout objet qui utilise une langue autre que la langue du formulaire.

Pour définir la propriété Locale d’un formulaire :
1. Choisissez Fichier > Propriétés du formulaire, puis sélectionnez l’onglet Par défaut.
2. Sélectionnez la langue appropriée pour le paramètre régional du formulaire (voir l’illustration 17)
3. Cliquez sur OK

![Modification des paramètres régionaux du formulaire dans la boîte de dialogue Propriétés du formulaire](/help/forms/using/assets/image-17.png)

Figure 17 : **Modification des paramètres régionaux du formulaire dans la boîte de dialogue Propriétés du formulaire**

Pour définir la propriété Local du sous-formulaire de niveau supérieur ou d’un objet nécessitant une autre langue :
1. Sélectionner le sous-formulaire ou l’objet de niveau supérieur dans la vue de conception
1. Pour afficher la palette Objet, choisissez Fenêtre > Objet
1. Dans la palette Objet, sélectionnez l’onglet Champ, puis, dans la liste Paramètre régional, sélectionnez la langue à utiliser pour l’objet (voir l’illustration 18). Lorsque vous appliquez des paramètres régionaux différents à des objets, gardez à l’esprit que les objets situés dans les tableaux et les sous-formulaires reçoivent automatiquement les mêmes paramètres régionaux que le tableau et l’objet de sous-formulaire.

![Modification des paramètres régionaux d’un objet](/help/forms/using/assets/image-18.png)

Figure 18 : **Modification des paramètres régionaux d’un objet**

**Points de contrôle connexes**:
* WCAG 1.0
   * 4.1 Identifier clairement les changements dans la langue naturelle du texte d’un document et les équivalents textuels (par exemple, les sous-titres).
* WCAG 2.0
   * 3.1.1 Langue de la page : la langue humaine par défaut de chaque page Web peut être déterminée par programmation. (Niveau A)
   * 3.1.2 Langue d’un passage : la langue humaine de chaque passage ou expression du contenu peut être déterminée par programmation, à l’exception des noms propres, des termes techniques, des mots d’une langue indéterminée, ainsi que des mots ou expressions devenus partie intégrante du langage courant du texte qui l’entoure immédiatement. (Niveau AA)
