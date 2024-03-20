---
title: Désactiver l’UAC pour la configuration PDFG applicable à la fois à JEE et OSGI
description: Découvrez les étapes à suivre pour désactiver la configuration UAC pour PDFG afin de corriger la conversion Word vers PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 62%

---

# Impossible de convertir un fichier Word ou Excel en PDF sous Windows Server. {#unable-to-convert-word-excel-files-PDF}

## Problème {#issue}

Lorsque l’utilisateur tente de convertir des fichiers Word ou Excel en PDF sur Microsoft® Windows Server, l’erreur suivante se produit :

*Message d’erreur du convertisseur principal :*
*Le système ALC-PDG-015-003-The ne peut pas ouvrir le fichier d’entrée. Envoyez à nouveau votre fichier ou contactez votre administrateur système.*


## Solution {#solution}

Procédez comme suit :

1. Pour accéder à l’utilitaire de configuration système, sélectionnez **[!UICONTROL Démarrer > Exécuter]** et saisissez **[!UICONTROL MSCONFIG]**.
1. Cliquez sur l’onglet **[!UICONTROL Outils]**, faites défiler l’écran vers le bas, puis sélectionnez **[!UICONTROL Modifier les paramètres de contrôle de compte d’utilisateur]**. Cliquez sur **[!UICONTROL Launch]** vous pouvez donc exécuter la commande dans une nouvelle fenêtre.
1. Déplacez le curseur sur le niveau Ne jamais m’avertir. Cela fait, fermez la fenêtre de commande, puis celle de la configuration du système.
1. Vérifiez que le paramètre de registre pour l’UAC est défini sur 0 (zéro). Pour vérifier, procédez comme suit :

   1. Microsoft® recommande de sauvegarder le registre avant de le modifier. Pour obtenir la procédure détaillée, voir [Comment sauvegarder et restaurer le registre dans Windows](https://support.microsoft.com/fr-fr/help/322756).
   1. Ouvrez l’éditeur de registre Microsoft® Windows. Pour ouvrir l’éditeur de registre, accédez à Démarrer > Exécuter, saisissez regedit, puis cliquez sur OK.
   1. Accédez à `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Vérifiez que la valeur de EnableLUA est définie sur 0 (zéro).
   1. Assurez-vous que la valeur de **EnableLUA** est définie sur 0 (zéro). Si la valeur n’est pas 0, remplacez-la par 0. Fermez l’éditeur du registre.

1. Redémarrez l’ordinateur.

## Application {#appliesto}

Cette solution s’applique au serveur AEM Forms on JEE et à AEM Forms on OSGi Server.
