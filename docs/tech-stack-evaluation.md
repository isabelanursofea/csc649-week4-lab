# Tech Stack Evaluation

## Project
PillPal: An Intelligent Mobile-based Pill Identification System for Unlabelled Pills

## Requirements that drive the decision
- FR1: The system identifies a loose pill from a camera photo and shows its name and information.
- FR2: The user can keep a medication list with schedule reminders.
- NFR1: An identification result is returned within 5 seconds on a normal Wi-Fi connection.
- NFR2: The app runs on an Android phone and is simple enough for older adults to use.
- NFR3: The system can be built by one student, with free tools, before the project deadline.

## Options
- Option A: Flutter app plus a FastAPI server that runs the YOLOv8 model.
- Option B: Flutter app with the model converted to run on the phone (TFLite), with no server.
- Option C: Expo (React Native) app plus a FastAPI server that runs the YOLOv8 model.

## Decision matrix
Weight: how important the criterion is for YOUR project (1 = low, 5 = high).
Score: how well each option does (1 = poor, 5 = excellent).
Weighted score = weight x score. Add them up for each option.

| Criterion                          | Weight | A score | B score | C score |
|------------------------------------|--------|---------|---------|---------|
| Fits my requirements               | 5      | 5       | 3       | 5       |
| Skills I already have              | 4      | 3       | 2       | 4       |
| Time to build before my deadline   | 5      | 3       | 2       | 4       |
| Free hosting and tools             | 3      | 4       | 5       | 4       |
| Performance and security needs     | 4      | 4       | 5       | 4       |
| Room to grow later                 | 2      | 4       | 4       | 3       |
| **Total (weighted)**               |        | **88**  | **76**  | **95**  |

## Decision record
- **Context:** I am building a mobile app that identifies unlabelled pills from a photo. I am working alone with a fixed deadline, a free-tools budget, and existing Expo code for the planner. The YOLOv8 model is easier to run on a server than to convert for a phone, and offline use is out of scope.
- **Decision:** Option C, an Expo app that sends the photo to a FastAPI server running the YOLOv8 classification model.
- **Reasons:** (1) It meets FR1 and NFR1, because a server runs the full model and returns a result quickly. (2) It meets NFR3, because I can reuse my existing Expo planner code and I know it better than Flutter. (3) It scored highest in the matrix (95), ahead of Option A (88) and Option B (76), mainly because of my skills and the time I have.
- **Consequences:** Easy: training and updating the model on the server, and reusing my planner. Hard: the app does not work without a network connection, and the photo leaves the phone, so I must state this in the privacy note and keep the photos off permanent storage.
- **Risks and next review:** The server may not be reachable on demo day, and reminders may be unreliable under Android 13 battery settings. I will test the server connection and the reminders on my Samsung A32 in the first prototype, and review this decision if either fails, or if offline use becomes a requirement (then Option B).