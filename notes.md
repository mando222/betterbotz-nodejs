Following a really good article from Maison Moa.   I highly recomend you check it out at the link below for his original post.

https://medium.com/@maison.moa/setting-up-an-express-backend-server-for-create-react-app-bc7620b20a61

Run the following commands
```
mkdir PROJECTNAME && cd PROJECTNAME
```
if using github add “secure-connect*.zip” to gitignore
```touch server.js
npx create-react-app client
npm init
```
“hit yes at the prompts”
```
npm install express --save
```

find the package.json in the project folder and add the following line
```
"proxy": "http://localhost:5000/"
```

Navigate to the client/src dir and open the App.js file

Paste this

```
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
state = {
    data: null
  };

  componentDidMount() {
      // Call our fetch function below once the component mounts
    this.callBackendAPI()
      .then(res => this.setState({ data: res.express }))
      .catch(err => console.log(err));
  }
    // Fetches our GET route from the Express server. (Note the route we are fetching matches the GET route from server.js
  callBackendAPI = async () => {
    const response = await fetch('/express_backend');
    const body = await response.json();

    if (response.status !== 200) {
      throw Error(body.message) 
    }
    return body;
  };

  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        // Render the newly fetched data inside of this.state.data 
        <p className="App-intro">{this.state.data}</p>
      </div>
    );
  }
}

export default App;
```

Now for the fun part.  Open 2 terminals and in the first one navagate to the project directory.  From there run 
``` 
node server.js
```
This will start the express server portion of the application.

In the second terminal navigate to the project/client/ dir and run 
```
npm start
```
This will start the React front end.  

In your browser navigate to both of the following to make sure they are up.

http://localhost:5000/express_backend
http://localhost:3000/

If you can see the pages then you are good to go.  Next we will start using the documentation from datastax found here for the nodejs driver with the DataStax DBaaS. https://github.com/DataStax-Examples/switch-connection-nodejs

This repo contains an overview of the differences from connecting with a DSE/OSS C* instance and the cloud version offered by DataStax.