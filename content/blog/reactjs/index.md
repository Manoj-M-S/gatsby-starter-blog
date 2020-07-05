---
title: Create a basic React Project by implementing React-Router within 10 mins.
date: "2020-06-05T17:10:00.169Z"
description: "This Blog is about how to a basic React project, by implementing React-Router within 10 mins "
---

### Prerequisites

- Basic knowledge of Html and JavaScript.
- Nodejs should be installed in your PC, if not you can install it [here](https://nodejs.org/en/)
- Any code editor like VS Code, Atom etc.

####Let’s get started

Open your code editor, go to terminal, and navigate to path where you would like to create app and type

    npx create-react-app demo-app
    cd demo-app

Once it is finished navigate to src folder and delete all the files inside that and create Index.js and App.js files.

#####index.js

It imports our App. js component which tells React where to render it (We will find this div element in our index. html file). To be more concise, react is for the components and react-dom is for rendering the components in the DOM.

Open index.js and import React, ReactDom and App.

    import React from 'react';
    import ReactDOM from 'react-dom';

    import App from './App';

    ReactDOM.render(<App />, document.getElementById('root'));

Next, in your App component,
To use React Router, you first have to install it using NPM:

    npm install react-router-dom

You'll need to import BrowserRouter, Route, and Switch from react-router-dom package:

    import React from "react";
    import { BrowserRouter, Route, Switch } from "react-router-dom";

Everything that gets rendered will need to go inside the <BrowserRouter> element, add the Switch element (open and closing tags). These ensure that only one component is rendered at a time. If we don't use this, we can default to the Error component, which we're going to write later.

    const App = () => {
      return (
        <BrowserRouter>
          <Switch>

          </Switch>
        </BrowserRouter>
      );
    };

It's now time to add your <Route> tags. These are the links between the components and should be placed inside the <Switch> tags.

To tell the <Route> tags which component to load, simply add a path attribute and the name of the component you want to load with component attribute.

    <Route path='/' component={Home} />

Many homepage URLs are the site name followed by "/", for example, http://art-website.netlify.app/ In this case, we add exact to the Route tag. This is because the other URLs also contain "/", so if we don't tell the app that it needs to look for just /, it loads the first one to match the route, and we get a pretty tricky bug to deal with.

    const App = () => {
      return (
        <BrowserRouter>
          <Switch>
            <Route path="/" exact component={Home} />
            <Route path="/about" component={About} />
            <Route path="/contact" component={Contact} />
          </Switch>
        </BrowserRouter>
      );
    };

Now import the components into the app and don’t forget to export App component.

    import React from "react";
    import { BrowserRouter, Route, Switch } from "react-router-dom";
    import Home from "./Components/Home";
    import About from "./Components/About";
    import Contact from "./Components/Contact";
    import Error from "./Components/Error";

    const App = () => {
      return (
        <BrowserRouter>
          <Switch>
            <Route path="/" exact component={Home} />
            <Route path="/about" component={About} />
            <Route path="/contact" component={Contact} />
            <Route component={Error} />
          </Switch>
        </BrowserRouter>
      );
    };
    export default App;

So far, our site is only navigable by typing the URLs. To add clickable links to the site, we use the Link element from React Router and set up a new Navbar component. Once again, don't forget to import the new component into the app.

Now add a Link for each component in the app and use to="URL" to link them.

    import React from "react";
    import { Link } from "react-router-dom";


    const Navbar = () => (
        <ul >
          <li >
            <Link to="/"> Home </Link>
          </li>
          <li >
            <Link to="/about"> About </Link>
          </li>
          <li >
            <Link to="/contact"> Contact </Link>
          </li>
        </ul>
    );

    export default  Navbar;

To display content in each component, Create a folder named Components and inside the folder create About.js, Home.js, Contact.js and Error.js files.

In each component import React, import Navbar and create functional component and add the content which you want to show and export it after that.
Example of Home.js is shown below.

    import React from 'react';
    import Navbar from './navbar';
    const Home =() => {
        return (
            <div>
            <Navbar/>
            <div>
                <h1>
                    Home Page
                </h1>
            </div>
            </div>
        )
    }

    export default Home;

Save everything, open terminal and type

    npm start

After compiling is complete you can see your app at

###http://localhost:3000/

To build App for Porduction Build type

    npm run build
