---
title: Configuration des attributs système avancés
seo-title: Configuration des attributs système avancés
description: 'Utilisez la page Configurer les attributs système avancés pour modifier certains paramètres du fichier de configuration sans qu’il soit nécessaire de l’exporter, de le modifier et de l’importer. '
seo-description: 'Utilisez la page Configurer les attributs système avancés pour modifier certains paramètres du fichier de configuration sans qu’il soit nécessaire de l’exporter, de le modifier et de l’importer. '
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 91%

---

# Configuration des attributs système avancés {#configure-advanced-system-attributes}

Utilisez la page Configurer les attributs système avancés pour modifier certains paramètres du fichier de configuration sans qu’il soit nécessaire de l’exporter, de le modifier et de l’importer (voir [Importation et exportation du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)).

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > User Management > Configuration > Configurer les attributs système avancés]**.
1. (Facultatif) Modifiez l’un des attributs de session suivants :

   **Limite du délai d’expiration de la session (en minutes) :** durée, en minutes, avant qu’un utilisateur ne soit automatiquement déconnecté du système. Par défaut, les composants d&#39;AEM forms comme Workbench expirent au bout de deux heures, indépendamment de la présence ou non d’activité, et l’utilisateur doit se reconnecter. Les valeurs valides sont `1` à `1440`. La valeur par défaut est `120` (2 heures). Ce paramètre met à jour la clé d’entrée `SAML/Producer/assertionValidityInMinutes` dans le fichier de configuration.

   >[!NOTE]
   >
   >Vous ne devez pas définir un délai d’attente de session inférieur à 10 minutes, sinon le système risque de ne pas se comporter correctement. La valeur recommandée est comprise entre 10 et 120 (minutes).

   **Seuil d’identification (en secondes) :** cette valeur indique une durée de mise en mémoire pour compenser les retards dus aux différences de temps système entre le serveur d’applications AEM forms d’une grappe. AEM forms antidate la durée de connexion d’un utilisateur en fonction de la durée (en secondes) spécifiée dans cette propriété. Les valeurs valides sont `0` à `3600`. La valeur par défaut est `60`. Ce paramètre met à jour la clé d’entrée `SAML/Producer/assertionThresholdInSeconds` dans le fichier de configuration.

   **Nombre maximal de renouvellements autorisés pour une identification :** nombre maximal de fois où la session d’un utilisateur peut être renouvelée de façon transparente sans nécessiter une ouverture de session. Les valeurs valides sont `0` à `9999`. Une valeur de `0` signifie que les assertions ne sont pas renouvelées. La valeur par défaut est 10. Ce paramètre met à jour la clé d’entrée `SAML/Producer/maxAssertionRenewalCount` dans le fichier de configuration.

1. (Facultatif) Modifiez l’un des attributs de synchronisation des annuaires suivants :

   **Consignation de statistiques de synchronisation :** permet de spécifier si User Management doit créer un journal des statistiques détaillées pendant le processus de synchronisation (voir [Activation ou désactivation de la journalisation détaillée lors de la synchronisation](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)).

   **Expression cron d’achèvement de synchronisation :** intervalle auquel User Management tente d’effectuer à nouveau les synchronisations ayant échoué (voir [Configuration de l’option de nouvelle synchronisation des annuaires](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)).

   **Délai d’expiration de verrouillage de tâche de grappe en minutes :** option utilisée dans les environnements organisés en grappes. Si la synchronisation échoue sur un nœud et que le verrouillage de la grappe n’est pas désactivé, cette valeur permet de spécifier le nombre de minutes durant lesquelles un autre nœud doit patienter avant de forcer l’acquisition du verrouillage. La valeur par défaut est de `15` minutes. Les valeurs valides sont `1` à `1440` minutes.

1. (Facultatif) Modifiez les attributs suivants, puis cliquez sur **[!UICONTROL OK]** :

   **Contrôle des événements dans User Manager :** sélectionnez cette option pour activer le contrôle des événements de synchronisation des annuaires et des événements d’authentification tels que les réussites, les échecs et les verrouillages. Par défaut, cette option n’est pas sélectionnée, à moins que vous ayez installé un composant qui requiert un contrôle, comme Rights Management. Ce paramètre met à jour la clé d’entrée `APSAuditService` dans le fichier de configuration.

   **Création automatique de groupe dynamique :** permet la création automatique de groupes dynamiques à partir des domaines d’adresses électroniques (voir [Créer un groupe dynamique](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)).

Vous pouvez également revenir aux paramètres d’origine de User Management en cliquant sur Recharger.
