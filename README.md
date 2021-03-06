# Focus 
## Git repo for Orbital 2020
##### Level: Gemini
###### By Tan Pinxi & Amelia Yamato

### Problem: 
Currently, many teenagers and young adults are highly distracted by social media and entertainment websites when working on their computers. With study and work commitments, it is important for one to manage their time well, and the best way to start is by being conscious of how they're spending their time online.

Currently, there is no available website or software to help users see how much time is wasted on social media or other websites, let alone an analytics dashboard that summarises everything concisely. Therefore, self-imposed goals are hard to reinforce. Moreover, the current solutions are too manual, such as asking users to self-record, which may be unsustainable in the long-term for users who need it most. 

### Solution:
Instead of a manual recording process that may be inaccurate, we decided to develop a fully automated, background process to monitor website usage on desktop. This means that there is no additional work for users - just download, setup, and let it work in the background. The desktop browser plugin is passive and non-invasive, only monitoring pre-approved websites.
We will also have a user-facing control panel to view usage statistics, ensuring that it is simple to use.

### User Stories: 
Gaby has a problem focusing on work when she uses her computer and realises that she has this issue of self-discipline. For a first step, she decides to keep track of the time she spends on various websites. Hence, she finds Focus and selects Youtube and Facebook as her "flagged" websites, and at the end of each day, she goes to the analytics dashboard to get a sense of how much time she spends on each website. After seeing that she spends a whopping 4 hours on Youtube, she decides to make a conscious effort to decrease her usage. 


### Execution: 

#### Functional Prototype (Product Demo)

#### Product Demo 
[Link to product demo](https://youtu.be/J1Ob3R9aZXE)

#### Screenshots of Application 

![dashboard](https://imgur.com/8bm2gSW.jpg)

The dashboard displays the usage statistics collected from our browser extension so users can view their usage breakdowns and daily usage for each site. 

![settings](https://imgur.com/td4RqRJ.jpg)

Users can view the list of monitored sites on the settings page (implemented), and will also be able to add and delete sites (implemented).

#### Database
Contains files to setup MySQL database, which is currently hosted on localhost. RequestHandler provides API for the extension and dashboard to access the database via XMLHttpRequests.

#### Extension
The browser extension is hosted on TamperMonkey and uses both standard HTML/javascript functions as well as functions provided by GreaseMonkey under the GM library.

#### Interactive Dashboard (User Interface)
We are using an open-source modular framework, Cube.js, to build the main analytics dashboard / control panel for the users. Cube.js is run back-end as a service, managing the connection to a mySQL database and pre-aggregation, query-queueing and more. Cube.js also exposes an API for our front-end application, allowing us to build customised dashboards and other analytics features. Using ReactJS, we are able to customise the user interface of the analytics dashboard.

### Internal Use

Github for version control and collaboration. 

### Feature Breakdown 

* Extension 

Helps to keep track of the usage time for each website. This data is then stored in a mySQL database used for the dashboard's backend.

* Interactive Analytics Dashboard 

Allows users to see their usage time on websites, which updates when the page is refreshed.

* Setting website usage restriction

Allows users to key in the time limit they'd like to keep their usage on a certain website to.


### Why this product satisfies User Needs:

Since the main intention of the browser plug-in is to make users more aware of their usage of certain websites and make them conscious of how they are spending their time, rather than explicitly *limiting* usage times, we believe that the interactive and user-friendly dashboard will be able to achieve this. 

Though there may be existing products that help users track their screen time in-browser, they either more manual to start the tracking (Toggl app) or does not provide a usage breakdown by website. Hence, by integrating a browser plugin with an interactive web application, we are able to satisfy the needs of users. 

### How we evaluated our solution:

1. User focus group / interview + Usability testing 

We gathered a group of our 10 friends and walked them through the installation instructions for the web application, and how to launch the webpage. We focused on making sure that out solution was easy for users to set up and use, so that they would want to keep using it. This is the main point of our product, ensuring the ease of monitoring website usage time so that users will build a sustainable habit.

**Key Feedback**

* Dashboard was intuitive and easy to understand, with a nice user interface. 
* Data presented on the dashboard would look better as graphs, rather than pie charts.
 * **Initially**, we had used pie charts to show the usage time breakdown by website, but that proved to be difficult to read when some websites were used       relatively far less than the rest.
* Usage times were accurate down to the minute
* Compared the timing reflected on the dashboard with a manual phone timer when the user was on a webpage. The timings recorded with the plugin was accurate.

2. Survey 

Surveyed friends by posting polls on social media about features that they would prefer to have in a platform like Focus. 88% responded that the interactive dashboard would be sufficient to understand their website usages, and the remaining 12% shared that they would like to have a pop-up window or reminder that prompts them when they are nearing their self-imposed limit. 

 
3. Self-evaluation

Personally, we found the dashboard easy to read and navigate. However, after using it, we decided to make it more interactive for users by allowing them to input the websites that they wanted to flag via a tab where they can insert their own websites. Hence, we created a tab that allows users to input up to 20 websites of their own choice that they'd like to flag. 


### Installation Instructions: 

If you'd like to test the web application on your own device, please follow these installation instructions: 

1. Clone this repository

```git clone https://github.com/FizzyAgent/Orbital2020.git```

2. Install node, npm and mySQL

```
brew install node
npm install -g cubejs-cli
brew install mySQL
```

3. Under Database folder
    1. Run focus.sql to setup the MySQL database
    1. Create a .env file with the following information:
```
DB_HOST=localhost
DB_USER=<username>
DB_PASS=<password>
```

4. Run the following command in the project and focus-dashboard directories

```npm install```

5. Install the TamperMonkey chrome extension from [here](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo) and deploy the Focus.js script found under Extension

6. Go to the Database directory and run the Express server

```node RequestHandler.js```

7. Go to the focus-dashboard directory and run Cube-js

```npm run dev```

8. Go to the focus-dashboard\dashboard-app directory and run the react-app

```npm start```

### Feature Updates After Milestone 2 

* Custom website selection 

Allows users to input the sites that they'd like to flag. This allows any website to be added to a "watch list", instead of just social media sites.
Currently, the user can select a list of common "distracting" websites from a pre-defined list. By milestone 3, we hope to add the functionality of allowing the user to input what sites they'd like to monitor on their own.

* Implement data restriction

Do data pre-processing to make sure that no website usage timings from more than a week ago are in the dashboard or else it would be too bloated.

* Ability to change time range when viewing website usage 

Allowing the user to see their website usage for a week-long period as well. 

* Allows users to input their desired time limit 

Text box allows users to input the time limit they would like to keep to for each specified website.


### Potential Additional Features 

* Pop-up window: Reminder when the user is reaching the time limit

Since our target audience for the application are people who would like to limit their usage on certain flagged sites, we would like to take it further by prompting the user to reduce their usage if their screen time or time on a certain website reaches a certain level. This can possibly be in the form of a reminder.

* Blocking those specific websites once the user has exceeded a certain number of hours on it

### Link to Log

[Orbital Project Log](https://docs.google.com/spreadsheets/d/1SRgkBZBMHGSurudhpTh65sO5Hk9Beoih99OlxObK6D8/edit?usp=sharing)

**Total Hours:**

* Amelia: 143
* Pinxi: 150


