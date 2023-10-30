---
title: Désactiver l’UAC pour la configuration PDFG applicable à la fois à JEE et OSGI
description: Procédure de désactivation de l’UAC pour la configuration PDFG pour corriger la conversion Word en PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 93%

---

# Impossible de convertir un fichier Word ou Excel en PDF sous Windows Server. {#unable-to-convert-word-excel-files-PDF}

## Problème {#issue}

Lorsque l’utilisateur ou l’utilisatrice tente de convertir des fichiers Word ou Excel en PDF sur Microsoft Windows Server, l’erreur suivante se produit :

*Message d’erreur du convertisseur principal :
ALC-PDG-015-003-Le système ne peut pas ouvrir le fichier d’entrée. Envoyez à nouveau le fichier ou contactez votre administrateur système.*


## Solution {#solution}

Exécutez les étapes suivantes afin de résoudre ce problème :
1. Pour accéder à l’utilitaire de configuration système, sélectionnez **[!UICONTROL Démarrer > Exécuter]** et saisissez **[!UICONTROL MSCONFIG]**.
1. Cliquez sur l’onglet **[!UICONTROL Outils]**, faites défiler l’écran vers le bas, puis sélectionnez **[!UICONTROL Modifier les paramètres de contrôle de compte d’utilisateur]**. Cliquez sur **[!UICONTROL Démarrer]** pour lancer la commande dans une nouvelle fenêtre.
1. Déplacez le curseur sur le niveau Ne jamais m’avertir. Cela fait, fermez la fenêtre de commande, puis celle de la configuration du système.
1. Vérifiez que le paramètre de registre pour l’UAC est défini sur 0 (zéro). Pour vérifier, procédez comme suit :

   1. Microsoft® recommande de sauvegarder le registre avant de le modifier. Pour obtenir la procédure détaillée, voir [Comment sauvegarder et restaurer le registre dans Windows](https://support.microsoft.com/fr-fr/help/322756).
   1. Ouvrez l’éditeur de registre Microsoft® Windows. Pour ouvrir l’éditeur de registre, accédez à Démarrer > Exécuter, saisissez regedit, puis cliquez sur OK.
   1. Accédez à `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assurez-vous que la valeur de EnableLUA est définie sur 0 (zéro).
   1. Assurez-vous que la valeur de **EnableLUA** est définie sur 0 (zéro). Si la valeur n’est pas 0, remplacez la valeur par 0. Fermez l’éditeur du registre.

1. Redémarrez votre ordinateur.

## Application {#appliesto}

Cette solution s’applique aux éléments suivants :
* AEM Forms sur le serveur JEE
* AEM Forms sur le serveur OSGi
