---
title: Test des applications mobiles
seo-title: Test des applications mobiles
description: Test des applications mobiles
seo-description: 'null'
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 2%

---

# Test des applications mobiles{#testing-mobile-apps}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Compte tenu du large éventail d’appareils sur le marché et de périphériques publiés, le test de vos applications est devenu extrêmement important. Il s’agit d’une zone dans laquelle les fonctionnalités et la convivialité peuvent faire l’objet de révisions mineures sur une boutique d’applications, mais où un seul défaut peut entraîner la désinstallation de votre application. Il faut faire attention à vos plans de test et à l’assurance qualité. Le lien suivant couvre de nombreux sujets qui doivent être abordés en général, tels que l’identification de votre environnement, la définition de cas de test, les types de tests, les hypothèses, l’implication du client, etc. Il est également question des outils permettant de contribuer aux efforts de test. Les outils internes, tels que [Hobbes](/help/sites-developing/hobbes.md), peuvent vous aider à tester l’interface utilisateur web. [Tough ](/help/sites-developing/tough-day.md) Daycan peut stresser vos instances avec une charge simulée. Si votre environnement de test possède déjà une expérience avec des outils tiers, tels que Selenium, ils peuvent également être utilisés.

Lors du développement d’une application mobile, il existe de nombreuses nouvelles préoccupations spécifiques aux appareils qui doivent être prises en compte avec celles des tests traditionnels.

* Fonctionnel : toutes les exigences sont-elles respectées par votre application ?
* Fonctionnalité : l’application est-elle facile à utiliser et à comprendre par votre client ?
* Performances : que se passe-t-il lors d’un pic d’utilisation ? Les éléments de l’application, tels que les glissières et les carrousels, sont-ils rapides et ne vous détournent pas de l’expérience ?
* Échec ou interruption - Que se passe-t-il en cas d’appel ou de notification entrant pendant l’exécution de votre application ? Que se passe-t-il en cas de panne de réseau ou de panne de courant ?
* Installation et mises à jour - Comment se passe l’installation ? Comment les mises à jour sont-elles publiées ?
* Technique - Votre application consomme-t-elle trop d’énergie d’un appareil ?
* Localisation : toutes les zones de votre application sont-elles traduites ?
* Certification : votre application a-t-elle été certifiée ? Les clients peuvent-ils se fier à ce qu’il respecte toutes les exigences légales relatives à la confidentialité des données ?

Vous devez répondre à ces questions lors de vos tests automatisés et manuels.

## Tests automatisés {#automated-testing}

Un certain degré de test automatisé doit être effectué pour couvrir la variété des tailles d’écran, des contraintes de mémoire, des méthodes d’entrée et des systèmes d’exploitation. Non seulement il couvre la plupart des cas de test, mais il peut accélérer les tests de régression lorsque de nouvelles fonctionnalités ou de nouveaux appareils sont introduits. Idéalement, vos outils d’automatisation devraient réduire ou limiter la duplication des efforts. Utilisez des outils ou des structures afin que vos efforts de test s’appliquent à toutes les plateformes. Le graphique suivant illustre la structure simplifiée d’un environnement de test pour les tests de l’interface utilisateur web et les tests d’applications mobiles. Le côté gauche du graphique affiche une série de noeuds Selenium avec des navigateurs. SeleniumGrid peut mettre en place des tests d’IU web courants sur n’importe lequel de ces noeuds. Le hub Selenium peut également se connecter à Appium pour les tests d’applications multiplateformes. Seuls les simulateurs sont affichés, mais vous pouvez incorporer adb, pour Android et des utilitaires Xcode pour les appareils iOS. Des liens sont fournis ultérieurement dans ce document, où vous trouverez des détails spécifiques sur les outils mentionnés.

![chlimage_1](assets/chlimage_1.jpeg)

## Test manuel {#manual-testing}

