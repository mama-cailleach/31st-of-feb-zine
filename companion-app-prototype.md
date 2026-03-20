---
layout: page
title: Companion App Prototype
permalink: /companion-app-prototype/
---

<div class="sheet">
  <h2>Prototype Runner</h2>
  <p class="no-print">
    This browser prototype reads live game data from <code>site.data.tables</code> and runs one full loop.
  </p>

  <div class="proto-grid">
    <div>
      <h3>Session Controls</h3>
      <p><strong>Phase:</strong> <span id="phaseLabel">Not started</span></p>
      <p><strong>Status:</strong> <span id="statusLabel">idle</span></p>
      <button id="startBtn" type="button">Start New Loop</button>
      <button id="rollBtn" type="button" disabled>Roll d100 For Phase</button>
      <button id="complianceBtn" type="button" disabled>Use Compliance</button>
      <button id="autoRunBtn" type="button" disabled>Auto-Run Full Loop</button>
      <button id="endBtn" type="button" disabled>End Loop Now</button>
      <p>
        <label>
          <input id="stepModeToggle" type="checkbox" />
          Step-by-step mode (preview before apply)
        </label>
      </p>
      <div class="batch-row">
        <label for="batchCountInput">Batch loops</label>
        <input id="batchCountInput" type="number" min="1" max="5000" value="100" />
        <button id="runBatchBtn" type="button">Run Batch</button>
      </div>
    </div>

    <div>
      <h3>Stats</h3>
      <table class="sheet-table">
        <thead>
          <tr>
            <th>Stat</th>
            <th>Current</th>
          </tr>
        </thead>
        <tbody>
          <tr><td>Battery</td><td id="batteryValue">-</td></tr>
          <tr><td>Stability</td><td id="stabilityValue">-</td></tr>
          <tr><td>SIP</td><td id="sipValue">-</td></tr>
          <tr><td>Running Success Probability</td><td id="probabilityValue">-</td></tr>
          <tr><td>Threshold Triggered</td><td id="thresholdValue">-</td></tr>
        </tbody>
      </table>
    </div>
  </div>

  <h3>Pending Event (Step-by-step)</h3>
  <div id="pendingPanel" class="pending-panel">
    <p id="pendingSummary">No pending event.</p>
    <div class="proto-grid">
      <div>
        <label for="overrideProbability">Probability</label>
        <input id="overrideProbability" type="number" min="0" max="1" step="0.01" />
      </div>
      <div>
        <label for="overrideBatteryDelta">Battery Delta</label>
        <input id="overrideBatteryDelta" type="number" step="1" />
      </div>
      <div>
        <label for="overrideStabilityDelta">Stability Delta</label>
        <input id="overrideStabilityDelta" type="number" step="1" />
      </div>
    </div>
    <button id="applyPendingBtn" type="button" disabled>Apply Pending Event</button>
    <button id="cancelPendingBtn" type="button" disabled>Discard Pending Event</button>
  </div>

  <h3>Phase Event Log</h3>
  <table class="sheet-table">
    <thead>
      <tr>
        <th>Phase</th>
        <th>Roll</th>
        <th>Event</th>
        <th>Category</th>
        <th>Probability</th>
        <th>Battery Delta</th>
        <th>Stability Delta</th>
      </tr>
    </thead>
    <tbody id="eventLogBody">
      <tr><td colspan="7">No events yet.</td></tr>
    </tbody>
  </table>

  <h3>Loop Receipt</h3>
  <pre id="receiptOutput">Start a loop to generate a receipt.</pre>

  <h3>Batch Summary</h3>
  <pre id="batchOutput">Run a batch to see aggregate balance metrics.</pre>
</div>

