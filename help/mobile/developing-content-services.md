---
title: Content Services
seo-title: Content Services
description: 'null'
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La fonctionnalité Content Services est uniquement documentée à des fins d’aperçu.
>
>Il peut être modifié avec la version 6.3 GA Service Pack 1.

AEM Mobile Content Services est une fonctionnalité légère qui permet de demander du contenu géré par AEM. Cela permet à tous les développeurs d’applications de récupérer du contenu de manière très performante sans avoir à connaître en profondeur le référentiel de contenu (JCR) et le cadre Web (Sling) d’AEM. Il permet de découpler les applications qui demandent du référentiel de contenu.

Content Services propose plusieurs nouveaux éléments AEM qui permettent aux développeurs d’accéder au contenu géré AEM sans connaître la structure de référentiel de ce contenu.

Ces éléments sont nécessaires pour conserver une certaine flexibilité et permettre une extension future en fournissant une couche d’abstraction entre le contenu géré AEM et les applications mobiles qui consomment le contenu. Cela permet à AEM Content Services de fonctionner comme une couche d’abstraction entre les exigences de contenu de l’application native et le référentiel de contenu AEM.

Content Services peut diffuser le contenu sous forme de ressources, de contenu HTML compressé (HTML/CSS/JS) ou de contenu indépendant du canal.

>[!CAUTION]
>
>**Conditions préalables:**
>
>Avant de commencer avec Content Services, veillez à activer l’indicateur Content Services. Pour activer la création et la gestion de modèles dans votre application, vous devez activer les modèles de données dans l’explorateur de configuration.
>
>Voir **[Administration de Content Services](/help/mobile/developing-content-services.md)**pour plus d’informations.

![chlimage_1-143](assets/chlimage_1-143.png)

Une fois que vous avez défini l&#39;indicateur Content Services et activé les modèles de données dans l&#39;explorateur de configuration, reportez-vous aux ressources ci-dessous pour commencer à utiliser AEM Mobile Content Services, familiarisez-vous avec les Concepts de Content Services tels que la gestion des modèles, la gestion des entités, puis la diffusion/rendu de contenu pour AEM Mobile Content Services.

* Modèles dans le référentiel
* Rendu et livraison

