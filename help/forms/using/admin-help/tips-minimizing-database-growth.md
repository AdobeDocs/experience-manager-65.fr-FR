---
title: Conseils pour minimiser la croissance de la base de données
seo-title: Conseils pour minimiser la croissance de la base de données
description: Les processus de longue durée stockent des données de processus dans la base de données AEM Forms. La croissance de la base de données AEM forms peut être minimisée grâce à quelques stratégies simples de configuration de produit et de conception de processus.
seo-description: Les processus de longue durée stockent des données de processus dans la base de données AEM Forms. La croissance de la base de données AEM forms peut être minimisée grâce à quelques stratégies simples de configuration de produit et de conception de processus.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 100%

---


# Conseils pour minimiser la croissance de la base de données {#tips-for-minimizing-database-growth}

Les processus de longue durée stockent des données de processus dans la base de données AEM Forms. La croissance de la base de données AEM forms peut être minimisée grâce à quelques stratégies simples de configuration de produit et de conception de processus.

## Conseils pour la conception de processus {#process-design-tips}

Dans la mesure du possible, utilisez des processus de longue durée. Les processus de courte durée ne stockent pas de données le concernant dans la base de données. L’inconvénient des processus de courte durée réside dans le fait que leur statut et leur état ne font pas l’objet d’un suivi dans Administration Console et que le système ne stocke aucun historique.

Certaines opérations de service, comme l’opération d’affectation de tâche dans le service User, requièrent des processus de longue durée. Dans ce cas, vous pouvez segmenter le processus en plusieurs sous-processus dont vous raccourcissez la durée dans la mesure du possible. Avec cette stratégie, les sous-processus de courte durée doivent pouvoir gérer les éléments de données volumineux, comme les valeurs de document.

Utilisez les variables avec parcimonie. Si vous exploitez des processus de longue durée, un espace est alloué dans la base de données à chaque variable de chaque instance de processus. L’utilisation stratégique de variables permet d’économiser un espace considérable. Par exemple, vous pouvez remplacer des valeurs de variable lorsque les anciennes valeurs ne sont plus nécessaires au processus. Veillez également à supprimer les variables que vous avez créées et que vous n’exploitez pas. Vous pouvez valider le processus pour identifier les variables inutilisées.

Préférez les types de variable simples (par exemple, string ou int) aux types de variable complexes. La base de données alloue un espace aux variables même lorsque celles-ci ne contiennent aucune valeur. En général, les variables complexes requièrent davantage d’espace que les variables simples.

## Conseils pour l’administration du produit  {#product-administration-tips}

Utilisez efficacement le stockage global de documents. Le répertoire de stockage global de documents sur le serveur Forms permet de stocker, entre autres, les fichiers qui sont transmis aux services AEM Forms dans les processus. Pour améliorer les performances, les documents plus petits sont stockés en mémoire et conservés dans la base de données.

Administration Console s’appuie sur la propriété Taille maximale par défaut de la ligne d’entrée du document, pour configurer la taille maximale des documents stockés en mémoire et maintenus dans la base de données (voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)). Si vous affectez une valeur faible à cette propriété, la plupart des documents sont conservés dans le répertoire de stockage global de documents et non dans la base de données. L’avantage est que vous pouvez plus facilement supprimer des fichiers de ce répertoire lorsqu’ils ne sont plus nécessaires.
