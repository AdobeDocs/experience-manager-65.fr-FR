---
title: Mise en cache et performances
description: Découvrez les différentes configurations disponibles pour activer GraphQL et la mise en cache de contenu afin d’optimiser les performances de votre implémentation commerciale.
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 73%

---

# Mise en cache et performances {#caching}

## Mise en cache des réponses des composants et de GraphQL {#graphql}

Les composants principaux AEM CIF prennent déjà en charge la mise en cache des réponses GraphQL pour les composants individuels. Cette fonctionnalité peut être utilisée pour réduire considérablement le nombre d’appels d’arrière-plan GraphQL. Une mise en cache efficace peut être réalisée, en particulier pour les requêtes qui se répètent, comme la récupération de l’arborescence des catégories pour un composant de navigation ou la récupération de toutes les valeurs d’agrégations/de facettes disponibles affichées sur les pages de recherche de produits et de catégories.

Pour les composants principaux AEM CIF, la mise en cache étant configurée composant par composant, il est possible de contrôler si (et pendant combien de temps) les requêtes/réponses GraphQL sont mises en cache pour chaque composant. Il est également possible de définir le comportement de mise en cache des services OSGi à l’aide du client GraphQL.

### Configuration

Une fois configuré pour un composant donné, le cache commence à stocker les requêtes et les réponses GraphQL telles que définies par chaque entrée de configuration du cache. La taille du cache et la durée de mise en cache de chaque entrée doivent être définies projet par projet, en fonction, par exemple, de la fréquence à laquelle les données du catalogue peuvent changer, de l’importance cruciale qu’un composant affiche toujours les dernières données possibles, etc. Notez qu’il n’y a pas d’invalidation du cache. Soyez donc prudent lors de la définition des durées du cache.

Lors de la configuration de la mise en cache des composants, le nom du cache doit correspondre au nom des composants **proxy** que vous définissez dans votre projet.

Avant d’envoyer une requête GraphQL, le client vérifie que la même requête GraphQL **exacte** est déjà mise en cache et renvoie éventuellement la réponse mise en cache. Pour qu’il y ait une correspondance, la requête GraphQL DOIT correspondre exactement : en d’autres termes, la requête, le nom de l’opération (le cas échéant) et les variables (le cas échéant) DOIVENT tous être identiques à la requête mise en cache, et tous les en-têtes HTTP personnalisés susceptibles d’être définis DOIVENT également être identiques. Par exemple, l’en-tête `Store` Magento DOIT correspondre.

### Exemples

Nous vous recommandons de configurer une certaine mise en cache pour le service de recherche qui récupère toutes les valeurs d’agrégations/de facettes disponibles affichées sur les pages de recherche de produits et de catégories. Ces valeurs ne changent généralement que lorsqu’un nouvel attribut est par exemple ajouté à des produits. Par conséquent, la durée de cette entrée de cache peut être « importante » si l’ensemble d’attributs de produit ne change pas souvent. Bien que cela soit spécifique au projet, nous recommandons des valeurs de quelques minutes dans les phases de développement du projet et de quelques heures sur des systèmes de production stables.

Ces valeurs sont généralement configurées avec l’entrée de cache suivante :

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Un autre exemple de scénario où la fonction de mise en cache GraphQl est recommandée réside dans le composant de navigation, car celui-ci envoie la même requête GraphQL sur toutes les pages. Dans ce cas, l’entrée de cache est généralement définie sur :

```
venia/components/structure/navigation:true:10:600
```

Lorsque vous considérez le [magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia) est utilisé. Notez l’utilisation du nom du proxy de composant `venia/components/structure/navigation`, et **non pas** le nom du composant de navigation CIF (`core/cif/components/structure/navigation/v1/navigation`).

La mise en cache d’autres composants doit être définie projet par projet, généralement en coordination avec la mise en cache configurée au niveau du Dispatcher. N’oubliez pas qu’il n’y a pas d’invalidation active de ces caches. Par conséquent, la durée de mise en cache doit être soigneusement définie. Il n’existe aucune valeur « universelle » qui correspondrait à tous les projets et cas d’utilisation possibles. Assurez-vous de définir une stratégie de mise en cache au niveau du projet qui correspond au mieux aux exigences de votre projet.

## Mise en cache de Dispatcher {#dispatcher}

La mise en cache de pages ou de fragments AEM dans le [Dispatcher AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) constitue une bonne pratique pour un projet AEM. En règle générale, elle repose sur des techniques d’invalidation qui garantissent qu’un contenu modifié dans AEM est correctement mis à jour dans le Dispatcher. Il s’agit d’une fonctionnalité essentielle de la stratégie de mise en cache du Dispatcher AEM.

Outre le CIF du contenu géré par AEM pur, une page peut généralement afficher des données commerciales récupérées dynamiquement à partir de Magento via GraphQL. Bien que la structure de la page elle-même puisse ne jamais changer, le contenu commercial peut changer, par exemple, si certaines données de produit (telles que le nom ou le prix) changent dans Magento.

Pour vous assurer que les pages CIF peuvent être mises en cache pendant une durée limitée dans AEM Dispatcher, nous vous recommandons donc d’utiliser l’[invalidation du cache basée sur le temps](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl) (également appelée mise en cache basée sur TTL) lors de la mise en cache de pages CIF dans AEM Dispatcher. Cette fonctionnalité peut être configurée en AEM avec le package [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) supplémentaire.

Avec la mise en cache TTL, un développeur définit généralement une ou plusieurs durées de mise en cache pour les pages AEM sélectionnées. Cela garantit que les pages CIF sont uniquement mises en cache dans le Dispatcher AEM jusqu’à la durée configurée et que le contenu sera fréquemment mis à jour.

>[!NOTE]
>
>Bien que les données côté serveur puissent être mises en cache par AEM Dispatcher, certains composants CIF tels que les composants `product`, `productlist` et `searchresults` récupèrent généralement les prix des produits dans une requête de navigateur côté client lorsque la page est chargée. Ainsi, le contenu dynamique crucial est toujours récupéré au chargement de la page.

## Ressources supplémentaires

- [Magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Configuration de la mise en cache GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
