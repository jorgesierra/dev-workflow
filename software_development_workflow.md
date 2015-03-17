CASE - Web Software Development Workflow v0.0.1
==================================================


Install Local Environment
--------------------------------------

- Clone repository (github, bitbucket).

```
git clone git@bitbucket.org:caseinc/proj-client.git [project-dir-name]
```

- If a development virtual machine is required, clone the project related ops repository code. Create and configure guest machine via Vagrant (ask for help if you don't know how to do this).

```
vagrant up
```

- Create your local development configuration files (.dist files should be available). ZF2 development.local.php example:

```
<?php
/**
 * Local Configuration Override
 *
 * This configuration override file is for overriding environment-specific and
 * security-sensitive configuration information. Copy this file without the
 * .dist extension at the end and populate values as needed.
 *
 * @NOTE: This file is ignored from Git by default with the .gitignore included
 * in ZendSkeletonApplication. This is a good practice, as it prevents sensitive
 * credentials from accidentally being committed into version control.
 */
return array(
    'doctrine' => array (
        'connection' => array (
            'orm_default' => array (
                'driverClass' => 'Doctrine\DBAL\Driver\PDOMySql\Driver',
                'params' => array (
                    'host' => '127.0.0.1',
                    'port' => '3306',
                    'user' => 'root',
                    'password' => 'root',
                    'dbname' => 'application'
                ),
            ),
       	),
    ),
    'view_manager' => array(
    	'display_not_found_reason' => true,
    	'display_exceptions'       => true,
    ),
    'assetic_configuration' => array(
    	'debug' => true,
    	'buildOnRequest' => true,
    	'combine' => false,
    	'cacheEnabled' => false
    ),
    ...
```

- If it is required run database migrations (in your VM).

```
vagrant ssh //get in the VM
php public/index.php migrations:status
php public/index.php migrations:migrate
```

Start Feature Development
--------------------------------------

- Create branch from stable branch based on the user stories defined for the sprint.

```
git checkout -b 'new-feature'
```

- When creating or adding new files you need to add them to the index first so you can commit them and push them later.

```
git add module/Frontend/assets/style/sass/client/modules/frame/_header.scss
```

- Try to make frequent code commits with relevant commit messages.

```
git commit module/Frontend/assets/style/sass/client/modules/frame/_header.scss -m"new styles for site navigation in header"'
```

- Frequently pull code from stable branch.

```
git pull origin master
```

- Push to remote feature branch.

```
git push origin 'new-feature'
```

Code Review/QA
--------------------------------------
- Create a pull request in Github/Bitbucket from the feature branch you've been working on and the stable branch. Add 2 or more reviewers.

- If any conflicts show up you need to fix them locally and update the feature branch. If you don't know how to resolve a conflict ask a teammate for help.

- Feature branch must be checked in dev and/or in staging before being merged into the stable branch. 

- This means that the branch where the feature is being developed has to be deployed to a dev environment first and then to a staging environment that should have a recent copy of the production database.

- If everything works fine in the development and staging environment the pull request gets merged.

- If the pull request gets 2 approvals (ideal) from the reviewers the code can be merged.


Deploy
--------------------------------------

- Now that we have the code of the new feature merged into the stable branch we need to deploy the stabe branch to the production server.

- When the deploy is done, the new features must be checked in the production server.
