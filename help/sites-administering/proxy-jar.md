---
title: Outil de serveur proxy (proxy.jar)
seo-title: Outil de serveur proxy (proxy.jar)
description: Découvrez l’outil de serveur proxy dans AEM.
seo-description: Découvrez l’outil de serveur proxy dans AEM.
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 97%

---


# Outil de serveur proxy (proxy.jar){#proxy-server-tool-proxy-jar}

Le serveur proxy joue le rôle d’un serveur intermédiaire qui relaie les demandes entre un client et un serveur. Il effectue le suivi de toutes les interactions client/serveur et crée un journal de l’ensemble de la communication TCP. Vous pouvez ainsi surveiller ce qui se passe, sans avoir à accéder au serveur principal.

Le serveur proxy se trouve dans le dossier d’installation approprié :

* &lt;chemin_accès_install_cq>/opt/helpers/proxy.jar
* &lt;chemin_accès_install_crx>/opt/helpers/proxy.jar

Vous pouvez utiliser le serveur proxy pour surveiller toutes les interactions client/serveur, quel que soit le protocole de communication sous-jacent. Vous pouvez, par exemple, surveiller les protocoles suivants :

* HTTP pour les pages web
* HTTPS pour les pages web sécurisées
* SMTP pour les messages électroniques
* LDAP pour la gestion des utilisateurs

Vous pouvez, par exemple, placer le serveur proxy entre deux applications qui communiquent par un réseau TCP/IP, par exemple, un navigateur web et AEM. Vous pouvez ainsi surveiller ce qui se passe exactement lorsque vous demandez une page AEM.

## Démarrage de l’outil de serveur proxy {#starting-the-proxy-server-tool}

L&#39;outil se trouve dans le dossier /opt/helpers de votre installation AEM. Pour le lancer, saisissez :

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### Options {#options}

* **q (mode silencieux)** N’écrit pas les demandes dans la fenêtre de la console. Utilisez cette option si vous ne souhaitez pas ralentir la connexion ou si vous voulez consigner la sortie dans un journal (voir l’option -logfile).
* **b (mode binaire)** Si vous recherchez des combinaisons d’octets spécifiques dans le trafic, activez le mode binaire. La sortie contient alors la sortie sous forme hexadécimale et de caractères.
* **t (entrées du fichier journal horodatage)** Ajoute un horodatage à chaque sortie du journal. L’horodatage est en secondes. Il n’est donc peut-être pas adapté à la recherche de demandes uniques. Utilisez cette option pour rechercher des événements qui se sont produits à une heure spécifique si vous utilisez le serveur proxy pendant une longue période.
* **logfile &lt;nom_fichier> (écriture dans le fichier journal)** Écrit la conversation client/serveur dans un fichier journal. Ce paramètre fonctionne également en mode silencieux.
* **i &lt;retraitsNum> i (ajout d’un retrait)** Chaque connexion active figure en retrait pour une meilleure lisibilité. La valeur par défaut est de 16 niveaux. (Nouveauté de proxy.jar version 1.16).

## Utilisations de l’outil de serveur proxy  {#uses-of-the-proxy-server-tool}

Les scénarios ci-dessous indiquent une partie des fins auxquelles l’outil de serveur proxy peut être utilisé : 

**Recherche de cookies et de leur valeur**

L’exemple d’entrée de journal ci-dessous montre tous les cookies, ainsi que leur valeur, envoyés par le client à la sixième connexion établie depuis le démarrage du serveur proxy :

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**Vérification des en-têtes et de leur valeur** L’exemple d’entrée de journal ci-dessous indique que le serveur peut établir une connexion persistante et que l’en-tête de longueur du contenu est configuré correctement :

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**Vérification du fonctionnement de la connexion persistante**

**Connexion persistante** signifie qu’un client réutilise la connexion au serveur pour transmettre plusieurs fichiers (code de page, images, feuilles de style, etc.). Sans connexion persistante, le client doit établir une nouvelle connexion pour chaque demande.

Pour vérifier si la connexion persistante fonctionne :

1. Démarrez le serveur proxy.
1. Demandez une page.

* Si la connexion persistante fonctionne, le nombre de connexions ne doit pas dépasser 5 à 10.
* Si la connexion persistante ne fonctionne pas, le nombre de connexions augmente rapidement.

**Recherche de demandes perdues**

Si vous perdez des demandes dans une configuration de serveur complexe (avec un pare-feu et un répartiteur, par exemple), vous pouvez utiliser le serveur proxy pour déterminer où les demandes ont été perdues. Dans le cas d’un pare-feu :

