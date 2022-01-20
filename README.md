# rtmp-streamer [![npm version](https://badge.fury.io/js/rtmp-streamer.svg)](https://badge.fury.io/js/rtmp-streamer)

<a href="http://www.wtfpl.net/"><img
       src="http://www.wtfpl.net/wp-content/uploads/2012/12/wtfpl-badge-4.png"
       width="80" height="15" alt="WTFPL" /></a>
       
[![NPM](https://nodei.co/npm/rtmp-streamer.png)](https://npmjs.org/package/rtmp-streamer)

> 브라우저에 포함된 swf를 통해 rtmp 스트림을 푸시하는 javascript 라이브러리


#### Demo

모든 http 컨테이너에 프로젝트 디렉토리를 로드하여 실행 demo

처럼 [http-server](https://www.npmjs.com/package/http-server):

```bash
 $ http-server -p 8888 
```

또는 [PHP build-in web server](http://php.net/manual/en/features.commandline.webserver.php):

```bash
 $ php -S 0.0.0.0:8888 
```

입장 `http://localhost:8888/demo`

![screenshot](http://blog.chxj.name/content/images/2016/06/screenshot.png)


#### Install

```
 $ npm install rtmp-streamer
```

OR

```
 $ bower install rtmp-streamer
```


#### Tutorial

`rtmp-streamer`는 [AMD](http://requirejs.org/docs/whyamd.html) 사양을 따르며 [`require.js`](http://requirejs.org/) 등을 통해 로드할 수 있습니다. 페이지에 `RtmpStreamer.swf`를 포함해야 합니다. 그렇지 않으면 `rtmp-streamer`가 올바르게 로드되지 않습니다.

```html
<object>
    <embed id="rtmp-streamer" src="../RtmpStreamer.swf" bgcolor="#999999" quality="high"
           width="320" height="240" allowScriptAccess="sameDomain" type="application/x-shockwave-flash"></embed>
</object>
```

```javascript
require(["rtmp-streamer"], function (RtmpStreamer) {
  var streamer = new RtmpStreamer(document.getElementById('rtmp-streamer'));
  streamer.publish(url, name);
});

```


#### Document

```javascript
  /**
   * Push video to RTMP stream from local camera.
   *
   * @param url  - The RTMP stream URL
   * @param name - The RTMP stream name
   */
   function publish(url, name);

  /**
   * Pull video from RTMP stream.
   *
   * @param url  - The RTMP stream URL
   * @param name - The RTMP stream name
   */
   function play(url, name);

  /**
   * Disconnect from RTMP stream
   */
   function disconnect();

  /**
   * Set the screen width and height.
   *
   * @param width  - The screen width (pixels). The default value is 320.
   * @param height - The screen height (pixels). The default value is 240.
   */
   function setScreenSize(width, height);

  /**
   * Set the screen position.
   *
   * @param x - The screen horizontal position (pixels). The default value is 0.
   * @param y - The screen vertical position (pixels). The default value is 0.
   */
   function setScreenPosition(x, y);

  /**
   * Set the camera mode.
   *
   * @param width  - The requested capture width (pixels). The default value is 640.
   * @param height - The requested capture height (pixels). The default value is 480.
   * @param fps    - The requested capture frame rate, in frames per second. The default value is 15.
   */
   function setCamMode(width, height, fps);

  /**
   * Set the camera frame interval.
   *
   * @param frameInterval - The number of video frames transmitted in full (called keyframes) instead of being interpolated by the video compression algorithm.
   * The allowed values are 1 through 300.
   * The default value is 15, which means that every 15th frame is a keyframe. A value of 1 means that every frame is a keyframe.
   */
   function setCamFrameInterval(frameInterval);

  /**
   * Set the camera quality.
   *
   * @param bandwidth - Specifies the maximum amount of bandwidth that the current outgoing video feed can use, in bytes per second (bps).
   *    To specify that the video can use as much bandwidth as needed to maintain the value of quality, pass 0 for bandwidth.
   *    The default value is 200000.
   * @param quality   - An integer that specifies the required level of picture quality, as determined by the amount of compression
   *     being applied to each video frame. Acceptable values range from 1 (lowest quality, maximum compression) to 100
   *    (highest quality, no compression). To specify that picture quality can vary as needed to avoid exceeding bandwidth, pass 0 for quality.
   *    The default value is 90.
   */
   function setCamQuality(bandwidth, quality);

  /**
   * Set the microphone quality.
   *
   * @param quality - The encoded speech quality when using the Speex codec. Possible values are from 0 to 10.
   * Higher numbers represent higher quality but require more bandwidth, as shown in the following table.
   * The bit rate values that are listed represent net bit rates and do not include packetization overhead.
   * ------------------------------------------
   * Quality value | Required bit rate (kbps)
   *-------------------------------------------
   *      0        |       3.95
   *      1        |       5.75
   *      2        |       7.75
   *      3        |       9.80
   *      4        |       12.8
   *      5        |       16.8
   *      6        |       20.6
   *      7        |       23.8
   *      8        |       27.8
   *      9        |       34.2
   *      10       |       42.2
   *-------------------------------------------
   * The default value is 9.
   */
   function setMicQuality(quality);

  /**
   * Set the microphone rate.
   *
   * @param rate - The rate at which the microphone is capturing sound, in kHz. Acceptable values are 5, 8, 11, 22, and 44.
   * The default value is 44.
   */
   function setMicRate(rate);

```


#### RTMP 서버를 빠르게 구축하시겠습니까? 노력하다 Wowza(https://www.wowza.com/free-trial)

[Install & Configuration](https://www.wowza.com/forums/content.php?217-How-to-install-and-configure-Wowza-Streaming-Engine)

![wowza](http://blog.chxj.name/content/images/2016/06/wowza.png)


#### 라이브 스트리밍 클라우드 서비스 채택

테이크 [세븐 니우윤](https://www.qiniu.com/products/pili) 예를 들어:

매개변수를 설정하는 방법은 OBS와 같은 도구를 사용하여 스트림을 푸시하는 방법과 유사하며 주소는 라이브 클라우드의 공간 이름이고 데이터 스트림 이름은 라이브 스트림의 이름에 인증 매개변수를 더한 것입니다.:

![](http://blog.chxj.name/content/images/2017/03/Screen-Shot-2017-03-12-at-3.16.09-PM.png)


Qiniu의 라이브 클라우드 관리 배경에서 푸시 비디오 미리보기:

![](http://blog.chxj.name/content/images/2017/03/Screen-Shot-2017-03-12-at-2.01.27-PM.png)



