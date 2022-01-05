# Final Space 👾 - Front-End React Project

by [Gayatri](https://github.com/gayatrirajgor) and [Ricardo](https://github.com/rjriverac)

## Table of Contents
|No. | Content                      | 
|----|------------------------------|
|1   | [Project Overview](#overview)|
|2   | [Project Brief](#brief)      |  
|3   | [Technologies Used](#tech)   |
|4   | [Concept](#concept)          |
|5   | [Approach](#approach)        |
|6   | [Wins & Challenges](#wins)   |
|7   | [Future Ideas](#ideas)       |
|8   | [Result](#result)

<a name="overview"></a>
## 1. Overview
For my second project on the Software Engineering Immersive at General Assembly, I was assigned a 48-hour paired hackathon to design a React application that uses a public API.

This was deployed via Netlify and can be accessed [here](https://final-space-project.netlify.app/).

<a name="brief"></a>
## 2. Brief 📃
* Build a React application that consumes a public API
* The app should contain several components and include a router with several 'pages'.
* Be deployed online 

<a name="tech"></a>
## 3. Technologies 💻
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

<a name="concept"></a>
## 4. Concept 🧐
The idea behind this project was to showcase information on the characters from the show Final Space as well as information about the episodes. All of the data presented was obtained from a public API.

<a name="approach"></a>
## 5. Approach ✏️

### Day 1
We first researched a number of APIs and decided to showcase data based on the TV show, Final Space. After deciding on the API, we utilised Insomnia to examine what data we would receive from the various endpoints and discussed how we would show this on the front end. 

### Day 2
On the second day, we constructed all of the components we required and also set up the routes for them.

### Day 3 (AM)
On the day of our submission, we spent the morning working on styling and refactoring code. 

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
* [Home](#home)
* [Characters](#characters) (display all characters)
* [Episodes](#episodes) (display all episodes)
* [Individual Character](#character) (displays information about individual character)
* [Individual Epsiode](#episode) (displays information about individual episode)

<a name="home"></a>
### Homepage
The homepage included a hero image along with two buttons. The first button sends the user to all of the show's characters, while the second button brings the user to all of the show's episodes.

<a name="characters"></a>
### All Characters 
To display all of the show's characters, I used an Axios request from the API within a `useEffect` and modified the hook's state. I then used a map function on the array of characters to display them on the website, and they were styled as cards with Bulma. The cards were then wrapped in a link, allowing the user to click on the card to learn more about the particular characters and episodes.

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
The screenshot below shows that when a user types 'q' into the search bar, the characters that begin with Q are retrieved.

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
<img width="1431" alt="Screenshot 2021-12-20 at 19 08 07" src="https://user-images.githubusercontent.com/59033443/146819612-b89a438c-f639-4b30-99ca-007a4f9f198f.png">

<a name="episodes"></a>
### All Episodes
We utilised the same approach to display all of the episodes of the show as we did to showcase all of the characters.
```js
useEffect(() => {
    const getData = async() => {
      try {
        const { data } = await axios.get('https://finalspaceapi.com/api/v0/episode')
        setEpisodeArray(data)
      } catch (error) {
        console.log(error)
      }
    }
    getData()
  },[])
```

<a name="character"></a>
### Individual Characters Page
The `id` was passed through the `useEffect` to get the data about the individual characters, and we had to get the data from another endpoint to get the quotes said by those characters. Once all the data had been received, they were styled as tiles with Bulma.
```js
useEffect(() => {
    const getData = async () => {
      try {
        const { data } = await axios.get(`https://finalspaceapi.com/api/v0/character/${id}`)
        setCharacter(data)
      } catch (error) {
        console.log(error)
      }
    }
    const getQuotes = async () => {
      try {
        const { data } = await axios.get('https://finalspaceapi.com/api/v0/quote')
        setQuotes(data)
      } catch (error) {
        console.log(error)
      }
    }
    getData()
    getQuotes()
  }, [id])
```
In order to display the quotes on the front end, we utilised `filter` to return quotes said by those characters.
```js
{quotes.filter(quote => quote.by === character.name).map((quote,index)=> {
                  return (
                    <li key={index}>{quote.quote}</li>
                  )
})}
```

<a name="episode"></a>
### Individual Episodes Page
We utilised an Axios GET request to get the information of the episode by the id to retrieve the data about a particular episode. The retrieved data was then shown on the front end, as seen below.

```js
<div className="column is-half animate__animated animate__slow animate__slideInLeft">
                    <figure className="image" id="episode-image">
                      <img src={episode.img_url} alt={episode.name}/>
                    </figure>
                  </div>
                  <div className="column is-half animate__animated animate__slow animate__slideInRight">
                    <div className="tile is-ancestor is-vertical">
                      <div className="tile is-parent">
                        <div className="tile is-child box">
                          <p className="title has-text-weight-normal is-6"><i className="fas fa-video"></i> Directed by:</p>
                          <p>{episode.director}</p>
                        </div>
                        <div className="tile is-child box">
                          <p className="title has-text-weight-normal is-6"><i className="fas fa-broadcast-tower"></i> Air Date</p>
                          <p>{episode.air_date}</p>
                        </div>
                      </div>
                      <div className="tile is-parent">
                        <div className="tile is-child box">
                          <p className="title is-6 has-text-weight-normal"><i className="fas fa-pencil-alt"></i> Written By</p>
                          <p>{episode.writer}</p>
                        </div>
                      </div>
```

<a name="wins"></a>
## 6. Wins & Challenges 🏆
### Wins
* Successfully mapping data from a public API
* After only a week of learning React, I was proud of the functionality we were able to produce in the two days we worked on this project.

### Challenges 
* I was using Bulma for the first time throughout this project, thus it took some time to become familiar with the framework. However, after I realised how it worked, I could see the advantages of using it for styling, such as Bulma being lightweight as well as simple to customise the framework. 

<a name="ideas"></a>
## 7. Future Ideas 💭
* Mobile responsive 
* Add filter features

<a name="result"></a>
## 8. Result
### Homepage
<img width="1430" alt="Screenshot 2021-11-14 at 17 16 53" src="https://user-images.githubusercontent.com/59033443/141691253-7a066424-cae5-44c1-a04e-8bf3cc5f91cb.png">

### All Characters Page
<img width="1433" alt="Screenshot 2021-12-20 at 19 06 47" src="https://user-images.githubusercontent.com/59033443/146819523-6ee83738-8d7d-4099-90a2-91a6642692be.png">

### All Episodes Page
<img width="1694" alt="Screenshot 2021-12-21 at 17 50 16" src="https://user-images.githubusercontent.com/59033443/146975745-399082ab-cbd0-4a73-8ad2-210632ed2b0c.png">

### Individual Character Page
<img width="1671" alt="Screenshot 2021-12-21 at 17 22 05" src="https://user-images.githubusercontent.com/59033443/146972339-2c318540-ada5-491b-99f8-e310ace8ab97.png">

### Individual Episode Page

![Screenshot 2021-12-21 at 21 52 23](https://user-images.githubusercontent.com/59033443/147002227-9686382d-22e4-4975-ab00-4ea53e7331c5.png)
