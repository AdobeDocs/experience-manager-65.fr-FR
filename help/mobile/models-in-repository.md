---
title: Modèles dans le référentiel
seo-title: Modèles dans le référentiel
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 2%

---


# Modèles dans le référentiel{#models-in-repository}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Un modèle contient un ensemble de types de données qui définissent les propriétés qui seront finalement rendues par les services de contenu. Un modèle définit également les relations entre les autres modèles afin d’appliquer l’intégrité des données.

En tant que développeur, vous devez connaître la structure du modèle dans le référentiel. Vous pouvez créer vos propres modèles et entités en fonction des besoins de votre application.

## Création de types de modèle {#creating-model-types}

Il existe deux types de modèle fournis par le système sous */libs/settings/mobileapps/model-types*. Si vous souhaitez remplacer les types de modèle système, un noeud *mobileapps/model-types* doit être créé sous le noeud de configuration sur lequel vous souhaitez que le remplacement se produise.

Par exemple, si vous avez créé des configurations à */conf/myconf1* et */conf/myconf2* et que vous souhaitez remplacer les types de modèle système uniquement sur *conf1*, vous créez un noeud *mobileapps/model-types* sous les paramètres de *conf1*.

Si vous souhaitez autoriser l’ajout de types de données à un modèle, le type de modèle doit comporter un noeud enfant nommé &quot;scaffolding&quot; de type &quot;cq:Page&quot; et un type de ressource *wcm/scaffolding/components/scaffolding*.

La page de génération de modèles automatique doit également inclure une propriété *dataTypesConfig* sur le noeud PageContent qui indique que les modèles de types de données créés à partir de ce type seront autorisés à être utilisés.

>[!NOTE]
>
>Un **Scaffolding** est une page qui définit les types de données qui peuvent être modifiés par une entité en fonction du modèle. Chaque type de données peut également être configuré pour définir comment le champ sera présenté dans l’interface utilisateur, ainsi que la manière dont la valeur de données sera conservée.

### Configuration des types de données {#data-types-config}

Le noeud de configuration des types de données contient une liste d’éléments de type de données. Chaque élément de type de données indique comment un type de données apparaîtra dans l’éditeur de modèles ainsi que la manière dont il doit être conservé pour un rendu éventuel par une entité.

| **Nom de la propriété** | **Description** |
|---|---|
| fieldIcon | classe de l’icône CoralUI pour représenter le type de données |
| fieldPropResourceType | composant qui affiche toutes les propriétés pour la configuration du type de données |
| fieldProperties | liste à plusieurs valeurs des composants de propriété utilisés lorsque fieldPropResourceType est *mobileapps/caas/gui/components/models/editor/datatypes/field* |
| fieldResourceType | resourceType du noeud persistant pour le type de données (c’est-à-dire le composant qui effectuera le rendu de la propriété dans l’éditeur d’entité) |
| fieldViewResourceType | composant à utiliser pour le type de données de rendu dans la vue de l’éditeur de modèles (fieldResourceType sera utilisé si cette propriété est omise). |
| fieldTitle | nom du type de données qui sera affiché dans l’éditeur de modèles |
| multiFieldResourceType | type de ressource à utiliser sur le noeud persistant lorsque plusieurs valeurs sont sélectionnées |
| renderType | indice de rendu pour le rendu côté client |

### Superposition de configuration des types de données {#data-types-config-overlay}

La propriété &#39;dataTypesConfig&#39; prend en charge la fusion des ressources Sling. Cela signifie que les types de données utilisés par les types de modèle système (ou même les types de modèle personnalisés) peuvent être personnalisés à l’aide de noeuds de recouvrement.

Une superposition de */libs/settings/mobileapps/models/formbuilderconfig/datatypes* devra être créée, puis personnalisée selon vos besoins.

Par exemple, une superposition pour le type de données String peut être ajoutée afin de remplacer fieldResourceType par un composant personnalisé.

Pour plus d’informations sur la fusion des ressources Sling, voir [Utilisation de Sling Resource Merger dans AEM](/help/sites-developing/sling-resource-merger.md).

![chlimage_1-7](assets/chlimage_1-7.png)

### Types de données {#data-types}

Un type de données de modèle est un composant de formulaire capable d’inclure des données lors de la publication d’un formulaire. Le composant de type de données peut être aussi complexe que vous le souhaitez. Un exemple de type de données personnalisé peut être un bloc d’adresse pour un pays particulier afin d’éviter d’avoir à le recréer tout le temps à l’aide des types de données primitifs.

Voir &#39;/libs/mobileapps/caas/components/form/contentreference&#39; comme exemple de type de données personnalisé.

