<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AEWorks Manager - Integrated Database Edition</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2c3e50;
            --primary-light: #3b536e;
            --accent: #3498db;
            --accent-light: #5dade2;
            --success: #2ecc71;
            --warning: #f39c12;
            --danger: #e74c3c;
            --light: #f8f9fa;
            --dark: #34495e;
            --gray: #95a5a6;
            --light-gray: #ecf0f1;
            --border-radius: 8px;
            --box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            --transition: all 0.3s ease;
        }
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        /* Login Modal */
        #loginModal {
            display: flex;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .login-box {
            background: white;
            padding: 30px;
            border-radius: var(--border-radius);
            width: 100%;
            max-width: 400px;
            text-align: center;
            box-shadow: var(--box-shadow);
        }
        .login-box h3 {
            margin-bottom: 20px;
            color: var(--primary);
        }
        .login-box input {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: var(--border-radius);
            font-size: 16px;
        }
        /* Header */
        header {
            text-align: center;
            margin-bottom: 25px;
            padding: 20px;
            background: linear-gradient(135deg, var(--primary), var(--dark));
            color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }
        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        /* User Bar */
        #userBar {
            background: var(--dark);
            color: white;
            padding: 12px 20px;
            text-align: right;
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        /* Toolbar */
        .toolbar {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 25px;
            background: white;
            padding: 15px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }
        .toolbar-group {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            flex: 1;
        }
        .btn {
            padding: 12px 18px;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            font-weight: bold;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 15px;
        }
        .btn i {
            font-size: 18px;
        }
        .btn-primary { background: var(--accent); color: white; }
        .btn-success { background: var(--success); color: white; }
        .btn-warning { background: var(--warning); color: white; }
        .btn-danger { background: var(--danger); color: white; }
        .btn-outline { background: transparent; border: 2px solid var(--primary); color: var(--primary); }
        .btn:hover { 
            transform: translateY(-2px); 
            box-shadow: 0 4px 8px rgba(0,0,0,0.15);
        }
        /* Tab System */
        .tab-container {
            width: 100%;
            box-shadow: var(--box-shadow);
            background-color: white;
            border-radius: var(--border-radius);
            overflow: hidden;
            margin-bottom: 30px;
        }
        .tab-buttons {
            display: flex;
            background-color: var(--primary);
            overflow-x: auto;
        }
        .tab-button {
            padding: 14px 24px;
            background: none;
            border: none;
            color: white;
            cursor: pointer;
            font-size: 15px;
            transition: 0.3s;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .tab-button:hover { background-color: rgba(255,255,255,0.1); }
        .tab-button.active {
            background-color: white;
            color: var(--primary);
            font-weight: bold;
            border-top-left-radius: var(--border-radius);
            border-top-right-radius: var(--border-radius);
        }
        .tab-content {
            display: none;
            padding: 25px;
            max-height: 60vh;
            overflow-y: auto;
        }
        .tab-content.active { display: block; }
        .tab-content h2 {
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--light-gray);
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--primary);
        }
        .tab-content .import-section {
            margin: 10px 0 20px 0;
            padding: 10px;
            background-color: #f0f3f5;
            border-radius: var(--border-radius);
        }
        .tab-content .import-section p {
            font-size: 13px;
            color: var(--dark);
            margin-top: 8px;
        }
        /* Tables */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }
        th {
            background-color: var(--dark);
            color: white;
            padding: 12px 15px;
            text-align: left;
            position: sticky;
            top: 0;
            z-index: 10;
            font-weight: 600;
        }
        td {
            padding: 12px 15px;
            border-bottom: 1px solid #eee;
        }
        .take-off-table td {
            padding: 8px 10px;
        }
        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 15px;
            transition: var(--transition);
        }
        input:disabled {
            background-color: #f1f1f1;
            cursor: not-allowed;
        }
        input:focus, select:focus, textarea:focus {
            border-color: var(--accent);
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }
        tr:nth-child(even) { background-color: #f9f9f9; }
        tr:hover { background-color: var(--light-gray); }
        .label {
            font-weight: bold;
            margin-bottom: 5px;
            color: var(--dark);
            font-size: 14px;
        }
        /* Footer */
        footer {
            text-align: center;
            margin-top: 40px;
            color: var(--gray);
            font-size: 14px;
            padding: 20px;
            border-top: 1px solid #eee;
        }
        /* Manage Pages */
        .manage-page {
            display: none;
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            padding: 25px;
            margin-bottom: 30px;
        }
        .manage-page h2 {
            margin-bottom: 20px;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .manage-page .import-section {
            margin: 20px 0;
            padding: 15px;
            background-color: var(--light-gray);
            border-radius: var(--border-radius);
            border: 1px solid #ddd;
        }
        .manage-page .import-section p {
            font-size: 14px;
            color: var(--dark);
            margin-top: 10px;
        }
        .back-btn {
            margin-bottom: 20px;
            background: var(--primary);
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            font-weight: bold;
        }
        /* Action buttons */
        .action-btn {
            padding: 6px 12px;
            margin: 0 3px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 13px;
            display: inline-flex;
            align-items: center;
            gap: 5px;
            transition: var(--transition);
        }
        .edit-btn { background-color: var(--accent); color: white; }
        .delete-btn { background-color: var(--danger); color: white; }
        .save-btn { background-color: var(--success); color: white; }
        .action-btn:hover { opacity: 0.9; transform: translateY(-2px); }
        /* Project Status Bar */
        .status-bar { display: flex; justify-content: space-between; background: white; padding: 15px; border-radius: var(--border-radius); box-shadow: var(--box-shadow); margin-bottom: 25px; overflow-x: auto; }
        .status-item { text-align: center; padding: 10px; min-width: 100px; opacity: 0.5; transition: var(--transition); }
        .status-indicator { width: 15px; height: 15px; border-radius: 50%; background: var(--gray); margin: 0 auto 10px; transition: var(--transition); }
        .status-item.active { opacity: 1; font-weight: bold; }
        .status-item.active .status-indicator { background: var(--success); box-shadow: 0 0 10px var(--success); }
        .status-name { font-size: 13px; font-weight: 500; }
        /* Project Preview & Modals */
        .project-preview { background: white; border-radius: var(--border-radius); padding: 20px; box-shadow: var(--box-shadow); margin-bottom: 20px; }
        .project-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }
        .project-title { font-size: 1.4rem; color: var(--primary); }
        .project-code { background: var(--light-gray); padding: 5px 10px; border-radius: 20px; font-weight: 500; color: var(--dark); }
        .project-details { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px; }
        .detail-item { display: flex; flex-direction: column; }
        .detail-label { font-size: 0.85rem; color: var(--gray); margin-bottom: 5px; }
        .detail-value { font-weight: 500; }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); justify-content: center; align-items: center; z-index: 1000; }
        .modal-content { background: white; padding: 30px; border-radius: var(--border-radius); width: 90%; max-width: 700px; max-height: 80vh; overflow-y: auto; box-shadow: 0 10px 30px rgba(0,0,0,0.3); }
        .modal-content h3 { margin-bottom: 20px; color: var(--primary); display: flex; align-items: center; gap: 10px; }
        .close-btn { margin-top: 20px; background: var(--danger); color: white; border: none; padding: 10px 20px; cursor: pointer; border-radius: var(--border-radius); font-weight: 500; display: inline-flex; align-items: center; gap: 8px; }
        /* Notification */
        .notification { position: fixed; top: 20px; right: 20px; padding: 15px 25px; border-radius: var(--border-radius); color: white; font-weight: 500; z-index: 1001; display: flex; align-items: center; gap: 10px; transform: translateX(120%); transition: transform 0.3s ease; }
        .notification.show { transform: translateX(0); }
        .notification.success { background-color: var(--success); }
        .notification.error { background-color: var(--danger); }
        .notification i { font-size: 20px; }
        /* Costing Tab Specifics */
        .costing-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(380px, 1fr)); gap: 30px; }
        .costing-section h3 { color: var(--primary); border-bottom: 2px solid var(--accent); padding-bottom: 8px; margin-bottom: 15px; }
        .costing-table { width: 100%; }
        .costing-table td { padding: 10px 5px; }
        .costing-table td:first-child { font-weight: 500; color: var(--dark); }
        .costing-table td:last-child { text-align: right; font-weight: bold; }
        .costing-table td small { color: var(--gray); font-weight: normal; margin-left: 8px; }
        .costing-table input[type=number] { text-align: right; padding-right: 5px; }
        .cost-summary-table tr.total-row td { border-top: 2px solid var(--dark); font-size: 1.1rem; }
        .cost-summary-table tr.grand-total-row td { font-size: 1.25rem; background-color: var(--primary-light); color: white; }
        /* Preview Details */
        .details-toggle { cursor: pointer; color: var(--accent); font-weight: bold; margin-top: 10px; display: inline-block; }
        .details-content { display: none; margin-top: 15px; border-top: 1px solid var(--light-gray); padding-top: 15px; }
        
        /* Work Manager Styles */
        .work-manager-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        
        .work-planning-section, .resource-allocation-section {
            background: #f8fafc;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }
        
        .work-section-title {
            color: #2c5282;
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 1px dashed #cbd5e0;
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .work-input-group {
            margin-bottom: 15px;
        }
        
        .work-input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #4a5568;
        }
        
        .work-input-group input {
            width: 100%;
            padding: 8px 12px;
            border: 1px solid #cbd5e0;
            border-radius: 4px;
        }
        
        .work-results {
            background: #edf2f7;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
        }
        
        .work-results h4 {
            margin-bottom: 10px;
            color: #2c5282;
        }
        
        .optimize-btn {
            background: #38a169;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            margin-top: 15px;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .reset-btn {
            background: #e53e3e;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            margin-top: 15px;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .role-allocation {
            margin-top: 15px;
        }
        
        .role-allocation h4 {
            margin-bottom: 10px;
            color: #2c5282;
        }
        
        .role-inputs {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }
        
        .resource-summary {
            margin-top: 20px;
            padding-top: 15px;
            border-top: 1px solid #cbd5e0;
        }
        
        .summary-row {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
        }
        
        .bottleneck {
            background: #fff9db;
            padding: 10px;
            border-radius: 4px;
            margin-top: 10px;
            font-weight: 600;
        }
        
        /* Invoice Styles */
        .invoice-container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 25px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        
        .invoice-header {
            background: linear-gradient(135deg, #1a3a6c, #2c5282);
            color: white;
            padding: 30px 40px;
            position: relative;
        }
        
        .company-name {
            font-size: 2.2rem;
            font-weight: 700;
            margin-bottom: 5px;
            letter-spacing: 0.5px;
        }
        
        .address {
            font-size: 1.1rem;
            opacity: 0.9;
            max-width: 70%;
        }
        
        .invoice-title {
            position: absolute;
            top: 30px;
            right: 40px;
            text-align: right;
        }
        
        .invoice-title h1 {
            font-size: 2.8rem;
            font-weight: 700;
            opacity: 0.8;
        }
        
        .invoice-content {
            padding: 30px 40px;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            margin-bottom: 25px;
        }
        
        .info-box {
            background: #f8fafc;
            border-radius: 8px;
            padding: 20px;
            border-left: 4px solid #2c5282;
        }
        
        .info-box h3 {
            color: #2c5282;
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 1px dashed #cbd5e0;
        }
        
        .info-row {
            display: flex;
            margin-bottom: 10px;
        }
        
        .info-label {
            font-weight: 600;
            min-width: 120px;
            color: #4a5568;
        }
        
        .shipping-info {
            background: #edf2f7;
            padding: 15px 20px;
            border-radius: 8px;
            margin-bottom: 25px;
            font-weight: 500;
        }
        
        .items-table {
            width: 100%;
            border-collapse: collapse;
            margin: 30px 0;
        }
        
        .items-table th {
            background: #2c5282;
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }
        
        .items-table td {
            padding: 15px;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .items-table tr:nth-child(even) {
            background-color: #f8fafc;
        }
        
        .items-table tr:last-child td {
            border-bottom: none;
        }
        
        .totals-section {
            display: flex;
            justify-content: space-between;
            margin: 30px 0;
        }
        
        .payment-info {
            flex: 1;
            background: #f8fafc;
            padding: 20px;
            border-radius: 8px;
            margin-right: 20px;
            border-left: 4px solid #38a169;
        }
        
        .payment-info h3 {
            color: #2c5282;
            margin-bottom: 15px;
        }
        
        .totals-table {
            background: #f0f7ff;
            border-radius: 8px;
            padding: 20px;
            min-width: 300px;
        }
        
        .total-row {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px dashed #cbd5e0;
        }
        
        .total-row:last-child {
            border-bottom: none;
        }
        
        .grand-total {
            font-size: 1.3rem;
            font-weight: 700;
            color: #1a3a6c;
            margin-top: 10px;
        }
        
        .terms-section {
            background: #edf2f7;
            padding: 25px;
            border-radius: 8px;
            margin: 30px 0;
        }
        
        .terms-section h3 {
            color: #2c5282;
            margin-bottom: 15px;
        }
        
        .terms-list {
            padding-left: 25px;
        }
        
        .terms-list li {
            margin-bottom: 10px;
        }
        
        .correspondence {
            display: flex;
            justify-content: space-between;
            padding: 20px;
            background: #f8fafc;
            border-radius: 8px;
        }
        
        .invoice-guide-section {
            background: white;
            margin-top: 40px;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }
        
        .invoice-guide-section h2 {
            color: #2c5282;
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 2px solid #e2e8f0;
        }
        
        .guide-table {
            width: 100%;
            border-collapse: collapse;
        }
        
        .guide-table th {
            background: #2c5282;
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }
        
        .guide-table td {
            padding: 15px;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .guide-table tr:nth-child(even) {
            background-color: #f8fafc;
        }
        
        .footer {
            text-align: center;
            padding: 25px;
            background: #1a202c;
            color: #a0aec0;
            margin-top: 40px;
        }
        
        /* Print Styles */
        @media print {
            body * {
                visibility: hidden;
            }
            .invoice-container, .invoice-container * {
                visibility: visible;
            }
            .invoice-container {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                max-width: 1000px;
            }
            .no-print {
                display: none !important;
            }
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .work-manager-container {
                grid-template-columns: 1fr;
            }
            
            .role-inputs {
                grid-template-columns: 1fr;
            }
            
            .info-grid {
                grid-template-columns: 1fr;
            }
            
            .totals-section {
                flex-direction: column;
            }
            
            .payment-info {
                margin-right: 0;
                margin-bottom: 20px;
            }
            
            .correspondence {
                flex-direction: column;
            }
            
            .invoice-title {
                position: relative;
                top: 0;
                right: 0;
                text-align: left;
                margin-top: 20px;
            }
        }
    </style>
</head>
<body>
    <!-- Login Modal -->
    <div id="loginModal"><div class="login-box"><h3><i class="fas fa-lock"></i> Login to AEWorks</h3><input type="text" id="username" placeholder="Username"><input type="password" id="password" placeholder="Password"><button class="btn btn-primary" onclick="login()" style="width:100%;margin-top:15px;"><i class="fas fa-sign-in-alt"></i> Login</button></div></div>
    <!-- Notification -->
    <div id="notification" class="notification"><i class="fas fa-check-circle"></i><span id="notificationText">Operation successful</span></div>
    <!-- Main App -->
    <div id="mainApp" class="container">
        <div id="userBar"><div id="userInfo"></div><button onclick="logout()" class="btn btn-danger"><i class="fas fa-sign-out-alt"></i> Logout</button></div>
        <header><h1><i class="fas fa-industry"></i> AEWorks Manager</h1><p>Integrated Project & Material Database System</p></header>
        <!-- Project Status Bar -->
        <div class="status-bar"><div class="status-item" data-status-value="0"><div class="status-indicator"></div><div class="status-name">Quote</div></div><div class="status-item" data-status-value="15"><div class="status-indicator"></div><div class="status-name">Started</div></div><div class="status-item" data-status-value="35"><div class="status-indicator"></div><div class="status-name">Procurement</div></div><div class="status-item" data-status-value="55"><div class="status-indicator"></div><div class="status-name">WIP</div></div><div class="status-item" data-status-value="75"><div class="status-indicator"></div><div class="status-name">Assembly</div></div><div class="status-item" data-status-value="85"><div class="status-indicator"></div><div class="status-name">Finishes</div></div><div class="status-item" data-status-value="90"><div class="status-indicator"></div><div class="status-name">Package</div></div><div class="status-item" data-status-value="95"><div class="status-indicator"></div><div class="status-name">Shipped</div></div><div class="status-item" data-status-value="100"><div class="status-indicator"></div><div class="status-name">Closeout</div></div></div>
        <div class="toolbar"><div class="toolbar-group"><button id="saveTemplate" class="btn btn-primary"><i class="fas fa-save"></i> Save</button><button id="loadTemplate" class="btn btn-success"><i class="fas fa-folder-open"></i> Load</button><button id="listProjects" class="btn btn-warning"><i class="fas fa-list"></i> List</button></div><div class="toolbar-group"><button id="manageClients" class="btn btn-outline"><i class="fas fa-users"></i> Clients</button><button id="manageContacts" class="btn btn-outline"><i class="fas fa-address-book"></i> Contacts</button><button id="manageCentres" class="btn btn-outline"><i class="fas fa-warehouse"></i> Centres</button><button id="manageMaterials" class="btn btn-outline"><i class="fas fa-boxes"></i> Materials</button></div></div>
        <div class="tab-container">
            <div class="tab-buttons">
                <button class="tab-button active" onclick="openTab(event, 'ProjectSpec')"><i class="fas fa-project-diagram"></i> Project</button>
                <button class="tab-button" onclick="openTab(event, 'FramingSpec')"><i class="fas fa-ruler-combined"></i> Framing</button>
                <button class="tab-button" onclick="openTab(event, 'FinishesSpec')"><i class="fas fa-paint-roller"></i> Finishes</button>
                <button class="tab-button" onclick="openTab(event, 'DeliverySpec')"><i class="fas fa-truck"></i> Delivery</button>
                <button class="tab-button" onclick="openTab(event, 'CostingSpec')"><i class="fas fa-calculator"></i> Costing</button>
                <button class="tab-button" onclick="openTab(event, 'WorkManager')"><i class="fas fa-tasks"></i> Work Manager</button>
                <button class="tab-button" onclick="openTab(event, 'Preview')"><i class="fas fa-eye"></i> Preview</button>
                <button class="tab-button" onclick="openTab(event, 'Invoice')"><i class="fas fa-file-invoice"></i> Invoice</button>
            </div>
            <!-- Project Tab -->
            <div id="ProjectSpec" class="tab-content active">
                <h2><i class="fas fa-cogs"></i> Project Specifications</h2>
                <table id="projectTable">
                    <tr><td><label for="projName">Project Name</label></td><td><input type="text" id="projName" oninput="generateProjectCode()"></td></tr>
                    <tr><td><label for="jobsThisYear">Jobs This Year</label></td><td><input type="number" id="jobsThisYear" value="1" oninput="generateProjectCode()"></td></tr>
                    <tr><td><label for="year">Year</label></td><td><input type="text" id="year" value="25" maxlength="2" oninput="generateProjectCode()"></td></tr>
                    <tr><td><label for="projectCode">Project Code</label></td><td><input type="text" id="projectCode" readonly></td></tr>
                    <tr><td><label for="projectStatus">Status</label></td><td><select id="projectStatus" onchange="updateStatusBar()"><option value="0">Quote Request</option><option value="5">Submit Quotation</option><option value="15">Started - Deposit</option><option value="35">Procurement</option><option value="55">Work In Progress - Parts</option><option value="75">Assembly</option><option value="85">Finishes</option><option value="90">Package</option><option value="95">Shipped</option><option value="100">Closeout</option></select></td></tr>
                    <tr><td><label for="prodCentre">Production Centre</label></td><td><select id="prodCentre" onchange="fillCentreData()"></select></td></tr>
                    <tr><td><label for="prodCoords">Production Coords</label></td><td><input type="text" id="prodCoords" readonly></td></tr>
                    <tr><td><label for="clientName">Client Name</label></td><td><select id="clientName" onchange="fillClientData()"></select></td></tr>
                    <tr><td><label for="clientMgr">Client Mgr.</label></td><td><input type="text" id="clientMgr"></td></tr>
                    <tr><td><label for="clientPhone">Client Phone</label></td><td><input type="text" id="clientPhone"></td></tr>
                    <tr><td><label for="clientEmail">Client Email</label></td><td><input type="email" id="clientEmail"></td></tr>
                    <tr><td><label for="clientAddr">Client Address</label></td><td><input type="text" id="clientAddr"></td></tr>
                    <tr><td><label for="destCitySelect">Destination City</label></td><td><select id="destCitySelect" onchange="handleCityChange()"></select></td></tr>
                    <tr><td><label for="destCoords">Destination Coords</label></td><td><input type="text" id="destCoords" placeholder="Select a city or choose custom"></td></tr>
                    <tr><td><label for="projMgr">Project Mgr.</label></td><td><select id="projMgr" onchange="fillContactData()"></select></td></tr>
                    <tr><td><label for="mgrPhone">Mgr Phone</label></td><td><input type="text" id="mgrPhone"></td></tr>
                    <tr><td><label for="mgrEmail">Mgr Email</label></td><td><input type="email" id="mgrEmail"></td></tr>
                </table>
            </div>
            <!-- Framing Tab -->
            <div id="FramingSpec" class="tab-content">
                <h2><i class="fas fa-ruler-combined"></i> Framing Material Take-Off</h2>
                <button onclick="addFramingRow()" class="btn btn-success"><i class="fas fa-plus"></i> Add Framing Item</button>
                <div class="import-section"><input type="file" id="framingTakeOffImport" accept=".csv" style="display:none;"><button onclick="document.getElementById('framingTakeOffImport').click()" class="btn btn-warning"><i class="fas fa-upload"></i> Import from CSV</button><p><strong>Required CSV Headers:</strong> Description,Framing Material,Length (m),Width (m),Quantity</p></div>
                <div style="overflow-x:auto;"><table id="framingTakeOffTable" class="take-off-table"><thead><tr><th>S/No</th><th style="width:30%;">Description</th><th style="width:35%;">Framing Material</th><th>Length (m)</th><th>Width (m)</th><th>Quantity</th><th>Actions</th></tr></thead><tbody id="framingTakeOffTableBody"></tbody></table></div>
            </div>
            <!-- Finishes Tab -->
            <div id="FinishesSpec" class="tab-content">
                <h2><i class="fas fa-paint-roller"></i> Finishes Material Take-Off</h2>
                <button onclick="addFinishRow()" class="btn btn-success"><i class="fas fa-plus"></i> Add Finish Item</button>
                <div class="import-section"><input type="file" id="finishesTakeOffImport" accept=".csv" style="display:none;"><button onclick="document.getElementById('finishesTakeOffImport').click()" class="btn btn-warning"><i class="fas fa-upload"></i> Import from CSV</button><p><strong>Required CSV Headers:</strong> Description,Finish Material,Quantity</p></div>
                <div style="overflow-x:auto;"><table id="finishesTakeOffTable" class="take-off-table"><thead><tr><th>S/No</th><th style="width:40%;">Description</th><th style="width:40%;">Finish Material</th><th>Quantity</th><th>Actions</th></tr></thead><tbody id="finishesTakeOffTableBody"></tbody></table></div>
            </div>
            <!-- Delivery Tab -->
            <div id="DeliverySpec" class="tab-content">
                <h2><i class="fas fa-truck"></i> Delivery & Shipping</h2>
                <p>Enter the dimensions of the final, assembled, and packaged shipment to calculate shipping costs.</p>
                <table id="deliveryTable">
                    <tr><td><label for="shippingLength">Overall Shippable Length (m)</label></td><td><input type="number" id="shippingLength" placeholder="e.g., 2.4"></td></tr>
                    <tr><td><label for="shippingWidth">Overall Shippable Width (m)</label></td><td><input type="number" id="shippingWidth" placeholder="e.g., 1.2"></td></tr>
                    <tr><td><label for="shippingHeight">Overall Shippable Height (m)</label></td><td><input type="number" id="shippingHeight" placeholder="e.g., 1.8"></td></tr>
                </table>
            </div>
            <!-- Costing Tab -->
            <div id="CostingSpec" class="tab-content">
                <h2><i class="fas fa-calculator"></i> Project Costing</h2>
                <button onclick="calculateProjectCostAndDisplay()" class="btn btn-primary" style="margin-bottom:20px;"><i class="fas fa-play-circle"></i> Calculate Costs</button>
                <div class="costing-grid">
                    <div class="costing-section" id="costingVariablesSection"><h3><i class="fas fa-sliders-h"></i> Costing Variables</h3><button onclick="saveCostingDefaults()" class="btn btn-outline" style="margin-top:-10px; margin-bottom: 15px;"><i class="fas fa-save"></i> Save as Default</button></div>
                    <div class="costing-section" id="costingResultsSection"><h3><i class="fas fa-chart-bar"></i> Cost Breakdown</h3></div>
                </div>
            </div>
            <!-- Work Manager Tab -->
            <div id="WorkManager" class="tab-content">
                <h2><i class="fas fa-tasks"></i> Work Manager</h2>
                <div class="work-manager-container">
                    <!-- Work Planning Section -->
                    <div class="work-planning-section">
                        <h3 class="work-section-title"><i class="fas fa-chart-line"></i> Work Planning</h3>
                        
                        <div class="work-input-group">
                            <label for="targetCompletionDays">Target Completion (days)</label>
                            <input type="number" id="targetCompletionDays" value="14" min="1">
                        </div>
                        
                        <div class="work-input-group">
                            <label for="workHoursPerDay">Work Hours Per Day</label>
                            <input type="number" id="workHoursPerDay" value="8" min="1" max="24">
                        </div>
                        
                        <div class="work-results">
                            <h4>Calculated Requirements</h4>
                            <div class="summary-row">
                                <span>Total Production Time:</span>
                                <span id="totalProductionTime">0 hours</span>
                            </div>
                            <div class="summary-row">
                                <span>Total Work Days Required:</span>
                                <span id="totalWorkDaysRequired">0 days</span>
                            </div>
                            <div class="summary-row">
                                <span>Recommended Team Size:</span>
                                <span id="recommendedTeamSize">0 people</span>
                            </div>
                            <div class="summary-row">
                                <span>Total Personnel Required:</span>
                                <span id="totalPersonnelRequired">0</span>
                            </div>
                        </div>
                        
                        <div class="work-input-group">
                            <label for="actualPersonnelAvailable">Actual Personnel Available</label>
                            <input type="number" id="actualPersonnelAvailable" value="5" min="1">
                        </div>
                        
                        <div class="work-results">
                            <h4>Project Timeline</h4>
                            <div class="summary-row">
                                <span>Estimated Completion Time:</span>
                                <span id="estimatedCompletionTime">0 days</span>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Resource Allocation Section -->
                    <div class="resource-allocation-section">
                        <h3 class="work-section-title"><i class="fas fa-users"></i> Resource Allocation</h3>
                        
                        <div class="role-allocation">
                            <h4>Personnel Allocation by Role</h4>
                            <div class="role-inputs">
                                <div class="work-input-group">
                                    <label for="partsProductionPersonnel">Parts Production</label>
                                    <input type="number" id="partsProductionPersonnel" value="2" min="0">
                                </div>
                                <div class="work-input-group">
                                    <label for="partsProductionTime">Time Required (hours)</label>
                                    <input type="text" id="partsProductionTime" value="0" readonly>
                                </div>
                                
                                <div class="work-input-group">
                                    <label for="framingAssemblyPersonnel">Framing Assembly</label>
                                    <input type="number" id="framingAssemblyPersonnel" value="1" min="0">
                                </div>
                                <div class="work-input-group">
                                    <label for="framingAssemblyTime">Time Required (hours)</label>
                                    <input type="text" id="framingAssemblyTime" value="0" readonly>
                                </div>
                                
                                <div class="work-input-group">
                                    <label for="finishesPersonnel">Finishes</label>
                                    <input type="number" id="finishesPersonnel" value="2" min="0">
                                </div>
                                <div class="work-input-group">
                                    <label for="finishesTime">Time Required (hours)</label>
                                    <input type="text" id="finishesTime" value="0" readonly>
                                </div>
                                
                                <div class="work-input-group">
                                    <label for="packagingPersonnel">Packaging</label>
                                    <input type="number" id="packagingPersonnel" value="0" min="0">
                                </div>
                                <div class="work-input-group">
                                    <label for="packagingTime">Time Required (hours)</label>
                                    <input type="text" id="packagingTime" value="0" readonly>
                                </div>
                            </div>
                            
                            <button class="optimize-btn" onclick="optimizePersonnelAllocation()">
                                <i class="fas fa-bolt"></i> Optimize
                            </button>
                            <button class="reset-btn" onclick="resetWorkManager()">
                                <i class="fas fa-redo"></i> Reset
                            </button>
                        </div>
                        
                        <div class="resource-summary">
                            <div class="summary-row">
                                <span>Total Personnel:</span>
                                <span id="totalPersonnelSummary">5</span>
                            </div>
                            <div class="summary-row">
                                <span>Bottleneck Role:</span>
                                <span id="bottleneckRole">N/A</span>
                            </div>
                            <div class="summary-row">
                                <span>Estimated Completion:</span>
                                <span id="estimatedCompletionSummary">0 days</span>
                            </div>
                            <div class="bottleneck" id="bottleneckMessage">
                                No bottleneck identified
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- Preview Tab -->
            <div id="Preview" class="tab-content">
                <h2><i class="fas fa-eye"></i> Project Preview & Cost Summary</h2>
                <div id="projectPreviewContainer"></div>
            </div>
            <!-- Invoice Tab -->
            <div id="Invoice" class="tab-content">
                <h2><i class="fas fa-file-invoice"></i> Invoice Generation</h2>
                <div class="toolbar-group" style="margin-bottom: 20px;">
                    <button id="generateInvoice" class="btn btn-primary"><i class="fas fa-file-pdf"></i> Generate PDF Invoice</button>
                    <button id="printInvoice" class="btn btn-outline" style="display: none;"><i class="fas fa-print"></i> Print Invoice</button>
                </div>
                <div id="invoiceContainer" class="invoice-container" style="display: none;"></div>
            </div>
        </div>
        <footer><p>© 2025 AEWorks Ltd. Integrated v4.0 | <i class="fas fa-shield-alt"></i> Secure Database System</p></footer>
    </div>
    <!-- Manage Pages -->
    <div id="manageClientsPage" class="manage-page"><button onclick="goBack()" class="back-btn"><i class="fas fa-arrow-left"></i> Back</button><h2><i class="fas fa-users"></i> Manage Clients</h2><button onclick="addClient()" class="btn btn-success" style="margin-bottom:20px;"><i class="fas fa-plus"></i> Add New Client</button><div style="overflow-x:auto;"><table id="clientTable"><thead><tr><th>Manager</th><th>Name</th><th>Phone</th><th>Email</th><th>Address</th><th>Destination</th><th>Actions</th></tr></thead><tbody id="clientTableBody"></tbody></table></div></div>
    <div id="manageContactsPage" class="manage-page"><button onclick="goBack()" class="back-btn"><i class="fas fa-arrow-left"></i> Back</button><h2><i class="fas fa-address-book"></i> Manage Contacts</h2><button onclick="addContact()" class="btn btn-success" style="margin-bottom:20px;"><i class="fas fa-plus"></i> Add New Contact</button><div class="import-section"><input type="file" id="contactImport" accept=".csv" style="display:none;"><button onclick="document.getElementById('contactImport').click()" class="btn btn-warning"><i class="fas fa-upload"></i> Import Master List</button><p><strong>Headers:</strong> name,designation,phone1,email1</p></div><div style="overflow-x:auto;"><table id="contactTable"><thead><tr><th>Name</th><th>Designation</th><th>Phone</th><th>Email</th><th>Actions</th></tr></thead><tbody id="contactTableBody"></tbody></table></div></div>
    <div id="manageCentresPage" class="manage-page"><button onclick="goBack()" class="back-btn"><i class="fas fa-arrow-left"></i> Back</button><h2><i class="fas fa-warehouse"></i> Manage Production Centres</h2><button onclick="addCentre()" class="btn btn-success" style="margin-bottom:20px;"><i class="fas fa-plus"></i> Add New Centre</button><div style="overflow-x:auto;"><table id="centreTable"><thead><tr><th>Name</th><th>Can Ship?</th><th>Coordinates</th><th>Floor Space (sqm)</th><th>Actions</th></tr></thead><tbody id="centreTableBody"></tbody></table></div></div>
    <div id="manageMaterialsPage" class="manage-page"><button onclick="goBack()" class="back-btn"><i class="fas fa-arrow-left"></i> Back</button><h2><i class="fas fa-boxes"></i> Manage Materials</h2><div class="tabs"><div class="tab active" onclick="openMaterialTab(event,'Framing')">Framing Materials</div><div class="tab" onclick="openMaterialTab(event,'Finishes')">Finishes & Accessories</div></div><div id="Framing" class="material-tab-content active"><h3>Framing Materials</h3><button onclick="addFramingMaterial()" class="btn btn-success" style="margin-bottom:10px;"><i class="fas fa-plus"></i> Add Framing Material</button><div class="import-section"><input type="file" id="framingImport" accept=".csv" style="display:none;"><button onclick="document.getElementById('framingImport').click()" class="btn btn-warning"><i class="fas fa-upload"></i> Import Master List</button><p><strong>Headers:</strong> MATERIAL / GROUP,FRAMING MATERIALS,RATE,Surface Area</p></div><div style="overflow-x:auto;"><table id="framingMaterialTable"><thead><tr><th>Group</th><th>Name</th><th>Rate (₦/m or ₦/m²)</th><th>Surface Area (m²/m, linear only)</th><th>Actions</th></tr></thead><tbody id="framingMaterialTableBody"></tbody></table></div></div><div id="Finishes" class="material-tab-content" style="display:none;"><h3>Finishes & Accessories</h3><button onclick="addFinishMaterial()" class="btn btn-success" style="margin-bottom:10px;"><i class="fas fa-plus"></i> Add Finish/Accessory</button><div class="import-section"><input type="file" id="finishImport" accept=".csv" style="display:none;"><button onclick="document.getElementById('finishImport').click()" class="btn btn-warning"><i class="fas fa-upload"></i> Import Master List</button><p><strong>Headers:</strong> MATERIAL / GROUP,NAME - MATERIAL,PRICE,Coverage</p></div><div style="overflow-x:auto;"><table id="finishMaterialTable"><thead><tr><th>Group</th><th>Name</th><th>Price (₦)</th><th>Coverage (m²)</th><th>Actions</th></tr></thead><tbody id="finishMaterialTableBody"></tbody></table></div></div></div>
    <div id="projectListModal" class="modal"><div class="modal-content"><h3><i class="fas fa-list"></i> Saved Projects</h3><div id="projectList"><ul id="projectListItems" style="list-style-type:none;padding:0;"></ul></div><button onclick="closeProjectList()" class="close-btn"><i class="fas fa-times"></i> Close</button></div></div>
    <!-- PDF Libraries -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script>
        // --- CONFIGURATION ---
        const LOCAL_SHIPPING_RATE_PER_CUBIC_METER=250, NATIONAL_SHIPPING_RATE_PER_CUBIC_METER=350, LOCAL_DISTANCE_THRESHOLD=35;
        const NIGERIAN_CITIES=[{name:"Lagos",coords:"6.5244, 3.3792"},{name:"Abuja",coords:"9.0765, 7.3986"},{name:"Kano",coords:"12.0022, 8.5920"},{name:"Ibadan",coords:"7.3776, 3.9470"},{name:"Port Harcourt",coords:"4.8156, 7.0498"},{name:"Benin City",coords:"6.3350, 5.6037"},{name:"Kaduna",coords:"10.5222, 7.4414"},{name:"Abeokuta",coords:"7.1475, 3.3619"},{name:"Onitsha",coords:"6.1667, 6.7833"},{name:"Warri",coords:"5.5167, 5.7500"},{name:"Enugu",coords:"6.4497, 7.5014"}];
        // --- GLOBAL STATE & DB ---
        let currentProject={framingTakeOff:[],finishesTakeOff:[],costingVariables:{}, adjustedCosts: null}, currentUser=null;
        let framingMaterialOptionsHTML='', finishesMaterialOptionsHTML='';
        const dbKeys=['clients','contacts','centres','framingMaterials','finishMaterials','projects','defaultCostingVariables'];
        function getData(k){try{const d=localStorage.getItem(k);return d?JSON.parse(d):[];}catch(e){console.error(`Error getting ${k}`,e);return[];}}
        function saveData(k,d){try{localStorage.setItem(k,JSON.stringify(d));return true;}catch(e){console.error(`Error saving ${k}`,e);showNotification(`Failed to save ${k}.`,'error');return false;}}
        dbKeys.forEach(k=>{if(!localStorage.getItem(k))saveData(k,[]);});
        // --- UI & NOTIFICATIONS ---
        function showNotification(m,t='success'){const n=document.getElementById('notification'),tx=document.getElementById('notificationText');tx.textContent=m;n.className=`notification ${t} show`;setTimeout(()=>n.className='notification',4000);}
        function updateStatusBar(){const v=parseInt(document.getElementById('projectStatus').value);document.querySelectorAll('.status-item').forEach(i=>{i.classList.remove('active');if(parseInt(i.dataset.statusValue)<=v)i.classList.add('active');});}
        // --- AUTH & INIT ---
        function login(){const u=document.getElementById('username').value,p=document.getElementById('password').value,users={'admin':{p:'admin123',r:'admin'},'manager':{p:'mgr123',r:'manager'},'viewer':{p:'view123',r:'viewer'}};if(users[u]&&users[u].p===p){currentUser={u,r:users[u].r};document.getElementById('loginModal').style.display='none';document.getElementById('userInfo').innerHTML=`Logged in as <strong>${u}</strong> (${currentUser.r})`;if(currentUser.r==='viewer')document.querySelectorAll('input,select,button').forEach(el=>el.disabled=true);document.getElementById('userBar').style.display='flex';preloadDefaultData();initCostingTab();refreshDropdowns();populateCitiesDropdown();renderFramingTakeOffTable();renderFinishesTakeOffTable();updateStatusBar();}else{showNotification("Invalid credentials","error");}}
        function logout(){currentUser=null;document.getElementById('loginModal').style.display='flex';document.getElementById('userBar').style.display='none';}
        function preloadDefaultData(){if(getData('centres').length===0)saveData('centres',[{name:"Iju Factory - AEWorks",ship:"Y",coords:"6.613735, 3.504107",floorSpace:"150"},{name:"AEWorks Ologogoro",ship:"Y",coords:"6.682121, 3.268985",floorSpace:"50"}]);if(getData('clients').length===0)saveData('clients',[{mgr:"Engr Abe",name:"AEWorks Ltd",phone:"08123218669",email:"ola@aeworks.com",address:"Ogudu, Lagos",destination:"Lagos"},{mgr:"S. Manchester",name:"Jaza Energy Inc",phone:"2348123218779",email:"sebastian@jaza.com",address:"Ibadan, Oyo",destination:"Ibadan"}]);if(getData('contacts').length===0)saveData('contacts',[{name:"Abe Olatunde P",designation:"Manager/Designer",phone1:"2348123218779",email1:"abe@aeworks.com"}]);if(getData('framingMaterials').length===0)saveData('framingMaterials',initialFramingData);if(getData('finishMaterials').length===0)saveData('finishMaterials',initialFinishData);}
        function init(){document.getElementById('manageClients').onclick=()=>showPage('manageClientsPage');document.getElementById('manageContacts').onclick=()=>showPage('manageContactsPage');document.getElementById('manageCentres').onclick=()=>showPage('manageCentresPage');document.getElementById('manageMaterials').onclick=()=>showPage('manageMaterialsPage');document.getElementById('saveTemplate').onclick=saveProject;document.getElementById('loadTemplate').onclick=loadProject;document.getElementById('listProjects').onclick=showProjectList;document.getElementById('contactImport').addEventListener('change',(e)=>handleMasterFileUpload(e,'contacts',['name','designation','phone1','email1'],renderContactsTable));document.getElementById('framingImport').addEventListener('change',(e)=>handleMasterFileUpload(e,'framingMaterials',['MATERIAL / GROUP','FRAMING MATERIALS','RATE','Surface Area'],renderFramingMaterialsTable));document.getElementById('finishImport').addEventListener('change',(e)=>handleMasterFileUpload(e,'finishMaterials',['MATERIAL / GROUP','NAME - MATERIAL','PRICE','Coverage'],renderFinishMaterialsTable));document.getElementById('framingTakeOffImport').addEventListener('change',(e)=>handleTakeOffFileUpload(e,'framing'));document.getElementById('finishesTakeOffImport').addEventListener('change',(e)=>handleTakeOffFileUpload(e,'finishes'));document.getElementById('generateInvoice').onclick=generateInvoice;document.getElementById('printInvoice').onclick=printInvoice;document.body.addEventListener('click',function(e){const t=e.target.closest('.action-btn');const toggle=e.target.closest('.details-toggle');if(toggle){const content=toggle.nextElementSibling;if(content&&content.classList.contains('details-content')){const isVisible=content.style.display==='block';content.style.display=isVisible?'none':'block';toggle.textContent=isVisible?'Show Details':'Hide Details';}}if(!t)return;const i=parseInt(t.getAttribute('data-index')),aM={'edit-client-btn':()=>editClient(i),'save-client-btn':()=>saveClient(i),'delete-client-btn':()=>deleteClient(i),'edit-contact-btn':()=>editContact(i),'save-contact-btn':()=>saveContact(i),'delete-contact-btn':()=>deleteContact(i),'edit-centre-btn':()=>editCentre(i),'save-centre-btn':()=>saveCentre(i),'delete-centre-btn':()=>deleteCentre(i),'edit-framing-btn':()=>editFramingMaterial(i),'save-framing-btn':()=>saveFramingMaterial(i),'delete-framing-btn':()=>deleteFramingMaterial(i),'edit-finish-btn':()=>editFinishMaterial(i),'save-finish-btn':()=>saveFinishMaterial(i),'delete-finish-btn':()=>deleteFinishMaterial(i),'delete-framing-takeoff-btn':()=>deleteFramingRow(i),'delete-finish-takeoff-btn':()=>deleteFinishRow(i)},k=Array.from(t.classList).find(c=>aM[c]);if(k)aM[k]();});}
        // --- NAVIGATION & UI FLOW ---
        function openTab(e,t){document.querySelectorAll('.tab-content').forEach(el=>el.classList.remove('active'));document.querySelectorAll('.tab-button').forEach(b=>b.classList.remove('active'));document.getElementById(t).classList.add('active');e.currentTarget.classList.add('active');if(t==='Preview')generateProjectPreview();if(t==='WorkManager')setupWorkManager();if(t==='Invoice')setupInvoiceTab();}
        function showPage(p){document.querySelectorAll('.manage-page').forEach(el=>el.style.display='none');document.querySelector('.tab-container').style.display='none';document.getElementById(p).style.display='block';if(p==='manageClientsPage')renderClientsTable();if(p==='manageContactsPage')renderContactsTable();if(p==='manageCentresPage')renderCentresTable();if(p==='manageMaterialsPage'){renderFramingMaterialsTable();renderFinishMaterialsTable();}}
        function goBack(){document.querySelectorAll('.manage-page').forEach(p=>p.style.display='none');document.querySelector('.tab-container').style.display='block';}
        // --- GENERIC CRUD & Specifics (Collapsed) ---
        function makeRowEditable(r,f){r.querySelectorAll('td:not(:last-child)').forEach((t,i)=>{t.innerHTML=`<input type="text" value="${t.textContent}" data-field="${f[i]}">`;});}
        function saveRowData(r,d,f){r.querySelectorAll('input[data-field]').forEach(i=>{d[i.dataset.field]=i.value;});}
        function toggleActionButtons(r,e,t,i){const a=r.querySelector('td:last-child');if(e)a.innerHTML=`<button class="action-btn save-btn save-${t}-btn" data-index="${i}"><i class="fas fa-save"></i></button>`;else a.innerHTML=`<button class="action-btn edit-btn edit-${t}-btn" data-index="${i}"><i class="fas fa-edit"></i></button><button class="action-btn delete-btn delete-${t}-btn" data-index="${i}"><i class="fas fa-trash"></i></button>`;}
        function renderClientsTable(){const d=getData('clients'),t=document.getElementById('clientTableBody');t.innerHTML='';d.forEach((c,i)=>{const r=t.insertRow();r.innerHTML=`<td>${c.mgr||''}</td><td>${c.name||''}</td><td>${c.phone||''}</td><td>${c.email||''}</td><td>${c.address||''}</td><td>${c.destination||''}</td><td><button class="action-btn edit-btn edit-client-btn" data-index="${i}"><i class="fas fa-edit"></i></button><button class="action-btn delete-btn delete-client-btn" data-index="${i}"><i class="fas fa-trash"></i></button></td>`;});}
        function addClient(){const d=getData('clients');d.push({mgr:'New Mgr',name:'New Client',phone:'',email:'',address:'',destination:''});if(saveData('clients',d)){showNotification("Client added.","success");renderClientsTable();refreshDropdowns();}}
        function editClient(i){const r=document.getElementById('clientTableBody').rows[i];makeRowEditable(r,['mgr','name','phone','email','address','destination']);toggleActionButtons(r,true,'client',i);}
        function saveClient(i){const d=getData('clients'),r=document.getElementById('clientTableBody').rows[i];saveRowData(r,d[i],['mgr','name','phone','email','address','destination']);if(saveData('clients',d)){showNotification("Client updated.","success");renderClientsTable();refreshDropdowns();}}
        function deleteClient(i){if(confirm("Are you sure?")){const d=getData('clients');d.splice(i,1);if(saveData('clients',d)){showNotification("Client deleted.","success");renderClientsTable();refreshDropdowns();}}}
        function renderContactsTable(){const d=getData('contacts'),t=document.getElementById('contactTableBody');t.innerHTML='';d.forEach((c,i)=>{const r=t.insertRow();r.innerHTML=`<td>${c.name||''}</td><td>${c.designation||''}</td><td>${c.phone1||''}</td><td>${c.email1||''}</td><td><button class="action-btn edit-btn edit-contact-btn" data-index="${i}"><i class="fas fa-edit"></i></button><button class="action-btn delete-btn delete-contact-btn" data-index="${i}"><i class="fas fa-trash"></i></button></td>`;});}
        function addContact(){const d=getData('contacts');d.push({name:'New Contact',designation:'New Role',phone1:'',email1:''});if(saveData('contacts',d)){showNotification("Contact added.","success");renderContactsTable();refreshDropdowns();}}
        function editContact(i){const r=document.getElementById('contactTableBody').rows[i];makeRowEditable(r,['name','designation','phone1','email1']);toggleActionButtons(r,true,'contact',i);}
        function saveContact(i){const d=getData('contacts'),r=document.getElementById('contactTableBody').rows[i];saveRowData(r,d[i],['name','designation','phone1','email1']);if(saveData('contacts',d)){showNotification("Contact updated.","success");renderContactsTable();refreshDropdowns();}}
        function deleteContact(i){if(confirm("Are you sure?")){const d=getData('contacts');d.splice(i,1);if(saveData('contacts',d)){showNotification("Contact deleted.","success");renderContactsTable();refreshDropdowns();}}}
        function renderCentresTable(){const d=getData('centres'),t=document.getElementById('centreTableBody');t.innerHTML='';d.forEach((c,i)=>{const r=t.insertRow();r.innerHTML=`<td>${c.name||''}</td><td>${c.ship||''}</td><td>${c.coords||''}</td><td>${c.floorSpace||''}</td><td><button class="action-btn edit-btn edit-centre-btn" data-index="${i}"><i class="fas fa-edit"></i></button><button class="action-btn delete-btn delete-centre-btn" data-index="${i}"><i class="fas fa-trash"></i></button></td>`;});}
        function addCentre(){const d=getData('centres');d.push({name:'New Centre',ship:'Y',coords:'0,0',floorSpace:'0'});if(saveData('centres',d)){showNotification("Centre added.","success");renderCentresTable();refreshDropdowns();}}
        function editCentre(i){const r=document.getElementById('centreTableBody').rows[i];makeRowEditable(r,['name','ship','coords','floorSpace']);toggleActionButtons(r,true,'centre',i);}
        function saveCentre(i){const d=getData('centres'),r=document.getElementById('centreTableBody').rows[i];saveRowData(r,d[i],['name','ship','coords','floorSpace']);if(saveData('centres',d)){showNotification("Centre updated.","success");renderCentresTable();refreshDropdowns();}}
        function deleteCentre(i){if(confirm("Are you sure?")){const d=getData('centres');d.splice(i,1);if(saveData('centres',d)){showNotification("Centre deleted.","success");renderCentresTable();refreshDropdowns();}}}
        function openMaterialTab(e,t){document.querySelectorAll('.material-tab-content').forEach(e=>e.style.display='none');document.querySelectorAll('.tabs .tab').forEach(e=>e.classList.remove('active'));document.getElementById(t).style.display='block';e.currentTarget.classList.add('active');}
        function renderFramingMaterialsTable(){const m=getData('framingMaterials').filter(m=>m&&m['FRAMING MATERIALS']),t=document.getElementById('framingMaterialTableBody');t.innerHTML='';m.forEach((mat,i)=>{const r=t.insertRow();r.innerHTML=`<td>${mat['MATERIAL / GROUP']||''}</td><td>${mat['FRAMING MATERIALS']||''}</td><td>${mat['RATE']||''}</td><td>${mat['Surface Area']||''}</td><td><button class="action-btn edit-btn edit-framing-btn" data-index="${i}"><i class="fas fa-edit"></i></button><button class="action-btn delete-btn delete-framing-btn" data-index="${i}"><i class="fas fa-trash"></i></button></td>`;});}
        function addFramingMaterial(){const m=getData('framingMaterials');m.push({'MATERIAL / GROUP':'GROUP','FRAMING MATERIALS':'New Material','RATE':0,'Surface Area':0});if(saveData('framingMaterials',m)){showNotification("Material added.","success");renderFramingMaterialsTable();refreshDropdowns();}}
        function editFramingMaterial(i){const r=document.getElementById('framingMaterialTableBody').rows[i];makeRowEditable(r,['MATERIAL / GROUP','FRAMING MATERIALS','RATE','Surface Area']);toggleActionButtons(r,true,'framing',i);}
        function saveFramingMaterial(i){const all=getData('framingMaterials'),m=all.filter(m=>m&&m['FRAMING MATERIALS']),r=document.getElementById('framingMaterialTableBody').rows[i];saveRowData(r,m[i],['MATERIAL / GROUP','FRAMING MATERIALS','RATE','Surface Area']);if(saveData('framingMaterials',all)){showNotification("Material updated.","success");renderFramingMaterialsTable();refreshDropdowns();}}
        function deleteFramingMaterial(i){if(confirm("Delete material?")){const all=getData('framingMaterials'),m=all.filter(m=>m&&m['FRAMING MATERIALS']),item=m[i],orig=all.findIndex(x=>x===item);if(orig>-1)all.splice(orig,1);if(saveData('framingMaterials',all)){showNotification("Material deleted.","success");renderFramingMaterialsTable();refreshDropdowns();}}}
        function renderFinishMaterialsTable(){const m=getData('finishMaterials').filter(m=>m&&m['NAME - MATERIAL']),t=document.getElementById('finishMaterialTableBody');t.innerHTML='';m.forEach((mat,i)=>{const r=t.insertRow();r.innerHTML=`<td>${mat['MATERIAL / GROUP']||''}</td><td>${mat['NAME - MATERIAL']||''}</td><td>${mat['PRICE']||''}</td><td>${mat['Coverage']||''}</td><td><button class="action-btn edit-btn edit-finish-btn" data-index="${i}"><i class="fas fa-edit"></i></button><button class="action-btn delete-btn delete-finish-btn" data-index="${i}"><i class="fas fa-trash"></i></button></td>`;});}
        function addFinishMaterial(){const m=getData('finishMaterials');m.push({'MATERIAL / GROUP':'GROUP','NAME - MATERIAL':'New Accessory','PRICE':0,'Coverage':0});if(saveData('finishMaterials',m)){showNotification("Accessory added.","success");renderFinishMaterialsTable();refreshDropdowns();}}
        function editFinishMaterial(i){const r=document.getElementById('finishMaterialTableBody').rows[i];makeRowEditable(r,['MATERIAL / GROUP','NAME - MATERIAL','PRICE','Coverage']);toggleActionButtons(r,true,'finish',i);}
        function saveFinishMaterial(i){const all=getData('finishMaterials'),m=all.filter(m=>m&&m['NAME - MATERIAL']),r=document.getElementById('finishMaterialTableBody').rows[i];saveRowData(r,m[i],['MATERIAL / GROUP','NAME - MATERIAL','PRICE','Coverage']);if(saveData('finishMaterials',all)){showNotification("Accessory updated.","success");renderFinishMaterialsTable();refreshDropdowns();}}
        function deleteFinishMaterial(i){if(confirm("Delete accessory?")){const all=getData('finishMaterials'),m=all.filter(m=>m&&m['NAME - MATERIAL']),item=m[i],orig=all.findIndex(x=>x===item);if(orig>-1)all.splice(orig,1);if(saveData('finishMaterials',all)){showNotification("Accessory deleted.","success");renderFinishMaterialsTable();refreshDropdowns();}}}
        // --- FORM DATA BINDING ---
        function refreshDropdowns(){populateSelect('clientName',getData('clients'),'name');populateSelect('projMgr',getData('contacts'),'name');populateSelect('prodCentre',getData('centres'),'name');let fOpt='<option value="">-- Select --</option>',finOpt='<option value="">-- Select --</option>';getData('framingMaterials').filter(m=>m&&m['FRAMING MATERIALS']).forEach(m=>{fOpt+=`<option value="${m['FRAMING MATERIALS']}">${m['FRAMING MATERIALS']}</option>`;});framingMaterialOptionsHTML=fOpt;getData('finishMaterials').filter(m=>m&&m['NAME - MATERIAL']).forEach(m=>{finOpt+=`<option value="${m['NAME - MATERIAL']}">${m['NAME - MATERIAL']}</option>`;});finishesMaterialOptionsHTML=finOpt;}
        function populateSelect(id,arr,field){const s=document.getElementById(id),c=s.value;s.innerHTML='<option value="">-- Select --</option>';arr.forEach(i=>{if(i&&i[field])s.add(new Option(i[field],i[field]));});s.value=c;}
        function populateCitiesDropdown(){const s=document.getElementById('destCitySelect');s.innerHTML='<option value="">-- Select City --</option>';NIGERIAN_CITIES.forEach(c=>s.add(new Option(c.name,c.name)));s.add(new Option("Other / Custom","Custom"));}
        function handleCityChange(){const s=document.getElementById('destCitySelect'),c=document.getElementById('destCoords');if(s.value==="Custom"){c.value="";c.readOnly=false;c.placeholder="Enter custom lat, long";}else{const city=NIGERIAN_CITIES.find(ci=>ci.name===s.value);c.value=city?city.coords:"";c.readOnly=true;}}
        function fillClientData(){const c=getData('clients').find(cl=>cl.name===document.getElementById('clientName').value);if(c){['clientMgr:mgr','clientPhone:phone','clientEmail:email','clientAddr:address'].forEach(m=>{const[e,k]=m.split(':');document.getElementById(e).value=c[k]||'';});const s=document.getElementById('destCitySelect');s.value=c.destination||'';handleCityChange();}}
        function fillContactData(){const c=getData('contacts').find(ct=>ct.name===document.getElementById('projMgr').value);if(c){document.getElementById('mgrPhone').value=c.phone1||'';document.getElementById('mgrEmail').value=c.email1||'';}}
        function fillCentreData(){const c=getData('centres').find(ce=>ce.name===document.getElementById('prodCentre').value);if(c)document.getElementById('prodCoords').value=c.coords||'';}
        function generateProjectCode(){const n=document.getElementById('projName').value.trim(),j=document.getElementById('jobsThisYear').value||1,y=document.getElementById('year').value.trim().slice(-2);if(n){const w=n.split(/\s+/);let a=w.length>=3?w.slice(0,3).map(w=>w[0]).join(''):w.length===2?w[0][0]+w[1].substring(0,2):n.substring(0,3);document.getElementById('projectCode').value=`AEP-${a.toUpperCase()}-${j.toString().padStart(3,'0')}.${y}`;}}
        // --- TAKE-OFF TABLES ---
        function isSheetMaterial(name){if(!name)return false;const k=['HDF','MDF','Glass','Sheet','Board','Mesh','Plate'];return k.some(key=>name.toLowerCase().includes(key.toLowerCase()));}
        function toggleDimensionInputs(selectElement){const row=selectElement.closest('tr');if(!row)return;const widthInput=row.querySelector('.takeoff-width');const isSheet=isSheetMaterial(selectElement.value);widthInput.disabled=!isSheet;if(!isSheet)widthInput.value=0;}
        function updateFramingTakeOffFromUI(){const newTakeOff=[];document.querySelectorAll('#framingTakeOffTableBody tr').forEach(r=>{newTakeOff.push({desc:r.querySelector('.takeoff-desc').value,material:r.querySelector('.takeoff-material').value,length:r.querySelector('.takeoff-length').value,width:r.querySelector('.takeoff-width').value,qty:r.querySelector('.takeoff-qty').value});});currentProject.framingTakeOff=newTakeOff;}
        function renderFramingTakeOffTable(){const t=document.getElementById('framingTakeOffTableBody');t.innerHTML='';currentProject.framingTakeOff.forEach((item,i)=>{const r=t.insertRow();const isSheet=isSheetMaterial(item.material);r.innerHTML=`<td>${i+1}</td><td><input type="text" class="takeoff-desc" value="${item.desc||''}"></td><td><select class="takeoff-material" onchange="toggleDimensionInputs(this)">${framingMaterialOptionsHTML}</select></td><td><input type="number" class="takeoff-length" value="${item.length||0}" step="0.01"></td><td><input type="number" class="takeoff-width" value="${item.width||0}" step="0.01" ${isSheet?'':'disabled'}></td><td><input type="number" class="takeoff-qty" value="${item.qty||1}"></td><td><button class="action-btn delete-btn delete-framing-takeoff-btn" data-index="${i}"><i class="fas fa-trash"></i></button></td>`;r.querySelector('.takeoff-material').value=item.material||'';});}
        function addFramingRow(){updateFramingTakeOffFromUI();currentProject.framingTakeOff.push({desc:'',material:'',length:0,width:0,qty:1});renderFramingTakeOffTable();}
        function deleteFramingRow(i){updateFramingTakeOffFromUI();currentProject.framingTakeOff.splice(i,1);renderFramingTakeOffTable();}
        function updateFinishesTakeOffFromUI(){const newTakeOff=[];document.querySelectorAll('#finishesTakeOffTableBody tr').forEach(r=>{newTakeOff.push({desc:r.querySelector('.takeoff-desc').value,material:r.querySelector('.takeoff-material').value,qty:r.querySelector('.takeoff-qty').value});});currentProject.finishesTakeOff=newTakeOff;}
        function renderFinishesTakeOffTable(){const t=document.getElementById('finishesTakeOffTableBody');t.innerHTML='';currentProject.finishesTakeOff.forEach((item,i)=>{const r=t.insertRow();r.innerHTML=`<td>${i+1}</td><td><input type="text" class="takeoff-desc" value="${item.desc||''}"></td><td><select class="takeoff-material">${finishesMaterialOptionsHTML}</select></td><td><input type="number" class="takeoff-qty" value="${item.qty||1}"></td><td><button class="action-btn delete-btn delete-finish-takeoff-btn" data-index="${i}"><i class="fas fa-trash"></i></button></td>`;r.querySelector('.takeoff-material').value=item.material||'';});}
        function addFinishRow(){updateFinishesTakeOffFromUI();currentProject.finishesTakeOff.push({desc:'',material:'',qty:1});renderFinishesTakeOffTable();}
        function deleteFinishRow(i){updateFinishesTakeOffFromUI();currentProject.finishesTakeOff.splice(i,1);renderFinishesTakeOffTable();}
        // --- WORK MANAGER ---
        function setupWorkManager() {
            // Initialize work manager values
            document.getElementById('targetCompletionDays').value = 14;
            document.getElementById('workHoursPerDay').value = 8;
            document.getElementById('actualPersonnelAvailable').value = 5;
            
            // Set default role allocations
            document.getElementById('partsProductionPersonnel').value = 2;
            document.getElementById('framingAssemblyPersonnel').value = 1;
            document.getElementById('finishesPersonnel').value = 2;
            document.getElementById('packagingPersonnel').value = 0;
            
            // Add event listeners
            document.getElementById('targetCompletionDays').addEventListener('input', calculateWorkRequirements);
            document.getElementById('workHoursPerDay').addEventListener('input', calculateWorkRequirements);
            document.getElementById('actualPersonnelAvailable').addEventListener('input', calculateWorkRequirements);
            
            // Role allocation listeners
            document.getElementById('partsProductionPersonnel').addEventListener('input', updateResourceAllocation);
            document.getElementById('framingAssemblyPersonnel').addEventListener('input', updateResourceAllocation);
            document.getElementById('finishesPersonnel').addEventListener('input', updateResourceAllocation);
            document.getElementById('packagingPersonnel').addEventListener('input', updateResourceAllocation);
            
            // Initial calculation
            calculateWorkRequirements();
        }
        
        function calculateWorkRequirements() {
            // Get values from UI
            const targetCompletionDays = parseFloat(document.getElementById('targetCompletionDays').value) || 14;
            const workHoursPerDay = parseFloat(document.getElementById('workHoursPerDay').value) || 8;
            const actualPersonnel = parseFloat(document.getElementById('actualPersonnelAvailable').value) || 5;
            
            // Calculate total production time (this would normally come from project data)
            // For now, we'll simulate it based on project size
            const totalProductionTime = calculateTotalProductionTime();
            
            // Calculate requirements
            const totalWorkDaysRequired = totalProductionTime / workHoursPerDay;
            const recommendedTeamSize = Math.ceil(totalWorkDaysRequired / targetCompletionDays);
            const totalPersonnelRequired = recommendedTeamSize;
            
            // Calculate estimated completion time with actual personnel
            let estimatedCompletionTime = totalWorkDaysRequired / actualPersonnel;
            if (isNaN(estimatedCompletionTime) || !isFinite(estimatedCompletionTime)) {
                estimatedCompletionTime = 0;
            }
            
            // Update UI
            document.getElementById('totalProductionTime').textContent = `${totalProductionTime.toFixed(1)} hours`;
            document.getElementById('totalWorkDaysRequired').textContent = `${totalWorkDaysRequired.toFixed(1)} days`;
            document.getElementById('recommendedTeamSize').textContent = `${recommendedTeamSize} people`;
            document.getElementById('totalPersonnelRequired').textContent = totalPersonnelRequired;
            document.getElementById('estimatedCompletionTime').textContent = `${estimatedCompletionTime.toFixed(1)} days`;
            
            // Update resource allocation section
            updateResourceAllocation();
        }
        
        function calculateTotalProductionTime() {
            // This would normally calculate based on project specifications
            // For demonstration, we'll use a simple calculation based on project size
            const projectSize = currentProject.framingTakeOff.length + currentProject.finishesTakeOff.length;
            return projectSize * 10; // 10 hours per component
        }
        
        function updateResourceAllocation() {
            // Get values from UI
            const totalProductionTime = parseFloat(document.getElementById('totalProductionTime').textContent) || 0;
            const workHoursPerDay = parseFloat(document.getElementById('workHoursPerDay').value) || 8;
            const actualPersonnel = parseFloat(document.getElementById('actualPersonnelAvailable').value) || 5;
            
            // Get role allocations
            const partsProduction = parseFloat(document.getElementById('partsProductionPersonnel').value) || 0;
            const framingAssembly = parseFloat(document.getElementById('framingAssemblyPersonnel').value) || 0;
            const finishes = parseFloat(document.getElementById('finishesPersonnel').value) || 0;
            const packaging = parseFloat(document.getElementById('packagingPersonnel').value) || 0;
            
            // Calculate total personnel
            const totalPersonnel = partsProduction + framingAssembly + finishes + packaging;
            
            // Calculate time required for each role (simplified)
            const partsProductionTime = (totalProductionTime * 0.4) / partsProduction;
            const framingAssemblyTime = (totalProductionTime * 0.2) / framingAssembly;
            const finishesTime = (totalProductionTime * 0.3) / finishes;
            const packagingTime = (totalProductionTime * 0.1) / packaging;
            
            // Update UI
            document.getElementById('partsProductionTime').value = partsProduction > 0 ? (partsProductionTime * workHoursPerDay).toFixed(1) : 'N/A';
            document.getElementById('framingAssemblyTime').value = framingAssembly > 0 ? (framingAssemblyTime * workHoursPerDay).toFixed(1) : 'N/A';
            document.getElementById('finishesTime').value = finishes > 0 ? (finishesTime * workHoursPerDay).toFixed(1) : 'N/A';
            document.getElementById('packagingTime').value = packaging > 0 ? (packagingTime * workHoursPerDay).toFixed(1) : 'N/A';
            
            // Find bottleneck
            const roleTimes = [
                {name: 'Parts Production', time: partsProductionTime},
                {name: 'Framing Assembly', time: framingAssemblyTime},
                {name: 'Finishes', time: finishesTime},
                {name: 'Packaging', time: packagingTime}
            ];
            
            // Filter out roles with no personnel
            const validRoleTimes = roleTimes.filter(role => role.time > 0);
            
            if (validRoleTimes.length > 0) {
                const bottleneck = validRoleTimes.reduce((max, role) => role.time > max.time ? role : max, {time: -Infinity});
                document.getElementById('bottleneckRole').textContent = bottleneck.name;
                document.getElementById('bottleneckMessage').textContent = `Bottleneck: ${bottleneck.name} will determine the completion time`;
                document.getElementById('bottleneckMessage').classList.add('bottleneck');
                
                // Calculate estimated completion based on bottleneck
                const estimatedCompletion = bottleneck.time;
                document.getElementById('estimatedCompletionSummary').textContent = `${estimatedCompletion.toFixed(1)} days`;
            } else {
                document.getElementById('bottleneckRole').textContent = 'N/A';
                document.getElementById('bottleneckMessage').textContent = 'No personnel assigned to any role';
                document.getElementById('bottleneckMessage').classList.remove('bottleneck');
                document.getElementById('bottleneckMessage').style.backgroundColor = '#fbdada';
                document.getElementById('estimatedCompletionSummary').textContent = '0 days';
            }
            
            document.getElementById('totalPersonnelSummary').textContent = totalPersonnel;
        }
        
        function optimizePersonnelAllocation() {
            // Get values
            const totalPersonnel = parseFloat(document.getElementById('actualPersonnelAvailable').value) || 5;
            
            // Simple optimization: allocate personnel based on workload percentage
            document.getElementById('partsProductionPersonnel').value = Math.max(1, Math.round(totalPersonnel * 0.4));
            document.getElementById('framingAssemblyPersonnel').value = Math.max(1, Math.round(totalPersonnel * 0.2));
            document.getElementById('finishesPersonnel').value = Math.max(1, Math.round(totalPersonnel * 0.3));
            document.getElementById('packagingPersonnel').value = Math.max(0, totalPersonnel - 
                (parseInt(document.getElementById('partsProductionPersonnel').value) || 0) -
                (parseInt(document.getElementById('framingAssemblyPersonnel').value) || 0) -
                (parseInt(document.getElementById('finishesPersonnel').value) || 0));
            
            updateResourceAllocation();
            showNotification("Personnel allocation optimized.", "success");
        }
        
        function resetWorkManager() {
            document.getElementById('targetCompletionDays').value = 14;
            document.getElementById('workHoursPerDay').value = 8;
            document.getElementById('actualPersonnelAvailable').value = 5;
            document.getElementById('partsProductionPersonnel').value = 2;
            document.getElementById('framingAssemblyPersonnel').value = 1;
            document.getElementById('finishesPersonnel').value = 2;
            document.getElementById('packagingPersonnel').value = 0;
            
            calculateWorkRequirements();
            showNotification("Work Manager reset to default values.", "success");
        }
        
        // --- INVOICE GENERATION ---
        function setupInvoiceTab() {
            // Reset invoice container
            document.getElementById('invoiceContainer').innerHTML = '';
            document.getElementById('invoiceContainer').style.display = 'none';
            document.getElementById('printInvoice').style.display = 'none';
        }
        
        function generateInvoice() {
            // First calculate costs to get accurate pricing
            const costResults = calculateProjectCost();
            
            // Get current date
            const today = new Date();
            const invoiceDate = today.toLocaleDateString();
            const invoiceNumber = `INV-${today.getFullYear()}-${Math.floor(1000 + Math.random() * 9000)}`;
            
            // Format currency values
            const formatCurrency = (value) => {
                return new Intl.NumberFormat('en-NG', { 
                    style: 'currency', 
                    currency: 'NGN',
                    minimumFractionDigits: 0
                }).format(value).replace('₦', '');
            };
            
            // Calculate VAT (7.5%)
            const vat = costResults.salesPrice * 0.075;
            const grandTotal = costResults.salesPrice + vat;
            
            // Get client information
            const clientName = document.getElementById('clientName').value || 'Client';
            const clientAddress = document.getElementById('clientAddr').value || 'Address';
            const clientCity = document.getElementById('clientAddr').value || 'City';
            
            // Get project information
            const projectName = document.getElementById('projName').value || 'Project';
            const projectCode = document.getElementById('projectCode').value || 'Project Code';
            const salesRep = document.getElementById('projMgr').value || 'Sales Representative';
            const shippingLocation = document.getElementById('destCitySelect').value || 'Shipping Location';
            
            // Build the invoice HTML
            const invoiceHTML = `
                <div class="invoice-header">
                    <div>
                        <div class="company-name">APT ENGINEERING WORKS LTD</div>
                        <div class="address">Plot A, Obaferni Awolowo way, Alausa Ikeja, Lagos</div>
                    </div>
                    <div class="invoice-title">
                        <h1>INVOICE</h1>
                    </div>
                </div>
                
                <div class="invoice-content">
                    <div class="info-grid">
                        <div class="info-box">
                            <h3><i class="fas fa-building"></i> SOLD TO</h3>
                            <div class="info-row">
                                <div class="info-label">Name:</div>
                                <div>${clientName}</div>
                            </div>
                            <div class="info-row">
                                <div class="info-label">Address:</div>
                                <div>${clientAddress}</div>
                            </div>
                            <div class="info-row">
                                <div class="info-label">City, State, ZIP:</div>
                                <div>${clientCity}</div>
                            </div>
                            <div class="info-row">
                                <div class="info-label">Country:</div>
                                <div>NIGERIA</div>
                            </div>
                        </div>
                        
                        <div class="info-box">
                            <h3><i class="fas fa-file-invoice"></i> INVOICE DETAILS</h3>
                            <div class="info-row">
                                <div class="info-label">Invoice #:</div>
                                <div>${invoiceNumber}</div>
                            </div>
                            <div class="info-row">
                                <div class="info-label">Invoice Date:</div>
                                <div>${invoiceDate}</div>
                            </div>
                            <div class="info-row">
                                <div class="info-label">Your Order:</div>
                                <div>${projectName}</div>
                            </div>
                            <div class="info-row">
                                <div class="info-label">Sales Rep:</div>
                                <div>${salesRep}</div>
                            </div>
                            <div class="info-row">
                                <div class="info-label">F.O.B:</div>
                                <div>AEWorks</div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="shipping-info">
                        <i class="fas fa-truck"></i> <strong>Shipped To:</strong> ${shippingLocation}
                    </div>
                    
                    <table class="items-table">
                        <thead>
                            <tr>
                                <th>ITEM NO</th>
                                <th>DESCRIPTION</th>
                                <th>QTY</th>
                                <th>UNIT PRICE</th>
                                <th>AMOUNT (₦)</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>1</td>
                                <td>${projectName} - Custom Engineering Solution</td>
                                <td>1</td>
                                <td>${formatCurrency(costResults.salesPrice)}</td>
                                <td>${formatCurrency(costResults.salesPrice)}</td>
                            </tr>
                            <tr>
                                <td colspan="4" style="text-align: right; font-weight: 600;">Subtotal</td>
                                <td>${formatCurrency(costResults.salesPrice)}</td>
                            </tr>
                            <tr>
                                <td colspan="4" style="text-align: right; font-weight: 600;">VAT (7.5%)</td>
                                <td>${formatCurrency(vat)}</td>
                            </tr>
                        </tbody>
                    </table>
                    
                    <div class="totals-section">
                        <div class="payment-info">
                            <h3><i class="fas fa-university"></i> PAYMENT INFORMATION</h3>
                            <p><strong>Please make all checks payable to:</strong></p>
                            <p>Account Name: APT ENGINEERING WORKS LTD</p>
                            <p>Bank name: ACCESS BANK PLC</p>
                            <p>Acc. No: 0064324677</p>
                        </div>
                        
                        <div class="totals-table">
                            <div class="total-row">
                                <div>Subtotal:</div>
                                <div>₦${formatCurrency(costResults.salesPrice)}</div>
                            </div>
                            <div class="total-row">
                                <div>VAT:</div>
                                <div>₦${formatCurrency(vat)}</div>
                            </div>
                            <div class="total-row">
                                <div>Shipping:</div>
                                <div>-</div>
                            </div>
                            <div class="total-row grand-total">
                                <div>GRAND TOTAL:</div>
                                <div>₦${formatCurrency(grandTotal)}</div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="terms-section">
                        <h3><i class="fas fa-file-contract"></i> TERMS & CONDITIONS</h3>
                        <ul class="terms-list">
                            <li>60% deposition kickoff</li>
                            <li>Project is to be built according to project specifications</li>
                            <li>Project to be completed in ${document.getElementById('targetCompletionDays') ? document.getElementById('targetCompletionDays').value : 14} working days</li>
                        </ul>
                    </div>
                    
                    <div class="correspondence">
                        <div>
                            <h3><i class="fas fa-user"></i> CORRESPONDENCE</h3>
                            <p>${document.getElementById('clientMgr').value || 'Project Manager'}</p>
                            <p>${document.getElementById('clientPhone').value || 'Phone'}</p>
                            <p>${document.getElementById('clientEmail').value || 'Email'}</p>
                        </div>
                        <div style="text-align: right;">
                            <div style="margin-top: 20px;">
                                <img src="https://api.qrserver.com/v1/create-qr-code/?size=100x100&data=${invoiceNumber}" alt="Invoice QR Code">
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="invoice-guide-section" style="display: none;">
                    <h2><i class="fas fa-file-invoice-dollar"></i> INVOICE TYPE GUIDE</h2>
                    <table class="guide-table">
                        <thead>
                            <tr>
                                <th>Scenario</th>
                                <th>Best Invoice Type</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Selling a product/service</td>
                                <td>Standard Invoice</td>
                            </tr>
                            <tr>
                                <td>International shipping</td>
                                <td>Commercial Invoice</td>
                            </tr>
                            <tr>
                                <td>Subscription billing</td>
                                <td>Recurring Invoice</td>
                            </tr>
                            <tr>
                                <td>Hourly work tracking</td>
                                <td>Timesheet Invoice</td>
                            </tr>
                            <tr>
                                <td>Partial project payments</td>
                                <td>Interim Invoice</td>
                            </tr>
                            <tr>
                                <td>Refunding a customer</td>
                                <td>Credit Invoice</td>
                            </tr>
                            <tr>
                                <td>Charging extra fees</td>
                                <td>Debit Invoice</td>
                            </tr>
                            <tr>
                                <td>Final project payment</td>
                                <td>Final Invoice</td>
                            </tr>
                            <tr>
                                <td>Late payment follow-up</td>
                                <td>Past Due Invoice</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                
                <div class="footer">
                    <p>APT ENGINEERING WORKS LTD &copy; ${today.getFullYear()} | Invoice #${invoiceNumber}</p>
                    <p>This is an electronically generated invoice - no signature required</p>
                </div>
            `;
            
            // Set the HTML to the container
            const invoiceContainer = document.getElementById('invoiceContainer');
            invoiceContainer.innerHTML = invoiceHTML;
            invoiceContainer.style.display = 'block';
            
            // Show the print button
            document.getElementById('printInvoice').style.display = 'inline-block';
            
            // Generate PDF
            html2canvas(invoiceContainer, {
                scale: 2,
                useCORS: true,
                logging: false
            }).then(canvas => {
                const imgData = canvas.toDataURL('image/png');
                const pdf = new jspdf.jsPDF({
                    orientation: 'portrait',
                    unit: 'mm',
                    format: 'a4'
                });
                
                const imgWidth = 210; // A4 width in mm
                const pageHeight = 297; // A4 height in mm
                const imgHeight = canvas.height * imgWidth / canvas.width;
                let heightLeft = imgHeight;
                let position = 0;
                
                pdf.addImage(imgData, 'PNG', 0, position, imgWidth, imgHeight);
                heightLeft -= pageHeight;
                
                while (heightLeft >= 0) {
                    position = heightLeft - imgHeight;
                    pdf.addPage();
                    pdf.addImage(imgData, 'PNG', 0, position, imgWidth, imgHeight);
                    heightLeft -= pageHeight;
                }
                
                // Generate filename with project code and date
                const dateStr = `${today.getFullYear()}${(today.getMonth()+1).toString().padStart(2, '0')}${today.getDate().toString().padStart(2, '0')}`;
                const filename = `Invoice_${projectCode.replace(/[^a-zA-Z0-9]/g, '_')}_${dateStr}.pdf`;
                
                // Save the PDF
                pdf.save(filename);
                
                showNotification("PDF invoice generated successfully!", "success");
            }).catch(error => {
                console.error("Error generating PDF:", error);
                showNotification("Error generating PDF invoice. Please try again.", "error");
            });
        }
        
        function printInvoice() {
            window.print();
        }
        
        // --- CORE PROJECT LOGIC ---
        function saveProject(){
            const code=document.getElementById('projectCode').value;
            if(!code){showNotification("Project name is required.","error");return;}
            updateFramingTakeOffFromUI();
            updateFinishesTakeOffFromUI();
            const pData={
                framingTakeOff:currentProject.framingTakeOff,
                finishesTakeOff:currentProject.finishesTakeOff,
                costingVariables:{},
                adjustedCosts: currentProject.adjustedCosts || null
            };
            const fields=['projName','jobsThisYear','year','projectCode','projectStatus','prodCentre','prodCoords','clientName','clientMgr','clientPhone','clientEmail','clientAddr','destCitySelect','destCoords','projMgr','mgrPhone','mgrEmail','shippingLength','shippingWidth','shippingHeight'];
            fields.forEach(id=>pData[id]=document.getElementById(id).value);
            document.querySelectorAll('#costingVariablesSection input').forEach(input=>{
                pData.costingVariables[input.id]=input.value;
            });
            pData.savedAt=new Date().toISOString();
            const projects=getData('projects'),i=projects.findIndex(p=>p.projectCode===code);
            if(i>-1)projects[i]=pData;
            else projects.push(pData);
            if(saveData('projects',projects))showNotification(`Project ${code} saved.`,'success');
        }
        function loadProject(code=null){
            if(!code){showProjectList();return;}
            const p=getData('projects').find(pr=>pr.projectCode===code);
            if(p){
                Object.keys(p).forEach(k=>{
                    const e=document.getElementById(k);
                    if(e)e.value=p[k];
                });
                currentProject.framingTakeOff=p.framingTakeOff||[];
                currentProject.finishesTakeOff=p.finishesTakeOff||[];
                currentProject.costingVariables=p.costingVariables||{};
                currentProject.adjustedCosts=p.adjustedCosts||null;
                initCostingTab();
                Object.keys(currentProject.costingVariables).forEach(id=>{
                    const input=document.getElementById(id);
                    if(input)input.value=currentProject.costingVariables[id];
                });
                renderFramingTakeOffTable();
                renderFinishesTakeOffTable();
                handleCityChange();
                updateStatusBar();
                openTab({currentTarget:document.querySelector('.tab-button')},'ProjectSpec');
                showNotification(`Project ${p.projectCode} loaded.`,'success');
                closeProjectList();
            }else{
                showNotification("Project not found!","error");
            }
        }
        function showProjectList(){
            const p=getData('projects'),l=document.getElementById('projectListItems');
            l.innerHTML=p.length===0?'<li style="padding:15px;text-align:center;">No saved projects</li>':'';
            p.sort((a,b)=>new Date(b.savedAt)-new Date(a.savedAt)).forEach(pr=>{
                const li=document.createElement('li');
                li.style.cssText='padding:15px;border-bottom:1px solid #eee;cursor:pointer;';
                li.onclick=()=>loadProject(pr.projectCode);
                const s=document.querySelector(`#projectStatus option[value='${pr.projectStatus}']`)?.textContent||'Unknown',
                      d=new Date(pr.savedAt).toLocaleDateString();
                li.innerHTML=`<div style="display:flex;justify-content:space-between;"><div><strong>${pr.projectCode}</strong> - ${pr.projName||'Unnamed'}</div><div style="font-size:0.9rem;color:#7f8c8d;">${d}</div></div>
                <div style="margin-top:8px;display:flex;gap:15px;font-size:0.9rem;">
                    <span><i class="fas fa-user"></i> ${pr.projMgr||'N/A'}</span>
                    <span><i class="fas fa-industry"></i> ${pr.prodCentre||'N/A'}</span>
                    <span style="background:var(--accent);color:white;padding:3px 8px;border-radius:20px;">${s}</span>
                </div>`;
                l.appendChild(li);
            });
            document.getElementById('projectListModal').style.display='flex';
        }
        function closeProjectList(){
            document.getElementById('projectListModal').style.display='none';
        }
        function calculateHaversineDistance(c1,c2){
            if(!c1||!c2)return -1;
            const r=(v)=>(v*Math.PI)/180;
            try{
                const[t1,n1]=c1.split(',').map(Number),
                      [t2,n2]=c2.split(',').map(Number);
                if([t1,n1,t2,n2].some(isNaN))return -1;
                const R=6371,d=r(t2-t1),o=r(n2-n1);
                const a=Math.sin(d/2)**2+Math.cos(r(t1))*Math.cos(r(t2))*Math.sin(o/2)**2;
                return R*2*Math.atan2(Math.sqrt(a),Math.sqrt(1-a));
            }catch(e){
                console.error("Coord parse error:",e);
                return -1;
            }
        }
        function generateProjectPreview(){
            const container=document.getElementById('projectPreviewContainer');
            container.innerHTML='';
            const get=(id)=>document.getElementById(id).value;
            const sE=document.getElementById('projectStatus'),
                  sT=sE.options[sE.selectedIndex]?.text||'Unknown';
            const costResults=calculateProjectCost();
            const pC=document.createElement('div');
            pC.className='project-preview';
            pC.innerHTML=`
                <div class="project-header">
                    <div class="project-title">${get('projName')||'Unnamed'}</div>
                    <div class="project-code">${get('projectCode')||'No Code'}</div>
                </div>
                <div class="project-details">
                    <div class="detail-item"><span>Client</span><span>${get('clientName')||'N/A'}</span></div>
                    <div class="detail-item"><span>Manager</span><span>${get('projMgr')||'N/A'}</span></div>
                    <div class="detail-item"><span>Center</span><span>${get('prodCentre')||'N/A'}</span></div>
                    <div class="detail-item"><span>Status</span><span>${sT}</span></div>
                </div>`;
            container.appendChild(pC);
            const mC=document.createElement('div');
            mC.className='project-preview';
            mC.innerHTML=`
                <div class="project-header">
                    <div class="project-title">Cost & Quote Summary</div>
                    <span class="details-toggle">Show Details</span>
                </div>
                <div class="details-content" style="display:block;">
                    <table class="cost-summary-table">
                        <tr class="grand-total-row">
                            <td><strong>Recommended Sales Price</strong></td>
                            <td><strong>${costResults.formatN(costResults.salesPrice)}</strong></td>
                        </tr>
                        <tr class="total-row">
                            <td><strong>Total Estimated Cost</strong></td>
                            <td><strong>${costResults.formatN(costResults.totalCost)}</strong></td>
                        </tr>
                        <tr>
                            <td>Target Profit</td>
                            <td>${costResults.formatN(costResults.profit)}</td>
                        </tr>
                    </table>
                </div>
                <div class="project-header" style="margin-top:20px;">
                    <div class="project-title">Materials Cost Breakdown</div>
                    <span class="details-toggle">Show Details</span>
                </div>
                <div class="details-content">
                    <table>
                        <thead>
                            <tr>
                                <th>Description</th>
                                <th>Material</th>
                                <th>Qty</th>
                                <th>Unit Price</th>
                                <th>Total Price</th>
                            </tr>
                        </thead>
                        <tbody>${costResults.materialDetailsHTML}</tbody>
                    </table>
                </div>
                <div class="project-header" style="margin-top:20px;">
                    <div class="project-title">Other Costs Breakdown</div>
                    <span class="details-toggle">Show Details</span>
                </div>
                <div class="details-content">
                    <table class="costing-table">${costResults.otherCostsHTML}</table>
                </div>`;
            container.appendChild(mC);
        }
        // --- BULK IMPORT ---
        function handleMasterFileUpload(e,k,h,rFn){
            const f=e.target.files[0];
            if(!f)return;
            const r=new FileReader();
            r.onload=function(ev){
                const t=ev.target.result,
                      p=parseCSV(t,h);
                if(p.error){
                    showNotification(p.error,"error");
                    return;
                }
                const d=getData(k).concat(p.data);
                if(saveData(k,d)){
                    showNotification(`${p.data.length} records imported to ${k}.`,"success");
                    rFn();
                    refreshDropdowns();
                }
            };
            r.readAsText(f);
            e.target.value='';
        }
        function handleTakeOffFileUpload(e,type){
            const f=e.target.files[0];
            if(!f)return;
            const r=new FileReader();
            r.onload=function(ev){
                let h,tA,rFn,m;
                if(type==='framing'){
                    h=['Description','Framing Material','Length (m)','Width (m)','Quantity'];
                    tA=currentProject.framingTakeOff;
                    rFn=renderFramingTakeOffTable;
                    m={'Description':'desc','Framing Material':'material','Length (m)':'length','Width (m)':'width','Quantity':'qty'};
                }else{
                    h=['Description','Finish Material','Quantity'];
                    tA=currentProject.finishesTakeOff;
                    rFn=renderFinishesTakeOffTable;
                    m={'Description':'desc','Finish Material':'material','Quantity':'qty'};
                }
                const p=parseCSV(ev.target.result,h);
                if(p.error){
                    showNotification(p.error,"error");
                    return;
                }
                p.data.forEach(cR=>{
                    const nR={};
                    for(const k in m){
                        const cRKey=Object.keys(cR).find(key=>key.toLowerCase()===k.toLowerCase());
                        if(cRKey)nR[m[k]]=cR[cRKey];
                    }
                    tA.push(nR);
                });
                rFn();
                showNotification(`${p.data.length} take-off items imported.`,"success");
            };
            r.readAsText(f);
            e.target.value='';
        }
        function parseCSV(text,expectedHeaders){
            const lines=text.trim().replace(/\r/g,'').split('\n');
            const fileHeaders=lines[0].split(',').map(h=>h.trim());
            const fileHeadersLower=fileHeaders.map(h=>h.toLowerCase());
            const expectedHeadersLower=expectedHeaders.map(h=>h.toLowerCase());
            for(const expected of expectedHeadersLower){
                if(!fileHeadersLower.includes(expected)){
                    return{error:`CSV missing required header: ${expectedHeaders[expectedHeadersLower.indexOf(expected)]}`};
                }
            }
            const data=[];
            for(let i=1;i<lines.length;i++){
                if(!lines[i])continue;
                const values=lines[i].split(',');
                const obj={};
                fileHeaders.forEach((header,index)=>{
                    obj[header]=values[index]?values[index].trim():'';
                });
                data.push(obj);
            }
            return{data};
        }
        // --- COSTING TAB ---
        const COST_VARS_STRUCTURE = {
            "Labor Rates (₦/day)":{
                general_labor:["General Labor",12000],
                painter_labor:["Painter",20000],
                support_labor:["Support Staff",9600],
                admin_labor:["Admin",16000]
            },
            "Production Rates & Assumptions":{
                fitting_hrs_per_meter:["Fitting (hrs/m)",0.2],
                assembly_hrs_per_frame:["Assembly (hrs/frame)",0.5],
                testing_hrs_per_frame:["Testing (hrs/frame)",0.25],
                cleaning_sqm_per_hr:["Cleaning (m²/hr)",8],
                priming_sqm_per_hr:["Priming (m²/hr)",10],
                painting_sqm_per_hr:["Painting (m²/hr)",8],
                packaging_mins_per_frame:["Packaging (mins/frame)",10],
                meters_per_cutting_disc:["Meters per Cutting Disc",10],
                electrodes_per_meter:["Weld Electrodes per Meter",2],
                brushes_per_sqm:["Wire Brushes per m²",0.05],
                sandpaper_per_sqm:["Sandpaper per m²",0.083]
            },
            "Overheads":{
                facility_rate:["Facility Rental (₦/day)",24000],
                power_rate:["Power Supply (₦/day)",8000],
                design_cost:["Design Costs (₦)",50000],
                supervision_cost_percent:["Supervision (% of Labor)",15]
            },
            "Profit":{
                markup_percent:["Markup (%)",25]
            }
        };
        function initCostingTab(){
            const varContainer=document.getElementById('costingVariablesSection'),
                  resContainer=document.getElementById('costingResultsSection');
            let varHTML='', resHTML='';
            const defaultVars=getData('defaultCostingVariables');
            for(const category in COST_VARS_STRUCTURE){
                varHTML+=`<h4>${category}</h4><table class="costing-table">`;
                for(const key in COST_VARS_STRUCTURE[category]){
                    const[label,defaultValue]=COST_VARS_STRUCTURE[category][key];
                    const value=defaultVars[key]||defaultValue;
                    varHTML+=`<tr><td>${label}</td><td><input type="number" id="${key}" value="${value}"></td></tr>`;
                    if(currentProject.costingVariables[key]===undefined){
                        currentProject.costingVariables[key]=value;
                    }
                }
                varHTML+='</table>';
            }
            varContainer.innerHTML=`
                <h3><i class="fas fa-sliders-h"></i> Costing Variables</h3>
                <button onclick="saveCostingDefaults()" class="btn btn-outline" style="margin-top:-10px;margin-bottom:15px;">
                    <i class="fas fa-save"></i> Save as Default
                </button>
                ${varHTML}`;
            resHTML=`
                <div id="costingResultContent">
                    <p style="text-align:center;color:var(--gray);">Click 'Calculate Costs' to see the breakdown.</p>
                </div>`;
            resContainer.innerHTML=`
                <h3><i class="fas fa-chart-bar"></i> Cost Breakdown</h3>
                ${resHTML}`;
        }
        function saveCostingDefaults(){
            const newDefaults={};
            for(const category in COST_VARS_STRUCTURE){
                for(const key in COST_VARS_STRUCTURE[category]){
                    newDefaults[key]=document.getElementById(key).value;
                }
            }
            saveData('defaultCostingVariables',newDefaults);
            showNotification("Costing variables saved as default for new projects.","success");
        }
        // --- COST CALCULATION ENGINE ---
        function calculateProjectCostAndDisplay(){
            const results=calculateProjectCost();
            displayCostResults(results);
            showNotification("Costs calculated successfully!","success");
        }
        function calculateProjectCost(){
            const vars={}, res={materialDetails:[]};
            // Load all costing variables
            for(const c in COST_VARS_STRUCTURE){
                for(const k in COST_VARS_STRUCTURE[c]){
                    vars[k]=parseFloat(document.getElementById(k).value)||0;
                }
            }
            // Update take-off data from UI
            updateFramingTakeOffFromUI();
            updateFinishesTakeOffFromUI();
            // Initialize cost totals
            let totalFramingCost=0,
                totalCladdingCost=0,
                totalLinearLength=0,
                totalSurfaceArea=0,
                uniqueFrames=new Set();
            const framingDb=getData('framingMaterials'),
                  finishesDb=getData('finishMaterials');
            // Calculate framing material costs
            currentProject.framingTakeOff.forEach(item=>{
                const m=framingDb.find(db=>db['FRAMING MATERIALS']===item.material);
                if(!m)return;
                const len=parseFloat(item.length)||0,
                      wid=parseFloat(item.width)||0,
                      qty=parseFloat(item.qty)||0,
                      rate=parseFloat(m.RATE)||0,
                      saM=parseFloat(m['Surface Area'])||0,
                      desc=item.desc.trim();
                if(desc)uniqueFrames.add(desc);
                const isClad=isSheetMaterial(item.material);
                let itemCost=0, itemSA=0, unitPrice=0;
                if(isClad){
                    itemSA=(len*wid)*qty*2;
                    itemCost=(len*wid)*qty*rate;
                    unitPrice=rate;
                }else{
                    itemSA=len*qty*saM;
                    itemCost=len*qty*rate;
                    unitPrice=rate;
                    totalLinearLength+=len*qty;
                }
                res.materialDetails.push({
                    desc,
                    material:item.material,
                    qty:`${qty} ${isClad?'pcs':'m²'}`,
                    unitPrice,
                    totalPrice:itemCost
                });
                totalSurfaceArea+=itemSA;
                if(isClad){
                    totalCladdingCost+=itemCost;
                }else{
                    totalFramingCost+=itemCost;
                }
            });
            // Calculate finishes/connectors costs
            let totalFinishesConnectorsCost=0;
            currentProject.finishesTakeOff.forEach(item=>{
                const m=finishesDb.find(db=>db['NAME - MATERIAL']===item.material);
                if(!m)return;
                const qty=parseFloat(item.qty)||0,
                      price=parseFloat(m.PRICE)||0;
                res.materialDetails.push({
                    desc:item.desc,
                    material:item.material,
                    qty,
                    unitPrice:price,
                    totalPrice:qty*price
                });
                totalFinishesConnectorsCost+=qty*price;
            });
            // Calculate labor and production costs
            const workDayHours=8;
            // Fitting labor
            res.fittingTime=totalLinearLength*vars.fitting_hrs_per_meter;
            res.fittingLaborCost=(res.fittingTime/workDayHours)*vars.general_labor;
            // Fitting consumables
            res.numDiscs=Math.ceil(totalLinearLength/vars.meters_per_cutting_disc);
            res.numElectrodes=Math.ceil(totalLinearLength*vars.electrodes_per_meter);
            res.fittingConsumablesCost=(res.numDiscs*vars.cutting_disc_cost)+(res.numElectrodes*vars.welding_electrode_cost);
            // Assembly and testing
            res.assemblyTime=uniqueFrames.size*vars.assembly_hrs_per_frame;
            res.testingTime=uniqueFrames.size*vars.testing_hrs_per_frame;
            res.qaqcCost=((res.assemblyTime+res.testingTime)/workDayHours)*vars.general_labor;
            res.uniqueFramesCount=uniqueFrames.size;
            // Finishes labor
            res.cleaningTime=totalSurfaceArea/vars.cleaning_sqm_per_hr;
            res.cleaningLabor=(res.cleaningTime/workDayHours)*vars.general_labor;
            res.numBrushes=Math.ceil(totalSurfaceArea*vars.brushes_per_sqm);
            res.numSandpaper=Math.ceil(totalSurfaceArea*vars.sandpaper_per_sqm);
            res.cleaningConsumables=(res.numBrushes*vars.wire_brush_cost)+(res.numSandpaper*vars.sandpaper_cost);
            res.primingTime=totalSurfaceArea/vars.priming_sqm_per_hr;
            res.primingLabor=(res.primingTime/workDayHours)*vars.painter_labor;
            res.paintingTime=totalSurfaceArea/vars.painting_sqm_per_hr;
            res.paintingLabor=(res.paintingTime/workDayHours)*vars.painter_labor;
            res.finishesLabor=res.cleaningLabor+res.primingLabor+res.paintingLabor;
            // Packaging
            res.packagingTime=uniqueFrames.size*(vars.packaging_mins_per_frame/60);
            res.packagingLabor=(res.packagingTime/workDayHours)*vars.support_labor;
            // Total production time
            res.totalProdTime=res.fittingTime+res.assemblyTime+res.testingTime+
                            res.cleaningTime+res.primingTime+res.paintingTime+
                            res.packagingTime;
            // Shipping costs
            const shipL=parseFloat(document.getElementById('shippingLength').value)||0,
                  shipW=parseFloat(document.getElementById('shippingWidth').value)||0,
                  shipH=parseFloat(document.getElementById('shippingHeight').value)||0;
            const vol=shipL*shipW*shipH;
            res.shippingCost=0;
            const dist=calculateHaversineDistance(
                document.getElementById('prodCoords').value,
                document.getElementById('destCoords').value
            );
            if(dist!==-1){
                const isL=dist<=LOCAL_DISTANCE_THRESHOLD,
                      rate=isL?LOCAL_SHIPPING_RATE_PER_CUBIC_METER:NATIONAL_SHIPPING_RATE_PER_CUBIC_METER;
                res.shippingCost=vol*rate;
            }
            // Overheads
            const totalProdDays=res.totalProdTime/workDayHours;
            res.facilityCost=totalProdDays*vars.facility_rate;
            res.powerCost=totalProdDays*vars.power_rate;
            res.adminCost=totalProdDays*vars.admin_labor;
            // Supervision
            res.totalLabor=res.fittingLaborCost+res.qaqcCost+res.finishesLabor+res.packagingLabor;
            res.supervisionCost=res.totalLabor*(vars.supervision_cost_percent/100);
            // Totals
            res.totalMaterialCost=totalFramingCost+totalCladdingCost+totalFinishesConnectorsCost;
            res.totalConsumableCost=res.fittingConsumablesCost+res.cleaningConsumables;
            res.totalOverhead=res.facilityCost+res.powerCost+res.adminCost+vars.design_cost+res.supervisionCost;
            res.totalCost=res.totalLabor+res.totalMaterialCost+res.totalConsumableCost+res.totalOverhead+res.shippingCost;
            // Pricing
            res.salesPrice=res.totalCost*(1+vars.markup_percent/100);
            res.profit=res.salesPrice-res.totalCost;
            // Formatting helper
            res.formatN=(v)=>`₦${(v||0).toLocaleString(undefined,{minimumFractionDigits:2,maximumFractionDigits:2})}`;
            // Generate material details HTML
            res.materialDetailsHTML='';
            res.materialDetails.forEach(item=>{
                res.materialDetailsHTML+=`
                    <tr>
                        <td>${item.desc}</td>
                        <td>${item.material}</td>
                        <td>${item.qty}</td>
                        <td>${res.formatN(item.unitPrice)}</td>
                        <td>${res.formatN(item.totalPrice)}</td>
                    </tr>`;
            });
            // Generate other costs breakdown HTML
            res.otherCostsHTML=`
                <tr>
                    <td>Fitting Labor</td>
                    <td>${res.formatN(res.fittingLaborCost)}<small>(${(res.fittingTime/workDayHours).toFixed(1)} man-days @ ${res.formatN(vars.general_labor)}/day)</small></td>
                </tr>
                <tr>
                    <td>Fitting Consumables</td>
                    <td>${res.formatN(res.fittingConsumablesCost)}<small>(${res.numDiscs} discs, ${res.numElectrodes} elec.)</small></td>
                </tr>
                <tr>
                    <td>QAQC & Fits</td>
                    <td>${res.formatN(res.qaqcCost)}<small>(${res.uniqueFramesCount} frames)</small></td>
                </tr>
                <tr>
                    <td>Finishes Labor</td>
                    <td>${res.formatN(res.finishesLabor)}<small>(${((res.cleaningTime+res.primingTime+res.paintingTime)/workDayHours).toFixed(1)} man-days)</small></td>
                </tr>
                <tr>
                    <td>Finishes Consumables</td>
                    <td>${res.formatN(res.cleaningConsumables)}<small>(${res.numBrushes} brushes, ${res.numSandpaper} sheets)</small></td>
                </tr>
                <tr>
                    <td>Packaging Labor</td>
                    <td>${res.formatN(res.packagingLabor)}<small>(${(res.packagingTime/workDayHours).toFixed(1)} man-days)</small></td>
                </tr>
                <tr>
                    <td>Shipping</td>
                    <td>${res.formatN(res.shippingCost)}<small>(${vol.toFixed(2)} m³)</small></td>
                </tr>
                <tr>
                    <td>Facility & Power</td>
                    <td>${res.formatN(res.facilityCost+res.powerCost)}<small>(${totalProdDays.toFixed(1)} days)</small></td>
                </tr>
                <tr>
                    <td>Admin</td>
                    <td>${res.formatN(res.adminCost)}<small>(${totalProdDays.toFixed(1)} days)</small></td>
                </tr>
                <tr>
                    <td>Design</td>
                    <td>${res.formatN(vars.design_cost)}</td>
                </tr>
                <tr>
                    <td>Supervision</td>
                    <td>${res.formatN(res.supervisionCost)}<small>(${vars.supervision_cost_percent}% of labor)</small></td>
                </tr>`;
            // Apply any saved adjustments
            if(currentProject.adjustedCosts){
                res.totalMaterialCost = currentProject.adjustedCosts.totalMaterialCost;
                res.totalLabor = currentProject.adjustedCosts.totalLabor;
                res.totalConsumableCost = currentProject.adjustedCosts.totalConsumableCost;
                res.totalOverhead = currentProject.adjustedCosts.totalOverhead;
                res.shippingCost = currentProject.adjustedCosts.shippingCost;
                res.totalCost = currentProject.adjustedCosts.totalCost;
                res.salesPrice = currentProject.adjustedCosts.salesPrice;
                res.profit = res.salesPrice - res.totalCost;
                // Update the markup percentage input
                document.getElementById('markup_percent').value = currentProject.adjustedCosts.markupPercent;
            }
            return res;
        }
        function displayCostResults(res) {
            const container = document.getElementById('costingResultContent');
            if (!res) { container.innerHTML = `<p>Error calculating costs.</p>`; return; }
            container.innerHTML = `
                <table class="costing-table cost-summary-table">
                    <tr>
                        <td>Total Material Cost</td>
                        <td><input type="number" id="totalMaterialCost" value="${res.totalMaterialCost}" step="0.01" onchange="updateCostFromInput('totalMaterialCost')"></td>
                    </tr>
                    <tr>
                        <td>Total Direct Labor</td>
                        <td><input type="number" id="totalLabor" value="${res.totalLabor}" step="0.01" onchange="updateCostFromInput('totalLabor')"></td>
                    </tr>
                    <tr>
                        <td>Total Consumable Cost</td>
                        <td><input type="number" id="totalConsumableCost" value="${res.totalConsumableCost}" step="0.01" onchange="updateCostFromInput('totalConsumableCost')"></td>
                    </tr>
                    <tr>
                        <td>Total Overhead</td>
                        <td><input type="number" id="totalOverhead" value="${res.totalOverhead}" step="0.01" onchange="updateCostFromInput('totalOverhead')"></td>
                    </tr>
                    <tr>
                        <td>Shipping Cost</td>
                        <td><input type="number" id="shippingCost" value="${res.shippingCost}" step="0.01" onchange="updateCostFromInput('shippingCost')"></td>
                    </tr>
                    <tr class="total-row">
                        <td><strong>Total Cost</strong></td>
                        <td><strong><input type="number" id="totalCost" value="${res.totalCost}" step="0.01" onchange="updateCostFromInput('totalCost')"></strong></td>
                    </tr>
                    <tr>
                        <td>Markup Percentage</td>
                        <td><input type="number" id="markupPercent" value="${parseFloat(document.getElementById('markup_percent').value)}" step="0.01" onchange="updateMarkup()">%</td>
                    </tr>
                    <tr class="grand-total-row">
                        <td><strong>Rec. Sales Price</strong></td>
                        <td><strong><input type="number" id="salesPrice" value="${res.salesPrice}" step="0.01" onchange="updateCostFromInput('salesPrice')"></strong></td>
                    </tr>
                    <tr>
                        <td>Target Profit</td>
                        <td><input type="number" id="profit" value="${res.profit}" step="0.01" readonly></td>
                    </tr>
                </table>
                <button onclick="saveAdjustedCosts()" class="btn btn-primary" style="margin-top:15px;">
                    <i class="fas fa-save"></i> Save Adjusted Costs
                </button>`;
        }
        function updateCostFromInput(id) {
            const value = parseFloat(document.getElementById(id).value) || 0;
            // Recalculate dependent values
            if (id === 'totalCost') {
                const markup = parseFloat(document.getElementById('markup_percent').value) / 100;
                const salesPrice = value * (1 + markup);
                document.getElementById('salesPrice').value = salesPrice.toFixed(2);
                document.getElementById('profit').value = (salesPrice - value).toFixed(2);
            } 
            else if (id === 'salesPrice') {
                const totalCost = parseFloat(document.getElementById('totalCost').value) || 0;
                document.getElementById('profit').value = (value - totalCost).toFixed(2);
            }
            else {
                // Recalculate total cost if any component changes
                const material = parseFloat(document.getElementById('totalMaterialCost').value) || 0;
                const labor = parseFloat(document.getElementById('totalLabor').value) || 0;
                const consumables = parseFloat(document.getElementById('totalConsumableCost').value) || 0;
                const overhead = parseFloat(document.getElementById('totalOverhead').value) || 0;
                const shipping = parseFloat(document.getElementById('shippingCost').value) || 0;
                const total = material + labor + consumables + overhead + shipping;
                document.getElementById('totalCost').value = total.toFixed(2);
                const markup = parseFloat(document.getElementById('markup_percent').value) / 100;
                document.getElementById('salesPrice').value = (total * (1 + markup)).toFixed(2);
                document.getElementById('profit').value = (total * markup).toFixed(2);
            }
        }
        function updateMarkup() {
            const markupPercent = parseFloat(document.getElementById('markupPercent').value) || 0;
            document.getElementById('markup_percent').value = markupPercent;
            const totalCost = parseFloat(document.getElementById('totalCost').value) || 0;
            const salesPrice = totalCost * (1 + (markupPercent / 100));
            document.getElementById('salesPrice').value = salesPrice.toFixed(2);
            document.getElementById('profit').value = (salesPrice - totalCost).toFixed(2);
        }
        function saveAdjustedCosts() {
            // Save all adjusted values to the current project
            currentProject.adjustedCosts = {
                totalMaterialCost: parseFloat(document.getElementById('totalMaterialCost').value) || 0,
                totalLabor: parseFloat(document.getElementById('totalLabor').value) || 0,
                totalConsumableCost: parseFloat(document.getElementById('totalConsumableCost').value) || 0,
                totalOverhead: parseFloat(document.getElementById('totalOverhead').value) || 0,
                shippingCost: parseFloat(document.getElementById('shippingCost').value) || 0,
                totalCost: parseFloat(document.getElementById('totalCost').value) || 0,
                salesPrice: parseFloat(document.getElementById('salesPrice').value) || 0,
                markupPercent: parseFloat(document.getElementById('markupPercent').value) || 0
            };
            // Update the default markup percentage if changed
            const defaults = getData('defaultCostingVariables');
            defaults.markup_percent = currentProject.adjustedCosts.markupPercent;
            saveData('defaultCostingVariables', defaults);
            showNotification("Adjusted costs saved to project", "success");
        }
        // --- INITIAL DATA & APP START ---
        const initialFramingData=[{"MATERIAL / GROUP":"MILD STEEL ROD","FRAMING MATERIALS":"#8 - Steel Rebar","RATE":"682.54","Surface Area":"0.025"},{"MATERIAL / GROUP":"HDF Board","FRAMING MATERIALS":"18mm MDF Sheet","RATE":"25000","Surface Area":"0"}];
        const initialFinishData=[{"MATERIAL / GROUP":"Paints/Coats","NAME - MATERIAL":"Emulsion Basic","PRICE":"16000","Coverage":"30"},{"MATERIAL / GROUP":"Package (Carton/Films)","NAME - MATERIAL":"0.4mm Nylon","PRICE":"8000","Coverage":"50"}];
        window.onload=function(){document.getElementById('userBar').style.display='none';init();setTimeout(()=>{document.getElementById('username').value='admin';document.getElementById('password').value='admin123';login();},100);};
    </script>
</body>
</html>