Outre les tests automatisés, votre application doit passer par un cycle de tests manuels. Les clients exécutant l’application sur un appareil réel ne peuvent pas être dupliqués par un script. Ici aussi, vous avez de nombreuses options. Vous pouvez utiliser une plateforme, telle que HockeyApp, pour définir qui a accès et recueillir des commentaires. Vous pouvez également déléguer l’ensemble du processus à un service tel que UTest, ElusiveStars ou Testin. Si vous disposez d’un groupe de testeurs internes, mais que vous ne disposez pas de variantes d’appareils, il existe des services cloud où vous pouvez effectuer des tests manuels sur leur groupe de périphériques. L&#39;un de ces services est SauceLabs. Vous pouvez également créer des applications à distance sur PhoneGap Enterprise et les installer sur des périphériques locaux sous la forme de tests d’acceptation ou de démonstration. Consultez le site Web [PhoneGap](https://phonegap.com/) pour connaître les dernières fonctionnalités et la documentation la plus récente. Quelle que soit l&#39;approche, les tests manuels devraient être effectués;

* atteindre une cible importante de testeurs,
* tester par rapport à un grand groupe d’appareils (idéalement des appareils réels, mais des simulateurs/émulateurs si des appareils réels ne sont pas disponibles),
* fournir des commentaires informatifs :

   * rapports de blocage,
   * analytics/tracking,
   * la convivialité,
   * les domaines d&#39;attention,
   * performance,
   * consommation de données/d’énergie, etc.

## Outils {#tools}

Un large éventail d’outils est disponible pour tester les applications mobiles. Le choix des options à utiliser dépendra de votre situation spécifique : fonctionnalités, prix, assistance, couverture, etc. Vous trouverez ci-dessous une brève description de certains outils et services disponibles.

**Selenium**

* Structure qui comprend une API pour les scripts de test permettant de flux WebDriver et de contrôler différents navigateurs.
* Vous pouvez l’utiliser conjointement avec Appium pour tester des périphériques réels.
* SeleniumGrid redirige les tests entre les noeuds pour les tests parallèles.
* L’IDE Selenium permet de réduire l’écriture de cas de test.

Pour plus d’informations, voir [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Un service de test basé sur le cloud avec des hooks d’intégration continue et des tests d’appareil réels.
* Inclut un outil de filtrage d’applications qui vérifie la compatibilité des appareils, analyse les journaux, traverse les vues, prend des captures d’écran et surveille les performances.

Pour plus d’informations, voir [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium est un framework multi-plateformes populaire pour automatiser les tests mobiles.
* En outre, un inspecteur est inclus avec des fonctionnalités d’enregistrement pour faciliter les cas de test de code.

Pour plus d’informations, voir [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs fournit des tests basés sur le cloud et s’intègre à une intégration continue.
* Les tests s’exécutent automatiquement dans leur environnement cloud ou vous pouvez démarrer un appareil ou une plateforme spécifique et effectuer des tests manuels pour résoudre les problèmes.

Pour plus d’informations, voir [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Un service d&#39;externalisation qui teste vos applications mobiles.
* Comprend un grand nombre d’appareils et offre un large éventail de types de tests : performance, qualité, fonctionnalité, certification, localisation, consommation de données, etc.

Pour plus d’informations, voir [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeyApp**

* HockeyApp tombe sous le test manuel où l&#39;application mobile est envoyée dans une boutique d&#39;applications personnelle où les testeurs peuvent la télécharger et l&#39;essayer.

Pour plus d’informations, voir [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Bien qu’il ne s’agisse pas d’un outil de test, Jenkins constitue un cadre d’intégration continue qui constitue la colonne vertébrale des tests automatisés. De nombreux modules externes tiers sont disponibles pour étendre les fonctionnalités. Par exemple, le module externe SeleniumGrid fournit une interface utilisateur pour aider à gérer le hub et les noeuds Selenium.

Pour plus d’informations, voir [https://jenkins-ci.org/](https://jenkins-ci.org/) et [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
