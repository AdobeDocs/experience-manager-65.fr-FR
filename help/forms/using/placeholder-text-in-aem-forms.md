---
title: Texte d’espace réservé dans AEM Forms
description: Le texte d’espace réservé est destiné à aider l’utilisateur à saisir des données lorsque la commande n’a pas de valeur. Il peut s’agir d’un exemple de valeur ou d’une brève description du format attendu.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: 6dbec0f41396c2b41d5324c4ecf6f1f33b1d0780
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 67%

---

# Texte d’espace réservé dans AEM Forms {#placeholder-text-in-aem-forms}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

Le texte d’espace réservé représente un mot ou une expression courte. L’objectif est d’aider l’utilisateur à saisir des données lorsque le contrôle n’a pas de valeur. Un texte d’espace réservé peut être un exemple de valeur ou une brève description du format attendu. Le texte d’espace réservé s’affiche avant que l’utilisateur ne saisisse une valeur et il est supprimé lorsque l’utilisateur saisit ou sélectionne une valeur.

>[!NOTE]
>
>Le texte d’espace réservé doit avoir, le cas échéant, une valeur qui ne contient aucun caractère de nouvelle ligne.

![Un composant de date avec et sans le texte d’espace réservé](assets/dat-picker-place-holder-text.png)

**A.** Composant de date avec le texte d’espace réservé **B.** Composant de date sans le texte d’espace réservé

AEM Forms prend en charge le texte d’espace réservé pour la zone Mot de passe, le sélecteur de date, la zone numérique et les champs de zone de texte.\
Les textes d’espace réservé ne sont pas pris en charge pour le widget natif de date en HTML5. Pour spécifier un texte d’espace réservé :

1. Cliquez avec le bouton droit sur un composant qui prend en charge le texte d’espace réservé, puis cliquez sur **Modifier**. La boîte de dialogue Modifier le composant apparaît.

1. Ouvrez l’onglet **Titre et texte.**
1. Indiquez un mot ou un groupe de mots court dans **la zone d’espace réservé**. Cliquez sur **OK**.

>[!NOTE]
>
>Le texte d’espace réservé n’est pas pris en charge sous Microsoft Internet Explorer 9.
