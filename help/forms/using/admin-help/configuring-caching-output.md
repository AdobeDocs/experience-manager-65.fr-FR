---
title: Configuration du cache pour Output
seo-title: Configuration du cache pour Output
description: Le service Output met en cache les conceptions de formulaire, les fragments et les images. Découvrez comment configurer la mise en cache pour la sortie.
seo-description: Le service Output met en cache les conceptions de formulaire, les fragments et les images. Découvrez comment configurer la mise en cache pour la sortie.
uuid: 00bffeb5-c9c4-4a46-98b5-e14ec9f4514e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5398abd-f62c-485d-9f4b-a316c0de2b6b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 89%

---


# Configuration du cache pour Output  {#configuring-caching-for-output}

Le service Output permet de fusionner des données de formulaire XML dans une conception de formulaire créée dans Designer pour produire un flux de sortie de documents dans différents formats.

La page Output d’Administration Console contient des paramètres contrôlant la méthode de mise en cache d’éléments par le service Output. Vous pouvez ajuster ces paramètres pour optimiser les performances du service Output.

Le service Output met en cache les éléments suivants :

* **conceptions de formulaire :** le service Output met en cache les conceptions de formulaire qu’il récupère du référentiel ou de sources HTTP. Cette mise en cache améliore les performances car le service Output récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des demandes de rendu ultérieures.
* **fragments et images :** le service Output peut mettre en cache les fragments et les images utilisés dans les conceptions de formulaire. Lorsque le service met en cache ces objets, il améliore les performances car les fragments et les images ne sont lus à partir du référentiel qu’à la première demande.

Le service Output stocke le cache à deux emplacements :

