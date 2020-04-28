---
title: Recommandations relatives aux formulaires HTML5
seo-title: Recommandations relatives aux formulaires HTML5
description: Modifiez vos formulaires HTML5 basés sur XFA pour optimiser les performances.
seo-description: Découvrez comment modifier vos formulaires HTML5 basés sur XFA pour optimiser les performances.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
translation-type: tm+mt
source-git-commit: b6c013a31b70166cba80fea53dffc3794ffee5b8

---


# Recommandations relatives aux formulaires HTML5{#best-practices-for-html-forms}

## Présentation {#overview}

AEM Forms comporte un composant appelé les formulaires HTML5. Il permet d’effectuer le rendu des formulaires PDF basés sur XFA existants (fichiers XDP) au format HTML5. Ce document fournit des conseils et des recommandations pour réduire le temps de chargement et améliorer les performances des formulaires HTML5 sur les périphériques mobiles.

La plupart des périphériques mobiles présentent des capacités de traitement et de mémoire limitées. Il aide à améliorer le temps de veille des périphériques mobiles. Les navigateurs web qui s’exécutent sur un périphérique mobile ont accès à des ressources limitées (capacités de mémoire et de traitement limitées). Lorsque la limite est atteinte, le navigateur devient lent. Ce document propose des recommandations permettant de conserver la taille d’un formulaire HTML5 sous contrôle. Un formulaire plus petit respecte les limites de mémoire et de traitement d’un périphérique et offre une expérience fluide.

Bien que les recommandations abordées dans cet article soient destinées aux formulaires HTML5, elles s’appliquent également aux formulaires PDF basés sur XFA. Ces meilleures pratiques contribuent globalement aux performances globales des formulaires HTML5. Une planification soigneuse permet de développer des formulaires efficaces et productifs. Pour commencer :

## Les nœuds sont la devise des formulaires HTML5, dépensez-les à bon escient. {#nodes-are-currency-of-html-forms-spend-them-wisely}

En règle générale, un formulaire XFA comporte plusieurs éléments. Par exemple, un tableau, un champ de texte et des images. Un certain nombre de propriétés permettent de contrôler le comportement et l’aspect de chaque élément. Lorsqu’un formulaire XFA est rendu au format HTML5, tous les éléments XFA et les propriétés correspondantes sont convertis en nœuds MODEL ou DOM HTML. Ces nœuds augmentent la taille et la complexité d’un DOM. Le rendu du formulaire HTML5 prend plus de temps.

Il est plus facile pour les navigateurs d’effectuer le rendu d’un DOM plus petit. Ainsi, vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour réduire le nombre de nœuds. Par conséquent, vous devez créer une structure DOM allégée :

* Utilisez la propriété de légende pour ajouter un libellé à un champ. N’utilisez pas un élément de texte distinct pour ajouter un libellé. Cela permet d’alléger la structure et d’améliorer les performances. Cela permet également d’éviter les problèmes de mise en page.
* Limitez le nombre d’éléments de texte de dessin sur un formulaire au strict minimum. Les éléments de dessin permettent d’améliorer la lisibilité et l’apparence mais ne permettent pas de stocker des informations. Nous vous conseillons de fusionner les éléments de texte de dessin multiples dans un élément de texte de dessin. Essayez de réduire le volume d’un formulaire par tous les moyens.

## Les formulaires légers sont plus performants et permettent de conserver les ressources compressées {#lite-forms-perform-better-keep-the-resources-compressed}

Un formulaire HTML5 peut contenir plusieurs ressources externes, telles que des fichiers image, JavaScript et CSS. Chaque fois que le navigateur demande un formulaire, les ressources externes sont envoyées via le réseau. Le temps nécessaire pour la transmission sur le réseau est directement proportionnel à la taille des fichiers.

Par conséquent, la réduction de la taille des ressources externes et l’utilisation des ressources absolument nécessaires est la meilleure méthode pour améliorer les performances des formulaires. Vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour réduire la taille des ressources externes d’un formulaire :

