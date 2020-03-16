---
title: Nouveautés d’Adobe Experience Manager 6.5 Service Pack 4
description: Nouveautés d’Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ed756d785864131c2e031aec4331388bc057576b

---


# Nouveautés d’Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (AEM) 6.5 offre des fonctionnalités et des améliorations continues grâce aux Service Packs trimestriels de cette année. La nouvelle approche profite à nos clients lorsqu&#39;ils adoptent les innovations plus rapidement.

La dernière version d’AEM Service Pack 4 (6.5.4.0) est publiée le 5 **mars 2020**. Cet article met en évidence les fonctionnalités que le dernier Service Pack  le  pour rendre votre voyage AEM plus enrichissant.

## AEM Sites {#aem-sites}

### Amélioration des performances dans divers domaines {#performance-improvements}

* Réduction du temps de chargement et d’initialisation de ContextHub dans un site (contexthub.kernel.js). Le chargement des pages s’en trouve accéléré lors d’une visite sur le site.

* Réduction du temps d’actualisation d’une page après avoir fait glisser et déposé des fragments d’expérience dans l’éditeur de page Sites.

* Réduction du temps de chargement des entrées pour une page Sites avec plus de 200 copies dynamiques dans l’aperçu de la Live Copy.

* Amélioration de la gestion des URL incomplètes ou incorrectes. De telles URL peuvent ralentir l’éditeur de modèles.

En outre, AEM 6.5.4.0 inclut des améliorations du système de style. Vous pouvez désormais sélectionner des styles dans la boîte de dialogue du composant.

## AEM Assets {#aem-assets}

### Intégration de Brand Portal via Adobe I/O Console {#assets-integration-bp}

Vous pouvez désormais configurer AEM Assets avec Brand Portal via la console d’E/S Adobe. La console d’E/S Adobe fournit un jeton IMS pour l’autorisation du locataire du portail de marque. Auparavant, les ressources AEM étaient configurées avec le portail de marque dans l’interface utilisateur classique via la passerelle OAuth héritée. Les configurations utilisant la passerelle OAuth héritée seront prises en charge jusqu’au 6 avril 2020. Si vous ne modifiez pas l’intégration, les configurations existantes continueront à fonctionner.

Vous pouvez créer une nouvelle intégration ou mettre à niveau vos paramètres d’intégration vers la console d’E/S Adobe.

### Accessibility enhancements {#accessibility-enhancements}

Les ressources Experience Manager comprennent les améliorations d’accessibilité suivantes :

* Vous pouvez utiliser les touches fléchées du clavier pour déplacer et déplacer des zones dans des images agrandies. Pour plus d’informations, reportez-vous à la section [de fichiers à l’aide de touches du clavier uniquement](../assets/managing-assets-touch-ui.md#previewing-assets).

* Les cases à cocher à états mixtes (dans lesquelles, sauf si vous sélectionnez tous les prédicats imbriqués, les cases de premier niveau ne sont pas sélectionnées et sont enfoncées) dans le panneau  du sont lisibles par les lecteurs d’écran.

* Les contraintes de format de date et d’heure sont fournies dans les libellés de champ des champs de date, afin de permettre aux utilisateurs de saisir la date dans le format correct à l’aide du clavier.

   Par exemple, `On Time (MM-DD-YYYY HH:mm)`. Ici MM est le mois dans un format à deux chiffres, AAAA est l&#39;année, JJ est le jour dans un format à deux chiffres, HH est l&#39;heure dans un format militaire à 24 heures et mm est la minute.

* Le `X` symbole du bouton permettant de supprimer les balises actuellement sélectionnées est désormais annoncé par les lecteurs d’écran, ainsi que le nombre de balises sélectionnées.

## AEM Forms {#aem-forms}

### Générer une sortie imprimable dans le AEM Forms {#generate-printable-output}

Si vous souhaitez qu’une solution imprime ou enregistre plusieurs copies d’un fichier de modèle source et l’intègre à un fichier de données avec de nombreux enregistrements, une nouvelle étape de processus Générer une sortie imprimable est disponible dans AEM Forms. Par exemple, si vous souhaitez imprimer un formulaire source avec un nom différent chaque fois qu’il est imprimé, vous pouvez avoir ces noms dans le fichier de données et les intégrer à un fichier de modèle standard.

Tirez parti de cette fonctionnalité en utilisant **Outils** > **[!UICONTROL Processus]** > **[!UICONTROL Modèles]** > **[!UICONTROL Créer, puis recherchez l’étape Générer une sortie imprimable.]******

![Générer une sortie imprimable](assets/generate-print-output-demo.gif)

Pour plus d’informations sur cette fonctionnalité, voir Flux de travaux centrés sur [Forms sur OSGi - Guide de référence](../forms/using/aem-forms-workflow-step-reference.md)des étapes.

### Prise en charge de plusieurs colonnes pour les formulaires adaptatifs et les communications interactives en mode Disposition {#multi-column-adaptive-forms}

Vous pouvez désormais définir le nombre de colonnes d’un panneau dans les formulaires adaptatifs et les communications interactives.

Vous pouvez trouver la nouvelle option en passant en mode Mise en page. Appuyez sur le panneau que vous souhaitez convertir en format à plusieurs colonnes, sélectionnez son parent et appuyez sur l’icône à plusieurs colonnes pour définir le nombre de colonnes du panneau.

![Mise en page multi-colonnes](assets/multi-column-layout.gif)

Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner des composants](../forms/using/resize-using-layout-mode.md).

