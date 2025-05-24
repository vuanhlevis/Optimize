# Optimize
## For improve loading time videos and images:
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


## Voice Integration
Base on voice quality and the pricing, i think elevenlabs TTS is the good choice for us:
- Easy to Use
- Realistic Voices: The voices generated sound very human-like. They are often clear and have natural-sounding tones and inflections, making the audio more engaging.
- Voice Cloning: A standout feature is its ability to create a digital copy of a real voice(even style and tone).
- Multiple Languages: ElevenLabs supports many different languages.
