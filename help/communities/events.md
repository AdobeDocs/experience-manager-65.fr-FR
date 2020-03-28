---
title: OSGi pour les composants de communautés
seo-title: OSGi pour les composants de communautés
description: Les  OSGi sont envoyées et peuvent déclencher des écouteurs asynchrones.
seo-description: Les  OSGi sont envoyées et peuvent déclencher des écouteurs asynchrones.
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# OSGi pour les composants de communautés {#osgi-events-for-communities-components}

## Présentation {#overview}

Lorsque les membres interagissent avec les fonctionnalités des communautés, des  OSGi sont envoyées, ce qui peut déclencher des écouteurs asynchrones, tels que des notifications ou des gamification (score et badge).

L’instance [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) d’un composant enregistre le  de comme `actions` cela se produit pour une `topic`instance. SocialEvent inclut une méthode pour renvoyer une `verb` associée à l’action. Il existe une relation *n-1* entre `actions` et `verbs`.

Pour les composants Communities livrés dans la version, les tableaux suivants décrivent la `verbs` définition pour chaque `topic` utilisation disponible.

## Rubriques et verbes {#topics-and-verbs}

[Composant](calendar-basics-for-developers.md)Calendrier SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbe** | **Description** |
|---|---|
| POST | crée un de calendrier  |
| AJOUTER | commentaires d’un membre sur un de calendrier  |
| UPDATE | le de calendrier ou le commentaire du membre est modifié |
| DELETE | le de calendrier ou le commentaire du membre est supprimé |

[Composant](essentials-comments.md)de commentaires SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbe** | **Description** |
|---|---|
| POST | crée un commentaire |
| AJOUTER | les réponses du membre au commentaire |
| UPDATE | le commentaire du membre est modifié. |
| DELETE | commentaire du membre supprimé |

[Composant](essentials-file-library.md)de bibliothèque de fichiers SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbe** | **Description** |
|---|---|
| POST | crée un dossier |
| ATTAQUE | le membre télécharge un fichier |
| UPDATE | met à jour un dossier ou un fichier |
| DELETE | supprime un dossier ou un fichier |

[Composant](essentials-forum.md)du forum SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbe** | **Description** |
|---|---|
| POST | membre crée une rubrique de forum |
| AJOUTER | réponses des membres au sujet du forum |
| UPDATE | Le sujet ou la réponse du membre du forum est modifié |
| DELETE | Le sujet ou la réponse du membre du forum est supprimé |

[Composant](blog-developer-basics.md)de SocialEvent `topic`= com/adobe/cq/social/

| **Verbe** | **Description** |
|---|---|
| POST | crée un article de blog |
| AJOUTER | commentaires d&#39;un membre sur un article de blog |
| UPDATE | l’article ou le commentaire du blog du membre est modifié. |
| DELETE | article ou commentaire de blog du membre supprimé |

[Composant](qna-essentials.md)QA SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbe** | **Description** |
|---|---|
| POST | crée une question QnA |
| AJOUTER | crée une réponse QnA |
| UPDATE | QnUne question ou une réponse du membre est modifiée |
| SELECT | la réponse du membre est sélectionnée |
| DÉSÉLECTIONNER | la réponse du membre est désélectionnée |
| DELETE | QnUne question ou une réponse du membre est supprimée |

[Composant](reviews-basics.md)Révisions SocialEvent `topic`= com/adobe/cq/social/review

| **Verbe** | **Description** |
|---|---|
| POST | membre crée une révision |
| UPDATE | révision du membre est modifiée |
| DELETE | la révision du membre est supprimée |

[Composant](rating-basics.md)de notation SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbe** | **Description** |
|---|---|
| AJOUTER | le contenu du membre a été amélioré |
| SUPPRIMER LA COTE | le contenu du membre a été mal évalué |

[Composant](essentials-voting.md)de vote SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbe** | **Description** |
|---|---|
| AJOUTER VOTE | le contenu du membre a été voté |
| SUPPRIMER LE VOTE | le contenu du membre a été rejeté |

**Composants** SocialEvent prenant en charge la modération `topic`= com/adobe/cq/social/modération

| **Verbe** | **Description** |
|---|---|
| DENY | le contenu du membre est refusé |
| INDICATEUR COMME INAPPROPRIÉ | le contenu du membre est marqué |
| INAPPROPRIÉ | le contenu du membre n’est pas marqué |
| ACCEPTER | le contenu du membre est approuvé par le modérateur |
| CLOSE | le membre ferme les commentaires aux modifications et aux réponses |
| OUVRIR | commentaire de réouverture du membre |

##  pour les composants personnalisés {#events-for-custom-components}

Pour un composant personnalisé, la classe [abstraite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) SocialEvent doit être étendue d pour enregistrer le  du composant comme `actions`cela se produit pour un `topic`composant.

Le personnalisé remplacerait la méthode `getVerb()` de sorte qu’une valeur appropriée `verb`soit renvoyée pour chaque `action`élément. Le `verb` retour d’une action peut être un élément couramment utilisé ( `POST`) ou spécialisé pour le composant ( `ADD RATING`). Il existe une relation *n-1* entre `actions`et `verbs`.

>[!NOTE]
>
>Assurez-vous qu’une extension personnalisée est enregistrée avec un rang inférieur à toute implémentation existante dans le produit.

### pseudo-code pour le de composants personnalisés {#pseudo-code-for-custom-component-event}

[org.osgi.service..](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystream.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystream.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## Exemple d’écouteur d’événements à filtrer  données de flux {#sample-eventlistener-to-filter-activity-stream-data}

Il est possible d&#39;écouter les  de dans le but de modifier ce qui apparaît dans le flux  de l&#39;.

L’exemple de pseudo-code suivant supprime le DELETE pour le composant Comments du flux  de l’.

### pseudo-code pour EventListener {#pseudo-code-for-eventlistener}

Nécessite le [dernier pack](deploy-communities.md#latestfeaturepack)de fonctionnalités.

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```

