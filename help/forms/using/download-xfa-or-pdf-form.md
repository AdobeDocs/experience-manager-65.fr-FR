---
title: Téléchargement d’un modèle de formulaire XFA ou PDF
seo-title: Download an XFA or a PDF form template
description: Vous pouvez exporter des formulaires du référentiel vers le système local et faire migrer les formulaires téléchargés vers le nouveau référentiel.
seo-description: You can export forms from the repository to the local system and migrate the downloaded forms to new repository.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 100%

---

# Téléchargement d’un modèle de formulaire XFA ou PDF {#download-an-xfa-or-a-pdf-form-template}

L’opération de téléchargement, comme son nom l’indique, permet d’exporter des formulaires du référentiel vers le système local. Associée à l’opération de transfert, elle vous permet de faire migrer des formulaires d’un référentiel vers un autre.

Dans AEM Forms, l’opération de téléchargement est prise en charge pour les types de ressource suivants :

* Modèles de formulaire (formulaires XFA)
* Formulaires PDF
* Documents (fichiers PDF aplatis)

AEM Forms prend en charge le téléchargement de ces types de ressource de manière individuelle ou dans un dossier contenant un ou plusieurs formulaires pris en charge.

Outre ces ressources, vous pouvez télécharger le type `Resource` de ressources s’il est présent dans un dossier. L’objectif de cette fonctionnalité est de vous permettre de télécharger la ressource à laquelle fait référence un formulaire XFA, ainsi que le formulaire proprement dit.

## Téléchargement d’un ou de plusieurs formulaires {#download-one-or-more-forms}

1. Connectez-vous à l’interface utilisateur d’AEM Forms à l’adresse `https://<server>:<port>/aem/forms.html`.

1. Accédez à l’emplacement de la ressource que vous souhaitez télécharger.

1. Sélectionnez la ressource. Cliquez sur l’icône **[!UICONTROL Télécharger]** ![aem6forms_download](assets/aem6forms_download.png) dans la barre d’outils.

   >[!NOTE]
   >
   >Vous ne pouvez sélectionner qu’un seul formulaire à télécharger. Si vous souhaitez télécharger plusieurs formulaires, vous devez les télécharger en tant que dossier.

1. Dans la boîte de dialogue qui s’affiche, cliquez sur **[!UICONTROL Télécharger]**.

   AEM Forms génère un fichier ZIP qui contient le fichier ou le dossier sélectionné.

   Si vous téléchargez un dossier, les ressources prises en charge dans le dossier sont téléchargées dans la hiérarchie existante.

   Le fichier ZIP est enregistré dans le dossier `Downloads` sur votre système.

## Remarques relatives à l’opération de transfert {#related-considerations-for-the-upload-operation}

* Vous pouvez transférer un fichier ZIP vers tout autre emplacement dans le même référentiel ou dans un autre.
* La hiérarchie des ressources d’un dossier est conservée pendant l’opération de transfert.
* Toute modification des métadonnées apportée aux ressources téléchargées avant le téléchargement est répercutée lors du transfert. 
