document.addEventListener('DOMContentLoaded', () => {
  const autoFields = document.querySelectorAll('input.auto-default-min');
  console.log('Found auto-default fields:', autoFields);

  autoFields.forEach(input => {
    console.log('Binding blur handler to:', input);
    let timer;

    input.addEventListener('blur', () => {
      console.log('Blur fired on:', input);
      if (input.value.trim() === '') {
        console.log('Starting 5s timer for blank field…');
        timer = setTimeout(() => {
          const minVal = parseFloat(input.min) || 0;
          console.log(`Timer done → autofilling ${minVal}`);
          input.value = minVal;
          showInputToast(
            `No value entered — defaulting to minimum of ${minVal}.`,
            input
          );
          runBtn.disabled = !isFormValid();
        }, 5000);
      }
    });

    ['focus', 'input'].forEach(evt => {
      input.addEventListener(evt, () => {
        console.log(`${evt} on ${input.id} → clearing timer`);
        clearTimeout(timer);
      });
    });
  });
});
