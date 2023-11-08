---
title: Configuration des paramètres de type de fichier
seo-title: Configuring file type settings
description: Découvrez comment configurer les paramètres de type de fichier.
seo-description: Learn how to configure file type settings.
uuid: 58a05500-ffbb-4fa2-8ae1-8ac80ab2d099
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89f4d3cf-eb2e-4d55-8209-16ecbba03792
source-git-commit: e2a3470784beb04c2179958ac6cb98861acfaa71
workflow-type: tm+mt
source-wordcount: '6167'
ht-degree: 53%

---


# Configuration des paramètres de type de fichier {#configuring-file-type-settings}

Dans PDF Generator, vous pouvez configurer les paramètres de l’application pour les types de fichiers pris en charge. Sous Windows, vous pouvez configurer les paramètres de l’application pour chaque type de fichier pris en charge. Sous UNIX et Linux, vous pouvez configurer les paramètres de l’application pour HTML-to-PDF et OpenOffice.

Sur la page Paramètres de type de fichier , vous pouvez effectuer les tâches suivantes :

* [Création ou modification d’un paramètre de type de fichier](#create-or-edit-file-type-settings)
* Spécifiez les paramètres de type de fichier à utiliser par défaut (voir [Importation et exportation de fichiers de configuration PDF Generator](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr))
* [Modification des paramètres par défaut](/help/forms/using/admin-help/configuring-file-type-settings1.md#change-the-default-settings)
* [Activer la prise en charge de PDF/A](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)
* [Supprimer un paramètre de type de fichier](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)

>[!NOTE]
>
>Les paramètres de type de fichier ne sont pas disponibles pour les convertisseurs de secours tels que Acrobat pour la conversion de HTML en PDF, Microsoft PowerPoint, Microsoft Word et Microsoft Excel.

## Création ou modification de paramètres de type de fichier {#create-or-edit-file-type-settings}

Créez ou modifiez un paramètre de type de fichier pour spécifier comment l’application gère la conversion des types de fichiers pris en charge. Sous Windows, vous pouvez configurer les paramètres de l’application pour chaque type de fichier pris en charge. Sous UNIX et Linux, vous pouvez configurer les paramètres de l’application pour HTML-to-PDF et OpenOffice.

1. Dans Administration Console, cliquez sur **[!UICONTROL Services]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL Paramètres de type de fichier]**.
1. Cliquez sur Nouveau ou sur le nom d’un paramètre.
1. Dans la zone Extensions de nom de fichier, saisissez les extensions de nom de fichier, séparées par des virgules, pour les types de fichiers acceptés pour cette application. N’insérez pas de point avant ou d’espace entre les extensions. La valeur par défaut est de `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Facultatif) Pour utiliser la reconnaissance de code optique de texte dans des graphiques ou des images, sélectionnez Utiliser la reconnaissance optique des caractères et définissez les options suivantes :

**Langue principale de reconnaissance optique des caractères :** définit la langue à utiliser par le moteur de reconnaissance optique des caractères pour identifier les caractères. La valeur par défaut est Anglais (US).

**Style de sortie PDF :** sélectionnez Image indexable pour afficher une image bitmap des pages au premier plan et le texte numérisé sur une couche invisible sous-jacente. L’aspect de la page ne change pas, mais le texte devient sélectionnable et lisible. Sélectionnez Texte formaté et images pour reconstruire la page d’origine à l’aide de texte, polices, images et autres éléments graphiques reconnus. La valeur par défaut est Image indexable (exacte).

**Sous-échantillonner les images :** Réduit le nombre de pixels dans les images monochromes, en niveaux de gris et en couleur. Le sous-échantillonnage des images numérisées est effectué une fois la reconnaissance optique des caractères terminée. La valeur par défaut est la plus basse (600 dpi). Cette option n’est pas disponible si vous définissez le style de sortie du PDF sur Image indexable (Exact).

1. Renseignez les informations requises dans les sections suivantes :

   [Importation et exportation des fichiers de configuration de PDF Generator](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)

[Paramètres d’exportation Adobe PDF (Windows uniquement)](#adobe-pdf-export-settings-windows-only)

[Paramètres de conversion du HTML en PDF](#html-to-pdf-settings)

[Paramètres de conversion des vidéos Flash en PDF](#flash-videos-to-pdf-settings)

[Paramètres de conversion du format XPS en PDF](#xps-to-pdf-settings)

[Paramètres d’optimisation de PDF](#pdf-optimizer-settings)

[Paramètres de Microsoft Excel (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-excel-settings-windows-only)

[Paramètres de Microsoft PowerPoint (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-powerpoint-settings-windows-only)

[Paramètres de Microsoft Project (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-project-settings-windows-only)

[Paramètres de Microsoft Word (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-word-settings-windows-only)

[Paramètres de Microsoft Visio (Windows uniquement)](#visio)

[Paramètres de Microsoft Publisher (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-publisher-settings-windows-only)

[Paramètres d’AutoCAD (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#autocad-settings-windows-only)

[Paramètres d’OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings1.md#openoffice-settings)

[Paramètres d’autres applications (Windows uniquement)](#other-applications-settings-windows-only)

   Pour accéder à une autre section, cliquez sur son lien sur la page web ou utilisez les boutons [!UICONTROL Suivant] ou **[!UICONTROL Précédent]**.

1. Après avoir renseigné toutes les sections, cliquez sur **[!UICONTROL Enregistrer]** ou **[!UICONTROL Enregistrer sous]** puis saisissez le nom du paramètre.

Il est possible de personnaliser la prise en charge de divers types de fichier (voir « [Ajout de formats de fichier natifs pris en charge](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html) » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_lc_programming_11_fr)).

## Modifier les paramètres par défaut {#change-the-default-settings}

Vous pouvez modifier la valeur par défaut des paramètres Adobe PDF, des paramètres de sécurité et des paramètres de type de fichier qui s’appliquent aux sources nouvellement créées. La modification des valeurs par défaut n’a aucune incidence sur les paramètres des sources existantes.

1. Dans Administration Console, cliquez sur **[!UICONTROL Services > PDF Generator]**.
1. Sur le **[!UICONTROL Paramètres Adobe PDF]**, **[!UICONTROL Paramètres de type de fichier]**, ou **[!UICONTROL Paramètres de protection]** page, cliquez sur **[!UICONTROL Définition des paramètres par défaut]**.
1. Sélectionnez les paramètres par défaut de votre choix. Un ou plusieurs des paramètres suivants sont disponibles sur la page Définir les paramètres par défaut :

   **[!UICONTROL Paramètres Adobe PDF]** : la valeur par défaut dʼorigine est Standard (Acrobat 6).

   **[!UICONTROL Paramètres de sécurité]** : la valeur par défaut originale est Aucune protection (Acrobat 5).

   **[!UICONTROL Paramètres de type de fichier]** : la valeur par défaut dʼorigine est Standard.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Supprimer un paramètre de type de fichier {#delete-a-file-type-setting}

Vous pouvez supprimer un paramètre de type de fichier qui n’est plus utilisé.

1. Dans Administration Console, cliquez sur **[!UICONTROL Services > PDF Generator > Paramètres de type de fichier]**.
1. Cochez la case en regard du paramètre à supprimer. Vous pouvez sélectionner plusieurs sources. Les paramètres qui ne comportent pas de case à cocher sont toujours inclus dans PDF Generator et ne peuvent pas être supprimés.
1. Cliquez sur **[!UICONTROL Supprimer]** puis, sur la page Confirmation de suppression, cliquez sur **[!UICONTROL Supprimer]**.

## Paramètres d’image vers PDF {#image-to-pdf-settings}

Les options suivantes déterminent le mode de conversion des fichiers image en PDF. Pour plus d’informations sur l’accès à ces paramètres, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensions de nom de fichier :** liste des extensions de fichier, séparées par des virgules, pouvant être converties.

**Essayer le convertisseur de secours :** PDF Generator peut convertir les fichiers image en PDF avec Java™ ou Acrobat. Lorsque cette option est sélectionnée et qu’une conversion échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion à l’aide de la méthode alternative. Si une autre méthode échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

>[!NOTE]
>
>Les fichiers JPEG 2000 ne peuvent être convertis qu’avec Acrobat.

**Utiliser la reconnaissance optique des caractères :** définit si l’OCR (reconnaissance optique de caractères) doit être appliquée au fichier PDF. Un logiciel d’OCR vous permet de rechercher, corriger et copier du texte dans un fichier PDF.

***Remarque ** : la fonction OCR pour les fichiers PDF (PDF indexables) est uniquement prise en charge sous Microsoft Windows.*

**Langue principale de reconnaissance optique des caractères :** définit la langue à utiliser par le moteur de reconnaissance optique des caractères pour identifier les caractères.

**Style de sortie PDF :** détermine le type de fichier PDF à créer. Tous les formats appliquent la reconnaissance optique de caractères, ainsi que la reconnaissance de polices et de pages, aux images textuelles et les convertissent en texte normal.

**Image indexable :** vérifie que le texte est indexable et sélectionnable. Cette option conserve l’image d’origine, la dessine selon les besoins et place un calque de texte invisible dessus. L’option Sous-échantillonner les images détermine si l’image est sous-échantillonnée et dans quelle mesure.

**Image indexable (exacte) :** vérifie que le texte est indexable et sélectionnable. Cette option conserve l’image d’origine et place un calque de texte invisible dessus. Recommandé pour les cas qui nécessitent une fidélité maximale à l’image d’origine.

**ClearScan :** synthétise une nouvelle police Type 3 pratiquement identique à l’originale et conserve l’arrière-plan de la page en reprenant une copie basse résolution.

**Sous-échantillonner les images :** permet de réduire le nombre de pixels dans les images monochromes, en niveaux de gris et en couleur, une fois la reconnaissance optique de caractères terminée. Sélectionnez le degré de sous-échantillonnage à appliquer. Les options à plus grand nombre diminuent le sous-échantillonnage, ce qui produit des PDF à plus haute résolution.

## Paramètres d’exportation Adobe PDF (Windows uniquement) {#adobe-pdf-export-settings-windows-only}

Le paramètre Exporter le type de fichier de la section Paramètres d’exportation d’Adobe PDF est utilisé pour convertir un fichier de PDF dans un autre format. Le format par défaut est HTML 4.01 avec des feuilles de style en cascade (CSS) 1.0(&amp;ast;.htm, &amp;ast;.html).

Pour plus d’informations sur l’accès à ce paramètre, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Paramètres de conversion du HTML en PDF {#html-to-pdf-settings}

Les options suivantes déterminent la manière dont les fichiers de HTML sont convertis en PDF. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Essayer le convertisseur de secours :** PDF Generator peut convertir les fichiers HTML en PDF avec Java™ ou Acrobat. Lorsque cette option est sélectionnée et qu’une conversion échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion à l’aide de la méthode alternative. Si une autre méthode échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**Codage par défaut :** définit le codage d’entrée du texte du fichier à partir d’un menu de systèmes d’exploitation et d’alphabets. Utilise la sélection de l’option Codage par défaut uniquement si le fichier HTML source ne spécifie aucun type de codage.

**Forcer le codage sélectionné :** ignore tout codage spécifié dans le fichier HTML source et utilise la sélection indiquée par l’option Codage par défaut.

### Paramètres d’indexation {#spidering-settings}

*Spidering* analyse les pages web à la recherche de liens vers d’autres pages web. Lorsqu’un lien vers une autre page web est rencontré, la page de destination est récupérée et incluse dans le document du PDF généré. Activez ces options pour définir le nombre de niveaux à extraire et à convertir en PDF :

**Télécharger uniquement x niveaux :** permet d’indexer et de convertir des pages jusqu’à la profondeur de niveau défini depuis l’URL de la page de base. Une valeur égale à 1 permet de convertir uniquement l’URL indiquée.

**Télécharger le site entièrement :** permet de convertir l’ensemble du site en partant de l’URL fournie.

**Utiliser un seul chemin :** tous les liens renvoyant à des pages, qui ne se trouvent pas sur le même chemin d’accès relatif que celui de l’URL de base ne sont pas convertis pendant l’indexation.

**Utiliser un seul serveur :** les liens renvoyant à des pages, qui se trouvent sur des serveurs différents, ne sont pas convertis lors de l’indexation. Seuls les liens pointant vers le même serveur que l’URL spécifiée sont convertis.

### Paramètres de conversion de page {#page-conversion-settings}

Activez ces options pour spécifier le mode de conversion des pages de HTML. En fonction de la taille de la page, les valeurs de largeur, de hauteur et de marge s’ajustent en conséquence.

**Format de page :** sélectionnez Personnalisé et indiquez la largeur et la hauteur, ou sélectionnez un format prédéfini.

**Orientation :** sélectionnez le format portrait ou paysage pour le document PDF converti.

**Marges :** permet de définir les marges (Haut, Bas, Gauche, Droite) du document PDF généré.

**Ajouter des signets au PDF :** permet d’ajouter des signets au document PDF.

**Activer le balisage de PDF :** permet d’incorporer des balises dans le document PDF.

**Définir les paramètres d’affichage initiaux :** permet de configurer les paramètres Options du document, Options de fenêtre et Options de l’interface utilisateur. Ces paramètres déterminent le mode d’affichage initial du contenu.

### Options du document {#document-options}

Activez ces options pour indiquer comment afficher le contenu, afficher les pages dans le document du PDF et spécifier le niveau d’agrandissement :

**Afficher :** permet de sélectionner les panneaux à ouvrir dans Acrobat lorsque le document PDF est ouvert.

**Mise en page :** permet de sélectionner le type de mise en page du document PDF.

**Zoom :** permet de choisir un zoom prédéfini de l’affichage initial du document PDF ou de sélectionner une valeur personnalisée. Le choix d’un paramètre par défaut indique que l’agrandissement Acrobat par défaut est utilisé.

**Ouvrir à la page :** permet d’indiquer le numéro de page auquel le PDF doit s’ouvrir.

### Options de fenêtre {#window-options}

Activez ces options pour définir la taille et l’affichage de la fenêtre.

**Redimensionner la fenêtre par rapport à la page initiale :** permet de redimensionner la fenêtre Acrobat au format de la page initiale.

**Centrer la fenêtre sur l’écran :** permet de positionner la fenêtre au centre de l’écran.

**Ouvrir en mode Plein écran :** permet d’ouvrir la fenêtre en mode plein écran.

**Afficher :** permet d’afficher le titre du document ou le nom de fichier dans la fenêtre.

### Options de l’interface utilisateur {#user-interface-options}

Activez ces options pour définir l’aspect de la fenêtre :

**Masquer la barre de menus :** permet de masquer la barre de menus dans le document PDF.

**Masquer les barres d’outils :** permet de masquer les barres d’outils dans le document PDF.

**Masquer les commandes d’affichage :** permet de masquer les commandes d’affichage dans le document PDF.

## Paramètres de conversion des vidéos Flash en PDF {#flash-videos-to-pdf-settings}

PDF Generator prend en charge la possibilité d’envoyer une vidéo pour un Flash d’Adobe (fichier SWF ou FLV) et de créer un fichier de PDF avec une vidéo pour un Flash d’Adobe incorporé. Cette conversion ne nécessite pas l’installation du Flash Player d’Adobe sur le serveur Forms. Pour plus d’informations sur l’accès à cette option, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensions de nom de fichier :** liste des extensions de fichier, séparées par des virgules, pouvant être converties.

## Paramètres de conversion du format XPS en PDF {#xps-to-pdf-settings}

XML Paper Specification (XPS) est utilisé dans l’imprimante Windows. Il s’agit d’un format Microsoft qui peut être créé à partir de n’importe quelle application Microsoft Office. AEM forms permet de convertir des fichiers XPS en PDF.

**Extensions de nom de fichier :** liste séparée par des virgules de toutes les extensions de nom des fichiers XPS pouvant être convertis. Il n’existe actuellement un seul format : .xps.

## Paramètres d’optimisation de PDF {#pdf-optimizer-settings}

PDF Generator prend en charge la possibilité de réduire la taille des fichiers du PDF. Le fait d’utiliser tous ces paramètres ou seulement quelques-uns dépend de la manière dont vous envisagez d’utiliser les fichiers et des propriétés essentielles qu’un fichier doit posséder. Dans la plupart des cas, les paramètres par défaut sont adaptés pour une efficacité maximale : économiser de l’espace en supprimant les polices incorporées, en compressant les images et en supprimant les éléments des fichiers qui ne sont plus nécessaires.

>[!NOTE]
>
>L’optimisation d’un document signé numériquement supprime et invalide les signatures numériques.

Pour plus d’informations sur l’accès à ce paramètre, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Version PDF cible :** définit la version d’Acrobat avec laquelle le PDF est compatible.

### Polices {#fonts}

1. Sélectionner **Polices.**
1. Sélectionnez l’une des options suivantes :

   **Désincorporer toutes les polices :** désincorpore toutes les polices incorporées.

   **Ne désincorporer aucune police :** ne désincorpore aucune police.

   **Désincorporer certaines polices :** désincorpore seulement les polices spécifiées. Pour spécifier les polices à désincorporer, procédez comme suit :

   * Si nécessaire, sélectionnez un autre répertoire de polices dans le **Source de la police** menu déroulant. Ce menu déroulant répertorie les répertoires de polices spécifiés dans **Accueil > Paramètres > Core System > Configurations de base**.
   * Sélectionnez une ou plusieurs polices dans le **Polices disponibles** répertorier et cliquer **Ajouter**. Ces polices sont ajoutées au **Polices à désincorporer** liste.
   * Si vous souhaitez désincorporer des polices qui n’existent pas sur le serveur Forms, saisissez les noms de ces polices dans la variable **Ajout de polices à désincorporer** de la boîte. Cliquez sur **Ajouter**.

   >[!NOTE]
   >
   >*Pour désincorporer des polices dont les jeux partiels sont incorporés dans le document, ajoutez un signe + avant le nom de la police. Par exemple : « +Helvetica ».*

1. Pour incorporer uniquement les jeux partiels utilisés des polices incorporées, sélectionnez **Créer des jeux partiels de toutes les polices incorporées**.

   >[!NOTE]
   >
   >*Si vous utilisez cette option en combinaison avec **Désincorporer certaines polices**, polices dans la variable **A**les polices ajoutées à la liste désincorporée sont toujours complètement désincorporées.*

   >[!NOTE]
   >
   >*La création de jeux partiels de polices permet d’incorporer uniquement une portion d’une police. Un jeu partiel de police ne contient que les caractères utilisés dans votre document.*

### Transparence {#transparency}

Si votre document de PDF comprend des illustrations qui contiennent de la transparence, vous pouvez utiliser les paramètres de PDF Optimizer pour aplatir la transparence et réduire la taille de fichier.

>[!NOTE]
>
>Si Acrobat 4.0 et versions ultérieures sont sélectionnées en tant que version du PDF Target, tous les objets transparents sont aplatis. Pour les autres versions de Target PDF, la transparence est prise en charge et vous pouvez configurer les paramètres de transparence.

Sélectionner **Transparence** pour configurer les paramètres de transparence lors de l’optimisation des documents du PDF.

**Niveau de transparence :** spécifie la quantité d’informations vectorielles qui seront conservées. Des paramètres plus élevés préservent plus d’objets vectoriels, tandis que des paramètres plus bas pixellisent plus d’objets vectoriels ; des paramètres intermédiaires préservent des zones simples sous forme vectorielle et pixellisent les zones complexes. Sélectionnez le paramètre le plus bas pour pixelliser toutes les illustrations.

>[!NOTE]
>
>La quantité de pixellisation qui se produit dépend de la complexité de la page et des types d’objets se chevauchant.

**Dessins au trait et texte** : résolution de pixellisation de tous les objets : images, illustrations vectorielles, texte et dégradés. Les valeurs prises en charge sont comprises entre 1 pixel par pouce (ppp) et 9 600 ppp.

>[!NOTE]
>
>La résolution des dessins au trait et du texte doit généralement être définie entre 600 et 1 200 ppp pour fournir une pixellisation de haute qualité, en particulier sur le type serif ou de petite taille de point.

**Dégradés et filets** : résolution de pixellisation des dégradés et filets. Cette valeur doit être comprise entre 1 et 1200 ppp.

>[!NOTE]
>
>Définissez de préférence la résolution des dégradés et des filets entre 150 et 300 ppp, étant donné qu’une résolution plus élevée augmente le temps d’impression et la taille des fichiers sans toutefois améliorer la qualité des dégradés, des ombres portées et des contours progressifs.

**Vectoriser tout le texte** : convertit tous les objets de type (type de point, type de zone et type de chemin) en contours et supprime l’ensemble des informations de glyphe sur les types dans les pages contenant de la transparence. Cette option garantit la cohérence de la largeur du texte lors de l’aplatissement. Notez que si vous activez cette option, les petites polices apparaissent légèrement plus épaisses lorsqu’elles sont affichées dans Acrobat ou imprimées sur des imprimantes de bureau à faible résolution. Cela n’a aucune incidence sur la qualité du type imprimé sur les imprimantes à haute résolution ou les imageurs d’images.

**Vectoriser tous les contours** : convertit tous les contours en tracés simples remplis dans les pages contenant de la transparence. Cette option garantit la largeur des contours pendant l’aplatissement. Notez que l’activation de cette option a pour effet de donner aux contours fins un aspect légèrement plus épais et peut dégrader les performances d’aplatissement.

**Ecrêter les zones complexes** : garantit que les limites entre l’illustration vectorielle et l’illustration pixellisée s’inscrivent sur les tracés d’objet. Cette option réduit les artefacts de raccordement qui subviennent lorsqu’un objet est partiellement pixellisé (une partie de l’objet restant vectorielle).

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Certains pilotes d’impression traitent les dessins pixellisés et vectoriels différemment, ce qui entraîne parfois un assemblage de couleurs. Vous pouvez minimiser les problèmes de combinaison en désactivant certains paramètres de gestion des couleurs spécifiques au pilote d’impression. Ces paramètres varient selon chaque imprimante. Pour plus d’informations, reportez-vous à la documentation fournie avec cette dernière.

Conserver la surimpression : fusionne la couleur des illustrations transparentes et la couleur d’arrière-plan afin de créer un effet de surimpression.

Le tableau suivant présente les types d’imprimantes courants ainsi que leur résolution mesurée en ppp, leur trame par défaut mesurée en lignes par pouce (lpi) et une résolution de rééchantillonnage des images mesurées en pixels par pouce (ppp). Par exemple, si vous imprimez sur une imprimante laser de 600 dpi, vous devez saisir 170 pour la résolution à laquelle les images doivent être rééchantillonnées.

**Images** Sélectionnez Images pour définir les options de compression et de rééchantillonnage des images en couleurs, niveaux de gris et monochrome. Vous pouvez souhaiter tester ces options pour trouver le bon équilibre entre la taille du fichier et la qualité d’image. Le paramètre de résolution relatif à la couleur et aux niveaux de gris doit être 1,5 à 2 fois le lignage de trame auquel le fichier doit être imprimé. La résolution des images monochromes doit être identique à celle du périphérique de sortie, mais l’enregistrement d’une image monochrome à une résolution supérieure à 1 500 dpi augmente la taille du fichier sans améliorer notablement la qualité de l’image. Les images qui seront agrandies, telles que les cartes, peuvent nécessiter des résolutions plus élevées.

>[!NOTE]
>
>Le rééchantillonnage d’images monochromes peut avoir des résultats inattendus, comme l’affichage d’aucune image. Dans ce cas, désactivez le rééchantillonnage et convertissez à nouveau le fichier. Ce problème est plus susceptible de survenir avec le sous-échantillonnage, et moins avec le sous-échantillonnage bicubique.

<table>
 <tbody>
  <tr>
   <th><p><strong>Résolution de l’imprimante</strong></p> </th>
   <th><p><strong>Écran de ligne par défaut</strong></p> </th>
   <th><p><strong>Résolution de l’image</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi (imprimante laser)</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppp</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi (imprimante laser)</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppp</p> </td>
  </tr>
  <tr>
   <td><p>1 200 dpi (imageuse d’images)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppp</p> </td>
  </tr>
  <tr>
   <td><p>2 400 dpi (imageuse d’images)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppp</p> </td>
  </tr>
 </tbody>
</table>

#### Ignorer les objets {#discard-objects}

* Sélectionner **Ignorer les objets** pour spécifier les objets à supprimer du PDF et optimiser les lignes incurvées dans les dessins CAO.
* **Ignorer les actions d’envoi, d’importation et de réinitialisation de formulaire** : désactive toutes les actions concernant la soumission ou l’importation de données de formulaire, et la réinitialisation de champs de formulaire. Cette option conserve les objets de formulaire auxquels des actions sont liées.
* **Ignorer tous les scripts JavaScript** : supprime du fichier toutes les actions qui utilisent JavaScript.
* **Ignorer les miniatures de page incorporées**: supprime les miniatures de page incorporées. Cette option est utile pour les documents volumineux, qui peuvent prendre un certain temps pour dessiner les miniatures de page une fois que vous avez cliqué sur le bouton Pages .
* **Convertir les traits lissés en courbes**: réduit le nombre de points de contrôle utilisés pour créer des courbes dans des dessins CAO, ce qui se traduit par des fichiers PDF plus petits et un rendu plus rapide à l’écran.
* **Ignorer les paramètres d’impression incorporés** : supprime les paramètres d’impression incorporés, comme la mise à l’échelle de la page et le mode recto/verso.
* **Ignorer les signets**: supprime tous les signets du document.
* **Aplatissement des champs de formulaire**: rend les champs de formulaire inutilisables sans modification de leur apparence. Les données de formulaire sont fusionnées avec la page pour devenir du contenu de page.
* **Ignorer les images de remplacement** : supprime toutes les versions d’une image, sauf la version destinée à être affichée à l’écran. Certains PDF incluent plusieurs versions d’une même image à des fins différentes, telles que l’affichage basse résolution à l’écran et l’impression haute résolution.
* **Ignorer les balises du document** : supprime les balises du document, ainsi que les fonctionnalités d’accessibilité au texte et de redistribution de celui-ci.
* **Détecter et fusionner les fragments d’image** : recherche les images ou les masques qui sont fragmentés en petites parties et tente de les fusionner dans une même image ou un même masque.
* **Ignorer l’index de recherche incorporé** : supprime les index de recherche incorporés, ce qui réduit la taille du fichier.

#### Ignorer les données utilisateur {#discard-user-data}

Sélectionner **Ignorer les données utilisateur** pour supprimer les informations personnelles que vous ne souhaitez pas distribuer ou partager avec d’autres utilisateurs.

* **Ignorer tous les commentaires, les formulaires et les fichiers multimédia** : supprime tous les commentaires, formulaires, champs de formulaire et contenus multimédias du PDF.
* **Ignorer toutes les données d’objet** : supprime tous les objets du PDF.
* **Ignorer les références croisées externes** : supprime les liens vers d’autres documents. Les liens qui pointent vers d’autres emplacements dans le PDF ne sont pas supprimés.
* **Ignorer le contenu du calque masqué et aplatir les calques visibles**: réduit la taille du fichier. Le document optimisé ressemble au PDF d’origine, mais ne contient pas d’informations sur les calques.
* **Ignorer les métadonnées et les informations sur le document** : supprime le contenu du dictionnaire d’informations du document ainsi que tous les flux de métadonnées (Utilisez la commande Enregistrer sous pour restaurer les flux de métadonnées dans une copie du PDF.)
* **Ignorer les pièces jointes** : supprime tous les fichiers en pièce jointe, y compris ceux ajoutés au PDF en tant que commentaires. (PDF Optimizer n’optimise pas les fichiers joints.)
* **Ignorer les données privées des autres applications** : supprime du document PDF les informations utiles uniquement à l’application ayant créé le document. Ce paramètre n’a aucune incidence sur les fonctionnalités du PDF, mais il réduit la taille du fichier.

### Nettoyage {#clean-up}

Sélectionnez **Nettoyage** pour supprimer du document les éléments inutiles.
Ces éléments sont obsolètes ou inutiles pour l’utilisation prévue du document. La suppression de certains éléments peut affecter gravement les fonctionnalités du PDF. Par défaut, seuls les éléments qui n’affectent pas les fonctionnalités sont sélectionnés. Si vous n’êtes pas certain des conséquences de la suppression d’autres options, utilisez les sélections par défaut.

**Compression**

Sélectionnez l’une des options de compression plate suivantes dans le menu déroulant :

* Compresser l’intégralité du fichier
* Compresser la structure du document
* Supprimer la compression
* Ne pas modifier la compression

**Utiliser Flate pour coder les flux non codés** : applique la compression plate à tous les flux non encodés.

**Ignorer les signets non valides** : supprime les signets qui pointent vers des pages supprimées à l’intérieur du document.

**Ignorer les destinations existantes non référencées** : supprime les destinations existantes qui ne sont pas référencées à l’intérieur du document PDF. Cette option ne recherche pas les liens d’autres fichiers ou sites web de PDF.

**Optimiser le fichier PDF pour l’affichage rapide des pages Web** : restructure un document PDF pour un téléchargement page à page à partir des serveurs Web.

**Utiliser Flate dans les flux en codage LZW** : applique la compression Flate à tous les flux de contenu et à toutes les images en codage LZW.

**Ignorer les liens non valides** : supprime les liens vers des destinations incorrectes.

**Optimiser le contenu de la page** : convertit tous les caractères de fin de ligne en espaces, ce qui améliore la compression plate.

## Paramètres de Microsoft Excel (Windows uniquement) {#microsoft-excel-settings-windows-only}

Ces options déterminent la manière dont les fichiers Excel Microsoft sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](#create-or-edit-file-type-settings).

**Essayer OpenOffice comme convertisseur de secours** : lorsque cette option est sélectionnée et qu’une conversion utilisant Microsoft Excel échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion en utilisant OpenOffice. Si la conversion utilisant OpenOffice échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**Extensions de nom de fichier** : permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est de `xls,xlsx`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

**Créer un fichier compatible avec le format PDF/A-1a** : rend obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF.

**Ajouter des signets à Adobe PDF** : permet de convertir des noms de feuille de calcul Excel en signets. Cette option est sélectionnée par défaut.

**Ajuster la feuille de calcul à une page** : permet de réduire la taille du texte afin qu’il s’affiche sur une seule page de feuille de calcul.

**Convertir le classeur entier :** permet de convertir toutes les feuilles de calcul du fichier Excel. Si cette option n’est pas sélectionnée seule la page en cours est convertie.

**Exécuter automatiquement les macros :** exécute les macros du document Excel (par exemple une macro qui insère l’heure actuelle) avant de le convertir.

**Convertir les informations sur le document** : ajoute les propriétés du document PDF à partir des informations du fichier source se rapportant au document. Cela inclut des informations telles que le titre, l’auteur, l’objet et les mots-clés du document.

**Ajouter des liens à Adobe PDF** : permet de convertir les liens hypertexte du fichier source en liens hypertexte dans le document PDF.

**Joindre le fichier source au fichier Adobe PDF** : lorsque cette option est sélectionnée, la feuille de calcul Excel d’origine est insérée en pièce jointe dans le document PDF généré.

**Activer l’accessibilité et la redistribution avec des fichiers Adobe PDF balisés** : permet d’incorporer des balises dans le document PDF pour offrir des fonctionnalités d’accessibilité et de redistribution.

**Liste de compléments Excel à charger** : par défaut (pour des raisons de sécurité), aucun complément Excel n’est exécuté lors de la conversion d’un fichier Excel en PDF. Pour permettre l’exécution de certains compléments Excel au moment de la conversion, fournissez une liste séparée par des virgules indiquant le nom de ces compléments.

**Liste des feuilles de calcul à convertir** : lorsque cette zone est vide, toutes les feuilles de calcul de la feuille de calcul Excel sont incluses dans le PDF généré. Pour convertir de manière sélective un sous-ensemble des feuilles de calcul, fournissez une liste de noms de feuilles séparés par des virgules.

## Paramètres de Microsoft PowerPoint (Windows uniquement) {#microsoft-powerpoint-settings-windows-only}

Ces options déterminent la manière dont les fichiers Microsoft PowerPoint sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Essayer OpenOffice comme convertisseur de secours]**: lorsque cette option est sélectionnée et qu’une conversion utilisant Microsoft PowerPoint échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion à l’aide d’OpenOffice. Si la conversion utilisant OpenOffice échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**[!UICONTROL Extensions de nom de fichier]** : permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est ppt,pptx. N’insérez pas de point devant les extensions ou d’espace entre celles-ci.

**[!UICONTROL Convertir les informations sur le document]** : permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, l’objet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.

**[!UICONTROL Ajouter des signets à Adobe PDF]** : permet de convertir des titres PowerPoint en signets. Cette option est sélectionnée par défaut.

**[!UICONTROL Joindre le fichier source au fichier Adobe PDF]** : permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. Cette option est désélectionnée par défaut.

**[!UICONTROL Activer l’accessibilité et la redistribution avec un fichier Adobe PDF balisé]** : permet d’incorporer les balises dans le fichier PDF. Cette option est désélectionnée par défaut.

**[!UICONTROL Convertir le multimédia en multimédia PDF]** : permet de convertir le multimédia en multimédia PDF, lorsque cela est possible. Cette option est sélectionnée par défaut.

**[!UICONTROL Convertir les notes du présentateur]** : permet de convertir les notes du présentateur en PDF.

**[!UICONTROL Exécuter automatiquement les macros]** : exécute les macros du document PowerPoint (par exemple une macro qui insère l’heure actuelle) avant de le convertir.

**[!UICONTROL Mise en page des PDF basée sur les paramètres de l’imprimante PowerPoint]** : permet d’utiliser les paramètres de l’imprimante PowerPoint pour la mise en page du document PDF.

**[!UICONTROL Ajouter des liens à Adobe PDF]** : permet de conserver tous les liens lors de la conversion du fichier. L’aspect des liens reste généralement inchangé. Les liens ne peuvent être créés que si l’option Activer l’accessibilité est également sélectionnée. Cette option est désélectionnée par défaut.

**[!UICONTROL Enregistrer les transitions entre diapositives dans Adobe PDF]** : permet de convertir les transitions entre diapositives. Cette option est sélectionnée par défaut.

**[!UICONTROL Enregistrer les animations dans Adobe PDF]** : permet d’enregistrer les animations converties dans le fichier PDF.

**[!UICONTROL Convertir les diapositives masquées en pages PDF]** : permet de convertir les diapositives masquées.

**[!UICONTROL Créer un fichier compatible avec le format PDF/A-1a]** : rend obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF. Certaines fonctionnalités de PowerPoint ne sont pas converties lorsque vous créez un fichier de PDF. Si une transition PowerPoint n’a pas de transition équivalente dans Acrobat, une transition similaire est remplacée. Si plusieurs effets d’animation se trouvent dans la même diapositive, un seul effet est utilisé. Les transitions de page et les puces volantes sont converties.

## Paramètres de Microsoft Project (Windows uniquement) {#microsoft-project-settings-windows-only}

Ces options déterminent la manière dont les fichiers de projet Microsoft sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](#create-or-edit-file-type-settings).

1. **[!UICONTROL Extensions de nom de fichier :]** permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est de `mpp`. N’insérez pas de point devant les extensions ou d’espace entre celles-ci.

1. **[!UICONTROL Convertir les informations sur le document]** : permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, l’objet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.
1. **[!UICONTROL Joindre le fichier source au fichier Adobe PDF]** : permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 
1. **[!UICONTROL Créer un fichier compatible avec le format PDF/A-1a]** : rend obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF.
1. **[!UICONTROL Exécuter automatiquement les macros :]** exécute les macros dans le document Microsoft Project (par exemple, une macro qui insère l’heure actuelle) avant de le convertir.

## Paramètres de Microsoft Word (Windows uniquement) {#microsoft-word-settings-windows-only}

Ces options déterminent la manière dont les fichiers Microsoft Word sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](#create-or-edit-file-type-settings).

**[!UICONTROL Essayer OpenOffice comme convertisseur de secours]**: lorsque cette option est sélectionnée et qu’une conversion utilisant Microsoft Word échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion à l’aide d’OpenOffice. Si la conversion utilisant OpenOffice échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**[!UICONTROL Extensions de nom de fichier]** : permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est de `doc,docx,rtf,txt`. N’insérez pas de point devant les extensions ou d’espace entre celles-ci.

**[!UICONTROL Convertir les informations sur le document]** : permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, l’objet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.

**[!UICONTROL Ajouter des signets à Adobe PDF]** : permet de convertir des titres en signets. Cette option est sélectionnée par défaut.

**[!UICONTROL Joindre le fichier source au fichier Adobe PDF]** : permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 

**[!UICONTROL Convertir les références croisées et la table des matières en liens]** : permet de convertir les références croisées et les entrées de la table des matières en liens. Cette option est sélectionnée par défaut.

**[!UICONTROL Activer l’accessibilité et la redistribution avec un fichier Adobe PDF balisé]** : permet d’incorporer les balises dans le fichier PDF. Cette option est sélectionnée par défaut.

**[!UICONTROL Créer un fichier compatible avec le format PDF/A-1a]** : cette option permet de rendre obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF.

**[!UICONTROL Exécuter automatiquement les macros]** : exécute les macros du document Word (par exemple une macro qui insère l’heure actuelle) avant de le convertir.

**[!UICONTROL Conserver les annotations du document au format Adobe PDF]** : permet de convertir les annotations du document Word en annotations dans le fichier PDF.

**[!UICONTROL Ajouter des liens à Adobe PDF]** : permet de convertir les liens hypertexte du fichier source en liens hypertexte dans le document PDF.

**[!UICONTROL Convertir les liens de notes de fin et de bas de page]** : permet de créer des liens à partir des citations de fin et de bas de page en notes dans le document PDF.

**[!UICONTROL Convertir les commentaires affichés en notes dans Adobe PDF]** : permet de convertir les commentaires du document Word en notes de texte dans le document PDF.

**[!UICONTROL Activer le balisage avancé]** : ajoute des balises avancées pour une meilleure accessibilité.

**[!UICONTROL Convertir tous les styles en signets]** : permet de convertir tous les styles du document Word en signets dans le document PDF.

**[!UICONTROL Styles avec niveaux]** : permet de spécifier les styles du document Word à convertir en signets dans le document PDF. Indique également le niveau des signets. Pour utiliser cette fonction, désélectionnez la fonction **[!UICONTROL Convertir tous les styles en signets]** et indiquez les noms des styles au format suivant :

styleName1=level1[,styleName2=level2...]

Si un nom de style Microsoft Word comporte des virgules (,) ou des signes égal (=), ces caractères doivent être précédés par un caractère d’échappement (« \ »). Par exemple, spécifiez un style nommé « Titre, 1 » comme suit : Titre\, 1.

## Paramètres de Microsoft Visio (Windows uniquement) {#visio}

**Convertir les informations sur le document** : permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, l’objet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut. Cette option est activée par défaut.

**Ajouter des liens à Adobe PDF :** permet de conserver tous les liens. Cette option est sélectionnée par défaut.

**Ajouter des signets à Adobe PDF** : permet de convertir des titres en signets. Cette option est sélectionnée par défaut.

**Joindre le fichier source au fichier Adobe PDF** : permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 

**Toujours aplatir les calques dans Adobe PDF** : permet d’aplatir tous les calques Visio.

**Convertir toutes les pages** : permet de convertir toutes les pages du fichier Visio.

**Ouvrir Le Panneau Calques Lorsqu’Il Est Affiché Dans Adobe Acrobat**: si les calques Visio ne sont pas aplatis, une fenêtre s’ouvre dans laquelle vous pouvez spécifier les calques qui sont conservés dans le fichier du PDF lors de leur ouverture à l’aide d’Acrobat. Cette option est sélectionnée par défaut.

**Créer un fichier conforme à la norme PDF/A-1b** : rend obligatoire l’utilisation du paramètre Adobe PDF PDF/A-1b:2005 (RVB).

**Convertir les commentaires en commentaires Adobe PDF** : permet de convertir les notes Visio en commentaires PDF.

## Paramètres de Microsoft Publisher (Windows uniquement) {#microsoft-publisher-settings-windows-only}

Ces options déterminent la manière dont les fichiers de l’éditeur Microsoft sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](#create-or-edit-file-type-settings).

**[!UICONTROL Extensions de nom de fichier]** : permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est de `pub`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

## Paramètres d’AutoCAD (Windows uniquement) {#autocad-settings-windows-only}

Ces options déterminent la manière dont les fichiers AutoCAD sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Extensions de nom de fichier]** : permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est de `dwg`. N’insérez pas de point devant les extensions ou d’espace entre celles-ci.

**[!UICONTROL Convertir les informations sur le document]** : permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, l’objet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.

**[!UICONTROL Ajouter des signets à Adobe PDF]** : permet de convertir des titres en signets. 

**[!UICONTROL Toujours aplatir les calques dans Adobe PDF]**: aplatit tous les calques AutoCAD.

**[!UICONTROL Ouvrir le panneau Calques lors de l’affichage dans Adobe Acrobat]** : permet d’afficher la structure des calques lors de l’ouverture du PDF dans Acrobat.

**[!UICONTROL Créer un fichier compatible avec le format PDF/E-1]** : crée un fichier compatible avec le format PDF/E-1. PDF/E est une norme ISO relative à l’échange de documentation technique et d’ingénierie. Pour plus d’informations sur PDF/E-1, voir [Normes de l’Adobe et du secteur](https://www.adobe.com/enterprise/standards/index.html).

**[!UICONTROL Convertir toutes les mises en page]** : comprend toutes les mises en page du PDF.

**[!UICONTROL Convertir l’espace modèle en 3D]** : lorsqu’elle est sélectionnée, la mise en page de l’espace de modèle est convertie en annotation 3D dans le PDF.

**[!UICONTROL Ajout De Liens À Adobe PDF]**: si cette option est sélectionnée, tous les liens sont conservés.

**[!UICONTROL Joindre le fichier source au fichier Adobe PDF]** : permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 

**[!UICONTROL Créer un fichier conforme à la norme PDF/A-1b]** : rend obligatoire l’utilisation du paramètre Adobe PDF PDF/A-1b.

**[!UICONTROL Convertir tous les calques]** : par défaut, PDF Generator ne convertit que le calque par défaut des fichiers AutoCAD au format PDF et non l’ensemble des calques des fichiers. Sélectionnez cette option pour convertir tous les calques du fichier.

**[!UICONTROL Incorporer les informations d’échelle]**: conserve les informations d’échelle du dessin.

**[!UICONTROL Convertir la mise en page actuelle]** : ne comprend que la mise en page actuelle du PDF.

**[!UICONTROL Liste des mises en page AutoCAD à convertir]** : un dessin AutoCAD peut avoir plusieurs mises en page. Lorsque cette zone est vide, toutes les mises en page du dessin AutoCAD sont incluses dans le document de PDF généré. Pour convertir un sous-ensemble de mises en page de manière sélective, fournissez une liste de noms de mises en page séparés par des virgules.

## Paramètres d’OpenOffice {#openoffice-settings}

Ces options déterminent la manière dont les fichiers OpenOffice sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**Essayer PDFMaker comme convertisseur de secours** : lorsque cette option est sélectionnée et qu’une conversion utilisant OpenOffice échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion en utilisant PDFMaker. Si la conversion utilisant PDFMaker échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**Extensions de nom de fichier** : permet de définir les extensions de nom de fichier acceptées par cette application en les séparant par des virgules. La valeur par défaut est de `odt,odp,ods,odg,odf,sxw,sxi,sxd`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

**Plage**: convertit toutes les pages ou spécifie des pages particulières ou une plage de pages. Si aucune plage de pages n’est définie, toutes les pages sont converties. Pour exporter une plage de pages, utilisez le format 3-6. Pour exporter des pages uniques, utilisez le format 7;9;11. Vous pouvez exporter une combinaison de plages de pages et de pages uniques à l’aide d’un format tel que 3-6;8;10;12.

**Orientation de page** : pour les fichiers en texte brut seulement, sélectionnez le format portrait ou paysage pour le document PDF converti.

**Images** : permet de configurer le mode de conversion des images. Les images EPS avec des aperçus incorporés sont exportées uniquement en tant qu’aperçus. Les images EPS sans aperçus incorporés sont exportées en tant qu’espaces réservés vides. Avec la compression sans perte des images, tous les pixels sont conservés. Avec la compression JPEG des images et un niveau de qualité élevé, la plupart des pixels sont conservés. Avec un niveau de qualité faible, certains pixels sont perdus et des artefacts sont introduits, mais les tailles de fichier sont réduites.

**Général**: activez les options permettant de convertir un PDF balisé ou d’exporter des notes de document Writer et FormCalc, des effets de transition de diapositives Impress ou des pages vierges vers le PDF. Lorsque des balises sont exportées, la taille du fichier peut augmenter de grandes quantités. Certaines balises exportées sont des tables des matières, des liens hypertexte et des contrôles.

Vous pouvez également spécifier le mode d’envoi des formulaires. Les options disponibles sont XML, FDF, PDF ou HTML. Ce paramètre remplace la propriété URL du contrôle que vous définissez dans le document. Un seul paramètre commun peut être sélectionné pour le document du PDF :

* PDF (envoie le document entier)
* FDF (envoie le contenu de la commande)
* HTML
* XML

**PDF balisé** : permet la création de PDF balisés à partir de documents OpenOffice. Le PDF balisé contient des informations sur la structure du contenu du document. Cela peut s’avérer utile lors de l’affichage du document sur des périphériques dotés de différents écrans et lors de l’utilisation d’un logiciel de lecteur d’écran. Il permet également aux logiciels d’accessibilité d’effectuer diverses opérations utiles avec le document du PDF, telles que la lecture à haute voix du contenu du document du PDF.

**Exporter des notes** : permet de convertir les notes de documents OpenOffice en notes de texte dans le document PDF généré.

**Utiliser des effets de transition** : permet de convertir les effets de transition de diapositives dans des présentations OpenOffice en effets de transition PDF correspondants.

**Envoyer des formulaires au format** : permet de créer un formulaire PDF pouvant être rempli et imprimé par l’utilisateur du document PDF.

**Exporter les pages vierges insérées automatiquement** : lorsque cette option est sélectionnée, les pages vierges insérées automatiquement sont incluses dans le document PDF généré. Cela s’avère utile si vous imprimez un document PDF recto verso. Par exemple, un livre peut être configuré de sorte que la première page du chapitre commence toujours sur une page impaire. Si le chapitre précédent se termine sur une page impaire, OpenOffice insère une page paire vierge. Cette option contrôle l’inclusion ou non de cette page paire dans le PDF généré.

## Paramètres d’autres applications (Windows uniquement) {#other-applications-settings-windows-only}

Vous ne pouvez pas modifier les paramètres d’autres applications à l’aide de la console d’administration ; ils affichent les extensions de nom de fichier pour les types de fichiers pris en charge. Pour plus d’informations sur l’accès à ces paramètres, voir [Création ou modification de paramètres de type de fichier](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect : `wpd`
* Adobe PageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Il est possible de personnaliser la prise en charge de ces types de fichier. Pour plus d’informations, voir « Ajouter la prise en charge de formats de fichier natifs supplémentaires » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_62).

Pour obtenir de l’aide sur la configuration d’une imprimante réseau PDFG, voir [Configuration d’une imprimante réseau PDFG (Windows uniquement)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
