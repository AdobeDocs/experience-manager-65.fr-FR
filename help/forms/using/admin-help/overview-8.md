---
title: Présentation du service de sortie
description: Output permet de fusionner des données de formulaire XML dans une conception de formulaire créée dans Designer afin de créer un flux de sortie de documents dans différents formats.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '260'
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
* Définition des polices à incorporer. (Voir [Définition des polices à incorporer](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Définition des options de configuration XCI. (Voir [Définition des options de configuration XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Définition des paramètres de protection. (Voir [Définition des paramètres de sécurité](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Après avoir modifié les paramètres, cliquez sur Enregistrer pour les appliquer à Output. Vous n’avez pas besoin de redémarrer le serveur pour que les modifications prennent effet, mais vous devrez peut-être redémarrer le service Output lors de la configuration des paramètres du cache.
