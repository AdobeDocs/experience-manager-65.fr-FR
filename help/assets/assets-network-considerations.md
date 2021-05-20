---
title: Remarques et exigences relatives au réseau
description: Discute des considérations relatives au réseau lors de la conception d’un déploiement  [!DNL Adobe Experience Manager Assets] .
contentOwner: AG
role: Architect, Administrator
feature: Outils de développement
exl-id: 1313842c-18b1-4727-ba63-b454d0f5a2cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 72%

---

# [!DNL Assets] considérations relatives au réseau  {#assets-network-considerations}

Comprendre votre réseau est aussi important que de comprendre [!DNL Adobe Experience Manager Assets]. Le réseau peut affecter les chargements, les téléchargements et l’expérience utilisateur. La création d’un diagramme de la topologie du réseau vous permet d’identifier les goulots d’étranglement et les zones sous-optimisées du réseau que vous devez optimiser pour améliorer les performances du réseau et l’expérience de l’utilisateur.

Veillez à inclure les éléments suivants dans votre diagramme de réseau :

* La connectivité du périphérique client (par exemple, l’ordinateur, le mobile ou la tablette) au réseau.
* La topologie du réseau d’entreprise.
* Lien vers Internet à partir du réseau de l’entreprise et de l’environnement [!DNL Experience Manager].
* Topologie de l’environnement [!DNL Experience Manager].
* Définissez les consommateurs simultanés de l’interface réseau [!DNL Experience Manager].
* Workflows définis du déploiement [!DNL Experience Manager].

## Connectivité de l’appareil client au réseau d’entreprise {#connectivity-from-the-client-device-to-the-corporate-network}

Commencez par créer le diagramme de la connectivité entre les différents périphériques client et le réseau d’entreprise. À ce stade, identifiez les ressources partagées, telles que les connexions Wi-Fi, pour lesquelles plusieurs utilisateurs accèdent au même point ou commutateur Ethernet pour transférer et télécharger des ressources.

![chlimage_1-353](assets/chlimage_1-353.png)

Les périphériques client se connectent au réseau d’entreprise de différentes façons, telles que le wi-fi, Ethernet sur un commutateur partagé et le VPN. L’identification et la compréhension des goulots d’étranglement sur ce réseau sont importantes pour la [!DNL Assets] planification et la modification du réseau.

En haut à gauche du diagramme, on peut voir trois périphériques partageant un point d’accès WiFi de 48 Mbps. Si tous les périphériques effectuent un chargement simultané, la bande passante du réseau wi-fi est partagée entre les périphériques. Par rapport au système dans son ensemble, un utilisateur peut rencontrer un goulot d’étranglement différent pour les trois clients sur ce canal divisé.

La mesure de la vitesse réelle d’un réseau Wi-Fi est complexe, car un périphérique lent peut impacter d’autres clients sur le point d’accès. Si vous prévoyez d’utiliser le Wi-Fi pour manipuler les ressources, effectuez un test de vitesse sur plusieurs clients en même temps pour évaluer le débit.

Le coin inférieur gauche du graphique présente deux périphériques connectés au réseau d’entreprise via des canaux indépendants. Par conséquent, chaque périphérique peut atteindre une vitesse comprise entre 10 Mbps et 100 Mbps.

L’ordinateur présenté à droite, connecté au réseau d’entreprise via un VPN, a un débit limité, avec une vitesse de 1 Mbps. L’expérience utilisateur est totalement différente avec une connexion de 1 Mbps et avec une connexion de 1 Gbps. En fonction de la taille des ressources que les utilisateurs manipulent, leur liaison VPN peut s’avérer insuffisante pour la tâche.

## La topologie du réseau d’entreprise  {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

Le diagramme présente des vitesses de liaison plus élevées au sein du réseau d’entreprise que ce qui est généralement utilisé. Ces canaux sont des ressources partagées. Si le commutateur partagé doit gérer 50 clients, il peut s’agir d’un goulot d’étranglement. Dans le diagramme initial, seuls deux ordinateurs partagent la connexion.

## Liaison à Internet à partir du réseau d’entreprise et de l’ [!DNL Experience Manager] environnement {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

Il est important de prendre en compte les facteurs inconnus de la connexion Internet et VPC, car la bande passante sur Internet peut être restreinte par des pics de chargement ou des pannes de fournisseur à grande échelle. En général, une connexion Internet est fiable. Toutefois, cela peut parfois entraîner la création de goulots d’étranglement.

