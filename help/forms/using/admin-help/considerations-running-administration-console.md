---
title: Remarques concernant l’exécution d’Administration Console
description: Ce document répertorie quelques points à prendre en compte lors de l’exécution d’Administration Console.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 21%

---

# Remarques concernant l’exécution d’Administration Console {#considerations-when-running-administrationconsole}

Voici quelques éléments à prendre en compte lors de l’exécution d’Administration Console :

* Si vous accédez à la console d’administration en utilisant l’URL `https://[hostname]:'port'/adminui`, le nom d’hôte spécifié ne peut pas contenir de caractères de soulignement. Dans le cas contraire, les liens vers certaines zones d’Administration Console risquent de ne pas fonctionner correctement.
* Si vous exécutez une console d’administration dans Windows Explorer sur un système d’exploitation japonais, vous pouvez rencontrer les problèmes suivants :

   * Cliquer sur un lien vous renvoie à la page de connexion au lieu du lien attendu.
   * Un clic sur un lien affiche une erreur d’autorisation.

  La bonne pratique consiste à exécuter Administration Console à partir d’un autre navigateur, tel que Mozilla Firefox, pour s’assurer qu’aucun lien n’échoue.

* N’utilisez pas de barre oblique inverse () lorsque vous effectuez des recherches dans la console d’administration.
