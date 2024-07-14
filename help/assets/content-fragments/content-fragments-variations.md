---
title: Variations – création de contenu de fragment
description: Découvrez comment les variations peuvent rendre votre contenu découplé dans AEM encore plus flexible en vous permettant de créer du contenu pour un fragment, puis de créer des variantes de ce contenu selon vos besoins.
feature: Content Fragments
role: User
exl-id: 50982ede-7ccf-45b2-b0dd-a49d23e0f971
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2309'
ht-degree: 100%

---

# Variations – créer du contenu de fragment{#variations-authoring-fragment-content}

Les [variations](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) sont une fonction importante des fragments de contenu AEM car elles permettent de créer et de modifier des copies du contenu maître pour une utilisation sur des canaux spécifiques ou dans des cas spécifiques, ce qui rend la diffusion de votre contenu découplé encore plus flexible.

Dans l’onglet **Variations**, vous pouvez :

* [saisir le contenu](#authoring-your-content) de votre fragment ;
* [créer et gérer les variations](#managing-variations) du contenu **maître** ;

Vous pouvez effectuer diverses autres actions selon le type de données que vous modifiez, par exemple :

* [Insérer des ressources visuelles dans votre fragment](#inserting-assets-into-your-fragment) (images)

* Sélectionner entre [Texte enrichi](#rich-text), [Texte brut](#plain-text) et [Markdown](#markdown) pour la modification

* [Chargement du contenu](#uploading-content)

* [Affichage des statistiques clés](#viewing-key-statistics) (à propos du texte sur plusieurs lignes)

* [Création d’un résumé de texte](#summarizing-text)

* [Synchronisation des variations avec le contenu maître](#synchronizing-with-master)

>[!CAUTION]
>
>Une fois qu’un fragment a été publié et/ou référencé, AEM affiche un avertissement lorsqu’un auteur ou une autrice ouvre à nouveau ce fragment en mode d’édition. Il s’agit de signaler que les modifications apportées au fragment sont également répercutées sur les pages référencées.

## Création de contenu {#authoring-your-content}

Lorsque vous ouvrez votre fragment de contenu pour le modifier, l’onglet **Variations** s’ouvre par défaut. Ici, vous pouvez créer le contenu, pour le contenu principal ou toute autre variation que vous avez. Le fragment structuré contient différents champs avec divers types de données, qui ont été définis dans le modèle de contenu.

Par exemple :

![éditeur plein écran](assets/cfm-variations-02.png)

Vous pouvez effectuer les actions suivantes :

* Apportez des modifications à votre contenu directement dans l’onglet **Variations**. Chaque type de données fournit différentes options de modification, par exemple :

   * Pour les champs **Plusieurs lignes de texte**, vous pouvez également ouvrir l’[éditeur plein écran](#full-screen-editor) pour :

      * sélectionner le [format](#formats) ;
      * voir davantage d’options de modification (pour le format [Texte enrichi](#rich-text)) ;
      * accéder à un éventail d’[actions](#actions).

   * Pour les champs **Référence de fragment**, l’option [Modifier le fragment de contenu](#fragment-references-edit-content-fragment) peut être disponible, selon la définition du modèle.

* Attribuez des **Balises** à la variation actuelle. Les balises peuvent être ajoutées, mises à jour et supprimées.

   * Les [balises](/help/sites-authoring/tags.md) sont puissantes lors de l’organisation de vos fragments, car elles peuvent être utilisées pour la classification et la taxonomie du contenu. Les balises peuvent être utilisées pour rechercher du contenu (par balises) et appliquer des opérations en bloc.

      * Les recherches d’une balise renvoient le fragment avec la variation balisée en surbrillance.
      * Vous pouvez également utiliser les balises de variation pour regrouper des variations pour un profil de réseau de diffusion de contenu (CDN) spécifique (pour la mise en cache CDN), au lieu d’utiliser le nom de la variation.

     Par exemple, vous pouvez baliser les fragments pertinents en tant que « lancement de Noël » pour ne les parcourir que sous forme de sous-ensemble, ou les copier pour les utiliser avec un autre lancement futur dans un nouveau dossier.

  >[!NOTE]
  >
  >Vous pouvez également ajouter des **balises** (à la variation **principale**) dans le cadre des [métadonnées](/help/assets/content-fragments/content-fragments-metadata.md).

* [Créez et gérez les variations](#managing-variations) du contenu **principal**.

### Éditeur plein écran {#full-screen-editor}

Lors de la modification d’un champ de plusieurs lignes de texte, vous pouvez ouvrir l’éditeur plein écran ; cliquez dans le texte, puis sélectionnez l’icône d’action suivante :

![Icône de l’éditeur plein écran](assets/cfm-variations-03.png)

L’éditeur de texte s’ouvre alors en plein écran :

![éditeur plein écran](assets/cfm-variations-fullscreentexteditor.png)

L’éditeur de texte plein écran fournit les éléments suivants :

* Accès à diverses [actions](#actions)
* Selon le [format](#formats), des options de formatage supplémentaires ([Texte enrichi](#rich-text))

### Actions {#actions}

Les actions suivantes sont également disponibles (pour tous les [formats](#formats)) lorsque l’éditeur plein écran (c’est-à-dire pour le texte multiligne) est ouvert :

* Sélection du [format](#formats) ([Texte enrichi](#rich-text), [Texte brut](#plain-text) ou [Texte (Markdown](#markdown)))

* [Chargement du contenu](#uploading-content)

* [Affichage des statistiques de texte](#viewing-key-statistics)

* [Synchronisation avec le gabarit](#synchronizing-with-master) (lors de la modification d’une variation)

* [Création d’un résumé de texte](#summarizing-text)

### Formats {#formats}

Les options de modification du texte multiligne dépendent du format sélectionné :

* [Texte enrichi](#rich-text)
* [Texte brut](#plain-text)
* [Texte (Markdown)](#markdown)

Le format peut être sélectionné dans l’éditeur plein écran.

### Texte enrichi {#rich-text}

La modification de texte enrichi permet de mettre en forme :

* Gras
* Italique
* Souligné
* Alignement : gauche, centre et droite
* Liste à puces
* Liste numérotée
* Mise en retrait : augmenter, diminuer
* Création/suppression d’hyperliens
* Coller le texte/à partir de Word
* Insérer un tableau
* Style de paragraphe : paragraphe et en-tête 1/2/3
* [Insérer une ressource](#inserting-assets-into-your-fragment)
* Ouvrez l’éditeur plein écran où les options de mise en forme suivantes sont disponibles :
   * Rechercher
   * Rechercher/remplacer
   * Vérificateur orthographique
   * [Annotations](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Insérer un fragment de contenu](#inserting-content-fragment-into-your-fragment) ; disponible lorsque votre champ **Plusieurs lignes de texte** est configuré avec l’option **Autoriser la référence de fragment** activée.

Les [actions](#actions) sont également accessibles à partir de l’éditeur plein écran.

### Texte brut {#plain-text}

Le texte brut permet de saisir du contenu de manière rapide, sans formatage ni Markdown. Vous pouvez également ouvrir l’éditeur plein écran pour accomplir d’autres [actions](#actions).

>[!CAUTION]
>
>Si vous sélectionnez **Texte brut**, vous risquez de perdre le formatage, les annotations et/ou les ressources que vous avez insérés dans du **texte enrichi** ou dans **Markdown**.

### Markdown {#markdown}

>[!NOTE]
>
>Pour plus d’informations, consultez la documentation [Markdown](/help/assets/content-fragments/content-fragments-markdown.md).

Vous pouvez ainsi mettre en forme votre texte à l’aide de Markdown. Vous pouvez définir :

* Titres
* Paragraphes et sauts de ligne
* Liens
* Images
* Blocs de citations
* Listes
* Accent
* Blocs de code
* Échappements par barre oblique inverse

Vous pouvez également ouvrir l’éditeur plein écran pour accomplir d’autres [actions](#actions).

>[!CAUTION]
>
>Si vous basculez entre **Texte enrichi** et **Texte (Markdown)**, des effets inattendus peuvent apparaître avec les Blocs de citations et Blocs de code, dans la mesure où le traitement de ces deux formats peut être différent.

### Références à un fragment {#fragment-references}

Si le modèle de fragment de contenu contient des références à un fragment, les auteurs de fragments peuvent disposer d’options disponibles supplémentaires :

* [Modifier le fragment de contenu](#fragment-references-edit-content-fragment)
* [Nouveau fragment du contenu](#fragment-references-new-content-fragment)

![Références à un fragment](assets/cfm-variations-12.png)

#### Modifier le fragment de contenu {#fragment-references-edit-content-fragment}

L’option **Modifier le fragment de contenu** ouvre ce fragment dans un nouvel onglet de fenêtre.

<!--
The option **Edit Content Fragment** opens that fragment in a new editor tab (within the same browser tab).

Selecting the original tab again (for example, **Little Pony Inc.**), will close this secondary tab (in this case, **Adam Smith**).

![Fragment References](assets/cfm-variations-editreference.png)
-->

#### Nouveau fragment de contenu {#fragment-references-new-content-fragment}

L’option **Nouveau fragment de contenu** permet de créer un fragment. Pour ce faire, une variante de l’assistant de création de fragment de contenu s’ouvre dans l’éditeur.

Vous pouvez ensuite créer un fragment en procédant comme suit :

1. naviguez jusqu’au dossier requis et sélectionnez-le ;
1. sélectionnez **Suivant** ;
1. spécifiez les propriétés ; par exemple le **Titre** ;
1. sélectionnez **Créer** ;
1. et sélectionnez enfin :
   1. **Terminer** pour retourner au fragment original tout en référençant le nouveau fragment ;
   1. **Ouvrir** référence le nouveau fragment et ouvre le nouveau fragment à modifier dans un nouvel onglet du navigateur.

### Affichage des statistiques clés {#viewing-key-statistics}

Lorsque l’éditeur plein écran est ouvert, l’action **Statistiques de texte** affiche différentes informations au sujet du texte.

Par exemple :

![statistics](assets/cfm-variations-04.png)

### Chargement de contenu {#uploading-content}

Pour simplifier le processus de création de fragments de contenu, vous pouvez charger du texte préparé dans un éditeur externe et l’ajouter directement au fragment.

### Résumé de texte {#summarizing-text}

Le résumé de texte a été conçu pour permettre aux utilisateurs et utilisatrices de réduire la longueur de leur texte à un nombre prédéfini de mots tout en conservant les éléments clés et la signification globale.

>[!NOTE]
>
>À un niveau plus technique, le système conserve les phrases qu’il évalue comme ayant le *meilleur rapport de densité et d’unicité des informations* selon des algorithmes spécifiques.

>[!CAUTION]
>
>Le fragment de contenu doit posséder un dossier de langue valide (code ISO) en tant qu’ancêtre ; celui-ci permet de déterminer le modèle de langue à utiliser.
>
>Par exemple, `en/` comme dans le chemin d’accès suivant :
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>L’anglais est disponible par défaut.
>
>D’autres langues sont disponibles en tant que packages de modèle de langue à partir du partage de modules :
>
>* [Français (fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=fr?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [Allemand (de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=fr?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [Italien (it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [Espagnol (es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=fr?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>

1. Sélectionnez **Principal** ou la variation requise.
1. Ouvrez l’éditeur plein écran.

1. Sélectionnez **Résumer le texte** dans la barre d’outils.

   ![récapitulation](assets/cfm-variations-05.png)

1. Indiquez le nombre cible de mots et sélectionnez **Démarrer** :
1. Le texte original s’affiche côte à côte avec la synthèse proposée :

   * Toutes les phrases à éliminer sont surlignées en rouge et barrées.
   * Cliquez sur une phrase en surbrillance si vous souhaitez la conserver dans le contenu résumé.
   * Cliquez sur une phrase non mise en surbrillance si vous souhaitez l’éliminer.

1. Sélectionnez **Résumer** pour confirmer les modifications.

1. Le texte original s’affiche côte à côte avec la synthèse proposée :

   * Toutes les phrases à éliminer sont surlignées en rouge et barrées.
   * Cliquez sur une phrase en surbrillance si vous souhaitez la conserver dans le contenu résumé.
   * Cliquez sur une phrase non mise en surbrillance si vous souhaitez l’éliminer.
   * Les statistiques de synthèse s’affichent : **Réel** et **Cible**-
   * Vous pouvez **prévisualiser** les modifications.

   ![comparaison des résumés](assets/cfm-variations-06.png)

### Annotation d’un fragment de contenu {#annotating-a-content-fragment}

Pour supprimer un fragment :

1. Sélectionnez **Principal** ou la variation requise.

1. Ouvrez l’éditeur plein écran.

1. L’icône **Annoter** est disponible dans la barre d’outils supérieure. Vous pouvez sélectionner du texte si nécessaire.

   ![annoter](assets/cfm-variations-07.png)

1. Une boîte de dialogue s’affiche. Vous pouvez y saisir votre annotation.

   ![Annoter](assets/cfm-variations-07a.png)

1. Sélectionnez **Appliquer** dans la boîte de dialogue.

   ![annoter](assets/cfm-variations-annotations-apply-icon.png)

   Si l’annotation a été appliquée au texte sélectionné, ce texte reste en surbrillance.

   ![Annoter](assets/cfm-variations-07b.png)

1. Fermez l’éditeur plein écran. Les annotations restent en surbrillance. Si cette option est sélectionnée, une boîte de dialogue apparaît pour vous permettre de modifier encore l’annotation.

1. Sélectionnez **Enregistrer**.

1. Fermez l’éditeur plein écran. Les annotations restent en surbrillance. Si cette option est sélectionnée, une boîte de dialogue apparaît pour vous permettre de modifier encore l’annotation.

   ![annoter](assets/cfm-variations-07c.png)

### Affichage, modification et suppression d’annotations {#viewing-editing-deleting-annotations}

Les annotations :

* Sont mise en surbrillance sur le texte, en mode plein écran et en mode normal de l’éditeur. Les détails complets d’une annotation peuvent ensuite être affichés, modifiés et/ou supprimés, en cliquant sur le texte mis en surbrillance, ce qui ouvre de nouveau la boîte de dialogue.

  >[!NOTE]
  >
  >Un sélecteur en liste déroulante est fourni si plusieurs annotations ont été appliquées à une partie du texte.

* Lorsque vous supprimez tout le texte auquel l’annotation a été appliquée, cette dernière est également supprimée.

* Peuvent être répertoriées et supprimées en sélectionnant l’onglet **Annotations** dans l’éditeur de fragments.

  ![annotations](assets/cfm-variations-08.png)

* Peuvent être affichées et supprimées dans la [chronologie](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) pour le fragment sélectionné.

### Insertion de ressources dans votre fragment {#inserting-assets-into-your-fragment}

Pour simplifier le processus de création de fragments de contenu, vous pouvez ajouter directement des [Ressources](/help/assets/manage-assets.md) (images) au fragment.

Elles sont ajoutées à la séquence de paragraphes du fragment sans aucune mise en forme ; le formatage peut être effectué lorsque le [fragment est utilisé/référencé sur une page](/help/sites-authoring/content-fragments.md).

>[!CAUTION]
>
>Ces ressources ne peuvent pas être déplacées ni supprimées sur une page de référence ; ce type d’opération doit être effectué dans l’éditeur de fragment.
>
>Toutefois, la mise en forme de la ressource (par exemple, sa taille) doit être effectuée dans l’[éditeur de page](/help/sites-authoring/content-fragments.md). La représentation de la ressource dans l’éditeur de fragment est uniquement destinée à la création du flux de contenu.

>[!NOTE]
>
>Il existe différentes méthodes pour ajouter des [images](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) au fragment et/ou à la page.

1. Positionnez le curseur à l’endroit où vous souhaitez ajouter l’image.
1. Utilisez l’icône **Insérer une ressource** pour ouvrir la boîte de dialogue de recherche.

   ![icône d’insertion de ressource](assets/cfm-variations-09.png)

1. Dans la boîte de dialogue, vous pouvez effectuer l’une des opérations suivantes :

   * Accéder à la ressource souhaitée dans la gestion des actifs numériques (DAM)
   * Rechercher la ressource dans la gestion des ressources numériques (DAM)

   Une fois la ressource souhaitée localisée, sélectionnez-la en cliquant sur la miniature.

1. Utilisez **Sélectionner** pour ajouter la ressource au système de paragraphes de votre fragment de contenu à l’emplacement actuel.

   >[!CAUTION]
   >
   >Si vous modifiez le format après l’ajout en tant que ressource à :
   >
   >* **Texte brut** : la ressource est effacée du fragment.
   >* **Markdown** : la ressource n’est pas visible, mais elle est toujours présente lorsque vous revenez à **Texte enrichi**.

### Insertion d’un fragment de contenu dans votre fragment {#inserting-content-fragment-into-your-fragment}

Pour faciliter la création de fragments de contenu, vous pouvez également ajouter un autre fragment de contenu à votre fragment.

Celui-ci est ajouté en tant que référence à l’emplacement actuel dans votre fragment.

>[!NOTE]
>
>Cette option est disponible lorsque l’option **Autoriser la référence de fragment** est activée pour votre champ **Plusieurs lignes de texte**.

>[!CAUTION]
>
>Ces ressources ne peuvent pas être déplacées ni supprimées sur une page de référence ; ce type d’opération doit être effectué dans l’éditeur de fragment.
>
>Toutefois, la mise en forme de la ressource (par exemple, sa taille) doit être effectuée dans l’[éditeur de page](/help/sites-authoring/content-fragments.md). La représentation de la ressource dans l’éditeur de fragment est uniquement destinée à la création du flux de contenu.

>[!NOTE]
>
>Il existe différentes méthodes pour ajouter des [images](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) au fragment et/ou à la page.

1. Placez le curseur à l’endroit où vous souhaitez ajouter le fragment.
1. Utilisez l’icône **Insérer un fragment de contenu** pour ouvrir la boîte de dialogue de recherche.

   ![Icône Insérer un fragment de contenu](assets/cfm-variations-13.png)

1. Dans la boîte de dialogue, vous pouvez effectuer l’une des opérations suivantes :

   * accéder au fragment requis dans le dossier Ressources ;
   * rechercher le fragment.

   Une fois la ressource souhaitée localisée, sélectionnez-la en cliquant sur la miniature.

1. Utilisez **Sélectionner** pour ajouter une référence au fragment de contenu sélectionné à votre fragment de contenu actuel (à l’emplacement actuel).

   >[!CAUTION]
   >
   >Si vous modifiez le format, après avoir ajouté une référence à un autre fragment, procédez comme suit :
   >
   >* **Texte brut** : la référence est effacée du fragment.
   >* **Markdown** : la référence reste.

## Gestion des variations {#managing-variations}

### Création d’une variation {#creating-a-variation}

Les variations vous permettent de prendre le contenu **principal** et le varier en fonction de l’objectif (si nécessaire).

Pour créer une variation :

1. Ouvrez votre fragment et assurez-vous que le panneau latéral est visible.
1. Sélectionnez **Variations** dans la barre d’icônes du panneau latéral.
1. Sélectionnez **Créer une variation**.
1. Une boîte de dialogue s’ouvre. Spécifiez le **titre** et la **description** correspondant à la nouvelle variation.
1. Sélectionnez **Ajouter** et le **contenu principal** du fragment est copié dans la nouvelle variation, qui est maintenant ouverte pour [modification](#editing-a-variation).

   >[!NOTE]
   >
   >Lors de la création d’une variation, c’est toujours le contenu **principal** qui est copié et non pas la variation ouverte.

   >[!NOTE]
   >
   >Lorsque vous créez une variation, toutes les **balises** actuellement affectées au contenu **principal** sont copiées dans la nouvelle variation.

### Modifier une variation {#editing-a-variation}

Modifiez le contenu de la variation après l’une des opérations suivantes :

* [Création de la variation](#creating-a-variation).
* Ouvrez un fragment existant, puis sélectionnez la variation requise dans le panneau latéral.

![Modification d’une variation](assets/cfm-variations-10.png)

### Modification du nom d’une variation {#renaming-a-variation}

Pour renommer une variation existante :

1. Ouvrez votre fragment et sélectionnez **Variations** dans le panneau latéral.
1. Sélectionnez la variation requise.
1. Sélectionnez **Renommer** dans le menu déroulant **Actions**.

1. Saisissez le nouveau **Titre** et/ou la nouvelle **Description** dans la boîte de dialogue qui s’affiche.

1. Confirmez l’action **Renommer**.

>[!NOTE]
>
>Cela affecte uniquement la variation **Titre**.

### Suppression d’une variation {#deleting-a-variation}

Pour supprimer une variation existante :

1. Ouvrez votre fragment et sélectionnez **Variations** dans le panneau latéral.
1. Sélectionnez la variation requise.
1. Sélectionnez **Supprimer** dans le menu déroulant **Actions**.

1. Confirmez l’action **Supprimer** dans la boîte de dialogue.

>[!NOTE]
>
>Vous ne pouvez pas supprimer le **Maître**.

### Synchronisation avec le maître {#synchronizing-with-master}

Le **contenu principal** est une partie d’un fragment de contenu et, par définition, il contient la copie princaple du contenu, tandis que les variations contiennent les versions individuelles, mises à jour et personnalisées de ce contenu. Lorsque le contenu principal est mis à jour, il est possible que ces modifications soient également liées aux variations et qu’elles doivent, par conséquent, être appliquées à celles-ci.

Lors de la modification d’une variation, vous avez accès à l’action de synchronisation de l’élément actif de la variation avec le contenu principal. Vous pouvez ainsi copier automatiquement les modifications apportées au contenu principal dans la variation requise.

>[!CAUTION]
>
>La synchronisation n’est disponible que pour copier les modifications *du **Maître**dans la variation*.
>
>Seul l’élément actif de la variation est synchronisé.
>
>La synchronisation fonctionne uniquement avec le type de données **texte multiligne**.
>
>Le transfert des modifications n’est pas proposé *entre une variation et le **Maître***.

<!-- needs new screenshot for synchronize effect -->

1. Ouvrez votre fragment de contenu dans l’éditeur de fragments. Assurez-vous que le **contenu principal** a été modifié.

1. Sélectionnez une variation spécifique, puis l’action de synchronisation appropriée à partir :

   * du menu déroulant du sélecteur **Actions** – **Synchroniser l’élément actif avec le gabarit** ;

     ![Synchronisation avec le maître](assets/cfm-variations-11a.png)

   * de la barre d’outils de l’éditeur plein écran – **Synchroniser avec le gabarit**.

     ![Synchronisation avec le maître](assets/cfm-variations-11b.png)

1. Le contenu principal et la variation sont affichés côte à côte :

   * le contenu ajouté (à la variation) figure en vert.
   * le contenu supprimé (de la variation) figure en rouge.
   * le texte remplacé apparaît en bleu

   ![Synchronisation avec le maître](assets/cfm-variations-11c.png)

1. Sélectionnez **Synchroniser**. La variation est alors mise à jour et affichée.
