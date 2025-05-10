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
      font-size: 2.5em;
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

    .required::before {
      content: "* ";
      color: red;
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
      font-size: 1.1em;
      color: green;
      margin-top: 20px;
      display: none;
    }

    #checkbox-error {
      color: red;
      display: none;
      font-size: 0.9em;
      margin-top: 10px;
    }
  </style>
</head>
<body>

  <h2>Contact Us</h2>
  <form id="contact-form" action="https://formspree.io/f/xrbqbryo" method="POST" target="_top">
    <div class="fs-field">
      <label class="fs-label required" for="name">Name</label>
      <input class="fs-input" id="name" name="name" required />
    </div>
    <div class="fs-field">
      <label class="fs-label required" for="email">Email Address</label>
      <input class="fs-input" id="email" name="email" required />
    </div>
    <div class="fs-field">
      <label class="fs-label required" for="number">Phone Number</label>
      <input class="fs-input" id="number" name="number" required />
    </div>

    <div class="fs-field">
      <label class="fs-label required">What can we help you with?</label>
      <div class="fs-checkbox-group">
        <label><input type="checkbox" id="service-final" name="services[]" value="Final Expense"> Final Expense</label>
        <label><input type="checkbox" id="service-life" name="services[]" value="Life Insurance"> Life Insurance</label>
        <label><input type="checkbox" id="service-annuities" name="services[]" value="Annuities"> Annuities</label>
        <label><input type="checkbox" id="service-medicare" name="services[]" value="Medicare"> Medicare</label>
        <label><input type="checkbox" id="service-dental" name="services[]" value="Dental"> Dental</label>
        <label><input type="checkbox" id="service-vision" name="services[]" value="Vision"> Vision</label>
        <label><input type="checkbox" id="service-aca" name="services[]" value="ACA Marketplace"> ACA Marketplace</label>
      </div>
      <div id="checkbox-error">Please select at least one option.</div>
    </div>

    <div class="fs-field">
      <label class="fs-label" for="contact-time">When would you like to be contacted?</label>
      <input class="fs-input" type="datetime-local" id="contact-time" name="contact-time">
    </div>

    <div class="fs-button-group">
      <button class="fs-button" type="submit">Send</button>
    </div>
  </form>

  <p id="form-status">Thank you! Your message has been sent.</p>

  <script>
    const form = document.getElementById('contact-form');
    const status = document.getElementById('form-status');
    const checkboxGroup = document.querySelectorAll('input[name="services[]"]');
    const checkboxError = document.getElementById('checkbox-error');

    form.addEventListener('submit', async (e) => {
      e.preventDefault();

      // Check if at least one checkbox is selected
      let isChecked = Array.from(checkboxGroup).some(checkbox => checkbox.checked);

      if (!isChecked) {
        checkboxError.style.display = 'block';  // Show error message if no checkbox is selected
        return;  // Prevent form submission
      } else {
        checkboxError.style.display = 'none';  // Hide error message if any checkbox is selected
      }

      const data = new FormData(form);
      try {
        const res = await fetch("https://formspree.io/f/xrbqbryo", {
          method: "POST",
          body: data,
          headers: { 'Accept': 'application/json' }
        });
        if (res.ok) {
          status.style.display = "block";
          status.textContent = "Thank you! Your message has been sent.";
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
