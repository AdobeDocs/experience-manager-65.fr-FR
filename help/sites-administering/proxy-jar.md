---
title: Outil de serveur proxy (proxy.jar)
seo-title: Proxy Server Tool (proxy.jar)
description: Découvrez l’outil de serveur proxy dans AEM.
seo-description: Learn about the Proxy Server Tool in AEM.
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 32%

---

# Outil de serveur proxy (proxy.jar){#proxy-server-tool-proxy-jar}

Le serveur proxy joue le rôle d’un serveur intermédiaire qui relaie les demandes entre un client et un serveur. Il effectue le suivi de toutes les interactions client/serveur et crée un journal de l’ensemble de la communication TCP. Vous pouvez ainsi contrôler ce qui se passe exactement, sans avoir à accéder au serveur principal.

Le serveur proxy se trouve dans le dossier d’installation approprié :

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

Vous pouvez utiliser le serveur proxy pour surveiller toutes les interactions client/serveur, quel que soit le protocole de communication sous-jacent. Par exemple, vous pouvez surveiller les protocoles suivants :

* HTTP pour les pages web
* HTTPS pour les pages Web sécurisées
* SMTP pour les emails
* LDAP pour la gestion des utilisateurs

Par exemple, vous pouvez positionner le serveur proxy entre deux applications qui communiquent via un réseau TCP/IP ; un navigateur web et une AEM, par exemple. Vous pouvez ainsi surveiller ce qui se passe exactement lorsque vous demandez une page d’AEM.

## Démarrage de l’outil de serveur proxy {#starting-the-proxy-server-tool}

Cet outil se trouve dans le dossier /opt/helpers de votre installation AEM. Pour le lancer, saisissez :

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### Options {#options}

* **q (mode silencieux)** N’écrit pas les demandes dans la fenêtre de la console. Utilisez cette option si vous ne souhaitez pas ralentir la connexion ou si vous enregistrez la sortie dans un fichier (voir option -logfile ).
* **b (mode binaire)** Si vous recherchez des combinaisons d’octets spécifiques dans le trafic, activez le mode binaire. La sortie contiendra alors la sortie hexadécimale et la sortie de caractères.
* **t (entrées du fichier journal horodatage)** Ajoute un horodatage à chaque sortie du journal. L’horodatage est en secondes. Il n’est donc peut-être pas adapté à la recherche de demandes uniques. Utilisez-le pour localiser les événements qui se sont produits à un moment spécifique si vous utilisez le serveur proxy sur une période plus longue.
* **logfile &lt;nom_fichier> (écriture dans le fichier journal)** Écrit la conversation client/serveur dans un fichier journal. Ce paramètre fonctionne également en mode silencieux.
* **i &lt;retraitsNum> i (ajout d’un retrait)** Chaque connexion active figure en retrait pour une meilleure lisibilité. La valeur par défaut est de 16 niveaux. (Nouveau dans proxy.jar version 1.16).

## Utilisation de l’outil de serveur proxy {#uses-of-the-proxy-server-tool}

Les scénarios ci-dessous indiquent une partie des fins auxquelles l’outil de serveur proxy peut être utilisé : 

**Rechercher les cookies et leurs valeurs**

L’exemple d’entrée de journal suivant montre tous les cookies et leurs valeurs envoyés par le client lors de la 6e connexion ouverte depuis le démarrage du proxy :

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**Recherche d’en-têtes et de leur valeur** L’exemple d’entrée de journal suivant montre que le serveur peut établir une connexion persistante et que l’en-tête de longueur du contenu a été correctement défini :

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**Vérification du fonctionnement de la connexion persistante**

**Connexion persistante** signifie qu’un client réutilise la connexion au serveur pour transmettre plusieurs fichiers (code de page, images, feuilles de style, etc.). Sans persistance, le client doit établir une nouvelle connexion pour chaque demande.

Pour vérifier si la persistance fonctionne :

1. Démarrez le serveur proxy.
1. Demandez une page.

* Si la connexion persistante fonctionne, le compteur de connexions ne doit jamais dépasser 5 à 10 connexions.
* Si la connexion persistante ne fonctionne pas, le compteur de connexions augmente rapidement.

**Recherche de requêtes perdues**

Si vous perdez des requêtes dans un paramètre de serveur complexe, par exemple avec un pare-feu et un dispatcher, vous pouvez utiliser le serveur proxy pour déterminer où la requête a été perdue. En cas de pare-feu :

1. Démarrer un proxy avant un pare-feu
1. Démarrer un autre proxy après un pare-feu
1. Utilisez-les pour voir jusqu’où vont les demandes.

