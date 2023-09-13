---
toc: true
comments: false
layout: post
title: NBA Ranking
description: Rank some randomly generated NBA players
type: tangibles
courses: { csa: {week: 3} }
permalink: /nba-bracket
---

<html>
<head>
    <title>Random NBA Players</title>
</head>
<body>
    <h1>Random NBA Players</h1>
    <button onclick="displayRandomPlayers()">Get 10 Random Players</button>
    <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Position</th>
                <th>Team</th>
            </tr>
        </thead>
        <tbody id="playerTableBody">
            <!-- Table rows will be added here -->
        </tbody>
    </table>
    <form id="myForm">
        <label for="textBox">Rank These Players</label>
        <input type="text" id="textBox" name="textBox">
        <button type="submit">Submit</button>
    </form>
    <div id="rankedPlayers">
        <h2>Ranked Players</h2>
        <ul id="rankedList"></ul>
    </div>
    <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Position</th>
                <th>Team</th>
            </tr>
        </thead>
        <tbody id="rankedPlayersTableBody">
            <!-- Ranked players will be added here -->
        </tbody>
    </table>
    <script>
        // Global array to store player rankings
        const playerRankings = [];
        
        // Global array to store player data
        let playerDataArray = [];

        function handleFormSubmit() {
            const form = document.getElementById('myForm');
            form.addEventListener('submit', function(event) {
                event.preventDefault(); // Prevent the form from submitting and refreshing the page
                const textBoxValue = document.getElementById('textBox').value;
                // Assuming textBoxValue contains the player's name or ID
                playerRankings.push(textBoxValue); // Store the ranking in the array
                rearrangeTable(); // Rearrange the table based on rankings
            });
        }

        function rearrangeTable() {
            // Sort the playerDataArray based on the order of rankings entered by the user
            playerDataArray.sort((a, b) => {
                const aIndex = playerRankings.indexOf(a.full_name);
                const bIndex = playerRankings.indexOf(b.full_name);
                return aIndex - bIndex;
            });

            // Update the rankedPlayersTableBody with the sorted data
            const rankedPlayersTableBody = document.getElementById('rankedPlayersTableBody');
            rankedPlayersTableBody.innerHTML = '';

            for (const player of playerDataArray) {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${player.id}</td>
                    <td>${player.first_name}</td>
                    <td>${player.last_name}</td>
                    <td>${player.position}</td>
                    <td>${player.team.full_name}</td>
                `;
                rankedPlayersTableBody.appendChild(row);
            }
        }

        // Call the function to set up the form handling and initialize the ranked players list and table
        handleFormSubmit();

        async function fetchRandomPlayers() {
            const url = 'https://free-nba.p.rapidapi.com/players?page=0&per_page=100'; // Increase per_page for more choices
            const options = {
                method: 'GET',
                headers: {
                    'X-RapidAPI-Key': 'f9e05fed4fmshda97f8933d9e076p192198jsn5018f8cb51c3',
                    'X-RapidAPI-Host': 'free-nba.p.rapidapi.com'
                }
            };
            try {
                const response = await fetch(url, options);
                const data = await response.json();
                return data.data; // Extract the player data from the response
            } catch (error) {
                console.error(error);
            }
        }

        async function displayRandomPlayers() {
            const playerData = await fetchRandomPlayers();
            playerDataArray = playerData; // Store the player data for later use
            if (playerData) {
                const playerTableBody = document.getElementById('playerTableBody');
                playerTableBody.innerHTML = ''; // Clear previous rows
                for (let i = 0; i < 10; i++) {
                    const randomIndex = Math.floor(Math.random() * playerData.length);
                    const randomPlayer = playerData[randomIndex];
                    // Create a new row for the random player
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${randomPlayer.id}</td>
                        <td>${randomPlayer.first_name}</td>
                        <td>${randomPlayer.last_name}</td>
                        <td>${randomPlayer.position}</td>
                        <td>${randomPlayer.team.full_name}</td>
                    `;
                    playerTableBody.appendChild(row);
                }
            }
        }
    </script>
</body>
</html>

**Project Title:** NBA Player Ranking 

**Project Description:**
Our project involves utilizing movie-related data through an appropriate API, processing and integrating this data, and creating a unique visualization or application for our class.

**Project Goals:**
1. To use NBA player data from an API.
2. Practice using JavaScript to create a coherent project containing inputs and outputs.
3. To practice agile methodology and pair programming to maximize project management, organization, and planning.

**Project Team:**
- Tanay Patel
- Paaras Purohit

**Extra Help:**
- Yuri & Shreyas
- ChatGPT

**Project Timeline:**

*Day 1: Project Initiation and Planning*
- Define project objectives and goals.
- Select an appropriate movie-related API.
- Develop a project plan, including a timeline.
- Create a project presentation outline.

*Day 2-3: Data Retrieval and Processing*
- Access the chosen API and set up authentication (if required).
- Retrieve movie-related data, including but not limited to titles, ratings, genres, and release dates.
- Resolve any API fetching issues and adapt the project scope if necessary.
- Develop data processing scripts to clean and format the data for visualization.

*Day 4-5: Visualization Development*
- Choose a visualization or application concept (e.g., interactive movie ratings chart, recommendation system, or movie trivia game).
- Begin developing the chosen concept using appropriate technologies (e.g., JavaScript, Python, HTML/CSS).
- Test and refine the visualization/application for accuracy and functionality.

*Day 6: Agile Methodology and Iterative Programming*
- Implement agile methodology to manage the project efficiently.
- Conduct a sprint meeting to review progress and address any issues.
- Make iterative improvements based on feedback received during the sprint review.

*Day 7: Documentation and Presentation*
- Create detailed documentation explaining the project's architecture, code, and data sources.
- Prepare a visually appealing presentation summarizing the project's journey, challenges, and outcomes.
- Practice the presentation and address any gaps or areas for improvement.

*Day 8: Final Presentation and Submission*
- Present the project to the class, highlighting key aspects, challenges, and lessons learned.
- Address any questions or feedback from the class.
- Submit the project presentation, documentation, and code.

**Lessons Learned:**
- Maintain open and regular communication between pair about project progress.
- Plan for hiccups and be prepared to have to change initial plans to successfully complete project.
