(use-package doom-themes
      :if window-system
      :ensure t
      :config
      (load-theme 'doom-molokai t)
      (doom-themes-org-config)
      (doom-themes-visual-bell-config)
      (menu-bar-mode -1)
      (tool-bar-mode -1)
      (fringe-mode -1)
      (scroll-bar-mode -1))

(add-to-list 'default-frame-alist
	     '(font . "JetBrains Mono-14"))

(setq inhibit-startup-message t)

(tool-bar-mode -1)
(menu-bar-mode -1)
(scroll-bar-mode -1)

(setq ring-bell-function 'ignore)

(setq locale-coding-system 'utf-8)
(set-terminal-coding-system 'utf-8)
(set-keyboard-coding-system 'utf-8)
(set-selection-coding-system 'utf-8)
(prefer-coding-system 'utf-8)

(setq make-backup-files nil)
(setq auto-save-default nil)

(defalias 'yes-or-no-p 'y-or-n-p)

(use-package async
  :ensure t
  :init (dired-async-mode 1))

(use-package all-the-icons
  :ensure t
  :init)

(use-package all-the-icons-dired
  :ensure t
  :init (add-hook 'dired-mode-hook 'all-the-icons-dired-mode))

(use-package all-the-icons-ibuffer
  :ensure t
  :init (all-the-icons-ibuffer-mode 1))

(use-package async
  :ensure t
  :init (dired-async-mode 1))


(use-package vterm
  :ensure t
  :init
  (global-set-key (kbd "<s-return>") 'vterm))

(use-package dashboard
  :ensure t
  :config
    (dashboard-setup-startup-hook)
    (setq dashboard-startup-banner "~/.emacs.d/img/avatar.png")
    (setq dashboard-items '((recents  . 5)
			    (projects . 5)))
    (setq dashboard-banner-logo-title "I am just a coder for fun"))

(use-package spaceline
  :ensure t
  :config
  (require 'spaceline-config)
  (setq powerline-default-separator (quote arrow))
  (spaceline-spacemacs-theme))

(use-package diminish
  :ensure t
  :init
  (diminish 'which-key-mode)
  (diminish 'linum-relative-mode)
  (diminish 'hungry-delete-mode)
  (diminish 'visual-line-mode)
  (diminish 'subword-mode)
  (diminish 'beacon-mode)
  (diminish 'irony-mode)
  (diminish 'page-break-lines-mode)
  (diminish 'auto-revert-mode)
  (diminish 'rainbow-delimiters-mode)
  (diminish 'rainbow-mode)
  (diminish 'yas-minor-mode)
  (diminish 'flycheck-mode)
  (diminish 'helm-mode))

(setq display-time-default-load-average nil)


(global-subword-mode 1)

(setq electric-pair-pairs '(
			   (?\{ . ?\})
			   (?\( . ?\))
			   (?\[ . ?\])
			   (?\" . ?\")
			   ))
(electric-pair-mode t)



(use-package hungry-delete
  :ensure t
  :config (global-hungry-delete-mode))

(use-package beacon
  :ensure t
  :config
    (beacon-mode 1))

(use-package rainbow-mode
  :ensure t
  :init (add-hook 'prog-mode-hook 'rainbow-mode))

(use-package rainbow-delimiters
  :ensure t
  :init
  (rainbow-delimiters-mode 1))

(use-package expand-region
  :ensure t
  :bind ("C-q" . er/expand-region))

(use-package zzz-to-char
  :ensure t
  :bind ("M-z" . zzz-up-to-char))

(setq kill-ring-max 100)

(use-package popup-kill-ring
  :ensure t
  :bind ("M-y" . popup-kill-ring))

(use-package magit
  :ensure t
  :config
  (setq magit-push-always-verify nil)
  (setq git-commit-summary-max-length 50)
  :bind
  ("M-g" . magit-status))

(use-package sudo-edit
  :ensure t
  :bind ("s-e" . sudo-edit))

(defun kill-curr-buffer ()
  (interactive)
  (kill-buffer (current-buffer)))
(global-set-key (kbd "C-x k") 'kill-curr-buffer)

(defun toggle-maximize-buffer () "Maximize buffer"
       (interactive)
       (if (= 1 (length (window-list)))
           (jump-to-register '_)
         (progn
           (set-register '_ (list (current-window-configuration)))
           (delete-other-windows))))
(global-set-key [(super shift return)] 'toggle-maximize-buffer)



(use-package which-key
  :ensure t
  :init
  (which-key-mode))



(setq ido-enable-flex-matching t)
(setq ido-everywhere t)
(ido-mode 1)

(use-package ido-vertical-mode
  :ensure t
  :init
  (ido-vertical-mode 1))
(setq ido-vertical-define-keys 'C-n-and-C-p-only)

(use-package smex
  :ensure t
  :init (smex-initialize)
  :bind
  ("M-x" . smex))

(global-set-key (kbd "C-x C-b") 'ibuffer)

(setq ibuffer-expert t)

(defun kill-all-buffers ()
  (interactive)
  (mapc 'kill-buffer (buffer-list)))
(global-set-key (kbd "C-M-s-k") 'kill-all-buffers)

(use-package avy
  :ensure t
  :bind
  ("C-." . avy-goto-char))

(use-package switch-window
  :ensure t
  :config
  (setq switch-window-input-style 'minibuffer)
  (setq switch-window-increase 4)
  (setq switch-window-threshold 2)
  (setq switch-window-shortcut-style 'qwerty)
  (setq switch-window-qwerty-shortcuts
	'("a" "s" "d" "f" "h" "j" "k" "l"))
  :bind
  ([remap other-window] . switch-window))

(defun split-and-follow-horizontally ()
  (interactive)
  (split-window-below)
  (balance-windows)
  (other-window 1))
(global-set-key (kbd "C-x 2") 'split-and-follow-horizontally)

(defun split-and-follow-vertically ()
  (interactive)
  (split-window-right)
  (balance-windows)
  (other-window 1))
(global-set-key (kbd "C-x 3") 'split-and-follow-vertically)

(use-package company
  :ensure t
  :config
  (setq company-idle-delay 1)
  (setq company-minimum-prefix-length 3)
  :init
  (company-mode 1))

(with-eval-after-load 'company
  (define-key company-active-map (kbd "M-n") nil)
  (define-key company-active-map (kbd "M-p") nil)
  (define-key company-active-map (kbd "C-n") #'company-select-next)
  (define-key company-active-map (kbd "C-p") #'company-select-previous)
  (define-key company-active-map (kbd "SPC") #'company-abort))

(use-package swiper
  :ensure t
  :bind ("C-s" . swiper))

(setq display-time-24hr-format t)
(setq display-time-format "%H:%M")

(display-time-mode 1)


(use-package fancy-battery
  :ensure t)

(use-package dired-launch
  :ensure t
  :init
  (dired-launch-enable))
