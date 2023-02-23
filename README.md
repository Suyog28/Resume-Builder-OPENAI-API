# Resume-Builder-OPENAI-API

# Resume-Builder-OPENAI-API

Creating a resume builder with React, NodeJS and AI 🚀

#

javascript

#

programming

#

tutorial

#

react
TL;DR
In this article, you'll learn how to create a resume builder using React, Node.js, and the OpenAI API.
What's better to look for a job and say you have build a job resume builder with AI to do so? 🤩

A small request 🥺
I produce content weekly, and your support helps so much to create more content. Please support me by clicking the "Love" button. You probably want to "Save" this article also, so you can just click both buttons. Thank you very very much! ❤️

Click

Introduction to the OpenAI API
GPT-3 is a type of artificial intelligence program developed by OpenAI that is really good at understanding and processing human language. It has been trained on a huge amount of text data from the internet, which allows it to generate high-quality responses to a wide range of language-related tasks.

For this article we will use OpenAI GPT3.
Once the ChatGPT API is out, I will create another article using it 🤗
I have been a big fan of OpenAI from the day they released their first API, I have turned to one of the employees and sent them a nice request to get access to the beta version of GPT3, and I got it 😅

GIFGPT3

That's me in Dec 30, 2020

Novu - the first open-source notification infrastructure
Just a quick background about us. Novu provides a unified API that makes it simple to send notifications through multiple channels, including In-App, Push, Email, SMS, and Chat. With Novu, you can create custom workflows and define conditions for each channel, ensuring that your notifications are delivered in the most effective way possible.

GIFNovu

I would be super happy if you could give us a star! And let me also know in the comments ❤️
https://github.com/novuhq/novu

Project Setup
Here, I'll guide you through creating the project environment for the web application. We'll use React.js for the front end and Node.js for the backend server.

Create the project folder for the web application by running the code below:
mkdir resume-builder
cd resume-builder
mkdir client server
Setting up the Node.js server
Navigate into the server folder and create a package.json file.
cd server & npm init -y
Install Express, Nodemon, and the CORS library.
npm install express cors nodemon
ExpressJS is a fast, minimalist framework that provides several features for building web applications in Node.js, CORS is a Node.js package that allows communication between different domains, and Nodemon is a Node.js tool that automatically restarts the server after detecting file changes.

Create an index.js file - the entry point to the web server.
touch index.js
Set up a Node.js server using Express.js. The code snippet below returns a JSON object when you visit the http://localhost:4000/api in your browser.
//👇🏻index.js
const express = require("express");
const cors = require("cors");
const app = express();
const PORT = 4000;

app.use(express.urlencoded({ extended: true }));
app.use(express.json());
app.use(cors());

app.get("/api", (req, res) => {
res.json({
message: "Hello world",
});
});

app.listen(PORT, () => {
console.log(`Server listening on ${PORT}`);
});
Configure Nodemon by adding the start command to the list of scripts in the package.json file. The code snippet below starts the server using Nodemon.
//In server/package.json

"scripts": {
"test": "echo \"Error: no test specified\" && exit 1",
"start": "nodemon index.js"
},
Congratulations! You can now start the server by using the command below.
npm start
Setting up the React application
Navigate into the client folder via your terminal and create a new React.js project.
cd client
npx create-react-app ./
Install Axios and React Router. React Router is a JavaScript library that enables us to navigate between pages in a React application. Axios is a promise-based Node.js HTTP client for performing asynchronous requests.
npm install axios react-router-dom
Delete the redundant files, such as the logo and the test files from the React app, and update the App.js file to display Hello World as below.
function App() {
return (

<div>
<p>Hello World!</p>
</div>
);
}
export default App;
Navigate into the src/index.css file and copy the code below. It contains all the CSS required for styling this project.
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&display=swap");

