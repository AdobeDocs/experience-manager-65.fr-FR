---
title: Activation des conversions de fichiers multithreads
description: Découvrez comment activer les conversions de fichiers multithreads.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 6%

---

# Activation des conversions de fichiers multithreads {#enabling-multi-threaded-file-conversions}

PDF Generator vous permet d’activer les conversions de fichiers multithreads pour certains types de fichiers. La conversion de fichiers multithreads améliore les performances de PDF Generator en lui permettant d’effectuer plusieurs conversions en même temps.

## Activation des conversions multithreads de fichiers OpenOffice, Word et PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Par défaut, PDF Generator ne peut convertir qu’un seul document OpenOffice, Microsoft® Word ou PowerPoint à la fois. Si vous activez les conversions multithreads, PDF Generator peut convertir plusieurs documents simultanément. PDF Generator lance plusieurs instances d’OpenOffice ou de PDFMaker (utilisés pour effectuer les conversions Word et PowerPoint).

>[!NOTE]
>
>Les conversions de fichiers multithreads ne sont pas prises en charge avec Microsoft® Word 2003 et PowerPoint 2003. Pour activer les conversions de fichiers multithreads, effectuez une mise à niveau vers Microsoft® Word 2007 et PowerPoint 2007 ou Microsoft® Word 2010 et PowerPoint 2010.

>[!NOTE]
>
Les conversions de fichiers multithreads ne sont pas prises en charge avec Microsoft® Excel, Microsoft® Visio, Microsoft® Project ou Microsoft® Publisher.

Chaque instance d’OpenOffice ou de PDFMaker est lancée à l’aide d’un compte utilisateur distinct. Chaque compte utilisateur ajouté doit être un utilisateur valide disposant de droits d’administrateur sur le serveur Forms. Dans un environnement organisé en grappe, le même ensemble d’utilisateurs doit être valide pour tous les noeuds de la grappe.

Sur la page Comptes d’utilisateurs de la console d’administration, vous pouvez spécifier les comptes d’utilisateurs à utiliser pour les conversions de fichiers multithreads. Vous pouvez ajouter des comptes, les supprimer ou modifier des mots de passe de compte. Si vous exécutez PDF Generator sous Windows Server 2003 ou Windows Server 2008, ajoutez au moins trois comptes d’utilisateurs disposant de droits d’administrateur.

Lors de l’ajout d’utilisateurs pour OpenOffice, Microsoft® Word ou Microsoft® PowerPoint sous Windows Server 2003 ou 2008, ou pour OpenOffice sous Linux® ou Sun™ Solaris™, fermez les boîtes de dialogue d’activation initiale pour tous les utilisateurs.

### Ajouter le droit de remplacer le jeton de niveau processus {#add-the-right-to-replace-the-process-level-token}

Sur un système d’exploitation Windows, les comptes utilisateur administrateur utilisés pour la conversion de PDF (utilisateurs de PDFG) doivent remplacer les privilèges de jeton de niveau processus. Vous pouvez ajouter ce droit à l’aide de l’éditeur de stratégie de groupe :

1. Dans le menu Démarrer de Windows, cliquez sur Exécuter, puis saisissez gpedit.msc.
1. Cliquez sur Stratégie d’ordinateur local > Configuration d’ordinateur > Paramètres Windows > Paramètres de sécurité > Stratégies locales > Attribution des droits utilisateur. Modifiez la variable *Remplacer un jeton de niveau processus* pour inclure le groupe Administrateurs.
1. Ajoutez l’utilisateur à l’entrée Remplacer un jeton de niveau processus .

### Configuration supplémentaire requise pour OpenOffice, Microsoft® Word et Microsoft® PowerPoint sous Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Si vous exécutez OpenOffice, Microsoft® Word ou Microsoft® PowerPoint sous Windows Server 2008, désactivez l’UAC pour chaque utilisateur ajouté.

