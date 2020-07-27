---
title: Configuration de SSL pour JBoss Application Server
seo-title: Configuration de SSL pour JBoss Application Server
description: Découvrez comment configurer SSL pour JBoss Application Server.
seo-description: Découvrez comment configurer SSL pour JBoss Application Server.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 52%

---


# Configuration de SSL pour JBoss Application Server {#configuring-ssl-for-jboss-application-server}

Pour configurer SSL sur JBoss Application Server, vous avez besoin d’informations d’identification SSL pour l’authentification. Vous pouvez utiliser l’outil Java keytool pour créer des informations d’identification ou demander des informations d’identification à une autorité de certification (CA) et les importer. Vous devez ensuite activer SSL sur JBoss.

Pour exécuter l’outil keytool, il suffit de saisir une commande qui comprend toutes les informations requises pour créer le fichier de stockage des clés.

Dans cette procédure :

* `[appserver root]` est le répertoire racine du serveur d’applications exécutant AEM forms.
* `[type]` correspond à un nom de dossier qui varie selon le type d’installation réalisé.

## Création d’informations d’identification SSL {#create-an-ssl-credential}

1. In a command prompt, navigate to *[JAVA HOME]*/bin and type the following command to create the credential and keystore:

   `keytool -genkey -dname "CN=`*Nom *d’hôte`, OU=`** Nom `, O=`*de *Société Nom`,L=`** Ville NomÉtat Code du pays&quot; key_passwordnom_stockage`, S=`* *`, C=``-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`**`.keystore`

   >[!NOTE]
   >
   >Replace `[JAVA_HOME]` with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment. nom_hôte correspond au nom de domaine complet du serveur d’applications.

1. Enter the `keystore_password` when prompted for a password. Le mot de passe du fichier de stockage des clés et celui de la clé doivent être identiques.

   >[!NOTE]
   >
   >The `keystore_password` *ntered at this step may be the same password (key_password) that you entered in step 1, or it may be different.*

1. Copy the *keystorename*.keystore to the `[appserver root]/server/[type]/conf` directory by typing one of the following commands:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * Copie (grappe Windows Server) `keystorename.keystore[appserver root]\domain\configuration`
   * (Serveur unique Linux) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Grappe de serveurs Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Exportez le fichier de certificat en exécutant la commande suivante :

   * (Serveur unique) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Grappe de serveurs) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Saisissez le *mot_de_passe_clés* lorsque vous êtes invité à saisir un mot de passe.
1. Copy the AEMForms_cert.cer file to the *[appserver root]\conf *directory by typing the following command:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Grappe Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Serveur unique Linux) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Grappe de serveurs Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Affichez le contenu du certificat en exécutant la commande suivante :

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. To provide write access to the cacerts file in `[JAVA_HOME]\jre\lib\security`, if required, perform the following task:

   * (Windows) Cliquez avec le bouton droit de la souris sur le fichier cacerts et sélectionnez Propriétés, puis l’attribut Lecture seule.
   * (Linux) Type `chmod 777 cacerts`

1. Importez le certificat en saisissant la commande suivante :

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_cert *`.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Type `changeit` as the password. Il s’agit du mot de passe par défaut d’une installation Java, mais l’administrateur système peut l’avoir modifié.
1. Lorsque vous êtes invité à saisir `Trust this certificate? [no]`:, tapez `yes`. La confirmation « Certificate was added to keystore » s’affiche.
1. Si vous vous connectez via SSL à partir de Workbench, vous devez installer le certificat sur le serveur Workbench.
1. Dans un éditeur de texte, ouvrez les fichiers suivants pour les modifier :

   * Single Server - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * Cluster de serveurs - `[appserver root]`/domain/configuration/host.xml

   * Server Cluster - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **Pour un serveur unique,** ajoutez l’élément suivant dans le fichier lc_&lt;dbaname/tunkey>.xml après la section &lt;security-realms> :

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Locate the `<server>` section present after the following code:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Ajoutez ce qui suit à la section &lt;server> située après le code ci-dessus :

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Pour la grappe de serveurs,** dans la racine [du]serveur d’applications \domain\configuration\host.xml sur tous les noeuds, ajoutez ce qui suit après la section &lt;security-realms> :

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   On the primary node of the Server Cluster, in the [appserver root]\domain\configuration\domain_&lt;dbname>.xml, locate the &lt;server> section present after the following code:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Ajoutez ce qui suit à la section &lt;server> située après le code ci-dessus :

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Remplacez la valeur des attributs `keystoreFile` et `keystorePass` par le mot de passe du fichier de stockage des clés que vous avez spécifié lors de la création dudit fichier.
1. Redémarrez le serveur d’applications :

   * Pour les installations clé en main :

      * Dans le Panneau de configuration de Windows, cliquez sur Outils d’administration puis sur Services.
      * Sélectionnez JBoss pour les formulaires Adobe Experience Manager.
      * Sélectionnez Action > Arrêter.
      * Attendez que la mention indiquant l’arrêt du service s’affiche.
      * Sélectionnez Action > Démarrer.
   * Pour les installations de JBoss configurées manuellement ou préconfigurées par Adobe :

      * From a command prompt, navigate to *`[appserver root]`*/bin.
      * Arrêtez le serveur en saisissant la commande suivante :

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * Attendez l’arrêt complet du processus JBoss (il rend la main au terminal dans lequel il a été démarré).
      * Démarrez le serveur en saisissant la commande suivante :

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. Pour accéder à Administration Console à l’aide de SSL, saisissez `https://[host name]:'port'/adminui` dans un navigateur Web :

   Le port SSL par défaut pour JBoss est 8443. A partir de là, spécifiez ce port lors de l’accès à AEM forms.

## Demande d’informations d’identification à une autorité de certification {#request-a-credential-from-a-ca}

1. In a command prompt, navigate to *[JAVA HOME]*/bin and type the following command to create the keystore and the key:

   `keytool -genkey -dname "CN=`*Nom *d’hôte`, OU=`** Nom `, O=`*de *Société Nom`, L=`** Ville NomÉtat Code du pays&quot;--key_passwordnom_stockage_clés`, S=`* *`, C=`**`-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`**`.keystore`

   >[!NOTE]
   >
   >Replace *`[JAVA_HOME]`* with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.

1. Saisissez le commande suivante afin de générer une demande de certificat à envoyer à l’autorité de certification :

   `keytool -certreq -alias` &quot;AEMForms Cert&quot; `-keystore`*nom_stockage *de clés`.keystore -file`*AEMFormscertRequest.csr*

1. Dès que votre demande de certificat est remplie, passez à la procédure suivante.

## Utilisation d’informations d’identification obtenues auprès d’une autorité de certification pour activer SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. In a command prompt, navigate to *`[JAVA HOME]`*/bin and type the following command to import the root certificate of the CA with which the CSR has been signed:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Si le certificat racine ne figure pas dans le navigateur, importez-le également à cet endroit.

   >[!NOTE]
   >
   >Replace *`[JAVA_HOME]`with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.*

1. In a command prompt, navigate to *`[JAVA HOME]`*/bin and type the following command to import the credential into the keystore:

   `keytool -import -trustcacerts -file`*CACertificateName *`.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* Replace `[JAVA_HOME]` with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.
   >* le certificat signé par l’autorité de certification et importé va remplacer un certificat public autosigné s’il existe.


1. Suivez les étapes 13 à 18 de la section Création d’informations d’identification SSL.
