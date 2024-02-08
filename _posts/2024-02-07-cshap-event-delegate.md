---
title: C# Event and Delegate
date: 2023-02-07 01:01:01 +0700
categories: [C#, Event, Delegate]
tags: [c#]     # TAG names should always be lowercase
---

# 1. Introduction
Nội dung bài viết liên quan tới việc giao tiếp giữa hai object sử dụng Event

# 2. Events 
A mechanism for communication between objects
Used in building loosely coupled applications
Helps extending applications

# 4. Delegates
Agreement/Contract between Publisher and Subcriber
Determines the signature of the event handler method in Subscriber

# 5. Example
Ví dụ VideoEncoder thực hiện hàm encode video, sau khi encode hoàn tất chúng ta có nhu cầu gửi thông tin tới user thông qua MailServer hoặc MessageSever. Cơ chế là khi VideoEncoder hoàn tất quá trình encode sẽ rase lên một event, MailServer và MessageServer lắng nghe bản tin và thực hiện công việc gửi tin nhắn.

## 5.1 Message
Video.cs
``` c#
    public class Video
    {
        public string Title { get; set; }
    }
```

VideoEventArgs.cs
``` c#
    public class VideoEventArgs : EventArgs
    {
        public Video Video { get; set; }
    }
```

## 5.2 Publisher
VideoEncoder.cs
``` c#
    public class VideoEncoder
    {
        // 1. Define delegate like contract
        // 2. Define event based on delegate
        // 3. Rase event
        
        //public delegate void VideoEncoderEventHandler(object source, VideoEventArgs args);
        //public event VideoEncoderEventHandler? VideoEncodedEvent;

        public event EventHandler<VideoEventArgs>? VideoEncodedEvent;

        public void Encode(Video video) 
        {
            Console.WriteLine("Encoding Video ... " + video.Title);
            Thread.Sleep(3000);

            OnVideoEncoded(video);
        }

        protected virtual void OnVideoEncoded(Video video)
        {
            if(VideoEncodedEvent != null)
            {
                VideoEncodedEvent(this, new VideoEventArgs() { Video=video});
            }
        }
    }
```

## 5.3 Subcriber
MailServer.cs
``` c#
    public class MailServer
    {
        public void OnVideoEncoded(object source, VideoEventArgs args)
        {
            Console.WriteLine("Mail Server: Sending an email " + args.Video.Title);
        }
    }
```

MessageSever.cs
``` c#
    public class MessageSever
    {
        public void OnVideoEncoded(object source, VideoEventArgs args)
        {
            Console.WriteLine("Message Sever: Sending a text message " + args.Video.Title);
        }
    }
```

# 5.4 Do Subcribe
Probram.cs
``` c#
    private static void Main(string[] args)
    {
        var video = new Video() { Title = "Video 1" };
        var videoEncoder = new VideoEncoder(); //Publisher
        var mailServer = new MailServer(); //Subscriber
        var messageServer = new MessageSever(); //Subscriber

        videoEncoder.VideoEncodedEvent += mailServer.OnVideoEncoded;
        videoEncoder.VideoEncodedEvent += messageServer.OnVideoEncoded;

        videoEncoder.Encode(video);
    }
```