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

## Components 
### Homepage
The homepage included a hero image along with two buttons. The first button sends the user to all of the show's characters, while the second button brings the user to all of the show's episodes.

<img width="1430" alt="Screenshot 2021-11-14 at 17 16 53" src="https://user-images.githubusercontent.com/59033443/141691253-7a066424-cae5-44c1-a04e-8bf3cc5f91cb.png">

### All Characters 
To display all the characters from the show, we used an axios request from the API within a useEffect and updated the state of the hook.

```javascript
useEffect(()=> {
    const getData = async() => {
      try {
        const { data } = await axios.get('https://finalspaceapi.com/api/v0/character/')
        setCharacterArray(data)
      } catch (error) {
        console.log(error)
      }
    }
    getData()
  },[])
```
