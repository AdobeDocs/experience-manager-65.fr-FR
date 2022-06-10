---
title: Intégration [!DNL Experience Manager Assets] avec  [!DNL Adobe Workfront]
description: Présentation de l’intégration entre [!DNL Assets] et [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
source-git-commit: 57304cfb7706377fa5dd7cce0e5863839ffee553
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 95%

---

# Intégration d’[!DNL Adobe Experience Manager Assets] à [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] est une application de gestion du travail qui vous permet de gérer l’ensemble du cycle de vie du travail en un seul endroit. L’intégration entre [!DNL Workfront] et [!DNL Adobe Experience Manager Assets] permet aux entreprises d’améliorer la vitesse du contenu et le délai de mise sur le marché en établissant des liens intrinsèques entre le travail et la gestion des ressources numériques. Dans le cadre de la gestion de leur travail dans Workfront, les utilisateurs ont accès aux documents et images requis.

Le [!DNL Workfront for Experience Manager enhanced connector] permet des processus d’entreprise améliorés avec des workflows de bout en bout et fournit des expériences client de bout en bout personnalisées et un stockage central. Adobe propose un connecteur standard et un connecteur amélioré pour intégrer les deux solutions. Pour une comparaison, reportez-vous aux fonctionnalités prises en charge ci-dessous et consultez la section [Nouveautés du  [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] permet à votre entreprise de :

* Créer automatiquement des dossiers Experience Manager liés dans Workfront et organiser les dossiers en fonction des portfolios, programmes et projets Workfront.
* Synchroniser les métadonnées de projet Workfront avec les dossiers Experience Manager liés.
* Mettre à jour des métadonnées d’Experience Manager avec de nouvelles versions.
* Définir des statuts d’objet Workfront en fonction de conditions configurables à l’aide de workflows Experience Manager.
* Publier des ressources dans l’environnement de publication d’Experience Manager ou dans Brand Portal.

Consultez les sections relatives à la prise en charge de la plateforme et aux [conditions préalables pour le connecteur amélioré](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe requiert le déploiement et la configuration du [!DNL Adobe Workfront for Experience Manager enhanced connector] uniquement par le biais de partenaires certifiés ou d’[!DNL Adobe Professional Services]. S’il est déployé et configuré sans partenaire certifié ou sans [!DNL Adobe Professional Services], il n’est pas pris en charge par Adobe.
>
>* Adobe peut apporter des mises à jour à [!DNL Adobe Workfront] et [!DNL Adobe Experience Manager], lesquelles peuvent rendre ce connecteur inutile. Si cela se produit, les clients peuvent être amenés à abandonner l’utilisation de ce connecteur.
>
>* Adobe prend en charge les versions 1.7.4 et ultérieures du connecteur. Les versions précédentes et personnalisées ne sont pas prises en charge. Pour vérifier la version améliorée du connecteur, accédez au `digital.hoodoo` groupe disponible dans le volet de gauche de [Gestionnaire de modules](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr).
>
>* Consultez [Examen de certification des partenaires pour Workfront pour le connecteur amélioré Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Pour plus d’informations sur l’examen, voir [Guide Exam](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Comparer les différentes intégrations entre [!DNL Assets] et [!DNL Workfront] {#feature-parity-matrix}

Vous trouverez ci-dessous les détails des fonctionnalités disponibles à travers différents types d’intégrations entre [!DNL Assets] et [!DNL Workfront].

| Fonctionnalité | Description | [!DNL Workfront] et [!DNL Assets Essentials] | [!DNL Workfront] pour le connecteur [!DNL Experience Manager] | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| Méthodes de déploiement | Approprié pour quelle offre [!DNL Assets]. | Assets Essentials | Cloud Service, Adobe Managed Services, On-Premise | Cloud Service, Adobe Managed Services, On-Premise |
| Envoyer des fichiers numériques depuis [!DNL Workfront] vers [!DNL Assets] | La dernière version d’un document WF peut être chargée vers AEM Assets, et sera liée en tant que nouvelle version du document. | ✓ | ✓ | ✓ |
| Lier manuellement des dossiers AEM à des objets Workfront | Les dossiers AEM existants peuvent être liés en tant que dossier Workfront. Ses ressources enfants sont liées en tant que nouveaux documents Workfront. | ✓ | ✓ | ✓ |
| Lier [!DNL Assets] aux objets Workfront | Les ressources existantes dans AEM peuvent être liées à un nouveau document Workfront ou à une nouvelle version d’un document existant. | ✓ | ✓ | ✓ |
| Envoyer automatiquement à AEM les ressources ajoutées aux dossiers liés | Si le document est ajouté à un dossier lié, la ressource associée est automatiquement chargée dans AEM Assets en tant que nouvelle ressource. | ✓ | ✓ | ✓ |
| Télécharger des ressources AEM Assets liées à partir de Workfront | Lorsqu’une ressource est liée dans Workfront, l’utilisateur peut télécharger les octets de la ressource. | ✓ | ✓ | ✓ |
| Rechercher des ressources AEM Assets à partir de Workfront | Le sélecteur AEM Assets de Workfront permet de rechercher des ressources en texte intégral. | ✓ | ✓ | ✓ |
| Afficher et parcourir la hiérarchie des dossiers AEM à partir de Workfront | Le sélecteur AEM Assets de Workfront permet de parcourir la hiérarchie d’AEM Assets limitée par les contrôles d’accès et les autorisations associés à l’utilisateur définis dans AEM. | ✓ | ✓ | ✓ |
| Dissocier des ressources d’AEM Assets dans Workfront | Une ressource liée existante provenant d’AEM peut être dissociée du document Workfront associé. Cela ne supprime pas la ressource d’origine dans AEM. | ✓ | ✓ | ✓ |
| Ajouter une ressource nouvellement versionnée à AEM Assets à partir de Workfront | Lorsqu’une nouvelle version est ajoutée à un document dans Workfront, un utilisateur peut envoyer la nouvelle version à AEM pour remplacer la version existante. | ✓ | ✓ | ✓ |
| Rediriger les utilisateurs vers AEM en cas de clic sur les ressources liées dans Workfront | Les utilisateurs sont redirigés vers AEM pour prévisualiser une ressource liée dans Workfront. | ✓ | ✓ | Personnalisé |
| Créer automatiquement des dossiers AEM liés dans Workfront | Créez automatiquement des dossiers AEM liés dans Workfront à l’aide des statuts d’objet. Organisez automatiquement les dossiers AEM en fonction des portfolios, programmes et projets Workfront. | Non | Non | ✓ |
| Synchronisation des commentaires | Synchroniser automatiquement les commentaires des ressources de [!DNL Workfront] vers [!DNL Assets] | Non | ✓ | ✓ |
| Mapper les métadonnées des ressources Workfront à AEM Assets | Les propriétés des formulaires personnalisés et des objets Workfront peuvent être mappées aux propriétés des métadonnées des ressources AEM. Les valeurs sont transmises lors du chargement ou de la liaison initial(e). | ✓ | ✓ | ✓ |
| Créer automatiquement des formulaires personnalisés pour les documents dans Workfront | Joignez des formulaires personnalisés aux documents, tâches et problèmes Workfront à l’aide des workflows AEM. | Non | Ajoutez manuellement le formulaire personnalisé, puis la synchronisation automatique fonctionne. | ✓ |
| Mise à jour automatique bidirectionnelle des métadonnées entre AEM Assets et Workfront | Mettez automatiquement à jour les métadonnées entre AEM Assets et Workfront. | Non | ✓ | ✓ |
| Mapper les métadonnées de Workfront aux dossiers AEM Assets | Synchronisez les métadonnées des projets Workfront avec les dossiers AEM liés. | Non | Non | ✓ |
| Mettre à jour les métadonnées AEM avec de nouvelles versions | Une configuration peut être effectuée dans AEM pour déterminer si une ressource nouvellement versionnée dans Workfront transmet également les modifications apportées à ses métadonnées. | Non | Non | ✓ |
| Mettre automatiquement à jour les métadonnées AEM lors des modifications apportées aux formulaires personnalisés dans Workfront | Workfront est configuré de telle sorte que les propriétés de métadonnées de ressources AEM spécifiées sont mappées à un formulaire personnalisé de document. Lorsquʼune ressource est initialement liée ou mise à jour, les valeurs de ces propriétés de métadonnées sont copiées dans le champ de formulaire personnalisé du document Workfront correspondant. Il convient de sʼassurer que la modification provenant dʼAEM ne soit pas renvoyée à AEM comme sʼil sʼagissait dʼune modification provenant de Workfront. | Non | ✓ | ✓ |
| Créer une version BAT sur les ressources liées | Lors de la liaison d’une ressource dans Workfront, un BAT peut être automatiquement généré. | Non | ✓ | Personnalisé |
| Définir le statut des objets Workfront | Définissez les statuts des objets Workfront en fonction de conditions configurables à l’aide de workflows AEM. | Non | Non | ✓ |
| Publier des ressources dans lʼenvironnement de publication AEM ou dans Brand Portal | Cette fonctionnalité permet aux utilisateurs de Workfront de publier automatiquement les ressources liées dans un environnement de publication AEM ou dans Brand Portal. | Non | Non | ✓ |
