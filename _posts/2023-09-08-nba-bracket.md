---
toc: true
comments: false
layout: post
title: NBA Movie Bracket
description: The basic layout of how our project will be
type: tangibles
courses: { csa: {week: 3} }
permalink: /nba-bracket
---

<html>
<head>
    <style>
        th.sorted-asc::after {
            content: " ▲";
        }
        th.sorted-desc::after {
            content: " ▼";
        }
    </style>
</head>
<body>
    <h1>Random NBA Players</h1>
    <button onclick="displayRandomPlayers()">Get 10 Random Players</button>
    <table>
        <thead>
            <tr>
                <th onclick="sortTable(0)">ID</th>
                <th onclick="sortTable(1)">First Name</th>
                <th onclick="sortTable(2)">Last Name</th>
                <th onclick="sortTable(3)">Position</th>
                <th onclick="sortTable(4)">Team</th>
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
    <script>
        let playerData = []; // Store player data globally for sorting
        function handleFormSubmit() {
            const form = document.getElementById('myForm');
            const submittedTextSpan = document.getElementById('submittedText');
            form.addEventListener('submit', function(event) {
                event.preventDefault(); // Prevent the form from submitting and refreshing the page
                const textBoxValue = document.getElementById('textBox').value;
                submittedTextSpan.textContent = textBoxValue;
            });
        }
        // Call the function to set up the form handling
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
                playerData = data.data; // Store player data globally
            } catch (error) {
                console.error(error);
            }
        }
        async function displayRandomPlayers() {
            await fetchRandomPlayers();
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
        function sortTable(columnIndex) {
            const table = document.querySelector('table');
            const rows = Array.from(table.getElementsByTagName('tr'));
            const isAscending = table.rows[0].cells[columnIndex].classList.contains('sorted-asc');
            // Remove sorting classes from all columns
            table.querySelectorAll('th').forEach(th => {
                th.classList.remove('sorted-asc', 'sorted-desc');
            });
            // Sort the rows based on the selected column
            rows.sort((a, b) => {
                const cellA = a.cells[columnIndex].textContent.trim();
                const cellB = b.cells[columnIndex].textContent.trim();
                return isAscending ? cellA.localeCompare(cellB) : cellB.localeCompare(cellA);
            });
            // Add sorting class to the clicked column
            table.rows[0].cells[columnIndex].classList.add(isAscending ? 'sorted-desc' : 'sorted-asc');
            // Rebuild the table with sorted rows
            for (let i = 0; i < rows.length; i++) {
                table.tBodies[0].appendChild(rows[i]);
            }
        }
    </script>
</body>
</html>

**Project Title:** NBA Player Ranking Experiment

**Project Description:**
Our project aimed to utilize NBA player data from an appropriate API, process and integrate this data, and attempt to create a unique visualization or application for our class to rank players based on user input. However, we encountered numerous open-ended challenges in the process.

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
- Define project objectives and goals, including the intention to rank players based on user input.
- Select an appropriate NBA player data API.
- Develop a project plan, including a timeline, with an emphasis on experimental aspects.
- Create a project presentation outline highlighting our intent to rank players.

*Day 2-3: Data Retrieval and Processing*
- Access the chosen NBA player data API and set up authentication (if required).
- Retrieve NBA player-related data, including but not limited to player names, statistics, and team affiliations.
- Encounter challenges in fetching and processing data due to its complexity and variability.
- Realize the open-ended nature of the ranking criteria and explore various approaches.

*Day 4-5: Ranking Experimentation*
- Choose a ranking concept (e.g., best players based on performance metrics, strongest players by physical attributes).
- Begin developing the ranking experiment using JavaScript, HTML, and CSS.
- Face difficulties in defining a universal ranking criterion, as "best" or "strongest" could have multiple interpretations.
- Experiment with user input and diverse ranking criteria, leading to open-ended errors.

*Day 6: Agile Methodology and Adaptation*
- Implement agile methodology to address ongoing challenges and uncertainties.
- Conduct a sprint meeting to discuss our struggles and potential directions.
- Acknowledge that the open-ended nature of player ranking may not yield a single, definitive result.

*Day 7: Documentation and Presentation*
- Create comprehensive documentation explaining the challenges faced in the project, especially related to ranking criteria.
- Prepare a presentation highlighting our experimentation, errors, and lessons learned.
- Practice the presentation, emphasizing the complexity of ranking NBA players.

*Day 8: Final Presentation*
- Present the project to the class, discussing our attempts to rank players based on user input and the challenges encountered.
- Encourage class discussion on the subjectivity of ranking criteria in the context of NBA players.
- Submit the project presentation, documentation, and code, along with our insights into the complexities of ranking.

**Lessons Learned:**
- Acknowledge the complexity of open-ended tasks, especially when defining subjective criteria like "best" or "strongest."
- Emphasize the importance of adapting project goals and expectations in response to challenges.
- Encourage discussions on the subjective nature of ranking, promoting critical thinking and debate within the class.

- **Peer Feedback:** Yuri and Shreyas told us to make the table more interactive and organized by adding ways to sort the table. We told them about our difficulties with reorganizing the table with the user input, and they suggested this other idea.