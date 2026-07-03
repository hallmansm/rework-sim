# Flow Simulation — the Rework Backwash Effect

A single-file discrete event simulation showing why a team with 33% rework
isn't "33% slower" — it's past a queueing cliff.

**Run it:** open [the live simulator](https://hallmansm.github.io/rework-sim/) —
or just download `index.html` and double-click it. No install, no build, no dependencies.

## The model

- Work arrives at rate **λ** per day; the team processes **μ** items per day.
- A fraction **d** of completed items come back as defects and re-enter
  through the same door as new work.
- Expected passes per shipped item = 1 + d + d² + … = **1/(1−d)** — a
  geometric series. Effective arrival is λ/(1−d).
- Utilization ρ = λ/((1−d)·μ). The system is stable only while ρ < 1, so the
  critical defect rate is **d\* = 1 − λ/μ: your rework budget is exactly your
  slack.** Past it there is no steady state — the backlog grows every day,
  forever, and lead time becomes a function of the calendar, not of the work.

Watch it happen: start at d=0 (stable), set d=0.10 (the edge, at λ=9 μ=10),
then d=0.33 (collapse — the defect queue drains fine because rework cuts the
line, and the displacement lands in the product backlog, permanently).

## Credits

Concept and model: Steve Hallman ([The Agile Couch](https://theagilecouch.com)).
Built with Claude. Visual layout inspired by Michel Grootjans'
[explaining-flow](https://github.com/michelgrootjans/explaining-flow) —
a complementary simulator for team topology and WIP limits (his has no rework
loop; this one is single-stage with a rework loop; use both).
