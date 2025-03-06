<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Classroom Seat Reservation System</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

        body {
            font-family: 'Roboto', sans-serif;
            margin: 20px;
            background: linear-gradient(to right, #6a11cb, #2575fc);
            color: #f8f9fa;
            animation: fadeInBody 2s;
        }

        .container {
            max-width: 1200px;
            margin: auto;
            animation: fadeInContainer 1.5s;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        h1 {
            text-align: center;
            color: #ffffff;
            animation: slideDownTitle 1.2s;
        }

        .form-container {
            text-align: center;
            margin-bottom: 20px;
        }

        .form-container input,
        .form-container select {
            padding: 10px;
            margin: 10px;
            font-size: 16px;
            border-radius: 5px;
            border: 1px solid #ccc;
            background-color: #ffffff;
            color: #000000;
        }

        .form-container button {
            padding: 10px 20px;
            background-color: #ff6f61;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: transform 0.3s, background-color 0.3s;
        }

        .form-container button:hover {
            background-color: #d45d50;
            transform: scale(1.1);
        }

        .section {
            display: none;
            margin-top: 20px;
            padding: 15px;
            background-color: #3a3b3c;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .classroom {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100%;
        }

        .screen {
            width: 100%;
            background-color: #222;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            position: sticky;
            top: 0;
            margin-bottom: 20px;
        }

        .student-list {
            width: 100%;
            display: grid;
            grid-template-columns: repeat(6, 1fr); /* 6 seats per row */
            gap: 10px;
            margin-top: 20px;
        }

        .student-list div {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 10px;
            background-color: #ffffff;
            border: 1px solid #ccc;
            border-radius: 50%; /* Make seats circular */
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            transition: transform 0.3s;
        }

        .student-list div.selected {
            background-color: #ff6f61;
            color: white;
        }

        .student-list div:hover {
            transform: scale(1.05);
        }

        .seat-btn {
            margin-top: 10px;
            padding: 5px 10px;
            background-color: #ff6f61;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .seat-btn:disabled {
            background-color: gray;
            cursor: not-allowed;
        }

        .result {
            margin-top: 20px;
            padding: 10px;
            background-color: #ff6f61;
            color: white;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            display: none;
            animation: fadeInResult 1s;
        }

        .seat-name {
            color: orange; /* Seat names in orange color */
        }

        @keyframes fadeInBody {
            from {
                opacity: 0;
            }

            to {
                opacity: 1;
            }
        }

        @keyframes fadeInContainer {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideDownTitle {
            from {
                transform: translateY(-30px);
                opacity: 0;
            }

            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        @keyframes fadeInResult {
            from {
                opacity: 0;
                transform: translateY(20px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>

<body>
    <div class="container">
        <h1>Smart Classroom Seat Reservation System</h1>

        <!-- Registration Form -->
        <div class="form-container" id="registration-form">
            <h2>Enter Your Details</h2>
            <input type="text" id="reg-number" placeholder="Enter Registration Number" required><br>
            <select id="lab-selection" required>
                <option value="" disabled selected>Select Lab</option>
                <option value="lab101">Lab 101</option>
                <option value="lab201">Lab 201</option>
                <option value="lab301">Lab 301</option>
                <option value="lab401">Lab 401</option>
                <option value="lab501">Lab 501</option>
                <option value="lab601">Lab 601</option>
            </select><br><br>
            <button onclick="openReservation()">Proceed</button>
        </div>

        <!-- Lab Reservation Sections -->
        <div id="lab101" class="section">
            <h2>Lab 101</h2>
            <div class="classroom">
                <div class="screen">Screen</div>
                <div class="student-list" id="student-list101"></div>
            </div>
        </div>

        <div id="lab201" class="section">
            <h2>Lab 201</h2>
            <div class="classroom">
                <div class="screen">Screen</div>
                <div class="student-list" id="student-list201"></div>
            </div>
        </div>

        <div id="lab301" class="section">
            <h2>Lab 301</h2>
            <div class="classroom">
                <div class="screen">Screen</div>
                <div class="student-list" id="student-list301"></div>
            </div>
        </div>

        <div id="lab401" class="section">
            <h2>Lab 401</h2>
            <div class="classroom">
                <div class="screen">Screen</div>
                <div class="student-list" id="student-list401"></div>
            </div>
        </div>

        <div id="lab501" class="section">
            <h2>Lab 501</h2>
            <div class="classroom">
                <div class="screen">Screen</div>
                <div class="student-list" id="student-list501"></div>
            </div>
        </div>

        <div id="lab601" class="section">
            <h2>Lab 601</h2>
            <div class="classroom">
                <div class="screen">Screen</div>
                <div class="student-list" id="student-list601"></div>
            </div>
        </div>

        <div class="result" id="result"></div>
    </div>

    <script>
        let selectedSeat = null;

        function openReservation() {
            const regNumber = document.getElementById('reg-number').value;
            const labSelection = document.getElementById('lab-selection').value;

            if (!regNumber || !labSelection) {
                alert("Please fill in all details.");
                return;
            }

            // Hide the registration form
            document.getElementById('registration-form').style.display = 'none';

            // Show the selected lab section
            showSection(labSelection);
            populateStudentList(labSelection, 72);
        }

        // Function to show the selected section
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                section.style.display = 'none';
            });
            document.getElementById(sectionId).style.display = 'block';
        }

        // Function to populate the student list dynamically (72 seats, 12 columns, 6 rows)
        function populateStudentList(classId, totalSeats) {
            const studentListDiv = document.getElementById(student-list${classId.slice(-3)});
            studentListDiv.innerHTML = ''; // Clear previous seats if any
            for (let seat = 1; seat <= totalSeats; seat++) {
                const seatDiv = document.createElement('div');
                seatDiv.id = ${classId}-seat${seat};
                seatDiv.innerHTML = `
                    <span class="seat-name">Seat ${seat}</span>
                    <button class="seat-btn" onclick="bookSeat('${classId}', '${seatDiv.id}', ${seat})">Book</button>
                `;
                studentListDiv.appendChild(seatDiv);
            }
        }

        // Function to book a seat
        function bookSeat(classId, seatId, seatNumber) {
            if (selectedSeat) {
                alert("You can only book one seat at a time!");
                return;
            }

            const regNumber = document.getElementById('reg-number').value;
            const seatDiv = document.getElementById(seatId);
            const bookButton = seatDiv.querySelector('button');

            // Disable the button and mark the seat as booked
            bookButton.disabled = true;
            seatDiv.classList.add('selected');

            selectedSeat = seatId; // Store the selected seat

            alert(Seat ${seatNumber} has been booked successfully by Registration Number: ${regNumber}!);

            // Show confirmation
            document.getElementById('result').innerText = You have successfully booked Seat ${seatNumber}.;
            document.getElementById('result').style.display = 'block';
        }
    </script>
</body>

</html>