1. Cliquez sur Panneau de Contrôle > Comptes d’utilisateurs > Activer ou désactiver le contrôle des comptes d’utilisateurs.
1. Désélectionnez la case « Utiliser le contrôle des comptes d’utilisateurs (UAC) pour vous aider à protéger votre ordinateur » et cliquez sur OK.
1. Redémarrez l’ordinateur pour que les paramètres prennent effet.

### Configuration supplémentaire requise pour OpenOffice sous Linux® ou Solaris™ {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Ajout de comptes d’utilisateurs. (Voir [Ajout d’un compte d’utilisateur](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. Ensuite, vous devez modifier le fichier /etc/sudoers. L’autorisation par défaut pour ce fichier est 440. Définissez l’autorisation d’écriture pour ce fichier.
1. Ajoutez des entrées pour les utilisateurs supplémentaires (autres que l’administrateur exécutant le serveur Forms) dans le fichier /etc/sudoers. Par exemple, si vous exécutez AEM Forms en utilisant le nom d’utilisateur « Icadm » et un serveur appelé « myhost » et que vous souhaitez incarner les utilisateurs user1 et user2, ajoutez les entrées suivantes dans le fichier /etc/sudoers :

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Cette configuration permet à lcadm d’exécuter n’importe quelle commande sur l’hôte &quot;myhost&quot; en tant qu’utilisateur1 ou utilisateur2 sans demander de mot de passe.

   >[!NOTE]
   >
   Assurez-vous que vous avez attribué les rôles utilisateur système et utilisateur PDFG à &quot;user1&quot; et &quot;user2&quot; . Pour attribuer un rôle PDFG à un utilisateur, voir [Ajout d’un compte d’utilisateur](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. Toujours dans le fichier /etc/sudoers, recherchez et commentez cette ligne en ajoutant un signe dièse (#) au début de la ligne :

   ```shell
   Defaults requiretty
   ```

   Vous pouvez ainsi ajouter des utilisateurs Linux®.

1. Remplacez l’autorisation pour le fichier etc/sudoers par 440.
1. Autoriser tous les utilisateurs ajoutés via [Ajout d’un compte d’utilisateur](enabling-multi-threaded-file-conversions.md#add-a-user-account) pour établir des connexions au serveur Forms. Par exemple, pour autoriser un utilisateur local nommé user1 à se connecter au serveur Forms, utilisez la commande suivante :

   `xhost +local:user1@`

   Pour plus d’informations, voir la documentation sur les commandes xhost.

1. Redémarrez le serveur.

>[!NOTE]
>
OpenOffice doit être installé dans un répertoire accessible à tous les utilisateurs de PDFG. Vous pouvez le vérifier en vous connectant en tant qu’utilisateur PDFG et en vérifiant si vous pouvez lancer OpenOffice sans problème.

### Ajout d’un compte d’utilisateur {#add-a-user-account}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Comptes utilisateur.
1. Cliquez sur Ajouter et saisissez le nom et le mot de passe d’un utilisateur possédant des privilèges d’administrateur sur le serveur Forms. Si vous configurez des utilisateurs pour OpenOffice, fermez les boîtes de dialogue d’activation OpenOffice initiales.

   >[!NOTE]
   >
   Si vous configurez des utilisateurs pour OpenOffice, le nombre d’instances d’OpenOffice ne peut pas être supérieur au nombre de comptes d’utilisateurs spécifié dans cette étape.

1. Redémarrez le serveur Forms.

### Suppression d’un utilisateur de la liste utilisée pour les conversions de fichiers multithreads {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Comptes utilisateur.
1. Cochez la case en regard de l’utilisateur à supprimer, puis cliquez sur Supprimer.
1. Sur la page de confirmation, cliquez sur Supprimer.
1. Redémarrez le serveur Forms.

### Modification du mot de passe d’un compte {#change-the-password-for-an-account}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Comptes utilisateur.
1. Cliquez sur le nom d’utilisateur, puis saisissez et confirmez le nouveau mot de passe. Ce mot de passe doit correspondre au mot de passe système de l’utilisateur.
