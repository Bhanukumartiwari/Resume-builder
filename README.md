# Resume-builder
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Free Resume Builder with Templates</title>

  <!-- ✅ SEO -->
  <meta name="description" content="Free Resume Builder Online - Create your professional ATS-friendly resume with multiple templates. Preview instantly and download in PDF format. 100% free resume maker tool." />
  <meta name="keywords" content="resume builder, free resume maker, cv templates, online cv generator, resume pdf download, ats resume builder, professional cv builder free" />
  <meta name="author" content="Resume Builder Hub" />

  <!-- ✅ Schema.org JSON-LD -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "SoftwareApplication",
    "name": "Free Resume Builder with Templates",
    "applicationCategory": "BusinessApplication",
    "operatingSystem": "All",
    "url": "https://bhanukumartiwari.github.io/resume-builder/",
    "description": "Free Resume Builder with templates - Create a professional resume, preview instantly, and download PDF. 100% free online CV maker tool.",
    "creator": { "@type": "Organization", "name": "Resume Builder Hub" },
    "offers": { "@type": "Offer", "price": "0", "priceCurrency": "INR", "availability": "https://schema.org/InStock" },
    "keywords": ["resume builder","resume templates","free resume maker","cv generator","ats resume","resume pdf download"]
  }
  </script>

  <!-- ✅ jsPDF -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

  <style>
    body { font-family: Arial, sans-serif; background: #f4f7f9; padding: 20px; color: #333; }
    h1 { text-align: center; color: #2a4d69; }
    .container { max-width: 800px; margin: auto; background: white; padding: 20px; border-radius: 12px; box-shadow: 0 5px 15px rgba(0,0,0,0.1);}
    label { font-weight: bold; margin-top: 10px; display: block; }
    input, textarea, select { width: 100%; padding: 10px; margin-top: 5px; border-radius: 6px; border: 1px solid #ccc; }
    button { margin-top: 15px; padding: 12px; border: none; border-radius: 8px; background: #2a4d69; color: white; font-weight: bold; cursor: pointer; }
    button:hover { background: #1f364d; }
    .resume-preview { margin-top: 30px; padding: 20px; border: 1px solid #ddd; background: #fafafa; border-radius: 10px; }
    .template-modern { font-family: Arial, sans-serif; color: #2a4d69; }
    .template-minimal { font-family: Georgia, serif; color: #111; }
    .template-creative { font-family: "Courier New", monospace; color: #444; background: #eef; padding: 15px; border-radius: 8px; }
  </style>
</head>
<body>
  <h1>Free Resume Builder with Templates</h1>
  <div class="container">
    <label>Full Name</label>
    <input type="text" id="name" placeholder="Enter your full name" />

    <label>Email</label>
    <input type="email" id="email" placeholder="Enter your email" />

    <label>Phone</label>
    <input type="text" id="phone" placeholder="Enter your phone number" />

    <label>Summary</label>
    <textarea id="summary" rows="3"></textarea>

    <label>Skills</label>
    <textarea id="skills" rows="2"></textarea>

    <label>Experience</label>
    <textarea id="experience" rows="4"></textarea>

    <label>Education</label>
    <textarea id="education" rows="3"></textarea>

    <label>Choose Resume Template</label>
    <select id="template">
      <option value="modern">Modern</option>
      <option value="minimal">Minimal</option>
      <option value="creative">Creative</option>
    </select>

    <button onclick="previewResume()">Preview Resume</button>
    <button onclick="downloadPDF()">Download as PDF</button>

    <div class="resume-preview" id="resumePreview">
      <h2>Resume Preview</h2>
      <p>Fill the form and click Preview to see your resume here.</p>
    </div>
  </div>

  <script>
    function previewResume() {
      const name = document.getElementById("name").value;
      const email = document.getElementById("email").value;
      const phone = document.getElementById("phone").value;
      const summary = document.getElementById("summary").value;
      const skills = document.getElementById("skills").value;
      const experience = document.getElementById("experience").value;
      const education = document.getElementById("education").value;
      const template = document.getElementById("template").value;

      let templateClass = "";
      if (template === "modern") templateClass = "template-modern";
      if (template === "minimal") templateClass = "template-minimal";
      if (template === "creative") templateClass = "template-creative";

      document.getElementById("resumePreview").innerHTML = `
        <div class="${templateClass}">
          <h2>${name}</h2>
          <p><strong>Email:</strong> ${email}</p>
          <p><strong>Phone:</strong> ${phone}</p>
          <h3>Summary</h3><p>${summary}</p>
          <h3>Skills</h3><p>${skills}</p>
          <h3>Experience</h3><p>${experience}</p>
          <h3>Education</h3><p>${education}</p>
        </div>
      `;
    }

    async function downloadPDF() {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();
      const name = document.getElementById("name").value;
      const email = document.getElementById("email").value;
      const phone = document.getElementById("phone").value;
      const summary = document.getElementById("summary").value;
      const skills = document.getElementById("skills").value;
      const experience = document.getElementById("experience").value;
      const education = document.getElementById("education").value;

      let y = 20;
      doc.setFont("helvetica", "bold");
      doc.setFontSize(18);
      doc.text(name, 20, y); y += 10;
      doc.setFont("helvetica", "normal");
      doc.setFontSize(12);
      doc.text(`Email: ${email}`, 20, y); y += 7;
      doc.text(`Phone: ${phone}`, 20, y); y += 10;
      doc.setFont("helvetica", "bold"); doc.text("Summary", 20, y); y += 7;
      doc.setFont("helvetica", "normal"); doc.text(doc.splitTextToSize(summary, 170), 20, y); y += 15;
      doc.setFont("helvetica", "bold"); doc.text("Skills", 20, y); y += 7;
      doc.setFont("helvetica", "normal"); doc.text(doc.splitTextToSize(skills, 170), 20, y); y += 15;
      doc.setFont("helvetica", "bold"); doc.text("Experience", 20, y); y += 7;
      doc.setFont("helvetica", "normal"); doc.text(doc.splitTextToSize(experience, 170), 20, y); y += 15;
      doc.setFont("helvetica", "bold"); doc.text("Education", 20, y); y += 7;
      doc.setFont("helvetica", "normal"); doc.text(doc.splitTextToSize(education, 170), 20, y);

      doc.save("resume.pdf");
    }
  </script>
</body>
</html>
