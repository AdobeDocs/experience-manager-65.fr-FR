---
title: Configuration du cache pour Forms
description: Découvrez comment configurer les paramètres du cache et comment prendre en compte les considérations de grappe pour les caches.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 28%

---

# Configuration du cache pour Forms{#configuring-caching-for-forms}

Le service Forms prend les conceptions de formulaire créées dans Designer et les effectue dans différents formats.

La page Forms d’Administration Console contient des paramètres qui contrôlent la manière dont le service Forms met en cache les éléments. Vous pouvez ajuster ces paramètres pour optimiser les performances du service Forms.

Le service Forms met en cache les éléments suivants :

* **conceptions de formulaire :** le service Forms met en cache les conceptions de formulaire qu’il récupère du référentiel ou de sources HTTP. Cette mise en cache améliore les performances, car le service Forms récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des demandes de rendu ultérieures.
* **fragments et images :** le service Forms peut mettre en cache les fragments et les images utilisés dans les conceptions de formulaire. Lorsque le service Forms met en cache ces objets, il améliore les performances car les fragments et les images ne sont lus à partir du référentiel qu’à la première demande.
* **formulaires :** le service Forms met en cache les formulaires qu’il rend. Ce type de mise en cache améliore les performances, car le service Forms n’a pas besoin de résoudre et de générer le même formulaire dans les demandes ultérieures.

Forms stocke le cache à deux emplacements :

