---
title: Configuration de SSL pour serveur WebLogic
seo-title: Configuration de SSL pour serveur WebLogic
description: Découvrez comment créer des informations d’identification SSL pour le serveur WebLogic et comment configurer SSL pour ce serveur.
seo-description: Découvrez comment créer des informations d’identification SSL pour le serveur WebLogic et comment configurer SSL pour ce serveur.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 74%

---


# Configuration de SSL pour serveur WebLogic {#configuring-ssl-for-weblogic-server}

Pour configurer SSL sur WebLogic Server, vous avez besoin d’informations d’identification SSL à des fins d’authentification. Vous pouvez utiliser l’outil Java keytool pour effectuer les tâches suivantes visant à créer ces informations :

* Créez une paire de clés publique/privée, conservez la clé publique dans un certificat autosigné X.509 v1 enregistré en tant que chaîne de certificats à un seul élément, puis enregistrez la chaîne de certificats et la clé privée dans un nouveau fichier de stockage des clés. Il s’agit du fichier de stockage de clés d’identité personnalisée du serveur d’applications.
* Extrayez le certificat et insérez-le dans un nouveau fichier de stockage des clés. Il s’agit du fichier de stockage de clés d’approbation personnalisée du serveur d’applications.

Configurez ensuite WebLogic pour qu’il utilise les fichiers de stockage des clés d’identité et d’approbation personnalisées que vous avez créés. Désactivez également la fonction de vérification du nom d’hôte de WebLogic car le nom unique utilisé pour créer les fichiers de stockage de clés ne comprend pas le nom de l’ordinateur hébergeant WebLogic.

## Création d’informations d’identification SSL pour WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

La commande keytool se situe généralement dans le répertoire Java jre/bin et doit comprendre plusieurs options et valeurs d’option, répertoriées dans le tableau suivant.

<table>
 <thead>
  <tr>
   <th><p>Option de keytool</p></th>
   <th><p>Description</p></th>
   <th><p>Valeur de l’option</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>Alias du fichier de stockage des clés.</p></td>
   <td>
    <ul>
     <li><p>Fichier de stockage des clés d'identité personnalisée : <code>ads-credentials</code></p></li>
     <li><p>Fichier de stockage des clés d’approbation personnalisée : <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>Algorithme utilisé pour générer la paire de clés.</p></td>
   <td><p>RSA</p><p>Vous pouvez utiliser un autre algorithme selon la stratégie de votre entreprise.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>Emplacement et nom du fichier de stockage de clés.</p><p>Cet emplacement peut contenir le chemin d’accès absolu du fichier. Il peut également s’agir du chemin d’accès relatif du répertoire courant de l’invite de commande dans laquelle la commande keytool a été saisie.</p></td>
   <td>
    <ul>
     <li><p>Fichier de stockage des clés d'identité personnalisée : <code>[</code><i>domaine du serveur d’applications<code>]</code></i><code>/adobe/</code><i>[nom du serveur]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Fichier de stockage des clés d’approbation personnalisée : <code>[</code><i>domaine du serveur d’applications<code>]</code></i><code>/adobe/</code><i>[nom du serveur]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>Emplacement et nom du fichier de certificat.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>Nombre de jours pendant lesquels le certificat est considéré comme valide.</p></td>
   <td><p>3650</p><p>Vous pouvez utiliser une autre valeur, selon la stratégie de votre entreprise.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>Mot de passe protégeant le contenu du fichier de stockage des clés. </p></td>
   <td>
    <ul>
     <li><p>Fichier de stockage des clés d’identité personnalisée : le mot de passe du fichier de stockage des clés doit correspondre au mot de passe des informations d’identification SSL spécifié pour le composant Trust Store d’Administration Console.</p></li>
     <li><p>Fichier de stockage de clés d’approbation personnalisée : appliquez le mot de passe utilisé pour le fichier de stockage des clés d’identité personnalisé.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>Mot de passe protégeant la clé privée de la paire de clés.</p></td>
   <td><p>Utilisez le même mot de passe que celui utilisé pour l'option <code>-storepass</code>. Ce mot de passe de clé doit comprendre au moins 6 caractères.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Nom identifiant le propriétaire du fichier de stockage des clés.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> est l’identification de l’utilisateur propriétaire du fichier de stockage des clés.</p></li>
     <li><p><code><i>[Group Name]</i></code> est l'identification du groupe d'entreprise auquel appartient le propriétaire du fichier de stockage des clés.</p></li>
     <li><p><code><i>[Company Name]</i></code> est le nom de votre organisation.</p></li>
     <li><p><code><i>[City Name]</i></code> est la ville où se trouve votre organisation.</p></li>
     <li><p><code><i>[State or province]</i></code> est l’état ou la province où se trouve votre organisation.</p></li>
     <li><p><code><i>[Country Code]</i></code> est le code à deux lettres du pays où se trouve votre organisation.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Pour plus d’informations sur l’utilisation de la commande keytool, consultez le fichier keytool.html inclus dans la documentation de votre JDK.

## Création de fichiers de stockage des clés d’identité et d’approbation personnalisées  {#create-the-custom-identity-and-trust-keystores}

