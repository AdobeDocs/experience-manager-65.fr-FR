---
title: Recommandations relatives aux formulaires HTML5
description: Modifiez vos formulaires HTML5 basés sur XFA pour optimiser les performances.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
docset: aem65
feature: HTML5 Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 20%

---

# Recommandations relatives aux formulaires HTML5{#best-practices-for-html-forms}

## Présentation {#overview}

AEM Forms comporte un composant appelé HTML5 forms. Il permet de générer des PDF forms XFA existants (fichiers XDP) au format HTML5. Ce document fournit des instructions et des recommandations pour réduire le temps de chargement et améliorer les performances des formulaires HTML5 sur les périphériques mobiles.

La plupart des périphériques mobiles ont une puissance de traitement et des capacités de mémoire limitées. Cela permet d’améliorer l’heure de veille des appareils mobiles. Les navigateurs web s’exécutant sur un appareil mobile ont accès à des ressources limitées (mémoire et capacités de traitement limitées). Une fois la limite atteinte, le comportement du navigateur devient atone. Ce document fournit des recommandations pour garder la taille d’un formulaire HTML5 en échec. Un formulaire plus petit n’enfreint pas les limites de mémoire et de puissance de traitement d’un appareil et offre une expérience fluide.

Bien que les recommandations abordées dans cet article soient destinées aux formulaires HTML5, elles s’appliquent également aux formulaires PDF basés sur XFA. Ces meilleures pratiques contribuent globalement aux performances globales des formulaires HTML5. Une planification soigneuse permet de développer des formulaires efficaces et productifs. Commençons par :

## Les noeuds sont la devise des formulaires HTML5, dépensez-les sagement {#nodes-are-currency-of-html-forms-spend-them-wisely}

En règle générale, un formulaire XFA comporte plusieurs éléments. Par exemple, un tableau, un champ de texte et des images. Chaque élément possède plusieurs propriétés pour contrôler le comportement et l’aspect de l’élément. Lorsqu’un formulaire XFA est rendu au format HTML5, tous les éléments XFA et les propriétés correspondantes sont convertis en noeuds DOM de modèle ou de HTML. Ces noeuds augmentent la taille et la complexité d’un DOM. Ralentir le rendu du formulaire HTML5.

Il est plus facile pour les navigateurs de rendre un DOM plus allégé. Ainsi, vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour réduire le nombre de noeuds. Par conséquent, générez une structure DOM allégée :

* Utilisez la propriété caption pour ajouter un libellé à un champ. N’utilisez pas d’élément Texte distinct pour ajouter un libellé. Cela permet de perdre du poids supplémentaire, ce qui entraîne des gains de performances. Cela permet également d’éviter les problèmes de mise en page.
* Le nombre d’éléments de texte de dessin sur un formulaire doit être réduit au minimum. Les éléments de dessin sont utiles pour améliorer la lisibilité et l’aspect, mais ne disposent d’aucune fonctionnalité de stockage d’informations. Il est conseillé de fusionner plusieurs éléments de texte de dessin en un seul élément de texte de dessin. Ne lâchez pas la pierre pour alléger le formulaire.

## Les formulaires Lite sont plus performants et les ressources restent compressées. {#lite-forms-perform-better-keep-the-resources-compressed}

Un formulaire HTML5 peut contenir plusieurs ressources externes, telles que des fichiers image, JavaScript et CSS. Chaque fois qu’un navigateur demande un formulaire, les ressources externes sont envoyées sur le réseau. Le temps nécessaire pour parcourir le réseau est directement proportionnel à la taille des fichiers.

Par conséquent, la réduction de la taille des ressources externes et l’utilisation uniquement des ressources absolument nécessaires est la méthode privilégiée pour améliorer les performances des formulaires. Vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour réduire la taille des ressources externes d’un formulaire :

