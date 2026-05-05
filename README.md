<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Handover Inspection Productivity Dashboard 2025</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #FF4C00;
            --primary-light: #FFF0E8;
            --primary-mid: #FF8A5C;
            --secondary: #FF6B35;
            --accent: #FFB088;
            --dark: #1A1A2E;
            --text: #2D2D3A;
            --text-light: #6B7280;
            --bg: #FAFBFC;
            --card-bg: #FFFFFF;
            --border: #E5E7EB;
            --success: #10B981;
            --warning: #F59E0B;
            --danger: #EF4444;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg);
            color: var(--text);
            line-height: 1.6;
        }

        /* Header */
        .header {
            background: var(--primary);
            color: white;
            padding: 1.5rem 2rem;
            box-shadow: 0 4px 20px rgba(255, 76, 0, 0.2);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .header h1 {
            font-size: 1.5rem;
            font-weight: 800;
            letter-spacing: -0.5px;
        }

        .header-sub {
            font-size: 0.85rem;
            opacity: 0.9;
            font-weight: 400;
        }

        .download-btn {
            background: white;
            color: var(--primary);
            border: none;
            padding: 0.6rem 1.2rem;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .download-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }

        /* Container */
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 2rem;
        }

        /* KPI Cards */
        .kpi-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 1.2rem;
            margin-bottom: 2rem;
        }

        .kpi-card {
            background: var(--card-bg);
            border-radius: 16px;
            padding: 1.5rem;
            box-shadow: 0 2px 12px rgba(0,0,0,0.06);
            border: 1px solid var(--border);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .kpi-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--primary);
        }

        .kpi-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 8px 24px rgba(255, 76, 0, 0.12);
        }

        .kpi-icon {
            width: 44px;
            height: 44px;
            background: var(--primary-light);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--primary);
            font-size: 1.2rem;
            margin-bottom: 1rem;
        }

        .kpi-value {
            font-size: 2rem;
            font-weight: 800;
            color: var(--dark);
            letter-spacing: -1px;
        }

        .kpi-label {
            font-size: 0.85rem;
            color: var(--text-light);
            font-weight: 500;
            margin-top: 0.25rem;
        }

        .kpi-change {
            display: inline-flex;
            align-items: center;
            gap: 0.25rem;
            font-size: 0.8rem;
            font-weight: 600;
            margin-top: 0.5rem;
            padding: 0.2rem 0.5rem;
            border-radius: 6px;
        }

        .kpi-change.positive {
            background: #D1FAE5;
            color: var(--success);
        }

        .kpi-change.negative {
            background: #FEE2E2;
            color: var(--danger);
        }

        /* Section Headers */
        .section-header {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            margin: 2.5rem 0 1.2rem 0;
        }

        .section-header h2 {
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--dark);
        }

        .section-line {
            flex: 1;
            height: 2px;
            background: linear-gradient(to right, var(--primary), transparent);
            border-radius: 2px;
        }

        /* Charts Grid */
        .charts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .chart-card {
            background: var(--card-bg);
            border-radius: 16px;
            padding: 1.5rem;
            box-shadow: 0 2px 12px rgba(0,0,0,0.06);
            border: 1px solid var(--border);
        }

        .chart-card h3 {
            font-size: 1rem;
            font-weight: 600;
            color: var(--dark);
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .chart-card h3 i {
            color: var(--primary);
        }

        .chart-container {
            position: relative;
            height: 300px;
        }

        .chart-container.tall {
            height: 380px;
        }

        /* Staff Cards Grid */
        .staff-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .staff-card {
            background: var(--card-bg);
            border-radius: 14px;
            padding: 1.25rem;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            border: 1px solid var(--border);
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .staff-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(255, 76, 0, 0.1);
            border-color: var(--primary-mid);
        }

        .staff-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 0.75rem;
        }

        .staff-name {
            font-weight: 700;
            font-size: 0.95rem;
            color: var(--dark);
            line-height: 1.3;
        }

        .staff-badge {
            background: var(--primary-light);
            color: var(--primary);
            padding: 0.2rem 0.6rem;
            border-radius: 20px;
            font-size: 0.7rem;
            font-weight: 600;
            white-space: nowrap;
        }

        .staff-meta {
            font-size: 0.8rem;
            color: var(--text-light);
            margin-bottom: 0.75rem;
        }

        .staff-meta i {
            color: var(--primary);
            margin-right: 0.25rem;
        }

        .staff-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.5rem;
            margin-bottom: 0.75rem;
        }

        .stat-box {
            background: var(--primary-light);
            border-radius: 8px;
            padding: 0.5rem;
            text-align: center;
        }

        .stat-box.inhouse {
            background: #F0F9FF;
        }

        .stat-value {
            font-size: 0.85rem;
            font-weight: 700;
            color: var(--dark);
        }

        .stat-label {
            font-size: 0.65rem;
            color: var(--text-light);
            font-weight: 500;
        }

        .progress-bar {
            height: 6px;
            background: var(--border);
            border-radius: 3px;
            overflow: hidden;
            margin-top: 0.5rem;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 3px;
            transition: width 0.5s ease;
        }

        .progress-fill.low {
            background: linear-gradient(90deg, var(--warning), #FBBF24);
        }

        .progress-fill.critical {
            background: linear-gradient(90deg, var(--danger), #F87171);
        }

        .util-text {
            display: flex;
            justify-content: space-between;
            font-size: 0.75rem;
            margin-top: 0.25rem;
            font-weight: 600;
        }

        .util-text .value {
            color: var(--primary);
        }

        /* Tables */
        .table-card {
            background: var(--card-bg);
            border-radius: 16px;
            padding: 1.5rem;
            box-shadow: 0 2px 12px rgba(0,0,0,0.06);
            border: 1px solid var(--border);
            overflow-x: auto;
            margin-bottom: 2rem;
        }

        .table-card h3 {
            font-size: 1rem;
            font-weight: 600;
            color: var(--dark);
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
        }

        thead th {
            background: var(--primary-light);
            color: var(--primary);
            font-weight: 600;
            text-align: left;
            padding: 0.75rem 1rem;
            border-bottom: 2px solid var(--primary);
            white-space: nowrap;
        }

        tbody td {
            padding: 0.75rem 1rem;
            border-bottom: 1px solid var(--border);
            color: var(--text);
        }

        tbody tr:hover {
            background: var(--primary-light);
        }

        .util-pill {
            display: inline-flex;
            align-items: center;
            padding: 0.2rem 0.6rem;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.8rem;
        }

        .util-pill.high {
            background: #D1FAE5;
            color: #059669;
        }

        .util-pill.medium {
            background: #FEF3C7;
            color: #D97706;
        }

        .util-pill.low {
            background: #FEE2E2;
            color: #DC2626;
        }

        /* Insights Section */
        .insights-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .insight-card {
            background: var(--card-bg);
            border-radius: 14px;
            padding: 1.25rem;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            border-left: 4px solid var(--primary);
        }

        .insight-card h4 {
            font-size: 0.9rem;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .insight-card h4 i {
            color: var(--primary);
        }

        .insight-card p {
            font-size: 0.85rem;
            color: var(--text-light);
            line-height: 1.6;
        }

        .insight-card .highlight {
            color: var(--primary);
            font-weight: 700;
        }

        /* Filters */
        .filter-bar {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
            flex-wrap: wrap;
        }

        .filter-btn {
            padding: 0.5rem 1rem;
            border: 1px solid var(--border);
            background: white;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            transition: all 0.2s;
        }

        .filter-btn:hover, .filter-btn.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }

        /* Search */
        .search-box {
            width: 100%;
            max-width: 400px;
            padding: 0.75rem 1rem;
            border: 1px solid var(--border);
            border-radius: 10px;
            font-size: 0.9rem;
            margin-bottom: 1rem;
            font-family: inherit;
        }

        .search-box:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(255, 76, 0, 0.1);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .container { padding: 1rem; }
            .header h1 { font-size: 1.2rem; }
            .charts-grid { grid-template-columns: 1fr; }
            .staff-grid { grid-template-columns: 1fr; }
            .kpi-grid { grid-template-columns: repeat(2, 1fr); }
            .chart-container { height: 250px; }
            table { font-size: 0.75rem; }
            th, td { padding: 0.5rem; }
        }

        @media (max-width: 480px) {
            .kpi-grid { grid-template-columns: 1fr; }
            .header-content { flex-direction: column; text-align: center; }
        }

        /* Animations */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .animate-in {
            animation: fadeIn 0.6s ease forwards;
        }

        .delay-1 { animation-delay: 0.1s; }
        .delay-2 { animation-delay: 0.2s; }
        .delay-3 { animation-delay: 0.3s; }
        .delay-4 { animation-delay: 0.4s; }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--bg);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--primary-mid);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--primary);
        }
    </style>
