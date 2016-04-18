## Use JavaScipt to Speech Your Text/ 使用JavaScript 拼读你的文本 

在w3c草案中增加了对[Web Speech Api](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html)的支持;主要作用在
两个非常重要的方面:
+ [语音识别](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html#speechreco-section) (将所说的转换成文本文字 / speech to text);
+ [语音合成](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html#tts-section) (将文本文字读出来 / text to speech);

而chrome在版本33发布后宣布对该特性的支持;今天重要介绍第二部分。

### 开始使用

``` js
// 你可以直接打开你的控制台粘贴下面代码
var words = new SpeechSynthesisUtterance('Hello captain');
window.speechSynthesis.speak(words);
```

当然你还可以修改很多参数去调整你的发音:

+ `volume`:声音; 
+ `rate`:发音速度;
+ `pitch`:音调;
+ `voice`:声音;
+ `language`:语言(en,zh,ja...[更多参考](http://www.mathguide.de/info/tools/languagecode.html))

``` js
var words = new SpeechSynthesisUtterance();
var voices = window.speechSynthesis.getVoices();
msg.voice = voices[10]; // 
msg.voiceURI = 'native';
msg.volume = 1; // 0 to 1
msg.rate = 1; // 0.1 to 10
msg.pitch = 2; //0 to 2
msg.text = 'I am Stark';
msg.lang = 'en';

msg.onend = function(e) {
  console.log('Finished in ' + event.elapsedTime + ' seconds.');
};

speechSynthesis.speak(words);
```

#### 设置发音
你可以通过下面函数获取可以使用的发音列表名称
``` js
speechSynthesis.getVoices().forEach(function(voice) {
  console.log(voice.name, voice.default ? '(default)' :'');
});
```
大概你可以获取下面的一个列表
``` js
// 省略一部分结果
Google Deutsch 
Google US English 
Google UK English Female 
Google UK English Male 
Google 日本語 
Google 普通话（中国大陆）  
Google 國語（臺灣） 
```
接下来我们可以试验下改变发音名称
``` js
var msg = new SpeechSynthesisUtterance('hey captain,sometime I just want to break you perfect teeth');
msg.voice = speechSynthesis.getVoices().filter(function(voice) { return voice.name == 'Google US English'; })[0];
speechSynthesis.speak(msg);
```

除了英文，我们还可以使用其他语言
``` JS
// 使用日语
var msg = new SpeechSynthesisUtterance('おはようございます');
msg.voice = speechSynthesis.getVoices().filter(function(voice) { return voice.name == 'Google 日本語'; })[0];
speechSynthesis.speak(msg);
// or 使用中文
var msg = new SpeechSynthesisUtterance('美国队长3');
msg.voice = speechSynthesis.getVoices().filter(function(voice) { return voice.name == 'Google 普通话（中国大陆）'; })[0];
speechSynthesis.speak(msg);
```


### 浏览器支持

+ Chrome 33+
+ iOS7 safari部分支持 (测试iOS8支持,iOS9不支持)

 兼容性检测
 
```js
if ('speechSynthesis' in window) {
 // Synthesis support. Make your web apps talk!
}

```
如果对于不支持的浏览器，我们可以使用老的方法，即将需要发音的单词发送到服务端进行处理，返回一个音频，类似如下:
``` js
// 使用来自谷歌翻译的音频
var audio = new Audio();
audio.src ='http://translate.google.com/translate_tts?ie=utf-8&tl=en&q=' + encodeURI('hello captain');
audio.play();
```

### 推荐框架

当然我们如果追求快速开发的话，我们现在依旧有成熟的框架来支持这个功能，让他实现更多浏览器的支持。
+ [ResponsiveVoice.JS](http://responsivevoice.org/) 是一款基于html5的跨平台的发音支持类库，支持超过56种语言和168种
声音，分为免费版和商业版。[Demo](http://events.jackpu.com/text-to-speech/)

+ [speak.js](https://github.com/kripken/speak.js/) 基于eSpeack改造而来的一款js单词拼读类库.

+ [meSpeak.js ](http://www.masswerk.at/mespeak/)是一个100%的客户端发音类库，支持chrome和safari，并且无需要任何html元素；

+ [say.js](https://github.com/marak/say.js/)一款基于node.js的发音扩展类库。

持续更新中...

### 参考

[1] [Web apps that talk - Introduction to the Speech Synthesis API
](https://developers.google.com/web/updates/2014/01/Web-apps-that-talk-Introduction-to-the-Speech-Synthesis-API?hl=en) 

[2] [using-google-text-to-speech-in-javascript](http://stackoverflow.com/questions/15653145/using-google-text-to-speech-in-javascript)

[3] [A More Awesome Web: Features You've Always Wanted - Google I/O 2013
](https://www.youtube.com/watch?time_continue=1695&v=N_wTBKMuJis)

[4] [HTML Speech API Examples](https://lists.w3.org/Archives/Public/public-xg-htmlspeech/2011Nov/att-0008/web-speech-sample-code.html)



