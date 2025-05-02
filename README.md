  // 1) Grab all your default-zero fields
  const zeroFields = form.querySelectorAll('input[type="number"].default-zero');

  zeroFields.forEach(input => {
    let timerId;

    // When they leave the field…
    input.addEventListener('blur', () => {
      // only if it’s still blank
      if (input.value.trim() === '') {
        timerId = setTimeout(() => {
          // determine your minimum
          const min = input.min 
            ? parseFloat(input.min) 
            : (input.dataset.min ? parseFloat(input.dataset.min) : 0);

          // autofill & toast
          input.value = min;
          showInputToast(
            `No value entered → defaulting to minimum of ${min}.`, 
            input
          );

          // re-run your “enable button?” check
          runBtn.disabled = !isFormValid();
        }, 5_000);
      }
    });

    // if they focus back or type something, cancel the timer
    input.addEventListener('focus', () => clearTimeout(timerId));
    input.addEventListener('input', () => clearTimeout(timerId));
  });
