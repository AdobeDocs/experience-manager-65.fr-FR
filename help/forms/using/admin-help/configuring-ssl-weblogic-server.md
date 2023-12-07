---
title: Configuration de SSL pour WebLogic Server
description: Découvrez comment créer des informations d’identification SSL à utiliser sur le serveur WebLogic et comment configurer SSL pour WebLogic Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 32%

---


# Configuration de SSL pour WebLogic Server {#configuring-ssl-for-weblogic-server}

Pour configurer SSL sur WebLogic Server, vous avez besoin d’informations d’identification SSL pour l’authentification. Vous pouvez utiliser Java keytool pour effectuer les tâches suivantes pour créer des informations d’identification :

* Créez une paire de clés publique/privée, placez la clé publique dans un certificat autosigné X.509 v1 stocké en tant que chaîne de certificats à un seul élément, puis stockez la chaîne de certificats et la clé privée dans un nouveau KeyStore. Il s’agit du fichier de stockage des clés d’identité personnalisée du serveur d’applications.
* Extrayez le certificat et insérez-le dans un nouveau KeyStore. Ce fichier de stockage des clés est le fichier de stockage des clés d’approbation personnalisée du serveur d’applications.

Ensuite, configurez WebLogic pour qu’il utilise les fichiers de stockage des clés d’identité personnalisée et d’approbation personnalisée que vous avez créés. Désactivez également la fonction de vérification du nom d’hôte de WebLogic, car le nom unique utilisé pour créer les fichiers de stockage de clés n’incluait pas le nom de l’ordinateur hébergeant WebLogic.

## Création d’informations d’identification SSL pour WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

La commande keytool se trouve généralement dans le répertoire Java jre/bin et doit inclure plusieurs options et valeurs d’option, qui sont répertoriées dans le tableau suivant.

<table>
 <thead>
  <tr>
   <th><p>Option keytool</p></th>
   <th><p>Description</p></th>
   <th><p>Valeur de l'option</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>L’alias du KeyStore.</p></td>
   <td>
    <ul>
     <li><p>Fichier de stockage de clés d’identité personnalisée : <code>ads-credentials</code></p></li>
     <li><p>Fichier de stockage de clés d’approbation personnalisée :  <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>Algorithme à utiliser pour générer la paire de clés.</p></td>
   <td><p>RSA</p><p>Vous pouvez utiliser un autre algorithme, en fonction de la stratégie de votre société.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>L’emplacement et le nom du fichier de stockage des clés.</p><p>L’emplacement peut inclure le chemin d’accès absolu au fichier. Il peut également s’agir du répertoire actuel de l’invite de commande dans laquelle la commande keytool est saisie.</p></td>
   <td>
    <ul>
     <li><p>Fichier de stockage de clés d’identité personnalisée : <code>[</code><i>domaine du serveur d’applications<code>]</code></i><code>/adobe/</code><i>[server name]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Fichier de stockage de clés d’approbation personnalisée : <code>[</code><i>domaine du serveur d’applications<code>]</code></i><code>/adobe/</code><i>[server name]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>L’emplacement et le nom du fichier de certificat.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>Nombre de jours pendant lesquels le certificat est considéré comme valide.</p></td>
   <td><p>3650</p><p>Vous pouvez utiliser une autre valeur, selon la stratégie de votre société.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>Mot de passe qui protège le contenu du fichier de stockage des clés. </p></td>
   <td>
    <ul>
     <li><p>Fichier de stockage de clés d’identité personnalisée : le mot de passe du fichier de stockage de clés doit correspondre au mot de passe des informations d’identification SSL spécifié pour le composant Trust Store d’Administration Console.</p></li>
     <li><p>Fichier de stockage de clés d’approbation personnalisée : utilisez le même mot de passe que celui utilisé pour le fichier de stockage de clés d’identité personnalisée.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>Mot de passe qui protège la clé privée de la paire de clés.</p></td>
   <td><p>Utilisez le même mot de passe que celui de l’option <code>-storepass</code>. Le mot de passe de la clé doit comporter au moins six caractères.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Nom unique qui identifie la personne propriétaire du KeyStore.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> est l’identification de l’utilisateur propriétaire du fichier de stockage des clés.</p></li>
     <li><p><code><i>[Group Name]</i></code> est l’identification du groupe de l’entreprise auquel le propriétaire du fichier de stockage des clés appartient.</p></li>
     <li><p><code><i>[Company Name]</i></code> est le nom de votre entreprise.</p></li>
     <li><p><code><i>[City Name]</i></code> est la ville où votre entreprise est située.</p></li>
     <li><p><code><i>[State or province]</i></code> est l’État ou la province où se trouve votre entreprise.</p></li>
     <li><p><code><i>[Country Code]</i></code> est le code à deux lettres du pays où se trouve votre entreprise.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Pour plus d’informations sur l’utilisation de la commande keytool, consultez le fichier keytool.html qui fait partie de la documentation de votre JDK.

## Création de fichiers de stockage des clés d’identité et d’approbation personnalisées {#create-the-custom-identity-and-trust-keystores}

