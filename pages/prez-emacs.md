## Présentation emacs

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

### Plugins

* Auto completion : auto-complete et yasnippet
* Toujours avoir le bon nombre de parentheses, crochets… : autopair
* Affichage à la sublime text : minimap
* Annuler de manière visuelle : undo-tree
* Thèmes : solarized, zenburn, ir-black…

Ils sont tous disponibles avec package.el (de base dans emacs24, peut être installé sur emacs23).

### Exemples

[http://github.com/khady/emacs.d]()
