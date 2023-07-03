---
title: Composants de base
seo-title: Foundation Components
description: Composants de base
seo-description: null
uuid: 3caf9123-ae58-4590-af2f-57ef076daf7f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: ea2a523e-8d26-4be4-822f-35f153e40308
docset: aem65
legacypath: /content/docs/en/aem/6-2/author/page-authoring/default-components/editmode
pagetitle: Foundation Components
exl-id: 278701f3-3f0c-45f4-90b7-c0e316a7da8a
source-git-commit: cae9890cd61d6d894f34c7299e2e15ee70e14ac9
workflow-type: tm+mt
source-wordcount: '7210'
ht-degree: 44%

---

# Composants de base {#foundation-components}

>[!CAUTION]
>
>La plupart des composants de base sont obsolètes depuis AEM 6.5. Consultez les [Notes de mise à jour ](/help/release-notes/deprecated-removed-features.md) pour plus d’informations.
>
>Adobe recommande d’utiliser des [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) dans AEM projets. Ces composants font partie de la [Exemple de contenu We.Retail](/help/sites-developing/we-retail.md) et peut également [installé séparément et utilisé pour le développement](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=fr) par votre administrateur.
>
>Vous pouvez utiliser la [Suite d’outils de modernisation AEM](https://opensource.adobe.com/aem-modernize-tools/) pour refactoriser votre site basé sur les composants de base afin d’utiliser les composants principaux.

Les composants de base ont été conçus pour être utilisés lors de la création de contenu d’une page web standard. Ils forment un sous-ensemble des composants prêts à l’emploi pour une installation standard d’AEM.

Certains sont immédiatement disponibles via l’explorateur de composants. D’autres ressources sont également disponibles en utilisant [mode de conception](/help/sites-authoring/default-components-designmode.md) (si la page est basée sur un modèle statique) ou par [modification du modèle](/help/sites-authoring/templates.md) (si la page est basée sur un modèle modifiable).

L’utilisation des composants de base est prise en charge, mais ils ont été abandonnés et remplacés par des composants principaux qui offrent plus d’extensibilité et de flexibilité.

>[!NOTE]
>
>Cette section ne traite que des composants disponibles « prêts à l’emploi » dans une installation AEM standard.
>
>Selon votre instance, vous pouvez avoir développé des composants personnalisés explicitement pour vos besoins. Ces composants personnalisés peuvent même avoir le même nom que certains des composants décrits ici.

Les composants sont disponibles sur la page **Composants** dans le panneau latéral de l’éditeur de page lorsque [modification d’une page](/help/sites-authoring/editing-content.md).

Vous pouvez sélectionner un composant et le faire glisser vers l’emplacement souhaité sur votre page. Vous pouvez ensuite la modifier à l’aide de :

* [Configurer les propriétés](/help/sites-authoring/editing-page-properties.md)
* [Modifier le contenu](/help/sites-authoring/editing-content.md)

* [Modifier le contenu - Mode plein écran](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

Les composants sont triés selon différentes catégories appelées groupes de composants, notamment :

* [Général](#general): Comprend des composants de base, notamment du texte, des images, des tableaux et des graphiques.
* [Colonnes](#columns): Comprend les composants nécessaires pour organiser la mise en page du contenu.
* [Formulaire](#formgroup): Inclut tous les composants nécessaires pour créer un formulaire.

## Général {#general}

Les composants Général sont les composants de base que vous utilisez pour créer du contenu.

### Elément de compte {#account-item}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Vous pouvez définir un lien avec un titre et une description.

![chlimage_1-88](assets/chlimage_1-88.png)

### Image adaptative {#adaptive-image}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal Image](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=fr) au lieu de .

Le composant d’image adaptative génère des images dimensionnées en fonction de la fenêtre dans laquelle s’ouvre la page web. Pour utiliser le composant, vous devez fournir une image issue du système de fichiers ou du gestionnaire des actifs numériques. Une fois la page web ouverte, le navigateur télécharge une copie de l’image qui a été redimensionnée afin qu’elle convienne à la fenêtre active.

Les caractéristiques suivantes peuvent déterminer la taille de la fenêtre :

* Écran du périphérique : Les périphériques mobiles affichent généralement les pages web afin qu’elles s’étendent sur tout l’écran.
* Taille de la fenêtre du navigateur Web : Les utilisateurs d’ordinateurs portables et de bureau peuvent redimensionner les fenêtres du navigateur web.

Par exemple, le composant génère une petite image lorsque la page web s’ouvre sur un téléphone mobile et une image de taille moyenne sur une tablette. Sur un ordinateur portable, le composant crée et diffuse une grande image lorsque la page est ouverte dans un navigateur web agrandi. Lorsque le navigateur web est redimensionné pour s’adapter à une partie de l’écran, le composant s’adapte en fournissant une image plus petite et en actualisant l’affichage.

#### Formats d’image pris en charge {#supported-image-formats}

Vous pouvez utiliser des fichiers image des extensions de nom de fichier suivantes avec le composant Image adaptative :

* .jpg
* .jpeg
* .png
* .gif &#42;&#42;

>[!CAUTION]
>
>Les fichiers de GIF animés ne sont pas pris en charge dans AEM pour les rendus adaptatifs.

#### Tailles et qualité des images {#images-sizes-and-quality}

Le tableau suivant répertorie la largeur de l’image générée en fonction de la largeur de la fenêtre d’affichage. La hauteur de l’image générée est calculée pour préserver le rapport L/H et éviter l’apparition de bandes blanches sur les bords de l’image. Le recadrage peut être utilisé pour éviter les espaces blancs.

Si l’image est au format JPEG, sa qualité peut aussi dépendre de la taille de la fenêtre d’affichage, Les qualités de JPEG suivantes sont possibles :

* Faible (0,42)
* Moyen (0,82)
* Élevée (1,00)

| **Plage de largeurs de la fenêtre d’affichage (pixels)** | **Largeur de l’image (pixels)** | **Qualité JPEG** | **Type de périphérique ciblé** |
|---|---|---|---|
| largeur &lt;= 319 | 320 | faible |  |
| largeur = 320 | 320 | moyenne | Téléphone mobile (portrait) |
| 320 &lt; largeur &lt; 481 | 480 | moyenne | Téléphone mobile (paysage) |
| 480 &lt; largeur &lt; 769 | 476 | élevé | Tablette (portrait) |
| 768 &lt; largeur &lt; 1 025 | 620 | élevé | Tablette (paysage) |
| largeur &lt;= 1025 | full (taille d’origine) | élevé | Poste de travail |

#### Propriétés {#properties}

La boîte de dialogue permet de modifier les propriétés pour votre instance du composant Image adaptative. Parmi ces propriétés, nombreuses sont celles qui sont communes au composant d’image sur lequel il est basé. Les propriétés sont disponibles dans deux onglets :

* **Image**

   * **Image**
Faites glisser une image à partir de l’outil de recherche de contenu ou cliquez pour ouvrir une fenêtre de recherche dans laquelle vous pouvez charger une image. Ensuite, vous pouvez la recadrer, la faire pivoter ou la supprimer. Pour effectuer un zoom avant ou arrière sur l’image, utilisez le curseur situé sous l’image (au-dessus des boutons OK et Annuler).

   * **Recadrer**
Copier une partie d’une image. Faites glisser la bordure pour recadrer l’image.

   * **Rotation**
Cliquez plusieurs fois sur Rotation pour faire pivoter l’image dans la position souhaitée.

   * **Effacer**
Permet de supprimer l’image actuelle.

* **Avancé**

   * **Titre**
Le composant Image adaptative n’utilise pas cette propriété.

   * **Texte de remplacement**
Texte secondaire à utiliser pour l’image.

   * **Lier à**
Le composant Image adaptative n’utilise pas cette propriété.

   * **Description**
Le composant Image adaptative n’utilise pas cette propriété.

#### Extension du composant d’image adaptative {#extending-the-adaptive-image-component}

Pour plus d’informations sur la personnalisation du composant Image adaptative, voir [Présentation du composant d’image adaptative](/help/sites-developing/responsive.md#using-adaptive-images).

### Carrousel {#carousel}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal du carrousel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=fr) au lieu de .

Le composant Carrousel vous permet d’afficher des images associées à des pages individuelles :

* un à la fois
* pour une courte période
* dans un ordre que vous spécifiez
* avec un délai que vous spécifiez

Les commandes cliquables permettent également à l’utilisateur de parcourir les pages affichées en temps réel, à la demande. La sélection de l’image de page actuellement visible vous conduit à cette page. En d’autres termes, le carrousel agit comme une commande de navigation.

#### Propriétés {#properties-1}

Ces propriétés sont disponibles dans deux onglets :

* **Carrousel**
Vous spécifiez ici la manière dont le carrousel fonctionne :

   * Vitesse de lecture
Le temps en millisecondes avant l’affichage de la diapositive suivante.
   * Temps de transition Délai en millisecondes de la transition entre deux diapositives.
   * Type des commandes
Diverses options sont disponibles dans un menu déroulant ; par exemple, les boutons Précédent/Suivant ou les commutateurs haut-droit.

* **Liste**

  Vous spécifiez ici la manière dont les pages sont incluses dans votre carrousel :

   * **Créer la liste à l’aide de**
Il existe plusieurs façons de créer une liste de pages : Pages enfants, Liste fixe, Recherche ou Recherche avancée (toutes décrites ci-dessous). Quelle que soit la méthode choisie, les pages que vous incluez dans votre liste doivent déjà être associées à une image. C’est cette image qui s’affiche dans le carrousel. S’il n’existe aucune image pour une page donnée sous les Propriétés de page de cette page, vous devez associer une image à la page avant de commencer. Dans le cas contraire, le carrousel affiche une page principalement vierge. Voir [Modification des propriétés de page](/help/sites-authoring/editing-page-properties.md).
Selon l’élément que vous choisissez, un nouveau panneau s’affiche :

      * **Options des pages enfants**

         * **Page parente**
Spécifiez un chemin d’accès manuellement ou à l’aide du sélecteur. Laissez vide pour utiliser la page actuelle comme page parente.

      * **Options de la liste fixe**

         * **Pages**
Sélectionnez une liste de pages. Utilisation `+` pour ajouter d’autres entrées et les boutons haut/bas pour ajuster l’ordre.

      * **Options de recherche**

         * **Démarrer dans**
Spécifiez un chemin de départ manuellement ou à l’aide du sélecteur.

         * **Requête de recherche**
Entrez une requête de recherche en texte brut.

      * **Options de la recherche avancée**

         * **Notation des prédicats de QueryBuilder**
Entrez une requête de recherche à l’aide de la notation des prédicats de QueryBuilder. Par exemple, entrez « fulltext=Marketing » pour afficher dans le carrousel toutes les pages comportant le terme « Marketing » dans leur contenu.
Consultez [API QueryBuilder](/help/sites-developing/querybuilder-api.md) pour consulter une étude complète sur les expressions de requête et d’autres exemples.

   * **Classer par**
Sélectionnez `jcr:title`, `jcr:created`, `cq:lastModified` ou `cq:template` dans le menu déroulant.

   * **Limite**
Facultatif. Nombre maximal d’éléments que vous souhaitez utiliser dans le carrousel.

>[!NOTE]
>
>Vous pouvez créer un composant de carrousel personnalisé pour Adobe Experience Manager qui affiche des ressources numériques dans la gestion des actifs numériques AEM. Voir [Création de composants de carrousel personnalisés pour Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr).

### Graphique {#chart}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Le composant Graphique vous permet d’ajouter un graphique à barres, en courbes ou en secteurs. AEM crée un graphique à partir des données que vous fournissez. Vous fournissez des données en les saisissant directement dans l’onglet Données ou en copiant et en collant une feuille de calcul.

* **Données**

   * **Données de graphique**
Ajoutez vos données de graphique au format CSV ; une virgule (« , ») est utilisée comme séparateur de valeurs.

* **Avancé**

   * **Type de graphique**
Effectuez un choix parmi les types suivants : Histogramme, Graphique en secteurs et Graphique en courbe.

   * **Texte de remplacement**
Affiche du texte de remplacement au lieu du graphique.

   * **Largeur**
Largeur du graphique en pixels.

   * **Hauteur**
Hauteur du graphique en pixels.

L’exemple suivant illustre des données de graphique suivies de l’histogramme qui en résulte :

![chlimage_1-89](assets/chlimage_1-89.png) ![dc_chart_use](assets/dc_chart_use.png)

>[!NOTE]
>
>Vous pouvez créer un contrôle graphique d’AEM personnalisé qui affiche les données dans AEM JCR. Pour plus d’informations, voir [Affichage des données Adobe Experience Manager dans un graphique](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr).

### Fragment de contenu {#content-fragment}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de fragment de contenu](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=fr) au lieu de .

[Fragments de contenu](/help/sites-authoring/content-fragments.md) sont créées et gérées en tant que ressources indépendantes de la page. Vous pouvez ensuite utiliser ces fragments et leurs variantes lors de la création de vos pages de contenu.

### Importateur de conception {#design-importer}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Ce composant permet de télécharger un fichier zip contenant un module de conception.

### Télécharger {#download}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Le composant Télécharger crée un lien dans la page web sélectionnée pour télécharger un fichier spécifique. Vous pouvez soit faire glisser une ressource à partir de l’outil de recherche de contenu, soit charger un fichier.

* **Télécharger**

   * **Description**
Courte description affichée avec le lien de téléchargement.

   * **Fichier**
Le fichier peut être téléchargé sur la page web qui en résulte. Faites glisser une ressource à partir de l’outil de recherche de contenu ou sélectionnez la zone afin de télécharger le fichier à télécharger.

L’exemple suivant montre le composant Télécharger dans Geometrixx :

![dc_download_use](assets/dc_download_use.png)

### Externe {#external}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Le composant d’intégration d’application externe (**Externe**) permet d’incorporer des applications externes dans une page AEM en utilisant un iframe.

* **Externe**

   * **Application cible**
Indiquez l’URL de l’application Web à intégrer, par exemple :

     ```
     https://en.wikipedia.org/wiki/Main_Page
     ```

   * **Transmettre les paramètres**
Cochez les cases correspondant aux paramètres à transmettre à l’application, lorsque cela s’avère nécessaire.

   * **Largeur et Hauteur**
Définissez la taille de l’iframe.

L’application externe est intégrée au système de paragraphes de la page AEM, par exemple, lorsque vous utilisez une application cible de `https://en.wikipedia.org/wiki/Main_Page` :

![chlimage_1-90](assets/chlimage_1-90.png)

>[!NOTE]
>
>Selon votre cas d’utilisation, d’autres options sont disponibles pour l’intégration d’applications externes, par exemple : [Intégration de portlets](/help/sites-administering/aem-as-portal.md).

### Flash {#flash}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

Le composant Flash vous permet de charger une animation Flash. Vous pouvez faire glisser une ressource Flash de l’outil de recherche de contenu sur le composant, ou vous pouvez utiliser la boîte de dialogue :

* **Flash**

   * **Animation Flash**

     Fichier d’animation Flash. Faites glisser une ressource à partir de l’outil de recherche de contenu ou cliquez pour ouvrir une fenêtre de navigation.

   * **Taille**

     Dimensions en pixels de la zone d’affichage contenant l’animation.

* **Image de remplacement**

  Autre image à afficher.

* **Avancé**

   * **Menu contextuel**

     Indique si le menu contextuel doit être affiché ou masqué.

   * **Mode Fenêtre**

     Permet de spécifier comment la fenêtre doit apparaître (opaque, transparente ou comme une fenêtre distincte, par exemple).

   * **Couleur d’arrière-plan**

     Couleur de fond sélectionnée à partir de la palette de couleurs fournie.

   * **Version minimale**

     Version minimale d’Adobe Flash Player requise pour exécuter l’animation. La valeur par défaut est 9.0.0.

   * **Attributs**

     Tous les autres attributs requis.

### Image {#image}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal Image](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=fr) au lieu de .

Le composant Image affiche une image et le texte qui l’accompagne selon les paramètres définis.

Vous pouvez télécharger une image, puis la modifier et la manipuler (par exemple, la recadrer, la faire pivoter, ajouter un lien/titre/texte).

Vous pouvez faire glisser et déposer une image à partir du [Explorateur de ressources](/help/sites-authoring/author-environment-tools.md#assets-browser) directement sur le composant ou son [Boîte de dialogue de configuration](/help/sites-authoring/editing-content.md#component-edit-dialog). Vous pouvez également télécharger une image à partir de la boîte de dialogue Configurer ; cette boîte de dialogue contrôle également toutes les définitions et la manipulation de l’image :

![chlimage_1-91](assets/chlimage_1-91.png)

Une fois l’image téléchargée (et pas avant), vous pouvez utiliser [modification statique](/help/sites-authoring/editing-content.md#edit-content) pour recadrer/faire pivoter l’image selon les besoins :

![Barre d’outils d’édition statique](do-not-localize/chlimage_1-15.png)

>[!NOTE]
>
>L’éditeur statique utilise la taille et les proportions d’origine de l’image lors de l’édition. Vous pouvez également spécifier des propriétés de hauteur et de largeur. Toute restriction de taille et de proportion définie dans les propriétés est appliquée lorsque vous enregistrez vos modifications.
>
>Selon votre instance, des restrictions minimales et maximales peuvent également être imposées par la variable [conception de la page](/help/sites-developing/designer.md). Ces restrictions sont développées pendant la mise en oeuvre du projet.

Différentes autres options sont disponibles en mode Plein écran. Par exemple, Carte et Zoom :

![Mode de modification plein écran - carte et zoom](do-not-localize/chlimage_1-16.png)

>[!NOTE]
>
>Internet Explorer ne permet pas de surveiller la progression du chargement.
>
>Les utilisateurs d’Internet Explorer doivent télécharger l’image et cliquer sur **Ok**, puis rouvrez l’image pour afficher le fichier chargé dans l’aperçu et pour pouvoir effectuer des modifications (c’est-à-dire, le recadrage).
>
>Reportez-vous à [Plateformes certifiées](/help/release-notes/release-notes.md#certifiedplatforms) pour en savoir plus sur les fonctions HTML5 utilisées par AEM.

Lorsqu’une image est chargée, vous pouvez configurer ce qui suit :

* **Map**

  Pour mapper une image, sélectionnez Mapper. Vous pouvez spécifier ensuite comment créer la zone cliquable (rectangle, polygone, etc.) et l’emplacement sur lequel la zone doit pointer.

* **Recadrer**

  Pour supprimer une partie d’une image, sélectionnez Recadrer. Utilisez la souris pour effectuer le recadrage.

* **Rotation**

  Pour faire pivoter une image, sélectionnez Rotation. Répétez l’opération jusqu’à ce que l’image ait pivoté comme vous le souhaitez.

* **Effacer**

  Permet de supprimer l’image actuelle.

* **Titre**

  Titre de l’image.

* **Texte de remplacement**

  Texte de remplacement à utiliser lors de la création de contenu accessible.

* **Lier à**

  Créez un lien vers les ressources ou d’autres pages de votre site Web.

* **Description**

  Description de l’image.

* **Taille**

  Permet de définir la hauteur et la largeur de l’image.

>[!NOTE]
>
>Certaines options ne sont disponibles que dans l’éditeur plein écran.

L’image finale (avec son **Titre** et sa **Description**) peut s’afficher comme suit :

![chlimage_1-92](assets/chlimage_1-92.png)

### Conteneur de disposition {#layout-container}

Ce composant fournit un système de paragraphes/grille qui permet d’ajouter et de positionner des composants dans un [grille réactive](/help/sites-authoring/responsive-layout.md). Vous pouvez définir différentes mises en page de contenu en fonction de la largeur des appareils cibles, y compris divers téléphones, tablettes et ordinateurs de bureau.

![chlimage_1-93](assets/chlimage_1-93.png)

>[!NOTE]
>
>Ce composant a été mis en œuvre avec le [langage de modèle HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=fr).

### Liste {#list}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal Liste](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) au lieu de .

Le composant Liste vous permet de configurer des critères de recherche pour l’affichage d’une liste :

* **Liste**

   * **Construire la liste avec**

     Indiquez ici où la liste récupère son contenu. Il existe plusieurs méthodes :

   * Selon l’élément que vous choisissez, un nouveau panneau s’affiche :

      * **Options des pages enfants**

         * **Enfants de** (Page parente)

           Spécifiez un chemin manuellement ou à l’aide du sélecteur. Laisser ce champ vide pour utiliser la page active en tant que Parent.

      * **Options de la liste fixe**

         * **Pages**

           Sélectionnez une liste de pages. Utilisez + pour ajouter d’autres entrées et les boutons haut/bas pour ajuster l’ordre.

      * **Options de recherche**

         * Démarrer dans

           Spécifiez un chemin de départ manuellement ou à l’aide du sélecteur.

         * Requête de recherche

           Vous pouvez entrer une requête de recherche en texte brut.

      * **Options de la recherche avancée**

         * **Notation des prédicats de QueryBuilder**

           Vous pouvez saisir une requête de recherche à l’aide de la notation de prédicat de QueryBuilder. Par exemple, vous pouvez saisir « fulltext=Marketing » pour que toutes les pages comportant « Marketing » dans leur contenu s’affichent dans le carrousel.

           Consultez [API QueryBuilder](/help/sites-developing/querybuilder-api.md) pour découvrir une étude complète sur les expressions de requête et d’autres exemples.

      * **Balises**

        Spécifiez la variable **Page parente**, **Balises/Mots-clés** et vos critères de correspondance requis.

   * **Afficher comme**

     Permet de spécifier comment les éléments doivent être répertoriés (Liens, Teasers et Actualités).

   * **Classer par**

     Permet de spécifier si la liste doit être classée. Si c’est le cas, indique les critères à utiliser pour le tri. Vous pouvez saisir un critère ou en sélectionner un dans la liste déroulante fournie à cet effet.

   * **Limite**

     Permet de spécifier le nombre maximal d’éléments à afficher dans la liste.

   * **Activer le flux**

     Indique si un flux RSS doit être activé pour la liste.

   * **Paginer après**

     Vous pouvez indiquer ici le nombre d’éléments de la liste à afficher simultanément. Une liste comportant plus d’éléments que spécifié utilise la pagination pour afficher la liste en plusieurs parties.

L’exemple suivant illustre une **Liste** de la façon dont elle peut afficher une liste de pages enfants (la conception est contrôlée par les définitions CSS personnalisées d’une conception de site).

![dc_list_use](assets/dc_list_use.png)

### Connexion {#login}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

Fournit les champs Nom d’utilisateur et Mot de passe .

![chlimage_1-94](assets/chlimage_1-94.png)

Vous pouvez configurer :

* Se connecter

   * Libellé de section

     Texte d’introduction pour les champs de saisie.

   * Libellé du nom de l’utilisateur

     Texte pour étiqueter le champ de nom d’utilisateur.

   * Libellé du mot de passe

     Texte pour étiqueter le champ du mot de passe.

   * Libellé du bouton Se connecter

     Texte du bouton de connexion.

   * Rediriger vers

     Vous pouvez spécifier la page de votre site Web qui doit s’ouvrir une fois l’utilisateur connecté.

* Déjà connecté

   * Libellé du bouton Continuer

     Texte pour indiquer que l’utilisateur est déjà connecté.

### Statut de la commande {#order-status}

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

* **Titre**

   * **Titre**

     Spécifiez le texte du titre à afficher.

   * **Lien**

     Spécifiez la page (produit) pour laquelle le statut de la commande doit être affiché.

   * **Type / Taille**

     Faites votre choix dans la sélection fournie.

![chlimage_1-95](assets/chlimage_1-95.png)

### Référence {#reference}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de fragment de contenu](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=fr) au lieu de .

Le **Référence** vous permet de référencer du texte à partir d’une autre page de votre site web AEM (dans l’instance active). Le contenu du paragraphe référencé s’affiche alors comme s’il se trouvait sur la page active. Le contenu est mis à jour lorsque le paragraphe source change (une actualisation de la page peut s’avérer nécessaire).

* **Référence de paragraphe**

   * **Référence**

     Spécifiez le chemin d’accès à la page et au paragraphe à référencer (y compris le contenu).

Pour spécifier le chemin d’accès à un paragraphe, vous devez ajouter le suffixe suivant :

`.../jcr:content/par/<paragraph-ID>`

Par exemple :

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

Outre le référencement d’un paragraphe spécifique, le chemin peut également être modifié pour spécifier un système de paragraphes entier. Vous pouvez effectuer cette référence en suffixant le chemin d’accès avec les éléments suivants :

`/jcr:content/par`

Par exemple :

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

Après la configuration, le contenu s’affiche exactement comme sur la page source. Le fait qu’il s’agisse d’une référence n’est visible que lorsque vous ouvrez le composant en vue de le modifier :

![chlimage_1-96](assets/chlimage_1-96.png)

### Rechercher {#searching}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal Recherche rapide](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/quick-search.html) au lieu de .

Le composant Rechercher offre des capacités de recherche à votre page.

Vous pouvez configurer :

* Rechercher

   * **Types de nœuds**

     Si la recherche doit se limiter à un type de nœud spécifique, indiquez-le ici. Par exemple, `cq:Page`.

   * **Chemin d’accès de la recherche**

     Indiquez la page racine de la branche que vous souhaitez rechercher.

   * **Texte du bouton de recherche**

     Nom affiché sur le bouton de recherche actuel.

   * **Texte des statistiques**

     Texte affiché au-dessus des résultats de la recherche.

   * **Texte Aucun résultat**

     Si la recherche ne renvoie aucun résultat, le texte entré ici est affiché.

   * **Vérifier l’orthographe du texte**

     Si une personne saisit un terme similaire, ce texte est affiché devant le terme.
Par exemple, si vous saisissez `Geometrixxe`, le système affiche &quot;Voulez-vous dire ? Geometrixx&quot;.

   * **Texte Pages similaires**

     Texte affiché à côté d’un résultat pour des pages similaires. Pour afficher les pages ayant un contenu similaire, cliquez sur ce lien.

   * **Texte Recherches connexes**

     Texte affiché à côté des recherches de termes et sujets associés.

   * **Texte Tendances des recherches**

     Titre situé au-dessus des termes de recherche entrés par un utilisateur.

   * **Libellé Pages de résultats**

     Texte qui apparaît en bas de cette liste avec des liens vers d’autres pages de résultats.

   * **Libellé Précédent**

     Nom qui apparaît sur le lien vers les pages de recherche précédentes.

   * **Libellé Suivant**

     Nom qui apparaît sur le lien vers les pages de recherche suivantes.

L’exemple ci-dessous montre le composant Recherche après une recherche du mot *`geometrixx`* dans le répertoire racine d’une installation standard. Il illustre également la pagination des résultats :

![dc_search_use](assets/dc_search_use.png)

L’exemple suivant montre un terme de recherche mal orthographié et non disponible :

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Plan du site {#sitemap}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Navigation](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/navigation.html), [Navigation par langue](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/language-navigation.html), et [Composants principaux du chemin de navigation](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/breadcrumb.html) au lieu de .

Liste automatique du plan du site qui (avec les paramètres par défaut) répertorie toutes les pages (sous forme de liens actifs) du site Web actuel. Par exemple (extrait) :

![dc_sitemap_use](assets/dc_sitemap_use.png)

Au besoin, vous pouvez configurer les éléments suivants :

* **Plan du site**

   * **Chemin racine**

     Chemin d’accès à partir duquel la liste doit commencer.

### Slideshow {#slideshow}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal du carrousel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=fr) au lieu de .

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

Ce composant vous permet de charger une série d’images à afficher sous forme de diaporama sur votre page. Vous pouvez ajouter ou supprimer des images et attribuer un titre à chacune d’elles. Sous Avancé, vous pouvez également spécifier la taille de la zone d’affichage.

Vous pouvez configurer :

* **Diapositives**

   * **Nouvelle diapositive**

     Spécifiez une sélection de diapositives à l’aide des boutons **Ajouter** (et **Supprimer**).

   * **Titre**

     Si nécessaire, indiquez un titre. Le titre est superposé sur la diapositive appropriée.

* **Avancé**

   * **Taille**

     Permet de spécifier la largeur et la hauteur en pixels.

Le composant Diaporama affiche ensuite de manière répétée chacune d’elles de manière séquentielle, pendant une courte période, avant de passer à la diapositive suivante :

![dc_slideshow_use](assets/dc_slideshow_use.png)

### Tableau {#table}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal Texte](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=fr) au lieu de .

>[!NOTE]
>
>Le **Tableau** Le composant de base est basé sur la variable [Éditeur de texte enrichi](/help/sites-authoring/rich-text-editor.md), comme l’est la variable **[Texte](#text)** Composant de base.

Le **Tableau** est préconfiguré pour vous permettre de créer, de remplir et de formater un tableau. La boîte de dialogue vous permet de configurer votre tableau et de créer le contenu en effectuant l’une des opérations suivantes :

* à partir de zéro
* copie et collage d’une feuille de calcul ou d’un tableau à partir d’un éditeur externe (Excel, OpenOffice et Bloc-notes, par exemple).

Vous pouvez apporter des modifications standard au contenu à l’aide de l’éditeur intégré :

![dc_table](assets/dc_table.png)

En mode Plein écran, vous pouvez configurer la disposition du tableau :

![chlimage_1-97](assets/chlimage_1-97.png)

La capture d’écran ci-après illustre l’utilisation du composant Tableau (la conception est déterminée par le CSS propre au site) :

![dc_table_use](assets/dc_table_use.png)

### Nuage de balises {#tag-cloud}

Un nuage de balises affiche une sélection des balises appliquées au contenu de votre site web sous forme graphique :

![dc_tagclouduse](assets/dc_tagclouduse.png)

Lorsque vous configurez le composant Nuage de balises, vous pouvez spécifier les options suivantes :

* **Balises à afficher**

  Emplacement à partir duquel les balises à afficher sont rassemblées. Faites votre choix entre une page, une page avec tous les enfants ou toutes les balises.

* **Page**

  Sélectionnez la page à référencer.

* **Aucun lien sur les balises**

  Permet de spécifier si les balises affichées doivent se comporter comme des liens.

Pour plus d’informations sur l’application de balises, voir [Utilisation des balises](/help/sites-authoring/tags.md).

### Texte {#text}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal Texte](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=fr) au lieu de .

>[!NOTE]
>
>Le **Texte** Le composant de base est basé sur la variable [Éditeur de texte enrichi](/help/sites-authoring/rich-text-editor.md), comme l’est la variable **Tableau** Composant de base.

Le composant Texte permet de saisir un bloc de texte à l’aide d’un éditeur WYSIWYG, avec les fonctionnalités fournies par [Éditeur de texte enrichi](/help/sites-authoring/rich-text-editor.md). Une sélection d’icônes vous permet de mettre en forme votre texte, notamment les caractéristiques de police, l’alignement, les liens, les listes et la mise en retrait.

![chlimage_1-98](assets/chlimage_1-98.png)

Lorsque vous ouvrez la **boîte de dialogue de configuration**, vous pouvez également définir les éléments suivants :

* **Espacement**
* **Style de texte**

Le texte formaté s’affiche sur la page. La conception réelle dépend du CSS du site :

![dc_text_use](assets/dc_text_use.png)

Pour plus d’informations sur le composant Texte et les fonctions de l’éditeur de texte enrichi, reportez-vous à la page [Éditeur de texte enrichi](/help/sites-authoring/rich-text-editor.md).

#### Édition statique {#inplace-editing}

Outre le mode d’édition de texte enrichi basé sur une boîte de dialogue, AEM fournit également [Modification statique](/help/sites-authoring/editing-content.md), qui permet de modifier directement le texte tel qu’il s’affiche dans la mise en page.

### Texte et Image {#text-image}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Image](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=fr) et [Composant principal Texte](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=fr) au lieu de .

Le composant Texte et image permet d’ajouter un bloc de texte et une image. Vous pouvez également ajouter et modifier du texte et des images séparément. Voir [Texte](#text) et [Image](#image) composants pour plus de détails.

![chlimage_1-99](assets/chlimage_1-99.png)

Vous pouvez configurer :

* **Styles de composant** (**Styles**)

  Vous pouvez aligner ici l’image à droite ou à gauche. Le paramètre par défaut est aligné à **Gauche**, avec l’image à gauche.

* **Propriétés de l’image** (**Propriétés d’image avancées**)

  Sous cet onglet, vous pouvez spécifier les paramètres suivants :

   * **Ressource image**

     Téléchargez l’image requise.

   * **Titre**

     Titre du bloc, affiché en pointant la souris.

   * **Texte de remplacement**

     Texte de remplacement à afficher lorsque l’image ne peut pas être affichée. Si rien n’est indiqué, le titre est utilisé.

   * **Lier à**

     Spécifiez un chemin cible.

   * **Description**

     Description de l’image.

   * **Taille**

     Définit la hauteur et la largeur de l’image.

L’exemple suivant illustre un composant Image de texte qui affiche l’image alignée à gauche :

![dc_textimage_use](assets/dc_textimage_use.png)

### Titre {#title}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal du titre](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en) au lieu de .

Le composant Titre peut effectuer l’une des opérations suivantes :

* Affichez le nom de la page active en laissant le champ Titre vide.
* Affichez le texte que vous indiquez dans le champ Titre .

Vous pouvez configurer :

* **Titre**

  Si vous voulez utiliser un nom différent du titre de la page, saisissez-le ici.

* **Lien**

  URI si le titre doit se comporter comme un lien.

* **Type / Taille**

  Sélectionnez Petit ou Grand dans la liste déroulante. Petit est généré en tant qu’image. L’option Grand est générée sous forme de texte.

L’exemple suivant illustre une **Titre** composant affiché ; la conception est déterminée par le CSS spécifique au site.

![dc_title_use](assets/dc_title_use.png)

### Vidéo {#video}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant Incorporer des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html) au lieu de .

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

Le **Vidéo** permet de placer un élément vidéo prédéfini prêt à l’emploi sur une page.

Voir aussi [Configuration des profils vidéo](/help/sites-administering/config-video.md#configuringvideoprofiles) à utiliser avec les éléments HTML5.

Après avoir placé une instance du composant sur votre page, vous pouvez configurer les éléments suivants :

* Vidéo

   * **Ressource vidéo**

     Chargez ou déposez la ressource vidéo.

   * **Taille**

     La taille native de la vidéo (largeur x hauteur en pixels) apparaît dans les zones en regard de Taille (voir ci-dessus). Saisissez ici manuellement la largeur et la hauteur pour remplacer les dimensions natives de la vidéo. Sélection **OK** ferme la boîte de dialogue.

>[!NOTE]
>
>Les formats pris en charge sont les suivants :
>
>* `.mp4`
>* `Ogg`
>* `FLV` (Flash video)

## Colonnes {#columns}

Les colonnes sont un mécanisme permettant de contrôler la mise en page du contenu dans AEM. Dans une installation standard, des composants pour créer deux ou trois colonnes sont fournis.

L’exemple suivant illustre le composant Deux colonnes en cours d’utilisation. Vous pouvez utiliser des espaces réservés pour les nouveaux composants :

![dc_columncontroluse](assets/dc_columncontroluse.png)

### 2 colonnes {#columns-1}

Composant Contrôle de colonne qui utilise par défaut deux colonnes égales.

### 3 colonnes {#columns-2}

Composant Contrôle de colonne qui utilise par défaut trois colonnes égales.

### Contrôle de colonne {#column-control}

Le composant Contrôle de colonne permet aux utilisateurs de sélectionner la manière dont ils souhaitent fractionner le contenu du panneau principal de la page web en plusieurs colonnes. Les utilisateurs peuvent sélectionner le nombre de colonnes requis (dans une liste prédéfinie), puis créer, supprimer ou déplacer du contenu dans chacune des colonnes.

* **Contrôle de colonne**

   * **Disposition des colonnes**

     Sélectionnez le nombre de colonnes à rendre. Une fois créée, chaque colonne dispose de son propre lien pour faire glisser des composants ou des ressources lors de l’ajout de contenu.

## Formulaire {#form}

>[!CAUTION]
>
>Le composant Foundation est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Les composants Formulaire servent à créer des formulaires permettant aux visiteurs d’envoyer leur saisie. Les composants Forms et de formulaire peuvent être utilisés pour collecter des informations, notamment les commentaires des utilisateurs (par exemple, un questionnaire de satisfaction client) et des informations sur les utilisateurs (par exemple, l’enregistrement des utilisateurs).

>[!NOTE]
>
>Voir [Aide d’AEM Forms](/help/forms/home.md) pour plus d’informations sur AEM Forms.

Forms est constitué de plusieurs composants différents :

* **Formulaire**

  Le composant Formulaire définit le début et la fin d’un nouveau formulaire dans la page. D’autres composants peuvent ensuite être placés entre ces éléments, tels que des tableaux et des téléchargements.

* **Champs et éléments de formulaire**

  Les champs de formulaire et les éléments peuvent inclure des zones de texte, des boutons radio et des images. L’utilisateur exécute souvent une action dans un champ de formulaire (saisie de texte, par exemple). Pour plus d’informations, reportez-vous à la section Eléments de formulaire individuels .

* **Composants de profil**

  Les composants de profil se rapportent aux profils du visiteur utilisés pour la collaboration sociale et d’autres domaines dans lesquels la personnalisation des visiteurs est requise.

Vous trouverez ci-dessous un exemple de formulaire. Il se compose de la variable **Formulaire** composant (début et fin), avec deux **Formulaire** **Texte** champs utilisés pour la saisie, un **Général** **Texte** champ utilisé pour le texte du prospect et une **Envoyer** bouton .

![dc_form](assets/dc_form.png)

>[!NOTE]
>
>Pour plus d’informations sur le développement et la personnalisation de vos formulaires, reportez-vous à la section [Développement d’une page Forms](/help/sites-developing/developing-forms.md). Cette fonctionnalité inclut l’ajout d’actions, de contraintes, le préchargement de champs et l’utilisation de scripts pour appeler un service à l’action, entre autres.

### Paramètres communs à (plusieurs) composants de formulaire {#settings-common-to-many-form-components}

Bien que chacun des composants de formulaire ait un objectif différent, la plupart sont composés d’options et de paramètres similaires.

Lors de la configuration de l’un des composants de formulaire, les onglets suivants sont disponibles dans la boîte de dialogue :

* **Titre et texte**

  Vous devez y indiquer les informations de base, telles que le titre du formulaire et le texte d’accompagnement. Le cas échéant, il vous permet également de définir d’autres informations clés, telles que si le champ peut être sélectionné plusieurs fois et si des éléments peuvent être sélectionnés.

* **Valeurs initiales**

  Permet de spécifier une valeur par défaut.

* **Contraintes**

  Vous pouvez indiquer ici si un champ est obligatoire et y placer des contraintes (par exemple, doit être numérique).

* **Style**

  Indique la taille et le style des champs.

>[!NOTE]
>
>Les champs affichés varient considérablement en fonction du composant individuel.

Ces onglets vous fournissent les paramètres nécessaires. Les onglets peuvent dépendre du type de composant individuel, mais peuvent inclure les éléments suivants :

* **Titre et texte**

   * **Nom de l’élément**

     Nom de l’élément de formulaire. Il indique où, dans le référentiel, les données sont stockées.
Ce champ est obligatoire et ne doit contenir que les caractères suivants :

      * caractères alphanumériques
      * `_ . / : -`

   * **Titre**

     Titre affiché avec le champ. Si rien n’est indiqué, le titre par défaut s’affiche.

   * **Description**

     Vous permet de fournir des informations supplémentaires à l’utilisateur, si nécessaire. Sur le formulaire, il s’affiche sous le champ, dans une police plus petite que le titre.

   * **Afficher/Masquer**

     Détermine le moment où le champ est visible.

* **Valeurs initiales**

   * **Valeur par défaut**

     Valeur affichée dans le champ à l’ouverture du formulaire. C’est-à-dire avant que l’utilisateur n’ait saisi des données.

* **Contraintes**

   * **Requis**

     Les contraintes dépendent du type de composant de formulaire, mais fournit une ou plusieurs zones de clic pour indiquer que ce champ est obligatoire ou que certaines parties de ce champ sont obligatoires.

   * **Message obligatoire**

     Message informant les utilisateurs que ce champ est obligatoire. Un champ obligatoire est également marqué d’un astérisque.

   * **Contrainte**

     Les contraintes disponibles pour la sélection dépendent du type de composant de formulaire.

   * **Message de contrainte**

     Message qui informe les utilisateurs de ce qui est obligatoire.

* **Style**

   * **Taille**

     En lignes et en colonnes.

   * **Largeur**

     En pixels.

   * **CSS**

### Formulaire (composant) {#form-component}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de conteneur de formulaires](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html) au lieu de .

Le composant Formulaire définit le début et la fin d’un formulaire à l’aide de la fonction **Début du formulaire** et **Fin de formulaire** éléments . Le début et la fin sont toujours associés pour s’assurer que le formulaire est correctement défini.

![dc_form-1](assets/dc_form-1.png)

Entre le début et la fin d’un formulaire, vous pouvez ajouter des composants qui définissent les champs de saisie réels à l’intention des utilisateurs.

>[!NOTE]
>
>Le composant de formulaire des composants de base ne prend en charge que l’utilisation d’autres composants de formulaire (bouton, texte, masqué, etc.). Utilisation [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) les composants de formulaire dans un formulaire de composant de base (et inversement) ne sont pas pris en charge.

#### Début du formulaire {#start-of-form}

Ce composant définit le début d’un nouveau formulaire sur une page. Vous pouvez configurer :

* **Formulaire**

   * **Page de remerciement**

     Page à référencer pour remercier les visiteurs pour leur message. Si rien n’est indiqué, le formulaire s’affiche de nouveau après envoi.

   * **Démarrer le workflow**

     Détermine quel workflow est déclenché une fois le formulaire envoyé.

* **Avancé**

   * **Type d’action**

     Un formulaire requiert une action. L’action définit l’opération déclenchée avec les données soumises par l’utilisateur (semblable à action= en langage HTML). Certains ont besoin d’une **Configuration d’action**.
Plusieurs types d’action sont inclus dans une installation AEM standard :

      * **Demande de compte**
      * **Créer le contenu**
      * **Créer un prospect**
      * **Créer un compte et le mettre à jour**
      * **Service de messagerie électronique : créer un abonné et l’ajouter à la liste**
      * **Service de messagerie électronique : envoyer un message de répondeur automatique**
      * **Service de messagerie électronique : désabonner l’utilisateur de la liste**
      * **Modifier la communauté**
      * **Modifier les ressources**
      * **Modifier les ressources contrôlées du workflow**
      * **Courrier**
      * **Détails de la commande passée**
      * **Mise à jour du profil**
      * **Réinitialiser le mot de passe**
      * **Définir le mot de passe**
      * **Stocker le contenu**

        Type d’action par défaut.

      * **Stocker le contenu avec les chargements**
      * **Envoyer la commande**
      * **Désabonner l’abonné**
      * **Mettre à jour la commande**

   * **Identifiant de formulaire**

     L’identifiant du formulaire l’identifie de façon unique. Utilisez cet identifiant si plusieurs formulaires figurent sur une seule page ; assurez-vous qu’ils présentent des identifiants différents.

   * **Chemin de chargement**

     Chemin d’accès aux propriétés de nœud, utilisé pour charger les valeurs prédéfinies dans les champs du formulaire.

     Champ facultatif qui spécifie le chemin d’accès à un noeud dans le référentiel. Lorsque ce nœud comporte des propriétés qui correspondent aux noms des champs, les champs adéquats du formulaire sont préchargés avec la valeur de ces propriétés. S’il n’existe aucune correspondance, le champ contient la valeur par défaut.

     Le champ **Chemin de chargement** vous permet de précharger des valeurs dans les champs obligatoires du formulaire. Consultez [Préchargement des valeurs de formulaire](/help/sites-developing/developing-forms.md#preloading-form-values).

   * **Validation du client**

     Indique si la validation du client est requise pour ce formulaire (validation du serveur) *always* se produit). La validation du client peut être réalisée à l’aide de la fonction **Captcha Forms** composant.

   * **Type de ressource de validation**

     Définit le type de ressource de validation si vous souhaitez valider la totalité du formulaire (et non des champs séparés). Si vous validez le formulaire dans son intégralité, vous devez également inclure l’un des éléments suivants :

      * Un script pour la validation du client

        `/apps/<*myApp*>/form/<*myValidation*>/formclientvalidation.jsp`

      * Un script pour la validation du côté serveur

        `/apps/<*myApp*>/form/<*myValidation*>/formservervalidation.jsp`

   * **Configuration de l’action**

     Les options disponibles dans **Configuration d’action** dépendent de la sélection **Type d’action**:

      * **Demande de compte**

         * **Page Créer un compte**

           Page utilisée lors de la création d’un compte.

      * **Créer le contenu**

         * Chemin d’accès au contenu

           Chemin d’accès à tout type de contenu utilisé par le formulaire. Saisissez un chemin qui se termine par une barre oblique `/`. La barre oblique signifie que, pour chaque port de formulaire, un nouveau nœud est créé à l’emplacement indiqué, par exemple :

           `/forms/feedback/`

         * **Type**

           Sélectionnez le type requis.

         * **Formulaire**

           Spécifiez le formulaire.

         * **Rendu avec**

           Sélectionnez l’option désirée dans la liste.

         * **Type de ressource**

           S’il est défini, il est ajouté à chaque commentaire sous la forme `sling:resourceType`

         * **Sélecteur d’affichage**

      * **Créer un prospect**

         * **Le prospect est ajouté à cette liste.**

           Spécifiez la liste de prospects requise.

      * **Créer un compte et le mettre à jour**

         * **Groupe initial**

           Groupe auquel affecter un nouvel utilisateur.

         * **Accueil**

           Page à afficher après une connexion réussie.

         * **Chemin**

           Chemin (relatif) vers l’emplacement de création et de stockage du nouveau compte.

         * **Afficher des données...**

           Lorsque vous sélectionnez ce bouton, les informations relatives aux résultats du formulaire sont accessibles dans l’éditeur en bloc. Vous avez alors la possibilité d’exporter les informations vers un fichier `.tsv` (séparé par des tabulations) (en vue de l’utiliser, par exemple, dans une feuille de calcul Excel).

      * **Courrier**

         * **De**

           Saisissez l’adresse électronique d’où doit provenir le courrier électronique.

         * **Envoyer à**

           Entrez une ou plusieurs adresses électroniques auxquelles le formulaire est envoyé.

         * **CC**

           Saisissez une ou plusieurs adresses électroniques en copie carbone invisible.

         * **CCI**

           Saisissez une ou plusieurs adresses email en Cci.

         * **Objet**

           Saisissez l’objet du courrier électronique.

      * **Réinitialiser le mot de passe**

         * **Page Changer le mot de passe**

           Page utilisée lors de la modification du mot de passe.

      * **Stocker le contenu**

         * **Chemin d’accès au contenu**

           Chemin d’accès à tout type de contenu utilisé par le formulaire. Saisissez un chemin qui se termine par une barre oblique `/`. La barre oblique signifie que, pour chaque port de formulaire, un nouveau nœud est créé à l’emplacement indiqué, par exemple :
           `/forms/feedback/`

         * **Afficher des données...**

           Cliquez sur ce bouton pour accéder aux informations relatives aux résultats de formulaire dans l’éditeur en bloc. À partir de là, vous pouvez exporter les informations vers un fichier .tsv (séparé par des tabulations) (à utiliser dans une feuille de calcul Excel, par exemple).

      * **Stocker le contenu avec les chargements**

        Dispose des mêmes options que **Stocker le contenu**.

      * **Désabonner l’abonné**

         * **La piste est supprimée de cette liste.**

           Spécifiez la liste de prospects requise.

#### Fin de formulaire {#end-of-form}

Marque la fin du formulaire. Vous pouvez configurer les éléments suivants :

* **Fin de formulaire**

   * **Afficher le bouton Envoyer**

     Indique si un bouton Envoyer doit être affiché ou non.

   * **Envoyer le nom**

     Identifiant si vous utilisez plusieurs boutons d’envoi dans un formulaire.

   * **Envoyer le titre**

     Nom qui s’affiche sur le bouton, tel que Envoyer ou Envoyer.

   * **Afficher le bouton Réinitialiser**

     Si vous cochez cette case, le bouton Réinitialiser est visible.

   * **Réinitialiser le titre**

     Nom qui s’affiche sur le bouton Réinitialiser .

   * **Description**

     Informations qui s’affichent sous le bouton.

### Nom de compte {#account-name}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de texte de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) au lieu de .

Permet à l’utilisateur de saisir un nom de compte :

![dc_form_accountname](assets/dc_form_accountname.png)

### Adresse {#address}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de texte de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) au lieu de .

Permet d&#39;ajouter un champ d&#39;adresse internationale au format suivant :

![dc_form_addressfield](assets/dc_form_addressfield.png)

Le composant est configuré pour une utilisation immédiate, mais vous pouvez modifier la configuration, si nécessaire. Par exemple, des contraintes peuvent être ajoutées pour les éléments individuels de l’adresse. Le fait de laisser les champs vides signifie que les paramètres par défaut sont utilisés.

### Captcha {#captcha}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

Le composant Captcha requiert que l’utilisateur saisisse une chaîne alphanumérique comme affichée à l’écran. La chaîne change à chaque actualisation.

![dc_form_captcha](assets/dc_form_captcha.png)

Vous pouvez configurer différents paramètres pour ce composant, notamment un message à afficher lorsque la chaîne captcha n’est pas valide.

### Groupe de cases à cocher {#checkbox-group}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal des options de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) au lieu de .

Une case à cocher vous permet de créer une liste composée d’une ou de plusieurs cases à cocher (plusieurs d’entre elles peuvent être simultanément cochées).

![dc_form_checkboxgroupuse](assets/dc_form_checkboxgroupuse.png)

Vous pouvez spécifier différents paramètres, notamment un titre, une description et un nom d’élément. Les boutons + et - vous permettent d’ajouter ou de supprimer des éléments, puis de les positionner à l’aide des flèches haut et bas.

>[!NOTE]
>
>Utilisation **Chemin de chargement des éléments** vous pouvez précharger la liste de groupes de cases à cocher avec des valeurs.
>
>Consultez [Préchargement des champs de formulaire avec de multiples valeurs](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Informations de la carte de crédit {#credit-card-details}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Vous permet de fournir les champs nécessaires pour saisir les détails de la carte de crédit. Vous pouvez le configurer pour spécifier les types de carte acceptés et les informations requises (par exemple, le code de sécurité).

![chlimage_1-100](assets/chlimage_1-100.png)

### Liste déroulante {#dropdown-list}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal des options de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) au lieu de .

Une liste déroulante peut être configurée pour être utilisée avec différentes valeurs pouvant être sélectionnées :

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

Vous pouvez spécifier un titre et les éléments à afficher dans la liste. Les boutons + et - vous permettent d’ajouter ou de supprimer des éléments de liste, puis de les positionner à l’aide des boutons Haut et Bas. Vous pouvez indiquer si les utilisateurs sont autorisés à sélectionner plusieurs éléments de la liste, ainsi que tout élément qui doit être automatiquement sélectionné la première fois qu’ils ouvrent la liste (valeurs initiales).

>[!NOTE]
>
>Utilisation **Chemin de chargement des éléments** vous pouvez précharger la liste déroulante avec des valeurs.
>
>Consultez [Préchargement des champs de formulaire avec de multiples valeurs](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Chargement du fichier {#file-upload}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Le composant Chargement du fichier fournit à l’utilisateur un moyen pour sélectionner un fichier et le charger.

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
>
>Vous pouvez créer un composant de chargement personnalisé pour charger des fichiers vers un servlet Sling. Pour plus d’informations, voir [Chargement de fichiers dans Adobe Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-cloud-service-create-asset-servlet-for-uploading-small-files/td-p/404276).

### Champ masqué {#hidden-field}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal Masqué du formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-hidden.html) au lieu de .

Permet de créer un champ masqué. Ces champs masqués peuvent être utilisés à diverses fins. Par exemple, lorsque vous devez effectuer une action après l’envoi du formulaire ou lorsque des données masquées sont requises dans le post-traitement.

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
>
>Vous pouvez également personnaliser votre formulaire pour afficher ou masquer des composants de formulaire spécifiques en fonction de la valeur d’autres champs du formulaire. La modification de la visibilité d’un champ de formulaire est utile lorsque le champ n’est nécessaire que dans des conditions spécifiques.
>
>Voir [Affichage et masquage des composants de formulaire](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components).

### Bouton Image {#image-button}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de bouton de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) au lieu de .

Un bouton d’image permet de créer un bouton comportant vos texte et image :

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### Téléchargement de l’image {#image-upload}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Le composant Chargement de l’image fournit à l’utilisateur un moyen pour sélectionner un fichier image et le charger.

![dc_form_imageupload](assets/dc_form_imageupload.png)

### Champ du lien {#link-field}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Le champ Lien permet à l’utilisateur de spécifier une URL.

![dc_form_link](assets/dc_form_link.png)

Le plus souvent utilisé pour le formulaire d’événement de calendrier, où il est utilisé pour le champ URL/lien d’un événement.

### Champ Mot de passe {#password-field}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Permet à l’utilisateur de saisir son mot de passe :

![dc_form_password](assets/dc_form_password.png)

### Réinitialisation du mot de passe {#password-reset}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Ce composant fournit deux champs à votre utilisateur pour :

* saisie d’un mot de passe
* saisie répétée du mot de passe pour vérifier que la saisie est correcte.

Avec les paramètres par défaut, le composant apparaît comme suit :

![dc_password_reset](assets/dc_password_reset.png)

### Groupe de cases d’option {#radio-group}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal des options de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) au lieu de .

Un groupe de cases d’option fournit une liste composée d’une ou de plusieurs cases d’option (une seule case peut être sélectionnée à un moment donné).

Vous pouvez spécifier le nom de l’élément ainsi qu’un titre et une description. Les boutons + et - vous permettent d’ajouter ou de supprimer des éléments, de les positionner à l’aide des flèches haut et bas, puis de spécifier une valeur par défaut, le cas échéant :

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
>
>L’option **Chemin de chargement des éléments** permet de précharger des valeurs dans les cases d’option.
>
>Consultez [Préchargement des champs de formulaire avec de multiples valeurs](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Bouton Envoyer {#submit-button}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de bouton de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) au lieu de .

Ce composant vous permet de créer un bouton Envoyer avec le texte par défaut :

![dc_form_submitbutton](assets/dc_form_submitbutton.png)

Ou votre propre texte :

![dc_form_submitbuttonuse](assets/dc_form_submitbuttonuse.png)

### Champ des balises {#tags-field}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) au lieu de .

Ce champ vous permet de sélectionner des balises :

![dc_form_tags_use](assets/dc_form_tags_use.png)

Vous pouvez spécifier différents paramètres, notamment les espaces de noms, à l’aide de l’onglet spécialisé :

* **Champ de balise**

   * **Espaces de noms autorisés**

      * **Geometrixx Outdoors**
      * **Workflow**
      * **Forum**
      * **Images de photothèque**
      * **Geometrixx Media**
      * **Balises standard**
      * **Marketing**
      * **Propriétés de l’élément**
      * **Largeur en pixels**
      * **Taille de la fenêtre contextuelle**

### Champ de texte {#text-field}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de texte de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) au lieu de .

Le champ de texte standard peut être configuré selon la taille requise et avec votre propre piste dans le message :

![dc_form_text](assets/dc_form_text.png)

### Bouton d’envoi du workflow {#workflow-submit-button-s}

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant principal de bouton de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) au lieu de .

Permet de créer un bouton Envoyer à utiliser dans un workflow.

![chlimage_1-101](assets/chlimage_1-101.png)
