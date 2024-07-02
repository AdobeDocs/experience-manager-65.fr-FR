---
title: Recommandations relatives aux formulaires HTML5
description: Modifiez vos formulaires HTML5 basés sur XFA pour optimiser les performances.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '1402'
ht-degree: 100%

---

# Recommandations relatives aux formulaires HTML5{#best-practices-for-html-forms}

## Présentation {#overview}

AEM Forms possède un composant appelé formulaires HTML5. Il permet d’effectuer le rendu des PDF forms existants basés sur XFA (fichiers XDP) au format HTML5. Ce document fournit des lignes directrices et des recommandations pour réduire le temps de chargement et améliorer les performances des formulaires HTML5 sur les appareils mobiles.

La plupart des appareils mobiles ont une puissance de traitement et des capacités de mémoire limitées. Cela contribue à améliorer le temps de veille des appareils mobiles. Les navigateurs web exécutés sur un appareil mobile ont accès à des ressources limitées (mémoire et capacités de traitement limitées). Une fois la limite atteinte, le comportement du navigateur devient lent. Ce document fournit des recommandations pour contrôler la taille d’un formulaire HTML5. Un formulaire plus petit n’enfreint pas les limites de mémoire et de puissance de traitement d’un appareil et offre une expérience fluide.

Bien que les recommandations abordées dans cet article soient destinées aux formulaires HTML5, elles s’appliquent également aux formulaires PDF basés sur XFA. Ces meilleures pratiques contribuent globalement aux performances globales des formulaires HTML5. Une planification soigneuse permet de développer des formulaires efficaces et productifs. Commençons !

## Les nœuds sont la monnaie des formulaires HTML5, utilisez-les judicieusement {#nodes-are-currency-of-html-forms-spend-them-wisely}

Généralement, un formulaire XFA comporte plusieurs éléments. Par exemple, un tableau, un champ de texte et des images. Chaque élément possède plusieurs propriétés pour contrôler son comportement et son apparence. Lorsqu’un formulaire XFA est rendu au format HTML5, tous les éléments XFA et les propriétés correspondantes sont convertis en nœuds Model ou HTML DOM. Ces nœuds ajoutent à la taille et à la complexité d’un DOM. Cela ralentit le rendu du formulaire HTML5.

Il est plus facile pour les navigateurs d’effectuer le rendu d’un DOM plus épuré. Ainsi, vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour réduire le nombre de nœuds. Par conséquent, générez une structure DOM allégée :

* Utilisez la propriété de légende pour ajouter une étiquette à un champ. N’utilisez pas d’élément Text distinct pour ajouter une étiquette. Cela aide à perdre du poids supplémentaire, entraînant des gains de performances. Cela permet également d’éviter les problèmes de mise en page.
* Gardez le nombre d’éléments de texte Draw sur un formulaire au strict minimum. Les éléments Draw sont utiles pour améliorer la lisibilité et l’apparence, mais n’ont aucune capacité de stockage d’informations. Il est conseillé de fusionner plusieurs éléments de texte Draw en un seul. Ne négligez aucun effort pour épurer davantage un formulaire.

## Les formulaires allégés fonctionnent mieux et conservent les ressources compressées {#lite-forms-perform-better-keep-the-resources-compressed}

Un formulaire HTML5 peut contenir plusieurs ressources externes, telles que des fichiers image, JavaScript et CSS. Chaque fois qu’un navigateur demande un formulaire, les ressources externes sont envoyées sur le réseau. Le temps nécessaire pour parcourir le réseau est directement proportionnel à la taille des fichiers.

Par conséquent, la réduction de la taille des ressources externes et l’utilisation unique des ressources absolument nécessaires sont la méthode privilégiée pour améliorer les performances des formulaires. Vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour réduire la taille des ressources externes d’un formulaire :

