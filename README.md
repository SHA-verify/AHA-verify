<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>eCertificate Verification | Saudi Heart Association CPR</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #f4f6f9;
            color: #333;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }
        .top-bar {
            background-color: #006837;
            color: #fff;
            padding: 15px 30px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 4px solid #8dc63f;
        }
        .top-bar h1 {
            font-size: 18px;
            font-weight: 600;
            letter-spacing: 0.3px;
        }
        .top-bar span {
            font-size: 13px;
            opacity: 0.9;
        }
        .main-wrapper {
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            padding: 40px 15px;
        }
        .verify-card {
            background: #ffffff;
            width: 100%;
            max-width: 720px;
            border-radius: 6px;
            box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
            border: 1px solid #e1e8ed;
            overflow: hidden;
        }
        .card-header {
            background-color: #f8fafc;
            padding: 18px 25px;
            border-bottom: 1px solid #e1e8ed;
        }
        .card-header h2 {
            color: #006837;
            font-size: 19px;
            margin-bottom: 4px;
        }
        .card-header p {
            color: #64748b;
            font-size: 13px;
        }
        .card-body {
            padding: 25px;
        }
        .input-group {
            margin-bottom: 20px;
        }
        .input-group label {
            display: block;
            font-weight: 600;
            font-size: 14px;
            color: #1e293b;
            margin-bottom: 8px;
        }
        .search-box {
            display: flex;
            gap: 10px;
        }
        .search-box input {
            flex: 1;
            padding: 11px 15px;
            border: 1px solid #cbd5e1;
            border-radius: 4px;
            font-size: 15px;
            outline: none;
            transition: border-color 0.2s;
        }
        .search-box input:focus {
            border-color: #006837;
        }
        .search-box button {
            background-color: #006837;
            color: #fff;
            border: none;
            padding: 11px 28px;
            border-radius: 4px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
        }
        .search-box button:hover {
            background-color: #004d29;
        }
        .result-section {
            display: none;
            margin-top: 25px;
            border: 1px solid #d6e9c6;
            border-radius: 4px;
            overflow: hidden;
        }
        .status-banner {
            background-color: #dff0d8;
            color: #3c763d;
            padding: 12px 18px;
            font-weight: 600;
            font-size: 14px;
            border-bottom: 1px solid #d6e9c6;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            padding: 12px 18px;
            text-align: left;
            border-bottom: 1px solid #e2e8f0;
            font-size: 14px;
        }
        th {
            width: 38%;
            background-color: #f8fafc;
            color: #475569;
            font-weight: 600;
        }
        td {
            color: #0f172a;
            font-weight: 500;
        }
        .badge-valid {
            background-color: #dcfce7;
            color: #166534;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 12px;
            font-weight: 700;
        }
        .error-alert {
            display: none;
            margin-top: 20px;
            background-color: #fef2f2;
            color: #991b1b;
            border: 1px solid #fecaca;
            padding: 14px 18px;
            border-radius: 4px;
            font-size: 14px;
        }
        footer {
            text-align: center;
            padding: 15px;
            font-size: 12px;
            color: #64748b;
            border-top: 1px solid #e2e8f0;
            background: #fff;
        }
    </style>
</head>
<body>

    <div class="top-bar">
        <h1>eCertificate Verification Portal</h1>
        <span>CPR / BLS / ACLS / PALS / NRP</span>
    </div>

    <div class="main-wrapper">
        <div class="verify-card">
            <div class="card-header">
                <h2>Verify eCertificate</h2>
                <p>Enter the eCertificate ID printed on the certificate to verify its authenticity.</p>
            </div>
            <div class="card-body">
                <div class="input-group">
                    <label for="certInput">eCertificate ID *</label>
                    <div class="search-box">
                        <input type="text" id="certInput" placeholder="e.g. 25568309814">
                        <button onclick="verifyCert()">Verify</button>
                    </div>
                </div>

                <div id="errorBox" class="error-alert">
                    <strong>Invalid eCertificate ID:</strong> No matching record found. Please verify the number and try again.
                </div>

                <div id="resultBox" class="result-section">
                    <div class="status-banner">
                        ✔ Valid eCertificate Record Found
                    </div>
                    <table>
                        <tr>
                            <th>eCertificate ID</th>
                            <td id="resId"></td>
                        </tr>
                        <tr>
                            <th>Trainee Name</th>
                            <td id="resName"></td>
                        </tr>
                        <tr>
                            <th>Course Title</th>
                            <td id="resCourse"></td>
                        </tr>
                        <tr>
                            <th>Registration ID</th>
                            <td id="resReg"></td>
                        </tr>
                        <tr>
                            <th>Issue Date</th>
                            <td id="resIssue"></td>
                        </tr>
                        <tr>
                            <th>Expiration Date</th>
                            <td id="resExpiry"></td>
                        </tr>
                        <tr>
                            <th>Training Center</th>
                            <td id="resCenter"></td>
                        </tr>
                        <tr>
                            <th>Status</th>
                            <td><span class="badge-valid">VALID / ACTIVE</span></td>
                        </tr>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <footer>
        &copy; 2026 eCertificate Verification System. All Rights Reserved.
    </footer>

    <script>
        // قاعدة بيانات الشهادات (أضف بيانات كل متدرب جديد هنا)
        const certificatesDB = {
            "25568309814": {
                name: "AMR AHMED SOLIMAN AGWA",
                course: "SHA ACLS Provider",
                regId: "34487",
                issueDate: "2026-10-28",
                expiryDate: "2028-10-28",
                center: "PSMMC Training Center"
            },
            "25568309815": {
                name: "SULTAN RASHED SALEH",
                course: "SHA BLS Provider",
                regId: "34488",
                issueDate: "2024-12-01",
                expiryDate: "2026-12-01",
                center: "MedSkill Academy Training Center"
            }
        };

        function verifyCert(autoId = null) {
            const inputVal = (autoId || document.getElementById("certInput").value).trim();
            const resultBox = document.getElementById("resultBox");
            const errorBox = document.getElementById("errorBox");

            if (!inputVal) return;

            if (certificatesDB[inputVal]) {
                const cert = certificatesDB[inputVal];
                document.getElementById("resId").textContent = inputVal;
                document.getElementById("resName").textContent = cert.name;
                document.getElementById("resCourse").textContent = cert.course;
                document.getElementById("resReg").textContent = cert.regId;
                document.getElementById("resIssue").textContent = cert.issueDate;
                document.getElementById("resExpiry").textContent = cert.expiryDate;
                document.getElementById("resCenter").textContent = cert.center;

                errorBox.style.display = "none";
                resultBox.style.display = "block";
            } else {
                resultBox.style.display = "none";
                errorBox.style.display = "block";
            }
        }

        // التحقق التلقائي عند فتح الرابط من خلال رمز QR Code
        window.onload = function() {
            const urlParams = new URLSearchParams(window.location.search);
            const idFromUrl = urlParams.get('id');
            if (idFromUrl) {
                document.getElementById("certInput").value = idFromUrl;
                verifyCert(idFromUrl);
            }
        };
    </script>

</body>
</html>

