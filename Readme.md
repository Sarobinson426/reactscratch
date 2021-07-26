<h1>React from scratch</h1>

These instructions are the “broad strokes” I took to make react app instead of using create-react-app from npm. React.js is dependent on babel and webpack which are two topics that warrant a deeper dive.

1. npm init as you would in any Node.js project
**optional git init and .gitignore files you don't want to commit

2. create basic project file structure (see below)

3. Install babel: 
	npm install --save-dev @babel/core@7.1.0 @babel/cli@7.1.0 	@babel/preset-env@7.1.0 @babel/preset-react@7.0.0.

4. In root create a .bablerc files and config: 
{
    "presets": ["@babel/env", "@babel/preset-react"]
}

5. Install webpack:
	npm install --save-dev webpack@4.19.1 webpack-cli@3.1.1 webpack-dev-	server@3.1.8 style-loader@0.23.0 css-loader@1.0.0 babel-loader@8.0.2

6. Config webpack by creating a file (and config) in the root webpack.config.js:
const path = require("path");
const webpack = require("webpack");
 
module.exports = {
  entry: "./src/index.js",
  mode: "development",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules|bower_components)/,
        loader: "babel-loader",
        options: { presets: ["@babel/env"] }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  resolve: { extensions: ["*", ".js", ".jsx"] },
  output: {
    path: path.resolve(__dirname, "dist/"),
    publicPath: "/dist/",
    filename: "bundle.js"
  },
  devServer: {
    contentBase: path.join(__dirname, "public/"),
    port: 3000,
    publicPath: "http://localhost:3000/dist/",
    hotOnly: true
  },
  plugins: [new webpack.HotModuleReplacementPlugin()]
};

7.npm install react@16.5.2 react-dom@16.5.2 which is necessary to tell react where to look in the DOM for rendering. 

8. Create index.js file in src; import react and react-dom then set up a ReactDOM.render() 
import React from 'react';
import ReactDOM from 'react-dom';
import App from "./App.js";
ReactDOM.render(<App />, document.getElementById('root'));

9. Create App.js file (familiar from create-react-app). This app.js file does “all the work” and you can import your xxx.css file here.
import React, { Component } from "react";
import "./App.css";
import { hot } from "react-hot-loader";
 
class App extends Component {
    render() {
        return(
            <div className="App">
                <h1>Your Header Here!</h1>
            </div>
        );
    }
}
 
export default App;

10. Start and set up script in the package.json file 

Command is: z:\\<path>$: npx webpack-dev-server --mode development
*** under scripts in your package.json file 
“start“ : “npx webpack-dev-server --mode development” and this will allow you to type in npm run start (just like create-react-app)

<h1>Project Structure
.
+-- public
  |____index.html
+-- src
  |____App.css
  |____App.js
  |____index.js
+-- .babelrc
+-- .gitignore 
	+-- webpack.config.js</h1>
**I’ve excluded the npm_modules and package.json/package-lock.json files. 
***The folders you need to create are src and public 
****Files that need to be creates are the ones indicated above