- {
  font-family: "Space Grotesk", sans-serif;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  }
  form {
  padding: 10px;
  width: 80%;
  display: flex;
  flex-direction: column;
  }
  input {
  margin-bottom: 15px;
  padding: 10px 20px;
  border-radius: 3px;
  outline: none;
  border: 1px solid #ddd;
  }
  h3 {
  margin: 15px 0;
  }
  button {
  padding: 15px;
  cursor: pointer;
  outline: none;
  background-color: #5d3891;
  border: none;
  color: #f5f5f5;
  font-size: 16px;
  font-weight: bold;
  border-radius: 3px;
  }
  .app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 30px;
  }
  .app > p {
  margin-bottom: 30px;
  }
  .nestedContainer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  }
  .companies {
  display: flex;
  flex-direction: column;
  width: 39%;
  }
  .currentInput {
  width: 95%;
  }
  #photo {
  width: 50%;
  }
  #addBtn {
  background-color: green;
  margin-right: 5px;
  }
  #deleteBtn {
  background-color: red;
  }
  .container {
  min-height: 100vh;
  padding: 30px;
  }
  .header {
  width: 80%;
  margin: 0 auto;
  min-height: 10vh;
  background-color: #e8e2e2;
  padding: 30px;
  border-radius: 3px 3px 0 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  }
  .resumeTitle {
  opacity: 0.6;
  }
  .headerTitle {
  margin-bottom: 15px;
  }
  .resumeImage {
  vertical-align: middle;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  }
  .resumeBody {
  width: 80%;
  margin: 0 auto;
  padding: 30px;
  min-height: 80vh;
  border: 1px solid #e0e0ea;
  }
  .resumeBodyTitle {
  margin-bottom: 5px;
  }
  .resumeBodyContent {
  text-align: justify;
  margin-bottom: 30px;
  }
  Building the application user interface
  Here, we'll create the user interface for the resume builder application to enable users to submit their information and print the AI-generated resume.

Create a components folder within the client/src folder containing the Home.js, Loading.js, Resume.js, ErrorPage.js files.
cd client/src
mkdir components
touch Home.js Loading.js Resume.js ErrorPage.js
From the code snippet above:

The Home.js file renders the form field to enable users to enter the necessary information.
The Loading.js contains the component shown to the user when the request is pending.
The Resume.js displays the AI-generated resume to the user.
The ErrorPage.js is shown when an error occurs.
Update the App.js file to render the components using React Router.
import React from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./components/Home";
import Resume from "./components/Resume";

const App = () => {
return (

<div>
<BrowserRouter>
<Routes>
<Route path='/' element={<Home />} />
<Route path='/resume' element={<Resume />} />
</Routes>
</BrowserRouter>
</div>
);
};

export default App;
The Home page
Here, you'll learn how to build a form layout that can send images via HTTP request and dynamically add and remove input fields.

First, update the Loading component to render the code snippet below, shown to the user when the resume is pending.
import React from "react";

const Loading = () => {
return (

<div className='app'>
<h1>Loading, please wait...</h1>
</div>
);
};

export default Loading;
Next, update the ErrorPage.js file to display the component below when users navigate directly to the resume page.
import React from "react";
import { Link } from "react-router-dom";

const ErrorPage = () => {
return (

<div className='app'>
<h3>
You've not provided your details. Kindly head back to the{" "}
<Link to='/'>homepage</Link>.
</h3>
</div>
);
};

export default ErrorPage;
Copy the code snippet below into the Home.js file
import React, { useState } from "react";
import Loading from "./Loading";