1. Ouvrez une invite de commande et accédez à *[domaine du serveur d’applications]*/adobe/*[nom du serveur]*.
1. Saisissez la commande suivante :

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Remplacez `[JAVA_HOME]`*par le répertoire dans lequel le JDK est installé et remplacez le texte en italique par les valeurs correspondant à votre environnement.*

   Par exemple :

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   Le fichier de stockage de clés d’identité personnalisée nommé ads-credentials.jks est créé dans le répertoire [domaine du serveur d’applications]/adobe/[nom du serveur].

1. Extrayez le certificat du fichier de stockage des clés ads-credentials en tapant la commande suivante :

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Remplacez `[JAVA_HOME]` par le répertoire dans lequel le JDK est installé et remplacez `store`*_* `password`* par le mot de passe du fichier de stockage des clés d’identité personnalisée.*

   Par exemple :

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   Le fichier de certificat nommé ads-ca.cer est créé dans le répertoire [domaine du serveur d’applications]/adobe/[*nom du serveur*].

1. Copiez le fichier ads-ca.cer sur tous les ordinateurs hôtes devant établir des communications sécurisées avec le serveur d’applications.
1. Insérez le certificat dans un nouveau fichier de stockage des clés (celui des clés d’approbation personnalisée) à l’aide de la commande suivante :

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Remplacez `[JAVA_HOME]` par le répertoire dans lequel le JDK est installé, puis remplacez `store`*_* `password` et `key`*_* `password` *par vos propres mots de passe.*

   Par exemple :

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

Le fichier de stockage de clés d’approbation personnalisée nommé ads-ca.jks est créé dans le répertoire [domaine du serveur d’applications]/adobe/&#39;server&#39;.

Configurez WebLogic pour qu’il utilise les fichiers de stockage des clés d’identité et d’approbation personnalisées que vous avez créés. Désactivez également la fonction de vérification du nom d’hôte de WebLogic car le nom unique utilisé pour créer les fichiers de stockage de clés ne comprend pas le nom de l’ordinateur hébergeant WebLogic Server.

## Configuration de WebLogic pour l’utilisation de SSL  {#configure-weblogic-to-use-ssl}

1. Début de WebLogic Server Administration Console en saisissant `https://`*[nom d’hôte ]*`:7001/console` dans la ligne d’adresse d’un navigateur Web.
1. Sous Environnement, dans Domain Configurations, sélectionnez **Servers > &#39;server&#39; > Configuration > General**.
1. Sous General, dans Configuration, assurez-vous que les options **Listen Port Enabled** et **SSL Listen Port Enabled** sont sélectionnées. Si elles ne sont pas activées, effectuez les opérations suivantes :

   1. Sous Change Center, cliquez sur **Lock &amp; Edit** pour modifier les sélections et leurs valeurs.
   1. Sélectionnez les cases à cocher **Listen Port Enabled** et **SSL Listen Port Enabled**.

1. Si le serveur est un serveur géré, indiquez un numéro de port non utilisé dans les champs Listen Port et SSL Listen Port (par exemple, 8001 et 8002). Sur un serveur autonome, le port SSL par défaut est 7002.
1. Cliquez sur **Release Configuration**.
1. Sous Environnement, dans Domain Configurations, cliquez sur **Servers > [*Managed Server*] > Configuration > General**.
1. Sous General, dans Configuration, sélectionnez **Keystores**.
1. Sous Change Center, cliquez sur **Lock &amp; Edit** pour modifier les sélections et leurs valeurs.
1. Cliquez sur **Change** pour afficher la liste des fichiers de stockage des clés sous forme de liste déroulante et sélectionnez **Custom Identity And Custom Trust**.
1. Sous Identity, spécifiez les valeurs suivantes :

   **Custom Identity Keystore** :  *[domaine]* du serveur d’applications/adobe/nom *[de]* serveur/ads-credentials.jks, où *domaine[ du ] serveur d’applications*est le chemin d’accès réel et le  *[nom de]* serveur est le nom du serveur d’applications.

   **Custom Identity Keystore Type** : JKS

   **Custom Identity Keystore Passphrase** : *mon_mot_de_passe* (mot de passe du fichier de stockage des clés d’identité personnalisée)

1. Sous Trust, spécifiez les valeurs suivantes :

   **Nom** du fichier de stockage de clés d&#39;approbation personnalisée :  `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, où  `*[appserverdomain]*` est le chemin réel

   **Custom Trust Keystore Type** : JKS

   **Custom Trust Keystore Pass Phrase** : *mon_mot_de_passe* (mot de passe de la clé d’approbation personnalisée)

1. Sous General, dans Configuration, sélectionnez **SSL**.
1. Par défaut, Keystore est sélectionné pour Identity et Trust Locations. Si ce n’est pas le cas, remplacez la valeur.
1. Sous Identity, spécifiez les valeurs suivantes :

   **Private Key Alias** : ads-credentials

   **Passphrase** : *mon_mot_de_passe*

1. Cliquez sur **Release Configuration**.

## Désactivation de la fonction de vérification du nom d’hôte  {#disable-the-hostname-verification-feature}

1. Dans l’onglet Configuration, cliquez sur SSL.
1. Sous Advanced, sélectionnez None dans la liste Hostname Verification.

   Si la fonction de vérification du nom d’hôte n’est pas activée, le champ Common Name (CN) doit contenir le nom d’hôte du serveur.

1. Sous Change Center, cliquez sur Lock &amp; Edit pour modifier les sélections et leurs valeurs.
1. Redémarrez le serveur d’applications.

