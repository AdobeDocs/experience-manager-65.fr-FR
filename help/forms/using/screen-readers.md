---
title: Lecteurs d’écran pour les formulaires HTML5
description: Répertorie les lecteurs d’écran pris en charge avec les formulaires HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 100%

---

# Lecteurs d’écran pour les formulaires HTML5 {#screen-readers-for-html-forms}

Les composants de formulaires HTML5 rendent des modèles de formulaires XFA au format HTML5. Tous les navigateurs standard prenant en charge HTML5 peuvent générer ces formulaires. Pour prendre en charge une expérience de capture de données similaire dans les formulaires PDF et HTML5, la mise en page des formulaires PDF est conservée dans les formulaires HTML5.

Les formulaires HTML5 utilisent des constructions HTML standard, ce qui permet d’utiliser les outils d’accessibilité usuels du format HTML avec ces formulaires. Si un formulaire est conçu selon les bonnes pratiques relatives aux formulaires accessibles, il fonctionne avec n’importe quel lecteur d’écran pris en charge. En outre, ces formulaires sont activés pour la navigation au clavier.

## Normes d’accessibilité {#accessibility-standards}

Les formulaires HTML5 sont conformes à la section 508 concernant l’accessibilité avec des exceptions connues. Voir [VPAT pour les formulaires HTML5](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) pour plus d’informations.

## Lecteurs d’écran certifiés pour les formulaires HTML5 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 sur Microsoft® Windows
* VoiceOver sur macOS X et iPad

### JAWS {#jaws}

Toutes les combinaisons de touches et tous les raccourcis par défaut fonctionnent pour les formulaires HTML5. Pour plus d’informations sur l’utilisation de JAWS, consultez le site [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### Voix off {#voiceover}

HTML5 prend en charge toutes les combinaisons de touches et tous les mouvements par défaut de la voix off. Pour plus d’informations sur la configuration et l’utilisation de VoiceOver, consultez le site [https://www.apple.com/fr/accessibility/vision/](https://www.apple.com/fr/accessibility/vision/).

## Problèmes connus {#known-issues}

* **(Internet Explorer 9 uniquement)** : dans les formulaires HTML5, les pages sont chargées à la demande (dynamiquement). Le chargement des pages à la demande provoque des problèmes dans le fonctionnement des lecteurs d’écran. Lorsque le focus du lecteur d’écran se trouve sur le dernier champ de la page et que l’utilisateur appuie sur la touche de tabulation, le lecteur d’écran retourne au premier champ de la première page du formulaire.
* **(Internet Explorer 9 uniquement)** La commande Sélecteur de date dans les formulaires HTML5 n’est pas totalement accessible avec le clavier. Dans le contrôle du Sélecteur de date, si vous appuyez sur les touches Haut/Bas plusieurs fois, le contrôle Sélecteur de date se ferme et le point de focalisation passe au prochain/dernier champ.

* VoiceOver ne peut pas détecter les touches de flèches sur le widget de date sur Safari iPad.
