---
title: Développement de projets AEM à l’aide d’Eclipse
description: Ce guide décrit l’utilisation d’Eclipse pour le développement de projets basés sur AEM
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 56%

---

# Développement de projets AEM à l’aide d’Eclipse{#how-to-develop-aem-projects-using-eclipse}

Ce guide explique comment utiliser Eclipse pour développer des projets basés sur AEM.

>[!NOTE]
>
>Adobe fournit désormais les [outils de développement AEM pour Eclipse](/help/sites-developing/aem-eclipse.md) qui vous aident à développer des solutions AEM avec Eclipse.

## Présentation {#overview}

Pour commencer AEM développement sur Eclipse, les étapes suivantes sont nécessaires.

Chacune d’elles est expliquée plus en détail dans le reste de cette rubrique pratique.

* Installer Eclipse 4.3 (Kepler)
* Configurer votre projet AEM basé sur Maven
* Préparation de la prise en charge JSP d’Eclipse dans le fichier POM Maven
* Importation du projet Maven dans Eclipse

>[!NOTE]
>
>Ce guide est basé sur Eclipse 4.3 (Kepler) et AEM 5.6.1.

## Installer Eclipse {#install-eclipse}

Téléchargez l’« IDE Eclipse pour le développement Java EE » depuis la [page des téléchargements d’Eclipse](https://www.eclipse.org/downloads/).

Installez Eclipse en suivant la procédure [Instructions d’installation](https://wiki.eclipse.org/Eclipse/Installation).

## Configurer votre projet AEM basé sur Maven {#set-up-your-aem-project-based-on-maven}

Ensuite, configurez le projet en utilisant Maven comme décrit dans la rubrique [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Préparation de la prise en charge JSP pour Eclipse {#prepare-jsp-support-for-eclipse}

Eclipse peut également fournir une assistance lors de l’utilisation de JSP, par exemple :

* le remplissage automatique des bibliothèques de balises ;
* Connaissance Eclipse des objets définis par &lt;cq:defineobjects /> et &lt;sling:defineobjects />

Pour que cela fonctionne :

1. Suivez les instructions de la section [Comment travailler avec des JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) de la rubrique [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Ajoutez ce qui suit au &lt;build /> dans le POM de votre module de contenu.

   Le module externe de prise en charge Maven d’Eclipse, m2e, ne fournit pas de prise en charge pour le module externe maven-jspc-plugin, et cette configuration indique à m2e d’ignorer le module externe et la tâche connexe de nettoyer les résultats de la compilation temporaire.

   Ce n’est pas un problème : comme indiqué dans la section [Comment travailler avec des JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), le plugin maven-jspc-plugin de cette configuration n’est utilisé que pour valider la compilation des JSP dans le cadre du processus de création. Eclipse signale déjà les problèmes rencontrés dans les JSP et ne se repose pas sur ce plugin Maven pour le faire.

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Importation du projet Maven dans Eclipse {#import-the-maven-project-into-eclipse}

1. Dans Eclipse, sélectionnez File (Ficher) > Import (Importer)...
1. Dans la boîte de dialogue d’importation, sélectionnez Maven > Existing Maven Projects (Projets Maven existants), puis cliquez sur Next (Suivant).

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Saisissez le chemin d’accès au dossier de niveau supérieur du projet et cliquez sur « Tout sélectionner » et « Terminer ».

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Vous êtes à présent prêt à utiliser Eclipse pour développer le projet AEM, notamment la saisie semi-automatique.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Si vous incluez `/libs/foundation/global.jsp` ou d’autres JSP dans `/libs`, vous devez le copier dans votre projet afin qu’Eclipse puisse résoudre l’inclusion. En même temps, vous devez vous assurer qu’ils ne sont pas inclus dans le package de contenu Maven. La rubrique [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md) décrit comment réaliser cette opération.
