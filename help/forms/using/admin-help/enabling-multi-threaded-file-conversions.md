---
title: Activation des conversions de fichiers multithreads
description: Découvrez comment activer des conversions de fichiers multithreads.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 100%

---

# Activation des conversions de fichiers multithreads {#enabling-multi-threaded-file-conversions}

PDF Generator permet d’effectuer des conversions multithreads de certains types de fichiers. Ce type de conversion améliore les performances de PDF Generator en lui permettant d’effectuer plusieurs conversions simultanément.

## Activer les conversions multithreads de fichiers OpenOffice, Word et PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Par défaut, PDF Generator ne peut convertir qu’un document OpenOffice, Microsoft® Word ou PowerPoint à la fois. Si vous activez les conversions de fichiers multithreads, PDF Generator peut convertir plusieurs documents simultanément. PDF Generator lance plusieurs instances d’OpenOffice ou PDFMaker (utilisés pour effectuer les conversions Word et PowerPoint).

>[!NOTE]
>
>Les conversions de fichiers multithreads ne sont pas prises en charge avec Microsoft® Word 2003 et PowerPoint 2003. Pour activer les conversions de fichiers multithreads, effectuez une mise à niveau vers Microsoft® Word 2007 et PowerPoint 2007 ou Microsoft® Word 2010 et PowerPoint 2010.

>[!NOTE]
>
>La conversion multithread de fichiers n’est pas prise en charge avec Microsoft® Excel, Microsoft® Visio, Microsoft® Project et Microsoft® Publisher.

Chaque instance d’OpenOffice ou de PDFMaker est lancée avec un compte utilisateur séparé. Chaque compte utilisateur ajouté doit correspondre à un utilisateur ou une utilisatrice valide disposant de droits d’administration sur le serveur Forms. Dans un environnement en cluster, le même groupe d’utilisateurs et d’utilisatrices doit être valide sur tous les nœuds du cluster.

Dans la page Comptes utilisateur de la console d’administration, vous pouvez spécifier les comptes à utiliser pour les conversions de fichier multithreads. Vous pouvez ajouter des comptes, en supprimer ou modifier des mots de passe de compte. Si vous exécutez PDF Generator sous Windows Server 2003 ou 2008, vous devez ajouter au moins trois comptes utilisateurs possédant des droits d’administration.

Lors de l’ajout d’utilisateurs ou d’utilisatrices pour OpenOffice, Microsoft® Word ou Microsoft® PowerPoint sous Windows 2003 ou 2008, ou pour OpenOffice sous Linux® ou Sun™ Solaris™, fermez les boîtes de dialogue d’activation initiale pour tous les utilisateurs et utilisatrices.

### Ajouter le droit de remplacer le jeton de niveau processus {#add-the-right-to-replace-the-process-level-token}

Sur un système d’exploitation Windows, les comptes utilisateur de l’administrateur ou de l’administratrice utilisés pour la conversion au format PDF (utilisateurs et utilisatrices de PDFG) doivent disposer du droit Remplacer le jeton de niveau processus. Vous pouvez ajouter ce droit à l’aide de l’Éditeur de politiques de groupe :

1. Dans le menu Démarrer de Windows, cliquez sur Exécuter puis saisissez gpedit.msc.
1. Cliquez sur Politique Ordinateur local > Configuration ordinateur > Paramètres Windows > Paramètres de sécurité > Politiques locales > Attribution des droits utilisateur. Modifiez la règle *Remplacer un jeton de niveau processus* pour inclure le groupe Administrateurs et administratrices.
1. Ajoutez l’utilisateur ou l’utilisatrice à l’entrée Remplacer un jeton de niveau processus.

### Configuration supplémentaire requise pour OpenOffice, Microsoft® Word et Microsoft® PowerPoint sous Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Si vous exécutez OpenOffice, Microsoft® Word ou Microsoft® PowerPoint sous Windows 2008, désactivez le Contrôle de compte utilisateur (UAC) à chaque utilisateur ou utilisatrice ajoutée.

1. Cliquez sur Panneau de configuration > Comptes utilisateurs > Activer ou désactiver le contrôle de compte utilisateur.
1. Désélectionnez la case « Utiliser le contrôle des comptes d’utilisateurs (UAC) pour vous aider à protéger votre ordinateur » et cliquez sur OK.
1. Redémarrez l’ordinateur pour que ces paramètres soient pris en compte.

