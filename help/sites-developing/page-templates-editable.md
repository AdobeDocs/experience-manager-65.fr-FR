---
title: Modèles de pages – Modifiables
description: Des modèles modifiables ont été introduits afin de permettre aux personnes qui ne développent pas de créer et de modifier des modèles, de fournir des modèles qui conservent une connexion dynamique à toutes les pages créées à partir de ces modèles et de rendre le composant de page plus générique.
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '3186'
ht-degree: 96%

---

# Modèles de pages – Modifiables {#page-templates-editable}

Les modèles modifiables ont été élaborés pour :

* Permettre aux personnes spécialisées dans la création de [créer et de modifier des modèles](/help/sites-authoring/templates.md).

   * Ces auteurs spécialisés sont connus sous le nom de **créateurs (ou auteurs) de modèles**.
   * Les créateurs de modèles doivent être membres du groupe `template-authors`.

* Fournir des modèles qui conservent un lien dynamique avec les pages que ces personnes ont servi à créer. De cette manière, toute modification apportée au modèle est répercutée dans les pages proprement dites.
* Rendre le composant de page plus générique, ce qui permet d’utiliser le composant de page principal sans personnalisation.

Avec les modèles modifiables, les éléments qui constituent une page sont isolés au sein des composants. Vous pouvez configurer les combinaisons de composants nécessaires dans une interface utilisateur, rendant ainsi inutile le développement d’un nouveau composant de page pour chaque variante de page.

>[!NOTE]
>
>Des [modèles statiques](/help/sites-developing/page-templates-static.md) sont également disponibles.

Ce document :

* donne une vue d’ensemble de la création de modèles modifiables ;

   * Pour plus d’informations, consultez la section [Création de modèles de page](/help/sites-authoring/templates.md).

* décrit les tâches d’administration ou de développement requises pour créer des modèles modifiables ;
* décrit les bases techniques des modèles modifiables ;

Dans ce document, nous partons du principe que vous êtes déjà rompu à la création et la modification de modèles. Consultez le document [Création de modèles de page](/help/sites-authoring/templates.md) qui détaille les fonctionnalités des modèles modifiables telles qu’elles sont présentées au créateur d’un modèle.

>[!NOTE]
>
>Le tutoriel suivant peut également s’avérer intéressant pour configurer un modèle de page modifiable dans un nouveau projet :
>[Prise en main d’AEM Sites Partie 2 - Création d’une page et d’un modèle de base](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html?lang=fr)

## Création d’un modèle {#creating-a-new-template}

La création de modèles modifiables s’effectue essentiellement à l’aide de la [console de modèles et de l’éditeur de modèles](/help/sites-authoring/templates.md). Cette tâche est de la responsabilité d’une personne spécialisée dans la création de modèles. Cette section vous donne un aperçu de ce processus. Elle décrit ensuite ce qui se passe au niveau technique.

Pour plus d’informations sur l’utilisation de modèles modifiables dans un projet AEM, voir [Création d’un projet AEM à l’aide de Lazybones](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478?profile.language=fr).

Lors de la création d’un modèle modifiable :