const Home = () => {
const [fullName, setFullName] = useState("");
const [currentPosition, setCurrentPosition] = useState("");
const [currentLength, setCurrentLength] = useState(1);
const [currentTechnologies, setCurrentTechnologies] = useState("");
const [headshot, setHeadshot] = useState(null);
const [loading, setLoading] = useState(false);

    const handleFormSubmit = (e) => {
        e.preventDefault();
        console.log({
            fullName,
            currentPosition,
            currentLength,
            currentTechnologies,
            headshot,
        });
        setLoading(true);
    };
    //👇🏻 Renders the Loading component you submit the form
    if (loading) {
        return <Loading />;
    }
    return (
        <div className='app'>
            <h1>Resume Builder</h1>
            <p>Generate a resume with ChatGPT in few seconds</p>
            <form
                onSubmit={handleFormSubmit}
                method='POST'
                encType='multipart/form-data'
            >
                <label htmlFor='fullName'>Enter your full name</label>
                <input
                    type='text'
                    required
                    name='fullName'
                    id='fullName'
                    value={fullName}
                    onChange={(e) => setFullName(e.target.value)}
                />
                <div className='nestedContainer'>
                    <div>
                        <label htmlFor='currentPosition'>Current Position</label>
                        <input
                            type='text'
                            required
                            name='currentPosition'
                            className='currentInput'
                            value={currentPosition}
                            onChange={(e) => setCurrentPosition(e.target.value)}
                        />
                    </div>
                    <div>
                        <label htmlFor='currentLength'>For how long? (year)</label>
                        <input
                            type='number'
                            required
                            name='currentLength'
                            className='currentInput'
                            value={currentLength}
                            onChange={(e) => setCurrentLength(e.target.value)}
                        />
                    </div>
                    <div>
                        <label htmlFor='currentTechnologies'>Technologies used</label>
                        <input
                            type='text'
                            required
                            name='currentTechnologies'
                            className='currentInput'
                            value={currentTechnologies}
                            onChange={(e) => setCurrentTechnologies(e.target.value)}
                        />
                    </div>
                </div>
                <label htmlFor='photo'>Upload your headshot image</label>
                <input
                    type='file'
                    name='photo'
                    required
                    id='photo'
                    accept='image/x-png,image/jpeg'
                    onChange={(e) => setHeadshot(e.target.files[0])}
                />

                <button>CREATE RESUME</button>
            </form>
        </div>
    );

};

export default Home;
Form

The code snippet renders the form field below. It accepts the full name and current work experience - (year, position, title) and allows the user to upload a headshot image via the form field.

Lastly, you need to accept the user's previous work experience. So, add a new state that holds the array of job descriptions.
const [companyInfo, setCompanyInfo] = useState([{ name: "", position: "" }]);
Add the following functions which help with updating the state.
//👇🏻 updates the state with user's input
const handleAddCompany = () =>
setCompanyInfo([...companyInfo, { name: "", position: "" }]);

//👇🏻 removes a selected item from the list
const handleRemoveCompany = (index) => {
const list = [...companyInfo];
list.splice(index, 1);
setCompanyInfo(list);
};
//👇🏻 updates an item within the list
const handleUpdateCompany = (e, index) => {
const { name, value } = e.target;
const list = [...companyInfo];
list[index][name] = value;
setCompanyInfo(list);
};
The handleAddCompany updates the companyInfo state with the user's input, handleRemoveCompany is used to remove an item from the list of data provided, and the handleUpdateCompany updates the item properties - (name and position) within the list.

Next, render the UI elements for the work experience section.
return (

<div className='app'>
<h3>Companies you've worked at</h3>
<form>
{/_--- other UI tags --- _/}
{companyInfo.map((company, index) => (
<div className='nestedContainer' key={index}>
<div className='companies'>
<label htmlFor='name'>Company Name</label>
<input
type='text'
name='name'
required
onChange={(e) => handleUpdateCompany(e, index)}
/>
</div>
<div className='companies'>
<label htmlFor='position'>Position Held</label>
<input
type='text'
name='position'
required
onChange={(e) => handleUpdateCompany(e, index)}
/>
</div>

                    <div className='btn__group'>
                        {companyInfo.length - 1 === index && companyInfo.length < 4 && (
                            <button id='addBtn' onClick={handleAddCompany}>
                                Add
                            </button>
                        )}
                        {companyInfo.length > 1 && (
                            <button id='deleteBtn' onClick={() => handleRemoveCompany(index)}>
                                Del
                            </button>
                        )}
                    </div>
                </div>
            ))}

            <button>CREATE RESUME</button>
        </form>
    </div>

);
The code snippet maps through the elements within the companyInfo array and displays them on the webpage. The handleUpdateCompany function runs when a user updates the input field, then handleRemoveCompany removes an item from the list of elements, and the handleAddCompany adds a new input field.

GIFResumePage

The Resume page
This page shows the resume generated from the OpenAI API in a printable format. Copy the code below into the Resume.js file. We'll update its content later in this tutorial.
import React from "react";
import ErrorPage from "./ErrorPage";

