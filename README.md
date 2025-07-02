<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IBPS Exam Countdown 2025</title>
    <style>
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f6f9;
            color: #333;
            line-height: 1.6;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh; /* Ensures full viewport height */
        }
        h1 {
            color: #1a73e8;
            font-size: 2.2em;
            margin: 20px 0;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        table {
            width: 100%;
            max-width: 1000px;
            border-collapse: collapse;
            background-color: #fff;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
        }
        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #e0e0e0;
        }
        th {
            background-color: #1a73e8;
            color: white;
            font-weight: 600;
            font-size: 1.2em;
        }
        td {
            font-size: 1em;
        }
        /* Exam-specific text colors */
        .exam-po {
            color: #1a73e8; /* Blue for IBPS PO */
        }
        .exam-clerk {
            color: #2e7d32; /* Green for IBPS Clerk */
        }
        .exam-rrb-po {
            color: #e65100; /* Orange for IBPS RRB PO */
        }
        .exam-rrb-clerk {
            color: #c2185b; /* Pink for IBPS RRB Clerk */
        }
        /* Bold for Mains rows */
        .mains {
            font-weight: bold;
        }
        /* Alternating row colors */
        tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        tr:hover {
            background-color: #e8f0fe;
        }
        /* Responsive design for mobile */
        @media (max-width: 600px) {
            table {
                font-size: 0.85em;
            }
            th, td {
                padding: 10px;
            }
            h1 {
                font-size: 1.8em;
            }
            body {
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <h1>IBPS Exam Countdown 2025</h1>
    <table id="examTable">
        <thead>
            <tr>
                <th>Exam Date</th>
                <th>Exam</th>
                <th>Exam Type</th>
                <th>Days Until Exam</th>
            </tr>
        </thead>
        <tbody id="examBody">
            <!-- Table rows will be populated by JavaScript -->
        </tbody>
    </table>

    <script>
        // Exam data from IBPS Calendar 2025-26
        const exams = [
            {
                name: "IBPS PO (CRP PO/MT-XV)",
                class: "exam-po",
                prelimDates: ["2025-08-17", "2025-08-23", "2025-08-24"],
                mainsDate: "2025-10-12"
            },
            {
                name: "IBPS Clerk (CRP CSA-XV)",
                class: "exam-clerk",
                prelimDates: ["2025-10-04", "2025-10-05", "2025-10-11"],
                mainsDate: "2025-11-29"
            },
            {
                name: "IBPS RRB PO (Officer Scale I)",
                class: "exam-rrb-po",
                prelimDates: ["2025-11-22", "2025-11-23"],
                mainsDate: "2025-12-28"
            },
            {
                name: "IBPS RRB Clerk (Office Assistant)",
                class: "exam-rrb-clerk",
                prelimDates: ["2025-12-06", "2025-12-07", "2025-12-13", "2025-12-14"],
                mainsDate: "2026-02-01"
            }
        ];

        // Flatten exam data into an array of {date, examName, type, class}
        const dateEntries = [];
        exams.forEach(exam => {
            exam.prelimDates.forEach(date => {
                dateEntries.push({ date, examName: exam.name, type: "Prelims", class: exam.class });
            });
            dateEntries.push({ date: exam.mainsDate, examName: exam.name, type: "Mains", class: exam.class });
        });

        // Sort by date
        dateEntries.sort((a, b) => new Date(a.date) - new Date(b.date));

        // Function to calculate days between two dates
        function getDaysUntil(targetDate) {
            const today = new Date();
            const target = new Date(targetDate);
            today.setHours(0, 0, 0, 0);
            target.setHours(0, 0, 0, 0);
            const diffTime = target - today;
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            return diffDays >= 0 ? diffDays : "Passed";
        }

        // Function to format date as DD Month YYYY
        function formatDate(dateStr) {
            const date = new Date(dateStr);
            const options = { day: 'numeric', month: 'long', year: 'numeric' };
            return date.toLocaleDateString('en-GB', options);
        }

        // Populate the table
        const tableBody = document.getElementById('examBody');
        dateEntries.forEach(entry => {
            const row = document.createElement('tr');
            const daysUntil = getDaysUntil(entry.date);
            row.className = `${entry.class} ${entry.type === 'Mains' ? 'mains' : ''}`;
            row.innerHTML = `
                <td>${formatDate(entry.date)}</td>
                <td>${entry.examName}</td>
                <td>${entry.type}</td>
                <td>${daysUntil}</td>
            `;
            tableBody.appendChild(row);
        });
    </script>
</body>
</html>
