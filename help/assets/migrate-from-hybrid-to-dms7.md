---
title: Migration de Contenu multimédia dynamique - Mode hybride vers Contenu multimédia dynamique - Mode S7
description: Découvrez comment migrer votre instance de Contenu multimédia dynamique - Mode hybride vers Contenu multimédia dynamique - Mode S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: f466193a259d9e8869d7f79eafda1be20869e4af
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---


# À propos du passage de Contenu multimédia dynamique hybride à Contenu multimédia dynamique-Scene7 {#about-migrating}

Dynamic Media-Hybrid est une ancienne version de l’intégration de Contenu multimédia dynamique à Adobe Experience Manager. La version hybride a été introduite pour la première fois dans AEM (Adobe Experience Manager) 6.1. Bien que l&#39;Adobe continue de prendre en charge le mode hybride, il ne s&#39;agit pas du mode préféré (Dynamic Media-Scene7 est le mode préféré). Il ne prend pas non plus en charge les nouvelles fonctionnalités telles que la recadrage intelligente et les images panoramiques. Tandis que Dynamic Media-Scene7 le fait.

D’autres différences clés entre Dynamic Media-Hybrid et Dynamic Media-Scene7 sont les suivantes :

* Structure des URL.
* Ingestion de vidéos.
* Création et enregistrement de rendus d’image.
* Configuration et informations d’identification du cloud (mise en service).

Deux options sont disponibles lorsque vous passez de Dynamic Media-Hybrid à Dynamic Media-Scene7. La première option consiste à simplement configurer une nouvelle instance de Dynamic Media-Scene7 sur AEM. La deuxième option consiste à migrer votre instance existante de Dynamic Media-Hybrid vers Dynamic Media-Scene7. Cette option présente un tableau détaillé sous les étapes et les points à prendre en compte lors du déplacement.

>[!IMPORTANT]
>
>Adobe recommande de ne pas migrer une implémentation hybride Contenu multimédia dynamique vers Dynamic Media-Scene7 sur les instances de production en direct.

## Option 1 - Mise en service d’une nouvelle instance de Dynamic Media-Scene7 sur AEM {#provision-new-dms7}

N’hésitez pas à recommencer à zéro avec une nouvelle instance de Dynamic Media-Scene7 activée sur Adobe Experience Manager. Outre l’assimilation et le traitement des ressources par l’intermédiaire du Cloud Service Contenu multimédia dynamique, il est vivement recommandé d’effectuer un audit d’Adobe de l’utilisation des ressources, des workflows et des composants. Dans de nombreux cas, les composants et les workflows personnalisés peuvent être remplacés par des fonctions plus récentes et prêtes à l’emploi.

## Option 2 - Migration de votre instance existante de Contenu multimédia dynamique hybride vers Contenu multimédia dynamique - Scene7 {#process-for-migrating}

| Étape | Tâche | Considérations |
|---|---|---|
| 1 | Cloner l’instance d’auteur dynamique hybride média. | Vous devez conserver votre instance existante de Dynamic Media-Hybrid Author à des fins de secours jusqu’à ce que les étapes restantes de ce processus de migration soient terminées. |
| 2 | Début de l’instance Auteur clonée en mode Contenu multimédia dynamique-Scene7. |  |
| 3 | Dans Adobe Experience Manager Cloud Services, configurez Dynamic Media avec les informations d’identification de Dynamic Media-Scene7. | L’Adobe doit approuver la mise en service de Dynamic Media-Scene7. Les environnements Dynamic MediaM-Hybrid et Dynamic Media-Scene7 concomitants seront pris en charge pendant une durée limitée. |
| 4 | Créez un lot de migration pour assimiler les ressources en fonction des besoins.<br>Supprimez les fichiers PTIFF locaux créés lors de l’assimilation initiale dans Dynamic Media-Hybrid. | Si tous les fichiers sont actuellement disponibles dans votre instance Contenu multimédia dynamique hybride, un clone de ces fichiers les inclut déjà tous. Par conséquent, aucun lot n’est nécessaire. |
| 5 | Exécutez le processus de mise à jour des ressources pour synchroniser les ressources avec le Cloud Service Contenu multimédia dynamique. | L’Adobe recommande que le processus de mise à jour soit effectué par lots pour permettre la compaction. |
| 6 | Migration des paramètres prédéfinis de visionneuse, d’image et de vidéo. |  |
| 7 | Parcourez chaque ressource référencée par une Gestion de contenu Web et mettez à jour ses URL associées. |  |
| 8 | Migrez tous les workflows personnalisés pour prendre en charge le nouveau mode Contenu multimédia dynamique Scene7 (mises à jour manuelles). |  |
| 9 | Vérifiez le téléchargement et la configuration de votre Gestion de contenu Web. |  |
| 10 | Après la vérification, obtenez une approbation pour désactiver l’auteur dynamique hybride média (conservez la valeur de retour arrière). |  |
| 11 | Supprimez l’instance Dynamic Media-Hybrid Author après environ un mois d’utilisation réussie de Dynamic Media-Scene7. |  |