* **en mémoire :** les éléments sont stockés dans la mémoire pour un accès rapide. Le cache mémoire est limité en taille et supprimé au redémarrage du serveur.
* **sur le disque :** les éléments sont stockés dans le système de fichiers du serveur. Le cache disque est doté d’une plus grande capacité que le cache mémoire et il est conservé au redémarrage du serveur. L’emplacement du cache disque dépend du serveur d’applications. Pour plus d’informations sur la modification de l’emplacement du cache disque, voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Définition du mode de cache {#specifying-the-cache-mode}

Le service Output gère deux modes de mise en cache :

* sans condition ;
* en utilisant le point de contrôle du cache.

Si vous basculez entre les différents modes de mise en cache, redémarrez le service Output pour que ce changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou consultez la section [Démarrage ou arrêt des services associés aux modules AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

L’heure du point de contrôle du cache est automatiquement réinitialisée lors du basculement d’un mode à l’autre.

### Utilisation de la mise en cache sans condition  {#using-unconditional-caching}

Dans ce mode, lorsque le service Output reçoit une demande, il valide les ressources requises (conception de formulaire et tout actif lié comme les fragments et les images). Le service compare l’horodatage des ressources du référentiel à celui des ressources du cache. Si la ressource du cache est plus ancienne, le service la met à jour.

Ce mode de mise en cache garantit l’utilisation des ressources les plus récentes. Cependant, les performances sont affectées car le service Output valide les éléments mis en cache en les comparant à ceux du référentiel à chaque demande. Ce mode de mise en cache convient aux environnements de développement ou intermédiaires dans lesquels les ressources sont fréquemment mises à jour et pour lesquels les performances ne sont pas la priorité.

**Définition de la mise en cache sans condition**

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, sélectionnez Sans condition et cliquez sur Enregistrer.

### Utilisation du point de contrôle du cache  {#use-the-cache-check-point}

Lorsqu’il est dans ce mode, le service Output ne recherche les versions des ressources les plus récentes dans le référentiel que lorsque l’horodatage de la ressource mise en cache est plus ancien que l’heure du point de contrôle du cache. L’heure du point de contrôle du cache le plus récent s’affiche dans la page Output d’Administration Console.

Utilisez ce mode de cache dans des environnements de production hautes performances où les performances constituent une priorité et dans lesquels les ressources sont rarement modifiées. Vous pouvez réinitialiser l’heure du point de contrôle du cache lorsque vous souhaitez déployer les modifications apportées aux ressources du référentiel.

**Définition de l’utilisation d’un point de contrôle de cache**

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, sélectionnez Uniquement si la dernière validation est antérieure à l’heure du point de contrôle du cache et cliquez sur Enregistrer.

**Réinitialisation du point de contrôle du cache**

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, cliquez sur Point de contrôle du cache.

### Réinitialisation du contenu du cache  {#reset-the-cache-contents}

Vous pouvez vider le contenu du cache à tout moment. Après la réinitialisation du cache, la première demande est plus lente pour chaque formulaire, car le service Output effectue un rendu complet et crée un nouveau contenu de cache.

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres de contrôle du cache de sortie, sélectionnez Réinitialiser le cache.

## Configuration des paramètres du cache  {#configuring-cache-settings}

Vous pouvez spécifier les paramètres utilisés par le service Output pour la mise en cache, de façon à optimiser les performances de l’environnement AEM forms.

Pour accéder à ces paramètres, dans Administration Console, cliquez sur Services > Output.

>[!NOTE]
>
>la configuration requise sur le disque pour le cache est identique à celle du référentiel.

### Définition des paramètres du cache global  {#specifying-global-cache-settings}

Les paramètres de la zone **Paramètres du cache global** affectent tous les types de cache. Si vous modifiez l’un de ces paramètres, redémarrez le service Output pour que ce changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou consultez la section [Démarrage ou arrêt des services associés aux modules AEM forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille maximale du Document du cache (Ko) : taille maximale, en kilo-octets, d’une conception de formulaire ou d’une autre ressource pouvant être stockée dans n’importe quel cache mémoire.** Ce paramètre global s’applique à tous les caches mémoire. Si une ressource est supérieure à cette valeur, elle n’est pas mise en cache dans la mémoire. La valeur par défaut est 1024 kilo-octets. Ce paramètre n’a aucune incidence sur le cache disque.

**Mise en cache du rendu des formulaires activée :** par défaut, cette option est sélectionnée, ce qui signifie que les formulaires rendus sont mis en cache pour être récupérés ultérieurement. Ce paramètre a peu d’incidence sur les performances du service Output, car il ne met pas les documents non interactifs en cache. Cette option n’a aucune incidence lorsque vous utilisez le service Output avec des documents non interactifs rendus sur le client.

### Mise en cache des conceptions de formulaire  {#caching-form-designs}

Lorsque le service Output reçoit une demande de rendu, il récupère la conception de formulaire dans le référentiel ou à partir d’une source HTTP et la met en cache. Cette mise en cache améliore les performances car le service Output récupère la conception de formulaire à partir du cache et non plus à partir du référentiel lors des demandes de rendu ultérieures.

Le service Output met toujours les conceptions de formulaire en cache sur le disque. Si les conceptions de formulaire sont stockées sur le serveur, ces fichiers sont considérés comme le cache disque. Le service Output met également les conceptions de formulaire en cache dans la mémoire, en fonction du paramètre défini dans la zone **Mise en mémoire cache des modèles**. Si vous modifiez l’un de ces paramètres, redémarrez le service pour que ce changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou consultez la section [Démarrage ou arrêt des services associés aux modules AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) pour obtenir des instructions.

**Taille du cache de configuration de modèle :** nombre maximal d’objets de configuration de modèle à conserver en mémoire. La valeur par défaut est 100. Il est recommandé de la définir sur une valeur supérieure ou égale à celle de la Taille du cache des modèles. Ce paramètre n’a aucune incidence sur le cache disque.

**Taille du cache des modèles :** nombre maximal d’objets de contenu de modèle à conserver en mémoire. La valeur par défaut est 100. Ce paramètre n’a aucune incidence sur le cache disque.

**Activé :** cette case à cocher est activée par défaut, ce qui signifie que les modèles de formulaire sont mis en cache en mémoire. Si cette option n’est pas sélectionnée, les modèles de formulaire sont uniquement mis en cache sur le disque.

### Mise en cache des fragments et images  {#caching-fragments-and-images}

Le service Output met en cache les fragments et les images utilisés dans les conceptions de formulaire sur le disque. Cela améliore les performances car les fragments et les images ne sont lus à partir du référentiel qu’à la première demande. Lors des demandes suivantes, le service Output lit les fragments et les images à partir du cache disque. Les fragments et les images ne sont mis en cache que sur le disque, pas dans la mémoire.

Vous pouvez utiliser les paramètres suivants pour contrôler la mise en cache de fragments et d’images sur le disque. Ces paramètres se situent dans la zone **Paramètres du cache des ressources de modèle** :

**Mise en** cache des ressourcesSélectionnez l&#39;une des options suivantes dans la liste :

**Activé pour les fragments et les images :** le service Output met en cache les fragments et les images. Il s’agit de l’option par défaut.

**Activé pour les fragments :** le service Output met en cache les fragments, mais pas les images.

**Désactivé :** le service Output ne met pas en cache les fragments ou les images.

**Intervalle de nettoyage (secondes) :** indique la fréquence à laquelle le service Output supprime les anciens fichiers de cache non valides. Le service ne supprime pas les fichiers cache valides. Si vous modifiez l’intervalle de nettoyage, redémarrez le service Output pour que ce changement soit appliqué. Pour redémarrer ce service, utilisez Workbench ou consultez la section Démarrage ou arrêt des services associés aux modules AEM Forms pour obtenir des instructions.

## Remarques concernant la mise en grappe pour les caches {#clustering-considerations-for-caches}

Dans un environnement organisé en grappe, chaque nœud gère ses propres caches mémoire et disque. Le contenu du cache de chaque nœud dépend des formulaires rendus sur ce dernier.

L’emplacement du cache doit être identique (même disque et chemin d’accès) pour chaque nœud de la grappe. Ne placez pas le cache à un emplacement de stockage partagé.

Si vous utilisez la page Output d’Administration Console pour modifier les paramètres de mise en cache d’un nœud particulier, les paramètres de mise en cache des autres nœuds sont mis à jour lorsqu’une demande atteint le nœud en question. Ce comportement s’applique également au bouton Réinitialiser le cache. Si vous cliquez sur le bouton Réinitialiser le cache pour un nœud, le cache est immédiatement supprimé de ce nœud. Le cache des autres nœuds est vidé lorsqu’une demande atteint le nœud en question.
