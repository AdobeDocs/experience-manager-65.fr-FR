---
title: Présentation des modèles
seo-title: Présentation des modèles
description: Présentation des modèles
seo-description: 'null'
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---


# Présentation des modèles{#models-overview}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

La gestion des modèles implique la création et la gestion de modèles dans le but d&#39;associer des objets de données éventuels. Chaque modèle comprend toutes les propriétés et définitions de champ nécessaires pour faciliter la création et le rendu des objets.

La gestion des modèles implique la création de **modèles**, **entités** et **espaces**. Le diagramme suivant illustre la relation entre le contenu AEM et les modèles.

![chlimage_1-81](assets/chlimage_1-81.png)

## Modèle de contenu {#the-content-model}

Un modèle décrit le type de contenu et indique quelles informations seront disponibles pour l’application native. Il s’agit d’une description de ce qui constitue un élément de contenu. Un modèle de contenu est la règle pour créer un élément de contenu. Le modèle de contenu inclut les données disponibles, les ressources pouvant être utilisées, la relation entre les ressources et les données, la relation avec d’autres modèles de contenu et les métadonnées disponibles.

Les modèles servent également à transformer le contenu AEM existant en objets faciles à utiliser par les applications mobiles natives.

Content Services fournit quelques modèles prêts à l’emploi pour les objets courants tels que les ressources, les collections de ressources, les pages HTML, les configurations d’application et les pages indépendantes du canal. Ils seront configurables de manière à répondre aux besoins spécifiques des clients sans nécessiter un effort de développement AEM.

L’utilisateur peut créer ses propres modèles. Cela permet la création de nouveaux types de contenu qui ne sont pas encore gérés par AEM. La création de modèle se fait via une interface utilisateur utilisant des types primitifs existants.

Le diagramme suivant illustre le modèle de contenu pour les applications AEM Mobile et comment les entités, les dossiers et les espaces sont affectés à une application.

![chlimage_1-82](assets/chlimage_1-82.png)

### Les modèles {#the-models}

Les modèles sont utilisés pour déterminer comment les entités sont créées. Ils définissent ce qui est disponible dans une entité et comment ces données sont générées à partir du contenu AEM. Avant de début à travailler avec des espaces, des dossiers et des entités, vous devez maîtriser la création et la gestion de modèles.

>[!NOTE]
>
>Un modèle existe en dehors d’une application, car plusieurs applications peuvent l’utiliser.


Voir **[Modèles](/help/mobile/administer-mobile-apps.md)** pour créer et gérer des modèles dans le tableau de bord et le référentiel.

### Entités dans le modèle de contenu {#entities-in-content-model}

Une entité est une instance d’un modèle de contenu. Une entité est exposée à la bibliothèque côté client via l’API Content Services et permet à une application native d’accéder au contenu de manière indépendante du canal.

Dans le cas d’un contenu AEM existant, une entité est générée à l’aide d’un modèle et de la source de contenu AEM. Par exemple, une entité de page est un objet indépendant du canal et de la mise en page qui est généré à partir d’une page AEM et du modèle de page.

Les modifications apportées au contenu référencé d&#39;une entité entraînent une modification de l&#39;entité. Par exemple, si un *cq:page* est mis à jour, toutes les entités basées sur cette page seront également mises à jour.

Voir **[Utilisation d&#39;entités](/help/mobile/spaces-and-entities.md)** pour créer des entités personnalisées à partir de modèles.

>[!NOTE]
>
>Si le modèle ne correspond pas à un contenu AEM existant, tel que le client a créé un nouveau modèle, une interface utilisateur sera créée afin qu’un client puisse créer une nouvelle entité.


### Espaces dans le modèle de contenu {#spaces-in-content-model}

Un espace est utilisé pour organiser les entités pour un accès facile. Un espace peut contenir un ou plusieurs types d&#39;entité et peut contenir des sous-dossiers.

Du côté AEM, un espace est un moyen pratique de gérer les entités qui sont liées. Il peut également être utilisé pour attribuer des autorisations. L&#39;autorisation peut être accordée à un espace, qui protégera alors les entités qui se trouvent dans cet espace.

*Par exemple*,

Un utilisateur possède trois classifications générales d&#39;entités. L&#39;une est destinée à un usage interne uniquement, l&#39;autre est approuvée pour un usage public et encore une troisième concerne les entités communes utilisées par de nombreuses applications. Pour faciliter la gestion, l’utilisateur crée trois espaces : *internal*, *public* (avec du contenu en anglais et en français) et *common* pour gérer les entités appropriées, comme indiqué ci-dessous :

* /content/entités/internal
* /content/entités/public/fr
* /content/entités/public/fr
* /content/entités/common

Un point de terminaison de service sera fourni à l’espace afin que la bibliothèque cliente native puisse demander une liste du contenu d’un espace. Cette &quot;liste&quot; est renvoyée sous la forme d’un objet JSON.

Voir **[Espaces et entités](/help/mobile/spaces-and-entities.md)** pour la création et la publication d’espaces.

>[!NOTE]
>
>Un espace peut être utilisé par de nombreuses applications et une application peut utiliser de nombreux espaces.

### Dossiers dans le modèle de contenu {#folders-in-content-model}

Les dossiers permettent aux utilisateurs d&#39;organiser les entités selon les besoins et facilitent un contrôle de liste de contrôle d&#39;accès plus précis. Les espaces peuvent inclure des dossiers pour mieux organiser le contenu et les ressources de l’espace. Un utilisateur peut créer sa propre hiérarchie sous un espace.

Voir **[Utilisation de dossiers dans un espace](/help/mobile/spaces-and-entities.md)** pour créer et gérer des dossiers dans un espace.
