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

### Model Architecture
General Architecture of DIA-TTS model
![Model](https://github.com/vuanhlevis/Optimize/blob/main/assets/The-general-architecture-of-the-DIA-TTS-model-which-consists-of-an-encoder-a-DIA-based.png) 


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
We can follow up with this public API to integration model: <br>
    - [fal.ai ](https://fal.ai/models/fal-ai/dia-tts)<br>
    - [segmind](https://www.segmind.com/models/dia/api)<br>



3. Video quality
   - Considering that video quality is significantly influenced by the accuracy of lip-syncing, I conducted in-depth research and have compiled a comparison of several models, as presented below.

| Model / Service     | Open/Commercial | Input (Image+Audio / Video+Audio) | Real-time Capable   | Output Res.          | Lip-sync Quality        | Expression/Emotion    | API / Ease of Use          | Hardware (GPU?)   | Pricing (if SaaS)     |
| ------------------- | --------------- | --------------------------------- | ------------------- | -------------------- | ----------------------- | --------------------- | -------------------------- | ----------------- | --------------------- |
| **Sonic**           | Open            | Image + Audio                     | ✔ (∼60 FPS on GPU)  | High (≥512×512)      | ★★★★★ (MOS \~4.6/5)     | Auto (diverse)        | Code (PyTorch) easy to use | GPU (e.g. RTX)    | Free (open-source)    |
| **GeneFace++**      | Open            | Image + Audio                     | ✔ (real-time)       | 512×512 (3D NeRF)    | ★★★★★ (high-detail)     | 3D pose auto          | Complex (NeRF setup)       | GPU (high-end)    | Free (open-source)    |
| **Wav2Lip**         | Open            | Video + Audio (→ Video) (image✔)  | ≈10–15 FPS (GPU)    | Medium (256–512)     | ★★★★☆ (very accurate)   | None (neutral)        | Simple (pip install)       | GPU (recommended) | Free (open-source)    |
| **VideoReTalking**  | Open            | Video + Audio (→ Video)           | ✘ (offline)         | Matches input (HD)   | ★★★★☆ (high-quality)    | Yes (handles emotion) | Complex (multi-stage)      | GPU               | Free (open-source)    |
| **MakeItTalk**      | Open            | Image + Audio                     | ✘ (offline)         | Low–Med (256)        | ★★★☆☆ (expressive)      | Yes (speaker style)   | Research code (demo)       | GPU               | Free (open-source)    |
| **Sync (sync.so)**  | Com’l (API)     | Video + Audio (→ Video)           | ✔ (∼25 FPS GPU)     | 512×512 (hi-quality) | ★★★★★ (state-of-art)    | None                  | Easy (HTTP API)            | Cloud (GPU)       | \~\$2–3/min (model-2) |
| **D-ID API**        | Com’l (API)     | Image + Audio (→ Video)           | ✔ (100 FPS claimed) | Up to 1024×1024      | ★★★★☆ (very good)       | None                  | Easy (cloud API)           | Cloud (GPU)       | Subscription (custom) |
| **LipDub AI**       | Com’l (API)     | Image or Video + Audio            | ✘ (offline)         | HD (1080p)           | ★★★★★ (Hollywood-level) | None                  | Enterprise API             | Cloud (GPU)       | Enterprise pricing    |
| **Vozo AI**         | Com’l (Web/API) | Image & Video + Audio             | ✔ (low-latency)     | HD (1080p)           | ★★★★☆ (very realistic)  | None                  | Web/priv. API              | Cloud (GPU)       | By plan (not public)  |
| **Everypixel Labs** | Com’l (API)     | Video + Audio (→ Video)           | ✘ (offline)         | Matches input (HD)   | ★★★★☆ (very good)       | None                  | Easy (pay-as-you-go)       | Cloud (GPU)       | \~\$1 per minute      |
| **Tavus API**       | Com’l (API)     | Video + Audio / Dubbing           | ✘ (offline)         | Matches input (HD)   | ★★★★☆ (high)            | None                  | Easy (tiered API)          | Cloud (GPU)       | Free–\$375/mo (plans) |
| **Synthesia**       | Com’l (Web/API) | *Avatar model only (Text→Video)*  | ✘ (offline)         | HD (up to 1080p)     | ★★★★☆ (realistic)       | None                  | Easy (web/API)             | Cloud (GPU)       | \$89+/mo (Creator)    |
| **HeyGen**          | Com’l (Web/API) | *Avatar model only (Text→Video)*  | ✘ (offline)         | HD (1080p)           | ★★★★☆ (good)            | None                  | API (Enterprise)           | Cloud (GPU)       | Enterprise (contact)  |
| **Colossyan**       | Com’l (Web/API) | *Avatar model only (Text→Video)*  | ✘ (offline)         | 720–1080p            | ★★★☆☆ (fair)            | None                  | API (enterprise)           | Cloud (GPU)       | Enterprise (contact)  |
| **Hour One**        | Com’l (Web/API) | *Avatar model only (Text→Video)*  | ✘ (offline)         | HD (up to 1080p)     | ★★★☆☆ (good)            | None                  | API (enterprise)           | Cloud (GPU)       | Enterprise (contact)  |


_In case of generate video + Dubbed Audio_: Specialized APIs excel. **Sync.so**’s lip-sync API yields top-notch alignment (at ~25 fps real-time throughput). **LipDub AI** is targeted at “Hollywood” quality.

_Static Image → Talking Video_: For the highest realism and fidelity, modern NeRF methods (GeneFace++, Sonic) lead the field. Sonic offers the best lip-sync accuracy (MOS~4.6/5) with no setup cost.


