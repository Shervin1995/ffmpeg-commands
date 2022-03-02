# FFmpeg
1400.12.10

1. download from [here]()!
2. add to path!
3. open powershell 
4. documents videos 


## Windows Powershell Command

* ...

`ffmpeg -ss 30 -t 3 -i videos/1.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 videos/1.gif`

--------------------------------------------

* Reverse (Video)

`ffmpeg -i videos/1.mp4 -vf reverse videos/2.mp4`


--------------------------------------------

* Reverse (Video and Audio)

`ffmpeg -i videos/1.mp4 -vf reverse -af areverse videos/2.mp4`

--------------------------------------------

* Encode

`ffmpeg -i videos/1.mp4 videos/1-1.mp4`


--------------------------------------------

* gif 

`ffmpeg -i videos/1.mp4 -r 4 videos/121.gif`


--------------------------------------------

* Scale (method 1)

`ffmpeg -i videos/1-1.mp4 -filter:v scale=1080:-1 videos/1-2.mp4`


--------------------------------------------

* Scale (method 2)

`ffmpeg -i videos/z.mp4 -vf "scale=320:240:force_original_aspect_ratio=decrease,pad=320:240:(ow-iw)/2:(oh-ih)/2" videos/z-1.mp4`

[more info](https://superuser.com/questions/547296/resizing-videos-with-ffmpeg-avconv-to-fit-into-static-sized-player)


--------------------------------------------

* Mute

`ffmpeg -i videos/z-1.mp4 -an videos/z-2.mp4`


--------------------------------------------

* BW 

`ffmpeg -i videos/2-1.mp4 -vf hue=s=0 -c:a copy videos/2-3.mp4`


--------------------------------------------

* Capture Video

`ffmpeg -i videos/2.mp4 -ss 00:00:01.000 -vframes 1 videos/2.jpg`


--------------------------------------------

* Brightness

`ffmpeg -i videos/bm98.06.16.mp4 -vf eq=brightness=0.10:saturation=1.1 -c:a copy videos/bm98.06.16-2.mp4`


--------------------------------------------

* Rotate

`ffmpeg -i videos/1.mp4 -vf "transpose=2" -codec:a copy videos/1-1.mp4`

```
"transpose=1" 			// Right 90  degrees 
"transpose=2" 			// Left  90  degrees 
"transpose=1,transpose=1" 	// Right 180 degrees 
```

--------------------------------------------

* Watermark

`ffmpeg -i videos/z-1.mp4 -i videos/wm.png -filter_complex "overlay=10:10" videos/z-2.mp4`

--------------------------------------------  

* Create 5 second Video from an Image

`ffmpeg -loop 1 -i videos/intro.png -c:v libx264 -t 5 -pix_fmt yuv420p videos/intro.mp4`

--------------------------------------------

* Speedup2x (Video and Audio)

`ffmpeg -i videos/1-1.mp4 -filter_complex "[0:v]setpts=0.5*PTS[v];[0:a]atempo=2.0[a]" -map "[v]" -map "[a]" videos/1-2.mp4`

--------------------------------------------

* Speedup2x (Video)

`ffmpeg -i videos/2-1.mp4 -filter:v "setpts=0.5*PTS" videos/2-2.mp4`

--------------------------------------------

* Seeking

`ffmpeg -i videos/1.mp3 -ss 00:00:00 -to 00:01:10 -c copy videos/1-1.mp3`

--------------------------------------------


* Concat (Video and Audio)

`ffmpeg -f concat -i videos/mylist.txt -c copy videos/z1.mp4`

note0: if your videos has same bitrate,
video will be with sound :-)

note1: create "mylist.txt" like this: 
file 'picture.mp4'
file '1.mp4'

note2: use *concat[vid] 2times!
1st time for all execpt thnx4wach.mp4
2nd time for result.mp4 and thnx4wach.mp4

--------------------------------------------

* Concat (Video and Audio)


`ffmpeg -i videos/1.mp4 -i videos/2.mp4 -i videos/3.mp4 -filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0][2:v:0][2:a:0]concat=n=3:v=1:a=1[outv][outa]" -map "[outv]" -map "[outa]" videos/z1.mp4`

`ffmpeg -i videos/2.mp4 -i videos/3.mp4 -i videos/4.mp4 -i videos/5.mp4 -filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0][2:v:0][2:a:0][3:v:0][3:a:0]concat=n=4:v=1:a=1[outv][outa]" -map "[outv]" -map "[outa]" videos/z.mp4`

--------------------------------------------

* Add Audio

`ffmpeg -i videos/1-1.mp4 -i videos/1-1.mp3 videos/1.mp4`

--------------------------------------------

* Video On Video

```
ffmpeg 
    -i main-video.mp4 -i intro.avi 
    -filter_complex " 
        [0:v]setpts=PTS-STARTPTS,scale=960x720[top]; 
        [1:v]setpts=PTS-STARTPTS,scale=260x120[bottom]; 
        [top][bottom]overlay=x=(W-w)/2:eof_action=pass" 
    -acodec aac -vcodec libx264 out.mp4
```

`ffmpeg -i videos/11.mp4 -i videos/12.mp4 -filter_complex "[0:v]setpts=PTS-STARTPTS,scale=960x720[top]; [1:v]setpts=PTS-STARTPTS,scale=320x240[bottom]; [top][bottom]overlay=x=(W-w)/2:eof_action=pass" -acodec aac -vcodec libx264 videos/z.mp4`



