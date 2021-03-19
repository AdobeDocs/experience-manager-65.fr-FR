---
title: Expiration des objets statiques
seo-title: Expiration des objets statiques
description: Découvrez comment configurer AEM pour que les objets statiques n’expirent pas (pendant un intervalle de temps raisonnable).
seo-description: Découvrez comment configurer AEM pour que les objets statiques n’expirent pas (pendant un intervalle de temps raisonnable).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuration
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 95%

---


# Expiration des objets statiques{#expiration-of-static-objects}

Les objets statiques (par exemple, les icônes) ne changent pas. Par conséquent, le système devrait être configuré de façon à ce qu’elles n’expirent pas (pendant une période raisonnable) de façon à réduire le trafic inutile.

Cela se répercute de la manière suivante :

* Décharge les demandes de l’infrastructure du serveur.
* Augmente les performances de chargement des pages dans la mesure où le navigateur met en cache les objets dans le cache du navigateur.

Les expirations sont spécifiées par la norme HTTP concernant « l’expiration » des fichiers (voir, par exemple, Chapitre 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) « Hypertext Transfer Protocol - HTTP 1.1 »). Cette norme utilise l’en-tête pour permettre aux clients de mettre en cache des objets jusqu’à ce qu’ils soient considérés comme périmés ; ces objets sont mis en cache pendant la durée spécifiée sans qu’aucun contrôle d’état ne soit effectué sur le serveur d’origine.

>[!NOTE]
>
>Cette configuration est complètement distincte du dispatcher (et ne fonctionnera pas pour lui).
>
>Le dispatcher a pour objectif de mettre les données en mémoire cache en amont d’AEM.

Tous les fichiers, qui ne sont pas dynamiques et qui ne changent pas au fil du temps, peuvent et doivent être mis en cache. La configuration du serveur HTTPD Apache peut ressembler à l’une des suivantes, selon l’environnement :

>[!CAUTION]
>
>Soyez prudent lorsque vous définissez la période pendant laquelle un objet est considéré comme étant à jour. Dans la mesure où il n’y a *pas de vérification tant que la période spécifiée n’a pas expiré*, le client peut finir par présenter du contenu ancien à partir du cache.

1. **Pour une instance d’auteur :**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Cela permet au cache intermédiaire (par exemple le cache du navigateur) de stocker des fichiers CSS, Javascript, PNG et GIF pendant un mois au maximum, jusqu’à leur expiration. Cela signifie qu’il est inutile de les demander à AEM ou au serveur web, mais qu’ils peuvent rester dans le cache du navigateur.

   Les autres sections du site ne doivent pas être mises en cache sur une instance d’auteur, car elles peuvent être modifiées à tout moment.

1. **Pour une instance de publication :**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   Cela permet au cache intermédiaire (par exemple le cache du navigateur) de stocker des fichiers CSS, Javascript, PNG et GIF pendant un jour au maximum dans les caches clients. Bien que cet exemple illustre les paramètres globaux pour tout ce qui se trouve en dessous de `/content` et `/etc/designs`, vous devez le rendre plus granulaire.

   Selon la fréquence de mise à jour de votre site, vous pouvez également envisager de mettre en cache les pages HTML. Un intervalle de temps raisonnable serait d’une heure :

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Après avoir configuré les objets statiques, parcourez `request.log`, tout en sélectionnant les pages qui contiennent de tels objets, pour confirmer qu’aucune demande (inutile) n’est faite pour les objets statiques.
