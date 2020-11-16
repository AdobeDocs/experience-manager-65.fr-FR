---
title: 'Configuration de votre environnement de compte  '
seo-title: 'Configuration de votre environnement de compte  '
description: AEM vous dote des outils nécessaires pour configurer votre compte ainsi que certains aspects de l’environnement de création
seo-description: AEM vous dote des outils nécessaires pour configurer votre compte ainsi que certains aspects de l’environnement de création
uuid: ef31be29-5c18-4dc9-ad51-fb001588b31e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b610e19c-f8d9-4ae2-b056-9fd5cf541261
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 99%

---


# Configuration de votre environnement de compte  {#configuring-your-account-environment}

AEM vous dote des outils nécessaires pour configurer votre compte ainsi que certains aspects de l’environnement de création.

Grâce à l’option [Utilisateur](/help/sites-authoring/user-properties.md#user-settings) dans l’[en-tête](/help/sites-authoring/basic-handling.md#the-header) et à la boîte de dialogue associée [Mes préférences](#userpreferences), vous pouvez modifier vos options utilisateur.

Accédez tout d’abord à l’option [Utilisateur](/help/sites-authoring/user-properties.md#user-settings) dans l’en-tête.

## Paramètres utilisateur {#user-settings}

La boîte de dialogue **Paramètres utilisateur** donne accès aux options suivantes :

* Se faire passer pour

   * La fonction [Se faire passer pour](/help/sites-administering/security.md#impersonating-another-user) permet à un utilisateur de travailler au nom d’un autre.

* Profil

   * Offre un lien pratique vers vos [paramètres utilisateur](/help/sites-administering/security.md).

* [Mes préférences](/help/sites-authoring/user-properties.md#my-preferences)

   * Spécifiez les différents paramètres uniques à votre utilisateur.

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### Mes préférences {#my-preferences}

La boîte de dialogue **Mes préférences** est accessible par l’intermédiaire de l’option [Utilisateur](/help/sites-authoring/user-properties.md#user-settings) dans l’en-tête.

Chaque utilisateur peut définir certaines propriétés pour lui-même.

![capture d&#39;écran_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **Langue**

   Définit la langue à utiliser dans l’IU de l’environnement de création. Sélectionnez la langue de votre choix dans la liste des langues disponibles.

   Cette configuration est également utilisée dans l’IU classique.

* **Gestion des fenêtres**

   Définit le comportement ou l’ouverture des fenêtres. Vous avez le choix entre :

   * **Fenêtres multiples** (par défaut)

      * Les pages s’ouvrent dans une nouvelle fenêtre.
   * **Une seule fenêtre**

      * Les pages s’ouvrent dans la fenêtre actuelle.


* **Afficher les actions de bureau pour Assets**

   Cette option nécessite l’utilisation de l’application de bureau AEM.

* **Couleur de l’annotation**

   Cette opération définit la couleur par défaut utilisée pour les annotations.

   * Cliquez sur le bloc de couleurs pour ouvrir le sélecteur d’échantillon afin de choisir une couleur.
   * Vous pouvez également saisir le code hexadécimal de la couleur désirée dans le champ. 

* **Présentation de la date relative**

   Pour améliorer la lisibilité, AEM effectue le rendu des dates parmi les sept derniers jours comme des dates relatives (par exemple, il y a trois jours) et des dates antérieures comme des dates précises (par exemple, le 20 mars 2017).

   Cette option définit la manière dont les dates sont affichées dans le système. Les options suivantes sont disponibles :

   * **Toujours afficher la date exacte** : la date exacte est toujours affichée (ce n’est jamais une date relative).
   * **1 jour** : la date relative s’affiche pour les dates correspondant au jour même ; dans le cas contraire, une date exacte est affichée.

   * **7 jours (par défaut)** : la date relative s’affiche pour les dates parmi les sept derniers jours ; dans le cas contraire, une date exacte est affichée.

   * **1 mois** : la date relative s’affiche pour les dates correspondant au dernier mois ; dans le cas contraire, une date exacte est affichée.

   * **1 an** : la date relative s’affiche pour les dates correspondant à la dernière année ; dans le cas contraire, une date exacte est affichée.

   * **Toujours afficher la date relative** : les dates exactes ne sont jamais affichées, seules les dates relatives le sont.

* **Activer les raccourcis**

   AEM prend en charge un certain nombre de raccourcis clavier qui rendent la création plus efficace.

   * [Raccourcis clavier lors de la modification de pages](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [Raccourcis clavier pour les consoles](/help/sites-authoring/keyboard-shortcuts.md)

   Cette option active les raccourcis clavier. Ils sont activés par défaut, mais il est possible de les désactiver, par exemple si un utilisateur a certaines exigences d’accessibilité.

* **Utilisez une expérience de création de contenu classique**

   Cette option permet la création de pages basée sur l’[IU classique](/help/sites-classic-ui-authoring/home.md). Par défaut, l’IU standard est utilisée.

* **Activer la page d’accueil des ressources**

   Cette option est disponible uniquement si l’administrateur système a activé l’environnement Page d’accueil des ressources pour l’ensemble de l’entreprise.

* **Configuration Stock**

   Cette option permet de définir la configuration Adobe Stock préférée. Elle n’est disponible que si l’administrateur système a activé l’[intégration d’Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
