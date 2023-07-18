---
title: Application de bureau AEM pour AEM Forms
seo-title: AEM desktop app for AEM Forms
description: Application de bureau AEM pour AEM Forms
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 60%

---

# Application de bureau AEM pour AEM Forms {#aem-desktop-app-for-aem-forms}

L’application de bureau AEM vous permet de mapper le référentiel des actifs Adobe Experience Manager (AEM) et les fichiers binaires AEM Forms à un répertoire réseau sur votre système. Vous pouvez afficher les ressources synchronisées et les fichiers binaires dans un explorateur de fichiers et utiliser diverses applications pour modifier les fichiers selon vos besoins. Outre l’affichage des fichiers, vous pouvez également créer, charger et supprimer les fichiers binaires. Vous pouvez également ouvrir, modifier et enregistrer des fichiers directement à partir du logiciel. Par exemple, vous pouvez ouvrir et modifier directement un fichier XDP à partir de Designer. Les modifications apportées aux actifs localement sont répercutés dans le référentiel des AEM Assets et dans l’interface utilisateur AEM Forms.

Vous pouvez télécharger l’application à partir d’une instance AEM. Pour obtenir des informations détaillées sur le téléchargement de l’application, voir [Notes de mise à jour de l’application de bureau AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=fr).

## Actifs AEM Forms pris en charge par l’application de bureau AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Vous pouvez utiliser l’application pour synchroniser les fichiers binaires AEM Forms du type Form Templates (.xdp), PDF Form (.pdf), Document (.pdf), Images, Schéma XML (.xsd), Feuilles de style (.xfs). L’application répertorie tous les autres fichiers (fichiers non pris en charge) sous la forme de fichiers de 0 octet. L’énumération des fichiers non pris en charge comme fichiers de 0 octet garantit que l’utilisateur est conscient de l’existence d’autres ressources disponibles sur le serveur AEM Forms.

>[!NOTE]
>
>Un nom de fichier ne peut contenir que des caractères alphanumériques, des tirets ou des traits de soulignement.

## Activer AEM Forms pour l’application de bureau AEM {#enable-aem-forms-for-aem-desktop-app}

L’application de bureau AEM utilise le protocole WebDAV sous Microsoft Windows et SMB1 sous Mac OS X pour la connexion à un serveur AEM Forms. Par défaut, le serveur AEM Forms ne permet pas de synchroniser les fichiers binaires et d’autres ressources à l’aide d’un client WebDAV ou SMB. Effectuez les étapes suivantes pour activer AEM Forms pour l’application de bureau AEM :

1. Connectez-vous à AEM Forms en tant qu’administrateur.
1. Dans l’instance d’auteur, cliquez sur ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Outils]** ![marteau](assets/hammer.png) > **[!UICONTROL Déploiement > Opérations > Console web]**. La console web s’ouvre dans une nouvelle fenêtre.
1. Dans la fenêtre de la console Web, recherchez et ouvrez l’option **[!UICONTROL Configuration du module complémentaire Forms Manager]**.
1. Dans la boîte de dialogue Configuration du module complémentaire Forms Manager, désélectionnez la case à cocher **[!UICONTROL Synchroniser les ressources de façon asynchrone]**, puis cliquez sur **[!UICONTROL Enregistrer]**.
1. Redémarrez le serveur AEM Forms. Après le redémarrage, le serveur AEM Forms permet d’accepter et de partager du contenu avec lʼapplication de bureau AEM.
1. Ouvrez l’application et connectez-vous au serveur AEM Forms.

   Une fois la connexion établie, l’application remplit les dossiers `content/dam` et `content/dam/formsanddocuments`. En plus de déplacer des fichiers des dossiers ci-dessus vers des dossiers locaux, vous pouvez à l’inverse utiliser l’application pour déplacer du contenu entre des dossiers remplis automatiquement.
