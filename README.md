# Where does your battery % come from?

An interactive browser simulation of how a fuel gauge estimates the battery percentage shown by a phone. Built for the Global Virtual Hackathon 2026 theme **Unveiling Technology**.

## Run locally

Open [index.html](index.html) in a current browser. The simulation has no build step, external scripts, sign-in, or API key. See the [written project page](project.html). The narrated demo video accompanies the hackathon submission.

## Try it

1. Click **Check battery**. At the default inputs, follow the estimate from a 3.816 V resting reading to **42%** in the status bar.
2. Keep the same resting voltage and run a separate check at **0 min**. This run shows the starting estimate of **47%** because it includes zero charge used. The 10-minute and 0-minute checks both start from that same estimate.
3. Use **Detailed version** for the explanation of each phase, or toggle **X-ray**, **Power path**, and **Data path** to inspect the phone and its circuit.

## How the estimate works

`estimateBattery()` in `index.html` looks up an initial state of charge by interpolating measured resting voltages. It converts simulated shunt readings to current with Ohm’s law and adds current × time across the intervals. It subtracts the used charge, divides by full-charge capacity, and rounds the reported result. The playback draws each phase using those calculated values.

The resting-voltage profile comes from [Analog Devices’ lithium-ion cell characterization](https://www.analog.com/en/resources/design-notes/characterizing-a-lithiumion-li-cell-for-use-with-an-opencircuitvoltage-ocv-based-fuel-gauge.html). The [Texas Instruments bq27441-G1 datasheet](https://www.ti.com/lit/ds/symlink/bq27441-g1.pdf) illustrates real fuel-gauge hardware and communication. The current samples, 3,000 mAh capacity, and 75 mΩ cell resistance are simulated. The app uses a simplified model to show the estimation process.

## Development

AI tools helped develop and review the demo. The battery model runs directly in browser JavaScript. The video uses synthetic narration generated locally with [Piper’s Joe voice](https://huggingface.co/rhasspy/piper-voices/blob/main/en/en_US/joe/medium/MODEL_CARD).
