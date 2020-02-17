---
title: Remarques concernant l’exécution d’Administration Console
seo-title: Remarques concernant l’exécution d’Administration Console
description: Ce document répertorie quelques points à prendre en compte lors de l’exécution d’Administration Console.
seo-description: Ce document répertorie quelques points à prendre en compte lors de l’exécution d’Administration Console.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Remarques concernant l’exécution d’Administration Console {#considerations-when-running-administrationconsole}

Il existe plusieurs éléments à prendre en compte lors de l’exécution d’Administration Console :

* If you access administration console using the URL `https://[hostname]:[port]/adminui`, the specified host name cannot contain underscore characters. Dans le cas contraire, les liens vers certaines zones de Administration Console risquent de ne pas fonctionner correctement.
* Si vous exécutez Administration Console dans Windows Explorer sur un système d’exploitation japonais, il se peut que vous rencontriez les problèmes suivants :

   * Un clic sur un lien vous renvoie à la page d’ouverture de session au lieu du lien prévu.
   * Un clic sur un lien entraîne l’affichage d’une erreur d’autorisation.
   Il est conseillé d’exécuter Administration Console depuis un autre navigateur, tel que Mozilla Firefox, pour éviter que des liens n’échouent.

* N’utilisez pas de barres obliques inverses (\) lorsque vous exécutez des recherches dans Administration Console.

