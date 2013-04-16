## Présentation emacs

### Configuration

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

### Plugins

* Auto completion : auto-complete et yasnippet
* Toujours avoir le bon nombre de parentheses, crochets… : autopair
* Affichage à la sublime text : minimap
* Annuler de manière visuelle : undo-tree
* Thèmes : solarized, zenburn, ir-black…

Ils sont tous disponibles avec package.el (de base dans emacs24, peut être installé sur emacs23).

### Exemples

[http://github.com/khady/emacs.d]()
