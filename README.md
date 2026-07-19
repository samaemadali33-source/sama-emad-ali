<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live Event Theater</title>
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>

    <!-- Countdown Section -->
    <h2>Countdown</h2>
    <input type="number" id="countdownInput" value="10">
    <br><br>
    <button id="startBtn" class="btn">Start</button>
    <button id="stopBtn" class="btn">Stop</button>

    <!-- Username Section -->
    <h2>Username</h2>
    <input type="text" id="usernameInput">
    <p id="usernameFeedback"></p>

    <!-- Menu Section -->
    <ul id="menuList">
        <li>Home</li>
        <li>Movies</li>
        <li>Shows</li>
        <li>Tickets</li>
        <li>Contact</li>
    </ul>
    <p id="selectedOutput">Selected Item: None</p>

    <!-- Keyboard Display Section -->
    <h2>Keyboard Display</h2>
    <div id="keyboardBox"></div>

    <!-- Mouse Zone Section -->
    <h2>Mouse Zone</h2>
    <div id="mouseZone">Mouse Left</div>

    <script src="scripts/app.js"></script>
</body>
</html>







* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    max-width: 800px;
    margin: 30px auto;
    padding: 20px;
}

h2 {
    margin-top: 25px;
    margin-bottom: 10px;
}

/* Menu Styles */
ul {
    list-style-type: disc;
    padding-left: 40px;
    margin-bottom: 15px;
}

ul li {
    padding: 5px 10px;
    cursor: pointer;
    margin-bottom: 3px;
    transition: background-color 0.2s;
}

ul li:hover {
    background-color: #f0f0f0;
}

#selectedOutput {
    margin-bottom: 20px;
    font-size: 14px;
}

/* Keyboard Display */
#keyboardBox {
    width: 100%;
    padding: 15px;
    font-size: 18px;
    border: 1px solid #ccc;
    min-height: 50px;
    margin-bottom: 20px;
}

/* Mouse Zone */
#mouseZone {
    width: 100%;
    height: 120px;
    border: 1px solid #ccc;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 16px;
    cursor: pointer;
    margin-bottom: 20px;
    transition: background-color 0.2s;
}

/* Countdown */
#countdownInput {
    width: 100%;
    padding: 15px;
    font-size: 18px;
    border: 1px solid #ccc;
    margin-bottom: 10px;
}

.btn {
    padding: 5px 15px;
    cursor: pointer;
    margin-right: 5px;
}

/* Username Input */
#usernameInput {
    padding: 8px 12px;
    font-size: 14px;
    border: 1px solid #ccc;
    width: 200px;
}

#usernameFeedback {
    margin-top: 8px;
    font-size: 14px;
}






// ============================================
// Step 2: Event Delegation on Menu
// ============================================
const menuList = document.getElementById('menuList');
const selectedOutput = document.getElementById('selectedOutput');

menuList.addEventListener('click', function(event) {
    if (event.target.tagName === 'LI') {
        // Remove highlight from all items
        const allItems = menuList.querySelectorAll('li');
        allItems.forEach(item => {
            item.style.backgroundColor = '';
        });
        // Highlight the clicked item
        event.target.style.backgroundColor = '#d0e8ff';
        // Display its text in the output area
        selectedOutput.textContent = 'Selected Item: ' + event.target.textContent;
    }
});

// ============================================
// Step 3: Keyboard Display
// ============================================
const keyboardBox = document.getElementById('keyboardBox');

document.addEventListener('keydown', function(event) {
    if (event.key === 'Enter') {
        keyboardBox.textContent = 'Submitted!';
    } else {
        keyboardBox.textContent = event.key;
    }
});

// ============================================
// Step 4: Mouse Events on Mouse Zone
// ============================================
const mouseZone = document.getElementById('mouseZone');

mouseZone.addEventListener('mouseenter', function() {
    mouseZone.textContent = 'Mouse Entered';
});

mouseZone.addEventListener('mouseleave', function() {
    mouseZone.textContent = 'Mouse Left';
});

mouseZone.addEventListener('click', function() {
    const colors = ['#ffcccc', '#ccffcc', '#ccccff', '#ffffcc', '#ffccff', '#ccffff'];
    const randomColor = colors[Math.floor(Math.random() * colors.length)];
    mouseZone.style.backgroundColor = randomColor;
});

// ============================================
// Step 5: Countdown Timer
// ============================================
const countdownInput = document.getElementById('countdownInput');
const startBtn = document.getElementById('startBtn');
const stopBtn = document.getElementById('stopBtn');
let countdownInterval = null;

startBtn.addEventListener('click', function() {
    // Clear any existing interval first
    if (countdownInterval) {
        clearInterval(countdownInterval);
    }

    let count = parseInt(countdownInput.value);

    if (isNaN(count) || count <= 0) {
        countdownInput.value = 10;
        count = 10;
    }

    countdownInput.value = count;

    countdownInterval = setInterval(function() {
        count--;
        countdownInput.value = count;

        if (count <= 0) {
            clearInterval(countdownInterval);
            countdownInterval = null;
            countdownInput.value = 'Time is up!';
        }
    }, 1000);
});

stopBtn.addEventListener('click', function() {
    if (countdownInterval) {
        clearInterval(countdownInterval);
        countdownInterval = null;
    }
});

// ============================================
// Step 6: Real-time Input Validation
// ============================================
const usernameInput = document.getElementById('usernameInput');
const usernameFeedback = document.getElementById('usernameFeedback');

usernameInput.addEventListener('input', function() {
    const value = usernameInput.value;

    if (value.length < 4) {
        usernameFeedback.textContent = 'Username is too short!';
        usernameFeedback.style.color = 'red';
        usernameInput.style.border = '2px solid red';
    } else {
        usernameFeedback.textContent = 'Username looks good!';
        usernameFeedback.style.color = 'green';
        usernameInput.style.border = '2px solid green';
    }
});
