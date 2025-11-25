---
title: Refactorisation de SocialUtils
description: Le package com.adobe.cq.social.ugcbase.SocialUtils a été abandonné dans AEM 6.1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Refactorisation de SocialUtils {#socialutils-refactoring}

## Package SocialUtils obsolète {#socialutils-package-deprecated}

Le package `com.adobe.cq.social.ugcbase.SocialUtils` a été abandonné dans AEM 6.1.

Les tableaux suivants répertorient les méthodes à utiliser à la place des méthodes `SocialUtils`.

## Package SocialResourceUtilities  {#socialresourceutilities-package}

| Méthodes dans com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities | Notes |
|---|---|
| Boolean checkPermission(ResourceResolver resolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource) |  |
| Resource getUGCResource(Resource userResource) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrrf) | nouveau |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrrf, String resourceTypeHint) | nouveau |
| Resource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booléen hasModeratePermissions(ressource) |  |
| String resourceToACLPath(Resource resource) |  |
| String resourceToUGCStoragePath(Resource resource) | remplace String resourceToUGCPath(Resource) |
| Chaîne UGCToResourcePath(Resource) |  |
| String UGCToResourcePath(String ugcPath) | signature de méthode modifiée |
| String UGCToResourcePath(String ugcPath, ResourceResolver resolver) | nouveau |

| Méthodes dans `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities | Notes |
|---|---|
| SocialResourceProvider getSocialResourceProvider(Resource) | remplace SocialResourceProvider getConfiguredProvider(Resource resource) |

## Package SCFUtilities {#scfutilities-package}

| Méthodes dans `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| Chaîne getAvatar(UserProperties userProperties) |
| Chaîne getAvatar(UserProperties userProperties, taille en entier) |
| Chaîne getAvatar(UserProperties userProperties, Chaîne absoluDefaultAvatar) |
| Chaîne getAvatar(UserProperties userProperties, Chaîne absoluDefaultAvatar, SocialUtils.AVATAR_SIZE) |
| Page getContainerPage(Resource resource) |
| String getSocialProfileURL(String username, ResourceResolver resolver, Page ) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## Réservé À Un Usage Interne {#for-internal-use-only}

| boolean canAddNode(session, String path) |
|---|
| String createUniqueNameHint(String message) |
| String createUniqueNameHint(String message, int numRandomChars) |
| String generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(Chemin d’accès de la chaîne, résolveur ResourceResolver) |
| String getPagePath(Resource resource) |
| String getPagePath(String path) |
| String getResourceTypeForIncludedResource(composant de ressource, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource, String styleProperty, String defaultValue) |
| boolean isResourceOwner(Resource) |
| String mapUGCPath(Resource resource) |
| String mapUGCPath(String ugcPath, ResourceResolver resolver) |
| boolean mayPost(ResourceResolver, Resource resource) |
| Chaîne readyUserGeneratedContent(ResourceResolver, chemin de la chaîne) |

## Méthodes Plus Disponibles {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Resource getResourceAtPath(ResourceResolver resolver, chemin de chaîne) |
| Resource getResourceAtPath(ResourceResolver resolver, Chemin de chaîne, Type de chaîne resourceType) |
| Configuration getStorageCloudServiceConfig(Resource) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booléen mayAccessUGC(ResourceResolver resolver) |
