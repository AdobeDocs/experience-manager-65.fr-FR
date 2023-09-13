---
title: Content Services
description: Content Services
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%

---

# Content Services{#content-services}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La fonctionnalité Content Services est documentée à des fins d’aperçu uniquement.
>
>Il peut être modifié avec la version 6.3 GA Service Pack 1.

AEM Mobile Content Services est une fonctionnalité légère qui permet de demander du contenu géré par AEM. Cela permet à tous les développeurs d’applications d’obtenir du contenu de manière très performante sans avoir à posséder une connaissance approfondie du référentiel de contenu AEM (JCR) et de la structure web (Sling). Il permet de découpler les applications qui le demandent du référentiel de contenu.

Content Services introduit plusieurs nouveaux éléments d’AEM qui permettent à un développeur d’accéder AEM contenu géré sans connaître la structure de référentiel de ce contenu.

Ces concepts sont nécessaires pour préserver la flexibilité et permettre une extension future en fournissant une couche d’abstraction entre le contenu géré par AEM et les applications mobiles utilisant le contenu. Cela permet à AEM Content Services de fonctionner comme une couche d’abstraction entre les exigences de contenu de l’application native et le référentiel de contenu AEM.

Content Services peut diffuser le contenu sous la forme de ressources, de HTML empaqueté (HTML/CSS/JS) ou de contenu indépendant des canaux.

>[!CAUTION]
>
>**Conditions préalables:**
>
>Avant de commencer à utiliser Content Services, assurez-vous d’activer l’indicateur Content Services. Pour activer la création et la gestion des modèles dans votre application, activez les modèles de données dans le navigateur de configuration.
>
>Voir **[Administration de Content Services](/help/mobile/developing-content-services.md)** et la variable [Explorateur de configuration](/help/sites-administering/configurations.md) pour plus d’informations.

![chlimage_1-143](assets/chlimage_1-143.png)

Après avoir défini l’indicateur Content Services et activé les modèles de données dans le navigateur de configuration, reportez-vous aux ressources ci-dessous pour commencer à utiliser AEM Mobile Content Services. Familiarisez-vous avec les Concepts de Content Services, tels que la gestion des modèles, la gestion des entités, suivie de la diffusion/du rendu de contenu pour AEM Mobile Content Services.

* Modèles dans le référentiel
* Rendu et diffusion
