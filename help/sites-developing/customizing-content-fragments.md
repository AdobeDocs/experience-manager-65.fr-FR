---
title: Personnalisation et extensions de fragments de contenu
seo-title: Personnalisation et extensions de fragments de contenu
description: Un fragment de contenu étend une ressource standard.
seo-description: Un fragment de contenu étend une ressource standard.
uuid: f72c3a23-9b0d-4fab-a960-bb1350f01175
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d0770bee-4be5-4a6a-8415-70fdfd75015c
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '2749'
ht-degree: 84%

---


# Personnalisation et extensions de fragments de contenu {#customizing-and-extending-content-fragments}

Un fragment de contenu étend une ressource standard. Voir :

* [Création et gestion des fragments de contenu](/help/assets/content-fragments/content-fragments.md) et [Création de pages avec des fragments de contenu](/help/sites-authoring/content-fragments.md) pour plus d’informations sur les fragments de contenu.

* [Gestions des ressources](/help/assets/manage-assets.md) et [Personnalisation et extension des ressources](/help/assets/extending-assets.md) pour plus d’informations sur les ressources standard.

## Architecture {#architecture}

Les [parties constituantes](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) de base d’un fragment de contenu sont les suivantes :

* un *fragment de contenu,*
* constitué d’un ou de plusieurs *éléments de contenu* s,
* et qui peut avoir une ou plusieurs *Variation de contenu* s.

Selon le type de fragment, des modèles sont également utilisés :

>[!CAUTION]
>
>Les [modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) sont désormais recommandés pour créer tous les fragments.
>
>Les modèles de fragment de contenu sont utilisés pour tous les exemples dans We.Retail.

* Modèles de fragment de contenu :

   * utilisés pour définir des fragments de contenu comportant le contenu structuré.
   * Les modèles de fragment de contenu définissent la structure d’un fragment de contenu lors de sa création.
   * Un fragment référençant le modèle, les modifications du modèle peuvent impacter tous les fragments dépendants.
   * Les modèles sont composés de types de données.
   * Les fonctions pour ajouter des variations, etc., doivent mettre à jour le fragment en conséquence.

   >[!CAUTION]
   >
   >Toutes les modifications apportées à un modèle de fragment de contenu existant peuvent impacter les fragments dépendants, ce qui peut engendrer des propriétés orphelines dans ces fragments.

* Des modèles de fragment de contenu :

   * utilisés pour définir des fragments de contenu simples.
   * Les modèles définissent la structure (de base, texte seul) d’un fragment de contenu lors de sa création.
   * Le modèle étant copié dans le fragment lorsqu’il est créé, les modifications ultérieures du modèle ne seront pas répercutées dans les fragments existants.
   * Les fonctions pour ajouter des variations, etc., doivent mettre à jour le fragment en conséquence.
   * [Les ](/help/sites-developing/content-fragment-templates.md) modèles de fragments de contenu fonctionnent différemment de ceux d’autres mécanismes de modélisation au sein de l’écosystème AEM (modèles de page, etc.). C’est la raison pour laquelle ils doivent être pris en compte séparément.
   * S’il est basé sur un modèle, le type MIME du contenu est géré sur le contenu. Cela signifie que chaque élément et variation peut avoir un type MIME différent.

### Intégration avec Assets {#integration-with-assets}

La gestion des fragments de contenu (CFM) fait partie d’AEM Assets pour les raisons suivantes :

* Les fragments de contenu sont des ressources.
* Ils utilisent la fonctionnalité Assets existante.
* Ils sont entièrement intégrés à Assets (consoles d’administration, etc.).

#### Mappage de fragments de contenu structuré à Assets {#mapping-structured-content-fragments-to-assets}

![structurée de fragment à actif](assets/fragment-to-assets-structured.png)

Les fragments de contenu avec du contenu structuré (c’est-à-dire basé sur un modèle de fragment de contenu) sont mappés à une ressource unique :

* L’ensemble du contenu est stocké sous le nœud `jcr:content/data` de la ressource :

   * Les données d’éléments sont stockées sous le sous-nœud maître :
      `jcr:content/data/master`

   * Les variations sont stockées sous un sous-nœud portant le nom de la variation : par exemple, `jcr:content/data/myvariation`

   * Les données de chaque élément sont stockées dans le sous-nœud respectif comme une propriété avec le nom d’élément :
par exemple, le contenu de l’élément `text` est stocké en tant que propriété `text` sur `jcr:content/data/master`.

* Les métadonnées et le contenu associé sont stockés sous `jcr:content/metadata`
Hormis le titre et la description, qui ne sont pas considérés comme des métadonnées traditionnelles et sont stockés sur 
`jcr:content`

#### Mappage des fragments de contenu simples à Assets {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

Les fragments de contenu simples (basés sur un modèle) sont associés à un composite constitué d’une ressource principale et de sous-ressources (facultatives) :

* Toutes les informations d’un fragment ne correspondant pas à du contenu (telles que le titre, la description, les métadonnées et la structure) sont gérées sur la ressource principale de manière exclusive.
* Le contenu du premier élément d’un fragment est mappé au rendu d’origine de la ressource principale.

   * Les variations du premier élément (si elles existent) sont mappées à d’autres rendus de la ressource principale.

* Les éléments supplémentaires (s’ils existent) sont mappés aux sous-ressources de la ressource principale.

   * Le contenu principal de ces éléments supplémentaires est mappé au rendu d’origine de la sous-ressource respective.
   * Les autres variations (le cas échéant) de tout élément supplémentaire sont mappées aux autres rendus de la sous-ressource respective.

#### Emplacement des ressources   {#asset-location}

Comme pour les ressources standard, un fragment de contenu est conservé sous :

`/content/dam`

#### Autorisations de ressources {#asset-permissions}

Pour plus d’informations, voir [Fragments de contenu – considérations sur la suppression](/help/assets/content-fragments/content-fragments-delete.md).

#### Intégration de fonction {#feature-integration}

* La fonction de gestion des fragments de contenu (CFM) repose sur le noyau Assets, mais devrait être aussi indépendante que possible.
* CFM possède ses propres mises en œuvre pour les éléments en mode Carte/Colonnes/Liste. Celles-ci se connectent aux mises en œuvre de rendu de contenu existantes d’Assets.
* Plusieurs composants d’Assets ont été étendus pour prendre en charge les fragments de contenu.

### Utilisation des fragments de contenu dans les pages {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Le [composant de base Fragment de contenu](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) est désormais recommandé. Voir [Développement de composants de base](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) pour plus d’informations.

Les fragments de contenu peuvent être référencés dans les pages AEM, exactement comme n’importe quel autre type de ressource. AEM fournit le composant de base de [**** fragment de contenu](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) [qui permet d’inclure des fragments de contenu sur vos pages](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). Vous pouvez également étendre ce composant principal **Fragment de contenu**.

* Le composant utilise la propriété `fragmentPath` pour référencer le fragment de contenu. La propriété `fragmentPath` est traitée de la même façon que les propriétés similaires d’autres types de ressources, par exemple, lorsque le fragment de contenu est déplacé vers un autre emplacement.

* Le composant permet de sélectionner la variation à afficher.
* En outre, une plage de paragraphes peut être sélectionnée pour limiter la sortie ; par exemple, pour la sortie en plusieurs colonnes.
* Le composant accepte le [contenu intermédiaire](/help/sites-developing/components-content-fragments.md#in-between-content) :

   * Ici, le composant permet de placer d’autres ressources (images, etc.) entre les paragraphes du fragment référencé.
   * Pour le contenu intermédiaire, vous devez :

      * être conscient du risque de références instables ; le contenu intermédiaire (ajouté lors de la création d’une page) n’a pas de rapport fixe avec le paragraphe adjacent, et l’insertion d’un nouveau paragraphe (dans l’éditeur de fragments de contenu) avant la position du contenu intermédiaire peut entraîner la perte de l’emplacement relatif ;
      * tenir compte des paramètres supplémentaires (par exemple, tels que les filtres de variation et de paragraphe) afin d’éviter les faux positifs dans les résultats de recherche.

>[!NOTE]
>
>**Modèle de fragment de contenu :**
>
>Lors de l’utilisation d’un fragment de contenu qui était basé sur un modèle de fragment de contenu sur une page, le modèle est référencé. Cela signifie que si le modèle n’a pas été publié lorsque vous publiez la page, celui-ci est marqué et le modèle ajouté aux ressources à publier avec la page.
>
>**Modèle de fragment de contenu :**
>
>Lors de l’utilisation d’un fragment de contenu qui était basé sur un modèle de fragment de contenu sur une page, il n’y a aucune référence, car le modèle a été copié lors de la création du fragment.

#### Configuration à l’aide de la console OSGi {#configuration-using-osgi-console}

La mise en œuvre principale des fragments de contenu est, par exemple, responsable du rendu des instances d’un fragment utilisé sur une page indexable, ou de la gestion du contenu de médias mixtes. Cette mise en œuvre doit savoir quels composants sont utilisés pour le rendu des fragments, ainsi que la façon dont le rendu est paramétré.

Les paramètres de cette configuration peuvent être configurés dans la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), pour le lot OSGi **Configuration du composant de fragment de contenu**.

* ****
Types de ressourcesliste de 
`sling:resourceTypes` peut être fourni pour définir les composants utilisés pour le rendu des fragments de contenu et où le traitement en arrière-plan doit être appliqué.

* **Propriétés de référence** Une liste de propriétés peut être configurée pour spécifier l’emplacement où la référence au fragment est stockée pour le composant correspondant.

>[!NOTE]
>
>Il n’y a aucun mappage direct entre la propriété et le type de composant.
>
>AEM prend simplement la première propriété qui se trouve sur un paragraphe. Par conséquent, vous devez sélectionner les propriétés avec soin.

![capture d&#39;écran_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Il existe d’autres instructions que vous devez respecter pour vous assurer que votre composant est compatible avec le traitement des fragments de contenu en arrière-plan :

* Le nom de la propriété dans laquelle le ou les éléments à rendre sont définis doit être `element` ou `elementNames`.

* Le nom de la propriété dans laquelle est définie la dont le rendu doit être effectué·doit être `variation`variation ou `variationName`.

* Si la sortie de plusieurs éléments est prise en charge (en utilisant `elementNames` pour spécifier plusieurs éléments), le mode d&#39;affichage réel est défini par la propriété `displayMode` :

   * Si la valeur est `singleText` (et qu’un seul élément est configuré), l’élément est rendu sous forme de texte avec contenu intermédiaire, prise en charge de la mise en page, etc. Il s’agit de la valeur par défaut pour les fragments dans lesquels un seul élément est rendu.
   * Dans le cas contraire, une méthode bien plus simple est utilisée (elle pourrait être appelée « mode Formulaire »), où aucun contenu intermédiaire n’est pris en charge et le contenu du fragment est rendu « en l’état ».

* Si le fragment est rendu pour `displayMode` == `singleText` (implicitement ou explicitement), les propriétés supplémentaires suivantes entrent en jeu :

   * `paragraphScope` définit si tous les paragraphes, ou seulement une plage de paragraphes, doivent être rendus (valeurs :  `all` vs.  `range`)

   * if `paragraphScope` == `range` alors la propriété `paragraphRange` définit la plage de paragraphes à rendre

### Intégration à d’autres structures {#integration-with-other-frameworks}

Les fragments de contenu peuvent être intégrés à :

* **Des traductions**

   Les fragments de contenu sont entièrement intégrés au processus de traduction [AEM](/help/sites-administering/tc-manage.md). Au niveau architectural, cela présente les implications suivantes :

   * Les traductions d’un fragment de contenu sont en fait des fragments distincts, par exemple :

      * elles sont situées sous des racines linguistiques différentes :

         `/content/dam/<path>/en/<to>/<fragment>`

         ou

         `/content/dam/<path>/de/<to>/<fragment>`

      * mais ils partagent exactement le même chemin relatif sous la racine de la langue :

         `/content/dam/<path>/en/<to>/<fragment>`

         ou

         `/content/dam/<path>/de/<to>/<fragment>`
   * Outre les chemins basés sur des règles, il n’existe aucune connexion entre les différentes versions linguistiques d’un fragment de contenu ; elles sont traitées comme deux fragments distincts, bien que l’IU fournisse les moyens de naviguer entre les variantes de langues.
   >[!NOTE]
   >
   >Le workflow de traduction AEM fonctionne avec `/content` :
   >
   >    * Les modèles de fragment de contenu résidant dans `/conf` ; ils ne sont pas inclus dans ces traductions. Vous pouvez [internationaliser les chaînes de l’IU](/help/sites-developing/i18n-dev.md).
      >
      >    
   * Les modèles étant copiés pour créer le fragment, cela est donc implicite.


* **Des schémas de métadonnées**

   * Les fragments de contenu (ré)utilisent les [schémas de métadonnées](/help/assets/metadata-schemas.md) qui peuvent être définis par de ressources standard.
   * CFM fournit son propre schéma spécifique :

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      il peut être étendu si nécessaire.

   * Le formulaire de schéma respectif est intégré à l’éditeur de fragments.

## API de gestion des fragments de contenu – côté serveur  {#the-content-fragment-management-api-server-side}

Vous pouvez utiliser l’API côté serveur pour accéder à vos fragments de contenu ; voir :

[com.adobe.cq.dam.cfm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>Il est fortement conseillé d’utiliser l’API côté serveur plutôt que d’accéder directement à la structure du contenu.

### Interfaces principales  {#key-interfaces}

Les trois interfaces suivantes peuvent faire office de points d’entrée :

* **Modèle de fragment** ([FragmentTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   Utilisez `FragmentTemplate.createFragment()` pour créer un fragment.

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   Cette interface représente :

   * un modèle de fragment de contenu utilisé pour créer un fragment de contenu ;
   * et (après la création) les informations structurelles de ce fragment

   Ces informations peuvent inclure les éléments suivants :

   * Accès aux données de base (titre et description)
   * Accès aux modèles pour les éléments du fragment :

      * Établissement de la liste des modèles d’éléments
      * Obtention des informations structurelles pour un élément donné
      * Accès au modèle d’élément (voir `ElementTemplate`)
   * Accès aux modèles pour les variations du fragment :

      * Établissement de la liste des modèles de variations
      * Obtenir des informations structurelles pour une variation donnée
      * Accès au modèle de variation (voir `VariationTemplate`)
   * Obtention du contenu associé initial

   Interfaces qui représentent des informations importantes :

   * `ElementTemplate`

      * Obtention des informations de base (nom et titre)
      * Obtention du contenu de l’élément initial
   * `VariationTemplate`

      * Obtention des informations de base (nom, titre et description)






* **Fragment de contenu** ([ContentFragment](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Cette interface vous permet d’utiliser un fragment de contenu de façon abstraite.

   >[!CAUTION]
   >
   >Il est fortement recommandé d’accéder à un fragment par l’intermédiaire de cette interface. La modification directe de la structure de contenu doit être évitée.

   L’interface permet les actions suivantes :

   * Gestion des informations de base (par exemple, obtenir le nom ou obtenir/définir le titre/la description)
   * Accès aux métadonnées
   * Accès aux éléments :

      * Établissement de la liste des éléments
      * Obtention des éléments par nom
      * Création des éléments (voir [Restrictions](#caveats))

      * Accès aux données des éléments (voir `ContentElement`)
   * Établissement de la liste des variations définies pour le fragment
   * Création des variations de manière globale
   * Gestion du contenu associé :

      * Établissement de la liste des collections
      * Ajout de collections
      * Suppression de collections
   * Accès au modèle du fragment ou modèle

   Les interfaces représentant les éléments clés d’un fragment sont :

   * **Élément de contenu** ([ContentElement](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtention des informations de base (nom, titre et description)
      * Obtention/définition de contenu
      * Accès aux variations d’un élément :

         * Établissement de la liste des variations
         * Obtention des variations par nom
         * Création de variations (voir [Restrictions](#caveats))
         * Suppression de variations (voir [Restrictions](#caveats))
         * Accès aux données de variation (voir `ContentVariation`)
      * Raccourci pour résoudre les variations (en appliquant une certaine logique supplémentaire spécifique à la mise en œuvre si la variation spécifiée n’est pas disponible pour un élément)
   * **Variation de contenu** ([ContentVariation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtention des informations de base (nom, titre et description)
      * Obtention/définition de contenu
      * Synchronisation unique, en fonction des informations sur les dernières modifications

   Chacune des trois interfaces (`ContentFragment`, `ContentElement` et `ContentVariation`) étend l’interface `Versionable`, ce qui ajoute des fonctionnalités de contrôle de version, requises pour les fragments de contenu :

   * Création d’une version de l’élément
   * Établissement de la liste des versions de l’élément
   * Obtention du contenu d’une version spécifique de l’élément dont les versions sont contrôlées







### Adaptation – utilisation d’adaptTo()  {#adapting-using-adaptto}

Ce qui suit peut être adapté :

* `ContentFragment` peut être adapté en :

   * `Resource` - la ressource Sling sous-jacente ; notez que la mise à jour du sous-jacent  `Resource` directement nécessite la reconstruction de l’ `ContentFragment` objet.

   * `Asset` - l&#39; `Asset` abstraction DAM qui représente le fragment de contenu ; notez que la mise à jour  `Asset` directe nécessite la reconstruction de l’ `ContentFragment` objet.

* `ContentElement` peut être adapté en :

   * `ElementTemplate` pour accéder aux informations structurelles de l’élément.

* `FragmentTemplate` peut être adapté en :

   * `Resource` - la  `Resource` détermination du modèle référencé ou du modèle original copié ;

      * les modifications effectuées par le biais de `Resource` ne sont pas automatiquement répercutées dans le `FragmentTemplate`.

* `Resource` peut être adapté en :

   * `ContentFragment`
   * `FragmentTemplate`

### Restrictions {#caveats}

Il convient de noter les éléments suivants :

* Cette API est mise en œuvre afin de fournir les fonctionnalités prises en charge par l’IU.
* L’API entière est conçue pour **ne pas** conserver les modifications automatiquement (sauf indication contraire dans l’API JavaDoc). Vous devez donc toujours valider le résolveur de ressources de la requête correspondante (ou le résolveur que vous utilisez).
* Tâches qui peuvent nécessiter des efforts supplémentaires :

   * La création/suppression d’éléments ne met pas à jour la structure de données de fragments simples (basés sur un modèle de fragments).
   * La création de variations de `ContentElement` ne met pas à jour la structure de données (tandis que la création globale à partir de `ContentFragment` la met à jour).

   * La suppression des variations existantes ne met pas à jour la structure de données.

## L’API de gestion des fragments de contenu – côté client   {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Pour AEM 6.5, l’API côté client est interne.

### Informations supplémentaires {#additional-information}

Reportez-vous aux informations suivantes :

* `filter.xml`

   Le fichier `filter.xml` pour la gestion des fragments de contenu est configuré pour ne pas chevaucher le module de contenu de base d’Assets.

## Sessions de modification {#edit-sessions}

Une session de modification est lancée lorsque l’utilisateur ouvre un fragment de contenu dans l’une des pages de l’éditeur. La session de modification est terminée lorsque l’utilisateur quitte l’éditeur en sélectionnant **Enregistrer** ou **Annuler**.

### Conditions requises {#requirements}

Les conditions pour contrôler une session de modification sont les suivantes :

* La modification d’un fragment de contenu qui peut être réparti sur plusieurs vues (= pages HTML) doit être atomique.
* La modification doit également être *transactionnelle* ; à la fin de la session de modification, les modifications doivent être validées (enregistrées) ou restaurées (annulées).
* Les cas limites doivent être traités correctement. Il peut s’agir de situations telles qu’un utilisateur quittant la page en saisissant une URL manuellement ou en utilisant la navigation globale.
* Un enregistrement automatique récurrent (toutes les x minutes) doit être disponible pour éviter toute perte de données.
* Si un fragment de contenu est modifié par deux utilisateurs simultanément, l’un ne doit pas écraser les modifications de l’autre.

#### Processus  {#processes}

Les processus impliqués sont les suivants :

* Démarrage d’une session

   * Une nouvelle version du fragment de contenu est créée.
   * L’enregistrement automatique est démarré.
   * Les cookies sont configurés afin de définir le fragment actuellement modifié et de signifier qu’une session de modification est ouverte.

* Fin d’une session

   * L’enregistrement automatique est arrêté.
   * Lors de la validation :

      * Les informations sur la dernière modification sont mises à jour.
      * Les cookies sont supprimés.
   * Lors de la restauration :

      * La version du fragment de contenu créée lors du démarrage de la session de modification est restaurée.
      * Les cookies sont supprimés.


* Modification

   * Toutes les modifications (enregistrement automatique inclus) sont effectuées sur le fragment de contenu actif, et non dans une zone séparée et protégée.
   * Par conséquent, ces modifications sont répercutées immédiatement sur les pages AEM faisant référence au fragment de contenu respectif.

#### Actions  {#actions}

Les actions possibles sont les suivantes :

* Entrée sur une page

   * Vérifier si une session de modification est déjà présente en vérifiant le cookie correspondant.

      * S’il en existe un, vérifier que la session de modification a été démarrée pour le fragment de contenu qui est en cours de modification.

         * S’il s’agit du fragment en cours, rétablir la session.
         * Si ce n’est pas le cas, essayer d’annuler la modification du fragment de contenu précédemment modifié et supprimer les cookies (aucune session de modification n’est présente après).
      * En l’absence de session de modification, attendre la première modification apportée par l’utilisateur (voir ci-dessous).
   * Vérifier si le fragment de contenu est déjà référencé sur une page et afficher les informations appropriées si tel est le cas.



* Modification de contenu

   * Chaque fois que l’utilisateur modifie le contenu et qu’aucune session de modification n’est présente, une nouvelle session de modification est créée (voir [Démarrage d’une session](#processes)).

* Sortie d’une page

   * Si une session de modification est présente, et si les modifications n’ont pas été conservées, une boîte de dialogue de confirmation modale s’affiche pour avertir l’utilisateur de la perte potentielle de contenu et pour lui permettre de rester sur la page.

## Exemples {#examples}

### Exemple : accès à un fragment de contenu existant {#example-accessing-an-existing-content-fragment}

Pour ce faire, vous pouvez adapter la ressource qui représente l’API à :

`com.adobe.cq.dam.cfm.ContentFragment`

Par exemple :

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Exemple : création d’un fragment de contenu  {#example-creating-a-new-content-fragment}

Pour créer un fragment de contenu par programmation, vous devez utiliser :

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Par exemple :

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exemple : spécification de l’intervalle d’enregistrement automatique  {#example-specifying-the-auto-save-interval}

L’intervalle d’enregistrement automatique (exprimé en secondes) peut être défini à l’aide de Configuration Manager (ConfMgr) :

* Nœud : `<*conf-root*>/settings/dam/cfm/jcr:content`
* Nom de la propriété : `autoSaveInterval`
* Type : `Long`

* Valeur par défaut : `600` (10 minutes) ; cette valeur est définie sur `/libs/settings/dam/cfm/jcr:content`

Si vous souhaitez définir un intervalle d’enregistrement automatique de 5 minutes, vous devez définir la propriété sur le nœud, par exemple :

* Nœud : `/conf/global/settings/dam/cfm/jcr:content`
* Nom de la propriété : `autoSaveInterval`

* Type : `Long`

* Valeur : `300` (5 minutes correspondent à 300 secondes).

## Modèles de fragment de contenu {#content-fragment-templates}

Voir [Modèles de fragment de contenu](/help/sites-developing/content-fragment-templates.md) pour plus d’informations.

## Composants pour la création de page {#components-for-page-authoring}

Pour plus d’informations, voir :

* [Composants de base – composant de fragment de contenu](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) (recommandé)
* [Composants de fragment de contenu – composants pour la création de pages](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
