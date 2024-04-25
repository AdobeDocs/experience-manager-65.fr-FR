---
title: Expiration des objets statiques
description: Découvrez comment configurer Adobe Experience Manager pour que les objets statiques n’expirent pas (pendant une durée raisonnable).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 100%

---

# Expiration des objets statiques{#expiration-of-static-objects}

Les objets statiques (par exemple, les icônes) ne changent pas. Par conséquent, le système doit être configuré de manière à ce qu’ils n’expirent pas (pendant une période raisonnable) et ainsi réduire le trafic inutile.

Cela a les effets suivants :

* Décharge les requêtes de l’infrastructure du serveur.
* Augmente les performances du chargement des pages, car le navigateur met en cache les objets dans la mémoire cache du navigateur.

Les expirations sont spécifiées par la norme HTTP concernant « l’expiration » des fichiers (voir, par exemple, le chapitre 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) « Hypertext Transfer Protocol - HTTP 1.1 »). Cette norme utilise l’en-tête pour permettre aux clients de mettre en cache des objets jusqu’à ce qu’ils soient considérés comme périmés ; ces objets sont mis en cache pendant la durée spécifiée sans qu’aucun contrôle de statut ne soit effectué sur le serveur d’origine.

>[!NOTE]
>
>Cette configuration est distincte de Dispatcher (et ne fonctionne pas pour lui).
>
>Dispatcher a pour objectif de mettre les données en cache en amont d’Adobe Experience Manager (AEM).

Tous les fichiers, qui ne sont pas dynamiques et qui ne changent pas au fil du temps, peuvent et doivent être mis en cache. La configuration du serveur Apache HTTPD peut ressembler à ce qui suit, selon l’environnement :

>[!CAUTION]
>
>Faites attention lorsque vous définissez la durée pendant laquelle un objet est considéré comme étant à jour. Comme il n’y a *pas de vérification tant que la durée spécifiée n’a pas expiré*, le client peut finir par présenter de l’ancien contenu à partir du cache.

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

   Cela permet au cache intermédiaire (par exemple, la mémoire cache du navigateur) de stocker des fichiers CSS, JavaScript, PNG et GIF pendant un mois au maximum, jusqu’à leur expiration. Cela signifie qu’ils n’ont pas besoin d’être demandés à AEM ou au serveur web, mais peuvent rester dans la mémoire cache du navigateur.

   Les autres sections du site ne doivent pas être mises en cache sur une instance de création, car elles peuvent être modifiées à tout moment.

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

   Cela permet au cache intermédiaire (par exemple la mémoire cache du navigateur) de stocker des fichiers CSS, JavaScript, PNG et GIF pendant un jour au maximum dans les caches clients. Bien que cet exemple illustre les paramètres globaux pour tout ce qui se situe sous `/content` et `/etc/designs`, vous devriez les rendre plus granulaires.

   Selon la fréquence de mise à jour de votre site, vous pouvez également envisager de mettre en cache les pages HTML. Une heure constitue une durée raisonnable :

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Après avoir configuré les objets statiques, parcourez `request.log`, tout en sélectionnant les pages qui contiennent de tels objets, pour confirmer qu’aucune demande (inutile) n’est faite pour les objets statiques.
