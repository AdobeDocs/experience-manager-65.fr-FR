---
title: Utilisation des jeux de formulaires dans l’espace de travail AEM Forms
seo-title: Working with Formsets in AEM Forms workspace
description: Un jeu de formulaires est un assortiment de formulaires HTML5 regroupés et présentés comme un ensemble unique de formulaires aux utilisateurs finaux. Découvrez comment utiliser des jeux de formulaires dans l’espace de travail AEM Forms.
seo-description: A formset is a collection of HTML5 forms grouped and presented as a single set of forms to end users. Learn how you can work with formsets in AEM Forms workspace.
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 100%

---

# Utilisation des jeux de formulaires dans l’espace de travail AEM Forms{#working-with-formsets-in-aem-forms-workspace}

Un jeu de formulaires est un assortiment de formulaires HTML5 regroupés et présentés comme un ensemble unique de formulaires aux utilisateurs finaux. Lorsque les utilisateurs finaux commencent à compléter un jeu de formulaires, ils passent facilement d’un formulaire à l’autre. Le jeu de formulaires peut ensuite être envoyé en un simple clic. Pour plus d’informations sur les jeux de formulaires et la manière de les configurer, consultez [Jeux de formulaires dans AEM Forms](../../forms/using/formset-in-aem-forms.md).

L’espace de travail AEM Forms prend en charge les jeux de formulaires. Avec les jeux de formulaires, plusieurs formulaires associés à un service ou processus peuvent être regroupés pour automatiser un processus d’entreprise et présentés aux utilisateurs finaux. Dans ce cas, les utilisateurs peuvent remplir le jeu entier comme un seul et il n’est pas nécessaire de classer, envoyer et suivre des processus ou des formulaires individuels.

## Comment joindre un jeu de formulaires au point de départ dans l’application d’espace de travail AEM Forms {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Créez un flux de processus d’entreprise dans Workbench. Pour plus d’informations, consultez l’[aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).
1. Dans les propriétés de processus du point de départ, sélectionnez **Utiliser une ressource CRX** dans Présentation et Données.

   ![1-3](assets/1-3.png)

1. Cliquez sur ![Parcourir](assets/browse.png) (Parcourir) à côté du chemin d’accès à la ressource CRX. La boîte de dialogue Sélection de l’actif de formulaire s’affiche.

   ![2-1](assets/2-1.png)

1. Cliquez sur l’onglet **Jeu de formulaires**, sélectionnez le jeu de formulaires approprié dans la liste, puis cliquez sur **OK**.

1. Déployez l’application après avoir mis à jour les autres propriétés pertinentes du processus.

## Utilisation des jeux de formulaires dans l’espace de travail AEM Forms {#using-formset-in-nbsp-aem-forms-workspace}

Une fois qu’un jeu de formulaires est attaché à un point de départ, ce dernier peut être appelé, comme n’importe quel autre, depuis l’espace de travail d’AEM Forms.

Les opérations prises en charge sur le jeu de formulaires via l’espace de travail AEM Forms sont les suivantes :

* Enregistrer en tant que brouillon
* Verrouiller
* Abandonner
* Envoyer
* Ajouter des pièces jointes
* Ajouter des remarques
* Se déplacer d’un formulaire à l’autre au sein d’un jeu de formulaires à l’aide des boutons Précédent et Suivant

![3-1](assets/3-1.png)

>[!NOTE]
>
>Pour améliorer les performances durant le déplacement d’un formulaire à l’autre d’un jeu de formulaires, tous les boutons de l’espace de travail (Précédent, Suivant, Envoyer, etc.) sont désactivés jusqu’à ce que le formulaire approprié soit complètement rendu.
