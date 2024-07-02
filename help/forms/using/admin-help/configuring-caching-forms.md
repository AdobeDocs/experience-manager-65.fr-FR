---
title: Configuration du cache pour Forms
description: Découvrez comment configurer les paramètres du cache et les considérations à prendre en compte concernant les clusters pour les caches.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '1611'
ht-degree: 100%

---

# Configuration du cache pour Forms{#configuring-caching-for-forms}

Le service Forms utilise des conceptions de formulaire créées dans Designer et les génère sous divers formats.

La page Forms dans la console d’administration contient des paramètres qui contrôlent la manière dont le service Forms met en cache les éléments. Vous pouvez ajuster ces paramètres pour optimiser les performances du service Forms.

Le service Forms met en cache les éléments suivants :

* **conceptions de formulaire :** le service Forms met en cache les conceptions de formulaire qu’il récupère du référentiel ou de sources HTTP. Cette mise en cache améliore les performances, car le service Forms récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des demandes de rendu ultérieures.
* **fragments et images :** le service Forms peut mettre en cache les fragments et les images utilisés dans les conceptions de formulaire. Lorsque le service Forms met en cache ces objets, il améliore les performances car les fragments et les images ne sont lus à partir du référentiel qu’à la première demande.
* **formulaires :** le service Forms met en cache les formulaires qu’il rend. Ce type de mise en cache améliore les performances, car le service Forms n’a pas besoin de résoudre et de générer le même formulaire pour des demandes ultérieures.

Forms stocke le cache à deux emplacements :

