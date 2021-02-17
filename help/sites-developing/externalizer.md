---
title: Externalisation d’URL
seo-title: Externalisation d’URL
description: Externalizer est un service OSGI qui vous permet de transformer, par programmation, un chemin d’accès aux ressources en une URL externe et absolue.
seo-description: Externalizer est un service OSGI qui vous permet de transformer, par programmation, un chemin d’accès aux ressources en une URL externe et absolue.
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 36%

---


# Externalisation d’URL{#externalizing-urls}

En AEM, le **Externalizer** est un service OSGI qui vous permet de transformer par programmation un chemin de ressources (ex. `/path/to/my/page`) dans une URL externe et absolue (par exemple, `https://www.mycompany.com/path/to/my/page`) en préfixant le chemin d’accès avec un DNS préconfiguré.

Comme une instance ne peut pas connaître son URL visible en externe si elle s’exécute derrière une couche Web et qu’il est parfois nécessaire de créer un lien en dehors de l’étendue de la requête, ce service fournit un emplacement central pour configurer ces URL externes et les créer.

Cette page explique comment configurer le service **Externalizer** et l’utiliser. Pour plus d’informations, reportez-vous aux [JavaDocs](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Configuration du service Externalizer {#configuring-the-externalizer-service}

Le service **Externalizer** vous permet de définir de manière centralisée plusieurs domaines qui peuvent être utilisés pour préfixer par programmation les chemins de ressources. Chaque domaine est identifié par un nom unique utilisé pour faire référence au domaine par programmation.

Pour définir un mappage de domaine pour le service **Externalizer**, procédez comme suit :

1. Accédez au gestionnaire de configuration par **Outils**, puis **Console Web**, ou saisissez :

   `https://<host>:<port>/system/console/configMgr`

1. Cliquez sur **Externalisateur de liens Day CQ** pour ouvrir la boîte de dialogue de configuration.

   >[!NOTE]
   >
   >Le lien direct vers la configuration est `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Définissez un mappage **Domains** : un mappage consiste en un nom unique qui peut être utilisé dans le code pour référencer le domaine, un espace et le domaine :

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Où :

   * **** les schémas sont généralement http ou https, mais peuvent également être ftp, etc.

      * utiliser https pour appliquer les liens https, si nécessaire
      * il sera utilisé si le code client ne remplace pas le schéma lors de la demande d’externalisation d’une URL.
   * **Le** serveur est le nom d’hôte (peut être un nom de domaine ou une adresse ip).
   * **port**  (facultatif) est le numéro de port.
   * **contextpath** (facultatif) n’est défini que si AEM est installé en tant qu’application web sous un chemin de contexte différent.

   Par exemple : `production https://my.production.instance`

   Les noms de mappage suivants sont prédéfinis et doivent toujours être définis en fonction de leur utilisation AEM :

   * `local` - l&#39;instance locale
   * `author` - le DNS du système de création
   * `publish` - DNS du site Web destiné au public

   >[!NOTE]
   >
   >Une configuration personnalisée vous permet d’ajouter une nouvelle catégorie, telle que `production`, `staging` ou même des systèmes externes non AEM tels que `my-internal-webservice`. Il est utile d’éviter de figer de telles URL à différents emplacements de la base de code d’un projet.

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

>[!NOTE]
>
>L&#39;Adobe vous recommande [d&#39;ajouter la configuration au référentiel](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Utilisation du service Externalizer {#using-the-externalizer-service}

Cette section illustre quelques exemples d’utilisation du service **Externalizer:**

1. **Pour obtenir le service Externalizer dans un JSP :**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Pour externaliser un chemin d’accès avec le domaine « publish » :**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   En supposant le mappage de domaines :

   * `publish https://www.website.com`

   `myExternalizedUrl` se termine par la valeur :

   * `https://www.website.com/contextpath/my/page.html`


1. **Pour externaliser un chemin d’accès avec le domaine « author » :**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   En supposant le mappage de domaines :

   * `author https://author.website.com`

   `myExternalizedUrl` se termine par la valeur :

   * `https://author.website.com/contextpath/my/page.html`


1. **Pour externaliser un chemin d’accès avec le domaine « local », procédez comme suit :**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   En supposant le mappage de domaines :

   * `local https://publish-3.internal`

   `myExternalizedUrl` se termine par la valeur :

   * `https://publish-3.internal/contextpath/my/page.html`


1. Vous trouverez d’autres exemples dans les [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
