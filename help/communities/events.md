---
title: Composants des Événements OSGi pour les communautés
seo-title: Composants des Événements OSGi pour les communautés
description: Les événements OSGi sont envoyés et peuvent déclencher des écouteurs asynchrones.
seo-description: Les événements OSGi sont envoyés et peuvent déclencher des écouteurs asynchrones.
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 5%

---


# Composants des Événements OSGi pour les communautés  {#osgi-events-for-communities-components}

## Présentation {#overview}

Lorsque les membres interagissent avec les fonctionnalités des communautés, des événements OSGi sont envoyés, ce qui peut déclencher des écouteurs asynchrones, tels que des notifications ou une gamification (score et badge).

L’instance [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) d’un composant enregistre les événements comme `actions` ceux qui se produisent pour un `topic`composant. SocialEvent comprend une méthode permettant de renvoyer une `verb` variable associée à l’action. Il y a une relation *n-1* entre `actions` et `verbs`.

Pour les composants Communities fournis dans la version, les tableaux suivants décrivent la `verbs` définition pour chaque `topic` composant disponible à utiliser.

## Rubriques et verbes {#topics-and-verbs}

[Composant](calendar-basics-for-developers.md)Calendrier SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un événement de calendrier |
| AJOUTER | Commentaires des membres sur un événement de calendrier |
| UPDATE | Le événement de calendrier ou le commentaire du membre est modifié |
| DELETE | Le événement de calendrier ou le commentaire du membre est supprimé |

[Composant](essentials-comments.md)Commentaires SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un commentaire |
| AJOUTER | Réponses du membre au commentaire |
| UPDATE | Le commentaire du membre est modifié. |
| DELETE | Le commentaire du membre est supprimé |

[Composant](essentials-file-library.md)de bibliothèque de fichiers SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un dossier |
| ATTAQUE | Le membre télécharge un fichier |
| UPDATE | Le membre met à jour un dossier ou un fichier |
| DELETE | Le membre supprime un dossier ou un fichier |

[Composant](essentials-forum.md)du forum SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbe** | **Description** |
|---|---|
| POST | Le membre crée une rubrique de forum |
| AJOUTER | Réponses des membres au sujet du forum |
| UPDATE | Le sujet ou la réponse du membre sur le forum est modifié |
| DELETE | Le sujet ou la réponse du membre sur le forum est supprimé |

[Composant](blog-developer-basics.md)journal SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un article de blog |
| AJOUTER | Commentaires d&#39;un membre sur un article de blog |
| UPDATE | L&#39;article ou le commentaire du blog du membre est modifié |
| DELETE | L&#39;article ou le commentaire du blog du membre est supprimé |

[Composant](qna-essentials.md)QnA SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée une question QnA |
| AJOUTER | Un membre crée une réponse QnA |
| UPDATE | Question ou réponse QnA du membre modifiée |
| SELECT | La réponse du membre est sélectionnée |
| DÉSÉLECTIONNER | La réponse du membre est désélectionnée |
| DELETE | Question ou réponse QnA du membre supprimée |

[Composant](reviews-basics.md)de révision SocialEvent `topic`= com/adobe/cq/social/review

| **Verbe** | **Description** |
|---|---|
| POST | Le membre crée une révision |
| UPDATE | La révision du membre est modifiée. |
| DELETE | La révision du membre est supprimée |

[Composant](rating-basics.md)de notation SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbe** | **Description** |
|---|---|
| AJOUTE | Le contenu du membre a été amélioré |
| SUPPRESSION DE LA COTE | Le contenu du membre a été abaissé |

[Composant](essentials-voting.md)de vote SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbe** | **Description** |
|---|---|
| AJOUTER VOTE | Le contenu du membre a été voté |
| SUPPRIMER LE VOTE | Le contenu du membre a été rejeté |

**Composants** SocialEvent prenant en charge la modération `topic`= com/adobe/cq/social/modération

| **Verbe** | **Description** |
|---|---|
| DENY | Le contenu du membre est refusé |
| INDICATEUR INAPPROPRIÉ | Le contenu du membre est marqué |
| INAPPROPRIÉ | Le contenu du membre n&#39;est pas marqué |
| ACCEPTER | Le contenu du membre est approuvé par le modérateur |
| CLOSE | Le membre ferme les commentaires aux modifications et aux réponses |
| OUVRIR | Commentaire de réouverture du membre |

## Événements pour les composants personnalisés {#events-for-custom-components}

Pour un composant personnalisé, la classe [abstraite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) SocialEvent doit être étendue d pour enregistrer les événements du composant comme `actions`cela se produit pour un `topic`composant.

Le événement personnalisé remplacerait la méthode `getVerb()` afin qu’un paramètre approprié `verb`soit renvoyé pour chaque `action`méthode. L&#39; `verb` action renvoyée peut être couramment utilisée (par exemple `POST`) ou spécialisée pour le composant (par exemple `ADD RATING`). Il existe une relation *n-1* entre `actions`et `verbs`.

>[!NOTE]
>
>Assurez-vous qu’une extension personnalisée est enregistrée avec un classement inférieur à toute implémentation existante dans le produit.

### Code pseudo pour le Événement de composants personnalisés {#pseudo-code-for-custom-component-event}

[org.osgi.service.événement.Événement](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
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

## Exemple d&#39;écouteur d&#39;événement pour filtrer les données du flux d&#39;Activité {#sample-eventlistener-to-filter-activity-stream-data}

Il est possible d&#39;écouter les événements dans le but de modifier ce qui apparaît dans le flux d&#39;activité.

L&#39;exemple de pseudo-code suivant supprime les événements DELETE pour le composant Commentaires du flux d&#39;activité.

### Pseudo-code pour EventListener {#pseudo-code-for-eventlistener}

Requiert le [dernier pack de fonctionnalités](deploy-communities.md#latestfeaturepack).

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

