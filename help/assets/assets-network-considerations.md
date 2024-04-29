---
title: Remarques et exigences relatives au réseau
description: Décrit les considérations concernant le réseau lors de la conception d’un déploiement d’ [!DNL Adobe Experience Manager Assets] .
contentOwner: AG
role: Architect, Admin
feature: Developer Tools
exl-id: 1313842c-18b1-4727-ba63-b454d0f5a2cc
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1010'
ht-degree: 100%

---

# Remarques relatives au réseau [!DNL Assets] {#assets-network-considerations}

Comprendre votre réseau est aussi important que de comprendre [!DNL Adobe Experience Manager Assets]. Le réseau peut affecter le chargement, le téléchargement et l’expérience client. La représentation schématique de la topologie de votre réseau permet d’identifier les points d’étranglement et les zones sous-optimisées du réseau que vous devez corriger pour améliorer les performances du réseau et l’expérience client.

Assurez-vous d’inclure les éléments suivants dans votre diagramme de réseau :

* Connectivité du périphérique client (par exemple, ordinateur, mobile et tablette) au réseau.
* La topologie du réseau d’entreprise.
* La liaison montante à Internet à partir du réseau d’entreprise et de l’environnement [!DNL Experience Manager].
* La topologie de l’environnement [!DNL Experience Manager].
* La définition des consommateurs simultanés de l’interface réseau [!DNL Experience Manager].
* Les workflows définis du déploiement d’[!DNL Experience Manager].

## Connectivité de l’appareil client au réseau d’entreprise {#connectivity-from-the-client-device-to-the-corporate-network}

Commencez par schématiser la connectivité entre les périphériques clients individuels et le réseau d’entreprise. À ce stade, identifiez les ressources partagées, telles que les connexions WiFi, où plusieurs utilisateurs et utilisatrices accèdent au même point ou commutateur Ethernet pour charger et télécharger des ressources.

![chlimage_1-353](assets/chlimage_1-353.png)

Les appareils client se connectent au réseau d’entreprise de différentes façons, telles que le wi-fi, Ethernet sur un commutateur partagé et le VPN. L’identification et la connaissance des goulots d’étranglement sur ce réseau sont importantes pour la planification d’[!DNL Assets] et pour modifier le réseau.

En haut à gauche du diagramme, trois appareils sont représentés comme partageant un point d’accès WiFi de 48 Mbps. Si tous les appareils chargent simultanément, la bande passante du réseau WiFi est partagée entre les appareils. Par rapport au système dans son ensemble, un utilisateur peut rencontrer un goulot d’étranglement différent pour les trois clients sur ce canal divisé.

Mesurer la vitesse réelle d’un réseau WiFi constitue un défi, car un appareil lent peut avoir un impact sur les autres clients du point d’accès. Si vous envisagez d’utiliser le WiFi pour les interactions avec les ressources, effectuez un test de vitesse sur plusieurs clients simultanément pour évaluer le débit.

Le coin inférieur gauche du diagramme représente deux appareils connectés au réseau d’entreprise via des canaux indépendants. Par conséquent, chaque appareil peut bénéficier d’une vitesse minimale de 10 Mbit/s et 100 Mbit/s.

L’ordinateur affiché à droite dispose d’un accès limité au réseau d’entreprise via un VPN avec une vitesse de 1 Mbit/s. L’expérience client pour la connexion à 1 Mbit/s est très différente de l’expérience client sur la connexion à 1 Gbit/s. En fonction de la taille des ressources avec lesquelles les utilisateurs et utilisatrices interagissent, leur liaison montante VPN peut être inadéquate pour la tâche.

## La topologie du réseau d’entreprise  {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

Le diagramme affiche des vitesses de liaison montante plus élevées au sein du réseau d’entreprise que celles généralement utilisées. Ces canaux sont des ressources partagées. Si le commutateur partagé est censé gérer 50 clients, il peut se transformer en goulot d’étranglement. Dans le diagramme initial, seuls deux ordinateurs partagent la connexion.

## Liaison montante à Internet à partir du réseau d’entreprise et de l’environnement [!DNL Experience Manager] {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

Il est important de prendre en compte les facteurs inconnus sur internet et la connexion VPC, car la bande passante sur internet peut être altérée en raison de pics de charge ou de pannes à grande échelle du fournisseur. En général, la connectivité internet est fiable. Cependant, cela peut parfois introduire des goulots d’étranglement.

