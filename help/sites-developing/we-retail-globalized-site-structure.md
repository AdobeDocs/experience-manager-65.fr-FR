---
title: Test de la structure de site globalisée dans We.Retail
description: Test de la structure de site globalisée dans We.Retail
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 27%

---

# Test de la structure de site globalisée dans We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail a été créé avec une structure de site globalisée offrant un gabarit de langue qui peut être copié en direct sur des sites web spécifiques à un pays. Tout est prêt à l’emploi pour vous permettre d’expérimenter cette structure et les fonctionnalités de traduction intégrées.

## Essayer de le faire {#trying-it-out}

1. Ouvrez la console Sites à partir de **Navigation globale -> Sites**.
1. Passez en mode Colonnes (s’il n’est pas déjà principal) et sélectionnez We.Retail. Notez l’exemple de structure par pays avec la Suisse, les Etats-Unis, la France, etc., à côté du Principal Langue.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Sélectionnez Suisse et affichez les racines de la langue pour les langues de ce pays. Il n&#39;y a pas encore de contenu sous ces racines.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Basculez vers la vue Liste. Vous pouvez remarquer que les copies linguistiques pour les pays sont toutes des Live Copies.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Revenez au mode Colonnes, cliquez sur le Principal Langue et affichez les racines du gabarit de langue avec le contenu. Seul l&#39;anglais a du contenu.

   We.Retail ne contient aucun contenu traduit, mais la structure et la configuration sont en place pour vous permettre de démontrer les services de traduction.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Le gabarit de langue Anglais étant ouvert, ouvrez le rail **Références** dans la console Sites et sélectionnez ensuite **Copies de langue**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Cochez la case en regard de l’option **Copies de langue** libellé pour sélectionner toutes les copies de langue. Dans le **Mise à jour des copies de langue** de la section , sélectionnez l’option pour **Création d’un projet de traduction**. Attribuez un nom au projet et cliquez sur **Mettre à jour**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Un projet est créé pour chaque traduction de langue. Les afficher sous **Navigation -> Projets**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Cliquez sur Allemand pour afficher les détails du projet de traduction. L’état est dans **Version préliminaire**. Pour commencer la traduction avec le service de traduction de Microsoft®, cliquez sur le chevron en regard de l’option **Tâche de traduction** titre et sélectionner **Début**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Le projet de traduction commence. Cliquez sur les points de suspension en bas de la carte Tâche de traduction pour afficher les détails. Pages avec l’état **Prêt pour la révision** ont déjà été traduits par le service de traduction.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Si vous sélectionnez l’une des pages dans la liste et ensuite **Aperçu dans Sites** dans la barre d’outils, la page traduite s’ouvre dans l’éditeur de page.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Cette procédure a démontré l’intégration intégrée à la traduction automatique de Microsoft®. En utilisant la variable [AEM structure d’intégration de traduction](/help/sites-administering/translation.md), vous pouvez intégrer de nombreux services de traduction standard pour orchestrer la traduction d’AEM.

## Informations supplémentaires {#further-information}

Pour obtenir tous les détails techniques, reportez-vous au document de création [Traduction de contenu pour des sites multilingues](/help/sites-administering/translation.md).
