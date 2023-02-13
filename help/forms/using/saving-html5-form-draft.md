---
title: Enregistrer un formulaire HTML5 en tant que brouillon
seo-title: Saving an HTML5 form as a draft
description: Enregistrez un formulaire HTML5 comme brouillon et reprenez le remplissage du formulaire ultérieurement.
seo-description: Save an HTML5 form as a draft and resume filling the form at a later stage.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '300'
ht-degree: 100%

---

# Enregistrer un formulaire HTML5 en tant que brouillon {#saving-an-html-form-as-a-draft}

Vous pouvez enregistrer un formulaire HTML5 comme brouillon et reprendre le remplissage du formulaire ultérieurement. Le portail des formulaires permet à tout utilisateur d’enregistrer et de restaurer un formulaire HTML5. Pour activer la fonctionnalité d’enregistrement en tant que brouillon, ajoutez les configurations suivantes au nœud de profil :

## Profil personnalisé permettant d’activer la fonctionnalité Enregistrer en tant que brouillon {#custom-profile-to-allow-save-as-draft-feature}

En standard, AEM Forms fournit un profil **Enregistrer en tant que brouillon**. Vous pouvez générer un formulaire avec le profil Enregistrer en tant que brouillon pour activer la fonctionnalité de brouillon pour un formulaire HTML5. Vous pouvez spécifier le profil de rendu HTML pour un formulaire dans le [Gestionnaire de formulaires](/help/forms/using/introduction-managing-forms.md).

Pour activer la fonctionnalité Enregistrer en tant que brouillon et l’appliquer à votre [profil personnalisé](/help/forms/using/custom-profile.md) existant, ajoutez les configurations suivantes à votre nœud de profil :

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

## Stockage et liste des brouillons {#drafts-storage-and-listing}

Après l’activation de la fonctionnalité Enregistrer en tant que brouillon pour un formulaire, lorsque le formulaire est enregistré, il est répertorié dans le [composant Drafts and Submissions](/help/forms/using/draft-submission-component.md). Vous pouvez extraire le formulaire enregistré et commencer son remplissage depuis le composant Drafts and Submissions.

Pour activer les listes de formulaires du composant Brouillons et Envois, ajoutez la propriété suivante au nœud de profil :

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
   <td>Pour que les brouillons et les formulaires soient répertoriés dans le <br /> composant Brouillons et envois du portail Formulaires après envoi</td>
  </tr>
 </tbody>
</table>

Par défaut, AEM Forms stocke les données d’utilisateur associées au brouillon et à l’envoi d’un formulaire dans le nœud /content/forms/fp de l’instance de publication. Vous pouvez ajouter votre fournisseur personnalisé de stockage. Pour plus de détails, consultez [Stockage personnalisé pour le composant Drafts and Submissions](/help/forms/using/adding-custom-storage-provider-forms.md).
