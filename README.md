function attachAutoDefault(input, showInputToast, isFormValid, runBtn) {
  let timer;

  input.addEventListener('blur', () => {
    if (input.value.trim() === '') {
      timer = setTimeout(() => {
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

  const cancel = () => clearTimeout(timer);
  input.addEventListener('focus', cancel);
  input.addEventListener('input',  cancel);
}
