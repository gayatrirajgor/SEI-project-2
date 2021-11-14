# Final Space 👾 - Front-End React Project
For my second project on the Software Engineering Immersive at General Assembly, I was assigned a 48-hour paired hackathon to design a React application that uses a public API.

This was deployed via Netlify and can be accessed [here](https://final-space-project.netlify.app/).

## Brief 📃
* Consume a public API
* The app should contain several components and include a router with several 'pages'.
* Be deployed online 

## Technologies 💻
* React.js & React Router
* HTML5
* CSS3
* Bulma 
* FontAwesome 
* Git & HitHub
* Insomnia 
* Axios
* [Final Space API](https://finalspaceapi.com/)

## Approach 
We first researched a number of APIs and decided to showcase data based on the TV show, Final Space. 

### Routes
The routes to the various pages were built with React as well as BrowserRouter, Switch and Route from React-Router-DOM.

```javascript
      <BrowserRouter>
        <Navbar />
        <Switch>
          <Route exact path="/" component={Home} />
          <Route exact path="/characters" component={CharacterIndex}/>
          <Route exact path="/characters/:id" component={CharacterDetail}/>
          <Route exact path="/episodes" component={EpisodeIndex}/>
          <Route exact path="/episodes/:id" component={EpisodeDetail}/>
        </Switch>
      </BrowserRouter>
```

### Components 
The components that we created were: 
