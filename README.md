# Optimize
## 1.Improve loading time videos and images:
- _Optimize video files_:
    we reduce the file size without compromising quality by using efficient videos format and compressing videos(h264,265 or vp9)

![Model](https://github.com/vuanhlevis/Optimize/blob/main/assets/h264_vp9.jpg)
![Model](https://github.com/vuanhlevis/Optimize/blob/main/assets/h264_h265_vp9_av1.png)
- _Adaptive streaming_:
    instead of sending the whole video at once, we deliver small pieces tailored to the user's internet speef. This can help videos start faster and play smothly without interruptions

 ![Model](https://github.com/vuanhlevis/Optimize/blob/main/assets/file_chunk.png) 
 
- _Global delivery_: can use specialized services called Content Delivery Network (CDN) to store video file to servers closer to users around the world, minimizing delays by location. Setting plan for object caching on Cloudfont, assets, audio or creator can be stored longer

 ![Model](https://github.com/vuanhlevis/Optimize/blob/main/assets/CDN.png) 

- _Preprocessing_: video can be prepared and optimized ahead of time so the are ready to be delivered instantly when requested


## 2. Voice Integration
Make audio more quality, and the voice of actor more natual i found a Model TTS of Nari Labs seems to be good if we have enough resource to integration
### Model Overview
    - Dia (often referred to as DIA-1.6B) – a 1.6 billion-parameter neural TTS model
    - Architecture Highlights:
        - End-to-end diffusion-decoder backbone
        - Multi-speaker conditional encoder
        - Direct 24 kHz dual-channel waveform output

### Traning Inspirations & Data Flow
```
[text transcript + speaker tags + nonverbal tokens]
                 ↓
        Text tokenizer → Text token IDs
                 ↓
       (optional) audio prompt → Codec tokens
                 ↓
[Transformer (1.6B-param decoder)]
                 ↓
     Autoregressive prediction of
      next audio codec token
                 ↓
     Descript Audio Codec decode
                 ↓
          24 kHz waveform
```

### Audio Quality & Features
| Feature                     | Description                                                                                        |
| --------------------------- | -------------------------------------------------------------------------------------------------- |
| **Expressiveness**          | Customizable speaker tones, emotional inflections, laughter, sighs, coughs, even screams.          |
| **Zero-Shot Voice Cloning** | Captures a new speaker’s timbre from just seconds of reference audio.                              |
| **Nonverbal Cues**          | Generates natural non-speech sounds (laughter, throat clears, etc.) alongside dialogue.            |
| **Real-Time Throughput**    | \~40 tokens/sec on a single NVIDIA A4000 GPU (\~10 GB VRAM). Plans for CPU support & quantization. |
| **Quality Benchmark**       | Independent testers note MOS scores on par with top commercial TTS (≈4.3–4.5).                     |


### Implement with API: 
We can follow up with this public API to integration model: [fal.ai ](https://fal.ai/models/fal-ai/dia-tts)

## 3. Video quality 

