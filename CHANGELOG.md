Changelog
=========

Unreleased
----------

- Tagged tasks.
  [tomashavlas]

v1.1
----

*Released: 2016-07-01*

- Created cleanup target for tests.
  [tomashavlas]

- Added `bool` filter to boolean variables in conditions.
  [tomashavlas]

- Added `trim` filter when checking for non-empty variables in conditions.
  [tomashavlas]

- Replaced complex conditions with `changed` and `failed` filters in acceptance tests.
  [tomashavlas]

- Added `register` prefix to variables created by Ansible role.
  [tomashavlas]

- Updated minimal Ansible version to `2.0`.
  [tomashavlas]

- Refactored template files to more readable state.
  [tomashavlas]

- Replaced `enabled` option, with `disabled` option to honor pattern used in other roles.
  [tomashavlas]

- Created `sudo__specs_rename_unmanaged` option, allowing to rename all unmanaged drop-in configuration files.
  [tomashavlas]

v1.0
----

*Released: 2016-06-14*

- First public release
  [tomashavlas]
