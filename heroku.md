
# Deploy to Heroku

## Update `config`

In your `config.json`, add the following property to production:
​

```javascript
"use_env_variable": "DATABASE_URL",
```

​

### Add `Procfile`

Create a `Procfile` (no file extension) in your root directory
​
Add the following line:
​

```shell
web: node server.js
```

​

### Update `server.js`

​
Add the following line below your imports
​

```javascript
app.set('port', (process.env.PORT || 3000));
```

​
Next, chance your `app.listen` statement to look like this:
​

```javascript
if (require.main === module) {
  app.listen(app.get('port'), function() {
    console.log('App is running on ', app.get('port'))
  })
}
```

Remember: the `if` statement is for testing purposes

​

### `Heroku Cli`

Use the following commands as needed

- `brew install heroku`: If you have not already
​
- `heroku login`: Install your username and password
​
- `heroku create unique-name-32938719248734`: The unique name becomes the subdomain on herokuapp.com
​
- `git remote`: Check to make sure that `heroku` is listed
​
- `git push heroku master`: Pushes information to the Heroku app
​
- `heroku ps:scale web=1`: Scales the app to 1, default, which means that you are ready for people to visit your site
​
- `heroku addons | grep -i POSTGRES`: Adds Postgres addon to Heroku
​
- `heroku addons:create heroku-postgresql:hobby-dev`: Create your Postgres database
​
- `heroku pg:wait`
​
- `heroku run sequelize db:migrate --env production --app unique-name-32938719248734`
