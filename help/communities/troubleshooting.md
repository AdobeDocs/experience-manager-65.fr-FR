---
title: Résolution des incidents
seo-title: Résolution des incidents
description: Dépannage de la communauté, y compris les problèmes connus
seo-description: Dépannage de la communauté, y compris les problèmes connus
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---


# Résolution des incidents {#troubleshooting}

Cette section contient des préoccupations communes et des questions connues.

## Problèmes connus {#known-issues}

### Echec de récupération du répartiteur {#dispatcher-refetch-fails}

Lors de l’utilisation de Dispatcher 4.1.5 avec une version plus récente de Jetty, une récupération peut entraîner l’impossibilité de recevoir une réponse du serveur distant après avoir attendu que la demande expire.

L’utilisation de Dispatcher 4.1.6 ou version ultérieure permettra de résoudre ce problème.

### Impossible d’accéder à la publication du forum après la mise à niveau à partir de CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Si un forum a été créé sur CQ 5.4 et que des sujets ont été publiés, puis que le site a été mis à niveau vers AEM 5.6.1 ou une version ultérieure, toute tentative de vue des publications existantes peut entraîner une erreur sur la page :

Caractère de modèle non autorisé &quot;a&#39;Impossible d&#39;envoyer la requête à `/content/demoforums/forum-test.html` ce serveur et les journaux contiennent les éléments suivants :

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

Le problème est que la chaîne de format pour com.day.cq.commons.date.RelativeTimeFormat a été modifiée entre 5.4 et 5.5 de sorte que la valeur &quot;a&quot; pour &quot;ago&quot; ne soit plus acceptée.

Ainsi, tout code utilisant l’API RelativeTimeFormat() doit changer :

* Origine: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* Pour :`final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

L’échec est différent sur l’auteur et la publication. Sur l&#39;auteur, il échoue silencieusement et n&#39;affiche simplement pas les sujets du forum. Lors de la publication, l’erreur est générée sur la page.

Pour plus d’informations, voir l’API [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API.

## Préoccupations communes {#common-concerns}

### Avertissement dans les journaux : Barres de poignées obsolètes {#warning-in-logs-handlebars-deprecated}

Au démarrage (pas au premier - mais tous les jours après), l&#39;avertissement suivant peut être vu dans les journaux :

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` a été remplacé par `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Cet avertissement peut être ignoré en toute sécurité, car `jknack.handlebars.Handlebars`il est utilisé par [SCF](scf.md#handlebarsjavascripttemplatinglanguage)et s&#39;accompagne de son propre utilitaire d&#39;assistance i18n. En début, il est remplacé par un aide [](handlebars-helpers.md#i-n)i18n spécifique AEM. Cet avertissement est généré par la bibliothèque tierce pour confirmer le remplacement d’un assistant existant.

### Avertissement dans les journaux : OakResourceListener, processusOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

La publication de plusieurs rubriques de forum Communautés de réseaux sociaux peut générer d’énormes quantités de journaux d’avertissement et d’informations provenant d’OakResourceListener processOsgiEventQueue.

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

La mise à niveau de AEM 5.6.1 GA vers la dernière version de cq-socialcommunautés-pkg-1.4.x ou vers AEM 6.0 entraîne des erreurs dans le fichier journal au démarrage pour une condition qui se résoudra comme en atteste l&#39;erreur qui n&#39;est pas visible au redémarrage.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
