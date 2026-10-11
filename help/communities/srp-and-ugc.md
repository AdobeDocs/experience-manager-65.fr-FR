---
title: SRP et UGC Essentials
description: Présentation du fournisseur de ressources de stockage et du contenu généré par l’utilisateur
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%
---
# SRP et UGC Essentials {#srp-and-ugc-essentials}

## Présentation {#introduction}

Si vous ne connaissez pas le fournisseur de ressources de stockage (SRP) et sa relation avec le contenu créé par l’utilisateur, consultez les sections [Stockage de contenu de la communauté](working-with-srp.md) et [Présentation du fournisseur de ressources de stockage](srp.md).

Cette section de la documentation fournit des informations essentielles sur SRP et UGC.

## API StorageResourceProvider {#storageresourceprovider-api}

L’API SocialResourceProvider (API SRP) est une extension de différentes API de fournisseur de ressources Sling. Elle comprend la prise en charge de la pagination et de l’incrément atomique (utile pour le comptage et la notation).

Les requêtes sont nécessaires pour les composants SCF, car il est nécessaire de trier par date, utilité, nombre de votes, etc. Toutes les options SRP disposent de mécanismes de requête flexibles qui ne reposent pas sur le regroupement.

L’emplacement de stockage du SRP intègre le chemin du composant. L’API SRP doit toujours être utilisée pour accéder au contenu créé par l’utilisateur, car le chemin d’accès racine dépend de l’option SRP sélectionnée, telle que ASRP, MSRP ou JSRP.

L’API SRP n’est pas une classe abstraite, c’est une interface. Une implémentation personnalisée ne doit pas être effectuée à la légère, car les avantages des améliorations futures des implémentations internes seraient perdus lors de la mise à niveau vers une nouvelle version.

Les moyens d’utiliser l’API SRP passent par les utilitaires fournis, tels que ceux figurant dans le package SocialResourceUtilities.

Lors de la mise à niveau à partir d’AEM 6.0 ou d’une version antérieure, il sera nécessaire de migrer le contenu créé par l’utilisateur pour tous les SRP, pour lesquels un outil Open Source est disponible. Voir [Mise à niveau vers AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Historiquement, les utilitaires permettant d’accéder au contenu créé par l’utilisateur se trouvaient dans le package SocialUtils, qui n’existe plus.
>
>Pour les utilitaires de remplacement, voir [Refactorisation de SocialUtils](socialutils.md).

## Méthode utilitaire pour accéder au contenu créé par l’utilisateur {#utility-method-to-access-ugc}

Pour accéder au contenu créé par l’utilisateur, utilisez une méthode du package SocialResourceUtilities qui renvoie un chemin d’accès approprié au contenu créé par l’utilisateur à partir de SRP et remplace la méthode obsolète qui se trouve dans le package SocialUtils.

Voici un exemple minimal d’utilisation de la méthode resourceToUGCStoragePath() dans un servlet :

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

Pour d&#39;autres remplacements de SocialUtils, voir [Refactorisation de SocialUtils](socialutils.md).

Pour obtenir des instructions de codage, consultez [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>Le chemin d’accès renvoyé par resourceToUGCStoragePath() n’est *pas* adapté à la [vérification ACL](srp.md#for-access-control-acls).

## Méthode utilitaire pour accéder aux listes de contrôle d’accès {#utility-method-to-access-acls}

Certaines implémentations de SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification d’ACL. Les nœuds fantômes fournissent un emplacement dans le référentiel local auquel les listes de contrôle d’accès peuvent être appliquées.

Grâce à l&#39;API SRP, toutes les options SRP effectuent la même vérification de l&#39;emplacement de l&#39;ombre avant toutes les opérations CRUD.

Pour vérifier les listes de contrôle d’accès, utilisez une méthode qui renvoie un chemin d’accès approprié pour vérifier les autorisations appliquées au contenu créé par l’utilisateur de la ressource.

Voici un exemple simple d’utilisation de la méthode resourceToACLPath() dans un servlet :

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>Le chemin d’accès renvoyé par resourceToACLPath() n’est *pas* adapté pour [accéder au contenu créé par l’utilisateur](#utility-method-to-access-acls) lui-même.

## Emplacements de stockage liés au contenu créé par l’utilisateur {#ugc-related-storage-locations}

Les descriptions suivantes de l’emplacement de stockage peuvent s’avérer utiles lors du développement avec JSRP ou peut-être MSRP. Il n’existe actuellement aucune interface utilisateur pour accéder au contenu créé par l’utilisateur stocké dans ASRP, comme il en existe pour JSRP ([](../../help/sites-developing/developing-with-crxde-lite.md)) et MSRP (outils MongoDB).

**Emplacement du composant**

Lorsqu’un membre entre dans le contenu créé par l’utilisateur dans l’environnement de publication, il interagit avec un composant dans le cadre d’un site AEM.

Un exemple de ce composant est le [composant commentaires](http://localhost:4502/content/community-components/en/comments.html) qui existe dans le site [Guide des composants de communauté](components-guide.md). Le chemin d’accès au nœud de commentaire dans le référentiel local est : .

* Chemin du composant = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Emplacement du nœud caché**

La création du contenu créé par l’utilisateur crée également un [nœud fantôme](srp.md#about-shadow-nodes-in-jcr) auquel les listes de contrôle d’accès nécessaires sont appliquées. Le chemin d’accès au nœud fantôme correspondant dans le référentiel local résulte de l’ajout du chemin d’accès racine du nœud fantôme au chemin d’accès du composant :

* Chemin racine = `/content/usergenerated`
* Nœud fantôme de commentaire = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Emplacement du contenu créé par l’utilisateur**

Le contenu créé par l’utilisateur n’est créé dans aucun de ces emplacements et n’est accessible qu’à l’aide d’une [ méthode utilitaire](#utility-method-to-access-ugc) qui appelle l’API SRP.

* Chemin racine = `/content/usergenerated/asi/srp-choice`
* Nœud UGC pour JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Gardez à l’esprit que* pour JSRP, le nœud du contenu créé par l’utilisateur sera *uniquement* présent sur l’instance AEM (création ou publication) sur laquelle il a été saisi. Si elle est entrée sur une instance de publication, la modération ne sera pas possible à partir de la console de modération en mode de création.

## Informations connexes {#related-information}

* [Présentation du fournisseur de ressources de stockage](srp.md) - Introduction et présentation de l’utilisation du référentiel.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes d&#39;utilitaire obsolètes aux méthodes d&#39;utilitaire SRP actuelles.
