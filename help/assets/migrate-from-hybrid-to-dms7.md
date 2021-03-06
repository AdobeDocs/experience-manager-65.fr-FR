---
title: Migration de Dynamic Media - mode hybride vers Dynamic Media - mode S7
description: Découvrez comment migrer votre instance de Dynamic Media - mode hybride vers Dynamic Media - mode S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Mode Scene7, mode hybride
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 2%

---

# À propos du passage de Dynamic Media-Hybrid à Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid est une ancienne version de l’intégration de Dynamic Media à Adobe Experience Manager. La version hybride a été introduite dans Adobe Experience Manager 6.1. Bien qu’Adobe continue à prendre en charge le mode hybride, il ne s’agit pas du mode préféré. Dynamic Media-Scene7 est le mode préféré. Le mode hybride ne prend pas en charge les nouvelles fonctionnalités telles que le recadrage intelligent et les images panoramiques, tandis que Dynamic Media-Scene7 les prend en charge.

Voici quelques autres différences clés entre Dynamic Media-Hybrid et Dynamic Media-Scene7 :

* Structure des URL.
* Ingestion de vidéos.
* Création et stockage des rendus d’image.
* Configuration et informations d’identification du cloud (mise en service).

Deux options sont disponibles lorsque vous passez de Dynamic Media-Hybrid à Dynamic Media-Scene7. La première option consiste à simplement configurer une nouvelle instance de Dynamic Media-Scene7 sur Experience Manager. La deuxième option consiste à migrer votre instance existante de Dynamic Media-Hybrid vers Dynamic Media-Scene7. Cette option présente sous la forme d’un tableau les étapes et les considérations à prendre en compte lors du déplacement.

>[!IMPORTANT]
>
>Adobe recommande de ne pas migrer une implémentation Dynamic Media hybride vers Dynamic Media-Scene7 sur les instances de production en direct.

## Option 1 - Configuration d’une nouvelle instance de Dynamic Media-Scene7 sur Experience Manager {#provision-new-dms7}

Envisagez simplement de commencer à zéro avec une nouvelle instance configurée de Dynamic Media-Scene7 sur Adobe Experience Manager. Outre l’ingestion et le traitement de ressources par le biais de Dynamic Media Cloud Service, un audit d’Adobe de l’utilisation des ressources, des workflows et des composants est vivement recommandé. Souvent, vous pouvez remplacer des composants et des workflows personnalisés à l’aide de fonctionnalités plus récentes et prêtes à l’emploi.

## Option 2 - Migration de votre instance existante de Dynamic Media-Hybrid vers Dynamic Media-Scene7 {#process-for-migrating}

| Étape | Tâche | Considérations |
|---|---|---|
| 1 | Cloner l’instance d’auteur Dynamic Media-hybride. | Conservez votre instance existante d’auteur Dynamic Media-Hybrid à des fins de secours jusqu’à ce que les étapes restantes de ce processus de migration soient terminées. |
| 2 | Démarrez l’instance d’auteur clonée en mode Dynamic Media-Scene7. |  |
| 3 | Dans les Cloud Services Adobe Experience Manager, configurez Dynamic Media avec les informations d’identification Dynamic Media-Scene7. | Adobe doit approuver la mise en service de Dynamic Media-Scene7. Par conséquent, vous disposez d’environnements Dynamic MediaM-Hybrid et Dynamic Media-Scene7 simultanés, pris en charge par Adobe, mais pour une durée limitée uniquement. |
| 4 | Créez un lot de migration afin de pouvoir ingérer des ressources si nécessaire.<br>Supprimez les fichiers PTIFF locaux créés lors de l’ingestion initiale dans Dynamic Media-Hybrid. | Si toutes les ressources sont actuellement disponibles dans votre instance Dynamic Media-Hybrid, un clone de ces ressources les inclut déjà toutes. Par conséquent, aucun lot n’est nécessaire. |
| 5 | Exécutez le workflow de mise à jour des ressources afin de synchroniser les ressources avec Dynamic Media Cloud Service. | Adobe vous recommande d’exécuter le workflow de mise à jour par lots pour permettre la compression. |
| 6 | Migration des paramètres prédéfinis de visionneuse, d’image et de vidéo. |  |
| 7 | Parcourez chaque ressource référencée de la gestion de contenu web et mettez à jour les URL associées. |  |
| 8 | Migrez tous les workflows personnalisés que vous souhaitez prendre en charge le nouveau mode Dynamic Media-Scene7 (mises à jour manuelles). |  |
| 9 | Vérifiez le téléchargement et la configuration de la gestion de contenu web. |  |
| 10 | Après vérification, obtenez une approbation pour désactiver Dynamic Media-Hybrid Author (conserver comme solution de secours). |  |
| 11 | Supprimez l’instance Dynamic Media-Hybrid Author après environ un mois d’utilisation réussie de Dynamic Media-Scene7. |  |
