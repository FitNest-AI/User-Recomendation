## How to run this API on your local machine 💻
If you want to run this API Server on your local machine, you need to do these steps:
- First, clone this repository. `git clone https://github.com/FitNest-AI/Workout-Recomender.git`
- Second, open the terminal and go to this project's root directory.
- Third, type `pip install requirement.txt` in your terminal and hit enter button.
- Fourth, type `flask run` in your terminal and hit enter button.
- Finally, the server will run on your http://127.0.0.1:5200

## How to deploy this API to Cloud Run 🚀
If you want to deploy this API server to Cloud Run, you need to follow this steps:
- First, open your Google Cloud Console. https://console.cloud.google.com/
- Second, open the Cloud Shell at the right top corner in the Google Cloud Console. Make sure you enable Cloud Run API and Cloud Build API before.
- Third, copy the command below to cloning this repository into the Cloud Shell.
 ```
git clone https://github.com/FitNest-AI/Workout-Recomender.git
 ```

- Fourth, go to this project's root directory in the Cloud Shell.
```
cd Workout Recomender
export PROJECT_ID= <Your GCP project ID>
```
- Fifth, add the .env file with Variables to the Workout Recomender folder
```
MONGO_URI: <your MONGO_URI>
SECRET_KEY: <your SECRET_KEY>
```

- Sixth, copy the command below to build the image container and upload it to the Container Registry.
 ```
gcloud builds submit \
  --tag asia.gcr.io/$PROJECT_ID/workout-recomender
  ```
- seventh, copy the command below to deploy your image container to Cloud Run.
 ```
 gcloud run deploy fitnest-backend \
  --image asia.gcr.io/$PROJECT_ID/workout-recomender \
  --platform managed \
  --cpu=1 \
  --memory=512Mi \
  --region asia-southeast2 \
  --allow-unauthenticated \
  --max-instances=3 \
  --port=5200
 ```
- Finally, your API server will be deploy to Cloud Run and you will get the URL in the Cloud Shell to access the your server.

## Fetch workout Recommendation

**HTTP Request**

```
    GET /?q={{workout_name}}&page={{page}}
```

**Query**

| Parameter | Description                     |
| :-------- | :------------------------------ |
| `q`       | The workout name for search.    |
| `page`    | The page number for pagination. |

**Response Body**

| Parameter              | Description                                                                |
| :--------------------- | :------------------------------------------------------------------------- |
| `data`                 | An object containing workout information.                                  |
| `data.count`           | The total number of workouts available.                                    |
| `data.current_page`    | The current page number.                                                   |
| `data.page`            | The page number for pagination.                                            |
| `data.workout`         | An array of workout objects.                                               |
| `data.workout._id`     | The unique identifier for the workout.                                     |
| `data.workout.day`     | The day associated with the workout.                                       |
| `data.workout.desc`    | Description of the workout.                                                |
| `data.workout.level`   | The difficulty level of the workout.                                       |
| `data.workout.moveset` | An array of exercise objects within the workout.                           |
| `data.workout.name`    | The name of the workout.                                                   |
| `data.workout.point`   | Points associated with different muscle groups for the workout.            |
| `data.workout.rest`    | Rest time between sets in seconds.                                         |
| `data.workout.time`    | Duration of the workout in HH:mm format.                                   |
| `data.workout.userId`  | The unique identifier of the user associated with the workout.             |
| `message`              | A message indicating the success of the workout data fetch.                |
| `data`                 | A boolean indicating whether the workout data fetch was successful or not. |

**Example**

```
curl GET "{{base_url}}/?q={{workout_name}}&page={{page}}"
```

