# SafeStage Climate Planner

Build the SafeStage frontend as a clean, modern React web app for an AI-powered outdoor event climate-safety platform.

Brand/UI

Primary brand colour: beautiful modern purple (#7C3AED or a close elegant purple).

Use a clean white/light background, purple accents, soft cards, rounded corners and subtle shadows.

Professional SaaS/dashboard feel.

Responsive on desktop and mobile.

Keep the design polished but lightweight — do not overbuild or add unnecessary animations.

Product name: SafeStage

Tagline: Plan safer. Decide smarter.

Core pages

Landing page

Dashboard

Create Event

Event Analysis / Results

Heat Map

AI Planning Assistant

What-If Simulation

Climate Readiness Report

IMPORTANT: BACKEND CONTRACT
The frontend must integrate with my existing FastAPI backend. Do NOT invent, rename, or restructure the API endpoints, request variables, or response fields.

Backend endpoints:

POST /events

Request:

{
  "name": "string",
  "event_type": "string",
  "venue_name": "string",
  "address": "string",
  "latitude": 0,
  "longitude": 0,
  "attendance": 0,
  "start_datetime": "ISO datetime",
  "end_datetime": "ISO datetime",
  "user_id": "string | null"
}


POST /analyze

Request:

{
  "event_id": "string"
}


Expected response uses:
event_id, supported, message, provider, readiness_score, readiness_score_label, heat_risk_summary, temperature_summary, smart_date_recommendations, best_date_option, venue_layout_recommendations, heat_risk_zones, recommendations, ai_explanation, analyzed_at.

POST /simulate

Request:

{
  "event_id": "string",
  "scenario_a": "string",
  "scenario_b": "string",
  "history": [
    {
      "role": "user | assistant",
      "content": "string"
    }
  ]
}


Response uses:
event_id, supported, message, scenario_a, scenario_b, recommended, score_difference, reason, tactical_action_plan, ai_simulation_insights.

Each scenario result contains:
name, readiness_score, heat_risk_level, avg_temp_c, max_temp_c, peak_heat_exposure_hours, risk_factors, mitigations.

GET /heatmap

Query parameters:

event_id
OR

latitude

longitude

optional timestamp

Response uses:
supported, message, event_id, latitude, longitude, timestamp, provider, geojson, zones.

Each heat-risk zone contains:
zone_id, name, risk_level, avg_temp_c, coordinates, advice.

POST /chat

Request:

{
  "event_id": "string",
  "message": "string",
  "history": [
    {
      "role": "user | assistant | system",
      "content": "string"
    }
  ]
}


Response:

{
  "event_id": "string",
  "reply": "string",
  "context_used": {}
}


GET /report?event_id={event_id}

This returns a PDF file. The frontend should provide a Download Climate Readiness Report button and handle the PDF response correctly.

GET /events/{event_id} returns the event:
id, user_id, name, event_type, venue_name, address, latitude, longitude, attendance, start_datetime, end_datetime, created_at, updated_at.

GET /events returns a list of events.

GET /health can be used to display backend connection/system status.

Frontend behaviour

Create Event form should collect exactly the fields required by POST /events.

After creating an event, store the returned event ID and use it for analysis.

The Analysis page should call POST /analyze using the event ID.

Display the readiness score prominently.

Display temperature summary, heat-risk level, smart date/time recommendations, best date option, venue layout recommendations, risk zones and AI explanation.

Heat Map page should consume the actual /heatmap GeoJSON/zones response. Do not fabricate heat zones.

Simulation page should allow users to enter Scenario A and Scenario B and display both returned scenario results side-by-side, including readiness scores, heat risk, temperatures, risk factors and mitigations.

AI Assistant should maintain conversation history and send it using the exact /chat request structure.

Report button should download the actual PDF returned by /report.

Show proper loading, empty and API-error states.

Never display fake climate results when the backend has not returned data.

Dashboard
Create a simple overview showing:

Recent events

Event readiness score

Heat-risk status

Quick action to create an event

Quick action to analyze an event

Quick access to AI Assistant, Heat Map and Simulation

Use reusable components and a centralized API service/base URL so the FastAPI backend URL can easily be configured later.

Do not create authentication, payments, complex admin features, or unnecessary pages.

Most importantly: the frontend is a client for the existing SafeStage FastAPI backend. Preserve the exact API endpoint names, HTTP methods, request fields and response field names above. Do not create a second backend or mock API. Do not rename, flatten, reinterpret, or invent any API request/response fields. The backend contract provided above is the single source of truth for frontend integration.

This project was built with [Lovable](https://lovable.dev).

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/8b461159-1c3a-4fbf-b1ff-e9bad3676de5).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