const Resume = ({ result }) => {
if (JSON.stringify(result) === "{}") {
return <ErrorPage />;
}

    const handlePrint = () => alert("Print Successful!");
    return (
        <>
            <button onClick={handlePrint}>Print Page</button>
            <main className='container'>
                <p>Hello!</p>
            </main>
        </>
    );

};
How to submit images via forms in Node.js
Here, I'll guide you on how to submit the form data to the Node.js server. Since the form contains images, we'll need to set up Multer on the Node.js server.

💡 Multer is a Node.js middleware used for uploading files to the server.

Setting up Multer
Run the code below to install Multer
npm install multer
Ensure the form on the frontend application has the method and encType attributes, because Multer only process forms which are multpart.

<form method="POST" enctype="multipart/form-data"></form>
Import the Multer and the Node.js path packages into the index.js file.
const multer = require("multer");
const path = require("path");
Copy the code below into the index.js to configure Multer.
app.use("/uploads", express.static("uploads"));

const storage = multer.diskStorage({
destination: (req, file, cb) => {
cb(null, "uploads");
},
filename: (req, file, cb) => {
cb(null, Date.now() + path.extname(file.originalname));
},
});

const upload = multer({
storage: storage,
limits: { fileSize: 1024 _ 1024 _ 5 },
});
From the code snippet above:
The app.use() function enables Node.js to serve the contents of an uploads folder. The contents refer to static files such as images, CSS, and JavaScript files.
The storage variable containing multer.diskStorage gives us full control of storing the images. The function above stores the images in the upload folder and renames the image to its upload time (to prevent filename conflicts).
The upload variable passes the configuration to Multer and set a size limit of 5MB for the images.
Create the uploads folder on the server. This is where the images will be saved.
mkdir uploads
How to upload images to a Node.js server
Add a route that accepts all the form inputs from the React app. The upload.single("headshotImage") function adds the image uploaded via the form to the uploads folder.
app.post("/resume/create", upload.single("headshotImage"), async (req, res) => {
const {
fullName,
currentPosition,
currentLength,
currentTechnologies,
workHistory,
} = req.body;

    console.log(req.body);

    res.json({
        message: "Request successful!",
        data: {},
    });

});
Update the handleFormSubmit function within the Home.js component to submit the form data to the Node.js server.
import axios from "axios";

const handleFormSubmit = (e) => {
e.preventDefault();

    const formData = new FormData();
    formData.append("headshotImage", headshot, headshot.name);
    formData.append("fullName", fullName);
    formData.append("currentPosition", currentPosition);
    formData.append("currentLength", currentLength);
    formData.append("currentTechnologies", currentTechnologies);
    formData.append("workHistory", JSON.stringify(companyInfo));
    axios
        .post("http://localhost:4000/resume/create", formData, {})
        .then((res) => {
            if (res.data.message) {
                console.log(res.data.data);
                navigate("/resume");
            }
        })
        .catch((err) => console.error(err));
    setLoading(true);

};
The code snippet above creates a key/value pair representing the form fields and their values which are sent via Axios to the API endpoint on the server. If there is a response, it logs the response and redirect the user to the Resume page.

How to communicate with the OpenAI API in Node.js
In this section, you'll learn how to communicate with the OpenAI API within the Node.js server.
We'll send the user's information to the API to generate a profile summary, job description, and achievements or related activities completed at the previous organisations. To accomplish this:

Install the OpenAI API Node.js library by running the code below.
npm install openai
Log in or create an OpenAI account here.

Click Personal on the navigation bar and select View API keys from the menu bar to create a new secret key.

Nav

Copy the API Key somewhere safe on your computer; we'll use it shortly.

Configure the API by copying the code below into the index.js file.
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
apiKey: "<YOUR_API_KEY>",
});

const openai = new OpenAIApi(configuration);
Create a function that accepts a text (prompt) as a parameter and returns an AI-generated result.
const GPTFunction = async (text) => {
const response = await openai.createCompletion({
model: "text-davinci-003",
prompt: text,
temperature: 0.6,
max_tokens: 250,
top_p: 1,
frequency_penalty: 1,
presence_penalty: 1,
});
return response.data.choices[0].text;
};
The code snippet above uses the text-davinci-003 model to generate an appropriate answer to the prompt. The other key values helps us generate the specific type of response we need.

