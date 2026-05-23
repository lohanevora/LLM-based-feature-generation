# LLM-based-feature-generation
pip install llm-feature-gen

OPENAI_API_KEY=your_api_key
OPENAI_MODEL=gpt-4.1-mini
OPENAI_AUDIO_MODEL=whisper-1

python3 - <<'PY'
from pathlib import Path

from llm_feature_gen import (
    discover_features_from_texts,
    generate_features_from_texts,
)

samples = {
    "demo_discover_texts/sample1.txt": "The dish was rich, spicy, and served in a deep bowl.",
    "demo_discover_texts/sample2.txt": "The dessert was light, creamy, and topped with fresh fruit.",
    "demo_texts/positive/review1.txt": "The meal was vibrant, aromatic, and beautifully plated.",
    "demo_texts/negative/review1.txt": "The service was slow and the food arrived cold.",
}

for file_name, text in samples.items():
    path = Path(file_name)
    path.parent.mkdir(parents=True, exist_ok=True)
    path.write_text(text, encoding="utf-8")

discovered = discover_features_from_texts("demo_discover_texts")
csv_paths = generate_features_from_texts(
    root_folder="demo_texts",
    merge_to_single_csv=True,
)

print(discovered)
print(csv_paths)
PY
