---
title: Présentation du service de sortie
description: Output permet de fusionner des données de formulaire XML dans une conception de formulaire créée dans Designer afin de créer un flux de sortie de documents dans différents formats.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 100%
---
# Présentation du service de sortie {#overview-of-output-service}

Output permet de fusionner des données de formulaire XML dans une conception de formulaire créée dans Designer afin de créer un flux de sortie de documents dans différents formats. Le flux de sortie peut être envoyé vers une imprimante réseau, une imprimante locale ou un fichier de disque.

Vous pouvez utiliser la page Output de la console d’administration pour administrer le service Output. Les paramètres que vous configurez sont utilisés au moment de l’exécution lorsque les paramètres équivalents n’ont pas été spécifiés via l’API AEM Forms. La configuration effectuée via le SDK AEM Forms remplace les paramètres configurés à l’aide de la console d’administration.

Pour plus d’informations sur le service Output, consultez le [guide de référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

Sur les pages Output de la console d’administration, vous pouvez exécuter les tâches suivantes :

* Indiquer des jeux de caractères pour l’internationalisation. (Voir [Modification du jeu de caractères](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Spécifier les chemins d’accès absolus et relatifs pour les URL, les URI, les XCI et les emplacements de fichiers. (Voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configurer la taille de la mémoire cache et la politque de mise en cache. (Voir [Définition du mode de cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) et [Configuration des paramètres du cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Rendre les polices disponibles sur le serveur d’applications. (Voir [Rendre les polices disponibles](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Spécifier les polices à incorporer. (Voir [Définition des polices à incorporer](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Définition des options de configuration XCI. (Voir [Définition des options de configuration XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Définition des paramètres de protection. (Voir [Définition des paramètres de sécurité](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Après avoir modifié les paramètres, cliquez sur Enregistrer pour les appliquer à Output. Vous n’avez pas besoin de redémarrer le serveur pour que les modifications prennent effet, mais vous devrez peut-être redémarrer le service Output lors de la configuration des paramètres du cache.