* **en mémoire :** Les éléments sont stockés en mémoire pour un accès rapide. Le cache en mémoire a une taille limitée et est supprimé lorsque vous redémarrez le serveur.
* **sur le disque :** Les éléments sont stockés dans le système de fichiers du serveur. La capacité du cache disque est supérieure à celle du cache en mémoire et elle est conservée lorsque vous redémarrez le serveur. L’emplacement du cache disque dépend de votre serveur d’applications. Pour plus d’informations sur la modification de l’emplacement du cache disque, voir [Configuration des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Spécification du mode de cache {#specifying-the-cache-mode}

Forms prend en charge deux modes de mise en cache :

* inconditionnel
* utilisation du point de contrôle du cache

Si vous basculez entre les modes de mise en cache, redémarrez le service Forms pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou voir [Démarrage ou arrêt des services associés aux modules d’AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

L’heure du point de contrôle du cache est réinitialisée automatiquement lorsque vous passez d’un mode à l’autre.

### Utilisation de la mise en cache inconditionnelle {#using-unconditional-caching}

Dans ce mode, lorsque le service Forms reçoit une demande, il valide les ressources requises (conception de formulaires et tout actif associé comme les fragments et les images). Le service Forms compare l’horodatage des ressources du référentiel à l’horodatage des ressources du cache. Si la ressource du cache est plus ancienne, le service Forms la met à jour.

Ce mode de mise en cache garantit que les ressources les plus récentes sont utilisées. Toutefois, les performances sont affectées, car le service Forms valide les éléments mis en cache par rapport au référentiel avec chaque requête. Ce mode de mise en cache est adapté aux environnements de développement et d’évaluation dans lesquels les ressources sont fréquemment mises à jour et où les performances ne sont pas une préoccupation principale.

**Spécification d’une mise en cache inconditionnelle**

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Paramètres de contrôle du cache de Forms, sélectionnez Sans condition et cliquez sur Enregistrer.

### Utilisation du point de contrôle du cache {#use-the-cache-check-point}

Dans ce mode, le service Forms recherche uniquement les nouvelles versions des ressources dans le référentiel lorsque l’horodatage de la ressource mise en cache est antérieur à l’heure du point de contrôle du cache. L’heure du dernier point de contrôle du cache s’affiche sur la page Forms dans Administration Console.

Utilisez ce mode de mise en cache dans des environnements de production hautement performants où les performances sont problématiques et où les modifications apportées aux ressources sont peu fréquentes. Vous pouvez réinitialiser l’heure du point de contrôle du cache lorsque vous souhaitez déployer les modifications apportées aux ressources du référentiel.

**Définition de l’utilisation d’un point de contrôle du cache**

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Paramètres de contrôle du cache de Forms, sélectionnez Uniquement si leur dernière validation a été effectuée avant l’heure du point de contrôle du cache, puis cliquez sur Enregistrer.

**Réinitialisation du point de contrôle du cache**

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Paramètres de contrôle du cache de Forms, cliquez sur Point de contrôle du cache.

**Réinitialisation du contenu du cache**

Vous pouvez effacer le contenu du cache à tout moment. Après la réinitialisation du cache, la première demande pour chaque formulaire est plus lente, car le service Forms effectue un rendu complet et crée un nouveau contenu de cache.

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Paramètres de contrôle du cache de Forms, cliquez sur Réinitialiser le cache.

## Configuration des paramètres du cache {#configuring-cache-settings}

Vous pouvez spécifier les paramètres utilisés par Forms pour la mise en cache, ce qui peut optimiser les performances de votre environnement d’AEM forms.

Pour accéder à ces paramètres, dans Administration Console, cliquez sur Services > Forms.

>[!NOTE]
>
>Les exigences de disque pour le cache doivent être égales au référentiel.

### Spécification des paramètres de cache globaux {#specifying-global-cache-settings}

Les paramètres du **Paramètres du cache global** affecte tous les types de caches. Si vous modifiez l’un de ces paramètres, redémarrez le service Forms pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou voir [Démarrage ou arrêt des services associés aux modules d’AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille max. du document du cache (Ko) :** taille maximale, en kilo-octets, d’une conception de formulaire ou autre ressource pouvant être stockée dans un cache mémoire. Ce paramètre global s’applique à tous les caches en mémoire. Si une ressource est supérieure à cette valeur, elle n’est pas mise en cache en mémoire. La valeur par défaut est 1024 kilo-octets. Ce paramètre n’a aucune incidence sur le cache disque.

**Mise en cache des rendus de formulaire activée :** cette option est sélectionnée par défaut, ce qui signifie que les formulaires rendus sont mis en cache pour récupération ultérieure. Ce paramètre améliore les performances car le service Forms ne doit effectuer le rendu d’un formulaire spécifique qu’une seule fois, puis utilise la version mise en cache. Cette option fonctionne avec la propriété de mise en cache de la conception de formulaire. Pour plus d’informations sur la configuration de cette valeur lors de la conception de formulaire, voir Aide de Designer.

### Mise en cache des conceptions de formulaire {#caching-form-designs}

Lorsque le service Forms reçoit une demande de rendu, il récupère la conception de formulaire du référentiel et la met en cache. Cette mise en cache améliore les performances, car le service Forms récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des requêtes de rendu ultérieures.

Le service Forms met toujours les conceptions de formulaire en cache sur le disque. Si les conceptions de formulaire sont stockées sur le serveur, ces fichiers sont considérés comme le cache disque. Le service Forms met également en cache les conceptions de formulaire en mémoire, selon le paramètre défini dans la variable **Mémoire cache des modèles** zone. Si vous modifiez l’un de ces paramètres, redémarrez le service Forms pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou voir [Démarrage ou arrêt des services associés aux modules d’AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille du cache de configuration des modèles :** nombre maximal d’objets de configuration de modèle à conserver en mémoire. La valeur par défaut est 100. Il est recommandé de définir cette valeur sur une valeur supérieure ou égale à la valeur Taille du cache du modèle . Ce paramètre n’a aucune incidence sur le cache disque.

**Taille du cache des modèles :** nombre maximal d’objets de contenu de modèle à conserver en mémoire. La valeur par défaut est 100. Ce paramètre n’a aucune incidence sur le cache disque.

**Activé :** cette case est cochée par défaut, ce qui signifie que les modèles de formulaire sont mis en mémoire cache. Lorsque cette option n’est pas sélectionnée, les modèles de formulaire sont uniquement mis en cache sur le disque.

### Mise en cache des formulaires rendus {#caching-rendered-forms}

Le service Forms met en cache les formulaires rendus afin qu’il n’ait pas à résoudre et à générer le même formulaire dans les demandes ultérieures. Les formulaires rendus sont mis en cache sur le disque et en mémoire.

Ces paramètres se trouvent dans la variable **Cache de rendu de formulaire en mémoire** zone. Si vous modifiez l’un de ces paramètres, redémarrez le service Forms pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou voir [Démarrage ou arrêt des services associés aux modules d’AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille du cache :** détermine le nombre maximal de formulaires rendus pouvant se trouver dans le cache mémoire. La valeur par défaut est 100. Ce paramètre n’a aucune incidence sur le cache disque.

**Activé :** cette case est cochée par défaut, ce qui signifie que les formulaires rendus sont mis en mémoire cache. Lorsque cette option n’est pas sélectionnée, les formulaires rendus sont uniquement mis en cache sur le disque.

### Mise en cache des fragments et des images {#caching-fragments-and-images}

Le service Forms met en cache les fragments et les images utilisés dans les conceptions de formulaire sur le disque. Cela améliore les performances car les fragments et les images ne sont lus à partir du référentiel que lors de la première requête. Ensuite, lors des demandes suivantes, le service Forms lit les fragments et les images du cache disque. Les fragments et les images ne sont mis en cache que sur le disque et non dans la mémoire.

Vous pouvez utiliser les paramètres suivants pour contrôler la mise en cache sur disque des fragments et des images. Ces paramètres se trouvent dans la variable **Paramètres du cache des ressources de modèle** area :

**Caching de ressources** Sélectionnez l’une des options suivantes dans la liste :

**Activé pour les fragments et les images :** le service Forms met en cache les fragments et les images. Il s’agit de l’option par défaut.

**Activé pour les fragments :** le service Forms met en cache les fragments, mais pas les images.

**Désactivé :** le service Forms ne met ni les fragments, ni les images en cache.

**Intervalle de nettoyage (en secondes) :** il détermine la fréquence de suppression des anciens fichiers de cache non valides par le service Forms. Le service Forms ne supprime pas les fichiers de cache valides. Si vous modifiez l’intervalle de nettoyage, redémarrez le service Forms pour que ce changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou consultez la section Démarrage ou arrêt des services associés aux modules AEM Forms pour obtenir des instructions. La valeur par défaut est de 600 secondes.

## Remarques relatives à la mise en grappe pour les caches {#clustering-considerations-for-caches}

Dans un environnement organisé en grappe, chaque noeud conserve sa propre mémoire et son propre cache disque. Le contenu du cache sur chaque noeud dépend des formulaires qui ont été rendus sur ce noeud.

L’emplacement du cache doit être identique (même disque et chemin d’accès) sur chaque noeud de la grappe. Ne placez pas le cache sur le stockage partagé.

Si vous utilisez la page Forms d’Administration Console pour modifier les paramètres de mise en cache d’un nœud particulier, les paramètres de mise en cache des autres nœuds sont mis à jour lorsqu’une demande atteint le nœud en question. Ce comportement s’applique également au bouton Réinitialiser le cache . Si vous cliquez sur le bouton Réinitialiser le cache pour un noeud, le cache est immédiatement supprimé de ce noeud. Le cache sur les autres noeuds est effacé lorsqu’une requête atteint ce noeud.
