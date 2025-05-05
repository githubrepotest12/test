document.addEventListener('DOMContentLoaded', () => {
  const form   = document.getElementById('simForm');
  const runBtn = document.getElementById('runSim');

  // 1) bind every existing auto-default-min field
  form
    .querySelectorAll('input.auto-default-min[type="number"]')
    .forEach(i => attachAutoDefault(i, showInputToast, isFormValid, runBtn));

  // 2) …your existing form logic (enable/disable runBtn, submit handler)…
});
