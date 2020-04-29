---
title: Refactorisation de SocialUtils
seo-title: Refactorisation de SocialUtils
description: Le package com.adobe.cq.social.ugcbase.SocialUtils était obsolète dans AEM 6.1.
seo-description: Le package com.adobe.cq.social.ugcbase.SocialUtils était obsolète dans AEM 6.1.
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# Refactorisation de SocialUtils {#socialutils-refactoring}

## Package SocialUtils obsolète {#socialutils-package-deprecated}

Le package `com.adobe.cq.social.ugcbase.SocialUtils` a été abandonné dans AEM 6.1.

Les tableaux suivants  les méthodes à utiliser à la place des méthodes SocialUtils.

## Package SocialResourceUtilities {#socialresourceutilities-package}

| Méthodes dans com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| Boolean checkPermission(ResourceResolver resolver resolver, chemin de chaîne, action de chaîne) |  |
| SocialResourceProvider getSocialResourceProvider(ressource ressource ressource) |  |
| SocialResourceConfiguration getStorageConfig(Ressource de ressource) |  |
| Ressource getUGCResource(Ressource utilisateurRessource) |  |
| Ressource getUGCResource(Ressource utilisateurRessource, ResourceResolverFactory rf) | new |
| Ressource getUGCResource(Ressource utilisateurResource, ResourceResolverFactory rf, String resourceTypeHint) | new |
| Ressource getUGCResource(Ressource utilisateurRessource, String resourceTypeHint) |  |
| booléen hasModératePermissions(ressource ressource ressource) |  |
| Ressource de chaîneToACLPath(ressource de ressource) |  |
| Ressource de chaîneToUGCStoragePath(ressource de ressource) | remplace String resourceToUGCPath(Resource resource) |
| String UGCToResourcePath(Ressource de ressource) |  |
| String UGCToResourcePath(String ugcPath) | signature de méthode modifiée |
| String UGCToResourcePath(String ugcPath, résolveur ResourceResolver) | new |

| Méthodes dans `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(ressource ressource ressource) | remplace SocialResourceProvider getConfisongeProvider(Ressource de ressource) |

## Package SCFUtilities {#scfutilities-package}

| Méthodes dans `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, taille entière) |
| String getAvatar(UserProperties userProperties, chaîne absolueDefaultAvatar) |
| String getAvatar(UserProperties userProperties, chaîne absolueDefaultAvatar, taille SocialUtils.AVATAR_SIZE) |
| Page getContainerPage(ressource) |
| Chaîne getSocialProfileURL(Nom d’utilisateur de chaîne, Résolveur de ressources, Page) |
| UserProperties getUserProperties(ResourceResolver resolve, String userId) |

## For Internal Use Only {#for-internal-use-only}

| booléen canAddNode(session, chemin de chaîne) |
|---|
| String createUniqueNameHint(message de chaîne) |
| String createUniqueNameHint(message de chaîne, int numRandomChars) |
| Chaîne generateRandomString(longueur int) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(chemin de chaîne, résolveur ResourceResolver) |
| String getPagePath(Ressource de ressource) |
| String getPagePath(String path) |
| String getResourceTypeForIncludedResource(composant Resource, chaîne defaultResourceType, chaîne designPropertyName) |
| String getResourceTypeFromDesign(Ressource de ressource, propriété de style de chaîne, valeur de valeur par défaut de chaîne) |
| booléen isResourceOwner(ressource ressource ressource) |
| String mapUGCPath (ressource de ressource) |
| String mapUGCPath(String ugcPath, ResourceResolver resolve) |
| booléen mayPost(ResourceResolver resolve, Resource Resource) |
| Chaîne prepareUserGeneratedContent(résolveur ResourceResolver, chemin d’accès de chaîne) |

## Les Méthodes Ne Sont Plus Disponibles {#methods-no-longer-available}

| Node createNode(ResourceResolver resolve, String path, String nodeType) |
|---|
| Ressource getResourceAtPath(résolveur ResourceResolver, chemin d’accès de chaîne) |
| Ressource getResourceAtPath(résolveur ResourceResolver, chemin de chaîne, type de ressource de chaîne) |
| Configuration getStorageCloudServiceConfig(ressource de ressource) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booléen mayAccessUGC(résolveur ResourceResolver) |

