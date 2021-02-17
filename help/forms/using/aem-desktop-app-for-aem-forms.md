---
title: AEM application pour ordinateur de bureau pour AEM Forms
seo-title: AEM application pour ordinateur de bureau pour AEM Forms
description: AEM application pour ordinateur de bureau pour AEM Forms
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 57%

---


# Application de bureau AEM pour AEM Forms {#aem-desktop-app-for-aem-forms}

AEM application de bureau vous permet de mapper le référentiel Adobe Experience Manager (AEM) Assets et les fichiers binaires AEM Forms à un répertoire réseau sur votre système. Vous pouvez afficher les actifs et les fichiers binaires synchronisés dans un explorateur de fichiers et utiliser différentes applications pour modifier les fichiers selon les besoins. Outre l’affichage des fichiers, vous pouvez également créer, charger et supprimer les fichiers binaires. Vous pouvez également ouvrir, modifier et enregistrer les fichiers directement à partir du logiciel. Par exemple, vous pouvez directement ouvrir et modifier un fichier XDP à partir de Designer. Les modifications apportées aux actifs localement sont répercutés dans le référentiel des actifs AEM et dans l’interface utilisateur AEM Forms.

Vous pouvez télécharger l’application à partir d’une instance AEM. Pour plus d’informations sur le téléchargement de l’application, voir [Notes de mise à jour AEM l’application de bureau](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## Ressources AEM Forms prises en charge dans l’application de bureau AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Vous pouvez utiliser l’application pour synchroniser les fichiers binaires des types suivants : modèles de formulaire (.xdp), formulaire PDF (.pdf), document (.pdf), images, schéma XML (.xsd), feuilles de style (.xfs). L’application répertorie tous les autres fichiers (fichiers non pris en charge) en tant que fichiers de 0 octets. L’énumération des fichiers non pris en charge en tant que fichiers de 0 octet garantit que l’utilisateur est conscient de l’existence d’autres ressources disponibles sur le serveur AEM Forms.

>[!NOTE]
>
>Un nom de fichier ne peut contenir que des caractères alphanumériques, des traits d’union ou des caractères de soulignement.

## Activer AEM Forms pour l’application de bureau AEM {#enable-aem-forms-for-aem-desktop-app}

AEM application de bureau utilise le protocole WebDAV sous Microsoft Windows et SMB1 sous Mac OS X pour se connecter à un serveur AEM Forms. Le serveur AEM Forms n’est pas activé pour synchroniser les fichiers binaires et autres ressources avec un client WebDAV ou SMB. Suivez les étapes ci-après pour activer AEM Forms pour AEM application de bureau :

1. Connectez-vous à AEM Forms en tant qu’administrateur.
1. Dans l’instance d’auteur, cliquez sur ![adobeexperience emanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Outils]** ![marteau](assets/hammer.png) **[!UICONTROL Déploiement > Opérations > Console Web]**. La console Web s’ouvre dans une nouvelle fenêtre.
1. Dans la fenêtre de la console Web, recherchez et ouvrez l’option **[!UICONTROL Configuration du module complémentaire Forms Manager]**.
1. Dans la boîte de dialogue Configuration du module complémentaire Forms Manager, désélectionnez la case à cocher **[!UICONTROL Synchroniser les ressources de façon asynchrone]**, puis cliquez sur **[!UICONTROL Enregistrer]**.
1. Redémarrez le serveur AEM Forms. Après le redémarrage, le serveur AEM Forms est activé pour accepter et partager du contenu avec AEM application de bureau.
1. Ouvrez l’application et connectez-vous au serveur AEM Forms.

   Une fois la connexion établie, l’application remplit les dossiers `content/dam` et `content/dam/formsanddocuments`. En plus de déplacer des fichiers des dossiers ci-dessus vers des dossiers locaux et vice versa, vous pouvez utiliser l’application pour déplacer le contenu entre des dossiers remplis automatiquement.

