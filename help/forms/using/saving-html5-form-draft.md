---
title: Enregistrement d’un formulaire HTML5 en tant que brouillon
seo-title: Enregistrement d’un formulaire HTML5 en tant que brouillon
description: Enregistrez un formulaire HTML5 comme brouillon et reprenez le remplissage du formulaire ultérieurement.
seo-description: Enregistrez un formulaire HTML5 comme brouillon et reprenez le remplissage du formulaire ultérieurement.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 66%

---


# Enregistrement d’un formulaire HTML5 en tant que brouillon {#saving-an-html-form-as-a-draft}

Vous pouvez enregistrer un formulaire HTML5 comme brouillon et reprendre le remplissage du formulaire ultérieurement. Le portail des formulaires permet à tout utilisateur d’enregistrer et de restaurer un formulaire HTML5. Pour activer la fonctionnalité Enregistrer en tant que brouillon, ajoutez les configurations suivantes au noeud de profil :

## Profil personnalisé permettant d&#39;activer la fonctionnalité Enregistrer en tant que brouillon {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms fournit un profil **Enregistrer en tant que brouillon** prêt à l’emploi. Vous pouvez générer un formulaire avec le profil Enregistrer en tant que brouillon pour activer la fonctionnalité de brouillon pour un formulaire HTML5. Vous pouvez spécifier le profil de rendu HTML pour un formulaire dans le [Gestionnaire de formulaires](/help/forms/using/introduction-managing-forms.md).

Pour activer la fonctionnalité Enregistrer en tant que brouillon pour votre [profil personnalisé](/help/forms/using/custom-profile.md) existant, ajoutez les propriétés suivantes à votre noeud de profil personnalisé :

<table>
 <tbody>
  <tr>
   <td><strong>Nom de la propriété</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>Chaîne</td>
   <td>true</td>
   <td><p>Active la fonction Enregistrer en tant que brouillon</p> <p>pour ce profil.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Chaîne</td>
   <td>true</td>
   <td><p>Autorise le chargement de pièces jointes</p> <p>avec ce profil.</p> </td>
  </tr>
 </tbody>
</table>

## Stockage et liste des brouillons  {#drafts-storage-and-listing}

Après l’activation de la fonctionnalité Enregistrer en tant que brouillon pour un formulaire, lorsque le formulaire est enregistré, il est répertorié dans le [composant Drafts and Submissions](/help/forms/using/draft-submission-component.md). Vous pouvez extraire le formulaire enregistré et commencer son remplissage depuis le composant Drafts and Submissions.

Pour activer la liste des formulaires pour le composant Drafts and Submission, ajoutez la propriété suivante au noeud de profil :

<table>
 <tbody>
  <tr>
   <td><strong>Nom de la propriété</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>Chaîne</td>
   <td>true</td>
   <td>Pour permettre aux brouillons et aux formulaires d’être répertoriés dans <br /> le composant Drafts &amp; Submissions du portail Forms après envoi</td>
  </tr>
 </tbody>
</table>

Par défaut, AEM Forms stocke les données utilisateur associées au brouillon et à l’envoi d’un formulaire dans le noeud /content/forms/fp de l’instance de publication. Vous pouvez ajouter votre fournisseur personnalisé de stockage. Pour plus de détails, consultez [Stockage personnalisé pour le composant Drafts and Submissions](/help/forms/using/adding-custom-storage-provider-forms.md).
