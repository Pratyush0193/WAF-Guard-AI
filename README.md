# WAF-Guard-AI

## AI-Assisted Web Threat Detection and Filtering

WAF-Guard-AI is a local web application security project that demonstrates how incoming HTTP requests can be inspected and classified using a combination of rule-based detection and machine-learning-assisted analysis.

The application was configured and tested locally in a Windows environment using Python and Flask.

## How It Works

Incoming HTTP requests are analyzed before a security decision is made.

```text
Incoming HTTP Request
        |
        v
 Request Inspection
        |
        +----------------------+
        |                      |
        v                      v
 Signature Analysis       ML-Assisted Analysis
        |                      |
        +----------+-----------+
                   |
                   v
             Threat Decision
              /          \
             /            \
          Valid          Malicious
            |                |
            v                v
          Allow             Block

The rule-based layer identifies recognizable malicious patterns, while the ML-assisted layer provides an additional analysis path for suspicious or obfuscated input.

Main Features
Detection of common web attack patterns
SQL injection identification
Cross-Site Scripting (XSS) detection
Analysis of encoded and obfuscated input
Rule/signature-based request filtering
Machine-learning-assisted anomaly analysis
Local web interface for security testing
Flask-based request analysis endpoint
Security testing evidence and output screenshots
Technology Used
Python
Flask
Scikit-learn
NumPy
LightGBM
JavaScript
HTML5
CSS3
Local Testing

All security testing for this project was performed against the local application.

The application runs on:

http://127.0.0.1:5000

This keeps the demonstration inside the local lab environment.

Example Test Cases
1. Normal Request

A basic request can be used to verify that legitimate traffic is allowed.

GET / HTTP/1.1
Host: localhost

Expected result:

Valid
2. SQL Injection Detection

A SQL injection pattern can be submitted to the request-analysis endpoint.

GET /search?q=' OR '1'='1' HTTP/1.1
Host: localhost

Expected result:

Malicious / Blocked
3. XSS Detection

A request containing a script payload can be used to test the XSS detection rules.

GET /comment?text=<script>alert('XSS')</script> HTTP/1.1
Host: localhost

Expected result:

Malicious / Blocked
4. Encoded Input

Encoded attack input can also be passed to the analysis layer.

GET /search?q=%27%20OR%20%271%27%3D%271 HTTP/1.1
Host: localhost

The encoded request is analyzed to determine whether it represents suspicious traffic.

Request Analysis API

The project also provides a local request-analysis endpoint.

Example PowerShell request:

$body = @{
    user_request = "GET / HTTP/1.1"
    uri = "/"
    get_data = ""
    post_data = ""
} | ConvertTo-Json

Invoke-RestMethod `
    -Uri "http://127.0.0.1:5000/check_request" `
    -Method POST `
    -ContentType "application/json" `
    -Body $body

A normal request should return a valid/clear classification.

Suspicious requests can return a malicious classification or trigger the additional ML analysis path.

Project Evidence

Testing screenshots are stored in the project evidence directory.

The evidence includes:

Application/dashboard output
Normal request testing
SQL injection detection
XSS detection
Encoded-input analysis
Terminal/API testing results
Installation
1. Clone the Repository
git clone https://github.com/Pratyush0193/WAF-Guard-AI.git

Move into the project directory:

cd WAF-Guard-AI
2. Create and Activate the Virtual Environment

On Windows PowerShell:

python -m venv venv

Activate it:

.\venv\Scripts\Activate.ps1
3. Install Dependencies
pip install -r requirements.txt
4. Start the Application
python app.py

The Flask application should then be available at:

http://127.0.0.1:5000

Open the address in a browser to access the local interface.

Project Structure
WAF-Guard-AI/
│
├── app.py
├── requirements.txt
├── setup.py
├── README.md
├── LICENSE
│
├── src/
│   └── hybrid_waf/
│       ├── models/
│       ├── routes/
│       └── utils/
│
├── static/
│   ├── home.js
│   ├── script.js
│   └── styles.css
│
├── templates/
│   ├── index.html
│   └── home.html
│
├── project-evidence/
│   └── testing screenshots
│
└── output-screenshots/
Security Testing Approach

The project demonstrates a layered approach to web request filtering:

Receive an HTTP request.
Extract relevant request information.
Inspect the request for known attack signatures.
Perform additional analysis on suspicious or unusual input.
Produce a security classification.
Allow legitimate traffic or block malicious traffic.

This approach demonstrates how traditional WAF rules can be combined with machine-learning techniques for additional threat analysis.

Important Note

This project is intended for local educational and security-testing purposes.

The attack examples included in the documentation should only be tested against systems that you own or are explicitly authorized to assess.

License

This project is distributed under the MIT License.


### Then save it

In your current PowerShell, **do not run `python app.py`**. Your terminal is currently free, as shown by:

```text
(venv) PS C:\Users\praty\Projects\Advanced-Web-Application-Firewall>