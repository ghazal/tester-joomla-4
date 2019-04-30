# Tester-joomla-4
Tester Joomla 4 avec Composer et Node/NPM

Ce tuto porte essentiellement sur un environnement macOS. 
Je ne peux donner que des pistes pour les autres OS.

Pour tester Joomla 4 avec ses dépendances, on a besoin d'un outil indispensable:
un Terminal.


### Pour macOS

J'utilise iTerm2 pour macOS, une alternative performante au Terminal natif de mac.

[iTerm2 - macOS Terminal Replacement](https://www.iterm2.com/)


### Pour Windows

[PuTTY - a free SSH and telnet client for Windows](https://www.putty.org/)



[Cmder | Console Emulator](https://cmder.net/)



### pour Linux

Pas de conseil à donner aux Linuxiens. Cet outil est dans l'ADN de Linux.

## Paramétrer l'environnement local pour Joomla 4

On aura besoin d'installer Git et Node/NPM via la CLI (Command Line Interface).

### Pour macOS

Après pas mal de tâtonnements, j'ai finalement choisi de passer par [Homebrew](https://www.wikiwand.com/fr/Homebrew_(gestionnaire_de_paquets)) pour mettre en place Git et Node/NPM.

#### Intaller Homebrew

[Le gestionnaire de paquets pour macOS — Homebrew](https://brew.sh/index_fr)


* La commande d'installation de Homebrew à copier coller dans le Terminal:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### Installer Git 
* Commande pour installer Git via Homebrew

```
brew install git
```
#### Installer Node et NPM
Rien de plus simple avec Homebrew.

* Commande pour installer Node et NPM via Homebrew

```
brew install node
```
Pour contrôler que Node et NPM sont correctement installés, il suffit de vérifier leurs versions :
```
node -v
```
```
npm -v
```

Il est à noter que la commande `-g` - pour "globally" - n'apparaît pas dans ces commandes. C'est là tout l'intérêt de Homebrew.

Avant de passer par Homebrew, je trouvais plein de posts où l'on conseillait de faire un [sudo](https://www.wikiwand.com/fr/Sudo) pour récupérer les droits `root` en tant qu'admin système. Pas très recommandé pour macOS.

![sudu boo](sudo-boo.jpg "sudo boo")


#### Astuce

On peut mettre à jour Homebrew, Node et NPM avec une seule commande :

```
brew update && brew upgrade node && npm update -g npm
```

### pour Windows

#### Installer Git

Ce tuto me paraît approprié :

[Installing Git on Linux, Mac OS X and Windows](https://gist.github.com/derhuerst/1b15ff4652a867391f03)

#### Installer Node et NPM

[How to Install Node.js® and NPM on Windows](https://blog.teamtreehouse.com/install-node-js-npm-windows) 


[Install Node.js and NPM on Windows](https://wsvincent.com/install-node-js-npm-windows/) 

### pour Linux	

#### Installer Git
Même tuto que plus haut :

[Installing Git on Linux, Mac OS X and Windows](https://gist.github.com/derhuerst/1b15ff4652a867391f03)


#### Installer Node et NPM
[How to Install Node.js and NPM on Linux](https://blog.teamtreehouse.com/install-node-js-npm-linux) 

## Installer Joomla 4

1 - Créer un dossier - testj4, par exemple - sur le serveur local.

2 - Dans le Terminal, définir le chemin vers le répertoire d'installation sur le serveur, en principe /htdocs/. 

* pour MAMP

		cd /Applications/MAMP/htdocs/testj4

* pour Bitnami

		cd /Applications/mampstack-[versionPHP]/apache2/htdocs/testj4
		
3 - Télécharger Joomla 4 via la command line

	git clone --depth=1 -b 4.0-dev https://github.com/joomla/joomla-cms/

C'est très rapide, et une fois l'opération terminée, on verra apparaître un dossier /joomla-cms/ dans /testj4/.

Pas la peine de déplacer /joomla-cms/, il suffit d'indiquer le bon chemin :

		cd joomla-cms
		
4 - Installer Composer

Il n'est pas nécessaire d'installer Composer `globally`.
Les fichiers `composer.json` et `composer.lock` sont là pour faire le job.

Commande pour installer Composer :

		composer install

Quand on voit `Generating optimized autoload files`, c'est bon.
		
5 - Installer NPM

Commande pour installer NPM :

		npm ci

Il y a plusieurs commandes pour installer NPM dans un répertoire, celle-ci est recommandée par les développeurs de Joomla.

Une définition dans la doc NPM :

[npm-ci | npm Documentation](https://docs.npmjs.com/cli/ci.html)

6 - A cette étape, aller boire un café, discuter avec son voisin, ça peut prendre un moment.

Les fichiers des paquets contenus dans NPM s'installent dans un dossier /node_modules/, puis, à l'aide de ces fichiers, les scripts Joomla installent tous les fichiers sass, css, js dans les bons dossiers.

7 - Quand tout est fini, si tout s'est bien passé, on voit :

`Testing binary`

`Binary is fine`


puis, plus bas :

`added 1010 packages in 300.388s`

... et on est content.

## Dernière étape

A partir de là, on peut installer Joomla 4 classiquement sur le serveur.

## Les commandes internes

Une fois Joomla 4 correctement installé sur le serveur, on peut utiliser les commandes suivantes si on modifie un fichier .scss ou .js :

`npm run watch:css`

ou

`npm run build:js`

Ces commandes vont chercher les modifications et mettre à jour les fichiers concernés.

#### Exemple d'utilisation de `npm run build:css`

* créer un fichier mycustom.scss dans le dossier /scss/ du template
* ouvrir le fichier build/build-modules-js/compilecss.es6.js
* vers la ligne 42, on trouve une liste de fichiers à compiler :

```
files = [
          `${RootPath}/templates/cassiopeia/scss/offline.scss`,
          `${RootPath}/templates/cassiopeia/scss/template.scss`,
          `${RootPath}/templates/cassiopeia/scss/template-rtl.scss`,
            `${RootPath}/templates/cassiopeia/scss/mycustom.scss`,
          `${RootPath}/administrator/templates/atum/scss/bootstrap.scss`,
          `${RootPath}/administrator/templates/atum/scss/fontawesome.scss`,
          `${RootPath}/administrator/templates/atum/scss/template.scss`,
          `${RootPath}/administrator/templates/atum/scss/template-rtl.scss`,
          `${RootPath}/installation/template/scss/template.scss`,
          `${RootPath}/installation/template/scss/template-rtl.scss`,
        ];
```
        
* rajouter l'appel au fichier mycustom.scss ligne 4, comme il est visible  sur cette liste
* après avoir intégré les modifs voulues dans le fichier mycustom.scss, appliquer la commande :

 `npm run build:css`
* deux fichiers nouvellement et automatiquement créés seront alors visibles dans le dossier /css/ du template :

 mycustom.css et mycustom.min.css

Postez dans Issues si vous avez des commentaires.

Post in Issues if you have comments.
