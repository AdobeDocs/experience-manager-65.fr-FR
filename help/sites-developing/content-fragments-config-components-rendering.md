---
title: Fragments de contenu Configuration des composants pour le rendu
seo-title: Fragments de contenu Configuration des composants pour le rendu
description: Fragments de contenu Configuration des composants pour le rendu
seo-description: Fragments de contenu Configuration des composants pour le rendu
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Fragments de contenu Configuration des composants pour le rendu{#content-fragments-configuring-components-for-rendering}

Il existe plusieurs services [](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) avancés liés au rendu des fragments de contenu. Pour utiliser ces services, les types de ressources de ces composants doivent se faire connaître à la structure des fragments de contenu.

Pour ce faire, configurez le service [OSGi - Configuration](#osgi-service-content-fragment-component-configuration)du composant Fragment de contenu.

>[!CAUTION]
>
>Si vous n’avez pas besoin des services [](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) avancés décrits ci-dessous, vous pouvez ignorer cette configuration.

>[!CAUTION]
>
>Lorsque vous étendez ou utilisez des composants prêts à l’emploi, il n’est pas recommandé de modifier la configuration.

>[!CAUTION]
>
>Vous pouvez créer un composant à partir de zéro qui utilise uniquement l’API Fragments de contenu, sans services avancés. Cependant, dans ce cas, vous devrez développer votre composant afin qu’il traite le traitement approprié.
>
>Il est donc recommandé d’utiliser les composants principaux.

## Définition des services avancés nécessitant une configuration {#definition-of-advanced-services-that-need-configuration}

Les services qui nécessitent l’enregistrement d’un composant sont les suivants :

* Déterminer correctement les dépendances au cours de la publication (c.-à-d. s’assurer que les fragments et modèles peuvent être publiés automatiquement avec une page s’ils ont changé depuis la dernière publication).
* Prise en charge des fragments de contenu dans la recherche de texte intégral.
* Gestion/gestion du contenu *intermédiaire.*
* Gestion/gestion des fichiers multimédias *mixtes.*
* Le répartiteur vire les fragments référencés (si une page contenant un fragment est republiée).
* Utilisation du rendu basé sur les paragraphes.

Si vous avez besoin d’une ou de plusieurs de ces fonctionnalités, il est alors (généralement) plus facile d’utiliser la fonctionnalité prête à l’emploi, au lieu de la développer entièrement.

## Service OSGi - Configuration du composant de fragment de contenu {#osgi-service-content-fragment-component-configuration}

La configuration doit être liée au service OSGi **Content Fragment Component Configuration**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>See [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for further details.

Par exemple :

![cfm-01](assets/cfm-01.png)

La configuration OSGi est la suivante :

<table>
 <tbody>
  <tr>
   <td>Libellé</td>
   <td>Configuration OSGi<br /> </td>
   <td>Description</td>
  </tr>
  <tr>
   <td><strong>Type de ressource</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>le type de ressource à enregistrer;p. ex. <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Propriété de référence</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>nom de la propriété contenant la référence au fragment ; par ex. <code>fragmentPath</code> ou <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propriété d’élément(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>nom de la propriété qui contient le ou les noms des éléments à rendre ;p. ex.<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propriété de variation</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>nom de la propriété qui contient le nom de la variation à rendre ;p. ex.<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Pour certaines fonctionnalités (par exemple, pour générer uniquement une plage de paragraphes), vous devez respecter certaines conventions :

<table>
 <tbody>
  <tr>
   <td>Nom de la propriété</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Propriété de chaîne qui définit la plage de paragraphes à générer en mode <em>de rendu pour un élément</em>unique.</p> <p>Format:</p>
    <ul>
     <li><code>1</code> ou <code>1-3</code> ou <code>1-3;6;7-8</code> ou <code>*-3;5-*</code></li>
     <li>évalué uniquement si <code>paragraphScope</code> la valeur est définie sur <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Propriété de chaîne qui définit le mode de sortie des paragraphes en mode <em>de rendu d’un élément</em>unique.</p> <p>Valeurs :</p>
    <ul>
     <li><code>all</code> : pour rendre tous les paragraphes</li>
     <li><code>range</code> : pour rendre la plage de paragraphes fournie par <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Propriété booléenne qui définit si les en-têtes (par exemple, <code>h1</code>, <code>h2</code>, <code>h3</code>) sont comptés comme des paragraphes (<code>true</code>) ou non (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Cela peut changer dans les jalons 6.5 suivants.

## Exemple {#example}

À titre d’exemple, reportez-vous aux sections suivantes (sur une instance AEM prête à l’emploi) :

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Contient :

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