Update the /resume/create route as done below.
app.post("/resume/create", upload.single("headshotImage"), async (req, res) => {
const {
fullName,
currentPosition,
currentLength,
currentTechnologies,
workHistory, //JSON format
} = req.body;

    const workArray = JSON.parse(workHistory); //an array

    //👇🏻 group the values into an object
    const newEntry = {
        id: generateID(),
        fullName,
        image_url: `http://localhost:4000/uploads/${req.file.filename}`,
        currentPosition,
        currentLength,
        currentTechnologies,
        workHistory: workArray,
    };

});
The code snippet above accepts the form data from the client, converts the workHistory to its original data structure (array), and puts them all into an object.

Next, create the prompts you want to pass into the GPTFunction.
//👇🏻 loops through the items in the workArray and converts them to a string
const remainderText = () => {
let stringText = "";
for (let i = 0; i < workArray.length; i++) {
stringText += ` ${workArray[i].name} as a ${workArray[i].position}.`;
}
return stringText;
};
//👇🏻 The job description prompt
const prompt1 = `I am writing a resume, my details are \n name: ${fullName} \n role: ${currentPosition} (${currentLength} years). \n I write in the technolegies: ${currentTechnologies}. Can you write a 100 words description for the top of the resume(first person writing)?`;
//👇🏻 The job responsibilities prompt
const prompt2 = `I am writing a resume, my details are \n name: ${fullName} \n role: ${currentPosition} (${currentLength} years). \n I write in the technolegies: ${currentTechnologies}. Can you write 10 points for a resume on what I am good at?`;
//👇🏻 The job achievements prompt
const prompt3 = `I am writing a resume, my details are \n name: ${fullName} \n role: ${currentPosition} (${currentLength} years). \n During my years I worked at ${
    workArray.length
} companies. ${remainderText()} \n Can you write me 50 words for each company seperated in numbers of my succession in the company (in first person)?`;

//👇🏻 generate a GPT-3 result
const objective = await GPTFunction(prompt1);
const keypoints = await GPTFunction(prompt2);
const jobResponsibilities = await GPTFunction(prompt3);
//👇🏻 put them into an object
const chatgptData = { objective, keypoints, jobResponsibilities };
//👇🏻log the result
console.log(chatgptData);
From the code snippet above:
The remainderText function loops through the array of work history and returns a string data type of all work experiences.
Then, there are three prompts with instructions on what is needed from the GPT-3 API.
Next, you store the results in an object and log them to the console.
Lastly, return the AI-generated result and the information the users entered. You can also create an array representing the database that stores results as done below.
let database = [];

app.post("/resume/create", upload.single("headshotImage"), async (req, res) => {
//...other code statements
const data = { ...newEntry, ...chatgptData };
database.push(data);

    res.json({
        message: "Request successful!",
        data,
    });

});
Displaying the response from the OpenAI API
In this section, I'll guide you through displaying the results generated from the OpenAI API in a readable and printable format on a web page.

Create a React state within the App.js file. The state will hold the results sent from the Node.js server.
import React, { useState } from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./components/Home";
import Resume from "./components/Resume";

const App = () => {
//👇🏻 state holding the result
const [result, setResult] = useState({});

    return (
        <div>
            <BrowserRouter>
                <Routes>
                    <Route path='/' element={<Home setResult={setResult} />} />
                    <Route path='/resume' element={<Resume result={result} />} />
                </Routes>
            </BrowserRouter>
        </div>
    );

};

export default App;
From the code snippet above, only setResult is passed as a prop into the Home component and only result for the Resume component. setResult updates the value of the result once the form is submitted and the request is successful, while result contains the response retrieved from the server, shown within the Resume component.

Update the result state within the Home component after the form is submitted and the request is successful.
const Home = ({ setResult }) => {
const handleFormSubmit = (e) => {
e.preventDefault();

        //...other code statements
        axios
            .post("http://localhost:4000/resume/create", formData, {})
            .then((res) => {
                if (res.data.message) {
                    //👇🏻 updates the result object
                    setResult(res.data.data);
                    navigate("/resume");
                }
            })
            .catch((err) => console.error(err));
        setLoading(true);
    };
    return <div></div>;

};
Update the Resume component as done below to preview the result within the React app.
import ErrorPage from "./ErrorPage";

