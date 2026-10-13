---
title: Conseils pour minimiser la croissance de la base de données
description: Les processus de longue durée stockent des données de processus dans la base de données AEM Forms. La croissance de la base de données AEM Forms peut être minimisée grâce à quelques stratégies simples de configuration de produit et de conception de processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 94%
---
# Conseils pour minimiser la croissance de la base de données {#tips-for-minimizing-database-growth}

Les processus de longue durée stockent des données de processus dans la base de données AEM Forms. La croissance de la base de données AEM Forms peut être minimisée grâce à quelques stratégies simples de configuration de produit et de conception de processus.

## Conseils pour la conception de processus {#process-design-tips}

Dans la mesure du possible, utilisez des processus de courte durée. Les processus de courte durée ne stockent pas de données de processus dans la base de données. L’inconvénient des processus de courte durée réside dans le fait que leur statut et leur état ne font pas l’objet d’un suivi dans la console d’administration et qu’il n’existe aucun historique du processus.

Certaines opérations de service, comme l’opération d’affectation de tâche dans le service Utilisateur, doivent être utilisées dans des processus de longue durée. Dans ce cas, vous pouvez segmenter le processus en plusieurs sous-processus dont vous raccourcissez la durée dans la mesure du possible. Avec cette stratégie, les sous-processus de courte durée doivent gérer les éléments de données volumineux, comme les valeurs de document.

Utilisez les variables avec parcimonie. Si vous exploitez des processus de longue durée, un espace est alloué dans la base de données à chaque variable de chaque instance de processus. L’utilisation stratégique de variables permet d’économiser un espace considérable. Par exemple, vous pouvez remplacer des valeurs de variable lorsque les anciennes valeurs ne sont plus nécessaires au processus. Veillez également à supprimer les variables que vous avez créées et que vous n’exploitez pas. Vous pouvez valider le processus pour identifier les variables inutilisées.

Utilisez des types de variable simples (par exemple, string ou int) et évitez d’utiliser des types de variable complexes lorsque cela est possible. La base de données alloue un espace aux variables même lorsque celles-ci ne contiennent aucune valeur. En général, les variables complexes requièrent davantage d’espace que les variables simples.

## Conseils pour l’administration du produit {#product-administration-tips}

Utilisez efficacement le stockage global de documents (GDS). Le répertoire de stockage global de documents sur le serveur Forms Server permet de stocker, entre autres, les fichiers qui sont transmis aux services AEM Forms dans les processus. Pour améliorer les performances, les documents plus petits sont stockés en mémoire et conservés dans la base de données.

La console d’administration s’appuie sur la propriété Taille maximale par défaut de la ligne d’entrée du document, pour configurer la taille maximale des documents stockés en mémoire et maintenus dans la base de données. (voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)). Si vous définissez cette propriété sur une valeur faible, la plupart des documents sont conservés dans le répertoire de stockage global de documents plutôt que dans la base de données. L’avantage est que vous pouvez plus facilement supprimer des fichiers de ce répertoire lorsqu’ils ne sont plus nécessaires.
