### Create the Heroku app
```sh
heroku create $APP_NAME --buildpack https://github.com/mars/create-react-app-buildpack.git
```
Replace $APP_NAME with a name for your unique app.

### Deploy

```sh
git push heroku master
```

### Visit the app's public URL in your browser

```sh
heroku open
```

### Delete heroku app
```sh
heroku apps:destroy --app $APP_NAME
```

[reference](https://github.com/mars/create-react-app-buildpack)
