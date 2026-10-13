---
title: Enregistrer un formulaire HTML5 en tant que brouillon
description: Enregistrez un formulaire HTML5 comme brouillon et reprenez le remplissage du formulaire ultérieurement.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 100%
---
# Enregistrer un formulaire HTML5 en tant que brouillon {#saving-an-html-form-as-a-draft}

Vous pouvez enregistrer un formulaire HTML5 comme brouillon et reprendre le remplissage du formulaire ultérieurement. Le Portail Formulaires permet aux utilisateurs et aux utilisatrices d’enregistrer et de restaurer un formulaire HTML5. Pour activer la fonctionnalité d’enregistrement en tant que brouillon, ajoutez les configurations suivantes au nœud de profil :

## Profil personnalisé permettant d’activer la fonctionnalité Enregistrer en tant que brouillon {#custom-profile-to-allow-save-as-draft-feature}

En standard, AEM Forms fournit un profil **Enregistrer en tant que brouillon**. Vous pouvez effectuer le rendu d’un formulaire avec le profil Enregistrer en tant que brouillon pour activer la fonctionnalité de brouillon pour un formulaire HTML5. Vous pouvez spécifier le profil de rendu HTML pour un formulaire dans [Forms Manager](/help/forms/using/introduction-managing-forms.md).

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
   <td><p>Active la fonctionnalité Enregistrer en tant que brouillon</p> <p>pour ce profil.</p> </td>
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

Après l’activation de la fonctionnalité Enregistrer en tant que brouillon pour un formulaire, lorsque le formulaire est enregistré, il est répertorié dans le [composant Drafts and Submissions](/help/forms/using/draft-submission-component.md). Vous pouvez récupérer le formulaire enregistré et commencer son remplissage depuis le composant Drafts and Submissions.

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
