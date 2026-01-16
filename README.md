<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank Exam Countdown 2026-27</title>
    <style>
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f6f9;
            color: #333;
            line-height: 1.6;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        h1 {
            color: #1a73e8;
            font-size: 2.2em;
            margin-bottom: 20px;
            text-align: center;
        }
        .container {
            width: 100%;
            max-width: 1000px;
            overflow-x: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            background-color: #fff;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            border-radius: 10px;
            overflow: hidden;
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
        }
        /* Specific Exam Colors */
        .exam-po { color: #1a73e8; }      /* Blue */
        .exam-clerk { color: #2e7d32; }   /* Green */
        .exam-rrb-po { color: #e65100; }  /* Orange */
        .exam-rrb-clerk { color: #c2185b; } /* Pink */
        
        .mains { font-weight: bold; background-color: #fffde7; }
        .passed { color: #9e9e9e; text-decoration: line-through; }
        tr:hover { background-color: #e8f0fe; }
    </style>
</head>
<body>

    <h1>Bank Exam Countdown 2026-27</h1>

    <div class="container">
        <table>
            <thead>
                <tr>
                    <th>Exam Date</th>
                    <th>Exam Name</th>
                    <th>Type</th>
                    <th>Days Remaining</th>
                </tr>
            </thead>
            <tbody id="examBody">
                </tbody>
        </table>
    </div>

    <script>
        const exams = [
            {
                name: "IBPS PO (CRP PO/MT-XVI)",
                class: "exam-po",
                prelimDates: ["2026-08-22", "2026-08-23"],
                mainsDate: "2026-10-04"
            },
            {
                name: "IBPS Clerk (CRP CSA-XVI)",
                class: "exam-clerk",
                prelimDates: ["2026-10-10", "2026-10-11"],
                mainsDate: "2026-12-27"
            },
            {
                name: "IBPS RRB PO (Officer Scale I)",
                class: "exam-rrb-po",
                prelimDates: ["2026-11-21", "2026-11-22"],
                mainsDate: "2026-12-20"
            },
            {
                name: "IBPS RRB Clerk (Office Assistant)",
                class: "exam-rrb-clerk",
                prelimDates: ["2026-12-06", "2026-12-12", "2026-12-13"],
                mainsDate: "2027-01-30"
            }
        ];

        const dateEntries = [];
        exams.forEach(exam => {
            exam.prelimDates.forEach(date => {
                dateEntries.push({ date, examName: exam.name, type: "Prelims", class: exam.class });
            });
            if (exam.mainsDate) {
                dateEntries.push({ date: exam.mainsDate, examName: exam.name, type: "Mains", class: exam.class });
            }
        });

        // Sort by date chronologically
        dateEntries.sort((a, b) => new Date(a.date) - new Date(b.date));

        function getDaysUntil(targetDate) {
            const today = new Date();
            const target = new Date(targetDate);
            today.setHours(0, 0, 0, 0);
            target.setHours(0, 0, 0, 0);
            const diffTime = target - today;
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            return diffDays;
        }

        function formatDate(dateStr) {
            const date = new Date(dateStr);
            return date.toLocaleDateString('en-GB', { day: 'numeric', month: 'short', year: 'numeric' });
        }

        const tableBody = document.getElementById('examBody');
        dateEntries.forEach(entry => {
            const row = document.createElement('tr');
            const daysUntil = getDaysUntil(entry.date);
            
            row.className = `${entry.class} ${entry.type === 'Mains' ? 'mains' : ''}`;
            
            let statusText = daysUntil > 0 ? daysUntil : (daysUntil === 0 ? "Today!" : "Passed");
            if (daysUntil < 0) row.classList.add('passed');

            row.innerHTML = `
                <td>${formatDate(entry.date)}</td>
                <td>${entry.examName}</td>
                <td>${entry.type}</td>
                <td>${statusText}</td>
            `;
            tableBody.appendChild(row);
        });
    </script>
</body>
</html>
