---
title: Principes de base de la SRP et du contenu généré par l’utilisateur
seo-title: Principes de base de la SRP et du contenu généré par l’utilisateur
description: Présentation du fournisseur de ressources de stockage et du contenu généré par l’utilisateur
seo-description: Présentation du fournisseur de ressources de stockage et du contenu généré par l’utilisateur
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Principes de base de la SRP et de l’UGC {#srp-and-ugc-essentials}

## Présentation {#introduction}

Si vous ne connaissez pas le fournisseur de ressources de stockage (SRP) et sa relation avec le contenu généré par l’utilisateur, consultez [Stockage de contenu de la communauté](working-with-srp.md) et [Présentation du fournisseur de ressources de stockage](srp.md).

Cette section de la documentation fournit des informations essentielles sur la SRP et le contenu généré par l’utilisateur.

## API StorageResourceProvider {#storageresourceprovider-api}

L’API SocialResourceProvider (API SRP) est une extension de diverses API Sling Resource Provider. Il comprend la prise en charge de la pagination et de l’incrément atomique (utile pour le décompte et la notation).

Les requêtes sont nécessaires pour les composants SCF, car il est nécessaire de trier par date, utilité, nombre de votes, etc. Toutes les options de SRP ont des mécanismes de requête flexibles qui ne reposent pas sur le regroupement.

L’emplacement de stockage SRP incorpore le chemin d’accès au composant. L’API SRP doit toujours être utilisée pour accéder au contenu généré par l’utilisateur, car le chemin racine dépend de l’option SRP sélectionnée, comme ASRP, MSRP ou JSRP.

L’API SRP n’est pas une classe abstraite, il s’agit d’une interface. Une implémentation personnalisée ne doit pas être entreprise à la légère, car les avantages des améliorations futures apportées aux implémentations internes seraient ignorés lors de la mise à niveau vers une nouvelle version.

Les moyens d’utilisation de l’API SRP sont les utilitaires fournis, tels que ceux trouvés dans le package SocialResourceUtilities.

Lors de la mise à niveau à partir d’AEM 6.0 ou d’une version antérieure, il sera nécessaire de migrer le contenu créé par l’utilisateur pour toutes les applications de gestion de la relation client (SRP), pour lesquelles un outil Open Source est disponible. Voir [Mise à niveau vers AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Historiquement, les utilitaires pour accéder au contenu créé par l’utilisateur étaient trouvés dans le package SocialUtils, qui n’existe plus.
>
>Pour les utilitaires de remplacement, voir [Refactorisation de SocialUtils](socialutils.md).

## Méthode utilitaire d’accès au contenu généré par l’utilisateur {#utility-method-to-access-ugc}

Pour accéder au contenu généré par l’utilisateur, utilisez une méthode du package SocialResourceUtilities qui renvoie un chemin approprié pour accéder au contenu créé par l’utilisateur à partir de la SRP et remplace la méthode obsolète trouvée dans le package SocialUtils .

Voici un exemple minimal d’utilisation de la méthode resourceToUGCStoragePath() dans une servlet :

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

Pour les autres remplacements de SocialUtils, voir [Refactorisation de SocialUtils](socialutils.md).

Pour obtenir des instructions sur le codage, consultez [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>Le chemin resourceToUGCStoragePath() renvoie *not* adapté à la [vérification ACL](srp.md#for-access-control-acls).

## Méthode utilitaire d’accès aux listes de contrôle d’accès {#utility-method-to-access-acls}

Certaines mises en oeuvre de la SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification de l’ACL. Les noeuds fantômes fournissent un emplacement dans le référentiel local auquel les listes de contrôle d’accès peuvent être appliquées.

À l’aide de l’API SRP, toutes les options de SRP effectuent la même vérification de l’emplacement fantôme avant toutes les opérations CRUD.

Pour vérifier les listes de contrôle d’accès, utilisez une méthode qui renvoie un chemin approprié pour vérifier les autorisations appliquées au contenu créé par l’utilisateur de la ressource.

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
>Le chemin renvoyé par resourceToACLPath() est *différent de* adapté à [l’accès au contenu créé par l’utilisateur](#utility-method-to-access-acls) lui-même.

## Emplacements de stockage associés à l’UGC {#ugc-related-storage-locations}

Les descriptions suivantes de l’emplacement de stockage peuvent s’avérer utiles lors du développement avec JSRP ou peut-être MSRP. Il n’existe actuellement aucune interface utilisateur pour accéder au contenu généré par l’utilisateur stocké dans ASRP, comme c’est le cas pour JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) et MSRP (outils MongoDB).

**Emplacement du composant**

Lorsqu’un membre entre dans le contenu généré par l’utilisateur dans l’environnement de publication, il interagit avec un composant dans le cadre d’un site AEM.

Un exemple de ce type de composant est le [composant de commentaires](http://localhost:4502/content/community-components/en/comments.html) qui existe dans le site [Guide des composants de communauté](components-guide.md). Le chemin d’accès au noeud de commentaire dans le référentiel local est le suivant :

* Chemin du composant = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Emplacement du noeud fantôme**

La création du contenu créé par l’utilisateur crée également un [noeud fantôme](srp.md#about-shadow-nodes-in-jcr) auquel les listes de contrôle d’accès nécessaires sont appliquées. Le chemin d’accès au noeud fantôme correspondant dans le référentiel local est le résultat de l’ajout du chemin racine du noeud fantôme au chemin d’accès du composant :

* Chemin racine = `/content/usergenerated`
* Noeud fantôme de commentaire = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Emplacement UGC**

Le contenu créé par l’utilisateur n’est créé à aucun de ces emplacements et ne doit être accessible qu’à l’aide d’une [méthode utilitaire](#utility-method-to-access-ugc) qui appelle l’API SRP.

* Chemin racine = `/content/usergenerated/asi/srp-choice`
* Noeud UGC pour JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Gardez à l’esprit que* pour JSRP, le noeud UGC  ** n’est présent que sur l’instance AEM (auteur ou publication) sur laquelle il a été saisi. Si elle est saisie sur une instance de publication, la modération ne sera pas possible dans la console de modération de l’instance de création.

## Informations connexes {#related-information}

* [Présentation du fournisseur de ressources de stockage](srp.md)  - Présentation et utilisation du référentiel.
* [Accès au contenu généré par l’utilisateur avec SRP](accessing-ugc-with-srp.md)  - Instructions de codage.
* [Refactorisation de SocialUtils](socialutils.md)  : mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.
