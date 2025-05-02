document.addEventListener('DOMContentLoaded', () => {
  const form   = document.getElementById('simForm');
  const runBtn = document.getElementById('runSim');

  form.addEventListener('input', () => {
    runBtn.disabled = !form.checkValidity();
  });

  form.addEventListener('submit', e => {
    // — 1) Default blanks to zero —
    form
      .querySelectorAll('input[type="number"].default-zero')
      .forEach(input => {
        if (input.value.trim() === '') {
          input.value = 0;
        }
      });

    // — 2) Disable any hidden inputs so they don’t trigger “not focusable” errors —
    form
      .querySelectorAll('input[type="number"]')
      .forEach(input => {
        // offsetParent===null means “not visible in layout”
        if (input.offsetParent === null) {
          input.disabled = true;
        }
      });

    // — 3) Then do your normal validity check —
    if (!form.checkValidity()) {
      e.preventDefault();
      form.reportValidity();
    }
    // else: let it go (or kick off your JS simulation)
  });
});