* Utilisation [images compressées](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Cela réduit l’activité réseau et la quantité de mémoire nécessaire pour générer un formulaire. Par conséquent, le temps de chargement du formulaire diminue considérablement.
* Utilisez l’option de minimisation dans AEM Configuration Manager (Day CQ HTML Library Manager) pour compresser les fichiers JavaScript et CSS. Pour plus d’informations, voir [Paramètres de configuration OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Activez la compression web. Cela réduit la taille des requêtes et des réponses provenant d’un formulaire. Pour plus d’informations, voir [Réglage des performances du serveur AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/performance-tuning-aem-forms.html).

## Maintenir l’intérêt en vie, afficher uniquement les champs requis  {#keep-the-interest-alive-show-only-required-fields}

Un formulaire HTML5 peut s’exécuter sur des centaines de pages. Le chargement d’un formulaire contenant un grand nombre de champs est lent dans le navigateur. Vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour optimiser les formulaires avec un grand nombre de champs et de pages :

* Envisagez de diviser les formulaires volumineux en plusieurs formulaires. Vous pouvez également utiliser un jeu de formulaires pour regrouper tous les formulaires plus petits et les présenter comme une seule unité. Un jeu de formulaires ne charge que les formulaires requis. De plus, dans un jeu de formulaires, vous pouvez configurer des champs communs dans différents formulaires pour partager des liaisons de données. Les liaisons de données aident les utilisateurs à remplir les informations communes une seule fois ; les informations sont automatiquement renseignées dans les formulaires suivants, ce qui entraîne des améliorations substantielles des performances. Pour plus d’informations sur les jeux de formulaires, voir [Jeu de formulaires dans les formulaires AEM](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html).
* Envisagez de diviser les sections et de déplacer chaque section vers une page différente. Les formulaires HTML5 chargent dynamiquement chaque page dans la requête de défilement de page. Seules les pages défilées (la page affichée et les pages qui la précèdent) sont stockées en mémoire ; le reste des pages est chargé à la demande. Ainsi, le fractionnement et le déplacement d’une section sur une page à elle seule réduit le temps nécessaire au chargement d’un formulaire. Vous pouvez également utiliser la première page du formulaire comme page d’entrée. Elle est similaire à la table des matières d’un livre. Une landing page du formulaire contient uniquement des liens vers les autres sections du formulaire. Cela améliore considérablement le temps de chargement de la première page du formulaire et améliore l’expérience utilisateur.
* Conservez les sections conditionnelles masquées par défaut. Rendez ces sections visibles uniquement lorsqu’une condition spécifique est remplie. Cela permet de maintenir la taille du DOM à un minimum. Vous pouvez également utiliser la navigation par onglets pour afficher une seule section à la fois.

## Moins c’est plus, réduire le nombre de pages {#less-is-more-reduce-the-number-of-pages}

Les formulaires HTML5 peuvent contenir des champs pilotés par les données (tableaux et sous-formulaires). Ces champs augmentent la taille du formulaire au moment de l’exécution. Par exemple, un tableau piloté par les données d’un formulaire HTML5 peut contenir des milliers de lignes. De tels tableaux peuvent entraîner une dégradation de la mise en page et des performances. Les optimisations proposées ci-dessous peuvent vous aider à réduire le temps de chargement des formulaires HTML5 avec des champs pilotés par les données :

* Utilisez les scripts XFA pour obtenir une navigation paginée afin d’afficher les champs pilotés par les données (tableaux et sous-formulaires). Dans la navigation paginée, seules des données spécifiques s’affichent sur une page. Il limite l’opération de peinture du navigateur aux champs affichés à un moment donné et facilite la navigation dans un formulaire. De plus, les utilisateurs des appareils mobiles sont intéressés uniquement par un sous-ensemble de données. Cela permet de fournir une expérience utilisateur de grande qualité et de réduire le délai nécessaire au chargement des données requises. Vous obtenez deux solutions pour le prix d’une.  Notez également que la navigation paginée n’est pas disponible en mode prêt à l’emploi. Vous pouvez utiliser des scripts XFA pour développer la navigation paginée.

* Envisagez de fusionner plusieurs colonnes en lecture seule en une seule colonne. Cela réduit la mémoire requise pour afficher le formulaire. Évitez également d’afficher les colonnes qui ne nécessitent aucune entrée de la part des utilisateurs.
* Évaluation de la division du formulaire piloté par les données en une [jeu de formulaires](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html), si les suggestions ci-dessus ne produisent pas de nombreuses améliorations. Par exemple, si un tableau comporte plus de 1 000 lignes, déplacez toutes les 100 lignes dans un autre formulaire. Cela permet d’améliorer le temps de chargement et les performances des formulaires.  Notez également qu’un jeu de formulaires produit un fichier XML d’envoi consolidé pour tous les formulaires. Pour différencier les données de chaque formulaire, utilisez différentes racines de données. Pour plus d’informations, voir [Jeu de formulaires dans AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html).

## Puissance de deux pour le document d’enregistrement (DOR) {#power-of-two-for-document-of-record-dor}

Un formulaire XFA peut comporter un grand nombre de sections dédiées uniquement au document d’enregistrement (DOR). Pour réduire le nombre de nœuds et améliorer les performances d’un formulaire de ce type, vous pouvez conserver différentes copies du formulaire, une copie pour remplir le formulaire et une autre pour générer le document d’enregistrement sur le serveur. Dans la copie destinée à remplir le formulaire XFA, les champs requis pour la capture des données sont affichés. Dans le formulaire XFA de génération de document d’enregistrement, conservez les champs requis uniquement dans la sortie imprimée du formulaire. Avant de choisir l’approche suggérée, évaluez le gain de performance et la surcharge de maintenance.

## Lectures recommandées  {#recommended-reads}

Les formulaires Adobe Experience Manager (AEM) peuvent vous aider à transformer des transactions complexes en expériences numériques simples et attrayantes. Toutefois, il faut un effort concerté pour développer des formes efficaces et productives. Outre HTML5 Forms, voici quelques recommandations de lecture pour les bonnes pratiques générales AEM :

* [Bonnes pratiques en matière de déploiement et de maintenance d’AEM](/help/sites-deploying/best-practices.md)
* [Meilleures pratiques pour la création de contenu](/help/sites-authoring/best-practices.md)
* [Meilleures pratiques d’administration dans AEM ](/help/sites-administering/administer-best-practices.md)
* [Meilleures pratiques pour le développement de solutions](/help/sites-developing/best-practices.md)
* [Meilleures pratiques pour travailler avec les formulaires adaptatifs](/help/forms/using/adaptive-forms-best-practices.md)
* [Le serveur AEM Forms n’incorpore pas de polices à un formulaire PDF dynamique](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Carte de référence rapide {#quick-reference-card}

Vous pouvez imprimer la carte suivante (cliquez sur la carte pour télécharger une version haute résolution) et la conserver sur votre bureau pour une référence rapide :
[![Carte de référence rapide des bonnes pratiques Forms HTML5](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
