# TITLE: “Meme Generator: Beta”

#### Report
##### For Project Phase-I of C2C-SVCE

## Team: Classy Devs


## Team Members

Rasswanth S, 3rd yr, CSE
Rohith PR, 3rd yr, CSE
Sai Hari Krishna 2nd yr, CSE


# ABSTRACT

*App that gets the help of External API for getting Meme related images and Meme Template, and an inbuilt text editor for generating Meme in an easy way. A simple and not a complex Web Application, A very simple User Interface with not so many fancy functionality, focused for providing a responsive Web Application.

Further developments are possible in Native Mobile Application development and designing an independent “web crawler” for collecting Meme images without explicit use of API.*


# INTRODUCTION

## Technology Stack:
We are following the popular MERN stack development for developing the web app but this app doesn't require any database or Backend. 

 Back-end Framework:
 Express Js
 Front-end Framework:
 React Js
 API:
 Imgflip API

We will be using Imgflip open source picture API for generating random pictures. The user will be using different fonts for memes so we will be embedding the different fonts that are available.

Much Less Complexity:
Through this simple implementation, more focused only on meme creation and nothing much more.

Further Developments:
Font manipulation, Choosing an image from a gallery of images, user uploading and using the image of his/her choice, Native Mobile Application, Image manipulation.

Font Manipulation: Font can be changed, color of fonts can be changed, size and font family can be changed. 

Image Gallery: Displaying the Top picked images in the Meme Editor page.

Image Manipulation: Customization of Image, Cropping, Flipping, Rotation etc..


# Code Explanation

Starting with our index.html we have a <root> element to which the index.js will get embedded. As index.js

```
ReactDOM.render(
    <App />,document.getElementById('root')
);
```

Then going to index.js, there is a <App/> component which is getting rendered.

```
function App() {
    return (
        <div>
            <Header />
            <MemeGenerator />
        </div>
    )
}

export default App
```

The App element consist of two other components ```<Header/>``` and ```<MemeGenerator/>``` where the Header component is responsible for the Page Header that consist of an image and the Page Heading.

```
function Header() {
    return (
        <header>
            <img 
                src="http://www.pngall.com/wp-content/uploads/2016/05/Trollface.png" 
                alt="Problem?"
            />
            <p>Meme Generator</p>
        </header>
    )
}

export default Header
```

The MemeGenarator component act as soul of the Application which has the core functionality of the app.

Using React component Class and componentDidMount function we are getting the image from the Imgflip API.

```
class MemeGenerator extends Component {
    constructor() {
        super()
        this.state = {
            topText: "",
            bottomText: "",
            randomImg: "http://i.imgflip.com/1bij.jpg",
            allMemeImgs: []
        }
        this.handleChange = this.handleChange.bind(this)
        this.handleSubmit = this.handleSubmit.bind(this)
    }
    
    componentDidMount() {
        fetch("https://api.imgflip.com/get_memes")
            .then(response => response.json())
            .then(response => {
                const {memes} = response.data
                this.setState({ allMemeImgs: memes })
            })
    }
```


Then finally we use the render function to render the image in the page.

```
render() {
        return (
            <div>
                <form className="meme-form" onSubmit={this.handleSubmit}>
                    <input 
                        type="text"
                        name="topText"
                        placeholder="Top Text"
                        value={this.state.topText}
                        onChange={this.handleChange}
                    /> 
                    <input 
                        type="text"
                        name="bottomText"
                        placeholder="Bottom Text"
                        value={this.state.bottomText}
                        onChange={this.handleChange}
                    /> 
                
                    <button>Gen</button>
                </form>
                <div className="meme">
                    <img src={this.state.randomImg} alt="" />
                    <h2 className="top">{this.state.topText}</h2>
                    <h2 className="bottom">{this.state.bottomText}</h2>
                </div>
            </div>
        )
    }
```

The handleChange() and handleSubmit() function sets the TOP and BOTTOM text of the Image.

```
handleChange(event) {
        const {name, value} = event.target
        this.setState({ [name]: value })
    }
    
handleSubmit(event) {
        event.preventDefault()
        const randNum = Math.floor(Math.random() * this.state.allMemeImgs.length)
        const randMemeImg = this.state.allMemeImgs[randNum].url
        this.setState({ randomImg: randMemeImg })
    }
```


### Hence these are the basic functionality behind the Meme Generator: Beta.


## Reference: These are the resources that we have referred while making this Application 
##### https://www.youtube.com/watch?v=DLX62G4lc44, https://imgflip.com/memegenerator, https://css-tricks.com/creating-your-own-meme-generator/ 


## Github Url : https://github.com/Compute-2-Compete-SVCE/Classy-Devs