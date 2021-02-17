---
title: Mise en œuvre d’un évaluateur de prédicat personnalisé pour Query Builder.
seo-title: Mise en œuvre d’un évaluateur de prédicat personnalisé pour Query Builder.
description: Query Builder offre un moyen simple pour effectuer des requêtes sur le référentiel de contenu.
seo-description: Query Builder offre un moyen simple pour effectuer des requêtes sur le référentiel de contenu.
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 93%

---


# Mise en œuvre d’un évaluateur de prédicat personnalisé pour Query Builder{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Cette section décrit comment étendre [Query Builder](/help/sites-developing/querybuilder-api.md) en mettant en œuvre un évaluateur de prédicat personnalisé.

## Présentation {#overview}

[Query Builder](/help/sites-developing/querybuilder-api.md) offre un moyen simple pour effectuer des requêtes sur le référentiel de contenu. CQ est livré avec un ensemble d’évaluateurs de prédicats qui vous aide à traiter vos données.

Toutefois, vous pouvez simplifier vos requêtes en mettant en œuvre un évaluateur de prédicat personnalisé qui masque une partie de la complexité et assure une meilleure sémantique.

Un prédicat personnalisé peut également réaliser d’autres actions qui ne sont pas directement possibles avec XPath, par exemple :

* Recherche de certaines données d’un service donné
* Filtrage personnalisé basé sur le calcul

>[!NOTE]
>
>Les problèmes de performances doivent être pris en compte lors de la mise en œuvre d’un prédicat personnalisé.

>[!NOTE]
>
>Vous trouverez des exemples de requêtes dans la section [Query Builder](/help/sites-developing/querybuilder-api.md).

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-search-custom-predicate-evaluator sur GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip).

### L’évaluateur de prédicat en détail {#predicate-evaluator-in-detail}

Un évaluateur gère l’évaluation de certains prédicats qui constituent les contraintes définissant une requête.

Il mappe une contrainte de recherche de plus haut niveau (par exemple, « width > 200 ») sur une requête JCR spécifique qui est adaptée au modèle de contenu actuel (par exemple, metadata/@width > 200). Il peut également filtrer manuellement les nœuds et vérifier leurs contraintes.

>[!NOTE]
>
>Pour plus d’informations sur `PredicateEvaluator` et le module `com.day.cq.search`, voir la [documentation Java](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html).

### Mise en œuvre d’un évaluateur de prédicat personnalisé pour les métadonnées de réplication {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

En guise d’illustration, cette section décrit comment créer un évaluateur de prédicat personnalisé qui aide à évaluer les données en fonction des métadonnées de réplication :

* `cq:lastReplicated` qui stocke la date de la dernière action de réplication.

* `cq:lastReplicatedBy` qui stocke l’ID de l’utilisateur qui a déclenché la dernière action de réplication.

* `cq:lastReplicationAction` qui stocke la dernière action de réplication (par exemple, activation ou désactivation).

#### Requête sur les métadonnées de réplication avec les évaluateurs de prédicats par défaut {#querying-replication-metadata-with-default-predicate-evaluators}

La requête suivante récupère la liste des nœuds dans la branche `/content` qui a été activée par `admin` depuis le début de l’année.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Cette requête est valide, mais peu lisible et ne met pas en évidence la relation entre les trois propriétés de réplication. La mise en œuvre d’un évaluateur de prédicat personnalisé réduit la complexité et améliore la sémantique de cette requête.

#### Objectifs {#objectives}

L’objectif de `ReplicationPredicateEvaluator` consiste à prendre en charge la requête ci-dessus à l’aide de la syntaxe ci-après.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Le regroupement des prédicats de métadonnées de réplication avec un évaluateur de prédicat personnalisé permet de créer une requête pertinente.

#### Mise à jour des dépendances Maven {#updating-maven-dependencies}

>[!NOTE]
>
>La configuration de nouveaux projets AEM à l’aide de Maven est décrite dans [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).

Tout d’abord, vous devez mettre à jour les dépendances Maven de votre projet. `PredicateEvaluator` fait partie de l’artefact `cq-search` et doit donc être ajouté à votre fichier pom Maven.

>[!NOTE]
>
>La portée de la dépendance `cq-search` est définie sur `provided`, car `cq-search` sera fourni par le conteneur `OSGi`.

pom.xml

Le fragment de code suivant montre les différences, au [format diff unifié](https://fr.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

[aem-search-custom-prédicate-évaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)-  [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### Écriture de ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

Le projet `cq-search` contient la classe abstraite `AbstractPredicateEvaluator`. Il est possible d’améliorer cela moyennant quelques étapes pour mettre en œuvre votre évaluateur de prédicat personnalisé `(PredicateEvaluator`).

>[!NOTE]
>
>La procédure suivante explique comment créer une expression `Xpath` afin de filtrer des données. Une autre option consisterait à mettre en œuvre la méthode `includes` qui sélectionne les données sur la base de la ligne. Pour plus d’informations, voir la [documentation Java](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29).

1. Créez une classe Java qui étend `com.day.cq.search.eval.AbstractPredicateEvaluator`.
1. Annotez votre classe avec un `@Component` comme suit :

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   Le fragment de code suivant montre les différences, au [format diff unifié](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -19,8 +19,11 @@
  */
 package com.adobe.aem.docs.search;

+import org.apache.felix.scr.annotations.Component;
+
 import com.day.cq.search.eval.AbstractPredicateEvaluator;

+@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
 public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

 }
```

[aem-search-custom-prédicate-évaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)-  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>La `factory` doit être une chaîne unique commençant par `com.day.cq.search.eval.PredicateEvaluator/` et se terminant par le nom de votre `PredicateEvaluator` personnalisé.

>[!NOTE]
>
>Le nom de `PredicateEvaluator` est le nom du prédicat, qui est utilisé pour créer des requêtes.

1. Remplacement :

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   Avec la méthode de remplacement, vous créez une expression `Xpath` basée sur le `Predicate` fourni comme argument.

### Exemple d’évaluateur de prédicat personnalisé pour les métadonnées de réplication {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

La mise en œuvre complète de ce `PredicateEvaluator` peut être semblable à la classe suivante.

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```

[aem-search-custom-prédicate-évaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)-  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
