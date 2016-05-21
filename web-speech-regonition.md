# 使用 JavaScript 进行语音识别

之前写过了[语音合成,即是进行文字发音](https://github.com/JackPu/text-to-speech)，当然现在也支持了语音识别，
即将你所说的转化成文字。Chrome 浏览器在版本25之后开始对这一特性的支持。

### 基础用法

``` javascript
var recognition = new webkitSpeechRecognition();
recognition.onresult = function(event) { 
  console.log(event) 
}
recognition.start();

```






### 参考

+ [The HTML5 Speech Recognition API](http://shapeshed.com/html5-speech-recognition-api/)

+ [Voice Driven Web Apps: Introduction to the Web Speech API](https://developers.google.com/web/updates/2013/01/Voice-Driven-Web-Apps-Introduction-to-the-Web-Speech-API?hl=en)

