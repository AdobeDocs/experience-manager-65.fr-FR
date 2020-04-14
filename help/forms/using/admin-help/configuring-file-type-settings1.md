---
title: Configuration des paramètres de type de fichier
seo-title: Configuration des paramètres de type de fichier
description: Découvrez comment configurer des paramètres de type de fichier.
seo-description: Découvrez comment configurer des paramètres de type de fichier.
uuid: 58a05500-ffbb-4fa2-8ae1-8ac80ab2d099
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89f4d3cf-eb2e-4d55-8209-16ecbba03792
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Configuration des paramètres de type de fichier {#configuring-file-type-settings}

Dans PDF Generator, vous pouvez définir les paramètres de l’application pour les types de fichiers pris en charge. Sous Windows, vous pouvez définir les paramètres de l’application pour chaque type de fichier pris en charge. Sous UNIX et Linux, vous pouvez définir les paramètres de l’application pour les formats HTML en PDF et OpenOffice.

Dans la page Paramètres de type de fichier, vous pouvez effectuer les tâches suivantes :

* [Création ou modification d’un paramètre de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)
* Spécifiez les paramètres de type de fichier à utiliser par défaut (voir [Importation et exportation de fichiers de configuration PDF Generator](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [Modification des paramètres par défaut](/help/forms/using/admin-help/configuring-file-type-settings1.md#change-the-default-settings)
* [Activation de la prise en charge de PDF/A](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [Suppression d’un paramètre de type de fichier](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>les paramètres de type de fichier ne sont pas disponibles pour les convertisseurs de secours, tels que Acrobat pour conversion du format HTML au format PDF, Microsoft PowerPoint, Microsoft Word et Microsoft Excel.

## Création ou modification de paramètres de type de fichier {#create-or-edit-file-type-settings}

Vous créez ou modifiez un paramètre de type de fichier pour définir la manière dont l’application traite la conversion des types de fichier pris en charge. Sous Windows, vous pouvez définir les paramètres de l’application pour chaque type de fichier pris en charge. Sous UNIX et Linux, vous pouvez définir les paramètres de l’application pour les formats HTML en PDF et OpenOffice.

1. Dans Administration Console, cliquez sur **[!UICONTROL Services]** >**[!UICONTROL PDF Generator]** > **[!UICONTROL Paramètres de type de fichier]**.
1. Cliquez sur Créer ou sur le nom d’un paramètre.
1. Dans la zone Extensions de nom de fichier, saisissez les extensions de nom de fichier séparées par des virgules pour les types de fichier pris en charge par cette application. N’insérez pas de point avant les extensions ou d’espace entre celles-ci. La valeur par défaut est `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Facultatif) Pour utiliser la reconnaissance de code optique de texte dans des graphiques ou des images, sélectionnez Utiliser la reconnaissance optique des caractères et définissez les options suivantes :

**Langue principale de l&#39;OCRL :** Langue à utiliser par le moteur de reconnaissance optique des caractères pour identifier les caractères. La valeur par défaut est Anglais (Etats-Unis).

**Style de sortie PDF :** sélectionnez Image indexable pour afficher une image bitmap des pages au premier plan et le texte numérisé sur une couche invisible sous-jacente. L’apparence de la page ne change pas, toutefois il devient possible de sélectionner et de lire le texte. Sélectionnez Texte formaté et images pour reconstruire la page d’origine à l’aide du texte, des polices, des images et des autres éléments graphiques reconnus. La valeur par défaut est Image indexable (exacte).

**Sous-échantillonner les images :** permet de réduire le nombre de pixels dans les images monochromes, en niveaux de gris et en couleur. Le sous-échantillonnage des images numérisées s’effectue après la reconnaissance optique des caractères. La valeur par défaut est la moins élevée (600 dpi). Cette option n’est pas disponible si vous sélectionnez Image indexable (exacte) pour l’option Style de sortie PDF.

1. Fournissez les informations requises dans ces zones :

   [Importation et exportation des fichiers de configuration de PDF Generator](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

   [Paramètres d’exportation Adobe PDF (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-2)

   [Paramètres de conversion du HTML en PDF](#html-to-pdf-settings)

   [Paramètres de conversion des vidéos Flash en PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-9)

   [Paramètres de conversion du format XPS en PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-10)

   [Paramètres d’optimisation de PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-11)

   [Paramètres de Microsoft Excel (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-excel-settings-windows-only)

   [Paramètres de Microsoft PowerPoint (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-powerpoint-settings-windows-only)

   [Paramètres de Microsoft Project (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-project-settings-windows-only)

   [Paramètres de Microsoft Word (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-word-settings-windows-only)

   [Paramètres de Microsoft Visio (Windows uniquement)](#visio)

   [Paramètres de Microsoft Publisher (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-publisher-settings-windows-only)

   [Paramètres d’AutoCAD (Windows uniquement)](/help/forms/using/admin-help/configuring-file-type-settings1.md#autocad-settings-windows-only)

   [Paramètres d’OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings1.md#openoffice-settings)

   [Paramètres d’autres applications (Windows uniquement)](#other-applications-settings-windows-only)

   To go to another section, click its link on the web page or use the **[!UICONTROL Next]**or **[!UICONTROL Previous]** buttons.

1. Après avoir renseigné toutes les sections, cliquez sur **[!UICONTROL Enregistrer]** ou **[!UICONTROL Enregistrer sous]** puis saisissez le nom du paramètre.

Il est possible de personnaliser la prise en charge de divers types de fichier (voir « [Ajout de formats de fichier natifs pris en charge](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html) » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_lc_programming_11)).

## Modification des paramètres par défaut {#change-the-default-settings}

Vous pouvez modifier la valeur par défaut des paramètres Adobe PDF, des paramètres de sécurité et des paramètres de type de fichier qui s’appliquent aux sources nouvellement créées. La modification des valeurs par défaut n’a aucune incidence sur les paramètres des sources existantes.

1. Dans Administration Console, cliquez sur **[!UICONTROL Services > PDF Generator]**.
1. Dans la page **[!UICONTROL Paramètres Adobe PDF]**, **[!UICONTROL Paramètres de type de fichier]** ou **[!UICONTROL Paramètres de protection]**, cliquez sur **[!UICONTROL Définir les paramètres par défaut]**.
1. Sélectionnez les paramètres par défaut souhaités. Dans la page Définir les paramètres par défaut, un ou plusieurs des paramètres suivants sont disponibles :

   **[!UICONTROL Paramètres]** Adobe PDF : La valeur par défaut d’origine est Standard (Acrobat 6).

   **[!UICONTROL Paramètres]** de sécurité : La valeur par défaut d’origine est Aucune sécurité (Acrobat 5).

   **[!UICONTROL Paramètres]** de type de fichier : La valeur par défaut d’origine est Standard.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Suppression d’un paramètre de type de fichier {#delete-a-file-type-setting}

Vous pouvez supprimer un paramètre de type de fichier qui n’est plus utilisé.

1. Dans Administration Console, cliquez sur **[!UICONTROL Services > PDF Generator > Paramètres de type de fichier]**.
1. Cochez la case en regard du paramètre à supprimer. Vous pouvez sélectionner plusieurs sources. Les paramètres en regard desquels ne figure aucune case à cocher sont toujours inclus dans PDF Generator et ne peuvent pas être supprimés.
1. Cliquez sur **[!UICONTROL Supprimer]**, puis, dans la page Confirmation de suppression, cliquez à nouveau sur **[!UICONTROL Supprimer]**.

## Paramètres de conversion d’image en PDF {#image-to-pdf-settings}

Les options suivantes permettent de déterminer comment les fichiers image sont convertis en PDF. Pour plus d’informations sur l’accès à ces paramètres, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensions de nom de fichier :** d’extensions de nom de fichier séparé par des virgules pouvant être converties.

**Essayer le convertisseur de secours :** PDF Generator peut utiliser Java™ ou Acrobat pour convertir des fichiers image au format PDF. Lorsque cette option est sélectionnée et qu’une conversion échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion en utilisant la méthode alternative. Si la méthode alternative échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

***Remarque ** : les fichiers JPEG 2000 ne peuvent être convertis qu’avec Acrobat.*

**Utiliser la reconnaissance optique des caractères :** Indique s’il faut appliquer la reconnaissance optique des caractères au PDF. Un logiciel d’OCR vous permet de rechercher, corriger et copier du texte dans un fichier PDF.

***Remarque ** : la fonction OCR pour les fichiers PDF (PDF indexables) est uniquement prise en charge sous Microsoft Windows.*

**Langue principale de reconnaissance optique des caractères :** Indique la langue à utiliser par le moteur de reconnaissance optique des caractères pour identifier les caractères.

**Style de sortie PDF :** Détermine le type de fichier PDF à produire. Tous les formats appliquent la reconnaissance optique de caractères, ainsi que la reconnaissance de polices et de pages, aux images textuelles et les convertissent en texte normal.

**Image indexable :** Garantit que le texte peut faire l’objet d’une recherche et peut être sélectionné. Cette option conserve l’image d’origine, corrige son décalage au besoin et place un calque de texte invisible dessus. L’option Sous-échantillonner les images détermine si l’image est sous-échantillonnée et dans quelle mesure.

**Image indexable (exacte) :** Garantit que le texte peut faire l’objet d’une recherche et peut être sélectionné. Cette option conserve l’image d’origine et place un calque de texte invisible dessus. Elle est recommandée dans les situations où la fidélité à l’image d’origine est une priorité.

**ClearScan :** Synthétise une nouvelle police Type 3 qui se rapproche étroitement de l’original et conserve l’arrière-plan de la page en utilisant une copie basse résolution.

**Sous-échantillonner les images :** Réduit le nombre de pixels dans les images monochromes, en niveaux de gris et en couleur une fois la reconnaissance optique des caractères terminée. Choisissez le niveau de sous-échantillonnage à appliquer. Les valeurs les plus élevées diminuent le sous-échantillonnage et génèrent des PDF de meilleure résolution.

## Paramètres d’exportation Adobe PDF (Windows uniquement) {#adobe-pdf-export-settings-windows-only}

Le paramètre Exporter le type de fichier dans la section des paramètres d’exportation Adobe PDF permet de convertir un fichier PDF dans un autre format. La valeur par défaut est HTML 4.01 avec feuilles de style en cascade (CSS) 1.0(&amp;ast;.htm, &amp;ast;.html).

Pour plus d’informations sur l’accès à ce paramètre, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Paramètres de conversion du HTML en PDF {#html-to-pdf-settings}

Les options suivantes permettent de déterminer comment les fichiers HTML sont convertis en PDF. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Essayer le convertisseur de secours :** PDF Generator peut utiliser Java™ ou Acrobat pour convertir des fichiers HTML au format PDF. Lorsque cette option est sélectionnée et qu’une conversion échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion en utilisant la méthode alternative. Si la méthode alternative échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**Codage par défaut :** Définit le codage d’entrée du texte du fichier à partir d’un menu de systèmes d’exploitation et d’alphabets. Utilise la sélection de l’option Codage par défaut uniquement si le fichier HTML source ne spécifie aucun type de codage.

**Forcer le codage sélectionné :** Ignore tout codage spécifié dans le fichier source HTML et utilise la sélection indiquée dans l’option Codage par défaut.

### Paramètres d’indexation {#spidering-settings}

*L’indexation* recherche dans les pages Web des liens renvoyant à d’autres pages Web. Si un lien renvoyant à une autre page Web est trouvé, la page de destination est extraite et incluse dans le document PDF généré. Activez ces options pour définir le nombre de niveaux à extraire et à convertir en PDF :

**Obtenir uniquement X niveaux :** Déplace et convertit les pages jusqu’à une profondeur du niveau spécifié à partir de l’URL de base. Une valeur égale à 1 permet de convertir uniquement l’URL indiquée.

**Obtenir l&#39;intégralité du site :** Convertit l’intégralité du site, en commençant par l’URL fournie.

**Rester sur le même chemin :** Les liens pointant vers des pages qui ne se trouvent pas sur le même chemin relatif que l’URL de base ne sont pas convertis lors de l’indexation.

**Rester sur le même serveur :** Les liens pointant vers des pages sur des serveurs différents ne sont pas convertis lors de l’indexation. Seuls les liens renvoyant au même serveur que l’URL définie sont convertis.

### Paramètres de conversion de pages {#page-conversion-settings}

Activez ces options pour spécifier le mode de conversion des pages HTML. Les valeurs de largeur, de hauteur et de marge s’ajustent en fonction du format de page.

**Format de page :** Choisissez personnalisé et spécifiez la largeur et la hauteur, ou sélectionnez des dimensions prédéfinies.

**Orientation :** Sélectionnez Portrait ou Paysage pour le  PDF converti.

**Marges :** Indique les marges (Haut, Bas, Gauche et Droite) dans le  PDF généré.

**Ajouter signets au format PDF :** Ajoute des signets au  PDF.

**Activer le PDF balisé :** Incorpore des balises dans le  PDF.

**Définissez les paramètres de  initiaux du :** Permet de configurer les options de  du, les options de fenêtre et les options de l’interface utilisateur. Ces paramètres déterminent le mode d’affichage initial du contenu.

### Options du document {#document-options}

Ces options permettent de définir le mode d’affichage du contenu et des pages du document PDF et de spécifier le niveau de zoom :

**Afficher :** Sélectionnez les volets à ouvrir dans Acrobat à l’ouverture du PDF.

**Mise en page :** Sélectionnez le type de mise en page du PDF.

**Zoom :** Choisissez un facteur de zoom prédéfini pour la  initiale du PDF ou sélectionnez une valeur personnalisée. Le choix d’un paramètre par défaut implique l’utilisation du zoom par défaut d’Acrobat.

**Ouvrir à la page :** Spécifiez le numéro de page auquel le PDF s’ouvre.

### Options de fenêtre {#window-options}

Ces options permettent de définir le format et le mode d’affichage de la fenêtre.

**Redimensionner la fenêtre sur la page initiale :** Redimensionne la fenêtre Acrobat à la taille de la page initiale.

**Centrer la fenêtre sur l&#39;écran :** Ouvre la fenêtre au centre de l’écran.

**Ouvrir en mode Plein écran :** Ouvre la fenêtre en mode plein écran.

**Afficher :** Affiche le titre ou le nom de fichier  du dans la fenêtre.

### Options de l’interface utilisateur {#user-interface-options}

Ces options permettent de définir l’apparence de la fenêtre :

**Masquer la barre de menus :** Masque la barre de menus dans le  PDF.

**Masquer les barres d’outils :** Masque les barres d’outils dans le  PDF.

**Masquer les commandes de fenêtre :** Masque les commandes de la fenêtre dans le  PDF.

## Paramètres de conversion des vidéos Flash en PDF {#flash-videos-to-pdf-settings}

PDF Generator permet de soumettre une vidéo pour Adobe Flash (au format SWF ou FLV) et de créer un fichier PDF incorporant une vidéo pour Adobe Flash. Cette conversion ne nécessite pas l’installation d’Adobe Flash Player sur le serveur Forms. Pour plus d’informations sur l’accès à cette option, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensions de nom de fichier :** d’extensions de nom de fichier séparé par des virgules pouvant être converties.

## Paramètres de conversion du format XPS en PDF {#xps-to-pdf-settings}

Le format XPL (XML Paper Specification) est utilisé pour l’impression sous Windows. Il s’agit d’un format Microsoft pouvant être créé à partir de n’importe quelle application Microsoft Office. AEM forms permet de convertir des fichiers XPS en PDF.

**Extensions de nom de fichier :** séparé par des virgules de toutes les extensions de nom de fichier XPS pouvant être converties. Il n’existe actuellement un seul format : .xps.

## Paramètres d’optimisation de PDF {#pdf-optimizer-settings}

PDF Generator permet de réduire la taille des fichiers PDF. Le nombre de paramètres utilisés dépend de la façon dont vous envisagez d’exploiter les fichiers et des propriétés qu’un fichier doit posséder. Dans la plupart des cas, les paramètres par défaut ont une efficacité optimale : économie d’espace grâce à la suppression des polices incorporées, compression des images et suppression des éléments superflus dans les fichiers.

>[!NOTE]
>
>l’optimisation d’un document numériquement signé supprime et invalide les signatures numériques.

Pour plus d’informations sur l’accès à ce paramètre, voir [Création ou modification de paramètres de type de fichier](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Version PDF  :** Indique la version d’Acrobat avec laquelle le PDF est compatible.

### Polices {#fonts}

1. Sélectionnez **Polices**.
1. Sélectionnez l’une des options suivantes :

   **Désincorporer toutes les polices :** désincorpore toutes les polices incorporées.

   **Ne désincorporez aucune police :** Ne désincorpore aucune police.

   **Désincorporer certaines polices :** désincorpore uniquement les polices spécifiées. Effectuez les étapes suivantes pour spécifier les polices à désincorporer :

   * Sélectionnez un autre répertoire de polices à partir du menu déroulant **Source des polices** si nécessaire. Ce menu déroulant présente la liste des répertoires de polices spécifiés dans **Accueil > Paramètres > Core System > Configurations de base**.
   * Sélectionnez une ou plusieurs polices dans la liste **Polices disponibles** et cliquez sur **Ajouter**. Les polices sont ajoutées à la liste **Polices à désincorporer**.
   * Si vous voulez désincorporer des polices qui n’apparaissent pas sur le serveur Forms, saisissez les noms de ces polices dans la zone **Ajouter des polices à désincorporer**. Cliquez sur **Ajouter**.
   >[!NOTE]
   >
   >*Pour désincorporer des polices dont les jeux partiels sont incorporés dans le document, ajoutez un signe + avant le nom de la police (par exemple : +Helvetica).*

1. Pour incorporer uniquement les jeux partiels utilisés des polices incorporées, sélectionnez **Créer des jeux partiels de toutes les polices incorporées**.

   >[!NOTE]
   >
   >*si vous utilisez cette option en association avec **Désincorporer certaines polices**, les polices figurant dans la liste **A**jouter des polices à désincorporer sont tout de même désincorporées en totalité.*

   >[!NOTE]
   >
   >*La création de jeux partiels de police permet d’incorporer uniquement une portion d’une police. Un jeu partiel de police ne contient que les caractères utilisés dans le document concerné.*

### Transparence {#transparency}

Si votre document PDF contient des illustrations utilisant la transparence, vous pouvez utiliser les paramètres d’optimisation de PDF pour aplatir la transparence et réduire la taille du fichier.

>[!NOTE]
>
>Si la version PDF cible sélectionnée est Acrobat 4.0 ou une version ultérieure, tous les objets transparents sont aplatis. La transparence est prise en charge pour les autres versions PDF cibles, ce qui vous permet de définir les paramètres de transparence.

Sélectionnez **Transparence** pour configurer les paramètres de transparence lors de l’optimisation des documents PDF.

**Niveau** de transparence Indique la quantité d’informations vectorielles qui seront conservées. Plus la valeur est élevée, plus le nombre d’objets vectoriels conservés l’est aussi, alors que plus la valeur est faible, plus le nombre d’objets vectoriels pixellisés est important. Une valeur moyenne conserve les zones simples sous forme vectorielle et les zones complexes sous forme pixellisées. Sélectionnez la valeur la plus faible pour pixelliser l’ensemble de l’illustration.

>[!NOTE]
>
>le niveau de pixellisation atteint dépend de la complexité de la page et des types d’objets se chevauchant.

**Art au trait et Résolution du texte** auxquelles tous les objets, y compris les images, les illustrations vectorielles, le texte et les dégradés, sont pixellisés. Cette valeur peut être comprise entre 1 et 9600 pixels par pouce (ppp).

>[!NOTE]
>
>La résolution des dessins au trait et du texte doit généralement être définie entre 600 et 1200 ppp pour une qualité de pixellisation optimale, notamment en serif ou en une petite taille de points.

**Dégradé et maillage** Résolution à laquelle le dégradé et les filets sont pixellisés. Cette valeur doit être comprise entre 1 et 1200 ppp.

>[!NOTE]
>
>Définissez de préférence la résolution des dégradés et des filets entre 150 et 300 ppp, étant donné qu’une résolution plus élevée augmente le temps d’impression et la taille des fichiers sans toutefois améliorer la qualité des dégradés, des ombres portées et des contours progressifs.

**Convertir tout le texte en contours** Convertit tous les objets de type (type de point, type de zone et type de chemin) en contours et supprime toutes les informations de glyphe de type sur les pages contenant de la transparence. Cette option préserve la largeur du texte lors de l’aplatissement. Notez que l’activation de cette option a pour effet de donner aux petites polices un aspect légèrement plus épais lorsqu’elles sont affichées dans Acrobat ou lors de l’impression sur des imprimantes de bureau à faible résolution. La qualité du type imprimé sur des imprimantes à résolution élevée ou sur des photocomposeuses n’est pas affectée.

**Convertir tous les contours en contours** Convertit tous les contours en tracés simples remplis sur les pages contenant de la transparence. Cette option préserve la largeur des contours lors de l’aplatissement. Notez que l’activation de cette option a pour effet de donner aux contours fins un aspect légèrement plus épais et peut dégrader les performances de l’aplatissement.

**Ecrêter les régions** complexes Garantit que les limites entre l’illustration vectorielle et l’illustration pixellisée s’étendent le long des chemins d’objet. Cette option réduit les artefacts de raccordement qui subviennent lorsqu’un objet est partiellement pixellisé (une partie de l’objet restant vectorielle). 

>[!NOTE]
>
>certains pilotes d’imprimante traitent les dessins pixellisés et vectorisés différemment, ce qui entraîne parfois un raccordement de couleurs. Vous pouvez arriver à minimiser les problèmes de jointure en désactivant certains paramètres de gestion des couleurs spécifiques au pilote d’impression. Ces paramètres varient selon les imprimantes, consultez la documentation de votre imprimante pour obtenir plus de détails.

Conserver la surimpression : fusionne la couleur des illustrations transparentes et la couleur d’arrière-plan afin de créer un effet de surimpression.

Le tableau suivant répertorie les types d’imprimantes courants ainsi que leur résolution mesurée en dpi, leur lignage de trame par défaut mesuré en lpi, et une résolution de rééchantillonnage des images mesurée en ppi. Par exemple, si vous imprimez sur une imprimante laser 600 dpi, vous devez saisir 170 pour la résolution de rééchantillonnage des images.

**Images** Sélectionnez des images pour définir des options de compression et de rééchantillonnage pour les images monochromes, en niveaux de gris et en couleur. Vous pouvez souhaiter tester ces options pour trouver le bon équilibre entre la taille du fichier et la qualité d’image. Le paramètre de résolution relatif à la couleur et aux niveaux de gris doit être 1,5 à 2 fois le lignage de trame auquel le fichier doit être imprimé. La résolution des images monochromes doit être identique à celle du périphérique de sortie ; toutefois, notez bien que le fait d’enregistrer une image monochrome à une résolution supérieure à 1500 dpi augmente la taille du fichier sans améliorer significativement la qualité d’image. Les images susceptibles d’être agrandies, telles que les cartes, peuvent nécessiter des résolutions supérieures.

>[!NOTE]
>
>le rééchantillonnage d’images monochromes peut avoir des effets inattendus, comme l’affichage d’aucune image. Si tel est le cas, désactivez le rééchantillonnage et convertissez de nouveau le fichier. Ce problème est davantage susceptible de survenir au cours d’un échantillonnage, alors que c’est au cours du sous-échantillonnage bicubique qu’il est le moins fréquent.

<table>
 <tbody>
  <tr>
   <th><p><strong>Résolution de l’imprimante</strong></p> </th>
   <th><p><strong>Lignage de trame par défaut</strong></p> </th>
   <th><p><strong>Résolution d’image</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi (imprimante laser)</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi (imprimante laser)</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1 200 dpi (imageuse film)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2 400 dpi (imageuse film)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### Ignorer les objets {#discard-objects}

* Sélectionnez **Ignorer les objets** pour spécifier les objets à supprimer du PDF et optimiser les lignes courbes dans les dessins CAO.
* **Ignorer les actions d’envoi, d’importation et de réinitialisation de formulaire **: désactive toutes les actions concernant la soumission ou l’importation de données de formulaire, et la réinitialisation de champs de formulaire.  Cette option conserve les objets de formulaire associés à des actions.
* **Ignorer tous les scripts JavaScript **: supprime du fichier toutes les actions qui utilisent JavaScript.
* **Rejeter les vignettes de page intégrée** : supprime les vignettes de page intégrée. Cette option est très utile pour les documents volumineux, qui peuvent prendre beaucoup de temps pour dessiner les vignettes lorsque vous cliquez sur le bouton Pages.
* **Convertir les traits lissés en courbes** : permet de réduire le nombre de points de contrôle utilisés pour créer des courbes dans des dessins CAO, ce qui entraîne une réduction de la taille des fichiers PDF et une accélération du rendu à l’écran.
* **Ignorer les paramètres d’impression incorporés **: supprime les paramètres d’impression incorporés, comme la mise à l’échelle de la page et le mode recto/verso.
* **Ignorer les signets** : supprime tous les signets du document.
* **Aplatissement des champs de formulaire** : rend les champs de formulaire inutilisables, sans modifier leur apparence. Les données de formulaire sont fusionnées avec la page.
* **Ignorer les images de remplacement **: supprime toutes les versions d’une image, sauf la version destinée à être affichée à l’écran. Certains PDF contiennent plusieurs versions de la même image pour différentes finalités, comme l’affichage basse résolution à l’écran et l’impression haute résolution.
* **Ignorer les balises du document **: supprime les balises du document, ainsi que les fonctionnalités d’accessibilité au texte et de redistribution de celui-ci.
* **Détecter et fusionner les fragments d’image **: recherche les images ou les masques qui sont fragmentés en petites parties et tente de les fusionner dans une même image ou un même masque.
* **Ignorer l’index de recherche incorporé **: supprime les index de recherche incorporés, ce qui réduit la taille du fichier.

#### Ignorer les données utilisateur {#discard-user-data}

Sélectionnez **Ignorer les données utilisateur** pour supprimer toutes les informations personnelles que vous ne souhaitez pas distribuer ou communiquer à d’autres utilisateurs.

* **Ignorer tous les commentaires, les formulaires et les fichiers multimédia **: supprime tous les commentaires, formulaires, champs de formulaire et contenus multimédias du PDF.
* **Ignorer toutes les données d’objet **: supprime tous les objets du PDF.
* **Ignorer les références croisées externes **: supprime les liens vers d’autres documents. Les liens vers d’autres sections du document PDF sont conservés.
* **Ignorer le contenu du calque masqué et aplatir les calques visibles** : réduit la taille du fichier. Le document optimisé est identique au PDF d’origine mais ne contient aucune information de calque.
* **Ignorer les métadonnées et les informations sur le document **: supprime le contenu du dictionnaire d’informations du document ainsi que tous les flux de métadonnées  (utilisez la commande Enregistrer sous pour restaurer les flux de métadonnées dans une copie du PDF).
* **Ignorer les pièces jointes **: supprime tous les fichiers en pièce jointe, y compris ceux ajoutés au PDF en tant que commentaires. (PDF Optimizer n’optimise pas les fichiers en pièce jointe).
* **Ignorer les données privées des autres applications **: supprime du document PDF les informations utiles uniquement à l’application ayant créé le document.  Ce paramètre ne modifie pas les fonctionnalités du PDF, mais diminue la taille du fichier.

### Nettoyage {#clean-up}

Sélectionnez **Nettoyage** pour supprimer du document les éléments inutiles.
Ces éléments sont obsolètes ou inutiles pour l’utilisation prévue du document. La suppression de certains éléments peut affecter gravement les fonctionnalités du PDF. Par défaut, seuls ceux qui ne modifient en rien ces fonctionnalités sont sélectionnés. Si vous avez des doutes quant aux conséquences de la suppression d’autres éléments, utilisez les paramètres par défaut.

**Compression**

sélectionnez l’une des options de compression Flate suivantes dans le menu déroulant :

* Compresser le fichier entier
* Compresser la structure du document
* Supprimer la compression
* Ne pas modifier la compression

**Utiliser Flate pour coder les flux non codés **: applique la compression plate à tous les flux non encodés.

**Ignorer les signets non valides **: supprime les signets qui pointent vers des pages supprimées à l’intérieur du document.

**Ignorer les destinations existantes non référencées **: supprime les destinations existantes qui ne sont pas référencées à l’intérieur du document PDF. Cette option ne vérifie pas les liens provenant d’autres fichiers PDF ou sites Web.

**Optimiser le fichier PDF pour l’affichage rapide des pages Web **: restructure un document PDF pour un téléchargement page à page à partir des serveurs Web.

**Utiliser Flate dans les flux en codage LZW **: applique la compression Flate à tous les flux de contenu et à toutes les images en codage LZW.

**Ignorer les liens non valides **: supprime les liens vers des destinations incorrectes.

**Optimiser le contenu de la page **: convertit tous les caractères de fin de ligne en espaces, ce qui améliore la compression plate.

## Paramètres de Microsoft Excel (Windows uniquement) {#microsoft-excel-settings-windows-only}

Ces options permettent de déterminer comment les fichiers Microsoft Excel sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

**Essayez OpenOffice comme convertisseur** de secours : Lorsque cette option est sélectionnée et qu’une conversion utilisant Microsoft Excel échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion à l’aide d’OpenOffice. Si la méthode avec OpenOffice échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**Extensions de nom de fichier **: permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est `xls,xlsx`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

**Créer un fichier compatible avec le format PDF/A-1a **: rend obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF.

**Ajouter Signets au format Adobe PDF**: permet de convertir les noms de feuille de calcul Excel en signets. Cette option est sélectionnée par défaut.

**Ajuster la feuille de calcul à une seule page**: Réduit la taille du texte pour l’adapter à la feuille de calcul sur une seule page.

**Convertir l&#39;intégralité du classeur**: permet de convertir toutes les feuilles de calcul dans le fichier Excel. Si cette option n’est pas sélectionnée seule la page en cours est convertie.

**Exécution automatique** des macros : Exécute toutes les macros dans le  Excel (par exemple, une macro qui insère l’heure actuelle) avant de convertir le  du.

**Convertir les informations** du : Ajoute des propriétés de  PDF basées sur les informations  du dans le fichier source. Cela inclut des informations telles que le titre, l’auteur, le sujet et les mots-clés du document.

**Ajouter des liens à Adobe PDF **: permet de convertir les liens hypertexte du fichier source en liens hypertexte dans le document PDF.

**Joindre le fichier source au fichier Adobe PDF**: Lorsque cette option est sélectionnée, la feuille de calcul Excel d’origine est insérée en tant que pièce jointe dans le  PDF généré.

**Activer l’accessibilité et la redistribution avec le PDF** Adobe balisé : Incorpore des balises dans le PDF pour activer l’accessibilité et la redistribution.

**De Compléments Excel À Charger**: Par défaut (pour des raisons de sécurité), aucun complément Excel n’est exécuté lorsqu’un fichier Excel est converti au format PDF. Pour permettre l’exécution de certains compléments Excel au moment de la conversion, fournissez une liste séparée par des virgules indiquant le nom de ces compléments.

**De Feuilles De Calcul À Convertir**: Lorsque cette zone est vide, toutes les feuilles de calcul de la feuille de calcul Excel sont incluses dans le PDF généré. Pour convertir un sous-ensemble spécifique des feuilles, fournissez une liste séparée par des virgules indiquant leur nom.

## Paramètres de Microsoft PowerPoint (Windows uniquement) {#microsoft-powerpoint-settings-windows-only}

Ces options permettent de déterminer comment les fichiers Microsoft PowerPoint sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Essayer OpenOffice comme convertisseur de secours]** : lorsque cette option est sélectionnée et qu’une conversion utilisant Microsoft PowerPoint échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion en utilisant OpenOffice. Si la méthode avec OpenOffice échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**[!UICONTROL Extensions de nom de fichier ]**: permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est ppt,pptx. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

**[!UICONTROL Convertir les informations sur le document ]**: permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, le sujet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.

**[!UICONTROL Ajouter des signets à Adobe PDF ]**: permet de convertir des titres PowerPoint en signets.  Cette option est sélectionnée par défaut.

**[!UICONTROL Joindre le fichier source au fichier Adobe PDF ]**: permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe.  Cette option est désélectionnée par défaut.

**[!UICONTROL Activer l’accessibilité et la redistribution avec un fichier Adobe PDF balisé]** : permet d’incorporer des balises dans le fichier PDF. Cette option est désélectionnée par défaut.

**[!UICONTROL Convertir le multimédia en multimédia PDF ]**: permet de convertir le multimédia en multimédia PDF, lorsque cela est possible.  Cette option est sélectionnée par défaut.

**[!UICONTROL Convertir les notes du présentateur ]**: permet de convertir les notes du présentateur en PDF.

**[!UICONTROL Exécuter automatiquement les macros ]**: exécute les macros du document PowerPoint (par exemple une macro qui insère l’heure actuelle) avant de le convertir.

**[!UICONTROL Mise en page des PDF basée sur les paramètres de l’imprimante PowerPoint ]**: permet d’utiliser les paramètres de l’imprimante PowerPoint pour la mise en page du document PDF.

**[!UICONTROL Ajouter des liens à Adobe PDF ]**: permet de conserver tous les liens lors de la conversion du fichier. En règle générale, l’apparence des liens n’est pas affectée. Il n’est possible de créer des liens que si l’option Activer l’accessibilité est également sélectionnée. Cette option est désélectionnée par défaut.

**[!UICONTROL Enregistrer les transitions entre diapositives dans Adobe PDF ]**: permet de convertir les transitions entre diapositives. Cette option est sélectionnée par défaut.

**[!UICONTROL Enregistrer les animations dans Adobe PDF ]**: permet d’enregistrer les animations converties dans le fichier PDF.

**[!UICONTROL Convertir les diapositives masquées en pages PDF ]**: permet de convertir les diapositives masquées.

**[!UICONTROL Créer un fichier compatible avec le format PDF/A-1a ]**: rend obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF. Un certain nombre de fonctions de PowerPoint ne sont pas converties lorsque vous créez un fichier PDF. Si une transition PowerPoint ne possède pas d’équivalent dans Acrobat, elle est remplacée par une transition similaire. Si plusieurs effets d’animation se trouvent sur la même diapositive, un seul effet est utilisé. Les transitions de page et les puces volantes sont converties.

## Paramètres de Microsoft Project (Windows uniquement) {#microsoft-project-settings-windows-only}

Ces options permettent de déterminer comment les fichiers Microsoft Project sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

1. **[!UICONTROL Extensions de nom de fichier :]** Spécifie les extensions de nom de fichier pour les types de fichiers, séparées par des virgules, qui sont acceptées pour cette application. La valeur par défaut est `mpp`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

1. **[!UICONTROL Convertir les informations sur le document ]**: permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, le sujet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.
1. **[!UICONTROL Joindre le fichier source au fichier Adobe PDF ]**: permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 
1. **[!UICONTROL Créer un fichier compatible avec le format PDF/A-1a ]**: rend obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF.
1. **[!UICONTROL Exécution automatique]** des macros : Exécute toutes les macros dans le Microsoft Project (par exemple, une macro qui insère l’heure actuelle) avant de convertir l’ du.

## Paramètres de Microsoft Word (Windows uniquement) {#microsoft-word-settings-windows-only}

Ces options permettent de déterminer comment les fichiers Microsoft Word sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

**[!UICONTROL Essayer OpenOffice comme convertisseur de secours]** : lorsque cette option est sélectionnée et qu’une conversion utilisant Microsoft Word échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion en utilisant OpenOffice. Si la méthode avec OpenOffice échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**[!UICONTROL Extensions de nom de fichier ]**: permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est `doc,docx,rtf,txt`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

**[!UICONTROL Convertir les informations sur le document ]**: permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, le sujet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.

**[!UICONTROL Ajouter des signets à Adobe PDF ]**: permet de convertir des titres en signets.  Cette option est sélectionnée par défaut.

**[!UICONTROL Joindre le fichier source au fichier Adobe PDF ]**: permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 

**[!UICONTROL Convertir les références croisées et la table des matières en liens ]**: permet de convertir les références croisées et les entrées de la table des matières en liens.  Cette option est sélectionnée par défaut.

**[!UICONTROL Activer l’accessibilité et la redistribution avec un fichier Adobe PDF balisé ]**: permet d’incorporer les balises dans le fichier PDF. Cette option est sélectionnée par défaut.

**[!UICONTROL Créer un fichier compatible avec le format PDF/A-1a ]**: cette option permet de rendre obligatoire l’utilisation du paramètre PDF/A-1b:2005 RVB Adobe PDF.

**[!UICONTROL Exécuter automatiquement les macros ]**: exécute les macros du document Word (par exemple une macro qui insère l’heure actuelle) avant de le convertir.

**[!UICONTROL Conserver les annotations du document au format Adobe PDF ]**: permet de convertir les annotations du document Word en annotations dans le fichier PDF.

**[!UICONTROL Ajouter des liens à Adobe PDF ]**: permet de convertir les liens hypertexte du fichier source en liens hypertexte dans le document PDF.

**[!UICONTROL Convertir les liens de notes de fin et de bas de page ]**: permet de créer des liens à partir des citations de fin et de bas de page en notes dans le document PDF.

**[!UICONTROL Convertir les commentaires affichés en notes dans Adobe PDF ]**: permet de convertir les commentaires du document Word en notes de texte dans le document PDF.

**[!UICONTROL Activer le balisage avancé ]**: ajoute des balises avancées pour une meilleure accessibilité.

**[!UICONTROL Convertir tous les styles en signets ]**: permet de convertir tous les styles du document Word en signets dans le document PDF.

**[!UICONTROL Styles avec niveaux ]**: permet de spécifier les styles du document Word à convertir en signets dans le document PDF. Permet également de spécifier le niveau des signets. Pour utiliser cette fonctionnalité, désélectionnez l’option **[!UICONTROL Convertir tous les styles en signets]** et spécifiez le nom des styles en adoptant le format suivant :

styleName1=level1[,styleName2=level2...]

Si un nom de style Microsoft Word comporte des virgules (,) ou des signes égal (=), ces caractères doivent être précédés par un caractère d’échappement (\). Par exemple, spécifiez un style nommé « Titre, 1 » comme suit : Titre\, 1.

## Paramètres de Microsoft Visio (Windows uniquement) {#visio}

**Convertir les informations sur le document **: permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, le sujet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut. Cette option est activée par défaut.

**Liens Ajouter vers Adobe PDF**: Conserve tous les liens. Cette option est sélectionnée par défaut.

**Ajouter des signets à Adobe PDF **: permet de convertir des titres en signets.  Cette option est sélectionnée par défaut.

**Joindre le fichier source au fichier Adobe PDF **: permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 

**Toujours aplatir Les Calques Dans Adobe PDF**: Aplatit tous les calques Visio.

**Convertir toutes les pages**: permet de convertir toutes les pages du fichier Visio.

**Ouvrir le panneau Calques lors de l’affichage dans Adobe Acrobat** : si les calques Visio ne sont pas aplatis, permet d’ouvrir une fenêtre dans laquelle vous pouvez préciser les calques qui sont conservés dans le fichier PDF lorsqu’ils sont ouverts dans Acrobat. Cette option est sélectionnée par défaut.

**Créer un fichier** compatible PDF/A-1b : Force l’utilisation du paramètre Adobe PDF PDF/A-1b:2005 (RVB).

**Convertir les commentaires en commentaires** Adobe PDF : permet de convertir des notes Visio en commentaires PDF.

## Paramètres de Microsoft Publisher (Windows uniquement) {#microsoft-publisher-settings-windows-only}

Ces options permettent de déterminer comment les fichiers Microsoft Publisher sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

**[!UICONTROL Extensions de nom de fichier ]**: permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est `pub`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

## Paramètres d’AutoCAD (Windows uniquement) {#autocad-settings-windows-only}

Ces options permettent de déterminer comment les fichiers AutoCAD sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Extensions de nom de fichier ]**: permet de définir les extensions de nom de fichier acceptées pour cette application en les séparant par des virgules. La valeur par défaut est `dwg`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

**[!UICONTROL Convertir les informations sur le document ]**: permet d’ajouter des informations sur le document depuis la boîte de dialogue Propriétés du fichier source, y compris le titre, le sujet, l’auteur, les mots-clés, le responsable, la société, la catégorie et les commentaires. Cette option est sélectionnée par défaut.

**[!UICONTROL Ajouter des signets à Adobe PDF ]**: permet de convertir des titres en signets. 

**[!UICONTROL Toujours aplatir les calques dans Adobe PDF]** : permet d’aplatir tous les calques AutoCAD.

**[!UICONTROL Ouvrir le panneau Calques lors de l’affichage dans Adobe Acrobat ]**: permet d’afficher la structure des calques lors de l’ouverture du PDF dans Acrobat.

**[!UICONTROL Créer un fichier compatible avec le format PDF/E-1 ]**: crée un fichier compatible avec le format PDF/E-1. PDF/E est une norme ISO relative à l’échange de documents d’ingénierie et techniques. Pour plus de détails sur PDF/E-1, reportez-vous au document [Formats Adobe et formats de l’industrie](https://www.adobe.com/enterprise/standards/index.html).

**[!UICONTROL Convertir toutes les mises en page ]**: comprend toutes les mises en page du PDF.

**[!UICONTROL Convertir l’espace modèle en 3D ]**: lorsqu’elle est sélectionnée, la mise en page de l’espace de modèle est convertie en annotation 3D dans le PDF.

**[!UICONTROL Ajouter des liens à Adobe PDF]** : permet de conserver tous les liens.

**[!UICONTROL Joindre le fichier source au fichier Adobe PDF ]**: permet d’ajouter le fichier source au fichier PDF sous forme de pièce jointe. 

**[!UICONTROL Créer un fichier conforme à la norme PDF/A-1b]** : rend obligatoire l’utilisation du paramètre Adobe PDF PDF/A-1b.

**[!UICONTROL Convertir tous les calques ]**: par défaut, PDF Generator ne convertit que le calque par défaut des fichiers AutoCAD au format PDF et non l’ensemble des calques des fichiers. Sélectionnez cette option pour convertir tous les calques du fichier.

**[!UICONTROL Incorporer des informations d’échelle :]** permet de conserver toutes les informations d’échelle du dessin.

**[!UICONTROL Convertir la mise en page actuelle ]**: ne comprend que la mise en page actuelle du PDF.

**[!UICONTROL Liste des mises en page AutoCAD à convertir ]**: un dessin AutoCAD peut avoir plusieurs mises en page.  Lorsque cette zone est vide, toutes les mises en page du dessin AutoCAD sont incluses dans le document PDF généré. Pour convertir un sous-ensemble spécifique des mises en pages, fournissez une liste séparée par des virgules indiquant leur nom.

## Paramètres d’OpenOffice {#openoffice-settings}

Ces options permettent de déterminer comment les fichiers OpenOffice sont convertis. Pour plus d’informations sur l’accès à ces options, voir [Création ou modification de paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**Essayer PDFMaker comme convertisseur de secours **: lorsque cette option est sélectionnée et qu’une conversion utilisant OpenOffice échoue ou atteint le délai d’expiration spécifié, PDF Generator tente d’effectuer la conversion en utilisant PDFMaker. Si la méthode avec PDFMaker échoue ou atteint le délai d’expiration spécifié, une exception est consignée dans le fichier journal.

**Extensions de nom de fichier **: permet de définir les extensions de nom de fichier acceptées par cette application en les séparant par des virgules. La valeur par défaut est `odt,odp,ods,odg,odf,sxw,sxi,sxd`. N’insérez pas de point dans les extensions ou d’espace entre celles-ci.

**Plage**: permet de convertir toutes les pages ou de définir certaines pages ou une plage de pages. Si aucune plage n’est définie, toutes les pages sont converties. Pour exporter une plage de pages, utilisez le format 3-6. Pour exporter une page à la fois, utilisez le format 7;9;11. Vous pouvez exporter plusieurs plages de pages et des pages isolées à l’aide d’un format de type 3-6;8;10;12.

**Orientation de page **: pour les fichiers en texte brut seulement, sélectionnez le format portrait ou paysage pour le document PDF converti.

**Images **: permet de configurer le mode de conversion des images. Les images EPS contenant des aperçus intégrés sont exportées uniquement en tant qu’aperçus. Les images EPS ne contenant pas d’aperçus intégrés sont exportées uniquement en tant qu’espaces réservés. La compression sans perte des images permet de conserver tous les pixels. La compression JPEG des images et un niveau de qualité élevé permettent de conserver pratiquement tous les pixels. Avec un niveau de qualité faible, certains pixels sont perdus et des artefacts apparaissent, mais les fichiers ont une taille plus petite.

**Général** : ces options permettent de convertir un PDF balisé ou d’exporter des notes de document Writer et FormCalc, des effets de transition entre diapositives Impress ou des pages vides vers le PDF. Lors de l’exportation des balises, la taille du fichier peut augmenter considérablement. Parmi les balises exportées figurent les tables des matières, les liens hypertexte et les commandes.

Vous pouvez également définir la manière dont les formulaires sont envoyés. Les options sont XML, FDF, PDF ou HTML. Ce paramètre permet de remplacer la propriété de l’URL de commande que vous avez définie dans le document. Seul un paramètre commun peut être sélectionné pour le document PDF :

* PDF (envoie le document entier)
* FDF (envoie le contenu de la commande)
* HTML
* XML

**PDF balisé **: permet la création de PDF balisés à partir de documents OpenOffice. Les PDF balisés contiennent des informations se rapportant à la structure du contenu du document. Cela peut s’avérer utile lors de l’affichage du document sur des périphériques dotés d’écrans différents, et lors de l’utilisation d’un lecteur d’écran logiciel. Cela permet également aux logiciels d’accessibilité de réaliser diverses opérations utiles au niveau du document PDF, telles que la lecture à voix haute de son contenu.

**Exporter des notes **: permet de convertir les notes de documents OpenOffice en notes de texte dans le document PDF généré.

**Utiliser des effets de transition **: permet de convertir les effets de transition de diapositives dans des présentations OpenOffice en effets de transition PDF correspondants.

**Envoyer des formulaires au format **: permet de créer un formulaire PDF pouvant être rempli et imprimé par l’utilisateur du document PDF.

**Exporter les pages vierges insérées automatiquement **: lorsque cette option est sélectionnée, les pages vierges insérées automatiquement sont incluses dans le document PDF généré. Cela s’avère utile si vous imprimez un document PDF recto verso. Par exemple, un livre pourrait être configuré de façon que la première page du chapitre commence toujours sur une page impaire. Si le chapitre précédent se termine sur une page impaire, OpenOffice insère une page paire vierge. Cette option contrôle l’inclusion de cette page paire dans le PDF généré.

## Other application settings (Windows only) {#other-applications-settings-windows-only}

Vous ne pouvez pas modifier les paramètres d’autres applications dans Administration Console. Ils indiquent les extensions correspondant aux types de fichiers pris en charge. Pour plus d’informations sur l’accès à ces paramètres, voir [Création ou modification de paramètres de type de fichier](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* Adobe PageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Il est possible de personnaliser la prise en charge de ces types de fichier. For more information, see “Adding Support for Additional Native File Formats” in [Programming with AEM forms](https://www.adobe.com/go/learn_aemforms_programming_62).

Pour obtenir de l’aide sur la configuration d’une imprimante réseau PDFG, voir [Configuration d’une imprimante réseau PDFG (Windows uniquement)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
