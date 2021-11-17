---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: Introduction à l’intégration entre [!DNL Assets] et [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: c742e89a56c383e6dde8a6aee5bc3d124d73343d
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] intégration avec [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] est une application de gestion du travail qui vous aide à gérer l’ensemble du cycle de vie du travail au même endroit. L&#39;intégration entre [!DNL Workfront] et [!DNL Adobe Experience Manager Assets] permet aux entreprises d’améliorer la vitesse du contenu et le délai de mise sur le marché en établissant des liens intrinsèques entre le travail et la gestion des ressources numériques. Dans le cadre de la gestion de leur travail dans Workfront, les utilisateurs ont accès aux documents et images requis.

Le [!DNL Workfront for Experience Manager enhanced connector] permet des processus d’entreprise améliorés avec des workflows de bout en bout et fournit des expériences client de bout en bout personnalisées et un stockage central. Adobe propose un connecteur standard et un connecteur amélioré pour intégrer les deux solutions. Pour une comparaison, reportez-vous aux fonctionnalités prises en charge ci-dessous et reportez-vous à la section [nouveautés de la [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] permet à votre entreprise de :

* Créez automatiquement des dossiers de Experience Manager liés dans Workfront et organisez les dossiers en fonction des Portfolios, programmes et projets Workfront.
* Synchronisez les métadonnées de projet Workfront avec les dossiers de Experience Manager liés.
* Mises à jour des métadonnées de Experience Manager avec de nouvelles versions.
* Définissez des statuts d’objet Workfront en fonction de conditions configurables à l’aide de workflows Experience Manager.
* Publiez des ressources dans l’environnement de publication Experience Manager ou dans Brand Portal.

Voir la prise en charge de la plateforme et [conditions préalables pour le connecteur amélioré](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>L’Adobe nécessite le déploiement et la configuration de [!DNL Adobe Workfront for Experience Manager enhanced connector] uniquement par le biais de partenaires certifiés ; [!DNL Adobe Professional Services]. Si elles sont déployées et configurées sans partenaire certifié ou [!DNL Adobe Professional Services], il n’est pas pris en charge par Adobe.
>
>Adobe peut mettre à jour les [!DNL Adobe Workfront] et [!DNL Adobe Experience Manager] qui rendent ce connecteur redondant ; si cela se produit, les clients peuvent être tenus de passer de l’utilisation de ce connecteur.

## Comparaison de différentes intégrations entre [!DNL Assets] et [!DNL Workfront] {#feature-parity-matrix}

Vous trouverez ci-dessous les détails des fonctionnalités disponibles via différents types d’intégrations entre les [!DNL Assets] et [!DNL Workfront].

| Fonctionnalité | Description | [!DNL Workfront] et [!DNL Assets Essentials] | [!DNL Workfront] pour [!DNL Experience Manager] connector | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| Méthodes de déploiement | Approprié pour lequel [!DNL Assets] offre. | Assets Essentials | Cloud Service, Adobe Managed Services, On-Premise | Cloud Service, Adobe Managed Services, On-Premise |
| Envoi de fichiers numériques depuis [!DNL Workfront] to [!DNL Assets] | La dernière version d’un document WF peut être téléchargée vers AEM Assets, qui sera liée en tant que nouvelle version du document. | ✓ | ✓ | ✓ |
| Lier manuellement des dossiers AEM à des objets Workfront | Les dossiers AEM existants peuvent être liés en tant que dossier Workfront et ses ressources enfants sont liés en tant que nouveaux documents Workfront. | ✓ | ✓ | ✓ |
| Lien [!DNL Assets] vers les objets Workfront | Les ressources existantes dans AEM peuvent être liées à un nouveau document Workfront ou à une nouvelle version d’un document existant. | ✓ | ✓ | ✓ |
| Les ressources ajoutées aux dossiers liés sont automatiquement envoyées à AEM | Si le document est ajouté à un dossier lié, la ressource associée est automatiquement chargée dans AEM Assets en tant que nouvelle ressource. | ✓ | ✓ | ✓ |
| Téléchargement d’AEM Assets lié depuis Workfront | Lorsqu’une ressource est liée dans Workfront, l’utilisateur peut télécharger les octets de la ressource. | ✓ | ✓ | ✓ |
| Recherche d’AEM Assets depuis Workfront | Le sélecteur AEM Assets de Workfront permet de rechercher des ressources en texte intégral. | ✓ | ✓ | ✓ |
| Affichage et navigation dans AEM hiérarchie de dossiers à partir de Workfront | Le sélecteur AEM Assets dans Workfront permet de parcourir la hiérarchie AEM Assets limitée par les contrôles d’accès et les autorisations associés à l’utilisateur définis dans AEM. | ✓ | ✓ | ✓ |
| Annulation de la liaison de ressources à partir d’AEM Assets dans Workfront | Une ressource liée existante provenant d’AEM peut être dissociée du document Workfront associé. Cela ne supprime pas la ressource d’origine dans AEM. | ✓ | ✓ | ✓ |
| Ajout d’une ressource nouvellement versionnée à AEM Assets à partir de Workfront | Lorsqu’une nouvelle version est ajoutée à un document dans Workfront, un utilisateur peut envoyer la nouvelle version à AEM pour remplacer la version existante. | ✓ | ✓ | ✓ |
| Ressources liées dans Workfront en cas de clic sur Utilisateur direct pour AEM | Les utilisateurs sont redirigés vers AEM pour prévisualiser une ressource liée dans Workfront. | ✓ | ✓ | Personnalisé |
| Création automatique de dossiers d’AEM liés dans Workfront | Créez automatiquement des dossiers d’AEM liés dans Workfront à l’aide des statuts d’objet. Organisez automatiquement AEM dossiers en fonction des Portfolios, programmes et projets Workfront. | Non | Non | ✓ |
| Synchronisation des commentaires | Synchronisation automatique des commentaires pour les ressources de [!DNL Workfront] to [!DNL Assets] | Non | ✓ | ✓ |
| Mappage des métadonnées des ressources Workfront à AEM Assets | L’objet Workfront et les propriétés de formulaire personnalisées peuvent être mappés aux propriétés de métadonnées AEM ressource. Les valeurs seront transmises lors du téléchargement/lien initial. | ✓ | ✓ | ✓ |
| Créer automatiquement le document Forms personnalisé dans Workfront | Joindre des formulaires personnalisés à des documents Workfront, des tâches et des problèmes à l’aide de processus AEM. | Non | Ajoutez manuellement le formulaire personnalisé, puis la synchronisation automatisée fonctionne | ✓ |
| Mise à jour automatique bidirectionnelle des métadonnées entre AEM Assets et Workfront | Mettre à jour automatiquement les métadonnées entre AEM Assets et Workfront. | Non | ✓ | ✓ |
| Mappage des métadonnées Workfront aux dossiers AEM Assets | Synchroniser les métadonnées de projet Workfront avec les dossiers d’AEM liés. | Non | Non | ✓ |
| AEM Mises à jour des métadonnées avec de nouvelles versions | Une configuration dans AEM peut être effectuée pour déterminer si une ressource nouvellement versionnée dans Workfront envoie également les modifications apportées à ses métadonnées. | Non | Non | ✓ |
| Mise à jour automatique des métadonnées AEM lors des modifications apportées à Forms personnalisé dans Workfront | Workfront est configuré de sorte que les propriétés de métadonnées de ressource AEM spécifiées soient mappées à un formulaire personnalisé de document. Lorsqu’une ressource est initialement liée ou lorsqu’une ressource est mise à jour, les valeurs de ces propriétés de métadonnées sont copiées dans le champ de formulaire personnalisé de document Workfront correspondant. Il faut prendre soin d’empêcher que la modification ne soit renvoyée à AEM comme s’il s’agissait d’une modification originaire de Workfront. | Non | ✓ | ✓ |
| Créer une version de BAT sur les ressources liées | Lors de la liaison d’une ressource dans Workfront, un BAT peut être généré automatiquement. | Non | ✓ | Personnalisé |
| Définir l’état sur les objets Workfront | Définir des statuts d’objet Workfront en fonction de conditions configurables à l’aide AEM workflows | Non | Non | ✓ |
| Publication de ressources dans l’environnement de publication AEM ou Brand Portal | Donnez aux utilisateurs de Workfront la possibilité de publier automatiquement les ressources liées dans un environnement de publication AEM ou dans Brand Portal. | Non | Non | ✓ |