Tous les types de données primitifs utilisent des composants de formulaire Granite existants. Voir : [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

Tout type de données personnalisé peut ensuite être ajouté à une configuration de type de données à utiliser par l’éditeur de modèles.

## Création de modèles {#creating-models}

Vous pouvez commencer à créer des modèles une fois que tous les types de modèle et de données souhaités ont été développés. Les auteurs finiront par utiliser des modèles pour créer des entités à partir desquelles Content Services utilise pour effectuer le rendu de ses données.

La création d’un modèle consiste à sélectionner un type de modèle autorisé en fonction de la configuration actuelle, puis à fournir un titre et une description.

Pour en savoir plus sur la création et la gestion d’un modèle à partir du tableau de bord, voir [Création d’un modèle](/help/mobile/administer-mobile-apps.md) sous la section Création pour les applications mobiles.

### Propriétés d’un modèle {#properties-of-a-model}

Le tableau suivant affiche les propriétés définies pour un modèle :

| **Nom de la propriété** | **Description** |
|---|---|
| Titre du modèle | nom du modèle |
| Description | description du modèle |
| Miniature  | image miniature du modèle |
| Type de modèle | type du modèle (il peut s’agir d’une chaîne simple ou d’un chemin d’accès à un composant réel). |
| Enfants autorisés | chemin d’accès d’un modèle autorisé à être un enfant de ce modèle |
| Parents autorisés | chemin d’accès d’un modèle autorisé à être un parent de ce modèle |

>[!NOTE]
>
>Les propriétés *enfants autorisés* et *parents autorisés* suivent les mêmes règles que les modèles de page. Pour plus d’informations, voir [Modèles de page](/help/sites-developing/page-templates-static.md).
>
>En référence à la propriété *Type de modèle* , tous les modèles doivent avoir un super type *mobileapps/caas/components/data/entity*, mais peuvent avoir un sous-type qui permet de personnaliser la diffusion de contenu. Le fait de s’assurer que tous les types de modèle sont uniques peut également aider les clients des services de contenu à distinguer les objets dans les données.

### Modification d’un modèle {#editing-a-model}

La modification d’un modèle implique l’ouverture du formulaire de boîte de dialogue de génération de modèles automatique associé à un modèle pour modification. En règle générale, la génération de modèles automatique est un noeud enfant du modèle, mais elle peut être située en dehors du modèle si vous le souhaitez en spécifiant son chemin d’accès à l’aide de la propriété &quot;cq:scaffolding&quot;. Cela s’avère utile si vous souhaitez partager le même échafaudage entre plusieurs modèles qui doivent avoir des propriétés différentes.

Lorsque le modèle est localisé, l’éditeur de modèles génère tout ce qui se trouve sous &quot;jcr:content/cq:dialog/content&quot;. Actuellement, seule une mise en page fixe de 3 colonnes au maximum est prise en charge par le moteur de créateur de formulaires côté client. La liste de tous les types de données spécifiés dans la configuration des types de données se trouve à droite de la boîte de dialogue de formulaire rendu. Vous pouvez modifier les types de données en cliquant dessus. Le rail de droite passe alors à l’onglet Propriétés pour le type de données sélectionné. De nouveaux types de données peuvent être ajoutés en les faisant glisser sur le canevas de prévisualisation. Cliquez sur Enregistrer pour propager les modifications au serveur. Cliquez sur Annuler pour fermer l’éditeur de modèles.

>[!NOTE]
>
>Tous les modèles sont des modèles, ils suivent donc toutes les règles de modèle AEM. Cela permet d’utiliser des propriétés telles que les propriétés *allowedParents* et *allowedChildren*. Elles sont efficaces lors de la création d’entités basées sur un modèle. Les règles de modèle garantissent que les entités ne peuvent être basées que sur certains modèles selon leur hiérarchie.
>
>Pour en savoir plus sur la modification d’un modèle à partir du tableau de bord, voir [Création d’un modèle](/help/mobile/administer-mobile-apps.md) sous la section Création pour les applications mobiles.

### Modèles système {#system-models}

Deux types de modèles système prédéfinis sont fournis pour une réutilisation simple du contenu. Ces modèles ne peuvent pas être modifiés.

**** Modèle de pagesLe modèle Pages fournit une méthode rapide pour réutiliser du contenu existant de Sites pour une diffusion par des services de contenu.

Le resourceType des entités basé sur le modèle Pages est : mobileapps/caas/components/data/pages

Chemin : Chemin d’accès à une page Sites. Le contenu de ce chemin (et de ses enfants) sera rendu par les gestionnaires de services de contenu.

**** Modèle AssetsLe modèle Assets fournit une méthode rapide pour réutiliser du contenu existant d’Assets en vue de sa diffusion par les services de contenu.

Le resourceType des entités basé sur le modèle Pages est : *mobileapps/caas/components/data/assets.*

Liste des ressources : Liste des chemins d’accès à partir d’Assets. Chaque ressource est ajoutée en tant que noeud d’entité enfant avec un resourceType *wcm/foundation/components/image*.

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation de ces modèles pour créer des modèles à partir du tableau de bord, voir [Création d’un modèle](/help/mobile/administer-mobile-apps.md) sous la section Création pour les applications mobiles.
