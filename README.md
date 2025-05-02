document.addEventListener('DOMContentLoaded', () => {
  const pauseInput = document.getElementById('licdurshow');
  let blankTimer;

  pauseInput.addEventListener('blur', () => {
    // only start the timer if it’s still blank
    if (pauseInput.value.trim() === '') {
      blankTimer = setTimeout(() => {
        // pick up the defined min (fallback to 0)
        const minVal = pauseInput.min ? parseFloat(pauseInput.min) : 0;

        // autofill & notify
        pauseInput.value = minVal;
        showInputToast(
          `No minutes entered — defaulting to minimum of ${minVal}.`,
          pauseInput
        );

        // re-validate your Run button (if you have isFormValid())
        document.getElementById('runSim').disabled = !isFormValid();
      }, 5000);
    }
  });

  // if they focus back or type, cancel the pending autofill
  pauseInput.addEventListener('focus', () => clearTimeout(blankTimer));
  pauseInput.addEventListener('input', () => clearTimeout(blankTimer));
});
