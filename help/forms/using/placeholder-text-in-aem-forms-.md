---
title: Texte d’espace réservé dans AEM Forms
seo-title: Placeholder text in AEM Forms
description: Le texte d’espace réservé est destiné à aider l’utilisateur à saisir des données lorsque la valeur de la commande est vide. Il peut s’agir d’un exemple de valeur ou une brève description du format attendu.
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '215'
ht-degree: 100%

---

# Texte d’espace réservé dans AEM Forms {#placeholder-text-in-aem-forms}

Le texte d’espace réservé représente un mot ou un groupe de mots court. Il est destiné à aider l’utilisateur à saisir des données lorsque la valeur de la commande est vide. Un texte d’espace réservé peut être un exemple de valeur ou une brève description du format attendu. Le texte d’espace réservé s’affiche avant que l’utilisateur ne saisisse une valeur et il est supprimé lorsque l’utilisateur saisit ou sélectionne une valeur.

>[!NOTE]
>
>Le texte d’espace réservé doit avoir, le cas échéant, une valeur qui ne contient aucun caractère de nouvelle ligne.

![Un composant de date avec et sans le texte d’espace réservé](assets/dat-picker-place-holder-text.png)

**A.** Composant de date avec le texte d’espace réservé **B.** Composant de date sans le texte d’espace réservé

AEM Forms prend en charge le texte d’espace réservé pour la zone Mot de passe, le sélecteur de date, la zone numérique et les champs de zone de texte.\
Les textes d’espace réservé ne sont pas pris en charge pour le widget natif de date en HTML5. Pour spécifier un texte d’espace réservé :

1. Effectuez un clic droit sur un composant prenant en charge le texte d’espace réservé et cliquez sur **Modifier**. La boîte de dialogue Modifier le composant apparaît.

1. Ouvrez l’onglet **Titre et texte.**
1. Indiquez un mot ou un groupe de mots court dans **la zone d’espace réservé**. Cliquez sur **OK**.

>[!NOTE]
>
>Le texte d’espace réservé n’est pas pris en charge sous Microsoft Internet Explorer 9.
