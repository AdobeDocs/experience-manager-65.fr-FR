---
title: Restructuration des référentiels de Forms dans AEM 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Forms.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 45%

---

# Restructuration des référentiels de Forms dans AEM 6.5{#forms-repository-restructuring-in-aem}

Comme indiqué dans la page parent [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients effectuant une mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact sur la solution AEM Forms. Certaines modifications demandent du travail lors du processus de mise à niveau vers AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau vers une version future.

**Avec la mise à niveau vers la version 6.5**

* [Divers](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Avant la future mise à niveau**

* [Configuration du service cloud Echosign](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurations du service cloud Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurations du service cloud Typekit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Divers](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Divers {#misc}

| **Emplacement précédent** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/fp/components` |
| **Conseils de restructuration** | Toute référence explicite dans le code personnalisé à l’emplacement existant doit être mise à jour vers le nouvel emplacement. |
| **Remarques** | Ces bibliothèques clientes ne doivent pas être modifiées ni étendues. |

| **Emplacement précédent** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/rte` |
| **Conseils de restructuration** | Pour les ressources des bibliothèques clientes qui peuvent être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/af/authoring/clientlibs` |
| **Conseils de restructuration** | Pour les ressources des bibliothèques clientes qui peuvent être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/xfaforms/clientlibs/` |
| **Conseils de restructuration** | Pour les ressources des bibliothèques clientes qui peuvent être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/af/runtime/clientlibs` |
| **Conseils de restructuration** | Pour les ressources des bibliothèques clientes qui peuvent être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/af/runtime/clientlibs` |
| **Conseils de restructuration** | Pour les ressources des bibliothèques clientes qui peuvent être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/expeditor/clientlibs` |
| **Conseils de restructuration** | Pour les ressources des bibliothèques clientes qui peuvent être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/fmaddon` |
| **Conseils de restructuration** | La modification de ces clientlibs n’a jamais été recommandée ou prise en charge. Si des modifications ont été apportées à ces clientlibs, elles doivent être restaurées afin d’utiliser le code fourni par AEM. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/aep` |
|---|---|
| **Nouvel emplacement** | `/var/fd/content/annotations` |
| **Conseils de restructuration** | La modification de ces clientlibs n’a jamais été recommandée ou prise en charge. Si des modifications ont été apportées à ces clientlibs, elles doivent être restaurées afin d’utiliser le code fourni par AEM. |
| **Remarques** | S/O |

## Avant la future mise à niveau {#prior-to-upgrade}

### Configuration du service cloud Echosign {#echosign-cloud-service-configuration}

| **Emplacement précédent** | `/etc/cloudservices/echosign` |
|---|---|
| **Nouvel emplacement** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Conseils de restructuration** | La variable [Migration différée du contenu](/help/sites-deploying/lazy-content-migration.md) à déclencher à partir de l’interface utilisateur de migration de Forms. |
| **Remarques** | S/O |

### Configurations du service cloud Recaptcha {#recaptcha-cloud-service-configurations}

| **Emplacement précédent** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nouvel emplacement** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Conseils de restructuration** | La variable [Migration différée du contenu](/help/sites-deploying/lazy-content-migration.md) à déclencher à partir de l’interface utilisateur de migration de Forms. |
| **Remarques** | S/O |

### Configurations du service cloud Typekit {#typekit-cloud-service-configurations}

| **Emplacement précédent** | `/etc/cloudservices/typekit` |
|---|---|
| **Nouvel emplacement** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Conseils de restructuration** | La variable [Migration différée du contenu](/help/sites-deploying/lazy-content-migration.md) à déclencher à partir de l’interface utilisateur de migration de Forms. |
| **Remarques** | S/O |

### Divers {#misc-1}

| **Emplacement précédent** | `/etc/cloudservices/fdm` |
|---|---|
| **Nouvel emplacement** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Conseils de restructuration** | La variable [Migration différée du contenu](/help/sites-deploying/lazy-content-migration.md) à déclencher à partir de l’interface utilisateur de migration de Forms. |
| **Remarques** | S/O |

| **Emplacement précédent** | `/etc/designs/fd/fp` |
|---|---|
| **Nouvel emplacement** | `/libs/fd/fp` |
| **Conseils de restructuration** | Mettez à jour toutes les références aux modèles /etc pour qu’elles pointent vers leurs `/libs` leurs homologues. |
| **Remarques** | S/O |