<style>
  .proto-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1rem;
    margin-bottom: 1rem;
  }

  button {
    margin-right: 0.4rem;
    margin-bottom: 0.4rem;
    padding: 0.45rem 0.7rem;
    border: 1px solid var(--line);
    background: var(--surface);
    color: var(--text);
    cursor: pointer;
  }

  button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  #receiptOutput {
    background: var(--surface);
    border: 1px solid var(--line);
    padding: 0.75rem;
    white-space: pre-wrap;
  }

  #batchOutput {
    background: var(--surface);
    border: 1px solid var(--line);
    padding: 0.75rem;
    white-space: pre-wrap;
  }

  .pending-panel {
    background: var(--surface);
    border: 1px solid var(--line);
    padding: 0.75rem;
    margin-bottom: 1rem;
  }

  .pending-panel label {
    display: block;
    font-size: 0.9rem;
    margin-bottom: 0.2rem;
  }

  .pending-panel input {
    width: 100%;
    padding: 0.35rem;
    border: 1px solid var(--line);
    background: #fff;
  }

  .batch-row {
    margin-top: 0.5rem;
    display: grid;
    grid-template-columns: auto 100px auto;
    gap: 0.4rem;
    align-items: center;
  }

  .batch-row input {
    width: 100%;
    padding: 0.3rem;
    border: 1px solid var(--line);
    background: #fff;
  }
</style>

<script id="gameData" type="application/json">
{{ site.data.tables | jsonify }}
</script>

