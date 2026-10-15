# StudyPilot: Adaptive Practice for Math and Science

StudyPilot is an adaptive learning prototype inspired by tools such as Carnegie Learning's MATHia. It tracks a student's quiz answers, estimates how well they know each topic, finds the weakest topics and serves customised practice problems.

Built for **IBM SkillsBuild Masterclass 5: Creating Real Life Projects**.

## Screenshots

| Home | Dashboard |
|---|---|
| ![Home screen](screenshots/01-home.png) | ![Mastery dashboard](screenshots/05-dashboard.png) |

More screens (feedback, hints, focus mode, dark mode, mobile) are in the [`screenshots`](screenshots) folder and in [`docs/StudyPilot_Project_Screenshots.pdf`](docs/StudyPilot_Project_Screenshots.pdf).

## Features

- **Diagnostic start:** one quick level 1 problem per topic, so the engine learns the student's level.
- **Mastery tracking:** a score for each topic, updated after every answer with Bayesian Knowledge Tracing.
- **Adaptive recommendations:** the next problem comes from the weakest topic, at a difficulty that matches mastery. Each problem shows why it was chosen.
- **Unlimited problems:** numbers are generated randomly for each of 5 topics (linear equations, percentages, speed and motion, Ohm's law, area), covering both math and science.
- **Dashboard:** overall readiness score, coloured mastery bars (red = weak, amber = developing, green = strong), trend lines, a "focus next" suggestion and a recent-answers log.
- **Hints:** a hint button; a correct answer after a hint does not raise mastery.
- **Practice focus:** adaptive mode, or drill a single topic.
- **Light and dark themes**, and a responsive layout for phones.
- Progress is saved in the browser (`localStorage`). There is no backend.

## How it works

1. **Mastery model (Bayesian Knowledge Tracing).** Each topic starts at P(known) = 0.30. After an answer the probability is updated using slip (0.10) and guess (0.30, 0.20 or 0.10 for levels 1 to 3) values, then a learning step of 0.15 is applied.
2. **Difficulty.** Mastery below 40% gives level 1 problems, below 70% gives level 2, and 70% or more gives level 3.
3. **Recommender.** Topics with no history come first. After that the engine picks the lowest-mastery topic, with a small chance of choosing the second-weakest, and it moves on if the same topic has been served three times in a row.

The model parameters are starting guesses, not values fitted to real student data.

## Run it

No build step is needed. Open `index.html` in a browser.

To publish it with GitHub Pages: **Settings > Pages > Build and deployment > Deploy from a branch**, choose `main` and the `/ (root)` folder, then save. The app will be served at `https://<your-username>.github.io/<repo-name>/`.

## Project files

```
index.html                      the app (HTML, CSS and JavaScript in one file)
screenshots/                    screenshots of the running app
docs/
  StudyPilot_Lean_Canvas.pdf
  StudyPilot_Concept_Note.pdf
  StudyPilot_Presentation.pptx
  StudyPilot_Project_Screenshots.pdf
```

## Ideas for next steps

- A teacher dashboard that compares students and shows weak topics across a class
- Worked solutions after each answer
- More topics (fractions, force and motion) and a teacher-reviewed question bank
- A Python backend (FastAPI) with a database, and fitting the model parameters to real answer data
