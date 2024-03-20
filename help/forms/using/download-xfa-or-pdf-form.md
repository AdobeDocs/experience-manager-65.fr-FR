---
title: Télécharger un modèle de formulaire XFA ou PDF
description: Vous pouvez exporter des formulaires du référentiel vers le système local et migrer les formulaires téléchargés vers le nouveau référentiel.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 40%

---

# Télécharger un modèle de formulaire XFA ou PDF {#download-an-xfa-or-a-pdf-form-template}

L’opération de téléchargement, comme son nom l’indique, vous permet d’exporter des formulaires du référentiel vers le système local. Associée à l’opération de chargement, cette opération vous permet de migrer vos formulaires d’un référentiel vers un autre.

Dans AEM Forms, l’opération de téléchargement est prise en charge pour les types de ressources suivants :

* Modèles de formulaire (XFA Forms)
* Formulaires PDF
* Documents (fichiers de PDF plats)

AEM Forms prend en charge le téléchargement de ces types de formulaires individuellement ou dans un dossier contenant un ou plusieurs formulaires pris en charge.

Outre ces ressources, vous pouvez télécharger le type `Resource` de ressources s’il est présent dans un dossier. L’objectif de cette fonctionnalité est de vous permettre de télécharger la ressource à laquelle fait référence un formulaire XFA, ainsi que le formulaire proprement dit.

## Téléchargement d’un ou de plusieurs formulaires {#download-one-or-more-forms}

1. Connectez-vous à l’interface utilisateur d’AEM Forms à l’adresse `https://<server>:<port>/aem/forms.html`.

1. Accédez à l’emplacement de la ressource que vous souhaitez télécharger.

1. Sélectionnez la ressource. Cliquez sur l’icône **[!UICONTROL Télécharger]** ![aem6forms_download](assets/aem6forms_download.png) dans la barre d’outils.

   >[!NOTE]
   >
   >Vous ne pouvez sélectionner qu’un seul formulaire à télécharger. Si vous souhaitez télécharger plusieurs formulaires, vous devez les télécharger sous la forme d’un dossier.

1. Dans la boîte de dialogue qui s’affiche, cliquez sur **[!UICONTROL Télécharger]**.

   AEM Forms génère un fichier ZIP contenant le fichier sélectionné ou le dossier sélectionné.

   Si vous téléchargez un dossier, les ressources prises en charge dans le dossier sont téléchargées dans leur hiérarchie existante.

   Le fichier ZIP est enregistré dans le dossier `Downloads` sur votre système.

## Remarques relatives à l’opération de chargement {#related-considerations-for-the-upload-operation}

* Vous pouvez charger le fichier ZIP vers n’importe quel autre emplacement du même référentiel ou d’un autre référentiel.
* La hiérarchie des ressources d’un dossier est conservée pendant l’opération de chargement.
* Toute modification des métadonnées apportée aux ressources téléchargées avant le téléchargement est répercutée lors du transfert. 
