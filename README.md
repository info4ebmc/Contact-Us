<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Us</title>
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
    <div class="fs-field">
      <label class="fs-label" for="message">What services are you looking for?</label>
      <textarea class="fs-textarea" id="message" name="message"></textarea>
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
