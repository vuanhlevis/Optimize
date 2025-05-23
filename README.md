# Optimize
For improve loading time videos and images:
- _Optimize video files_:
    we reduce the file size without compromising quality by using efficient videos format and compressing videos(h264,265 or vp9)

![Model](https://github.com/vuanhlevis/Optimize/blob/main/assets/h264_vp9.jpg)

- _Adaptive streaming_:
    instead of sending the whole video at once, we deliver small pieces tailored to the user's internet speef. This can help videos start faster and play smothly without interruptions

 ![Model](https://github.com/vuanhlevis/Optimize/blob/main/assets/file_chunk.png) 
 
- _Global delivery_: can use specialized services called Content Delivery Network (CDN) to store video file to servers closer to users around the world, minimizing delays by location. Setting plan for object caching on Cloudfont, assets, audio or creator can be stored longer
- _Preprocessing_: video can be prepared and optimized ahead of time so the are ready to be delivered instantly when requested
