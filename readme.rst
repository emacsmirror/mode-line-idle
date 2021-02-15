##############
Mode Line Idle
##############

Simple delayed text evaluation for the mode-line.

This package provides a convenient way to defer text evaluation in a way that can be
easily integrated into existing mode-line's without requiring a minor mode or configuration.

Available via `melpa <https://melpa.org/#/mode-line-idle>`__.


Motivation
==========

To be able to add useful information into the mode-line without slowing down Emacs performance.

While delaying updates is not so difficult,
having multiple timers can become awkward when mixed in with the mode-lines configuration.

Instead of avoiding expensive information in the mode-line, it can be calculated when idle.


Usage
=====

To use ``mode-line-idle`` you will need to set ``mode-line-format`` using ``eval`` (examples below).

The function signature is:

``(mode-line-idle delay content default-text &rest keywords)``

:delay:
   The number of seconds to delay evaluation once Emacs is idle.
:content:
   The text to evaluate which can be a tree that gets converted into a string,
   this takes on a similar for to ``mode-line-format`` (more on this below).
:default-text:
   The text to show before the value has been computed.


Optional Keyword Arguments
--------------------------

``:interrupt``
   When non-nil, evaluating the string will be interrupted on key input.

   This is intended for long running operations,
   to prevent them locking Emacs if the user begins typing while the operation is running.

   Interruption uses the same behavior as ``quit``,
   see ``with-no-input`` documentation for details.


Examples
--------

Simple example showing a delayed evaluated block in the mode line.

.. code-block:: elisp

   (defvar my-date '(:eval (current-time-string)))
   (setq-default mode-line-format
     (list "Example " '(:eval (mode-line-idle 1.0 my-date "?"))))

The block to evaluate can be included inline as well.

.. code-block:: elisp

   (setq-default mode-line-format
     (list "Example " '(:eval (mode-line-idle 1.0 (:eval '(current-time-string)) "?"))))

As with ``mode-line-format``, ``propertize`` is supported.

.. code-block:: elisp

   (defvar my-date '(:propertize (:eval (current-time-string)) face warning))
   (setq-default mode-line-format
     (list "Example " '(:eval (mode-line-idle 1.0 my-date "?"))))


Two timers, with different faces.

.. code-block:: elisp

   (defvar my-date '(:eval (current-time-string)))
   (defvar my-word '(:eval (count-words (point-min) (point-max))))
   (setq-default mode-line-format
     (list "Example " '(:eval (list
                                "Date: "
                                (mode-line-idle 1.0 my-date "...")
                                " Word Count: "
                                (mode-line-idle 3.0 my-word "?" :interrupt t)))))


Installation
============

This package can be installed from melpa.

.. code-block:: elisp

   (use-package mode-line-idle
     :commands (mode-line-idle))