1. Créez un [dossier pour les modèles](#template-folders). Ce dossier n’est pas obligatoire, mais il fait partie des bonnes pratiques recommandées.
1. Sélectionnez un [type de modèle](#template-type). Ce type est copié afin de créer la [définition du modèle](#template-definitions).

   >[!NOTE]
   >
   >Une sélection de types de modèles prêts à l’emploi est fournie. Vous pouvez également [créer vos propres types de modèles spécifiques à un site](/help/sites-developing/page-templates-editable.md#creating-template-types), si nécessaire.

1. Configurez la structure, les politiques de contenu, le contenu initial et la mise en page du nouveau modèle.

   **Structure**

   * La structure permet de définir les composants et le contenu de votre modèle.
   * Les composants définis dans la structure du modèle ne peuvent pas être déplacés sur une page créée ni supprimés des pages créées.

      * Si vous créez un modèle dans un dossier personnalisé en dehors de l’`We.Retail`exemple de contenu, vous pouvez choisir des composants de base ou utiliser des [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=fr).

   * Si vous souhaitez que les personnes créant les pages puissent ajouter et supprimer des composants, ajoutez un système de paragraphes au modèle.
   * Les composants peuvent être déverrouillés et reverrouillés pour vous permettre de définir le contenu initial.

   Pour plus d’informations sur la façon dont un créateur de modèles définit la structure, voir [Création de modèles de page](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Pour connaître les détails techniques de la structure, consultez la section [Structure](/help/sites-developing/page-templates-editable.md#structure) de ce document.

   **Politiques**

   * Les politiques de contenu définissent les propriétés de conception d’un composant.

      * Par exemple, les composants disponibles ou les dimensions minimales/maximales.

   * Ces politiques s’appliquent au modèle (et aux pages créées avec le modèle).

   Pour plus d’informations sur la façon dont une personne créant des modèles définit des politiques, voir [Création de modèles de page](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Pour connaître les détails techniques des politiques, consultez la section [Politiques de contenu](/help/sites-developing/page-templates-editable.md#content-policies) de ce document.

   **Contenu initial**

   * Le contenu initial définit le contenu qui s’affiche lors de la première création d’une page en fonction du modèle.
   * Le contenu initial peut ensuite être modifié par les personnes créant les pages.

   Pour plus d’informations sur la façon dont un créateur de modèles définit la structure, voir [Création de modèles de page](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Pour plus d’informations techniques sur le contenu initial, reportez-vous à la rubrique [Contenu initial](/help/sites-developing/page-templates-editable.md#initial-content) de ce document.

   **Disposition**

   * Vous pouvez définir la disposition du modèle pour différents appareils.
   * La mise en page réactive pour les modèles fonctionne de la même manière que pour la création de pages.

   Pour plus d’informations sur la façon dont le créateur d’un modèle définit la mise en page de ce dernier, voir [Création de modèles de page](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Pour plus d’informations techniques sur la mise en page d’un modèle, reportez-vous à la rubrique [mise en page](/help/sites-developing/page-templates-editable.md#layout) de ce document.

1. Activez le modèle, puis autorisez-le pour des arborescences de contenu spécifiques.

   * Un modèle peut être activé ou désactivé afin de le rendre disponible ou indisponible pour les personnes créant les pages.
   * Un modèle peut être rendu disponible ou indisponible pour certaines branches de la page.

   Pour plus d’informations sur la façon dont un créateur de modèles active un modèle, voir [Création de modèles de page](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Pour obtenir des informations techniques sur l’activation d’un modèle, consultez la section [Activation et autorisation d’un modèle à utiliser](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use) dans ce document

1. Utilisez-le pour créer des pages de contenu.

   * Lorsque vous utilisez un modèle pour créer une page, il n’existe aucune différence visible ni indication permettant de distinguer les modèles statiques des modèles modifiables.
   * Pour le créateur de pages, le processus est transparent.

   Pour plus d’informations sur la façon dont un créateur de pages utilise le modèle afin de créer une page, voir [Création et organisation des pages](/help/sites-authoring/managing-pages.md#templates).

   Pour obtenir des informations techniques sur la création de pages à l’aide de modèles modifiables, consultez la section [Pages de contenu créées](/help/sites-developing/page-templates-editable.md#resultant-content-pages) de ce document.

>[!TIP]
>
>Ne saisissez jamais d’informations qui doivent être internationalisées dans un modèle. Pour l’internationalisation, il est recommandé d’utiliser la [fonction de localisation des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=fr).

>[!NOTE]
>
>Les modèles sont des outils puissants pour rationaliser votre processus de création de page. Cependant, un nombre excessif de modèles peut submerger les auteurs et semer la confusion dans la création de pages. Une bonne règle d’or consiste à maintenir le nombre de modèles au-dessous de 100.
>
>Adobe ne recommande pas d’avoir plus de 1 000 modèles en raison des impacts potentiels sur le rendement.

>[!NOTE]
>
>La bibliothèque cliente de l’éditeur suppose la présence de l’espace de noms `cq.shared` dans les pages de contenu. S’il est absent, l’erreur JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` s’affiche.
>
>`cq.shared` est inclus dans tous les exemples de pages de contenu. Par conséquent, tout contenu basé sur ces pages inclut automatiquement `cq.shared`. Toutefois, si vous décidez de créer vos propres pages de contenu à partir de zéro, sans vous servir de l’exemple de contenu, vous devez veiller à inclure l’espace de noms `cq.shared`.
>
>Pour plus d’informations, voir [Utilisation des bibliothèques côté client](/help/sites-developing/clientlibs.md).

## Dossiers de modèles {#template-folders}

Pour organiser vos modèles, vous pouvez utiliser les dossiers suivants :

* **global**
* Spécifique au site
Les dossiers spécifiques au site que vous créez pour organiser vos modèles sont créés avec des privilèges d’administration de gestion de comptes.

>[!NOTE]
>
>Bien que vous puissiez imbriquer vos dossiers, lorsque l’utilisateur ou l’utilisatrice les visualise dans la console **Modèles**, ils sont présentés sous la forme d’une structure plate.

Dans une instance d’AEM standard, le dossier **global** existe déjà dans la console de modèles. Ce dossier contient les modèles par défaut et fait office de dossier de rechange si le dossier actif ne contient pas de politiques et/ou de types de modèles. Vous pouvez ajouter vos modèles par défaut à ce dossier ou créer un dossier (recommandé).

>[!NOTE]
>
>Il est conseillé de créer un dossier pour stocker vos modèles personnalisés et de ne pas utiliser le dossier global.

>[!CAUTION]
>
>Les dossiers doivent être créés par un utilisateur disposant des droits `admin`.

Les types de modèles et les politiques sont hérités dans tous les dossiers selon l’ordre de priorité suivant :

1. Dossier actif.
1. Parent ou parents du dossier actif.
1. `/conf/global`
1. `/apps`
1. `/libs`

Une liste de toutes les entrées autorisées est créée. Si des configurations se chevauchent (`path`/`label`), seule l’instance la plus proche du dossier actif s’affiche pour l’utilisateur.

Il existe plusieurs manières de créer un dossier.

* Par programmation ou avec CRXDE Lite
* Utilisation de l’explorateur de configurations

## Utilisation de CRXDE Lite  {#using-crxde-lite}

1. Un nouveau dossier (sous /conf) peut être créé pour votre instance, soit par programmation soit avec CRXDE Lite.

   La structure suivante doit être utilisée :

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. Vous pouvez ensuite définir les propriétés suivantes sur le nœud racine du dossier :

   `<your-folder-name> [sling:Folder]`

   Nom : `jcr:title`

   * Type : `String`

   * Valeur : titre (du dossier) que vous souhaitez afficher dans la console **Modèles**.

1. *Outre* les autorisations et les droits de création standard (par exemple, `content-authors`), vous devez maintenant attribuer les groupes et définir les droits d’accès nécessaires (listes de contrôle d’accès, ACL) pour que les créateurs et les créatrices puissent créer des modèles dans le nouveau dossier.

   Le groupe `template-authors` est le groupe par défaut qui doit être attribué. Pour plus d’informations, consultez la section suivante [ACL et groupes](/help/sites-developing/page-templates-editable.md#acls-and-groups).

   Pour plus d’informations sur la gestion et l’affectation de droits d’accès, consultez la section [Gestion des droits d’accès.](/help/sites-administering/user-group-ac-admin.md#access-right-management)

### Utilisation de l’explorateur de configurations {#using-the-configuration-browser}

1. Accédez à **Navigation globale** > **Outils** > **Explorateur de configuration**.

   Les dossiers existants sont répertoriés à gauche, y compris le dossier **Global**.

1. Cliquez sur **Créer**.
1. Les champs suivants doivent être configurés dans la boîte de dialogue **Créer une configuration** :

   * **Titre** : indiquez un titre pour le dossier de configuration.
   * **Modèles modifiables** : sélectionnez cette option pour autoriser les modèles modifiables dans ce dossier.

1. Cliquez sur **Créer**.

>[!NOTE]
>
>Dans le navigateur de configurations, vous pouvez modifier le dossier global et activer l’option **Modèles modifiables** si vous souhaitez créer des modèles dans ce dossier. Toutefois, cette pratique n’est pas recommandée.
>
>Pour plus d’informations, consultez la documentation relative au [Navigateur de configuration](/help/sites-administering/configurations.md).

### ACL et groupes {#acls-and-groups}

Une fois les dossiers modèles créés (soit par CRXDE, soit par le navigateur de configuration), des ACL doivent être définies pour les groupes appropriés pour les dossiers modèles afin d’assurer une sécurité adéquate.

Les dossiers de modèles de l’[`We.Retail`implémentation de référence](/help/sites-developing/we-retail.md) peuvent être utilisés à titre d’exemple.

#### Groupe template-authors {#the-template-authors-group}

Le groupe `template-authors` est utilisé pour gérer l’accès aux modèles. Il est fourni en standard avec AEM, mais il est vide. Les utilisateurs doivent donc être ajoutés au groupe pour le projet/site.

>[!CAUTION]
>
>Le groupe `template-authors` est *uniquement* pour les utilisateurs et les utilisatrices qui doivent pouvoir créer des modèles.
>
>La modification des modèles est une fonctionnalité très puissante qui, si elle n’est pas exécutée correctement, peut entraîner l’échec des modèles existants. Par conséquent, ce rôle doit être ciblé et ne doit inclure que des utilisateurs et utilisatrices qualifiés.

Le tableau suivant présente les autorisations nécessaires à l’édition de modèles.

<table>
 <tbody>
  <tr>
   <th>Chemin</th>
   <th>Rôle/Groupe</th>
   <th>Autorisations<br /> </th>
   <th>Description</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Créateurs de modèles<br /> </td>
   <td>lecture, écriture, réplication</td>
   <td>Créateurs de modèles qui créent, lisent, mettent à jour, suppriment et répliquent des modèles spécifiques à un site. <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>Utilisateur web anonyme</td>
   <td>lecture</td>
   <td>L’utilisateur web anonyme doit lire les modèles lors du rendu d’une page.</td>
  </tr>
  <tr>
   <td>Auteurs de contenu</td>
   <td>réplication</td>
   <td>Lors de l’activation d’une page, les créateurs et créatrices de contenu doivent activer les modèles correspondants.</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lecture, écriture, réplication</td>
   <td>Créateurs de modèles qui créent, lisent, mettent à jour, suppriment et répliquent des modèles spécifiques à un site. <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>Utilisateur web anonyme</td>
   <td>lecture</td>
   <td>L’utilisateur web anonyme doit lire les politiques lors du rendu d’une page.</td>
  </tr>
  <tr>
   <td>Auteurs de contenu</td>
   <td>réplication</td>
   <td>Les auteurs et autrices de contenu doivent activer les politiques d’un modèle de page lors de l’activation d’une page.</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Créateur de modèles</td>
   <td>lecture</td>
   <td>La personne créant des modèles crée un modèle basé sur l’un des types de modèles prédéfinis.</td>
  </tr>
  <tr>
   <td>Utilisateur web anonyme</td>
   <td>aucune</td>
   <td>L’utilisateur web anonyme ne doit pas accéder aux types de modèles.</td>
  </tr>
 </tbody>
</table>

Ce groupe `template-authors` par défaut couvre les configurations de projet dans lesquelles tous les membres de `template-authors` sont autorisés à accéder à l’ensemble des modèles et à en créer. Pour les configurations plus complexes, lorsque plusieurs groupes de personnes créant des modèles sont nécessaires pour séparer l’accès aux modèles, vous devez créer davantage de groupes de personnes créant des modèles personnalisés. Toutefois, les autorisations des groupes de personnes créant des modèles restent les mêmes.

#### Modèles hérités sous /conf/global {#legacy-templates-under-conf-global}

Ne stockez pas de modèles dans `/conf/global`. Cependant, pour certaines installations héritées, il se peut qu’il y ait encore des modèles à cet emplacement. Dans ce cas *uniquement*, les chemins d’accès suivants `/conf/global` doivent être configurés explicitement.

<table>
 <tbody>
  <tr>
   <th>Chemin</th>
   <th>Rôle/Groupe</th>
   <th>Autorisations<br /> </th>
   <th>Description</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Créateurs de modèles</td>
   <td>lecture, écriture, réplication</td>
   <td>Auteurs de modèles qui créent, lisent, mettent à jour, suppriment et répliquent des modèles dans <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utilisateur web anonyme</td>
   <td>lecture</td>
   <td>L’utilisateur web anonyme doit lire les modèles lors du rendu d’une page.</td>
  </tr>
  <tr>
   <td>Auteurs de contenu</td>
   <td>réplication</td>
   <td>Les personnes créant du contenu doivent activer les modèles d’une page lors de l’activation de celle-ci.</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lecture, écriture, réplication</td>
   <td>Auteurs de modèles qui créent, lisent, mettent à jour, suppriment et répliquent des modèles dans <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utilisateur web anonyme</td>
   <td>lecture</td>
   <td>L’utilisateur web anonyme doit lire les politiques lors du rendu d’une page.</td>
  </tr>
  <tr>
   <td>Auteurs de contenu</td>
   <td>réplication</td>
   <td>Les auteurs et autrices de contenu doivent activer les politiques d’un modèle de page lors de l’activation d’une page.</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Créateur de modèles</td>
   <td>lecture</td>
   <td>La personne créant des modèles crée un modèle basé sur l’un des types de modèles prédéfinis.</td>
  </tr>
  <tr>
   <td>Utilisateur web anonyme</td>
   <td>aucune</td>
   <td>L’utilisateur web anonyme ne doit pas accéder aux types de modèles.</td>
  </tr>
 </tbody>
</table>

## Type de modèle {#template-type}

Lors de la création d’un modèle, indiquez un type de modèle :

* Les types de modèle fournissent de façon efficace des modèles pour un modèle. Lors de la création d’un modèle, la structure et le contenu initial du type de modèle sélectionné sont utilisés pour créer le modèle.

   * Le type de modèle est copié pour créer le modèle.
   * Une fois la copie effectuée, la seule connexion entre le modèle et le type de modèle est une référence statique à des fins d’information.

* Les types de modèle permettent de définir :

   * Le type de ressource du composant de page.
   * La politique du nœud racine qui définit les composants autorisés dans l’éditeur de modèles.
   * Il est recommandé par Adobe de définir les points d’arrêt pour la grille réactive et la configuration de l’émulateur mobile au niveau du type de modèle. Cette étape est facultative, car la configuration peut également être définie sur le modèle individuel (voir [Type de modèle et groupes d’appareils mobiles](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM fournit une petite sélection de types de modèle prêts à l’emploi tels que la Page HTML5 et la Page de formulaire adaptatif.

   * Des exemples supplémentaires sont fournis dans l’[`We.Retail`](/help/sites-developing/we-retail.md)exemple de contenu.

* Les types de modèle sont généralement définis par les développeurs et les développeuses.

Les types de modèles prêts à l’emploi sont stockés sous :

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Ne modifiez rien dans le chemin d’accès `/libs`. Cela est dû au fait que le contenu du `/libs` sera remplacé lors de la prochaine mise à niveau de votre instance (et peut être remplacé lorsque vous appliquez un correctif ou un pack de fonctionnalités).

Les types de modèle spécifiques à un site doivent être stockés dans l’emplacement comparable :

* `/apps/settings/wcm/template-types`

Les définitions de vos types de modèle personnalisés doivent être stockées dans des dossiers définis par l’utilisateur (ce qui est recommandé) ou bien dans `global`. Par exemple :

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Les types de modèle doivent respecter la structure de dossiers correcte (à savoir `/settings/wcm/...`). Dans le cas contraire, ils seront introuvables.

### Types de modèle et groupes d’appareils mobiles {#template-type-and-mobile-device-groups-br}

Les [groupes de terminaux](/help/sites-developing/mobile.md#device-groups) utilisés pour un modèle modifiable (défini en tant que chemin d’accès relatif de la propriété `cq:deviceGroups`) définissent les terminaux mobiles disponibles comme émulateurs dans le [mode de mise en page](/help/sites-authoring/responsive-layout.md) de la création de pages. Vous pouvez définir cette valeur à deux emplacements :

* Sur le type de modèle modifiable
* Sur le de modèle modifiable

Lors de la création d’un modèle modifiable, la valeur est copiée du type de modèle vers le modèle individuel. Si la valeur n’est pas définie sur le type, elle peut être définie sur le modèle. Une fois le modèle créé, il n’hérite d’aucun élément du type.

>[!CAUTION]
>
>La valeur de `cq:deviceGroups` doit être définie en tant que chemin d’accès relatif, tel que `mobile/groups/responsive`, et non comme chemin d’accès absolu, comme `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Avec les [modèles statiques](/help/sites-developing/page-templates-static.md), la valeur de `cq:deviceGroups` peut être définie à la racine du site.
>
>Avec les modèles modifiables, cette valeur est désormais stockée au niveau du modèle et n’est pas prise en charge au niveau racine de la page.

### Création de types de modèle {#creating-template-types}

Si vous avez créé un modèle qui peut servir de base pour d’autres modèles, vous pouvez le copier en tant que type de modèle.

1. Créez un modèle qui servira de base pour votre type de modèle. Pour ce faire, procédez comme vous le feriez pour n’importe quel modèle modifiable, [en suivant ces instructions](/help/sites-authoring/templates.md#creating-a-new-template-template-author).
1. À l’aide de CRXDE Lite, copiez le nouveau modèle créé depuis le nœud `templates` dans le nœud `template-types` sous le [dossier de modèles](/help/sites-developing/page-templates-editable.md#template-folders).
1. Supprimez le modèle du nœud `templates` sous le [dossier de modèles](/help/sites-developing/page-templates-editable.md#template-folders).
1. Dans la copie du modèle qui se trouve sous le nœud `template-types`, supprimez toutes les propriétés `cq:template` et `cq:templateType` de tous les nœuds `jcr:content`.

Vous pouvez également développer votre propre type de modèle en utilisant un exemple de modèle modifiable comme base (disponible sur GitHub).

Code sur Github

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-sites-example-custom-template-type sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master).

## Définitions de modèle {#template-definitions}

Les définitions des modèles modifiables sont stockées dans des [dossiers définis par l’utilisateur](/help/sites-developing/page-templates-editable.md#template-folders) (ce qui est recommandé) ou bien dans `global`. Par exemple :

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Le nœud racine du modèle est de type `cq:Template` avec la structure suivante :

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Les éléments principaux sont les suivants :

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

Ce nœud contient des propriétés pour le modèle :

* **Nom** : `jcr:title`

* **Nom** : `status`

   * **Type** : `String`

   * **Valeur** : `draft`, `enabled`, ou `disabled`.

### Structure {#structure}

Définit la structure de la page créée :

* Est fusionnée avec le contenu (`/initial`) lors de la création d’une page.
* Les modifications apportées à la structure sont répercutées dans toutes les pages créées avec le modèle.
* Le nœud `root` (`structure/jcr:content/root`) définit la liste des composants qui seront disponibles dans la page créée.

   * Les composants définis dans la structure du modèle ne peuvent être ni déplacés ni supprimés dans les pages créées.
   * Une fois qu’un composant est déverrouillé, la propriété `editable` est définie sur `true`.

   * Dès qu’un composant ayant déjà du contenu est déverrouillé, son contenu est déplacé vers la branche `initial`.

* Le nœud `cq:responsive` contient des définitions pour la mise en page réactive.

### Contenu initial {#initial-content}

Définit le contenu initial dont une nouvelle page disposera au moment de sa création :

* Contient un nœud `jcr:content` copié dans toute nouvelle page.
* Est fusionné avec la structure (`/structure`) lors de la création d’une page.
* Les pages existantes sont mises à jour si le contenu initial est modifié après la création.
* Le nœud `root` contient une liste de composants permettant de définir les éléments qui seront disponibles dans la page créée.
* Si du contenu est ajouté à un composant en mode de structure et que ce composant est ensuite déverrouillé (ou inversement), ce contenu est utilisé comme contenu initial.

### Mise en page {#layout}

Lors de la [modification d’un modèle, vous pouvez définir la mise en page](/help/sites-authoring/templates.md) et utiliser une [mise en page réactive standard](/help/sites-authoring/responsive-layout.md) qui peut également être [configurée](/help/sites-administering/configuring-responsive-layout.md).

### Politiques de contenu {#content-policies}

Les politiques de contenu (ou de conception) définissent les propriétés de conception d’un composant, telles que les disponibilité du composant ou les dimensions minimales/maximales. Ces politiques s’appliquent au modèle (et aux pages créées avec le modèle). Les politiques de contenu peuvent être créées et sélectionnées dans l’éditeur de modèles.

* La propriété `cq:policy`, sur le nœud `root`
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fournit une référence relative à la politique de contenu pour le système de paragraphes de la page.

* La propriété `cq:policy`, sur les nœuds component-explicit sous `root`, fournit des liens vers les politiques relatives aux composants individuels.

* Les définitions de politique réelles sont stockées sous :
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Les chemins d’accès des définitions de politique dépendent du chemin du composant. La `cq:policy` contient une référence relative à la configuration proprement dite.

>[!NOTE]
>
>L’éditeur de page ne propose pas de mode de conception pour les pages créées à partir de modèles modifiables.
>
>L’arborescence `policies` d’un modèle modifiable présente la même hiérarchie que la configuration du mode de conception d’un modèle statique sous :
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>La configuration du mode de conception d’un modèle statique a été définie par composant de page.

### Politiques de page {#page-policies}

Les stratégies de page vous permettent de définir [stratégie de contenu](#content-policies) pour la page (parsys principal), dans le modèle ou les pages créées.

### Activation et autorisation d’un modèle à utiliser {#enabling-and-allowing-a-template-for-use}

1. **Activer le modèle**

   Pour qu’un modèle puisse être utilisé, il doit être activé par l’un des moyens suivants :

   * [Activer le modèle](/help/sites-authoring/templates.md#enablingatemplateauthor) à partir de la console des **Modèles**.

   * Définir la propriété de statut sur le nœud `jcr:content`.

      * Par exemple, sous :
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Définissez la propriété :

         * Nom : statut
         * Type : chaîne
         * Valeur : `enabled`

1. **Modèles autorisés**

   * [Définissez les chemins d’accès aux modèles autorisés dans les **Propriétés de la page**](/help/sites-authoring/templates.md#allowing-a-template-author) de la page appropriée ou de la page racine d’une sous-branche.
   * Définissez la propriété :
     `cq:allowedTemplates`
Sur le `jcr:content` noeud de la branche requise.

   Par exemple, avec la valeur suivante :

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pages de contenu créées {#resultant-content-pages}

Les pages créées à partir de modèles modifiables :

* sont créées avec une sous-arborescence qui est fusionnée à partir de `structure` et `initial` dans le modèle ;

* contiennent des références aux informations contenues dans le modèle et le type de modèle. Vous pouvez utiliser cette fonctionnalité avec un nœud `jcr:content` ayant les propriétés suivantes :

   * `cq:template`
Fournit la référence dynamique au modèle proprement dit ; fait en sorte que les modifications apportées au modèle soient répercutées sur les pages proprement dites.

   * `cq:templateType`
Fournit une référence au type de modèle.

![chlimage_1-71](assets/chlimage_1-71.png)

Le schéma ci-dessus montre la corrélation entre les modèles, le contenu et les composants :

* Contrôleur – `/content/<my-site>/<my-page>`
Page résultante référençant le modèle. Le contenu contrôle l’ensemble du processus. En fonction des définitions, il accède au modèle et aux composants appropriés.

* Configuration – `/conf/<my-folder>/settings/wcm/templates/<my-template>`
Le [modèle et les politiques de contenu associées](#template-definitions) définissent la configuration de la page.

* Modèle – Lots OSGi
Les [lots OSGi](/help/sites-deploying/osgi-configuration-settings.md) mettent en œuvre la fonctionnalité.

* Vue – `/apps/<my-site>/components`Dans les environnements de création et de publication, le contenu est rendu par des [composants](/help/sites-developing/components.md).

Lors du rendu d’une page :

* **Modèles** :

   * La propriété `cq:template` de son nœud `jcr:content` sera référencée afin d’accéder au modèle correspondant à cette page.

* **Composants** :

   * Le composant de page fusionnera l’arborescence `structure/jcr:content` du modèle avec l’arborescence `jcr:content` de la page.

   * Le composant de page autorise uniquement l’auteur ou l’autrice à modifier les nœuds de la structure du modèle qui ont été marqués comme étant modifiables (ainsi que ses éventuels enfants).
   * Lors du rendu d’un composant sur une page, le chemin d’accès relatif de ce composant est prélevé dans le nœud `jcr:content` ; une recherche est ensuite effectuée dans le même emplacement sous le nœud `policies/jcr:content` du modèle.

      * La propriété `cq:policy` de ce nœud pointe vers la politique de contenu proprement dite (en d’autres termes, elle contient la configuration de conception de ce composant).

      * Cette fonctionnalité vous permet de disposer de plusieurs modèles réutilisant les mêmes configurations de politiques de contenu.
