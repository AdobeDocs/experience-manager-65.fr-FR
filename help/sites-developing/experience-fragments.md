---
title: Fragments d’expérience
seo-title: Fragments d’expérience
description: Découvrez comment personnaliser les fragments d’expérience.
seo-description: Découvrez comment personnaliser les fragments d’expérience.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 92%

---


# Fragments d’expérience{#experience-fragments}

## Principes élémentaires {#the-basics}

Un [fragment d’expérience](/help/sites-authoring/experience-fragments.md) est un groupe d’un ou plusieurs composants comprenant un contenu et une disposition pouvant être référencés dans les pages.

Un gabarit et/ou une variation du fragment d’expérience utilise :

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

En l’absence de `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, il revient à

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Rendu HTML brut {#the-plain-html-rendition}

Le sélecteur `.plain.` de l’URL permet d’accéder au rendu HTML brut.

Cela est possible à partir du navigateur. Cependant, le principal objectif consiste à autoriser d’autres applications (des applications web tierces et des implémentations mobiles personnalisées, par exemple) à accéder directement au contenu du fragment d’expérience en utilisant uniquement l’URL.

Le rendu HTML brut ajoute le protocole, l’hôte et le chemin d’accès au contexte à des chemins qui :

* sont du type `src`, `href` ou `action` ;

* se terminent par `-src` ou `-href`.

Par exemple :

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Les liens font toujours référence à l’instance de publication. Ils sont destinés à être utilisés par des tiers, de sorte qu’ils soient toujours appelés à partir de l’instance de publication, et non de l’auteur.

![xf-14](assets/xf-14.png)

Le sélecteur de rendu brut utilise un transformateur plutôt que des scripts supplémentaires ; le module [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) est utilisé comme transformateur. Cette configuration se trouve dans l’emplacement suivant :

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variations sociales {#social-variations}

Les variations sociales peuvent être publiées sur les réseaux sociaux (texte et image). Dans AEM, ces variations sociales peuvent contenir des composants ; des composants texte ou image, par exemple.

L’image et le texte de la publication sur le réseau social peuvent être extraits de n’importe quel type de ressource d’image ou de ressource de texte, à n’importe quel niveau de profondeur (dans le bloc fonctionnel ou dans le conteneur de mises en page).

Les variations sociales autorisent également les blocs fonctionnels et les prennent en compte lors de l’exécution d’actions sur les réseaux sociaux (dans l’environnement de publication).

Pour publier le contenu texte et image approprié sur le réseau social, il convient de respecter certaines conventions si vous développez vos propres composants personnalisés.

Pour ce faire, vous devez utiliser les propriétés suivantes :

* Pour extraire l’image

   * `fileReference`
   * `fileName`

* Pour extraire le texte

   * `text`

Les composants qui ne respectent pas cette convention ne sont pas pris en compte.

## Modèles de fragments d’expérience {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Seuls***[ les modèles modifiables sont pris en charge pour les fragments d’expérience.](/help/sites-developing/page-templates-editable.md)

When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).

Pour créer un modèle de fragment d’expérience détecté par l’assistant **Créer un fragment d’expérience**, vous devez suivre l’un des ensembles de règles suivants :

1. Les deux :

   1. Le type de ressource du modèle (le nœud initial) doit hériter de :
      `cq/experience-fragments/components/xfpage`

   1. Et le nom du modèle doit commencer par :
      `experience-fragments`
Cela permet aux utilisateurs de créer des fragments d’expérience dans /content/experience-fragments en tant que 
`cq:allowedTemplates` de ce dossier contient tous les modèles dont le nom commence par `experience-fragment`. Les clients peuvent mettre à jour cette propriété afin d’inclure leur propre schéma d’affectation de noms ou emplacement de modèle.

1. Les [modèles autorisés](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) peuvent être configurés dans la console des fragments d’expérience.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Composants des fragments d’expérience {#components-for-experience-fragments}

[Le développement de composants à utiliser avec/dans les fragments d’expérience est conforme aux pratiques standard.](/help/sites-developing/components.md)

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).

## Fournisseur de réécriture de liens de fragments d’expérience - HTML {#the-experience-fragment-link-rewriter-provider-html}

Dans AEM, vous avez la possibilité de créer des fragments d’expérience. Un fragment d’expérience :

* est constitué d’un groupe de composants avec une mise en page ;
* peut exister indépendamment d’une page AEM.

De tels groupes sont notamment utilisés pour incorporer du contenu dans des points de contact tiers, tels qu’Adobe Target.

### Réécriture de liens par défaut {#default-link-rewriting}

Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:

* de créer un fragment d’expérience ,
* d’y ajouter des composants ;
* de l’exporter ensuite en tant qu’offre Adobe Target, au format HTML ou JSON.

This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Elle nécessite une configuration Adobe Target valide, ainsi que des configurations pour l’externaliseur de liens.

L’externaliseur de liens sert à déterminer les URL appropriées qui sont nécessaires lors de la création de la version HTML de l’offre Target, qui est ensuite envoyée à Adobe Target. Cela s’avère nécessaire dans la mesure où Adobe Target exige que tous les liens de l’offre HTML Target soient accessibles au public ; cela signifie que les ressources auxquelles les liens font référence et le fragment d’expérience proprement dit doivent être publiés avant d’être utilisés.

Par défaut, lorsque vous créez une offre HTML Target, une requête est envoyée à un sélecteur Sling personnalisé dans AEM. Ce sélecteur est appelé `.nocloudconfigs.html`. Comme son nom l’indique, il crée un rendu HTML brut d’un fragment d’expérience, mais n’inclut pas de configurations cloud (qui seraient des informations superflues).

Une fois la page HTML générée, le pipeline Sling Rewriter apporte des modifications à la sortie :

1. Les éléments `html`, `head` et `body` sont remplacés par des éléments `div`. Les éléments `meta`, `noscript` et `title` sont supprimés (il s’agit d’éléments enfants de l’élément `head` d’origine et ils ne sont pas pris en compte lorsque celui-ci est remplacé par l’élément `div`).

   Cela permet de s’assurer que l’offre Target HTML peut être incluse dans les activités Target.

1. AEM modifie les liens internes présents dans le code HTML afin qu’ils pointent vers une ressource publiée.

   Pour identifier les liens à modifier, AEM suit ce modèle pour les attributs d’éléments HTML :

   1. Attributs `src`
   1. Attributs `href`
   1. Attributs `*-src` (comme data-src, custom-src, etc.)
   1. Attributs `*-href` (comme `data-href`, `custom-href`, `img-href`, etc.)

   >[!NOTE]
   >
   >Dans la plupart des cas, les liens internes du code HTML sont des liens relatifs, mais il peut arriver que des composants personnalisés fournissent des URL complètes dans le code HTML. Par défaut, AEM ignore ces URL complètes et n’effectue aucune modification.

   Les liens de ces attributs sont exécutés via l’externaliseur de liens AEM `publishLink()` afin de recréer l’URL comme si elle se trouvait sur une instance publiée et, de ce fait, accessible au public.

Lors de l’utilisation d’une implémentation prête à l’emploi, le processus décrit ci-dessus doit être suffisant pour générer l’offre Target à partir du fragment d’expérience, puis l’exporter vers Adobe Target. Toutefois, certains cas d’utilisation ne sont pas pris en compte dans ce processus, à savoir :

* Mappage Sling disponible uniquement sur l’instance de publication
* Redirections du Dispatcher

Pour ces cas d’utilisation, AEM propose l’interface du fournisseur de réécriture de liens.

### Interface du fournisseur de réécriture de liens {#link-rewriter-provider-interface}

>[!NOTE]
>
>Cette interface a été introduite dans [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/sp-release-notes.md).

Pour les cas plus complexes, non couverts par le [paramètre par défaut](#default-link-rewriting), AEM propose l’interface du fournisseur de réécriture de liens. Il s’agit d’une interface `ConsumerType` que vous pouvez implémenter dans vos bundles sous la forme d’un service. Elle ignore les modifications qu’AEM effectue sur les liens internes d’une offre HTML telle qu’elle est générée à partir d’un fragment d’expérience. Cette interface vous permet de personnaliser le processus de réécriture des liens HTML internes afin de l’adapter aux besoins de votre entreprise.

Voici quelques exemples d’implémentation de cette interface en tant que service :

* Les mappages Sling sont activés sur les instances de publication, mais pas sur l’instance de création.
* Un Dispatcher ou une technologie semblable est utilisé pour rediriger les URL en interne.
* Il existe des `sling:alias mechanisms` pour les ressources.

>[!NOTE]
>
>Cette interface traite uniquement les liens HTML internes de l’offre Target générée.

L’interface du fournisseur de réécriture de liens (`ExperienceFragmentLinkRewriterProvider`) se présente comme suit :

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Utilisation de l’interface du fournisseur de réécriture de liens {#how-to-use-the-link-rewriter-provider-interface}

Avant d’utiliser cette interface, vous devez créer un bundle contenant un nouveau composant de service qui l’implémente.

Ce service sera utilisé pour se connecter à la réécriture Exporter vers Target du fragment d’expérience afin d’avoir accès aux différents liens.

Par exemple, `ComponentService` :

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

Pour que le service fonctionne, trois méthodes doivent à présent être implémentées en interne :

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Vous devez indiquer au système s’il doit ou non réécrire les liens lorsqu’un appel est effectué pour Exporter vers Target sur une variation donnée du fragment d’expérience. Pour ce faire, implémentez la méthode suivante :

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Par exemple :

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Cette méthode reçoit, en tant que paramètre, la variation du fragment d’expérience qui est actuellement réécrite par le système Exporter vers Target.

Dans l’exemple ci-dessus, nous souhaitons réécrire les éléments suivants :

* Les liens présents dans `src`

* Uniquement les attributs `href`

* Pour un fragment d’expérience spécifique :
   `/content/experience-fragment/master`

Les autres fragments d’expérience transitant par le système Exporter vers la cible sont ignorés et ne sont pas affectés par les modifications implémentées dans ce service.

#### rewriteLink {#rewritelink}

S’agissant de la variation du fragment d’expérience concernée par le processus de réécriture, elle se poursuit pour permettre au service de traiter la réécriture du lien. Chaque fois qu’un lien est rencontré dans le code HTML interne, la méthode suivante est appelée :

`rewriteLink(String link, String tag, String attribute)`

En entrée, la méthode reçoit les paramètres suivants :

* `link`
Les 
`String` représentation du lien en cours de traitement. Il s’agit généralement d’une URL relative pointant vers la ressource sur l’instance de création.

* `tag`
Nom de l’élément HTML en cours de traitement.

* `attribute`
Nom exact de l’attribut.

Si, par exemple, le système Exporter vers Target traite actuellement cet élément, vous pouvez définir `CSSInclude` en tant que :

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

L’appel de la `rewriteLink()` méthode est effectué à l’aide des paramètres suivants :

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Lorsque vous créez le service, vous pouvez prendre des décisions en fonction de l’entrée indiquée, puis réécrire le lien en conséquence.

Dans notre exemple, nous souhaitons supprimer la partie `/etc.clientlibs` de l’URL et ajouter le domaine externe approprié. Pour simplifier les choses, nous partons du principe que nous avons accès à un résolveur de ressources pour le service, comme dans `rewriteLinkExample2` :

>[!NOTE]
>
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>Si la méthode ci-dessus renvoie `null`, le système Exporter vers Target laisse le lien tel quel, c’est-à-dire un lien relatif vers une ressource.

#### Priorités - getPriority {#priorities-getpriority}

Il n’est pas rare de devoir utiliser plusieurs services pour traiter différents types de fragments d’expérience, voire de disposer d’un service générique qui gère l’externalisation et le mappage pour tous les fragments d’expérience. Dans ce cas, des conflits peuvent survenir au niveau du service à utiliser. Aussi, AEM permet-il de définir des **priorités** pour différents services. Les priorités sont spécifiées en utilisant la méthode suivante :

* `getPriority()`

Cette méthode permet d’utiliser plusieurs services pour lesquels la méthode `shouldRewrite()` renvoie la valeur « true » pour le même fragment d’expérience. Le service qui renvoie la valeur la plus élevée à partir de sa méthode `getPriority()` est celui qui traite la variation du fragment d’expérience.

Par exemple, un `GenericLinkRewriterProvider` peut gérer le mappage de base pour tous les fragments d’expérience et lorsque la méthode `shouldRewrite()` renvoie `true` pour toutes les variations du fragment d’expérience. Pour plusieurs fragments d’expérience spécifiques, une gestion spéciale peut être souhaitable. Dans ce cas, vous pouvez donc fournir un `SpecificLinkRewriterProvider` pour lequel la méthode `shouldRewrite()` ne renvoie la valeur « true » que pour certaines variations du fragment d’expérience. Pour s’assurer que `SpecificLinkRewriterProvider` est choisi pour traiter ces variations du fragment d’expérience, il doit renvoyer dans sa méthode `getPriority()` un nombre supérieur à `GenericLinkRewriterProvider.`
