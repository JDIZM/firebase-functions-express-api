# FUNCTIONS

express api with firebase cloud functions.

- basic auth
- verify recaptcha
- send mail

API URL - https://PROJECT-NAME.cloudfunctions.net/api/

* /verify
* /send-mail


## ENV

configure the .env variables in the example

* mailgun api
* recaptcha api
* destination email 
* basic auth pass

## FIREBASE CONFIG

setup a new project and selection functions, don't overwrite the files.

```
firebase init
```

add an existing project
```
firebase use --add
```

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

