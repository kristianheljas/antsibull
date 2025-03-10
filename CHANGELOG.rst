================================================
antsibull -- Ansible Build Scripts Release Notes
================================================

.. contents:: Topics


v0.53.0
=======

Release Summary
---------------

Feature and bugfix release.

Minor Changes
-------------

- Add ``--tags-file`` option to the ``single``, ``rebuild-single``, and ``prepare`` subcommands. This allows including a collection git tags data file in ansible-build-data and the ansible sdist (https://github.com/ansible-community/antsibull/pull/476/).
- Add ``pyproject.toml`` to ansible sdist to use the ``setuptools.build_meta`` `PEP 517 <https://peps.python.org/pep-0517/>`__ backend. Tools that still call ``setup.py`` directly will work the same as they did before (https://github.com/ansible-community/antsibull/pull/471).
- Bump minimum ``antsibull-core`` requirement to 1.5.0. It contains changes that are needed for the new ``--tags-file`` option (https://github.com/ansible-community/antsibull/pull/476/).
- There have been internal refactorings to simplify typing (https://github.com/ansible-community/antsibull/pull/469).

Bugfixes
--------

- Correct Python version classifiers in the ansible ``setup.py`` template. Limit the Python 3.8 classifer to ansible 5 and 6 and add the Python 3.11 classifier to ansible >= 7 (https://github.com/ansible-community/antsibull/pull/479).
- Do not crash when the ``changelogs/changelog.yaml`` file of a collection cannot be loaded (https://github.com/ansible-community/antsibull/issues/481, https://github.com/ansible-community/antsibull/pull/482).

v0.52.0
=======

Release Summary
---------------

Major feature and bugfix release with breaking changes.

Minor Changes
-------------

- Add a ``validate-tags`` subcommand to ensure that collection versions in an Ansible release are tagged in collections' respective git repositories (https://github.com/ansible-community/antsibull/pull/456).
- Make compatible with antsibull-core 2.x.y (https://github.com/ansible-community/antsibull/pull/463).

Breaking Changes / Porting Guide
--------------------------------

- Drops support for Python 3.6 an 3.7 (https://github.com/ansible-community/antsibull/issues/458, https://github.com/ansible-community/antsibull/pull/460).
- The antsibull-docs dependency has been removed (https://github.com/ansible-community/antsibull/pull/451).

Removed Features (previously deprecated)
----------------------------------------

- The deprecated ``antsibull-lint`` subcommands have been removed. Use ``antsibull-changelog lint-changelog-yaml`` or ``antsibull-docs lint-collection-docs`` depending on your use-case (https://github.com/ansible-community/antsibull/pull/451).
- The deprecated ``build-collection`` subcommand of ``antsibull-build`` has been removed. Use ``collection`` instead (https://github.com/ansible-community/antsibull/pull/451).
- The deprecated ``build-multiple`` subcommand of ``antsibull-build`` has been removed. Use ``multiple`` instead (https://github.com/ansible-community/antsibull/pull/451).
- The deprecated ``build-single`` subcommand of ``antsibull-build`` has been removed. Use ``single`` instead (https://github.com/ansible-community/antsibull/pull/451).
- The deprecated ``new-acd`` subcommand of ``antsibull-build`` has been removed. Use ``new-ansible`` instead (https://github.com/ansible-community/antsibull/pull/451).

v0.51.2
=======

Release Summary
---------------

Bugfix release. The next minor release will no longer support Python 3.6 and 3.7.

Bugfixes
--------

- Add ``--collection-dir`` to the ``antsibull-build`` ``collection`` and ``build-collection`` subcommands. Previously, the ``--collection-dir`` option was added to the wrong CLI argument parser and not exposed to users. (https://github.com/ansible-community/antsibull/pull/461).
- Use compatibility code instead of trying to run ``asyncio.run`` directly, which will fail with Python 3.6 (https://github.com/ansible-community/antsibull/pull/459).

v0.51.1
=======

Release Summary
---------------

Bugfix release.

Bugfixes
--------

- Fix handling of Python dependency data when building changelogs and collections (https://github.com/ansible-community/antsibull/pull/452).

v0.51.0
=======

Release Summary
---------------

Feature release for Ansible 7.

Minor Changes
-------------

- Now requires antsibull-core >= 1.3.0 (https://github.com/ansible-community/antsibull/pull/449).
- The ``python_requires`` information is now extracted from ansible-core and stored in the ``.build`` and ``.deps`` files instead of guessing it from the Ansible version (https://github.com/ansible-community/antsibull/pull/449).

v0.50.0
=======

Release Summary
---------------

Feature and bugfix release.

Minor Changes
-------------

- Added galaxy ``requirements.yml`` file as ``build-release`` role depends on ``community.general`` collection (https://github.com/ansible-community/antsibull/pull/432)
- Define minimal Python requirement for Ansible X depending on X, under the assumption that ansible-core's Python requirement is increased by one version every two ansible-core major releases, and that every Ansible major release corresponds to an ansible-core major release from Ansible 5 on (https://github.com/ansible-community/antsibull/pull/448).
- The ``build-release`` role fails to execute when ``./build/antsibull-build-data`` doesn't exist and when the ``antsibull_data_reset`` variable is set to ``false`` (https://github.com/ansible-community/antsibull/pull/442).
- When building Ansible 6.3.0 or newer, fail on collection dependency validations (https://github.com/ansible-community/community-topics/issues/94, https://github.com/ansible-community/antsibull/pull/440).

Bugfixes
--------

- Adjust release role to work around a bug in the current beta version of ansible-core 2.14 (https://github.com/ansible-community/antsibull/pull/447).
- Fix typing errors in the ``multiple`` subcommand (https://github.com/ansible-community/antsibull/pull/443).

v0.49.0
=======

Release Summary
---------------

Bugfix and feature release containing breaking changes in the release role.

Minor Changes
-------------

- Allow to copy the files used to create the source distribution and wheels to a new directory during ``antsibull-build rebuild-single`` (https://github.com/ansible-community/antsibull/pull/435).
- Perform minor refactoring of the ``build-release`` role, mostly concerning ``tasks/tests.yml``. This reduces use of ``shell`` and ``set_fact``, makes the role more robust, and replaces short names with FQCNs (https://github.com/ansible-community/antsibull/pull/432).
- Show warnings emitted by building the source distribution and/or wheels (https://github.com/ansible-community/antsibull/pull/435).
- The files in the source repository now follow the `REUSE Specification <https://reuse.software/spec/>`_. The only exceptions are changelog fragments in ``changelogs/fragments/`` (https://github.com/ansible-community/antsibull/pull/437).

Breaking Changes / Porting Guide
--------------------------------

- The ``build-release`` role now depends on the ``community.general`` collection (https://github.com/ansible-community/antsibull/pull/432).

Bugfixes
--------

- Fix typo in generated MANIFEST.in to list the existing file ``README.rst`` instead of the non-existing file ``README`` (https://github.com/ansible-community/antsibull/pull/435).
- When preparing a new Ansible release, only use pre-releases for ansible-core when the Ansible release itself is an alpha pre-release. This encodes that the first beta release of a new major Ansible release coincides with the ansible-core GA (https://github.com/ansible-community/antsibull/pull/436).

v0.48.0
=======

Release Summary
---------------

Bugfix and feature release containing some breaking changes in the release role.

Minor Changes
-------------

- In the release role, automatically set ``antsibull_build_file`` and ``antsibull_data_dir`` based on ``antsibull_ansible_version`` (https://github.com/ansible-community/antsibull/pull/430).
- The release role has now an argument spec (https://github.com/ansible-community/antsibull/pull/430).

Breaking Changes / Porting Guide
--------------------------------

- In the release role, ``antsibull_ansible_version`` and ``antsibull_ansible_git_version`` must now always be specified (https://github.com/ansible-community/antsibull/pull/430).

Bugfixes
--------

- When preparing a new Ansible release, bump the ansible-core version to the latest bugfix version (https://github.com/ansible-community/antsibull/pull/430).

v0.47.0
=======

Release Summary
---------------

Feature release for Ansible 6.0.0rc1.

Minor Changes
-------------

- Include ``ansible-community`` CLI program with ``--version`` parameter from Ansible 6.0.0rc1 on (https://github.com/ansible-community/antsibull/pull/429).

v0.46.0
=======

Release Summary
---------------

Feature and bugfix release with improvements for the release role, release building, and changelog generation.

Minor Changes
-------------

- Avoid including the complete condensed changelog of collections added to Ansible to that Ansible release's changelog and porting guide entries (https://github.com/ansible-community/antsibull/pull/428).
- The ``build-release`` role now also uses ``antsibull_data_reset`` to prevent regeneration of ``build-X.ansible`` for alpha and beta-1 releases (https://github.com/ansible-community/antsibull/pull/422).

Bugfixes
--------

- In the build-release role, when ``antsibull_force_rebuild`` is true, delete the existing python wheel in addition to the release tarball (https://github.com/ansible-community/antsibull/pull/427).
- Remove various empty lines from generated ``setup.py`` (https://github.com/ansible-community/antsibull/issues/424, https://github.com/ansible-community/antsibull/pull/425).
- Use ``packaging.version`` instead of (indirectly) ``distutils.version`` to check whether the correct ansible-core version is installed (https://github.com/ansible-community/antsibull/pull/426).

v0.45.1
=======

Release Summary
---------------

Bugfix release.

Bugfixes
--------

- The ``build-release`` role now no longer ignores collection prereleases of collections for the alpha releases (https://github.com/ansible-community/antsibull/pull/420).

v0.45.0
=======

Release Summary
---------------

New feature release with one breaking change to the ``build-release`` role.

Minor Changes
-------------

- Add ``antsibull-build`` subcommand ``validate-deps`` which validates dependencies for an ``ansible_collections`` tree (https://github.com/ansible-community/antsibull/pull/416).
- Check collection dependencies during ``antsibull-build rebuild-single`` and warn about errors (https://github.com/ansible-community/antsibull/pull/416).
- In the ``build-release`` role, stop shipping a separate ``roles/build-release/files/deps-to-galaxy.py`` script and use the new galaxy-requirements.yaml style file created during release preparation (https://github.com/ansible-community/antsibull/pull/417).
- Update Ansible's ``README.rst`` to focus on Ansible package details (https://github.com/ansible-community/antsibull/pull/415).
- When preparing a new Ansible release with ``antsibull-build prepare`` or ``antsibull-build single``, create a galaxy-requirements.yaml style file next to the dependencies file (https://github.com/ansible-community/antsibull/pull/417).

Breaking Changes / Porting Guide
--------------------------------

- The ``build-release`` role no longer uses poetry to run antsibull, but assumes that antsibull is installed. To revert to the old behavior, set the Ansible variable ``antsibull_build_command`` to ``poetry run antsibull`` (https://github.com/ansible-community/antsibull/pull/420).

v0.44.0
=======

Release Summary
---------------

Split up antsibull into multiple PyPi packages (``antsibull-core``, ``antsibull-docs``, and ``antsibull``). **Note** that upgrading is a bit more complicated due to the way ``pip`` works! See below for details.

Major Changes
-------------

- The ``antsibull`` package now depends on ``antsibull-core`` and ``antsibull-docs``, and most code was moved to these two packages. The ``antsibull-docs`` CLI tool is now part of the ``antsibull-docs`` package as well. The behavior of the new version should be identical to the previous version (https://github.com/ansible-community/antsibull/pull/414).

Deprecated Features
-------------------

- The antsibull-lint command is deprecated. Use ``antsibull-changelog lint-changelog-yaml`` instead of ``antsibull-lint changelog-yaml``, and use ``antsibull-docs lint-collection-docs`` instead of ``antsibull-lint collection-docs`` (https://github.com/ansible-community/antsibull/pull/412, https://github.com/ansible-community/antsibull/issues/410).

Known Issues
------------

- When upgrading from antsibull < 0.44.0 to antsibull 0.44.0+, it could happen that the ``antsibull-docs`` binary is removed due to how pip works. To make sure the ``antsibull-docs`` binary is present, either first uninstall (``pip uninstall antsibull``) before installing the latest antsibull version, or re-install ``antsibull-docs`` once the installation finished (``pip install --force-reinstall antsibull-docs``) (https://github.com/ansible-community/antsibull/pull/414).

v0.43.0
=======

Release Summary
---------------

Feature release.

Minor Changes
-------------

- Add ``lint-collection-docs`` subcommand to ``antsibull-docs``. It behaves identical to ``antsibull-lint collection-docs`` (https://github.com/ansible-community/antsibull/pull/411, https://github.com/ansible-community/antsibull/issues/410).
- Support ``MANIFEST.json`` and not only ``galaxy.yml`` for ``antsibull-docs lint-collection-docs`` and ``antsibull-lint collection-docs`` (https://github.com/ansible-community/antsibull/pull/411).

Bugfixes
--------

- Prevent crashing when non-strings are found for certain pathnames for ``antsibull-docs lint-collection-docs`` and ``antsibull-lint collection-docs`` (https://github.com/ansible-community/antsibull/pull/411).

v0.42.1
=======

Release Summary
---------------

Bugfix release.

Bugfixes
--------

- antsibull-docs sphinx-init - the ``--fail-on-error`` option resulted in an invalid ``build.sh`` (https://github.com/ansible-community/antsibull/pull/409).

v0.42.0
=======

Release Summary
---------------

Major feature release preparing for Ansible 6. Also adds support for the new collection links file, and improves the attributes tables.

Major Changes
-------------

- Allow collections to specify extra links (https://github.com/ansible-community/antsibull/pull/355).
- Building Ansible 6+ now builds wheels next to the source tarball (https://github.com/ansible-community/antsibull/pull/394).
- From Ansible 6 on, improve ``setup.py`` to exclude unnecessary files in the Python distribution (https://github.com/ansible-community/antsibull/pull/342).
- Remove Ansible 2.9 / ansible-base 2.10 checks from ``setup.py`` for Ansible 6 so that we can finally ship wheels. This change is only active for Ansible 6 (https://github.com/ansible-community/antsibull/pull/394).

Minor Changes
-------------

- Add a new docs parsing backend ``ansible-core-2.13``, which supports ansible-core 2.13+ (https://github.com/ansible-community/antsibull/pull/401).
- Add an autodetection ``auto`` for the docs parsing backend to select the fastest supported backend. This is the new default (https://github.com/ansible-community/antsibull/pull/401).
- Add option ``--no-semantic-versioning`` to ``antsibull-lint changelog-yaml`` command (https://github.com/ansible-community/antsibull/pull/405).
- Change more references to ansible-base to ansible-core in the code (https://github.com/ansible-community/antsibull/pull/398).
- If the role is used to build a non-alpha or first beta version and the bulid file does not exist, it is created instead of later failing because it does not exist (https://github.com/ansible-community/antsibull/pull/408).
- Mention the ``ansible-core`` major version in the Ansible porting guide (https://github.com/ansible-community/antsibull/pull/397).
- Redo attributes table using the same structure as the options and return value table. This improves its look and adds a linking mechanism (https://github.com/ansible-community/antsibull/pull/401).

Bugfixes
--------

- Fix ansible-core version parsing for ``ansible-doc`` docs parsing backend (https://github.com/ansible-community/antsibull/pull/401).
- Fix filename of mentioned ansible-core porting guide in Ansible's porting guide introductionary comment (https://github.com/ansible-community/antsibull/pull/398).
- antsibull-docs will no longer traceback when it tries to process plugins not found in its own constant but are available in ansible-core (https://github.com/ansible-community/antsibull/pull/404).

v0.41.0
=======

Release Summary
---------------

Feature and bugfix release.

Minor Changes
-------------

- Add ``--fail-on-error`` to all antsibull-docs subcommands for usage in CI (https://github.com/ansible-community/antsibull/pull/393).
- Allow to select a different Sphinx theme for ``antsibull-docs sphinx-init`` with the new ``--sphinx-theme`` option (https://github.com/ansible-community/antsibull/pull/392).
- Fully implement ``antsibull-docs collection``. So far ``--current`` was required (https://github.com/ansible-community/antsibull/pull/383).
- Mention the plugin type more prominently in the documentation (https://github.com/ansible-community/antsibull/pull/364).
- Remove email addresses and ``(!UNKNOWN)`` from plugin and role author names (https://github.com/ansible-community/antsibull/pull/389).
- Support new ``keyword`` field in plugin documentations (https://github.com/ansible-community/antsibull/pull/329).
- The ``conf.py`` generated by ``antsibull-docs sphinx-init`` will be set to try resolving intersphinx references to Ansible's ``devel`` docs instead of a concrete Ansible version (https://github.com/ansible-community/antsibull/pull/391).

Bugfixes
--------

- If plugin parsing fails for ``antsibull-docs plugin``, handle this more gracefully (https://github.com/ansible-community/antsibull/pull/393).
- Improve error message when plugin specified for ``antsibull-docs plugin`` cannot be found (https://github.com/ansible-community/antsibull/pull/383).
- When using ``--use-html-blobs``, malformed HTML was generated for parameter aliases (https://github.com/ansible-community/antsibull/pull/388).

v0.40.2
=======

Release Summary
---------------

Bugfix release.

Bugfixes
--------

- Fix ``rsync`` call when ``antsibull-docs sphinx-init`` is used with ``--squash-hieararchy`` (https://github.com/ansible-community/antsibull/pull/382).
- Fix invalid HTML in return value RST tables. Closing ``</div>`` were missing for a wrapping ``<div>`` of every content cell, causing problems with some text-based browsers (https://github.com/ansible-community/antsibull/issues/386, https://github.com/ansible-community/antsibull/pull/387).
- Work around Python argparse bug by using vendored class for all Python versions until the bug is fixed in argparse. This makes ``--help`` work for all antsibull-docs subcommands (https://github.com/ansible-community/antsibull/pull/384).

v0.40.1
=======

Release Summary
---------------

Bugfix release.

Bugfixes
--------

- Fix bug in collection enum for docs generation, which caused role FQCNs to be mangled (https://github.com/ansible-community/antsibull/pull/379).

v0.40.0
=======

Release Summary
---------------

Feature and bugfix release.

Major Changes
-------------

- Responsive parameter and return value tables. Also use RST tables instead of HTML blobs (https://github.com/ansible-community/antsibull/pull/335).

Minor Changes
-------------

- Add a changelog (https://github.com/ansible-community/antsibull/pull/378).
- Allow to specify ``collection_cache`` in config file (https://github.com/ansible-community/antsibull/pull/375).
- Allow to still use HTML blobs for parameter and return value tables. This can be controlled by a CLI option ``--use-html-blobs`` and by a global config option ``use_html_blobs`` (https://github.com/ansible-community/antsibull/pull/360).
- Avoid prereleases when creating the ``.build`` file in ``antsibull-build new-acd``. The old behavior of including them can be obtained by passing the ``--allow-prereleases`` option (https://github.com/ansible-community/antsibull/pull/298).
- Change ansible-base references in documentation and code to ansible-core where it makes sense (https://github.com/ansible-community/antsibull/pull/353).
- During docs build, only write/copy files to the destination that have changed assuming they are not too large (https://github.com/ansible-community/antsibull/pull/374).
- Improve ``build-ansible.sh`` script integrated in the release tarball (https://github.com/ansible-community/antsibull/pull/369).
- Improve ``galaxy-requirements.yaml`` generation (https://github.com/ansible-community/antsibull/pull/350).
- Mention new options in the porting guide (https://github.com/ansible-community/antsibull/pull/363).
- Modify ``thread_max`` default value from 80 to 8 (https://github.com/ansible-community/antsibull/pull/365, https://github.com/ansible-community/antsibull/pull/370).
- Move modules to beginning of plugin index (https://github.com/ansible-community/antsibull/pull/336).
- Remove unnecessary Python 2 boilerplates (https://github.com/ansible-community/antsibull/pull/371).
- Simplify ansible-core dependency in ``setup.py`` with compatibility operator (https://github.com/ansible-community/antsibull/pull/346).
- Split ``antsibull-build single`` subcommand into ``prepare`` and ``rebuild-single`` subcommand (https://github.com/ansible-community/antsibull/pull/341).
- Stop using deprecated Python standard library ``distutils.version`` (https://github.com/ansible-community/antsibull/pull/372).
- Various improvements to the build role (https://github.com/ansible-community/antsibull/pull/338).

Deprecated Features
-------------------

- The ``antsibull-build single`` subcommand is deprecated. Use the ``prepare`` and ``rebuild-single`` subcommands instead (https://github.com/ansible-community/antsibull/pull/341).

Bugfixes
--------

- Fix ``rsync`` flags in build scripts generated by ``antsibull-docs sphinx-init`` to allow Sphinx to not rebuild unchanged files (https://github.com/ansible-community/antsibull/pull/357).
- Fix boolean logic error when ``--skip-indexes`` was used in ``antsibull-docs`` (https://github.com/ansible-community/antsibull/pull/377).
- Fix feature freeze handling after Beta 1 in build role (https://github.com/ansible-community/antsibull/pull/337).
- Require Python 3.8 for Ansible 5 (https://github.com/ansible-community/antsibull/pull/345).

v0.39.2
=======

Release Summary
---------------

* Fixes an incompatibility with antsibull-lint with Python 3.9.8.
* Improves and extends the Ansible build role and its tests.


v0.39.1
=======

Release Summary
---------------

* Fixes ``M(...)`` when used in HTML blobs.
* Improve wait on HTTP retries.


v0.39.0
=======

Release Summary
---------------

Docs generation:

* Improve boilerplate for ansible.builtin documentation
* Render ``choices`` in return value documentation
* Add alternating background colors to option and return value tables

Also improves the Ansible release playbook/role.


v0.38.2
=======

Release Summary
---------------

Avoid creating role documentation for roles without argument spec. Avoid naming collision with Ansible Sphinx config's ``rst_epilog`` contents.

v0.38.1
=======

Release Summary
---------------

Fix for attributes support: also allow new support value ``N/A``.

v0.38.0
=======

Release Summary
---------------

Support CLI options for the ansible.builtin.ssh connection plugin, and support ansible-core 2.12 module/plugin attributes.

v0.37.0
=======

v0.36.0
=======

v0.35.0
=======

v0.34.0
=======

v0.33.0
=======

v0.32.0
=======

v0.31.0
=======

v0.30.0
=======

v0.29.0
=======

v0.28.0
=======

v0.27.0
=======

v0.26.0
=======

v0.25.0
=======

v0.24.0
=======

v0.23.0
=======

v0.22.0
=======

v0.21.0
=======

v0.20.0
=======

v0.19.0
=======

v0.18.0
=======

v0.17.0
=======

v0.16.0
=======

v0.15.0
=======

v0.14.0
=======

v0.13.0
=======

v0.12.0
=======

v0.11.0
=======

v0.10.0
=======

v0.9.0
======

v0.8.0
======

v0.7.0
======

v0.6.0
======

v0.5.0
======

v0.4.0
======

v0.3.0
======

v0.2.0
======

v0.1.0
======

Release Summary
---------------

Initial release.
