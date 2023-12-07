---
title: Refactorisation de SocialUtils
description: Le package com.adobe.cq.social.ugcbase.SocialUtils a été abandonné dans AEM 6.1.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# Refactorisation de SocialUtils {#socialutils-refactoring}

## Package SocialUtils obsolète {#socialutils-package-deprecated}

Le package `com.adobe.cq.social.ugcbase.SocialUtils` a été abandonné dans AEM 6.1.

Les tableaux suivants répertorient les méthodes à utiliser au lieu de `SocialUtils` méthodes.

## Package SocialResourceUtilities  {#socialresourceutilities-package}

| Méthodes dans com.adobe.cq.social.srp.utility.api.SocialResourceUtilities |
|---|
| Valeur booléenne checkPermission(ResourceResolver resolver, chemin de chaîne, action de chaîne) |  |
| SocialResourceProvider getSocialResourceProvider(Resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource resource) |  |
| Resource getUGCResource(Resource userResource) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rf) | nouveau |
| Ressource getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | nouveau |
| Ressource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| boolean hasModératePermissions(Resource resource) |  |
| String resourceToACLPath(Resource resource) |  |
| String resourceToUGCStoragePath(Resource resource) | remplace String resourceToUGCPath(Resource resource) |
| Chaîne UGCToResourcePath(ressource ressource) |  |
| Chaîne UGCToResourcePath(String ugcPath) | signature de méthode modifiée |
| Chaîne UGCToResourcePath(chaîne ugcPath, résolveur ResourceResolver) | nouveau |

| Méthodes dans `com.adobe.cq.social.`Utilitaires.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(Resource) | remplace SocialResourceProvider getConfiguredProvider(Resource ressource) |

## Package SCFUtilities {#scfutilities-package}

| Méthodes dans `com.adobe.cq.social.`utility.scf.api.SCFUtilites |
|---|
| Chaîne getAvatar(UserProperties userProperties) |
| Chaîne getAvatar(UserProperties userProperties, int size) |
| Chaîne getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| Chaîne getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, taille SocialUtils.AVATAR_SIZE) |
| Page getContainerPage(Resource resource) |
| Chaîne getSocialProfileURL(Chaîne nom d’utilisateur, résolveur ResourceResolver, page) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## Pour une utilisation interne uniquement {#for-internal-use-only}

| booléen canAddNode(session de session, chemin d’accès de chaîne) |
|---|
| Chaîne createUniqueNameHint(message de chaîne) |
| Chaîne createUniqueNameHint(message de chaîne, int numRandomChars) |
| Chaîne generateRandomString(longueur int) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(chemin de chaîne, résolveur ResourceResolver) |
| Chaîne getPagePath(Resource resource) |
| Chaîne getPagePath(Chaîne path) |
| Chaîne getResourceTypeForIncludedResource(composant Ressource, chaîne defaultResourceType, chaîne designPropertyName) |
| Chaîne getResourceTypeFromDesign(ressource de ressource, chaîne styleProperty, chaîne defaultValue) |
| booléen isResourceOwner(Resource resource) |
| String mapUGCPath(Resource resource resource) |
| String mapUGCPath(String ugcPath, ResourceResolver resolver) |
| booléen mayPost(ResourceResolver resolver, Resource resource) |
| Chaîne prepareUserGeneratedContent(ResourceResolver resolver, chemin d’accès de chaîne) |

## Méthodes devenues indisponibles {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Ressource getResourceAtPath(ResourceResolver resolver, chemin d’accès de chaîne) |
| Resource getResourceAtPath(ResourceResolver resolver, String path, String resourceType) |
| Configuration de getStorageCloudServiceConfig(ressource de ressource) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booléen mayAccessUGC(ResourceResolver resolver) |
