<pre>flex
{
  display:-webkit-box;
  display:-ms-flexbox;
  display:-webkit-flex;
  display:flex;
}
{
  box-flex:1;
  -webkit-box-flex:1;
  -webkit-flex:1;
  -ms-flex:1;
  flex:1
  //兼容低端浏览器 平分空间
  width:0;
}</pre></br>
左上角倾斜标签</br>
<pre>
  '<div class="lanren">
     <img src="img/active/active.jpg" style="width:100%;">
     <div class="ribbon-lanren-green"><div class="ribbon-green active-bg1">进行中</div></div>
  </div>'
</pre>
<pre>
.lanren {
	position: relative;
    overflow: hidden;
    margin-top:-10px;
}
.lanren .ribbon-lanren-green {
	width: 85px;
	height: 88px;
	overflow: hidden;
	position: absolute;
	top: 0;
	left:0;
}
.lanren .ribbon-green {
	font: bold 15px Sans-Serif;
	text-align: center;
	text-shadow: rgba(255, 255, 255, 0.5) 0px 1px 0px;
	-webkit-transform: rotate(-45deg);
	-moz-transform: rotate(-45deg);
	-ms-transform: rotate(-45deg);
	-o-transform: rotate(-45deg);
	position: relative;
	padding: 7px 0;
	left: -35px;
	top:11px;
	width: 120px;
	-webkit-box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.3);
	-moz-box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.3);
	box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.3);
	background-color: #fff;
}
</pre>
