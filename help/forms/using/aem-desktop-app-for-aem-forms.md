---
title: Application de bureau Adobe Experience Manager (AEM) pour AEM Forms
description: Application de bureau Adobe Experience Manager (AEM) pour AEM Forms
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin,User
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '468'
ht-degree: 100%

---

# Application de bureau Adobe Experience Manager (AEM) pour AEM Forms {#aem-desktop-app-for-aem-forms}

L’application de bureau AEM vous permet de mapper le référentiel des actifs Adobe Experience Manager (AEM) et les fichiers binaires AEM Forms à un répertoire réseau sur votre système. Vous pouvez afficher les ressources synchronisées et les fichiers binaires dans un explorateur de fichiers et utiliser diverses applications pour modifier les fichiers selon vos besoins. Outre l’affichage des fichiers, vous pouvez également créer, charger et supprimer les fichiers binaires. Vous pouvez également ouvrir, modifier et enregistrer des fichiers directement dans le logiciel. Vous pouvez, par exemple, ouvrir et modifier un fichier XDP directement dans Designer. Les modifications apportées aux ressources localement sont répercutées dans le référentiel AEM Assets et dans l’interface utilisateur AEM Forms.

Vous pouvez télécharger l’application à partir d’une instance AEM. Pour obtenir des informations détaillées sur le téléchargement de l’application, voir [Notes de mise à jour de l’application de bureau AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=fr).

## Actifs AEM Forms pris en charge par l’application de bureau AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Vous pouvez utiliser l’application pour synchroniser les fichiers binaires des types suivants : modèles de formulaire (.xdp), formulaire PDF (.pdf), document (.pdf), images, schéma XML (.xsd), feuilles de style (.xfs). L’application répertorie tous les autres fichiers (fichiers non pris en charge) sous la forme de fichiers de 0 octet. L’utilisateur ou l’utilisatrice est ainsi au courant de l’existence des autres ressources disponibles sur le serveur AEM Forms. 

>[!NOTE]
>
>Un nom de fichier ne peut contenir que des caractères alphanumériques, des tirets ou des traits de soulignement.

## Activer AEM Forms pour l’application de bureau AEM {#enable-aem-forms-for-aem-desktop-app}

L’application de bureau AEM utilise le protocole WebDAV sous Microsoft® Windows et SMB1 sous macOS X pour la connexion à un serveur AEM Forms. Par défaut, le serveur AEM Forms ne permet pas de synchroniser les fichiers binaires et d’autres ressources à l’aide d’un client WebDAV ou SMB. Effectuez la procédure suivante pour activer AEM Forms pour l’application de bureau AEM :

1. Connectez-vous à AEM Forms en tant qu’administrateur.
1. Dans l’instance d’auteur, cliquez sur ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Outils]** ![marteau](assets/hammer.png) > **[!UICONTROL Déploiement > Opérations > Console web]**. La console web s’ouvre dans une nouvelle fenêtre.
1. Dans la fenêtre de la console web, recherchez et ouvrez l’option **[!UICONTROL Configuration du module complémentaire Forms Manager]**.
1. Dans la boîte de dialogue Configuration du module complémentaire Forms Manager, désélectionnez la case à cocher **[!UICONTROL Synchroniser les ressources de façon asynchrone]**, puis cliquez sur **[!UICONTROL Enregistrer]**.
1. Redémarrez le serveur AEM Forms. Après le redémarrage, le serveur AEM Forms permet d’accepter et de partager du contenu avec lʼapplication de bureau AEM.
1. Ouvrez l’application et connectez-vous au serveur AEM Forms.

   >[!NOTE]
   >
   > Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

   Une fois la connexion établie, l’application remplit les dossiers `content/dam` et `content/dam/formsanddocuments`. En plus de déplacer des fichiers des dossiers ci-dessus vers des dossiers locaux et vice versa, vous pouvez utiliser l’application pour déplacer le contenu entre des dossiers remplis automatiquement.
