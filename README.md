<script type="text/javascript">
        var gk_isXlsx = false;
        var gk_xlsxFileLookup = {};
        var gk_fileData = {};
        function filledCell(cell) {
          return cell !== '' && cell != null;
        }
        function loadFileData(filename) {
        if (gk_isXlsx && gk_xlsxFileLookup[filename]) {
            try {
                var workbook = XLSX.read(gk_fileData[filename], { type: 'base64' });
                var firstSheetName = workbook.SheetNames[0];
                var worksheet = workbook.Sheets[firstSheetName];

                // Convert sheet to JSON to filter blank rows
                var jsonData = XLSX.utils.sheet_to_json(worksheet, { header: 1, blankrows: false, defval: '' });
                // Filter out blank rows (rows where all cells are empty, null, or undefined)
                var filteredData = jsonData.filter(row => row.some(filledCell));

                // Heuristic to find the header row by ignoring rows with fewer filled cells than the next row
                var headerRowIndex = filteredData.findIndex((row, index) =>
                  row.filter(filledCell).length >= filteredData[index + 1]?.filter(filledCell).length
                );
                // Fallback
                if (headerRowIndex === -1 || headerRowIndex > 25) {
                  headerRowIndex = 0;
                }

                // Convert filtered JSON back to CSV
                var csv = XLSX.utils.aoa_to_sheet(filteredData.slice(headerRowIndex)); // Create a new sheet from filtered array of arrays
                csv = XLSX.utils.sheet_to_csv(csv, { header: 1 });
                return csv;
            } catch (e) {
                console.error(e);
                return "";
            }
        }
        return gk_fileData[filename] || "";
        }
        </script><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IBPS Exam Countdown 2025 (Date-Wise, Text Colored, Mains Bold)</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        table {
            width: 100%;
            max-width: 800px;
            margin: 20px auto;
            border-collapse: collapse;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        th, td {
            padding: 10px;
            text-align: left;
            border: 1px solid #ddd;
        }
        th {
            background-color: #4CAF50;
            color: white;
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
        tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        tr:hover {
            background-color: #f1f1f1;
        }
    </style>
</head>
<body>
    <h1>IBPS Exam Countdown 2025 (Date-Wise, Text Colored, Mains Bold)</h1>
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
            // Add Preliminary dates
            exam.prelimDates.forEach(date => {
                dateEntries.push({ date, examName: exam.name, type: "Prelims", class: exam.class });
            });
            // Add Mains date
            dateEntries.push({ date: exam.mainsDate, examName: exam.name, type: "Mains", class: exam.class });
        });

        // Sort by date
        dateEntries.sort((a, b) => new Date(a.date) - new Date(b.date));

        // Function to calculate days between two dates
        function getDaysUntil(targetDate) {
            const today = new Date();
            const target = new Date(targetDate);
            // Set time to midnight to avoid time-of-day discrepancies
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
            // Apply exam-specific text color class and bold for Mains
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
