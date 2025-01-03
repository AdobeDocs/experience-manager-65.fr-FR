---
title: Paramétrer les options d’internationalisation
description: Découvrez comment spécifier les paramètres régionaux utilisés pour le rendu des formulaires et comment spécifier le jeu de caractères utilisé pour encoder le flux de sortie.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 100%

---

# Paramétrer les options d’internationalisation{#setting-internationalization-options}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

## Indication des paramètres régionaux utilisés pour effectuer le rendu du formulaire {#specify-the-locale-used-to-render-forms}

Vous pouvez spécifier les paramètres régionaux utilisés lors du rendu d’un formulaire PDF. Les champs d’un formulaire PDF utilisent les paramètres régionaux spécifiés pour afficher les données. Par exemple, si le paramètre régional est défini sur Allemand, le formulaire utilise des séparateurs décimaux allemands pour les valeurs numériques. Les paramètres régionaux sont également utilisés pour envoyer des messages de validation aux appareils clients, tels que les navigateurs web, dans le cadre de transformations HTML.

1. Dans la console d’administration, cliquez sur Services > Formulaires.
1. Dans la liste de langues, dans l’onglet Internationalisation, sélectionnez les paramètres régionaux utilisés pour effectuer le rendu d’un formulaire. La valeur par défaut Anglais (États-Unis).
1. Cliquez sur Enregistrer.

## Définition du jeu de caractères utilisé pour encoder le flux de sortie {#specify-the-character-set-used-to-encode-the-output-stream}

1. Sous Internationalisation, dans la liste Jeu de caractères, sélectionnez un jeu de caractères. Ce paramètre dépend de l’API utilisée, à savoir renderHTMLForm ou renderPDFForm. Pour spécifier un jeu de caractères ne figurant pas dans la liste, sélectionnez Personnalisé et spécifiez la valeur d’encodage dans la zone qui s’affiche.

   Pour les transformations HTML, AEM forms prend en charge les valeurs d’encodage de caractères définies par le package `java.nio.charset` Si le paramètre sFormPreference prend la valeur PDFForm, seuls des jeux de caractères spécifiques sont pris en charge. Le jeu de caractères doit être un nom canonique valide. La valeur par défaut est ISO-8859-1.

1. Cliquez sur Enregistrer.
