---
title: Utilisation de l’outil de serveur proxy
seo-title: Utilisation de l’outil de serveur proxy
description: Le serveur proxy joue le rôle d’un serveur intermédiaire qui relaie les demandes entre un client et un serveur
seo-description: Le serveur proxy joue le rôle d’un serveur intermédiaire qui relaie les demandes entre un client et un serveur
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 91%

---


# Utilisation de l’outil de serveur proxy{#how-to-use-the-proxy-server-tool}

Le serveur proxy joue le rôle d’un serveur intermédiaire qui relaie les demandes entre un client et un serveur. Il effectue le suivi de toutes les interactions client/serveur et crée un journal de l’ensemble de la communication TCP. Vous pouvez ainsi surveiller ce qui se passe, sans avoir à accéder au serveur principal.

Dans votre installation AEM, le serveur proxy figure à cet emplacement :

`crx-quickstart/opt/helpers/proxy-2.1.jar`

Vous pouvez utiliser le serveur proxy pour surveiller toutes les interactions client-serveur, quel que soit le protocole de communication sous-jacent. Vous pouvez, par exemple, surveiller les protocoles suivants :

* HTTP pour les pages web
* HTTPS pour les pages web sécurisées
* SMTP pour les messages électroniques
* LDAP pour la gestion des utilisateurs

Vous pouvez, par exemple, placer le serveur proxy entre deux applications qui communiquent par un réseau TCP/IP, par exemple, un navigateur web et AEM. Vous pouvez ainsi surveiller ce qui se passe exactement lorsque vous demandez une page CQ.

## Démarrage de l’outil de serveur proxy {#starting-the-proxy-server-tool}

Démarrez le serveur à l’aide d’une ligne de commande :

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

N’écrit pas la sortie dans la fenêtre de la console. Utilisez cette option si vous ne souhaitez pas ralentir la connexion ou si vous voulez consigner la sortie dans un journal (voir l’option -logfile).

`-b`(mode binaire)

Si vous recherchez des combinaisons de bits spécifiques dans le trafic, activez le mode binaire. La sortie contient alors la sortie sous forme hexadécimale et de caractères.

`-t` (horodatage des entrées du journal)

Ajoute un horodatage à chaque sortie du journal. L’horodatage est en secondes. Il n’est donc peut-être pas adapté à la recherche de demandes uniques. Utilisez cette option pour rechercher des événements qui se sont produits à une heure spécifique si vous utilisez le serveur proxy pendant une longue période.

`-logfile <filename>`(écrire dans le fichier journal)

Écrit la communication client-serveur dans un fichier journal. Ce paramètre fonctionne également en mode silencieux.

**`-i <numIndentions>`**(ajouter une mise en retrait)

Chaque connexion active est mise en retrait pour une plus grande lisibilité. La valeur par défaut est de 16 niveaux. This feature was introduced with `proxy.jar version 1.16`.

### Format du journal {#log-format}

Les entrées de journal produites par proxy-2.1.jar ont toutes le format suivant :

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

Une demande de page web peut par exemple ressembler à cette entrée :

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C signifie que cette entrée provient du client (il s’agit d’une demande de page web).
* 0 correspond au nombre de connexions (le nombre de connexions commence à 0).
* # 00000 correspond au décalage dans le flux de bits. Comme il s’agit de la première entrée, le décalage est de 0.
* `[GET <?>]` correspond au contenu de la demande. Dans cet exemple, il s’agit de l’un des en-têtes HTTP (url).

Lorsqu’une connexion se ferme, les informations suivantes sont consignées :

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Elles indiquent le nombre de bits passés entre le client (`C`) et le serveur (`S`) au cours de la 6e connexion et à la vitesse moyenne.

**Exemple de sortie de journal**

À titre d’exemple, prenez une page qui génère le code suivant lors de la demande :

### Exemple {#example}

À titre d’exemple, prenez un document html très simple situé dans le référentiel dans :

`/content/test.html`

avec un fichier image situé dans

`/content/test.jpg`

The content of `test.html` is:

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

Assuming the AEM instance is running on `localhost:4502` we start the proxy like this:

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

The CQ/CRX instance can now be accessed though the proxy at `localhost:4444` and all communication via this port is logged to `test.log`.

La sortie du proxy montre l’interaction entre le navigateur et l’instance AEM.

Au démarrage, le proxy génère la sortie suivante :

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

Nous ouvrons ensuite un navigateur et nous accédons à la page de test :

`http://localhost:4444/content/test.html`

and we see the browser make a `GET` request for the page:

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

Les scénarios suivants montrent à quelles fins le serveur proxy peut être utilisé :

**Recherche de cookies et de leur valeur**

L’entrée de journal suivante montre tous les cookies et leur valeur envoyés par le client à la sixième connexion ouverte depuis le démarrage du proxy :

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**Recherche d’en-têtes et de leur valeur**

L’entrée de journal suivante montre que le serveur est capable d’effectuer une connexion persistante et que l’en-tête de longueur du contenu est configuré correctement :

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
* Si la connexion persistante fonctionne, le nombre de connexions ne doit pas dépasser 5 à 10.
* Si la connexion persistante ne fonctionne pas, le nombre de connexions augmente rapidement.

**Recherche de demandes perdues**

Si vous perdez des demandes dans une configuration de serveur complexe (avec un pare-feu et un répartiteur, par exemple), vous pouvez utiliser le serveur proxy pour déterminer où les demandes ont été perdues. Dans le cas d’un pare-feu :

* Démarrez un proxy avant un pare-feu.
* Démarrez un autre proxy avant un pare-feu.
* Déterminez jusqu’où vont les demandes.

**Demandes en suspens**

Si, de temps en temps, des demandes sont en suspens :

* Démarrez le proxy.
* Patientez ou écrivez le journal des accès dans un fichier en horodatant chaque entrée.
* Lorsque la demande est suspendue, vous pouvez déterminer le nombre de connexions ouvertes et la demande à la source du problème.

