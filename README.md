# ENCS4380 Homework 1: Dynamic Characteristics Interactive Toolkit

Interactive web toolkit that makes the dynamic characteristics of sensors visible (first-order and second-order response). Built for ENCS4380 Interfacing Techniques, Birzeit University (Instructor: Dr. Wasel Ghanem).

**Live site:** https://sereen-karakra.github.io/encs4380-dynamics-42/

## Team

|    Member         |             Responsibility                | Issue | Status |
|-------------------|-------------------------------------------|-------|--------|
| Maysam Abu Eid    | Module 1: First-order time response       |   #2  | Done (live) |
| Dania Abu Ayyash  | Module 2: First-order frequency response  |   #3  | Done   |
| Sereen Karakra    | Module 3: Second-order response           |   #1  | Done   |
| Raneem Khawaja    | Module 4: "Guess the sensor" challenge    |   #3  | Done   |
| Masa Awad         | Bonus: own ODE solver (Euler and RK4) vs closed-form (`bonus.html`) |  #4   | Done   |

## Modules

### Module 1: First-order time response (`index.html`)
Thermometer model: τ·dy/dt + y = K·x(t), G(s) = K / (τs + 1).

- Sliders for gain K, time constant τ, and input amplitude/ramp rate; input type is step or ramp.
- Time-domain plot that redraws instantly (input, ideal output, sensor output).
- Step: markers at t = τ (63.2% of KA) and t = 3τ (95% of KA).
- Ramp: lag = τ and steady-state error = K·A·τ, shown on the plot and in the metrics.
- Error-fraction plot: ln(e(t)/e(0)) against t is a straight line with slope −1/τ; the measured slope is compared with the theory.
- "Predict, then check" box: the user picks an answer first, then checks it.
- Validation table with expected value, measured value, and PASS/FAIL.

Validation checks currently passing on the page: y(τ) = 0.632·KA, y(3τ) = 0.95·KA, ramp steady-state error = K·A·τ, ramp lag = τ, log-plot slope = −1/τ.

### Module 2: First-order frequency response (`module2.html`)
Implemented in this project package (push to GitHub before the 9 Nov checkpoint).

- Live τ, input frequency (Hz), gain K, and amplitude sliders; input/output steady-state sine plots.
- Normalized amplitude ratio M, phase lag, output amplitude KAM, signed dynamic error δ = M − 1.
- Log-frequency Bode magnitude and phase plots, with ωc = 1/τ marked.
- Dynamic-error calculator: maximum allowable τ at a selectable frequency/error limit.
- Predict-then-check interaction and independent validation cases from Homework 1 (0.93, 21.8°, 0.52 ms, 9.3°).

The sine plot uses the **steady-state** solution; it intentionally omits the start-up transient.

## Module 3: Second-order response (module3.html)

Mass-spring-damper model: m·x″ + b·x′ + k·x = F, G(s) = K·ωn² / (s² + 2ζωn·s + ωn²), with K = 1/k, ωn = √(k/m), ζ = b / (2√(km)).

- Sliders for mass m, damping b, stiffness k, and step force F; all plots and numbers update live.
- Shows ωn, ζ, the damping case (underdamped, critically damped, overdamped), DC gain K, and the final value F/k.
- Step response x(t) from the closed-form solution for each damping case, with the final value line and the peak marked.
- Metrics read from the plotted curve: rise time (10–90%), peak time, overshoot, and 2% settling time, shown next to the theoretical overshoot and peak time.
- Pole plot in the s-plane: complex pair for ζ < 1, real poles for ζ ≥ 1.
- State-space panel: x1 = x, x2 = x′, with matrices A, B, C and the eigenvalues of A, which match the poles of G(s).
- Phase plane (x1, x2) computed with our own RK4 integrator: a spiral when underdamped, no spiral when overdamped.
- "Predict, then check" box: what happens to the overshoot when damping b increases.
- Validation table with expected value, our value, and PASS/FAIL: ζ = 0.5 overshoot (16.3 %), ζ = 1 has no overshoot, and eigenvalues of A equal the poles (−1 ± j1.732 for m = 1, b = 2, k = 4).
- The number of plot points is increased for very low damping so the oscillations are drawn smoothly.
  
### Module 4: "Guess the sensor" challenge (`module4.html`)

- Random first-order or underdamped second-order sensors.
- First-order challenges use a unit step or a steady-state sine input.
- Second-order challenges use a unit step.
- Measured responses include small random noise.
- Users estimate tau, or zeta and omega n.
- After submission, the true parameters are revealed and the true
  and estimated responses are plotted together.
