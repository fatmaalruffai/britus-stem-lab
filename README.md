# Britus Education Virtual STEM Lab

One website for all grades (KG–Grade 12). Students sign in with their name, school and grade, then open the interactive STEM projects for their grade: build the model, wire it, code it and test it in the browser. Each project unlocks after the previous one is finished. Teachers open a dashboard to follow every student's progress.

This project is made as a virtual lab for the **STEM Nexus Arabia curriculum**.

**Concept & Development Lead:** Fatma Alruffai, Britus Education

## Projects

| Grade | Order | Project | Folder |
|---|---|---|---|
| 3 | 1 | Levers (Simple Machines, Project 6) | `labs/levers/` |
| 3 | 2 | Little Lever Builder (homework) | `labs/little-lever-builder/` |
| 4 | 1 | Power Up the Toys | `labs/power-toys/` |
| 4 | 2 | Battery Builder (homework) | `labs/battery-builder/` |
| 5 | 1 | Plants and Pollinators (Project 3) | `labs/pollinators/` |
| 5 | 2 | Virtual Robotics Lab | `labs/robotics/` |
| 9 | 1 | Joints (Project 1) | `labs/joints/` |
| 9 | 2 | Build a Mixer (Project 8: Moments) | `labs/mixer/` |

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
- `SETTINGS.adminPassword`: the Britus admin password that sees all schools (temporary)
- `SETTINGS.apiUrl`: the server address (empty = this device only)
- `PROJECTS`: which projects each grade has, in order

## Acknowledgments

- **three.js** (MIT licence) for the 3D models.
- **LEGO®, WeDo 2.0** and **Kidsuno** are trademarks of their owners, named only to describe the physical kits the models are based on.
- **GoatCounter** for anonymous visit counts.

© 2026 Britus Education · Fatma Alruffai
