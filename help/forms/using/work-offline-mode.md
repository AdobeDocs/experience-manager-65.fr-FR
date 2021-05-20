---
title: Utilisation en mode hors ligne
seo-title: Utilisation en mode hors ligne
description: Utilisez l’application AEM Forms sur votre périphérique mobile en dehors de vos réseaux AEM Forms ou en mode hors ligne complet
seo-description: Utilisez l’application AEM Forms sur votre périphérique mobile en dehors de vos réseaux AEM Forms ou en mode hors ligne complet
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 82%

---

# Utilisation en mode hors ligne {#working-in-the-offline-mode}

Le mode hors ligne de l’application AEM Forms vous permet de travailler en toute transparence, même si l’application est hors ligne. Vous pouvez ouvrir, mettre à jour et même envoyer un formulaire sans avoir besoin d’une connexion réseau.

Vous commencez à travailler sur l’application AEM Forms en synchronisant votre application avec le serveur AEM Forms. Tous les formulaires qui vous sont assignés sont téléchargés dans votre application. Pour AEM Forms sur JEE, les tâches sont récupérées dans l’onglet des tâches, les formulaires associés à des points de départ et d’autres formulaires sous l’onglet Formulaires. Pour AEM Forms sur OSGi, seuls les formulaires sont chargés dans l’onglet Formulaires.

Pour plus de d’informations sur la synchronisation de l’application, consultez la section [Synchronisation de l’application](/help/forms/using/sync-app.md).

## Disponibilité des formulaires en mode hors ligne  {#making-forms-available-offline}

Lorsque vous synchronisez votre application avec le serveur AEM Forms, les formulaires sont téléchargés sur votre périphérique mobile. Cependant, par défaut, les pièces jointes associées avec le formulaire ne sont pas téléchargées. Cela signifie que si vous êtes en ligne, vous pouvez afficher les pièces jointes. Toutefois, pour pouvoir afficher la pièce jointe en mode hors ligne, modifiez les paramètres par défaut de votre application.

Pour vous assurer que les pièces jointes associées sont téléchargées avec chaque formulaire, activez l’option de récupération des pièces jointes. Pour plus d’informations, consultez [Mise à jour des paramètres généraux](/help/forms/using/update-general-settings.md).

Le téléchargement de données sur le périphérique mobile pouvant affecter ses performances, l’option de récupération des pièces jointes est désactivée par défaut. Les pièces jointes sont récupérées sur le périphérique pour toutes les tâches téléchargées à partir du serveur après le réglage de ce paramètre sur ON (Activé). En mode hors ligne, un utilisateur peut alors travailler sur toutes les tâches téléchargées sur l’appareil après avoir défini les options **Récupérer les pièces jointes** sur ON.

## Configuration du service hors ligne pour l’application AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

Le service hors ligne de l’application AEM Forms identifie les ressources utilisées dans un formulaire. L’application AEM Forms s’appuie sur ce service pour obtenir des informations sur les dépendances des formulaires. Des informations sur les dépendances des formulaires sont requises pour activer les fonctionnalités hors ligne. Le service hors ligne de l’application AEM Forms met en cache les chemins ou les URL des ressources utilisées dans un formulaire. Le cache est mis à jour en fonction des modifications apportées au formulaire et de la période de validité configurée pour le service hors ligne. La mise en cache des chemins ou des URL des ressources utilisées dans un formulaire améliore les performances côté serveur.

Pour configurer le composant hors ligne côté serveur de l’application AEM Forms :

1. Dans l’instance d’auteur, accédez à **Adobe Experience Manager** >**Outils** > **Forms** > **Configurer le service hors ligne de l’application Forms**.

   URL : `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. Sous Paramètres généraux, vous pouvez effectuer les opérations suivantes :

   * **Effacer le cache** : efface le cache côté serveur des dépendances de formulaires.
   * **Réinitialiser la configuration** : Réinitialise la configuration hors ligne de l’application AEM Forms.
   * **Période de validité du cache** : indique la période de validité du cache hors ligne côté serveur.
   * **Chemins d’observation des ressources** : indique les chemins où le service hors connexion assure le suivi des modifications de ressources. Si des modifications apparaissent dans les chemins indiqués, le cache hors ligne de tous les formulaires dépendants est mis à jour. Par exemple, `/etc/clientlibs/fd,/content/dam/images`.

1. Dans l’onglet **Cache de ressource manuel**, spécifiez les dépendances des formulaires que le service hors ligne ne peut pas identifier. Vous pouvez spécifier des ressources telles que les images chargées à partir de Javascript. L’application AEM Forms téléchargera ensuite ces ressources pour le mode hors ligne.
