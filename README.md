# EclipsePluginSummary
A summary of the web ressources and tutorials for Eclipse Plugin Developement. 
Résumé des ressources et tutoriels sur le Web pour le développement de plugins Eclipse.

Je ne traite pas ici des plugins Rich Client Platform (RCP) qui sont, en peu de mots, une version stand-alone d’un plug-in contrairement au plugin que nous allons développer ici qui ne peut être exécuté seul, il faut lui associer obligatoirement une application Eclipse.

===

## Structure d'un plug-in
Deux fichiers manifestes: META-INF/MANIFEST.MF et plug-in.xml et les fichiers java fesant fonctionner le plugin

+ _MANIFEST.MF_ est exploité par le noyau d'Eclipse, Equinox, pour obtenir des informations sur le plug-in (version, liste des classes visibles, ...) qui serviront notamment à gérer le cycle de vie du plug-in et ses relations avec les autres plug-ins.
+ _plugin.xml_ est propre à Eclipse. Il sert à concrétiser les fonctionnalités d'extensibilité d'Eclipse. Via ce fichier, optionnel, des plugins vont déclarer des points d'extension et d'autres se brancher sur ces points d'extension.



## PDE
*Plug-in Development Environment* est un environnement dédié d'Eclipse qui permet de simplifier le développement des plugins. Il se décompose en 3 outils:

+ Un assistant de création de projets plugin, avec notamment des modèles de plugins.
+ Un éditeur pour les fichiers manifestes (plugin.xml).
+ Un workspace test pour le plugin. Les plugins en développement sont automatiquement intégrés dans cette copie pour pouvoir les tester. Il est possible de créer autant de workspace qu'on veut pour tester le plugin sous différentes configurations. (aller dans Run Configuration/Eclipse Application/new Configuration)

*Note: Il devrait déjà être installé sur les dernières versions d'Eclipse. Si ce n'est pas le cas, suivre le Step1 de ce lien* https://medium.com/@invictus42/creating-your-first-eclipse-plugin-9b1b5ba33b58 

## Phase de développement
1. Sous éclipse faire "Nouveau projet" > "Projet de plug-in". Renseigner les champs, indiquer si le plugin va contribuer à l'interface utilisateur.
2. Choisir le template de l'extension la plus adaptée à la création de votre plugin. il est possible d'en choisir plusieurs. 
3. Configuration du fichier plugin.xml
4. Développement du code.
5. Test du plugin. Sur le projet, faire Run as/Eclipse  Application. Un nouveau workspace s'ouvre contenant le plugin. 
il est conseillé sous arguments de mettre la commande -clean pour forcer la relecture de tous les fichiers manifeste à chaque exécution.
6. Exportation du plugin: cliquer droit sur le projet et choisir Exporter... puis choisir "Plug-ins et fragments déployables"
7. Intégration du plugin dans Eclipse. Dézipper l'archive zip dans le répertoire plugins d'Eclipse.
8. Relancer Eclipse


## Fichier Plugin.xml - les onglets
+	**Présentation** 
 	nous indique les informations générales du plugin. "La classe" indique la classe qui lance le plugin. Elle est auto-générée.
+	**Dépendances** 
  	permet de spécifier les packages qui vont être utiles pour développer le plugin : une list de plugins
  	ex. :org.eclipse.ui.actionSets : Permet au plugin de créer des menus.
+	**Runtime ou Exécution** 
	pour inclure des bibliothèques ou obtenir des informations sur les bibliothèques.
+	**Extensions** 
	c'est l'architecture du plugin. Décrit les fonctionnalités qui seront apportées à Eclipse ou à un autre plugin. On peut se servir de dépendance telle que le point d'extension : actionSets. Dans cet exemple, actionSets contient un jeu d'action (actionSet), une action (un bouton) et un menu pour déclencher le plugin.
+	**Points d'extensions** 
	 permet d'offrir des fonctionnalités pour d'autres plugins. Il est nécessaire d'écrire un schéma, avec l'aide de l'éditeur, pour que l'exécution du point d'extension se fasse correctement. le schéma sera utilisé par tous les clients du point d'extension.
	 Eclipse en possède beaucoup pour simplifier nos développements de plugin. Ex.: org.eclipse.ui.actionSets est un point d'extension
+	**Build ou Compilation** 
 	définit les options et la configuration de la compilation en une librairie. On y définit le type, la visibilité et le contenu de la futur librairie.
+	**MANIFEST.MF** 
	pour gérer le cycle de vie du plug-in et ses relations avec les autres plug-ins. Contient les informations sur le plug-in (version, liste des classes visibles, ...)
+	**plugin.xml** 
	la visualisation brute du fichier
+	**build.properties** 
	fichier de configuration pour déployer le plugin. Ecrit sous forme clé = valeur. Précise ce qui est inclus de ce qui ne l'est pas.



## Sources
### Tutoriels 
+ **FR** Une vue rapide du process de développement d'un plugin et du fichier plugin.xml. C'est une bonne première approche pour qui ne veut pas passer trop de temps. 
Les écrans ne sont pas à jour. Un exemple à télécharger : plugin pour insérer un attribut avec ses getters et setters. 
http://www-igm.univ-mlv.fr/~dr/XPOSE2004/vforel/exemple.html
+ **ENG** Très technique, bien qu'assez court, sur le fonctionnement d'un plugin fait à partir de rien(aucune extension). Beaucoup de bon conseils notamment sur le temps de chargement. 
https://www.eclipse.org/articles/Article-PDE-does-plugins/PDE-intro.html
+ **FR** Tutoriel en 2 parties (la seconde est sur RCP) qui détail les relations entre plugin 
http://www.eclipsetotale.com/articles/Developpement_de_plugins_Eclipse_partie1.html 
+ **ENG** Plugin qui lit le nombre de match d'un pattern sur la console. Simple et efficace mais qui ne présente pas vraiment PDE. 
https://medium.com/@invictus42/creating-your-first-eclipse-plugin-9b1b5ba33b58
+ **ENG**  Un autre plugin : remplace une console, utilisée pour entrer des arguments afin d'exécuter une application, par la sélection de mot dans un fichier. 
http://scg.unibe.ch/archive/projects/Bals10b-EclipsePlugins.pdf

### A creuser
+ **ENG** Tutoriel qui semble assez détaillé
http://www.vogella.com/tutorials/EclipsePlugin/article.html


### Autres
+ **ENG** plugin pour faire des cheatSheet : aider les utilisateurs dans l'utilisation d'instructions complexes d'un logiciel.
https://www.eclipse.org/pde/pde-ui/articles/cheat_sheet_dev_workflow/index.html

# A venir
un exemple de plugin...
