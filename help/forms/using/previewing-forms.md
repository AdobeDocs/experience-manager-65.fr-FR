---
title: Prévisualisation d’un formulaire
seo-title: Prévisualisation d’un formulaire
description: Vous pouvez prévisualiser vos formulaires avant de les publier ou de les activer pour vérifier qu’ils répondent à vos attentes. Les options d’aperçu peuvent varier en fonction des types de formulaire pris en charge.
seo-description: Vous pouvez prévisualiser vos formulaires avant de les publier ou de les activer pour vérifier qu’ils répondent à vos attentes. Les options d’aperçu peuvent varier en fonction des types de formulaire pris en charge.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Formulaires adaptatifs
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 100%

---

# Prévisualisation d’un formulaire {#previewing-a-form}

## Présentation {#overview}

Dans AEM Forms, vous pouvez prévisualiser les formulaires et les documents figurant dans le référentiel. En procédant de la sorte, vous pouvez déterminer exactement l’apparence et le comportement des formulaires lorsqu’ils sont publiés pour les utilisateurs finaux.

Lorsque vous prévisualisez des formulaires, ils sont rendus dans une interface interactive et l’utilisateur peut les remplir avec des données. Lorsque vous prévisualisez des documents, ils sont rendus en mode non interactif et l’utilisateur peut uniquement les afficher. Pour les formulaires, une option supplémentaire d’aperçu personnalisé est disponible. Grâce à cette option, vous pouvez prévisualiser le formulaire à l’aide des données provenant d’un fichier XML. Ces données remplissent certains champs ou tous les champs du formulaire prévisualisé.

Le tableau ci-dessous répertorie les options d’aperçu disponibles pour les différents types de formulaire pris en charge :

<table>
 <tbody>
  <tr>
   <td><strong>Type de ressource</strong><br /> </td>
   <td><strong>Options d’aperçu disponibles</strong><br /> </td>
  </tr>
  <tr>
   <td>Document</td>
   <td>Aperçu au format PDF</td>
  </tr>
  <tr>
   <td>Formulaire PDF</td>
   <td>Aperçu au format PDF et aperçu avec des données<br /> </td>
  </tr>
  <tr>
   <td>Formulaire adaptatif</td>
   <td>Aperçu au format HTML et aperçu au format HTML avec des données</td>
  </tr>
  <tr>
   <td>Modèle de formulaire</td>
   <td>Aperçu au format PDF, aperçu au format PDF avec des données, aperçu HTML, aperçu au format HTML avec des données<br /> </td>
  </tr>
 </tbody>
</table>

## Prévisualisation d’un formulaire {#previewing-a-form-1}

1. Sélectionnez une ressource à prévisualiser, puis cliquez sur Aperçu de ![aem6forms_preview](assets/aem6forms_preview.png) dans la barre d’outils Actions.

   >[!NOTE]
   >
   >Pour sélectionner une ressource, passez en mode Liste à partir de la vue Carte par défaut. Cliquez sur ![aem6forms_viewlist](assets/aem6forms_viewlist.png) ou ![aem6forms_viewcard](assets/aem6forms_viewcard.png) pour changer de vue.

1. Lorsque vous cliquez sur Aperçu, les options d’aperçu applicables pour le type d’actif sélectionné sont affichées. Cliquez sur l’option souhaitée pour effectuer le rendu de l’actif sélectionné dans un nouvel onglet.

   Vous avez le choix entre :

   * Aperçu au format HTML
   * Aperçu avec des données
   * Aperçu au format PDF (disponible pour les modèles de formulaire)

## Aperçu avec des données {#preview-with-data}

Lorsque vous sélectionnez **Aperçu avec des données**, vous pouvez voir à quoi ressemble le formulaire avec des données réelles saisies. L’option Aperçu avec des données vous permet de télécharger un fichier XML contenant des exemples de données d’utilisateurs. Les exemples de données d’utilisateurs sont utilisées pour renseigner le formulaire d’aperçu au format que vous choisissez.

1. Sélectionnez une ressource, cliquez sur Aperçu ![aem6forms_preview](assets/aem6forms_preview.png), puis sélectionnez **Aperçu avec des données**.
1. Dans la boîte de dialogue Aperçu du formulaire, fournissez FormData en tant que fichier XML. Cliquez sur Aperçu pour effectuer le rendu du formulaire avec les données fusionnées du fichier XML.
