---
title: Tableaux de bord
description: Découvrez comment créer, configurer et développer de nouveaux tableaux de bord AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 100%

---

# Tableaux de bord{#dashboards}

Lorsque vous utilisez AEM, vous pouvez gérer de nombreux contenus de différents types (par exemple, des pages ou des ressources). Les tableaux de bord AEM offrent un moyen simple et personnalisable de définir des pages qui affichent des données consolidées.

>[!NOTE]
>
>Les tableaux de bord AEM sont créés par utilisateur ou utilisatrice, de sorte qu’un utilisateur ou une utilisatrice ne peut accéder qu’à son propre tableau de bord.
>
>Cependant, les [modèles de tableau de bord](#creating-a-dashboard-template) peuvent être utilisés pour créer une disposition et une configuration commune à tous les de tableaux de bord.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Administration des tableaux de bord {#administering-dashboards}

### Création d’un tableau de bord {#creating-a-dashboard}

1. Dans la section **Outils**, cliquez sur **Console de configuration**.
1. Dans l’arborescence, double-cliquez sur **Tableau de bord**.
1. Cliquez sur **Nouveau tableau de bord**.
1. Saisissez le **Titre** (Mon tableau de bord, par exemple) et le **Nom**.
1. Cliquez sur **Créer**.

### Clonage d’un tableau de bord {#cloning-a-dashboard}

Vous pouvez, si vous le souhaitez, disposer de plusieurs tableaux de bord afin de consulter rapidement des informations sur votre contenu depuis différentes vues. Pour faciliter la création d’un tableau de bord, AEM propose une fonctionnalité de clonage que vous pouvez utiliser pour dupliquer un tableau de bord existant. Pour cloner un tableau de bord, procédez comme suit :

1. Dans la section **Outils**, cliquez sur **Console de configuration**.

1. Dans l’arborescence, cliquez sur **Tableau de bord**.
1. Cliquez sur le tableau de bord que vous souhaitez cloner.

1. Cliquez sur **Cloner**.

1. Saisissez le **Nom** de votre nouveau tableau de bord.

### Suppression d’un tableau de bord {#removing-a-dashboard}

1. Dans la section **Outils**, cliquez sur **Console de configuration**.

1. Dans l’arborescence, cliquez sur **Tableau de bord**.
1. Cliquez sur le tableau de bord à supprimer.

1. Cliquez sur **Supprimer**.

1. Cliquez sur **Oui** pour confirmer.

## Composants de tableau de bord {#dashboard-components}

### du commerce électronique {#overview}

Les composants de tableau de bord ne sont rien de plus que des [composants AEM](/help/sites-developing/developing-components-samples.md) standard. Cette section décrit les composants de rapport fournis avec AEM.

### Composants de rapport web analytics {#web-analytics-reporting-components}

AEM est fourni avec un ensemble de composants qui effectuent le rendu de plusieurs mesures de vos données [SiteCatalyst](/help/sites-administering/adobeanalytics.md). Ces composants sont répertoriés dans le sidekick, dans la section **Tableau de bord**.

Chaque composant de rapport comporte au moins trois onglets :

* **De base** : contient la configuration principale.

* **Rapport :** contient la configuration propre à chaque rapport.
* **Style :** contient la configuration du style, telle que la taille et la marge du graphique.

Les composants de rapport sont initialisés avec une configuration par défaut qui vous permet de configurer rapidement votre tableau de bord.

#### Configuration de base {#basic-configuration}

L’onglet **De base** donne accès aux entrées de configuration suivantes :

**Titre** - Titre affiché sur le tableau de bord.

**Type de requête** - Méthode de demande des données.

**Options de configuration** - Configuration à utiliser pour se connecter à SiteCatalyst. En l’absence de configuration, on suppose qu’elle est configurée sur la page Tableau de bord (via les propriétés de page).

**Identifiant de suite de rapports (facultatif)** Suite de rapports de SiteCatalyst que vous souhaitez utiliser pour générer le graphique.

#### Configuration de rapport {#report-configuration}

Pour pouvoir afficher des statistiques web, vous devez définir la période des données à récupérer. L’onglet **Rapport** fournit deux champs pour définir cette plage.

>[!NOTE]
>
>La définition d’une période étendue peut diminuer la réactivité du tableau de bord.

**Date à partir de** - Date absolue ou relative à partir de laquelle les données sont récupérées.

**Date jusque** - Date absolue ou relative jusqu’à laquelle les données sont récupérées.

Chaque composant définit également des paramètres spécifiques.

#### Rapport sur toute la durée {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Granularité de la date** : unité de temps de l’axe X (jour ou heure, par exemple).

**Mesures** - Liste des événements à afficher.

**Éléments** - Liste d’éléments qui répartit les données de mesure dans le graphique.

#### Rapport de liste avec classement {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**Éléments** - L’élément qui répartit les données de mesure dans le graphique.

**Mesures** L’événement que vous souhaitez afficher.

**Nombre des principaux éléments** Nombre d’éléments affichés par le rapport.

#### Rapport de classement {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**Mesures** L’événement que vous souhaitez afficher.

**Éléments** L’élément qui répartit les données de mesure dans le graphique.

#### Rapport de section du site supérieur {#top-site-section-report}

Ce composant affiche un graphique présentant la section la plus visitée d’un site web selon la configuration suivante.

![chlimage_1-29](assets/chlimage_1-29a.png)

**Nombre des principaux éléments** Nombre de sections affichées par le rapport.

#### Rapport de tendances {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Granularité de la date** : unité de temps de l’axe X (jour ou heure, par exemple).

**Mesures** L’événement que vous souhaitez afficher.

**Éléments** L’élément qui répartit les données de mesure dans le graphique.

## Étendre le tableau de bord {#extending-dashboard}

### du commerce électronique {#overview-1}

Les tableaux de bord sont des pages normales (`cq:Page`). N’importe quel composant peut donc être utilisé pour les assembler.

Un groupe de composants par défaut, `Dashboard`, contient les composants de génération de rapports d’analyse activés par défaut sur le modèle.

### Créer un modèle de tableau de bord {#creating-a-dashboard-template}

Un modèle définit le contenu par défaut d’un nouveau tableau de bord. Vous pouvez utiliser plusieurs modèles pour créer différents types de tableaux de bord.

Ces modèles sont créés de la même manière que les autres modèles de page, si ce n’est qu’ils sont stockés sous `/libs/cq/dashboards/templates/`. Consultez [Création d’un modèle Contentpage](/help/sites-developing/website.md#creating-the-contentpage-template).

>[!NOTE]
>
>Les modèles de tableau de bord sont partagés entre les utilisateurs et utilisatrices.

### Développer un composant Tableau de bord {#developing-a-dashboard-component}

Le développement d’un composant Tableau de bord consiste à créer un composant AEM ordinaire. Cette section décrit un exemple de composant qui affiche les 10 premières personnes contributrices.

![chlimage_1-31](assets/chlimage_1-31a.png)

Le composant « Auteurs principaux » est stocké dans le référentiel, sous `/apps/geometrixx-outdoors/components/reporting`. Il comprend les éléments suivants :

1. Un fichier `jsp` qui lit les données jcr et définit le pseudo-élément `html`.

1. Une bibliothèque côté client contenant un fichier `js` qui récupère et classe les données, puis remplit le pseudo-élément `html`.

![chlimage_1-32](assets/chlimage_1-32a.png)

Le fichier JavaScript suivant est défini dans la [bibliothèque cliente](/help/sites-developing/clientlibs.md) `geout.reporting.topauthors` en tant qu’enfant du composant lui-même.

Le composant [QueryBuilder](/help/sites-developing/querybuilder-api.md) est utilisé pour interroger le référentiel afin de lire les nœuds `cq:AuditEvent`. Le résultat de la requête est un objet JSON duquel sont extraites les contributions de l’auteur.

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

Le `JSP` inclut le `global.jsp` comme la `clientlib`.

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
