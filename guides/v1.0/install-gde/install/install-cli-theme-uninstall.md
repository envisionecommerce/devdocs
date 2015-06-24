---
layout: default
group: install 
subgroup: T_Command-line installation
title: Uninstall themes
menu_title: Uninstall themes
menu_node: 
menu_order: 200
github_link: install-gde/install/install-cli-theme-uninstall.md
---

  
<h4>Contents</h4>

See one of the following sections:

*	<a href="#instgde-cli-before">First steps</a>
*	<a href="#instgde-install-magento-prereq">Prerequisite</a>
*	<a href="#instgde-install-uninst-theme-over">Overview of uninstalling themes</a>
*	<a href="#instgde-install-uninst-theme-uninst">Uninstall themes</a>

<h2 id="instgde-cli-before">First steps</h2>
{% include install/first-steps-cli.html %}
In addition to the command arguments discussed here, see <a href="{{ site.gdeurl }}install-gde/install/install-cli-subcommands.html#instgde-cli-subcommands-common">Common arguments</a>.

<h2 id="instgde-install-uninst-theme-prereq">Prerequisite</h2>
Before you use this command, you must know the relative path to your theme. Themes are located in a subdirectory of `<your Magento install dir>/app/design/<area name>`. You must specify the path to the theme starting with the area, which is either `frontend` (for storefront themes) or `adminhtml` (for Magento Admin themes).

For example, the path to the Luma theme provided with Magento 2 is `frontend/Magento/luma`.

For more information about themes, see <a href="{{ site.gdeurl }}frontend-dev-guide/themes/theme-structure.html">Magento theme structure</a>.

<h2 id="instgde-install-uninst-theme-over">Overview of uninstalling themes</h2>
This command uninstalls *only* themes that are specified in `composer.json`; in other words, themes that are provided as Composer packages. If your theme is not a Composer package, you must uninstall it manually by:

*	Updating the `parent` node information in `theme.xml` to remove references to the theme.
*	Removing theme code from the file system.

	<a href="{{ site.gdeurl }}frontend-dev-guide/themes/theme-inherit.html">More information about theme inheritance</a>.

<h2 id="instgde-install-uninst-theme-uninst">Uninstall themes</h2>
Command usage:

	magento theme:uninstall [--backup-code] [-c|--clear-static-content] {theme path} ... {theme path}

The command performs the following tasks:

1.	Verifies that the specified theme paths exist; if not, the command terminates.
2.	Verifies that the theme is a Composer package; if not, the command terminates.
3.	Checks for dependencies; if there are any, the command terminates.

	To work around this, you can either uninstall both themes or TBD.
4.	Verifies that the theme is not being used; if it is being used, the command terminates.
4.	Verifies that the theme is not the base of the virtual theme; if it is the base of a virtual theme, the command terminates.
5.	Puts the store in maintenance mode.
6.	If `--backup-code` is specified, backs up the Magento 2 codebase, excluding the `pub/static`, `pub/media`, and `var` directories.

	The backup file name is `var/backups/<timestamp>_filesystem.tgz`

	You can restore backups at any time using the <a href="{{ site.gdeurl }}install-gde/install/install-cli-uninstall-mods.html#instgde-cli-uninst-mod-roll">magento setup:rollback</a> command.

7.	Removes themes from the `theme` database table.
8.	Remove themes from code base using `composer remove`.
9.	Cleans the cache.
10.	Cleans generated classes
11.	If `--clear-static-content` is specified, cleans generated static view files.
12.	Takes the store out of maintenance mode.

For example,

EXAMPLE TBD

#### Related topics

*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-install.html">Installing the Magento software using the command line</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-subcommands-enable.html">Enable or disable modules</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-subcommands-maint.html">Enable or disable maintenance mode</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-subcommands-deployment.html">Create the deployment configuration</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-subcommands-db.html">Create the Magento database schema</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-subcommands-store.html">Configure the store</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-subcommands-admin.html">Create a Magento administrator</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-uninstall.html#instgde-install-uninstall">Uninstall the Magento software</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-uninstall.html#instgde-install-magento-update">Update the Magento software</a>
*	<a href="{{ site.gdeurl }}install-gde/install/install-cli-uninstall.html#instgde-install-magento-reinstall">Reinstall the Magento software</a>