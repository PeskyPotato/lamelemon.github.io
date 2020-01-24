---
layout: post
title: Useful terminal commands and tools
date: 2019-10-25 13:55:58
link: /posts/terminal-commands
categories: posts
description: Useful terminal commands and tools to refer too
keywords: "linux, bash, tools, commands, terminal"
parentPost: true
authors:
    - PeskyPotato
---

## Introduction
These are commands and tools that I use often but need help remembering. 

## Contents
- [Introduction](#introduction)
- [ffmpeg](#ffmpeg)
    - [Concatenate two video files with audio](#concatenate-two-video-files-with-audio)
    - [Convert video to gif](#convert-video-to-gif)
    - [Create webm for 4chan](#create-webm-for-4chan)
    - [Merge audio and video](#merge-audio-and-video)
    - [Reverse video and audio](#reverse-video-and-audio)
    - [Trim video](#trim-video)
    - [Resources](#resources)
- [tar](#tar)
    - [Create an archive](#create-an-archive)
    - [Create a gzip compressed archive](#create-a-gzip-compressed-archive)
    - [Extract an archive](#extract-an-archive)
    - [Extract a gzip compressed tar archive](#extract-a-gzip-compressed-tar-archive)
    - [List files in an archive](#list-files-in-an-archive)
    - [List files in a compressed archive](#list-files-in-a-compressed-archive)
    - [Extract a specific file from an archive](#extract-a-specific-file-from-an-archive)

---
## ffmpeg

### Concatenate two video files with audio
(with the same codec)
```
ffmpeg -i cut.mkv -i cut_reversed.mkv -filter_complex "[0:v] [0:a] [1:v] [1:a] concat=n=2:v=1:a=1 [v] [a]" -map "[v]" -map "[a]" combined.mkv
```

| <!-- -->            | <!-- -->                                                                      |
| :-----------------: |:----------------------------------------------------------------------------- |
| -i                  | Specify input filename                                                        |
| -filter_complex     | Creates a complex filtergraph with inputs and/or outputs                      |
| -map                | Designate one or more input streams as the srouce for the output file         |

Explanation:
- [FFmpeg Concatenate](https://trac.ffmpeg.org/wiki/Concatenate)

### Convert video to gif
```
ffmpeg -y -i combined.mkv -vf fps=24,scale=1080:-1:flags=lanczos,palettegen palette.png
ffmpeg  -i combined.mkv -i palette.png -filter_complex "fps=24,scale=1080:-1:flags=lanczos[x];[x][1:v]paletteuse" out.gif 
```

| <!-- -->            | <!-- -->                                                 |
| :-----------------: |:-------------------------------------------------------- |
| -y                  | Overwrite output without asking                          |
| -i                  | Specify input filename                                   |
| -vf                 | Video filtergraph                                        |
| -filter_complex     | Creates a complex filtergraph with inputs and/or outputs |

Explanation and other resources:
- [How to make GIFS with FFMPEG (GIPHY Engineering)](https://engineering.giphy.com/how-to-make-gifs-with-ffmpeg/)
- [High quality GIF with FFmpeg](http://blog.pkh.me/p/21-high-quality-gif-with-ffmpeg.html)
- ["You can't just code a gif"](https://www.reddit.com/r/HighQualityGifs/comments/8kzru8/you_cant_just_code_a_gif/)

### Create webm for 4chan
```
ffmpeg -i your_video.mkv -ss 00:00:10.000 -to 00:00:20.000 -c:v libvpx -crf 4 -b:v 1500K -vf scale=640:-1 -ac 1 -c:a libvorbis output.webm
```

| <!-- -->            | <!-- -->                                                                                   |
| :-----------------: |:------------------------------------------------------------------------------------------ |
| -ss                 | Seek start position                                                                        |
| -to                 | Seek end position                                                                          |
| -c:v                | Encode all video streams                                                                   |
| -crf                | Cosntant Rate Factor, range from 0-51, lower is better quality                             |
| -b:v                | Set bitrate of video output file                                                           |
| -vf                 | Video filtergraph, used in this case to set width with automatic height according to ratio |
| -ac                 | Set number of audio channels, int his case to 1 so we reduce file size                     |
| -c:a                | Encode all audio streams                                                                   |

### Merge audio and video
Applies if video has audio
```
ffmpeg -i video.mkv -i audio.mp3 -c:v copy -c:a aac -strict experimental -map 0:v:0 -map 1:a:0 ouput.mkv
```

| <!-- -->            | <!-- -->                                                                      |
| :-----------------: |:----------------------------------------------------------------------------- |
| -i                  | Specify input filename                                                        |
| -c:v                | Encode all video streams                                                      |
| -c:a                | Encode all audio streams                                                      |
| -strict             | Specify how strictly to follow the standards                                  |
| -map                | Designate one or more input streams as the srouce for the output file         |


### Reverse video and audio
```
ffmpeg -i input.mkv -vf reverse -af areverse output.mkv
```

| <!-- -->            | <!-- -->                                                                      |
| :-----------------: |:----------------------------------------------------------------------------- |
| -i                  | Specify input filename                                                        |
| -vf                 | Video filtergraph                                                             |
| -t                  | Audio filtergraph                                                             |
 
### Trim video
```
ffmpeg -i input.mkv -ss 00:00:03 -t 00:00:08 -async 1 output.mkv
```

| <!-- -->            | <!-- -->                                                                      |
| :-----------------: |:----------------------------------------------------------------------------- |
| -i                  | Specify input filename                                                        |
| -ss                 | Seek start position                                                           |
| -t                  | Duration after start position                                                 |
| -async 1            | Start of audio stream is synchronised                                         |

### Resources
- [ffmpeg Documentation](https://www.ffmpeg.org/ffmpeg.html) - Official FFmpeg documentation
- [ffmprovisor](https://amiaopensource.github.io/ffmprovisr/) - A repository of useful FFmpeg commands for archivists

----
## tar

### Create an archive
```
tar -cvf send.tar send/ 
```

| <!-- -->            | <!-- -->               |
| :-----------------: |:---------------------- |
| -c                  | Create an archive      |
| -v                  | Verbose                |
| -f                  | Specify filename       |

### Create a gzip compressed archive
```
tar -czvf send.tar.gz send/
```

| <!-- -->            | <!-- -->                       |
| :-----------------: |:----------------------         |
| -c                  | Create an archive              |
| -z                  | Compress archive with gzip     |
| -v                  | Verbose                        |
| -f                  | Specify filename               |

### Extract an archive
```
tar -xvf send.tar
```

| <!-- -->            | <!-- -->                       |
| :-----------------: |:----------------------         |
| -x                  | Extract an archive             |
| -v                  | Verbose                        |
| -f                  | Specify filename               |

### Extract a gzip compressed tar archive
```
tar -xvzf send.tar
```

| <!-- -->            | <!-- -->                       |
| :-----------------: |:----------------------         |
| -x                  | Extract an archive             |
| -v                  | Verbose                        |
| -z                  | Decompress using gzip          |
| -f                  | Specify filename               |

### List files in an archive
```
tar -tvf send.tar
```

| <!-- -->            | <!-- -->                       |
| :-----------------: |:----------------------         |
| -t                  | List contents                  |
| -v                  | Verbose                        |
| -f                  | Specify filename               |

### List files in a compressed archive
```
tar -tzvf send.tar.gz
```

| <!-- -->            | <!-- -->                       |
| :-----------------: |:----------------------         |
| -t                  | List contents                  |
| -z                  | Decompress using gzip          |
| -v                  | Verbose                        |
| -f                  | Specify filename               |

### Extract a specific file from an archive
```
tar -xvf send.tar my_taxes.xlsx scan.pdf
```

| <!-- -->            | <!-- -->                       |
| :-----------------: |:----------------------         |
| -x                  | Extract an archive             |
| -v                  | Verbose                        |
| -f                  | Specify filename               |

`:)`
