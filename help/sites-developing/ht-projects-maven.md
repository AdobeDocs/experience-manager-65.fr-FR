---
title: Création de projets AEM à l’aide d’Apache Maven
description: Ce document décrit comment configurer un projet AEM basé sur Apache Maven.
exl-id: 451913bf-bb1e-4444-aee5-968ac30b5c9d
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 100%
---
# Création de projets AEM à l’aide d’Apache Maven {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5 respecte les bonnes pratiques de gestion des packages et de structure des projets, telles qu’elles sont mises en œuvre par le dernier archétype de projet AEM pour les implémentations On-Premise et AMS.

>[!TIP]
>
>Pour plus d’informations, consultez les ressources suivantes :
>
>* L’article sur la [structure de projet AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=fr) dans la documentation AEM as a Cloud Service pour savoir comment structurer des projets AEM modernes
>* La documentation sur l’[Archétype de projet AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr) pour savoir comment démarrer un nouveau projet AEM à l’aide de l’archétype
>* L’article [Plug-in de module de contenu Maven d’Adobe](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developer-tools/maven-plugin#developer-tools) dans la documentation d’AEM as a Cloud Service pour savoir comment déployer les applications AEM.
>
>Les trois documents s’appliquent à AEM 6.5.
