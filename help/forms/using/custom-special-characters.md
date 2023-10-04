---
title: Caractères spéciaux personnalisés dans Correspondence Management
description: Découvrez comment ajouter des caractères spéciaux personnalisés dans Correspondence Management.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 39%

---

# Caractères spéciaux personnalisés dans Correspondence Management{#custom-special-characters-in-correspondence-management}

## Présentation {#overview}

Correspondence Management dispose d’une prise en charge par défaut intégrée de 210 caractères spéciaux que vous pouvez facilement insérer dans les lettres.

Vous pouvez par exemple insérer les caractères spéciaux suivants :

* Symboles de devise tels que €,￥et £
* Symboles mathématiques tels que ∑, √, ∂ et ^
* Les symboles de ponctuation comme « et ».

Vous pouvez insérer des caractères spéciaux sous forme de lettres :

* Dans [l’éditeur de texte](/help/forms/using/document-fragments.md#createtext).
* Dans un [module modifiable et en ligne dans une correspondance](../../forms/using/create-correspondence.md#managecontent).

![caractères_spéciaux_dans_un_module_en_ligne](assets/specialcharactersinlinemodule.png)

L’administrateur peut ajouter la prise en charge de plus de caractères/de caractères spéciaux grâce à la personnalisation. Cet article fournit des instructions sur la manière d’ajouter la prise en charge de caractères spéciaux personnalisés supplémentaires.

## Ajout ou modification de la prise en charge des caractères spéciaux personnalisés dans Correspondence Management {#creatingfolderstructure}

Procédez comme suit pour ajouter la prise en charge des caractères spéciaux personnalisés :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Dans le dossier des applications, créez un dossier nommé **[!UICONTROL specialcharacters]** avec un chemin/une structure similaires au dossier specialcharacters (dans le dossier textEditorConfig sous libs) :

   1. Cliquez avec le bouton droit sur le dossier **specialcharacters** au chemin d’accès suivant et sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin d’accès :** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **Emplacement du recouvrement :** /apps/

      **Correspondance des types de nœuds :** activé.

      >[!NOTE]
      >
      >Ne modifiez pas la branche /libs . Toute modification que vous apportez peut être perdue, car cette branche est susceptible de changer lorsque vous :
      >
      >
      >
      >    * Effectuez une mise à niveau sur votre instance
      >    * Appliquer un correctif
      >    * Installation d’un Feature Pack
      >
      >

   1. Cliquez sur **OK**, puis sur **Enregistrer tout**. Le dossier specialcharacters est créé dans le chemin d’accès spécifié.

      Après avoir créé la superposition, vérifiez les balises de structure de noeud. Chaque noeud créé dans /apps à l’aide de la superposition doit avoir la même classe et les mêmes propriétés que celles définies dans /libs pour ce noeud. Si une propriété ou une balise est manquante dans la structure de noeud sous l’emplacement /apps , synchronisez ses balises avec le noeud correspondant dans /libs.

1. Assurez-vous que la variable **[!UICONTROL textEditorConfig]** possède les propriétés et valeurs suivantes :

   | Nom | Type | Valeur |
   |---|---|---|
   | cmConfigurationType | Chaîne | cmTextEditorConfiguration |
   | cssPath | Chaîne | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Cliquez avec le bouton droit sur le dossier **[!UICONTROL specialcharacters]** au chemin d’accès suivant et sélectionnez **Créer > Nœud enfant**, puis cliquez sur **Enregistrer tout** :

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance . Le noeud que vous avez ajouté est le dernier de la liste des caractères spéciaux dans l’interface utilisateur.
1. Cliquez sur **Enregistrer tout**.
1. Modifications apportées aux caractères spéciaux suivant les besoins :

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
     <li>Actualisez l’interface utilisateur Éditeur de texte\Création de correspondance afin que vous puissiez voir les modifications.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Mettre à jour les propriétés d’un caractère spécial existant</td>
   <td>
    <ol>
     <li>Recouvrez le noeud à mettre à jour comme expliqué ci-dessus et vérifiez les balises et les classes.</li>
     <li>Modifiez toutes les valeurs, telles que caption, value, endValue et multipleCaption. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez l’interface utilisateur Éditeur de texte\Création de correspondance afin que vous puissiez voir les modifications.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Masquer un caractère spécial</td>
   <td>
    <ol>
     <li>Recouvrez le nœud à masquer sous « /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters ».</li>
     <li>Ajoutez la propriété sling:hideResource (booléenne) au nœud à masquer (sous applications). </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez l’interface utilisateur Éditeur de texte\Création de correspondance afin que vous puissiez voir les modifications.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Masquer plusieurs caractères spéciaux</td>
   <td>
    <ol>
     <li>Ajoutez la propriété « sling:hideChildren (String or String[]) » sous « /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters ». </li>
     <li>Ajoutez des noms de noeud (caractères spéciaux à masquer) comme valeurs pour la propriété "sling:hideChildren". </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez l’interface utilisateur Éditeur de texte\Création de correspondance afin que vous puissiez voir les modifications.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordre des caractères spéciaux</td>
   <td>
    <ol>
     <li>Ajoutez un nœud enfant sous « /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters » avec les propriétés obligatoires. </li>
     <li>Ajoutez la propriété "sling:orderBefore (String)" au noeud enfant nouvellement créé. </li>
     <li>Ajoutez le nom du noeud comme valeur devant laquelle le caractère spécial nouvellement ajouté doit s’afficher. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez l’interface utilisateur Éditeur de texte\Création de correspondance afin que vous puissiez voir les modifications.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
