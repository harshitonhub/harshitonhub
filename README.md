# Harshit Jain

MSc Computer Science (Agentic AI/ML), University College Dublin — Dublin, Ireland

I like problems where the constraint is the actual engineering challenge — this year that meant squeezing a computer-vision model onto a phone instead of a GPU, and figuring out what a real signal looks like when the ground truth itself is uncertain.

## MirrorPoint — thermal injury detection for horses

At Cavalloré, an equine health-tech startup, I built the ML side of a system that uses thermal imaging and ride telemetry to catch injuries in horses before they become visible lameness. Vets already use thermography for this, but manually, on single hot spots — the goal was to make it systematic.

The core model, MirrorPoint, is a U-Net with an EfficientNet-B4 encoder that segments a horse's legs out of a thermal frame. It's evaluated against GrabCut pseudo-labels, not vet-confirmed ground truth, and I say that up front every time — it's a real limitation, not a footnote.

The more interesting piece is what sits on top of segmentation: a longitudinal pipeline that OCRs raw FLIR screenshots and tracks left-right temperature asymmetry as the actual unit of signal, checking directional consistency across proximal, mid, and distal points rather than trusting any single-point threshold. A 1–3°C difference becomes a flag for a vet to look at, not a diagnosis — the model's job is to reduce noise, not replace judgment.

Inference had to run on-device, so this wasn't GPU-serving — I converted everything to Core ML, TFLite, and ONNX with int8 quantization, and that constraint shaped model choices as much as accuracy did. Raw thermal files live in Cloudflare R2, structured metadata in MongoDB Atlas, and vets get human-readable exports via Google Drive. Over the internship, this pipeline took the signal-to-noise ratio from 1.8 to 4.0.

I also handled thermal camera procurement, which turned out to be its own lesson in how much hardware choice constrains what your model can even see.

## Also building

**[grid-oracle-f1-agent](https://github.com/harshitonhub/grid-oracle-f1-agent)** — an F1 pit-wall strategy agent on the OpenAI Responses API. It pulls real-time telemetry from OpenF1, retrieves from a knowledge base of race rules and history, and runs Monte Carlo simulations to back live strategy calls — closer to a decision-support tool than a chatbot.

**[aws-healthcare-insurance-analytics](https://github.com/harshitonhub/aws-healthcare-insurance-analytics)** — a small healthcare data warehouse on S3, Glue, and Athena, with a Streamlit front end, mostly to get hands dirty with AWS's analytics stack end to end.

Before this, two internships at Celebal Technologies in data science and data engineering — cut ETL integration time by 30% and improved a forecasting model's accuracy by 15%.

## Currently exploring

A scoped AI fairness and governance audit of a candidate-scoring tool, benchmarked against the EU AI Act and NYC Local Law 144 using Aequitas and Fairlearn. It's early, but it's the direction I want to keep pulling on — the gap between a model that works and a model whose decisions you can actually defend.

---

Finishing my MSc in September 2026. Python and PyTorch day to day, with the on-device (Core ML / TFLite / ONNX) and cloud (AWS, MongoDB Atlas, Cloudflare R2) stack from MirrorPoint. Always happy to talk through any of the above.
