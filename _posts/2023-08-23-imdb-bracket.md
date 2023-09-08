---
toc: true
comments: false
layout: post
title: IMDb Movie Bracket
description: The basic layout of how our project will be
type: tangibles
courses: { csa: {week: 3} }
permalink: /imdb-bracket
---

<html>
<body>
    <h1>Which Movie Is Better?</h1>
    <input type="text" id="textInput" placeholder="Which is better?">
    <button onclick="addRow()">Make Your Choice</button>
    <table id="whichMovieIsBetter" border="1">
        <tr>
            <th>Data</th>
        </tr>
    </table>
    <table border="1">
        <thead>
            <tr>
                <th>Rank</th>
                <th>Title</th>
                <th>Description</th>
                <th>Image</th>
                <th>Genre</th>
                <th>Thumbnail</th>
                <th>Rating</th>
                <th>Year</th>
            </tr>
        </thead>
        <tbody id="tableBody">
            <!-- Data will be inserted here -->
        </tbody>
    </table>
    <script>
        async function fetchData() {
            const url = 'https://imdb-top-100-movies.p.rapidapi.com/';
            const options = {
                method: 'GET',
                headers: {
                    'X-RapidAPI-Key': 'f9e05fed4fmshda97f8933d9e076p192198jsn5018f8cb51c3',
                    'X-RapidAPI-Host': 'imdb-top-100-movies.p.rapidapi.com'
                }
            };
            try {
                const response = await fetch(url, options);
                const data = await response.json();
                const tableBody = document.getElementById('tableBody');
                // Shuffle the data array to get a random order
                shuffleArray(data);
                // Display only the first two movies
                for (let i = 0; i < 2; i++) {
                    const item = data[i];
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${item.rank}</td>
                        <td>${item.title}</td>
                        <td>${item.description}</td>
                        <td><img src="${item.image}" alt="${item.title}" width="100"></td>
                        <td>${item.genre}</td>
                        <td><img src="${item.thumbnail}" alt="${item.title} Thumbnail" width="50"></td>
                        <td>${item.rating}</td>
                        <td>${item.year}</td>
                    `;
                    tableBody.appendChild(row);
                }
            } catch (error) {
                console.error(error);
            }
        }
        // Function to shuffle an array randomly
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }
        function addRow() {
            var textInput = document.getElementById("textInput");
            var table = document.getElementById("whichMovieIsBetter");
            if (textInput.value.trim() !== "") {
                fetchData();
                var newRow = table.insertRow(table.rows.length);
                var cell = newRow.insertCell(0);
                cell.innerHTML = textInput.value;
                textInput.value = "";
            } else {
                alert("Please enter some data.");
            }
        }
        // Call the fetchData function to initiate the API request
        fetchData();
    </script>
</body>
</html>

**Project Title:** IMDb Movie Bracket by Paaras Purohit & Tanay Patel

**Project Description:**
Our project involves utilizing movie-related data through an appropriate API, processing and integrating this data, and creating a unique visualization or application for our class.

**Project Goals:**
1. To explore and utilize movie-related data from an API.
2. To develop a unique and visually appealing project for our class.
3. To practice agile methodology and iterative programming for effective project management.

**Project Team:**
- Paaras Purohit
- Tanay Patel

**Extra Help:**
- Mr. Mortensen
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

**Risk Assessment:**
- Potential API limitations and fetching issues.
- Partner scheduling conflicts and communication challenges.
- Changes in project scope due to API limitations.
- Technical challenges during the development phase.
- Time management issues.

**Mitigation Strategies:**
- Regularly communicate with the teacher to provide updates and seek guidance.
- Utilize agile methodology to adapt to changing circumstances.
- Seek alternative data sources if API limitations persist.
- Prioritize efficient time management and communication within the team.
- Maintain a backup plan in case of technical challenges.

**Lessons Learned:**
- Maintain open and regular communication with the teacher about project progress.
- Plan for contingencies and be prepared to adapt to unexpected challenges.
- Agile methodology and iterative programming can help manage dynamic projects effectively.