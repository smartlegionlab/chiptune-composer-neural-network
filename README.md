# chiptune-composer-neural-network

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/smartlegionlab/chiptune-composer-neural-network)](https://github.com/smartlegionlab/chiptune-composer-neural-network/releases)
![GitHub top language](https://img.shields.io/github/languages/top/smartlegionlab/chiptune-composer-neural-network)
[![GitHub](https://img.shields.io/github/license/smartlegionlab/chiptune-composer-neural-network)](https://github.com/smartlegionlab/chiptune-composer-neural-network/blob/master/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/smartlegionlab/chiptune-composer-neural-network?style=social)](https://github.com/smartlegionlab/chiptune-composer-neural-network/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/smartlegionlab/chiptune-composer-neural-network?style=social)](https://github.com/smartlegionlab/chiptune-composer-neural-network/network/members)
![Neural Network](https://img.shields.io/badge/neural%20network-MLP-00d2ff)
![From Scratch](https://img.shields.io/badge/from%20scratch-100%25-4fc3f7)
![Pure JavaScript](https://img.shields.io/badge/pure%20JavaScript-ES6-f7df1e)
![Web Audio API](https://img.shields.io/badge/audio-Web%20Audio%20API-9cf)
![8-bit Chiptune](https://img.shields.io/badge/music-8--bit%20chiptune-ff7043)
![Live Generation](https://img.shields.io/badge/live-streaming-00e676)
![Model Export](https://img.shields.io/badge/model-export%20%2F%20import-00c853)

An interactive **8-bit chiptune composer** driven by a real multilayer perceptron (MLP) written **from scratch in pure JavaScript**. No frameworks, no libraries, no audio samples - every note is synthesized live in the browser with the Web Audio API.

---

## Overview

This standalone application implements the full training pipeline by hand - forward pass, error backpropagation, weight updates with gradient descent - and then streams an endless, always-in-key chiptune melody with bass and drums. The network has **two shared-hidden heads**: it predicts the next pitch class and, per bar, one of four rhythm grooves for the bass + drums.

Everything you hear is generated in real time. The neuron activation, weight magnitudes and the loss graph reflect the actual state of the network.

---

## Feature summary

- **Networks trained from scratch** in plain JavaScript (sigmoid activation, backpropagation, mini-batch SGD / Adam).
- **Multi-head output** - one hidden layer, two heads: pitch class (12 notes) and rhythm groove (4 per bar).
- **Native Web Audio engine** - square, triangle and noise voices, echo/delay feedback, low-pass, per-channel mutes and a master volume; no samples are loaded.
- **Live streaming** - the composer runs forever, locked to the chosen key and a chord progression, with an on-screen note roll.
- **Record to .wav** - capture the 16-bit PCM recording and download it.
- **Live visualization** - neurons as pulsing orbs (brightness = activation), synapses by weight sign and magnitude, plus pitch-probability bars.
- **Model persistence** - export / import the trained composer as a JSON file.
- **Responsive layout** - 3-column panels on desktop/landscape, single column in portrait.
- **Built-in Help and About** dialogs.

---

## Getting started

### Run with a local server

The application is split into an HTML file, a stylesheet and a script, so **opening the HTML file directly by double-click will not work** - serve the folder over HTTP:

```bash
python -m http.server 8000
```

then open [http://localhost:8000](http://localhost:8000). Any static server works (for example `npx serve` or a GitHub Pages deployment). No build step, no package manager, and no internet connection is required.

### How to use

1. Press **Play** - it unlocks Audio and starts live composition.
2. Record: **REC** → **Stop** → **Download** (.wav); **Reset** clears.
3. Adjust **Master Volume** and **Mute All / Unmute All**; each channel has its own Mute.
4. Choose **Key / Tempo / Temperature / Lead Density / Model influence / Echo**.
5. The network picks the melody and a per-bar rhythm groove for bass and drums, locked to the key and a chord progression.
6. **Copy Stats** / **Export / Import** saves and loads the trained composer as JSON.

---

## Architecture

- **Network**: 53 inputs → 48 sigmoid hidden neurons → 12 pitch-class outputs + a rhythm head (4 grooves).
- **Loss**: cross-entropy with softmax, trained by mini-batch SGD (momentum 0.9) or Adam, with weight decay and gradient/weight clipping.
- **Melody**: generated from the network distribution blended with the chord/scale model and temperature-sampled, always staying in key.

An educational demo of live music generation - every note is synthesized in the browser and the piece stays in key and follows a chord progression.

---

## License

This project is licensed under the **BSD 3-Clause License** - see [LICENSE](LICENSE).

---

**Author:** Alexander Suvorov · **Repository:** [github.com/smartlegionlab/chiptune-composer-neural-network](https://github.com/smartlegionlab/chiptune-composer-neural-network)

