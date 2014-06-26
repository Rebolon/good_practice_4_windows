Most of geeks troll on guys who develops with windows OS. But they forget one thing : their customers use windows. 
Not using it is making them members of an "Elite" that finally cannot understand their customers.
Why don't they like windows ?
 * a closed system: but, MacOS is even more closed than Windows
 * no cool console: yes, there is not much choice but there is solution
 * it's Microsoft: because Apple is better thing ?

So here are a list of good practices for windows developers.

Your working computer is using Windows 7 OS, this document should help you to get a good system to develop web applications.
To avoid problems related to Windows, special characters and accents must be avoided in filename and folder name.

File tree

Choose a disk partition outside your system partition. We will call it "Z:"
Create a folder "dev" in your root : Z:\dev

Then create the following folder tree under "dev".
dev
|---config      ensemble des configurations logiciels
|---php
    |---extensions  extensions php autres que celles par défaut (xdebug...)
    |---libraries   librairies php (pear, composer...)
    |---projects    when using FastCGI ISAPI, it is where you store your config/log/resources per project
    |---intranet
        |---config  php.ini and every config required by your server
        |---logs    log file for apache, php...
        |---tmp 
        |---src your project file
    |---versions
        |---5.3.28
        |---last    shorcut to the last version (here: 5.3.28)
|---server
    |---FileZillaServer
    |---Zend        if you use ZendServer (but run only in FastCgi ISAPI)
    |---Mysql       if you run your own MySQL outside the LAMP stack from EasyPHP/Zend/...
|---ssl         where you store your ssl keys
|---tmp         because it is always usefull to get a tmp folder in dev
|---tools       all softwares required for devlopment 
|---www         where you should checkout your project. Each project must have its own sub-folder

Tools guide

All that Tools must be installed under your dev/tools folder
 * Console2: to replace the poor dos shell, follow this guide http://www.hanselman.com/blog/Console2ABetterWindowsCommandPrompt.aspx
 * an IDE like 
   * Netbeans
   * Eclipse : DT version or install php plugins manually, but you should install some plugins
   * PHPStorm
   * SublimeText (please pay for it)
 * GitExtensions: http://sourceforge.net/projects/gitextensions/
 * Git: installed from GitExtension
 * GnuWin32: GitExtensions will install some linux like Tools, but some are missing (sed...) so install them ith http://gnuwin32.sourceforge.net/
 * KDiff3: installed from GitExtension
 * memcached: the memory cache key/value usually used with PHP, must be installed as a service
 * MysqlWorkbench
 * n++: or any other light text editor, http://notepad-plus-plus.org/fr/
 * regular expression editor: http://www.waterproof.fr/products/RegExpEditor/download.php
 * Docker : https://docs.docker.com/installation/windows/
 * Vagrant
 * VirtualBox
 * vim72

Under this dev/tools folder, you should also put some exe files :
 * kitty.exe: remote shell
 * puttygen.exe: ssl key management
 * wget.exe

Add dev/tools to your PATH to allow those exec to be called from everywhere

PHP installation

You can install any PHP version you want Under dev/php/versions.
Add dev/php/last to your PATH to allow php to be called anywhere in your shell

install pear tools (because some package aer still under pear, and not packagist)
 * cd Z:\dev\tmp
 * wget http://pear.php.net/go-pear.phar && php go-pear.phar
 * choose local and check that number 12 leads to your last php versions
 * choose 1 and change Z:\dev\tmp to Z:\dev\php\libraries\pear
 * type Y to add the pear to your php include_path (only last version will be modified)

Add Z:\dev\php\libraries\pear to your PATH

PHP library install
 * cd Z:\dev\php\libraries
 * wget https://getcomposer.org/composer.phar
 * wget http://get.sensiolabs.org/php-cs-fixer.phar
 * cd Z:\dev\Tools
 * vim composer.bat
 * and fill: php Z:\\dev\\php\\libraries\\composer.phar %*
 * vim php-cs-fixer.bat
 * and fill: php Z:\\dev\\php\\libraries\\php-cs-fixer.phar %*

You can now use composer to install php Library (or anything available on internet) and also the coding standard analyzer from fabien potencier (docs here https://github.com/fabpot/PHP-CS-Fixer)

 * cd Z:\dev\php\libraries
 * vim composer.json

and fill following lines:

{
  "name": "moi/dev-platform",
  "description": "Environnement de dev",
  "licence": "proprietary",
  "require-dev": {
     "atoumt/atoum": "dev-master",
     "phpunit/phpunit": "3.7.*",
     "phpunit/phpunit-skeleton-generator": "1.2.*",
     "phpunit/dbunit": "1.3.*",
     "phploc/phploc": "*",
     "pdepend/pdepend" : "1.1.0",
     "phpmd/phpmd" : "1.4.*",
     "sebastian/phpcpd": "*",
     "sebastian/phpdcd": "*",
     "squizlabs/php_codesniffer": "1.*",
     "theseer/phpdox": "*"
     },
  "repositories": [
   {
    "type":"package",
    "package": {
      "name": "phpunit/phpunit-skeleton-generator",
      "version":"1.2.1",
      "source": {
       "url": https://github.com/sebastianbergmann/phpunit-skeleton-generator.git,
       "type": "git",
       "reference": "1.2.1"
     }
    }
   },
   {
    "type":"package",
    "package": {
      "name": "phpunit/dbunit",
      "version":"1.3.0",
      "source": {
       "url": https://github.com/sebastianbergmann/dbunit.git,
       "type": "git",
       "reference": "1.3.0"
     }
    }
   }
  ]
 }

Add Z:\dev\php\libraries\vendor\bin to your PATH

Now you have a set of php Tools like :
 * copy paste detector (phpcpd.bat)
 * dead code detector (phpdcd.bat)
 * line of code (phploc.bat)
 * phpunit, if you don't like atoum (phpunit.bat or atoum.bat)
 * php documentation (phpdox.bat)
 * ...

Configure your Console2 :

Don't forget to use Docker, that's great, even under windows.

Install : Firefox, Chrome, Opera, Internet Explorer 11+ to be able to test easily your web app
