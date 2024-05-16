---
title: Optimiser les formulaires HTML5
description: Vous pouvez optimiser la taille de sortie des formulaires HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: HTML5 Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '285'
ht-degree: 100%

---

# Optimiser les formulaires HTML5 {#optimizing-html-forms}

HTML5 Forms effectue le rendu des formulaires au format HTML5. La sortie générée peut être volumineuse en fonction de facteurs tels que la taille du formulaire et les images qu’il contient. Pour optimiser le transfert des données, l’approche recommandée consiste à compresser la réponse HTML à l’aide du serveur web à partir duquel la demande est traitée. Cette approche réduit la taille de la réponse, le trafic réseau et le temps nécessaire pour diffuser les données entre les ordinateurs serveur et client.

Cet article décrit les étapes requises pour activer la compression sur le serveur web Apache 2.0 32 bits, avec JBoss.

>[!NOTE]
>
>Les instructions suivantes ne concernent que le serveur web Apache 2.0 32 bits.

Procurez-vous le logiciel du serveur web Apache correspondant à votre système d’exploitation :

* Windows : téléchargez le serveur web Apache à partir du site Apache HTTP Server Project.
* Solaris 64 bits : téléchargez le serveur web Apache à partir du site web Sunfreeware for Solaris.
* Linux : le serveur web Apache est préinstallé sur les systèmes Linux.

Apache peut communiquer avec JBoss à l’aide du protocole HTTP ou AJP.

1. Ne commentez pas les configurations de module suivantes dans le fichier *APACHE_HOME/conf/httpd.conf*.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Pour Linux, le répertoire APACHE_HOME par défaut est /etc/httpd/.

1. Configurez le proxy sur le port 8080 de JBoss.

   Ajoutez la configuration suivante au fichier de configuration *APACHE_HOME/conf/httpd.conf*.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Lorsque vous utilisez un proxy, les modifications de configuration suivantes sont requises :
   >
   >* Accès : *https://&lt;server>:&lt;port>/system/console/configMgr*
   * Modifier la configuration pour Apache Sling Referrer Filter
   * Dans le champ Autoriser les hôtes, ajoutez l’entrée pour le serveur proxy.

1. Activez la compression.

   Ajoutez la configuration suivante au fichier de configuration *APACHE_HOME/conf/httpd.conf*.

   ```xml
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

1. Pour accéder au serveur AEM, utilisez https://[Apache_server]:80.
