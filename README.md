<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailoring App</title>
    <style>
        :root {
            --green: #20D46B;
            --blue: #64A4FF;
            --purple: #B96DFF;
            --bg-main: #0B1B2A;
            --bg-card: #1B2B4A;
            --text-light: #A8B1C3;
            --red: #F04B3E;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background: #050d14;
            color: var(--text-light);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        /* Mobile App Frame Ratio Container */
        .app-frame {
            width: 100%;
            max-width: 420px;
            height: 100vh;
            max-height: 850px;
            background: var(--bg-main);
            border-radius: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            border: 4px solid #1B2B4A;
            position: relative;
        }

        /* Navbar */
        .navbar {
            background: var(--bg-card);
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid rgba(100, 164, 255, 0.1);
        }
        .navbar h2 {
            margin: 0;
            font-size: 18px;
            color: var(--blue);
            font-weight: bold;
            letter-spacing: 1px;
        }
        .menu-icon {
            font-size: 22px;
            cursor: pointer;
            color: var(--blue);
            user-select: none;
        }

        /* Dropdown Menu */
        .dropdown-menu {
            display: none;
            position: absolute;
            right: 15px;
            top: 60px;
            background: var(--bg-card);
            border: 1px solid var(--blue);
            border-radius: 10px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.6);
            z-index: 1000;
            width: 180px;
        }
        .dropdown-menu button {
            display: block;
            width: 100%;
            background: none;
            border: none;
            color: var(--text-light);
            padding: 12px 15px;
            text-align: left;
            cursor: pointer;
            font-size: 14px;
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }
        .dropdown-menu button:hover {
            background: var(--blue);
            color: var(--bg-main);
            font-weight: bold;
        }

        /* Scrollable Content Area */
        .content-area {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
        }
        .page {
            display: none;
        }
        .page.active {
            display: block;
        }

        h2, h3 {
            color: var(--blue);
            font-size: 16px;
            margin-top: 0;
        }

        /* Dashboard Cards */
        .dashboard {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 20px;
        }
        .card {
            background: var(--bg-card);
            padding: 15px;
            border-radius: 12px;
            border-left: 5px solid var(--blue);
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        }
        .card.profit-card {
            border-left-color: var(--green);
            background: #112d23;
        }
        .card.expense-card {
            border-left-color: var(--red);
            background: #2c1517;
        }
        .card p {
            font-size: 14px;
            margin: 6px 0;
            color: var(--text-light);
        }
        .card span {
            font-weight: bold;
            color: #fff;
        }

        /* Forms & Inputs */
        .form-box {
            background: var(--bg-card);
            padding: 15px;
            border-radius: 12px;
            border: 1px solid rgba(100, 164, 255, 0.2);
            margin-bottom: 20px;
        }
        .form-group {
            margin-bottom: 12px;
        }
        label {
            display: block;
            margin-bottom: 4px;
            font-weight: bold;
            color: var(--blue);
            font-size: 13px;
        }
        input, select {
            width: 100%;
            padding: 10px;
            box-sizing: border-box;
            background: var(--bg-main);
            border: 1px solid rgba(185, 109, 255, 0.3);
            color: #fff;
            border-radius: 8px;
            font-size: 14px;
        }
        button.btn-primary {
            background: var(--green);
            color: var(--bg-main);
            border: none;
            padding: 12px;
            cursor: pointer;
            border-radius: 8px;
            width: 100%;
            font-size: 15px;
            font-weight: bold;
            margin-top: 5px;
        }
        button.btn-primary:hover {
            opacity: 0.9;
        }

        /* Tables Container */
        .table-responsive {
            width: 100%;
            overflow-x: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
            background: var(--bg-card);
            border-radius: 8px;
            font-size: 12px;
        }
        th, td {
            border: 1px solid rgba(255,255,255,0.05);
            padding: 8px;
            text-align: left;
            white-space: nowrap;
        }
        th {
            background: #132238;
            color: var(--blue);
        }
        .whatsapp-link {
            color: var(--green);
            text-decoration: none;
            font-weight: bold;
        }
        
        .text-green { color: var(--green) !important; font-weight: bold; }
        .text-red { color: var(--red) !important; font-weight: bold; }
        .text-purple { color: var(--purple) !important; font-weight: bold; }
    </style>
