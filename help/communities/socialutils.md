---
title: Refactorisation de SocialUtils
seo-title: Refactorisation de SocialUtils
description: Le package com.adobe.cq.social.ugcbase.SocialUtils a été abandonné dans AEM 6.1.
seo-description: Le package com.adobe.cq.social.ugcbase.SocialUtils a été abandonné dans AEM 6.1.
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Refactorisation de SocialUtils {#socialutils-refactoring}

## Package SocialUtils obsolète {#socialutils-package-deprecated}

Le package `com.adobe.cq.social.ugcbase.SocialUtils` a été abandonné dans AEM 6.1.

Les tableaux suivants liste les méthodes à utiliser à la place des méthodes `SocialUtils`.

## Package SocialResourceUtilities {#socialresourceutilities-package}

| Méthodes de com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| CheckPermission booléenne (résolveur ResourceResolver, chemin de chaîne, action de chaîne) |  |
| SocialResourceProvider getSocialResourceProvider(Ressource de ressource) |  |
| SocialResourceConfiguration getStorageConfig(Ressource de ressources) |  |
| Ressource getUGCResource(Ressource utilisateurRessource) |  |
| Ressource getUGCResource(Resource userResource, ResourceResolverFactory rf) | new |
| Ressource getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | new |
| Ressource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booléen hasModeratePermissions(ressource ressource) |  |
| String resourceToACLPath(Resource resource) |  |
| String resourceToUGCStoragePath(Resource resource) | remplace String resourceToUGCPath(Resource resource) |
| String UGCToResourcePath(Ressource de ressource) |  |
| String UGCToResourcePath(String ugcPath) | signature de méthode modifiée |
| Chaîne UGCToResourcePath(chaîne ugcPath, résolveur ResourceResolver) | new |

| Méthodes de `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(Ressource de ressource) | Remplace SocialResourceProvider getConficonfiguredProvider(Ressource de ressource) |

## Package SCFUtilities {#scfutilities-package}

| Méthodes de `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| Chaîne getAvatar(UserProperties userProperties, chaîne absolueDefaultAvatar) |
| Chaîne getAvatar(UserProperties userProperties, chaîne absolueDefaultAvatar, taille SocialUtils.AVATAR_SIZE) |
| Page getContainerPage(ressource) |
| Chaîne getSocialProfileURL(nom d’utilisateur de chaîne, résolveur ResourceResolver, page) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## Pour un usage interne uniquement {#for-internal-use-only}

| booléen canAddNode(session, chemin d’accès de chaîne) |
|---|
| Chaîne createUniqueNameHint(message de chaîne) |
| Chaîne createUniqueNameHint(message de chaîne, int numRandomChars) |
| String generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(chemin de chaîne, résolveur ResourceResolver) |
| Chaîne getPagePath(ressource) |
| String getPagePath(String path) |
| String getResourceTypeForIncludedResource(composant Resource, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource resource, String styleProperty, String defaultValue) |
| booléen isResourceOwner(ressource ressource ressource) |
| String mapUGCPath(Resource resource) |
| String mapUGCPath(String ugcPath, ResourceResolver resolver) |
| booléen mayPost(résolveur ResourceResolver, ressource Resource) |
| String prepareUserGeneratedContent(ResourceResolver resolver, chemin d&#39;accès de chaîne) |

## Méthodes indisponibles {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Ressource getResourceAtPath(ResourceResolver resolver, chemin d&#39;accès de chaîne) |
| Ressource getResourceAtPath(ResourceResolver resolver, chemin de chaîne, type de ressource de chaîne) |
| Configuration de getStorageCloudServiceConfig(ressource ressource) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booléen mayAccessUGC(ResourceResolver resolver) |