Sur la liaison montante d’un réseau d’entreprise vers Internet, d’autres services peuvent utiliser la bande passante. Il est important de connaître la quantité de bande passante pouvant être dédiée ou donnée en priorité à Assets. Par exemple, si un lien de 1 Gbps est déjà utilisé à 80 %, vous ne pouvez allouer qu’un maximum de 20 % de la bande passante à [!DNL Experience Manager Assets].

Les pare-feu et les proxys de l’entreprise peuvent également influencer la bande passante de différentes manières. Ce type d’appareil peut prioriser la bande passante en utilisant la qualité de service, les limitations de bande passante par utilisateur ou utilisatrice ou les limitations de débit binaire par hôte. Il est important d’analyser ces goulots d’étranglement, car ils peuvent avoir un impact significatif sur l’expérience utilisateur d’[!DNL Assets].

Dans cet exemple, l’entreprise dispose d’une liaison de 10 Gbps. Cette taille devrait suffire pour plusieurs clients. De plus, le pare-feu impose une limite de débit hôte de 10 Mbit/s. Cette limitation peut potentiellement limiter le trafic vers un seul hôte à 10 Mbit/s, même si la liaison montante vers internet est à 10 Gbit/s.

Il s’agit du plus petit goulot d’étranglement concernant le client. Cependant, vous pouvez opter pour une modification ou la configuration d’une liste autorisée avec le groupe des opérations réseau responsable de ce pare-feu.

À partir des exemples de diagrammes, vous pouvez conclure que six appareils partagent un canal conceptuel de 10 Mbit/s. Selon la taille des ressources utilisées, cela peut s’avérer insuffisant pour répondre aux attentes des utilisateurs et des utilisatrices.

## Topologie de l’environnement [!DNL Experience Manager] {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

La conception de la topologie de l’environnement [!DNL Experience Manager] nécessite une connaissance détaillée de la configuration du système et de la manière dont le réseau est connecté à l’environnement de l’utilisateur.

L’exemple de scénario comprend une ferme de cinq serveurs, un espace de stockage binaire S3 et Dynamic Media déjà configurés.

Le Dispatcher partage une connexion de 100 Mbit/s avec deux entités, celle du monde externe et le déploiement [!DNL Experience Manager]. Pour les opérations de chargement et de téléchargement simultanées, vous devez diviser ce nombre par deux. Le stockage externe connecté utilise une connexion distincte.

Le déploiement [!DNL Experience Manager] partage sa connexion de 1 Gbit/s avec plusieurs services. Du point de vue de la topologie du réseau, cela équivaut à partager un seul canal avec plusieurs services.

En révisant le réseau de l’appareil client vers le déploiement [!DNL Experience Manager], le plus petit goulot d’étranglement semble se situer au niveau du pare-feu d’entreprise de 10 Mbits. Vous pouvez utiliser ces valeurs dans le calcul de dimensionnement du [Guide du dimensionnement des ressources](assets-sizing-guide.md) pour déterminer l’expérience de l’utilisateur.

## Workflows définis pour le déploiement d’[!DNL Experience Manager] {#defined-workflows-of-the-aem-deployment}

En tenant compte des performances du réseau, il peut être important de prendre en considération les workflows et la publication qui auront lieu dans le système. De plus, le stockage S3 ou tout autre stockage relié au réseau que vous utilisez et les requêtes d’E/S consomment de la bande passante réseau. Par conséquent, même dans un réseau entièrement optimisé, la performance peut être limitée par les E/S du disque.

Pour simplifier les processus d’assimilation des ressources (notamment lors du chargement d’un grand nombre de ressources), vous devez explorer leurs workflows et en savoir plus sur leur configuration.

Lors de l’évaluation de la topologie du workflow interne, vous devez analyser les éléments suivants :

* Procédures d’écriture d’une ressource
* Les workflows/événements qui se déclenchent lorsqu’une ressource ou une métadonnée est modifiée
* Procédures de lecture d’une ressource

Voici quelques éléments à vérifier :

* Lecture/écriture des métadonnées XMP
* Activation et réplication automatiques
* Application d’un filigrane
* Ingestion de sous-ressources/extraction de pages
* Chevauchement des workflows.

Voici un exemple client pour la définition d’un workflow de ressources.

![chlimage_1-357](assets/chlimage_1-357.png)
