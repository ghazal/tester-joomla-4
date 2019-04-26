# tester-joomla-4
Tester Joomla 4 avec Composer et Node/NPM

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

### pour Windows et Linux

Ce tuto me paraît approprié :

Installing Git on Linux, Mac OS X and Windows
https://gist.github.com/derhuerst/1b15ff4652a867391f03
