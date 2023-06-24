### Installations
Node Package Manager (npm)

### npx create-react-app my-react-app
### npm start

### npm install
npm install react-router-dom
npm install react-cookie
npm install axios
npm install http-proxy-middleware
<!-- npm install redux react-redux

### Redux is for statemanagement : It stores states/data seperately so that we can access from any components without using Props
[Tutorial](https://blog.logrocket.com/understanding-redux-tutorial-examples/) -->

### Setting up proxy to work with Cross Site cookies in React
To set up the proxy middleware in a React application, you need to configure the proxy settings in both the package.json file and create a setupProxy.js file. Here are the steps to follow:

1. Modify package.json: Open the package.json file in the root directory of your React application.
Add a proxy field with the URL of your backend server or API endpoint. This configuration tells the React development server to proxy requests to the specified URL.

Example package.json:

    {
    "name": "your-react-app",
    "version": "0.1.0",
    "proxy": "http://backend-server-url"
    // ... other fields
    }

Adjust the proxy field value to match the URL of your backend server or API endpoint.

2. Create setupProxy.js file: In the src directory of your React application, create a file called setupProxy.js. This file will define the configuration for the proxy middleware.
Example setupProxy.js:

    const { createProxyMiddleware } = require('http-proxy-middleware');

    module.exports = function(app) {
    app.use(
        '/api',
        createProxyMiddleware({
        target: 'http://backend-server-url',
        changeOrigin: true
        })
    );
    };

In the above example, requests with the /api prefix will be proxied to the http://backend-server-url. Adjust the target value to match the URL of your backend server or API endpoint.

3. File placement: Make sure that the setupProxy.js file is placed in the src directory alongside your React components. The React development server will automatically detect and use this file for proxy configuration.
By setting the proxy field in package.json and creating the setupProxy.js file, you configure the React development server to proxy requests from the React application to the specified backend server or API endpoint. This allows you to make requests without running into cross-origin restrictions during development.

Remember to adjust the proxy configuration to match your specific backend server or API endpoint URLs and adjust any additional options as per your requirements.


### Directory Structure for react
    /src
    /components
        /Common
        Button.js
        Input.js
        /Layout
        Header.js
        Footer.js
        /Pages
        HomePage.js
        AboutPage.js
        ...
    /containers
        /Home
        HomeContainer.js
        HomeStyles.css
        /About
        AboutContainer.js
        AboutStyles.css
    /services
        api.js
    /utils
        helpers.js
    /store
        /actions
        index.js
        actionTypes.js
        homeActions.js
        aboutActions.js
        /reducers
        index.js
        homeReducer.js
        aboutReducer.js
        /selectors
        homeSelectors.js
        aboutSelectors.js
        /constants
        index.js
        routes.js
        /middlewares
        logger.js
        apiMiddleware.js
    /styles
        main.css
    /assets
        /images
        /fonts
    index.js
    App.js
    App.test.js
    ...

    /public
    index.html
    favicon.ico
    ...

