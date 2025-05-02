document.addEventListener('DOMContentLoaded', () => {
  const form   = document.getElementById('simForm');
  const runBtn = document.getElementById('runSim');

  function isFormReallyValid() {
    // grab all form controls you care about
    const controls = [...form.querySelectorAll('input, select, textarea')];
    for (const ctrl of controls) {
      // 1) if it's a default-zero number and blank → skip validity
      if (
        ctrl.type === 'number' &&
        ctrl.classList.contains('default-zero') &&
        ctrl.value.trim() === ''
      ) continue;

      // 2) otherwise use the browser check
      if (!ctrl.checkValidity()) return false;
    }
    return true;
  }

  // enable/disable on any change
  form.addEventListener('input', () => {
    runBtn.disabled = !isFormReallyValid();
  });

  form.addEventListener('submit', e => {
    // default blanks → zero
    form.querySelectorAll('input.default-zero[type="number"]')
      .forEach(i => { if (i.value.trim() === '') i.value = 0 });

    // then do your normal validity guard
    if (!form.checkValidity()) {
      e.preventDefault();
      form.reportValidity();
    }
    // else: form is valid and will submit
  });
});
