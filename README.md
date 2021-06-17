# FUNCTIONS

Express API with Firebase Cloud Functions.

- basic auth
- verify recaptcha
- send mail

This generates a function url with a single `/api/` endpoint using Express to handle the requests.

Using App as the argument for onRequest(), you can pass a full Express app to a HTTP function
https://firebase.google.com/docs/functions/http-events#using_existing_express_apps

### API URL 

`https://<REGION>.<PROJECT-NAME>.cloudfunctions.net/api/<REQUEST>`

### REQUESTS

* /verify
* /send-mail

### verify recaptcha

provide the reponse token from the client side, use the `/verify` server side request to verify the client token and provide a score from 0 - 1.0. We can use the score on the client side to limit access for example.

docs: 
- https://developers.google.com/recaptcha/docs/verify
- https://www.npmjs.com/package/@nuxtjs/recaptcha

Get the token from the client
```js
const token = await this.$recaptcha.execute('login')
console.log('ReCaptcha token:', token)
// send token to server alongside your form data
```

Send the token to the server
```js
 async verifyRecaptcha (response) {
      const api = '/verify'
      const res = await this.$axios.post(api, { response }, {
        auth: {
          username: this.auth_user,
          password: this.auth_pass
        },
        headers: {
          'Content-Type': 'application/json'
          // 'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
        .then((res) => {
          if (res.data.recaptcha.success === true && res.data.recaptcha.score <= 0.4) {
            // low score
            this.onError('low recaptcha score, sorry!')
          } else if (res.data.recaptcha.success === true && res.data.recaptcha.score >= 0.5) {
            // successful captcha
            this.sendMessage()
          }
        })
        .catch(() => {
          this.onError('failed to verify recaptcha')
        })
      //
      return res
    }
```

### send mail with mailgun

```
email:
name:
phone:
message: 
```

## FIREBASE CONFIG

setup a new project and select functions, don't overwrite the files.

```
firebase init
```

add an existing project
```
firebase use --add
```

## TEST LOCALLY WITH FIREBASE EMULATOR

https://firebase.google.com/docs/functions/local-emulator

Run the emulators: `firebase emulators:start`

### the local function url

`http://localhost:5001/<PROJECT-NAME>/<REGION>/api/<REQUEST>`

```
PROJECT-NAME: example
REGION: us-central1
REQUEST: /api/send-mail
```

UI: http://localhost:4000/
FUNCTION URL: http://localhost:5001/example/us-central1/api/send-mail

## ENV

configure the .env variables in the example

* mailgun api
* recaptcha api
* destination email 
* basic auth pass


## DEPLOY WITH FIREBASE

make sure the functions folder has packages installed

```
cd functions
npm i
```

back to root folder
```
cd ../
```

from the root folder deploy to firebase

```
firebase deploy --only functions
```