* Utilisez des [images compressées](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Cela réduit l’activité réseau et la quantité de mémoire réseau nécessaire pour effectuer le rendu d’un formulaire. Par conséquent, le temps de chargement du formulaire diminue de manière significative.
* Utilisez l’option de minimisation dans AEM Configuration Manager (Day CQ HTML Library Manager) pour compresser les fichiers JavaScript et CSS. Pour plus de détails, voir [Paramètres de configuration sur OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Activez la compression web. Cela réduit la taille des requêtes et des réponses issues d’un formulaire. Pour plus d’informations, voir [Réglage des performances du serveur AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/performance-tuning-aem-forms.html).

## Maintenez l’intérêt en affichant uniquement les champs obligatoires  {#keep-the-interest-alive-show-only-required-fields}

Un formulaire HTML5 peut s’exécuter dans plusieurs centaines de pages. Un formulaire avec un grand nombre de champs est lent à charger dans le navigateur. Vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour optimiser les formulaires contenant un grand nombre de champs et de pages.

* Envisagez de diviser les formulaires volumineux en plusieurs formulaires. Vous pouvez également utiliser un ensemble de formulaires pour regrouper tous les formulaires plus petits et les présenter sous forme d’une seule unité. Un jeu de formulaires ne charge que les formulaires requis. De plus, dans un jeu de formulaires, vous pouvez configurer les champs communs de différents formulaires pour qu’ils partagent les liaisons de données. Les liaisons de données permettent aux utilisateurs de remplir les informations communes une seule fois. Ces dernières sont ensuite complétées automatiquement dans les formulaires suivants, ce qui améliore considérablement les performances. Pour de plus amples informations, voir [Jeu de formulaires dans AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html).
* Envisagez de diviser les sections et de placer chacune d’elles sur une page différente. Les formulaires HTML5 chargent dynamiquement chaque page lors de la requête de défilement de page. Seules les pages consultées (la page en cours d’affichage et les pages précédentes) sont stockées dans la mémoire ; le reste des pages est chargé sur demande. Par conséquent, la division et le placement d’une section sur une page distincte réduisent la durée de chargement d’un formulaire. Vous pouvez également utiliser la première page du formulaire en tant que page d’entrée. Elle est semblable à la table des matières d’un livre. Une page d’entrée du formulaire contient uniquement les liens conduisant vers d’autres sections du formulaire. Elle améliore considérablement le temps de chargement de la première page du formulaire et l’expérience utilisateur.
* Laissez les sections conditionnelles masquées par défaut. Affichez-les uniquement quand une condition spécifique est remplie. Cela permet de conserver la taille minimale du DOM. Vous pouvez également utiliser la navigation par onglets pour afficher une seule section à la fois.

## Pour faire mieux avec moins, réduisez le nombre de pages {#less-is-more-reduce-the-number-of-pages}

Les formulaires HTML5 peuvent contenir des champs axés sur des données (tableaux et sous-formulaires). Ces champs augmentent la taille du formulaire à l’exécution. Par exemple, un tableau axé sur des données d’un formulaire HTML5 peut contenir des milliers de lignes. Ces tableaux peuvent entraîner une dégradation de la mise en page et des performances. Les optimisations suggérées ci-dessous peuvent vous aider à réduire le temps de chargement des formulaires HTML5 contenant des champs axés sur des données :

* Utilisez des scripts XFA pour obtenir une navigation paginée pour afficher les champs axés sur des données (tableaux et sous-formulaires). Dans la navigation paginée, seules des données spécifiques sont affichées sur une page. Elle limite l’opération de peinture du navigateur aux champs affichés à la fois et facilite la navigation dans un formulaire. De plus, les utilisateurs des périphériques mobiles sont intéressés uniquement par un sous-ensemble de données. Cela permet de fournir une expérience utilisateur de grande qualité et de réduire le délai nécessaire au chargement des données requises. Vous obtenez deux solutions pour le prix d’une.  Notez également que la navigation par page n’est pas disponible en dehors de la zone. Vous pouvez utiliser des scripts XFA en vue de développer la navigation paginée.

* Envisagez de fusionner plusieurs colonnes en lecture seule en une seule colonne. Cela réduit la mémoire requise pour afficher le formulaire. En outre, il est préférable de ne pas afficher les colonnes qui n’exigent aucune intervention de la part de l’utilisateur.
* Envisagez de diviser le formulaire axé sur des données pour obtenir un [ensemble de formulaires](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html) si les suggestions ci-dessus ne produisent pas de nombreuses améliorations. Par exemple, si un tableau contient plus de 1 000 lignes, déplacez alors chaque ensemble de 100 lignes dans un formulaire différent. Cela permet d’améliorer le temps de chargement et les performances des formulaires.  Notez également qu’un jeu de formulaires génère un XML d’envoi consolidé pour tous les formulaires. Pour différencier les données de chaque formulaire, utilisez différentes racines de données. Pour plus d’informations, voir [Jeu de formulaires dans AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html).

## Power of two for Document of Record (DOR) {#power-of-two-for-document-of-record-dor}

Dans un formulaire XFA, un grand nombre de sections peut être dédié uniquement à un document d’enregistrement. Pour réduire le nombre de noeuds et améliorer les performances d’un tel formulaire, vous pouvez conserver différentes copies du formulaire : une copie pour remplir le formulaire et une autre pour générer des  d’enregistrement sur le serveur. Dans la copie utilisée pour remplir le formulaire XFA, affichez les champs requis uniquement pour capturer des données. Dans le formulaire XFA de génération du document d’enregistrement, conservez les champs requis uniquement dans la sortie imprimée du formulaire. Avant de choisir l’approche suggérée, évaluez le gain de performances et la surcharge de maintenance.

## Lectures recommandées  {#recommended-reads}

Adobe Experience Manager (AEM) Forms vous permet de transformer des opérations complexes en de simples et remarquables expériences numériques. Toutefois, vous devez chercher à développer des formulaires efficaces et productifs. Outre les formulaires HTML5, voici quelques recommandations de lecture au sujet des meilleures pratiques générales concernant AEM :

* [Meilleures pratiques pour le déploiement et la maintenance d’AEM](/help/sites-deploying/best-practices.md)
* [Meilleures pratiques pour la création de contenu](/help/sites-authoring/best-practices.md)
* [Meilleures pratiques d’administration dans AEM](/help/sites-administering/administer-best-practices.md) 
* [Meilleures pratiques pour le développement de solutions](/help/sites-developing/best-practices.md)
* [Meilleures pratiques pour travailler avec les formulaires adaptatifs](/help/forms/using/adaptive-forms-best-practices.md)
* [Le serveur AEM Forms n’incorpore pas de polices à un formulaire PDF dynamique.](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Carte de référence rapide {#quick-reference-card}

Vous pouvez imprimer la carte suivante (cliquez sur la carte pour télécharger une version haute résolution) et la conserver sur votre bureau pour une référence rapide :
Carte de référence rapide des meilleures pratiques des formulaires[ ![HTML5](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
