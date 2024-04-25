---
title: Communauté de dépannage
description: Découvrez la communauté de dépannage, y compris les problèmes connus et les préoccupations.
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
source-wordcount: '355'
ht-degree: 0%

---

# Communauté de dépannage {#troubleshooting}

Cette section contient des problèmes courants et des problèmes connus lors de la résolution des problèmes dans la communauté.

## Problèmes connus {#known-issues}

### Échec de la récupération de Dispatcher {#dispatcher-refetch-fails}

Lors de l’utilisation de Dispatcher 4.1.5 avec une version plus récente de Jetty, une récupération peut entraîner l’impossibilité de recevoir une réponse du serveur distant après avoir attendu que la demande expire.

L’utilisation de Dispatcher 4.1.6 ou version ultérieure résout ce problème.

### Impossible d’accéder à la publication du forum après la mise à niveau depuis CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Si un forum a été créé sur CQ 5.4 et que des sujets ont été publiés, puis que le site a été mis à niveau vers AEM 5.6.1 ou version ultérieure, toute tentative d’affichage des publications existantes peut entraîner une erreur sur la page :

Caractère de modèle non valide &quot;a&quot; Impossible d’envoyer la requête à `/content/demoforums/forum-test.html` sur ce serveur et les logs contiennent les éléments suivants :

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

Le problème est que la chaîne de format pour com.day.cq.commons.date.RelativeTimeFormat a été modifiée entre la version 5.4 et la version 5.5 de sorte que &quot;a&quot; pour &quot;ago&quot; ne soit plus accepté.

Par conséquent, tout code utilisant l’API RelativeTimeFormat() doit changer :

* De : `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* Pour : `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

L’échec est différent sur les instances de création et de publication. Sur l’auteur, il échoue silencieusement et n’affiche simplement pas les rubriques du forum. Lors de la publication, l’erreur est générée sur la page.

Voir [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API pour plus d’informations.

## Préoccupations communes {#common-concerns}

### Avertissement dans les journaux : Handlebars obsolètes {#warning-in-logs-handlebars-deprecated}

Au démarrage (et non au premier démarrage), l’avertissement suivant apparaît dans les journaux :

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` a été remplacé par `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Cet avertissement peut être ignoré en toute sécurité en tant que `jknack.handlebars.Handlebars`, utilisé par [SCF](scf.md#handlebarsjavascripttemplatinglanguage), est fourni avec son propre utilitaire d’assistance i18n. Au démarrage, il est remplacé par un AEM spécifique [Assistant i18n](handlebars-helpers.md#i-n). Cet avertissement est généré par la bibliothèque tierce pour confirmer le remplacement d’une assistance existante.

### Avertissement dans les journaux : OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

La publication de plusieurs rubriques de forum Communautés de réseaux sociaux peut entraîner un très grand nombre de logs d’avertissement et d’informations provenant d’OakResourceListener processOsgiEventQueue.

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

La mise à niveau d’AEM 5.6.1 vers la dernière version de cq-socialcommunities-pkg-1.4.x ou vers AEM 6.0 entraîne des erreurs dans le fichier journal. Cela se produit au démarrage pour une condition qui se résout elle-même, comme en témoigne l’erreur qui ne s’affiche pas au redémarrage.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
