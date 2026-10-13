---
title: Remarques concernant l’exécution de la console d’administration
description: Ce document répertorie quelques points à prendre en compte lors de l’exécution de la console d’administration.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 100%
---
# Remarques concernant l’exécution de la console d’administration {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Il existe plusieurs éléments à prendre en compte lors de l’exécution de la console d’administration :

* Si vous accédez à la console d’administration en utilisant l’URL `https://[hostname]:'port'/adminui`, le nom d’hôte spécifié ne peut pas contenir de caractères de soulignement. Dans le cas contraire, les liens vers certaines zones de la console d’administration risquent de ne pas fonctionner correctement.
* Si vous exécutez une console d’administration dans l’Explorateur de fichiers sur un système d’exploitation japonais, il se peut que vous rencontriez les problèmes suivants :

  * Un clic sur un lien vous renvoie à la page de connexion au lieu du lien prévu.
  * Un clic sur un lien entraîne l’affichage d’une erreur d’autorisation.

  La bonne pratique consiste à exécuter la console d’administration depuis un autre navigateur, tel que Mozilla Firefox, pour éviter que des liens n’échouent.

* N’utilisez pas de barres obliques inverses (\) lorsque vous exécutez des recherches dans la console d’administration.
