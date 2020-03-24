---
title: Nouveautés d’Adobe Experience Manager 6.5 Service Pack 4
description: Nouveautés d’Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 5eff26237415160e80e622eacabf5c40dfad00af

---


# Nouveautés d’Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (AEM) 6.5 offre des fonctionnalités et des améliorations continues au moyen de Service Packs trimestriels. L&#39;approche vous est bénéfique, car les innovations deviennent plus faciles à adopter.

AEM Service Pack 4 (6.5.4.0) est sorti le 5 **mars 2020**. Cet article met en évidence les fonctionnalités clés que les Service Packs 6.5  le  pour rendre votre voyage AEM plus enrichissant.

## AEM Sites {#aem-sites}

### Améliorations du système de style

Vous pouvez désormais sélectionner des styles dans la boîte de dialogue du composant à l’aide du système de style amélioré.

### Amélioration des performances dans divers domaines {#performance-improvements}

* Réduction du temps de chargement et d’initialisation de ContextHub dans un site (`contexthub.kernel.js`). Le chargement des pages s’en trouve accéléré lors d’une visite sur le site.

* Réduction du temps d’actualisation d’une page après avoir fait glisser des fragments d’expérience vers l’éditeur de page Sites.

* Réduction du temps de chargement des entrées sur une page Sites avec plus de 200 copies dynamiques dans l’aperçu **[!UICONTROL de la]** Live Copy.

* Amélioration de la gestion des URL incomplètes ou incorrectes. De telles URL peuvent ralentir l’éditeur de modèles.

## AEM Assets {#aem-assets}

### Configuration d’AEM Assets avec Brand Portal {#configure-assets-bp}

Le d’autorisations  entre les ressources AEM et le portail de marque est modifié. Auparavant, Brand Portal était configuré dans l’interface utilisateur classique via la passerelle OAuth héritée, qui fait appel à l’échange de jetons JWT pour obtenir un jeton d’accès IMS en vue de l’autorisation. AEM Assets est désormais configuré avec Brand Portal via Adobe I/O, qui fournit un jeton IMS pour autoriser votre client Brand Portal.

Les étapes de configuration des ressources AEM avec le portail de marque sont différentes selon votre version AEM et selon que vous effectuez une configuration pour la première fois ou une mise à niveau des configurations existantes. See [Configure AEM Assets with Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) for details.


### Accessibility enhancements {#accessibility-enhancements}

Les ressources Experience Manager comprennent les améliorations d’accessibilité suivantes :

* Vous pouvez utiliser les touches fléchées du clavier pour déplacer et déplacer des zones dans des images agrandies. Pour plus d’informations, reportez-vous à la section [de fichiers à l’aide de touches du clavier uniquement](../assets/managing-assets-touch-ui.md#previewing-assets).

* Les cases à cocher à états mixtes (dans lesquelles, sauf si vous sélectionnez tous les prédicats imbriqués, les cases de premier niveau ne sont pas sélectionnées et sont enfoncées) dans le panneau  du sont lisibles par les lecteurs d’écran.

* Les contraintes de format de date et d’heure sont fournies dans les libellés de champ des champs de date, afin de permettre aux utilisateurs de saisir la date dans le format correct à l’aide du clavier.

   Par exemple, `On Time (MM-DD-YYYY HH:mm)`. Ici MM est le mois dans un format à deux chiffres, AAAA est l&#39;année, JJ est le jour dans un format à deux chiffres, HH est l&#39;heure dans un format militaire à 24 heures et mm est la minute.

* Le `X` symbole du bouton permettant de supprimer les balises actuellement sélectionnées est désormais annoncé par les lecteurs d’écran, ainsi que le nombre de balises sélectionnées.

## AEM Forms {#aem-forms}

### Générer une sortie imprimable dans le AEM Forms {#generate-printable-output}

L’étape de flux de travail Générer une sortie imprimable vous permet d’intégrer un fichier de modèle source à un fichier de données. Cette intégration vous permet d’imprimer ou d’enregistrer différentes copies du fichier de modèle. L’étape génère une sortie PCL, PostScript, ZPL, IPL, TPCL ou DPL. Pour plus d’informations sur cette fonctionnalité, voir Flux de travaux centrés sur [Forms sur OSGi - Guide de référence](../forms/using/aem-forms-workflow-step-reference.md)des étapes.

![Générer une sortie imprimable](assets/generate-print-output-demo.gif)

### Prise en charge de plusieurs colonnes pour les formulaires adaptatifs et les communications interactives en mode Disposition {#multi-column-adaptive-forms}

Vous pouvez désormais définir le nombre de colonnes d’un panneau dans les formulaires adaptatifs et les communications interactives. Passez en mode de mise en page pour utiliser la nouvelle option multicolonne. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner des composants](../forms/using/resize-using-layout-mode.md).

![Mise en page multi-colonnes](assets/multi-column-layout.gif)

### Personnalisations de la boîte de réception AEM {#aem-inbox}

La nouvelle option Contrôle d’administration permet aux administrateurs d’effectuer les opérations suivantes :

* Personnaliser le texte et le logo de l’en-tête

* Contrôle de l’affichage des liens de navigation disponibles dans l’en-tête

