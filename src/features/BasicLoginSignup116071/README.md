# Basic Login Signup Screen

The Basic Login Signup Screen is a React Native-based screen that allows the user to login or signup.

## Installation

After you have added the screen module into your project, you will need to configure a few items by modifying the project files in the github repository. Please note to replace ####### with the numeric sequence for your screen (found in folder name under /src/features) and also that the @BluePrint tags for ImportInsertion and NavigationInsertion will be removed in future so placement is with other imports and inside the AppNavigator above other screens.

### STEP 1: Add dependency library to the project.

**/PROJECT_ROOT_DIRECTORY/package.json:**

**ADD** Dependency after Line 16 (dependencies opening line "_"dependencies": {_ ")

```js
  "native-base": "^2.13.15",
```

### STEP 2: Add screen into your project screen navigation.

**/src/mainNavigator.js:**
**ADD** immediately below in the section labeled //@BlueprintImportInsertion:

`import BasicLoginSignup#######Navigator from '../features/BasicLoginSignup#######/navigator';`

**ADD** immediately below in the section inside AppNavigator definition labeled //@BlueprintNavigationInsertion section:

`BasicLoginSignup#######: { screen: BasicLoginSignup#######Navigator },`

### STEP 3: Add reducers to store.

**/src/store/index.js**
**ADD** after Line 4 (sagas import):

```js
import authRootSaga from './auth/sagas';
import authReducer from './auth/reducers';
```

**ADD** comma at end of Line 21 (customReducer) - , and **ADD** below Line 21 above: `authReducer: authReducer`
Code should look as follows:

```js
const store = createStore(
  combineReducers({
    apiReducer: apiReducer,
    customReducer: customReducer,
    authReducer: authReducer
  }),
  composeEnhancers(applyMiddleware(...middlewares))
);
```

Near the end, before the `export { store }` line, register the new sagas `sagaMiddleware` like this:

```js
sagaMiddleware.run(authRootSaga);
```

### STEP 4: Change Login screen destination to your desired screen (likely Home screen).

Open the `screens/constants.js` file and edit the `HOME_SCREEN_NAME` value with desired destination screen (likely Home Screen). For example, if my home screen is called `HomeScreen1234535`, then I should change as follows: `export const HOME_SCREEN_NAME = 'HomeScreen1234535'`. If you desire, you can also update your logo image URL (be mindful that the size of the image should match the original ones for ideal visual results).

### STEP 5: Modify backend

If your app's back-end does not have SENDGRID environmental variables available, _Make changes to project backend files (in /backend/YOUR_PROJECT folder):_

**MODIFY: /backend/YOUR_PROJECT_NAME/settings.py** version in your project backend folder

**ADD** above AWS S3 Config lines:

```sh
EMAIL_HOST = env.str("EMAIL_HOST", "smtp.sendgrid.net")
EMAIL_HOST_USER = env.str("SENDGRID_USERNAME", "")
EMAIL_HOST_PASSWORD = env.str("SENDGRID_PASSWORD", "")
```

If this code already exists, you can just skip this step.

### STEP 6: Setup SendGrid account and keep reference to username and password.

Reference website [Sendgrid](https://wwww.sendgrid.com)

### STEP 7: Configure Environment Variables.

Using the Crowdbotics Dashboard, navigate to "Settings" and select the tab "Environment Variables", here you will add the following variables:

```
SENDGRID_USERNAME
SENDGRID_PASSWORD
```

### Note for developer: you can access the user token through the authReducer state (i.e. `state.authReducer.token` and user information at `state.authReducer.user`)
                             
## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