* **en mémoire :** les éléments sont stockés en mémoire pour un accès rapide. Le cache en mémoire possède une taille limitée et est supprimé lorsque vous redémarrez le serveur.
* **sur le disque :** les éléments sont stockés dans le système de fichiers du serveur. Le cache sur le disque est doté d’une plus grande capacité que le cache en mémoire et il est conservé au redémarrage du serveur. L’emplacement du cache sur le disque dépend de votre serveur d’applications. Pour plus d’informations sur la modification de l’emplacement du cache sur le disque, voir [Configuration des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Définition du mode de cache {#specifying-the-cache-mode}

Le service Forms gère deux modes de mise en cache :

* sans condition
* en utilisant le point de contrôle du cache.

Si vous basculez entre les différents modes de mise en cache, redémarrez le service Forms pour que ce changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou consultez la section [Démarrage ou arrêt des services associés aux modules AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

L’heure du point de contrôle du cache est automatiquement réinitialisée lors du basculement d’un mode à l’autre.

### Utilisation de la mise en cache sans condition {#using-unconditional-caching}

Dans ce mode, lorsque le service Forms reçoit une requête, il valide les ressources requises (conceptions de formulaire et toute ressource liée comme les fragments et les images). Le service Forms compare la date et l’heure des ressources du référentiel à celles des ressources du cache. Si la ressource du cache est plus ancienne, le service Forms la met à jour.

Ce mode de mise en cache garantit l’utilisation des ressources les plus récentes. Cependant, les performances sont affectées car le service Forms valide les éléments mis en cache en les comparant à ceux du référentiel à chaque requête. Ce mode de mise en cache convient aux environnements de développement ou de test dans lesquels les ressources sont fréquemment mises à jour et pour lesquels les performances ne sont pas la priorité.

**Définition de la mise en cache sans condition**

1. Dans Administration Console, cliquez sur Services > Forms.
1. Dans les Paramètres de contrôle du cache de Forms, sélectionnez Sans condition et cliquez sur Enregistrer.

### Utilisation du point de contrôle du cache {#use-the-cache-check-point}

Dans ce mode, le service Forms ne recherche les versions des ressources les plus récentes dans le référentiel que lorsque la date et l’heure de la ressource mise en cache sont antérieures à l’heure du point de contrôle du cache. L’heure du point de contrôle du cache le plus récent s’affiche dans la page Forms de la console d’administration.

Utilisez ce mode de mise en cache dans des environnements de production hautement performants où les performances sont d’un intérêt important et où les modifications apportées aux ressources sont peu fréquentes. Vous pouvez réinitialiser l’heure du point de contrôle du cache lorsque vous souhaitez déployer les modifications apportées aux ressources du référentiel.

**Définition de l’utilisation d’un point de contrôle du cache**

1. Dans la console d’administration, cliquez sur Services > Formulaires.
1. Dans les Paramètres de contrôle du cache de Forms, sélectionnez Uniquement si la dernière validation est antérieure à l’heure du point de contrôle du cache, puis cliquez sur Enregistrer.

**Réinitialisation du point de contrôle du cache**

1. Dans Administration Console, cliquez sur Services > Forms.
1. Dans les Paramètres de contrôle du cache de Forms, cliquez sur Point de contrôle du cache.

**Réinitialisation du contenu du cache**

Vous pouvez vider le contenu du cache à tout moment. Après la réinitialisation du cache, la premiè requête est plus lente pour chaque formulaire, car le service Forms effectue un rendu complet et crée un nouveau contenu de cache.

1. Dans Administration Console, cliquez sur Services > Forms.
1. Dans les Paramètres de contrôle du cache de Forms, sélectionnez Réinitialiser le cache.

## Configuration des paramètres du cache {#configuring-cache-settings}

Vous pouvez spécifier les paramètres utilisés par le service Forms pour la mise en cache, de façon à optimiser les performances de l’environnement AEM Forms.

Pour accéder à ces paramètres, dans la console d’administration, cliquez sur Services > Formulaires.

>[!NOTE]
>
>La configuration requise sur le disque pour le cache doit être identique à celle du référentiel.

### Définition des paramètres du cache global {#specifying-global-cache-settings}

Les paramètres de la zone **Paramètres du cache global** affectent tous les types de caches. Si vous modifiez l’un de ces paramètres, redémarrez le service Forms pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou consultez la section [Démarrer ou arrêter les services associés aux modules AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille max. du document du cache (Ko) :** taille maximale, en kilo-octets, d’une conception de formulaire ou autre ressource pouvant être stockée dans un cache mémoire. Ce paramètre global s’applique à tous les caches mémoire. Si une ressource est supérieure à cette valeur, elle n’est pas mise en cache dans la mémoire. La valeur par défaut est 1024 kilo-octets. Ce paramètre n’a aucune incidence sur le cache disque.

**Mise en cache des rendus de formulaire activée :** cette option est sélectionnée par défaut, ce qui signifie que les formulaires rendus sont mis en cache pour récupération ultérieure. Ce paramètre améliore les performances, car le service Forms ne doit effectuer le rendu d’un formulaire donné qu’une seule fois ; il utilise ensuite la version mise en cache. Cette option est associée à la propriété de mise en cache d’une conception de formulaire. Pour plus d’informations sur la configuration de cette valeur lors de la conception de formulaire, voir Aide de Designer.

### Mise en cache des conceptions de formulaire {#caching-form-designs}

Lorsque le service Forms reçoit une demande de rendu, il récupère la conception de formulaire dans le référentiel et la met en cache. Cette mise en cache améliore les performances, car le service Forms récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des requêtes de rendu ultérieures.

Le service Forms met toujours les conceptions de formulaire en cache sur le disque. Si les conceptions de formulaire sont stockées sur le serveur, ces fichiers sont considérés comme le cache disque. Le service Forms met également les conceptions de formulaire en cache dans la mémoire, en fonction du paramètre défini dans la zone **Mise en mémoire cache des modèles**. Si vous modifiez l’un de ces paramètres, redémarrez le service Forms pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou consultez la section [Démarrer ou arrêter les services associés aux modules AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille du cache de configuration des modèles :** nombre maximal d’objets de configuration de modèle à conserver en mémoire. La valeur par défaut est 100. Il est recommandé de la définir sur une valeur supérieure ou égale à celle de la Taille du cache des modèles. Ce paramètre n’a aucune incidence sur le cache disque.

**Taille du cache des modèles :** nombre maximal d’objets de contenu de modèle à conserver en mémoire. La valeur par défaut est 100. Ce paramètre n’a aucune incidence sur le cache disque.

**Activé :** cette case est cochée par défaut, ce qui signifie que les modèles de formulaire sont mis en mémoire cache. Si cette option n’est pas sélectionnée, les modèles de formulaire sont uniquement mis en cache sur le disque.

### Mise en cache des formulaires rendus {#caching-rendered-forms}

Le service Forms met les formulaires rendus en cache afin de ne pas devoir résoudre et effectuer le rendu du même formulaire lors de demandes ultérieures. Les formulaires rendus sont mis en cache sur le disque et dans la mémoire.

Ces paramètres se trouvent dans la zone **Mise en mémoire cache des rendus de formulaire**. Si vous modifiez l’un de ces paramètres, redémarrez le service Forms pour que la modification soit prise en compte. Pour redémarrer ce service, utilisez Workbench ou consultez la section [Démarrer ou arrêter les services associés aux modules AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille du cache :** détermine le nombre maximal de formulaires rendus pouvant se trouver dans le cache mémoire. La valeur par défaut est 100. Ce paramètre n’a aucune incidence sur le cache disque.

**Activé :** cette case est cochée par défaut, ce qui signifie que les formulaires rendus sont mis en mémoire cache. Si cette option n’est pas sélectionnée, les formulaires rendus sont uniquement mis en cache sur le disque.

### Mise en cache des fragments et images {#caching-fragments-and-images}

Le service Forms met en cache les fragments et les images utilisés dans les conceptions de formulaire sur le disque. Les performances sont améliorées, car les fragments et les images ne sont lus à partir du référentiel qu’à la première demande. Lors des demandes suivantes, le service Forms lit les fragments et les images à partir du cache disque. Les fragments et les images ne sont mis en cache que sur le disque, pas dans la mémoire.

Vous pouvez utiliser les paramètres suivants pour contrôler la mise en cache de fragments et d’images sur le disque. Ces paramètres se situent dans la zone **Paramètres du cache des ressources de modèle** :

**Caching de ressources** Sélectionnez l’une des options suivantes dans la liste :

**Activé pour les fragments et les images :** le service Forms met en cache les fragments et les images. Il s’agit de l’option par défaut.

**Activé pour les fragments :** le service Forms met en cache les fragments, mais pas les images.

**Désactivé :** le service Forms ne met ni les fragments, ni les images en cache.

**Intervalle de nettoyage (en secondes) :** il détermine la fréquence de suppression des anciens fichiers de cache non valides par le service Forms. Le service Forms ne supprime pas les fichiers de cache valides. Si vous modifiez l’intervalle de nettoyage, redémarrez le service Forms pour que ce changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou consultez la section Démarrage ou arrêt des services associés aux modules AEM Forms pour obtenir des instructions. La valeur par défaut est de 600 secondes.

## Remarques concernant la mise en cluster pour les caches {#clustering-considerations-for-caches}

Dans un environnement organisé en clusters, chaque nœud gère ses propres caches mémoire et disque. Le contenu du cache de chaque nœud dépend des formulaires rendus sur ce dernier.

L’emplacement du cache doit être identique (même disque et même chemin d’accès) pour chaque nœud du cluster. Ne placez pas le cache à un emplacement de stockage partagé.

Si vous utilisez la page Forms d’Administration Console pour modifier les paramètres de mise en cache d’un nœud particulier, les paramètres de mise en cache des autres nœuds sont mis à jour lorsqu’une demande atteint le nœud en question. Ce comportement s’applique également au bouton Réinitialiser le cache. Si vous cliquez sur le bouton Réinitialiser le cache pour un nœud, le cache est immédiatement supprimé de ce nœud. Le cache des autres nœuds est vidé lorsqu’une demande atteint le nœud en question.
