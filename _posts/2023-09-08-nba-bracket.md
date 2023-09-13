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
    <script>
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
                return data.data; // Extract the player data from the response
            } catch (error) {
                console.error(error);
            }
        }
        async function displayRandomPlayers() {
            const playerData = await fetchRandomPlayers();
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