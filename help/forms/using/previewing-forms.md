---
title: Prévisualisation d’un formulaire
description: Vous pouvez prévisualiser vos formulaires avant de les publier ou de les activer pour vous assurer qu’ils répondent aux attentes. Les options de prévisualisation peuvent varier selon les types de formulaire pris en charge.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms,Foundation Components
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 100%

---

# Prévisualisation d’un formulaire {#previewing-a-form}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

## Vue d’ensemble {#overview}

Dans AEM Forms, vous pouvez prévisualiser les formulaires et les documents figurant dans le référentiel. La prévisualisation permet de savoir exactement à quoi ressemblent les formulaires lorsqu’ils sont publiés pour les utilisatrices et utilisateurs finaux.

Lors de la prévisualisation de formulaires, ils sont rendus dans l’interface interactive et l’utilisateur ou l’utilisatrice peut les remplir avec des données. Lors de la prévisualisation de documents, ils sont rendus en mode non interactif et l’utilisateur ou l’utilisatrice peut uniquement les afficher. Pour les formulaires, une option supplémentaire de prévisualisation personnalisée est disponible. Grâce à cette option, vous pouvez prévisualiser le formulaire à l’aide des données d’un fichier XML. Les données remplissent certains ou tous les champs du formulaire prévisualisé.

Le tableau ci-dessous répertorie les options d’aperçu disponibles pour les différents types de formulaire pris en charge :

<table>
 <tbody>
  <tr>
   <td><strong>Type de ressource</strong><br /> </td>
   <td><strong>Options d’aperçu disponibles</strong><br /> </td>
  </tr>
  <tr>
   <td>Document</td>
   <td>Prévisualisation du PDF</td>
  </tr>
  <tr>
   <td>Formulaire PDF</td>
   <td>Aperçu au format PDF et aperçu avec des données<br /> </td>
  </tr>
  <tr>
   <td>Formulaire adaptatif</td>
   <td>Prévisualisation HTML et prévisualisation HTML avec des données</td>
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
   >Pour sélectionner une ressource, basculez vers la vue Liste à partir de la vue Carte par défaut. Cliquez sur ![aem6forms_viewlist](assets/aem6forms_viewlist.png) ou ![aem6forms_viewcard](assets/aem6forms_viewcard.png) pour changer de vue.

1. Lorsque vous cliquez sur Aperçu, les options d’aperçu applicables pour le type d’actif sélectionné sont affichées. Cliquez sur l’option souhaitée pour effectuer le rendu de la ressource sélectionnée dans un nouvel onglet.

   Vous avez le choix entre :

   * Prévisualiser au format HTML
   * Aperçu avec des données
   * Aperçu au format PDF (disponible pour les modèles de formulaire)

## Aperçu avec des données {#preview-with-data}

Lorsque vous sélectionnez **Aperçu avec des données**, vous pouvez voir à quoi ressemble le formulaire avec des données réelles saisies. L&#39;option Aperçu avec des données vous permet de charger un fichier XML contenant des exemples de données utilisateur. Les exemples de données utilisateur sont utilisés pour remplir le formulaire prévisualisé au format que vous choisissez.

1. Sélectionnez une ressource, cliquez sur Aperçu ![aem6forms_preview](assets/aem6forms_preview.png), puis sélectionnez **Aperçu avec des données**.
1. Dans la boîte de dialogue Aperçu du formulaire, fournissez FormData en tant que fichier XML. Cliquez sur Aperçu pour effectuer le rendu du formulaire avec les données fusionnées du fichier XML.
