---
title: Conseils pour minimiser la croissance de la base de données
description: Les processus de longue durée stockent les données de processus dans la base de données d’AEM forms. La croissance de la base de données d’AEM forms peut être réduite à l’aide de quelques stratégies de configuration de produit et de conception de processus simples.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Conseils pour minimiser la croissance de la base de données {#tips-for-minimizing-database-growth}

Les processus de longue durée stockent les données de processus dans la base de données d’AEM forms. La croissance de la base de données d’AEM forms peut être réduite à l’aide de quelques stratégies de configuration de produit et de conception de processus simples.

## Conseils sur la conception de processus {#process-design-tips}

Dans la mesure du possible, utilisez des processus de courte durée. Les processus de courte durée ne stockent pas de données de processus dans la base de données. L’inconvénient des processus de courte durée est que leur état et leur état ne sont pas suivis dans la console d’administration et qu’il n’existe aucun historique du processus.

Certaines opérations de service, telles que l’opération Assign Task (service User), nécessitent qu’elles soient utilisées dans des processus de longue durée. Dans ce cas, vous pouvez segmenter le processus en plusieurs sous-processus et les rendre de courte durée lorsque cela est possible. Si vous utilisez cette stratégie, les sous-processus de courte durée doivent gérer des éléments de données volumineux, tels que les valeurs de document.

Utilisez les variables avec parcimonie. Lors de l’utilisation de processus de longue durée, pour chaque instance de processus, de l’espace est alloué sur la base de données pour chaque variable du processus. L’utilisation stratégique de variables peut réduire considérablement l’espace. Par exemple, vous pouvez remplacer des valeurs de variable lorsque les anciennes valeurs ne sont plus nécessaires dans le processus. Supprimez également les variables que vous avez créées et que vous n’utilisez pas. Vous pouvez valider le processus pour rechercher des variables inutilisées.

Utilisez des types de variable simples (par exemple, string ou int) et évitez d’utiliser des types de variable complexes lorsque cela est possible. L’espace de base de données est alloué aux variables même lorsqu’elles ne contiennent pas de valeur. Les variables complexes requièrent généralement plus d’espace que les variables simples.

## Conseils d’administration de produit {#product-administration-tips}

Utilisez efficacement le stockage global de documents. Le répertoire de stockage global de documents sur le serveur Forms est utilisé pour stocker, entre autres, les fichiers transmis aux services faisant partie d’AEM forms dans les processus. Pour améliorer les performances, les documents plus petits sont stockés en mémoire et conservés dans la base de données.

Administration Console expose la propriété Taille maximale par défaut de la ligne d’entrée du document pour configurer la taille maximale des documents stockés en mémoire et conservés dans la base de données. (voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)). Si vous définissez cette propriété sur une valeur faible, la plupart des documents sont conservés dans le répertoire de stockage global de documents et non dans la base de données. L’avantage est de pouvoir supprimer plus facilement les fichiers qui ne sont plus nécessaires lorsqu’ils sont stockés dans le répertoire de stockage global de documents.