### Personnalisations de la boîte de réception AEM {#aem-inbox}

Avez-vous déjà ressenti le besoin de personnaliser les options disponibles dans l’en-tête AEM ? Il est maintenant possible avec notre nouvelle version du Service Pack avec l&#39;introduction d&#39;une option **[!UICONTROL de contrôle]** d&#39;administration.

**Personnaliser le texte d’en-tête**

Les administrateurs de processus peuvent désormais spécifier le texte d’en-tête de votre choix.

Vous trouverez la nouvelle option **[!UICONTROL Personnaliser le texte]** d’en-tête sous le sélecteur de  de (disponible en haut à droite de la barre d’outils) > Contrôle **** d’administration.

**Personnaliser le logo**

Comme pour la personnalisation du texte d’en-tête, les administrateurs de processus peuvent désormais spécifier le logo de l’en-tête de votre choix.

Vous trouverez la nouvelle option **[!UICONTROL Personnaliser le logo]** sous  de > Contrôle **[!UICONTROL d’administration]**.

Pour plus d’informations sur cette fonctionnalité, voir [Votre boîte de réception](../sites-authoring/inbox.md).

### Contrôle de navigation utilisateur {#user-navigation-control}

Les administrateurs de flux de travail ont désormais la possibilité de faire travailler les utilisateurs sur AEM en mode restreint en fonction de leur rôle. Les administrateurs peuvent contrôler l’affichage des options de navigation disponibles dans l’en-tête afin de limiter les utilisateurs à passer en mode de création de flux de travail ou à d’autres liens de solution.

Consultez les nouvelles options **[!UICONTROL de navigation]** Masquer sous  de > Contrôle **[!UICONTROL d’administration]**.

Pour plus d’informations sur cette fonctionnalité, voir [Votre boîte de réception](../sites-authoring/inbox.md).

### Prise en charge du texte enrichi dans les formulaires HTML5 {#rich-text-support}

Le champ de texte peut désormais afficher un d’options de formatage dans le formulaire HTML5 rendu. Vous devez définir le format du champ de texte dans Forms Designer pour appliquer les paramètres appropriés au champ.

Pour utiliser cette fonctionnalité, appuyez sur le champ de texte dans le de **[!UICONTROL conception]** dans Forms Designer. Dans l’onglet **[!UICONTROL Champ]** , sélectionnez Texte **** enrichi dans le déroulant Format **[!UICONTROL de]** champ pour appliquer les paramètres.

Pour plus d’informations, voir [Conception de modèles de formulaire pour les formulaires](../forms/using/designing-form-template.md)HTML5.

## Principaux points saillants

Outre les nouvelles fonctionnalités, AEM 6.5 Service Pack 4 inclut les points forts suivants :

* Vous pouvez désormais synchroniser des sous-arborescences de contenu sélectif avec le mode *Contenu* dynamique - Scene7 au lieu de toutes les sous-arborescences disponibles dans `content/dam`.

* L’intégration du modèle de données de formulaire avec le service Web SOAP prend désormais en charge les groupes de choix ou les attributs sur les éléments.

* L’entrée ou la sortie SOAP et les structures de données complexes prennent désormais en charge la substitution de groupe dynamique.

## Principales fonctionnalités des Service Packs version 6.5 d’AEM

### Smart Imaging for Dynamic Media {#smart-imaging}

L’imagerie dynamique utilise les caractéristiques de visualisation uniques de chaque utilisateur pour diffuser automatiquement les images optimisées pour leur expérience, ce qui se traduit par des performances accrues et une meilleure interaction. L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir [Smart Imaging](../assets/imaging-faq.md).

### Recherche visuelle pour AEM Assets {#visual-search}