1. Démarrez un proxy avant un pare-feu.
1. Démarrez un autre proxy avant un pare-feu.
1. Déterminez jusqu’où vont les demandes.

**Demandes en suspens**

Si de temps en temps, des demandes sont en suspens :

1. Démarrez proxy.jar.
1. Attendez ou écrivez le journal des accès dans un fichier, en horodatant chaque entrée.
1. Lorsque la demande est suspendue, vous pouvez déterminer le nombre de connexions ouvertes et la demande à la source du problème.

## Format des messages du journal  {#the-format-of-log-messages}

Toutes les entrées du journal générées par proxy.jar ont le format suivant :

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

Une demande de page web peut par exemple ressembler à cette entrée :

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C signifie que cette entrée provient du client (il s’agit d’une demande de page web).
* 0 correspond au nombre de connexions (le nombre de connexions commence à 0).
* # 00000 correspond au décalage dans le flux de bits. Comme il s’agit de la première entrée, le décalage est de 0.
* [GET  &lt;?>] est le contenu de la requête, dans l’exemple, l’un des en-têtes HTTP (url).

Lorsqu’une connexion se ferme, les informations suivantes sont consignées :

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Le nombre d’octets transmis entre le client et le serveur sur la 6e connexion est indiqué, ainsi que la vitesse moyenne.

## Exemple de sortie de journal  {#an-example-of-log-output}

Nous allons examiner un modèle simple, qui génère le code ci-dessous lorsqu’il est demandé :

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

Si AEM est exécuté sur localhost:4303, démarrez le serveur proxy comme suit :

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

Vous pouvez accéder au serveur (`localhost:4303`) sans serveur proxy, mais si vous y accédez par le biais de `localhost:4444`, le serveur proxy enregistre la communication. Ouvrez un navigateur et accédez à une page créée avec le modèle ci-dessus. Ensuite, consultez le fichier journal.

>[!NOTE]
>
>Jusqu’à proxy.jar version 1.14, les entrées de journal d’une connexion ne sont pas synchronisées, ce qui signifie que les entrées de journal d’une connexion client/serveur ne sont pas nécessaires dans l’ordre séquentiel approprié. Les versions récentes (>= 1.14) du serveur proxy ne présentent pas ce problème.

Au démarrage, les informations ci-dessous sont écrites dans le journal :

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

Les champs d’en-tête ci-dessous figurent au début de la première connexion (0), qui demande la page HTML principale :

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

Le client demande une connexion persistante afin que le serveur puisse envoyer plusieurs fichiers sur la même connexion :

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

Le serveur proxy est un outil approprié pour vérifier si des cookies sont définis correctement ou non. En l’occurrence, nous découvrons :

* le cookie cq3session généré par AEM
* le cookie de changement du mode d’affichage généré par CFC
* un cookie appelé « JSESSIONID », créé automatiquement par JSP s’il n’est pas désactivé explicitement à l’aide de &lt;%@ page session=&quot;false&quot; %> :

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

Le serveur met fin à la connexion 0 après la demande. La connexion persistance est impossible, car la demande comporte un point d’interrogation. Cela signifie que le serveur ne peut pas renvoyer de version mise en cache et ne peut donc pas déterminer la longueur du contenu à ce moment, ce qui est nécessaire pour une connexion persistante.

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

Ici, le serveur commence à envoyer le code HTML sur la connexion 0 :

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

La connexion 0 se ferme dès que le fichier HTML a été envoyé :

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

À présent, la sortie commence pour la connexion 1, qui télécharge l’image contenue dans le code HTML :

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

Là encore, le client demande une connexion persistante :

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

Pour la connexion 1, le serveur peut fournir une connexion persistante, car l’image est statique et la longueur du contenu est donc connue.

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

Le serveur renvoie la longueur du contenu de l’image sur la connexion 1 :

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

Maintenant que la longueur du contenu est établie, le serveur envoie les données de l’image sur la connexion 1 :

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

Une fois que le délai d’expiration de la connexion persistante est atteint, la connexion 1 se ferme également :

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

L’exemple ci-dessus est simple en comparaison, car les deux connexions sont établies séquentiellement :

* Tout d’abord, le serveur renvoie le code HTML.
* Ensuite, le navigateur demande l’image et établit une nouvelle connexion.

Dans la pratique, une page peut générer de nombreuses demandes d’images, de feuilles de style, de fichiers JavaScript, etc. parallèles. Cela signifie que les fichiers journaux comportent des entrées de connexions établies en parallèle qui se chevauchent. Dans ce cas, il est recommandé d’utiliser l’option -i pour améliorer la lisibilité.
