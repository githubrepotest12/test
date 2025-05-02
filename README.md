document.addEventListener('DOMContentLoaded', () => {
  const form   = document.getElementById('simForm');
  const runBtn = document.getElementById('runSim');

  // helper to test “valid enough” (your existing isFormValid)
  function isFormValid() { /* … */ }

  // delegate focusout (bubbling version of blur) to start the 5s timer
  form.addEventListener('focusout', e => {
    const input = e.target.closest('input.auto-default-min');
    if (!input) return;
    if (input.value.trim() === '') {
      // stash a timer ID on the element itself
      input._autoDefaultTimer = setTimeout(() => {
        const minVal = parseFloat(input.min) || 0;
        input.value = minVal;
        showInputToast(
          `No value entered—defaulting to minimum of ${minVal}.`,
          input
        );
        runBtn.disabled = !isFormValid();
      }, 5000);
    }
  });

  // delegate focusin (bubbling version of focus) and input to cancel that timer
  form.addEventListener('focusin',  e => {
    const input = e.target.closest('input.auto-default-min');
    if (input && input._autoDefaultTimer) clearTimeout(input._autoDefaultTimer);
  });
  form.addEventListener('input',    e => {
    const input = e.target.closest('input.auto-default-min');
    if (input && input._autoDefaultTimer) clearTimeout(input._autoDefaultTimer);
    
    // also keep your “enable button” logic up to date
    runBtn.disabled = !isFormValid();
  });

  // (optional) on submit you still zero-fill and validate as before
  form.addEventListener('submit', e => {
    form.querySelectorAll('input.auto-default-min').forEach(i => {
      if (i.value.trim() === '') i.value = parseFloat(i.min)||0;
    });
    if (!isFormValid()) {
      e.preventDefault();
      form.reportValidity();
    }
  });
});
