---
title: Configuration des paramètres Adobe PDF
seo-title: Configuration des paramètres Adobe PDF
description: Découvrez comment configurer les paramètres de fichier PDF Adobe.
seo-description: Découvrez comment configurer les paramètres de fichier PDF Adobe.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '7278'
ht-degree: 74%

---


# Configuration des paramètres Adobe PDF{#configuring-adobe-pdf-settings}

La page Paramètres Adobe PDF contient les paramètres de conversion que vous pouvez définir comme sources à utiliser. Il vous est possible d’utiliser les options PDF prédéfinies ou d’en créer. Les paramètres PDF déterminent précisément le mode de conversion des fichiers, ainsi que la structure et les fonctions PDF qui en résultent. Les options Adobe PDF étaient autrefois désignées sous le nom de paramètres ou d’options de travail Distiller®.

Dans la page Paramètres Adobe PDF, vous pouvez effectuer les opérations suivantes :

* afficher les paramètres PDF prédéfinis (voir [A propos des paramètres PDF prédéfinis](configuring-pdf-settings.md#about-the-predefined-pdf-settings)) ;
* créer un paramètre PDF ou modifier le paramètre créé précédemment (voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings)) ;
* spécifier les paramètres PDF par défaut (voir [Modification des paramètres par défaut](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)) ;
* télécharger un fichier d’options PDF sur le serveur (voir [Téléchargement de paramètres PDF](configuring-pdf-settings.md#upload-pdf-settings)) ;
* supprimer les paramètres PDF personnalisés (voir [Suppression de paramètres PDF](configuring-pdf-settings.md#delete-pdf-settings)) ;
* télécharger des fichiers épilogue et prologue (voir [Téléchargement des fichiers épilogue et prologue](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files)).

Les paramètres Adobe PDF sont applicables uniquement aux conversions basées sur PDFMaker. Ceux-ci incluent les conversions suivantes :

* Document Microsoft Word (DOC, DOCX, RTF, TXT)
* Document Microsoft Excel (XLS, XLSX)
* Document Microsoft PowerPoint (PPT, PPTX)
* Document Microsoft Project (MPP)
* Document Microsoft Visio (VSD)

>[!NOTE]
>
>Si vous utilisez OpenOffice pour convertir les formats ci-dessus, les paramètres Adobe PDF ne sont donc pas appliqués.

## A propos des paramètres PDF prédéfinis {#about-the-predefined-pdf-settings}

PDF Generator propose plusieurs options PDF prédéfinies à utiliser. Ces paramètres ne sont pas modifiables, mais vous pouvez créer un paramètre basé sur un des paramètres existants et l’enregistrer sous un autre nom.

**Impression de haute qualité :** crée des fichiers PDF pour une sortie de haute qualité. Ce paramètre :

* sous-échantillonne les images en couleur et en niveaux de gris à 300 dpi ;
* sous-échantillonne les images monochromes à 1 200 dpi ;
* imprime avec une résolution d’image supérieure ;
* utilise d’autres paramètres pour conserver le maximum d’informations relatives au document d’origine.

Les fichiers PDF obtenus peuvent être ouverts dans Adobe Acrobat 5 et Adobe Acrobat Reader® 5 et versions ultérieures.

**Pages surdimensionnées :** crée des documents PDF adaptés à l’affichage et à l’impression fiables de dessins d’ingénierie de plus de 200 x 200 pouces. Les documents PDF créés peuvent être ouverts dans Adobe Acrobat Professional, Acrobat Standard 7 ou versions ultérieures et Adobe Reader 7 ou versions ultérieures.

**PDF/A-1B 2005 CMJN / PDF/A-1B 2005 RGB :** Vérifie la conformité des travaux entrants à la norme ISO pour la conservation à long terme (archivage) des documents électroniques et crée des fichiers PDF/A uniquement s’ils sont conformes. Ces fichiers sont utilisés principalement à des fins d’archivage. Les fichiers conformes ne peuvent contenir que du texte, des images ligne par ligne et des objets vectoriels. Ils ne peuvent contenir ni chiffrement ni scripts. De plus, toutes les polices doivent être incorporées de sorte que les documents puissent être ouverts et affichés comme ils ont été créés. Le paramètre PDF/A-1b utilise le format PDF 1.4 et convertit toutes les couleurs en CMJN ou RVB, selon le standard utilisé. Les fichiers PDF créés avec ce fichier de paramètres peuvent être ouverts dans Acrobat 5, Acrobat Reader 5 et versions ultérieures. Pour plus d’informations sur PDF/A, voir Adobe et les standards du marché.

**PDF/X-1a 2001:** Vérifie les travaux entrants pour la conformité à la norme PDF/X-1a et crée des fichiers PDF uniquement s’ils sont conformes. PDF/X-1a est une norme ISO relative à l’échange de contenu graphique. PDF/X-1a requiert l’incorporation de toutes les polices, la définition de toutes les zones PDF appropriées et l’affichage en couleurs CMJN ou couleurs d’accompagnement. Les fichiers PDF répondant aux normes PDF/X-1a sont soumis à des conditions d’impression spécifiques (par exemple, l’impression rotative offset selon les Specifications Web Offset Publications). Pour plus d’informations sur PDF/X, voir Adobe et les standards du marché.

**PDF/X-3 2002:** Vérifie la conformité des travaux entrants à la norme PDF/X-3 et crée des fichiers PDF uniquement s’ils sont conformes. Comme PDF/X-1a, PDF/X-3 est une norme ISO relative à l’échange de contenu graphique. La principale différence réside dans le fait que la norme PDF/X-3 prend en charge les couleurs de référence.

**Appuyez sur Qualité :** crée des fichiers PDF pour une impression de haute qualité (par exemple, sur une imageuse d’images ou une imageuse de plaques). Dans ce cas, la taille de fichier n’est pas prise en compte. L’objectif est de gérer toutes les informations dans un fichier PDF, dont un imprimeur commercial ou un prestataire de services de pré-presse a besoin pour imprimer correctement le document. Cet ensemble d’options :

* sous-échantillonne les images en couleur et en niveaux de gris à 300 dpi ;
* sous-échantillonne les images monochromes à 1 200 dpi ;
* incorpore une partie des polices utilisées dans le document ;
* imprime avec une résolution d’image supérieure ;
* ne pivote pas automatiquement les pages en fonction de l’orientation du texte ou des commentaires DSC (Document Structuring Conventions) ;
* utilise d’autres paramètres pour conserver le maximum d’informations relatives au document d’origine.

Les travaux d’impression échouent s’ils sont associés à des polices qui ne peuvent pas être incorporées. Les fichiers PDF obtenus peuvent être ouverts dans Acrobat 5 et Acrobat Reader 5 et versions ultérieures.

>[!NOTE]
>
>avant de créer un fichier PDF à transmettre à un imprimeur ou à un prestataire de services de prépresse, déterminez la résolution de sortie et les autres paramètres d’impression ou demandez un fichier .joboptions contenant les paramètres recommandés. Vous devrez peut-être personnaliser les options Adobe PDF pour un prestataire particulier, puis fournir votre propre fichier .joboptions.

**Taille de fichier la plus petite :** crée des fichiers PDF pour l’affichage sur le Web ou sur un intranet, ou pour la distribution via un système de messagerie pour l’affichage à l’écran. Cet ensemble d’options utilise la compression, le sous-échantillonnage et une résolution d’image relativement faible. Il convertit toutes les couleurs en RVB et n’incorpore pas les polices à moins que cela ne soit nécessaire. Il optimise également les fichiers pour le téléchargement page à page. Les fichiers PDF obtenus peuvent être ouverts dans Acrobat 5 et Acrobat Reader 5.0 et versions ultérieures.

**Standard :** crée des fichiers PDF à imprimer sur des imprimantes de bureau ou des copieurs numériques, à publier sur un CD ou à envoyer à un client en tant que BAT de publication. Cet ensemble d’options utilise la compression et le sous-échantillonnage pour réduire la taille du fichier. Il incorpore également les jeux partiels de toutes les polices utilisées dans le fichier, convertit toutes les couleurs en RVB et imprime à une résolution moyenne afin de créer un rendu relativement précis du document original. Notez que les jeux partiels de polices Microsoft Windows ne sont pas incorporés par défaut. Les fichiers PDF obtenus peuvent être ouverts dans Acrobat 5 et Acrobat Reader 5.0 et versions ultérieures.

## Ajout ou modification de paramètres PDF  {#add-or-edit-pdf-settings}

Les paramètres PDF déterminent précisément le mode de conversion des fichiers, ainsi que la structure et les fonctions PDF qui en résultent. Définissez un nouveau paramètre PDF ou modifiez-en un que vous avez déjà créé. Les paramètres prédéfinis ne sont pas modifiables, mais vous pouvez créer un paramètre basé sur l’un des paramètres existants et l’enregistrer sous un autre nom.

1. Dans Administration Console, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Créer ou sur le nom d’un paramètre.
1. Dans la page relative à la création ou à la modification d’un paramètre Adobe PDF, renseignez les champs obligatoires de ces sections :

   [Options générales](configuring-pdf-settings.md#general-options)

   [Options relatives aux images](configuring-pdf-settings.md#images-options)

   [Options relatives aux polices](configuring-pdf-settings.md#fonts-options)

   [Options relatives aux couleurs](configuring-pdf-settings.md#color-options)

   [Options avancées](configuring-pdf-settings.md#advanced-options)

   [Options de rapport et de conformité aux normes](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

   [Options d’affichage initial](configuring-pdf-settings.md#initial-view-options)

   Pour accéder à une autre section, cliquez sur son lien dans la page Web ou utilisez les boutons Suivant et Précédent.

1. Après avoir renseigné toutes les sections, cliquez sur Enregistrer ou Enregistrer sous et saisissez le nom du paramètre.

## Téléchargement de paramètres PDF  {#upload-pdf-settings}

Vous pouvez copier les paramètres PDF disponibles sur le serveur PDF Generator en les téléchargeant à partir d’un ordinateur local ou d’un emplacement réseau.

1. Dans Administration Console, cliquez sur Services > PDF Generator > Paramètres Adobe PDF, puis sur Télécharger.
1. Dans la page Télécharger les paramètres Adobe PDF, cliquez sur Parcourir, recherchez le fichier et cliquez sur Ouvrir.
1. Cliquez sur OK, puis de nouveau sur OK.

## Suppression de paramètres PDF  {#delete-pdf-settings}

Vous pouvez supprimer définitivement les paramètres PDF qui ne sont plus nécessaires.

1. Dans Administration Console, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cochez la case en regard du paramètre à supprimer. Vous pouvez sélectionner plusieurs paramètres.
1. Cliquez sur Supprimer, puis, dans la page Confirmation de suppression, cliquez à nouveau sur Supprimer.

## Options générales {#general-options}

Les options générales permettent de spécifier la version d’Acrobat à utiliser pour la compatibilité des fichiers et les autres options de fichier et de périphérique. Pour plus d’informations sur l’accès aux options générales, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Options du fichier {#file-options}

**Compatibilité :** niveau de compatibilité du fichier PDF. Pour les documents qui seront largement diffusés, sélectionnez Acrobat 4 (PDF 1.3) ou Acrobat 5 (PDF 1.4) afin de vous assurer que tous les utilisateurs peuvent afficher et imprimer le document. Si vous créez des fichiers à l’aide de la compatibilité Acrobat 5 ou versions ultérieures, il se peut qu’ils ne soient pas compatibles avec les versions antérieures d’Acrobat. Les sous-sections suivantes indiquent certaines différences entre les fichiers PDF créés à l’aide de différents niveaux de compatibilité d’Acrobat.

<table>
 <tbody>
  <tr>
   <th><p>Acrobat 4 (PDF 1.3)</p> </th>
   <th><p>Acrobat 5 (PDF 1.4)</p> </th>
   <th><p>Acrobat 6 (PDF 1.5)</p> </th>
   <th><p>Acrobat 7 (PDF 1.6) et Acrobat 8 (PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>Ces fichiers PDF peuvent être ouverts avec Acrobat 3.0, Acrobat Reader 3.0 et versions ultérieures.</p> </td>
   <td><p>Ces fichiers PDF peuvent être ouverts avec Acrobat 3.0, Acrobat Reader 3.0 et versions ultérieures. Cependant, il se peut que des fonctions spécifiques des versions ultérieures soient perdues ou impossibles à afficher.</p> </td>
   <td><p>La plupart de ces fichiers PDF peuvent être ouverts avec Acrobat 4, Acrobat Reader 4.0 et versions ultérieures. Cependant, il se peut que des fonctions spécifiques des versions ultérieures soient perdues ou impossibles à afficher.</p> </td>
   <td><p>La plupart de ces fichiers PDF peuvent être ouverts avec Acrobat 4, Acrobat Reader 4.0 et versions ultérieures. Cependant, il se peut que des fonctions spécifiques des versions ultérieures soient perdues ou impossibles à afficher.</p> </td>
  </tr>
  <tr>
   <td><p>Ne peut pas contenir d’illustrations utilisant des effets de transparence en direct. Toute transparence doit être aplatie avant de procéder à la conversion en PDF 1.3.</p> </td>
   <td><p>Prend en charge l’utilisation de la transparence en direct dans les illustrations (la fonction d’Acrobat Distiller aplatit la transparence).</p> </td>
   <td><p>Prend en charge l’utilisation de la transparence en direct dans les illustrations (la fonction d’Acrobat Distiller aplatit la transparence).</p> </td>
   <td><p>Prend en charge l’utilisation de la transparence en direct dans les illustrations (la fonction d’Acrobat Distiller aplatit la transparence).</p> </td>
  </tr>
  <tr>
   <td><p>Les calques ne sont pas pris en charge.</p> </td>
   <td><p>Les calques ne sont pas pris en charge.</p> </td>
   <td><p>Conserve les calques lors de la création de fichiers PDF à partir d’applications qui prennent en charge la génération de documents PDF superposés, telles qu’Illustrator® CS ou InDesign® CS et versions ultérieures.</p> </td>
   <td><p>Conserve les calques lors de la création de fichiers PDF à partir d’applications qui prennent en charge la génération de documents PDF superposés, telles qu’Illustrator CS ou InDesign CS et versions ultérieures.</p> </td>
  </tr>
  <tr>
   <td><p>L’espace colorimétrique DeviceN avec 8 colorants est pris en charge.</p> </td>
   <td><p>L’espace colorimétrique DeviceN avec 8 colorants est pris en charge.</p> </td>
   <td><p>L’espace colorimétrique DeviceN avec jusqu’à 31 colorants est pris en charge.</p> </td>
   <td><p>L’espace colorimétrique DeviceN avec jusqu’à 31 colorants est pris en charge.</p> </td>
  </tr>
  <tr>
   <td><p>Les polices multioctets peuvent être incorporées (Distiller convertit les polices lors de leur incorporation).</p> </td>
   <td><p>Les polices multioctets peuvent être incorporées</p> </td>
   <td><p>Les polices multioctets peuvent être incorporées</p> </td>
   <td><p>Les polices multioctets peuvent être incorporées.</p> </td>
  </tr>
  <tr>
   <td><p>La protection RC4 40 bits est prise en charge.</p> </td>
   <td><p>La protection RC4 128 bits est prise en charge.</p> </td>
   <td><p>La protection RC4 128 bits est prise en charge.</p> </td>
   <td><p>La protection RC4 128 bits et AES (Advanced Encryption Standard) 128 bits AES (Advanced Encryption Standard) est prise en charge.</p> </td>
  </tr>
 </tbody>
</table>

**Compression au niveau de l’objet :** consolide les petits objets (qui ne sont pas compressibles eux-mêmes) en flux qui peuvent être compressés efficacement.

**Désactivé :** ne compresse aucune information structurelle dans le document PDF. Sélectionnez cette option si vous souhaitez que les utilisateurs affichent, naviguent et interagissent avec des signets et d’autres informations structurelles à l’aide d’Acrobat 5 et versions ultérieures.

**Balises uniquement :** compresse les informations structurelles dans le document PDF. Cette option génère un fichier PDF pouvant être ouvert et imprimé avec Acrobat 5. Les utilisateurs ne peuvent pas afficher les informations d’accessibilité, de structure ou de balisage du PDF dans Acrobat 5 ou Acrobat Reader 5.0 mais l’opération est possible dans Acrobat 6 et Adobe Reader 6.0.

**Rotation automatique des pages :** définit la rotation automatique des pages en fonction de l’orientation du texte ou des commentaires DSC. Par exemple, il peut s’avérer nécessaire de faire pivoter certaines pages (comme celles qui contiennent des tableaux) afin de pouvoir les lire. Sélectionnez Individuelle pour faire pivoter chaque page selon l’orientation du texte de celle-ci. Sélectionnez Collective par fichier pour faire pivoter toutes les pages du document selon l’orientation de la majorité du texte.

>[!NOTE]
>
>si Traiter les commentaires DSC est sélectionnée dans les paramètres Avancées et si des %%commentaires relatifs à l’orientation de l’affichage sont inclus, ces derniers sont prioritaires dans le choix de l’orientation de la page.

**Liaison :** indique si un fichier PDF doit être affiché avec une liaison à gauche ou à droite. Ce paramètre modifie l’affichage des pages en mise en page Continue-Page double et l’affichage des miniatures côte à côte.

**Résolution :** définit l’émulation de la résolution d’une imprimante pour les fichiers d’entrée qui ajustent leur comportement en fonction de la résolution de l’imprimante sur laquelle ils sont en train d’imprimer. Pour la plupart des fichiers d’entrée, une résolution plus élevée permet d’obtenir des fichiers PDF de plus grande taille et de meilleure qualité, alors qu’une résolution moins élevée donne des fichiers PDF de qualité inférieure et de plus petite taille. Plus couramment, la résolution détermine le nombre d’étapes d’un dégradé. Vous pouvez saisir une valeur comprise entre 72 et 4000. Conservez ce paramètre comme valeur par défaut à moins que vous ne prévoyiez d’imprimer le fichier sur une imprimante spécifique et que vous ne souhaitiez émuler la résolution définie dans le fichier d’entrée original.

>[!NOTE]
>
>l’augmentation de la valeur du paramètre de résolution entraîne l’accroissement de la taille du fichier et peut légèrement faire accroître la durée nécessaire au traitement de certains fichiers.

**Toutes les pages ou Pages de :** indique les pages à convertir. Ne renseignez pas la zone A afin de créer une plage comprise entre le numéro de page entré dans la zone De et la fin du fichier.

**Optimiser pour la Vue Web rapide :** restructure le fichier pour le téléchargement page par page (diffusion d’octets) depuis les serveurs Web. Cette option donne la possibilité de compresser du texte et des dessins au trait, indépendamment des paramètres de compression choisis dans l’onglet Images. L’accès et l’affichage lors du téléchargement du fichier à partir du Web ou d’un réseau s’en trouvent accélérés. Cette option est désactivée par défaut.

### Format de page par défaut  {#default-page-size}

Les options de Format de page par défaut permettent de définir le format de page à utiliser lorsque celui-ci n’est pas spécifié dans le fichier original. Habituellement, les fichiers Adobe PostScript incluent ces informations, à l’exception des fichiers PostScript encapsulés (EPS) qui indiquent un format de cadre mais pas un format de page. Le format de page maximal autorisé est 31 800 000 cm dans les deux sens. Ces options permettent de configurer le format de page par défaut :

**Largeur:** Largeur de la page

**Hauteur :** Hauteur de la page

**Unités :** unités à utiliser pour les paramètres de largeur et de hauteur

## Options relatives aux images {#images-options}

Les options Images permettent de définir la compression et le rééchantillonnage des images. Vous pouvez utiliser ces options pour rechercher un juste équilibre entre le format de page et la qualité de l’image. Pour plus d’informations sur l’accès aux paramètres Images, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Ces options servent à configurer les images monochromes, en niveaux de gris et en couleur.

**Sous-échantillonnage :** définissez une valeur pour chaque type d’image. Pour sous-échantillonner des images monochromes, en niveaux de gris ou en couleur, PDF Generator associe les pixels dans une zone d’échantillonnage afin d’obtenir un plus grand pixel. Indiquez la résolution de votre périphérique de sortie en dpi et saisissez une résolution en dpi dans la zone Pour les images au-dessus de. Pour toutes les images dont la résolution dépasse ce seuil, PDF Generator combine les pixels, le cas échéant, afin de réduire la résolution (ppi) au niveau du paramètre dpi défini. Pour désactiver le sous-échantillonnage, sélectionnez Désactivé. Les options sont les suivantes :

**Sous-échantillonnage moyen à :** Moyenne des pixels d’une zone d’échantillonnage et remplace la zone entière par la couleur moyenne des pixels à la résolution spécifiée.

**Sous-échantillonnage bicubique à :** utilise une moyenne pondérée pour déterminer la couleur des pixels et produit généralement de meilleurs résultats que la méthode de sous-échantillonnage moyenne simple. La méthode bicubique est la plus lente, mais également la plus précise et est celle qui offre les dégradés de tons les plus lisses.

**Sous-échantillonnage à :** sélectionne un pixel au centre de la zone d’échantillonnage et remplace la zone entière par ce pixel à la résolution spécifiée. Comparée à l’échantillonnage classique, cette méthode permet de réduire significativement la durée de conversion. Cependant, les images qui en résultent sont moins lisses et continues.

Le paramètre de résolution relatif à la couleur et aux niveaux de gris doit être 1,5 à 2 fois la linéature de trame auquel le fichier doit être imprimé (à condition que vous n’alliez pas en deçà de ce paramètre de résolution recommandé, les images qui ne contiennent aucune ligne droite, aucun motif géométrique ou aucun motif répété ne sont pas affectées par une résolution inférieure). La résolution des images monochromes doit être identique à celle du périphérique de sortie. Toutefois, sachez que l’enregistrement d’une image monochrome à une résolution supérieure à 1 500 dpi augmente la taille du fichier sans améliorer significativement la qualité de l’image.

Vous devez également tenir compte que les utilisateurs peuvent utiliser la loupe. A titre d’exemple, si vous créez le document PDF d’un plan, pensez à utiliser une résolution d’image plus élevée afin que les utilisateurs puissent zoomer sur ce plan.

>[!NOTE]
>
>le rééchantillonnage d’images monochromes peut avoir des effets inattendus, comme l’affichage d’aucune image. Si tel est le cas, désactivez le rééchantillonnage et convertissez de nouveau le fichier. Ce problème est davantage susceptible de survenir au cours d’un échantillonnage, alors que c’est au cours du sous-échantillonnage bicubique qu’il est le moins fréquent.

Ce tableau répertorie les types d’imprimantes courants ainsi que leur résolution mesurée en dpi, leur linéature de trame par défaut mesurée en lpi, et une résolution de rééchantillonnage des images mesurées en ppi. Par exemple, pour imprimer sur une imprimante laser de 600 dpi, saisissez 170 comme résolution de rééchantillonnage des images.

<table>
 <tbody>
  <tr>
   <th><p>Résolution de l’imprimante</p> </th>
   <th><p>Lignage de trame par défaut</p> </th>
   <th><p>Résolution d’image</p> </th>
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

**Compression :** définissez une valeur à appliquer aux images monochromes, en niveaux de gris et en couleur. Pour les images en niveaux de gris et en couleur, définissez également la qualité d’image :

* Pour les images en couleur ou en niveaux de gris, sélectionnez ZIP afin d’appliquer une compression fonctionnant bien sur les images contenant de grandes zones de couleur unique ou de motifs répétés. Ces images peuvent être des captures d’écran, des images simples créées à l’aide de programmes de dessin et des images monochromes contenant des motifs répétés. Sélectionnez JPEG, qualité minimale à maximale, pour appliquer un mode de compression adapté aux images en niveaux de gris ou en couleur, comme les photographies en demi-teinte, qui contiennent davantage de détails reproductibles à l’écran ou sur papier. Sélectionnez Automatique (JPEG) pour déterminer automatiquement la meilleure qualité qui soit pour les images en niveaux de gris ou en couleur.
* Pour les images monochromes, sélectionnez la compression CCITT Groupe 4, CCITT Groupe 3, ZIP, JPEG2000, Automatique (JPEG2000) ou Run Length.

Assurez-vous que les images monochromes sont numérisées en monochrome et non en niveaux de gris. Le texte est parfois numérisé par défaut sous forme d’images en niveaux de gris. Le texte en niveaux de gris compressé à l’aide de la méthode JPEG n’est pas clair et peut être illisible.

**Qualité de l’image :** configure la qualité de l’image pour les images en niveaux de gris et en couleur. Les options disponibles sont Minimale, Faible, Moyenne, Elevée et Maximale.

**Lissage des gris :** permet de lisser les bords dentelés dans les images monochromes. Sélectionnez 2 bits, 4 bits ou 8 bits pour définir 4, 16 ou 256 niveaux de gris (le lissage des gris peut donner un aspect flou aux corps intermédiaires ou aux lignes fines).

>[!NOTE]
>
>la compression du texte et des dessins au trait est toujours activée.

**Stratégie d’image :** définissez une stratégie pour les images monochromes, en niveaux de gris et en couleur. Si la résolution d’image est inférieure à la résolution spécifiée, vous pouvez toujours sélectionner Ignorer pour poursuivre, envoyer un message d’avertissement ou annuler le travail.

## Options relatives aux polices  {#fonts-options}

Ces options permettent de définir les polices à incorporer dans un fichier PDF et s’il convient d’incorporer un jeu partiel de caractères utilisés dans ce même fichier. Pour plus d’informations sur l’accès aux options relatives aux polices, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>lorsque vous combinez des fichiers PDF ayant le même jeu partiel de polices, PDF Generator tente de combiner ces jeux partiels.

**Incorporer toutes les polices :** incorpore toutes les polices utilisées dans le fichier. L’incorporation des polices est nécessaire à la conformité avec la norme PDF/X.

**Jeux partiels de polices incorporées lorsque le pourcentage de caractères utilisés est inférieur à :** si vous sélectionnez cette option, indiquez un pourcentage de seuil pour l’incorporation d’un seul jeu partiel de polices. Par exemple, si le seuil est de 35 et que moins de 35 % des caractères sont utilisés, PDF Generator incorpore uniquement ces caractères. Seules les polices avec des bits de droits d’accès appropriés sont incorporées.

**Echec de l’incorporation :** indique comment PDF Generator répond s’il ne trouve pas de police à incorporer lors du traitement d’un fichier. Vous pouvez demander à PDF Generator d’ignorer la demande et de remplacer la police, de vous avertir et de remplacer la police ou d’annuler le traitement du travail en cours.

**Source des polices :** emplacement des polices utilisées par PDF Generator.

### Définition des polices à incorporer {#specify-which-fonts-to-embed}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Créer ou sur le nom d’un paramètre.
1. Cliquez sur Polices et désélectionnez Incorporer toutes les polices.
1. Dans la liste Source des polices, sélectionnez une source de police, puis cliquez sur Atteindre pour actualiser la liste des polices dans la zone située sur le côté gauche.
1. Cliquez sur une police dans la zone de gauche, puis sur Ajouter en regard de la case correspondante pour la faire passer dans la liste Toujours incorporer ou Ne jamais incorporer. Répétez cette procédure pour chaque police. Maintenez la touche Ctrl enfoncée tout en cliquant sur la souris pour sélectionner plusieurs polices à déplacer.
1. Pour supprimer une police de la liste Toujours incorporer ou Ne jamais incorporer, sélectionnez-la et cliquez sur Supprimer en regard de la case voulue. Par cette action, vous ne supprimez pas la police de votre système, mais vous retirez uniquement la référence de celle-ci dans la liste.
1. Si la police à définir n’est pas affichée, tapez son nom dans la zone Ajouter une police, puis cliquez sur Toujours incorporer ou Ne jamais incorporer. Les noms de police ne peuvent pas contenir de caractères alphanumériques.

>[!NOTE]
>
>une police TrueType peut contenir un paramètre (ajouté par le concepteur de cette police) l’empêchant d’être incorporée dans des fichiers PDF.

>[!NOTE]
>
>Les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client, assurez-vous de redémarrer le système sur lequel AEM forms est installé.

## Options relatives aux couleurs  {#color-options}

Ces options permettent de définir la prise en charge des couleurs par PDF Generator. Pour plus d’informations sur l’accès aux options relatives aux couleurs, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Paramètres de couleur Adobe  {#adobe-color-settings}

**Fichier de paramètres :** Cette liste contient une liste de paramètres de couleur qui sont également utilisés dans les applications graphiques majeures, telles que Adobe Photoshop et Adobe Illustrator. Le paramètre de couleur sélectionné détermine les autres paramètres Adobe de couleur de cette page. Par exemple, si vous sélectionnez un paramètre autre qu’Aucune, tous les paramètres autres que ceux relatifs à Données dépendantes du périphérique sont prédéfinis et provisoirement inaccessibles. Il vous est possible de modifier les paramètres Stratégies de gestion des couleurs et Espaces de travail seulement si vous avez sélectionné Aucune pour Fichier de paramètres.

### Stratégies de gestion des couleurs {#color-management-policies}

Si vous avez sélectionné Aucune pour Fichier de paramètres, la zone Stratégies de gestion des couleurs indique la manière dont PDF Generator convertit les couleurs non gérées d’un fichier PostScript.

**Ne pas modifier les couleurs :** laisse les couleurs dépendantes du périphérique inchangées et conserve les couleurs indépendantes du périphérique comme l’équivalent le plus proche possible dans PDF. Cette option s’avère utile pour les ateliers d’impression ayant étalonné l’ensemble de leurs périphériques, ayant utilisé ces informations pour définir les couleurs du fichier et qui impriment uniquement sur ces périphériques.

**Référencer les balises pour la gestion des couleurs :** incorpore un profil de consortium de couleurs international lors de la conversion de fichiers et de l’étalonnage des couleurs dans les images, ce qui rend les couleurs des fichiers PDF résultants indépendantes du périphérique si vous avez sélectionné la compatibilité Acrobat 4 (PDF 1.3) ou ultérieure. Cependant, les espaces colorimétriques dépendants du périphérique des fichiers (RVB, Niveaux de gris et CMJN) sont convertis en espaces colorimétriques de référence (CalRVB, CalGray et LAB).

**Baliser uniquement les images pour la gestion des couleurs :** incorpore les profils ICC uniquement dans les images, et non dans le texte ou les graphiques, lors de la conversion de fichiers si vous avez sélectionné la compatibilité Acrobat 4 (PDF 1.3). Cela empêche le texte noir de subir une variation chromatique. Cependant, les espaces colorimétriques dépendants du périphérique des images (RVB, Niveaux de gris et CMJN) sont convertis en espaces colorimétriques de référence (CalRVB, CalGray et LAB). Les textes et les graphiques ne sont pas convertis.

**Convertir toutes les couleurs en sRVB ou Convertir toutes les couleurs en CMJN :** permet d’étalonner la couleur dans le fichier, ce qui rend la couleur indépendante du périphérique, comme pour l’option Tout marquer pour la gestion des couleurs. Si vous avez sélectionné la compatibilité Acrobat 4 (PDF 1.3) ou versions ultérieures et Convertir toutes les couleurs en sRVB, en CMJN et RVB, les images RVB sont converties en sRVB.

Quelle que soit l’option de compatibilité choisie, les images en niveaux de gris ne sont pas modifiées. Cela entraîne habituellement une réduction du volume et une augmentation de la vitesse d’affichage des fichiers PDF, car la description des images RVB nécessite une quantité d’informations moins importante que celle des images CMJN. RVB est l’espace colorimétrique natif utilisé sur les écrans, c’est pourquoi aucune conversion de couleur n’est nécessaire lors de l’affichage, ce qui contribue à accélérer l’affichage en ligne. Cette option est recommandée si le fichier PDF est utilisé en ligne ou avec des imprimantes à faible résolution.

**Mode de rendu du document :** méthode permettant de mapper les couleurs entre les espaces colorimétriques. Quelle que soit la méthode, son résultat dépend des profils des espaces colorimétriques. Par exemple, certains profils donnent des résultats identiques avec des méthodes différentes. Voici les options de disponibles :

>[!NOTE]
>
>dans tous les cas, il est possible d’ignorer ou de remplacer les modes par des opérations de gestion des couleurs qui surviennent après la création du fichier PDF.

**Conserver :** signifie que l’intention est spécifiée dans le périphérique de sortie plutôt que dans le fichier PDF. Dans de nombreux périphériques de sortie, Colorimétrie relative est le mode par défaut.

**Perception :** conserve les valeurs de couleur relatives parmi les pixels d’origine lors de leur mappage à la gamme de destination. Cette méthode donne la possibilité de conserver la relation visuelle entre les couleurs, bien que les valeurs des couleurs elles-mêmes puissent changer.

**Saturation :** conserve les valeurs de saturation relative des pixels d’origine. Cette méthode est adaptée aux graphiques d’entreprise, pour lesquels la relation exacte entre les couleurs n’est pas aussi importante que le fait d’avoir des couleurs saturées éclatantes.

**Colorimétrie relative :** permet de faire correspondre le point blanc de l’espace source au point blanc de l’espace de destination.

**Colorimétrie absolue :** désactive la correspondance des points blancs et noirs lors de la conversion des couleurs. Cette méthode n’est pas recommandée à moins que vous ne deviez conserver les couleurs de signature, telles que celles utilisées dans les marques et les logos.

### Espaces de travail {#working-spaces}

Pour l’ensemble des valeurs de la liste se trouvant sous Stratégies de gestion des couleurs, autres que Reproduire les couleurs, sélectionnez les options répertoriées dans les listes situées dans la zone Espace de travail afin de spécifier les profils ICC à utiliser pour la définition et l’étalonnage des espaces colorimétriques en niveaux de gris, RVB et CMJN des fichiers PDF convertis. Voici les options de disponibles :

**Gris :** définit l’espace colorimétrique de toutes les images en niveaux de gris des fichiers. Cette option est disponible uniquement si vous choisissez Référencer les couleurs ou Référencer les images uniquement. Le profil ICC par défaut pour les images en niveaux de gris est Gamma gris 2.2. Il vous est également possible de sélectionner Aucun pour empêcher la conversion des images en niveaux de gris.

**RVB :** définit l’espace colorimétrique de toutes les images RVB des fichiers. La valeur par défaut sRVB IEC61966-2.1 est généralement recommandée, car ce standard est en passe de devenir la référence et de nombreux périphériques de sortie le prennent en charge. Il vous est également possible de sélectionner Aucun pour empêcher la conversion des images en RVB.

**CMJN :** définit l’espace colorimétrique de toutes les images CMJN dans les fichiers. La valeur par défaut est U.S. Web Coated (SWOP) v2. Il vous est également possible de sélectionner Aucun pour empêcher la conversion des images en CMJN.

>[!NOTE]
>
>le fait de sélectionner Aucun pour les trois espaces de travail revient à sélectionner Reproduire les couleurs.

**Conserver les valeurs CMJN pour les espaces colorimétriques CMJN étalonnés :** lorsque cette option est sélectionnée, les valeurs CMJN indépendantes du périphérique sont traitées comme des valeurs dépendantes du périphérique (DeviceCMJN), les espaces colorimétriques indépendants du périphérique sont ignorés et les fichiers PDF/X-1a utilisent la valeur Convertir toutes les couleurs en CMJN. Si elle n’est pas sélectionnée, les espaces colorimétriques de référence sont convertis en CMJN si la valeur Convertir toutes les couleurs en CMJN est affectée à la stratégie de gestion des couleurs.

### Données dépendantes du périphérique  {#device-dependent-data}

Ces paramètres s’appliquent si vous manipulez des documents créés à l’aide d’applications graphiques ou de documentation de pointe, telles qu’Adobe Illustrator et Adobe InDesign. Pour plus d’informations, consultez la documentation fournie avec l’application.

Les fonctions de transfert sont utilisées pour obtenir un effet artistique et pour s’adapter aux spécifications d’un périphérique de sortie spécifique. Par exemple, un fichier destiné à une impression sur une imageuse film spécifique peut contenir des fonctions de transfert qui compensent l’élargissement du point inhérent à cette imprimante.

**Conserver les paramètres Sous Suppression des couleurs et Génération noire :** conserve ces paramètres s’ils existent dans le fichier PostScript. Densité de noir calcule la quantité de noir à utiliser lors de la tentative de reproduction d’une couleur spécifique. UCR réduit la quantité de composants cyan, magenta et jaune pour compenser la quantité de noir ajoutée par le paramètre densité de noir. En raison d’une quantité d’encre utilisée moins importante, le paramètre UCR est généralement utilisé pour l’impression sur papier journal et papier non couché.

**Lorsque des fonctions de transfert sont détectées :** détermine la marche à suivre lorsque des fonctions de transfert sont détectées :

**Conserver :** conserve les fonctions de transfert habituellement utilisées pour compenser le gain de points ou la perte de points qui peuvent survenir lors du transfert d’une image vers un film. L’élargissement du point survient lorsque les points d’encre dont une page imprimée est composée sont plus grands que sur la trame de similigravure (par exemple, en raison de l’étalement sur le papier). Par contre, le rétrécissement du point survient lorsque les points s’impriment en plus petit. Grâce à cette option, les fonctions de transfert sont conservées dans le fichier et appliquées à ce dernier lors de son impression.

**Appliquer :** Ne conserve pas la fonction de transfert mais l&#39;applique au fichier, ce qui modifie les couleurs du fichier. Cette option est utile pour créer des effets de couleur dans un fichier. Cette option est sélectionnée par défaut pour les nouveaux paramètres.

**Supprimer :** supprime toutes les fonctions de transfert appliquées. Supprimez ces fonctions de transfert sauf si le fichier PDF est imprimé sur le même périphérique que celui pour lequel le fichier PostScript source a été créé.

**Conserver les informations sur les demi-teintes :** conserve les informations sur les demi-teintes dans les fichiers. Les informations sur les demi-teintes consistent en des points qui contrôlent la quantité d’encre déposée par les périphériques d’impression en demi-teinte à un emplacement spécifique sur le papier. En faisant varier la densité et la grandeur du point, on crée l’illusion de variations de gris ou d’une couleur continue. Pour une image en CMJN, quatre trames de similigravure sont utilisées, c’est-à-dire une pour chaque encre utilisée dans le processus d’impression.

En imprimerie traditionnelle, une demi-teinte est obtenue en plaçant une trame de similigravure entre un film et l’image, puis en exposant le film. Les équivalents électroniques, comme dans Adobe Photoshop, permettent aux utilisateurs de définir les attributs de la trame de similigravure avant d’imprimer le film ou le papier. Les informations en demi-teintes doivent être utilisées avec un périphérique de sortie spécifique.

## Options avancées  {#advanced-options}

Ces options avancées permettent d’indiquer les commentaires DSC à conserver dans le fichier PDF et comment définir les autres options qui affectent la conversion à partir du format PostScript. Dans un fichier PostScript, les commentaires DSC contiennent des informations sur le fichier (comme l’application d’origine, la date de création et l’orientation de la page). Ils fournissent également une structure pour la description des pages du fichier (comme les instructions de début et de fin d’une section de prologue). Ces commentaires peuvent servir en cas d’impression du document. Pour plus d’informations sur l’accès aux options avancées, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Les options avancées permettent de mieux comprendre le langage PostScript et la manière dont il est traduit en PDF (Voir[ adobe postscript 3](https://www.adobe.com/products/postscript/main.html)).

**Autoriser le fichier PostScript à remplacer les paramètres Adobe PDF :** utilise les paramètres stockés dans un fichier PostScript au lieu du fichier de paramètres Adobe PDF actuel. Avant de traiter un fichier PostScript, vous pouvez placer des paramètres dans le fichier pour contrôler les aspects suivants :

* la compression du texte et des graphiques,
* le sous-échantillonnage et l’encodage des images échantillonnées,
* l’incorporation de polices Type 1 et d’instances de polices Type 1 Multiple Master.

**Autoriser les XObjects:** PostScript stocke les informations qui s’affichent sur de nombreuses pages du même fichier, telles qu’une image d’arrière-plan ou des informations d’en-tête et de pied de page. Leur utilisation peut contribuer à accélérer l’impression, mais nécessite une plus grande mémoire d’imprimante. Pour empêcher la création de XObjects au format PostScript, désélectionnez cette option si vous créez des fichiers PDF avec une compatibilité Acrobat 5 (PDF 1.4) ou versions ultérieures.

**Convertir les dégradés en ombres lissées :** permet de convertir les dégradés en ombres lissées pour Acrobat 4 et les versions ultérieures, ce qui réduit les fichiers PDF et peut améliorer la qualité de la sortie finale. PDF Generator convertit les dégradés issus d’Adobe Illustrator, Adobe InDesign, Adobe Freehand MX, CorelDraw, Quark XPress et Microsoft PowerPoint.

**Convertir les lignes lissées en courbes :** réduit la quantité de points de contrôle utilisés pour créer des courbes dans des dessins CAO, ce qui se traduit par des PDF plus petits et un rendu plus rapide à l’écran.

**Conserver la sémantique de la page de copie de niveau 2 :** Utilise l’opérateur de page de copie défini dans LanguageLevel 2 PostScript au lieu de dans LanguageLevel 3 PostScript. Si vous disposez d’un fichier PostScript et que cette option est sélectionnée, un opérateur copypage copie la page. Si cette option n’est pas sélectionnée, l’équivalent d’une opération showpage est exécuté, mais l’état de l’image n’est pas réinitialisé.

**Conserver les paramètres de surimpression :** conserve les paramètres de surimpression dans les fichiers convertis au format PDF. Les couleurs surimprimées consistent en deux encres ou plus imprimées l’une sur l’autre. Par exemple, si une encre cyan s’imprime sur une encre jaune, la couleur de surimpression obtenue est verte. Sans surimpression, le jaune sous-jacent ne serait pas imprimé et donnerait du cyan.

**La surimpression par défaut est une surimpression non nulle :** empêche les objets surimprimés avec des valeurs CMJN nulles d’éliminer les objets CMJN situés en dessous. Pour ce faire, il suffit d’insérer le paramètre d’état d’image OPM 1 dans le fichier PDF partout où Setoverprint est présent.

**Enregistrer les paramètres Adobe PDF dans un fichier PDF :** incorpore le fichier de paramètres utilisé pour créer le fichier PDF. Vous pouvez ouvrir et afficher le fichier d’options (portant l’extension .joboptions) dans la boîte de dialogue Pièces jointes d’Acrobat. Le fichier de paramètres Adobe PDF devient alors un élément de l’arborescence EmbeddedFiles au sein du fichier PDF.

**Enregistrer les images JPEG d’origine au format PDF si possible :** traite les images JPEG compressées (images déjà compressées à l’aide du codage DCT) sans les compresser à nouveau. Si cette option est sélectionnée, PDF Generator décompresse les images JPEG afin de vérifier qu’elles ne sont pas corrompues. Toutefois, elle ne recompresse pas les images valides. L’image d’origine est traitée sans aucune modification. Les performances sont alors accrues en raison d’une décompression non suivie d’une recompression et les données d’image ainsi que les métadonnées sont conservées.

**Enregistrer le ticket de tâche portable dans un fichier PDF :** conserve un ticket de tâche PostScript dans un fichier PDF. Le dossier de correspondance contient des informations relatives au fichier PostScript, telles que le format de page, la résolution et des informations de recouvrement, plutôt que les informations sur le contenu. Il est possible d’utiliser ces informations ultérieurement dans un flux de travail ou pour l’impression du PDF.

**Utilisez Prologue.ps et Epilogue.ps :** envoie un fichier prologue et épilogue à chaque tâche. Il est possible d’utiliser ces fichiers de plusieurs manières. Par exemple, les fichiers prologue peuvent être modifiés pour définir des pages de couverture. Les fichiers épilogue peuvent être modifiés pour résoudre une série de procédures d’un fichier PostScript. Il est possible de télécharger les fichiers (voir Téléchargement des fichiers épilogue et prologue).

**Traiter les commentaires DSC :** permet de gérer les informations DSC à partir d’un fichier PostScript. Les sous-options disponibles sont les suivantes :

**Enregistrer les avertissements DSC :** affiche des messages d’avertissement sur les commentaires DSC problématiques pendant le traitement et les ajoute à un fichier journal.

**Conserver les informations EPS de DSC :** permet de conserver les informations, telles que l’application d’origine et la date de création d’un fichier EPS. Si cette option est désélectionnée, la page est dimensionnée et centrée en fonction du coin supérieur gauche de l’objet supérieur gauche et du coin inférieur droit de l’objet inférieur droit de la page.

**Conserver les commentaires OPI :** conserve les informations requises pour remplacer une image ou un commentaire FPO (For Placement Only) par l’image haute résolution située sur les serveurs qui prennent en charge les versions 1.3 et 2.0 d’Open Prepress Interface (OPI).

**Conserver les informations sur le Document de DSC :** conserve les informations telles que le titre, la date et l’heure de création. Lorsque vous ouvrez un fichier PDF dans Acrobat, ces informations s’affichent dans le panneau de description des propriétés du document.

**Redimensionner la page et centrer l’illustration pour les fichiers EPS :** Centre une image EPS et redimensionne la page de manière à l’ajuster à l’image. Cette option concerne uniquement les travaux composés d’un seul fichier EPS.

## Options de rapport et de conformité aux normes  {#standards-reporting-and-compliance-options}

PDF Generator peut vérifier le contenu des documents d’un fichier PostScript et s’assurer ainsi qu’il réponde aux critères de la norme PDF/X-1a, PDF/X-3 ou PDF/A avant la création du fichier PDF. Pour les fichiers conformes à la norme PDF/X, vous pouvez demander que le fichier PostScript réponde à d’autres critères en sélectionnant d’autres options sous Rapport et conformité aux normes. La disponibilité des options dépend de la norme choisie.

Les fichiers conformes à la norme PDF/X sont principalement utilisés en tant que format d’échange normalisé de fichiers PDF dédiés à une impression haute résolution. A moins de créer un document PDF destiné à être imprimé, vous pouvez ignorer les normes de conformité PDF/X.

Les fichiers compatibles PDF/A sont utilisés principalement à des fins d’archivage. La conservation à long terme étant l’objectif, le document doit contenir uniquement les éléments nécessaires à l’ouverture et à l’affichage tout au long de la vie à laquelle il se destine. Par exemple les fichiers conformes à la norme PDF/A ne peuvent contenir que du texte, des images ligne par ligne et des objets vectoriels. Ils ne peuvent contenir ni chiffrement ni scripts. De plus, toutes les polices doivent être incorporées de sorte que les documents puissent être ouverts et affichés comme ils ont été créés. En d’autres termes, les documents conformes à la norme PDF/A sont *plus fins* que ceux conformes à la norme PDF/X, qui sont dédiés à une impression de pointe.

>[!NOTE]
>
>si vous avez défini un dossier de contrôle pour la création de fichiers conformes à la norme PDF/A, vérifiez que vous n’avez pas ajouté de protection à ce dossier, car la norme PDF/A n’autorise pas de chiffrement.

Pour plus d’informations sur l’accès aux options de rapport et conformité aux normes, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Norme de conformité :** sélectionnez une norme pour produire un rapport indiquant si le fichier est conforme aux exigences et, dans le cas contraire, les problèmes rencontrés. Lorsque la valeur Acrobat 4.0 est affectée au paramètre Compatibilité dans la page Paramètres généraux, toutes les options ci-dessous sont activées. Lorsque la valeur Acrobat 5.0 est affectée à l’option Compatibilité, seules les options Acrobat 5.0 peuvent être sélectionnées. Lorsqu’une autre valeur est affectée à l’option Compatibilité, les options suivantes sont inaccessibles :

* PDF/X-1a (compatible avec Acrobat 4.0)
* PDF/X-3 (compatible avec Acrobat 4.0)
* PDF/X-1a (compatible avec Acrobat 5.0)
* PDF/X-3 (compatible avec Acrobat 5.0)
* PDF/A-1b (compatible avec Acrobat 5.0)

### Options des normes PDF/X  {#options-for-pdf-x-standards}

**Lorsque cette propriété n’est pas conforme :** indique si le fichier PDF doit être créé si le fichier PostScript ne répond pas aux exigences de la norme PDF/X. Cette option est disponible si une valeur autre qu’Aucune est affectée à l’option Norme de conformité de la page Rapport et conformité aux normes.

**Continuer :** Crée un fichier PDF.

**Annuler la tâche :** crée un fichier PDF uniquement si le fichier PostScript répond aux exigences PDF/X des options de rapport sélectionnées et s’il est par ailleurs valide. Si les deux options de rapport PDF/X sont sélectionnées et que le fichier PostScript ne répond qu’à un seul jeu de critères PDF/X (par exemple, PDF/X-3), PDF Generator crée le fichier conforme.

**Si aucune zone de rognage ou zone graphique n’est spécifiée :** disponible lorsque la norme de conformité de la page Rapports des normes et conformité est définie sur une option autre qu’Aucune.

**Signaler comme erreur :** indique que le fichier PostScript n’est pas conforme si l’une des options de rapports est sélectionnée et qu’une zone de rognage ou une zone graphique est absente d’une page.

**Définir la zone de rognage sur la zone de support avec des décalages :** calcule les valeurs en points de la zone de rognage en fonction des décalages de la zone de support des pages respectives si ni la zone de rognage ni la zone graphique n’est spécifiée. La zone de rognage est toujours aussi petite ou plus petite que la zone de support qui l’entoure.

**Si la zone de fond perdu n&#39;est pas spécifiée :** disponible lorsque la norme de conformité de la page Rapports des normes et conformité est définie sur une option autre que Aucune.

**Définir la zone de fond perdu sur la zone de support :** utilise les valeurs de la zone de support pour la zone de fond perdu si la zone de fond perdu n’est pas spécifiée.

**Définir la zone de fond perdu sur la zone de rognage avec décalages :** calcule les valeurs en points de la zone de fond perdu en fonction des décalages de la zone de rognage des pages respectives si la zone de fond perdu n’est pas spécifiée. La zone de fond perdu est toujours aussi grande ou plus grande que la zone de rognage insérée.

**Valeurs par défaut si elles ne sont pas spécifiées dans le Document :** cette option est disponible lorsque la norme de conformité de la page Rapports des normes et conformité est définie sur une option autre que Aucune.

**Nom du Profil du mode de sortie :** indique la condition d’impression caractérisée pour laquelle le document est préparé. Si un document ne spécifie aucun nom de profil du mode de sortie, PDF Generator utilise la valeur sélectionnée à partir de ce menu. Vous pouvez sélectionner un des noms fournis ou saisir un nom dans l’espace prévu à cet effet. Si votre flux de travail nécessite la définition du mode de sortie, sélectionnez Aucun. Tout document ne répondant pas aux exigences ne passe pas le contrôle de conformité.

**Identifiant de condition de sortie :** indique le nom de référence spécifié par le registre du nom du profil du mode de sortie.

**Condition de sortie :** décrit la condition d’impression souhaitée. Cette entrée peut être utile au destinataire du document PDF.

**Nom du registre (URL) :** indique l’adresse Web pour plus d’informations sur le registre. L’URL est saisie automatiquement pour les noms de registre ICC.

**Recouvrement :** indique l’état du recouvrement dans le document. La conformité à la norme PDF/X requiert la valeur True ou False. Si le document ne spécifie pas l’état de recouvrement, la valeur fournie ici est utilisée. Si votre flux de travail nécessite la définition de cet état, sélectionnez Ne pas définir. Tout document ne répondant pas aux exigences ne passe pas le contrôle de conformité.

### Options de la norme PDF/A  {#options-for-pdf-a-standard}

Ces options sont activées si le paramètre Compatibilité (dans la page des paramètres généraux) est défini sur Acrobat 4 (PDF 1.3) ou Acrobat 5 (PDF 1.4).

**Lorsque cette propriété n’est pas conforme :** indique si le fichier PDF doit être créé si le fichier PostScript ne répond pas aux exigences de la norme PDF/A.

**Continuer :** Crée un fichier PDF même si le fichier PostScript ne répond pas aux exigences de la norme.

**Annuler la tâche :** crée un fichier PDF uniquement si le fichier PostScript répond aux exigences PDF/A et est par ailleurs valide.

**Nom du Profil du mode de sortie :** indique la condition d’impression caractérisée pour laquelle le document a été préparé et est requis pour la conformité à la norme PDF/A. Si votre flux de travail nécessite de connaître le mode de sortie, sélectionnez Aucun. Le document ne pourra pas vérifier la conformité si cette information n’est pas fournie.

**Condition de sortie :** décrit la condition d’impression souhaitée. Cette entrée, non obligatoire, peut être utilisée pour fournir des informations utiles au destinataire du document PDF.

## Options d’affichage initial  {#initial-view-options}

Ces options sont réparties en trois zones : Options du document, Options de fenêtre et Options de l’interface utilisateur. Pour plus d’informations sur l’accès aux options d’affichage initial, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Pour utiliser ces options, sélectionnez Définir les paramètres d’affichage initiaux.

### Options du document  {#document-options}

Les options du document contrôlent l’apparence du document au sein de la fenêtre, comme le niveau de zoom et le type de défilement.

**Afficher:** Détermine les panneaux et onglets affichés par défaut dans la fenêtre de l’application. Panneau et page Signets permet d’ouvrir le panneau du document et l’onglet Signets.

**Mise en page :** détermine si le document est affiché sur une seule page, en mode Page en vis-à-vis, Page continue ou Page en mode Page en vis-à-vis continu.

**Zoom :** définit le niveau de zoom utilisé pour afficher le document à l’ouverture. La valeur par défaut est celle configurée par l’utilisateur dans les préférences Acrobat ou Adobe Reader.

**Ouvrir au numéro de page :** Définit la page à laquelle le document s’ouvre, c’est-à-dire généralement la page 1.

>[!NOTE]
>
>les valeurs par défaut des options relatives au zoom et à la mise en page sont celles des options des utilisateurs définies dans les préférences d’affichage des pages dans Acrobat ou Adobe Reader.

### Options de fenêtre  {#window-options}

Les options suivantes déterminent la manière dont la fenêtre s’ajuste dans la zone d’écran lorsqu’un utilisateur ouvre le document. Cependant, elles ne s’appliquent pas si un PDF s’affiche dans un navigateur Web.

**Redimensionner la fenêtre en page initiale :** Ajuste la fenêtre de document pour l’ajuster en toute simplicité autour de la page d’ouverture, en fonction des options sélectionnées sous Options de Document.

**Centrer la fenêtre sur l’écran :** positionne la fenêtre au centre de la zone d’écran.

**Ouvrir en mode Plein écran :** agrandit la fenêtre du document et affiche le document sans les commandes de la barre de menus, de la barre d’outils ou de la fenêtre.

**Afficher:Nom de** fichier affiche le nom de fichier dans la barre de titre de la fenêtre. Titre du document indique le titre du document dans la barre de titre de la fenêtre.

### Options de l’interface utilisateur {#user-interface-options}

Les options de l’interface utilisateur déterminent les commandes à afficher ou à masquer lorsque l’utilisateur ouvre le document.

**Masquer la barre de menus:** Si cette option est sélectionnée, masque la barre de menus

**Masquer les barres d’outils :** si cette option est sélectionnée, les barres d’outils sont masquées.

**Masquer les commandes de fenêtre:** Si cette option est sélectionnée, masque les commandes de fenêtre

>[!NOTE]
>
>si vous masquez la barre de menus et la barre d’outils, les utilisateurs sont dans l’impossibilité d’appliquer des commandes et de sélectionner des outils à moins d’en connaître le raccourci clavier lorsqu’ils ouvrent le fichier dans Acrobat.

## Téléchargement des fichiers épilogue et prologue  {#uploading-and-downloading-prologue-and-epilogue-files}

Les fichiers prologue permettent d’ajouter du code PostScript personnalisé qui s’exécute au début de chaque tâche PostScript en cours de conversion. Les fichiers épilogue servent à ajouter du code PostScript personnalisé qui s’exécute à la fin de chaque tâche PostScript. Vous pouvez télécharger ces fichiers depuis le serveur afin de les enregistrer localement. Si vous le souhaitez, vous pouvez télécharger ces fichiers afin de les configurer indépendamment ou de les transférer vers un autre emplacement ou un autre ordinateur.

Il est possible d’utiliser ces fichiers de plusieurs manières. Par exemple, les fichiers prologue peuvent être modifiés pour définir des pages de couverture et les fichiers épilogue pour résoudre une série de procédures d’un fichier PostScript. Vous pouvez également sélectionner et télécharger des fichiers épilogue et prologue à envoyer avec chaque travail.

### Téléchargement d’un fichier prologue ou épilogue  {#download-a-prologue-or-epilogue-file}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Créer ou sur le nom d’un paramètre.
1. Cliquez sur Avancées puis, en regard de l’option Utiliser les fichiers Prologue.ps/Epilogue, cliquez sur Télécharger.
1. Dans la page Télécharger des fichiers Prologue et Epilogue, cliquez sur Prologue.ps ou Epilogue.ps, puis sur Enregistrer.

### Téléchargement d’un fichier prologue ou épilogue  {#upload-a-prologue-or-epilogue-file}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Créer ou sur le nom d’un paramètre.
1. Cliquez sur Avancées puis, en regard de l’option Utiliser les fichiers Prologue.ps/Epilogue.ps, cliquez sur Télécharger.
1. Dans la page Télécharger des fichiers Prologue et Epilogue, cliquez sur Parcourir pour sélectionner un fichier prologue ou épilogue.
1. Recherchez le fichier et cliquez sur Ouvrir.
1. Pour utiliser le fichier, assurez-vous que l’option Utiliser les fichiers Prologue.ps/Epilogue.ps est sélectionnée dans la zone Avancées de la page relative à la création ou à la modification de paramètre Adobe PDF.
1. Cliquez sur Enregistrer

>[!NOTE]
>
>PDF Generator ne prend en charge les fichiers épilogue et prologue que pour la conversion de fichiers PostScript et Postscript encapsulés en PDF.

