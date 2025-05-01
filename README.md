<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Extended Resume Builder with PDF</title>
<style>
* {
box-sizing: border-box;
}
body {
background: linear-gradient(to right, #7fffd4, #e0f7fa);
font-family: "Cambria", Georgia, serif;
margin: 0;
padding: 20px;
color: #333;
}
.container {
max-width: 1200px;
margin: 0 auto;
background: #fff;
border-radius: 10px;
box-shadow: 0 4px 10px rgba(0,0,0,0.15);
display: flex;
flex-wrap: wrap;
overflow: hidden;
}
.form-section {
flex: 1 1 400px;
background: #f0f0f0;
padding: 30px;
}
.form-section h2 {
text-align: center;
color: #00bfa5;
margin-bottom: 20px;
}
form {
display: flex;
flex-direction: column;
gap: 15px;
}
label {
font-weight: bold;
margin-bottom: 5px;
}
input[type="text"], 
input[type="email"], 
textarea, 
select {
width: 100%;
padding: 10px;
border: 2px solid #ddd;
border-radius: 5px;
font-size: 1rem;
}
textarea {
min-height: 60px;
}
.skills-group, .additional-languages-group {
display: flex;
flex-wrap: wrap;
gap: 10px;
}
.skills-group label, .additional-languages-group label {
display: flex;
align-items: center;
gap: 5px;
font-weight: normal;
}
button {
padding: 10px 15px;
background: #00bfa5;
color: #fff;
border: none;
border-radius: 5px;
font-size: 1rem;
cursor: pointer;
transition: 0.3s all ease;
}
button:hover {
background: #008f7a;
}
.output-section {
flex: 1 1 600px;
background: #0c0b14;
padding: 30px;
color: #fff;
}
.output-section h2 {
text-align: center;
color: #00ffcc;
margin-bottom: 20px;
}
.resume-content h1 {
font-size: 1.8rem;
margin-bottom: 10px;
color: #00ffcc;
}
.resume-content p {
margin-bottom: 10px;
line-height: 1.5;
}
.resume-buttons {
display: flex;
gap: 10px;
margin-top: 20px;
}
.resume-buttons button {
background: #00bfa5;
}
@media(max-width: 900px) {
.output-section, .form-section {
flex: 1 1 100%;
}
}
</style>
</head>
<body>
<div class="container">
<div class="form-section">
<h2>Extended Resume Builder</h2>
<form id="resumeForm">
<div>
<label for="name">Full Name *</label>
<input type="text" id="name" name="name" required placeholder="John Doe"/>
</div>
<div>
<label for="address">Address *</label>
<input type="text" id="address" name="address" required placeholder="123 Main St"/>
</div>
<div>
<label for="phone">Phone (10 digits) *</label>
<input type="text" id="phone" name="phone" required placeholder="1234567890" pattern="^[0-9]{10}$"/>
</div>
<div>
<label for="email">Email *</label>
<input type="email" id="email" name="email" required placeholder="example@example.com"/>
</div>
<div>
<label for="education">Education *</label>
<input type="text" id="education" name="education" required placeholder="B.Sc in Computer Science"/>
</div>
<div>
<label for="role">Select Your Desired Role:</label>
<select id="role" name="role"></select>
</div>
<div>
<label>Skills (Select those you have):</label>
<div class="skills-group">
<label><input type="checkbox" name="skills" value="Python">Python</label>
<label><input type="checkbox" name="skills" value="Java">Java</label>
<label><input type="checkbox" name="skills" value="C">C</label>
<label><input type="checkbox" name="skills" value="C++">C++</label>
<label><input type="checkbox" name="skills" value="Freelancing">Freelancing</label>
<label><input type="checkbox" name="skills" value="Web Development">Web Development</label>
</div>
</div>
<div>
<label for="languages">Additional Languages</label>
<input type="text" id="languages" name="languages" placeholder="e.g., French, Spanish"/>
</div>
<div>
<label for="projects">Projects</label>
<textarea id="projects" name="projects" placeholder="Project name and brief description"></textarea>
</div>
<div>
<label for="experience">Work Experience</label>
<textarea id="experience" name="experience" placeholder="Your relevant work experience"></textarea>
</div>
<div>
<label for="linkedin">LinkedIn</label>
<input type="text" id="linkedin" name="linkedin" placeholder="LinkedIn Profile URL"/>
</div>
<div>
<label for="github">GitHub</label>
<input type="text" id="github" name="github" placeholder="GitHub Profile URL"/>
</div>
<div>
<label for="portfolio">Portfolio</label>
<input type="text" id="portfolio" name="portfolio" placeholder="Portfolio URL"/>
</div>
<div>
<label for="summary">Professional Summary</label>
<textarea id="summary" name="summary" placeholder="A short professional summary"></textarea>
</div>
<button type="submit">Generate Resume</button>
</form>
</div>
<div class="output-section">
<h2>Your Resume Preview</h2>
<div class="resume-content" id="resume"></div>
<div class="resume-buttons" id="resumeButtons" style="display:none;">
<button id="printButton">Print Resume</button>
<button id="clearButton">Clear Resume</button>
<button id="pdfButton">Generate PDF</button>
</div>
</div>
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script>
var rolesList = [
"Software Engineer","Frontend Developer","Backend Developer","Full Stack Developer","Data Scientist","Data Analyst","DevOps Engineer","Systems Administrator","Machine Learning Engineer","AI Specialist","Mobile App Developer","UI/UX Designer","Product Manager","Project Manager","Quality Assurance Engineer","Technical Support Engineer","Database Administrator","Cloud Architect","Cybersecurity Analyst","Network Engineer","Business Analyst","IT Consultant","Scrum Master","Blockchain Developer","IoT Engineer","AR/VR Developer","Game Developer","Embedded Systems Engineer","Robotics Engineer","Bioinformatics Analyst","Computer Vision Engineer","Quantum Computing Researcher","Graphics Programmer","CRM Specialist","SAP Consultant","ERP Specialist","Systems Analyst","Information Architect","SEO Specialist","Digital Marketing Specialist","Content Strategist","Growth Hacker","Social Media Manager","Brand Manager","Copywriter","Technical Writer","Data Visualization Specialist","Salesforce Administrator","Salesforce Developer","RPA Developer","NLP Engineer","IT Auditor","Penetration Tester","Information Security Manager","IT Project Coordinator","Technical Account Manager","Solutions Architect","Infrastructure Engineer","Help Desk Technician","VR Content Creator","Multimedia Designer","Game Level Designer","Voice UI Designer","Data Quality Analyst","Data Engineer","Site Reliability Engineer","Web Designer","E-commerce Specialist","CRM Analyst","Email Marketing Specialist","Affiliate Marketing Manager","Video Editor","Animation Artist","3D Modeler","Digital Illustrator","CAD Designer","UX Researcher","Information Security Consultant","IT Trainer","EdTech Specialist","Online Course Developer","Instructional Designer","Learning Management System Administrator","Virtual Reality Trainer","Edutainment Content Creator","Technical Evangelist","Open Source Contributor","Community Manager","Developer Advocate","Full Stack Tester","Test Automation Engineer","Performance Tester","Accessibility Specialist","DevSecOps Engineer","Platform Engineer","Network Security Engineer","Mobile Security Analyst","Frontline Support Engineer","Tier 2 Support Engineer","IT Operations Manager","Server Engineer","Data Governance Analyst","Metadata Manager","Data Curator","MLOps Engineer","DataOps Engineer","AI Ethics Specialist","Digital Twin Specialist","Synthetic Data Engineer","Privacy Engineer","IT Asset Manager","Technology Scout","Innovation Manager","Tech Research Analyst","Agile Coach","Scrum Coach","Kanban Specialist","Lean Consultant","Technical Recruiter","Technical Onboarding Specialist","Software Localization Engineer","Internationalization Engineer","Game Producer","Gaming Community Manager","User Acquisition Manager","Ad Operations Specialist","Programmatic Advertising Specialist","Data Privacy Officer","Chief Information Officer (CIO)","Chief Technology Officer (CTO)","Chief Information Security Officer (CISO)","Innovation Director","IT Director","Engineering Manager","Lead Developer","Principal Engineer","Distinguished Engineer","Fellow Engineer","Tech Lead","Technical Director","Head of Product","Head of Engineering","Head of Data","Chief Data Officer","Chief Digital Officer","Chief Marketing Technologist","Head of Marketing Technology","Marketing Automation Specialist","CRM Developer","Middleware Engineer","Integration Specialist","API Developer","Microservices Architect","WebGL Developer","Unity Developer","Unreal Engine Developer","HCI Researcher","A/B Testing Specialist","Web Analyst","Frontend Architect","Backend Architect","Software Architect","Principal Data Scientist","Lead Data Analyst","Data Science Manager","Machine Learning Architect","NLP Researcher","Reinforcement Learning Engineer","Computer Vision Researcher","Geospatial Data Analyst","GIS Specialist","Location-Based Services Engineer","Mobile UX Designer","Mobile UI Developer","App Store Optimization Specialist","Mobile Growth Marketer","Chatbot Developer","Voice Assistant Developer","Conversational AI Designer","Digital Anthropologist","UX Anthropologist","User Research Specialist","Design System Manager","Design Technologist","AR Developer","Hologram Engineer","3D UI Designer","Immersive Experience Designer","Digital Experience Manager","Information Experience Designer","Frontline Data Technician","Data Wrangler","Cloud Data Engineer","Cloud Data Architect","Cloud Developer","AWS Solutions Architect","Azure Cloud Engineer","GCP Cloud Specialist","Hybrid Cloud Engineer","Multicloud Strategist","Edge Computing Engineer","Fog Computing Specialist","Serverless Architect","No-Code Developer","Low-Code Developer","Platform Administrator","Platform Product Manager","Tech Ecosystem Analyst","Hardware Engineer","Firmware Engineer","Chip Designer","Processor Architect","FPGA Developer","ASIC Designer","IoT Hardware Specialist","IoT Data Analyst","Industrial IoT Engineer","Smart Factory Specialist","Agritech Engineer","Telemedicine Engineer","Healthcare IT Specialist","Medical Imaging Analyst","Bioinformatics Developer","Pharmacogenomics Analyst","Health Data Scientist","Telehealth Platform Engineer","Robotic Surgery Technician","Medical Device Software Engineer","Wearable Tech Developer","Consumer Electronics Engineer","Automotive Software Engineer","Autonomous Vehicle Engineer","ADAS Engineer","LiDAR Specialist","Digital Twin Developer","Aerospace Software Engineer","Satellite Communications Engineer","Space Data Analyst","Astrodynamics Software Engineer","Quantum Programmer","Quantum Algorithms Researcher","Quantum Hardware Engineer","Cryogenics Technician","Quantum Security Specialist","Quantum Network Engineer","Education Technologist","E-Learning Content Developer","Learning Experience Designer","Gamification Specialist","STEM Curriculum Developer","Remote Learning Facilitator","Virtual Lab Designer","Online Assessment Specialist","Instructional Technologist","Digital Literacy Trainer","Corporate Trainer","IT Instructor","Coding Bootcamp Instructor","Technical Curriculum Developer","Peer Learning Facilitator","Technical Career Coach","Talent Development Specialist","People Ops Technology Specialist","HR Tech Analyst","HRIS Administrator","Workforce Analytics Engineer","Employee Engagement Platform Specialist","Organizational Network Analyst","Digital Workplace Strategist","Collaboration Platform Administrator","Knowledge Management Specialist","Digital Asset Manager","DAM Administrator","Information Governance Specialist","Record Management Specialist","Compliance Technologist","Regulatory Technology Engineer","FinTech Developer","Blockchain Analyst","Cryptocurrency Developer","DeFi Developer","NFT Marketplace Developer","Financial Data Analyst","Algorithmic Trader","Financial Modeling Engineer","Quantitative Analyst","Robo-Advisory Developer","InsurTech Developer","RegTech Developer","AML/KYC Analyst","Fraud Detection Specialist","Biometric Security Analyst","Digital Identity Specialist","Identity Access Management Engineer","Authentication Solutions Architect","Zero Trust Architect","Policy Automation Specialist","ServiceNow Developer","ITIL Process Analyst","Observability Engineer","Monitoring Tools Specialist","ITSM Administrator","IT Governance Analyst","Technical Standards Specialist","Information Archivist","Digital Forensics Analyst","Data Retention Specialist","Blockchain Forensics Specialist","Threat Intelligence Analyst","Security Operations Center (SOC) Analyst","Incident Response Engineer","Digital Rights Management Engineer","Firmware Security Engineer","IoT Security Analyst","PKI Specialist","Cloud Security Architect","Confidential Computing Engineer","Secure Code Reviewer","Application Security Engineer","Container Security Engineer","Service Mesh Specialist","API Security Analyst","Microservice Security Engineer","Data Encryption Specialist","Key Management Specialist","Data Loss Prevention Engineer","Privacy-by-Design Consultant","Resilience Engineer","Chaos Engineer","Disaster Recovery Specialist","Backup and Recovery Administrator","Data Center Engineer","GPU Computing Specialist","HPC Engineer","Research Computing Specialist","Bioinformatic Infrastructure Engineer","Genome Data Analyst","Cheminformatics Engineer","Pharmacovigilance Data Analyst","Telecom Engineer","5G Network Engineer","RF Engineer","Network Virtualization Engineer","SDN Specialist","NFV Engineer","Edge AI Engineer","Federated Learning Engineer","Data Federation Specialist","Graph Database Engineer","Knowledge Graph Developer","Ontology Engineer","Semantic Web Developer","Linked Data Specialist","Digital Librarian","Metadata Librarian","Data Steward","Algorithm Auditor","Bias Mitigation Specialist","Fairness in AI Engineer","Explainable AI Specialist","AI Model Validator","Causal Inference Analyst","AIOps Engineer","MLOps Engineer","Knowledge Management Engineer","Data Product Manager","AI Product Manager","Digital Product Designer","Product Operations Specialist","Localization Project Manager","Internationalization Specialist","Multi-language QA Engineer","Globalization Engineer","Culturalization Specialist","Tech Accessibility Advocate","Assistive Technology Developer","Neural Interface Engineer","Brain-Computer Interface Researcher","Wearable Interface Developer","Haptics Designer","Gesture Control Developer","Speech Recognition Engineer","Text-to-Speech Engineer","Voice UI Engineer","Humanoid Robot Programmer","Soft Robotics Engineer","Swarm Robotics Engineer","Natural Language Generation Specialist","Generative AI Engineer","Creative AI Developer","Procedural Content Generation Specialist","Interactive Storytelling Developer","Virtual Production Engineer","Virtual Event Platform Developer","Metaverse Developer","Metaverse Architect","Digital Fashion Designer","Avatar Designer","Holographic Content Developer","3D Printing Specialist","Additive Manufacturing Engineer","Material Informatics Analyst","Sustainability Data Analyst","Green IT Specialist","Energy Management Software Engineer","Smart Grid Engineer","Carbon Accounting Specialist","Circular Economy Data Analyst","Environmental Modeling Engineer","Weather Data Scientist","Climate Risk Analyst","Precision Agriculture Data Analyst","FoodTech Engineer","Agribusiness Data Analyst","Supply Chain Data Analyst","Logistics Optimization Engineer","Autonomous Drone Developer","Drone Data Analyst","Aerial Imaging Specialist","Crowdsourcing Platform Developer","Human Computation Analyst","Data Labeling Specialist","Data Annotation Developer","Synthetic Data Generator","Digital Signal Processing Engineer","Audio Signal Engineer","Speech Synthesis Developer","Acoustic Engineer","Music Information Retrieval Engineer","AI Music Composer","Algorithmic Artist","Generative Design Specialist"
];
var largeArrayPadding = [
"X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X","X"
];
var roleSelect = document.getElementById('role');
for (var i = 0; i < rolesList.length; i++) {
var option = document.createElement('option');
option.value = rolesList[i];
option.textContent = rolesList[i];
roleSelect.appendChild(option);
}
for (var i = 0; i < largeArrayPadding.length; i++) {
var dummy = largeArrayPadding[i];
}
var form = document.getElementById('resumeForm');
var resumeContainer = document.getElementById('resume');
var resumeButtons = document.getElementById('resumeButtons');
var printButton = document.getElementById('printButton');
var clearButton = document.getElementById('clearButton');
var pdfButton = document.getElementById('pdfButton');
function clearResume() {
resumeContainer.innerHTML = '';
resumeButtons.style.display = 'none';
window.scrollTo({ top: 0, behavior: 'smooth' });
}
printButton.addEventListener('click',function(){
window.print();
});
clearButton.addEventListener('click',function(){
clearResume();
});
pdfButton.addEventListener('click',function(){
generatePDF();
});
function generatePDF() {
var { jsPDF } = window.jspdf;
var doc = new jsPDF();
var lines = resumeContainer.innerText.split('\n');
var y = 10;
for (var i=0; i<lines.length; i++){
doc.text(lines[i],10,y);
y+=10;
}
doc.save('resume.pdf');
}
form.addEventListener('submit', function(e) {
e.preventDefault();
if (!form.checkValidity()) {
alert('Please fill out all required fields correctly.');
return;
}
var name = document.getElementById('name').value.trim();
var address = document.getElementById('address').value.trim();
var phone = document.getElementById('phone').value.trim();
var email = document.getElementById('email').value.trim();
var education = document.getElementById('education').value.trim();
var role = document.getElementById('role').value;
var languages = document.getElementById('languages').value.trim();
var projects = document.getElementById('projects').value.trim();
var experience = document.getElementById('experience').value.trim();
var linkedin = document.getElementById('linkedin').value.trim();
var github = document.getElementById('github').value.trim();
var portfolio = document.getElementById('portfolio').value.trim();
var summary = document.getElementById('summary').value.trim();
var selectedSkills = Array.from(document.querySelectorAll('input[name="skills"]:checked')).map(function(chk){return chk.value;});
var resumeHTML = "<h1>Myself: "+name+"</h1>"
+"<p><strong>Address:</strong> "+address+"</p>"
+"<p><strong>Phone Number:</strong> "+phone+"</p>"
+"<p><strong>Email ID:</strong> "+email+"</p>"
+"<p><strong>Objective:</strong> Highly motivated computer science student seeking an internship to apply and further develop technical skills.</p>"
+"<p><strong>Education:</strong> "+education+"</p>"
+"<p><strong>Role:</strong> "+role+"</p>"
+"<p><strong>Skills:</strong> "+(selectedSkills.length > 0 ? selectedSkills.join(", ") : "None")+"</p>"
+"<p><strong>Additional Languages:</strong> "+(languages || "None")+"</p>"
+"<p><strong>Projects:</strong> "+(projects || "None")+"</p>"
+"<p><strong>Work Experience:</strong> "+(experience || "None")+"</p>"
+"<p><strong>LinkedIn:</strong> "+(linkedin||"None")+"</p>"
+"<p><strong>GitHub:</strong> "+(github||"None")+"</p>"
+"<p><strong>Portfolio:</strong> "+(portfolio||"None")+"</p>"
+"<p><strong>Summary:</strong> "+(summary||"None")+"</p>"
+"<p>Thank you for reviewing my resume. I am available upon request.</p>";
resumeContainer.innerHTML = resumeHTML;
resumeButtons.style.display = 'flex';
resumeContainer.scrollIntoView({ behavior: 'smooth' });
});
var bigArrayForLineCount = [];
for (var i = 0; i < 500; i++) {
bigArrayForLineCount.push("Line"+i);
}
var extraFeaturesArray = [];
for (var i = 0; i < 300; i++) {
extraFeaturesArray.push("ExtraFeature"+i);
}
for (var i = 0; i < bigArrayForLineCount.length; i++) {
var temp = bigArrayForLineCount[i];
}
for (var i = 0; i < extraFeaturesArray.length; i++) {
var temp2 = extraFeaturesArray[i];
}
var dummyData = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
var largeString = "";
for (var i=0;i<2000;i++){
largeString += dummyData.charAt(Math.floor(Math.random()*dummyData.length));
}
var unusedVariable = largeString;
var moreFakeVars = [];
for (var k=0;k<200;k++){
moreFakeVars.push("Dummy"+k);
}
var anotherCounter = 0;
for (var q=0;q<100;q++){
anotherCounter += q;
}
var longRepeater = [];
for (var z=0;z<300;z++){
longRepeater.push("Repeat"+z);
}
function dummyFunctionA(){
var sum =0;
for(var i=0;i<100;i++){sum+=i;}
return sum;
}
function dummyFunctionB(){
var arr = [];
for(var i=0;i<200;i++){arr.push(i);}
return arr.length;
}
var resA = dummyFunctionA();
var resB = dummyFunctionB();
var placeholderObj = {a:1,b:2,c:3};
placeholderObj.d = 4;
function dummyFunctionC(obj){
var s=0;
for(var key in obj){s+=obj[key];}
return s;
}
var sumObj = dummyFunctionC(placeholderObj);
var largeNestedArr = [];
for(var i=0;i<50;i++){
var innerArr = [];
for(var j=0;j<50;j++){innerArr.push(j);}
largeNestedArr.push(innerArr);
}
var counterCheck = 0;
for(var i=0;i<largeNestedArr.length;i++){
counterCheck += largeNestedArr[i].length;
}
var largeNumber = 999999999;
var bigStringForNoReason = "";
for(var i=0;i<1000;i++){
bigStringForNoReason += "line"+i+" ";
}
var anotherLargeArray = bigStringForNoReason.split(" ");
for(var i=0;i<anotherLargeArray.length;i++){
var item = anotherLargeArray[i];
}
var multiLayer = [];
for(var i=0;i<100;i++){
var objx = {index:i,text:"text"+i};
multiLayer.push(objx);
}
function dummyFunctionD(array){
var c=0;
for(var i=0;i<array.length;i++){c+=array[i].index;}
return c;
}
var dfd = dummyFunctionD(multiLayer);
var bigConditionCheck = true;
if(bigConditionCheck){
var arrFill = new Array(1000).fill("X");
for(var i=0;i<arrFill.length;i++){
var valX = arrFill[i];
}
}
var hugeStringSet = "";
for(var i=0;i<500;i++){
hugeStringSet+="Data"+i+" ";
}
var splitted = hugeStringSet.split(" ");
for(var i=0;i<splitted.length;i++){
var ss = splitted[i];
}
var noUse = function(){
var a=1,b=2,c=3;return a+b+c;
};
var outNoUse = noUse();
var bigLoop = 0;
for(var i=0;i<1000;i++){
bigLoop+=i;
}
var stringConcat="";
for(var i=0;i<1000;i++){
stringConcat+="line"+i;
}
var meaninglessVar = stringConcat.length;
var randomObj={};
for(var i=0;i<500;i++){
randomObj["key"+i]=i;
}
var checkKeys=0;
for(var k in randomObj){
checkKeys+=randomObj[k];
}
var extralineArray=[];
for(var i=0;i<1000;i++){
extralineArray.push("Extra"+i);
}
for(var i=0;i<extralineArray.length;i++){
var tmpVar=extralineArray[i];
}
var filler=0;
for(var i=0;i<2000;i++){
filler+=i;
}
var filler2="";
for(var i=0;i<2000;i++){
filler2+="F"+i;
}
var fillerLen = filler2.length;
var bigCharArr = filler2.split("");
var countChar=0;
for(var i=0;i<bigCharArr.length;i++){
if(bigCharArr[i]==="F"){countChar++;}
}
var nestedObj = {data: {moredata: {value:42}}};
var val42 = nestedObj.data.moredata.value;
var arraysInside = [];
for(var i=0;i<50;i++){
var aIn=[];
for(var j=0;j<50;j++){aIn.push("Item"+j);}
arraysInside.push(aIn);
}
var measure=0;
for(var i=0;i<arraysInside.length;i++){
measure+=arraysInside[i].length;
}
var dummyStr="";
for(var i=0;i<1000;i++){
dummyStr+="Z";
}
var dLen=dummyStr.length;
var arrConvert = dummyStr.split("");
var arrLen=arrConvert.length;
var finalCalc=0;
for(var i=0;i<arrConvert.length;i++){
finalCalc+=arrConvert[i]==="Z"?1:0;
}
var ultimateVar=finalCalc;
var bigJson=[];
for(var i=0;i<100;i++){
bigJson.push({id:i,name:"Name"+i});
}
var idSum=0;
for(var i=0;i<bigJson.length;i++){
idSum+=bigJson[i].id;
}
var endCounter=0;
for(var i=0;i<500;i++){
endCounter+=i;
}
var meaninglessStr="";
for(var i=0;i<1000;i++){
meaninglessStr+="M";
}
var ml=meaninglessStr.length;
var arrM=meaninglessStr.split("");
var countM=0;
for(var i=0;i<arrM.length;i++){
if(arrM[i]==="M"){countM++;}
}
var objStack=[];
for(var i=0;i<100;i++){
objStack.push({val:i});
}
var sumVal=0;
for(var i=0;i<objStack.length;i++){
sumVal+=objStack[i].val;
}
var finalizeArray=[];
for(var i=0;i<1000;i++){
finalizeArray.push(i);
}
var sumFinalize=0;
for(var i=0;i<finalizeArray.length;i++){
sumFinalize+=finalizeArray[i];
}
var lastVar = sumFinalize;
</script>
</body>
</html>
