document.querySelectorAll('input.auto-default-min').forEach(input => {
  let timer;

  input.addEventListener('blur', () => {
    if (input.value.trim() === '') {
      timer = setTimeout(() => {
        const minVal = parseFloat(input.min) || 0;
        input.value = minVal;
        showInputToast(
          `No value entered — defaulting to minimum of ${minVal}.`,
          input
        );
        runBtn.disabled = !isFormValid();
      }, 5000);
    }
  });

  ['focus','input'].forEach(evt =>
    input.addEventListener(evt, () => clearTimeout(timer))
  );
});
