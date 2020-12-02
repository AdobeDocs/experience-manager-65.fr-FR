---
title: SRP et UGC Essentials
seo-title: SRP et UGC Essentials
description: Présentation du fournisseur de ressources d'Enregistrement et du contenu généré par l'utilisateur
seo-description: Présentation du fournisseur de ressources d'Enregistrement et du contenu généré par l'utilisateur
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# SRP et UGC Essentials {#srp-and-ugc-essentials}

## Présentation {#introduction}

Si vous ne connaissez pas bien le fournisseur de ressources d’enregistrement (SRP) et sa relation avec le contenu généré par l’utilisateur, visitez [Enregistrement de contenu communautaire](working-with-srp.md) et [Présentation du fournisseur de ressources d’Enregistrement](srp.md).

Cette section de la documentation contient des renseignements essentiels sur le PRS et le CU.

## API StorageResourceProvider {#storageresourceprovider-api}

L’API SocialResourceProvider (API SRP) est une extension de plusieurs API du fournisseur de ressources Sling. Il comprend la prise en charge de la pagination et de l’incrément atomique (utile pour le décompte et le score).

Les requêtes sont nécessaires pour les composants de la SCF, car il est nécessaire de trier par date, utilité, nombre de votes, etc. Toutes les options du PSR sont dotées de mécanismes de requête flexibles qui ne reposent pas sur le cumul.

L&#39;emplacement de l&#39;enregistrement SRP incorpore le chemin du composant. L&#39;API SRP doit toujours être utilisée pour accéder à l&#39;UGC car le chemin racine dépend de l&#39;option SRP sélectionnée, telle que ASRP, MSRP ou JSRP.

L&#39;API SRP n&#39;est pas une classe abstraite, c&#39;est une interface. Une mise en oeuvre personnalisée ne doit pas être entreprise à la légère, car les avantages des améliorations futures apportées aux implémentations internes seraient négligés lors de la mise à niveau vers une nouvelle version.

Les méthodes d’utilisation de l’API SRP sont les utilitaires fournis, tels que ceux qui se trouvent dans le package SocialResourceUtilities.

Lors de la mise à niveau à partir de AEM 6.0 ou d&#39;une version antérieure, il sera nécessaire de migrer UGC pour tous les fichiers SRP, pour lesquels un outil Open Source est disponible. Voir [Mise à niveau vers AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Historiquement, les utilitaires d’accès à l’UGC se trouvaient dans le package SocialUtils, qui n’existe plus.
>
>Pour les utilitaires de remplacement, voir [Refactoring SocialUtils](socialutils.md).

## Méthode d&#39;utilitaire pour accéder à l&#39;UGC {#utility-method-to-access-ugc}

Pour accéder à l’UGC, utilisez une méthode issue du package SocialResourceUtilities qui renvoie un chemin d’accès approprié pour accéder à l’UGC à partir de SRP et remplace la méthode déconseillée trouvée dans le package SocialUtils.

Voici un exemple minimal d&#39;utilisation de la méthode resourceToUGCStoragePath() dans une servlet :

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

Pour d’autres remplacements de SocialUtils, voir [Refactorisation de SocialUtils](socialutils.md).

Pour obtenir des instructions de codage, consultez [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>Le chemin d&#39;accès que renvoie la ressourceToUGCStoragePath() est *non* approprié pour la vérification de [ACL](srp.md#for-access-control-acls).

## Méthode d&#39;utilitaire pour accéder aux listes ACL {#utility-method-to-access-acls}

Certaines implémentations SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification ACL. Les noeuds d’ombre fournissent un emplacement dans le référentiel local auquel les ACL peuvent être appliquées.

A l’aide de l’API SRP, toutes les options SRP effectuent la même vérification de l’emplacement de l’ombre avant toutes les opérations CRUD.

Pour vérifier les listes de contrôle d&#39;accès, utilisez une méthode qui renvoie un chemin approprié pour vérifier les autorisations appliquées à l&#39;UGC de la ressource.

Voici un exemple simple d’utilisation de la méthode resourceToACLPath() dans une servlet :

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
>Le chemin renvoyé par resourceToACLPath() est *non* approprié pour [accéder à l&#39;UGC](#utility-method-to-access-acls) lui-même.

## Emplacement des Enregistrements liés à l&#39;UGC {#ugc-related-storage-locations}

Les descriptions suivantes de l&#39;emplacement des enregistrements peuvent être utiles pour le développement avec le Programme de recherche en milieu de travail (JSRP) ou peut-être le Programme de recherche en milieu de travail (MSRP). Il n&#39;existe actuellement aucune interface utilisateur pour accéder à l&#39;UGC stocké dans ASRP, comme il en existe pour JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) et MSRP (outils MongoDB).

**Emplacement du composant**

Lorsqu’un membre entre à l’UGC dans l’environnement de publication, il interagit avec un composant dans le cadre d’un site AEM.

Un exemple de ce type de composant est le [composant commentaires](http://localhost:4502/content/community-components/en/comments.html) qui existe dans le site [Community Components Guide](components-guide.md). Le chemin d’accès au noeud de commentaires dans le référentiel local est :

* Chemin du composant = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Emplacement du noeud fantôme**

La création de l&#39;UGC crée également un [noeud fantôme](srp.md#about-shadow-nodes-in-jcr) auquel les ACL nécessaires sont appliquées. Le chemin d’accès au noeud fantôme correspondant dans le référentiel local est le résultat du préattente du chemin d’accès racine du noeud fantôme au chemin d’accès du composant :

* Chemin racine = `/content/usergenerated`
* Commenter le noeud fantôme = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Emplacement UGC**

L&#39;UGC est créé dans aucun de ces emplacements et ne doit être accessible qu&#39;à l&#39;aide d&#39;une [méthode d&#39;utilitaire](#utility-method-to-access-ugc) qui appelle l&#39;API SRP.

* Chemin racine = `/content/usergenerated/asi/srp-choice`
* Noeud UGC pour JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Notez* que, pour JSRP, le noeud UGC n’est  ** présent que sur l’instance AEM (auteur ou publication) sur laquelle il a été saisi. Si elle est saisie sur une instance de publication, la modération ne sera pas possible à partir de la console de modération sur l’auteur.

## Informations connexes {#related-information}

* [Présentation](srp.md)  du fournisseur de ressources d&#39;Enregistrement - Présentation et présentation de l&#39;utilisation du référentiel.
* [Accès à l&#39;UGC avec des directives de codage SRP](accessing-ugc-with-srp.md) .
* [SocialUtils Refactoring](socialutils.md)  - Mise en correspondance des méthodes d’utilitaire obsolètes avec les méthodes d’utilitaire SRP actuelles.
