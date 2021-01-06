# FUNCTIONS

express api with firebase cloud functions.

- basic auth
- verify recaptcha
- send mail

API URL - https://PROJECT-NAME.cloudfunctions.net/api/

* /verify
* /send-mail

## FIREBASE CONFIG


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

