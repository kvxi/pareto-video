# pareto-video

Using prompt evaluation to create a pareto frontier of the most optimal AI configurations for video transcript generation. The only models being tested are whisper-1, whisper-v3-large, whisper-v3-large-turbo. Results showed that empty initial prompt is most effective for whisper-v3-large and whisper-v3-large-turbo. Even attempting to overfit an initial prompt on the data makes the WER worse for those models. However, both automatic prompt engineering (auto_prompt_engineering.ipynb) and overfitting an initial prompt were highly effective for whisper-1, greatly improving the WER score.

Prompts work differently for these transcription models. They do not take in instructions. Rather, the text supplied as a prompt is simply hallucinated text. 

For example: to improve performance of a transcription model at picking up punctuation, the prompt should not read "Always use proper punctuation" Instead, it would be a sentence matching the style of the content, using punctuation: "Let's begin this video. First up! "

# Findings

The findings show that without an initial prompt whisper-v3-large-turbo is likely just as accurate as whisper-1 for general transcription of audio. Prompt engineering makes whisper-1 the most accurate by far. However, v3-large-turbo is still vastly cheaper for transcription tasks. 

Example spend on the three models for the same task suite:
whisper-v1 $1.75
whisper-large-v3 $0.45
whisper-large-v3-turbo $0.16

Open Diagram Results.pdf for quantitative WER performance of different configurations, and a visualization of the pareto frontier (optimal configurations).

## Setup

### Prerequisites

Python 3.10+

[ffmpeg](https://ffmpeg.org/) — only needed for running video_convert to convert mp4s to mp3. Not needed if you're just testing on the already present mp3s. 

Jupyter, to run the notebooks, or use the VS Code notebook editor.

### Install

```bash
git clone <repo-url>
cd pareto-vimeo

python3 -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

pip install -r requirements.txt
```

`requirements.txt` pulls in:

### API keys

Add vars.env to root and fill in the following api keys.

```env
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
GROQ_API_KEY=gsk_...
```

### Running

1. `configuration_eval.ipynb`: Set RUN_EVAL_SWEEP = True to run it.
Runs eval on golden_set (dataset of transcriptions verified by hand) and scores WER against the corrected transcripts. Each configuration is a pair of model + prompt. Various models and prompts are used. Running it creates an eval_report into /outputs to visualize WER scoring for each configuration. 

The report also shows a pareto frontier for the different configurations.

One eval report has been converted to pdf format as Diagram Results.pdf

2. `auto_prompt_engineering.ipynb`: Play with a transcript prompt engineering workflow. Outputs go to `outputs/prompt_engineering_outputs/`.
