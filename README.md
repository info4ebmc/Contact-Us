<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Us</title>
  <style>
    h2 {
      color: green;
      font-size: 2.5em;
    }

    .fs-button {
      background-color: green;
      color: white;
      padding: 15px 30px;
      font-size: 1.2em;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .fs-button:hover {
      background-color: darkgreen;
    }

    .fs-field {
      margin-bottom: 10px;
    }

    .fs-label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }

    /* Smaller input fields */
    .fs-input,
    .fs-textarea {
      width: 80%;  /* Reduced the width */
      padding: 8px;  /* Reduced padding */
      font-size: 0.9em;  /* Smaller font */
      box-sizing: border-box;
      margin-bottom: 8px;
    }

    .fs-textarea {
      height: 100px; /* Make the textarea height smaller */
    }

    .fs-input[type="datetime-local"] {
      padding: 6px;
    }

    .fs-button-group {
      margin-top: 15px;
    }
  </style>
</head>
<body>

  <h2>Contact Us</h2>
  <form id="contact-form" action="https://formspree.io/f/xrbqbryo" method="POST" target="_top">
    <div class="fs-field">
      <label class="fs-label" for="name">Name</label>
      <input class="fs-input" id="name" name="name" required />
    </div>
    <div class="fs-field">
      <label class="fs-label" for="email">Email Address</label>
      <input class="fs-input" id="email" name="email" required />
    </div>
    <div class="fs-field">
      <label class="fs-label" for="number">Phone Number</label>
      <input class="fs-input" id="number" name="number" required />
    </div>
<!-- Inside the form, under What can we help you with? -->
<div class="fs-field">
  <label class="fs-label">What can we help you with?</label>
  <div class="fs-checkbox-group">
    <label><input type="checkbox" name="services[]" value="Final Expense"> Final Expense</label>
    <label><input type="checkbox" name="services[]" value="Life Insurance"> Life Insurance</label>
    <label><input type="checkbox" name="services[]" value="Annuities"> Annuities</label>
    <label><input type="checkbox" name="services[]" value="Medicare Advantage"> Medicare Advantage</label>
    <label><input type="checkbox" name="services[]" value="Medicare Supplement"> Medicare Supplement</label>
    <label><input type="checkbox" name="services[]" value="Dental and Vision"> Dental and Vision</label>
    <label><input type="checkbox" name="services[]" value="ACA Marketplace"> ACA Marketplace</label> <!-- New line added -->
  </div>
</div>
</div>
    <div class="fs-field">
      <label class="fs-label" for="contact-time">When would you like to be contacted?</label>
      <input class="fs-input" type="datetime-local" id="contact-time" name="contact-time">
    </div>
    <div class="fs-button-group">
      <button class="fs-button" type="submit">Send</button>
    </div>
  </form>

  <p id="form-status" style="display:none; color:green;">Thank you! Your message has been sent.</p>

  <script>
    const form = document.getElementById('contact-form');
    const status = document.getElementById('form-status');

    form.addEventListener('submit', async (e) => {
      e.preventDefault();
      const data = new FormData(form);
      try {
        const res = await fetch("https://formspree.io/f/xrbqbryo", {
          method: "POST",
          body: data,
          headers: { 'Accept': 'application/json' }
        });
        if (res.ok) {
          status.style.display = "block";
          form.reset();
        } else {
          status.textContent = "Oops! There was a problem.";
          status.style.display = "block";
        }
      } catch (err) {
        status.textContent = "Error submitting form.";
        status.style.display = "block";
      }
    });
  </script>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Us</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      margin: 0;
    }

    h2 {
      color: green;
      font-size: 2em;
      text-align: center;
    }

    form {
      max-width: 600px;
      margin: auto;
    }

    .fs-field {
      margin-bottom: 15px;
    }

    .fs-label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }

    .fs-input,
    .fs-textarea,
    .fs-checkbox-group {
      width: 100%;
      padding: 10px;
      font-size: 1em;
      box-sizing: border-box;
    }

    .fs-textarea {
      height: 100px;
    }

    .fs-input[type="datetime-local"] {
      padding: 8px;
    }

    .fs-button {
      background-color: green;
      color: white;
      padding: 15px;
      font-size: 1em;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      width: 100%;
    }

    .fs-button:hover {
      background-color: darkgreen;
    }

    .fs-checkbox-group label {
      display: block;
      margin-bottom: 8px;
      font-weight: normal;
    }

    .fs-checkbox-group input[type="checkbox"] {
      margin-right: 10px;
    }

    #form-status {
      text-align: center;
      font-size