</head>
<body>

<div class="app-frame">
    <!-- Navbar -->
    <div class="navbar">
        <h2>TAILORING APP</h2>
        <div class="menu-icon" onclick="toggleMenu()">☰</div>
        <div class="dropdown-menu" id="dropdownMenu">
            <button onclick="switchPage('dashboardPage')">Dashboard</button>
            <button onclick="switchPage('customerPage')">Add Customer</button>
            <button onclick="switchPage('itemPage')">Add Item</button>
            <button onclick="switchPage('employeePage')">Add Employee</button>
            <button onclick="switchPage('completedPage')">Completed Works</button>
            <button onclick="switchPage('analyticsPage')">Data Analytics</button>
        </div>
    </div>

    <!-- Main Content App View -->
    <div class="content-area">

        <!-- 1. DASHBOARD PAGE -->
        <div id="dashboardPage" class="page active">
            <h2>DASHBOARD OVERVIEW</h2>
            <div class="dashboard">
                <div class="card profit-card">
                    <h3>Total Revenue & Profit</h3>
                    <p>Total Revenue: ₹<span id="totRevenue">0</span></p>
                    <p>Total Profit: <span class="text-green">₹<span id="totProfit">0</span></span></p>
                </div>
                <div class="card">
                    <h3>BEBI Platform</h3>
                    <p>Revenue: ₹<span id="bebiRev">0</span> | Profit: <span class="text-green">₹<span id="bebiProf">0</span></span></p>
                </div>
                <div class="card">
                    <h3>LEDI Platform</h3>
                    <p>Revenue: ₹<span id="lediRev">0</span> | Profit: <span class="text-green">₹<span id="lediProf">0</span></span></p>
                </div>
                <div class="card" style="border-left-color: var(--purple); background: #1f122b;">
                    <h3>Anu's Account</h3>
                    <p style="font-size: 18px;" class="text-purple">₹<span id="anuTotal">0</span></p>
                </div>
            </div>

            <h3>Active Ongoing Works</h3>
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>WhatsApp</th>
                            <th>Platform</th>
                            <th>Delivery</th>
                            <th>Revenue</th>
                            <th>Profit</th>
                            <th>Anu's Share</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody id="activeCustomerTable"></tbody>
                </table>
            </div>
        </div>

        <!-- 2. ADD CUSTOMER PAGE -->
        <div id="customerPage" class="page">
            <div class="form-box">
                <h2>Add New Customer</h2>
                <div class="form-group"><label>Customer Name</label><input type="text" id="custName"></div>
                <div class="form-group"><label>WhatsApp Number</label><input type="text" id="custPhone" placeholder="919876543210"></div>
                <div class="form-group"><label>Platform</label><select id="platform"><option value="BEBI">BEBI</option><option value="LEDI">LEDI</option></select></div>
                <div class="form-group"><label>Delivery Date</label><input type="date" id="delDate"></div>
                <div class="form-group"><label>Total Price</label><input type="number" id="totPrice" oninput="calculatePreview()"></div>
                <div class="form-group"><label>Advance Amount</label><input type="number" id="advAmount"></div>
                <div class="form-group"><label>Total Expense</label><input type="number" id="totExpense" oninput="calculatePreview()"></div>
                <div class="form-group"><label>Stitched By (Employee)</label><select id="stitchEmp"></select></div>
                <div class="form-group"><label>Stitching Amount</label><input type="number" id="stitchAmount"></div>
                
                <div style="background: var(--bg-main); padding: 10px; border-radius: 8px; margin-bottom: 15px; border: 1px dashed var(--blue);">
                    <p>Preview Profit: <span class="text-green">₹<span id="calcProfit">0</span></span></p>
                    <p>Anu's Share: <span class="text-purple">₹<span id="calcAnu">0</span></span></p>
                </div>
                <button class="btn-primary" onclick="addCustomer()">Save Customer</button>
            </div>
        </div>

        <!-- 3. ADD ITEM PAGE -->
        <div id="itemPage" class="page">
            <div class="form-box">
                <h2>Add Item (Max 5MB Image)</h2>
                <div class="form-group"><label>Item Name</label><input type="text" id="itemName"></div>
                <div class="form-group"><label>Item Price</label><input type="number" id="itemPrice"></div>
                <div class="form-group"><label>Upload Image (Max 5MB)</label><input type="file" id="itemImage" accept="image/*"></div>
                <button class="btn-primary" onclick="addItem()">Save Item</button>
            </div>
            <h3>Item List</h3>
            <div class="table-responsive">
                <table>
                    <thead><tr><th>Image</th><th>Name</th><th>Price</th><th>Action</th></tr></thead>
                    <tbody id="itemTableBody"></tbody>
                </table>
            </div>
        </div>

        <!-- 4. ADD EMPLOYEE PAGE -->
        <div id="employeePage" class="page">
            <div class="form-box">
                <h2>Manage Employees</h2>
                <div class="form-group"><label>Employee Name</label><input type="text" id="empName"></div>
                <button class="btn-primary" onclick="addEmployee()">Save Employee</button>
            </div>
            <h3>Employee List</h3>
            <div class="table-responsive">
                <table>
                    <thead><tr><th>Name</th><th>Action</th></tr></thead>
                    <tbody id="employeeTableBody"></tbody>
                </table>
            </div>
        </div>

        <!-- 5. COMPLETED WORKS -->
        <div id="completedPage" class="page">
            <h2>Completed Works</h2>
            <div class="table-responsive">
                <table>
                    <thead><tr><th>Name</th><th>Platform</th><th>Delivery</th><th>Revenue</th><th>Profit</th><th>Anu's Share</th><th>Action</th></tr></thead>
                    <tbody id="completedCustomerTable"></tbody>
                </table>
            </div>
        </div>

        <!-- 6. DATA ANALYTICS PAGE -->
        <div id="analyticsPage" class="page">
            <h2>Data Analytics by Date</h2>
            <div class="form-box" style="margin-bottom: 15px;">
                <div class="form-group"><label>Select Date</label><input type="date" id="filterDate" onchange="filterAnalytics()"></div>
            </div>
            <h3>Filtered Report</h3>
            <div class="table-responsive">
                <table>
                    <thead><tr><th>Name</th><th>Platform</th><th>Date</th><th>Revenue</th><th>Profit</th><th>Expense</th></tr></thead>
                    <tbody id="analyticsTableBody"></tbody>
                </table>
            </div>
        </div>

    </div>
