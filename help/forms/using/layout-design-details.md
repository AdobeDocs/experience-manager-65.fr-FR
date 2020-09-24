---
title: Conception de la mise en page
seo-title: Conception de la mise en page
description: Détails de conception de la mise en page explique comment créer des mises en page à utiliser pour vos lettres ou vos communications interactives.
seo-description: Conception de la mise en page Les détails expliquent comment créer des mises en page à utiliser pour vos lettres ou communications interactives.
uuid: 469a8a71-88f7-4102-bb02-38ed05390f6c
content-type: reference
topic-tags: correspondence-management, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 683809ac-089b-49bf-a72c-67d32439081f
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 66%

---


# Conception de la mise en page{#layout-design}

Les modèles de formulaire XFA ou XDP sont ceux de :

* [Lettres](/help/forms/using/create-letter.md)
* [Canal d’impression](/help/forms/using/web-channel-print-channel.md#printchannel) des [communications interactives](/help/forms/using/interactive-communications-overview.md)

* Fragments de mise en page

Les XDP sont conçus dans Adobe Forms Designer. Cet article fournit des détails sur la conception de vos fichiers XDP pour créer des correspondances/communications interactives efficaces, comme l’emplacement d’utilisation des champs de formulaire ou des zones de cible et le moment d’utilisation des fragments de mise en page.

## Création d’une mise en page pour des lettres ou pour le canal d’impression des communications interactives {#creating-a-layout-for-letters-or-for-interactive-communications-print-channel}

Une mise en page définit l’apparence graphique d’une lettre/ ou d’un canal d’impression d’une communication interactive. La mise en page peut contenir des champs de formulaire types comme « Adresse » et « Numéro de référence ». Elle contient également des sous-formulaires vides indiquant les zones cible. Le concepteur de formulaires crée la mise en page et, une fois celle-ci terminée, le spécialiste des applications l’envoie au serveur AEM. À partir de là, la mise en page peut être sélectionnée lors de la création d’un modèle de correspondance ou du canal d’impression d’une communication interactive.

![Concepteur : crée une mise en page](assets/claimsubrogationlayout.png)

Procédez comme suit pour créer des mises en page pour des lettres/le canal d’impression des communications interactives :

1. Analysez la mise en page et déterminez le contenu qui se répétera sur toutes les pages. Il s’agit en général de l’en-tête et du pied de page. Ce contenu est placé sur les gabarits de la mise en page. Le contenu restant va dans le corps des pages de la mise en page. Dans un dossier de police, le logo et l’adresse de la société pourront être ajoutés à l’en-tête ou au pied de page du gabarit Par exemple, l’avis d’annulation utilise la même présentation.
1. Lors de la conception des pages courantes, divisez le contenu des pages en sections. Chaque section est conçue comme un sous-formulaire intégré dans la mise en page ou comme une mise en page de fragment. Si la section contient un tableau, modélisez-la comme fragment de mise en page.
1. Une mise en page peut être conçue comme suit :

   1. Faites de chaque section un sous-formulaire distinct contenant tous les éléments de la section.
   1. Faites de chaque section un enfant du même sous-formulaire parent. La mise en page du sous-formulaire parent est définie de manière à permettre à la mise en page des sections de s’ajuster si les sections précédentes accueillent des données fusionnées en quantité importante.
   1. La section Résidence principale peut être réutilisée dans d’autres mises en page. Créez-la comme une mise en page de fragment.
   1. La section Détails d’intérêt supplémentaires ne contient que deux éléments placés l’un au-dessous de l’autre, elle peut contenir des données de grande taille et elle est conçue comme une mise en page souple.
   1. D’autres sections contiennent des éléments à des positions spécifiques ; elles sont donc conçues comme des mises en page positionnées.
   1. Eclatez une section en plusieurs sous-formulaires si la section contient des éléments à des positions spécifiques et si ces éléments contiennent de grandes quantités de données. Organisez ensuite les sous-formulaires pour obtenir le comportement souhaité.
   1. Pour la section Résidence principale, ajoutez une zone cible d’espace réservé. Cet espace réservé est lié au fragment Résidence principale au moment de la conception de la lettre/communication interactive.
   1. Téléchargez la mise en page (et le fragment qui utilise la mise en page, le cas échéant) sur le serveur AEM Forms.

### Utiliser un sous-formulaire dans un modèle XDP {#usesubformxdp}

Une fois que vous avez analysé la disposition requise pour créer votre communication interactive, vous pouvez créer des sous-formulaires dans le modèle XDP à l’aide de Forms Designer. Les composants de sous-formulaire vierges utilisés dans le modèle XDP génèrent l’affichage de zones de cible dans le canal d’impression de la communication interactive.

>[!NOTE]
>
>ajoutez le contenu au canal d’impression de la communication interactive au lieu d’ajouter le contenu au composant de sous-formulaire du modèle XDP. ajoutez le contenu dans les zones de cible du canal d’impression à l’aide de fragments de [document, de graphiques, d’images](create-interactive-communication.md#step2)et de fragments de mise en page.

Pour utiliser un sous-formulaire dans un modèle XDP, procédez comme suit :

1. Open the Forms Designer, select **File** > **New** > **Use a blank form**, tap **Next**, and then tap **Finish** to open the form for template creation.

   Assurez-vous que les options **Bibliothèque d’objets** et **Objet** sont sélectionnées dans le menu **Fenêtre**.

1. Faites glisser le composant **Sous-formulaire** de la **bibliothèque d’objets** vers le formulaire.

   ![Concepteur de composants](assets/subform_component_designer_new.png)

1. Sélectionnez le sous-formulaire pour afficher les options correspondantes dans la fenêtre **Objet** dans le volet de droite.
1. Select the **Subform** tab and select **Flowed** from the **Content** drop-down list. Faites glisser l’extrémité gauche du sous-formulaire pour ajuster la longueur.

   ![Sous-formulaire avec enchaînement](assets/object_subform_flowed_new.png)

1. In the **Binding** tab:

   1. Indiquez le nom du sous-formulaire dans le champ **Nom** .
   1. Sélectionnez **Aucune liaison de données** dans la liste déroulante **Liaison de données**.

1. De même, sélectionnez le sous-formulaire racine dans le volet de gauche.

   ![Sous-formulaire racine](assets/root_subform_designer_new.png)

1. Select the **Subform** tab and select **Flowed** from the **Content** drop-down list. Dans l’onglet **Liaisons** :

   1. Indiquez le nom du sous-formulaire dans le champ **Nom** .
   1. Sélectionnez **Aucune liaison de données** dans la liste déroulante **Liaison de données**.

   Répétez les étapes 2 à 5 pour ajouter d’autres sous-formulaires au modèle XDP. ajoutez [du texte, des fragments de document, des images et des graphiques](create-interactive-communication.md#step2) dans les zones de cible uniquement lors de la création de la communication interactive.

1. Sélectionnez **Fichier** > **Enregistrer sous** pour enregistrer le fichier sur le système de fichiers local :

   1. Accédez à l’emplacement d’enregistrement du fichier et spécifiez un nom pour le modèle XDP.
   1. Sélectionnez **.xdp** dans la liste déroulante **Type**.

   1. Appuyez sur **Save** (Enregistrer).

### Utilisation du composant Champ d’image dans un modèle XDP {#use-image-field-component-in-an-xdp-template}

Utilisez le composant Champ d’image ou Sous-formulaire du modèle XDP et ajoutez une image lors de la création de la communication interactive.

>[!NOTE]
>
>ajoutez l’image sur le canal d’impression de la communication interactive au lieu d’ajouter l’image au composant Champ d’image ou Sous-formulaire du modèle XDP. Pour plus d’informations, voir [Ajouter du contenu à la communication](../../forms/using/create-interactive-communication.md#step2)interactive.

Pour utiliser le composant Champ d’image dans un modèle XDP, procédez comme suit :

1. Drag-and-drop the **Image Field** component from the **Object Library** to the form.
1. Sélectionnez le sous-formulaire pour afficher les options correspondantes dans la fenêtre **Objet** dans le volet de droite.
1. In the **Binding** tab:

   1. Indiquez un nom pour le champ d’image dans le champ **Nom** .
   1. Sélectionnez **Aucune liaison de données** dans la liste déroulante **Liaison de données**.

### Créer un modèle XDP pour des fragments de mise en page {#xdplayoutfragments}

Utilisez le composant Tableau de Forms Designer pour créer des fragments de mise en page, puis utilisez-les pour créer des tableaux lors de la création du canal d’impression de la communication interactive. L’utilisation de fragments de mise en page pour créer des tableaux garantit que le contenu du tableau conserve la structure lorsque le canal Web est généré automatiquement à l’aide du canal d’impression.

>[!NOTE]
>
>Entrez du texte dans les cellules du tableau ou [créez une liaison avec les objets](create-interactive-communication.md#step2) du modèle de données de formulaire uniquement lors de la création de la communication interactive.

Suivez les étapes ci-après pour utiliser le composant Tableau dans le modèle XDP à l’aide de Forms Designer :

1. Drag-and-drop the **Table** component from the **Object Library** to the form.
1. In the **Insert Table** dialog:

   1. Spécifiez le nombre de lignes et de colonnes du tableau.
   1. Cochez la case **Inclure la rangée d’en-tête dans le tableau** pour inclure une rangée dans l’en-tête du tableau.
   1. Appuyez sur **OK**.

1. Appuyez sur **+** dans le volet de gauche en regard du nom du tableau, cliquez avec le bouton droit sur les noms de cellule inclus dans l’en-tête et les autres lignes, puis sélectionnez **Renommer l’objet** pour renommer les cellules du tableau.
1. Cliquez sur les champs de texte d’en-tête de tableau de la Vue **de** conception et renommez-les.
1. Faites glisser le composant Champ **de** texte de la bibliothèque **d’** objets vers chaque cellule de tableau de la Vue **** de conception. Effectuez cette étape pour pouvoir lier des cellules de tableau aux objets de modèle de données de formulaire lors de la création de la communication interactive.

   ![Champs de texte dans un tableau](assets/text_fields_table_new.png)

1. Select the name of the row from the left pane and select **Object** > **Binding** > **Repeat Row for Each Data Item**. Effectuez cette étape pour vous assurer que si une liaison est créée entre les cellules de tableau de cette ligne avec des objets de modèle de données de formulaire de type collection, la ligne de tableau est automatiquement répétée pour chaque élément de données disponible dans la base de données.

   Entrez du texte dans les cellules du tableau ou [créez une liaison avec les objets](create-interactive-communication.md#step2) du modèle de données de formulaire uniquement lors de la création de la communication interactive.

1. Sélectionnez **Fichier** > **Enregistrer sous** pour enregistrer le fichier sur le système de fichiers local :

   1. Accédez à l’emplacement d’enregistrement du fichier et spécifiez le nom du modèle XDP.
   1. Sélectionnez **.xdp** dans la liste déroulante **Type**.

   1. Appuyez sur **Enregistrer**.

### Télécharger le modèle XDP sur le serveur AEM Forms {#uploadxdptemplate}

Une fois que vous avez créé un modèle XDP à l’aide de Forms Designer, vous devez le télécharger sur le serveur AEM Forms pour qu’il soit disponible lors de la création de la communication interactive.

1. Sélectionnez **Formulaires** > **Formulaires et documents**.
1. Appuyez sur **Create** (Créer) > **File Upload** (Téléchargement de fichier). 
1. Accédez à l’emplacement du modèle XDP sur le système de fichiers local et appuyez sur **Ouvrir** pour importer le modèle XDP sur le serveur AEM Forms.

## Utilisation d’un schéma {#using-schema}

Vous pouvez utiliser un schéma dans une mise en page ou dans un fragment de mise en page, mais ce n’est pas obligatoire. Si vous utilisez un schéma, vérifiez les éléments suivants :

1. La mise en page et tous les fragments de mise en page utilisés dans une lettre/communication interactive utilisent le même schéma que la lettre/communication interactive.
1. Tous les champs obligatoires à remplir avec des données sont liés au schéma.

## Création de champs associables {#creating-relatable-fields}

Par défaut, tous les champs sont considérés comme pouvant être associés à diverses sources de données. Si votre mise en page contient des champs qui ne sont pas associables à une source de données, nommez ces champs à l’aide d’un suffixe « _int » (interne), par exemple pageCount_int.

Un champ associable doit :

* être un XFA &lt;field> ou &lt;exclGroup>
* disposer d’une référence de liaison XFA ;
* s’il s’agit d’un champ &lt;exclGroup>, il doit contenir au moins un champ de bouton radio enfant, faute de quoi son type de valeur ne pourra pas être déterminé.

Un champ associable doit :

* avoir un nom.

Un champ associable ne doit pas :

* inclure de suffixe « _int » dans son nom ;
* avoir une liaison définie comme « aucune » ;
* être l’enfant d’un élément &lt;exclGroup>

Dès lors qu’un champ associable répond aux critères décrits ci-dessus, il peut être situé à n’importe quel emplacement et dans n’importe quel niveau d’imbrication de la mise en page. Vous pouvez utiliser les champs associables dans les pages de gabarit.

La configuration de la mise en page des champs est plus flexible que celle des sous-formulaires de zone cible. Mais les champs sont liés à un seul type de valeur. Vous pouvez définir un champ pour qu’il soit grand ou définir le champ avec une hauteur ou une largeur fixes, etc. Le résultat du module ou de la règle est envoyé dans le champ. 

## Quand utiliser des sous-formulaires et des champs de texte {#deciding-when-to-use-subforms-and-text-nbsp-fields}

Utilisez un sous-formulaire si vous voulez capturer plusieurs contenus de module dans une mise en forme de haut en bas à flux vertical (plusieurs paragraphes ou images). Votre mise en page doit gérer le fait que le sous-formulaire se développe en hauteur afin d’accueillir son contenu. Si vous n’êtes pas sûr que la longueur du contenu associé au sous-formulaire/à la cible ne dépassera jamais l’espace réservé dans la mise en page pour le sous-formulaire, créez ce dernier en tant qu’enfant dans un conteneur de sous-formulaires à mise en page souple. Cette procédure garantit que les objets de mise en page situés en dessous du sous-formulaire se déplaceront vers le bas au fur et à mesure que le sous-formulaire s’agrandira.

Utilisez un champ si vous souhaitez capturer dans votre schéma de mise en page des données de module ou d’élément du dictionnaire de données (car les champs sont liés à des données) ou pour afficher un contenu de module dans une page de gabarit. N’oubliez pas que le contenu d’une page de gabarit ne présente pas une mise en page souple modulable en fonction du contenu de la page. Assurez-vous donc que le champ d’image est utilisé comme logo de l’en-tête. Le tableau qui suit indique plusieurs critères permettant de décider quand utiliser un sous-formulaire ou un champ dans une mise en page.

<table>
 <tbody>
  <tr>
   <td><p><strong>Utilisez un sous-formulaire lorsque</strong></p> </td>
   <td><p><strong>Utilisez un champ de texte lorsque</strong></p> </td>
  </tr>
  <tr>
   <td><p>Il contient une combinaison d’éléments, tels que Nom de famille et Prénom.</p> </td>
   <td><p>Il contient un seul élément, tel que Numéro de police.</p> </td>
  </tr>
  <tr>
   <td><p>Il comprend plusieurs paragraphes.</p> </td>
   <td><p>Le texte passe à la ligne suivante et est justifié.</p> </td>
  </tr>
  <tr>
   <td><p>Les groupes de données conditionnels, facultatifs et répétitifs sont liés à des sous-formulaires afin de réduire le risque d’erreurs de conception susceptibles de survenir lorsque des scripts sont utilisés pour obtenir les mêmes résultats.</p> </td>
   <td><p>Les éléments tels que le logo et l’adresse de votre organisation apparaissent sur toutes les pages d’une lettre/communication interactive. Dans ce cas, créez des champs de formulaire pour ces éléments et placez-les sur la page de gabarit. Si vous définissez la liaison du champ sur « Aucune liaison de données », le champ Aucun champ apparaît comme champ associable dans l’Éditeur de lettre/communication interactive. Si vous souhaitez associer certains types de contenu à ces champs, ces derniers doivent contenir des liaisons.</p> <p>Si l’adresse de votre société contient plusieurs lignes de données, utilisez deux champs de texte avec l’option « Autoriser plusieurs lignes » pour représenter l’adresse dans la mise en page.</p> <p>Si le type de données d’un champ de texte est défini comme texte brut, la sortie du module se fait en version texte brut plutôt qu’en version texte enrichi (toutes les mises en forme sont ignorées). Pour conserver la mise en forme, définissez le type de données du champ de texte comme texte enrichi.</p> </td>
  </tr>
  <tr>
   <td><p>Le texte fait l’objet d’une mise en page souple.</p> </td>
   <td><p>Les champs de texte et d’image sont utilisés dans les pages de gabarit. Les pages de gabarit ne peuvent pas utiliser de sous-formulaires comme zones cible.</p> </td>
  </tr>
  <tr>
   <td><p>Les objets sont groupés et organisés sans lier le sous-formulaire à un élément de données.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Le sous-formulaire contient un champ de texte. Le sous-formulaire peut s’agrandir sans écraser les autres objets situés plus bas dans la mise en page.</p> </td>
   <td><p>Vous avez besoin d’accéder facilement à ses données dans le post-traitement.</p> </td>
  </tr>
 </tbody>
</table>

## Configuration d’éléments répétitifs {#setting-up-repetitive-elements}

Lorsque des éléments comme le logo et l’adresse de votre organisation figurent sur toutes les pages d’une lettre/communication interactive, créez des champs de formulaire pour ces éléments et placez-les sur la page de gabarit. Utilisez la liaison Nom (Nom du champ) pour ces champs.

## Specify the server render format {#specify-the-server-nbsp-render-format}

Utilisez le format de rendu du serveur de la mise en page pour le formulaire XML dynamique, faute de quoi aucune lettre/communication interactive basée sur cette mise en page ne s’affichera correctement. Par défaut, le format de rendu du serveur dans LiveCycle Designer est défini comme formulaire XML dynamique. Pour vous assurer que vous utilisez le format correct :

* Dans Designer, cliquez sur **Fichier** > **Propriétés de formulaire** > **Valeurs par défaut** et assurez-vous que la configuration de Format/Rendu PDF est définie comme formulaire XML dynamique.

