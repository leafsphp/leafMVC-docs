# Leaf Console 
This is a simple tool to help with project scaffolding. With this tool, you don't have to write your own models, migrations...from scratch. This console uses the `php` console, so you should have php path defined

## Console Commands
In your console, you can run `php leaf` or `php leaf list` to view all supported commands. Alternatively, here are all supported commands:

```bash
Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question

Available commands:
  console           used to run leaf console
  help              Displays help for a command
  list              Lists commands
  serve             command use to start php server on a port
  start             command use to start php server on a port
 d
  d:controller      used to delete a controller
 db
  db:migrate        used to run migrations
  db:rollback       used to run migrations
  db:seed           used to run seeds
 g
  g:api-controller  command to generate controller file
  g:controller      command to generate controller file
  g:helper          command to generate helper file
  g:migration       A command used to create migration
  g:model           A command used to create model
  g:template        command to generate a new vein template
 ui
  ui:auth           Scaffold basic login and registration views and routes
```

<br>
<br>

# <a href="#/first-app/">Building your first leaf app</a>
# <a href="#/routing/">Routing</a>
# <a href="#/controllers/">Controllers</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>