---
layout : post
category : blog
tags : [Html5]
---

how to check html5 works in your brower ?  I found two ways for this , if you find other ways to test , please comment to me , thank you . :D 

#####First : create one JS with new HTML5 Element , such as `video` ,`audio` and so on. here comes an example . 

    <p>your browser support video? </p> 

    <div id="checkVideoResult" style="margin:10px 0 0 0; border:0;padding:0;">
      <button onclick="checkVideo()" style="font-family:Arial, Helvetica,sans-serif;">Check</button>
    </div>

    <script type="text/javascript">
    function checkVideo()
      { 
        if(!!document.createElement('video').canPlayType)
          { 
            var vidTest=document.createElement("video");
            oggTest=vidTest.canPlayType('video/ogg; codecs="theora, vorbis"');
    if (!oggTest)
    {
      h264Test=vidTest.canPlayType('video/mp4; codecs="avc1.42E01E,mp4a.40.2"');
        if (!h264Test)
          {
            document.getElementById("checkVideoResult").innerHTML="Sorry. No video support."
          }
        else
          {
            if (h264Test=="probably")
              {
                document.getElementById("checkVideoResult").innerHTML="Yes! Full support!";
              }
            else
              {
                document.getElementById("checkVideoResult").innerHTML="Well. Some support.";
               }
         }
    }
    else
    {
      if (oggTest=="probably")
      {
        document.getElementById("checkVideoResult").innerHTML="Yes! Full support!";
      }
      else
      {
        document.getElementById("checkVideoResult").innerHTML="Well.Some support.";
      }
    }
     }
      else
     {
       document.getElementById("checkVideoResult").innerHTML="Sorry. No video support."
     }
    }
    </script>

But this method seems not a simple and neat way. so I think the second way would be better . 

#####Second : use `Moderniz` js lib. 

Download : http://modernizr.com/downloads/modernizr-2.5.3.js ; Document : http://modernizr.com/docs/ 

an example : 

    <script>
      function test(){
        if (Modernizr.canvas){
          document.getElementById("test").innerHTML="ok , canvas can be used";
        } else {
          document.getElementById("test").innerHTML="Sorry. cavas can not be used";
          }
        }
    </script>


    <p>test support HTML5 canvas</p>

    <div id="test" style="margin:10px 0 0 0; border:0;padding:0;">
      <button onclick="test()" style="font-family:Arial, Helvetica,sans-serif;">Check</button>
    </div>





 
