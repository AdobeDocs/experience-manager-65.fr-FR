---
title: Personnaliser les pages affichées par le gestionnaire d’erreurs
description: Adobe Experience Manager est fourni avec un gestionnaire d’erreurs standard pour gérer les erreurs HTTP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 100%

---

# Personnaliser les pages affichées par le gestionnaire d’erreurs{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager (AEM) s’accompagne d’un outil standard destiné à la gestion des erreurs HTTP, en affichant par exemple :

![chlimage_1-67](assets/chlimage_1-67a.png)

Les scripts fournis par le système existent (sous `/libs/sling/servlet/errorhandler`) pour répondre aux codes d’erreur. Par défaut, les fichiers suivants sont disponibles avec une instance CQ standard :

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM est basé sur Apache Sling. En tant que tel, consultez [Gestion des erreurs](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html) pour plus d’informations sur la gestion des erreurs Sling.

>[!NOTE]
>
>Sur une instance de création, le [filtre de débogage de la gestion du contenu web CQ](/help/sites-deploying/osgi-configuration-settings.md) est activé par défaut. Le code de réponse est toujours 200. Le gestionnaire d’erreurs par défaut répond en écrivant la trace de la pile complète à la réponse.
>
>Sur une instance de publication, le filtre de débogage de la gestion du contenu web CQ est *toujours* désactivé (même s’il est configuré comme étant activé).

## Méthode de personnalisation des pages affichées par le gestionnaire d’erreurs {#how-to-customize-pages-shown-by-the-error-handler}

Vous pouvez développer vos propres scripts afin de personnaliser les pages affichées par le gestionnaire d’erreurs lors de la détection d’une erreur. Vos pages personnalisées sont créées sous `/apps` et se superposent aux pages par défaut (qui se trouvent sous `/libs`).

>[!NOTE]
>
>Voir [Utilisation des recouvrements](/help/sites-developing/overlays.md) pour plus d’informations.

1. Dans le référentiel, copiez le ou les scripts par défaut :

   * de `/libs/sling/servlet/errorhandler/`
   * vers `/apps/sling/servlet/errorhandler/`

   Puisque le chemin de destination n’existe pas par défaut, vous devez le créer lorsque vous effectuez cette opération pour la première fois.

1. Accédez à `/apps/sling/servlet/errorhandler` et effectuez l’une des opérations suivantes :

   * Modifier le script existant approprié pour fournir les informations requises.
   * Créer un script, et le modifier, pour le code requis

1. Enregistrez les modifications et effectuez un test.

>[!CAUTION]
>
>Les gestionnaires 404.jsp et 403.jsp ont été conçus pour prendre en charge l&#39;authentification CQ5, notamment pour permettre la connexion au système en cas d&#39;erreur.
>
>Le remplacement de ces deux gestionnaires doit être effectué avec précaution.

### Personnalisation de la réponse aux erreurs HTTP 500 {#customizing-the-response-to-http-errors}

Les erreurs HTTP 500 sont dues à des exceptions côté serveur.

* **[500 : Erreur de serveur interne](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
Le serveur a rencontré une condition inattendue qui l’a empêché de satisfaire la demande.

Lorsque le traitement des demandes provoque une exception, le framework Apache Sling (sur laquelle CQ est basé) :

* consigne l’exception
* renvoie :

   * le code de réponse HTTP 500
   * la trace de la pile d’exception

  dans le corps de la réponse.

La [personnalisation des pages affichées par le gestionnaire d’erreurs](#how-to-customize-pages-shown-by-the-error-handler) permet de créer un script `500.jsp`. Cependant, il n’est utilisé que si `HttpServletResponse.sendError(500)` est exécuté de manière explicite ; c’est-à-dire à partir d’un détecteur d’exceptions.

Dans le cas contraire, le code de réponse est défini sur 500, mais le script `500.jsp` n’est pas exécuté.

Pour gérer les erreurs de type 500, le nom de fichier du script de gestionnaire d’erreurs doit être identique à la classe d’exception (ou superclasse). Pour gérer toutes ces exceptions, vous pouvez créer un script `/apps/sling/servlet/errorhandler/Throwable.js`p ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Sur une instance de création, le [filtre de débogage de la gestion du contenu web CQ](/help/sites-deploying/osgi-configuration-settings.md) est activé par défaut. Le code de réponse est toujours 200. Le gestionnaire d’erreurs par défaut répond en écrivant la trace de la pile complète à la réponse.
>
>Des réponses avec le code 500 sont nécessaires pour un gestionnaire d’erreurs personnalisé. Par conséquent, le [filtre de débogage de la gestion du contenu web CQ doit être désactivé](/help/sites-deploying/osgi-configuration-settings.md). Cela garantit le renvoi du code de réponse 500 qui, à son tour, déclenche le gestionnaire d’erreurs Sling approprié.
>
>Sur une instance de publication, le filtre de débogage de la gestion du contenu web CQ est *toujours* désactivé (même s’il est configuré comme étant activé).
