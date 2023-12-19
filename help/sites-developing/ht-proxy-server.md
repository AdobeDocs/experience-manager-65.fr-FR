---
title: Utilisation de l’outil de serveur proxy
description: Le serveur proxy joue le rôle d’un serveur intermédiaire qui relaie les demandes entre un client et un serveur
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 7222a0c3-cdb9-4c73-9d53-26f00792e439
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 96%

---

# Utilisation de l’outil de serveur proxy{#how-to-use-the-proxy-server-tool}

Le serveur proxy joue le rôle d’un serveur intermédiaire qui relaie les demandes entre un client et un serveur. Il effectue le suivi de toutes les interactions client/serveur et crée un journal de l’ensemble de la communication TCP. Vous pouvez ainsi surveiller exactement ce qui se passe, sans avoir à accéder au serveur principal.

Dans votre installation AEM, le serveur proxy figure à cet emplacement :

`crx-quickstart/opt/helpers/proxy-2.1.jar`

Vous pouvez utiliser le serveur proxy pour surveiller toutes les interactions client/serveur, quel que soit le protocole de communication sous-jacent. Par exemple, vous pouvez surveiller les protocoles suivants :

* HTTP pour les pages web
* HTTPS pour les pages web sécurisées
* SMTP pour les e-mails
* LDAP pour la gestion des utilisateurs et utilisatrices

Vous pouvez, par exemple, placer le serveur proxy entre deux applications qui communiquent par un réseau TCP/IP, par exemple, un navigateur web et AEM. Vous pouvez ainsi surveiller exactement ce qui se passe lorsque vous demandez une page CQ.

## Démarrage de l’outil de serveur proxy {#starting-the-proxy-server-tool}

Démarrez le serveur en ligne de commande :

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**Paramètres**

`<host>`

Il s’agit de l’adresse de l’hôte de l’instance CRX à laquelle vous souhaitez vous connecter. Si l’instance se trouve sur votre ordinateur local, il s’agit de `localhost`.

`<remoteport>`

Il s’agit du port de l’hôte de l’instance CRX cible. Par exemple, le port par défaut d’une nouvelle installation AEM est **`4502`**. Le port par défaut d’une instance de création AEM nouvellement installée est `4502`.

`<localport>`

Il s’agit du port de votre ordinateur local auquel vous souhaitez vous connecter pour accéder à l’instance CRX par le biais du proxy.

**Options**

`-q` (mode silencieux)

N’écrit pas la sortie dans la fenêtre de la console. Utilisez cette option si vous ne souhaitez pas ralentir la connexion ou si vous enregistrez la sortie dans un fichier (voir option -logfile).

`-b` (mode binaire)

Si vous recherchez des combinaisons d’octets spécifiques dans le trafic, activez le mode binaire. La sortie contiendra alors la sortie hexadécimale et la sortie de caractères.

`-t` (horodatage des entrées du journal)

Ajoute un horodatage à chaque sortie de journal. L’horodatage est en secondes. Il n’est donc peut-être pas adapté à la recherche de demandes uniques. Utilisez-le pour localiser les événements qui se sont produits à un moment spécifique si vous utilisez le serveur proxy sur une période plus longue.

`-logfile <filename>` (pour écrire dans le fichier journal)

Écrit la conversation client-serveur dans un fichier journal. Ce paramètre fonctionne également en mode silencieux.

**`-i <numIndentions>`** (pour ajouter une mise en retrait)

Chaque connexion active est mise en retrait pour une meilleure lisibilité. La valeur par défaut est de 16 niveaux. Cette fonctionnalité a été ajoutée à `proxy.jar version 1.16`.

### Format du journal {#log-format}

Toutes les entrées du journal générées par proxy-2.1.jar ont le format suivant :

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

Par exemple, une requête pour une page web peut se présenter comme suit :

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C signifie que cette entrée provient du client (il s’agit d’une requête de page web).
* 0 est le numéro de connexion (le compteur de connexions commence à 0)
* #00000 correspond au décalage dans le flux d’octets. Comme il s’agit de la première entrée, le décalage est de 0.
* `[GET <?>]` correspond au contenu de la demande. Dans cet exemple, il s’agit de l’un des en-têtes HTTP (url).

Lorsqu’une connexion se ferme, les informations suivantes sont consignées :

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Elles indiquent le nombre d’octets transférés entre le client (`C`) et le serveur (`S`) au cours de la sixième connexion et à la vitesse moyenne.

**Exemple de sortie du journal**

Prenons l’exemple d’une page qui génère le code suivant si nécessaire :

### Exemple {#example}

Par exemple, prenez un document HTML simple dans le référentiel à l’adresse

`/content/test.html`

Avec un fichier image à l’adresse

`/content/test.jpg`

Le contenu de `test.html` est le suivant :

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

En supposant que l’instance AEM est en cours d’exécution `localhost:4502`, le proxy est démarré comme suit :

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

L’instance CQ/CRX est maintenant accessible via le proxy à `localhost:4444`. Toutes les communications via ce port sont consignées dans `test.log`.

Si vous observez maintenant la sortie du proxy, vous voyez l’interaction entre le navigateur et l’instance AEM.

Au démarrage, le proxy génère les résultats suivants :

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

Nous ouvrons ensuite un navigateur et nous accédons à la page de test :

`http://localhost:4444/content/test.html`

Nous pouvons voir que le navigateur effectue une demande `GET` pour la page :

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

L’instance AEM répond avec le contenu du fichier `test.html` :

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### Utilisations du serveur proxy {#uses-of-the-proxy-server}

Les scénarios ci-dessous indiquent une partie des fins auxquelles le serveur proxy peut être utilisé : 

**Rechercher les cookies et leurs valeurs**

L’exemple d’entrée de journal suivant montre tous les cookies et leurs valeurs envoyés par le client lors de la sixième connexion ouverte depuis le démarrage du proxy :

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**Recherche d’en-têtes et de leurs valeurs**

L’exemple d’entrée de journal suivant montre que le serveur peut établir une connexion persistante et que l’en-tête de longueur du contenu a été correctement défini :

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**Vérification du fonctionnement de la connexion persistante**

Une connexion persistante est une fonctionnalité HTTP qui permet de réutiliser une connexion TCP au serveur pour effectuer plusieurs demandes (pour le code de page, les images, les feuilles de style, etc.). Sans connexion persistante, le client doit établir une nouvelle connexion pour chaque demande.

Pour vérifier si la connexion persistante fonctionne :

* Démarrez le serveur proxy.
* Demandez une page.
* Si la connexion persistante fonctionne, le compteur de connexions ne doit jamais dépasser 5 à 10 connexions.
* Si la connexion persistante ne fonctionne pas, le compteur de connexions augmente rapidement.

**Recherche de requêtes perdues**

Si vous perdez des requêtes dans un paramètre de serveur complexe, par exemple, avec un pare-feu et un Dispatcher, vous pouvez utiliser le serveur proxy pour déterminer où la requête a été perdue. S’il y a un pare-feu :

* Démarrez un proxy avant un pare-feu.
* Démarrez un autre proxy après un pare-feu.
* Utilisez-les pour voir l’étendue des requêtes.

**Requêtes bloquées**

S’il vous arrive de rencontrer des requêtes bloquées :

* Démarrez le proxy.
* Patientez ou écrivez le journal d’accès dans un fichier, chaque entrée ayant une date et une heure spécifiques.
* Lorsque la requête se bloque, vous pouvez voir le nombre de connexions ouvertes et identifier la requête qui pose problème.
