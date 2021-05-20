---
title: Événements OSGi pour les composants Communities
seo-title: Événements OSGi pour les composants Communities
description: Les événements OSGi sont envoyés et peuvent déclencher des écouteurs asynchrones.
seo-description: Les événements OSGi sont envoyés et peuvent déclencher des écouteurs asynchrones.
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 5%

---

# Événements OSGi pour les composants Communities {#osgi-events-for-communities-components}

## Présentation {#overview}

Lorsque les membres interagissent avec les fonctionnalités de Communities, des événements OSGi sont envoyés, qui peuvent déclencher des écouteurs asynchrones, tels que des notifications ou des jeux vidéo (notation et badge).

L’instance [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) d’un composant enregistre les événements sous la forme `actions` qui se produisent pour une balise `topic`. SocialEvent inclut une méthode pour renvoyer une `verb` associée à l’action. Il existe une relation *n-1* entre `actions` et `verbs`.

Pour les composants Communities fournis dans la version, les tableaux suivants décrivent les `verbs` définis pour chaque `topic` disponible à utiliser.

## Sujets et verbes {#topics-and-verbs}

[Calendrier ](calendar-basics-for-developers.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/calendar

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un événement de calendrier |
| AJOUTER | Commentaires des membres sur un événement de calendrier |
| UPDATE | L’événement ou le commentaire de calendrier du membre est modifié. |
| DELETE | L’événement ou le commentaire de calendrier du membre est supprimé. |

[Comments ](essentials-comments.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/comment

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un commentaire |
| AJOUTER | Réponses des membres au commentaire |
| UPDATE | Le commentaire du membre est modifié |
| DELETE | Le commentaire du membre est supprimé. |

[File Library ](essentials-file-library.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/fileLibrary

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un dossier |
| ATTACH | Le membre charge un fichier |
| UPDATE | Le membre met à jour un dossier ou un fichier |
| DELETE | Le membre supprime un dossier ou un fichier |

[Forum ](essentials-forum.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/forum

| **Verbe** | **Description** |
|---|---|
| POST | Rubrique de forum créée par un membre |
| AJOUTER | Réponses des membres au sujet du forum |
| UPDATE | Le sujet ou la réponse du forum du membre est modifié |
| DELETE | Suppression de la rubrique ou de la réponse du forum du membre |

[Journal ](blog-developer-basics.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/journal

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un article de blog. |
| AJOUTER | Commentaires des membres sur un article de blog |
| UPDATE | Article ou commentaire du blog du membre modifié |
| DELETE | L’article ou le commentaire du blog du membre est supprimé. |

[Q&amp;R ](qna-essentials.md)
ComponentSocialEvent  `topic` = com/adobe/cq/social/qna

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée une question Q&amp;R |
| AJOUTER | Un membre crée une réponse Q&amp;R |
| UPDATE | Question ou réponse Q&amp;R du membre modifié |
| SELECT | La réponse du membre est sélectionnée |
| UNSELECT | La réponse du membre est désélectionnée |
| DELETE | Question ou réponse Q&amp;R du membre supprimée |

[Révisions ](reviews-basics.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/review

| **Verbe** | **Description** |
|---|---|
| POST | Création d’une révision par membre |
| UPDATE | La révision du membre est modifiée. |
| DELETE | La révision du membre est supprimée |

[Évaluation ](rating-basics.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/tally

| **Verbe** | **Description** |
|---|---|
| AJOUTER UNE NOTE | Le contenu du membre a été noté |
| SUPPRESSION DE LA NOTE | Le contenu du membre a été abaissé. |

[Vote ](essentials-voting.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/tally

| **Verbe** | **Description** |
|---|---|
| AJOUTER UN VOTE | Le contenu du membre a été voté |
| SUPPRIMER LE VOTE | Le contenu du membre a été rejeté |

****
Composants activés pour la modérationSocialEvent  `topic`= com/adobe/cq/social/modération

| **Verbe** | **Description** |
|---|---|
| DENY | Le contenu du membre est refusé |
| INDICATEUR INAPPROPRIÉ | Le contenu du membre est marqué |
| INAPPROPRIÉ | Le contenu du membre n’est pas marqué |
| ACCEPT | Le contenu du membre est approuvé par le modérateur |
| CLOSE | Le membre ferme le commentaire aux modifications et aux réponses |
| OUVRIR | Commentaire de réouverture de membre |

## Événements pour les composants personnalisés {#events-for-custom-components}

Pour un composant personnalisé, la [classe abstraite SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) doit être étendue d pour enregistrer les événements du composant comme `actions`qui se produisent pour un `topic`.

L’événement personnalisé remplace la méthode `getVerb()` de sorte qu’une valeur `verb`appropriée soit renvoyée pour chaque `action`. La valeur `verb` renvoyée pour une action peut être couramment utilisée (telle que `POST`) ou spécialisée pour le composant (telle que `ADD RATING`). Il existe une relation *n-1* entre `actions`et `verbs`.

>[!NOTE]
>
>Assurez-vous qu’une extension personnalisée est enregistrée avec un classement inférieur à toute implémentation existante dans le produit.

### Pseudo-code pour l’événement de composant personnalisé {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html); 
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html); 
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html); 
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

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

## Exemple d’écouteur d’événement pour filtrer les données du flux d’activités {#sample-eventlistener-to-filter-activity-stream-data}

Il est possible d’écouter les événements dans le but de modifier ce qui apparaît dans le flux d’activité.

L’exemple de pseudo-code suivant supprime les événements DELETE du composant Commentaires du flux d’activités.

### Pseudo-code pour EventListener {#pseudo-code-for-eventlistener}

Nécessite [le dernier Feature Pack](deploy-communities.md#latestfeaturepack).

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
