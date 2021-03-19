---
title: 'Texte d’espace réservé dans AEM Forms '
seo-title: 'Texte d’espace réservé dans AEM Forms '
description: Le texte d’espace réservé est destiné à aider l’utilisateur à saisir des données lorsque la valeur de la commande est vide. Il peut s’agir d’un exemple de valeur ou une brève description du format attendu.
seo-description: Le texte d’espace réservé est destiné à aider l’utilisateur à saisir des données lorsque la valeur de la commande est vide. Il peut s’agir d’un exemple de valeur ou une brève description du format attendu.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Formulaires adaptatifs
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 95%

---


# Texte d’espace réservé dans AEM Forms {#placeholder-text-in-aem-forms}

Le texte d’espace réservé représente un mot ou un groupe de mots court. Il est destiné à aider l’utilisateur à saisir des données lorsque la valeur de la commande est vide. Un texte d’espace réservé peut être un exemple de valeur ou une brève description du format attendu. Le texte d’espace réservé s’affiche avant que l’utilisateur ne saisisse une valeur et il est supprimé lorsque l’utilisateur saisit ou sélectionne une valeur.

>[!NOTE]
>
>Le texte d’espace réservé doit avoir, le cas échéant, une valeur qui ne contient aucun caractère de nouvelle ligne.

![Un composant de date avec et sans le texte d’espace réservé](assets/dat-picker-place-holder-text.png)

**Composant A.** Date avec le texte d’espace réservé  **B.** Date sans texte d’espace réservé

AEM Forms prend en charge le texte d’espace réservé pour la zone Mot de passe, le sélecteur de date, la zone numérique et les champs de zone de texte.\
Les textes d’espace réservé ne sont pas pris en charge pour le widget natif de date en HTML5. Pour spécifier un texte d’espace réservé :

1. Effectuez un clic droit sur un composant prenant en charge le texte d’espace réservé et cliquez sur **Modifier**. La boîte de dialogue Modifier le composant apparaît.

1. Ouvrez l&#39;onglet **Titre et texte.**
1. Indiquez un mot ou un groupe de mots court dans **la zone d’espace réservé**. Cliquez sur **OK**.

>[!NOTE]
>
>Le texte d’espace réservé n’est pas pris en charge sous Microsoft Internet Explorer 9.

