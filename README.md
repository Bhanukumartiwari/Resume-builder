# Resume-builder
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>Advanced Resume Builder</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
  <style>
    body{margin:0;font-family:Arial,Helvetica,sans-serif;background:#f5f5f5;color:#111}
    .container{display:grid;grid-template-columns:360px 1fr;gap:16px;max-width:1200px;margin:20px auto;padding:10px}
    .card{background:#fff;border-radius:8px;padding:16px;box-shadow:0 4px 10px rgba(0,0,0,.08)}
    label{font-weight:600;font-size:0.9rem;margin-top:12px;display:block}
    input,textarea,select{width:100%;padding:8px;margin-top:4px;border:1px solid #ccc;border-radius:6px}
    textarea{min-height:60px;resize:vertical}
    button{margin-top:10px;padding:8px 12px;border:none;border-radius:6px;cursor:pointer;background:#0073e6;color:#fff;font-weight:600}
    h2{margin:6px 0}
    .resume{background:#fff;padding:30px;max-width:800px;margin:auto;font-size:14px;line-height:1.5}
    /* ==== Templates ==== */
    .modern h1{font-size:22px;color:#0073e6;margin-bottom:4px}
    .modern h2{font-size:16px;color:#0073e6;border-bottom:2px solid #0073e6;margin-top:14px}
    .modern .section{margin-top:14px}

    .minimal h1{font-size:22px;text-transform:uppercase;margin-bottom:4px}
    .minimal h2{font-size:15px;margin-top:14px;background:#eee;padding:4px;border-left:4px solid #333}
    .minimal .section{margin-top:12px}

    .creative{font-family:'Georgia',serif;color:#2c2c54}
    .creative h1{font-size:26px;color:#d35400;margin-bottom:6px}
    .creative h2{font-size:16px;color:#d35400;border-bottom:1px dashed #d35400;margin-top:14px}
    .creative .section{margin-top:14px}
  </style>
</head>
<body>
<div class="container">
  <!-- Left Form -->
  <div class="card">
    <h2>Build Your Resume</h2>
    <button onclick="loadExample()">Load Example Resume</button>

    <label>Choose Template</label>
    <select id="template" onchange="applyTemplate()">
      <option value="modern">Modern</option>
      <option value="minimal">Minimal</option>
      <option value="creative">Creative</option>
    </select>

    <label>Name</label><input id="name" type="text" placeholder="Your Full Name"/>
    <label>Title</label><input id="title" type="text" placeholder="Data Analyst"/>
    <label>Contact</label><textarea id="contact" placeholder="Phone • Email • Location"></textarea>
    <label>Summary</label><textarea id="summary"></textarea>

    <label>Experience</label>
    <div id="expList"></div>
    <button type="button" onclick="addExperience()">+ Add Experience</button>

    <label>Education</label>
    <div id="eduList"></div>
    <button type="button" onclick="addEducation()">+ Add Education</button>

    <label>Certifications</label>
    <div id="certList"></div>
    <button type="button" onclick="addCert()">+ Add Certification</button>

    <label>Projects</label>
    <div id="projList"></div>
    <button type="button" onclick="addProject()">+ Add Project</button>

    <label>Skills</label>
    <textarea id="skills" placeholder="e.g. SQL, Python, Power BI"></textarea>

    <button onclick="refreshPreview()">Preview</button>
    <button onclick="downloadPdf()">Download PDF</button>
  </div>

  <!-- Right Preview -->
  <div class="card">
    <div id="resume" class="resume modern">
      <h1 id="p_name">Your Name</h1>
      <div id="p_title">Your Title</div>
      <div id="p_contact">Contact Info</div>

      <div class="section">
        <h2>SUMMARY</h2>
        <div id="p_summary">Write a short professional summary here.</div>
      </div>

      <div class="section">
        <h2>EXPERIENCE</h2>
        <div id="p_experience"></div>
      </div>

      <div class="section">
        <h2>EDUCATION</h2>
        <div id="p_education"></div>
      </div>

      <div class="section">
        <h2>CERTIFICATIONS</h2>
        <div id="p_cert"></div>
      </div>

      <div class="section">
        <h2>PROJECTS</h2>
        <div id="p_projects"></div>
      </div>

      <div class="section">
        <h2>SKILLS</h2>
        <div id="p_skills"></div>
      </div>
    </div>
  </div>
</div>

<script>
function addExperience(){
  const div=document.createElement("div");
  div.innerHTML=`<input type="text" placeholder="Company — Role (Dates)" class="exp"/><textarea placeholder="Description / Achievements" class="expDesc"></textarea>`;
  document.getElementById("expList").appendChild(div);
}
function addEducation(){
  const div=document.createElement("div");
  div.innerHTML=`<input type="text" placeholder="Degree — University (Year)" class="edu"/>`;
  document.getElementById("eduList").appendChild(div);
}
function addCert(){
  const div=document.createElement("div");
  div.innerHTML=`<input type="text" placeholder="Certification Name" class="cert"/>`;
  document.getElementById("certList").appendChild(div);
}
function addProject(){
  const div=document.createElement("div");
  div.innerHTML=`<input type="text" placeholder="Project Title" class="proj"/><textarea placeholder="Project details" class="projDesc"></textarea>`;
  document.getElementById("projList").appendChild(div);
}
function refreshPreview(){
  document.getElementById("p_name").innerText=document.getElementById("name").value;
  document.getElementById("p_title").innerText=document.getElementById("title").value;
  document.getElementById("p_contact").innerText=document.getElementById("contact").value;
  document.getElementById("p_summary").innerText=document.getElementById("summary").value;

  let expHtml="";
  document.querySelectorAll(".exp").forEach((e,i)=>{
    expHtml+=`<p><strong>${e.value}</strong><br>${document.querySelectorAll(".expDesc")[i].value}</p>`;
  });
  document.getElementById("p_experience").innerHTML=expHtml;

  let eduHtml="";
  document.querySelectorAll(".edu").forEach(e=>eduHtml+=`<p>${e.value}</p>`);
  document.getElementById("p_education").innerHTML=eduHtml;

  let certHtml="";
  document.querySelectorAll(".cert").forEach(e=>certHtml+=`<p>${e.value}</p>`);
  document.getElementById("p_cert").innerHTML=certHtml;

  let projHtml="";
  document.querySelectorAll(".proj").forEach((e,i)=>{
    projHtml+=`<p><strong>${e.value}</strong><br>${document.querySelectorAll(".projDesc")[i].value}</p>`;
  });
  document.getElementById("p_projects").innerHTML=projHtml;

  document.getElementById("p_skills").innerText=document.getElementById("skills").value;
}
function downloadPdf(){
  refreshPreview();
  const element=document.getElementById("resume");
  html2pdf().from(element).save("resume.pdf");
}
function loadExample(){
  document.getElementById("name").value="Bhanu Kumar Tiwari";
  document.getElementById("title").value="Data Analyst";
  document.getElementById("contact").value="+91 9782434496 • tiwaribhanu09@gmail.com • Delhi, India";
  document.getElementById("summary").value="Proficient in Data Visualization, Reporting, Dashboarding, and Statistical Analysis with hands-on experience in SQL, Power BI, and Python.";

  document.getElementById("expList").innerHTML="";
  addExperience();
  document.querySelector(".exp").value="GST Corporation Limited — Quality Control Executive (Jan 2022 – Present)";
  document.querySelector(".expDesc").value="Conducted product inspections per ISO standards, performed Root Cause Analysis, and collaborated cross-functionally for process improvements.";

  document.getElementById("eduList").innerHTML="";
  addEducation();
  document.querySelector(".edu").value="B.Tech in Mechanical — G.B. Pant Govt. Engineering College (2019)";

  document.getElementById("certList").innerHTML="";
  addCert();
  document.querySelector(".cert").value="Advanced Excel, SQL, Power BI, Python Certifications";

  document.getElementById("projList").innerHTML="";
  addProject();
  document.querySelector(".proj").value="Zomato Restaurant Analysis";
  document.querySelector(".projDesc").value="Analyzed dataset of 9551 restaurants in 15+ countries. Built Power BI reports with Power Query, Charts, and DAX.";

  document.getElementById("skills").value="SQL, Power BI, Excel, Python, Data Analysis, Reporting, Dashboarding";

  refreshPreview();
}
function applyTemplate(){
  const selected=document.getElementById("template").value;
  const resume=document.getElementById("resume");
  resume.className="resume "+selected;
}
</script>
</body>
</html>
