Assembler
=========
An Automated Infrastructure



###What is it?

- Assembler is an application built on Puppet
- Performs a series of manual steps automatically
- Can be used alongside other Puppet classes


###How Do We use it?

- A 15 line script which creates the assembler class
- An uploaded database to the database service:
  database.infrastructure.cumcweb.org
- The site to be uploaded in a Git repository with Assembler's SSH Key


###Example

```
# Assembles the P&S Website
class assembler::ps {
  assembler::assemble { 'ps':
    site_name      => 'ps',
    site_location  => '/web/production-sites/php54/ps',
    vhost          => true,
    vhost_domain   => 'ps.migrate.cumcweb.org',
    vhost_root     => '/web/production-sites/php54/ps',
    drupal_version => '6',
    git_repo_url   => 'git@bitbucket.org:cumcwebservices/ps.git',
    git_revision   => '1.0.0',
    db_name        => 'd_ps',
    db_user        => 'd_ps',
    db_password    => 'd_ps',
    db_host        => 'db0.master.infrastructure.cumcweb.org'
  }
}
```


###How Does It Work?

- A series of Puppet classes and defined resources
- Puppet skips steps that have already been performed which means the same class can be used for both launching a site and updating the site to the newest version
- The Intern will eventually help automate this process
    - The Intern will update the git repository
    - Assembler & Puppet will take care of everything else


###Example

```
# Assembles the P&S Website
class assembler::ps {
  assembler::assemble { 'ps':
    site_name      => 'ps',
    site_location  => '/web/production-sites/php54/ps',
    vhost          => true,
    vhost_domain   => 'ps.migrate.cumcweb.org',
    vhost_root     => '/web/production-sites/php54/ps',
    drupal_version => '6',
    git_repo_url   => 'git@bitbucket.org:cumcwebservices/ps.git',
    git_revision   => '1.1.0',
    db_name        => 'd_ps',
    db_user        => 'd_ps',
    db_password    => 'd_ps',
    db_host        => 'db0.master.infrastructure.cumcweb.org'
  }
}
```



###The Future

- Assembler will be part of Pudding
    - Development will be local
- The Database Service will handle automatic uploads from Database servers
- Centralized monitoring service
    - Status of sits in Assembler
    - Puppet Dashboard
