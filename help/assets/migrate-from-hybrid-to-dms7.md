---
title: Migration de Dynamic Media - Mode hybride vers le mode Dynamic Media - S7
description: Découvrez comment migrer votre instance de Dynamic Media - Mode hybride vers le mode Dynamic Media - S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
feature: Scene7 mode,Hybrid mode
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# À propos du passage de Dynamic Media-Hybrid à Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid est une version plus ancienne de l&#39;intégration de Dynamic Media avec Adobe Experience Manager. La version hybride a été introduite pour la première fois dans AEM (Adobe Experience Manager) 6.1. Bien que l&#39;Adobe continue de prendre en charge le mode hybride, il ne s&#39;agit pas du mode préféré (Dynamic Media est le mode préféré). Il ne prend pas non plus en charge les nouvelles fonctionnalités telles que la recadrage intelligente et les images panoramiques. Tandis que Dynamic Media-Scene7 le fait.

D&#39;autres différences clés entre Dynamic Media-Hybrid et Dynamic Media-Scene7 sont les suivantes :

* Structure des URL.
* Ingestion de vidéos.
* Création et enregistrement de rendus d’image.
* Configuration et informations d’identification du cloud (mise en service).

Deux options sont disponibles lorsque vous passez de Dynamic Media-Hybrid à Dynamic Media-Scene7. La première option consiste à simplement configurer une nouvelle instance de Dynamic Media-Scene7 sur AEM. La deuxième option consiste à migrer votre instance existante de Dynamic Media-Hybrid vers Dynamic Media-Scene7. Cette option présente un tableau détaillé sous les étapes et les points à prendre en compte lors du déplacement.

>[!IMPORTANT]
>
>Adobe recommande de ne pas migrer une implémentation Dynamic Media-Hybrid vers Dynamic Media-Scene7 sur des instances de production en direct.

## Option 1 - Mise en service d&#39;une nouvelle instance de Dynamic Media-Scene7 sur AEM {#provision-new-dms7}

Envisagez simplement de commencer à nouveau avec une nouvelle instance de Dynamic Media-Scene7 sur Adobe Experience Manager, configurée. Outre l’assimilation et le traitement des actifs par le biais du Cloud Service Dynamic Media, un audit d’Adobe de l’utilisation des actifs, des workflows et des composants est fortement recommandé. Dans de nombreux cas, les composants et les workflows personnalisés peuvent être remplacés par des fonctions plus récentes et prêtes à l’emploi.

## Option 2 - Migration de votre instance existante de Dynamic Media-Hybrid vers Dynamic Media-Scene7 {#process-for-migrating}

| Étape | Tâche | Considérations |
|---|---|---|
| 1 | Cloner l’instance d’auteur Dynamic Media-Hybrid. | Vous devez conserver votre instance existante d’auteur Dynamic Media-Hybrid à des fins de secours jusqu’à ce que les étapes restantes de ce processus de migration soient terminées. |
| 2 | Début de l’instance Auteur clonée en mode Dynamic Media-Scene7. |  |
| 3 | Dans Adobe Experience Manager Cloud Services, configurez Dynamic Media avec les informations d’identification Dynamic Media-Scene7. | L’Adobe doit approuver la mise en service de Dynamic Media-Scene7. Les environnements simultanément Dynamic MediaM-Hybrid et Dynamic Media-Scene7 seront pris en charge pendant une durée limitée. |
| 4 | Créez un lot de migration pour assimiler les ressources en fonction des besoins.<br>Supprimer les PTIFF locaux créés lors de l&#39;assimilation initiale dans Dynamic Media-Hybrid. | Si toutes les ressources sont actuellement disponibles dans votre instance Dynamic Media-Hybrid, un clone de celle-ci les inclut déjà toutes. Par conséquent, aucun lot n’est nécessaire. |
| 5 | Exécutez le processus de mise à jour des ressources pour synchroniser les ressources avec le Cloud Service Dynamic Media. | L’Adobe recommande que le processus de mise à jour soit effectué par lots pour permettre la compaction. |
| 6 | Migration des paramètres prédéfinis de visionneuse, d’image et de vidéo. |  |
| 7 | Parcourez chaque ressource référencée par une Gestion de contenu Web et mettez à jour ses URL associées. |  |
| 8 | Migrez tous les workflows personnalisés pour prendre en charge le nouveau mode Dynamic Media-Scene7 (mises à jour manuelles). |  |
| 9 | Vérifiez le téléchargement et la configuration de votre Gestion de contenu Web. |  |
| 10 | Après la vérification, obtenez une approbation pour désactiver l’auteur Dynamic Media-Hybrid (conservez la valeur de retour arrière). |  |
| 11 | Supprimez l’instance d’auteur hybride Dynamic Media après environ un mois d’utilisation réussie de Dynamic Media-Scene7. |  |
