## Présentation emacs

"But even if TextMate 2 drops from the sky fully-formed and marveled at by all, Emacs will still be there, waiting. It will be there when the icecaps melt and the cities drown, when humanity destroys itself in fire and zombies, when the roaches finally achieve sentience, take over, and begin using computers themselves - at which point its various Ctrl-Meta key-chords will seem not merely satisfyingly ergonomic for the typical arthropod, but also direct evidence for the universe’s Intelligent Design by some six-legged, multi-jointed God."
- Kieran Healy

### Configuration

#### Buffers

Tout ce qu'il faut pour pouvoir se deplacer dans les buffers avec les fleches (plutot que `C-x o`), et changer de taille.

Les deplacements, avec `Alt` et une fleche :
{{
(global-set-key (kbd "M-<up>") 'windmove-up)
(global-set-key (kbd "M-<down>") 'windmove-down)
(global-set-key (kbd "M-<right>") 'windmove-right)
(global-set-key (kbd "M-<left>") 'windmove-left)
}}

Les changements de taille, avec `Alt + Shift` + une fleche
{{
(global-set-key (kbd "M-S-<up>") 'enlarge-window)
(global-set-key (kbd "M-S-<down>") 'shrink-window)
(global-set-key (kbd "M-S-<right>") 'enlarge-window-horizontally)
(global-set-key (kbd "M-S-<left>") 'shrink-window-horizontally)
}}

Vous connaissez surement deja les raccourcis pour split les windows, `C-x 2` et `C-x 3`.
Mais il est aussi possible de preciser quelle taille doit faire le nouveau buffer.
{{
;; Faire une fenetre de 80 colonnes
M-80 C-x 3
;; Faire une fenetre de 20 lignes
M-20 C-x 2
}}

#### Compilation

Pour compiler dans emacs. Ce qui permet d'avoir un affichage en couleur de la sortie de GCC. Et de cliquer pour se retrouver directement sur la ligne qui pose probleme.
{{
(setq compilation-window-height 10)
(setq compilation-window-width 10)
(global-set-key [f8] `compile)
;;; C-F8 -> aller a la prochaine erreur de compilation
(global-set-key [f7] 'next-error)
}}

#### GDB

Permet de lancer gdb avec plusieurs fenetres (a la facon d'eclipse ou visual studio) et d'y acceder en une touche
{{
(setq-default gdb-many-windows t)
(global-set-key [f9] `gdb)
}}

#### Respecter la norme

Pour ne pas avoir de problème avec les 80 colonnes ou les espaces en fin de ligne :
{{
        ;; Whitespace mode (Eighty Column Rule)
        (require 'whitespace)
        (setq whitespace-style '(face empty tabs lines-tail trailing))
        (global-whitespace-mode t)
}}

#### Petites configuration utiles

Fichiers qui se mettent à jour automatiquement dans emacs (utile avec git/svn…)
{{
;; Auto reload file when there is a change
(global-auto-revert-mode t)
}}

Comportement de `C-w` identique a celui d'un shell
{{
(defun kill-region-or-word ()
  "Call `kill-region' or `backward-kill-word' depending on
whether or not a region is selected."
  (interactive)
  (if (and transient-mark-mode mark-active)
      (kill-region (point) (mark))
    (backward-kill-word 1)))
(global-set-key "\C-w" 'kill-region-or-word)
}}

Utiliser y et n a la place de yes et no
{{
(fset 'yes-or-no-p 'y-or-n-p)
}}

Remplacer la selection (comportement par defaut sur une selection dans toutes les applications)
{{
(delete-selection-mode 1)
}}

Afficher ou cacher ce qu'il y a encore 2 accolades
{{
(global-set-key [f5] 'hs-hide-block)
(global-set-key [f6] 'hs-show-block)
}}

#### Couleurs

Ne pas charger le meme theme si emacs est lance en mode graphique ou en nox
{{
(when window-system
  (load-theme 'solarized-dark))
}}

Il existe un plugin pour changer la couleur d'un unique buffer, pour avoir pour exemple un theme par mode :
[https://github.com/vic/color-theme-buffer-local]()

Changer les couleurs utilisees par `ansi-term` :
{{
(setq ansi-term-color-vector [unspecified "#3f3f3f" "#cc9393" "#7f9f7f" "#f0dfaf" "#8cd0d3" "#dc8cc3" "#93e0e3" "#dcdccc"])
}}

### Plugins

* Auto completion : auto-complete et yasnippet ou [company-mode](http://company-mode.github.io/)
* Speedbar dans la fenetre emacs (affichage de l'arborescence de fichiers) : [sr-speedbar](http://www.emacswiki.org/emacs/sr-speedbar.el)
* Toujours avoir le bon nombre de parentheses, crochets… : autopair
* Affichage à la sublime text : minimap
* Annuler de manière visuelle : undo-tree
* Thèmes : solarized, zenburn, ir-black…

Ils sont tous disponibles avec package.el (de base dans emacs24, peut être installé sur emacs23).

### Exemples

[http://github.com/khady/emacs.d]()
