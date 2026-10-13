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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 100%
---
# Paramétrer les options d’internationalisation{#setting-internationalization-options}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

## Spécifier les paramètres régionaux utilisés pour le rendu des formulaires {#specify-the-locale-used-to-render-forms}

Vous pouvez spécifier les paramètres régionaux utilisés lors du rendu d’un formulaire PDF. Les champs d’un formulaire PDF utilisent les paramètres régionaux spécifiés pour afficher les données. Par exemple, si les paramètres régionaux sont définis sur Allemand, le formulaire utilise des séparateurs décimaux allemands pour les valeurs numériques. Les paramètres régionaux sont également utilisés pour envoyer des messages de validation aux appareils clients, tels que les navigateurs web, dans le cadre de transformations HTML.

1. Dans la console d’administration, cliquez sur Services > Formulaires.
1. Dans la liste de langues, dans l’onglet Internationalisation, sélectionnez les paramètres régionaux utilisés pour effectuer le rendu d’un formulaire. La valeur par défaut est Anglais (États-Unis).
1. Cliquez sur Enregistrer.

## Définition du jeu de caractères utilisé pour encoder le flux de sortie {#specify-the-character-set-used-to-encode-the-output-stream}

1. Sous Internationalisation, dans la liste Jeu de caractères, sélectionnez un jeu de caractères. Ce paramètre dépend de l’API utilisée, à savoir renderHTMLForm ou renderPDFForm. Pour spécifier un jeu de caractères ne figurant pas dans la liste, sélectionnez Personnalisé et spécifiez la valeur d’encodage dans la zone qui s’affiche.

   Pour les transformations HTML, AEM forms prend en charge les valeurs d’encodage de caractères définies par le package `java.nio.charset` Si le paramètre sFormPreference prend la valeur PDFForm, seuls des jeux de caractères spécifiques sont pris en charge. Le jeu de caractères doit être un nom canonique valide. La valeur par défaut est ISO-8859-1.

1. Cliquez sur Enregistrer.