### Configuration supplémentaire requise pour OpenOffice sous Linux® ou Solaris™ {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Ajoutez des comptes utilisateurs. (voir [Ajouter un compte utilisateur](enabling-multi-threaded-file-conversions.md#add-a-user-account)).
1. Vous allez maintenant apporter des modifications au fichier /etc/sudoers. L’autorisation par défaut pour ce fichier est 440. Redéfinissez l’autorisation en écriture pour ce fichier.
1. Ajoutez des entrées pour les utilisateurs et utilisatrices supplémentaires (autres que l’administrateur ou l’administratrice exécutant le serveur Forms ) dans le fichier /etc/sudoers. Par exemple, si vous exécutez AEM Forms en utilisant le nom d’utilisateur « Icadm » et un serveur appelé « myhost » et que vous souhaitez incarner les utilisateurs ou utilisatrices user1 et user2, ajoutez les entrées suivantes dans le fichier /etc/sudoers :

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Cette configuration permet à l’utilisateur ou à l’utilisatrice lcadm d’exécuter toute commande sur l’hôte « myhost » en tant qu’« user1 » ou « user2 » sans devoir saisir un mot de passe.

   >[!NOTE]
   >
   >Vous devez avoir attribué les rôles d’utilisateur et utilisatrice système et d’utilisateur et utilisatrice PDFG à « user1 » et « user2 ». Pour attribuer un rôle PDFG à un utilisateur ou une utilisatrice, voir [Ajouter un compte utilisateur](enabling-multi-threaded-file-conversions.md#add-a-user-account).

1. Toujours dans le fichier /etc/sudoers, recherchez cette ligne et modifiez-la en ajoutant un signe dièse (#) au début de la ligne :

   ```shell
   Defaults requiretty
   ```

   Cela vous permet d’ajouter des utilisateurs et utilisatrices Linux®.

1. Redéfinissez l’autorisation pour le fichier etc/sudoers à 440.
1. Autorisez tous les utilisateurs et utilisatrices ajoutés via l’option [Ajouter un compte utilisateur](enabling-multi-threaded-file-conversions.md#add-a-user-account) à se connecter au serveur Forms. Par exemple, pour autoriser un utilisateur local ou une utilisatrice locale nommé(e) user1 à se connecter au serveur Forms, utilisez la commande suivante :

   `xhost +local:user1@`

   Pour en savoir plus, consultez la documentation relative à la commande xhost.

1. Redémarrez le serveur.

>[!NOTE]
>
>OpenOffice doit être installé dans un emplacement du répertoire auquel tous les utilisateurs et utilisatrices PDFG peuvent accéder. Vous pouvez vérifier en vous connectant en tant qu’utilisateur ou utilisatrice PDFG et en essayant de lancer OpenOffice.

### Ajout d’un compte utilisateur {#add-a-user-account}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Comptes utilisateur.
1. Cliquez sur Ajouter et saisissez le nom et le mot de passe d’un utilisateur ou d’une utilisatrice possédant des privilèges d’administration sur le serveur Forms. Si vous configurez des utilisateurs ou des utilisatrices pour OpenOffice, fermez les boîtes de dialogue d’activation OpenOffice initiales.

   >[!NOTE]
   >
   >Si vous configurez des utilisateurs ou des utilisatrices pour OpenOffice, le nombre d’instances d’OpenOffice ne peut pas être supérieur au nombre de comptes d’utilisateurs spécifié dans cette étape.

1. Redémarrez le serveur Forms.

### Suppression d’un utilisateur ou d’une utilisatrice de la liste utilisée pour les conversions de fichiers multithreads {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Comptes utilisateur.
1. Cochez la case en regard de l’utilisateur ou de l’utilisatrice à supprimer, puis cliquez sur Supprimer.
1. Sur la page de confirmation, cliquez sur Supprimer.
1. Redémarrez le serveur Forms.

### Modification du mot de passe d’un compte {#change-the-password-for-an-account}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Comptes utilisateur.
1. Cliquez sur le nom d’utilisateur ou d’utilisatrice, puis saisissez et confirmez le nouveau mot de passe. Ce mot de passe doit correspondre au mot de passe système de l’utilisateur ou de l’utilisatrice.
