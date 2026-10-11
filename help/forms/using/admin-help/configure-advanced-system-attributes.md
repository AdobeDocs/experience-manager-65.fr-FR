---
title: Configurer les attributs système avancés
description: Utilisez la page Configurer les attributs système avancés pour modifier certains paramètres du fichier de configuration sans qu’il soit nécessaire de l’exporter, de le modifier et de l’importer.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 100%
---
# Configurer les attributs système avancés {#configure-advanced-system-attributes}

Utilisez la page Configurer les attributs système avancés pour modifier certains paramètres du fichier de configuration sans qu’il soit nécessaire de l’exporter, de le modifier et de l’importer. (Voir [Importation et exportation du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > User Management > Configuration > Configurer les attributs système avancés]**.
1. (Facultatif) Modifiez l’un des attributs de session suivants :

   **Limite du délai d’expiration de la session (en minutes) :** durée, en minutes, avant qu’un utilisateur ne soit automatiquement déconnecté du système. Par défaut, les composants d’AEM forms comme l’atelier expirent au bout de deux heures, indépendamment de la présence ou non d’activité, et l’utilisateur ou l’utilisatrice doit se reconnecter. Les valeurs valides sont comprises entre `1` et `1440`. La valeur par défaut est `120` (2 heures). Ce paramètre met à jour la clé d’entrée `SAML/Producer/assertionValidityInMinutes` dans le fichier de configuration.

   >[!NOTE]
   >
   >Vous ne devez pas définir un délai d’expiration de session inférieur à 10 minutes, sinon le système risque de ne pas se comporter correctement. Il est recommandé de choisir une valeur comprise entre 10 et 120 (minutes).

   **Seuil d’identification (en secondes) :** cette valeur indique une durée de mise en mémoire pour compenser les retards dus aux différences de temps système entre le serveur d’applications AEM forms d’une grappe. AEM forms antidate l’heure de connexion d’un utilisateur ou d’une utilisatrice de la durée (en secondes) spécifiée dans cette propriété. Les valeurs valides sont comprises entre `0` et `3600`. La valeur par défaut est `60`. Ce paramètre met à jour la clé d’entrée `SAML/Producer/assertionThresholdInSeconds` dans le fichier de configuration.

   **Nombre maximal de renouvellements autorisés pour une identification :** nombre maximal de fois où la session d’un utilisateur peut être renouvelée de façon transparente sans nécessiter une ouverture de session. Les valeurs valides sont comprises entre `0` et `9999`. Une valeur de `0` signifie que les assertions ne sont pas renouvelées. La valeur par défaut est 10. Ce paramètre met à jour la clé d’entrée `SAML/Producer/maxAssertionRenewalCount` dans le fichier de configuration.

1. (Facultatif) Modifiez l’un des attributs de synchronisation des annuaires suivants :

   **Consignation de statistiques de synchronisation :** permet de spécifier si User Management doit créer un journal des statistiques détaillées pendant le processus de synchronisation (voir [Activation ou désactivation de la journalisation détaillée lors de la synchronisation](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)).

   **Expression cron d’achèvement de synchronisation :** intervalle auquel User Management tente d’effectuer à nouveau les synchronisations ayant échoué (voir [Configuration de l’option de nouvelle synchronisation des annuaires](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)).

   **Délai d’expiration de verrouillage de tâche de grappe en minutes :** option utilisée dans les environnements organisés en grappes. Si la synchronisation échoue sur un nœud et que le verrouillage de la grappe n’est pas libéré, cette valeur permet de spécifier le nombre de minutes durant lesquelles un autre nœud doit patienter avant de forcer l’acquisition du verrouillage. La valeur par défaut est de `15` minutes. Les valeurs valides se situent entre `1` et `1440` minutes.

1. (Facultatif) Modifiez les attributs suivants, puis cliquez sur **[!UICONTROL OK]** :

   **Contrôle des événements dans User Manager :** sélectionnez cette option pour activer le contrôle des événements de synchronisation des annuaires et des événements d’authentification tels que les réussites, les échecs et les verrouillages. Par défaut, cette option n’est pas sélectionnée, à moins que vous ayez installé un composant qui requiert un audit, comme Rights Management. Ce paramètre met à jour la clé d’entrée `APSAuditService` dans le fichier de configuration.

   **Création automatique de groupe dynamique :** permet la création automatique de groupes dynamiques à partir des domaines d’adresses électroniques (voir [Créer un groupe dynamique](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)).

Vous pouvez également revenir aux paramètres d’origine de User Management en cliquant sur Recharger.
