const form   = document.getElementById('simForm');
const runBtn = document.getElementById('runSim');

form.addEventListener('input', () => {
  runBtn.disabled = !form.checkValidity();
});

form.addEventListener('submit', e => {
  // 1) Default any blank “.default-zero” fields to 0
  form
    .querySelectorAll('input[type="number"].default-zero')
    .forEach(input => {
      if (input.value.trim() === '') {
        input.value = 0;
      }
    });

  // 2) Then run your normal validity guard
  if (!form.checkValidity()) {
    e.preventDefault();
    form.reportValidity();
  }
  // else: form will submit (or you kick off your JS simulation)
});