* Utilisez des [images compressées](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Cela réduit l’activité du réseau et la quantité de mémoire requise pour effectuer le rendu d’un formulaire. Par conséquent, le temps de chargement du formulaire diminue considérablement.
* Utilisez l’option de minification dans AEM Configuration Manager (Day CQ HTML Library Manager) pour compresser les fichiers JavaScript et CSS. Pour plus de détails, voir [Paramètres de configuration sur OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Activez la compression web. Elle permet de réduire la taille des requêtes et des réponses provenant d’un formulaire. Pour plus d’informations, voir [Réglage des performances du serveur AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/performance-tuning-aem-forms.html).

## Maintenez l’intérêt en affichant uniquement les champs obligatoires.  {#keep-the-interest-alive-show-only-required-fields}

Un formulaire HTML5 peut contenir des centaines de pages. Un formulaire comportant un grand nombre de champs est lent à charger dans le navigateur. Vous pouvez effectuer les optimisations suivantes sur un formulaire XFA pour optimiser les formulaires comportant un grand nombre de champs et de pages :

* Envisagez de diviser les formulaires volumineux en plusieurs formulaires. Vous pouvez également utiliser un jeu de formulaires pour regrouper tous les formulaires plus petits et les présenter sous forme d’une seule unité. Un jeu de formulaires charge uniquement les formulaires requis. De plus, dans un jeu de formulaires, vous pouvez configurer les champs communs de différents formulaires pour qu’ils partagent les liaisons de données. Les liaisons de données permettent aux utilisateurs et aux utilisatrices de remplir les informations communes une seule fois. Ces dernières sont ensuite complétées automatiquement dans les formulaires suivants, ce qui améliore considérablement les performances. Pour plus d’informations sur les jeux de formulaires, consultez [Jeu de formulaires dans AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html).
* Envisagez de diviser les sections et de déplacer chaque section vers une page différente. Les formulaires HTML5 chargent dynamiquement chaque page lors d’une requête de défilement de page. Seules les pages consultées (la page en cours d’affichage et les pages précédentes) sont stockées en mémoire ; le reste des pages est chargé à la demande. Ainsi, diviser et déplacer une section sur une page distincte réduit le temps nécessaire au chargement d’un formulaire. Vous pouvez également utiliser la première page du formulaire comme page de destination. Elle est similaire à la table des matières (TM) d’un livre. Une page de destination de formulaire contient uniquement des liens vers les autres sections du formulaire. Cela améliore considérablement le temps de chargement de la première page du formulaire et entraîne une meilleure expérience client.
* Par défaut, gardez les sections conditionnelles masquées. Affichez-les uniquement quand une condition spécifique est remplie. Cela permet de réduire au minimum la taille du DOM. Vous pouvez également utiliser la navigation par onglets pour n’afficher qu’une seule section à la fois.

## Pour faire mieux avec moins, réduisez le nombre de pages. {#less-is-more-reduce-the-number-of-pages}

Les formulaires HTML5 peuvent contenir des champs basés sur des données (tableaux et sous-formulaires). Ces champs augmentent la taille du formulaire au moment de l’exécution. Par exemple, un tableau basé sur des données dans un formulaire HTML5 peut s’étendre sur des milliers de lignes. De tels tableaux peuvent entraîner une dégradation de la disposition et des performances. Les optimisations suggérées ci-dessous peuvent vous aider à réduire le temps de chargement des formulaires HTML5 avec des champs basés sur des données :

* Utilisez des scripts XFA pour obtenir une navigation paginée afin d’afficher les champs basés sur des données (tableaux et sous-formulaires). En navigation paginée, seule des données spécifiques sont affichées sur une page. Il limite l’opération de peinture du navigateur aux champs affichés à un moment donné et facilite la navigation dans un formulaire. De plus, les utilisateurs des appareils mobiles sont intéressés uniquement par un sous-ensemble de données. Cela permet de fournir une expérience utilisateur de grande qualité et de réduire le délai nécessaire au chargement des données requises. Vous obtenez deux solutions pour le prix d’une.  Notez également que la navigation paginée n’est pas disponible en mode prêt à l’emploi. Vous pouvez utiliser les scripts XFA pour développer une navigation paginée.

* Envisagez de fusionner plusieurs colonnes en lecture seule en une seule colonne. Cela permet de réduire la mémoire requise pour afficher le formulaire. Évitez également d’afficher les colonnes qui ne nécessitent aucune saisie de la part des utilisateurs et utilisatrices.
* Envisagez de diviser le formulaire basé sur des données en un [jeu de formulaires](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html), si les suggestions ci-dessus n’apportent pas vraiment d’améliorations. Par exemple, si un tableau contient plus de 1 000 lignes, déplacez chaque ensemble de 100 lignes dans un formulaire différent. Cela permet d’améliorer le temps de chargement et les performances des formulaires.  Notez également qu’un jeu de formulaires produit un fichier XML d’envoi consolidé pour tous les formulaires. Pour différencier les données de chaque formulaire, utilisez différentes racines de données. Pour plus d’informations, voir [Jeu de formulaires dans AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-3/formset-in-aem-forms.html).

## Puissance deux pour le document d’enregistrement {#power-of-two-for-document-of-record-dor}

Un formulaire XFA peut comporter un grand nombre de sections dédiées uniquement au document d&#39;enregistrement (DOR). Pour réduire le nombre de nœuds et améliorer les performances d’un formulaire de ce type, vous pouvez conserver différentes copies du formulaire, une copie pour remplir le formulaire et une autre pour générer le document d’enregistrement sur le serveur. Dans la copie pour remplir le formulaire XFA, affichez les champs requis uniquement pour capturer les données. Dans le document d’enregistrement XFA généré, conservez les champs requis uniquement dans la sortie imprimée du formulaire. Avant de choisir l’approche suggérée, évaluez le gain de performances et les frais généraux de maintenance.

## Lectures recommandées  {#recommended-reads}

Les formulaires Adobe Experience Manager (AEM) peuvent vous aider à transformer des transactions complexes en expériences numériques simples et attrayantes. Cependant, cela nécessite des efforts concertés pour développer des formulaires efficaces et productifs. Outre HTML5 Forms, voici quelques recommandations de lecture concernant les bonnes pratiques générales d’AEM :

* [Bonnes pratiques en matière de déploiement et de maintenance d’AEM](/help/sites-deploying/best-practices.md)
* [Meilleures pratiques pour la création de contenu](/help/sites-authoring/best-practices.md)
* [Meilleures pratiques d’administration dans AEM ](/help/sites-administering/administer-best-practices.md)
* [Meilleures pratiques pour le développement de solutions](/help/sites-developing/best-practices.md)
* [Meilleures pratiques pour travailler avec les formulaires adaptatifs](/help/forms/using/adaptive-forms-best-practices.md)
* [Le serveur AEM Forms n’incorpore pas de polices à un formulaire PDF dynamique](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Carte de référence rapide {#quick-reference-card}

Vous pouvez imprimer la carte suivante (cliquez sur la carte pour télécharger une version haute résolution) et la conserver sur votre bureau pour une référence rapide :
[![Carte de référence rapide sur les bonnes pratiques de HTML5 Forms](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
