---
title: 'Balisage des ressources d’activation '
seo-title: 'Balisage des ressources d’activation '
description: Le balisage des ressources d’activation permet de filtrer les ressources et les chemins d’apprentissage lorsque les membres parcourent les catalogues.
seo-description: Le balisage des ressources d’activation permet de filtrer les ressources et les chemins d’apprentissage lorsque les membres parcourent les catalogues.
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Balisage des ressources d’activation{#tagging-enablement-resources} 

## Présentation {#overview}

Le balisage des ressources d’activation permet de filtrer les ressources et les chemins d’apprentissage lorsque les membres parcourent [des catalogues](functions.md#catalog-function).

Essentiellement :

* [Création d’une balise](../../help/sites-administering/tags.md#creating-a-namespace) pour chaque catalogue

   * [Définition des autorisations de balise](../../help/sites-administering/tags.md#setting-tag-permissions)
   * Pour les membres de la communauté uniquement (communauté fermée)

      * Autoriser l’accès en lecture pour le groupe de membres du site [communautaire](users.md#publish-group-roles)
   * Pour tout de site, qu’il soit connecté ou anonyme (communauté ouverte)

      * Autoriser l&#39;accès en lecture pour le `Everyone` groupe
   * [Publication des balises](../../help/sites-administering/tags.md#publishing-tags)



* [Définir la portée des balises d’un site communautaire](sites-console.md#tagging)

   * [Configuration des catalogues existants dans la structure du site](functions.md#catalog-function)

      * Il est possible d’ajouter des balises à l’instance de catalogue afin de contrôler le de balises présentées dans le d’interface utilisateur.
      * Peut ajouter des [pré-](catalog-developer-essentials.md#pre-filters), pour limiter les ressources incluses d’un catalogue.

* [Publication du site de la communauté](sites-console.md#publishing-the-site)
* [Appliquer des balises aux ressources](resources.md#create-a-resource) d’activation afin qu’elles puissent être filtrées de manière catégorique
* [Publication des ressources d’activation](resources.md#publish)

## Balises de site de la communauté {#community-site-tags}

Lors de la création ou de la modification d’un site de la communauté, le paramètre [](sites-console.md#tagging) Balisage définit l’étendue des balises disponibles pour les fonctionnalités du site en sélectionnant un sous-ensemble de balises existantes  .

Bien que des balises puissent être créées et ajoutées au site de la communauté à tout moment, il est recommandé de concevoir une taxonomie au préalable, comme pour concevoir une base de données. Voir [Utilisation des balises](../../help/sites-authoring/tags.md).

Lors de l’ajout ultérieur de balises à un site communautaire existant, il est nécessaire d’enregistrer la modification avant de pouvoir ajouter la nouvelle balise à une fonction de catalogue dans la structure du site.

Pour un site communautaire, une fois le site publié et les balises publiées, il est nécessaire de permettre l’accès en lecture aux membres de la communauté. See [Setting Tag Permissions](../../help/sites-administering/tags.md#setting-tag-permissions).

Voici comment il s’affiche dans CRXDE lorsqu’un administrateur applique des autorisations de lecture `/etc/tags/ski-catalog` pour le groupe `Community Enable Members`.

![chlimage_1-420](assets/chlimage_1-420.png)

## Balise de catalogue  {#catalog-tag-namespaces}

La fonction de catalogue utilise des balises pour se définir. Lors de la configuration de la fonction de catalogue dans un site de la communauté, l’ensemble de balises  d’ à choisir est défini par l’étendue des espaces de noms de balises définis pour le site de la communauté.

La fonction Catalogue comprend un paramètre de balise qui définit les balises répertoriées dans l’interface utilisateur de filtre du catalogue. Le paramètre &quot;Tous  &quot; fait référence à la portée de la balise  sélectionnée pour le site communautaire.

![chlimage_1-421](assets/chlimage_1-421.png)

## Application de balises aux ressources d’activation {#applying-tags-to-enablement-resources}

Les ressources d’activation et les chemins d’apprentissage s’affichent dans tous les catalogues une fois `Show in Catalog` cochés. L’ajout de balises aux ressources et aux chemins d’apprentissage permet le préfiltrage dans des catalogues spécifiques, ainsi que le filtrage dans l’interface utilisateur du catalogue.

La limitation des ressources d’activation et des chemins d’apprentissage à des catalogues spécifiques est réalisée en créant des [pré-](catalog-developer-essentials.md#pre-filters).

L’interface utilisateur du catalogue permet aux d’appliquer un filtre de balises au de ressources et de chemins d’apprentissage qui apparaissent dans ce catalogue.

L’administrateur appliquant les balises aux ressources d’activation doit connaître la balise   associée aux catalogues, ainsi que la taxonomie afin de sélectionner une sous-balise pour une catégorisation plus précise.

Si, par exemple, un `ski-catalog` a été créé et défini sur un catalogue nommé `Ski Catalog`, il peut avoir deux balises enfants : `lesson-1` et `lesson-2`.

Ainsi, toute ressource d’activation balisée avec l’une des balises suivantes :

* catalogue-ski:leçon-1
* catalogue-ski:leçon-2

s’affiche dans `Ski Catalog` une fois la ressource d’activation publiée.

![chlimage_1-422](assets/chlimage_1-422.png)

## Affichage du catalogue lors de la publication {#viewing-catalog-on-publish}

Une fois que tout a été configuré par l’auteur  le  et publié, l’expérience d’utilisation du catalogue pour trouver des ressources d’activation peut être expérimentée dans le de publication .

Si aucune balise   n’apparaît dans la liste déroulante, assurez-vous que les autorisations ont été correctement définies dans le de publication .

Si des balises   ont été ajoutées et sont manquantes, vérifiez que les balises et le site ont été republiés.

Si aucune ressource d’activation ne s’affiche après avoir sélectionné une balise lors de l’affichage du catalogue, assurez-vous qu’une balise issue des  du catalogue est appliquée à la ressource d’activation.

![chlimage_1-423](assets/chlimage_1-423.png)

