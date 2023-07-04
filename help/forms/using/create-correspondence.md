---
title: Créer une correspondance
seo-title: Create Correspondence
description: Après avoir créé un modèle de lettre, vous pouvez l’utiliser pour créer une correspondance dans AEM Forms en gérant les données, le contenu et les pièces jointes.
seo-description: After you have created a letter template, you can use it to create correspondence in AEM Forms by managing data, content, and attachments.
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
feature: Correspondence Management
exl-id: da966787-a3b9-420f-8b7c-f00d05c61d43
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: ht
source-wordcount: '3855'
ht-degree: 100%

---

# Créer une correspondance{#create-correspondence}

## Création de correspondance dans l’interface utilisateur de création de correspondance {#create-correspondence-in-the-create-correspondence-user-interface}

Après la création d’un [modèle de lettre dans Correspondence Management](../../forms/using/create-letter.md), l’utilisateur / agent / expert en assurance final peut ouvrir la lettre dans l’interface utilisateur Création de correspondance et créer une correspondance en saisissant des données, en installant du contenu et en gérant les pièces jointes. Enfin, l’expert ou l’experte en assurance ou l’agent peut gérer le contenu en mode aperçu et envoyer la lettre.

### Prévisualisation d’une correspondance {#preview-a-correspondence}

Sélectionnez la lettre à prévisualiser en procédant comme suit :

1. Sur la page Lettres, appuyez sur **Sélectionner**.
1. Sélectionnez la lettre appropriée en appuyant dessus.

   ![Sélectionner une lettre](assets/1_selectletter.png)

   Sélectionner une lettre

