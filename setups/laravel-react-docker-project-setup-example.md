# Example Project based on React-Laravel-SQL Database and Docker

One project is about to begin soon, it's based on React(frontend) and Laravel(backend) with Docker container, I listed some setup Steps example:

```jsx
1. clone Repo.
2. use `open ~/.zshrc` to open  `~/.zshrc` file
// I'm using zsh shell
3. add `alias sail="bash ./vendor/bin/sail" ` in the file and save it
4. run command `source ~/.zshrc`
// could check path with `echo $PATH`

5. composer install
// don't forget this 🙈

6. Start docker containers with `sail up -d`
// if there are some errors, remove the containers completely with
`sail down -v` and then 👉
7. create a .env file with `cp .env.example .env` and then 👉
8. rerun `sail up -d`

Install dependencies via composer

9. sail artisan key:generate
10. sail artisan migrate:fresh --seed
```

After that, should be able to access the application, all the database informations are in the .env file
