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

---


# Fragments d’expérience{#experience-fragments}

## Principes élémentaires {#the-basics}

Un [fragment d’expérience](/help/sites-authoring/experience-fragments.md) est un groupe d’un ou plusieurs composants comprenant un contenu et une disposition pouvant être référencés dans les pages.

Un maître et/ou une variante de fragment d’expérience utilise :

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Comme il n&#39;y en a pas `/libs/cq/experience-fragments/components/xfpage/xfpage.html` il revient à

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Rendu HTML brut {#the-plain-html-rendition}

Using the `.plain.` selector in the URL, you can access the plain HTML rendition.

Cela est possible à partir du navigateur. Cependant, le principal objectif consiste à autoriser d’autres applications (des applications web tierces et des implémentations mobiles personnalisées, par exemple) à accéder directement au contenu du fragment d’expérience en utilisant uniquement l’URL.

Le rendu HTML brut ajoute le protocole, l’hôte et le chemin d’accès au contexte à des chemins qui :

* du type: `src`, `href`ou `action`

* or end with: `-src`, or `-href`

Par exemple :

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Les liens font toujours référence à l’instance de publication. Ils sont destinés à être utilisés par des tiers, de sorte qu’ils soient toujours appelés à partir de l’instance de publication, et non de l’auteur.

![xf-14](assets/xf-14.png)

Le sélecteur de rendu brut utilise un transformateur plutôt que des scripts supplémentaires. le [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) est utilisé comme transformateur. Ceci est configuré à l’adresse

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variations sociales {#social-variations}

Les variantes de Social peuvent être publiées sur les réseaux sociaux (texte et image). Dans AEM, ces variantes sociales peuvent contenir des composants ; par exemple, les composants de texte, les composants d’image.

L’image et le texte de la publication sociale peuvent être extraits de n’importe quel type de ressource d’image ou de ressource de texte à n’importe quel niveau de profondeur (dans le bloc de création ou le conteneur de mise en page).

Les variations sociales permettent également de créer des blocs de création et de les prendre en compte lors de l’exécution d’actions sociales (dans l’environnement de publication).

Pour publier le texte et l’image appropriés sur le réseau de médias sociaux, certaines conventions doivent être respectées si vous développez vos propres composants personnalisés.

Pour ce faire, vous devez utiliser les propriétés suivantes :

* Pour extraire l’image

   * `fileReference`
   * `fileName`

* Pour extraire le texte

   * `text`

Les éléments qui n&#39;utilisent pas cette convention ne seront pas pris en considération.

## Modèles de fragments d’expérience {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Seuls*** les modèles [](/help/sites-developing/page-templates-editable.md) modifiables sont pris en charge pour les fragments d’expérience.

Lors du développement d’un nouveau modèle de fragments d’expérience, vous pouvez suivre les pratiques standard d’un modèle [](/help/sites-developing/page-templates-editable.md)modifiable.

Pour créer un modèle de fragment d’expérience détecté par l’assistant **Créer un fragment** d’expérience, vous devez suivre l’un des jeux de règles suivants :

1. les deux:

   1. Le type de ressource du modèle (le noeud initial) doit hériter de :
      `cq/experience-fragments/components/xfpage`

   1. Et le nom du modèle doit commencer par :
      `experience-fragments`
Cela permet aux utilisateurs de créer des fragments d’expérience dans /content/experience-fragments, car la `cq:allowedTemplates` propriété de ce dossier inclut tous les modèles dont le nom commence par `experience-fragment`. Les clients peuvent mettre à jour cette propriété pour inclure leur propre modèle de dénomination ou emplacement de modèle.

1. [Les modèles](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) autorisés peuvent être configurés dans la console Fragments d’expérience.
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Composants pour les fragments d’expérience {#components-for-experience-fragments}

[Le développement de composants](/help/sites-developing/components.md) à utiliser avec/dans les fragments d’expérience est conforme aux pratiques standard.

La seule configuration supplémentaire consiste à s’assurer que les composants sont [autorisés sur le modèle, ce qui se fait avec la stratégie](/help/sites-developing/page-templates-editable.md#content-policies)de contenu.

## Fournisseur de réécriture de liens de fragments d’expérience - HTML {#the-experience-fragment-link-rewriter-provider-html}

Dans AEM, vous avez la possibilité de créer des fragments d’expérience. Un fragment d’expérience :

* se compose d&#39;un groupe de composants et d&#39;une mise en page,
* peut exister indépendamment d’une page AEM.

L’un des cas d’utilisation de ces groupes consiste à incorporer du contenu dans des points de contact tiers, tels qu’Adobe Target.

### Réécriture de lien par défaut {#default-link-rewriting}

La fonction [Exporter vers Target](/help/sites-administering/experience-fragments-target.md) vous permet d’effectuer les opérations suivantes :

* créer un fragment d’expérience,
* y ajouter des composants,
* puis exportez-la en tant qu’offre Adobe Target, au format HTML ou JSON.

Cette fonctionnalité peut être [activée sur une instance d’auteur d’AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Il nécessite une configuration Adobe Target valide et des configurations pour l’Externalisateur de liens.

L’Externalisateur de liens permet de déterminer les URL appropriées nécessaires lors de la création de la version HTML de l’offre Target, qui est ensuite envoyée à Adobe Target. Cela est nécessaire car Adobe Target exige que tous les liens de l’offre HTML Target soient accessibles au public ; cela signifie que les ressources référencées par les liens et le fragment d’expérience lui-même doivent être publiées avant d’être utilisées.

Par défaut, lorsque vous créez une offre HTML Target, une requête est envoyée à un sélecteur Sling personnalisé dans AEM. Ce sélecteur est appelé `.nocloudconfigs.html`. Comme son nom l’indique, il crée un rendu HTML brut d’un fragment d’expérience, mais n’inclut pas les configurations de cloud (qui seraient des informations superflues).

Une fois la page HTML générée, le pipeline Sling Rewriter modifie la sortie :

1. Les éléments `html`, `head`et `body` sont remplacés par `div` des éléments. Les éléments `meta`, `noscript` et `title` sont supprimés (il s’agit d’éléments enfants de l’ `head` élément d’origine et ne sont pas pris en compte lorsque cet élément est remplacé par l’ `div` élément).

   Cela permet de s’assurer que l’offre Target HTML peut être incluse dans les activités Target.

1. AEM modifie tous les liens internes présents dans le code HTML afin qu’ils pointent vers une ressource publiée.

   Pour déterminer les liens à modifier, AEM suit ce modèle pour les attributs des éléments HTML :

   1. `src` attributs
   1. `href` attributs
   1. `*-src` attributs (comme data-src, custom-src, etc.)
   1. `*-href` attributs (comme `data-href`, `custom-href`, `img-href`, etc.)
   >[!NOTE]
   >
   >Dans la plupart des cas, les liens internes du code HTML sont des liens relatifs, mais il peut arriver que des composants personnalisés fournissent des URL complètes dans le code HTML. Par défaut, AEM ignore ces URL complètes et n’effectue aucune modification.

   Les liens de ces attributs sont exécutés via l’Externalisateur de liens AEM `publishLink()` afin de recréer l’URL comme s’il se trouvait sur une instance publiée et, de ce fait, disponible au public.

Lors de l’utilisation d’une implémentation prête à l’emploi, le processus décrit ci-dessus doit être suffisant pour générer l’offre Target à partir du fragment d’expérience, puis l’exporter vers Adobe Target. Toutefois, certains cas d&#39;utilisation ne sont pas pris en compte dans ce processus; il s’agit notamment des suivantes :

* Mappage Sling disponible uniquement sur l’instance de publication
* Redirections du répartiteur

Pour ces cas d’utilisation, AEM fournit l’interface du fournisseur de réécrivain de liens.

### Interface du fournisseur de réscripteur de liens {#link-rewriter-provider-interface}

>[!NOTE]
>
>Cette interface a été introduite dans [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/sp-release-notes.md).

Pour les cas plus complexes, non couverts par la [valeur par défaut](#default-link-rewriting), AEM offre l’interface du fournisseur de réécriture de liens. Il s’agit d’une `ConsumerType` interface que vous pouvez implémenter dans vos lots, en tant que service. Il contourne les modifications qu’AEM effectue sur les liens internes d’une offre HTML tel qu’il est généré à partir d’un fragment d’expérience. Cette interface vous permet de personnaliser le processus de réécriture des liens HTML internes pour l’aligner sur vos besoins.

Voici quelques exemples d’utilisation de cette interface en tant que service :

* Les mappages Sling sont activés sur les instances de publication, mais pas sur l’instance d’auteur.
* Un répartiteur ou une technologie similaire est utilisé pour rediriger les URL en interne.
* Il existe `sling:alias mechanisms` des ressources

>[!NOTE]
>
>Cette interface traite uniquement les liens HTML internes de l’offre Target générée.

L’interface du fournisseur de réécriture de liens ( `ExperienceFragmentLinkRewriterProvider`) est la suivante :

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Utilisation de l’interface du fournisseur de réécriture de liens {#how-to-use-the-link-rewriter-provider-interface}

Pour utiliser l’interface, vous devez d’abord créer un lot contenant un nouveau composant de service qui implémente l’interface du fournisseur de réécriture de liens.

Ce service sera utilisé pour se connecter à la réécriture Exportation de fragments d’expérience vers Target afin d’avoir accès aux différents liens.

Par exemple, `ComponentService`:

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

Pour que le service fonctionne, trois méthodes doivent être implémentées au sein du service :

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Vous devez indiquer au système s’il doit réécrire les liens lorsqu’un appel est lancé pour Exporter vers Target sur une certaine variation de fragment d’expérience. Pour ce faire, implémentez la méthode suivante :

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Par exemple :

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Cette méthode reçoit, en tant que paramètre, la variation du fragment d’expérience que le système Exporter vers Target est en cours de réécriture.

Dans l&#39;exemple ci-dessus, nous aimerions réécrire :

* liens présents dans `src`

* `href` attributs uniquement

* pour un fragment d’expérience spécifique :
   `/content/experience-fragment/master`

Les autres fragments d’expérience qui passent par le système Exporter vers Target sont ignorés et ne sont pas affectés par les modifications implémentées dans ce service.

#### rewriteLink {#rewritelink}

Pour la variation du fragment d’expérience affectée par le processus de réécriture, elle se poursuivra pour permettre au service de gérer la réécriture du lien. Chaque fois qu’un lien est rencontré dans le code HTML interne, la méthode suivante est appelée :

`rewriteLink(String link, String tag, String attribute)`

En entrée, la méthode reçoit les paramètres :

* `link`
Représentation `String` du lien en cours de traitement. Il s’agit généralement d’une URL relative pointant vers la ressource de l’instance d’auteur.

* `tag`
Nom de l’élément HTML en cours de traitement.

* `attribute`
Nom exact de l’attribut.

Si, par exemple, le système Exporter vers Target traite actuellement cet élément, vous pouvez définir `CSSInclude` :

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

L’appel à la `rewriteLink()` méthode est effectué à l’aide des paramètres suivants :

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Lorsque vous créez le service, vous pouvez prendre des décisions en fonction de l’entrée donnée, puis réécrire le lien en conséquence.

Dans notre exemple, nous souhaitons supprimer la `/etc.clientlibs` partie de l’URL et ajouter le domaine externe approprié. Pour simplifier les choses, nous considérons que nous avons accès à un Resource Resolver pour votre service, comme dans `rewriteLinkExample2`:

>[!NOTE]
>
>Pour plus d’informations sur la manière d’obtenir un résolveur de ressources par l’intermédiaire d’un utilisateur de service, voir Utilisateurs [de service dans AEM](/help/sites-administering/security-service-users.md).

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
>Si la méthode ci-dessus renvoie `null`, le système Exporter vers Target laisse le lien tel quel, un lien relatif vers une ressource.

#### Priorités - getPriority {#priorities-getpriority}

Il n’est pas rare que vous ayez besoin de plusieurs services pour traiter différents types de fragments d’expérience, ou même d’un service générique qui gère l’externalisation et le mappage pour tous les fragments d’expérience. Dans ces cas, des conflits sur le service à utiliser peuvent survenir. AEM permet donc de définir des **priorités** pour différents services. Les priorités sont spécifiées à l’aide de la méthode suivante :

* `getPriority()`

Cette méthode permet d’utiliser plusieurs services pour lesquels la `shouldRewrite()` méthode renvoie true pour le même fragment d’expérience. Le service qui renvoie le nombre le plus élevé de sa `getPriority()`méthode est le service qui traite la variation du fragment d’expérience.

Par exemple, vous pouvez avoir un `GenericLinkRewriterProvider` gestionnaire qui gère le mappage de base pour tous les fragments d’expérience et lorsque la `shouldRewrite()` méthode renvoie `true` pour toutes les variantes de fragments d’expérience. Pour plusieurs fragments d’expérience spécifiques, vous souhaiterez peut-être une gestion spéciale. Dans ce cas, vous pouvez donc fournir un `SpecificLinkRewriterProvider` pour lequel la `shouldRewrite()` méthode renvoie la valeur true uniquement pour certaines variantes de fragments d’expérience. Pour s’assurer que `SpecificLinkRewriterProvider` vous avez choisi de gérer ces variations de fragment d’expérience, il doit renvoyer dans sa `getPriority()` méthode un nombre supérieur à `GenericLinkRewriterProvider.`
