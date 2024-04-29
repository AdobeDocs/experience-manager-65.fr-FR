---
title: Migration de Dynamic Media en mode hybride vers Dynamic Media en mode S7
description: Découvrez comment migrer votre instance de Dynamic Media en mode hybride vers Dynamic Media en mode S7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '527'
ht-degree: 100%

---

# À propos du passage de Dynamic Media en mode hybride à Dynamic Media en mode Scene7 {#about-migrating}

Dynamic Media en mode hybride est une ancienne version de l’intégration de Dynamic Media à Adobe Experience Manager. La version hybride a été introduite dans Adobe Experience Manager 6.1. Bien qu’Adobe continue à prendre en charge le mode hybride, il ne s’agit pas du mode préconisé, qui est Dynamic Media en mode Scene7. Le mode hybride ne prend pas en charge les nouvelles fonctionnalités telles que le recadrage intelligent et les images panoramiques, tandis que Dynamic Media en mode Scene7 les prend en charge.

Voici quelques autres différences clés entre Dynamic Media en mode hybride et Dynamic Media en mode Scene7 :

* Structure des URL
* Ingestion de vidéos
* Création et stockage des rendus d’image
* Configuration et informations d’identification du cloud (mise en service)

Deux options sont disponibles lorsque vous passez de Dynamic Media en mode hybride à Dynamic Media en mode Scene7. La première option consiste à simplement configurer une nouvelle instance de Dynamic Media en mode Scene7 sur Experience Manager. La deuxième option consiste à migrer votre instance existante de Dynamic Media en mode hybride vers Dynamic Media en mode Scene7. Cette option présente sous la forme d’un tableau les étapes et les considérations à prendre en compte lors de la migration.

>[!IMPORTANT]
>
>Adobe recommande de ne pas migrer une implémentation Dynamic Media hybride vers Dynamic Media en mode Scene7 sur les instances d’exploitation en direct.

## Option 1 – Configuration d’une nouvelle instance de Dynamic Media en mode Scene7 sur Experience Manager {#provision-new-dms7}

Envisagez simplement de commencer à zéro avec une nouvelle instance configurée de Dynamic Media en mode Scene7 sur Adobe Experience Manager. Outre l’ingestion et le traitement de ressources par le biais su service cloud Dynamic Media, il est vivement recommandé de réaliser un audit d’Adobe de l’utilisation des ressources, des workflows et des composants. Souvent, vous pouvez remplacer des composants et des workflows personnalisés à l’aide de fonctionnalités plus récentes et prêtes à l’emploi.

## Option 2 – Migration de votre instance existante de Dynamic Media en mode hybride vers Dynamic Media en mode Scene7 {#process-for-migrating}

| Étape | Tâche | Considérations |
|---|---|---|
| 1 | Clonez l’instance d’auteur Dynamic Media en mode hybride. | Conservez votre instance existante d’auteur Dynamic Media en mode hybride comme instance de secours jusqu’à ce que les étapes restantes de ce processus de migration soient terminées. |
| 2 | Démarrez l’instance d’auteur clonée en mode Dynamic Media en mode Scene7. |  |
| 3 | Dans les services cloud Adobe Experience Manager, configurez Dynamic Media avec les informations d’identification Dynamic Media en mode Scene7. | Adobe doit approuver la mise en service de Dynamic Media en mode Scene7. Par conséquent, vous disposez simultanément d’environnements Dynamic Media en mode hybride et Dynamic Media en mode Scene7, pris en charge par Adobe, mais pour une durée limitée uniquement. |
| 4 | Créez un lot de migration afin de pouvoir ingérer des ressources si nécessaire.<br>Supprimez les fichiers PTIFF locaux créés lors de l’ingestion initiale dans Dynamic Media en mode hybride. | Si toutes les ressources sont actuellement disponibles dans votre instance Dynamic Media en mode hybride, un clone de ces ressources les inclut déjà toutes. Par conséquent, aucun lot n’est nécessaire. |
| 5 | Exécutez le workflow de mise à jour des ressources afin de synchroniser les ressources avec le service cloud Dynamic Media. | Adobe vous recommande d’exécuter le workflow de mise à jour par lots pour permettre la compression. |
| 6 | Migrez les paramètres prédéfinis de visionneuse, d’image et de vidéo. |  |
| 7 | Parcourez chaque ressource référencée de la gestion de contenu web et mettez à jour les URL associées. |  |
| 8 | Migrez tous les workflows personnalisés que vous souhaitez pour prendre en charge le nouvel environnement Dynamic Media en mode Scene7 (mises à jour manuelles). |  |
| 9 | Vérifiez le chargement et la configuration de la gestion de contenu web. |  |
| 10 | Après vérification, obtenez une approbation pour désactiver l’auteur Dynamic Media en mode hybride (conservez-le comme solution de secours). |  |
| 11 | Supprimez l’instance auteur Dynamic Media en mode hybride après environ un mois d’utilisation fructueuse de Dynamic Media en mode Scene7. |  |
