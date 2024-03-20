---
title: Test de la structure de site globalisée dans We.Retail
description: Découvrez comment tester une structure de site globalisée dans Adobe Experience Manager à l’aide de We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 89%

---

# Test de la structure de site globalisée dans We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail a été créé avec une structure de site globalisée offrant un gabarit de langue qui peut être copié en direct sur des sites web spécifiques à un pays. Tout est prêt à l’emploi pour vous permettre d’expérimenter cette structure et les fonctionnalités de traduction intégrées.

## Essayer de le faire {#trying-it-out}

1. Ouvrez la console Sites à partir de **Navigation globale > Sites**.
1. Passez en vue Colonnes (si elle n’est pas déjà active) et sélectionnez We.Retail. Notez l’exemple de structure pour la Suisse, les États-Unis, la France, etc. avec les gabarits de langue.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Sélectionnez Suisse et affichez les racines de langue pour les langues de ce pays. Il n’y a pas encore de contenu sous ces racines.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Basculez vers la vue Liste. Vous pouvez remarquer que les copies linguistiques pour les pays sont toutes des Live Copies.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Revenez en vue Colonnes, cliquez sur le gabarit de langue et affichez ses racines avec le contenu. Seul l’anglais comporte du contenu.

   We.Retail n’est fourni avec aucun contenu traduit, mais la structure et la configuration sont en place pour vous permettre d’appliquer des services de traduction.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Le gabarit de langue Anglais étant ouvert, ouvrez le rail **Références** dans la console Sites et sélectionnez ensuite **Copies de langue**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Cochez la case en regard du libellé **Copies de langue** pour sélectionner toutes les copies de langue. Dans la section **Mise à jour des copies de langue**, sélectionnez l’option pour **Créer un projet de traduction**. Indiquez un nom pour le projet puis cliquez sur **Mettre à jour**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Un projet est créé pour chaque langue traduite. Les afficher sous **Navigation > Projets**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Cliquez sur Allemand pour afficher les détails du projet de traduction. Le statut est **Brouillon**. Pour commencer la traduction avec le service de traduction de Microsoft®, cliquez sur le chevron en regard du titre **Tâche de traduction** et sélectionnez **Démarrer**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Le projet de traduction commence. Cliquez sur les points de suspension en bas de la carte Tâche de traduction pour afficher les détails. Les pages ayant le statut **Prête pour la révision** ont déjà été traduites par le service de traduction.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Si vous sélectionnez l’une des pages dans la liste et ensuite **Aperçu dans Sites** dans la barre d’outils, la page traduite s’ouvre dans l’éditeur de page.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Cette procédure montre l’intégration de la traduction automatique de Microsoft®. En utilisant le [framework d’intégration de traduction AEM](/help/sites-administering/translation.md), vous pouvez intégrer de nombreux services de traduction standard pour orchestrer la traduction d’AEM.

## Informations supplémentaires {#further-information}

Pour plus d’informations, voir le document de création [Traduction de contenu pour les sites multilingues](/help/sites-administering/translation.md) pour obtenir des informations techniques complètes.