</div>

<!-- Firebase SDKs -->
<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getFirestore, collection, addDoc, doc, updateDoc, deleteDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "YOUR_API_KEY",
        authDomain: "YOUR_AUTH_DOMAIN",
        projectId: "YOUR_PROJECT_ID",
        storageBucket: "YOUR_STORAGE_BUCKET",
        messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
        appId: "YOUR_APP_ID"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    let allCustomersCache = [];

    window.toggleMenu = function() {
        let menu = document.getElementById('dropdownMenu');
        menu.style.display = menu.style.display === 'block' ? 'none' : 'block';
    }

    window.switchPage = function(pageId) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.getElementById(pageId).classList.add('active');
        document.getElementById('dropdownMenu').style.display = 'none';
    }

    window.addEmployee = async function() {
        const name = document.getElementById('empName').value;
        if(!name) return alert('Enter name!');
        await addDoc(collection(db, "employees"), { name });
        document.getElementById('empName').value = '';
        alert('Employee Saved!');
    }

    window.deleteEmployee = async function(id) {
        if(confirm('Delete?')) await deleteDoc(doc(db, "employees", id));
    }

    window.addItem = async function() {
        const name = document.getElementById('itemName').value;
        const price = document.getElementById('itemPrice').value;
        const fileInput = document.getElementById('itemImage');
        
        if(!name || !price) return alert('Fill fields!');
        
        if(fileInput.files.length > 0) {
            let file = fileInput.files[0];
            if(file.size > 5 * 1024 * 1024) return alert('Image size must be less than 5MB!');
            
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async function() {
                await addDoc(collection(db, "items"), { name, price, imageUrl: reader.result });
                alert('Item Saved!');
                document.getElementById('itemName').value = '';
                document.getElementById('itemPrice').value = '';
                document.getElementById('itemImage').value = '';
            };
            return;
        }

        await addDoc(collection(db, "items"), { name, price, imageUrl: "" });
        alert('Item Saved!');
    }

    window.deleteItem = async function(id) {
        await deleteDoc(doc(db, "items", id));
    }

    window.calculatePreview = function() {
        const price = parseFloat(document.getElementById('totPrice').value) || 0;
        const expense = parseFloat(document.getElementById('totExpense').value) || 0;
        let rawProfit = price - expense;
        let anuShare = rawProfit > 300 ? 300 : (rawProfit > 0 ? rawProfit : 0);
        let finalProfit = rawProfit > 300 ? rawProfit - 300 : 0;

        document.getElementById('calcProfit').innerText = finalProfit;
        document.getElementById('calcAnu').innerText = anuShare;
    }

    window.addCustomer = async function() {
        const name = document.getElementById('custName').value;
        const phone = document.getElementById('custPhone').value;
        const platform = document.getElementById('platform').value;
        const delDate = document.getElementById('delDate').value;
        const totPrice = parseFloat(document.getElementById('totPrice').value) || 0;
        const advAmount = parseFloat(document.getElementById('advAmount').value) || 0;
        const totExpense = parseFloat(document.getElementById('totExpense').value) || 0;
        const stitchEmp = document.getElementById('stitchEmp').value;
        const stitchAmount = parseFloat(document.getElementById('stitchAmount').value) || 0;

        const rawProfit = totPrice - totExpense;
        let anuShare = rawProfit > 300 ? 300 : (rawProfit > 0 ? rawProfit : 0);
        let finalProfit = rawProfit > 300 ? rawProfit - 300 : 0;

        await addDoc(collection(db, "customers"), {
            name, phone, platform, delDate, totPrice, advAmount, totExpense, stitchEmp, stitchAmount,
            profit: finalProfit, anuAmount: anuShare, revenue: totPrice, status: 'ongoing'
        });

        alert('Customer Saved!');
        switchPage('dashboardPage');
    }

    window.markCompleted = async function(id) {
        await updateDoc(doc(db, "customers", id), { status: 'completed' });
    }

    window.deleteCust = async function(id) {
        if(confirm('Delete?')) await deleteDoc(doc(db, "customers", id));
    }

    window.filterAnalytics = function() {
        const selectedDate = document.getElementById('filterDate').value;
        let tbody = document.getElementById('analyticsTableBody');
        tbody.innerHTML = '';
        
        allCustomersCache.forEach(data => {
            if(!selectedDate || data.delDate === selectedDate) {
                tbody.innerHTML += `
                    <tr>
                        <td>${data.name}</td>
                        <td>${data.platform}</td>
                        <td>${data.delDate}</td>
                        <td>₹${data.revenue}</td>
                        <td class="text-green">₹${data.profit}</td>
                        <td class="text-red">₹${data.totExpense}</td>
                    </tr>
                `;
            }
        });
    }

    onSnapshot(collection(db, "employees"), (snapshot) => {
        let select = document.getElementById('stitchEmp');
        let empTable = document.getElementById('employeeTableBody');
        select.innerHTML = ''; empTable.innerHTML = '';
        snapshot.forEach(docSnap => {
            let emp = docSnap.data();
            select.innerHTML += `<option value="${emp.name}">${emp.name}</option>`;
            empTable.innerHTML += `<tr><td>${emp.name}</td><td><button onclick="deleteEmployee('${docSnap.id}')" style="background:var(--red); color:white; border:none; padding:4px 8px; border-radius:4px; cursor:pointer;">Delete</button></td></tr>`;
        });
    });

    onSnapshot(collection(db, "items"), (snapshot) => {
        let itemTable = document.getElementById('itemTableBody');
        itemTable.innerHTML = '';
        snapshot.forEach(docSnap => {
            let item = docSnap.data();
            itemTable.innerHTML += `
                <tr>
                    <td>${item.imageUrl ? `<img src="${item.imageUrl}" width="35" height="35" style="border-radius:4px; object-fit:cover;">` : 'No Img'}</td>
                    <td>${item.name}</td>
                    <td>₹${item.price}</td>
                    <td><button onclick="deleteItem('${docSnap.id}')" style="background:var(--red); color:white; border:none; padding:4px 8px; border-radius:4px; cursor:pointer;">Delete</button></td>
                </tr>
            `;
        });
    });

    onSnapshot(collection(db, "customers"), (snapshot) => {
        let activeTable = document.getElementById('activeCustomerTable');
        let completedTable = document.getElementById('completedCustomerTable');
        activeTable.innerHTML = ''; completedTable.innerHTML = '';
        allCustomersCache = [];

        let totRev = 0, totProf = 0, anuTot = 0, bebiRev = 0, bebiProf = 0, lediRev = 0, lediProf = 0;

        snapshot.forEach(docSnap => {
            let data = docSnap.data();
            let id = docSnap.id;
            allCustomersCache.push(data);

            totRev += data.revenue || 0;
            totProf += data.profit || 0;
            anuTot += data.anuAmount || 0;

            if(data.platform === 'BEBI') { bebiRev += data.revenue || 0; bebiProf += data.profit || 0; }
            else if(data.platform === 'LEDI') { lediRev += data.revenue || 0; lediProf += data.profit || 0; }

            let waLink = data.phone ? `https://wa.me/${data.phone.replace(/[^0-9]/g, '')}` : '#';

            let row = `
                <tr>
                    <td>${data.name}</td>
                    ${data.status === 'ongoing' ? `<td><a href="${waLink}" target="_blank" class="whatsapp-link">💬 ${data.phone || ''}</a></td>` : ''}
                    <td>${data.platform}</td>
                    <td>${data.delDate || ''}</td>
                    <td>₹${data.revenue}</td>
                    <td class="text-green">₹${data.profit}</td>
                    <td class="text-purple">₹${data.anuAmount}</td>
                    <td>
                        ${data.status === 'ongoing' ? `<button onclick="markCompleted('${id}')" style="background:var(--green); color:var(--bg-main); border:none; padding:4px 8px; border-radius:4px; cursor:pointer; font-weight:bold;">Done</button>` : ''}
                        <button onclick="deleteCust('${id}')" style="background:var(--red); color:white; border:none; padding:4px 8px; border-radius:4px; cursor:pointer;">Del</button>
                    </td>
                </tr>
            `;

            if(data.status === 'completed') completedTable.innerHTML += row;
            else activeTable.innerHTML += row;
        });

        document.getElementById('totRevenue').innerText = totRev;
        document.getElementById('totProfit').innerText = totProf;
        document.getElementById('anuTotal').innerText = anuTot;
        document.getElementById('bebiRev').innerText = bebiRev;
        document.getElementById('bebiProf').innerText = bebiProf;
        document.getElementById('lediRev').innerText = lediRev;
        document.getElementById('lediProf').innerText = lediProf;
        filterAnalytics();
    });
</script>

</body>
</html>
