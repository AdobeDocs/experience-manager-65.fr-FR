---
title: Supprimer des formulaires et des ressources associées
description: Comment supprimer un formulaire ou une ressource dans AEM Forms et son impact sur les ressources référencées et référentes et les formulaires XFA.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 29%

---

# Supprimer des formulaires et des ressources associées {#deleting-forms-and-related-resources}

Vous pouvez supprimer les formulaires et les actifs pour supprimer ces actifs du référentiel. L’opération de suppression fonctionne sur tous les types de ressources et dossiers.

Si vous supprimez une ressource de l’instance d’auteur, elle est également supprimée de l’instance de publication. Le serveur AEM Forms se compose des instances d’auteur et de publication. L’instance d’auteur est destinée à la création et à la gestion des ressources et des actifs de formulaires. L’instance Publier contient les actifs de formulaires publiés et les ressources associées disponibles pour les utilisateurs finaux.

## Suppression d’un formulaire {#how-to-delete-a-form}

1. Connectez-vous à l’interface utilisateur d’AEM Forms en accédant à `https://[hostname]:'port'/aem/forms.html.`.
1. Recherchez et sélectionnez le formulaire que vous souhaitez supprimer. Cliquez sur Supprimer ![aem6forms_delete2](assets/aem6forms_delete2.png) dans la barre d’outils et confirmez l’opération de suppression.

   >[!NOTE]
   >
   >Un seul formulaire peut être supprimé à la fois. Vous pouvez supprimer plusieurs formulaires séparément ou supprimer le dossier parent.

1. Avant de supprimer une ressource, AEM Forms recherche les références et demande une confirmation explicite. Cliquez sur Forcer la suppression si vous souhaitez supprimer la ressource quel que soit l’état de la relation.

   >[!NOTE]
   >
   >La suppression d’une ressource référencée par d’autres ressources peut entraîner des problèmes fonctionnels.

   >[!NOTE]
   >
   >Si la ressource sélectionnée est un dossier et qu’elle contient une ressource de ce type dans sa hiérarchie, supprimez les autres ressources séparément ou supprimez le dossier entier.

## Impact de la suppression d’un formulaire XFA référencé {#impact-of-deleting-a-referenced-xfa-form}

Dans AEM Forms, un modèle de formulaire XFA peut être référencé par un formulaire adaptatif ou un autre modèle de formulaire XFA. Un modèle peut également faire référence à une ressource ou à un autre modèle XFA.

Il n’est pas conseillé de supprimer un formulaire XFA qui est référencé par un formulaire adaptatif, car il peut corrompre le formulaire adaptatif. Lorsqu’un formulaire adaptatif fait référence à un formulaire XFA, ses champs sont liés. Après la suppression de XFA, le formulaire adaptatif ne peut pas synchroniser ses champs avec les champs XFA et affiche un message d’erreur pour ces champs. Pour plus d’informations sur l’impact de la suppression d’un formulaire XFA référencé et sur les formulaires adaptatifs erronés, reportez-vous à la section [Mise à jour des formulaires XFA référencés](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Pour supprimer un tel formulaire XFA, mettez à jour le formulaire adaptatif et supprimez les liaisons avec les champs XFA.
