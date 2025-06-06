<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>JavaScript Event Assignment</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>

  <header>
    <h1>JS Event Interaction Playground 🎮</h1>
  </header>

  <main>

    <!-- Event Button Section -->
    <section>
      <h2>Event Button</h2>
      <button id="actionBtn">Click Me!</button>
    </section>

    <!-- Image Gallery -->
    <section>
      <h2>Image Gallery</h2>
      <div id="gallery">
        <img id="gallery-img" src="https://via.placeholder.com/300" alt="Gallery Image" />
        <button id="next-img">Next Image</button>
      </div>
    </section>

    <!-- Tab Navigation -->
    <section>
      <h2>Tab Navigation</h2>
      <div class="tabs">
        <button class="tab" data-tab="1">Tab 1</button>
        <button class="tab" data-tab="2">Tab 2</button>
      </div>
      <div id="tab-content">
        <p>Select a tab to display content.</p>
      </div>
    </section>

    <!-- Form Validation -->
    <section>
      <h2>Signup Form</h2>
      <form id="signupForm">
        <label for="email">Email:</label>
        <input type="email" id="email" required />
        <br />
        <label for="password">Password:</label>
        <input type="password" id="password" required />
        <br />
        <button type="submit">Submit</button>
        <p id="form-msg"></p>
      </form>
    </section>

  </main>

  <script src="script.js"></scrip

    /* General Styles */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 2rem;
  background-color: #f0f4f8;
  color: #333;
}

h1, h2 {
  color: #1a1a1a;
}

section {
  margin-bottom: 2rem;
  padding: 1rem;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.05);
}

/* Buttons */
button {
  padding: 0.5rem 1rem;
  margin-top: 0.5rem;
  background-color: #8a2be2;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.3s ease;
}

button:hover {
  background-color: #6a1bb5;
}

/* Gallery Image */
#gallery img {
  width: 300px;
  height: auto;
  display: block;
  margin-bottom: 1rem;
}

/* Tabs */
.tabs {
  margin-bottom: 1rem;
}

.tab {
  margin-right: 0.5rem;
}

.tab.active {
  background-color: #00bcd4;
}

/* Form Message */
#form-msg {
  margin-top: 1rem;
  font-weight: bold;
}

    // ========== 1. BUTTON EVENTS ========== //
const actionBtn = document.getElementById("actionBtn");

actionBtn.addEventListener("click", () => {
  actionBtn.textContent = "You clicked me!";
  actionBtn.style.backgroundColor = "#39FF14";
});

actionBtn.addEventListener("dblclick", () => {
  alert("Double-click detected! 🤫");
});

actionBtn.addEventListener("mouseover", () => {
  actionBtn.style.transform = "scale(1.1)";
});
actionBtn.addEventListener("mouseout", () => {
  actionBtn.style.transform = "scale(1)";
});

// ========== 2. KEYPRESS DETECTION ========== //
document.addEventListener("keydown", (event) => {
  console.log(`Key pressed: ${event.key}`);
});

// ========== 3. IMAGE GALLERY ========== //
const images = [
  "https://via.placeholder.com/300?text=Image+1",
  "https://via.placeholder.com/300?text=Image+2",
  "https://via.placeholder.com/300?text=Image+3"
];

let currentImageIndex = 0;
const galleryImg = document.getElementById("gallery-img");
const nextImgBtn = document.getElementById("next-img");

nextImgBtn.addEventListener("click", () => {
  currentImageIndex = (currentImageIndex + 1) % images.length;
  galleryImg.src = images[currentImageIndex];
});

// ========== 4. TABS ========== //
const tabs = document.querySelectorAll(".tab");
const tabContent = document.getElementById("tab-content");

tabs.forEach(tab => {
  tab.addEventListener("click", () => {
    tabs.forEach(t => t.classList.remove("active"));
    tab.classList.add("active");

    const tabNumber = tab.dataset.tab;
    tabContent.innerHTML = `<p>Now viewing content for Tab ${tabNumber}.</p>`;
  });
});

// ========== 5. FORM VALIDATION ========== //
const signupForm = document.getElementById("signupForm");
const formMsg = document.getElementById("form-msg");

signupForm.addEventListener("submit", (e) => {
  e.preventDefault();

  const email = document.getElementById("email").value.trim();
  const password = document.getElementById("password").value;

  if (!email.includes("@") || !email.includes(".")) {
    formMsg.textContent = "❌ Please enter a valid email address.";
    formMsg.style.color = "red";
    return;
  }

  if (password.length < 8) {
    formMsg.textContent = "❌ Password must be at least 8 characters.";
    formMsg.style.color = "red";
    return;
  }

  formMsg.textContent = "✅ Form submitted successfully!";
  formMsg.style.color = "green";
});

// Real-time feedback while typing
document.getElementById("password").addEventListener("input", (e) => {
  const pwd = e.target.value;
  if (pwd.length < 8) {
    formMsg.textContent = "⚠️ Password is too short.";
    formMsg.style.color = "orange";
  } else {
    formMsg.textContent = "";
  }
});



