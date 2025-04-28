<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AI Analyzer Website</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(to right, #a8c0ff, #3f2b96);
      color: #fff;
      text-align: center;
      padding: 20px;
      min-height: 100vh;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
    }
    h1 {
      margin-top: 30px;
      font-size: 2.5em;
      animation: fadeIn 2s ease-in-out;
    }
    #preview {
      margin: 20px auto;
      max-width: 300px;
      max-height: 300px;
      border-radius: 15px;
      border: 2px solid #fff;
      display: none;
      object-fit: cover;
    }
    input[type="file"] {
      margin-top: 20px;
      padding: 10px;
      background-color: #0056b3;
      border: none;
      color: #fff;
      border-radius: 8px;
      cursor: pointer;
      width: 80%;
      max-width: 300px;
    }
    button {
      margin-top: 20px;
      padding: 12px 25px;
      background-color: #007bff;
      border: none;
      border-radius: 8px;
      font-size: 1em;
      color: #fff;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      background-color: #0056b3;
      transform: scale(1.05);
    }
    .result {
      margin: 30px auto;
      padding: 20px;
      background-color: rgba(255,255,255,0.1);
      border-radius: 10px;
      display: none;
      animation: fadeIn 2s;
      max-width: 500px;
    }
    .flags {
      margin-top: 20px;
    }
    .flags img {
      width: 80px;
      margin: 10px;
      border-radius: 8px;
      border: 2px solid #fff;
      background: #fff;
    }
    nav {
      margin: 20px 0;
      font-size: 1.1em;
      display: flex;
      justify-content: center;
      gap: 20px;
      flex-wrap: wrap;
    }
    nav a {
      color: #fff;
      text-decoration: none;
      font-weight: bold;
      padding: 5px 10px;
      border-radius: 5px;
      transition: 0.3s;
    }
    nav a:hover {
      background-color: rgba(255,255,255,0.2);
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    section {
      margin: 50px auto;
      max-width: 600px;
      text-align: left;
      padding: 20px;
      background-color: rgba(255,255,255,0.1);
      border-radius: 10px;
    }
    footer {
      margin-top: 50px;
      padding: 20px;
      font-size: 0.9em;
    }
  </style>
</head>
<body>
<div class="container">
  <h1>AI Photo Analyzer</h1>

  <nav>
    <a href="#privacy">Privacy Policy</a>
    <a href="#contact">Contact Us</a>
    <a href="#analyzer">Photo Analyzer</a>
  </nav>

  <div id="analyzer">
    <input type="file" accept="image/*" onchange="previewImage(event)">
    <br>
    <button onclick="analyzeImage()">Analyze Photo</button>

    <img id="preview" src="#" alt="Image Preview">

    <div class="result" id="result">
      <h2>Analysis Result:</h2>
      <p><strong>Age:</strong> <span id="age"></span></p>
      <p><strong>Emotion:</strong> <span id="emotion"></span></p>
      <p><strong>Relationship Status:</strong> <span id="status"></span></p>
      <p><strong>Mood Level:</strong> <span id="mood"></span>%</p>
      <div class="flags" id="flagContainer"></div>
    </div>
  </div>

  <section id="privacy">
    <h2>Privacy Policy</h2>
    <p>We respect your privacy. All uploaded images are processed locally in your browser and not stored on any server. No data is collected or shared with third parties.</p>
  </section>

  <section id="contact">
    <h2>Contact Us</h2>
    <p>Email: <a href="mailto:ghufranworld@gmail.com" style="color:#ffcc00;">ghufranworld@gmail.com</a></p>
    <p>For support or questions about our AI analyzer, please contact us via email.</p>
  </section>

  <footer>
    &copy; 2023 AI Photo Analyzer | All Rights Reserved
  </footer>
</div>

<script>
function previewImage(event) {
  const reader = new FileReader();
  reader.onload = function(){
    const output = document.getElementById('preview');
    output.src = reader.result;
    output.style.display = 'block';
    document.getElementById('result').style.display = 'none';
  };
  if(event.target.files[0]) {
    reader.readAsDataURL(event.target.files[0]);
  }
}

function analyzeImage() {
  const preview = document.getElementById('preview');
  if(!preview.src || preview.src === '#') {
    alert('Please upload an image first!');
    return;
  }

  const result = document.getElementById('result');
  const age = Math.floor(Math.random() * (23 - 15 + 1)) + 15;
  const mood = Math.floor(Math.random() * (100 - 50 + 1)) + 50;
  
  const emotions = ['Happy', 'Neutral', 'Excited', 'Calm', 'Surprised'];
  const statuses = ['Single', 'In a relationship', 'Married', 'Complicated'];
  
  document.getElementById('age').innerText = age;
  document.getElementById('mood').innerText = mood;
  document.getElementById('emotion').innerText = emotions[Math.floor(Math.random() * emotions.length)];
  document.getElementById('status').innerText = statuses[Math.floor(Math.random() * statuses.length)];

  const countries = [
    {code: 'us', name: 'USA'},
    {code: 'gb', name: 'UK'},
    {code: 'ca', name: 'Canada'},
    {code: 'au', name: 'Australia'},
    {code: 'fr', name: 'France'},
    {code: 'de', name: 'Germany'}
  ];
  const randomCountry = countries[Math.floor(Math.random() * countries.length)];

  document.getElementById('flagContainer').innerHTML = `
    <p><strong>Country:</strong> ${randomCountry.name}</p>
    <img src="https://flagcdn.com/w160/${randomCountry.code}.png" 
         alt="${randomCountry.name} Flag"
         style="width: 160px; height: auto;">
  `;

  result.style.display = 'block';
  result.scrollIntoView({ behavior: 'smooth' });
}
</script>
</body>
</html>
