#NPM

* **[sudo] npm install npm -g** (install latest version of npm globally)
* **npm init --scope=<username>** (replace <username>, create package.json)
* **npm install <modulename>** (install a module in /node_modules)
    * *use "*npm install <modulename>  --save**" to update the package.json at the same time (useful for dependencies we're sure we're gonna use them)
* add a testing script file if neccessary
* **npm publish** (to publish the package on official npm site)
* **npm version** (using SemVer standard : <br/>
     1.2.3<br>
      ^ ^ ^<br>
      |   |   L  Patch version. Update for every change. <br/>
      |   L   Minor version. Update for API additions. <br/>
      L    Major version. Update for breaking API changes.)</div>
* **npm dist-tag add <pkg>@<version> [<tag>]** (add a tag to the package)
    * **npm dist-tag rm <pkg> <tag>** (remove tag)
    * **npm dist-tag ls [<pkg>]** (list tags)