- Each required parameter must be within 10% for full marks.
- Outside the tolerance, the score decreases with the largest
  relative parameter error, down to a minimum of zero.
- One guess per sensor, with hints and a New Sensor button.
- The running score is stored in sessionStorage for the browser tab.
- Responsive layout for desktop and mobile screens.

### Bonus: Own ODE solver vs closed-form (`bonus.html`)
Our own numerical solver for the first-order sensor ODE τ·dy/dt + y = K·A, y(0) = 0, compared with the exact step response y(t) = K·A·(1 − e^(−t/τ)). This is the "your own ODE solver (Euler or RK4), plotted against the closed-form curve" bonus option.

- Both Euler and RK4 are implemented from scratch in JavaScript (no solver library).
- Sliders for gain K, time constant τ, step amplitude A, and step size h.
- Plot of the exact curve, the Euler points, and the RK4 points.
- Log-scale error plot |numerical − exact| for both methods, and metrics for the maximum error of each (plus the number of steps and h/τ).
- "Predict, then check" box on how the errors change when h is halved: Euler is first-order (error ∝ h), RK4 is fourth-order (error ∝ h⁴).

## Opening and navigation

Open `index.html` or the GitHub Pages home URL. Use the module navigation across the top to open Module 2 or Module 3. Module 4 is available through the navigation as "Guess the sensor", and the bonus page as "Bonus · ODE solver" (`bonus.html`).

## Screenshots

<img width="1528" height="294" alt="image" src="https://github.com/user-attachments/assets/5d845cf1-8dbd-4ba4-844e-ce5fd11b898d" />

<img width="1540" height="591" alt="image" src="https://github.com/user-attachments/assets/39edc31c-b975-40eb-8518-4b3b8ba8250d" />

<img width="1525" height="572" alt="image" src="https://github.com/user-attachments/assets/243c2e76-2b94-48f2-af9b-3d14dadfd61a" />
<img width="626" height="288" alt="image" src="https://github.com/user-attachments/assets/cf34041f-bfd3-41f7-a566-e8cb55f3a2e5" />


<img width="1526" height="171" alt="image" src="https://github.com/user-attachments/assets/a58bdf24-859d-4d20-8fdf-4e5b36e23a57" />
<img width="1521" height="665" alt="image" src="https://github.com/user-attachments/assets/55b234f3-4785-4534-9dd3-610fee6af890" />
<img width="1519" height="577" alt="image" src="https://github.com/user-attachments/assets/69a150d4-3ad7-4d56-a904-991f9cfe8010" />

<img width="648" height="282" alt="image" src="https://github.com/user-attachments/assets/10816c70-94c1-4ab8-97c2-a3715dfd5f92" />

<img width="1290" height="809" alt="image" src="https://github.com/user-attachments/assets/639dcfff-6569-48e0-9656-6eb5111cacca" />


## Technical notes

- Static site on GitHub Pages: plain HTML and JavaScript, no server or login needed.
- Plots use the closed-form responses from the lecture slides, drawn with [Chart.js](https://www.chartjs.org/).
- The bonus page also uses numerical solutions (Euler and RK4) written by us and compared against the closed-form curve.
- Work is tracked with one GitHub Issue per module, assigned to its owner.

## AI use

We used an AI assistant (Claude) as allowed by the homework. Maysam used it to review the Module 1 code and fix errors (ramp steady-state error for K ≠ 1, the error-fraction plot, markers, and the validation table), and to help write the issue and this README. Every member must be able to explain their own code and equations in the demo.
Sereen used Claude to review the Module 3 code (equations, poles, eigenvalues, RK4) and to find and fix an under-sampling problem in the plots for very small damping. She can explain the model, the equations, and the plots in the demo.
Raneem used ChatGPT for coding assistance, debugging, and explanations in Module 4.
Masa used Claude to help build the bonus page (`bonus.html`): the Euler and RK4 implementation, the error plot, and the "Predict, then check" box. She checked the results against the closed-form formula and can explain the solver steps and error orders in the demo.

## Timeline

| Date | Milestone |
|---|---|
| Tue 3 Nov 2026 | Checkpoint 1: Pages live, Module 1 working |
| Mon 9 Nov 2026 | Checkpoint 2: Modules 2 and 3 working |
| Thu 12 Nov 2026 | Final release v1.0 |
| Sun 15 and Mon 16 Nov 2026 | Group demos |
