---
title: SRP et UGC Essentials
seo-title: SRP et UGC Essentials
description: Présentation du fournisseur de ressources de stockage et du contenu généré par l'utilisateur
seo-description: Présentation du fournisseur de ressources de stockage et du contenu généré par l'utilisateur
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# SRP et UGC Essentials {#srp-and-ugc-essentials}

## Présentation {#introduction}

Si vous ne connaissez pas bien le fournisseur de ressources de stockage (SRP) et sa relation avec le contenu généré par l’utilisateur (UGC), consultez Présentation [du fournisseur de ressources de stockage](working-with-srp.md) et de [stockage de contenu de la](srp.md)communauté.

Cette section de la documentation fournit quelques informations essentielles sur le PRS et le CU.

## API StorageResourceProvider {#storageresourceprovider-api}

L’API SocialResourceProvider (API SRP) est une extension de diverses API du fournisseur de ressources Sling. Il comprend la prise en charge de la pagination et de l’incrément atomique (utile pour le décompte et le score).

Des requêtes sont nécessaires pour les composants SCF, car il est nécessaire de trier par date, utilité, nombre de votes, etc. Toutes les options SRP ont des mécanismes de requête souples qui ne reposent pas sur le cumul.

L’emplacement de stockage SRP incorpore le chemin d’accès au composant. L’API SRP doit toujours être utilisée pour accéder à l’UGC, car le chemin racine dépend de l’option SRP sélectionnée, telle que ASRP, MSRP ou JSRP.

L’API SRP n’est pas une classe abstraite, c’est une interface. Une implémentation personnalisée ne doit pas être entreprise à la légère, car les avantages des améliorations futures des implémentations internes seraient ignorés lors de la mise à niveau vers une nouvelle version.

Les méthodes d’utilisation de l’API SRP sont fournies par l’intermédiaire d’utilitaires fournis, tels que ceux figurant dans le package SocialResourceUtilities.

Lors de la mise à niveau à partir d’AEM 6.0 ou d’une version antérieure, il sera nécessaire de migrer UGC pour tous les fichiers SRP pour lesquels un outil Open Source est disponible. See [Upgrading to AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Historiquement, les utilitaires d’accès à l’UGC étaient trouvés dans le package SocialUtils, qui n’existe plus.
>
>Pour les utilitaires de remplacement, voir [SocialUtils Refactoring](socialutils.md).

## Méthode d&#39;utilitaire d&#39;accès à l&#39;UGC {#utility-method-to-access-ugc}

Pour accéder à l’UGC, utilisez une méthode du package SocialResourceUtilities qui renvoie un chemin approprié pour accéder à l’UGC à partir de SRP et remplace la méthode déconseillée trouvée dans le package SocialUtils.

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

Pour d’autres remplacements de SocialUtils, voir [SocialUtils Refactoring](socialutils.md).

Pour obtenir des instructions de codage, consultez [Accès à l’UGC avec SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>La ressource de chemin d&#39;accèsToUGCStoragePath() renvoie *ne convient *pas pour la vérification [des listes de](srp.md#for-access-control-acls)contrôle d&#39;accès.

## Méthode d&#39;utilitaire d&#39;accès aux listes de contrôle d&#39;accès {#utility-method-to-access-acls}

Certaines implémentations SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification ACL. Les noeuds d’ombre fournissent un emplacement dans le référentiel local auquel les ACL peuvent être appliquées.

A l’aide de l’API SRP, toutes les options SRP effectuent la même vérification de l’emplacement de l’ombre avant toutes les opérations CRUD.

Pour vérifier les listes de contrôle d’accès, utilisez une méthode qui renvoie un chemin approprié pour vérifier les autorisations appliquées au fichier UGC de la ressource.

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
>Le chemin renvoyé par resourceToACLPath() n&#39;est *pas *approprié pour [accéder à l&#39;UGC](#utility-method-to-access-acls) lui-même.

## Emplacements de stockage liés à UGC {#ugc-related-storage-locations}

Les descriptions suivantes de l’emplacement de stockage peuvent être utiles lors du développement avec JSRP ou MSRP. Il n’existe actuellement aucune interface utilisateur permettant d’accéder à l’UGC stocké dans ASRP, comme il en existe pour JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) et MSRP (outils MongoDB).

**emplacement du composant**

Lorsqu’un membre entre dans l’UGC dans l’environnement de publication, il interagit avec un composant dans le cadre d’un site AEM.

Un exemple de ce type de composant est le composant [](http://localhost:4502/content/community-components/en/comments.html) commentaires qui existe dans le site Guide [des composants de la](components-guide.md) communauté. Le chemin d’accès au noeud de commentaire dans le référentiel local est :

* Chemin du composant = */content/community-components/fr/commentaires/jcr:content/content/includable/commentaires*

**emplacement du noeud fantôme**

La création d’UGC crée également un noeud [d’](srp.md#about-shadow-nodes-in-jcr) ombre auquel les listes de contrôle d’accès nécessaires sont appliquées. Le chemin d’accès au noeud fantôme correspondant dans le référentiel local est le résultat du préattente du chemin d’accès racine du noeud fantôme au chemin d’accès du composant :

* Chemin d’accès racine = /content/usergenerated
* Noeud fantôme de commentaire = /content/usergenerated/content/community-components/fr/commentaires/jcr:content/content/includable/commentaires

**Emplacement UGC**

L’UGC n’est créé à aucun de ces emplacements et ne doit être accessible qu’à l’aide d’une méthode [d’](#utility-method-to-access-ugc) utilitaire qui appelle l’API SRP.

* Chemin racine = /content/usergenerated/asi/srp-choice
* Noeud UGC pour JSRP = /content/usergenerate/asi/jcr/content/community-components/fr/commentaires/jcr:content/content/includable/commentaires/srzd-let_it_be_

*N’oubliez* pas que, pour JSRP, le noeud UGC sera *uniquement* présent sur l’instance AEM (auteur ou publication) sur laquelle il a été saisi. Si elle est saisie sur une instance de publication, la modération ne sera pas possible à partir de la console de modération sur l’auteur.

## Informations connexes {#related-information}

* [Présentation](srp.md) du fournisseur de ressources de stockage - Présentation de l&#39;utilisation du référentiel
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - directives de codage
* [Réfactorisation](socialutils.md) de SocialUtils - Association des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles

