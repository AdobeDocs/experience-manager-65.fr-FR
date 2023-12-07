---
title: Personnalisation et extensions de fragments de contenu
description: Un fragment de contenu étend une ressource standard. Découvrez comment les personnaliser.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 63%

---


# Personnalisation et extensions de fragments de contenu{#customizing-and-extending-content-fragments}

Un fragment de contenu étend une ressource standard ; voir :

* [Création et gestion des fragments de contenu](/help/assets/content-fragments/content-fragments.md) et [Création de pages avec des fragments de contenu](/help/sites-authoring/content-fragments.md) pour plus d’informations sur les fragments de contenu.

* [Gestion des ressources](/help/assets/manage-assets.md) et [Personnalisation et extension de ressources](/help/assets/extending-assets.md) pour plus d’informations sur les ressources standard.

## Architecture {#architecture}

Les [éléments](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) de base d’un fragment de contenu sont les suivants :

* Un *fragment de contenu,*
* comportant un ou plusieurs *éléments de contenu*,
* et qui peut avoir une ou plusieurs *variations de contenu*.

Selon le type de fragment, des modèles sont également utilisés :

>[!CAUTION]
>
>Les [modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) sont désormais recommandés pour créer tous les fragments.
>
>Les modèles de fragment de contenu sont utilisés pour tous les exemples dans WKND.

>[!NOTE]
>
>Avant la version 6.3 d’AEM, les fragments de contenu étaient créés à partir de modèles (templates) différents des modèles (models) actuels.
>
>Les anciens modèles (templates) de fragment de contenu sont désormais obsolètes. Ils peuvent toujours être utilisés pour créer des fragments, mais il est recommandé d’utiliser à la place les nouveaux modèles de fragment de contenu. Aucune nouvelle fonctionnalité ne sera ajoutée aux modèles de fragment et elles seront supprimées dans une version ultérieure.

* Modèles de fragment de contenu :

   * Utilisé pour définir des fragments de contenu qui contiennent du contenu structuré.
   * Les modèles de fragment de contenu définissent la structure d’un fragment de contenu lors de sa création.
   * Un fragment référençant le modèle, les modifications du modèle peuvent impacter tous les fragments dépendants.
   * Les modèles sont composés de types de données.
   * Les fonctions permettant d’ajouter de nouvelles variations, etc., doivent mettre à jour le fragment en conséquence.

  >[!CAUTION]
  >
  >Toutes les modifications apportées à un modèle de fragment de contenu existant peuvent impacter les fragments dépendants, ce qui peut engendrer des propriétés orphelines dans ces fragments.

* Modèles de fragment de contenu :

   * utilisés pour définir des fragments de contenu simples.
   * Les modèles définissent la structure (de base, texte uniquement) d’un fragment de contenu lors de sa création.
   * Le modèle est copié dans le fragment lors de sa création. De ce fait, les modifications supplémentaires apportées au modèle ne seront pas répercutées dans les fragments existants.
   * Les fonctions permettant d’ajouter de nouvelles variations, etc., doivent mettre à jour le fragment en conséquence.
   * [Modèles de fragment de contenu](/help/sites-developing/content-fragment-templates.md) fonctionnent différemment des autres mécanismes de création de modèles au sein de l’écosystème AEM (par exemple, les modèles de page, etc.). Par conséquent, elles doivent être prises en compte séparément.
   * Lorsqu’il est basé sur un modèle, le type MIME du contenu est géré sur le contenu réel ; cela signifie que chaque élément et variation peuvent avoir un type MIME différent.

### Intégration à Assets {#integration-with-assets}

La gestion des fragments de contenu fait partie d’AEM Assets, car :

* les fragments de contenu sont des ressources ;
* ils utilisent la fonctionnalité Assets existante ;
* ils sont entièrement intégrés à Assets (consoles d’administration, etc.).

#### Mappage de fragments de contenu structuré à Assets {#mapping-structured-content-fragments-to-assets}

![fragment-to-assets-structured](assets/fragment-to-assets-structured.png)

Les fragments de contenu avec du contenu structuré (c’est-à-dire basé sur un modèle de fragment de contenu) sont mappés à une ressource unique :

* L’ensemble du contenu est stocké sous le nœud `jcr:content/data` de la ressource :

   * Les données d’éléments sont stockées sous le sous-nœud maître :
     `jcr:content/data/master`

   * Les variations sont stockées sous un sous-nœud portant le nom de la variation :
par exemple, `jcr:content/data/myvariation`.

   * Les données de chaque élément sont stockées dans le sous-nœud respectif en tant que propriété avec le nom d’élément :
par exemple, le contenu de l’élément `text` est stocké en tant que propriété `text` sur `jcr:content/data/master`.

* Les métadonnées et le contenu associé sont stockés sous `jcr:content/metadata`.
Hormis le titre et la description, qui ne sont pas considérés comme des métadonnées traditionnelles et sont stockés sur `jcr:content`.

#### Mappage des fragments de contenu simples à Assets {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

Les fragments de contenu simples (basés sur un modèle) sont mappés à un composite constitué d’une ressource principale et de sous-ressources (facultatives) :

* Toutes les informations autres que le contenu d’un fragment (titre, description, métadonnées, structure, etc.) sont gérées exclusivement sur la ressource principale.
* Le contenu du premier élément d’un fragment est mappé au rendu d’origine de la ressource principale.

   * Les variations (le cas échéant) du premier élément sont mappées à d’autres rendus de la ressource principale.

* Les éléments supplémentaires (s’ils existent) sont mappés aux sous-ressources de la ressource principale.

   * Le contenu principal de ces éléments supplémentaires est mappé au rendu d’origine de la sous-ressource respective.
   * Les autres variations (le cas échéant) de tout élément supplémentaire sont mappées aux autres rendus de la sous-ressource respective.

#### Emplacement des ressources {#asset-location}

Comme pour les ressources standard, un fragment de contenu est conservé sous :

`/content/dam`

#### Autorisations de ressources {#asset-permissions}

Pour plus d’informations, voir [Fragments de contenu – considérations sur la suppression](/help/assets/content-fragments/content-fragments-delete.md).

#### Intégration de fonction {#feature-integration}

* La fonctionnalité de gestion des fragments de contenu (CFM) repose sur le noyau Ressources, mais doit être aussi indépendante que possible.
* CFM possède ses propres mises en œuvre pour les éléments dans les vues Carte/Colonnes/Liste. Celles-ci se connectent aux mises en œuvre de rendu de contenu existantes d’Assets.
* Plusieurs composants d’Assets ont été étendus pour prendre en charge les fragments de contenu.

### Utilisation des fragments de contenu dans les pages {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Le [composant de base Fragment de contenu](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=fr) est désormais recommandé. Consultez la section [Développement des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=fr) pour plus d’informations.

Les fragments de contenu peuvent être référencés à partir des pages AEM, comme tout autre type de ressource. AEM fournit la variable [**Fragment de contenu** composant principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=fr) - a [qui permet d’inclure des fragments de contenu sur vos pages](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). Vous pouvez également étendre ce composant principal **Fragment de contenu**.

* Le composant utilise la propriété `fragmentPath` pour référencer le fragment de contenu. La propriété `fragmentPath` est traitée de la même façon que les propriétés similaires d’autres types de ressources, par exemple, lorsque le fragment de contenu est déplacé vers un autre emplacement.

* Le composant permet de sélectionner la variation à afficher.
* En outre, une plage de paragraphes peut être sélectionnée pour limiter la sortie. Par exemple, cela peut être utilisé pour la sortie multi-colonnes.
* Le composant permet [contenu intermédiaire](/help/sites-developing/components-content-fragments.md#in-between-content):

   * Ici, le composant vous permet de placer d’autres ressources (images, etc.) entre les paragraphes du fragment référencé.
   * Pour le contenu intermédiaire, vous devez :

      * être conscient du risque de références instables ; le contenu intermédiaire (ajouté lors de la création d’une page) n’a pas de rapport fixe avec le paragraphe adjacent, et l’insertion d’un nouveau paragraphe (dans l’éditeur de fragments de contenu) avant la position du contenu intermédiaire peut entraîner la perte de l’emplacement relatif ;
      * prendre en compte les paramètres supplémentaires (tels que les filtres de variation et de paragraphe) pour éviter les faux positifs dans les résultats de recherche ;

>[!NOTE]
>
>**Modèle de fragment de contenu :**
>
>Lors de l’utilisation d’un fragment de contenu basé sur un modèle de fragment de contenu sur une page, le modèle est référencé. Cela signifie que si le modèle n’a pas été publié lorsque vous publiez la page, celui-ci est marqué et le modèle ajouté aux ressources à publier avec la page.
>
>**Modèle de fragment de contenu :**
>
>Lors de l’utilisation d’un fragment de contenu qui était basé sur un modèle de fragment de contenu sur une page, il n’y a aucune référence car le modèle a été copié lors de la création du fragment.

#### Configuration avec la console OSGi {#configuration-using-osgi-console}

L’implémentation principale des fragments de contenu est, par exemple, chargée de rendre les instances d’un fragment utilisé sur une page consultable ou de gérer le contenu multimédia mixte. Cette implémentation doit savoir quels composants sont utilisés pour le rendu des fragments et comment le rendu est paramétré.

Les paramètres correspondants peuvent être configurés dans la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) pour le lot OSGi **Configuration des composants de fragments de contenu**.

* **Types de ressources**
Une liste de `sling:resourceTypes` peut être fourni pour définir les composants utilisés pour le rendu des fragments de contenu et l’emplacement auquel le traitement en arrière-plan doit être appliqué.

* **Propriétés de référence**
Une liste de propriétés peut être configurée pour spécifier l’emplacement où la référence au fragment est stockée pour le composant correspondant.

>[!NOTE]
>
>Il n’existe pas de mappage direct entre la propriété et le type de composant.
>
>AEM utilise simplement la première propriété disponible sur un paragraphe. Vous devez donc choisir les propriétés avec soin.

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Il existe d’autres instructions que vous devez respecter pour vous assurer que votre composant est compatible avec le traitement des fragments de contenu en arrière-plan :

* Le nom de la propriété dans laquelle le ou les éléments dont le rendu doit être effectué sont définis doit être `element` ou `elementNames`.

* Le nom de la propriété dans laquelle est définie la variation dont le rendu doit être effectué doit être `variation` ou `variationName`.

* Si la sortie de plusieurs éléments est prise en charge (à l’aide de `elementNames` pour spécifier plusieurs éléments), le mode d’affichage est défini par la propriété`displayMode` :

   * Si la valeur est `singleText` (et il n’y a qu’un seul élément configuré), l’élément est rendu sous forme de texte avec du contenu intermédiaire, la prise en charge de la mise en page, etc. Il s’agit de la valeur par défaut des fragments dans lesquels un seul élément est rendu.
   * Dans le cas contraire, une approche beaucoup plus simple est utilisée (peut être appelée &quot;vue de formulaire&quot;), où aucun contenu intermédiaire n’est pris en charge et le contenu du fragment est rendu &quot;tel quel&quot;.

* Si le fragment est rendu pour `displayMode` == `singleText` (de manière implicite ou explicite), les propriétés supplémentaires suivantes entrent en jeu :

   * `paragraphScope` définit si tous les paragraphes ou uniquement une plage de paragraphes doivent être rendus (valeurs `all` ou `range`).

   * Si `paragraphScope` == `range`, alors la propriété `paragraphRange` définit la plage de paragraphes dont le rendu doit être effectué.

### Intégration à d’autres structures {#integration-with-other-frameworks}

Les fragments de contenu peuvent être intégrés avec :

* **Des traductions**

  Les fragments de contenu sont entièrement intégrés au [workflow de traduction AEM](/help/sites-administering/tc-manage.md). Au niveau architectural, cela se traduit par les éléments suivants :

   * les traductions individuelles d’un fragment de contenu sont en fait des fragments distincts ; par exemple :

      * elles se trouvent sous différentes racines de langue :

        `/content/dam/<path>/en/<to>/<fragment>`

        ou

        `/content/dam/<path>/de/<to>/<fragment>`

      * mais ils partagent exactement le même chemin relatif sous la racine de langue :

        `/content/dam/<path>/en/<to>/<fragment>`

        ou

        `/content/dam/<path>/de/<to>/<fragment>`

   * Outre les chemins basés sur des règles, il n’existe aucune connexion entre les différentes versions linguistiques d’un fragment de contenu ; elles sont traitées comme deux fragments distincts, bien que l’IU fournisse les moyens de naviguer entre les variantes de langues.

  >[!NOTE]
  >
  >Le workflow de traduction AEM fonctionne avec `/content` :
  >
  >* Les modèles de fragment de contenu résidant dans `/conf` ; ils ne sont pas inclus dans ces traductions. Vous pouvez [internationaliser les chaînes de l’IU](/help/sites-developing/i18n-dev.md).
  >
  >* Les modèles étant copiés pour créer le fragment, ce processus est donc implicite.

* **Des schémas de métadonnées**

   * Les fragments de contenu (ré)utilisent les [schémas de métadonnées](/help/assets/metadata-schemas.md), qui peuvent être définis avec des ressources standard.
   * CFM fournit son propre schéma spécifique :

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     il peut être étendu si nécessaire.

   * Le formulaire de schéma respectif est intégré à l’éditeur de fragments.

## API de gestion des fragments de contenu – côté serveur {#the-content-fragment-management-api-server-side}

Vous pouvez utiliser l’API côté serveur pour accéder à vos fragments de contenu ; consultez :

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html).

