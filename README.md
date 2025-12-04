# AutoMV: Automatic Multi-Agent System for Music Video Generation

AutoMV is a **training-free, multi-agent system** that automatically generates coherent, long-form **music videos (MVs)** directly from a full-length song.  
The pipeline integrates music signal analysis, scriptwriting, character management, adaptive video generation, and multimodal verification—aiming to make high-quality MV production accessible and scalable.

This repository corresponds to the paper:

> **AutoMV: An Automatic Multi-Agent System for Music Video Generation**

---

## 🚀 Features

AutoMV is designed as a full music-to-video (M2V) production workflow with strong music-aware reasoning abilities.

### 🎼 Music Understanding and Preprocessing

- Beat tracking, structure segmentation (**SongFormer**)
- Vocal/accompaniment separation (**htdemucs**)
- Automatic lyrics transcription with timestamps (**Whisper**)
- Music captioning (genre, mood, vocalist attributes) using **Qwen2.5-Omni**

### 🎬 Multi-Agent Pipeline

- **Screenwriter Agent**: creates narrative descriptions, scene summaries, character settings  
- **Director Agent**: produces shot-level scripts, camera instructions, and prompts  
- **Verifier Agent**: checks physical realism, instruction following, and character consistency

### 🧍 Character Bank

- A structured database describing each character’s:  
  *face*, *hair*, *skin tone*, *clothing*, *gender*, *age*, etc.
- Ensures stable identity across multiple shots and scenes

### 🎥 Adaptive Video Generation Backends

- **Doubao Video API**: general cinematic shots  
- **Qwen-Wan 2.2**: lip-sync shots using vocal stems  
- Keyframe-guided generation with cross-shot continuity

### 🧪 Full-Song MV Benchmark (First of Its Kind)

Includes **12 fine-grained criteria** under 4 categories:

- Technical
- Post-production
- Content
- Art

Evaluated via **LLM judges** (Gemini-2.5-Pro/Flash) and **human experts**.

---

## 🧩 System Overview

AutoMV consists of four main stages:

1. **Music Preprocessing**  
2. **Screenwriter & Director Agents**  
3. **Keyframe + Video Clip Generation**  
4. **Gemini Verifier & Final Assembly**

A detailed architecture diagram is available in the paper.

---

## 📦 Installation

AutoMV is a training-free system, relying on MIR tools and LLM/VLM APIs.

### 1. Clone the repository

```bash
git clone https://github.com/xxx/AutoMV.git
cd AutoMV
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

Dependencies include:

- `ffmpeg`
- `htdemucs`
- `whisper`
- `pydub`
- SDKs for Gemini, Doubao, Qwen, etc.

### 3. Add API Keys

Create a `.env` file:

```bash
GEMINI_API_KEY=xxx
DOUBAO_API_KEY=xxx
QWEN_API_KEY=xxx
```

---

## 🎧 Usage

### 1. Prepare your audio

Place your `.mp3` or `.wav` file into:

```bash
./result/{music_video_name}/
```

### 2. Run AutoMV

```bash
python generate_pipeline.py
```

### 3. Output Structure

```bash
result/
  ├── {music_video_name}/        
      ├── camera/            # timeline scripts + shot prompts
      ├── picture/            # generated key images
      ├── output/              # generated short video segments
      └── final_mv.mp4        # final assembled music video
```

---

## 📊 Benchmark & Evaluation

We evaluate AutoMV with:

### **Objective Metric**

- **ImageBind Score (IB)** — cross-modal similarity
between audio and visual content

### **LLM-Based Evaluation (12 Criteria)**

Using multimodal LLMs (Gemini-2.5-Pro/Flash) to score:

- Technical quality
- Post-production
- Music content alignment
- Artistic quality

### **Human Expert Evaluation**

Music producers, MV directors, and industry practitioners scored each sub-criterion (1–5).

---

## 🧪 Experimental Results

On a benchmark of **30 professionally released songs**, AutoMV outperforms existing commercial systems:

| Method            | Cost   | Time     | IB ↑     | Human Score ↑ |
| ----------------- | ------ | -------- | -------- | ------------- |
| Revid.ai-base     | ~$10   | 5–10min  | 19.9     | 1.06          |
| OpenArt-story     | $20–40 | 10–20min | 18.5     | 1.45          |
| **AutoMV (ours)** | $10–20 | ~30min   | **24.4** | **2.42**      |
| Human (experts)   | ≥$10k  | Weeks    | 24.1     | 2.90          |

AutoMV greatly improves:

- Character consistency
- Shot continuity
- Audio–visual correlation
- Storytelling & theme relevance
- Overall coherence of long-form MVs

---

## 📚 Citation

If you use AutoMV in your research, please cite:

```bibtex
@article{AutoMV2026,
  title   = {AutoMV: An Automatic Multi-Agent System for Music Video Generation},
  author  = {Anonymous},
  journal = {arxiv},
  year    = {2025}
}
```

---

## 📝 License

This project is released under the MIT/BSD/Apache 2.0 License.

---

## 🤝 Acknowledgements

AutoMV builds on:

- Qwen-Wan 2.2 (lip-sync)
- Whisper
- htdemucs
- SongFormer
- Gemini Multimodal Verifier
