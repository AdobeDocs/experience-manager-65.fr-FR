---
title: Utiliser la signature tactile dans les formulaires HTML5
description: Les formulaires HTML5 sont de plus en plus utilisés sur les appareils tactiles, qui prennent tous en charge les signatures. La signature de documents sur les appareils mobiles est devenue une méthode reconnue pour signer des formulaires sur les appareils mobiles.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Forms Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '655'
ht-degree: 100%

---

# Utiliser la signature tactile dans les formulaires HTML5{#using-scribble-signature-in-html-forms}

Les formulaires HTML5 sont de plus en plus utilisés sur les appareils tactiles, qui prennent tous en charge les signatures. Le scribing (avec un stylet ou un doigt) est devenue une méthode reconnue pour signer des formulaires sur les appareils mobiles. Les formulaires HTML5 et Forms Designer offrent désormais la possibilité d’afficher un champ de signature tactile dans le formulaire. Lors du rendu du formulaire dans le navigateur, vous pouvez vous connecter à ces champs à l’aide d’un stylet, d’une souris ou de votre doigt.

## Comment concevoir un formulaire à l’aide d’un champ de signature tactile {#how-to-design-a-form-using-scribble-signature-field}

1. Ouvrez un formulaire dans Forms Designer.
1. Faites glisser le champ de signature tactile vers la page.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Les dimensions du champ sélectionné dans Forms Designer sont reflétées quand le champ est rendu. Toutefois, la dimension de la zone de signature rendue est calculée en fonction du format du champ et non de la dimension spécifiée dans Forms Designer.

1. Configurez le champ de signature tactile.

   Par défaut, le champ de signature tactile marque les informations de géolocalisation comme étant obligatoires pendant le processus de signature sur iPad (elles sont facultatives sur les autres appareils). Ce comportement par défaut peut être remplacé en modifiant la valeur de la propriété `geoLocMandatoryOnIpad`. Cette propriété est exposée sous la forme d’extras dans le champ de signature tactile. Les étapes de modification sont les suivantes :

   1. Sur le formulaire, sélectionnez le champ de signature tactile.
   1. Sélectionnez l’onglet **Source XML**.

      >[!NOTE]
      >
      >Pour ouvrir l’onglet Source XML, cliquez sur **Affichage** > **Source XML**.

   1. Recherchez la balise `<ui>` dans la balise `<field>` et modifiez le code source pour qu’il ressemble à l’exemple suivant :

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Sélectionnez l’onglet **Vue Conception**. Sur la page de confirmation, cliquez sur **Oui**.
   1. Enregistrez le formulaire.

1. Effectuez le rendu du formulaire sur un navigateur d’appareil mobile/de bureau pris en charge.

## Interface avec les signatures tactiles {#interfacing-with-the-scribble-signatures}

### Signature {#signing}

Une fois qu’un champ de signature tactile a été ajouté au formulaire et rendu, cliquez ou appuyez sur le champ pour ouvrir une boîte de dialogue. L’utilisateur ou utilisatrice peut apposer une signature tactile dans la zone de dessin désignée par un rectangle en pointillés, à l’aide d’une souris, d’un doigt ou d’un stylet.

![géolocalisation](assets/geolocation.png)

**A.** Pinceau **B.** Gomme **C.** Géolocalisation **D.** Informations de géolocalisation

### Géo-balisage {#geo-tagging}

Lorsque vous cliquez sur l’icône de géolocalisation lors de la création de la saisie tactile, l’emplacement géographique et la date/l’heure sont ajoutés au champ.

>[!NOTE]
>
Sur iPad, l’incorporation des informations de géolocalisation est obligatoire par défaut.

Sur iPad, l’icône de géolocalisation n’est pas affichée par défaut et les informations de géolocalisation sont automatiquement incorporées lorsque vous cliquez sur **OK**.

Pour les iPad, ce paramètre peut être modifié en remplaçant la valeur du paramètre `geoLocManadatoryOnIpad` par `0`, dans les paramètres initiaux du champ.

* Lorsque les informations de géolocalisation sont obligatoires, une zone de dessin réduite est présentée à l’utilisateur ou l’utilisatrice. Le texte de géolocalisation est ajouté lorsque l’utilisateur ou l’utilisatrice clique sur l’icône **OK** sur la zone restante.
* Dans d’autres cas, l’utilisateur ou l’utilisatrice se voit présenter une zone entièrement dédiée au dessin. Si l’utilisateur ou l’utilisatrice choisit d’incorporer des informations de géolocalisation, cette zone est redimensionnée pour s’adapter au texte de géolocalisation.

### Effacement d’une signature {#clearing-a-signature}

Lorsque vous utilisez cette fonctionnalité, un utilisateur peut cliquer sur l’icône **Gomme** pour effacer le champ et recommencer. Si des informations de géolocalisation ont été ajoutées, elles seront également effacées.

### Enregistrement d’une signature {#saving-a-signature}

Cliquez sur l’icône **OK** pour enregistrer la signature sous forme d’image dans le champ. L’image et les valeurs peuvent être envoyées au serveur pour un traitement ultérieur. Une fois qu’un utilisateur a cliqué sur **OK**, la saisie tactile effectuée est verrouillée. La signature ne peut plus être modifiée à l’aide du widget de griffonnage.

Appuyez ou cliquez sur le champ de griffonnage pour ouvrir la boîte de dialogue en mode lecture seule.

![3](assets/3.png)

### Sélection de la taille du stylo {#selecting-pen-size}

Cliquez sur l’icône **Brosses** pour afficher la liste des tailles de stylo disponibles. Cliquez sur la taille de stylo correspondant au stylo à utiliser.

### Suppression des signatures du formulaire {#delete-signatures-from-the-form}

Pour supprimer les signatures du formulaire :

* (Périphériques mobiles) Appuyez de manière prolongée sur le champ de signature et, dans la boîte de dialogue de confirmation, sélectionnez **Oui**.
* (Ordinateur de bureau) Pointez sur le champ de signature, puis cliquez sur l’icône **Annuler** puis, dans la boîte de dialogue de confirmation, cliquez sur **Oui**.
