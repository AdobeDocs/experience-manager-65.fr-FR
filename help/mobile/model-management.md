---
title: Modèles - Aperçu
description: Découvrez comment utiliser la gestion des modèles, qui implique la création et la gestion de modèles à associer à d’éventuels objets de données.
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 50785534-5784-4354-b123-5e640b7c0242
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Modèles - Aperçu{#models-overview}

{{ue-over-mobile}}

La gestion des modèles implique la création et la gestion de modèles pour l’association avec d’éventuels objets de données. Chaque modèle comprend toutes les propriétés et définitions de champ requises pour faciliter la création et le rendu des objets.

La gestion des modèles implique la création de **modèles**, **entités** et **espaces**. Le diagramme suivant illustre la relation entre le contenu AEM et les modèles.

![chlimage_1-81](assets/chlimage_1-81.png)

## Le modèle de contenu {#the-content-model}

Un modèle décrit le type de contenu et indique les informations disponibles pour l’application native. Il s’agit d’une description de ce qui constitue un élément de contenu. Un modèle de contenu est la règle pour créer un élément de contenu. Le modèle de contenu inclut les données disponibles, les ressources pouvant être utilisées, la relation entre les ressources et les données, la relation avec d’autres modèles de contenu et les métadonnées disponibles.

Les modèles servent également à transformer le contenu AEM existant en objets qui peuvent être facilement utilisés par les applications mobiles natives.

Content Services fournit quelques modèles prêts à l’emploi pour les objets courants tels que les ressources, les collections de ressources, les pages d’HTML, les configurations d’application et les pages indépendantes du canal. Ils sont configurables afin de répondre aux besoins spécifiques des clients sans nécessiter d’effort de développement AEM.

Les utilisateurs peuvent créer leurs propres modèles. Cela permet la création de nouveaux types de contenu qui ne sont pas déjà gérés par AEM. La création du modèle est effectuée via une interface utilisateur à l’aide de types primitifs existants.

Le diagramme suivant illustre le modèle de contenu des applications AEM Mobile et la manière dont les entités, les dossiers et les espaces sont affectés à une application.

![chlimage_1-82](assets/chlimage_1-82.png)

### Les modèles {#the-models}

Les modèles sont utilisés pour déterminer comment les entités sont créées. Ils définissent ce qui est disponible dans une entité et comment ces données sont générées à partir du contenu AEM. Avant de commencer à utiliser les espaces, les dossiers et les entités, vous devez vous familiariser avec la création et la gestion des modèles.

>[!NOTE]
>
>Un modèle existe en dehors d’une application, car plusieurs applications peuvent l’utiliser.
>

Pour créer et gérer des modèles dans le tableau de bord et le référentiel, voir **[Modèles](/help/mobile/administer-mobile-apps.md)**.

### Entités dans le modèle de contenu {#entities-in-content-model}

Une entité est une instance d’un modèle de contenu. Une entité est exposée via l’API Content Services à la bibliothèque côté client et permet à une application native d’accéder au contenu indépendamment du canal.

S’il existe du contenu AEM, une entité est générée à l’aide d’un modèle et de la source de contenu AEM. Par exemple, une entité de page est un objet indépendant du canal et de la mise en page généré à partir d’une page AEM et du modèle de page.

Les modifications apportées au contenu référencé d’une entité entraînent une modification de l’entité. Par exemple, si un *cq:page* est mis à jour, toutes les entités basées sur cette page sont également mises à jour.

Pour créer des entités personnalisées à partir de modèles, voir **[Utilisation d’entités](/help/mobile/spaces-and-entities.md)**.

>[!NOTE]
>
>Si le modèle ne correspond pas à un contenu AEM existant, comme c’est le cas lorsque le client a créé un modèle, il existe une interface utilisateur permettant au client de créer une entité.
>

### Espaces dans le modèle de contenu {#spaces-in-content-model}

Un espace est utilisé pour organiser les entités afin d’en faciliter l’accès. Un espace peut contenir un ou plusieurs types d&#39;entités et peut contenir des sous-dossiers.

Du côté d’AEM, un espace est un moyen pratique de gérer les entités associées. Il peut également être utilisé pour attribuer des autorisations. Une autorisation peut être accordée à un espace, ce qui protège les entités qui se trouvent dans cet espace.

*Par exemple*,

Un utilisateur possède trois classifications générales d’entités. L’un est réservé à un usage interne uniquement, un autre est approuvé pour un usage public et un troisième est toujours destiné à des entités courantes utilisées par de nombreuses applications. Pour faciliter la gestion, l&#39;utilisateur crée trois espaces, à savoir *interne*, *public* (avec des contenus en anglais et en français) et *commun* pour gérer les entités appropriées comme mentionné ci-dessous :

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

Un point d’entrée de service est fourni à l’espace afin que la bibliothèque cliente native puisse demander la liste du contenu d’un espace. Cette « liste » est renvoyée sous la forme d’un objet JSON.

Voir **[Espaces et entités](/help/mobile/spaces-and-entities.md)** pour créer et publier des espaces.

>[!NOTE]
>
>Un espace peut être utilisé par de nombreuses applications et une application peut utiliser de nombreux espaces.

### Dossiers dans le modèle de contenu {#folders-in-content-model}

Les dossiers permettent aux utilisateurs d’organiser les entités selon leurs besoins et facilitent un contrôle plus fin des listes de contrôle d’accès. Les espaces peuvent inclure des dossiers pour mieux organiser le contenu et les ressources de l’espace. Un utilisateur peut créer sa propre hiérarchie sous un espace.

Pour créer et gérer des dossiers dans un espace, voir **[Utilisation de dossiers dans un espace](/help/mobile/spaces-and-entities.md)**.