**Demandes en suspens**

Si vous rencontrez des requêtes de blocage de temps en temps :

1. Démarrez un fichier proxy.jar.
1. Attendez ou écrivez le journal des accès dans un fichier, chaque entrée ayant un horodatage.
1. Lorsque la requête commence à être suspendue, vous pouvez voir le nombre de connexions ouvertes et la requête qui pose problème.

## Format des messages du journal {#the-format-of-log-messages}

Les entrées de journal générées par proxy.jar ont toutes le format suivant :

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

Par exemple, une requête pour une page Web peut se présenter comme suit :

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C signifie que cette entrée provient du client (il s’agit d’une demande de page Web).
* 0 est le numéro de connexion (le compteur de connexions commence à 0)
* #00000 correspond au décalage dans le flux de bits. Comme il s’agit de la première entrée, le décalage est de 0.
* [GET &lt;?>] correspond au contenu de la demande. Dans cet exemple, il s’agit de l’un des en-têtes HTTP (url).

Lorsqu’une connexion se ferme, les informations suivantes sont consignées :

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Cela indique le nombre d’octets qui se sont écoulés entre le client et le serveur lors de la 6e connexion et à la vitesse moyenne.

## Exemple de sortie de journal {#an-example-of-log-output}

Nous passerons en revue un modèle simple qui génère le code suivant, si nécessaire :

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

Si AEM s’exécute sur localhost:4303, démarrez le serveur proxy comme suit :

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

Vous pouvez accéder au serveur (`localhost:4303`) sans serveur proxy, mais si vous y accédez par le biais de `localhost:4444`, le serveur proxy enregistre la communication. Ouvrez un navigateur et accédez à une page créée avec le modèle ci-dessus. Ensuite, consultez le fichier journal.

>[!NOTE]
>
>Jusqu’à proxy.jar version 1.14, les entrées de journal d’une connexion ne sont pas synchronisées, ce qui signifie que les entrées de journal d’une connexion client/serveur ne sont pas nécessaires dans l’ordre séquentiel approprié. Les versions plus récentes (>=1.14) du serveur proxy ne présentent pas ce problème.

Au démarrage, les informations suivantes sont écrites dans le journal :

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

Les champs d’en-tête suivants sont répertoriés au début de la première connexion (0), qui demande la page de HTML principale :

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

Le client demande une connexion persistante, de sorte que le serveur puisse envoyer plusieurs fichiers sur la même connexion :

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

Le serveur proxy est un outil approprié pour vérifier si des cookies sont définis correctement ou non. Nous voyons ici :

* cookie cq3session généré par AEM
* le cookie de basculement du mode d’affichage généré par le CFC ;
* un cookie nommé JSESSIONID ; il est automatiquement créé par JSP s’il n’est pas explicitement désactivé à l’aide de &lt;%@ page session=&quot;false&quot; %> :

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

Le serveur met fin à la connexion 0 après la demande. La connexion persistance est impossible, car la demande comporte un point d’interrogation. Cela signifie que le serveur ne peut pas renvoyer de version mise en cache et, par conséquent, ne peut pas déterminer la longueur du contenu à ce stade, ce qui est nécessaire pour une connexion persistante.

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

Ici, le serveur commence à envoyer le code HTML sur la connexion 0 :

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

La connexion 0 se ferme immédiatement après la diffusion du fichier de HTML :

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

Désormais, la sortie démarre pour la connexion 1, qui télécharge l’image contenue dans le code de HTML :

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

Encore une fois, le client demande une connexion persistante :

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

Pour la connexion 1, le serveur peut fournir la persistance, car l’image est statique et la longueur du contenu est donc connue.

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

Le serveur renvoie la longueur du contenu de l’image lors de la connexion 1 :

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

Maintenant que la longueur du contenu est établie, le serveur envoie les données image sur la connexion 1 :

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

Une fois le délai de maintien en vie atteint, la connexion 1 se ferme également :

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

L’exemple ci-dessus est relativement simple, car les deux connexions se produisent de manière séquentielle :

* le serveur renvoie d’abord le code de HTML.
* puis le navigateur demande l’image et ouvre une nouvelle connexion.

Dans la pratique, une page peut générer de nombreuses demandes d’images, de feuilles de style, de fichiers JavaScript, etc. parallèles. Cela signifie que les fichiers journaux comportent des entrées de connexions établies en parallèle qui se chevauchent. Dans ce cas, nous vous recommandons d’utiliser l’option -i pour améliorer la lisibilité.