```JSON
{
  "data": {
    "count": 2,
    "current_page": 1,
    "page": 1,
    "workout": [
      {
        "_id": "6580ac5b1f89cf75b1fae843",
        "day": "sunday",
        "desc": "Latihan ini memiliki gerkanyang sederhana untuk merenggangkan otot otot",
        "level": "medium",
        "moveset": [
          {
            "exerciseId": {
              "_id": "6580ab7ea5c4a153b84d34de",
              "desc": "Exercise targeting hips and glutes. Perform controlled hip thrusts for lower body strength and glute activation.",
              "direction": "side",
              "end": {
                "left_elbow": 360,
                "left_hip": 25,
                "left_knee": 100,
                "right_elbow": 360,
                "right_hip": 25,
                "right_knee": 100
              },
              "image": "https://storage.googleapis.com/formal-outpost-402813-bucket/exercise/dYjuOFZi3Gu7b1O2dC5AFj6DjeYuak54-20231114-014533",
              "instruction": "Sit with your back against a bench and a barbell across your hips. Lower and raise your hips for a controlled hip thrust.",
              "levelId": {
                "_id": "657e033a7744a82ac69b8e93",
                "name": "medium"
              },
              "name": "Hip Thrust",
              "orientation": "portrait",
              "start": {
                "left_elbow": 360,
                "left_hip": 130,
                "left_knee": 150,
                "right_elbow": 360,
                "right_hip": 130,
                "right_knee": 150
              },
              "targetMuscleId": [
                {
                  "_id": "657e325d1a78fdb254a7b3c5",
                  "name": "hips"
                },
                {
                  "_id": "657e033a7744a82ac69b8e9b",
                  "name": "glutes"
                }
              ]
            },
            "rep": 10,
            "set": 1
          },
          {
            "exerciseId": {
              "_id": "6580ab7ea5c4a153b84d34dd",
              "desc": "Exercise targeting biceps and forearms using dumbbells. Perform controlled curls with a neutral grip for strength and definition.",
              "direction": "front",
              "end": {
                "left_elbow": 180,
                "left_hip": 360,
                "left_knee": 360,
                "right_elbow": 180,
                "right_hip": 360,
                "right_knee": 360
              },
              "image": "https://storage.googleapis.com/formal-outpost-402813-bucket/exercise/dYjuOFZi3Gu7b1O2dC5AFj6DjeYuak54-20231114-014533",
              "instruction": "Stand with feet shoulder-width apart. Lower body by bending knees and hips. Rise back up to starting position.",
              "levelId": {
                "_id": "657e033a7744a82ac69b8e92",
                "name": "easy"
              },
              "name": "Hammer Curl",
              "orientation": "portrait",
              "start": {
                "left_elbow": 10,
                "left_hip": 360,
                "left_knee": 360,
                "right_elbow": 10,
                "right_hip": 360,
                "right_knee": 360
              },
              "targetMuscleId": [
                {
                  "_id": "657e033a7744a82ac69b8ea0",
                  "name": "biceps"
                },
                {
                  "_id": "657e30dc0ca4cc1590a3b044",
                  "name": "forearms"
                }
              ]
            },
            "rep": 20,
            "set": 1
          }
        ],
        "name": "Latihan Sederhana",
        "point": {
          "Quadriceps": 0,
          "abs": 0,
          "back": 0,
          "biceps": 20,
          "chest": 0,
          "forearms": 20,
          "glutes": 20,
          "hamstrings": 0,
          "hips": 20,
          "legs": 0,
          "shoulders": 0,
          "triceps": 0
        },
        "rest": 60,
        "time": "05:30",
        "userId": "657e7b1bd8d396dd896e840e"
      },
      {
        "_id": "6580accd1f89cf75b1fae855",
        "day": "sunday",
        "desc": "Latihan ini memiliki gerkanyang sederhana untuk merenggangkan otot otot",
        "level": "easy",
        "moveset": [
          {
            "exerciseId": {
              "_id": "6580ab7ea5c4a153b84d34e0",
              "desc": "Exercise targeting hips and lower abs. Perform leg raises to strengthen the lower abdominal muscles.",
              "direction": "side",
              "end": {
                "left_elbow": 360,
                "left_hip": 280,
                "left_knee": 360,
                "right_elbow": 360,
                "right_hip": 280,
                "right_knee": 360
              },
              "image": "https://storage.googleapis.com/formal-outpost-402813-bucket/exercise/dYjuOFZi3Gu7b1O2dC5AFj6DjeYuak54-20231114-014533",
              "instruction": "Lie on your back with legs extended. Lift your legs upward, keeping them straight, then lower them back down without touching the ground.",
              "levelId": {
                "_id": "657e033a7744a82ac69b8e92",
                "name": "easy"
              },
              "name": "Leg Raise",
              "orientation": "portrait",
              "start": {
                "left_elbow": 360,
                "left_hip": 10,
                "left_knee": 20,
                "right_elbow": 360,
                "right_hip": 10,
                "right_knee": 20
              },
              "targetMuscleId": [
                {
                  "_id": "657e325d1a78fdb254a7b3c5",
                  "name": "hips"
                },
                {
                  "_id": "657e033a7744a82ac69b8e9e",
                  "name": "abs"
                }
              ]
            },
            "rep": 10,
            "set": 2
          },
          {
            "exerciseId": {
              "_id": "6580ab7ea5c4a153b84d34dd",
              "desc": "Exercise targeting biceps and forearms using dumbbells. Perform controlled curls with a neutral grip for strength and definition.",
              "direction": "front",
              "end": {
                "left_elbow": 180,
                "left_hip": 360,
                "left_knee": 360,
                "right_elbow": 180,
                "right_hip": 360,
                "right_knee": 360
              },
              "image": "https://storage.googleapis.com/formal-outpost-402813-bucket/exercise/dYjuOFZi3Gu7b1O2dC5AFj6DjeYuak54-20231114-014533",
              "instruction": "Stand with feet shoulder-width apart. Lower body by bending knees and hips. Rise back up to starting position.",
              "levelId": {
                "_id": "657e033a7744a82ac69b8e92",
                "name": "easy"
              },
              "name": "Hammer Curl",
              "orientation": "portrait",
              "start": {
                "left_elbow": 10,
                "left_hip": 360,
                "left_knee": 360,
                "right_elbow": 10,
                "right_hip": 360,
                "right_knee": 360
              },
              "targetMuscleId": [
                {
                  "_id": "657e033a7744a82ac69b8ea0",
                  "name": "biceps"
                },
                {
                  "_id": "657e30dc0ca4cc1590a3b044",
                  "name": "forearms"
                }
              ]
            },
            "rep": 20,
            "set": 1
          }
        ],
        "name": "Latihan aja",
        "point": {
          "Quadriceps": 0,
          "abs": 20,
          "back": 0,
          "biceps": 20,
          "chest": 0,
          "forearms": 20,
          "glutes": 0,
          "hamstrings": 0,
          "hips": 20,
          "legs": 0,
          "shoulders": 0,
          "triceps": 0
        },
        "rest": 60,
        "time": "05:30",
        "userId": "657e7b1bd8d396dd896e840e"
      }
    ]
  },
  "message": "Workout data fetch successful",
  "success": true
}

```