<base target="_blank">
</head>
<body>
    <header class="header">
        <div class="header-content">
            <div>
                <h1><i class="fas fa-chart-line"></i> Handover Inspection Productivity Dashboard</h1>
                <div class="header-sub">2025 Annual Report &mdash; 116 Staff Members &mdash; 33 Branches &mdash; 5 Regions</div>
            </div>
            <button class="download-btn" onclick="downloadPPTX()">
                <i class="fas fa-file-powerpoint"></i> Download .pptx
            </button>
        </div>
    </header>

    <div class="container">
        <!-- KPI Summary -->
        <div class="kpi-grid">
            <div class="kpi-card animate-in delay-1">
                <div class="kpi-icon"><i class="fas fa-calendar-check"></i></div>
                <div class="kpi-value">209,290</div>
                <div class="kpi-label">Total Open Slots</div>
                <div class="kpi-change positive"><i class="fas fa-arrow-up"></i> All Regions</div>
            </div>
            <div class="kpi-card animate-in delay-2">
                <div class="kpi-icon"><i class="fas fa-check-circle"></i></div>
                <div class="kpi-value">155,384</div>
                <div class="kpi-label">Total Used Slots</div>
                <div class="kpi-change positive"><i class="fas fa-arrow-up"></i> 74.2% Utilized</div>
            </div>
            <div class="kpi-card animate-in delay-3">
                <div class="kpi-icon"><i class="fas fa-mobile-alt"></i></div>
                <div class="kpi-value">80.6%</div>
                <div class="kpi-label">Mobile Utilization</div>
                <div class="kpi-change positive"><i class="fas fa-arrow-up"></i> 45,470 Used</div>
            </div>
            <div class="kpi-card animate-in delay-4">
                <div class="kpi-icon"><i class="fas fa-building"></i></div>
                <div class="kpi-value">71.9%</div>
                <div class="kpi-label">Inhouse Utilization</div>
                <div class="kpi-change positive"><i class="fas fa-arrow-up"></i> 109,914 Used</div>
            </div>
            <div class="kpi-card animate-in delay-1">
                <div class="kpi-icon"><i class="fas fa-users"></i></div>
                <div class="kpi-value">116</div>
                <div class="kpi-label">Total Staff</div>
                <div class="kpi-change positive"><i class="fas fa-user-check"></i> 14 Perfect Score</div>
            </div>
            <div class="kpi-card animate-in delay-2">
                <div class="kpi-icon"><i class="fas fa-map-marker-alt"></i></div>
                <div class="kpi-value">33</div>
                <div class="kpi-label">Total Branches</div>
                <div class="kpi-change positive"><i class="fas fa-globe"></i> 5 Regions</div>
            </div>
        </div>

        <!-- Key Insights -->
        <div class="section-header">
            <h2><i class="fas fa-lightbulb"></i> Key Insights</h2>
            <div class="section-line"></div>
        </div>

        <div class="insights-grid">
            <div class="insight-card">
                <h4><i class="fas fa-trophy"></i> Top Performing Region</h4>
                <p><span class="highlight">NORTHERN</span> leads with <span class="highlight">79.9%</span> overall utilization, outperforming all other regions. This region has 23 staff members.</p>
            </div>
            <div class="insight-card">
                <h4><i class="fas fa-exclamation-triangle"></i> Attention Needed</h4>
                <p><span class="highlight">EAST MALAYSIA</span> has the lowest utilization at <span class="highlight">29.8%</span>, significantly below the company average of 74.2%. Focused intervention recommended.</p>
            </div>
            <div class="insight-card">
                <h4><i class="fas fa-chart-line"></i> Peak Performance</h4>
                <p>August 2025 recorded the highest overall utilization at <span class="highlight">84.0%</span>, while January 2025 was the lowest at <span class="highlight">65.5%</span>. Seasonal trends suggest Q3 is strongest.</p>
            </div>
            <div class="insight-card">
                <h4><i class="fas fa-star"></i> Perfect Scorers</h4>
                <p><span class="highlight">14 staff members</span> achieved 100% utilization. Mobile-only staff: 39, Inhouse-only: 40, Mixed: 37.</p>
            </div>
            <div class="insight-card">
                <h4><i class="fas fa-mobile-alt"></i> Mobile vs Inhouse</h4>
                <p>Mobile slots perform better at <span class="highlight">80.6%</span> vs Inhouse at <span class="highlight">71.9%</span>. The gap of 8.7 percentage points suggests mobile operations are more efficient.</p>
            </div>
            <div class="insight-card">
                <h4><i class="fas fa-building"></i> Top Branch</h4>
                <p><span class="highlight">KAJANG</span> (KLANG VALLEY) leads branches with <span class="highlight">93.8%</span> utilization across 3 staff.</p>
            </div>
        </div>

        <!-- Charts Section -->
        <div class="section-header">
            <h2><i class="fas fa-chart-pie"></i> Productivity Analytics</h2>
            <div class="section-line"></div>
        </div>

        <div class="charts-grid">
            <div class="chart-card animate-in">
                <h3><i class="fas fa-chart-area"></i> Monthly Utilization Trend</h3>
                <div class="chart-container">
                    <canvas id="monthlyChart"></canvas>
                </div>
            </div>
            <div class="chart-card animate-in">
                <h3><i class="fas fa-chart-bar"></i> Regional Comparison</h3>
                <div class="chart-container">
                    <canvas id="regionChart"></canvas>
                </div>
            </div>
            <div class="chart-card animate-in">
                <h3><i class="fas fa-chart-bar"></i> Branch Productivity (Top 15)</h3>
                <div class="chart-container tall">
                    <canvas id="branchChart"></canvas>
                </div>
            </div>
            <div class="chart-card animate-in">
                <h3><i class="fas fa-chart-pie"></i> Slot Distribution by Region</h3>
                <div class="chart-container">
                    <canvas id="distributionChart"></canvas>
                </div>
            </div>
        </div>

        <!-- Staff Cards Section -->
        <div class="section-header">
            <h2><i class="fas fa-id-card"></i> Team Member Performance</h2>
            <div class="section-line"></div>
        </div>

        <div class="filter-bar">
            <button class="filter-btn active" onclick="filterStaff('all')">All Regions</button>
            <button class="filter-btn" onclick="filterStaff('KLANG VALLEY')">Klang Valley</button>
            <button class="filter-btn" onclick="filterStaff('SOUTHERN')">Southern</button>
            <button class="filter-btn" onclick="filterStaff('NORTHERN')">Northern</button>
            <button class="filter-btn" onclick="filterStaff('EAST COAST')">East Coast</button>
            <button class="filter-btn" onclick="filterStaff('EAST MALAYSIA')">East Malaysia</button>
        </div>

        <input type="text" class="search-box" id="staffSearch" placeholder="🔍 Search by staff name or branch..." onkeyup="searchStaff()">

        <div class="staff-grid" id="staffGrid">

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="amirul aiman bin yahya" data-branch="cheras">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AMIRUL AIMAN BIN YAHYA</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> CHERAS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1461/1461</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,461 / 1,461 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad azli bin mat shafar" data-branch="puchong">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD AZLI BIN MAT SHAFAR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PUCHONG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">536/536</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 536 / 536 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="osman bin ishak" data-branch="glenmarie">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">OSMAN BIN ISHAK</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> GLENMARIE, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">303/303</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 303 / 303 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohd zulkifli bin abdullah" data-branch="b. pahat">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD ZULKIFLI BIN ABDULLAH</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> B. PAHAT, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">2/2</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">516/516</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 518 / 518 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad hanif bin nor abidin" data-branch="tmn megah">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD HANIF BIN NOR ABIDIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> TMN MEGAH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">322/322</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 322 / 322 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohammad hanis bin daya robi" data-branch="ipoh">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMMAD HANIS BIN DAYA ROBI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> IPOH, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">943/943</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 943 / 943 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="akmal fitri bin ahmad yusni" data-branch="seremban">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AKMAL FITRI BIN AHMAD YUSNI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SEREMBAN, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1533/1533</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,533 / 1,533 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohammad shafiq bin jasni" data-branch="p. medan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMMAD SHAFIQ BIN JASNI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. MEDAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">2/2</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">558/558</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 560 / 560 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad imran syakir bin lukman" data-branch="melaka">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD IMRAN SYAKIR BIN LUKMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MELAKA, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">379/379</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 379 / 379 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohamad ridzuan bin abdul rahman" data-branch="a. setar">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD RIDZUAN BIN ABDUL RAHMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> A. SETAR, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">668/668</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 668 / 668 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="mohd syafiq ikhwan bin ruzeman" data-branch="kuantan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD SYAFIQ IKHWAN BIN RUZEMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KUANTAN, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">440/440</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 440 / 440 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad nur hadi bin zaini" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD NUR HADI BIN ZAINI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">184/184</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 184 / 184 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad rafidi bin ramli" data-branch="kajang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD RAFIDI BIN RAMLI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KAJANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1877/1877</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,877 / 1,877 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="marwan bin abdullah" data-branch="p. juru">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MARWAN BIN ABDULLAH</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. JURU, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">100.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">481/481</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 481 / 481 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 100.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">100.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhamad firdhaus bin mokhtar" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMAD FIRDHAUS BIN MOKHTAR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">98.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1422/1446</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,422 / 1,446 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 98.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">98.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad afiq hakimi bin abdul rahim" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD AFIQ HAKIMI BIN ABDUL RAHIM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">97.2%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3536/3637</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,536 / 3,637 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 97.2%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">97.2%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad ikhwan bin mohamad nordin" data-branch="p. bayan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD IKHWAN BIN MOHAMAD NORDIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. BAYAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">97.2%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">385/396</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 385 / 396 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 97.2%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">97.2%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad zulhelman bin mohd okhir" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ZULHELMAN BIN MOHD OKHIR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">96.8%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">3/3</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3509/3625</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,512 / 3,628 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 96.8%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">96.8%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="ahmad aliff hakim bin shawal" data-branch="k. bharu">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AHMAD ALIFF HAKIM BIN SHAWAL</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> K. BHARU, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">95.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">865/906</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 865 / 906 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 95.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">95.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="syed hatim hakimy bin syed mohamad yusoff khydir" data-branch="cheras">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">SYED HATIM HAKIMY BIN SYED MOHAMAD YUSOFF KHYDIR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> CHERAS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">95.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1157/1216</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,157 / 1,216 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 95.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">95.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad alif bin mat shafar" data-branch="cheras">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ALIF BIN MAT SHAFAR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> CHERAS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">94.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1150/1216</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,150 / 1,216 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 94.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">94.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohamad ikhwan bin rosdi" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD IKHWAN BIN ROSDI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">94.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3475/3698</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,475 / 3,698 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 94.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">94.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad amirul arif bin azman" data-branch="kajang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD AMIRUL ARIF BIN AZMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KAJANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">93.2%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">555/614</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1571/1668</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,126 / 2,282 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 93.2%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">93.2%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhamad amirul adli bin mohd hakam" data-branch="cheras">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMAD AMIRUL ADLI BIN MOHD HAKAM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> CHERAS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">91.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">282/305</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2365/2604</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,647 / 2,909 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 91.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">91.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohamad asraff bin mohd fadzir" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD ASRAFF BIN MOHD FADZIR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">91.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">64/64</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3217/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,281 / 3,604 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 91.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">91.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="irfan farhan bin irwan fazly" data-branch="cheras">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">IRFAN FARHAN BIN IRWAN FAZLY</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> CHERAS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">90.8%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3214/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,214 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 90.8%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">90.8%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="putra amir hussin bin anuar" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">PUTRA AMIR HUSSIN BIN ANUAR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">90.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1/1</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3259/3619</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,260 / 3,620 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 90.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">90.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohamad aimullah bin mohamad zin" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD AIMULLAH BIN MOHAMAD ZIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">89.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2413/2690</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,413 / 2,690 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 89.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">89.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad danial bin halim" data-branch="glenmarie">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD DANIAL BIN HALIM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> GLENMARIE, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">89.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1083/1209</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,083 / 1,209 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 89.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">89.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad thazmi bin abdul rahman" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD THAZMI BIN ABDUL RAHMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">89.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">695/780</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 695 / 780 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 89.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">89.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="azli zulhelimi bin azmi" data-branch="p. juru">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AZLI ZULHELIMI BIN AZMI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. JURU, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">88.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3135/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,135 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 88.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">88.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad ammil raif bin norazmi" data-branch="s. alam">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD AMMIL RAIF BIN NORAZMI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> S. ALAM, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">87.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">282/305</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2276/2604</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,558 / 2,909 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 87.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">87.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohamad syahmi bin rebu" data-branch="ipoh">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD SYAHMI BIN REBU</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> IPOH, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">87.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3099/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,099 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 87.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">87.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad aniq hazman bin rosli" data-branch="tmn megah">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ANIQ HAZMAN BIN ROSLI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> TMN MEGAH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">87.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3090/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,090 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 87.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">87.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohamad sufi bin mohd sabari" data-branch="p. juru">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD SUFI BIN MOHD SABARI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. JURU, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">87.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3081/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,081 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 87.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">87.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="danish aslam bin zainuddin" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">DANISH ASLAM BIN ZAINUDDIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">87.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2055/2361</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,055 / 2,361 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 87.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">87.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad farhan bin usri" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD FARHAN BIN USRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">86.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">61/61</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3060/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,121 / 3,601 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohamad hafizuddin bin ghazali" data-branch="glenmarie">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD HAFIZUDDIN BIN GHAZALI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> GLENMARIE, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">86.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3068/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,068 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohammad amirul haqim bin bakri" data-branch="okr">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMMAD AMIRUL HAQIM BIN BAKRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> OKR, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">86.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1036/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,036 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="noor rahim bin mohd aris" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">NOOR RAHIM BIN MOHD ARIS</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">86.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">180/208</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 180 / 208 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohd aliff iskandar bin abdul nasser" data-branch="p. juru">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD ALIFF ISKANDAR BIN ABDUL NASSER</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. JURU, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">86.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1045/1209</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,045 / 1,209 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohammad syawal bin abdul razak" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMMAD SYAWAL BIN ABDUL RAZAK</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">86.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1033/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,033 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohamad azizi bin salleh" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD AZIZI BIN SALLEH</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">86.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">54/54</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3038/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 3,092 / 3,594 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="aiman syahizzad bin khairull" data-branch="s. alam">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AIMAN SYAHIZZAD BIN KHAIRULL</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> S. ALAM, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">86.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1038/1207</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,038 / 1,207 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 86.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">86.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad haziq bin khairi" data-branch="setapak">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD HAZIQ BIN KHAIRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SETAPAK, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">85.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">472/632</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1116/1216</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,588 / 1,848 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 85.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">85.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad irfan hazwan bin halim" data-branch="p. medan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD IRFAN HAZWAN BIN HALIM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. MEDAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">85.8%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1028/1199</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">3/3</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,031 / 1,202 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 85.8%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">85.8%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad nur aiman bin mohd nurfendi" data-branch="tmn megah">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD NUR AIMAN BIN MOHD NURFENDI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> TMN MEGAH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">85.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1024/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,024 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 85.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">85.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohd shahrul izam bin mohd jali" data-branch="kajang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD SHAHRUL IZAM BIN MOHD JALI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KAJANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">85.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1033/1208</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,033 / 1,208 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 85.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">85.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="afiq mirza bin romidi" data-branch="glenmarie">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AFIQ MIRZA BIN ROMIDI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> GLENMARIE, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">85.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1025/1201</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,025 / 1,201 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 85.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">85.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhamad aisar bin mohd nizam" data-branch="p. medan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMAD AISAR BIN MOHD NIZAM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. MEDAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">85.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1017/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,017 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 85.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">85.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad aliff iskandar bin mohamed hatal" data-branch="ipoh">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ALIFF ISKANDAR BIN MOHAMED HATAL</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> IPOH, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">85.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1026/1207</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,026 / 1,207 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 85.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">85.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad syahiran bin sueilan" data-branch="puchong">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD SYAHIRAN BIN SUEILAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PUCHONG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">84.8%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1020/1203</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,020 / 1,203 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 84.8%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">84.8%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="danial fakhry bin jani" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">DANIAL FAKHRY BIN JANI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">84.8%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1014/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,014 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 84.8%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">84.8%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohamad normuzamil bin azlan" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD NORMUZAMIL BIN AZLAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">84.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1022/1206</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,022 / 1,206 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 84.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">84.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="abdul mubin bin hapidz" data-branch="okr">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">ABDUL MUBIN BIN HAPIDZ</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> OKR, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">84.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1756/2079</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,756 / 2,079 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 84.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">84.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="adli bin amir" data-branch="s. alam">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">ADLI BIN AMIR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> S. ALAM, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">84.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1017/1210</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,017 / 1,210 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 84.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">84.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="mohamad amirul azreen bin roslan" data-branch="kuantan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD AMIRUL AZREEN BIN ROSLAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KUANTAN, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">83.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">1000/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,000 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 83.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">83.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="ahmad syawal fikri bin ahmad jafri" data-branch="melawati">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AHMAD SYAWAL FIKRI BIN AHMAD JAFRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MELAWATI, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">83.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">693/830</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 693 / 830 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 83.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">83.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad firdaus bin norizal" data-branch="putrajaya">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD FIRDAUS BIN NORIZAL</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PUTRAJAYA, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">83.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">819/986</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 819 / 986 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 83.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">83.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="rakin bin mohd ruzi" data-branch="p. medan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">RAKIN BIN MOHD RUZI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. MEDAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">83.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2941/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,941 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 83.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">83.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="ahmad dhiyauddin bin roslan" data-branch="glenmarie">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AHMAD DHIYAUDDIN BIN ROSLAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> GLENMARIE, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">82.8%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">990/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 990 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 82.8%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">82.8%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohamad afiq ikwan bin norizan" data-branch="s. alam">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD AFIQ IKWAN BIN NORIZAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> S. ALAM, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">82.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">988/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 988 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 82.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">82.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad ammar rafiq bin ismail" data-branch="ipoh">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD AMMAR RAFIQ BIN ISMAIL</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> IPOH, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">82.2%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">982/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">6/6</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 988 / 1,202 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 82.2%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">82.2%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="mohamad amir asyraf bin abdul halim" data-branch="kuantan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD AMIR ASYRAF BIN ABDUL HALIM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KUANTAN, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">82.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">985/1200</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 985 / 1,200 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 82.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">82.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhamad ikram bin nurun azman" data-branch="tmn megah">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMAD IKRAM BIN NURUN AZMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> TMN MEGAH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">81.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">977/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 977 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 81.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">81.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="hasrulazwan bin hassan" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">HASRULAZWAN BIN HASSAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">81.2%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">507/624</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 507 / 624 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 81.2%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">81.2%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="muhammad fazrul bin hasni" data-branch="kuantan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD FAZRUL BIN HASNI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KUANTAN, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">80.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2833/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,833 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill " style="width: 80.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">80.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad fadhilah bin baharin" data-branch="melaka">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD FADHILAH BIN BAHARIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MELAKA, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">79.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2821/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,821 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 79.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">79.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad hanif hizwan bin md halid" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD HANIF HIZWAN BIN MD HALID</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">79.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">4/4</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1576/1980</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,580 / 1,984 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 79.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">79.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad nabil mubasyir bin mohd zamri" data-branch="selayang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD NABIL MUBASYIR BIN MOHD ZAMRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SELAYANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">79.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">949/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 949 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 79.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">79.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="abdul rahim bin sabrun" data-branch="okr">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">ABDUL RAHIM BIN SABRUN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> OKR, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">79.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">943/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">7/7</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 950 / 1,203 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 79.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">79.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="sharwin pillai a/l kalaichelvan" data-branch="sg. buloh">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">SHARWIN PILLAI A/L KALAICHELVAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SG. BULOH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">78.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">783/996</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 783 / 996 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 78.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">78.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad hamirul hakim" data-branch="selayang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD HAMIRUL HAKIM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SELAYANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">77.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">932/1197</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 932 / 1,197 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 77.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">77.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohamad razif bin abdul rahim" data-branch="selayang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD RAZIF BIN ABDUL RAHIM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SELAYANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">77.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">549/607</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1216/1668</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,765 / 2,275 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 77.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">77.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad ikhmal bin mohd razi" data-branch="selayang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD IKHMAL BIN MOHD RAZI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SELAYANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">77.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1535/1978</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,535 / 1,978 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 77.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">77.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohd izzat bin ghazali" data-branch="s. alam">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD IZZAT BIN GHAZALI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> S. ALAM, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">77.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1584/2050</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,584 / 2,050 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 77.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">77.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad najmi bin mohd zaki" data-branch="p. juru">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD NAJMI BIN MOHD ZAKI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. JURU, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">76.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">160/208</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 160 / 208 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 76.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">76.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad shahid bin suhai" data-branch="melaka">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD SHAHID BIN SUHAI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MELAKA, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">76.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">912/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">13/13</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 925 / 1,209 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 76.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">76.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad aizat helmy bin abu hassan" data-branch="puchong">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD AIZAT HELMY BIN ABU HASSAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PUCHONG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">76.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2706/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,706 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 76.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">76.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhamad fazli bin ab hamid" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMAD FAZLI BIN AB HAMID</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">76.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">158/208</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 158 / 208 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 76.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">76.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="shukhaizi bin misbah" data-branch="p. south">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">SHUKHAIZI BIN MISBAH</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. SOUTH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">76.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">158/208</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 158 / 208 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 76.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">76.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohamad hafizulhilmy bin maseran" data-branch="jb eco">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD HAFIZULHILMY BIN MASERAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> JB ECO, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">75.8%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">473/624</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 473 / 624 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 75.8%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">75.8%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad nurkamaluddin bin mohd ahirwa" data-branch="b. pahat">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD NURKAMALUDDIN BIN MOHD AHIRWA</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> B. PAHAT, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">75.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">901/1199</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">13/13</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 914 / 1,212 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 75.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">75.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohammad mazzuan haqimi bin zamri" data-branch="seremban">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMMAD MAZZUAN HAQIMI BIN ZAMRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SEREMBAN, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">74.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">893/1199</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">8/8</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 901 / 1,207 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 74.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">74.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad muhaimin bin shaiful zam zam" data-branch="melaka">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD MUHAIMIN BIN SHAIFUL ZAM ZAM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MELAKA, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">74.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">889/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">7/7</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 896 / 1,203 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 74.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">74.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad ammar bin bahri" data-branch="sg. petani">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD AMMAR BIN BAHRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SG. PETANI, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">72.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">774/1062</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 774 / 1,062 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 72.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">72.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="ahmad thalha bin pisal" data-branch="seremban">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AHMAD THALHA BIN PISAL</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SEREMBAN, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">72.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2572/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,572 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 72.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">72.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="khoirul rijal bin abd hamid khan" data-branch="ampang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">KHOIRUL RIJAL BIN ABD HAMID KHAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> AMPANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">71.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">728/1018</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 728 / 1,018 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 71.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">71.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad firdaus bin maselan" data-branch="p. bayan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD FIRDAUS BIN MASELAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. BAYAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">71.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">482/528</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1086/1668</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,568 / 2,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 71.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">71.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="khairul abid bin khairi" data-branch="p. juru">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">KHAIRUL ABID BIN KHAIRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. JURU, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">71.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">847/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">8/8</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 855 / 1,204 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 71.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">71.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="ku muhammad adam bin ku mohd rozi" data-branch="a. setar">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">KU MUHAMMAD ADAM BIN KU MOHD ROZI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> A. SETAR, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">69.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2453/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,453 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 69.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">69.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad ikhmal hakim bin m.hiduwan" data-branch="sg. buloh">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD IKHMAL HAKIM BIN M.HIDUWAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SG. BULOH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">68.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">534/532</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">962/1668</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,496 / 2,200 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 68.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">68.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohd syafiq bin mohd faisal" data-branch="p. bayan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD SYAFIQ BIN MOHD FAISAL</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. BAYAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">66.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">15/19</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1315/1993</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,330 / 2,012 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 66.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">66.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohammad faiz bin izhar" data-branch="pantrans">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMMAD FAIZ BIN IZHAR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PANTRANS, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">64.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1528/2356</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,528 / 2,356 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 64.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">64.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="qusyairy daniel bin yusdy" data-branch="k. bharu">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">QUSYAIRY DANIEL BIN YUSDY</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> K. BHARU, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">64.0%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">6/6</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">2264/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 2,270 / 3,546 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 64.0%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">64.0%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad annas bin mohd yusoff" data-branch="a. setar">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ANNAS BIN MOHD YUSOFF</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> A. SETAR, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">63.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">764/1196</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 764 / 1,196 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 63.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">63.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="mohd hanif bin jamaludin" data-branch="p. bayan">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD HANIF BIN JAMALUDIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. BAYAN, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">63.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">148/245</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">22/22</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 170 / 267 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 63.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">63.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad isma syukran bin azman" data-branch="s. alam">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ISMA SYUKRAN BIN AZMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> S. ALAM, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">63.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">132/208</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 132 / 208 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 63.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">63.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="arif sufi bin mohamed" data-branch="k. terengganu">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">ARIF SUFI BIN MOHAMED</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> K. TERENGGANU, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">59.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">402/694</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">35/35</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 437 / 729 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 59.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">59.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST MALAYSIA" data-name="ronald majin" data-branch="k. kinabalu">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">RONALD MAJIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> K. KINABALU, EAST MALAYSIA
                        </div>
                    </div>
                    <span class="staff-badge">59.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">429/720</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 429 / 720 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 59.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">59.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST COAST" data-name="adib wa'ie bin mohamad ghani" data-branch="k. terengganu">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">ADIB WA'IE BIN MOHAMAD GHANI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> K. TERENGGANU, EAST COAST
                        </div>
                    </div>
                    <span class="staff-badge">58.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">307/372</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1154/2130</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,461 / 2,502 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 58.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">58.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="NORTHERN" data-name="muhammad zafran bin zamri" data-branch="sg. petani">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ZAFRAN BIN ZAMRI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SG. PETANI, NORTHERN
                        </div>
                    </div>
                    <span class="staff-badge">55.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">383/416</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">941/1980</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,324 / 2,396 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 55.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">55.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad sauqi bin jamaludin" data-branch="b. pahat">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD SAUQI BIN JAMALUDIN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> B. PAHAT, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">54.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1928/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,928 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill low" style="width: 54.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">54.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad shazwan shafiq bin mohd yusni" data-branch="okr">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD SHAZWAN SHAFIQ BIN MOHD YUSNI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> OKR, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">47.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">678/1416</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 678 / 1,416 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 47.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">47.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="muhammad rusydi bin azman" data-branch="muar">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD RUSYDI BIN AZMAN</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MUAR, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">46.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">481/1068</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">21/21</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 502 / 1,089 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 46.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">46.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad ariffin bin muhammad siddiq ravishanker" data-branch="setapak">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ARIFFIN BIN MUHAMMAD SIDDIQ RAVISHANKER</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> SETAPAK, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">44.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">430/567</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">564/1668</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 994 / 2,235 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 44.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">44.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST MALAYSIA" data-name="mohd firdaus yakup" data-branch="kuching">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD FIRDAUS YAKUP</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KUCHING, EAST MALAYSIA
                        </div>
                    </div>
                    <span class="staff-badge">39.3%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">382/972</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 382 / 972 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 39.3%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">39.3%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST MALAYSIA" data-name="muhammad islan bin tiblani" data-branch="k. kinabalu">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ISLAN BIN TIBLANI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> K. KINABALU, EAST MALAYSIA
                        </div>
                    </div>
                    <span class="staff-badge">36.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">222/262</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">737/2364</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 959 / 2,626 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 36.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">36.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad zuqni bin mahmud" data-branch="p. south">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD ZUQNI BIN MAHMUD</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> P. SOUTH, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">35.9%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">163/176</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">948/2916</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,111 / 3,092 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 35.9%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">35.9%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="mohamad shahrul haikal bin anuar" data-branch="pj midtown">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHAMAD SHAHRUL HAIKAL BIN ANUAR</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PJ MIDTOWN, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">33.6%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">75/104</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1046/3228</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,121 / 3,332 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 33.6%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">33.6%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="ahmad zakwan bin hisham" data-branch="ampang">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">AHMAD ZAKWAN BIN HISHAM</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> AMPANG, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">33.5%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1185/3540</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,185 / 3,540 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 33.5%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">33.5%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST MALAYSIA" data-name="riduan bin raiming" data-branch="tawau">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">RIDUAN BIN RAIMING</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> TAWAU, EAST MALAYSIA
                        </div>
                    </div>
                    <span class="staff-badge">30.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">264/449</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">455/1920</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 719 / 2,369 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 30.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">30.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhammad farid bin mohammad johari" data-branch="putrajaya">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHAMMAD FARID BIN MOHAMMAD JOHARI</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> PUTRAJAYA, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">29.7%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">1045/3516</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 1,045 / 3,516 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 29.7%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">29.7%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="SOUTHERN" data-name="mohd hanif bin mohd yazid" data-branch="muar">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MOHD HANIF BIN MOHD YAZID</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MUAR, SOUTHERN
                        </div>
                    </div>
                    <span class="staff-badge">21.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">0/0</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">753/3516</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 753 / 3,516 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 21.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">21.4%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="KLANG VALLEY" data-name="muhd hafizuddin bin latif" data-branch="melawati">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">MUHD HAFIZUDDIN BIN LATIF</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> MELAWATI, KLANG VALLEY
                        </div>
                    </div>
                    <span class="staff-badge">21.1%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">150/144</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">487/2868</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 637 / 3,012 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 21.1%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">21.1%</span>
                </div>
            </div>

            <div class="staff-card animate-in" data-region="EAST MALAYSIA" data-name="kelvin kalang anak gura" data-branch="kuching">
                <div class="staff-header">
                    <div>
                        <div class="staff-name">KELVIN KALANG ANAK GURA</div>
                        <div class="staff-meta">
                            <i class="fas fa-map-marker-alt"></i> KUCHING, EAST MALAYSIA
                        </div>
                    </div>
                    <span class="staff-badge">15.4%</span>
                </div>
                <div class="staff-stats">
                    <div class="stat-box">
                        <div class="stat-value">16/16</div>
                        <div class="stat-label">Mobile Slots</div>
                    </div>
                    <div class="stat-box inhouse">
                        <div class="stat-value">522/3468</div>
                        <div class="stat-label">Inhouse Slots</div>
                    </div>
                </div>
                <div style="font-size: 0.75rem; color: var(--text-light); margin-bottom: 0.25rem;">
                    Total: 538 / 3,484 slots
                </div>
                <div class="progress-bar">
                    <div class="progress-fill critical" style="width: 15.4%"></div>
                </div>
                <div class="util-text">
                    <span>Utilization</span>
                    <span class="value">15.4%</span>
                </div>
            </div>

        </div>

        <!-- Branch Productivity Table -->
        <div class="section-header">
            <h2><i class="fas fa-table"></i> Branch Productivity Breakdown</h2>
            <div class="section-line"></div>
        </div>

        <div class="table-card">
            <h3><i class="fas fa-building"></i> Branch Performance by Region</h3>
            <table>
                <thead>
                    <tr>
                        <th>Region</th>
                        <th>Branch</th>
                        <th>Staff</th>
                        <th>Open Mobile</th>
                        <th>Used Mobile</th>
                        <th>Mobile %</th>
                        <th>Open Inhouse</th>
                        <th>Used Inhouse</th>
                        <th>Inhouse %</th>
                        <th>Total Open</th>
                        <th>Total Used</th>
                        <th>Overall %</th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>KAJANG</td>
                        <td style="text-align:center">3</td>
                        <td style="text-align:right">1,822</td>
                        <td style="text-align:right">1,588</td>
                        <td><span class="util-pill high">87.2%</span></td>
                        <td style="text-align:right">3,545</td>
                        <td style="text-align:right">3,448</td>
                        <td><span class="util-pill high">97.3%</span></td>
                        <td style="text-align:right"><strong>5,367</strong></td>
                        <td style="text-align:right"><strong>5,036</strong></td>
                        <td><span class="util-pill high">93.8%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>CHERAS</td>
                        <td style="text-align:center">5</td>
                        <td style="text-align:right">2,737</td>
                        <td style="text-align:right">2,589</td>
                        <td><span class="util-pill high">94.6%</span></td>
                        <td style="text-align:right">7,605</td>
                        <td style="text-align:right">7,040</td>
                        <td><span class="util-pill high">92.6%</span></td>
                        <td style="text-align:right"><strong>10,342</strong></td>
                        <td style="text-align:right"><strong>9,629</strong></td>
                        <td><span class="util-pill high">93.1%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>PANTRANS</td>
                        <td style="text-align:center">8</td>
                        <td style="text-align:right">4</td>
                        <td style="text-align:right">4</td>
                        <td><span class="util-pill high">100.0%</span></td>
                        <td style="text-align:right">23,432</td>
                        <td style="text-align:right">21,197</td>
                        <td><span class="util-pill high">90.5%</span></td>
                        <td style="text-align:right"><strong>23,436</strong></td>
                        <td style="text-align:right"><strong>21,201</strong></td>
                        <td><span class="util-pill high">90.5%</span></td>
                    </tr>

                    <tr>
                        <td><strong>NORTHERN</strong></td>
                        <td>IPOH</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">2,403</td>
                        <td style="text-align:right">2,008</td>
                        <td><span class="util-pill high">83.6%</span></td>
                        <td style="text-align:right">4,489</td>
                        <td style="text-align:right">4,048</td>
                        <td><span class="util-pill high">90.2%</span></td>
                        <td style="text-align:right"><strong>6,892</strong></td>
                        <td style="text-align:right"><strong>6,056</strong></td>
                        <td><span class="util-pill high">87.9%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>GLENMARIE</td>
                        <td style="text-align:center">5</td>
                        <td style="text-align:right">3,606</td>
                        <td style="text-align:right">3,098</td>
                        <td><span class="util-pill high">85.9%</span></td>
                        <td style="text-align:right">3,843</td>
                        <td style="text-align:right">3,371</td>
                        <td><span class="util-pill high">87.7%</span></td>
                        <td style="text-align:right"><strong>7,449</strong></td>
                        <td style="text-align:right"><strong>6,469</strong></td>
                        <td><span class="util-pill high">86.8%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>TMN MEGAH</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">2,392</td>
                        <td style="text-align:right">2,001</td>
                        <td><span class="util-pill high">83.7%</span></td>
                        <td style="text-align:right">3,862</td>
                        <td style="text-align:right">3,412</td>
                        <td><span class="util-pill high">88.3%</span></td>
                        <td style="text-align:right"><strong>6,254</strong></td>
                        <td style="text-align:right"><strong>5,413</strong></td>
                        <td><span class="util-pill high">86.6%</span></td>
                    </tr>

                    <tr>
                        <td><strong>NORTHERN</strong></td>
                        <td>P. JURU</td>
                        <td style="text-align:center">6</td>
                        <td style="text-align:right">2,613</td>
                        <td style="text-align:right">2,052</td>
                        <td><span class="util-pill medium">78.5%</span></td>
                        <td style="text-align:right">7,569</td>
                        <td style="text-align:right">6,705</td>
                        <td><span class="util-pill high">88.6%</span></td>
                        <td style="text-align:right"><strong>10,182</strong></td>
                        <td style="text-align:right"><strong>8,757</strong></td>
                        <td><span class="util-pill high">86.0%</span></td>
                    </tr>

                    <tr>
                        <td><strong>SOUTHERN</strong></td>
                        <td>JB ECO</td>
                        <td style="text-align:center">13</td>
                        <td style="text-align:right">4,977</td>
                        <td style="text-align:right">4,285</td>
                        <td><span class="util-pill high">86.1%</span></td>
                        <td style="text-align:right">14,032</td>
                        <td style="text-align:right">12,055</td>
                        <td><span class="util-pill high">85.9%</span></td>
                        <td style="text-align:right"><strong>19,009</strong></td>
                        <td style="text-align:right"><strong>16,340</strong></td>
                        <td><span class="util-pill high">86.0%</span></td>
                    </tr>

                    <tr>
                        <td><strong>NORTHERN</strong></td>
                        <td>P. MEDAN</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">2,397</td>
                        <td style="text-align:right">2,047</td>
                        <td><span class="util-pill high">85.4%</span></td>
                        <td style="text-align:right">4,101</td>
                        <td style="text-align:right">3,502</td>
                        <td><span class="util-pill high">85.4%</span></td>
                        <td style="text-align:right"><strong>6,498</strong></td>
                        <td style="text-align:right"><strong>5,549</strong></td>
                        <td><span class="util-pill high">85.4%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>S. ALAM</td>
                        <td style="text-align:center">6</td>
                        <td style="text-align:right">4,126</td>
                        <td style="text-align:right">3,457</td>
                        <td><span class="util-pill high">83.8%</span></td>
                        <td style="text-align:right">4,654</td>
                        <td style="text-align:right">3,860</td>
                        <td><span class="util-pill high">82.9%</span></td>
                        <td style="text-align:right"><strong>8,780</strong></td>
                        <td style="text-align:right"><strong>7,317</strong></td>
                        <td><span class="util-pill high">83.3%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST COAST</strong></td>
                        <td>KUANTAN</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">2,396</td>
                        <td style="text-align:right">1,985</td>
                        <td><span class="util-pill high">82.8%</span></td>
                        <td style="text-align:right">3,980</td>
                        <td style="text-align:right">3,273</td>
                        <td><span class="util-pill high">82.2%</span></td>
                        <td style="text-align:right"><strong>6,376</strong></td>
                        <td style="text-align:right"><strong>5,258</strong></td>
                        <td><span class="util-pill high">82.5%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>PUCHONG</td>
                        <td style="text-align:center">3</td>
                        <td style="text-align:right">1,203</td>
                        <td style="text-align:right">1,020</td>
                        <td><span class="util-pill high">84.8%</span></td>
                        <td style="text-align:right">4,076</td>
                        <td style="text-align:right">3,242</td>
                        <td><span class="util-pill medium">79.5%</span></td>
                        <td style="text-align:right"><strong>5,279</strong></td>
                        <td style="text-align:right"><strong>4,262</strong></td>
                        <td><span class="util-pill high">80.7%</span></td>
                    </tr>

                    <tr>
                        <td><strong>SOUTHERN</strong></td>
                        <td>SEREMBAN</td>
                        <td style="text-align:center">3</td>
                        <td style="text-align:right">1,199</td>
                        <td style="text-align:right">893</td>
                        <td><span class="util-pill medium">74.5%</span></td>
                        <td style="text-align:right">5,081</td>
                        <td style="text-align:right">4,113</td>
                        <td><span class="util-pill high">80.9%</span></td>
                        <td style="text-align:right"><strong>6,280</strong></td>
                        <td style="text-align:right"><strong>5,006</strong></td>
                        <td><span class="util-pill medium">79.7%</span></td>
                    </tr>

                    <tr>
                        <td><strong>SOUTHERN</strong></td>
                        <td>MELAKA</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">2,392</td>
                        <td style="text-align:right">1,801</td>
                        <td><span class="util-pill medium">75.3%</span></td>
                        <td style="text-align:right">3,939</td>
                        <td style="text-align:right">3,220</td>
                        <td><span class="util-pill high">81.7%</span></td>
                        <td style="text-align:right"><strong>6,331</strong></td>
                        <td style="text-align:right"><strong>5,021</strong></td>
                        <td><span class="util-pill medium">79.3%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>SELAYANG</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">3,000</td>
                        <td style="text-align:right">2,430</td>
                        <td><span class="util-pill high">81.0%</span></td>
                        <td style="text-align:right">3,646</td>
                        <td style="text-align:right">2,751</td>
                        <td><span class="util-pill medium">75.5%</span></td>
                        <td style="text-align:right"><strong>6,646</strong></td>
                        <td style="text-align:right"><strong>5,181</strong></td>
                        <td><span class="util-pill medium">78.0%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>OKR</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">2,392</td>
                        <td style="text-align:right">1,979</td>
                        <td><span class="util-pill high">82.7%</span></td>
                        <td style="text-align:right">3,502</td>
                        <td style="text-align:right">2,441</td>
                        <td><span class="util-pill medium">69.7%</span></td>
                        <td style="text-align:right"><strong>5,894</strong></td>
                        <td style="text-align:right"><strong>4,420</strong></td>
                        <td><span class="util-pill medium">75.0%</span></td>
                    </tr>

                    <tr>
                        <td><strong>NORTHERN</strong></td>
                        <td>A. SETAR</td>
                        <td style="text-align:center">3</td>
                        <td style="text-align:right">1,196</td>
                        <td style="text-align:right">764</td>
                        <td><span class="util-pill medium">63.9%</span></td>
                        <td style="text-align:right">4,208</td>
                        <td style="text-align:right">3,121</td>
                        <td><span class="util-pill medium">74.2%</span></td>
                        <td style="text-align:right"><strong>5,404</strong></td>
                        <td style="text-align:right"><strong>3,885</strong></td>
                        <td><span class="util-pill medium">71.9%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>SG. BULOH</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">1,528</td>
                        <td style="text-align:right">1,317</td>
                        <td><span class="util-pill high">86.2%</span></td>
                        <td style="text-align:right">1,668</td>
                        <td style="text-align:right">962</td>
                        <td><span class="util-pill medium">57.7%</span></td>
                        <td style="text-align:right"><strong>3,196</strong></td>
                        <td style="text-align:right"><strong>2,279</strong></td>
                        <td><span class="util-pill medium">71.3%</span></td>
                    </tr>

                    <tr>
                        <td><strong>NORTHERN</strong></td>
                        <td>P. BAYAN</td>
                        <td style="text-align:center">4</td>
                        <td style="text-align:right">1,188</td>
                        <td style="text-align:right">1,030</td>
                        <td><span class="util-pill high">86.7%</span></td>
                        <td style="text-align:right">3,683</td>
                        <td style="text-align:right">2,423</td>
                        <td><span class="util-pill medium">65.8%</span></td>
                        <td style="text-align:right"><strong>4,871</strong></td>
                        <td style="text-align:right"><strong>3,453</strong></td>
                        <td><span class="util-pill medium">70.9%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST COAST</strong></td>
                        <td>K. BHARU</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">912</td>
                        <td style="text-align:right">871</td>
                        <td><span class="util-pill high">95.5%</span></td>
                        <td style="text-align:right">3,540</td>
                        <td style="text-align:right">2,264</td>
                        <td><span class="util-pill medium">64.0%</span></td>
                        <td style="text-align:right"><strong>4,452</strong></td>
                        <td style="text-align:right"><strong>3,135</strong></td>
                        <td><span class="util-pill medium">70.4%</span></td>
                    </tr>

                    <tr>
                        <td><strong>SOUTHERN</strong></td>
                        <td>B. PAHAT</td>
                        <td style="text-align:center">3</td>
                        <td style="text-align:right">1,201</td>
                        <td style="text-align:right">903</td>
                        <td><span class="util-pill medium">75.2%</span></td>
                        <td style="text-align:right">4,069</td>
                        <td style="text-align:right">2,457</td>
                        <td><span class="util-pill medium">60.4%</span></td>
                        <td style="text-align:right"><strong>5,270</strong></td>
                        <td style="text-align:right"><strong>3,360</strong></td>
                        <td><span class="util-pill medium">63.8%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>SETAPAK</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">1,199</td>
                        <td style="text-align:right">902</td>
                        <td><span class="util-pill medium">75.2%</span></td>
                        <td style="text-align:right">2,884</td>
                        <td style="text-align:right">1,680</td>
                        <td><span class="util-pill medium">58.3%</span></td>
                        <td style="text-align:right"><strong>4,083</strong></td>
                        <td style="text-align:right"><strong>2,582</strong></td>
                        <td><span class="util-pill medium">63.2%</span></td>
                    </tr>

                    <tr>
                        <td><strong>NORTHERN</strong></td>
                        <td>SG. PETANI</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">1,478</td>
                        <td style="text-align:right">1,157</td>
                        <td><span class="util-pill medium">78.3%</span></td>
                        <td style="text-align:right">1,980</td>
                        <td style="text-align:right">941</td>
                        <td><span class="util-pill low">47.5%</span></td>
                        <td style="text-align:right"><strong>3,458</strong></td>
                        <td style="text-align:right"><strong>2,098</strong></td>
                        <td><span class="util-pill medium">60.7%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST COAST</strong></td>
                        <td>K. TERENGGANU</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">1,066</td>
                        <td style="text-align:right">709</td>
                        <td><span class="util-pill medium">66.5%</span></td>
                        <td style="text-align:right">2,165</td>
                        <td style="text-align:right">1,189</td>
                        <td><span class="util-pill medium">54.9%</span></td>
                        <td style="text-align:right"><strong>3,231</strong></td>
                        <td style="text-align:right"><strong>1,898</strong></td>
                        <td><span class="util-pill medium">58.7%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>AMPANG</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">1,018</td>
                        <td style="text-align:right">728</td>
                        <td><span class="util-pill medium">71.5%</span></td>
                        <td style="text-align:right">3,540</td>
                        <td style="text-align:right">1,185</td>
                        <td><span class="util-pill low">33.5%</span></td>
                        <td style="text-align:right"><strong>4,558</strong></td>
                        <td style="text-align:right"><strong>1,913</strong></td>
                        <td><span class="util-pill low">42.0%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST MALAYSIA</strong></td>
                        <td>K. KINABALU</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">982</td>
                        <td style="text-align:right">651</td>
                        <td><span class="util-pill medium">66.3%</span></td>
                        <td style="text-align:right">2,364</td>
                        <td style="text-align:right">737</td>
                        <td><span class="util-pill low">31.2%</span></td>
                        <td style="text-align:right"><strong>3,346</strong></td>
                        <td style="text-align:right"><strong>1,388</strong></td>
                        <td><span class="util-pill low">41.5%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>PUTRAJAYA</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">986</td>
                        <td style="text-align:right">819</td>
                        <td><span class="util-pill high">83.1%</span></td>
                        <td style="text-align:right">3,516</td>
                        <td style="text-align:right">1,045</td>
                        <td><span class="util-pill low">29.7%</span></td>
                        <td style="text-align:right"><strong>4,502</strong></td>
                        <td style="text-align:right"><strong>1,864</strong></td>
                        <td><span class="util-pill low">41.4%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>P. SOUTH</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">384</td>
                        <td style="text-align:right">321</td>
                        <td><span class="util-pill high">83.6%</span></td>
                        <td style="text-align:right">2,916</td>
                        <td style="text-align:right">948</td>
                        <td><span class="util-pill low">32.5%</span></td>
                        <td style="text-align:right"><strong>3,300</strong></td>
                        <td style="text-align:right"><strong>1,269</strong></td>
                        <td><span class="util-pill low">38.5%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>MELAWATI</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">974</td>
                        <td style="text-align:right">843</td>
                        <td><span class="util-pill high">86.6%</span></td>
                        <td style="text-align:right">2,868</td>
                        <td style="text-align:right">487</td>
                        <td><span class="util-pill low">17.0%</span></td>
                        <td style="text-align:right"><strong>3,842</strong></td>
                        <td style="text-align:right"><strong>1,330</strong></td>
                        <td><span class="util-pill low">34.6%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td>PJ MIDTOWN</td>
                        <td style="text-align:center">1</td>
                        <td style="text-align:right">104</td>
                        <td style="text-align:right">75</td>
                        <td><span class="util-pill medium">72.1%</span></td>
                        <td style="text-align:right">3,228</td>
                        <td style="text-align:right">1,046</td>
                        <td><span class="util-pill low">32.4%</span></td>
                        <td style="text-align:right"><strong>3,332</strong></td>
                        <td style="text-align:right"><strong>1,121</strong></td>
                        <td><span class="util-pill low">33.6%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST MALAYSIA</strong></td>
                        <td>TAWAU</td>
                        <td style="text-align:center">1</td>
                        <td style="text-align:right">449</td>
                        <td style="text-align:right">264</td>
                        <td><span class="util-pill medium">58.8%</span></td>
                        <td style="text-align:right">1,920</td>
                        <td style="text-align:right">455</td>
                        <td><span class="util-pill low">23.7%</span></td>
                        <td style="text-align:right"><strong>2,369</strong></td>
                        <td style="text-align:right"><strong>719</strong></td>
                        <td><span class="util-pill low">30.4%</span></td>
                    </tr>

                    <tr>
                        <td><strong>SOUTHERN</strong></td>
                        <td>MUAR</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">1,068</td>
                        <td style="text-align:right">481</td>
                        <td><span class="util-pill low">45.0%</span></td>
                        <td style="text-align:right">3,537</td>
                        <td style="text-align:right">774</td>
                        <td><span class="util-pill low">21.9%</span></td>
                        <td style="text-align:right"><strong>4,605</strong></td>
                        <td style="text-align:right"><strong>1,255</strong></td>
                        <td><span class="util-pill low">27.3%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST MALAYSIA</strong></td>
                        <td>KUCHING</td>
                        <td style="text-align:center">2</td>
                        <td style="text-align:right">988</td>
                        <td style="text-align:right">398</td>
                        <td><span class="util-pill low">40.3%</span></td>
                        <td style="text-align:right">3,468</td>
                        <td style="text-align:right">522</td>
                        <td><span class="util-pill low">15.1%</span></td>
                        <td style="text-align:right"><strong>4,456</strong></td>
                        <td style="text-align:right"><strong>920</strong></td>
                        <td><span class="util-pill low">20.6%</span></td>
                    </tr>

                </tbody>
            </table>
        </div>

        <!-- Region Summary Table -->
        <div class="section-header">
            <h2><i class="fas fa-globe"></i> Regional Summary</h2>
            <div class="section-line"></div>
        </div>

        <div class="table-card">
            <h3><i class="fas fa-chart-bar"></i> Region Performance Overview</h3>
            <table>
                <thead>
                    <tr>
                        <th>Region</th>
                        <th>Staff Count</th>
                        <th>Open Mobile</th>
                        <th>Used Mobile</th>
                        <th>Mobile %</th>
                        <th>Open Inhouse</th>
                        <th>Used Inhouse</th>
                        <th>Inhouse %</th>
                        <th>Total Open</th>
                        <th>Total Used</th>
                        <th>Overall %</th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <td><strong>NORTHERN</strong></td>
                        <td style="text-align:center">23</td>
                        <td style="text-align:right">11,275</td>
                        <td style="text-align:right">9,058</td>
                        <td><span class="util-pill high">80.3%</span></td>
                        <td style="text-align:right">26,030</td>
                        <td style="text-align:right">20,740</td>
                        <td><span class="util-pill medium">79.7%</span></td>
                        <td style="text-align:right"><strong>37,305</strong></td>
                        <td style="text-align:right"><strong>29,798</strong></td>
                        <td><span class="util-pill medium">79.9%</span></td>
                    </tr>

                    <tr>
                        <td><strong>KLANG VALLEY</strong></td>
                        <td style="text-align:center">55</td>
                        <td style="text-align:right">27,475</td>
                        <td style="text-align:right">23,171</td>
                        <td><span class="util-pill high">84.3%</span></td>
                        <td style="text-align:right">78,785</td>
                        <td style="text-align:right">58,115</td>
                        <td><span class="util-pill medium">73.8%</span></td>
                        <td style="text-align:right"><strong>106,260</strong></td>
                        <td style="text-align:right"><strong>81,286</strong></td>
                        <td><span class="util-pill medium">76.5%</span></td>
                    </tr>

                    <tr>
                        <td><strong>SOUTHERN</strong></td>
                        <td style="text-align:center">25</td>
                        <td style="text-align:right">10,837</td>
                        <td style="text-align:right">8,363</td>
                        <td><span class="util-pill medium">77.2%</span></td>
                        <td style="text-align:right">30,658</td>
                        <td style="text-align:right">22,619</td>
                        <td><span class="util-pill medium">73.8%</span></td>
                        <td style="text-align:right"><strong>41,495</strong></td>
                        <td style="text-align:right"><strong>30,982</strong></td>
                        <td><span class="util-pill medium">74.7%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST COAST</strong></td>
                        <td style="text-align:center">8</td>
                        <td style="text-align:right">4,374</td>
                        <td style="text-align:right">3,565</td>
                        <td><span class="util-pill high">81.5%</span></td>
                        <td style="text-align:right">9,685</td>
                        <td style="text-align:right">6,726</td>
                        <td><span class="util-pill medium">69.4%</span></td>
                        <td style="text-align:right"><strong>14,059</strong></td>
                        <td style="text-align:right"><strong>10,291</strong></td>
                        <td><span class="util-pill medium">73.2%</span></td>
                    </tr>

                    <tr>
                        <td><strong>EAST MALAYSIA</strong></td>
                        <td style="text-align:center">5</td>
                        <td style="text-align:right">2,419</td>
                        <td style="text-align:right">1,313</td>
                        <td><span class="util-pill medium">54.3%</span></td>
                        <td style="text-align:right">7,752</td>
                        <td style="text-align:right">1,714</td>
                        <td><span class="util-pill low">22.1%</span></td>
                        <td style="text-align:right"><strong>10,171</strong></td>
                        <td style="text-align:right"><strong>3,027</strong></td>
                        <td><span class="util-pill low">29.8%</span></td>
                    </tr>

                </tbody>
            </table>
        </div>

        <footer style="text-align: center; padding: 2rem; color: var(--text-light); font-size: 0.85rem;">
            <p>Handover Inspection Productivity Dashboard 2025 &mdash; Generated on May 2026</p>
            <p style="margin-top: 0.5rem;"><i class="fas fa-chart-line" style="color: var(--primary);"></i> Data-driven insights for operational excellence</p>
        </footer>
    </div>

    <script>

        // Chart colors
        const primaryColor = '#FF4C00';
        const primaryLight = '#FF8A5C';
        const primaryMid = '#FFB088';
        const secondaryColor = '#FF6B35';
        const accentColor = '#FFF0E8';

        const chartColors = [
            '#FF4C00', '#FF6B35', '#FF8A5C', '#FFB088', '#FFD4C4',
            '#E85D04', '#F48C06', '#FAA307', '#FFBA08', '#6C757D'
        ];

        // Monthly Trend Chart
        const monthlyCtx = document.getElementById('monthlyChart').getContext('2d');
        new Chart(monthlyCtx, {
            type: 'line',
            data: {
                labels: ["Jan 2025", "Feb 2025", "Mar 2025", "Apr 2025", "May 2025", "Jun 2025", "Jul 2025", "Aug 2025", "Sep 2025", "Oct 2025", "Nov 2025", "Dec 2025"],
                datasets: [
                    {
                        label: 'Overall Utilization',
                        data: [65.5, 66.3, 72.5, 69.2, 82.0, 79.1, 80.3, 84.0, 79.9, 66.6, 73.4, 73.7],
                        borderColor: primaryColor,
                        backgroundColor: 'rgba(255, 76, 0, 0.1)',
                        borderWidth: 3,
                        tension: 0.4,
                        fill: true,
                        pointBackgroundColor: primaryColor,
                        pointBorderColor: '#fff',
                        pointBorderWidth: 2,
                        pointRadius: 5
                    },
                    {
                        label: 'Mobile Utilization',
                        data: [71.8, 70.4, 79.8, 75.0, 91.1, 81.2, 90.3, 87.2, 85.7, 72.1, 79.9, 78.8],
                        borderColor: '#FF8A5C',
                        backgroundColor: 'transparent',
                        borderWidth: 2,
                        borderDash: [5, 5],
                        tension: 0.4,
                        pointBackgroundColor: '#FF8A5C',
                        pointRadius: 4
                    },
                    {
                        label: 'Inhouse Utilization',
                        data: [63.7, 65.1, 70.3, 67.5, 79.4, 78.4, 75.7, 82.4, 77.3, 64.5, 70.5, 71.5],
                        borderColor: '#FFB088',
                        backgroundColor: 'transparent',
                        borderWidth: 2,
                        borderDash: [2, 2],
                        tension: 0.4,
                        pointBackgroundColor: '#FFB088',
                        pointRadius: 4
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                interaction: {
                    mode: 'index',
                    intersect: false
                },
                plugins: {
                    legend: {
                        position: 'top',
                        labels: {
                            usePointStyle: true,
                            padding: 15,
                            font: { family: 'Inter', size: 12 }
                        }
                    },
                    tooltip: {
                        backgroundColor: 'rgba(26, 26, 46, 0.9)',
                        titleFont: { family: 'Inter', size: 13 },
                        bodyFont: { family: 'Inter', size: 12 },
                        padding: 12,
                        cornerRadius: 8,
                        callbacks: {
                            label: function(context) {
                                return context.dataset.label + ': ' + context.parsed.y + '%';
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        max: 100,
                        grid: { color: 'rgba(0,0,0,0.05)' },
                        ticks: {
                            callback: function(value) { return value + '%'; },
                            font: { family: 'Inter' }
                        }
                    },
                    x: {
                        grid: { display: false },
                        ticks: { font: { family: 'Inter' } }
                    }
                }
            }
        });

        // Regional Comparison Chart
        const regionCtx = document.getElementById('regionChart').getContext('2d');
        new Chart(regionCtx, {
            type: 'bar',
            data: {
                labels: ["NORTHERN", "KLANG VALLEY", "SOUTHERN", "EAST COAST", "EAST MALAYSIA"],
                datasets: [
                    {
                        label: 'Overall Utilization %',
                        data: [79.9, 76.5, 74.7, 73.2, 29.8],
                        backgroundColor: chartColors.slice(0, 5),
                        borderRadius: 8,
                        borderSkipped: false
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: false },
                    tooltip: {
                        backgroundColor: 'rgba(26, 26, 46, 0.9)',
                        callbacks: {
                            label: function(context) {
                                return 'Utilization: ' + context.parsed.y + '%';
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        max: 100,
                        grid: { color: 'rgba(0,0,0,0.05)' },
                        ticks: {
                            callback: function(value) { return value + '%'; }
                        }
                    },
                    x: {
                        grid: { display: false }
                    }
                }
            }
        });

        // Branch Productivity Chart (Horizontal Bar)
        const branchCtx = document.getElementById('branchChart').getContext('2d');
        new Chart(branchCtx, {
            type: 'bar',
            data: {
                labels: ["PANTRANS", "JB ECO", "CHERAS", "P. JURU", "S. ALAM", "GLENMARIE", "IPOH", "SELAYANG", "P. MEDAN", "KUANTAN", "MELAKA", "SEREMBAN", "TMN MEGAH", "OKR", "A. SETAR"],
                datasets: [
                    {
                        label: 'Open Mobile',
                        data: [4, 4977, 2737, 2613, 4126, 3606, 2403, 3000, 2397, 2396, 2392, 1199, 2392, 2392, 1196],
                        backgroundColor: '#FFD4C4',
                        borderRadius: 4
                    },
                    {
                        label: 'Used Mobile',
                        data: [4, 4285, 2589, 2052, 3457, 3098, 2008, 2430, 2047, 1985, 1801, 893, 2001, 1979, 764],
                        backgroundColor: '#FF8A5C',
                        borderRadius: 4
                    },
                    {
                        label: 'Open Inhouse',
                        data: [23432, 14032, 7605, 7569, 4654, 3843, 4489, 3646, 4101, 3980, 3939, 5081, 3862, 3502, 4208],
                        backgroundColor: '#E5E7EB',
                        borderRadius: 4
                    },
                    {
                        label: 'Used Inhouse',
                        data: [21197, 12055, 7040, 6705, 3860, 3371, 4048, 2751, 3502, 3273, 3220, 4113, 3412, 2441, 3121],
                        backgroundColor: '#FF4C00',
                        borderRadius: 4
                    }
                ]
            },
            options: {
                indexAxis: 'y',
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'top',
                        labels: { usePointStyle: true, padding: 10 }
                    },
                    tooltip: {
                        backgroundColor: 'rgba(26, 26, 46, 0.9)',
                        callbacks: {
                            label: function(context) {
                                return context.dataset.label + ': ' + context.parsed.x.toLocaleString();
                            }
                        }
                    }
                },
                scales: {
                    x: {
                        grid: { color: 'rgba(0,0,0,0.05)' },
                        ticks: {
                            callback: function(value) { return value >= 1000 ? (value/1000).toFixed(0) + 'k' : value; }
                        }
                    },
                    y: {
                        grid: { display: false }
                    }
                }
            }
        });

        // Distribution Pie Chart
        const distCtx = document.getElementById('distributionChart').getContext('2d');
        new Chart(distCtx, {
            type: 'doughnut',
            data: {
                labels: ["NORTHERN", "KLANG VALLEY", "SOUTHERN", "EAST COAST", "EAST MALAYSIA"],
                datasets: [
                    {
                        data: [37305, 106260, 41495, 14059, 10171],
                        backgroundColor: chartColors.slice(0, 5),
                        borderWidth: 0,
                        hoverOffset: 10
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '60%',
                plugins: {
                    legend: {
                        position: 'right',
                        labels: {
                            usePointStyle: true,
                            padding: 15,
                            font: { family: 'Inter', size: 12 }
                        }
                    },
                    tooltip: {
                        backgroundColor: 'rgba(26, 26, 46, 0.9)',
                        callbacks: {
                            label: function(context) {
                                const total = context.dataset.data.reduce((a, b) => a + b, 0);
                                const pct = ((context.parsed / total) * 100).toFixed(1);
                                return context.label + ': ' + context.parsed.toLocaleString() + ' (' + pct + '%)';
                            }
                        }
                    }
                }
            }
        });

        // Staff filtering
        function filterStaff(region) {
            const cards = document.querySelectorAll('.staff-card');
            const buttons = document.querySelectorAll('.filter-btn');

            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            cards.forEach(card => {
                if (region === 'all' || card.dataset.region === region) {
                    card.style.display = 'block';
                    setTimeout(() => card.style.opacity = '1', 10);
                } else {
                    card.style.display = 'none';
                    card.style.opacity = '0';
                }
            });
        }

        // Staff search
        function searchStaff() {
            const query = document.getElementById('staffSearch').value.toLowerCase();
            const cards = document.querySelectorAll('.staff-card');

            cards.forEach(card => {
                const name = card.dataset.name;
                const branch = card.dataset.branch;
                if (name.includes(query) || branch.includes(query)) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        // Download PPTX function (placeholder - creates a simple alert)
        function downloadPPTX() {
            alert('PPTX Download Feature:\n\nIn a production environment, this would generate a PowerPoint presentation with all dashboard charts and tables.\n\nFor now, you can use the browser print function (Ctrl+P) to save as PDF, or export the data to Excel.');
        }

        // Intersection Observer for animations
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('.animate-in').forEach(el => {
            el.style.opacity = '0';
            el.style.transform = 'translateY(20px)';
            el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
            observer.observe(el);
        });
    </script>
</body>
</html>
