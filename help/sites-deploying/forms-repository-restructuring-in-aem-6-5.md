---
title: Restructuration des référentiels de Forms dans AEM 6.5
seo-title: Restructuration des référentiels de Forms dans AEM 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Forms.
seo-description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Mise à niveau
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 83%

---

# Restructuration des référentiels de Forms dans AEM 6.5{#forms-repository-restructuring-in-aem}

Comme décrit sur la page parent [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md) , les clients effectuant une mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact sur la solution AEM Forms. Certaines modifications nécessitent des efforts lors du processus de mise à niveau d’AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau ultérieure.

**Avec la mise à niveau vers la version 6.5**

* [Divers](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Avant la mise à niveau ultérieure**

* [Configuration du service cloud Echosign](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurations du service cloud Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurations du service cloud Typekit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Divers](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Divers {#misc}

| **Emplacement précédent** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/fp/components` |
| **Conseil de restructuration** | Toute référence explicite dans le code personnalisé à l’emplacement hérité doit être mise à jour vers le nouvel emplacement. |
| **Remarques** | Ces bibliothèques clientes ne doivent pas être modifiées ou étendues. |

| **Emplacement précédent** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/rte` |
| **Conseil de restructuration** | Pour les ressources des bibliothèques clientes pouvant être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/af/authoring/clientlibs` |
| **Conseil de restructuration** | Pour les ressources des bibliothèques clientes pouvant être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/xfaforms/clientlibs/` |
| **Conseil de restructuration** | Pour les ressources des bibliothèques clientes pouvant être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/af/runtime/clientlibs` |
| **Conseil de restructuration** | Pour les ressources des bibliothèques clientes pouvant être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/af/runtime/clientlibs` |
| **Conseil de restructuration** | Pour les ressources des bibliothèques clientes pouvant être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/expeditor/clientlibs` |
| **Conseil de restructuration** | Pour les ressources des bibliothèques clientes pouvant être référencées par des chemins absolus, vous devez utiliser des chemins plus récents dans les nouvelles ressources. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/fmaddon` |
| **Conseil de restructuration** | La modification de ces clientlibs n’a jamais été recommandée ou prise en charge. Si des modifications ont été apportées à ces clientlibs, vous devez les restaurer pour utiliser le code fourni par AEM. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/aep` |
|---|---|
| **Nouveaux emplacements** | `/var/fd/content/annotations` |
| **Conseil de restructuration** | La modification de ces clientlibs n’a jamais été recommandée ou prise en charge. Si des modifications ont été apportées à ces clientlibs, vous devez les restaurer pour utiliser le code fourni par AEM. |
| **Remarques** | N/A |

## Avant la mise à niveau future {#prior-to-upgrade}

### Configuration du service cloud Echosign {#echosign-cloud-service-configuration}

| **Emplacement précédent** | `/etc/cloudservices/echosign` |
|---|---|
| **Nouveaux emplacements** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Conseil de restructuration** | L’utilitaire [Migration différée de contenu](/help/sites-deploying/lazy-content-migration.md) doit être déclenché depuis l’interface utilisateur de migration Forms. |
| **Remarques** | N/A |

### Configurations du service cloud Recaptcha {#recaptcha-cloud-service-configurations}

| **Emplacement précédent** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nouveaux emplacements** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Conseil de restructuration** | L’utilitaire [Migration différée de contenu](/help/sites-deploying/lazy-content-migration.md) doit être déclenché depuis l’interface utilisateur de migration Forms. |
| **Remarques** | N/A |

### Configurations du service cloud Typekit  {#typekit-cloud-service-configurations}

| **Emplacement précédent** | `/etc/cloudservices/typekit` |
|---|---|
| **Nouveaux emplacements** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Conseil de restructuration** | L’utilitaire [Migration différée de contenu](/help/sites-deploying/lazy-content-migration.md) doit être déclenché depuis l’interface utilisateur de migration Forms. |
| **Remarques** | N/A |

### Divers  {#misc-1}

| **Emplacement précédent** | `/etc/cloudservices/fdm` |
|---|---|
| **Nouveaux emplacements** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Conseil de restructuration** | L’utilitaire [Migration différée de contenu](/help/sites-deploying/lazy-content-migration.md) doit être déclenché depuis l’interface utilisateur de migration Forms. |
| **Remarques** | N/A |

| **Emplacement précédent** | `/etc/designs/fd/fp` |
|---|---|
| **Nouveaux emplacements** | `/libs/fd/fp` |
| **Conseil de restructuration** | Toutes les références aux modèles /etc doivent éventuellement être mises à jour afin de pointer vers leurs homologues `/libs`. |
| **Remarques** | N/A |
