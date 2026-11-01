# 🚗 Insurance Claim AI Agent

A Streamlit application for exploring vehicle-damage insurance claim
analysis from an uploaded image.

The application passes the image to a backend workflow and displays
damage observations, repair-cost estimates, policy analysis, and a
generated claim recommendation.

## Overview

This project provides a single interface for reviewing the outputs of
an insurance-claim analysis workflow.

Users upload a damaged vehicle image and select Analyze Claim. The
application invokes the backend workflow and presents its results in
four sections:

1. Vehicle damage analysis
2. Repair-cost estimation
3. Policy analysis
4. Claim decision output

The interface integrates with a backend application imported from
graph.graph.

## Features

### 📷 Vehicle Image Upload

- Supports JPG, JPEG, and PNG files.
- Displays a preview of the uploaded image.
- Saves the uploaded file in a local temp directory for backend processing.

### 🔍 Damage Analysis

Displays the backend's assessment of:

- Damage severity
- Damage summary
- Damaged vehicle parts

### 💰 Repair-Cost Estimation

Displays:

- Replacement-parts table
- Parts cost
- Labour cost
- Total estimated repair cost

Amounts are displayed in Indian rupees.

### 📄 Policy Analysis

Displays the policy-analysis response returned by the backend.

The policy source, retrieval process, and coverage rules depend on the
backend implementation and are not defined in the Streamlit interface.

### ✅ Claim Decision Output

Displays the backend-generated:

- Claim status
- Approved amount
- Reason for the decision

These outputs should be treated as prototype recommendations requiring
review, not as an insurer's binding approval.

## Application Workflow

```text
Upload Vehicle Image
        ↓
Preview Uploaded Image
        ↓
Save Image to Temporary Storage
        ↓
Select "Analyze Claim"
        ↓
Invoke Backend Workflow
        ↓
Display Damage Analysis
        ↓
Display Repair-Cost Estimate
        ↓
Display Policy Analysis
        ↓
Display Claim Recommendation
```

The display order does not establish the internal execution order of
the backend workflow.

## Technology Stack

### Visible in the Application Code

- Python
- Streamlit
- Pillow
- Python os module
- Custom backend workflow imported from graph.graph

Additional model providers, orchestration libraries, retrieval tools,
and API integrations depend on the backend implementation.

## Backend Integration

The Streamlit interface imports the backend application:

```python
from graph.graph import app
```

When the user selects Analyze Claim, the interface invokes it with:

```python
state = {
    "image_path": image_path
}

result = app.invoke(state)
```

### Input Contract

The backend receives a dictionary containing the saved image path:

```python
{
    "image_path": "temp/uploaded_vehicle_image.jpg"
}
```

### Expected Output Contract

The interface expects the following structure:

```python
{
    "vision_output": {
        "severity": "...",
        "damage_summary": "...",
        "damaged_parts": [
            "..."
        ]
    },
    "cost_estimation": {
        "replaced_parts": [
            # Table-compatible replacement-part records
        ],
        "parts_cost": 0,
        "labor_cost": 0,
        "total_cost": 0
    },
    "policy_answer": "...",
    "final_decision": {
        "claim_status": "...",
        "approved_amount": 0,
        "reason": "..."
    }
}
```

The values above illustrate the required structure only. They are not
actual analysis results.

The backend must return compatible field names and value types for the
interface to render successfully.

## Suggested Project Structure

Adapt this structure to match the actual repository:

```text
Insurance_Claim_AI_Agent/
├── app.py
├── graph/
│   └── graph.py
├── requirements.txt
├── README.md
├── .gitignore
└── temp/
```

- app.py: Streamlit interface.
- graph/graph.py: Backend workflow exposing app.invoke().
- requirements.txt: Frontend and backend dependencies.
- temp/: Runtime storage for uploaded images; exclude from version control.

Include any additional backend modules, configuration files, and policy
resources required by your implementation.

## Installation and Setup

### 1. Obtain the Project

Clone or download the repository.

Open a terminal in the project root.

### 2. Create a Virtual Environment

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Or on macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
python -m pip install -r requirements.txt
```

The interface directly requires:

```text
streamlit
Pillow
```

The requirements file must also include all dependencies used by the
backend workflow. These cannot be determined from the frontend code alone.

Use versions verified in your working environment.

### 4. Configure the Backend

Ensure that:

- graph.graph can be imported.
- It exposes an app object with an invoke method.
- Any required model credentials or services are configured.
- Any required policy documents or pricing resources are available.
- Backend results match the expected output contract.

Keep credentials outside version control.

### 5. Run the Application

```bash
python -m streamlit run app.py
```

Open the local address shown in the terminal.

## How to Use

1. Open the Streamlit application.
2. Upload a JPG, JPEG, or PNG image of a damaged vehicle.
3. Review the image preview.
4. Select Analyze Claim.
5. Wait for the backend workflow to finish.
6. Review the damage summary and listed parts.
7. Inspect the estimated parts and labour costs.
8. Read the policy-analysis response.
9. Review the generated claim recommendation.

## Current Limitations

- The interface accepts an image but does not collect policy details,
  vehicle specifications, or claim documents through separate input fields.
- Policy context and pricing data must therefore come from the backend,
  if implemented.
- A single image may not show hidden damage or all affected components.
- No damage-detection accuracy or cost-estimation benchmark is established
  by the interface code.
- The interface assumes all expected backend fields are present.
- Backend errors and malformed responses are not explicitly handled.
- Uploaded files are saved using their original filenames, which can
  cause collisions between uploads.
- Temporary uploads are not automatically deleted.
- Every claim-status value is currently displayed with a success-style
  message, regardless of whether the outcome is approval or rejection.

## Privacy and Security

Vehicle images may contain identifying information, such as registration
plates, faces, or location details.

Before public deployment:

- Define how uploaded images are stored and deleted.
- Use unique, server-generated filenames.
- Validate uploaded file content and size.
- Keep credentials and uploaded images out of the repository.
- Review whether backend providers receive uploaded images.
- Obtain appropriate consent for processing claim-related information.
- Add access controls where required.

## Suggested .gitignore

```gitignore
# Virtual environments
.venv/
venv/

# Python cache
__pycache__/
*.py[cod]

# Local secrets
.env
.env.*
!.env.example
.streamlit/secrets.toml

# Uploaded images
temp/

# Notebook checkpoints
.ipynb_checkpoints/

# OS files
.DS_Store
Thumbs.db
```

## Future Improvements

- Add policy-document upload and policy identification.
- Collect vehicle make, model, year, and location.
- Support multiple images per claim.
- Validate backend responses before rendering.
- Add exception handling and user-friendly error messages.
- Use status-specific displays for approved, rejected, and review-required claims.
- Add unique upload filenames and automatic cleanup.
- Integrate documented repair-pricing sources.
- Add human review before any final claim decision.
- Evaluate damage analysis and cost estimates against reviewed examples.