const Resume = ({ result }) => {
//👇🏻 function that replaces the new line with a break tag
const replaceWithBr = (string) => {
return string.replace(/\n/g, "<br />");
};

    //👇🏻 returns an error page if the result object is empty
    if (JSON.stringify(result) === "{}") {
        return <ErrorPage />;
    }

    const handlePrint = () => alert("Printing");

    return (
        <>
            <button onClick={handlePrint}>Print Page</button>
            <main className='container' ref={componentRef}>
                <header className='header'>
                    <div>
                        <h1>{result.fullName}</h1>
                        <p className='resumeTitle headerTitle'>
                            {result.currentPosition} ({result.currentTechnologies})
                        </p>
                        <p className='resumeTitle'>
                            {result.currentLength}year(s) work experience
                        </p>
                    </div>
                    <div>
                        <img
                            src={result.image_url}
                            alt={result.fullName}
                            className='resumeImage'
                        />
                    </div>
                </header>
                <div className='resumeBody'>
                    <div>
                        <h2 className='resumeBodyTitle'>PROFILE SUMMARY</h2>
                        <p
                            dangerouslySetInnerHTML={{
                                __html: replaceWithBr(result.objective),
                            }}
                            className='resumeBodyContent'
                        />
                    </div>
                    <div>
                        <h2 className='resumeBodyTitle'>WORK HISTORY</h2>
                        {result.workHistory.map((work) => (
                            <p className='resumeBodyContent' key={work.name}>
                                <span style={{ fontWeight: "bold" }}>{work.name}</span> -{" "}
                                {work.position}
                            </p>
                        ))}
                    </div>
                    <div>
                        <h2 className='resumeBodyTitle'>JOB PROFILE</h2>
                        <p
                            dangerouslySetInnerHTML={{
                                __html: replaceWithBr(result.jobResponsibilities),
                            }}
                            className='resumeBodyContent'
                        />
                    </div>
                    <div>
                        <h2 className='resumeBodyTitle'>JOB RESPONSIBILITIES</h2>
                        <p
                            dangerouslySetInnerHTML={{
                                __html: replaceWithBr(result.keypoints),
                            }}
                            className='resumeBodyContent'
                        />
                    </div>
                </div>
            </main>
        </>
    );

};
The code snippet above displays the result on the webpage according to the specified layout. The function replaceWithBr replaces every new line (\n) with a break tag, and the handlePrint function will enable users to print the resume.

How to print React pages using the React-to-print package
Here, you'll learn how to add a print button to the web page that enables users to print the resume via the React-to-print package.

💡 React-to-print is a simple JavaScript package that enables you to print the content of a React component without tampering with the component CSS styles.

Run the code below to install the package
npm install react-to-print
Import the library within the Resume.js file and add the useRef hook.
import { useReactToPrint } from "react-to-print";
import React, { useRef } from "react";
Update the Resume.js file as done below.
const Resume = ({ result }) => {
const componentRef = useRef();

    const handlePrint = useReactToPrint({
        content: () => componentRef.current,
        documentTitle: `${result.fullName} Resume`,
        onAfterPrint: () => alert("Print Successful!"),
    });
    //...other function statements
    return (
        <>
            <button onClick={handlePrint}>Print Page</button>
            <main className='container' ref={componentRef}>
                {/*---other code statements---*/}
            </main>
        </>
    );

};
The handlePrint function prints the elements within the componentRef - main tag, sets the document's name to the user's full name, and runs the alert function when a user prints the form.

Congratulations! You've completed the project for this tutorial.

Here is a sample of the result gotten from the project:

GIFResult

Conclusion
So far, you've learnt:

what OpenAI GPT-3 is,
how to upload images via forms in a Node.js and React.js application,
how to interact with the OpenAI GPT-3 API, and
how to print React web pages via the React-to-print library.
This tutorial walks you through an example of an application you can build using the OpenAI API. With the API, you can create powerful applications useful in various fields, such as translators, Q&A, code explanation or generation, etc.

The source code for this tutorial is available here:

https://github.com/novuhq/blog/tree/main/resume-builder-with-react-chatgpt-nodejs
