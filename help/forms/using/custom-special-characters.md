---
title: Caractères spéciaux personnalisés dans Correspondence Management
description: Découvrez comment ajouter des caractères spéciaux personnalisés dans Correspondence Management.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 98%

---

# Caractères spéciaux personnalisés dans Correspondence Management{#custom-special-characters-in-correspondence-management}

## Présentation {#overview}

Correspondence Management offre une prise en charge par défaut et intégrée de 210 caractères spéciaux que vous pouvez facilement insérer sous forme de lettres.

Vous pouvez par exemple insérer les caractères spéciaux suivants :

* Symboles de devise tels que €,￥et £
* Symboles mathématiques tels que ∑, √, ∂ et ^
* Les symboles de ponctuation comme « et ».

Vous pouvez insérer des caractères spéciaux sous forme de lettres :

* Dans [l’éditeur de texte](/help/forms/using/document-fragments.md#createtext).
* Dans un [module modifiable et en ligne dans une correspondance](../../forms/using/create-correspondence.md#managecontent).

![caractères_spéciaux_dans_un_module_en_ligne](assets/specialcharactersinlinemodule.png)

L’administrateur peut ajouter la prise en charge de plus de caractères/de caractères spéciaux grâce à la personnalisation. Cet article fournit les instructions vous permettant d’ajouter la prise en charge de caractères spéciaux personnalisés supplémentaires.

## Ajouter ou modifier la prise en charge des caractères spéciaux personnalisés dans Correspondence Management {#creatingfolderstructure}

Procédez comme suit pour ajouter la prise en charge des caractères spéciaux personnalisés :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Dans le dossier des applications, créez un dossier nommé **[!UICONTROL specialcharacters]** dont le chemin d’accès/la structure est similaire au dossier specialcharacters (situé dans le dossier textEditorConfig sous libs) :

   1. Cliquez avec le bouton droit sur le dossier **specialcharacters** au chemin d’accès suivant et sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin d’accès :** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **Emplacement du recouvrement :** /apps/

      **Correspondance des types de nœuds :** activé.

      >[!NOTE]
      >
      >Ne modifiez pas la branche /libs. Toutes les modifications que vous apportez risquent d’être perdues, car cette branche est exposée aux modifications chaque fois que vous :
      >
      >
      >
      >    * Effectuez une mise à niveau sur votre instance.
      >    * Appliquez un correctif.
      >    * Installez un pack de fonctionnalités.
      >
      >

   1. Cliquez sur **OK**, puis sur **Enregistrer tout**. Le dossier specialcharacters est créé dans le chemin d’accès spécifié.

      Après avoir créé le recouvrement, vérifiez les balises de structure de nœud. Chaque nœud créé dans /apps à l’aide du recouvrement doit présenter la même classe et les mêmes propriétés que celles définies dans /libs pour ce nœud. Si une propriété ou une balise est manquante dans la structure de nœud sous l’emplacement /apps, synchronisez ses balises avec le nœud correspondant situé sous /libs.

1. Vérifiez que le nœud **[!UICONTROL textEditorConfig]** est doté des valeurs et propriétés suivantes :

   | Nom | Type | Valeur |
   |---|---|---|
   | cmConfigurationType | Chaîne | cmTextEditorConfiguration |
   | cssPath | Chaîne | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Cliquez avec le bouton droit sur le dossier **[!UICONTROL specialcharacters]** au chemin d’accès suivant et sélectionnez **Créer > Nœud enfant**, puis cliquez sur **Enregistrer tout** :

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance. Le nœud que vous avez ajouté apparaît en dernier dans la liste des caractères spéciaux de l’interface utilisateur.
1. Cliquez sur **Enregistrer tout**.
1. Apportez les modifications nécessaires aux caractères spéciaux :

<table>
 <tbody>
  <tr>
   <td><strong>To...</strong></td>
   <td><strong>Effectuez les étapes suivantes</strong></td>
  </tr>
  <tr>
   <td>Ajouter un caractère spécial personnalisé</td>
   <td>
    <ol>
     <li>Ajoutez un nœud enfant sous « /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters » avec les propriétés obligatoires.</li>
     <li>Cliquez sur Enregistrer tout</li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Mettez à jour les propriétés d’un caractère spécial existant.</td>
   <td>
    <ol>
     <li>Recouvrez le nœud pour qu’il soit mis à jour comme expliqué ci-dessus et vérifiez les balises et les classes.</li>
     <li>Remplacez toutes les valeurs, telles que caption, value, endValue et multipleCaption. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Masquer un caractère spécial</td>
   <td>
    <ol>
     <li>Recouvrez le nœud à masquer sous « /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters ».</li>
     <li>Ajoutez la propriété sling:hideResource (booléenne) au nœud à masquer (sous applications). </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Masquer plusieurs caractères spéciaux</td>
   <td>
    <ol>
     <li>Ajoutez la propriété « sling:hideChildren (String or String[]) » sous « /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters ». </li>
     <li>Ajoutez des noms de nœud (caractères spéciaux à masquer) sous forme de valeurs pour la propriété sling:hideChildren. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Classement des caractères spéciaux</td>
   <td>
    <ol>
     <li>Ajoutez un nœud enfant sous « /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters » avec les propriétés obligatoires. </li>
     <li>Ajoutez la propriété "sling:orderBefore (String)" au noeud enfant nouvellement créé. </li>
     <li>Ajoutez le nom du nœud comme valeur devant laquelle le caractère spécial récemment ajouté doit être affiché. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
