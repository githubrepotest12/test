// update scencount & scroll
  document.getElementById('scencount').value = x;
  const scenx = x - 1;

  // — right here, bind the new inputs —
  const runBtn      = document.getElementById('runSim');
  const newScenario = document.getElementById(`scenario${scenx}`);
  newScenario
    .querySelectorAll('input.auto-default-min[type="number"]')
    .forEach(i => attachAutoDefault(i, showInputToast, isFormValid, runBtn));

  // now bump x
  x++;
