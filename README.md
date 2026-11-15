# Britus Education Virtual STEM Lab

One website for all grades (KG–Grade 12). Students sign in with their name, school and grade, then open the interactive STEM projects for their grade: build the model, wire it, code it and test it in the browser. Each project unlocks after the previous one is finished. Teachers open a dashboard to follow every student's progress.

This project is made as a virtual lab for the **STEM Nexus Arabia curriculum**.

**Concept & Development Lead:** Fatma Alruffai, Britus Education

## Projects

| Grade | Project | Folder |
|---|---|---|
| 3 | Levers (Simple Machines, Project 6) | `labs/levers/` |
| 3 | Little Lever Builder (homework) | `labs/little-lever-builder/` |
| 4 | Power Up the Toys | `labs/power-toys/` |
| 4 | Battery Builder (homework) | `labs/battery-builder/` |
| 4 | Ring the Bell (Project 4, Early Electronics Kit) | `labs/bell/` |
| 5 | Plants and Pollinators (Project 3) | `labs/pollinators/` |
| 5 | Cleaning the Ocean (Project 4, LEGO WeDo 2.0) | `labs/ocean/` |
| 5 | Sort to Recycle (Project 5, LEGO WeDo 2.0) | `labs/recycle/` |
| 5 | Virtual Robotics Lab | `labs/robotics/` |
| 7 | Touchless Hand Wash Timer | `labs/handwash/` |
| 7 | Touchless Inventions | `labs/touchless/` |
| 7 | Conductivity Meter | `labs/conductivity/` |
| 9 | Joints (Project 1) | `labs/joints/` |
| 9 | Weight Machine (Project 2) | `labs/weightmachine/` |
| 9 | Energy Wheel (Project 3) | `labs/energywheel/` |
| 9 | Gold Foil Experiment (Project 4) | `labs/goldfoil/` |
| 9 | Chromatography | `labs/chromatography/` |
| 9 | Build a Mixer (Project 8: Moments) | `labs/mixer/` |
| 9 | Reflection (Project 10) | `labs/reflection/` |
| 9 | Wind Turbines (Project 12) | `labs/windturbines/` |
| 9 | Weather Seesaw (Project 13) | `labs/weatherseesaw/` |
| 11 | Raspberry Pi Pico Lab (Lessons 1–3: Meet the Pico, Blinking LED, Temperature Sensor) | `labs/picolab/` |

Students sign in with two names (first name and father's name), their school, grade and the school's student password.

Other grades show "Coming soon". Projects and their order are set in the `PROJECTS` list in `index.html`.

## How it works

- **Front end only.** `index.html` is the portal. Each lab is a single static HTML file (HTML, CSS, JavaScript). The 3D labs load three.js r128 from cdnjs. No build step.
- **Student data** is saved in the browser (`localStorage`) under three keys:
  - `britusStudent`: the signed-in student `{id, name, school, grade, joined}`
  - `britusStudents`: every student who signed in on this device, by id
  - `britusLab:v1`: progress `{ studentId: { labs: { labId: { step, done, updated } } } }`
- **Each lab** has a short script at the end of the file (marked "Britus Virtual STEM Lab") that records the student's current step and when the project is finished, and adds a "← My projects" button.
- **Teacher dashboard:** filters by school, grade, status and name, with an Excel (CSV) download. Each school has its own password and sees only its own students; an admin password sees all schools. Passwords are set in `SETTINGS.schools` and `SETTINGS.adminPassword`. This is a front-end check only (anyone can read the page source) and must be replaced by a real login.
- **Analytics:** anonymous page and step counts with GoatCounter (no cookies, no personal data).

## For IT: connecting a server and school login

All student data goes through one object, `Data`, in `index.html`. To save data centrally:

1. Host the whole folder on the school server or cloud hosting, behind school sign-in (Microsoft Entra ID / Google Workspace SSO), so only students and staff can open it.
2. Set `SETTINGS.apiUrl` in `index.html` to your API, for example `https://lab.school.edu/api`.
3. Provide these endpoints (JSON, cookies/credentials included):

| Method | Path | Body / response |
|---|---|---|
| `POST` | `/students` | `{id, name, school, grade, joined}` |
| `POST` | `/progress` | `{studentId, labs: {labId: {step, done, updated}}}` |
| `GET` | `/progress` | `[{student: {...}, labs: {...}}]` for the teacher dashboard |

With SSO in place, the student's identity can come from the login instead of the sign-in form, and the school passwords can be replaced by a staff role.

## Settings to edit

In `index.html`, at the top of the script:

- `SETTINGS.schools`: the school names students choose from
- `SETTINGS.schools`: school names and each school's teacher password (temporary)
- `SETTINGS.studentPassword`: the student login password (capitals and spaces do not matter)
- `SETTINGS.adminPassword`: the Britus admin password that sees all schools (temporary)
- `SETTINGS.apiUrl`: the server address (empty = this device only)
- `PROJECTS`: which projects each grade has, in order

## Acknowledgments

- **three.js** (MIT licence) for the 3D models.
- **LEGO®, WeDo 2.0** and **Kidsuno** are trademarks of their owners, named only to describe the physical kits the models are based on.
- **GoatCounter** for anonymous visit counts.

© 2026 Britus Education · Fatma Alruffai

## Credits

LEGO® and WeDo are trademarks of the LEGO Group. The building step pictures in Cleaning the Ocean are © The LEGO Group, shown for classroom use.