>[!CAUTION]
>
>Il est vivement recommandé d’utiliser l’API côté serveur au lieu d’accéder directement à la structure de contenu.

### Interfaces principales {#key-interfaces}

Les trois interfaces suivantes peuvent faire office de points d’entrée :

* **Modèle de fragment** ([FragmentTemplate](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

  Utilisation `FragmentTemplate.createFragment()` pour créer un fragment.

  ```
  Resource templateOrModelRsc = resourceResolver.getResource("...");
  FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
  ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
  ```

  Cette interface représente :

   * un modèle de fragment de contenu utilisé pour créer un fragment de contenu ;
   * et (après la création) les informations relatives à la structure de ce fragment.

  Ces informations peuvent inclure les éléments suivants :

   * Accès aux données de base (titre, description)
   * Accédez aux modèles/modèles pour les éléments du fragment :

      * Modèles d’élément de liste
      * Obtention d’informations structurelles pour un élément donné
      * Accès au modèle d’élément (voir `ElementTemplate`)

   * Accédez aux modèles pour les variantes du fragment :

      * Modèles de variation de liste
      * Obtention des informations structurelles pour une variation donnée
      * Accès au modèle de variation (voir `VariationTemplate`)

   * Obtenir le contenu associé initial

  Interfaces qui représentent des informations importantes :

   * `ElementTemplate`

      * Obtention des données de base (nom, titre)
      * Obtention du contenu initial de l’élément

   * `VariationTemplate`

      * Obtention des informations de base (nom, titre et description)

* **Fragment de contenu** ([ContentFragment](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Cette interface vous permet d’utiliser un fragment de contenu de manière abstraite.

  >[!CAUTION]
  >
  >Il est vivement recommandé d’accéder à un fragment via cette interface. La modification directe de la structure de contenu doit être évitée.

  L’interface permet les actions suivantes :

   * Gestion des informations de base (par exemple, obtenir le nom ou obtenir/définir le titre/la description)
   * Accès aux métadonnées
   * Accès aux éléments :

      * Éléments de liste
      * Obtention des éléments par nom
      * Création des éléments (voir [Restrictions](#caveats))

      * Accès aux données des éléments (voir `ContentElement`)

   * Variations de liste définies pour le fragment
   * Création globale de variations
   * Gestion du contenu associé :

      * Liste des collections
      * Ajout de collections
      * Suppression de collections

   * Accès au modèle ou au modèle du fragment

  Les interfaces qui représentent les éléments principaux d’un fragment sont les suivantes :

   * **Élément de contenu** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtention des informations de base (nom, titre et description)
      * Obtention/définition du contenu
      * Accès aux variations d’un élément :

         * Liste des variations
         * Obtention des variations par nom
         * Création de nouvelles variations (voir [Restrictions](#caveats))
         * Suppression de variations (voir [Restrictions](#caveats))
         * Accès aux données de variation (voir `ContentVariation`)

      * Raccourci pour résoudre les variations (application d’une logique de secours supplémentaire spécifique à l’implémentation si la variation spécifiée n’est pas disponible pour un élément)

   * **Variation de contenu** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtention des informations de base (nom, titre et description)
      * Obtention/définition du contenu
      * Synchronisation simple, basée sur la dernière information modifiée

  Chacune des trois interfaces (`ContentFragment`, `ContentElement` et `ContentVariation`) étend l’interface `Versionable`, ce qui ajoute des fonctionnalités de contrôle de version, requises pour les fragments de contenu :

   * Création d’une version de l’élément
   * Liste des versions de l’élément
   * Obtention du contenu d’une version spécifique de l’élément versionné

### Adaptation – utilisation d’adaptTo() {#adapting-using-adaptto}

Ce qui suit peut être adapté :

* `ContentFragment` peut être adapté en :

   * `Resource` : la ressource sous-jacente de Sling ; notez que la mise à jour directe de la `Resource` sous-jacente requiert la reconstruction de l’objet `ContentFragment` ;

   * `Asset` – Abstraction `Asset` de gestion des ressources numériques représentant le fragment de contenu ; la mise à jour directe de la `Asset` sous-jacente nécessite la reconstruction de l’objet `ContentFragment`.

* `ContentElement` peut être adapté en :

   * `ElementTemplate` pour accéder aux informations structurelles de l’élément.

* `FragmentTemplate` peut être adapté en :

   * `Resource` : la `Resource` déterminant le modèle référencé ou le modèle d’origine qui a été copié ;

      * les modifications apportées par l’intermédiaire de la `Resource` ne sont pas répercutées automatiquement dans le `FragmentTemplate`.

* `Resource` peut être adapté en :

   * `ContentFragment`
   * `FragmentTemplate`

### Restrictions {#caveats}

Il convient de noter les éléments suivants :

* L’API est mise en oeuvre afin de fournir des fonctionnalités prises en charge par l’interface utilisateur.
* L’API entière est conçue pour **ne pas** conserver les modifications automatiquement (sauf indication contraire dans l’API JavaDoc). Vous devrez donc toujours engager le résolveur de ressources de la requête correspondante (ou le résolveur que vous utilisez réellement).
* Tâches pouvant nécessiter un effort supplémentaire :

   * La création/suppression d’éléments ne met pas à jour la structure de données de fragments simples (basés sur un modèle de fragment).
   * La création de variations de `ContentElement` ne met pas à jour la structure de données (tandis que la création globale à partir de `ContentFragment` la met à jour).

   * La suppression de variations existantes ne met pas à jour la structure de données.

## L’API de gestion des fragments de contenu – côté client  {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Pour AEM 6.5, l’API côté client est interne.

### Informations supplémentaires {#additional-information}

Reportez-vous aux informations suivantes :

* `filter.xml`

  Le fichier `filter.xml` pour la gestion des fragments de contenu est configuré pour ne pas chevaucher le package de contenu de base d’Assets.

## Sessions de modification {#edit-sessions}

Une session de modification est lancée lorsque l’utilisateur ouvre un fragment de contenu dans l’une des pages de l’éditeur. La session de modification est terminée lorsque l’utilisateur quitte l’éditeur en sélectionnant **Enregistrer** ou **Annuler**.

### Conditions requises {#requirements}

Les conditions pour contrôler une session de modification sont les suivantes :

* La modification d’un fragment de contenu qui peut être réparti sur plusieurs vues (= pages HTML) doit être atomique.
* La modification doit également être *transactionnel*; à la fin de la session de modification, les modifications doivent être validées (enregistrées) ou restaurées (annulées).
* Les cas Edge doivent être gérés correctement, notamment lorsque l’utilisateur quitte la page en saisissant une URL manuellement ou en utilisant la navigation globale.
* Un enregistrement automatique périodique (toutes les x minutes) doit être disponible pour empêcher la perte de données.
* Si un fragment de contenu est modifié simultanément par deux utilisateurs, ils ne doivent pas remplacer les modifications de l’autre.

#### Processus {#processes}

Les processus impliqués sont les suivants :

* Démarrage d’une session

   * Une nouvelle version du fragment de contenu est créée.
   * L’enregistrement automatique est démarré.
   * Les cookies sont configurés afin de définir le fragment actuellement modifié et de signifier qu’une session de modification est ouverte.

* Fin d’une session

   * L’enregistrement automatique est arrêté.
   * Lors de la validation :

      * Les informations de dernière modification sont mises à jour.
      * Les cookies sont supprimés.

   * Lors du retour arrière :

      * La version du fragment de contenu créé au démarrage de la session de modification est restaurée.
      * Les cookies sont supprimés.

* Modification

   * Toutes les modifications (enregistrement automatique inclus) sont effectuées sur le fragment de contenu actif, et non dans une zone séparée et protégée.
   * Par conséquent, ces modifications sont répercutées immédiatement sur AEM pages qui font référence au fragment de contenu correspondant.

#### Actions {#actions}

Les actions possibles sont les suivantes :

* Saisie d’une page

   * Vérifiez si une session de modification est déjà présente en vérifiant le cookie correspondant.

      * S’il en existe un, vérifiez que la session de modification a été lancée pour le fragment de contenu en cours de modification.

         * Si le fragment actif, rétablissez la session.
         * Dans le cas contraire, essayez d’annuler la modification du fragment de contenu précédemment modifié et supprimez les cookies (aucune session de modification n’est présente par la suite).

      * S’il n’existe aucune session de modification, attendez la première modification effectuée par l’utilisateur (voir ci-dessous).

   * Vérifiez si le fragment de contenu est déjà référencé sur une page et affichez les informations appropriées si tel est le cas.

* Modification du contenu

   * Chaque fois que l’utilisateur modifie le contenu en l’absence de session de modification, une session de modification est créée (consultez [Démarrage d’une session](#processes)).

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

### Exemple : création d’un fragment de contenu {#example-creating-a-new-content-fragment}

Pour créer un fragment de contenu par programmation, vous devez utiliser :

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Par exemple :

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exemple : spécification de l’intervalle d’enregistrement automatique {#example-specifying-the-auto-save-interval}

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

Pour plus d’informations, voir

* [Composants principaux : composant de fragment de contenu](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=fr) (recommandé)
* [Composants de fragment de contenu – Composants pour la création de pages](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
