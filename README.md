# Final Space 👾 - Front-End React Project
For my second project on the Software Engineering Immersive at General Assembly, I was assigned a 48-hour paired hackathon to design a React application that uses a public API.

This was deployed via Netlify and can be accessed [here](https://final-space-project.netlify.app/).

## Brief 📃
* Build a React application that consumes a public API
* The app should contain several components and include a router with several 'pages'.
* Be deployed online 

## Technologies 💻
* React.js & React Router
* HTML5
* CSS3
* Bulma 
* FontAwesome 
* Git & GitHub
* Insomnia 
* Axios
* Animate CSS 
* [Final Space API](https://finalspaceapi.com/)

## Approach ✏️
We first researched a number of APIs and decided to showcase data based on the TV show, Final Space.

#### Day 1
* utilised Insomnia to examine what data we would receive from the various endpoints 
* discussed how we would show this on the front end. 

#### Day 2
* Constructed all of the components we required 
* Set up the routes for the components

#### Day 3 (AM)
* Worked on styling 
* Refactored code 

### Routes
The routes to the various pages were built with React as well as BrowserRouter, Switch and Route from React-Router-DOM.

```js
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
#### Homepage
The homepage included a hero image along with two buttons. The first button sends the user to all of the show's characters, while the second button brings the user to all of the show's episodes.

<img width="1430" alt="Screenshot 2021-11-14 at 17 16 53" src="https://user-images.githubusercontent.com/59033443/141691253-7a066424-cae5-44c1-a04e-8bf3cc5f91cb.png">

#### All Characters 
To display all of the show's characters, we used an axios request from the API within a `useEffect` and modified the hook's state. We then used a map function on the array of characters to display them on the website, and they were styled as cards with Bulma. The cards were then wrapped in a link, allowing the user to click on the card to learn more about the particular characters and episodes.

```js
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
#### Search
We gave the user the ability to search for characters by adding a search option. To do this, we utilised a `useEffect` to search through the characters array and return the character that matched what the user typed into the search field.

```js
useEffect(() => {
    const filteredCharac = () => {
      const regexSearch = new RegExp(search, 'i') 
      const filtered = characterArray.filter(character => {
        return regexSearch.test(character.name)
      })
      setFiltered(filtered)
    } 
    filteredCharac()
  }, [search])
```

## Wins 🏆
* Successfully mapping data from a public API
