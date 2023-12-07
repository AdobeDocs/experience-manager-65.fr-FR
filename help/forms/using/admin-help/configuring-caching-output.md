---
title: Configurer la mise en cache pour la sortie
description: Le service Output met en cache les conceptions de formulaire, les fragments et les images. Découvrez comment configurer la mise en cache pour la sortie.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 22%

---

# Configurer la mise en cache pour la sortie  {#configuring-caching-for-output}

Le service Output fusionne les données de formulaire XML avec une conception de formulaire créée dans Designer pour créer un flux de sortie de document dans différents formats.

La page Output d’Administration Console contient des paramètres qui contrôlent la manière dont le service Output met en cache les éléments. Vous pouvez ajuster ces paramètres pour optimiser les performances du service Output.

Le service Output met en cache les éléments suivants :

* **conceptions de formulaire :** le service Output met en cache les conceptions de formulaire qu’il récupère du référentiel ou de sources HTTP. Cette mise en cache améliore les performances car le service Output récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des demandes de rendu ultérieures.
* **fragments et images :** le service Output peut mettre en cache les fragments et les images utilisés dans les conceptions de formulaire. Lorsque le service Output met en cache ces objets, il améliore les performances car les fragments et les images ne sont lus à partir du référentiel que lors de la première requête.

Output stocke le cache à deux emplacements :