<script>
(() => {
  const data = JSON.parse(document.getElementById('gameData').textContent);

  const startBtn = document.getElementById('startBtn');
  const rollBtn = document.getElementById('rollBtn');
  const complianceBtn = document.getElementById('complianceBtn');
  const autoRunBtn = document.getElementById('autoRunBtn');
  const endBtn = document.getElementById('endBtn');
  const stepModeToggle = document.getElementById('stepModeToggle');
  const batchCountInput = document.getElementById('batchCountInput');
  const runBatchBtn = document.getElementById('runBatchBtn');

  const applyPendingBtn = document.getElementById('applyPendingBtn');
  const cancelPendingBtn = document.getElementById('cancelPendingBtn');
  const pendingSummary = document.getElementById('pendingSummary');
  const overrideProbability = document.getElementById('overrideProbability');
  const overrideBatteryDelta = document.getElementById('overrideBatteryDelta');
  const overrideStabilityDelta = document.getElementById('overrideStabilityDelta');

  const phaseLabel = document.getElementById('phaseLabel');
  const statusLabel = document.getElementById('statusLabel');

  const batteryValue = document.getElementById('batteryValue');
  const stabilityValue = document.getElementById('stabilityValue');
  const sipValue = document.getElementById('sipValue');
  const probabilityValue = document.getElementById('probabilityValue');
  const thresholdValue = document.getElementById('thresholdValue');

  const eventLogBody = document.getElementById('eventLogBody');
  const receiptOutput = document.getElementById('receiptOutput');
  const batchOutput = document.getElementById('batchOutput');

  const batteryConfig = data.character.vital_signs.find(v => v.id === 'battery');
  const stabilityConfig = data.character.vital_signs.find(v => v.id === 'stability');
  const sipConfig = data.character.vital_signs.find(v => v.id === 'sip');

  const phases = data.rules.loop.phases.slice().sort((a, b) => a.order - b.order);
  const thresholdDecimal = data.rules.probability.threshold_decimal;
  const thresholdEffect = data.rules.probability.threshold_effect;
  const complianceRule = data.rules.stability_maintenance.compliance_restore;

  let state = null;

  function clamp(value, min, max) {
    return Math.max(min, Math.min(max, value));
  }

  function updateUI() {
    if (!state) {
      phaseLabel.textContent = 'Not started';
      statusLabel.textContent = 'idle';
      batteryValue.textContent = '-';
      stabilityValue.textContent = '-';
      sipValue.textContent = '-';
      probabilityValue.textContent = '-';
      thresholdValue.textContent = '-';
      pendingSummary.textContent = 'No pending event.';
      applyPendingBtn.disabled = true;
      cancelPendingBtn.disabled = true;
      return;
    }

    phaseLabel.textContent = state.phaseIndex < phases.length
      ? phases[state.phaseIndex].name
      : 'Complete';

    statusLabel.textContent = state.status;
    batteryValue.textContent = state.stats.battery;
    stabilityValue.textContent = state.stats.stability;
    sipValue.textContent = state.stats.sip;
    probabilityValue.textContent = (state.runningProbability * 100).toFixed(4) + '%';
    thresholdValue.textContent = state.thresholdTriggered ? 'Yes' : 'No';

    const loopActive = state.status === 'active';
    rollBtn.disabled = !loopActive || state.phaseRolled || Boolean(state.pendingEvent);
    complianceBtn.disabled = !loopActive || state.complianceUsedThisPhase;
    autoRunBtn.disabled = !loopActive;
    endBtn.disabled = !loopActive;

    if (state.pendingEvent) {
      pendingSummary.textContent =
        state.pendingEvent.phaseName +
        ' | Roll ' + state.pendingEvent.roll +
        ' | ' + state.pendingEvent.prompt;
      applyPendingBtn.disabled = !loopActive;
      cancelPendingBtn.disabled = !loopActive;
      overrideProbability.disabled = !loopActive;
      overrideBatteryDelta.disabled = !loopActive;
      overrideStabilityDelta.disabled = !loopActive;
    } else {
      pendingSummary.textContent = 'No pending event.';
      applyPendingBtn.disabled = true;
      cancelPendingBtn.disabled = true;
      overrideProbability.disabled = true;
      overrideBatteryDelta.disabled = true;
      overrideStabilityDelta.disabled = true;
    }
  }

  function renderEventLog() {
    if (!state || state.events.length === 0) {
      eventLogBody.innerHTML = '<tr><td colspan="7">No events yet.</td></tr>';
      return;
    }

    eventLogBody.innerHTML = state.events.map(e => {
      return '<tr>' +
        '<td>' + e.phaseName + '</td>' +
        '<td>' + e.roll + '</td>' +
        '<td>' + e.prompt + '</td>' +
        '<td>' + e.category + '</td>' +
        '<td>' + e.probability + '</td>' +
        '<td>' + e.batteryDelta + '</td>' +
        '<td>' + e.stabilityDelta + '</td>' +
      '</tr>';
    }).join('');
  }

  function writeReceipt(reason) {
    const receipt = {
      session_id: state.sessionId,
      ended_by: reason,
      final_stats: {
        battery: state.stats.battery,
        stability: state.stats.stability,
        sip: state.stats.sip
      },
      rolled_event_count: state.events.length,
      running_success_probability: Number(state.runningProbability.toFixed(8)),
      threshold_triggered: state.thresholdTriggered,
      next_loop_date: '31st of February'
    };

    receiptOutput.textContent = JSON.stringify(receipt, null, 2);
  }

  function clearPendingEvent() {
    if (!state) {
      return;
    }

    state.pendingEvent = null;
    overrideProbability.value = '';
    overrideBatteryDelta.value = '';
    overrideStabilityDelta.value = '';
  }

  function endLoop(reason) {
    state.status = 'ended';
    state.phaseIndex = phases.length;
    writeReceipt(reason);
    updateUI();
  }

  function evaluateThreshold() {
    if (!state.thresholdTriggered && state.runningProbability <= thresholdDecimal) {
      state.thresholdTriggered = true;
      state.stats.stability = clamp(
        state.stats.stability + thresholdEffect.stability_delta,
        stabilityConfig.min,
        stabilityConfig.max
      );
      state.stats.sip = Math.max(sipConfig.min, state.stats.sip + thresholdEffect.sip_delta);
    }
  }

  function applyBatteryHardStop() {
    if (state.stats.battery <= batteryConfig.min) {
      state.stats.battery = batteryConfig.min;
      endLoop('battery_zero_hard_stop');
      return true;
    }
    return false;
  }

  function nextPhase() {
    state.phaseIndex += 1;
    state.phaseRolled = false;
    state.complianceUsedThisPhase = false;

    if (state.phaseIndex >= phases.length) {
      endLoop('return_phase_complete');
      return;
    }

    updateUI();
  }

  function buildResolvedEventForCurrentPhase() {
    if (!state || state.phaseIndex >= phases.length) {
      return null;
    }

    const phase = phases[state.phaseIndex];
    const roll = Math.floor(Math.random() * 100) + 1;
    const event = data.random_events.events.find(e => e.roll === roll);

    if (!event) {
      return null;
    }

    return {
      phaseId: phase.id,
      phaseName: phase.name,
      roll,
      prompt: event.prompt,
      category: event.category,
      probability: Number(event.default_probability),
      batteryDelta: Number(event.battery_delta),
      stabilityDelta: Number(event.stability_delta)
    };
  }

  function applyResolvedEvent(resolvedEvent) {
    state.stats.battery = clamp(
      state.stats.battery + resolvedEvent.batteryDelta,
      batteryConfig.min,
      batteryConfig.max
    );

    state.stats.stability = clamp(
      state.stats.stability + resolvedEvent.stabilityDelta,
      stabilityConfig.min,
      stabilityConfig.max
    );

    state.runningProbability = state.runningProbability * resolvedEvent.probability;

    state.events.push({
      phaseId: resolvedEvent.phaseId,
      phaseName: resolvedEvent.phaseName,
      roll: resolvedEvent.roll,
      prompt: resolvedEvent.prompt,
      category: resolvedEvent.category,
      probability: resolvedEvent.probability,
      batteryDelta: resolvedEvent.batteryDelta,
      stabilityDelta: resolvedEvent.stabilityDelta
    });

    state.phaseRolled = true;

    evaluateThreshold();
    renderEventLog();

    if (!applyBatteryHardStop()) {
      nextPhase();
    }
  }

  function rollPhaseEvent() {
    const baseResolvedEvent = buildResolvedEventForCurrentPhase();

    if (!baseResolvedEvent) {
      return;
    }

    if (state.stepMode) {
      state.pendingEvent = baseResolvedEvent;
      overrideProbability.value = String(baseResolvedEvent.probability);
      overrideBatteryDelta.value = String(baseResolvedEvent.batteryDelta);
      overrideStabilityDelta.value = String(baseResolvedEvent.stabilityDelta);
      updateUI();
      return;
    }

    applyResolvedEvent(baseResolvedEvent);
  }

  function autoRunActiveLoop() {
    if (!state || state.status !== 'active') {
      return;
    }

    if (state.pendingEvent) {
      receiptOutput.textContent = 'Cannot auto-run while a pending event is waiting in step-by-step mode. Apply or discard it first.';
      return;
    }

    let guard = 0;
    while (state && state.status === 'active' && guard < 20) {
      const event = buildResolvedEventForCurrentPhase();
      if (!event) {
        break;
      }
      applyResolvedEvent(event);
      guard += 1;
    }
  }

  function applyCompliance() {
    if (!state || state.status !== 'active' || state.complianceUsedThisPhase) {
      return;
    }

    state.stats.battery = clamp(
      state.stats.battery + complianceRule.battery_delta,
      batteryConfig.min,
      batteryConfig.max
    );

    state.stats.stability = clamp(
      state.stats.stability + complianceRule.stability_delta,
      stabilityConfig.min,
      complianceRule.stability_cap
    );

    state.complianceUsedThisPhase = true;

    if (!applyBatteryHardStop()) {
      updateUI();
    }
  }

  function startSession() {
    state = {
      sessionId: 'loop-' + Date.now(),
      status: 'active',
      phaseIndex: 0,
      phaseRolled: false,
      complianceUsedThisPhase: false,
      thresholdTriggered: false,
      stepMode: Boolean(stepModeToggle.checked),
      pendingEvent: null,
      runningProbability: 1,
      stats: {
        battery: batteryConfig.start,
        stability: stabilityConfig.start,
        sip: sipConfig.start
      },
      events: []
    };

    receiptOutput.textContent = 'Loop in progress...';
    renderEventLog();
    updateUI();
  }

  function simulateLoopForBatch() {
    const sim = {
      stats: {
        battery: batteryConfig.start,
        stability: stabilityConfig.start,
        sip: sipConfig.start
      },
      runningProbability: 1,
      thresholdTriggered: false,
      endedBy: 'return_phase_complete',
      rolledEventCount: 0
    };

    for (let i = 0; i < phases.length; i += 1) {
      const roll = Math.floor(Math.random() * 100) + 1;
      const event = data.random_events.events.find(e => e.roll === roll);

      if (!event) {
        continue;
      }

      sim.stats.battery = clamp(
        sim.stats.battery + Number(event.battery_delta),
        batteryConfig.min,
        batteryConfig.max
      );

      sim.stats.stability = clamp(
        sim.stats.stability + Number(event.stability_delta),
        stabilityConfig.min,
        stabilityConfig.max
      );

      sim.runningProbability = sim.runningProbability * Number(event.default_probability);
      sim.rolledEventCount += 1;

      if (!sim.thresholdTriggered && sim.runningProbability <= thresholdDecimal) {
        sim.thresholdTriggered = true;
        sim.stats.stability = clamp(
          sim.stats.stability + thresholdEffect.stability_delta,
          stabilityConfig.min,
          stabilityConfig.max
        );
        sim.stats.sip = Math.max(sipConfig.min, sim.stats.sip + thresholdEffect.sip_delta);
      }

      if (sim.stats.battery <= batteryConfig.min) {
        sim.stats.battery = batteryConfig.min;
        sim.endedBy = 'battery_zero_hard_stop';
        break;
      }
    }

    return sim;
  }

  function runBatchSimulation() {
    const requested = Number(batchCountInput.value);
    const loopCount = Number.isFinite(requested)
      ? Math.max(1, Math.min(5000, Math.floor(requested)))
      : 100;

    batchCountInput.value = String(loopCount);

    let thresholdCount = 0;
    let hardStopCount = 0;
    let completeCount = 0;
    let sumBattery = 0;
    let sumStability = 0;
    let sumSip = 0;
    let sumProbability = 0;

    for (let i = 0; i < loopCount; i += 1) {
      const result = simulateLoopForBatch();
      thresholdCount += result.thresholdTriggered ? 1 : 0;
      hardStopCount += result.endedBy === 'battery_zero_hard_stop' ? 1 : 0;
      completeCount += result.endedBy === 'return_phase_complete' ? 1 : 0;
      sumBattery += result.stats.battery;
      sumStability += result.stats.stability;
      sumSip += result.stats.sip;
      sumProbability += result.runningProbability;
    }

    const summary = {
      loop_count: loopCount,
      threshold_trigger_rate: Number((thresholdCount / loopCount).toFixed(4)),
      ended_by: {
        return_phase_complete: completeCount,
        battery_zero_hard_stop: hardStopCount
      },
      averages: {
        final_battery: Number((sumBattery / loopCount).toFixed(3)),
        final_stability: Number((sumStability / loopCount).toFixed(3)),
        final_sip: Number((sumSip / loopCount).toFixed(3)),
        running_success_probability: Number((sumProbability / loopCount).toFixed(6))
      }
    };

    batchOutput.textContent = JSON.stringify(summary, null, 2);
  }

  startBtn.addEventListener('click', startSession);
  rollBtn.addEventListener('click', rollPhaseEvent);
  autoRunBtn.addEventListener('click', autoRunActiveLoop);
  runBatchBtn.addEventListener('click', runBatchSimulation);
  applyPendingBtn.addEventListener('click', () => {
    if (!state || state.status !== 'active' || !state.pendingEvent) {
      return;
    }

    const probability = Number(overrideProbability.value);
    const batteryDelta = Number(overrideBatteryDelta.value);
    const stabilityDelta = Number(overrideStabilityDelta.value);

    const resolvedEvent = {
      phaseId: state.pendingEvent.phaseId,
      phaseName: state.pendingEvent.phaseName,
      roll: state.pendingEvent.roll,
      prompt: state.pendingEvent.prompt,
      category: state.pendingEvent.category,
      probability: Number.isFinite(probability) && probability >= 0 ? probability : state.pendingEvent.probability,
      batteryDelta: Number.isFinite(batteryDelta) ? batteryDelta : state.pendingEvent.batteryDelta,
      stabilityDelta: Number.isFinite(stabilityDelta) ? stabilityDelta : state.pendingEvent.stabilityDelta
    };

    clearPendingEvent();
    applyResolvedEvent(resolvedEvent);
  });
  cancelPendingBtn.addEventListener('click', () => {
    if (!state || state.status !== 'active') {
      return;
    }
    clearPendingEvent();
    updateUI();
  });
  stepModeToggle.addEventListener('change', () => {
    if (state && state.status === 'active') {
      state.stepMode = Boolean(stepModeToggle.checked);
      if (!state.stepMode) {
        clearPendingEvent();
      }
      updateUI();
    }
  });
  complianceBtn.addEventListener('click', applyCompliance);
  endBtn.addEventListener('click', () => {
    if (state && state.status === 'active') {
      endLoop('manual_stop');
    }
  });

  updateUI();
})();
</script>
