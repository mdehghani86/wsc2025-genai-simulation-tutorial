# WSC 2025 — GenAI + Simulation Tutorial: ER SimPy Model

Source code for the Emergency Room (ER) discrete-event simulation generated
from the structured prompt in **Figure 8** of:

> Dehghanimohammadabadi, M., Belsare, S., and Sadeghi, N. (2025).
> *A Tutorial on Generative AI and Simulation Modeling Integration.*
> Proceedings of the 2025 Winter Simulation Conference.
> https://www.informs-sim.org/wsc25papers/inv205.pdf

## Run

```bash
pip install simpy
python er_simulation.py
```

## What it does

* Patients arrive ~ Exponential(mean = 6 min) and are triaged with severity 1–10.
* Severity ≥ 7 → `CriticalCareBeds` (treatment ~ Triangular(20, 30, 45)).
* Severity < 7 → `StandardBeds` (treatment ~ Triangular(10, 15, 25)).
* Selection strategies via `select_next_patient(waiting_list, strategy)`:
  * `FIFO`
  * `ShortestExpectedTreatment` (severity-based proxy)
* Per-patient metrics: time in system, wait time, treatment time.
* Per-resource metrics: utilization, queue length, served count.
* All events logged with timestamp, patient ID, and description.

## Configure

Edit the `settings` dict passed to `run_experiment()`:

```python
run_experiment({
    "arrival_mean":       6.0,
    "critical_beds":      2,
    "standard_beds":      4,
    "selection_strategy": "ShortestExpectedTreatment",
    "n_replications":     3,
    "duration":           500.0,
})
```