Les utilisateurs de ressources peuvent rechercher des images visuellement similaires. AEM affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. See [Visual search](../assets/search-assets.md).

### Partage et demande l’accès aux éléments de boîte de réception d’un utilisateur {#share-request-access}

Vous pouvez partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu’un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander à d’autres utilisateurs l’accès aux éléments de la boîte de réception. Voir [Partage et demande d’accès aux éléments de boîte de réception d’un utilisateur](../forms/using/configure-shared-queues-osgi.md).

### Configuration du paramètre d’absence du bureau pour vos éléments de boîte de réception {#configure-out-of-office}

Si vous prévoyez d’être absent du bureau, vous pouvez indiquer ce qui se passe pour les éléments qui vous sont affectés pour cette période.
Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Vous pouvez définir une personne par défaut à laquelle tous vos éléments sont envoyés. Voir [Configuration des paramètres](../forms/using/configure-out-of-office-settings.md)d’absence du bureau.

### Générer plusieurs communications interactives à l’aide de l’API lot {#generate-multiple-ic}

Vous pouvez utiliser l’API de traitement par lots pour produire plusieurs communications interactives à partir d’un modèle. Le modèle est une communication interactive sans données. L’API de traitement par lots combine les données avec un modèle pour produire une communication interactive. L’API est utile pour la production de masse de communications interactives. Par exemple, factures de téléphone, relevés de carte de crédit pour plusieurs clients. Voir [Générer plusieurs communications interactives à l’aide de l’API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)par lot.

### Messages d’erreur de validation standard pour les formulaires adaptatifs {#standard-validation}

Les formulaires adaptatifs peuvent désormais s’intégrer aux services personnalisés pour effectuer des validations de données. Si les valeurs d’entrée ne répondent pas aux critères de validation et que le message d’erreur de validation renvoyé par le serveur est au format standard, les messages d’erreur s’affichent au niveau du champ dans le formulaire. Si les valeurs d’entrée ne répondent pas aux critères de validation et que le message d’erreur de validation du serveur n’est pas au format de message standard, les formulaires adaptatifs fournissent un mécanisme pour transformer les messages d’erreur de validation en un format standard afin qu’ils s’affichent au niveau du champ dans le formulaire. Voir Messages d’erreur de validation [standard pour les formulaires](../forms/using/standard-validation-error-messages-adaptive-forms.md)adaptatifs.

## Principales versions depuis AEM 6.5 SP3

Entre le 12 décembre 2019 et le 5 mars 2020, Adobe a publié les fonctionnalités suivantes, qui ne sont pas du livrable principal d’AEM :

* AEM Cloud Manager 2020.1.0 et 2020.2.0 Améliorations mensuelles apportées à Cloud Manager. Les deux dernières versions ont porté sur l’amélioration de l’état du pipeline et la possibilité de télécharger des journaux pour les différentes étapes. Lisez les notes de mise à jour complètes ici :
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* Mises à jour de l’interface de ligne de commande d’AEM Cloud ManagerAutomatisation du Cloud Manager  à l’aide de l’outil de ligne de commande. Nous étendons continuellement l&#39;interface de ligne de commande - rejoignez [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* Sites AEM : Archétype de projet 23Meilleure méthode pour d’un nouveau projet AEM. Avec Archetype 23, nous [fusionnons l&#39;archétype de projet pour les sites SPA et réguliers en un seul](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23), fournissant un thème par défaut pour lancer-votre développement frontal.

* Sites AEM : Site de référence WKND [Tout nouveau projet](https://www.wknd.site/) de référence contenant les meilleures pratiques pour créer des sites avec AEM. Pour en savoir plus, lisez le didacticiel [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) WKND mis à jour et saisissez le code de [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* Sites AEM : Commerce CIF Core Components 0.7.0 et 0.9.0Intégration de sites AEM et de Magento Commerce. Nous [étendons continuellement des composants principaux dédiés et un Archétype de projet avec une attention particulière au commerce](https://github.com/adobe/aem-core-cif-components/releases).

* Ressources AEM : Application de bureau 2.0.1.1
   [Obtenir un accès de bureau aux ressources](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens : Feature Pack 202001Digital Signage directement depuis AEM. Profitez des dernières améliorations apportées à Feature Pack, cette fois-ci nous [activons la lecture synchrone sur plusieurs lecteurs](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)de médias.

## Ressources utiles

* [Guides de l’utilisateur d’AEM 6.5](../user-guide/capabilities.md)

* [Notes de mise à jour générales d’Adobe Experience Manager 6.5](release-notes.md)

* [Notes de mise à jour du Service Pack pour Adobe Experience Manager 6.5](sp-release-notes.md)
