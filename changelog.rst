##########
Change Log
##########

- In development

  - Fix bug #4: support using an integer as the first element of a cons-cell to pad or truncate the following string
    (as documented by ``mode-line-format``).

- Version 0.3 (2024-04-20)

  - Fix error in ``assq-delete-all`` use.
  - Add ``mode-line-idle-force-update`` function to calculate pending idle timers.

- Version 0.2 (2022-07-10)

  Fix bug #2, where strings had any existing properties cleared.
  Add ``:interrupt`` keyword argument to support interrupting evaluation on input.
  Add ``:literal`` to prevent the ``%`` character being interpreted by ``mode-line-format``.

- Version 0.1 (2021-02-14)

  Initial release.