1. À partir d’une invite de commande, accédez à *[domaine du serveur d’applications]*/adobe/*[server name]*.
1. Saisissez la commande suivante :

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Remplacez `[JAVA_HOME]`*par le répertoire dans lequel le JDK est installé, puis remplacez le texte en italique par des valeurs correspondant à votre environnement.*

   Par exemple :

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   Le fichier de stockage de clés d’identité personnalisée nommé « ads-credentials.jks » est créé dans le répertoire [domaine du serveur d’applications]/adobe/[server name].

1. Extrayez le certificat du fichier de stockage des clés ads-credentials en tapant la commande suivante :

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**mot de passe**

   >[!NOTE]
   >
   >Remplacez `[JAVA_HOME]` par le répertoire dans lequel le JDK est installé, puis remplacez `store`*_* `password`* par le mot de passe du fichier de stockage des clés d’identité personnalisée.*

   Par exemple :

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   Le fichier de certificat nommé «a ds-ca.cer » est créé dans le répertoire [domaine du serveur d’applications]/adobe/[*server name*].

1. Copiez le fichier ads-ca.cer sur les ordinateurs hôtes qui ont besoin d’une communication sécurisée avec le serveur d’applications.
1. Insérez le certificat dans un nouveau fichier de stockage de clés (le fichier de stockage de clés d’approbation personnalisée) en saisissant la commande suivante :

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Remplacez `[JAVA_HOME]` par le répertoire dans lequel le JDK est installé, puis remplacez `store`*_* `password` et `key`*_* `password` *par vos propres mots de passe.*

   Par exemple :

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

Le fichier de stockage de clés d’approbation personnalisée nommé « ads-ca.jks » est créé dans le répertoire [appserverdomain]/adobe/&#39;server&#39;.

Configurez WebLogic pour qu’il utilise les fichiers de stockage des clés d’identité personnalisée et d’approbation personnalisée que vous avez créés. Désactivez également la fonction de vérification du nom d’hôte de WebLogic, car le nom unique utilisé pour créer les fichiers de stockage de clés n’incluait pas le nom de l’ordinateur hébergeant WebLogic Server.

## Configuration de WebLogic pour l’utilisation de SSL {#configure-weblogic-to-use-ssl}

1. Démarrez la console d’administration de WebLogic Server en saisissant le `https://`*[nom d’hôte ]*`:7001/console` dans la ligne d’adresse d’un navigateur web.
1. Sous Environnement, dans Configurations de domaines, sélectionnez **Serveurs > « serveur » > Configuration > Généralités**.
1. Sous Général, dans Configuration, assurez-vous que la variable **Listen Port Activé** et **Port d’écoute SSL activé** sont sélectionnées. Si cette option n’est pas activée, procédez comme suit :

   1. Sous Change Center, cliquez sur **Lock &amp; Edit** pour modifier les sélections et leurs valeurs.
   1. Vérifiez les **Listen Port Activé** et **Port d’écoute SSL activé** des cases à cocher.

1. Si ce serveur est un serveur géré, remplacez Listen Port par une valeur de port inutilisée (telle que 8001) et SSL Listen Port par une valeur de port inutilisée (telle que 8002). Sur un serveur autonome, le port SSL par défaut est 7002.
1. Cliquez sur **Configuration des versions**.
1. Sous Environnement, dans Configurations des domaines, cliquez sur **Serveurs > [*Serveur géré*] > Configuration > Généralités**.
1. Sous General, dans Configuration, sélectionnez **Keystores**.
1. Sous Change Center, cliquez sur **Lock &amp; Edit** pour modifier les sélections et leurs valeurs.
1. Cliquez sur **Modifier** pour obtenir la liste du stockage de clés sous forme de liste déroulante, puis sélectionnez **Identité Personnalisée Et Confiance Personnalisée**.
1. Sous Identity, spécifiez les valeurs suivantes :

   **Fichier de stockage des clés d’identité personnalisée** : *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks, où *[appserverdomain] * correspond au chemin d’accès réel et *[server name]* au nom du serveur d’applications.

   **Custom Identity Keystore Type**: JKS

   **Custom Identity Keystore Passphrase**: *mypassword* (mot de passe du fichier de stockage des clés d’identité personnalisé)

1. Sous Trust, spécifiez les valeurs suivantes :

   **Nom du fichier de stockage de clés d’approbation personnalisée **: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`où `*[appserverdomain]*` est le chemin d’accès réel

   **Type de fichier de stockage de clés d’approbation personnalisée**: JKS

   **Expression de transmission Trust Keystore personnalisée**: *mypassword* (mot de passe de clé d’approbation personnalisée)

1. Sous Général, dans Configuration, sélectionnez **SSL**.
1. Par défaut, le magasin de clés est sélectionné pour les emplacements d’identité et d’approbation. Si ce n’est pas le cas, remplacez-le par KeyStore.
1. Sous Identity, spécifiez les valeurs suivantes :

   **Alias de clé privée**: ads-credentials

   **Passphrase**: *mypassword*

1. Cliquez sur **Configuration des versions**.

## Désactivation de la fonction de vérification du nom d’hôte {#disable-the-hostname-verification-feature}

1. Dans l’onglet Configuration, cliquez sur SSL.
1. Sous Advanced, sélectionnez None dans la liste Hostname Verification.

   Si la vérification du nom d’hôte n’est pas désactivée, le nom commun (CN) doit contenir le nom d’hôte du serveur.

1. Sous Change Center, cliquez sur Lock &amp; Edit pour modifier les sélections et les valeurs.
1. Redémarrez le serveur d’applications.