Au niveau de la liaison du réseau d’entreprise à Internet, il peut exister d’autres services utilisant la bande passante. Il est important de connaître la quantité de bande passante pouvant être dédiée ou donnée en priorité à Assets. Par exemple, si un lien de 1 Gbit/s est déjà utilisé à 80 %, vous ne pouvez allouer qu’un maximum de 20 % de la bande passante pour [!DNL Experience Manager Assets].

Les pare-feu et les proxys de l’entreprise peuvent également influencer la bande passante de différentes manières. Ce type de périphérique peut prioriser la qualité du service de la bande passante, définir la bande passante maximale par utilisateur ou les limites de débit par hôte. Il s’agit de goulets d’étranglement importants à examiner, car ils peuvent avoir un impact significatif sur l’expérience utilisateur [!DNL Assets].

Dans cet exemple, l’entreprise dispose d’une liaison de 10 Gbps. Cela doit être suffisant pour prendre en charge plusieurs clients. Par ailleurs, le pare-feu impose une limite de débit par hôte de 10 Mbps. Cette restriction risque de ralentir le trafic d’un seul hôte à 10 Mbps, même si la liaison montante à l’Internet est de 10 Gbps.

Il s’agit du plus petit point d’étranglement orienté client. Cependant, vous pouvez évaluer une modification ou configurer une liste autorisée avec le groupe d’opérations réseau responsable de ce pare-feu.

Les exemples de diagrammes vous permettent de conclure que six périphériques partagent un canal conceptuel de 10 Mbps. Selon la taille des ressources exploitées, cela peut s’avérer insuffisant pour répondre aux attentes de l’utilisateur.

## Topologie de l&#39;environnement [!DNL Experience Manager] {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

La conception de la topologie de l’environnement [!DNL Experience Manager] nécessite une connaissance détaillée de la configuration du système et de la manière dont le réseau est connecté dans l’environnement de l’utilisateur.

L’exemple de scénario comprend une ferme de publication avec cinq serveurs, un magasin de binaires S3 et Dynamic Media configuré.

Dispatcher partage une connexion de 100 Mbit/s avec deux entités, le monde extérieur et le déploiement de [!DNL Experience Manager]. Pour les opérations simultanées de chargement et de téléchargement, vous devez diviser ce nombre par deux. L’espace de stockage externe joint utilise une connexion distincte.

Le déploiement [!DNL Experience Manager] partage sa connexion de 1 Gbit/s avec plusieurs services. Du point de vue de la topologie du réseau, cela équivaut à partager un seul canal avec plusieurs services.

En examinant le réseau de l’appareil client vers le déploiement [!DNL Experience Manager], le plus petit point d’étranglement semble être la limitation de pare-feu d’entreprise de 10 Mbit. Vous pouvez utiliser ces valeurs dans le calcul de dimensionnement du [Guide du dimensionnement des ressources](assets-sizing-guide.md) pour déterminer l’expérience de l’utilisateur.

## Workflows définis du déploiement [!DNL Experience Manager] {#defined-workflows-of-the-aem-deployment}

En tenant compte des performances du réseau, il peut être important de prendre en considération les workflows et la publication qui auront lieu dans le système. De plus, S3 ou tout autre stockage en réseau que vous utilisez, ainsi que les requêtes E/S consomment de la bande passante du réseau. Par conséquent, même dans un réseau entièrement optimisé, la performance peut être limitée par les E/S du disque.

Pour simplifier les processus d’assimilation des ressources (notamment lors du chargement d’un grand nombre de ressources), vous devez explorer leurs workflows et en savoir plus sur leur configuration.

Lors de l’évaluation de la topologie interne du workflow, vous devez analyser ce qui suit :

* Les procédures d’écriture d’une ressource
* Les workflows/événements qui se déclenchent lorsqu’une ressource ou une métadonnée est modifiée
* Procédures de lecture d’une ressource

Voici quelques éléments à vérifier :

* XMP des métadonnées en lecture/écriture différée
* Activation et réplication automatiques
* Application d’un filigrane  
* Assimilation de sous-ressources/Extraction de pages
* Chevauchement des workflows.

Voici un exemple de client pour la définition d’un workflow de ressource.

![chlimage_1-357](assets/chlimage_1-357.png)
