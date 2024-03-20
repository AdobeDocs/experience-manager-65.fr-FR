---
title: Paramétrer les options d’internationalisation
description: Découvrez comment spécifier les paramètres régionaux utilisés pour le rendu des formulaires et comment spécifier le jeu de caractères utilisé pour encoder le flux de sortie.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 32%

---

# Paramétrer les options d’internationalisation{#setting-internationalization-options}

## Spécification des paramètres régionaux utilisés pour le rendu des formulaires {#specify-the-locale-used-to-render-forms}

Vous pouvez spécifier les paramètres régionaux utilisés lors du rendu d’un formulaire de PDF. Les champs d’un formulaire de PDF utilisent les paramètres régionaux spécifiés pour afficher les données. Par exemple, si le paramètre régional est défini sur Allemand, le formulaire utilise des séparateurs décimaux allemands pour les valeurs numériques. Les paramètres régionaux sont également utilisés pour envoyer des messages de validation aux appareils clients, tels que les navigateurs web, dans le cadre de transformations de HTML.

1. Dans la console d’administration, cliquez sur Services > Forms.
1. Sous Internationalisation, dans la liste Langue, sélectionnez le paramètre régional utilisé pour générer un formulaire. La valeur par défaut est English (United States).
1. Cliquez sur Enregistrer.

## Définition du jeu de caractères utilisé pour encoder le flux de sortie {#specify-the-character-set-used-to-encode-the-output-stream}

1. Sous Internationalisation, dans la liste Jeu de caractères, sélectionnez un jeu de caractères. Ce paramètre dépend de l’API utilisée, renderHTMLForm ou renderPDFForm. Pour spécifier un jeu de caractères ne figurant pas dans la liste, sélectionnez Personnalisé et spécifiez la valeur d’encodage dans la zone qui s’affiche.

   Pour les transformations HTML, AEM forms prend en charge les valeurs d’encodage de caractères définies par le package `java.nio.charset` Si le paramètre sFormPreference prend la valeur PDFForm, seuls des jeux de caractères spécifiques sont pris en charge. Le jeu de caractères doit être un nom canonique valide. La valeur par défaut est ISO-8859-1.

1. Cliquez sur Enregistrer.
