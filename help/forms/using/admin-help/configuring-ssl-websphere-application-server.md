---
title: Configuration de SSL pour WebSphere Application Server
seo-title: Configuration de SSL pour WebSphere Application Server
description: Découvrez comment configurer SSL pour WebSphere Application Server.
seo-description: Découvrez comment configurer SSL pour WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 94%

---


# Configuration de SSL pour WebSphere Application Server {#configuring-ssl-for-websphere-application-server}

Cette section décrit la procédure permettant de configurer SSL sur IBM WebSphere Application Server.

## Création d’un compte d’utilisateur local sur WebSphere {#creating-a-local-user-account-on-websphere}

Pour activer SSL, WebSphere doit accéder à un compte d’utilisateur dans le registre utilisateur du système d’exploitation local, qui soit autorisé à administrer le système :

* (Windows) Créez un utilisateur Windows appartenant au groupe Administrateurs et possédant le droit d’agir en tant que partie du système d’exploitation (voir [Création d’un utilisateur Windows pour WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)).
* (Linux et UNIX) L’utilisateur peut être un utilisateur root ou un autre utilisateur possédant des droits racine. Lorsque vous activez le protocole SSL sur WebSphere, utilisez l’identifiant serveur et le mot de passe de cet utilisateur.

### Création d’un utilisateur Linux ou UNIX sur WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Ouvrez une session en tant qu’utilisateur root.
1. Ouvrez une invite de commande et créez un utilisateur en saisissant la commande suivante :

   * (Linux and Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Définissez le mot de passe du nouvel utilisateur en saisissant `passwd` à l’invite de commande.
1. (Linux and Solaris) Créez un fichier de mots de passe cachés en saisissant `pwconv` (sans paramètre) à l’invite de commande.

   >[!NOTE]
   >
   >(Linux et Solaris) pour que le registre de sécurité du système d’exploitation local du serveur d’applications WebSphere soit opérationnel, le fichier des mots de passe cachés doit exister. Ce fichier s’appelle généralement **/etc/shadow** et est basé sur le fichier /etc/passwd. S’il n’existe pas, une erreur se produit après l’activation de la sécurité globale et la configuration du registre de l’utilisateur comme système d’exploitation local.

1. Ouvrez le fichier de groupe du répertoire /etc dans un éditeur de texte.
1. Ajoutez l’utilisateur créé à l’étape 2 au groupe `root`.
1. Enregistrez et fermez le fichier 
1. (UNIX avec SSL activé) Démarrez et arrêtez WebSphere en tant qu’utilisateur root.

### Création d’un utilisateur Windows pour WebSphere {#create-a-windows-user-for-websphere}

1. Connectez-vous à Windows à l’aide d’un compte d’administrateur.
1. Sélectionnez **Démarrer > Panneau de configuration > Outils d’administration > Gestion de l’ordinateur > Utilisateurs et groupes locaux**.
1. Cliquez avec le bouton droit de la souris sur Utilisateurs et sélectionnez **Nouvel utilisateur**.
1. Saisissez votre nom d’utilisateur et votre mot de passe dans les zones appropriées, puis renseignez éventuellement les autres zones.
1. Supprimez la coche de la case **L’utilisateur doit changer de mot de passe à la prochaine ouverture de session** et cliquez sur **Créer** puis sur **Fermer**.
1. Cliquez sur **Utilisateurs**, cliquez avec le bouton droit de la souris sur l’utilisateur que vous venez de créer, puis choisissez **Propriétés**.
1. Cliquez sur l’onglet **Membre de**, puis sur **Ajouter**.
1. In the Enter The Object Names To Select box, type `Administrators`, click Check Names to ensure that the group name is correct.
1. Cliquez sur **OK**, puis de nouveau sur **OK**.
1. Sélectionnez **Démarrer > Panneau de configuration > Outils d’administration > Stratégie de sécurité locale > Stratégies locales**.
1. Cliquez sur Attribution des droits utilisateur, puis cliquez avec le bouton droit de la souris sur Fonctionner en tant que partie du système d’exploitation et sélectionnez Propriétés.
1. Cliquez sur **Ajouter un utilisateur ou un groupe**.
1. Dans la zone Entrez les noms des objets à sélectionner, saisissez le nom de l’utilisateur que vous avez créé à l’étape 4, cliquez sur **Vérifier les noms** pour vous assurer que le nom est correct, puis cliquez sur **OK**.
1. Cliquez sur **OK** pour fermer la boîte de dialogue Propriétés de Fonctionner en tant que partie du système d’exploitation.

### Configuration de WebSphere pour une utilisation de l’utilisateur nouvellement créé en tant qu’administrateur {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Vérifiez que WebSphere est en cours d’exécution.
1. Dans la console d’administration WebSphere, sélectionnez **Security > Global Security**.
1. Sous Administrative Security, sélectionnez les **rôles utilisateurs administratifs**.
1. Cliquez sur Add et effectuez les opérations suivantes :

   1. Type **&amp;ast;** in the search box and click search.
   1. Cliquez sur le rôle **Administrator**.
   1. Ajoutez l’utilisateur nouvellement créé dans la zone Mapped to role et mappez-le à Administrator.

1. Cliquez sur **OK** et enregistrez les modifications.
1. Redémarrez le profil WebSphere.

## Activation de la sécurité administrative {#enable-administrative-security}

1. Dans la console d’administration WebSphere, sélectionnez **Security > Global Security**.
1. Cliquez sur **Security Configuration Wizard**.
1. Assurez-vous que la case à cocher **Enable Application Security** est activée. Cliquez sur **Suivant**.
1. Sélectionnez **Federated Repositories** et cliquez sur **Next**.
1. Spécifiez les informations d’identification que vous souhaitez configurer et cliquez sur **Next**.
1. Cliquez sur **Terminer**.
1. Redémarrez le profil WebSphere.

   WebSphere commencera à utiliser le fichier de stockage de clés et le fichier de magasin d’approbations (Trust Store) par défaut.

## Activation de SSL (fichier Trust Store et clé personnalisés) {#enable-ssl-custom-key-and-truststore}

Vous pouvez créer des fichiers Trust Store et des fichiers de stockage de clés à l’aide de la console d’administration ou de l’utilitaire iKeyman. Pour un bon fonctionnement d’iKeyman, vérifiez que le chemin d’installation de WebSphere ne contient aucune parenthèse.

1. Dans la console d’administration WebSphere, sélectionnez **Security > SSL certificate and key management**.
1. Cliquez sur **Keystores and certificates** sous Related Items.
1. Dans la liste déroulante **Key store usages**, vérifiez que l’option **SSL Keystores** est sélectionnée. Cliquez sur **Nouveau**.
1. Saisissez un nom et une description logiques.
1. Spécifiez le chemin d’accès à l’emplacement où vous souhaitez créer le fichier de stockage de clés. Si vous avez déjà créé un fichier de stockage de clés par le biais d’iKeyman, spécifiez son chemin d’accès.
1. Spécifiez et confirmez le mot de passe.
1. Choisissez le type de fichier de stockage de clés et cliquez sur **Apply**.
1. Enregistrez la configuration principale.
1. Cliquez sur **Personal Certificate**.
1. Si vous avez déjà ajouté un fichier de stockage de clés à l’aide d’iKeyman, votre certificat s’affiche. Dans le cas contraire, vous devez ajouter un nouveau certificat autosigné en suivant la procédure ci-dessous :

   1. Sélectionnez **Create > Self-signed Certificate**.
   1. Spécifiez les valeurs appropriées dans le formulaire de certificat. Assurez-vous que le nom de l’alias et le nom commun restent le nom de domaine complet de l’ordinateur.
   1. Cliquez sur **Appliquer**.

1. Répétez les étapes 2 à 10 pour créer un fichier Trust Store.

## Application du fichier de stockage de clés et du fichier Trust Store personnalisés au serveur {#apply-custom-keystore-and-truststore-to-the-server}

1. Dans la console d’administration WebSphere, sélectionnez **Security > SSL certificate and key management**.
1. Cliquez sur **Manage endpoint security configuration**. La carte topologique locale s’ouvre.
1. Sous Inbound, sélectionnez un enfant direct de nœuds.
1. Sous Related Items, sélectionnez **SSL configurations**.
1. Sélectionnez **NodeDeafultSSLSetting**.
1. Dans les listes déroulantes de noms de fichier Trust Store et de fichier de stockage de clés, sélectionnez le fichier Trust Store et le fichier de stockage de clés que vous avez créés.
1. Cliquez sur **Appliquer**.
1. Enregistrez la configuration principale.
1. Redémarrez le profil WebSphere.

   Votre profil s’exécute à présent sur des paramètres SSL personnalisés et votre certificat.

## Activation de la prise en charge des applications AEM Forms natives {#enabling-support-for-aem-forms-natives}

1. Dans la console d’administration WebSphere, sélectionnez **Security > Global Security**.
1. Dans la section Authentication, développez **RMI/IIOP security** et cliquez sur **CSIv2 inbound communications**.
1. Assurez-vous que l’option **SSL-supported** est sélectionnée dans la liste déroulante Transport.
1. Redémarrez le profil WebSphere.

## Configuration de WebSphere pour convertir les URL commençant par https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Pour convertir une URL commençant par https, ajoutez un certificat de signataire correspondant à cette URL sur le serveur WebSphere.

**Création d’un certificat de signataire pour un site https**

1. Vérifiez que WebSphere est en cours d’exécution.
1. Dans WebSphere Administrative Console, naviguez jusqu’à Signer certificates, puis cliquez sur Security > SSL Certificate and Key Management > Key Stores and Certificates > NodeDefaultTrustStore > Signer Certificates.
1. Cliquez sur Retrieve From Port et effectuez les tâches suivantes :

   * Dans le champ Host, saisissez l’URL. Par exemple, saisissez `www.paypal.com`.
   * Dans le champ Port, saisissez `443`. Il s’agit du port SSL par défaut.
   * Dans le champ Alias, saisissez un alias.

1. Cliquez sur Retrieve Signer Information, puis vérifiez que les informations sont récupérées.
1. Cliquez sur Apply, puis sur Save.

Le service Generate PDF peut maintenant effectuer des conversions HTML en PDF à partir du site dont le certificat est ajouté.

>[!NOTE]
>
>Pour qu’une application se connecte à des sites SSL depuis WebSphere, un certificat de signataire est requis. Celui-ci est utilisé par JSSE (Java Secure Socket Extensions) pour valider les certificats envoyés par le site distant lors de l’établissement de la connexion SSL.

## Configuration des ports dynamiques {#configuring-dynamic-ports}

IBM WebSphere n’autorise pas les appels multiples à ORB.init () lorsque la Sécurité Globale est activée. Vous pouvez en savoir plus sur la restriction permanente à l’adresse https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Effectuez les étapes suivantes pour faire en sorte que le port soit dynamique et pour résoudre le problème :

1. Dans la console d’administration WebSphere, sélectionnez **Servers** > **Server Types** > **WebSphere application server**.
1. Dans la section Preferences, sélectionnez votre serveur.
1. Dans l’onglet **Configuration**, sous la section **Communications**, développez **Ports** et cliquez sur **Details**.
1. Cliquez sur les noms de port suivants, définissez le **numéro de port** sur 0 et cliquez sur **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configurer le fichier sling.properties {#configure-the-sling-properties-file}

1. Open `[aem-forms_root]`\crx-repository\launchpad\sling.properties file for editing.
1. Localisez la `sling.bootdelegation.ibm` propriété et ajoutez-la `com.ibm.websphere.ssl.*`au champ de valeur. Le champ mis à jour ressemble à ce qui suit :

   ```java
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Enregistrez le fichier et redémarrez le serveur.