L’option Contrôle d’administration n’est visible que pour les membres du groupe des administrateurs ou des administrateurs de processus. Pour plus d’informations sur cette fonctionnalité, voir [Votre boîte de réception](../sites-authoring/inbox.md).

### Prise en charge du texte enrichi dans les formulaires HTML5 {#rich-text-support}

Convertissez un champ de texte d’un formulaire XFA en champ de texte enrichi dans un formulaire HTML5. Pour plus d’informations, voir [Conception de modèles de formulaire pour les formulaires](../forms/using/designing-form-template.md)HTML5.

### Accessibility enhancements {#forms-accessibility-enhancements-6540}

Experience Manager Forms comprend les améliorations d’accessibilité suivantes :

* Les utilisateurs peuvent déplacer la mise au point des onglets sans problème pour le thème de référence Ultramarine-Accessible d’un formulaire adaptatif.

* Les lecteurs d’écran annoncent correctement les cases à cocher, les liens, le sélecteur de date et les champs de saisie de date dans un formulaire adaptatif.

* Chaque page d’un formulaire adaptatif comprend désormais un titre et un libellé de repère principal.

## Principales fonctionnalités des Service Packs version 6.5 d’AEM

### Smart Imaging for Dynamic Media (6.5.3.0) {#smart-imaging}

L’imagerie intelligente utilise les caractéristiques d’affichage uniques de chaque utilisateur pour fournir automatiquement les images adaptées optimisées pour leur expérience, ce qui améliore les performances et l’engagement. L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir [Smart Imaging](../assets/imaging-faq.md).

### Recherche visuelle pour AEM Assets (6.5.2.0) {#visual-search}

Les utilisateurs de ressources peuvent rechercher des images visuellement similaires. AEM affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. See [Visual search](../assets/search-assets.md).

### Partage et demande d’accès aux éléments de boîte de réception d’un utilisateur AEM Forms (6.5.3.0) {#share-request-access}

Vous pouvez partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu’un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander à d’autres utilisateurs l’accès aux éléments de la boîte de réception. Voir [Partage et demande d’accès aux éléments de boîte de réception d’un utilisateur](../forms/using/configure-shared-queues-osgi.md).

### Configuration des paramètres d’absence du bureau pour les éléments de boîte de réception d’un utilisateur AEM Forms (6.5.3.0) {#configure-out-of-office}

Si vous prévoyez d’être absent du bureau, vous pouvez indiquer ce qui se passe pour les éléments qui vous sont affectés pour cette période.
Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Vous pouvez définir une personne par défaut à laquelle tous vos éléments sont envoyés. Voir [Configuration des paramètres](../forms/using/configure-out-of-office-settings.md)d’absence du bureau.

### Générer plusieurs communications interactives à l’aide de l’API lot pour AEM Forms (6.5.3.0) {#generate-multiple-ic}

Vous pouvez utiliser l’API de traitement par lots pour produire plusieurs communications interactives à partir d’un modèle. Le modèle est une communication interactive sans données. L’API de traitement par lots combine les données avec un modèle pour produire une communication interactive. L’API est utile pour la production de masse de communications interactives. Par exemple, factures de téléphone, relevés de carte de crédit pour plusieurs clients. Voir [Générer plusieurs communications interactives à l’aide de l’API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)par lot.

## Principales versions depuis AEM 6.5 SP3

Entre le 12 décembre 2019 et le 5 mars 2020, Adobe a publié les fonctionnalités suivantes, qui ne font pas partie du livrable principal d’AEM :

* AEM Cloud Manager 2020.1.0 et 2020.2.0

   Améliorer l&#39;état du pipeline et la capacité de télécharger les journaux pour différentes étapes. Voir :

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)


* Mises à jour de l’interface de ligne de commande d’AEM Cloud Manager

   Automatisez le Cloud Manager à l’aide de l’outil de ligne de commande. Voir [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* Sites AEM : Archétype de projet 23

   La meilleure façon de  un nouveau projet AEM. Archetype 23 fusionne le [Project Archetype for SPA et les sites réguliers en un seul](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) et fournit un thème par défaut pour  votre développement frontal.

* Sites AEM : Site de référence WKND

   [Nouveau projet](https://www.wknd.site/) de référence contenant les meilleures pratiques relatives à la création de sites avec AEM. Pour en savoir plus, lisez le didacticiel [mis à jour de](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)WKND. Vous pouvez prendre le code le plus récent de [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* Sites AEM : Commerce CIF Core Components 0.7.0 et 0.9.0

   Intégrer les sites AEM au commerce Magento. Voir [Extension des composants principaux dédiés et Archétype de projet avec une attention particulière sur le commerce](https://github.com/adobe/aem-core-cif-components/releases).

* Ressources AEM : Application de bureau 2.0.1.1

   Voir [Obtention d’un accès de bureau aux ressources](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html).

* AEM Screens : Feature Pack 202001

   Digital Signage directement depuis AEM. Installez les améliorations avec le dernier Feature Pack pour [activer la lecture synchrone sur plusieurs lecteurs](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)de médias.

## Ressources utiles

* [Guides de l’utilisateur d’AEM 6.5](../user-guide/home.md)

* [Notes de mise à jour générales d’Adobe Experience Manager 6.5](release-notes.md)

* [Notes de mise à jour du Service Pack pour Adobe Experience Manager 6.5](sp-release-notes.md)
