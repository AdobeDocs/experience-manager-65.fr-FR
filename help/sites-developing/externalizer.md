---
title: Externalisation d’URL
seo-title: Externalizing URLs
description: Externalizer est un service OSGI qui vous permet de transformer, par programmation, un chemin d’accès à une ressource en URL absolue externe.
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 78%

---

# Externalisation d’URL{#externalizing-urls}

Dans AEM, la variable **Externalizer** est un service OSGI qui vous permet de transformer par programmation un chemin d’accès aux ressources (par exemple, `/path/to/my/page`) dans une URL externe et absolue (par exemple, `https://www.mycompany.com/path/to/my/page`) en ajoutant un préfixe au chemin d’accès avec un DNS préconfiguré.

Une instance ne peut pas connaître son URL visible en externe si elle s’exécute derrière une couche Web et il arrive qu’un lien doive être créé en dehors d’une étendue de demande. Dès lors, ce service fournit un emplacement centralisé pour configurer ces URL externes et les générer.

Cette page explique comment configurer la variable **Externalizer** et comment l’utiliser. Pour plus d’informations, reportez-vous à la section [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Configuration du service Externalizer {#configuring-the-externalizer-service}

Le service **Externalizer** vous permet de définir, de manière centralisée, plusieurs domaines pouvant être utilisés pour préfixer des chemins d’accès aux ressources par programmation. Chaque domaine est identifié par un nom unique utilisé pour référencer le domaine par programmation.

Pour définir un mappage de domaine pour la variable **Externalizer** service :

1. Accédez au gestionnaire de configuration via **Outils**, puis **Console Web**, ou saisissez :

   `https://<host>:<port>/system/console/configMgr`

1. Cliquez sur l’**Externaliseur de lien Day CQ** pour ouvrir la boîte de dialogue de configuration.

   >[!NOTE]
   >
   >Le lien direct vers la configuration est `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`.

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Définit un mappage de **domaines** : un mappage correspond à un nom unique (qui peut être utilisé dans le code pour référencer le domaine) d’un espace et du domaine :

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Où :

   * Le **schéma** est généralement http ou https ; cependant, il peut également s’agir de ftp, entre autres.

      * Utilisez le https pour appliquer des liens https, le cas échéant.
      * Il sera utilisé si le code client ne remplace pas le schéma lors de la demande d’externalisation d’une URL.

   * **Server** est le nom d’hôte (il peut s’agir d’un nom de domaine ou d’une adresse IP).
   * **Port** (facultatif) est le numéro de port.
   * **contextpath** (facultatif) est défini uniquement si AEM est installé en tant qu’application Web sous un autre chemin d’accès au contexte.

   Par exemple : `production https://my.production.instance`

   Les noms de mappage suivants sont prédéfinis et doivent toujours être configurés, car AEM en dépend :

   * `local` : instance locale
   * `author` : DNS du système de création
   * `publish` : DNS du site public

   >[!NOTE]
   >
   >Une configuration personnalisée vous permet d’ajouter une nouvelle catégorie, telle que `production`, `staging` ou même des systèmes externes non AEM tels que `my-internal-webservice`. Il est utile d’éviter de coder en dur de telles URL à différents endroits dans le code de base d’un projet.

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

>[!NOTE]
>
>Adobe vous recommande d’[ajouter la configuration au référentiel](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Utilisation du service Externalizer {#using-the-externalizer-service}

Cette section illustre quelques exemples d’utilisation du service **Externalizer :**

1. **Pour obtenir le service Externalizer dans un JSP :**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Pour externaliser un chemin d’accès avec le domaine « publish » :**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   En prenant le mappage de domaine :

   * `publish https://www.website.com`

   `myExternalizedUrl` se termine par la valeur :

   * `https://www.website.com/contextpath/my/page.html`

1. **Pour externaliser un chemin d’accès avec le domaine « author » :**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   En prenant le mappage de domaine :

   * `author https://author.website.com`

   `myExternalizedUrl` se termine par la valeur :

   * `https://author.website.com/contextpath/my/page.html`

1. **Pour externaliser un chemin d’accès avec le domaine « local », procédez comme suit :**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   En prenant le mappage de domaine :

   * `local https://publish-3.internal`

   `myExternalizedUrl` se termine par la valeur :

   * `https://publish-3.internal/contextpath/my/page.html`

1. Vous trouverez d’autres exemples dans les [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
