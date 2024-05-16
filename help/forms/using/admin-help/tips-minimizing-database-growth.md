---
title: Conseils pour minimiser la croissance de la base de données
description: Les processus de longue durée stockent des données de processus dans la base de données AEM Forms. La croissance de la base de données AEM Forms peut être minimisée grâce à quelques stratégies simples de configuration de produit et de conception de processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '408'
ht-degree: 100%

---

# Conseils pour minimiser la croissance de la base de données {#tips-for-minimizing-database-growth}

Les processus de longue durée stockent des données de processus dans la base de données AEM Forms. La croissance de la base de données AEM Forms peut être minimisée grâce à quelques stratégies simples de configuration de produit et de conception de processus.

## Conseils pour la conception de processus {#process-design-tips}

Dans la mesure du possible, utilisez des processus de courte durée. Les processus de courte durée ne stockent pas de données de processus dans la base de données. L’inconvénient des processus de courte durée réside dans le fait que leur statut et leur état ne font pas l’objet d’un suivi dans la console d’administration et que le système ne stocke aucun historique.

Certaines opérations de service, comme l’opération d’affectation de tâche dans le service Utilisateur, requièrent des processus de longue durée. Dans ce cas, vous pouvez segmenter le processus en plusieurs sous-processus dont vous raccourcissez la durée dans la mesure du possible. Avec cette stratégie, les sous-processus de courte durée doivent pouvoir gérer les éléments de données volumineux, comme les valeurs de document.

Utilisez les variables avec parcimonie. Si vous exploitez des processus de longue durée, un espace est alloué dans la base de données à chaque variable de chaque instance de processus. L’utilisation stratégique de variables permet d’économiser un espace considérable. Par exemple, vous pouvez remplacer des valeurs de variable lorsque les anciennes valeurs ne sont plus nécessaires au processus. Veillez également à supprimer les variables que vous avez créées et que vous n’exploitez pas. Vous pouvez valider le processus pour identifier les variables inutilisées.

Préférez les types de variable simples (par exemple, string ou int) aux types de variable complexes. La base de données alloue un espace aux variables même lorsque celles-ci ne contiennent aucune valeur. En général, les variables complexes requièrent davantage d’espace que les variables simples.

## Conseils pour l’administration du produit {#product-administration-tips}

Utilisez efficacement le stockage global de documents. Le répertoire de stockage global de documents sur le serveur Forms Server permet de stocker, entre autres, les fichiers qui sont transmis aux services AEM Forms dans les processus. Pour améliorer les performances, les documents plus petits sont stockés en mémoire et conservés dans la base de données.

La console d’administration s’appuie sur la propriété Taille maximale par défaut de la ligne d’entrée du document, pour configurer la taille maximale des documents stockés en mémoire et maintenus dans la base de données. (voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)). Si vous affectez une valeur faible à cette propriété, la plupart des documents sont conservés dans le répertoire de stockage global de documents et non dans la base de données. L’avantage est que vous pouvez plus facilement supprimer des fichiers de ce répertoire lorsqu’ils ne sont plus nécessaires.
