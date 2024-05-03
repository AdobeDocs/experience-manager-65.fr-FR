---
title: Utiliser en mode hors ligne
description: Mettre votre appareil mobile hors ligne en dehors de votre plage de réseau AEM Forms ou en mode hors ligne complet et travailler sur l’application AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 100%

---

# Utiliser en mode hors ligne {#working-in-the-offline-mode}

Le mode hors ligne de l’application d’AEM Forms permet de travailler en toute facilité, même lorsque l’application se déconnecte. Vous pouvez ouvrir, mettre à jour et même envoyer un formulaire sans avoir besoin d’une connexion réseau.

Commencez à travailler dans l’application AEM Forms en la synchronisant avec le serveur AEM Forms. Tous les formulaires qui vous sont assignés sont téléchargés dans votre application. Pour AEM Forms on JEE, les tâches sont récupérées dans l’onglet Tâches et les formulaires associés aux points de départ et autres formulaires dans l’onglet Formulaires. Pour AEM Forms on OSGi, seuls les formulaires sont chargés dans l’onglet Formulaires.

Pour plus d’informations sur les modalités de synchronisation de l’application, consultez [Synchronisation de l’application](/help/forms/using/sync-app.md).

## Rendre Forms disponible hors ligne {#making-forms-available-offline}

Lorsque vous synchronisez votre application avec le serveur AEM Forms, les formulaires sont téléchargés sur votre appareil mobile. Cependant, par défaut, les pièces jointes associées avec le formulaire ne sont pas téléchargées. Cela signifie que si vous êtes en ligne, vous pouvez afficher les pièces jointes. Toutefois, pour vous assurer que vous pouvez afficher la pièce jointe en mode hors ligne, modifiez les paramètres par défaut de votre application.

Pour vous assurer que les pièces jointes associées sont téléchargées avec chaque formulaire, activez l’option de récupération des pièces jointes. Pour plus d’informations, voir [Mise à jour des paramètres généraux](/help/forms/using/update-general-settings.md).

Le téléchargement de données sur l’appareil mobile pouvant affecter ses performances, l’option de récupération des pièces jointes est désactivée par défaut. Les pièces jointes sont récupérées sur l’appareil pour toutes les tâches téléchargées à partir du serveur après le réglage de ce paramètre sur ON (Activé). En mode hors ligne, un utilisateur peut ensuite travailler sur toutes les tâches téléchargées sur l’appareil après avoir activé l’option de **Récupération des pièces jointes**.

## Configuration du service hors ligne pour l’application AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

Le service hors ligne de l’application AEM Forms identifie les ressources utilisées dans un formulaire. L’application AEM Forms repose sur ce service pour obtenir des informations sur les dépendances des formulaires. Des informations sur les dépendances de formulaire sont requises pour activer les fonctionnalités hors ligne. Le service hors ligne de l’application AEM Forms met en cache les chemins ou les URL des ressources utilisées dans un formulaire. Le cache est mis à jour en fonction des modifications apportées au formulaire et de la période de validité configurée pour le service hors ligne. La mise en cache des chemins ou des URL des ressources utilisées dans un formulaire améliore les performances côté serveur.

Pour configurer le composant hors ligne côté serveur de l’application AEM Forms :

1. Dans l’instance de création, accédez à **Adobe Experience Manager** > **Outils** > **Formulaires** > **Configurer le service hors ligne de l’application Forms**.

   URL : `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. Sous Paramètres généraux, vous pouvez effectuer les opérations suivantes :

   * **Effacer le cache** : efface le cache côté serveur des dépendances de formulaire.
   * **Réinitialiser la configuration** : réinitialise la configuration hors ligne de l’application AEM Forms.
   * **Validité du cache** : indique la période de validité du cache hors ligne côté serveur.
   * **Chemins d’observation des ressources** : spécifie les chemins où le service hors ligne surveille les modifications de ressources. Si des modifications se produisent dans les chemins d’accès spécifiés, le cache hors ligne de tous les formulaires dépendants est mis à jour. Par exemple, `/etc/clientlibs/fd,/content/dam/images`.

1. Dans l’onglet **Cache de ressource manuel**, spécifiez les dépendances de formulaire que le service hors ligne ne peut pas identifier. Vous pouvez spécifier des ressources telles que des images chargées à partir de JavaScript. L’application AEM Forms téléchargera également ces ressources pour le mode hors ligne.
