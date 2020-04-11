---
title: Optimisation des formulaires HTML5
seo-title: Optimisation des formulaires HTML5
description: Vous pouvez optimiser la taille de sortie des formulaires HTML5.
seo-description: Vous pouvez optimiser la taille de sortie des formulaires HTML5.
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Optimisation des formulaires HTML5 {#optimizing-html-forms}

Les formulaires HTML5 génèrent des formulaires au format HTML5. Le résultat peut être volumineux en fonction de facteurs comme la taille du formulaire et les images qu’il contient. Pour optimiser le transfert de données, l’approche recommandée consiste à compresser la réponse HTML à l’aide du serveur Web à partir duquel la requête est traitée. Cette approche permet de réduire la taille de la réponse, le trafic réseau et le temps nécessaire pour transmettre les données entre le serveur et le client.

Cet article décrit les étapes à suivre pour activer la compression sur le serveur Web Apache 2.0 32 bits, avec JBoss.

*Remarque : Les instructions suivantes ne concernent que le serveur Web Apache 2.0 32 bits.*

Procurez-vous le logiciel du serveur Web Apache applicable sur votre système d’exploitation :

* Pour Windows, téléchargez le serveur Web Apache sur le site Apache HTTP Server Project.
* Pour Solaris 64 bits, téléchargez le serveur Web Apache sur le site Sunfreeware pour Solaris.
* Pour Linux, le serveur Web Apache est préinstallé sur le système.

Apache peut communiquer avec JBoss à l’aide du protocole HTTP ou AJP.

1. Ne commentez pas les configurations de module suivantes dans le fichier *APACHE_HOME/conf/httpd.conf*.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Pour Linux, la valeur par défaut d’APACHE_HOME est /etc/httpd/.

1. Configurez le proxy sur le port 8080 de JBoss.

   Ajoutez la configuration suivante au fichier de configuration *APACHE_HOME/conf/httpd.conf*.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Lorsque vous utilisez un proxy, les modifications de configuration suivantes sont requises :
   >
   >* Access: *https://&lt;server>:&lt;port>/system/console/configMgr*
   * Modification de la configuration pour Apache Sling Referrer Filter
   * Dans le champ Allow Hosts (Autoriser les hôtes), ajoutez une entrée pour le serveur proxy


1. Activez la compression.

   Ajoutez la configuration suivante au fichier de configuration *APACHE_HOME/conf/httpd.conf*.

   ```java
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. To access the AEM server, use https://[Apache_server]:80.
