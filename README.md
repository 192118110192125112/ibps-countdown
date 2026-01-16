
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BANK EXAM TRACKER 2026-27</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --po-blue: #2563eb;
            --clerk-green: #10b981;
            --rrb-orange: #f59e0b;
            --rrb-pink: #db2777;
            --text-main: #1e293b;
            --bg-body: #f8fafc;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-body);
            color: var(--text-main);
            margin: 0;
            padding: 40px 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        h1 {
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 40px;
            text-align: center;
            font-size: 2rem;
            color: #0f172a;
        }

        .container {
            width: 100%;
            max-width: 850px;
        }

        /* Exam Sections */
        .exam-section {
            background: white;
            border-radius: 16px;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            overflow: hidden;
            border: 1px solid #e2e8f0;
        }

        .exam-header {
            padding: 15px 25px;
            color: white;
            font-weight: 700;
            font-size: 1.1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .exam-content { padding: 10px 0; }

        .date-row {
            display: grid;
            grid-template-columns: 1fr 120px 120px;
            padding: 12px 25px;
            border-bottom: 1px solid #f1f5f9;
            align-items: center;
        }

        .date-row:last-child { border-bottom: none; }

        .date-text { font-weight: 600; font-size: 0.95rem; }

        /* Stage Badges */
        .badge {
            font-size: 0.7rem;
            font-weight: 800;
            text-transform: uppercase;
            padding: 4px 10px;
            border-radius: 6px;
            width: fit-content;
        }
        .pre-badge { background: #dbeafe; color: #1e40af; }
        .main-badge { background: #f3e8ff; color: #7e22ce; border: 1px solid #d8b4fe; }

        .days-left {
            text-align: right;
            font-weight: 800;
            color: var(--text-main);
        }

        .days-label { font-size: 0.65rem; color: #64748b; font-weight: 400; }

        /* Colors by Exam */
        .bg-po { background-color: var(--po-blue); }
        .bg-clerk { background-color: var(--clerk-green); }
        .bg-rrb-po { background-color: var(--rrb-orange); }
        .bg-rrb-clerk { background-color: var(--rrb-pink); }

        @media (max-width: 600px) {
            .date-row { grid-template-columns: 1fr 80px 70px; padding: 12px 15px; }
            .date-text { font-size: 0.85rem; }
            h1 { font-size: 1.5rem; }
        }
    </style>
</head>
<body>

    <h1>BANK EXAM COUNTDOWN 2026-27</h1>

    <div class="container" id="tracker">
        </div>

    <script>
        const examsData = [
            { id: 'po', name: "IBPS PO (CRP PO/MT-XVI)", color: "bg-po", dates: [
                { d: "2026-08-22", t: "Prelims" }, { d: "2026-08-23", t: "Prelims" }, { d: "2026-10-04", t: "Mains" }
            ]},
            { id: 'clerk', name: "IBPS Clerk (CRP CSA-XVI)", color: "bg-clerk", dates: [
                { d: "2026-10-10", t: "Prelims" }, { d: "2026-10-11", t: "Prelims" }, { d: "2026-12-27", t: "Mains" }
            ]},
            { id: 'rrb-po', name: "IBPS RRB Officer Scale I", color: "bg-rrb-po", dates: [
                { d: "2026-11-21", t: "Prelims" }, { d: "2026-11-22", t: "Prelims" }, { d: "2026-12-20", t: "Mains" }
            ]},
            { id: 'rrb-clerk', name: "IBPS RRB Office Assistant", color: "bg-rrb-clerk", dates: [
                { d: "2026-12-06", t: "Prelims" }, { d: "2026-12-12", t: "Prelims" }, { d: "2026-12-13", t: "Prelims" }, { d: "2027-01-30", t: "Mains" }
            ]}
        ];

        const tracker = document.getElementById('tracker');
        const today = new Date();
        today.setHours(0,0,0,0);

        examsData.forEach(exam => {
            let section = document.createElement('div');
            section.className = 'exam-section';
            
            let html = `<div class="exam-header ${exam.color}"><span>${exam.name}</span></div><div class="exam-content">`;
            
            exam.dates.forEach(item => {
                const target = new Date(item.d);
                const diff = Math.ceil((target - today) / (1000 * 60 * 60 * 24));
                const dateStr = target.toLocaleDateString('en-GB', { day: '2-digit', month: 'short', year: 'numeric' });
                const badgeClass = item.t === 'Mains' ? 'main-badge' : 'pre-badge';

                html += `
                    <div class="date-row">
                        <span class="date-text">${dateStr}</span>
                        <span><span class="badge ${badgeClass}">${item.t}</span></span>
                        <div class="days-left">
                            ${diff < 0 ? 'Done' : diff}
                            <div class="days-label">${diff < 0 ? 'COMPLETED' : 'DAYS LEFT'}</div>
                        </div>
                    </div>
                `;
            });

            html += `</div>`;
            section.innerHTML = html;
            tracker.appendChild(section);
        });
    </script>
</body>
</html>
