---
title: Personnalisation des pages affichées par le gestionnaire d’erreurs
seo-title: Personnalisation des pages affichées par le gestionnaire d’erreurs
description: AEM s’accompagne d’un outil standard destiné à la gestion des erreurs HTTP.
seo-description: AEM s’accompagne d’un outil standard destiné à la gestion des erreurs HTTP.
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 83%

---


# Personnalisation des pages affichées par le gestionnaire d’erreurs{#customizing-pages-shown-by-the-error-handler}

AEM s’accompagne d’un outil standard destiné à la gestion des erreurs HTTP, en affichant, par exemple :

![chlimage_1-67](assets/chlimage_1-67a.png)

Il existe des scripts fournis par le système (sous `/libs/sling/servlet/errorhandler`) pour répondre aux codes d’erreur. Par défaut, les éléments suivants sont disponibles avec une instance CQ standard :

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM est basé sur Apache Sling. Pour plus d’informations sur la gestion des erreurs Sling, voir [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html).

>[!NOTE]
>
>Sur une instance de création, le [filtre de débogage de la gestion du contenu web CQ](/help/sites-deploying/osgi-configuration-settings.md) est activé par défaut. Cela donne toujours comme résultat le code de réponse 200. Le gestionnaire d’erreurs par défaut répond en écrivant la trace de pile complète sur la réponse.
>
>Sur une instance de publication, le filtre de débogage de la gestion du contenu web CQ est *toujours* désactivé (même s’il est configuré comme étant activé).

## Méthode de personnalisation des pages affichées par le gestionnaire d’erreurs {#how-to-customize-pages-shown-by-the-error-handler}

Vous pouvez développer vos propres scripts afin de personnaliser les pages affichées par le gestionnaire d’erreurs lors de la détection d’une erreur. Vos pages personnalisées seront créées sous `/apps` et superposeront les pages par défaut (sous `/libs`).

>[!NOTE]
>
>Pour plus d’informations, voir [Utilisation de recouvrements](/help/sites-developing/overlays.md).

1. Dans le référentiel, copiez le ou les scripts par défaut :

   * de `/libs/sling/servlet/errorhandler/`
   * vers `/apps/sling/servlet/errorhandler/`

   Puisque le chemin de destination n’existe pas par défaut, vous devez le créer lorsque vous effectuez cette opération pour la première fois.

1. Accédez à `/apps/sling/servlet/errorhandler`. Ici, vous pouvez effectuer l’une des opérations suivantes :

   * Modifier le script existant approprié pour fournir les informations requises 
   * Créer un script, et le modifier, pour le code requis

1. Enregistrez les modifications et effectuez un test.

>[!CAUTION]
>
>Les gestionnaires 404.jsp et 403.jsp ont été spécialement conçus pour prendre en compte l’authentification CQ5 ; en particulier, pour permettre une connexion système si ces erreurs se produisent.
>
>Par conséquent, le remplacement de ces deux gestionnaires doit être effectué avec précaution.

### Personnalisation de la réponse aux erreurs HTTP 500 {#customizing-the-response-to-http-errors}

Les erreurs HTTP 500 sont dues à des exceptions côté serveur.

* **[500 : erreur de serveur interne](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) Le serveur a rencontré une condition inattendue qui l’a empêché de satisfaire la demande.**

Lorsque le traitement des requêtes génère une exception, la structure Apache Sling (sur laquelle l’AEM est créée) :

* consigne l’exception ;
* renvoie :

   * le code de réponse HTTP 500
   * la trace de la pile d’exception

   dans le corps de la réponse.

La [personnalisation des pages affichées par le gestionnaire d’erreurs](#how-to-customize-pages-shown-by-the-error-handler) permet de créer un script `500.jsp`. Cependant, il n’est utilisé que si `HttpServletResponse.sendError(500)` est exécuté de manière explicite ; c’est-à-dire à partir d’un détecteur d’exceptions.

Dans le cas contraire, le code de réponse est défini sur 500, mais le script `500.jsp` n’est pas exécuté.

Pour gérer les erreurs de type 500, le nom de fichier du script de gestionnaire d’erreurs doit être identique à la classe d’exception (ou superclasse). Pour gérer toutes ces exceptions, vous pouvez créer un script `/apps/sling/servlet/errorhandler/Throwable.js`p ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Sur une instance de création, le [filtre de débogage de la gestion du contenu web CQ](/help/sites-deploying/osgi-configuration-settings.md) est activé par défaut. Cela donne toujours comme résultat le code de réponse 200. Le gestionnaire d’erreurs par défaut répond en écrivant la trace de pile complète sur la réponse.
>
>Des réponses avec le code 500 sont nécessaires pour un gestionnaire d’erreurs personnalisé. Par conséquent, le [filtre de débogage de la gestion du contenu web CQ doit être désactivé](/help/sites-deploying/osgi-configuration-settings.md). Cela garantit le renvoi du code de réponse 500 qui, à son tour, déclenche le gestionnaire d’erreurs Sling approprié.
>
>Sur une instance de publication, le filtre de débogage de la gestion du contenu web CQ est *toujours* désactivé (même s’il est configuré comme étant activé).