1. Pour une lettre basée sur un dictionnaire de données, sélectionnez **Prévisualisation** > **Prévisualisation**. Ou, pour une lettre qui n’est pas basée sur un dictionnaire de données, sélectionnez **Aperçu**. Vous pouvez également pointer sur une lettre (sans la sélectionner) avec la souris et appuyer sur l’icône Aperçu de la lettre pour la prévisualiser.

   >[!NOTE]
   >
   >Si un élément de données n’est pas associé à la lettre, l’aperçu de la lettre s’ouvre. Sinon, si la lettre est basée sur un dictionnaire de données, Correspondence Management affiche les options de prévisualisation et de personnalisation dans le menu Prévisualisation et vous pouvez sélectionner l’une des deux options. Vous pouvez également associer des données de test à un dictionnaire de données. Lorsque le [dictionnaire de données est associé à des données de test](../../forms/using/data-dictionary.md#p-working-with-test-data-p), en sélectionnant l’option de prévisualisation, l’écran d’aperçu classique s’ouvre avec les données de test renseignées.

1. Pour être en mesure de rendre une correspondance lors de la prévisualisation, vous devez être un administrateur ou un membre de l’un des groupes suivants :

   * forms-users (pour prévisualiser sur instance d’auteur)
   * cm-agent-users (pour le rendu sur une instance de publication)

   Si vous ne disposez pas des autorisations requises, contactez votre administrateur pour obtenir des droits d’accès appropriés. Pour plus d’informations sur la création et l’ajout des utilisateurs aux groupes, voir [Ajouter des utilisateurs ou des groupes à un groupe](/help/sites-administering/security.md). Si vous tentez de rendre une correspondance sans avoir les autorisations appropriées, la page d’erreur 404 s’affiche.

1. Si vous avez sélectionné **Aperçu** > **Personnalisation**, une boîte de dialogue s’ouvre. Dans la boîte de dialogue, sélectionnez un fichier de données, correspondant au dictionnaire de données, avec lequel prévisualiser la lettre puis sélectionnez **Aperçu**. Un fichier de données est créé à partir d’un dictionnaire de données pour une lettre particulière. Pour plus d’informations sur le fichier de données, consultez la section [Dictionnaire de données](../../forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Aperçu de la lettre](assets/8_previewcustomdatafile.png)

1. L’aperçu HTML de la lettre (aperçu de formulaires mobiles) s’ouvre sur l’onglet Données actif par défaut.

   Pour plus d’informations sur les formulaires mobiles et les fonctionnalités qu’ils prennent en charge, consultez [Différences de caractéristiques entre les formulaires pour périphériques mobiles et les formulaires PDF](https://helpx.adobe.com/fr/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html).

   Il existe trois onglets : données, contenu et pièces jointes. S’il n’existe pas d’éléments de données (variables d’espace réservé et champs de mise en page), la lettre s’ouvre alors directement dans l’onglet Contenu. L’onglet Pièces jointes est disponible uniquement lorsque des pièces jointes sont présentes ou que l’accès à la bibliothèque est activé.

   >[!NOTE]
   >
   >Pour plus d’informations sur le basculement entre le mode de rendu HTML et PDF de la prévisualisation de lettre, voir [Modifier le mode de rendu de lettre](#changerenditionmode). Pour plus d’informations sur la prise en charge des PDF dans Correspondence Management et AEM, voir [Discontinuation des plug-ins de navigateur NPAPI et son impact](https://helpx.adobe.com/acrobat/kb/change-in-support-for-acrobat-and-reader-plug-ins-in-modern-web-.html). <!-- and [PDF Forms to HTML5 Forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html). THIS URL IS A 404 AND NO SUITABLE REPLACEMENT TOPIC WAS FOUND. CONSIDER DELETING OR ADDING NEW LINK. COMMENTING OUT SO USERS DON'T CLICK IT. -->

### Saisir des données {#enterdata}

Dans l’onglet Données, remplissez les champs de mise en page et les espaces réservés disponibles.

1. Saisissez les données et les variables de contenu dans les champs selon vos besoins. Remplissez tous les champs obligatoires identifiés par un astérisque (&#42;) pour activer le bouton **Envoyer**.

   Appuyez sur une valeur de champ de données dans l’aperçu de lettre HTML pour mettre en surbrillance le champ de données correspondant dans l’onglet Données.

   ![Saisissez des données dans la lettre](assets/2_enterdata.png) ![2_1_enterdata](assets/2_1_enterdata.png).

### Gérer le contenu {#managecontent}

Dans l’onglet Contenu, gérez le contenu tel que les fragments de document et les variables de contenu dans la lettre.

1. Sélectionnez **Contenu**. Correspondence Management affiche l’onglet de contenu de la lettre.

   ![Onglet Contenu - mettre en surbrillance le module dans le contenu](assets/3_content.png)

1. Modifiez les modules de contenu, selon les besoins, dans l’onglet Contenu. Pour activer le module de contenu approprié dans la hiérarchie des contenus, vous pouvez soit appuyer sur la ligne ou le paragraphe concerné dans l’aperçu de la lettre, soit appuyer directement sur le module de contenu dans la hiérarchie des contenus.

   Par exemple, la ligne « Nous avons passé en revue... » est sélectionnée dans le graphique ci-dessous et le module de contenu approprié est sélectionné dans l’onglet Contenu.

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   Dans l’onglet Contenu ou Données, en appuyant sur Mettre en surbrillance les modules sélectionnés (![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) dans le coin supérieur gauche de l’aperçu de lettre HTML, vous pouvez activer ou désactiver la fonctionnalité d’accès au module de contenu ou de données lorsque le texte, le paragraphe ou le champ de données approprié est sélectionné dans la prévisualisation de la lettre.

   Pour plus d’informations sur les actions disponibles pour différents modules dans l’interface utilisateur Création de correspondance, consultez la section [Actions et informations disponibles dans l’interface utilisateur de création de correspondance](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Pour localiser les modules de contenu, utilisez le champ Rechercher. Saisissez le nom ou le titre complet ou partiel du module de contenu pour le rechercher dans la correspondance.
1. Appuyez sur l’icône Affichage (![display](assets/display.png)) devant une liste, un texte, une condition ou une zone cible pour l’afficher ou le/la masquer dans la lettre.
1. Pour modifier un module de texte incorporé ou modifiable, appuyez sur l’icône **Modifier** (![edittextmodule](assets/edittextmodule.png)) ou cliquez deux fois sur le module de texte approprié dans la prévisualisation de la lettre.

   Le système affiche un éditeur de texte pour modifier et formater le texte.

   Le vérificateur orthographique par défaut de votre navigateur vérifie l’orthographe dans l’éditeur de texte. Pour gérer les vérifications d’orthographe et de grammaire, vous pouvez modifier les paramètres du vérificateur orthographique de votre navigateur ou installer des plug-ins/modules complémentaires externes de navigateur pour vérifier l’orthographe et la grammaire.

   Vous pouvez également utiliser les nombreux raccourcis clavier dans l’éditeur de texte pour gérer, modifier et mettre en forme le texte. Pour plus d’informations sur les raccourcis clavier de l’[Éditeur de texte](/help/forms/using/keyboard-shortcuts.md#correspondence-management) dans les Raccourcis clavier de Correspondence Management.

   ![5_edittextmodule](assets/5_edittextmodule.png)

   Vous pouvez réutiliser un ou plusieurs paragraphes de texte existant dans une autre application de document. Vous pouvez directement copier et coller du texte, provenant par exemple de MS Word, de pages HTML ou de toute autre application.

   Vous pouvez copier et coller un ou plusieurs paragraphes de texte dans un module de texte modifiable. Par exemple, vous pouvez disposer d’un document MS Word avec une liste à puces de preuves de résidence acceptables, comme suit :

   ![pastetextmsword](assets/pastetextmsword.png)

   Vous pouvez directement copier et coller le texte du document MS Word dans un module de texte modifiable. La mise en forme, telle que la liste à puces, la police et la couleur du texte, est conservée dans le module de texte.

   ![pastetexteditablemodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >Toutefois, la mise en forme du texte collé présente certaines [restrictions](https://helpx.adobe.com/fr/aem-forms/kb/cm-copy-paste-text-limitations.html).

   Vous pouvez mettre le texte et les nombres en retrait dans votre lettre à l’aide de la touche de tabulation. Par exemple, vous pouvez utiliser la touche de tabulation pour aligner plusieurs colonnes de texte d’une liste dans un format tabulaire.

   ![tabspaces](assets/tabspaces.png)

   Exemple : vous pouvez utiliser la touche de tabulation pour aligner plusieurs colonnes de texte sous forme de tableau.

   >[!NOTE]
   >
   >Pour plus d’informations sur la configuration de l’espacement des tabulations pour vos modules de texte et lettres, voir la section [Informations supplémentaires sur l’utilisation de l’espacement des tabulations pour l’agencement du texte](https://helpx.adobe.com/fr/aem-forms/kb/cm-tab-spacing-limitations.html).

1. Si nécessaire, insérez des caractères spéciaux dans la correspondance. Vous pouvez, par exemple, utiliser la palette des caractères spéciaux pour insérer les caractères suivants :

   * Symboles de devise tels que €,￥et £
   * Symboles mathématiques tels que ∑, √, ∂ et ^
   * Symboles de ponctuation tels que « et »

   ![specialcharacters](assets/specialcharacters.png)

   Correspondence Management offre une prise en charge intégrée de 210 caractères spéciaux. L’administrateur peut [ajouter la prise en charge de plus de caractères/de caractères spéciaux grâce à la personnalisation](../../forms/using/custom-special-characters.md).

1. Pour mettre en surbrillance\mettre en évidence des parties de texte dans un module incorporé modifiable, sélectionnez le texte et appuyez sur Couleur de surbrillance.

   ![letterbackgroundcolor](assets/letterbackgroundcolor.png)

   Vous pouvez soit directement sélectionner une couleur de base `**[A]**` dans la palette correspondante ou appuyer sur **Sélectionner** après avoir utilisé le curseur `**[B]**` pour sélectionner la teinte de couleur appropriée.

   Si vous le souhaitez, vous pouvez également accéder à l’onglet Avancé afin de sélectionner les niveaux de Teinte, Luminosité et Saturation appropriés `**[C]**` pour créer la couleur exacte, puis appuyer sur Sélectionner `**[D]**` pour appliquer la couleur de mise en évidence du texte.

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. Effectuez les modifications appropriées de contenu et de format, puis appuyez sur **Enregistrer**. Appuyez sur (![editnextmoduleccr](assets/editnextmoduleccr.png)) pour vous déplacer entre les modules de texte modifiables, ou cliquez sur **Enregistrer et suivant** pour enregistrer les modifications et passez au module de texte modifiable suivant.
1. Le système affiche également les variables vides pour chacune des branches. S’il n’existe aucune variable vide, les variables vides sont présentées comme 0. S’il y a des variables vides, vous pouvez appuyer sur une branche pour la développer et rechercher la variable vide. Utilisez la barre d’outils de contenu pour supprimer du contenu, augmenter ou diminuer le retrait du contenu, et insérer des sauts de page avant ou après le contenu.

   Vous pouvez insérer des sauts de page au-dessus et en dessous des modules de données, même s’ils font partie de listes et de conditions.

1. Appuyez sur Ouvrir/Fermer la variable de contenu (![opencontentvariables](assets/opencontentvariables.png)) pour ouvrir les variables de contenu et les remplir correctement.
1. Lorsque vous renseignez la variable vide correctement, le nombre de variables vides est défini sur 0.

   Dans l’interface utilisateur Création de correspondance, le nombre de variables vides est affiché à chaque niveau de la hiérarchie de tout module qui contient au moins une variable. Si un module contient des variables vides, le nombre s’affiche au niveau de la variable, du module, de la zone cible et du modèle de lettre.

   Le nombre de variables vides inclut :

   * Uniquement des variables du dictionnaire de données non protégées et d’espace réservé. Le nombre de variables n’inclut pas les variables de disposition ou d‘éléments de données protégées.
   * Champs obligatoires.
   * Champs de mise en page s’ils sont obligatoires et liés à l’utilisateur.
   * Uniquement les instances de variables uniques. Si un module, une zone cible ou un modèle de lettre contient deux instances ou plus d’une même variable, le nombre est affiché comme 1 (un). Cependant, pour chacune des instances, le nombre s’affiche comme 1.

   Le nombre de variables vides ne comprend pas les modules non sélectionnés. Si un module est inclus dans un modèle de lettre mais ne figure pas dans la lettre, le nombre de variables vides dans ce module n’est pas affiché.

   Pour la zone cible, le module et la variable, le nombre s’affiche à droite de chaque objet du modèle de lettre. Cependant, pour le modèle complet, le nombre s’affiche dans la barre de statut de Création de correspondance.

   Les modules d’un modèle de lettre affichent le nombre de variables vides comme décrit ci-dessous :

   * **Texte** : affiche la somme des variables d’espace réservé vides uniques et des éléments du dictionnaire de données contenus dans le module de texte.
   * **Condition** : affiche la somme des variables de condition vides uniques contenues dans la condition et des variables contenues dans les modules qui en résultent.
   * **Liste** : affiche la somme de toutes les variables vides uniques contenues dans les modules attribués à la liste.
   * **Zone cible** : affiche la somme de toutes les variables vides uniques contenues dans les modules attribués à la zone cible.

   Notez ce qui suit concernant les variables avec des valeurs par défaut :

   * Un champ de variable booléenne est défini par défaut sur *false*. Toutefois, la variable est considérée comme vide. Cela signifie que le nombre de variables inclut tous les champs de variable booléenne avec la valeur *false*.

   * Un champ de variable numérique est défini par défaut sur *0 (zéro)*. Toutefois, la variable est considérée comme vide. Cela signifie que le nombre de variables inclut tous les champs de variable numérique avec la valeur *0 (zéro)*.



#### Actions et informations disponibles dans l’onglet Contenu de la création de correspondance {#actions-and-info-available-in-the-create-correspondence-content-tab}

**Zone cible**

* Insertion d’une ligne vide : permet d’insérer une nouvelle ligne vide.
* Insertion de texte en ligne : permet d’insérer un nouveau module de texte.
* Verrouillage d’ordre (information) : indique que l’ordre du contenu ne peut pas être modifié.
* Valeurs vides (information) : indique le nombre de variables vides dans la zone cible.

**Module**

* Sélection (icône représentant un œil) : permet d’inclure ou d’exclure le module de la lettre.
* Ignorer les puces (applicable pour les modules de liste et leurs modules enfants) : ignore les puces dans un module particulier.
* Saut de page avant (applicable pour les modules enfants de la zone cible) : insère un saut de page avant le module.
* Saut de page après (applicable pour les modules enfants de la zone cible) : insère un saut de page avant le module.
* Valeurs vides (information) : indique le nombre de variables vides dans la zone cible.
* Modification (modules de texte uniquement) : ouvrez l’éditeur de texte enrichi pour modifier le module de texte.
* Panneau de données (modules de texte et de condition) : permet de déverrouiller toutes les variables du module.

**Module de liste**

* Insertion d’une ligne vide : permet d’insérer une nouvelle ligne vide.
* Bibliothèque de contenu : ouvre la bibliothèque de contenu pour ajouter des modules à la liste.
* Paramètre de liste (liste imbriquée uniquement) :
* Verrouillage d’ordre (information) : indique que l’ordre des éléments de la liste ne peut pas être modifié.

### Gestion des pièces jointes {#manage-attachments}

1. Sélectionnez **les pièces jointes**. Correspondence Management affiche les pièces jointes disponibles de la manière dont elles ont été configurées lors de la création du modèle de lettre.
1. Vous pouvez choisir de ne pas envoyer une pièce jointe avec la lettre en appuyant sur l’icône Afficher et en appuyant sur la croix dans la pièce jointe pour la supprimer de la lettre. Pour les pièces jointes spécifiées, lors de la création d’un modèle de lettre, comme étant obligatoires, les icônes Afficher et Supprimer sont désactivées.
1. Cliquer sur l’icône d’accès à la bibliothèque (![libraryaccess](assets/libraryaccess.png)) pour accéder à la bibliothèque de contenu et insérer des ressources DAM comme pièces jointes.

   >[!NOTE]
   >
   >L’icône d’accès à la bibliothèque n’est disponible que si l’accès à la bibliothèque a été activé lors de la création de la lettre.

1. Si l’ordre des pièces jointes n’a pas été verrouillé lors de la création de la correspondance, vous pouvez réorganiser les pièces jointes en sélectionnant une pièce jointe et en appuyant sur les flèches montantes et descendantes.

   Pour plus d’informations, consultez la section [Diffuser des pièces jointes](#attachmentdelivery).

### Gestion du contenu dans l’aperçu et envoi de la lettre {#manage-content-in-preview-and-submit-the-letter}

Vous pouvez effectuer des modifications relatives à la disposition et au contenu pour vous assurer que la lettre apparaît exactement comme vous le souhaitez et l’envoyer aux différents post-processus.

1. Pour mettre en surbrillance tout le contenu modifiable dans la lettre, cliquez sur **Mettre les sections modifiables en surbrillance**.

   Les contenus modifiables de la lettre sont mis en surbrillance avec un arrière-plan gris.

   ![Mettre en surbrillance le contenu modifiable](assets/4_highlightmoduleincontent-1.png)

1. Modifiez les modules de contenu, selon les besoins, dans l’onglet Contenu. Pour activer le module de contenu approprié dans la hiérarchie des contenus, vous pouvez soit appuyer sur la ligne ou le paragraphe concerné dans l’aperçu de la lettre, soit appuyer directement sur le module de contenu dans la hiérarchie des contenus.

   Par exemple, la ligne « Pour accéder à… » est sélectionnée dans le graphique ci-dessous et le module de contenu correspondant est sélectionné dans l’onglet Contenu.

   En cliquant sur Mettre les modules sélectionnés en surbrillance dans le contenu ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)), vous pouvez activer ou désactiver la fonctionnalité de mise en surbrillance du module de contenu dans l’onglet Contenu lorsque le texte, le paragraphe ou le champ de données approprié est sélectionné dans la prévisualisation de la lettre.

   Pour plus d’informations sur les actions disponibles pour différents modules dans l’interface utilisateur Création de correspondance, consultez la section [Actions et informations disponibles dans l’interface utilisateur de création de correspondance](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Pour insérer un saut de page dans la lettre, cliquez à l’endroit où vous souhaitez insérer un saut de page et sélectionnez Saut de page avant ou Saut de page après ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   Un espace réservé de saut de page explicite est inséré dans la lettre. Pour voir comment un saut de page explicite affecte la lettre, consultez l’aperçu sous forme de fichier PDF aplati.

   >[!NOTE]
   >
   >Les formulaires mobiles ne prenant pas en charge les sauts de page, les en-têtes et les pieds de page n’apparaissent qu’une seule fois. Vous pouvez toutefois définir explicitement des en-têtes et des pieds de page dans la disposition (par page) pour qu’ils apparaissent dans l’aperçu des formulaires mobiles. En outre, les pages vierges de la lettre, le cas échéant, n’apparaissent pas dans l’aperçu des formulaires mobiles.

   ![Saut de page explicite](assets/8_pagebreak.png)

1. Pour enregistrer la lettre en tant que brouillon et poursuivre sa rédaction plus tard, appuyez sur Enregistrer en tant que brouillon. Pour utiliser cette option, votre lettre doit être [publiée](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Pour plus d’informations, consultez la section Instance Brouillon sous [Enregistrement de brouillons et envoi d’instances de lettre](#savingdrafts).

   ![saveasdraft](assets/saveasdraft.png)

   La boîte de dialogue Nom du brouillon de la lettre s’affiche avec l’ID d’instance de lettre. Vous pouvez également modifier cet ID. Notez l’ID de lettre, puis appuyez sur **Terminé**. Vous pouvez utiliser cet ID ultérieurement pour [recharger le brouillon de la lettre](submit-letter-topostprocess.md#reloaddraft).

1. Pour afficher la lettre sous forme de fichier PDF aplati, avec la disposition et les sauts de page exacts, comme elle sera envoyée, cliquez sur Prévisualisation ( ![preview](assets/preview.png)).

   La lettre s’affiche sous forme de fichier PDF aplati. Le PDF aplati ressemble à l’identique à la lettre telle qu’elle sera envoyée, avec les mêmes polices, sauts et disposition.

   >[!NOTE]
   >
   >Si vous utilisez Mozilla Firefox et le type de rendu HTML pour prévisualiser la lettre sous forme de fichier PDF aplati, veillez à employer le plug-in natif du navigateur et non le plug-in Acrobat. Pour sélectionner le plug-in natif du navigateur, accédez aux paramètres de Mozilla Firefox, puis à Type de contenu PDF et sélectionnez Aperçu dans Firefox.

1. Si l’aperçu du fichier PDF aplati vous satisfait, cliquez sur **Envoyer** pour envoyer la lettre. Ou, pour apporter des modifications à la lettre, cliquez sur **Quitter la prévisualisation** pour rétablir l’aperçu de l’interface utilisateur Création de correspondance et y apporter des modifications. Lorsque vous appuyez sur Envoyer, si la configuration Gestion des instances de lettre est activée sur l’instance de publication, l’instance d’envoi de lettre est générée.

   Pour plus d’informations, consultez la section Instance Brouillon sous Enregistrement de brouillons et envoi d’instances de lettre.

   Vous pouvez également enregistrer la lettre en tant que brouillon pour y apporter des modifications plus tard.

   Une fois les modifications apportées, vous pouvez envoyer la lettre à partir de l’aperçu HTML5 ou appuyer à nouveau sur Aperçu pour examiner le fichier PDF aplati.

   Pour plus d’informations sur les différences entre les formulaires HTML5 et les formulaires PDF, voir [Différences de caractéristiques entre formulaires HTML5 et formulaires PDF](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## Enregistrement des brouillons et envoi d’instances de lettre {#savingdrafts}

Lorsqu’une lettre est générée dans l’interface utilisateur Création de correspondance, vous pouvez enregistrer la lettre comme étant en cours de consultation.

Il existe deux types d’instances de lettre pouvant être enregistrées : instance Brouillon ou instance Envoyer.

* **Instance Brouillon** : l’instance Brouillon capture l’état actuel de la lettre que vous prévisualisez. Pour enregistrer une instance Brouillon, assurez-vous d’abord que la lettre et toutes les ressources auxquelles la lettre fait référence sont à l’état Publié. Pour plus d’informations sur la publication d’une lettre, voir [Publication d’une ressource](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Vous devez publier une lettre avant de pouvoir l’enregistrer en tant que brouillon. En effet, lorsque vous publiez une lettre, vous créez une version de la lettre, de ses ressources dépendantes et de données à ce stade. La version publiée d’une lettre ne peut pas être modifiée par vous, un autre utilisateur ou une autre utilisatrice. Elle peut être restaurée ultérieurement sans aucune incompatibilité inattendue à partir de la version publiée. Vous pouvez retourner à cette instance plus tard et reprendre où vous en étiez.

* **Instance Envoyer** : l’instance Envoyer capture l’état de la lettre envoyée. L’instance Envoyer stocke l’état PDF de l’instance de lettre après son post-traitement ainsi que les données saisies par l’utilisateur dans l’interface utilisateur Création de correspondance.

Ces instances peuvent être enregistrées uniquement lorsque la lettre est en cours de consultation sur l’instance Publication. Par défaut, l’enregistrement sur les instances est désactivé. Pour activer l’enregistrement des instances de lettre, effectuez les étapes suivantes.

1. Dans AEM, ouvrez la configuration de la console web d’Adobe Experience Manager pour votre serveur via l’URL suivante : https://&lt;server>:&lt;port>/&lt;contextpath>/system/console/configMgr
1. Localisez les **[!UICONTROL configurations de Correspondence Management]** et cliquez dessus.
1. Cochez la configuration **[!UICONTROL Gestion des instances de lettre sur Publication]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

### Activer la fonction Enregistrer le brouillon {#enable-save-draft-feature}

Avant la publication de lettres ou l’enregistrement de brouillons sur l’instance de publication, effectuez les étapes suivantes sur l’instance d’auteur et de publication pour activer la fonction Enregistrer en tant que brouillon :

Les propriétés *cq:lastReplicationAction*, *cq:lastreplicated* et *cq:lastReplicatedBy* ne sont pas transférées vers l’instance de publication par défaut. Pour transférer les propriétés *cq:lastReplicationAction*, *cq:lastreplicated* et *cq:lastReplicatedBy* vers l’instance de publication, désactivez le composant [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory]. Pour désactiver le composant :

1. Sur l’instance d’auteur, ouvrez la console Composants de la console Web Adobe Experience Manager. L’URL par défaut est `http://author-server:port/system/console/components`.

1. Recherchez le composant **[!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory]**.

1. Cliquez sur l’icône ![bouton Désactiver](/help/forms/using/assets/enablebutton.png) pour désactiver le composant [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory].

![Instance d’auteur](/help/forms/using/assets/replicationproperties.png)

Pour activer la fonction Enregistrer en tant que brouillon, remplacez l’URL existante à l’adresse [!UICONTROL URL d’auteur VersionRestoreManager] avec l’URL de votre instance d’auteur. Pour remplacer l’URL :

1. Sur l’instance de publication, ouvrez [!UICONTROL Configuration de la console Web d’Adobe Manager]. L’URL par défaut est `https://publish-server:port/system/console/configMgr`.

1. Recherchez et ouvrez le composant **[!UICONTROL configurations Correspondence Management - Restauration de la version de l’instance d’auteur]**.

1. Localisez le champ **[!UICONTROL URL d’auteur VersionRestoreManager]** et spécifiez l’URL de l’instance d’auteur correspondante.

1. Cliquez sur Enregistrer.

![Instance de publication](/help/forms/using/assets/correspondencemanagement.png)

Lorsque l’enregistrement des instances de lettre est activé, vous avez la possibilité de sélectionner l’emplacement où les enregistrer. Il existe deux options pour enregistrer les instances de lettre : enregistrement local ou enregistrement à distance.

### Enregistrement local {#local-save}

Les instances de lettre sont enregistrées sur l’instance de publication et répliquées par inverse sur l’instance de création.

### Enregistrement à distance {#remote-save}

Cette option est destinée aux personnes ayant des inquiétudes quant à l’enregistrement des données utilisateur sur les instances Publication, ce qui est généralement le cas hors du pare-feu d’entreprise. Lorsque l’enregistrement à distance est activé, les instances de lettre ne sont pas enregistrées sur l’instance Publication mais sont enregistrées à distance sur l’auteur de traitement spécifié via les configurations du SDK client LiveCycle.

#### Activer l’enregistrement à distance {#enable-remote-save}

1. Dans AEM, ouvrez Configuration de la console web d’Adobe Experience Manager pour votre serveur via l’URL suivante : `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. Recherchez les **[!UICONTROL configurations de Correspondence Management]** et cliquez dessus.
1. Localisez la configuration **[!UICONTROL Enregistrement à distance]**, cochez-la, puis cliquez sur **[!UICONTROL Enregistrer]**.

#### Spécifiez les paramètres d’auteur de traitement {#specify-processing-author-settings}

1. Dans AEM, ouvrez Configuration de la console web Adobe Experience Manager pour votre serveur via l’URL suivante : `https://<server>:<port>/system/console/configMgr`

   ![Configuration de la console Web d’Adobe Experience Manager](assets/2configmanager.png)

1. Sur cette page, recherchez Adobe LiveCycle Client SDK Configuration et développez-le en cliquant dessus.

1. Dans l’URL du serveur de traitement, saisissez le nom de votre serveur LiveCycle, fournissez les informations de connexion, puis cliquez sur **Enregistrer**.

   ![Saisie du nom et des informations de connexion de votre serveur LiveCycle](assets/3configmanager.png)

1. Si nécessaire, définissez le nom d’utilisateur et le mot de passe avec lesquels accéder au serveur.

#### Livraison des pièces jointes {#attachmentdelivery}

* Les pièces jointes de la lettre sont disponibles après le processus dans le PDF, qui est créé après l’envoi de la lettre.
* Si la lettre est rendue à l’aide des API côté serveur sous la forme d’un PDF, interactif ou non, alors le PDF rendu contient des pièces jointes au format PDF.
* Si un post-traitement associé à un modèle de lettre est chargé dans le cadre des opérations d’envoi ou de finalisation de correspondance à l’aide de l’interface utilisateur Création de correspondance, les pièces jointes sont transmises en tant que liste &lt;com.adobe.idp.Document> dans le paramètre AttachmentDocs.
* Les mécanismes de diffusion prêts à l’emploi, tels que l’envoi par e-mail et l’impression, livrent les pièces jointes avec le PDF de la correspondance générée.

## Modes de rendu d’aperçu de lettre : aperçu de formulaires pour appareils mobiles et aperçu au format PDF {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

Dans AEM Forms, la solution Correspondence Management affiche une lettre en tant que document HTML dans l’IU Création de correspondance. Toutefois, la solution Correspondence Management prend toujours en charge le retour à un aperçu au format PDF au lieu de l’aperçu HTML. Pour plus d’informations sur le basculement entre les modes d’aperçu HTML et PDF, consultez [Changement de mode de rendu de lettre](#changerenditionmode).

Vous trouverez ci-dessous les avantages et les fonctionnalités disponibles dans l’aperçu HTML et PDF.

**Avantages de l’aperçu HTML/formulaires mobiles**

* **Appuyez sur une valeur de champ de données pour mettre en surbrillance le champ de données correspondant** : dans l’interface utilisateur Création de correspondance, vous pouvez appuyer sur une valeur de champ de données de la lettre pour mettre en surbrillance le champ de données correspondant dans l’onglet Données. Pour plus d’informations, consultez [Saisir des données](#enterdata).

* **Prise en charge du navigateur** : retrait graduel de la prise en charge des navigateurs NPAPI, ce qui affecte l’aperçu PDF de la lettre. L’aperçu de la lettre pour les formulaires mobiles/HTML n’est pas affecté par ce problème.
* **Mettre en surbrillance le contenu modifiable dans une lettre** : dans l’interface utilisateur Création de correspondance, vous pouvez appuyer sur Mettre en surbrillance le contenu modifiable pour mettre en surbrillance tout le contenu modifiable de la lettre en gris. Pour plus d’informations, consultez [Gestion du contenu](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **Avantages de l’aperçu PDF**

* **Saut de page** : dans l’aperçu au format PDF, vous pouvez afficher précisément comment les sauts de page dans la lettre affectent sa sortie.
* **Aperçu final** : dans l’aperçu au format PDF, vous pouvez afficher le formatage et l’aspect exacts de la lettre telle qu’elle apparaîtra à sa sortie.

Pour plus d’informations sur la prise en charge des scripts dans des formulaires PDF, reportez-vous à la section [Prise en charge des scripts](https://help.adobe.com/fr_FR/livecycle/11.0/ScriptingSupport/index.html).

Pour plus d’informations sur la prise en charge des scripts dans des formulaires HTML5, reportez-vous à la section [Prise en charge des scripts pour les formulaires HTML5](/help/forms/using/scripting-support.md).

### Changement du mode de rendu d’une lettre {#changerenditionmode}

Par défaut, l’interface utilisateur Création de correspondance utilise des formulaires HTML ou des formulaires mobiles pour rendre l’aperçu d’une lettre. L’aperçu des formulaires mobiles n’a aucun problème de rendu dans un navigateur, car il utilise le module externe natif du navigateur et ne requiert aucun module externe supplémentaire. Vous pouvez changer le mode de prévisualisation d’une lettre en PDF. Toutefois, les contraintes de navigateur peuvent créer des problèmes pour les différentes fonctionnalités de l’aperçu au format PDF interactif de la lettre.

Pour plus d’informations sur la compatibilité des navigateurs avec la prévisualisation de lettre, référez-vous à [Discontinuation des plug-ins du navigateur NPAPI et son impact](https://helpx.adobe.com/acrobat/kb/change-in-support-for-acrobat-and-reader-plug-ins-in-modern-web-.html).

Pour changer le mode d’aperçu de la lettre, effectuez les étapes suivantes :

1. Accédez à `https://[system]:'port'/system/console/configMgr`, puis, si nécessaire, ouvrez une session en tant qu’administrateur.
1. Accédez à **[!UICONTROL Configurations de Correspondence Management]** > **[!UICONTROL Type de rendu]** et sélectionnez **Rendu HTML** (par défaut) ou **Rendu PDF**.
1. Cliquez sur **[!UICONTROL Enregistrer]**.
