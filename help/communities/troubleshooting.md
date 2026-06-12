---
title: Résolution des problèmes de la communauté
description: Découvrez comment résoudre les problèmes de la communauté, y compris les problèmes connus et les préoccupations.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Résolution des problèmes de la communauté {#troubleshooting}

Cette section contient des préoccupations courantes et des problèmes connus lors du dépannage de la communauté .

## Problèmes connus {#known-issues}

### Échec de la récupération de Dispatcher {#dispatcher-refetch-fails}

Lors de l’utilisation de Dispatcher 4.1.5 avec une version plus récente de Jetty, une récupération peut entraîner l’échec de la réception de la réponse du serveur distant après l’expiration du délai de la requête.

L’utilisation de Dispatcher version 4.1.6 ou ultérieure résout ce problème.

### Impossible d’accéder à la publication du forum après la mise à niveau à partir de CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Si un forum a été créé sur CQ 5.4 et que des rubriques ont été publiées, puis que le site a été mis à niveau vers AEM 5.6.1 ou une version ultérieure, toute tentative d’affichage des publications existantes peut entraîner une erreur sur la page :

Caractère de modèle &#39;a&#39; non conforme
Impossible de traiter la demande à `/content/demoforums/forum-test.html` sur ce serveur. Les journaux contiennent les éléments suivants :

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

Le problème est que la chaîne de format de com.day.cq.commons.date.RelativeTimeFormat a été modifiée entre 5.4 et 5.5, de sorte que le « a » pour « ago » n’est plus accepté.

Ainsi, tout code utilisant l’API RelativeTimeFormat() doit changer :

* De : `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* A : `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

L’échec est différent sur les instances de création et de publication. En mode de création, il échoue silencieusement et n’affiche tout simplement pas les rubriques du forum. Lors de la publication, l’erreur s’affiche sur la page.

Voir l’API [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) pour plus d’informations.

## Préoccupations courantes {#common-concerns}

### Avertissement dans les journaux : Handlebars obsolètes {#warning-in-logs-handlebars-deprecated}

Au démarrage (pas le premier, mais tous les suivants), l’avertissement suivant peut s’afficher dans les journaux :

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` a été remplacé par `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Cet avertissement peut être ignoré en toute sécurité, car `jknack.handlebars.Handlebars`, utilisé par [SCF](scf.md#handlebarsjavascripttemplatinglanguage), est fourni avec son propre utilitaire d&#39;assistance i18n. Au démarrage, il est remplacé par un assistant [i18n spécifique à AEM](handlebars-helpers.md#i-n). Cet avertissement est généré par la bibliothèque tierce pour confirmer le remplacement d’un assistant existant.

### Avertissement dans les journaux : OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

La publication de plusieurs sujets de forum de communautés sociales peut entraîner d’énormes quantités de journaux d’avertissement et d’informations de la part du processus OakResourceListener processOsgiEventQueue.

Ces avertissements peuvent être ignorés en toute sécurité.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### Erreur dans les journaux : NoClassDefFoundError pour IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

La mise à niveau d’AEM 5.6.1 vers la dernière version de cq-socialcommunities-pkg-1.4.x ou vers AEM 6.0 entraîne des erreurs dans le fichier journal. Cela se produit au démarrage pour une condition qui se résout d’elle-même, comme en témoigne le fait que l’erreur n’est pas visible au redémarrage.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
