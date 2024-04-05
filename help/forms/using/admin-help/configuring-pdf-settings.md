---
title: Configuration des paramètres Adobe PDF
description: Découvrez comment configurer les paramètres Adobe PDF visibles sur la page Paramètres d’Adobe PDF. Vous pouvez utiliser les paramètres de PDF prédéfinis ou en créer de nouveaux.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 1bcb8429-c06e-4bd3-b422-4c512084dd09
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '7403'
ht-degree: 100%

---

# Configuration des paramètres Adobe PDF{#configuring-adobe-pdf-settings}

La page Paramètres Adobe PDF affiche les paramètres de conversion que vous pouvez spécifier pour que vos sources les utilisent. Vous pouvez utiliser les paramètres de PDF prédéfinis ou en créer de nouveaux. Les paramètres de PDF déterminent précisément le mode de conversion des fichiers, ainsi que la structure et les fonctions du PDF qui en résultent. Les paramètres Adobe PDF étaient auparavant appelés paramètres Distiller® ou options de traitement.

Sur la page Paramètres Adobe PDF, vous pouvez effectuer les tâches suivantes :

* Afficher les paramètres de PDF prédéfinis. (Voir [À propos des paramètres de PDF prédéfinis](configuring-pdf-settings.md#about-the-predefined-pdf-settings).)
* Créer un paramètre de PDF ou modifier un paramètre existant. (Voir [Ajout ou modification de paramètres de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).)
* Spécifier les paramètres de PDF par défaut. (Voir [Modification des paramètres par défaut](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings).)
* Charger un fichier de paramètres de PDF sur le serveur. (Voir [Chargement des paramètres de PDF](configuring-pdf-settings.md#upload-pdf-settings).)
* Supprimer les paramètres de PDF personnalisés. (Voir [Suppression des paramètres de PDF](configuring-pdf-settings.md#delete-pdf-settings).)
* Charger et télécharger des fichiers épilogue et prologue. (voir [Chargement et téléchargement des fichiers épilogue et prologue](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files).)

Les paramètres Adobe PDF sont applicables uniquement aux conversions basées sur PDFMaker. Il s’agit notamment des conversions suivantes :

* Document Microsoft Word (DOC, DOCX, RTF, TXT)
* Document Microsoft Excel (XLS, XLSX)
* Document Microsoft PowerPoint (PPT, PPTX)
* Document Microsoft Project (MPP)
* Document Microsoft Visio (VSD)

>[!NOTE]
>
>Lorsque vous utilisez OpenOffice pour convertir les formats ci-dessus, les paramètres Adobe PDF ne s’appliquent pas.

## À propos des paramètres de PDF prédéfinis {#about-the-predefined-pdf-settings}

PDF Generator fournit plusieurs paramètres de PDF prédéfinis. Vous ne pouvez pas modifier ces paramètres prédéfinis. Toutefois, vous pouvez créer un paramètre basé sur un paramètre existant en modifiant le paramètre et en l’enregistrant sous un nouveau nom.

**Haute qualité d’impression :** crée des fichiers PDF pour une sortie de haute qualité. Ce paramètre :

* sous-échantillonne les images en couleur et en niveaux de gris à 300 dpi ;
* sous-échantillonne les images monochromes à 1 200 dpi ;
* imprime avec une résolution d’image supérieure ;
* utilise d’autres paramètres pour conserver le maximum d’informations sur le document d’origine.

Vous pouvez ouvrir ces fichiers PDF dans Adobe Acrobat 5 et Adobe Acrobat Reader® 5 ou versions ultérieures.

**Pages surdimensionnées :** permet de créer des documents PDF adaptés à un affichage et à une impression fiables des dessins industriels dont les dimensions sont supérieures à 508 x 508 cm. Les documents PDF créés peuvent être ouverts dans Adobe Acrobat Professional, Acrobat Standard 7 ou versions ultérieures et Adobe Reader 7 ou versions ultérieures.

**PDF/A-1B 2005 CMJN/PDF/A-1B 2005 RGB :** vérifie la conformité des tâches entrantes à la norme ISO relative à la conservation à long terme (archivage) des documents électroniques et crée des fichiers PDF/A uniquement en cas de conformité. Ces fichiers sont principalement utilisés à des fins d’archivage. Les fichiers conformes ne peuvent contenir que du texte, des images pixellisées et des objets vectoriels ; ils ne peuvent pas contenir de chiffrement ni de scripts. En outre, toutes les polices doivent être incorporées afin que les documents puissent être ouverts et affichés comme ils ont été créés. PDF/A-1b utilise PDF 1.4 et convertit toutes les couleurs en CMJN ou en RGB, selon la norme choisie. Vous pouvez ouvrir les fichiers PDF créés avec ce fichier de paramètres dans Acrobat 5 et Acrobat Reader 5 et versions ultérieures. Pour plus d’informations sur PDF/A, voir Adobe et les standards du marché.

**PDF/X-1a 2001 :** vérifie la conformité des tâches entrantes à la norme PDF/X-1a et ne crée des fichiers PDF que s’ils sont conformes. PDF/X-1a est une norme ISO relative à l’échange de contenu graphique. PDF/X-1a requiert l’incorporation de toutes les polices, la définition des zones de PDF et l’affichage des couleurs en tant que couleurs CMJN ou d’accompagnement. Les fichiers PDF qui répondent aux exigences de PDF/X-1a sont ciblés sur une condition de sortie spécifique, telle que l’impression décalée web selon les spécifications des publications de décalage web. Pour plus d’informations sur PDF/X, voir Adobe et les standards du marché.

**PDF/X-3 2002 :** vérifie la conformité des travaux entrants à la norme PDF/X-3 et crée des fichiers PDF uniquement s’ils sont conformes. Tout comme PDF/X-1a, PDF/X-3 est une norme ISO relative à l’échange de contenu graphique. La principale différence est que PDF/X-3 prend en charge les couleurs indépendamment de l’appareil.

**Qualité d’impression :** crée des fichiers PDF pour une production d’impression de haute qualité (par exemple, sur une imageuse film ou une imageuse de plaques). Dans ce cas, la taille de fichier n’est pas prise en compte. L’objectif est de conserver toutes les informations du fichier PDF dont un imprimeur commercial ou un prestataire de services de prépresse a besoin pour l’imprimer correctement. Cet ensemble d’options :

* sous-échantillonne les images en couleur et en niveaux de gris à 300 dpi ;
* sous-échantillonne les images monochromes à 1 200 dpi ;
* incorpore les sous-ensembles de toutes les polices utilisées dans le document ;
* imprime avec une résolution d’image supérieure ;
* ne fait pas pivoter automatiquement les pages en fonction de l’orientation du texte ou des commentaires DSC (Document Structuring Conventions) ;
* utilise d’autres paramètres pour conserver le maximum d’informations sur le document d’origine.

Les traitements d’impression échouent s’ils incluent des polices qui ne peuvent pas être incorporées. Vous pouvez ouvrir ces fichiers PDF dans Acrobat 5 et Acrobat Reader 5 et versions ultérieures.

>[!NOTE]
>
>Avant de créer un fichier PDF à envoyer à un imprimeur commercial ou à un prestataire de services de prépresse, déterminez la résolution de sortie et d’autres paramètres, ou demandez un fichier .joboptions contenant les paramètres recommandés. Vous devrez peut-être personnaliser les paramètres Adobe PDF pour un fournisseur particulier, puis fournir votre propre fichier .joboptions.

**Taille de fichier réduite :** crée des fichiers PDF à afficher sur le Web ou sur un intranet ou à diffuser via un système de messagerie pour un affichage sur écran. Cet ensemble d’options utilise la compression, le sous-échantillonnage et une résolution d’image relativement faible. Il convertit toutes les couleurs en sRVB et n’incorpore pas les polices, sauf si nécessaire. Il optimise également les fichiers pour la diffusion d’octets. Vous pouvez ouvrir ces fichiers PDF dans Acrobat 5 et Acrobat Reader 5.0 et versions ultérieures.

**Standard :** crée des fichiers à imprimer sur des imprimantes de bureau ou des copieurs numériques, à publier sur CD ou à envoyer à un client comme preuve de publication. Cet ensemble d’options utilise la compression et le sous-échantillonnage pour réduire la taille du fichier. Il incorpore également les sous-ensembles de toutes les polices utilisées dans le fichier, convertit toutes les couleurs en sRVB et imprime à une résolution moyenne afin de créer un rendu raisonnablement précis du document d’origine. Notez que les sous-ensembles de polices Microsoft Windows ne sont pas incorporés par défaut. Vous pouvez ouvrir ces fichiers PDF dans Acrobat 5 et Acrobat Reader 5.0 et versions ultérieures.

## Ajout ou modification de paramètres de PDF {#add-or-edit-pdf-settings}

Les paramètres de PDF déterminent précisément le mode de conversion des fichiers, ainsi que la structure et les fonctions du PDF qui en résultent. Définissez un nouveau paramètre de PDF ou modifiez un paramètre existant. Vous ne pouvez pas modifier des paramètres prédéfinis. Toutefois, vous pouvez créer un paramètre basé sur un paramètre existant en le modifiant et en l’enregistrant sous un nouveau nom.

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Nouveau ou sur le nom d’un paramètre.
1. Sur la page Nouveau/Modifier le paramètre Adobe PDF, renseignez les informations requises dans les sections suivantes :

[Options générales](configuring-pdf-settings.md#general-options)

[Options relatives aux images](configuring-pdf-settings.md#images-options)

[Options relatives aux polices](configuring-pdf-settings.md#fonts-options)

[Options relatives aux couleurs](configuring-pdf-settings.md#color-options)

[Options avancées](configuring-pdf-settings.md#advanced-options)

[Options de rapport et de conformité aux normes](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

[Options d’affichage initial](configuring-pdf-settings.md#initial-view-options)

   Pour accéder à une autre section, cliquez sur son lien sur la page web ou utilisez les boutons Suivant ou Précédent.

1. Après avoir renseigné les informations dans toutes les sections, cliquez sur Enregistrer ou Enregistrer sous et saisissez le nom du paramètre.

## Chargement de paramètres de PDF {#upload-pdf-settings}

Vous pouvez rendre les paramètres de PDF disponibles sur le serveur PDF Generator en les chargeant depuis un ordinateur local ou un emplacement réseau.

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Paramètres Adobe PDF, puis cliquez sur Charger.
1. Sur la page Charger les paramètres Adobe PDF, cliquez sur Parcourir, recherchez le fichier de paramètres de PDF, puis cliquez sur Ouvrir.
1. Cliquez sur OK, puis de nouveau sur OK.

## Suppression de paramètres de PDF {#delete-pdf-settings}

Vous pouvez supprimer définitivement les paramètres de PDF si vous n’en avez plus besoin.

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cochez la case en regard du paramètre à supprimer. Vous pouvez sélectionner plusieurs paramètres.
1. Cliquez sur Supprimer, puis, sur la page Confirmation de suppression, cliquez à nouveau sur Supprimer.

## Options générales {#general-options}

Utilisez les options générales pour spécifier la version d’Acrobat à utiliser pour la compatibilité des fichiers et d’autres options de fichier et d’appareil. Pour plus d’informations sur l’accès aux options générales, voir [Ajout ou modification de paramètres de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Options de fichier {#file-options}

**Compatibilité :** niveau de compatibilité du fichier PDF. Pour les documents qui seront largement distribués, pensez à sélectionner Acrobat 4 (PDF 1.3) ou Acrobat 5 (PDF 1.4) pour vous assurer que tous les utilisateurs et utilisatrices peuvent afficher et imprimer le document. Si vous créez des fichiers en utilisant la compatibilité Acrobat 5 ou versions ultérieures, ils peuvent ne pas être compatibles avec les versions antérieures d’Acrobat. Les sous-sections suivantes présentent les différences entre les fichiers PDF créés à l’aide de différents niveaux de compatibilité Acrobat.

<table>
 <tbody>
  <tr>
   <th><p>Acrobat 4 (PDF 1.3)</p> </th>
   <th><p>Acrobat  5 (PDF 1.4)</p> </th>
   <th><p>Acrobat 6 (PDF 1.5)</p> </th>
   <th><p>Acrobat 7 (PDF 1.6) et Acrobat 8 (PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>Peut être ouvert avec Acrobat 3.0 et Acrobat Reader 3.0 et versions ultérieures.</p> </td>
   <td><p>Peut être ouvert avec Acrobat 3.0 et Acrobat Reader 3.0 et versions ultérieures. Les fonctionnalités spécifiques aux versions ultérieures peuvent être perdues ou non visibles.</p> </td>
   <td><p>La plupart peuvent être ouvertes avec Acrobat 4 et Acrobat Reader 4.0 et versions ultérieures. Les fonctionnalités spécifiques aux versions ultérieures peuvent être perdues ou non visibles.</p> </td>
   <td><p>La plupart peuvent être ouvertes avec Acrobat 4 et Acrobat Reader 4.0 et versions ultérieures. Les fonctionnalités spécifiques aux versions ultérieures peuvent être perdues ou non visibles.</p> </td>
  </tr>
  <tr>
   <td><p>Ne peut pas contenir d’illustrations qui utilisent des effets de transparence en direct. Toute transparence doit être aplatie avant la conversion en PDF 1.3.</p> </td>
   <td><p>Prend en charge l’utilisation de la transparence dynamique dans les illustrations. (La fonction Acrobat Distiller aplatit la transparence.)</p> </td>
   <td><p>Prend en charge l’utilisation de la transparence dynamique dans les illustrations. (La fonction Acrobat Distiller aplatit la transparence.)</p> </td>
   <td><p>Prend en charge l’utilisation de la transparence dynamique dans les illustrations. (La fonction Acrobat Distiller aplatit la transparence.)</p> </td>
  </tr>
  <tr>
   <td><p>Les calques ne sont pas pris en charge.</p> </td>
   <td><p>Les calques ne sont pas pris en charge.</p> </td>
   <td><p>Permet de conserver les calques lors de la création de fichiers PDF à partir d’applications qui prennent en charge la génération de documents PDF superposés, comme Adobe Illustrator® CS ou Adobe InDesign® CS et versions ultérieures.</p> </td>
   <td><p>Permet de conserver les calques lors de la création de fichiers PDF à partir d’applications qui prennent en charge la génération de documents PDF superposés, comme Illustrator CS ou InDesign CS et versions ultérieures.</p> </td>
  </tr>
  <tr>
   <td><p>L’espace colorimétrique DeviceN avec 8 colorants est pris en charge.</p> </td>
   <td><p>L’espace colorimétrique DeviceN avec 8 colorants est pris en charge.</p> </td>
   <td><p>L’espace colorimétrique DeviceN avec un maximum de 31 colorants est pris en charge.</p> </td>
   <td><p>L’espace colorimétrique DeviceN avec un maximum de 31 colorants est pris en charge.</p> </td>
  </tr>
  <tr>
   <td><p>Les polices multi-octets peuvent être incorporées. (Distiller convertit les polices lors de l’incorporation.)</p> </td>
   <td><p>Les polices multi-octets peuvent être incorporées.</p> </td>
   <td><p>Les polices multi-octets peuvent être incorporées.</p> </td>
   <td><p>Les polices multi-octets peuvent être incorporées.</p> </td>
  </tr>
  <tr>
   <td><p>La sécurité RC4 40 bits est prise en charge.</p> </td>
   <td><p>La sécurité RC4 128 bits est prise en charge.</p> </td>
   <td><p>La sécurité RC4 128 bits est prise en charge.</p> </td>
   <td><p>La sécurité RC4 128 bits et AES (Advanced Encryption Standard) 128 bits est prise en charge.</p> </td>
  </tr>
 </tbody>
</table>

**Niveau de compression de l’objet :** permet de consolider les petits objets (lesquels ne sont eux-mêmes plus compressibles) en flux qu’il est possible de compresser efficacement.

**Off :** permet de ne pas compresser les informations relatives à la structure du document PDF. Sélectionnez cette option si vous souhaitez que les utilisateurs affichent, naviguent et interagissent avec des signets et d’autres informations structurelles à l’aide d’Acrobat 5 et versions ultérieures.

**Balises seules :** permet de compresser les informations structurelles du document PDF. Cette option génère un fichier de PDF qui peut être ouvert et imprimé à l’aide d’Acrobat 5. Les utilisateurs et utilisatrices ne peuvent pas afficher d’informations d’accessibilité, de structure ou de PDF balisé dans Acrobat 5 ou Acrobat Reader 5.0, mais ils peuvent afficher ces informations dans Acrobat 6 et Adobe Reader 6.0.

**Auto-rotation des pages :** permet de définir la rotation automatique des pages en fonction de l’orientation du texte ou des commentaires DSC. Par exemple, certaines pages (telles que les pages qui contiennent des tableaux) peuvent nécessiter que l’utilisateur ou l’utilisatrice les fasse pivoter pour les lire. Sélectionnez Individuellement pour faire pivoter chaque page en fonction de l’orientation du texte sur cette page. Sélectionnez Collectivement par fichier pour faire pivoter toutes les pages du document en fonction de l’orientation de la plupart du texte.

>[!NOTE]
>
>Si vous avez sélectionné Traiter les commentaires DSC dans les paramètres avancés et si %%des commentaires d’orientation d’affichage sont inclus, ces commentaires sont prioritaires pour déterminer l’orientation de la page.

**Lier :** permet de définir si le fichier PDF doit être affiché avec une liaison à gauche ou à droite. Ce paramètre modifie l’affichage des pages en mise en page Continue-Page double et l’affichage des miniatures côte à côte.

**Résolution :** permet de définir l’émulation de la résolution d’une imprimante pour les fichiers d’entrée qui ajustent leur comportement en fonction de la résolution de l’imprimante vers laquelle ils envoient l’impression. Pour la plupart des fichiers d’entrée, un paramètre de résolution plus élevé génère des fichiers PDF de plus grande taille mais de meilleure qualité, et un paramètre plus faible génère des fichiers PDF de plus faible qualité. La résolution détermine généralement le nombre d’étapes d’un dégradé ou d’une fusion. Vous pouvez saisir une valeur comprise entre 72 et 4 000. Conservez ce paramètre comme valeur par défaut, sauf si vous envisagez d’imprimer le fichier PDF sur une imprimante spécifique et que vous souhaitez émuler la résolution définie dans le fichier d’entrée d’origine.

>[!NOTE]
>
>L’augmentation du paramètre de résolution augmente la taille du fichier et peut légèrement accroître le temps nécessaire au traitement de certains fichiers.

**Toutes les pages ou Pages de :** indique les pages à convertir. Ne renseignez pas la zone A afin de créer une plage comprise entre le numéro de page entré dans la zone De et la fin du fichier.

**Optimiser pour l’affichage web rapide :** Restructure le fichier pour le téléchargement page par page (service d’octets) à partir des serveurs web. Cette option compresse le texte et les dessins au trait, quels que soient les paramètres de compression sélectionnés dans l’onglet Images. La compression se traduit par un accès et un affichage plus rapides lors du téléchargement du fichier à partir du web ou d’un réseau. Cette option est désactivée par défaut.

### Taille de page par défaut {#default-page-size}

Les options Taille de page par défaut définissent la taille de page à utiliser lorsqu’elle n’est pas spécifiée dans le fichier d’origine. En règle générale, les fichiers Adobe PostScript incluent ces informations, à l’exception des fichiers EPS (Encapsulated PostScript), qui indiquent une taille de cadre mais pas une taille de page. La taille de page maximale autorisée est de 15 000 000 pouces (31 800 000 cm) dans les deux sens. Ces options permettent de configurer la taille de page par défaut :

**Largeur :** largeur de la page

**Hauteur :** hauteur de la page

**Unités :** unités de mesure à utiliser pour les paramètres de largeur et de hauteur

## Options Images {#images-options}

Les options Images permettent de définir la compression et le rééchantillonnage des images. Vous pouvez tester ces options pour trouver un équilibre approprié entre la taille du fichier et la qualité de l’image. Pour plus d’informations sur l’accès aux paramètres des images, voir [Ajout ou modification de paramètres de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Ces options permettent de configurer les images monochromes, en niveaux de gris et en couleur :

**Sous-échantillon :** définit une valeur pour chaque type d’image. Pour sous-échantillonner des images monochromes, en niveaux de gris ou en couleur, PDF Generator associe les pixels dans une zone d’échantillonnage afin d’obtenir un plus grand pixel. Indiquez la résolution de votre appareil de sortie en dpi et saisissez une résolution en dpi dans la zone Pour les images au-dessus de. Pour les images dont la résolution est supérieure à ce seuil, PDF Generator combine les pixels, si nécessaire, afin de réduire la résolution de l’image (pixels par pouce) au paramètre de ppp spécifié. Pour désactiver le sous-échantillonnage, sélectionnez Désactivé. Les options suivantes sont disponibles :

**Sous-échantillonage moyen :** établit la moyenne des pixels dans une zone d’échantillonnage et remplace l’ensemble de la zone par la couleur du pixel moyen à la résolution définie.

**Sous-échantillonage bicubique :** utilise une moyenne pondérée pour déterminer la couleur de pixel et offre généralement de meilleurs résultats que ceux de la méthode de sous-échantillonnage moyen. La méthode bicubique est la plus lente, mais également la plus précise et est celle qui offre les dégradés de tons les plus lisses.

**Sous-échantilloner à :** sélectionne un pixel au centre de la zone d’échantillonnage et remplace l’ensemble de la zone par ce pixel à la résolution définie. Le sous-échantillonnage réduit considérablement le temps de conversion par rapport à l’échantillonnage classique, mais il produit également des images moins lisses et continues.

Le paramètre de résolution pour la couleur et les niveaux de gris doit être 1,5 à 2 fois le lignage de trame auquel le fichier doit être imprimé. (À condition que vous n’alliez pas au-dessous de ce paramètre de résolution recommandé, les images ne contenant aucune ligne droite, aucun schéma géométrique ou aucun schéma répété ne sont pas affectées par une résolution plus faible.) La résolution des images monochromes doit être identique à celle du périphérique de sortie. Toutefois, le fait d’enregistrer une image monochrome à une résolution supérieure à 1 500 dpi augmente la taille du fichier sans améliorer significativement la qualité de l’image.

Déterminez également si les utilisateurs et utilisatrices doivent agrandir une page. Par exemple, si vous créez un document PDF d’une carte, envisagez d’utiliser une résolution d’image plus élevée afin que les utilisateurs et utilisatrices puissent zoomer sur cette carte.

>[!NOTE]
>
>Le rééchantillonnage d’images monochromes peut avoir des effets inattendus, comme l’affichage d’aucune image. Si tel est le cas, désactivez le rééchantillonnage et convertissez de nouveau le fichier. Ce problème est davantage susceptible de survenir au cours d’un sous-échantillonnage, alors que c’est au cours du sous-échantillonnage bicubique qu’il est le moins fréquent.

Ce tableau répertorie les types d’imprimantes courants ainsi que leur résolution mesurée en dpi, leur linéature de trame par défaut mesurée en lpi, et une résolution de rééchantillonnage des images mesurées en ppi. Par exemple, pour imprimer sur une imprimante laser de 600 dpi, saisissez 170 comme résolution de rééchantillonnage des images.

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
   <td><p>120 ppp</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi (imprimante laser)</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppp</p> </td>
  </tr>
  <tr>
   <td><p>1 200 dpi (imageuse film)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppp</p> </td>
  </tr>
  <tr>
   <td><p>2 400 dpi (imageuse film)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppp</p> </td>
  </tr>
 </tbody>
</table>

**Compression :** définit une valeur à appliquer aux images monochromes, à niveaux de gris et en couleur. Pour les images en niveaux de gris et en couleur, définissez également la qualité de l’image :

* Pour les images en niveaux de gris ou en couleur, sélectionnez ZIP pour appliquer une compression qui fonctionne bien sur les images avec des grandes zones de couleurs uniques ou de motifs répétés. Ces images peuvent être des captures d’écran, des images simples créées à l’aide de programmes de dessin et des images monochromes contenant des motifs répétés. Sélectionnez JPEG, qualité minimale à maximale, pour appliquer une compression adaptée aux images en niveaux de gris ou en couleur, comme les photographies en demi-teinte, qui contiennent davantage de détails reproductibles à l’écran ou sur papier. Sélectionnez Automatique (JPEG) pour déterminer automatiquement la meilleure qualité pour les images en niveaux de gris et en couleur.
* Pour les images monochromes, sélectionnez la compression CCITT Group 4, CCITT Group 3, ZIP, JPEG200, automatique (JPEG2000) ou Run Length.

Assurez-vous que les images monochromes sont numérisées en monochrome et non en niveaux de gris. Par défaut, le texte numérisé est parfois enregistré en tant qu’images en niveaux de gris. Le texte en niveaux de gris compressé à l’aide de la méthode de compression JPEG n’est pas clair et peut être illisible.

**Qualité d’image :** configure la qualité de l’image pour les images à niveaux de gris et en couleur. Les options disponibles sont Minimale, Faible, Moyenne, Elevée et Maximale.

**Anti-alias à gris :** lisse les bords dentés des images monochromes. Sélectionnez 2 bits, 4 bits ou 8 bits pour définir 4, 16 ou 256 niveaux de gris. (Le lissage peut donner un aspect flou aux petits motifs ou aux lignes fines).

>[!NOTE]
>
>La compression du texte et des dessins au trait est toujours activée.

**Politique d’image :** définit une politique pour les images monochromes, à niveaux de gris et en couleur. Si la résolution de l’image est inférieure à la résolution spécifiée, vous pouvez toujours sélectionner Ignorer pour poursuivre, envoyer un message d’avertissement ou annuler le traitement.

## Options relatives aux polices {#fonts-options}

Les options relatives aux polices permettent de définir les polices à incorporer dans un fichier PDF et d’incorporer un sous-ensemble de caractères utilisé dans ce PDF. Pour plus d’informations sur l’accès aux options relatives aux polices, voir [Ajout ou modification de paramètres de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>Lorsque vous combinez des fichiers PDF avec le même sous-ensemble de polices, PDF Generator tente de combiner les sous-ensembles de polices.

**Intégrer toutes les polices :** intègre toutes les polices utilisées dans le fichier. L’incorporation des polices est nécessaire à la conformité avec la norme PDF/X.

**Jeux partiels de polices incorporées lorsque le pourcentage de caractères utilisés est inférieur à :** si vous sélectionnez cette option, indiquez un pourcentage seuil pour intégrer uniquement un sous-ensemble de polices. Par exemple, si le seuil est de 35 et que moins de 35 % des caractères sont utilisés, PDF Generator incorpore uniquement ces caractères. Seules les polices avec des bits d’autorisation appropriés sont incorporées.

**Lorsque l’incorporation échoue :** définit la manière dont PDF Generator doit répondre s’il ne parvient pas à trouver une police à incorporer lors du traitement d’un fichier. Vous pouvez demander à PDF Generator d’ignorer la demande et de remplacer la police, de vous avertir et de remplacer la police ou d’annuler le traitement du travail en cours.

**Emplacement des polices :** emplacement des polices que PDF Generator utilise.

### Spécifier les polices à incorporer {#specify-which-fonts-to-embed}

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Nouveau ou sur le nom d’un paramètre.
1. Cliquez sur Polices et désélectionnez l’option Incorporer toutes les polices.
1. Dans la liste Source des polices, sélectionnez une source de police, puis cliquez sur Atteindre pour actualiser la liste des polices dans la zone située sur le côté gauche.
1. Cliquez sur une police dans la zone située à gauche. Cliquez ensuite sur Ajouter en regard de la zone appropriée pour la déplacer vers la liste Toujours incorporer ou Ne jamais incorporer. Répétez l’opération pour chaque police. Maintenez la touche Ctrl enfoncée tout en cliquant sur la souris pour sélectionner plusieurs polices à déplacer.
1. Pour supprimer une police de la liste Toujours incorporer ou Ne jamais incorporer, sélectionnez-la et cliquez sur Supprimer en regard de la case voulue. Par cette action, vous ne supprimez pas la police de votre système, mais vous supprimez uniquement la référence de celle-ci dans la liste.
1. Si la police à définir n’est pas affichée, tapez son nom dans la zone Ajouter une police, puis cliquez sur Toujours incorporer ou Ne jamais incorporer. Les noms de police ne peuvent pas contenir de caractères alphanumériques.

>[!NOTE]
>
>Une police TrueType peut contenir un paramètre (ajouté par le concepteur de cette police) l’empêchant d’être incorporée dans des fichiers PDF.

>[!NOTE]
>
>Les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client ou de la cliente, assurez-vous de redémarrer le système sur lequel AEM forms est installé.

## Options relatives aux couleurs {#color-options}

Ces options permettent de définir les informations sur la gestion des couleurs pour PDF Generator. Pour plus d’informations sur l’accès aux options relatives aux couleurs, voir [Ajouter ou modifier les paramètres de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Paramètres Adobe Color {#adobe-color-settings}

**Fichier de configuration :** cette liste répertorie les paramètres de couleur également utilisés dans la plupart des applications graphiques telles qu’ Adobe Photoshop et Adobe Illustrator. Le paramètre de couleur sélectionné détermine les autres paramètres Adobe Color de cette page. Par exemple, si vous sélectionnez un paramètre autre qu’Aucune, tous les paramètres autres que ceux relatifs à Données dépendantes du périphérique sont prédéfinis et provisoirement inaccessibles. Vous pouvez modifier les paramètres Politiques de gestion des couleurs et Espaces de travail seulement si vous avez sélectionné Aucune pour Fichier de paramètres.

### Politiques de gestion des couleurs {#color-management-policies}

Si vous avez sélectionné Aucune pour Fichier de paramètres, la zone Politiques de gestion des couleurs indique la manière dont PDF Generator convertit les couleurs non gérées d’un fichier PostScript.

**Laisser la couleur inchangée :** ne modifie pas les couleurs dépendantes de l’appareil et conserve les couleurs de référence de sorte qu’elles restent le plus proche possible de leur équivalent en PDF. Cette option s’avère utile pour les ateliers d’impression ayant étalonné l’ensemble de leurs appareils, ayant utilisé ces informations pour définir les couleurs du fichier et qui impriment uniquement sur ces appareils.

**Tout baliser pour Color Management :** incorpore un profil ICC lors de la conversion des fichiers et calibre la couleur des images pour rendre les couleurs des fichiers PDF obtenus indépendantes des appareils si vous avez sélectionné la compatibilité Acrobat 4 (PDF 1.3) ou versions ultérieures. Cependant, les espaces colorimétriques dépendants de l’appareil des fichiers (RVB, Niveaux de gris et CMJN) sont convertis en espaces colorimétriques de référence (CalRVB, CalGray et LAB).

**Ne baliser que les images pour Color Management :** incorpore des profils ICC dans les images uniquement et non dans les textes ou les graphiques lors de la conversion des fichiers si vous avez sélectionné la compatibilité Acrobat 4 (PDF 1.3). Cette option empêche le texte noir de subir une variation chromatique. Cependant, les espaces colorimétriques dépendants du périphérique des images (RVB, Niveaux de gris et CMJN) sont convertis en espaces colorimétriques de référence (CalRVB, CalGray et LAB). Le texte et les graphiques ne sont pas convertis.

**Convertit toutes les couleurs en sRGB ou Convertir toutes les couleurs en 
CMJN :** calibre la couleur du fichier en la rendant indépendante de l’appareil, comme pour l’option Baliser tout pour Color Management. Si vous avez sélectionné la compatibilité Acrobat 4 (PDF 1.3) ou version ultérieure et que vous effectuez une conversion en sRVB, les images CMJN et RGB sont converties en sRVB.

Quelle que soit l’option de compatibilité choisie, les images en niveaux de gris ne sont pas modifiées. Cela entraîne habituellement une réduction du volume et une augmentation de la vitesse d’affichage des fichiers PDF, car la description des images RVB nécessite une quantité d’informations moins importante que celle des images CMJN. RVB est l’espace colorimétrique natif utilisé sur les écrans, c’est pourquoi aucune conversion de la couleur n’est nécessaire lors de l’affichage, ce qui contribue à accélérer l’affichage en ligne. Cette option est recommandée si le fichier PDF est utilisé en ligne ou avec des imprimantes à faible résolution.

**Mode de génération du document :** méthode de mappage des couleurs entre les espaces colorimétriques. Quelle que soit la méthode, son résultat dépend des profils des espaces colorimétriques. Par exemple, certains profils donnent des résultats identiques avec des méthodes différentes. Voici les options de disponibles :

>[!NOTE]
>
>dans tous les cas, il est possible d’ignorer ou de remplacer les modes par des opérations de gestion des couleurs qui surviennent après la création du fichier PDF.

**Conserver :** signifie que l’intention est spécifiée dans l’appareil de sortie plutôt que dans le fichier PDF. Dans de nombreux appareils de sortie, Colorimétrie relative est le mode par défaut.

**Perception :** maintient les valeurs de couleur relatives entre les pixels d’origine lorsqu’ils sont mappés à la gamme de destination. Cette méthode donne la possibilité de conserver la relation visuelle entre les couleurs, bien que les valeurs des couleurs elles-mêmes puissent changer.

**Saturation :** maintient les valeurs de saturation relatives des pixels d’origine. Cette méthode est adaptée aux graphiques d’entreprise, pour lesquels la relation exacte entre les couleurs n’est pas aussi importante que le fait d’avoir des couleurs saturées éclatantes.

**Colorimétrie relative :** permet de remapper le point blanc de l’espace source avec celui de l’espace de destination.

**Colorimétrie absolue :** désactive la correspondance des points blanc et noir lors de la conversion des couleurs. Cette méthode n’est pas recommandée à moins que vous ne deviez conserver les couleurs de signature, telles que celles utilisées dans les marques et les logos.

### Espaces de travail {#working-spaces}

Pour l’ensemble des valeurs de la liste se trouvant sous Politiques de gestion des couleurs, autres que Reproduire les couleurs, sélectionnez les options répertoriées dans les listes situées dans la zone Espace de travail afin de spécifier les profils ICC à utiliser pour la définition et l’étalonnage des espaces colorimétriques en niveaux de gris, RVB et CMJN des fichiers PDF convertis. Voici les options de disponibles :

**Gris :** définit l’espace colorimétrique de toutes les images en niveaux de gris des fichiers. Cette option est disponible uniquement si vous choisissez Référencer les couleurs ou Référencer les images uniquement. Le profil ICC par défaut pour les images en niveaux de gris est Gamma gris 2.2. Vous pouvez également sélectionner Aucun pour empêcher la conversion des images en niveaux de gris.

**RVB :** définit l’espace colorimétrique de toutes les images en RVB des fichiers. La valeur par défaut sRVB IEC61966-2.1 est généralement recommandée, car ce standard est en passe de devenir la référence et de nombreux périphériques de sortie le prennent en charge. Vous pouvez également sélectionner Aucun pour empêcher la conversion des images en RVB.

**CMJN :** définit l’espace colorimétrique de toutes les images en CMJN des fichiers. La valeur par défaut est U.S. Web Coated (SWOP) v2. Vous pouvez également sélectionner Aucun pour empêcher la conversion des images en CMJN.

>[!NOTE]
>
>Sélectionner Aucun pour les trois espaces de travail revient à sélectionner Reproduire les couleurs.

**Conserver les valeurs CMYK pour les espaces couleur CMYK calibrés :** lorsque cette option est sélectionnée, les valeurs CMJN indépendantes de l’appareil sont traitées comme des valeurs dépendantes de l’appareil (DeviceCMYK), les espaces couleur indépendants de l’appareil sont ignorés et les fichiers PDF/X-1a utilisent la valeur Convertir toutes les couleurs en CMJN. Si cette option est désélectionnée, les espaces colorimétriques indépendants de l’appareil sont convertis en CMJN si la politiques de gestion des couleurs est définie sur Convertir toutes les couleurs en CMJN.

### Données dépendantes de l’appareil {#device-dependent-data}

Ces options s’appliquent si vous travaillez avec des documents créés à l’aide d’applications graphiques ou de documentation de pointe, telles qu’Adobe Illustrator et Adobe InDesign. Pour plus d’informations, consultez la documentation fournie avec l’application.

Les fonctions de transfert sont utilisées pour obtenir un effet artistique et pour s’adapter aux spécifications d’un périphérique de sortie spécifique. Par exemple, un fichier destiné à une impression sur une imageuse film spécifique peut contenir des fonctions de transfert qui compensent l’élargissement du point inhérent à cette imprimante.

**Conserver les paramètres UCR/densité de noir :** conserve ces paramètres s’ils existent dans le fichier PostScript. Densité de noir calcule la quantité de noir à utiliser lors de la tentative de reproduction d’une couleur spécifique. UCR réduit la quantité de composants cyan, magenta et jaune pour compenser la quantité de noir ajoutée par le paramètre densité de noir. En raison d’une quantité d’encre utilisée moins importante, le paramètre UCR est généralement utilisé pour l’impression sur papier journal et papier non couché.

**Lorsque des Fonctions de transfert sont trouvées :** détermine ce qu’il faut faire lorsque des fonctions de transfert sont trouvées :

**Conserver :** permet de conserver les fonctions de transfert qui sont traditionnellement utilisées pour compenser l’élargissement ou le rétrécissement de points qui peuvent se produire lors du transfert d’une image sur un film. L’élargissement du point survient lorsque les points d’encre dont une page imprimée est composée sont plus grands que sur la trame de similigravure (par exemple, en raison de l’étalement sur le papier). Par contre, le rétrécissement du point survient lorsque les points s’impriment en plus petit. Grâce à cette option, les fonctions de transfert sont conservées dans le fichier et appliquées à ce dernier lors de son impression.

**Appliquer :** permet de ne pas conserver la fonction de transfert, mais l’applique au fichier, pour en modifier les couleurs. Cette option est utile pour créer des effets de couleur dans un fichier. Par défaut, cette option est sélectionnée pour les nouveaux paramètres.

**Supprimer :** supprime toutes les fonctions de transfert appliquées. Supprimez ces fonctions de transfert sauf si le fichier PDF est imprimé sur le même appareil que celui pour lequel le fichier PostScript source a été créé.

**Conserver les informations de demi-teinte :** permet de conserver toutes les informations sur les demi-teintes des fichiers. Les informations sur les demi-teintes consistent en des points qui contrôlent la quantité d’encre déposée par les périphériques d’impression en demi-teinte à un emplacement spécifique sur le papier. En faisant varier la densité et la grandeur du point, on crée l’illusion de variations de gris ou d’une couleur continue. Pour une image en CMJN, quatre trames de similigravure sont utilisées, c’est-à-dire une pour chaque encre utilisée dans le processus d’impression.

En imprimerie traditionnelle, une demi-teinte est obtenue en plaçant une trame de similigravure entre un film et l’image, puis en exposant le film. Les équivalents électroniques, comme dans Adobe Photoshop, permettent aux utilisateurs et utilisatrices de définir les attributs de la trame de similigravure avant d’imprimer le film ou le papier. Les informations sur les demi-teintes sont destinées à être utilisées avec un périphérique de sortie particulier.

## Options avancées {#advanced-options}

Les options avancées spécifient les commentaires DSC (Document Structure Conventions) à conserver dans le fichier PDF et comment définir d’autres options qui affectent la conversion à partir de PostScript. Dans un fichier PostScript, les commentaires DSC contiennent des informations sur le fichier (telles que l’application d’origine, la date de création et l’orientation de page). Ils fournissent également une structure pour les descriptions de page dans le fichier (comme les instructions de début et de fin pour une section de prologue). Les commentaires DSC peuvent être utiles lorsque votre document est destiné à l’impression ou à la presse. Pour plus d’informations sur l’accès aux options avancées, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Lorsque vous utilisez les options avancées, il est utile de connaître le langage PostScript et la manière dont il est traduit en PDF. (Voir [Adobe PostScript 3](https://www.adobe.com/fr/products/postscript.html).)

**Permettre au fichier PostScript d’ignorer les paramètres Adobe PDF :** permet d’utiliser les paramètres stockés dans un fichier PostScript plutôt que dans le fichier des paramètres Adobe PDF actuel. Avant de traiter un fichier PostScript, vous pouvez y placer des paramètres afin de contrôler les aspects suivants :

* Compression de texte et de graphiques.
* Sous-échantillonnage et codage des images échantillonnées.
* Incorporation de polices Type 1 et d’instances de polices Type 1 Multiple Master.

**Autoriser les XObjects au format PostScript :** les XObjects au format PostScript permettent de stocker les informations qui apparaissent sur de nombreuses pages du même fichier, comme une image en arrière-plan ou les informations relatives à l’en-tête ou au pied de page. L’utilisation de XObjects au format PostScript peut entraîner une impression plus rapide, mais nécessite davantage de mémoire d’imprimante. Pour empêcher la création de XObjects au format PostScript, désélectionnez cette option si vous créez des fichiers PDF avec une compatibilité Acrobat 5 (PDF 1.4) ou ultérieure.

**Convertir les dégradés en ombres lissées :** permet de convertir des dégradés en ombres lissées pour Acrobat 4 et versions ultérieures en réduisant les fichiers PDF et en améliorant potentiellement la qualité de l’impression finale. PDF Generator convertit les dégradés issus d’Adobe Illustrator, Adobe InDesign, Adobe Freehand MX, CorelDraw, Quark Xpress et Microsoft PowerPoint.

**Convertir les traits lissés en courbes :** permet de réduire le nombre de points de contrôle utilisés pour créer des courbes dans des dessins CAO, ce qui entraîne une réduction de la taille des fichiers PDF et une accélération du rendu à l’écran.

**Conserver la sémantique copypage Niveau 2 :** permet d’utiliser l’opérateur copypage défini dans LanguageLevel 2 PostScript au lieu de celui de LanguageLevel 3 PostScript. Si vous disposez d’un fichier PostScript et que vous sélectionnez cette option, un opérateur copypage copie la page. Si cette option n’est pas sélectionnée, l’équivalent d’une opération showpage est exécuté, mais l’état du graphique n’est pas réinitialisé.

**Conserver les paramètres de surimpression :** permet de conserver les paramètres de surimpression dans les fichiers convertis en PDF. Les couleurs surimprimées consistent en deux encres ou plus imprimées l’une sur l’autre. Par exemple, lorsqu’une encre cyan s’imprime sur une encre jaune, la surimpression qui en résulte est de couleur verte. Sans surimpression, le jaune sous-jacent ne serait pas imprimé, ce qui donnerait une couleur cyan.

**Surimprimer des objets non nuls par défaut :** permet d’empêcher les objets surimprimés dont les valeurs CMJN sont nulles d’éliminer les objets CMJN sous-jacents. Pour ce faire, il suffit d’insérer le paramètre d’état d’image OPM 1 dans le fichier PDF partout où Setoverprint est présent.

**Enregistrer les paramètres Adobe PDF dans le fichier PDF :** permet d’incorporer le fichier de paramètres utilisé pour créer le fichier PDF. Vous pouvez ouvrir et afficher le fichier de paramètres (qui a une extension de nom de fichier .joboptions) dans la boîte de dialogue Pièces jointes dans Acrobat. Le fichier de paramètres Adobe PDF devient un élément de l’arborescence EmbeddedFiles dans le fichier PDF.

**Enregistrer les images au format JPEG dans le fichier PDF (si possible) :** permet de traiter les images compressées au format JPEG (images déjà compressées à l’aide de l’encodage DCT) sans avoir à les compresser de nouveau. Si cette option est sélectionnée, PDF Generator décompresse les images du JPEG pour s’assurer qu’elles ne sont pas corrompues. Toutefois, il ne recompresse pas les images valides, ce qui rend l’image d’origine intacte. Lorsque cette option est sélectionnée, les performances s’améliorent, car seule la décompression (et non la recompression) se produit, et les données et métadonnées d’image sont conservées.

**Enregistrer le dossier de correspondance dans le fichier PDF :** permet de conserver un dossier de correspondance PostScript dans un fichier PDF. Le dossier de correspondance contient des informations relatives au fichier PostScript, telles que le format de page, la résolution et des informations de recouvrement, plutôt que les informations sur le contenu. Ces informations peuvent être utilisées ultérieurement dans un workflow ou pour imprimer le PDF.

**Utiliser les fichiers Prologue.ps/Epilogue.ps :** permet d’envoyer un fichier prologue et épilogue avec chaque traitement. Ces fichiers ont de nombreux usages. Par exemple, les fichiers prologue peuvent être modifiés pour définir des pages de couverture. Les fichiers épilogue peuvent être modifiés pour résoudre une série de procédures d’un fichier PostScript. Vous pouvez charger ou télécharger les fichiers. (voir Téléchargement des fichiers épilogue et prologue).

**Traiter les commentaires DSC :** permet de gérer les informations d’un fichier PostScript. Les sous-options disponibles sont les suivantes :

**Enregistrer les avertissements DSC :** permet d’afficher des messages d’avertissement relatifs à des commentaires DSC posant problème lors du traitement et de les ajouter à un fichier journal.

**Préserver les informations EPS des commentaires DSC :** permet de conserver des informations relatives à l’application d’origine et à la date de création d’un fichier EPS, par exemple. Si cette option est désélectionnée, la page est dimensionnée et centrée en fonction du coin supérieur gauche de l’objet supérieur gauche et du coin inférieur droit de l’objet inférieur droit de la page.

**Conserver les commentaires OPI :** permet de conserver les informations nécessaires au remplacement d’une image FPO (For Placement Only) ou d’un commentaire dont l’image haute résolution est située sur les serveurs qui prennent en charge OPI (Open Prepress Interface) versions 1.3 et 2.0.

**Préserver les informations sur le document des commentaires DSC :** permet de conserver des informations relatives au titre, à la date et à l’heure de création, par exemple. Lorsque vous ouvrez un fichier PDF dans Acrobat, ces informations s’affichent dans le panneau de description des propriétés du document.

**Redimensionner la page et centrer les illustrations des fichiers EPS :** centre une image EPS et redimensionne la page de sorte qu’elle s’adapte étroitement à l’image. Cette option concerne uniquement les travaux composés d’un seul fichier EPS.

## Options de rapport et de conformité aux normes {#standards-reporting-and-compliance-options}

PDF Generator peut vérifier le contenu du document dans un fichier PostScript pour s’assurer qu’il répond aux critères standard PDF/X-1a, PDF/X-3 ou PDF/A avant de créer le fichier PDF. Pour les fichiers conformes à la norme PDF/X, vous pouvez demander que le fichier PostScript réponde à des critères supplémentaires en sélectionnant d’autres options dans « Rapports et conformité aux normes ». La disponibilité des options dépend de la norme choisie.

Les fichiers conformes à la norme PDF/X sont principalement utilisés en tant que format d’échange normalisé de fichiers PDF dédiés à une impression haute résolution. A moins de créer un document PDF destiné à être imprimé, vous pouvez ignorer les normes de conformité PDF/X.

Les fichiers compatibles avec PDF/A sont principalement utilisés à des fins d’archivage. La conservation à long terme étant l’objectif, le document doit contenir uniquement les éléments nécessaires à l’ouverture et à l’affichage tout au long de la vie à laquelle il se destine. Par exemple, les fichiers compatibles avec PDF/A ne peuvent contenir que du texte, des images matricielles et des objets vectoriels ; ils ne peuvent contenir ni chiffrement ni scripts. En outre, toutes les polices doivent être incorporées afin que les documents puissent être ouverts et affichés comme ils ont été créés. En d’autres termes, les documents conformes à la norme PDF/A sont *plus fins* que ceux conformes à la norme PDF/X, qui sont dédiés à une impression de pointe.

>[!NOTE]
>
>si vous avez défini un dossier de contrôle pour la création de fichiers conformes à la norme PDF/A, vérifiez que vous n’avez pas ajouté de protection à ce dossier, car la norme PDF/A n’autorise pas de chiffrement.

Pour plus d’informations sur l’accès aux options de rapport et de conformité aux normes, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Norme de conformité :** permet de sélectionner une norme afin de générer un rapport indiquant si le fichier est conforme aux exigences, et si tel n’est pas le cas, les problèmes rencontrés. Lorsque l’option Compatibilité de la page Paramètres généraux est définie sur Acrobat 4.0, les options ci-dessous sont activées. Lorsque l’option Compatibilité est définie sur Acrobat 5.0, seules les options Acrobat 5.0 sont disponibles pour la sélection. Lorsque l’option Compatibilité est définie sur une autre option, les options suivantes sont grisées :

* PDF/X-1a (compatible avec Acrobat 4.0)
* PDF/X-3 (compatible avec Acrobat 4.0)
* PDF/X-1a (compatible avec Acrobat 5.0)
* PDF/X-3 (compatible avec Acrobat 5.0)
* PDF/A-1b (compatible avec Acrobat 5.0)

### Options des normes PDF/X {#options-for-pdf-x-standards}

**Si non conforme :** indique s’il faut créer le fichier PDF en cas de non-conformité du fichier PostScript aux exigences de la norme PDF/X. Cette option est disponible si une valeur autre qu’Aucune est affectée à l’option Norme de conformité de la page Rapport et conformité aux normes.

**Continuer :** permet de créer un fichier PDF.

**Annuler la tâche :** permet de créer un fichier PDF seulement si le fichier PostScript répond aux exigences PDF/X des options de rapport sélectionnées et s’il est par ailleurs valide. Si les deux options de rapport PDF/X sont sélectionnées et que le fichier PostScript ne répond qu’à un seul jeu de critères PDF/X (par exemple, PDF/X-3), PDF Generator crée le fichier conforme.

**Si ni la zone de rognage ni la zone graphique ne sont spécifiées :** cette option est disponible lorsque la norme de conformité de la page Rapport et conformité aux normes est définie sur une option autre que Aucune.

**Signaler comme erreur :** signale le fichier PostScript comme non conforme si l’une des options de rapport est sélectionnée et si une zone de rognage ou une zone graphique manque sur une page.

**Définir la zone de rognage selon la zone de support avec des décalages (en points) :** permet de calculer les valeurs en points de la zone de rognage en fonction des décalages de la zone de support des pages respectives si ni la zone de rognage ni la zone graphique n’est spécifié. La zone de rognage est toujours aussi petite ou plus petite que la zone de support qui l’entoure.

**Si la zone de fond perdu n’est pas spécifiée :** cette option est disponible lorsque la Norme de conformité de la page Rapport et conformité aux normes est définie sur une option autre que Aucune.

**Définir la zone de fond perdu selon la zone de support :** permet d’utiliser les valeurs de la zone de support pour la zone de fond perdu si celle-ci n’est pas spécifié.

**Définir la zone de fond perdu selon la zone de rognage avec des décalages (en points) :** permet de calculer les valeurs en points de la zone de fond perdu en fonction des décalages de la zone de rognage des pages respectives si la zone de fond perdu n’est pas spécifié. La zone de fond perdu est toujours aussi grande ou plus grande que la zone de rognage insérée.

**Valeurs par défaut si elles ne sont pas spécifiées dans le document :** cette option est disponible lorsque l’option Norme de conformité de la page Rapport et conformité aux normes est définie sur une option autre que Aucune.

**Nom du profil du mode de sortie :** indique la condition d’impression caractérisée pour laquelle le document est préparé. Si un document ne spécifie pas de nom OutputIntent, PDF Generator utilise la valeur sélectionnée dans ce menu. Vous pouvez sélectionner l’un des noms fournis ou saisir un nom dans l’espace prévu à cet effet. Si votre workflow nécessite que le document spécifie des informations sur le mode de sortie, sélectionnez Aucun. Tout document ne répondant pas aux exigences ne passe pas le contrôle de conformité.

**Identifiant de condition de sortie :** permet d’indiquer le nom de référence spécifié par le registre du nom de profil du mode de sortie.

**Condition de sortie :** décrit la condition d’impression prévue. Cette entrée peut être utile au destinataire du document PDF.

**Nom du registre (URL) :** indique l’adresse Web pour plus d’informations sur le registre. L’URL est saisie automatiquement pour les noms de registre ICC.

**Recouvrement :** permet d’indiquer l’état de recouvrement du document. La conformité PDF/X requiert la valeur True ou False. Si le document ne spécifie pas l’état de recouvrement, la valeur fournie ici est utilisée. Si votre workflow nécessite que le document spécifie l’état de recouvrement, sélectionnez Ne pas définir. Tout document ne répondant pas aux exigences ne passe pas le contrôle de conformité.

### Options de la norme PDF/A {#options-for-pdf-a-standard}

Ces options sont activées lorsque l’option Compatibilité (dans la zone Général) est définie sur Acrobat 4 (PDF 1.3) ou Acrobat 5 (PDF 1.4).

**Si non conforme :** permet d’indiquer s’il convient de créer le fichier PDF en cas de non conformité du fichier PostScript aux exigences de la norme PDF/A.

**Continuer :** permet de créer un fichier PDF même si le fichier PostScript ne répond pas aux exigences de la norme.

**Annuler la tâche :** permet de créer un fichier PDF uniquement si le fichier PostScript est conforme aux exigences PDF/A et s’il est par ailleurs correct.

**Nom du profil du mode de sortie :** indique les conditions d’impression particulières pour lesquelles le document a été préparé et qui sont requises pour la conformité aux exigences PDF/A. Si votre workflow nécessite que le document spécifie des informations sur le mode de sortie, sélectionnez « Aucun ». La conformité du document ne pourra être vérifiée si cette information n’est pas fournie.

**Condition de sortie :** permet de décrire la condition d’impression voulue. Cette entrée n’est pas obligatoire, mais elle peut être utilisée pour fournir des informations utiles à la personne destinataire prévue du document PDF.

## Options d’affichage initial {#initial-view-options}

Ces options sont organisées en trois zones : Options du document, Options de fenêtre et Options de l’interface utilisateur. Pour plus d’informations sur l’accès aux options d’affichage initial, voir [Ajout ou modification de paramètres PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Pour utiliser ces options, sélectionnez Définir les paramètres d’affichage initiaux.

### Options du document {#document-options}

Les options du document contrôlent l’apparence du document au sein de la fenêtre, comme le niveau de zoom et le type de défilement.

**Afficher :** permet de déterminer les panneaux et onglets à afficher dans la fenêtre de l’application par défaut. Panneau et page Signets permet d’ouvrir le panneau du document et l’onglet Signets.

**Disposition de la page :** permet de déterminer le mode d’affichage du document : Une seule page, Page double, Continue ou Continue-page double.

**Zoom :** permet de définir la valeur de zoom auquel le document doit être affiché lors de son ouverture. La valeur par défaut est celle configurée par l’utilisateur dans les préférences Acrobat ou Adobe Reader.

**Ouvrir à la page :** permet de définir la page à laquelle s’ouvre le document (généralement la page 1).

>[!NOTE]
>
>Les valeurs par défaut des options relatives au zoom et à la disposition sont celles des options des utilisateurs et utilisatrices définies dans les préférences d’affichage des pages dans Acrobat ou Adobe Reader.

### Options de fenêtre {#window-options}

Les options de fenêtre déterminent le mode d’ajustement de la fenêtre dans la zone d’écran lorsqu’une personne ouvre le document. Toutefois, les options n’ont aucun effet lorsqu’un document PDF est affiché dans un navigateur web.

**Redimensionner la fenêtre par rapport à la page initiale :** permet d’ajuster la fenêtre de document pour qu’elle s’adapte parfaitement à la page ouverte conformément aux options sélectionnées dans Options du document.

**Centrer la fenêtre sur l’écran :** permet de positionner la fenêtre au centre de l’écran.

**Ouvrir en mode plein écran :** permet d’agrandir la fenêtre et d’afficher le document sans les commandes de la barre de menus, de la barre d’outils ou d’affichage.

**Afficher :** indique le nom du fichier dans la barre de titre de la fenêtre. Titre du document affiche le titre du document dans la barre de titre de la fenêtre.

### Options de l’interface utilisateur {#user-interface-options}

Les options de l’interface utilisateur déterminent les commandes à afficher ou à masquer lorsqu’une personne ouvre le document.

**Masquer la barre de menus :** si cette option est sélectionnée, la barre de menus est masquée.

**Masquer les barres d’outils :** si cette option est sélectionnée, les barres d’outils sont masquées.

**Masquer les commandes d’affichage :** permet de masquer les commandes d’affichage.

>[!NOTE]
>
>Si vous masquez la barre de menus et la barre d’outils, les utilisateurs et utilisatrices ne peuvent pas appliquer de commandes et sélectionner des outils à moins de connaître les raccourcis clavier lorsqu’ils ouvrent le fichier dans Acrobat.

## Chargement et téléchargement des fichiers prologue et épilogue {#uploading-and-downloading-prologue-and-epilogue-files}

Les fichiers prologue permettent d’ajouter du code PostScript personnalisé qui s’exécute au début de chaque tâche PostScript en cours de conversion. Les fichiers épilogue servent à ajouter du code PostScript personnalisé qui s’exécute à la fin de chaque tâche PostScript. Vous pouvez télécharger des fichiers épilogue et prologue à partir du serveur pour les enregistrer localement. Vous pouvez télécharger les fichiers pour les configurer indépendamment ou pour les charger vers un autre emplacement ou un autre ordinateur.

Ces fichiers ont de nombreux usages. Par exemple, les fichiers prologue peuvent être modifiés pour définir les pages de couverture et les fichiers épilogue pour résoudre une série de procédures d’un fichier PostScript. Vous pouvez également sélectionner et charger les fichiers épilogue et prologue à envoyer avec chaque travail.

### Téléchargement d’un fichier prologue ou épilogue {#download-a-prologue-or-epilogue-file}

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Nouveau ou sur le nom d’un paramètre.
1. Cliquez sur Avancées puis, en regard de l’option Utiliser les fichiers Prologue.ps/Epilogue, cliquez sur Télécharger.
1. Dans la page Télécharger des fichiers Prologue et Epilogue, cliquez sur Prologue.ps ou Epilogue.ps, puis sur Enregistrer.

### Chargement d’un fichier prologue ou épilogue {#upload-a-prologue-or-epilogue-file}

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Paramètres Adobe PDF.
1. Cliquez sur Nouveau ou sur le nom d’un paramètre.
1. Cliquez sur Avancées puis, en regard de l’option Utiliser les fichiers Prologue.ps/Epilogue.ps, cliquez sur Charger.
1. Dans la page Charger des fichiers Prologue et Epilogue, cliquez sur Parcourir pour sélectionner un fichier prologue ou épilogue.
1. Recherchez le fichier et cliquez sur Ouvrir.
1. Pour utiliser le fichier, assurez-vous que l’option Utiliser des fichiers Prologue.ps et Epilogue.ps est sélectionnée dans la zone Avancées de la page relative à la création ou à la modification de paramètre Adobe PDF.
1. Cliquez sur Enregistrer

>[!NOTE]
>
>PDF Generator ne prend en charge les fichiers épilogue et prologue que pour la conversion de fichiers PostScript et Postscript encapsulés en PDF.
