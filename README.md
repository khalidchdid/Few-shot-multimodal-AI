# Few-shot multimodal AI

Detect a rare visual event from a handful of examples, describe it, and generate a similar image. The case material covers skin lesions, olive-leaf disease, and manufacturing defects.

The application and examples come from [RareEventsMatter-VLM](https://github.com/kemoon/RareEventsMatter-VLM). This repository also includes the VLM-Inspector demo, a Streamlit walkthrough of the same three cases. The intended model is one multimodal vision-language model. The runnable backend uses CLIP for similarity, BLIP for captions, and Stable Diffusion for generation, because a single API was not available for the original demo.

## Layout

- `rare-event-detection/backend` is the FastAPI service: upload references, classify, describe, and generate.
- `rare-event-detection/frontend/frontend1` is the browser interface.
- `rare-event-detection/frontend/frontend2` is the VLM-Inspector demo. It shows saved few-shot examples, generated images, and classifications. It does not call the backend.
- `SKIN`, `OLIVES`, and `MANUFACTURING` are the example sets: training images, classifications, and generated samples.
- `VLM-Inspector.pdf` is the project write-up. `video.mov` is the demo recording.

## Run the API and the browser

From `rare-event-detection/backend`:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app:app --reload --host 0.0.0.0 --port 8000
```

The first start downloads the models. Then, from `rare-event-detection/frontend/frontend1`:

```bash
python3 -m http.server 3000
```

Open http://localhost:3000. The API docs are at http://localhost:8000/docs.

## Run the inspector

From `rare-event-detection/frontend/frontend2`:

```bash
pip install -r requirements.txt
streamlit run app.py
```

The images it shows are in `frontend2/assets`.
