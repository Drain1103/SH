
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin - Work Account Dashboard</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #1a365d;
            --secondary-color: #2a4365;
            --accent-color: #3182ce;
            --text-color: #2d3748;
            --text-light: #718096;
            --bg-color: #f7fafc;
            --card-bg: #ffffff;
            --border-color: #e2e8f0;
            --error-color: #e53e3e;
            --success-color: #38a169;
            --warning-color: #ed8936;
            --info-color: #4299e1;
        }

        .dark-mode {
            --primary-color: #2d3748;
            --secondary-color: #1a202c;
            --accent-color: #4299e1;
            --text-color: #e2e8f0;
            --text-light: #a0aec0;
            --bg-color: #1a202c;
            --card-bg: #2d3748;
            --border-color: #4a5568;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            transition: background-color 0.3s, color 0.3s;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            min-height: 100vh;
            padding: 2rem 1rem;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
        }

        .title {
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--primary-color);
        }

        .mode-toggle {
            background: none;
            border: none;
            color: var(--text-light);
            font-size: 1.2rem;
            cursor: pointer;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
            padding: 2rem;
            margin-bottom: 1.5rem;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background-color: var(--card-bg);
            border-radius: 8px;
            padding: 1.25rem;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            display: flex;
            flex-direction: column;
        }

        .stat-title {
            font-size: 0.875rem;
            color: var(--text-light);
            margin-bottom: 0.5rem;
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--primary-color);
        }

        .search-container {
            display: flex;
            margin-bottom: 1.5rem;
        }

        .search-input {
            flex: 1;
            padding: 0.75rem 1rem;
            border: 1px solid var(--border-color);
            border-radius: 8px 0 0 8px;
            font-size: 1rem;
            background-color: var(--card-bg);
            color: var(--text-color);
        }

        .search-input:focus {
            outline: none;
            border-color: var(--accent-color);
        }

        .search-btn {
            padding: 0.75rem 1.25rem;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 0 8px 8px 0;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .search-btn:hover {
            background-color: var(--secondary-color);
        }

        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 1rem;
            text-align: left;
            border-bottom: 1px solid var(--border-color);
        }

        th {
            font-weight: 600;
            color: var(--text-light);
            background-color: rgba(0, 0, 0, 0.02);
        }

        tr:hover {
            background-color: rgba(0, 0, 0, 0.02);
        }

        .password-cell {
            position: relative;
        }

        .password-text {
            letter-spacing: 2px;
            font-family: monospace;
        }

        .toggle-password {
            position: absolute;
            right: 1rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-light);
            cursor: pointer;
        }

        .first-time {
            display: inline-block;
            padding: 0.25rem 0.5rem;
            border-radius: 4px;
            font-size: 0.75rem;
            font-weight: 500;
        }

        .first-time.yes {
            background-color: rgba(56, 161, 105, 0.15);
            color: var(--success-color);
        }

        .first-time.no {
            background-color: rgba(229, 62, 62, 0.15);
            color: var(--error-color);
        }

        .actions {
            display: flex;
            gap: 0.5rem;
        }

        .action-btn {
            background: none;
            border: none;
            color: var(--text-light);
            cursor: pointer;
            font-size: 1rem;
            padding: 0.25rem;
            border-radius: 4px;
            transition: background-color 0.3s, color 0.3s;
        }

        .action-btn:hover {
            background-color: rgba(0, 0, 0, 0.05);
            color: var(--accent-color);
        }

        .export-btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.75rem 1.25rem;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 0.875rem;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .export-btn:hover {
            background-color: var(--secondary-color);
        }

        .notification {
            position: fixed;
            top: 1rem;
            right: 1rem;
            padding: 1rem;
            border-radius: 8px;
            background-color: var(--success-color);
            color: white;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            transform: translateX(120%);
            transition: transform 0.3s;
            z-index: 1000;
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification.error {
            background-color: var(--error-color);
        }

        .login-form {
            max-width: 400px;
            margin: 0 auto;
        }

        .form-group {
            margin-bottom: 1.25rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: var(--text-color);
        }

        .form-input {
            width: 100%;
            padding: 0.75rem 1rem;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 1rem;
            background-color: var(--card-bg);
            color: var(--text-color);
            transition: border-color 0.3s;
        }

        .form-input:focus {
            outline: none;
            border-color: var(--accent-color);
            box-shadow: 0 0 0 3px rgba(49, 130, 206, 0.2);
        }

        .btn {
            display: block;
            width: 100%;
            padding: 0.75rem;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .btn:hover {
            background-color: var(--secondary-color);
        }

        .btn:disabled {
            background-color: var(--text-light);
            cursor: not-allowed;
        }

        .error-message {
            color: var(--error-color);
            font-size: 0.75rem;
            margin-top: 0.25rem;
            display: none;
        }

        .error-message.visible {
            display: block;
        }

        .login-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 2rem 1rem;
        }

        .login-card {
            background-color: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
            padding: 2rem;
            width: 100%;
            max-width: 400px;
        }

        .login-logo {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
            text-align: center;
        }

        .login-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
            text-align: center;
        }

        .hidden {
            display: none;
        }

        @media (max-width: 768px) {
            .stats {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="login-container" id="loginContainer">
        <div class="login-card">
            <div class="login-logo">Admin Portal</div>
            <h2 class="login-title">Admin Login</h2>
            <form class="login-form" id="adminLoginForm">
                <div class="form-group">
                    <label for="adminPin" class="form-label">Admin PIN</label>
                    <input type="password" id="adminPin" class="form-input" placeholder="Enter admin PIN" autocomplete="current-password">
                    <div class="error-message" id="adminPinError">Please enter the correct admin PIN</div>
                </div>
                <button type="submit" class="btn" id="adminLoginButton">Login</button>
            </form>
        </div>
    </div>

    <div class="container hidden" id="adminDashboard">
        <div class="header">
            <h1 class="title">Work Account Dashboard</h1>
            <button class="mode-toggle" id="modeToggle">
                <i class="fas fa-moon"></i>
            </button>
        </div>

        <div class="card">
            <div class="stats">
                <div class="stat-card">
                    <div class="stat-title">Total Accounts</div>
                    <div class="stat-value" id="totalAccounts">0</div>
                </div>
                <div class="stat-card">
                    <div class="stat-title">New Today</div>
                    <div class="stat-value" id="newToday">0</div>
                </div>
                <div class="stat-card">
                    <div class="stat-title">Reused Numbers</div>
                    <div class="stat-value" id="reusedNumbers">0</div>
                </div>
            </div>

            <div class="search-container">
                <input type="text" class="search-input" id="searchInput" placeholder="Search by phone number or date...">
                <button class="search-btn" id="searchBtn">
                    <i class="fas fa-search"></i>
                </button>
            </div>

            <div class="table-container">
                <table id="accountsTable">
                    <thead>
                        <tr>
                            <th>Phone Number</th>
                            <th>Password</th>
                            <th>Created At</th>
                            <th>First Time</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="accountsTableBody">
                        <!-- Table rows will be populated by JavaScript -->
                    </tbody>
                </table>
            </div>

            <div style="margin-top: 1.5rem; text-align: right;">
                <button class="export-btn" id="exportBtn">
                    <i class="fas fa-file-export"></i>
                    Export to CSV
                </button>
            </div>
        </div>
    </div>

    <div class="notification" id="notification">
        <span id="notificationText"></span>
    </div>

    <script>
        // DOM Elements
        const loginContainer = document.getElementById('loginContainer');
        const adminDashboard = document.getElementById('adminDashboard');
        const adminLoginForm = document.getElementById('adminLoginForm');
        const adminPin = document.getElementById('adminPin');
        const adminPinError = document.getElementById('adminPinError');
        const modeToggle = document.getElementById('modeToggle');
        const totalAccounts = document.getElementById('totalAccounts');
        const newToday = document.getElementById('newToday');
        const reusedNumbers = document.getElementById('reusedNumbers');
        const searchInput = document.getElementById('searchInput');
        const searchBtn = document.getElementById('searchBtn');
        const accountsTableBody = document.getElementById('accountsTableBody');
        const exportBtn = document.getElementById('exportBtn');
        const notification = document.getElementById('notification');
        const notificationText = document.getElementById('notificationText');

        // State
        let accounts = JSON.parse(localStorage.getItem('workAccounts')) || [];
        let isDarkMode = localStorage.getItem('darkMode') === 'true';
        const ADMIN_PIN = "1234"; // In a real app, this would be securely stored

        // Initialize
        if (isDarkMode) {
            document.body.classList.add('dark-mode');
            modeToggle.innerHTML = '<i class="fas fa-sun"></i>';
        }

        // Admin login
        adminLoginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const pin = adminPin.value.trim();
            
            if (pin === ADMIN_PIN) {
                loginContainer.classList.add('hidden');
                adminDashboard.classList.remove('hidden');
                updateDashboard();
                showNotification('Admin login successful!');
            } else {
                adminPin.classList.add('error');
                adminPinError.classList.add('visible');
                showNotification('Invalid admin PIN', true);
            }
        });

        // Dark mode toggle
        modeToggle.addEventListener('click', () => {
            isDarkMode = !isDarkMode;
            document.body.classList.toggle('dark-mode');
            modeToggle.innerHTML = isDarkMode ? '<i class="fas fa-sun"></i>' : '<i class="fas fa-moon"></i>';
            localStorage.setItem('darkMode', isDarkMode);
        });

        // Update dashboard stats and table
        function updateDashboard() {
            // Update stats
            totalAccounts.textContent = accounts.length;
            
            // Calculate new accounts today
            const today = new Date();
            today.setHours(0, 0, 0, 0);
            const newAccountsToday = accounts.filter(acc => {
                const createdDate = new Date(acc.createdAt);
                createdDate.setHours(0, 0, 0, 0);
                return createdDate.getTime() === today.getTime();
            }).length;
            
            newToday.textContent = newAccountsToday;
            
            // Calculate reused numbers
            const uniqueNumbers = new Set(accounts.map(acc => acc.phone));
            reusedNumbers.textContent = accounts.length - uniqueNumbers.size;
            
            // Update table
            renderAccountsTable(accounts);
        }

        // Render accounts table
        function renderAccountsTable(accountsToRender) {
            accountsTableBody.innerHTML = '';
            
            if (accountsToRender.length === 0) {
                const emptyRow = document.createElement('tr');
                const emptyCell = document.createElement('td');
                emptyCell.colSpan = 5;
                emptyCell.textContent = 'No accounts found';
                emptyCell.style.textAlign = 'center';
                emptyRow.appendChild(emptyCell);
                accountsTableBody.appendChild(emptyRow);
                return;
            }
            
            accountsToRender.forEach((account, index) => {
                const row = document.createElement('tr');
                
                // Phone number
                const phoneCell = document.createElement('td');
                phoneCell.textContent = account.phone;
                row.appendChild(phoneCell);
                
                // Password
                const passwordCell = document.createElement('td');
                passwordCell.className = 'password-cell';
                const passwordText = document.createElement('span');
                passwordText.className = 'password-text';
                passwordText.textContent = '******';
                passwordCell.appendChild(passwordText);
                
                const togglePassword = document.createElement('i');
                togglePassword.className = 'fas fa-eye toggle-password';
                togglePassword.addEventListener('click', () => {
                    if (passwordText.textContent === '******') {
                        passwordText.textContent = account.password;
                        togglePassword.classList.remove('fa-eye');
                        togglePassword.classList.add('fa-eye-slash');
                    } else {
                        passwordText.textContent = '******';
                        togglePassword.classList.remove('fa-eye-slash');
                        togglePassword.classList.add('fa-eye');
                    }
                });
                passwordCell.appendChild(togglePassword);
                row.appendChild(passwordCell);
                
                // Created at
                const createdAtCell = document.createElement('td');
                const createdDate = new Date(account.createdAt);
                createdAtCell.textContent = createdDate.toLocaleString();
                row.appendChild(createdAtCell);
                
                // First time
                const firstTimeCell = document.createElement('td');
                const firstTimeBadge = document.createElement('span');
                firstTimeBadge.className = `first-time ${account.isFirstTime ? 'yes' : 'no'}`;
                firstTimeBadge.textContent = account.isFirstTime ? 'Yes' : 'No';
                firstTimeCell.appendChild(firstTimeBadge);
                row.appendChild(firstTimeCell);
                
                // Actions
                const actionsCell = document.createElement('td');
                const actions = document.createElement('div');
                actions.className = 'actions';
                
                const refreshBtn = document.createElement('button');
                refreshBtn.className = 'action-btn';
                refreshBtn.innerHTML = '<i class="fas fa-sync-alt"></i>';
                refreshBtn.title = 'Refresh';
                refreshBtn.addEventListener('click', () => {
                    updateDashboard();
                    showNotification('Dashboard refreshed');
                });
                actions.appendChild(refreshBtn);
                
                row.appendChild(actionsCell);
                accountsTableBody.appendChild(row);
            });
        }

        // Search functionality
        searchBtn.addEventListener('click', () => {
            const searchTerm = searchInput.value.trim().toLowerCase();
            
            if (!searchTerm) {
                renderAccountsTable(accounts);
                return;
            }
            
            const filteredAccounts = accounts.filter(account => {
                const phoneMatch = account.phone.includes(searchTerm);
                const dateMatch = account.createdAt.toLowerCase().includes(searchTerm);
                return phoneMatch || dateMatch;
            });
            
            renderAccountsTable(filteredAccounts);
            
            if (filteredAccounts.length === 0) {
                showNotification('No matching accounts found', true);
            } else {
                showNotification(`Found ${filteredAccounts.length} matching accounts`);
            }
        });

        // Search on Enter key
        searchInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                searchBtn.click();
            }
        });

        // Export to CSV
        exportBtn.addEventListener('click', () => {
            if (accounts.length === 0) {
                showNotification('No accounts to export', true);
                return;
            }
            
            // Create CSV content
            const headers = ['Phone Number', 'Password', 'Created At', 'First Time'];
            let csvContent = headers.join(',') + '\n';
            
            accounts.forEach(account => {
                const row = [
                    account.phone,
                    account.password,
                    account.createdAt,
                    account.isFirstTime ? 'Yes' : 'No'
                ];
                csvContent += row.join(',') + '\n';
            });
            
            // Create download link
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.setAttribute('href', url);
            link.setAttribute('download', `work_accounts_${new Date().toISOString().split('T')[0]}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            showNotification('CSV export successful');
        });

        // Show notification
        function showNotification(message, isError = false) {
            notificationText.textContent = message;
            notification.classList.toggle('error', isError);
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // Initialize dashboard on page load
        document.addEventListener('DOMContentLoaded', () => {
            // In a real app, you might want to check if the user is already logged in
            // For this demo, we'll just show the login screen
        });
    </script>
</body>
</html>
