---
title: Personnaliser la console de bienvenue (IU classique)
description: La console Bienvenue fournit une liste de liens vers les différentes consoles et fonctionnalités d’AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 48%

---

# Personnaliser la console de bienvenue (IU classique){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>Cette page traite de l’IU classique.
>
>Voir [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md) pour plus d’informations sur l’IU tactile standard.

La console de bienvenue fournit une liste de liens vers les différentes consoles et fonctionnalités d’AEM.

![cq_welcomescreen](assets/cq_welcomescreen.png)

Il est possible de configurer les liens visibles. Cela peut être défini pour des utilisateurs et/ou des groupes spécifiques. Les actions à entreprendre dépendent du type de cible (qui correspond à la section de la console dans laquelle ils se trouvent) :

* [Consoles principales](#links-in-main-console-left-pane) - Liens dans la console principale (volet de gauche)
* [Ressources, documentation et référence, fonctionnalités](#links-in-sidebar-right-pane) - Liens dans la barre latérale (volet de droite)

## Liens dans la console principale (volet de gauche) {#links-in-main-console-left-pane}

Cette section répertorie les principales consoles d’AEM.

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### Configuration de la visibilité des liens de la console principale {#configuring-whether-main-console-links-are-visible}

Les autorisations de niveau noeud déterminent si le lien peut être affiché ou non. Les nœuds en question sont les suivants :

* **Sites web :** `/libs/wcm/core/content/siteadmin`

* **Ressources numériques :** `/libs/wcm/core/content/damadmin`

* **Communauté :** `/libs/collab/core/content/admin`

* **Campagnes :** `/libs/mcm/content/admin`

* **Boîte de réception :** `/libs/cq/workflow/content/inbox`

* **Utilisateurs :** `/libs/cq/security/content/admin`

* **Outils :** `/libs/wcm/core/content/misc`

* **Balisage :** `/libs/cq/tagging/content/tagadmin`

Par exemple :

* Pour limiter l’accès à **Outils**, supprimez l’accès en lecture à partir de

  `/libs/wcm/core/content/misc`

Voir [Section de sécurité](/help/sites-administering/security.md) pour plus d’informations sur la définition des autorisations souhaitées.

### Liens dans la barre latérale (volet de droite) {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

Ces liens sont basés sur l’existence de nœuds à l’emplacement suivant *et* sur l’accès en lecture à ces mêmes nœuds :

`/libs/cq/core/content/welcome`

Trois sections sont proposées par défaut (elles sont légèrement espacées) :

<table>
 <tbody>
  <tr>
   <td><strong>Ressources</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Services cloud</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> Workflows</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> Gestion des tâches</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> Réplication</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> Rapports</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> Publications</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> Manuscrits</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>Documentation et référence</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Documentation</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> Références pour les développeurs</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>Fonctions</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> Packages</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> Partage de packages</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> Mise en cluster</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> Sauvegarde</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Console Web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Image mémoire du statut de la console Web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### Configuration de la visibilité des liens de la barre latérale {#configuring-whether-sidebar-links-are-visible}

Il est possible de masquer un lien d’utilisateurs ou de groupes spécifiques en supprimant l’accès en lecture aux noeuds qui représentent le lien.

* Ressources : supprimez l’accès à :

  `/libs/cq/core/content/welcome/resources/<link-target>`

* Documents : supprimez l’accès à :

  `/libs/cq/core/content/welcome/docs/<link-target>`

* Fonctionnalités : supprimez l’accès à :

  `/libs/cq/core/content/welcome/features/<link-target>`

Par exemple :

* Pour supprimer le lien vers **Rapports**, supprimez l’accès en lecture à partir de

  `/libs/cq/core/content/welcome/resources/reports`

* Pour supprimer le lien vers **Packages**, supprimez l’accès en lecture à partir de

  `/libs/cq/core/content/welcome/features/packages`

Voir [Section de sécurité](/help/sites-administering/security.md) pour plus d’informations sur la définition des autorisations souhaitées.

### Mécanisme de sélection de liens {#link-selection-mechanism}

L’outil `/libs/cq/core/components/welcome/welcome.jsp`ConsoleUtil[ est utilisé dans ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html). Il exécute une requête sur les nœuds qui possèdent la propriété :

* `jcr:mixinTypes` avec la valeur : `cq:Console`

>[!NOTE]
>
>Exécutez la requête suivante pour afficher la liste existante :
>
>* `select * from cq:Console`
>

Si un utilisateur ou un groupe ne possède pas l’autorisation de lecture sur un nœud avec le mixin `cq:Console`, ce nœud est récupéré par le biais d’une recherche `ConsoleUtil`. Par conséquent, il n’est pas répertorié dans la console.

### Ajout d’un élément personnalisé {#adding-a-custom-item}

La variable [mécanisme de sélection de lien](#link-selection-mechanism) peut être utilisé pour ajouter votre propre élément personnalisé à la liste des liens.

Ajoutez votre élément personnalisé à la liste en ajoutant le mixin `cq:Console` à votre widget ou ressource. Pour ce faire, vous devez définir la propriété suivante :

* `jcr:mixinTypes` avec la valeur : `cq:Console`
