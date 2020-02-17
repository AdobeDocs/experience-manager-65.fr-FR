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
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Modèles dans le référentiel{#models-in-repository}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Un modèle contient un ensemble de types de données qui définissent les propriétés qui seront finalement rendues par Content Services. Un modèle définit également les relations entre les autres modèles afin d’assurer l’intégrité des données.

En tant que développeur, vous devez connaître la structure du modèle dans le référentiel. Vous pouvez créer vos propres modèles et entités en fonction des besoins de votre application.

## Création de types de modèles {#creating-model-types}

Il existe deux types de modèles fournis par le système sous */libs/settings/mobileapps/model-types*. Si vous souhaitez remplacer les types de modèle système, un noeud *mobileapps/model-types* doit être créé sous le noeud de configuration sur lequel vous souhaitez que le remplacement se produise.

Par exemple, si vous avez créé des configurations à */conf/myconf1* et */conf/myconf2* et souhaitez remplacer les types de modèles système sur *conf1* uniquement, vous créerez un noeud *mobileapps/model-types sous les paramètres conf1.***

Si vous souhaitez autoriser l&#39;ajout de types de données à un modèle, le type de modèle doit avoir un noeud enfant nommé &quot;échafaudage&quot; de type &quot;cq:Page&quot; et un type de ressource de *wcm/scaffolding/components/scaffolding*.

La page d’échafaudage doit également inclure une propriété *dataTypesConfig* sur le noeud PageContent qui indique que les modèles de types de données créés à partir de ce type seront autorisés à être utilisés.

>[!NOTE]
>
>Un **échafaudage** est une page qui définit les types de données qui peuvent être modifiés par une entité en fonction du modèle. Chaque type de données peut également être configuré pour définir la présentation du champ dans l’interface utilisateur, ainsi que la manière dont la valeur des données sera conservée.

### Configuration des types de données {#data-types-config}

Le noeud de configuration des types de données contient une liste d’éléments de type de données. Chaque élément de type de données indique comment un type de données apparaîtra dans l&#39;éditeur de modèles, ainsi que la manière dont il doit être conservé pour un rendu éventuel par une entité.

| **Nom de la propriété** | **Description** |
|---|---|
| fieldIcon | classe de l’icône CoralUI représentant le type de données |
| fieldPropResourceType | qui restituera toutes les propriétés de configuration du type de données |
| fieldProperties | liste de plusieurs valeurs des composants de propriété utilisés lorsque fieldPropResourceType est *mobileapps/caas/gui/components/models/editor/datatypes/field* |
| fieldResourceType | resourceType du noeud persistant pour le type de données (c’est-à-dire le composant qui rendra la propriété dans l’éditeur d’entité) |
| fieldViewResourceType | composant à utiliser pour le rendu du type de données dans la vue de l’éditeur de modèles (fieldResourceType sera utilisé si cette propriété est omise) |
| fieldTitle | nom du type de données qui sera affiché dans l&#39;éditeur de modèles |
| multiFieldResourceType | type de ressource à utiliser sur le noeud persistant lorsque plusieurs valeurs sont sélectionnées |
| renderType | indice de rendu pour le rendu côté client |

### Incrustation de configuration des types de données {#data-types-config-overlay}

La propriété &quot;dataTypesConfig&quot; prend en charge la fusion des ressources Sling. Cela signifie que les types de données utilisés par les types de modèles système (ou même les types de modèles personnalisés) peuvent être personnalisés à l’aide de noeuds d’incrustation.

Une superposition de */libs/settings/mobileapps/models/formbuilderconfig/datatypes* devra être créée, puis personnalisée selon vos besoins.

Par exemple, une superposition pour le type de données String peut être ajoutée afin de transformer fieldResourceType en composant personnalisé.

Pour plus d’informations sur la fusion des ressources Sling, voir [Utilisation de la fusion des ressources Sling dans AEM](/help/sites-developing/sling-resource-merger.md).

![chlimage_1-7](assets/chlimage_1-7.png)

### Types de données {#data-types}

Un type de données de modèle est un composant de formulaire capable d’inclure des données à inclure lors de la publication d’un formulaire. Le composant de type de données peut être aussi compliqué que vous le souhaitez. Un exemple de type de données personnalisé peut être un bloc d’adresse pour un pays donné afin d’éviter d’avoir à le recréer tout le temps à l’aide des types de données primitifs.

Voir &#39;/libs/mobileapps/caas/components/form/contentreference&#39; comme exemple de type de données personnalisé.

Tous les types de données primitifs utilisent les composants de formulaire Granite existants. See: [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

Tout type de données personnalisé peut alors être ajouté à une configuration de type de données pour l’utiliser dans l’éditeur de modèles.

## Creating Models {#creating-models}

Vous pouvez commencer à créer des modèles une fois que tous les types de modèles et de données souhaités ont été développés. Les auteurs utiliseront en fin de compte des modèles pour créer des entités à partir desquelles Content Services utilisera les données qu’ils contiennent.

La création d&#39;un modèle consiste à sélectionner un type de modèle autorisé en fonction de la configuration actuelle, puis à fournir un titre et une description.

Pour en savoir plus sur la création et la gestion d&#39;un modèle à partir du tableau de bord, voir [Création d&#39;un modèle](/help/mobile/administer-mobile-apps.md) sous Création d&#39;un modèle dans la section Création pour les applications mobiles.

### Propriétés d’un modèle {#properties-of-a-model}

Le tableau suivant présente les propriétés définies pour un modèle :

| **Nom de la propriété** | **Description** |
|---|---|
| Titre du modèle | nom du modèle |
| Description | description du modèle |
| Miniature | image miniature du modèle |
| Type de modèle | type du modèle (il peut s’agir d’une chaîne simple ou d’un chemin d’accès à un composant réel) |
| Enfants autorisés | chemin d’accès d’un modèle autorisé comme enfant de ce modèle |
| Parents autorisés | chemin d’accès d’un modèle autorisé comme parent de ce modèle |

>[!NOTE]
>
>Les enfants ** autorisés et les propriétés parents ** autorisés suivent les mêmes règles que les modèles de page. For more information, see [Page Templates](/help/sites-developing/page-templates-static.md).
>
>En ce qui concerne la propriété Type *de* modèle, tous les modèles doivent avoir un super-type de *mobileapps/cas/components/data/entity* , mais peuvent avoir un sous-type qui permet de personnaliser la diffusion de contenu. En veillant à ce que tous les types de modèles soient uniques, vous pouvez également aider les clients des services de contenu à distinguer les objets des données.

### Modification d&#39;un modèle {#editing-a-model}

La modification d’un modèle implique l’ouverture du formulaire de boîte de dialogue d’échafaudage associé à un modèle à modifier. En règle générale, l’échafaudage est un noeud enfant du modèle, mais il peut être situé à l’extérieur du modèle si nécessaire en spécifiant son chemin à l’aide de la propriété &quot;cq:scaffolding&quot;. Cela s’avère utile si vous souhaitez partager le même échafaudage entre plusieurs modèles qui doivent avoir des propriétés différentes.

Lorsque l&#39;échafaudage du modèle est localisé, l&#39;éditeur de modèles génère tout ce qui se trouve sous &quot;jcr:content/cq:dialog/content&quot;. Actuellement, seule une mise en page fixe de 3 colonnes au maximum est prise en charge par le moteur du créateur de formulaires côté client. A droite de la boîte de dialogue du formulaire rendu se trouve une liste de tous les types de données spécifiés dans la configuration des types de données. Vous pouvez modifier les types de données en cliquant dessus. Le rail droit passe ensuite à l&#39;onglet Propriétés pour le type de données sélectionné. Vous pouvez ajouter de nouveaux types de données en les faisant glisser sur le canevas d’aperçu. Cliquez sur Enregistrer pour propager les modifications au serveur. Cliquez sur Annuler pour fermer l&#39;éditeur de modèles.

>[!NOTE]
>
>Tous les modèles sont des modèles. Ils suivent donc toutes les règles de modèles AEM. Cela permet d’utiliser des propriétés telles que ** allowedParents et *allowedChildren* . Elles sont efficaces lors de la création de nouvelles entités basées sur un modèle. Les règles de modèle garantissent que les entités ne peuvent être basées que sur certains modèles selon leur hiérarchie.
>
>Pour en savoir plus sur la modification d&#39;un modèle à partir du tableau de bord, voir [Création d&#39;un modèle](/help/mobile/administer-mobile-apps.md) sous Création d&#39;applications mobiles.

### Modèles système {#system-models}

Deux types de modèles système prédéfinis sont fournis pour une réutilisation simple du contenu. Ces modèles ne peuvent pas être modifiés.

**Modèle** de pages Le modèle de pages fournit une méthode rapide pour réutiliser le contenu existant des sites en vue de sa diffusion par les services de contenu.

Le type de ressource des entités basé sur le modèle Pages est : mobileapps/caas/components/data/pages

Chemin : Chemin d’accès à une page Sites. Le contenu de ce chemin (et de ses enfants) sera rendu par les gestionnaires de services de contenu.

**Modèle** Ressources Le modèle Ressources offre une méthode rapide pour réutiliser le contenu existant des Ressources en vue d’une diffusion par les services de contenu.

Le type de ressource des entités basé sur le modèle Pages est : *mobileapps/caas/components/data/assets.*

Liste des ressources : Liste des chemins d’accès des ressources. Chaque ressource est ajoutée en tant que noeud d’entité enfant avec un resourceType de *wcm/foundation/components/image*.

>[!NOTE]
>
>Pour en savoir plus sur l’utilisation de ces modèles pour la création de modèles à partir du tableau de bord, voir [Création d’un modèle](/help/mobile/administer-mobile-apps.md) sous Création d’applications mobiles.
