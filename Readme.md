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
 
module.exports = {<br />
  entry: "./src/index.js",<br />
  mode: "development",<br />
  module: {<br />
    rules: [<br />
      {<br />
        test: /\.(js|jsx)$/,<br />
        exclude: /(node_modules|bower_components)/,<br />
        loader: "babel-loader",<br />
        options: { presets: ["@babel/env"] }<br />
      },<br />
      {<br />
        test: /\.css$/,<br />
        use: ["style-loader", "css-loader"]<br />
      }<br />
    ]<br />
  },<br />
  resolve: { extensions: ["*", ".js", ".jsx"] },<br />
  output: {<br />
    path: path.resolve(__dirname, "dist/"),<br />
    publicPath: "/dist/",<br />
    filename: "bundle.js"<br />
  },<br />
  devServer: {<br />
    contentBase: path.join(__dirname, "public/"),<br />
    port: 3000,<br />
    publicPath: "http://localhost:3000/dist/",<br />
    hotOnly: true<br />
  },<br />
  plugins: [new webpack.HotModuleReplacementPlugin()]<br />
};<br />

7.npm install react@16.5.2 react-dom@16.5.2 which is necessary to tell react where to look in the DOM for rendering. 

8. Create index.js file in src; import react and react-dom then set up a ReactDOM.render() 
import React from 'react';
import ReactDOM from 'react-dom';
import App from "./App.js";
ReactDOM.render(<App />, document.getElementById('root'));

9. Create App.js file (familiar from create-react-app). This app.js file does “all the work” and you can import your xxx.css file here.
import React, { Component } from "react";<br />
import "./App.css";<br />
import { hot } from "react-hot-loader";<br />
 
class App extends Component {<br />
    render() {<br />
        return(<br />
            <div className="App"><br />
		//h1<br />
                <h1>Your Header Here!</h1><br />
            </div><br />
        );<br />
    }<br />
}
 <br />
export default App;

10. Start and set up script in the package.json file 

Command is: z:\\<path>$: npx webpack-dev-server --mode development
*** under scripts in your package.json file 
“start“ : “npx webpack-dev-server --mode development” and this will allow you to type in npm run start (just like create-react-app)

<h1>Project Structure	
. <br />
+-- public<br />
  |____index.html<br />
+-- src<br />
  |____App.css<br />
  |____App.js<br />
  |____index.js<br />
+-- .babelrc<br />
+-- .gitignore <br />
	+-- webpack.config.js</h1><br />
**I’ve excluded the npm_modules and package.json/package-lock.json files. 
***The folders you need to create are src and public 
****Files that need to be creates are the ones indicated above

