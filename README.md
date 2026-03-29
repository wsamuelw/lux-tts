# 🎙️ LuxTTS - Voice Cloning in Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/wsamuelw/LuxTTS/blob/main/Voice%20Clone%20Demo)

A step-by-step guide to clone any voice using **LuxTTS** (Lux Text-to-Speech) in Google Colab. Generate realistic speech synthesis with voice cloning capabilities—no local GPU required!

**Repository**: [ysharma3501/LuxTTS](https://github.com/ysharma3501/LuxTTS)

---

## 🌟 Features

- **Easy Voice Cloning**: Clone any voice with just a short audio sample
- **Fast Processing**: GPU-accelerated with CUDA support (includes K2 optimization)
- **Customizable Output**: Fine-tune volume, quality, speed, and more
- **No Local Setup Required**: Run entirely in Google Colab
- **High Quality Output**: Generate realistic, natural-sounding speech
- **Web-Friendly**: Download your generated audio directly from Colab

---

## 📋 Prerequisites

- A **Google account** (for Colab access)
- A **reference audio file** (WAV or MP3, any voice you want to clone)
- **5-10 minutes** of setup time

---

## 🚀 Quick Start

### Step 1: Open in Google Colab
1. Create a new notebook in [Google Colab](https://colab.research.google.com)
2. Copy the provided code cells into your notebook

### Step 2: Run Setup
Execute the first cell to clone the repository and install dependencies:
```python
!git clone https://github.com/ysharma3501/LuxTTS.git
%cd LuxTTS
!uv pip install -r requirements.txt
!pip install k2==1.24.4.dev20251030+cuda12.6.torch2.9.0 -f https://k2-fsa.github.io/k2/cuda.html --no-deps
```

### Step 3: Load the Model
Run the model loading cell (takes 30-60 seconds):
```python
from zipvoice.luxvoice import LuxTTS
lux_tts = LuxTTS('YatharthS/LuxTTS', device='cuda')
```

### Step 4: Upload Your Voice
Upload a reference audio file (WAV or MP3 format) containing the voice you want to clone.

### Step 5: Configure Settings
Adjust parameters to customize your output, then run the generation cell.

### Step 6: Download
Your cloned voice will be saved as `output.wav` and ready to download.

---

## ⚙️ Configuration Settings

Customize the voice cloning behavior by adjusting these parameters in **Step 4**:

| Parameter | Default | Range | Description |
|-----------|---------|-------|-------------|
| **text** | N/A | Any string | The text you want to synthesize |
| **rms** | 0.01 | 0.01–1.0 | Volume control (increase for louder output) |
| **t_shift** | 0.9 | 0.1–1.0 | Quality/style control (higher = better quality, slightly worse WER) |
| **num_steps** | 4 | 3–8+ | Processing steps (3-4 = best balance, higher = better quality but slower) |
| **speed** | 1.0 | 0.5–2.0 | Speech rate (1.0 = normal, <1.0 = slower, >1.0 = faster) |
| **return_smooth** | False | True/False | Smoothing (True = smoother, False = clearer articulation) |
| **ref_duration** | 10000 | 1000–30000 | Reference audio duration in milliseconds (lower = faster, increase if artifacts occur) |

### ⚡ Optimization Tips

- **For Speed**: Use `num_steps=3` and `ref_duration=5000`
- **For Quality**: Use `num_steps=6+` and `t_shift=0.95`
- **For Clarity**: Set `return_smooth=False` and `t_shift=0.85`
- **For Smoothness**: Set `return_smooth=True` and `t_shift=0.95`

---

## 📁 Input & Output

### Input Requirements
- **Audio Format**: WAV or MP3
- **Duration**: 5-20 seconds recommended (minimum: 2 seconds)
- **Quality**: Clear audio works best; avoid background noise
- **Sample Rate**: Any (will be auto-normalized)

### Output
- **File**: `output.wav`
- **Sample Rate**: 48kHz
- **Format**: WAV (PCM)
- **Duration**: Depends on text length

---

## 🔧 Troubleshooting

### Issue: Model Takes Too Long to Load
**Solution**: This is normal (30-60 seconds). First-time load is slower.

### Issue: "CUDA out of memory" Error
**Solution**: 
- Switch to CPU: Change `device='cuda'` to `device='cpu'`
- Reduce `ref_duration` to 5000
- Use `num_steps=3`

### Issue: Audio Has Artifacts or Distortion
**Solution**:
- Increase `ref_duration` to 15000
- Reduce `rms` to 0.005
- Increase `t_shift` to 0.95
- Use `return_smooth=True`

### Issue: Output Sounds Robotic
**Solution**:
- Increase `num_steps` to 6+
- Set `return_smooth=True`
- Increase `t_shift` to 0.9+

### Issue: Poor Voice Cloning Quality
**Solution**:
- Use a clearer reference voice (less background noise)
- Increase reference duration (10000-20000ms)
- Ensure reference audio is 5+ seconds
- Increase `num_steps` for better quality

---

## 💡 Best Practices

1. **Upload High-Quality Reference Audio**
   - Clear, clean voice samples work best
   - Minimize background noise
   - Use 5-20 second clips

2. **Test with Short Text First**
   - Start with 1-2 sentence outputs
   - Verify quality before generating long speeches

3. **Experiment with Parameters**
   - Save your favorite settings for future use
   - Document which settings work best for your voice

4. **Monitor GPU Usage**
   - Google Colab provides ~12-15GB of GPU memory
   - Reduce `num_steps` if you hit memory limits

---

## 📊 Performance Metrics

- **Setup Time**: ~5-10 minutes (one-time)
- **Model Load**: 30-60 seconds (per session)
- **Encoding Reference**: ~10 seconds
- **Synthesis**: 30 seconds – 2 minutes (depends on `num_steps` and text length)
- **Quality**: High-fidelity, natural speech output

---

## 🎯 Use Cases

- **Voice Cloning**: Create digital twins of voices
- **Text-to-Speech**: Generate speech for any text
- **Content Creation**: Create voiceovers and narration
- **Accessibility**: Generate audio from text for accessibility
- **Entertainment**: Create fun voice-cloned content
- **Prototyping**: Test TTS capabilities before production

---

## ⚠️ Ethical Considerations

- **Consent**: Only clone voices with permission from the speaker
- **Disclosure**: Clearly indicate when audio is AI-generated
- **Misuse Prevention**: Don't use voice cloning to impersonate or deceive
- **Respect Privacy**: Follow applicable laws regarding consent and data usage

---

## 🔗 Resources

- **Original Repository**: [ysharma3501/LuxTTS](https://github.com/ysharma3501/LuxTTS)
- **Model**: [YatharthS/LuxTTS](https://huggingface.co/YatharthS/LuxTTS) (Hugging Face)
- **Google Colab**: [colab.research.google.com](https://colab.research.google.com)

---

## 📝 Frequently Asked Questions

**Q: Can I use this commercially?**
A: Check the original repository's license. For commercial use, verify licensing terms with the model creators.

**Q: How long does each generation take?**
A: Usually 1-2 minutes depending on text length and `num_steps` setting.

**Q: Can I run this locally?**
A: Yes, but you'll need a GPU with CUDA support and the same dependencies. Google Colab is recommended for ease of use.

**Q: What's the maximum text length?**
A: There's no hard limit, but very long texts may timeout. Break into multiple chunks if needed.

**Q: Can I use different voice samples?**
A: Yes! Upload a different voice file and re-run the encoding and synthesis steps.

---

## 🤝 Contributing

Found a bug or have suggestions? Consider contributing to the original [LuxTTS repository](https://github.com/ysharma3501/LuxTTS).

---

## 📄 License

This code and documentation are provided as-is. See the original [LuxTTS repository](https://github.com/ysharma3501/LuxTTS) for license information.

---

## 🎉 Get Started Now!

Ready to clone some voices? Open [Google Colab](https://colab.research.google.com) and paste the code above. Your first cloned voice awaits! 🚀