* **en mémoire :** Les éléments sont stockés en mémoire pour un accès rapide. Le cache en mémoire a une taille limitée et est supprimé lorsque vous redémarrez le serveur.
* **sur le disque :** Les éléments sont stockés dans le système de fichiers du serveur. La capacité du cache disque est supérieure à celle du cache en mémoire et elle est conservée lorsque vous redémarrez le serveur. L’emplacement du cache disque dépend de votre serveur d’applications. Pour plus d’informations sur la modification de l’emplacement du cache disque, voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Spécification du mode de cache {#specifying-the-cache-mode}

Output prend en charge deux modes de mise en cache :

* inconditionnel
* utilisation du point de contrôle du cache

Si vous basculez entre les modes de mise en cache, redémarrez le service Output pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou voir [Démarrage ou arrêt des services associés aux modules d’AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

L’heure du point de contrôle du cache est réinitialisée automatiquement lorsque vous passez d’un mode à l’autre.

### Utilisation de la mise en cache inconditionnelle {#using-unconditional-caching}

Dans ce mode, lorsque le service Output reçoit une demande, il valide les ressources requises (conception de formulaire et tout actif associé comme les fragments et les images). Le service Output compare l’horodatage des ressources du référentiel à l’horodatage des ressources du cache. Si la ressource du cache est plus ancienne, le service Output la met à jour.

Ce mode de mise en cache garantit que les ressources les plus récentes sont utilisées. Toutefois, les performances sont affectées, car le service Output valide les éléments mis en cache par rapport au référentiel avec chaque requête. Ce mode de mise en cache est adapté aux environnements de développement et d’évaluation dans lesquels les ressources sont fréquemment mises à jour et où les performances ne sont pas une préoccupation principale.

**Spécification d’une mise en cache inconditionnelle**

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, sélectionnez Sans condition et cliquez sur Enregistrer.

### Utilisation du point de contrôle du cache {#use-the-cache-check-point}

Dans ce mode, le service Output ne recherche les nouvelles versions des ressources dans le référentiel que lorsque l’horodatage de la ressource mise en cache est antérieur à l’heure du point de contrôle du cache. L’heure du dernier point de contrôle du cache s’affiche sur la page Output d’Administration Console.

Utilisez ce mode de mise en cache dans des environnements de production hautement performants où les performances sont problématiques et où les modifications apportées aux ressources sont peu fréquentes. Vous pouvez réinitialiser l’heure du point de contrôle du cache lorsque vous souhaitez déployer les modifications apportées aux ressources du référentiel.

**Définition de l’utilisation d’un point de contrôle du cache**

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, sélectionnez Uniquement si leur dernière validation a été effectuée avant l’heure du point de contrôle du cache, puis cliquez sur Enregistrer.

**Réinitialisation du point de contrôle du cache**

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, cliquez sur Point de contrôle du cache.

### Réinitialisation du contenu du cache {#reset-the-cache-contents}

Vous pouvez effacer le contenu du cache à tout moment. Après la réinitialisation du cache, la première demande pour chaque formulaire est plus lente, car le service Output effectue un rendu complet et crée un nouveau contenu de cache.

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, cliquez sur Réinitialiser le cache.

## Configuration des paramètres du cache {#configuring-cache-settings}

Vous pouvez spécifier les paramètres utilisés par Output pour la mise en cache, ce qui peut optimiser les performances de votre environnement d’AEM forms.

Pour accéder à ces paramètres, dans Administration Console, cliquez sur Services > Output.

>[!NOTE]
>
>Les exigences de disque pour le cache doivent être égales au référentiel.

### Spécification des paramètres de cache globaux {#specifying-global-cache-settings}

Les paramètres du **Paramètres du cache global** affecte tous les types de caches. Si vous modifiez l’un de ces paramètres, redémarrez le service Output pour que le changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou voir [Démarrage ou arrêt des services associés aux modules d’AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille max. du document du cache (Ko) :** taille maximale, en kilo-octets, d’une conception de formulaire ou autre ressource pouvant être stockée dans un cache mémoire. Ce paramètre global s’applique à tous les caches en mémoire. Si la ressource est supérieure à cette valeur, elle n’est pas mise en cache en mémoire. La valeur par défaut est 1024 kilo-octets. Ce paramètre n’a aucune incidence sur le cache disque.

**Mise en cache des rendus de formulaire activée :** cette option est sélectionnée par défaut, ce qui signifie que les formulaires rendus sont mis en cache pour récupération ultérieure. Ce paramètre a peu d’effet sur les performances du service Output, car il ne met pas en cache les documents non interactifs. Cette option n’a aucun effet lorsque vous utilisez le service Output pour les documents non interactifs rendus sur le client.

### Mise en cache des conceptions de formulaire {#caching-form-designs}

Lorsque le service Output reçoit une demande de rendu, il récupère la conception de formulaire à partir du référentiel ou d’une source HTTP et la met en cache. Cette mise en cache améliore les performances car le service Output récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des requêtes de rendu ultérieures.

Le service Output met toujours les conceptions de formulaire en cache sur le disque. Si les conceptions de formulaire sont stockées sur le serveur, ces fichiers sont considérés comme le cache disque. Le service Output met également en cache les conceptions de formulaire en mémoire, selon le paramètre défini dans la variable **Mémoire cache des modèles** zone. Si vous modifiez l’un de ces paramètres, redémarrez le service Output pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou voir [Démarrage ou arrêt des services associés aux modules d’AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille du cache de configuration des modèles :** nombre maximal d’objets de configuration de modèle à conserver en mémoire. La valeur par défaut est 100. Il est recommandé de définir cette valeur sur une valeur supérieure ou égale à la valeur Taille du cache du modèle . Ce paramètre n’a aucune incidence sur le cache disque.

**Taille du cache des modèles :** nombre maximal d’objets de contenu de modèle à conserver en mémoire. La valeur par défaut est 100. Ce paramètre n’a aucune incidence sur le cache disque.

**Activé :** cette case est cochée par défaut, ce qui signifie que les modèles de formulaire sont mis en mémoire cache. Lorsque cette option n’est pas sélectionnée, les modèles de formulaire sont uniquement mis en cache sur le disque.

### Mise en cache des fragments et des images {#caching-fragments-and-images}

Le service Output met en cache les fragments et les images utilisés dans les conceptions de formulaire sur le disque. Cela améliore les performances car les fragments et les images ne sont lus à partir du référentiel que lors de la première requête. Ensuite, lors des demandes suivantes, le service Output lit les fragments et les images du cache disque. Les fragments et les images ne sont mis en cache que sur le disque et non dans la mémoire.

Vous pouvez utiliser les paramètres suivants pour contrôler la mise en cache sur disque des fragments et des images. Ces paramètres se trouvent dans la variable **Paramètres du cache des ressources de modèle** area :

**Mise en cache de ressources :** sélectionnez l’une des options suivantes dans la liste :

**Activée pour les fragments et les images :** le service Output met les fragments et les images en cache. Il s’agit de l’option par défaut.

**Activée pour les fragments :** le service Output met les fragments en cache, mais pas les images.

**Désactivée :** le service Output ne met ni les fragments, ni les images en cache.

**Intervalle de nettoyage (secondes) :** détermine la fréquence de suppression des anciens fichiers cache non valides par le service Output. Le service Output ne supprime pas les fichiers cache valides. Si vous modifiez l’intervalle de nettoyage, redémarrez le service Output pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou consultez la section Démarrage ou arrêt des services associés aux modules AEM Forms pour obtenir des instructions.

## Remarques relatives à la mise en grappe pour les caches {#clustering-considerations-for-caches}

Dans un environnement organisé en grappe, chaque noeud conserve sa propre mémoire et son propre cache disque. Le contenu du cache sur chaque noeud dépend des formulaires qui ont été rendus sur ce noeud.

L’emplacement du cache doit être identique (même disque et chemin d’accès) sur chaque noeud de la grappe. Ne placez pas le cache sur le stockage partagé.

Si vous utilisez la page Output d’Administration Console pour modifier les paramètres du cache d’un noeud particulier, les paramètres du cache des autres noeuds sont mis à jour lorsqu’une requête atteint ce noeud. Ce comportement s’applique également au bouton Réinitialiser le cache . Si vous cliquez sur le bouton Réinitialiser le cache pour un noeud, le cache est immédiatement supprimé de ce noeud. Le cache sur les autres noeuds est effacé lorsqu’une requête atteint ce noeud.
