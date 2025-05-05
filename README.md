document.addEventListener('DOMContentLoaded', () => {
  const form   = document.getElementById('simForm');
  const runBtn = document.getElementById('runSim');

  // your existing isFormValid() & showInputToast()

  form.addEventListener('focusout', e => {
    // catch any number input with auto-default-min
    const inp = e.target.closest('input.auto-default-min[type="number"]');
    if (!inp) return;

    // only if it stayed blank
    if (inp.value.trim() === '') {
      inp._autoTimer = setTimeout(() => {
        const minVal = parseFloat(inp.min) || 0;
        inp.value = minVal;
        showInputToast(
          `No value entered—defaulting to minimum of ${minVal}.`,
          inp
        );
        runBtn.disabled = !isFormValid();
      }, 5000);
    }
  });

  // cancel pending autofill on focusin or user typing
  form.addEventListener('focusin',  e => {
    const inp = e.target.closest('input.auto-default-min');
    if (inp && inp._autoTimer) clearTimeout(inp._autoTimer);
  });
  form.addEventListener('input',    e => {
    const inp = e.target.closest('input.auto-default-min');
    if (inp && inp._autoTimer) clearTimeout(inp._autoTimer);
    // keep your Run-button state up to date
    runBtn.disabled = !isFormValid();
  });
});
