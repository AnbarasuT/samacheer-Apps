samacheer-Apps
==============

index.html:
===========

<!DOCTYPE html>
<html>
<head>
    <title>Samacheer App</title>
    
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1" />
    <meta http-equiv="content-type" content="text/html; charset=utf-8">
    <script type="text/javascript" src="./js/cordova-1.8.1.js"></script>
    <script type="text/javascript" src="./js/jquery-1.8.2.min.js"></script>
    <script type="text/javascript" src="./js/jqmath-etc-0.2.0.min.js"></script>
    <script type="text/javascript" src="./js/iscroll.js"></script>
    <script type="text/javascript" src="./js/lolScroll.js"></script>
    <script type="text/javascript" src="./js/lolQuest.js"></script>
    <script type="text/javascript" src="./js/contentTemplate.js"></script>
    <script type="text/javascript" src="./js/questions.js"></script>
    <script type="text/javascript" src="./js/script.js"></script>
    
    <link rel="stylesheet" href="./css/jqmath-0.2.0.css">
    <link rel="stylesheet" href="./css/styles.css">
    <link rel="stylesheet" href="./css/customstyles.css">
    <link rel="stylesheet" href="./css/cover.css">
   
</head>
<body onresize="onPageResize();" onorientationchange="deviceTilted();" onselectstart="return false;" ondragstart="return false;" ontouchstart="event.preventDefault();">
    <div id="masterDiv">
        <div id="mainHolder">
            <div id="contentHolder">
                <div id="content" class="content">
                    <div id="scroller">
                        <div class="questionHolder">
                            <div id="ques" class="question whiteBg"></div>
                        </div>
                        <div class="optionsHolder">
                            <div id="options" class="options blueBg"></div>
                        </div>
                        <div id="response" class="response"></div>
                        <div id="endSpace"><br /><br /></div>
                    </div>
                </div>
            </div>
        </div>

        <div id="navUnitScroller">
            <div id="subNavbar">
                <div style="margin-top:0px;">
                    <div id="left_nav"><img src="commonImages/left.png" id="thumbNavIcon_L" align="absmiddle"></div>
                    <div id="right_nav"><img src="commonImages/right.png" id="thumbNavIcon_R" align="absmiddle"></div>
                </div>
                <div id="navBarHolder">
                    <div id="navBarSlider"></div>
                </div>
            </div>
        </div>
        <div id="footer">
            <div id="questionStatus">
                    <div id="currentQuestionDisp" class="blueBg"></div>
            </div>
            <div id="prevBtn" class="navBtns"></div>
            <div id="nextBtn" class="navBtns"></div>
        </div>
        <div id="semiBlocker" class="blocker"></div>
        <div id="header">
            <div id="headerGrad"></div>
            <div id="headerContent">
                <div id="homeBtn" class="homeBtn"></div><div class="verticalDiv"></div><div id="tocBtn" class="tocBtn"></div><div class="verticalDiv"></div><div id="submitBtn" class="submitBtn"></div>
                <div id="timerContainer">
                    <div id="timerIcon"></div>
                    <div id="timerText"></div>
                </div>
            </div>
        </div>
        <div id="stopScreen">
            <div id="youhave">You have stopped the test.</div>
            <div id="resume" class="popupBtns">RESUME <span class="resumecontent">&mdash; Return to test.</span></div>    
            <div id="quit" class="popupBtns">QUIT <span class="resumecontent">&mdash; Save and exit test.</span></div>
            <div id="submit" class="popupBtns">SUBMIT ANSWERS <span class="resumecontent">&mdash; I am done!</span></div>
        </div>
        <div id="submitScreen">
            <div id="haveyou">Have you finished the test?</div>
            <div id="submitYes" class="popupBtns">YES <span class="resumecontent">&mdash; FINAL SUBMIT</span></div>    
            <div id="submitNo" class="popupBtns">NO <span class="resumecontent">&mdash; I want to return to the test.</span></div>
        </div>
        <div id="fullBlocker" class="blocker"></div>
    </div>
    <div id="testDiv"></div>
    <div id="coverDiv"></div>
<!--    <audio id="clkaudio" src="audio/buttonclick.mp3"></audio><audio id="timeaudio" src="audio/timebeep.mp3"></audio>-->
</body>
</html>






contentTemplate:
===============

var useEvent;
var isTouchDevice = 'ontouchstart' in document.documentElement;
if(isTouchDevice){useEvent = "ontouchstart";}
else{useEvent = "onmousedown";}
var pages = {
	"pageList":{
		"coverPage":"<div style=\"font-weight:bold; text-align:center;\"><div class=\"TitleBg\"></div><div class=\"subTitleBg\"><div class=\"subTitleText\"></div><div class=\"blueBottomBg\"></div></div><div class=\"startBtn\" "+useEvent+"=\"proQ.animationEnded()\"></div></div>",
		
		"homePage":"<div class=\"home frontPages\"><div style=\"display:inline-block;\" id=\"startBtn\" "+useEvent+"=\"proQ.byLoadPage('quiz');\">Quiz</div><br /><div style=\"display:inline-block;\" "+useEvent+"=\"proQ.byLoadPage('tocPage');\">Contents</div><br /><div style=\"display:inline-block;\" "+useEvent+"=\"proQ.byLoadPage('settingsPage');\">Settings</div><br /><div style=\"display:inline-block;\" "+useEvent+"=\"proQ.byLoadPage('instructionPage');\">Instructions</div><br /><div style=\"display:inline-block;\" id=\"myReviewBtn\" "+useEvent+"=\"proQ.tryDisplayResult();\">Review Summary</div></div>",
		
		"settingsPage":"<div class=\"frontPages\"><div class='TocHeading' style='text-align:center; font-weight:bold;'><b>Settings</b><br/></div><br/><div style=\"display:inline-block;\" "+useEvent+"=\"proQ.onResetClick();\">Reset History</div></div>",
		
		"tocPage":"<div class=\"frontPages\"><div class='TocHeading' style='text-align:center; font-weight:bold;'><b>Contents</b><br/></div><br/><div style=\"text-align:left;\" id=\"tocContentHolder\" class=\"blueBg\"></div></div>",
		
		"instructionPage":"<div class='TocHeading' style='text-align:center; font-weight:bold;'><b>Instructions</b><br/></div><div style='text-align:left;' class='introContent'><div><b>Navigation</b></div><div class='imgcenter'><img  style='max-width:100%;' src='./commonImages/instruction_page_nav_bar_1.png' alt='' /></div><div><ol><li>Previous/Next buttons.</li><li>Question Number: Tap to open and close the Sub Navigation Bar.</li></ol></div><div class='imgcenter'><img  style='max-width:100%;' src='./commonImages/instruction_page_nav_bar_2.png' alt='' /></div><div><ol start='3'><li>Sub Navigation Bar in Test mode. Swipe for more questions.</li></ol></div>",
		
		"myReviewPage":"<div id=\"review_page\">"+
				"<div class=\"myreview_head\">My Review</div>"+
				"<div class='reviewHolder'>"+
				"<div style='float:left'>"+
				"<div class=\"review_bold\">Correct:</div>"+
				"<div class=\"review_bold\">Time:</div>"+
				"<div class=\"review_bold\">Missed</div>"+
				"<div class=\"review_normal\">Unanswered:</div>"+
				"<div class=\"review_normal\">Incorrect:</div>"+
				"</div>"+
				"<div style='float:right'>"+
				"<div id=\"resCorrect\" class=\"resultValues\"></div>"+
				"<div id=\"resTime\" class=\"resultValues\"></div>"+
				"<div class=\"resultValues\">&nbsp;</div>"+
				"<div id=\"resUnanswered\" class=\"resultValues\"></div>"+
				"<div id=\"resIncorrect\" class=\"resultValues\"></div>"+
				"</div>"+
				"</div>"+
				"<div id=\"reviewBtn\" "+useEvent+"=\"proQ.nextQuestion();\" class=\"review_whbold reviewBtn\">Examine Test Item Explanations</div>"+
				"<div class=\"tenspace\"></div>"+
				"<div class=\"review_whbold\"><span "+useEvent+"=\"jumpToUrl('http://www.siriustestprep.com/geometry-practicetest-actionplan');\">Additional Online Resources</span></div>"+
				"</div>",
	}
}


iscroll.js
===========

/*!
 * iScroll v4.2.5 ~ Copyright (c) 2012 Matteo Spinelli, http://cubiq.org
 * Released under MIT license, http://cubiq.org/license
 */
(function(window, doc){
var m = Math,
	dummyStyle = doc.createElement('div').style,
	vendor = (function () {
		var vendors = 't,webkitT,MozT,msT,OT'.split(','),
			t,
			i = 0,
			l = vendors.length;

		for ( ; i < l; i++ ) {
			t = vendors[i] + 'ransform';
			if ( t in dummyStyle ) {
				return vendors[i].substr(0, vendors[i].length - 1);
			}
		}

		return false;
	})(),
	cssVendor = vendor ? '-' + vendor.toLowerCase() + '-' : '',

	// Style properties
	transform = prefixStyle('transform'),
	transitionProperty = prefixStyle('transitionProperty'),
	transitionDuration = prefixStyle('transitionDuration'),
	transformOrigin = prefixStyle('transformOrigin'),
	transitionTimingFunction = prefixStyle('transitionTimingFunction'),
	transitionDelay = prefixStyle('transitionDelay'),

    // Browser capabilities
	isAndroid = (/android/gi).test(navigator.appVersion),
	isIDevice = (/iphone|ipad/gi).test(navigator.appVersion),
	isTouchPad = (/hp-tablet/gi).test(navigator.appVersion),

    has3d = prefixStyle('perspective') in dummyStyle,
    hasTouch = 'ontouchstart' in window && !isTouchPad,
    hasTransform = vendor !== false,
    hasTransitionEnd = prefixStyle('transition') in dummyStyle,

	RESIZE_EV = 'onorientationchange' in window ? 'orientationchange' : 'resize',
	START_EV = hasTouch ? 'touchstart' : 'mousedown',
	MOVE_EV = hasTouch ? 'touchmove' : 'mousemove',
	END_EV = hasTouch ? 'touchend' : 'mouseup',
	CANCEL_EV = hasTouch ? 'touchcancel' : 'mouseup',
	TRNEND_EV = (function () {
		if ( vendor === false ) return false;

		var transitionEnd = {
				''			: 'transitionend',
				'webkit'	: 'webkitTransitionEnd',
				'Moz'		: 'transitionend',
				'O'			: 'otransitionend',
				'ms'		: 'MSTransitionEnd'
			};

		return transitionEnd[vendor];
	})(),

	nextFrame = (function() {
		return window.requestAnimationFrame ||
			window.webkitRequestAnimationFrame ||
			window.mozRequestAnimationFrame ||
			window.oRequestAnimationFrame ||
			window.msRequestAnimationFrame ||
			function(callback) { return setTimeout(callback, 1); };
	})(),
	cancelFrame = (function () {
		return window.cancelRequestAnimationFrame ||
			window.webkitCancelAnimationFrame ||
			window.webkitCancelRequestAnimationFrame ||
			window.mozCancelRequestAnimationFrame ||
			window.oCancelRequestAnimationFrame ||
			window.msCancelRequestAnimationFrame ||
			clearTimeout;
	})(),

	// Helpers
	//translateZ = has3d ? ' translateZ(0)' : '',
    translateZ = has3d ? ' translateZ(0)' : '',

	// Constructor
	iScroll = function (el, options) {
		var that = this,
			i;

		that.wrapper = typeof el == 'object' ? el : doc.getElementById(el);
		that.wrapper.style.overflow = 'hidden';
		that.scroller = that.wrapper.children[0];

		// Default options
		that.options = {
			hScroll: true,
			vScroll: true,
			x: 0,
			y: 0,
			bounce: true,
			bounceLock: false,
			momentum: true,
			lockDirection: true,
			useTransform: true,
			useTransition: false,
			topOffset: 0,
			checkDOMChanges: false,		// Experimental
			handleClick: true,

			// Scrollbar
			hScrollbar: true,
			vScrollbar: true,
			fixedScrollbar: isAndroid,
			hideScrollbar: false,
			fadeScrollbar: has3d,
			scrollbarClass: '',

			// Zoom
			zoom: false,
			zoomMin: 1,
			zoomMax: 2,
			doubleTapZoom: 2,
			wheelAction: 'scroll',

			// Snap
			snap: false,
			snapThreshold: 1,

			// Events
			onRefresh: null,
			onBeforeScrollStart: function (e) { e.preventDefault(); },
			onScrollStart: null,
			onBeforeScrollMove: null,
			onScrollMove: null,
			onBeforeScrollEnd: null,
			onScrollEnd: null,
			onTouchEnd: null,
			onDestroy: null,
			onZoomStart: null,
			onZoom: null,
			onZoomEnd: null
		};

		// User defined options
		for (i in options) that.options[i] = options[i];
		
		// Set starting position
		that.x = that.options.x;
		that.y = that.options.y;

		// Normalize options
		that.options.useTransform = hasTransform && that.options.useTransform;
		that.options.hScrollbar = that.options.hScroll && that.options.hScrollbar;
		that.options.vScrollbar = that.options.vScroll && that.options.vScrollbar;
		that.options.zoom = that.options.useTransform && that.options.zoom;
		that.options.useTransition = hasTransitionEnd && that.options.useTransition;

		// Helpers FIX ANDROID BUG!
		// translate3d and scale doesn't work together!
		// Ignoring 3d ONLY WHEN YOU SET that.options.zoom
		if ( that.options.zoom && isAndroid ){
			translateZ = '';
		}
		translateZ = '';
		// Set some default styles
		that.scroller.style[transitionProperty] = that.options.useTransform ? cssVendor + 'transform' : 'top left';
		that.scroller.style[transitionDuration] = '0';
		that.scroller.style[transformOrigin] = '0 0';
		if (that.options.useTransition) that.scroller.style[transitionTimingFunction] = 'cubic-bezier(0.33,0.66,0.66,1)';
		
		if (that.options.useTransform) that.scroller.style[transform] = 'translate(' + that.x + 'px,' + that.y + 'px)' + translateZ;
		else that.scroller.style.cssText += ';position:absolute;top:' + that.y + 'px;left:' + that.x + 'px';

		if (that.options.useTransition) that.options.fixedScrollbar = true;

		that.refresh();

		that._bind(RESIZE_EV, window);
		that._bind(START_EV);
		if (!hasTouch) {
			if (that.options.wheelAction != 'none') {
				that._bind('DOMMouseScroll');
				that._bind('mousewheel');
			}
		}

		if (that.options.checkDOMChanges) that.checkDOMTime = setInterval(function () {
			that._checkDOMChanges();
		}, 500);
	};

// Prototype
iScroll.prototype = {
	enabled: true,
	x: 0,
	y: 0,
	steps: [],
	scale: 1,
	currPageX: 0, currPageY: 0,
	pagesX: [], pagesY: [],
	aniTime: null,
	wheelZoomCount: 0,
	
	handleEvent: function (e) {
		var that = this;
		switch(e.type) {
			case START_EV:
				if (!hasTouch && e.button !== 0) return;
				that._start(e);
				break;
			case MOVE_EV: that._move(e); break;
			case END_EV:
			case CANCEL_EV: that._end(e); break;
			case RESIZE_EV: that._resize(); break;
			case 'DOMMouseScroll': case 'mousewheel': that._wheel(e); break;
			case TRNEND_EV: that._transitionEnd(e); break;
		}
	},
	
	_checkDOMChanges: function () {
		if (this.moved || this.zoomed || this.animating ||
			(this.scrollerW == this.scroller.offsetWidth * this.scale && this.scrollerH == this.scroller.offsetHeight * this.scale)) return;

		this.refresh();
	},
	
	_scrollbar: function (dir) {
		var that = this,
			bar;

		if (!that[dir + 'Scrollbar']) {
			if (that[dir + 'ScrollbarWrapper']) {
				if (hasTransform) that[dir + 'ScrollbarIndicator'].style[transform] = '';
				that[dir + 'ScrollbarWrapper'].parentNode.removeChild(that[dir + 'ScrollbarWrapper']);
				that[dir + 'ScrollbarWrapper'] = null;
				that[dir + 'ScrollbarIndicator'] = null;
			}

			return;
		}

		if (!that[dir + 'ScrollbarWrapper']) {
			// Create the scrollbar wrapper
			bar = doc.createElement('div');
 
			if (that.options.scrollbarClass) bar.className = that.options.scrollbarClass + dir.toUpperCase();
			else bar.style.cssText = 'position:absolute;z-index:100;' + (dir == 'h' ? 'height:7px;bottom:1px;left:2px;right:' + (that.vScrollbar ? '7' : '2') + 'px' : 'width:7px;bottom:' + (that.hScrollbar ? '7' : '2') + 'px;top:2px;right:1px');

			bar.style.cssText += ';pointer-events:none;' + cssVendor + 'transition-property:opacity;' + cssVendor + 'transition-duration:' + (that.options.fadeScrollbar ? '350ms' : '0') + ';overflow:hidden;opacity:' + (that.options.hideScrollbar ? '0' : '1');

			that.wrapper.appendChild(bar);
			that[dir + 'ScrollbarWrapper'] = bar;

			// Create the scrollbar indicator
            bar.id = "lolScrollBar"+dir.toUpperCase();
			bar = doc.createElement('div');
			if (!that.options.scrollbarClass) {
				bar.style.cssText = 'position:absolute;z-index:100;background:rgba(0,0,0,0.5);border:1px solid rgba(255,255,255,0.9);' + cssVendor + 'background-clip:padding-box;' + cssVendor + 'box-sizing:border-box;' + (dir == 'h' ? 'height:100%' : 'width:100%') + ';' + cssVendor + 'border-radius:3px;border-radius:3px';
			}
			bar.style.cssText += ';pointer-events:none;' + cssVendor + 'transition-property:' + cssVendor + 'transform;' + cssVendor + 'transition-timing-function:cubic-bezier(0.33,0.66,0.66,1);' + cssVendor + 'transition-duration:0;' + cssVendor + 'transform: translate(0,0)' + translateZ;
			if (that.options.useTransition) bar.style.cssText += ';' + cssVendor + 'transition-timing-function:cubic-bezier(0.33,0.66,0.66,1)';

			that[dir + 'ScrollbarWrapper'].appendChild(bar);
			that[dir + 'ScrollbarIndicator'] = bar;
		}

		if (dir == 'h') {
			that.hScrollbarSize = that.hScrollbarWrapper.clientWidth;
			that.hScrollbarIndicatorSize = m.max(m.round(that.hScrollbarSize * that.hScrollbarSize / that.scrollerW), 8);
			that.hScrollbarIndicator.style.width = that.hScrollbarIndicatorSize + 'px';
			that.hScrollbarMaxScroll = that.hScrollbarSize - that.hScrollbarIndicatorSize;
			that.hScrollbarProp = that.hScrollbarMaxScroll / that.maxScrollX;
		} else {
			that.vScrollbarSize = that.vScrollbarWrapper.clientHeight;
			that.vScrollbarIndicatorSize = m.max(m.round(that.vScrollbarSize * that.vScrollbarSize / that.scrollerH), 8);
			that.vScrollbarIndicator.style.height = that.vScrollbarIndicatorSize + 'px';
			that.vScrollbarMaxScroll = that.vScrollbarSize - that.vScrollbarIndicatorSize;
			that.vScrollbarProp = that.vScrollbarMaxScroll / that.maxScrollY;
		}

		// Reset position
		that._scrollbarPos(dir, true);
	},
	
	_resize: function () {
		var that = this;
		setTimeout(function () { that.refresh(); }, isAndroid ? 200 : 0);
	},
	
	_pos: function (x, y) {
		if (this.zoomed) return;

		x = this.hScroll ? x : 0;
		y = this.vScroll ? y : 0;
		if (this.options.useTransform) {
			this.scroller.style[transform] = 'translate(' + x + 'px,' + y + 'px) scale(' + this.scale + ')' + translateZ;
		} else {
			x = m.round(x);
			y = m.round(y);
			this.scroller.style.left = x + 'px';
			this.scroller.style.top = y + 'px';
		}

		this.x = x;
		this.y = y;

		this._scrollbarPos('h');
		this._scrollbarPos('v');
	},

	_scrollbarPos: function (dir, hidden) {
		var that = this,
			pos = dir == 'h' ? that.x : that.y,
			size;

		if (!that[dir + 'Scrollbar']) return;

		pos = that[dir + 'ScrollbarProp'] * pos;

		if (pos < 0) {
			if (!that.options.fixedScrollbar) {
				size = that[dir + 'ScrollbarIndicatorSize'] + m.round(pos * 3);
				if (size < 8) size = 8;
				that[dir + 'ScrollbarIndicator'].style[dir == 'h' ? 'width' : 'height'] = size + 'px';
			}
			pos = 0;
		} else if (pos > that[dir + 'ScrollbarMaxScroll']) {
			if (!that.options.fixedScrollbar) {
				size = that[dir + 'ScrollbarIndicatorSize'] - m.round((pos - that[dir + 'ScrollbarMaxScroll']) * 3);
				if (size < 8) size = 8;
				that[dir + 'ScrollbarIndicator'].style[dir == 'h' ? 'width' : 'height'] = size + 'px';
				pos = that[dir + 'ScrollbarMaxScroll'] + (that[dir + 'ScrollbarIndicatorSize'] - size);
			} else {
				pos = that[dir + 'ScrollbarMaxScroll'];
			}
		}

		that[dir + 'ScrollbarWrapper'].style[transitionDelay] = '0';
		that[dir + 'ScrollbarWrapper'].style.opacity = hidden && that.options.hideScrollbar ? '0' : '1';
		that[dir + 'ScrollbarIndicator'].style[transform] = 'translate(' + (dir == 'h' ? pos + 'px,0)' : '0,' + pos + 'px)') + translateZ;
	},
	
	_start: function (e) {
		var that = this,
			point = hasTouch ? e.touches[0] : e,
			matrix, x, y,
			c1, c2;

		if (!that.enabled) return;
		
		var scrollStartRes;
		if (that.options.onBeforeScrollStart) scrollStartRes = that.options.onBeforeScrollStart.call(that, e);
		if (scrollStartRes == false) return;

		if (that.options.useTransition || that.options.zoom) that._transitionTime(0);

		that.moved = false;
		that.animating = false;
		that.zoomed = false;
		that.distX = 0;
		that.distY = 0;
		that.absDistX = 0;
		that.absDistY = 0;
		that.dirX = 0;
		that.dirY = 0;

		// Gesture start
		if (that.options.zoom && hasTouch && e.touches.length > 1) {
			c1 = m.abs(e.touches[0].pageX-e.touches[1].pageX);
			c2 = m.abs(e.touches[0].pageY-e.touches[1].pageY);
			that.touchesDistStart = m.sqrt(c1 * c1 + c2 * c2);

			that.originX = m.abs(e.touches[0].pageX + e.touches[1].pageX - that.wrapperOffsetLeft * 2) / 2 - that.x;
			that.originY = m.abs(e.touches[0].pageY + e.touches[1].pageY - that.wrapperOffsetTop * 2) / 2 - that.y;

			if (that.options.onZoomStart) that.options.onZoomStart.call(that, e);
		}

		if (that.options.momentum) {
			if (that.options.useTransform) {
				// Very lame general purpose alternative to CSSMatrix
				matrix = getComputedStyle(that.scroller, null)[transform].replace(/[^0-9\-.,]/g, '').split(',');
				x = +(matrix[12] || matrix[4]);
				y = +(matrix[13] || matrix[5]);
			} else {
				x = +getComputedStyle(that.scroller, null).left.replace(/[^0-9-]/g, '');
				y = +getComputedStyle(that.scroller, null).top.replace(/[^0-9-]/g, '');
			}
			
			if (x != that.x || y != that.y) {
				if (that.options.useTransition) that._unbind(TRNEND_EV);
				else cancelFrame(that.aniTime);
				that.steps = [];
				that._pos(x, y);
				if (that.options.onScrollEnd) that.options.onScrollEnd.call(that);
			}
		}

		that.absStartX = that.x;	// Needed by snap threshold
		that.absStartY = that.y;

		that.startX = that.x;
		that.startY = that.y;
		that.pointX = point.pageX;
		that.pointY = point.pageY;

		that.startTime = e.timeStamp || Date.now();
		if (that.options.onScrollStart) that.options.onScrollStart.call(that, e);

		that._bind(MOVE_EV, window);
		that._bind(END_EV, window);
		that._bind(CANCEL_EV, window);
	},
	
	_move: function (e) {
		var that = this,
			point = hasTouch ? e.touches[0] : e,
			deltaX = point.pageX - that.pointX,
			deltaY = point.pageY - that.pointY,
			newX = that.x + deltaX,
			newY = that.y + deltaY,
			c1, c2, scale,
			timestamp = e.timeStamp || Date.now();

		if (that.options.onBeforeScrollMove) that.options.onBeforeScrollMove.call(that, e);

		// Zoom
		if (that.options.zoom && hasTouch && e.touches.length > 1) {
			c1 = m.abs(e.touches[0].pageX - e.touches[1].pageX);
			c2 = m.abs(e.touches[0].pageY - e.touches[1].pageY);
			that.touchesDist = m.sqrt(c1*c1+c2*c2);

			that.zoomed = true;
 
            that.originX = m.abs(e.touches[0].pageX + e.touches[1].pageX - that.wrapperOffsetLeft * 2) / 2 - that.x;
            that.originY = m.abs(e.touches[0].pageY + e.touches[1].pageY - that.wrapperOffsetTop * 2) / 2 - that.y;

			scale = 1 / that.touchesDistStart * that.touchesDist * this.scale;

			if (scale < that.options.zoomMin) scale = 0.5 * that.options.zoomMin * Math.pow(2.0, scale / that.options.zoomMin);
			else if (scale > that.options.zoomMax) scale = 2.0 * that.options.zoomMax * Math.pow(0.5, that.options.zoomMax / scale);

			that.lastScale = scale / this.scale;
			newX = this.originX - this.originX * that.lastScale + this.x;
			newY = this.originY - this.originY * that.lastScale + this.y;
 //if(scale < that.options.zoomMin){scale = that.options.zoomMin; return;}
// else if(scale > that.options.zoomMax){scale = that.options.zoomMax; return;}
 
			this.scroller.style[transform] = 'translate(' + newX + 'px,' + newY + 'px) scale(' + scale + ')' + translateZ;

			if (that.options.onZoom) that.options.onZoom.call(that, e);
			//return;
		}

		that.pointX = point.pageX;
		that.pointY = point.pageY;

		// Slow down if outside of the boundaries
		if (newX > 0 || newX < that.maxScrollX) {
			newX = that.options.bounce ? that.x + (deltaX / 2) : newX >= 0 || that.maxScrollX >= 0 ? 0 : that.maxScrollX;
		}
		if (newY > that.minScrollY || newY < that.maxScrollY) {
			newY = that.options.bounce ? that.y + (deltaY / 2) : newY >= that.minScrollY || that.maxScrollY >= 0 ? that.minScrollY : that.maxScrollY;
		}

		that.distX += deltaX;
		that.distY += deltaY;
		that.absDistX = m.abs(that.distX);
		that.absDistY = m.abs(that.distY);

		if (that.absDistX < 6 && that.absDistY < 6) {
			return;
		}

		// Lock direction
		if (that.options.lockDirection) {
			if (that.absDistX > that.absDistY + 5) {
				newY = that.y;
				deltaY = 0;
			} else if (that.absDistY > that.absDistX + 5) {
				newX = that.x;
				deltaX = 0;
			}
		}

		that.moved = true;
		that._pos(newX, newY);
		that.dirX = deltaX > 0 ? -1 : deltaX < 0 ? 1 : 0;
		that.dirY = deltaY > 0 ? -1 : deltaY < 0 ? 1 : 0;

		if (timestamp - that.startTime > 300) {
			that.startTime = timestamp;
			that.startX = that.x;
			that.startY = that.y;
		}
		
		if (that.options.onScrollMove) that.options.onScrollMove.call(that, e);
	},
	
	_end: function (e) {
		if (hasTouch && e.touches.length !== 0) return;

		var that = this,
			point = hasTouch ? e.changedTouches[0] : e,
			target, ev,
			momentumX = { dist:0, time:0 },
			momentumY = { dist:0, time:0 },
			duration = (e.timeStamp || Date.now()) - that.startTime,
			newPosX = that.x,
			newPosY = that.y,
			distX, distY,
			newDuration,
			snap,
			scale;

		that._unbind(MOVE_EV, window);
		that._unbind(END_EV, window);
		that._unbind(CANCEL_EV, window);

		if (that.options.onBeforeScrollEnd) that.options.onBeforeScrollEnd.call(that, e);

		if (that.zoomed) {
			scale = that.scale * that.lastScale;
			scale = Math.max(that.options.zoomMin, scale);
			scale = Math.min(that.options.zoomMax, scale);
			that.lastScale = scale / that.scale;
			that.scale = scale;

			that.x = that.originX - that.originX * that.lastScale + that.x;
			that.y = that.originY - that.originY * that.lastScale + that.y;
			
			//that.scroller.style[transitionDuration] = '200ms';
			that.scroller.style[transform] = 'translate(' + that.x + 'px,' + that.y + 'px) scale(' + that.scale + ')' + translateZ;
			
			that.zoomed = false;
			that.refresh();
			if (that.options.onZoomEnd) that.options.onZoomEnd.call(that, e);
			return;
		}

		if (!that.moved) {
			if (hasTouch) {
				if (that.doubleTapTimer && that.options.zoom) {
					// Double tapped
					clearTimeout(that.doubleTapTimer);
					that.doubleTapTimer = null;
					if (that.options.onZoomStart) that.options.onZoomStart.call(that, e);
					that.zoom(that.pointX, that.pointY, that.scale == 1 ? that.options.doubleTapZoom : 1);
					if (that.options.onZoomEnd) {
						setTimeout(function() {
							that.options.onZoomEnd.call(that, e);
						}, 200); // 200 is default zoom duration
					}
				} else if (this.options.handleClick) {
					that.doubleTapTimer = setTimeout(function () {
						that.doubleTapTimer = null;

						// Find the last touched element
						target = point.target;
						while (target.nodeType != 1) target = target.parentNode;

						if (target.tagName != 'SELECT' && target.tagName != 'INPUT' && target.tagName != 'TEXTAREA') {
							ev = doc.createEvent('MouseEvents');
							ev.initMouseEvent('click', true, true, e.view, 1,
								point.screenX, point.screenY, point.clientX, point.clientY,
								e.ctrlKey, e.altKey, e.shiftKey, e.metaKey,
								0, null);
							ev._fake = true;
							target.dispatchEvent(ev);
						}
					}, that.options.zoom ? 250 : 0);
				}
			}

			that._resetPos(400);

			if (that.options.onTouchEnd) that.options.onTouchEnd.call(that, e);
			return;
		}

		if (duration < 300 && that.options.momentum) {
			momentumX = newPosX ? that._momentum(newPosX - that.startX, duration, -that.x, that.scrollerW - that.wrapperW + that.x, that.options.bounce ? that.wrapperW : 0) : momentumX;
			momentumY = newPosY ? that._momentum(newPosY - that.startY, duration, -that.y, (that.maxScrollY < 0 ? that.scrollerH - that.wrapperH + that.y - that.minScrollY : 0), that.options.bounce ? that.wrapperH : 0) : momentumY;

			newPosX = that.x + momentumX.dist;
			newPosY = that.y + momentumY.dist;

			if ((that.x > 0 && newPosX > 0) || (that.x < that.maxScrollX && newPosX < that.maxScrollX)) momentumX = { dist:0, time:0 };
			if ((that.y > that.minScrollY && newPosY > that.minScrollY) || (that.y < that.maxScrollY && newPosY < that.maxScrollY)) momentumY = { dist:0, time:0 };
		}

		if (momentumX.dist || momentumY.dist) {
			newDuration = m.max(m.max(momentumX.time, momentumY.time), 10);

			// Do we need to snap?
			if (that.options.snap) {
				distX = newPosX - that.absStartX;
				distY = newPosY - that.absStartY;
				if (m.abs(distX) < that.options.snapThreshold && m.abs(distY) < that.options.snapThreshold) { that.scrollTo(that.absStartX, that.absStartY, 200); }
				else {
					snap = that._snap(newPosX, newPosY);
					newPosX = snap.x;
					newPosY = snap.y;
					newDuration = m.max(snap.time, newDuration);
				}
			}

			that.scrollTo(m.round(newPosX), m.round(newPosY), newDuration);

			if (that.options.onTouchEnd) that.options.onTouchEnd.call(that, e);
			return;
		}

		// Do we need to snap?
		if (that.options.snap) {
			distX = newPosX - that.absStartX;
			distY = newPosY - that.absStartY;
			if (m.abs(distX) < that.options.snapThreshold && m.abs(distY) < that.options.snapThreshold) that.scrollTo(that.absStartX, that.absStartY, 200);
			else {
				snap = that._snap(that.x, that.y);
				if (snap.x != that.x || snap.y != that.y) that.scrollTo(snap.x, snap.y, snap.time);
			}

			if (that.options.onTouchEnd) that.options.onTouchEnd.call(that, e);
			return;
		}

		that._resetPos(200);
		if (that.options.onTouchEnd) that.options.onTouchEnd.call(that, e);
	},
	
	_resetPos: function (time) {
		var that = this,
			resetX = that.x >= 0 ? 0 : that.x < that.maxScrollX ? that.maxScrollX : that.x,
			resetY = that.y >= that.minScrollY || that.maxScrollY > 0 ? that.minScrollY : that.y < that.maxScrollY ? that.maxScrollY : that.y;

		if (resetX == that.x && resetY == that.y) {
			if (that.moved) {
				that.moved = false;
				if (that.options.onScrollEnd) that.options.onScrollEnd.call(that);		// Execute custom code on scroll end
			}

			if (that.hScrollbar && that.options.hideScrollbar) {
				if (vendor == 'webkit') that.hScrollbarWrapper.style[transitionDelay] = '300ms';
				that.hScrollbarWrapper.style.opacity = '0';
			}
			if (that.vScrollbar && that.options.hideScrollbar) {
				if (vendor == 'webkit') that.vScrollbarWrapper.style[transitionDelay] = '300ms';
				that.vScrollbarWrapper.style.opacity = '0';
			}

			return;
		}

		that.scrollTo(resetX, resetY, time || 0);
	},

	_wheel: function (e) {
		var that = this,
			wheelDeltaX, wheelDeltaY,
			deltaX, deltaY,
			deltaScale;

		if ('wheelDeltaX' in e) {
			wheelDeltaX = e.wheelDeltaX / 12;
			wheelDeltaY = e.wheelDeltaY / 12;
		} else if('wheelDelta' in e) {
			wheelDeltaX = wheelDeltaY = e.wheelDelta / 12;
		} else if ('detail' in e) {
			wheelDeltaX = wheelDeltaY = -e.detail * 3;
		} else {
			return;
		}
		
		if (that.options.wheelAction == 'zoom') {
			deltaScale = that.scale * Math.pow(2, 1/3 * (wheelDeltaY ? wheelDeltaY / Math.abs(wheelDeltaY) : 0));
			if (deltaScale < that.options.zoomMin) deltaScale = that.options.zoomMin;
			if (deltaScale > that.options.zoomMax) deltaScale = that.options.zoomMax;
			
			if (deltaScale != that.scale) {
				if (!that.wheelZoomCount && that.options.onZoomStart) that.options.onZoomStart.call(that, e);
				that.wheelZoomCount++;
				
				that.zoom(e.pageX, e.pageY, deltaScale, 400);
				
				setTimeout(function() {
					that.wheelZoomCount--;
					if (!that.wheelZoomCount && that.options.onZoomEnd) that.options.onZoomEnd.call(that, e);
				}, 400);
			}
			
			return;
		}
		
		deltaX = that.x + wheelDeltaX;
		deltaY = that.y + wheelDeltaY;

		if (deltaX > 0) deltaX = 0;
		else if (deltaX < that.maxScrollX) deltaX = that.maxScrollX;

		if (deltaY > that.minScrollY) deltaY = that.minScrollY;
		else if (deltaY < that.maxScrollY) deltaY = that.maxScrollY;
    
		if (that.maxScrollY < 0) {
			that.scrollTo(deltaX, deltaY, 0);
		}
	},
	
	_transitionEnd: function (e) {
		var that = this;

		if (e.target != that.scroller) return;

		that._unbind(TRNEND_EV);
		
		that._startAni();
	},


	/**
	*
	* Utilities
	*
	*/
	_startAni: function () {
		var that = this,
			startX = that.x, startY = that.y,
			startTime = Date.now(),
			step, easeOut,
			animate;

		if (that.animating) return;
		
		if (!that.steps.length) {
			that._resetPos(400);
			return;
		}
		
		step = that.steps.shift();
		
		if (step.x == startX && step.y == startY) step.time = 0;

		that.animating = true;
		that.moved = true;
		
		if (that.options.useTransition) {
			that._transitionTime(step.time);
			that._pos(step.x, step.y);
			that.animating = false;
			if (step.time) that._bind(TRNEND_EV);
			else that._resetPos(0);
			return;
		}

		animate = function () {
			var now = Date.now(),
				newX, newY;

			if (now >= startTime + step.time) {
				that._pos(step.x, step.y);
				that.animating = false;
				if (that.options.onAnimationEnd) that.options.onAnimationEnd.call(that);			// Execute custom code on animation end
				that._startAni();
				return;
			}

			now = (now - startTime) / step.time - 1;
			easeOut = m.sqrt(1 - now * now);
			newX = (step.x - startX) * easeOut + startX;
			newY = (step.y - startY) * easeOut + startY;
			that._pos(newX, newY);
			if (that.animating) that.aniTime = nextFrame(animate);
		};

		animate();
	},

	_transitionTime: function (time) {
		time += 'ms';
		this.scroller.style[transitionDuration] = time;
		if (this.hScrollbar) this.hScrollbarIndicator.style[transitionDuration] = time;
		if (this.vScrollbar) this.vScrollbarIndicator.style[transitionDuration] = time;
	},

	_momentum: function (dist, time, maxDistUpper, maxDistLower, size) {
		var deceleration = 0.0006,
			speed = m.abs(dist) / time,
			newDist = (speed * speed) / (2 * deceleration),
			newTime = 0, outsideDist = 0;

		// Proportinally reduce speed if we are outside of the boundaries
		if (dist > 0 && newDist > maxDistUpper) {
			outsideDist = size / (6 / (newDist / speed * deceleration));
			maxDistUpper = maxDistUpper + outsideDist;
			speed = speed * maxDistUpper / newDist;
			newDist = maxDistUpper;
		} else if (dist < 0 && newDist > maxDistLower) {
			outsideDist = size / (6 / (newDist / speed * deceleration));
			maxDistLower = maxDistLower + outsideDist;
			speed = speed * maxDistLower / newDist;
			newDist = maxDistLower;
		}

		newDist = newDist * (dist < 0 ? -1 : 1);
		newTime = speed / deceleration;

		return { dist: newDist, time: m.round(newTime) };
	},

	_offset: function (el) {
		var left = -el.offsetLeft,
			top = -el.offsetTop;
			
		while (el = el.offsetParent) {
			left -= el.offsetLeft;
			top -= el.offsetTop;
		}
		
		if (el != this.wrapper) {
			left *= this.scale;
			top *= this.scale;
		}

		return { left: left, top: top };
	},

	_snap: function (x, y) {
		var that = this,
			i, l,
			page, time,
			sizeX, sizeY;

		// Check page X
		page = that.pagesX.length - 1;
		for (i=0, l=that.pagesX.length; i<l; i++) {
			if (x >= that.pagesX[i]) {
				page = i;
				break;
			}
		}
		if (page == that.currPageX && page > 0 && that.dirX < 0) page--;
		x = that.pagesX[page];
		sizeX = m.abs(x - that.pagesX[that.currPageX]);
		sizeX = sizeX ? m.abs(that.x - x) / sizeX * 500 : 0;
		that.currPageX = page;

		// Check page Y
		page = that.pagesY.length-1;
		for (i=0; i<page; i++) {
			if (y >= that.pagesY[i]) {
				page = i;
				break;
			}
		}
		if (page == that.currPageY && page > 0 && that.dirY < 0) page--;
		y = that.pagesY[page];
		sizeY = m.abs(y - that.pagesY[that.currPageY]);
		sizeY = sizeY ? m.abs(that.y - y) / sizeY * 500 : 0;
		that.currPageY = page;

		// Snap with constant speed (proportional duration)
		time = m.round(m.max(sizeX, sizeY)) || 200;

		return { x: x, y: y, time: time };
	},

	_bind: function (type, el, bubble) {
		(el || this.scroller).addEventListener(type, this, !!bubble);
	},

	_unbind: function (type, el, bubble) {
		(el || this.scroller).removeEventListener(type, this, !!bubble);
	},


	/**
	*
	* Public methods
	*
	*/
	destroy: function () {
		var that = this;

		that.scroller.style[transform] = '';

		// Remove the scrollbars
		that.hScrollbar = false;
		that.vScrollbar = false;
		that._scrollbar('h');
		that._scrollbar('v');

		// Remove the event listeners
		that._unbind(RESIZE_EV, window);
		that._unbind(START_EV);
		that._unbind(MOVE_EV, window);
		that._unbind(END_EV, window);
		that._unbind(CANCEL_EV, window);
		
		if (!that.options.hasTouch) {
			that._unbind('DOMMouseScroll');
			that._unbind('mousewheel');
		}
		
		if (that.options.useTransition) that._unbind(TRNEND_EV);
		
		if (that.options.checkDOMChanges) clearInterval(that.checkDOMTime);
		
		if (that.options.onDestroy) that.options.onDestroy.call(that);
	},

	refresh: function () {
		var that = this,
			offset,
			i, l,
			els,
			pos = 0,
			page = 0;
 
		if (that.scale < that.options.zoomMin) that.scale = that.options.zoomMin;
		that.wrapperW = that.wrapper.clientWidth || 1;
		that.wrapperH = that.wrapper.clientHeight || 1;

		that.minScrollY = -that.options.topOffset || 0;
		that.scrollerW = m.round(that.scroller.offsetWidth * that.scale);
		that.scrollerH = m.round((that.scroller.offsetHeight + that.minScrollY) * that.scale);
		that.maxScrollX = that.wrapperW - that.scrollerW;
		that.maxScrollY = that.wrapperH - that.scrollerH + that.minScrollY;
		that.dirX = 0;
		that.dirY = 0;

		if (that.options.onRefresh) that.options.onRefresh.call(that);

		that.hScroll = that.options.hScroll && that.maxScrollX < 0;
		that.vScroll = that.options.vScroll && (!that.options.bounceLock && !that.hScroll || that.scrollerH > that.wrapperH);

		that.hScrollbar = that.hScroll && that.options.hScrollbar;
		that.vScrollbar = that.vScroll && that.options.vScrollbar && that.scrollerH > that.wrapperH;

		offset = that._offset(that.wrapper);
		that.wrapperOffsetLeft = -offset.left;
		that.wrapperOffsetTop = -offset.top;

		// Prepare snap
		if (typeof that.options.snap == 'string') {
			that.pagesX = [];
			that.pagesY = [];
			els = that.scroller.querySelectorAll(that.options.snap);
			for (i=0, l=els.length; i<l; i++) {
				pos = that._offset(els[i]);
				pos.left += that.wrapperOffsetLeft;
				pos.top += that.wrapperOffsetTop;
				that.pagesX[i] = pos.left < that.maxScrollX ? that.maxScrollX : pos.left * that.scale;
				that.pagesY[i] = pos.top < that.maxScrollY ? that.maxScrollY : pos.top * that.scale;
			}
		} else if (that.options.snap) {
			that.pagesX = [];
			while (pos >= that.maxScrollX) {
				that.pagesX[page] = pos;
				pos = pos - that.wrapperW;
				page++;
			}
			if (that.maxScrollX%that.wrapperW) that.pagesX[that.pagesX.length] = that.maxScrollX - that.pagesX[that.pagesX.length-1] + that.pagesX[that.pagesX.length-1];

			pos = 0;
			page = 0;
			that.pagesY = [];
			while (pos >= that.maxScrollY) {
				that.pagesY[page] = pos;
				pos = pos - that.wrapperH;
				page++;
			}
			if (that.maxScrollY%that.wrapperH) that.pagesY[that.pagesY.length] = that.maxScrollY - that.pagesY[that.pagesY.length-1] + that.pagesY[that.pagesY.length-1];
		}

		// Prepare the scrollbars
		that._scrollbar('h');
		that._scrollbar('v');

		if (!that.zoomed) {
			that.scroller.style[transitionDuration] = '0';
			that._resetPos(400);
		}
	},

	scrollTo: function (x, y, time, relative) {
		var that = this,
			step = x,
			i, l;

		that.stop();

		if (!step.length) step = [{ x: x, y: y, time: time, relative: relative }];
		
		for (i=0, l=step.length; i<l; i++) {
			if (step[i].relative) { step[i].x = that.x - step[i].x; step[i].y = that.y - step[i].y; }
			that.steps.push({ x: step[i].x, y: step[i].y, time: step[i].time || 0 });
		}

		that._startAni();
	},

	scrollToElement: function (el, time) {
		var that = this, pos;
		el = el.nodeType ? el : that.scroller.querySelector(el);
		if (!el) return;

		pos = that._offset(el);
		pos.left += that.wrapperOffsetLeft;
		pos.top += that.wrapperOffsetTop;

		pos.left = pos.left > 0 ? 0 : pos.left < that.maxScrollX ? that.maxScrollX : pos.left;
		pos.top = pos.top > that.minScrollY ? that.minScrollY : pos.top < that.maxScrollY ? that.maxScrollY : pos.top;
		time = time === undefined ? m.max(m.abs(pos.left)*2, m.abs(pos.top)*2) : time;

		that.scrollTo(pos.left, pos.top, time);
	},

	scrollToPage: function (pageX, pageY, time) {
		var that = this, x, y;
		
		time = time === undefined ? 400 : time;

		if (that.options.onScrollStart) that.options.onScrollStart.call(that);

		if (that.options.snap) {
			pageX = pageX == 'next' ? that.currPageX+1 : pageX == 'prev' ? that.currPageX-1 : pageX;
			pageY = pageY == 'next' ? that.currPageY+1 : pageY == 'prev' ? that.currPageY-1 : pageY;

			pageX = pageX < 0 ? 0 : pageX > that.pagesX.length-1 ? that.pagesX.length-1 : pageX;
			pageY = pageY < 0 ? 0 : pageY > that.pagesY.length-1 ? that.pagesY.length-1 : pageY;

			that.currPageX = pageX;
			that.currPageY = pageY;
			x = that.pagesX[pageX];
			y = that.pagesY[pageY];
		} else {
			x = -that.wrapperW * pageX;
			y = -that.wrapperH * pageY;
			if (x < that.maxScrollX) x = that.maxScrollX;
			if (y < that.maxScrollY) y = that.maxScrollY;
		}

		that.scrollTo(x, y, time);
	},

	disable: function () {
		this.stop();
		this._resetPos(0);
		this.enabled = false;

		// If disabled after touchstart we make sure that there are no left over events
		this._unbind(MOVE_EV, window);
		this._unbind(END_EV, window);
		this._unbind(CANCEL_EV, window);
	},
	
	enable: function () {
		this.enabled = true;
	},
	
	stop: function () {
		if (this.options.useTransition) this._unbind(TRNEND_EV);
		else cancelFrame(this.aniTime);
		this.steps = [];
		this.moved = false;
		this.animating = false;
	},
	
	zoom: function (x, y, scale, time) {
		var that = this,
			relScale = scale / that.scale;

		if (!that.options.useTransform) return;

		that.zoomed = true;
		time = time === undefined ? 200 : time;
		x = x - that.wrapperOffsetLeft - that.x;
		y = y - that.wrapperOffsetTop - that.y;
		that.x = x - x * relScale + that.x;
		that.y = y - y * relScale + that.y;

		that.scale = scale;
		that.refresh();

		that.x = that.x > 0 ? 0 : that.x < that.maxScrollX ? that.maxScrollX : that.x;
		that.y = that.y > that.minScrollY ? that.minScrollY : that.y < that.maxScrollY ? that.maxScrollY : that.y;

		that.scroller.style[transitionDuration] = time + 'ms';
		that.scroller.style[transform] = 'translate(' + that.x + 'px,' + that.y + 'px) scale(' + scale + ')' + translateZ;
		that.zoomed = false;
	},
	
	isReady: function () {
		return !this.moved && !this.zoomed && !this.animating;
	}
};

function prefixStyle (style) {
	if ( vendor === '' ) return style;

	style = style.charAt(0).toUpperCase() + style.substr(1);
	return vendor + style;
}

dummyStyle = null;	// for the sake of it

if (typeof exports !== 'undefined') exports.iScroll = iScroll;
else window.iScroll = iScroll;

})(window, document);



lolQuest:
=========


/*
 * lolQuest.js v1.2
 *
 * by WEB.RND@LOL
 *
 */

window.lolQuest = function(appID,container, prevBtn, nextBtn, questions, timerDiv, displayQNo, thumbnailSlider, thumbHolder, bookmarkBtn, fullThumbnailUnit, coverPageDiv, homeBtn, tocBtn, submitBtn) {
	if (!container || !prevBtn || !nextBtn) return null;
	proQ = this;
	//Object Declartion
	proQ.container = container;
	proQ.holder = document.getElementById(container).children[0].id;
	proQ.prevBtn = prevBtn;
	proQ.nextBtn = nextBtn;
	proQ.homeBtn = document.getElementById(homeBtn);
	proQ.tocBtn = document.getElementById(tocBtn);
	proQ.submitBtn = document.getElementById(submitBtn);
	proQ.timerDiv = timerDiv;
	proQ.validateBtn = "";
	proQ.displayQNo = displayQNo;
	proQ.thumbnailSlider = thumbnailSlider;
	proQ.thumbHolder = thumbHolder;
	proQ.bmBtn = bookmarkBtn;
	proQ.fullThumbnailUnit = fullThumbnailUnit;
	
	//Global vars *
	proQ.isReviewable = false;
	proQ.holderTemplate = "";
	proQ.validateOnSelect = true;
	proQ.currQuestion = 0;
	proQ.questions = questions;
	proQ.totalQuestions = questions.questionList.question.length;
	proQ.selectedOption = 0;
	proQ.score = new Array();
	proQ.selectedAnswer = new Array();
	proQ.bmState = new Array();
	proQ.currentPage = "coverPage";
	proQ.correctString = "Correct";
	proQ.wrongString = "Wrong";
	proQ.timeToSwipe = 250;
	proQ.optListType = "a";
	proQ.optAltratePageChange = false;
	proQ.autoNumberQuestions = false;
	proQ.swipeSensitivityX = 30;
	proQ.swipeSensitivityY = 60;
	proQ.appID = appID;
	proQ.isThumbVisible = false;
	proQ.currentQuizMode;
	proQ.subNavBtnClass = "subNavBtn";
	proQ.isOptionsImage;
	proQ.coverPageDiv = coverPageDiv;
	proQ.verticalDivCls = "verticalDiv";
	
	proQ.aniCurrentTime = 0;
	proQ.imageAniTime = 4000;
	proQ.coverAni;
	proQ.isCoverImage = true;
	proQ.isLoaded = false;
	proQ.useNavParent = false;
	proQ.loadCoverInit = false;
	proQ.TocContent = null;
	
	//Global vars
	proQ.downCoords = {};
	proQ.isMouseDown = false;
	proQ.isYNotMoved = true;
	proQ.downX = 0;
	proQ.downY = 0;
	proQ.scoreBtnText = "";
	proQ.prevBtnText = "";
	proQ.nextBtnText = "";
	proQ.replayBtnText = "";
	proQ.alphaSet = ['A','B','C','D','E','F','G','H','I','J'];
	proQ.questTimerState = "new";
	proQ.questTimerTime = 0;
	proQ.questSubTimerTime = new Array();
	proQ.timer;
	proQ.reviewTime = "---";
	proQ.flaggedCol = "#EC7F14";
	proQ.dimColor = "#D3D3D3";
	proQ.currentThumbView = 0;
	
	proQ.isTouchDevice = 'ontouchstart' in document.documentElement;
	window.addEventListener('resize', this, false);
	proQ.setup();
};

lolQuest.prototype = {
	setup: function(){
		try//tryHere*/
		{
			proQ.holderTemplate = document.getElementById(proQ.holder).outerHTML;
			proQ.bindTouchEvents();
			
			proQ.initQuest = parseInt(proQ.getLocStrg("_CurrentQuestion",0));
			proQ.currentQuizMode = proQ.getLocStrg("_QuizMode","live");
			proQ.questTimerTime = proQ.getLocStrg("_LastTime",0);
			proQ.currentPage = proQ.getLocStrg("_LastPage","coverPage");
			
			if(proQ.currentPage == "myReviewPage" || (proQ.currentPage == "quiz" && proQ.currentQuizMode == "review"))
				proQ.currentPage = "coverPage";
			proQ.score = proQ.getLocStrgArr("_Score",null);
			proQ.selectedAnswer = proQ.getLocStrgArr("_SelectedAnswer",null);
			proQ.bmState = proQ.getLocStrgArr("_BookmarkState",null);
			proQ.questSubTimerTime = proQ.getLocStrgArr("_SubTimerTime",null);
			
			if(proQ.score == null || proQ.score == "null"){proQ.score = new Array();}
			if(proQ.selectedAnswer == null || proQ.selectedAnswer == "null"){proQ.selectedAnswer = new Array();}
			if(proQ.bmState == null || proQ.bmState == "null"){proQ.bmState = new Array();}
			if(proQ.questSubTimerTime == null || proQ.questSubTimerTime == "null"){proQ.questSubTimerTime = new Array();}
			proQ.currQuestion = proQ.initQuest;
			$("."+$("#"+proQ.holder).attr('class')).css({'width':$(window).width()+'px'});
			if($(window).width() > 500 && $(window).height() > 500){proQ.timeToSwipe = 250; }else{proQ.timeToSwipe = 350;}
			clickAudio.load();
			clickAudio.play();
			proQ.loadPage();
			proQ.informMe('Prototype > Initalized');
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << setup", e);}//catchHere*/
	},
	byLoadPage: function(page){
		if(page && ((page != "myReviewPage" && proQ.currentQuizMode == "live") || proQ.currentQuizMode != "live")){
			if(page == "quiz" || page == "instructionPage" || page == "myReviewPage" || page == "tocPage" || (proQ.currentPage == "homePage" && page == "settingsPage") || page == "homePage"){
				if(proQ.currentPage == "coverPage" && page == "homePage") proQ.nextQuestion(page);
				else if(proQ.currentPage == "homePage" && page == "tocPage") proQ.nextQuestion(page);
				else if(proQ.currentPage == "quiz" && page == "tocPage") proQ.prevQuestion(page);
				else if(proQ.currentPage == "homePage" && page=="quiz") proQ.nextQuestion(0);
				else if((proQ.currentPage == "myReviewPage" && page=="coverPage") || (proQ.currentPage != "coverPage" && page == "homePage")) proQ.prevQuestion(page);
				else proQ.nextQuestion(page);
			}
			else proQ.prevQuestion(page);
		}
	},
	loadPage: function(funct){
		try//tryHere*/
		{
			var questHolder = document.getElementById(proQ.holder).children[0].children[0].children[0];
			var optionsHolder = document.getElementById(proQ.holder).children[0].children[1].children[0];
			var questionDisp = null;
			var responseHolder = null;
			var thumbHolder = null;
			var flag = null;
			var timerDisp = null;
			if(proQ.fullThumbnailUnit) thumbHolder = document.getElementById(proQ.fullThumbnailUnit);
			if(document.getElementById(proQ.holder).children[0].children.length > 2) responseHolder = document.getElementById(proQ.holder).children[0].children[2];
			if(proQ.bmBtn) flag = document.getElementById(proQ.bmBtn);
			if(proQ.timerDiv) timerDisp = document.getElementById(proQ.timerDiv).parentNode;
			if(proQ.displayQNo) questionDisp = document.getElementById(proQ.displayQNo);
			if(funct){
				if(funct == "next"){
					if(proQ.currentPage == "coverPage") proQ.currentPage = "homePage";
					else if(proQ.currentPage == "settingsPage") proQ.currentPage = "instructionPage";
					else if(proQ.currentPage == "myReviewPage"){
						proQ.currentPage = "quiz";
						proQ.loadQuestion(proQ.currQuestion);
					}
					else if(proQ.currentPage == "homePage") proQ.currentPage = "quiz";
				}
				else if(funct == "prev"){
					if(proQ.currentPage == "homePage") proQ.currentPage = "coverPage";
					else if(proQ.currentPage == "settingsPage") proQ.currentPage = "homePage";
					else if(proQ.currentPage == "instructionPage") proQ.currentPage = "homePage";
				}
				else if(proQ.isOneOfThePages(funct)) proQ.currentPage = funct;
			}
			if (typeof funct == "number") {
				proQ.loadQuestion(funct);
				proQ.currentPage = "quiz";
			}
			var nxt;
			var prv;
			if(proQ.useNavParent){
				nxt = document.getElementById(proQ.nextBtn).parentNode;
				prv = document.getElementById(proQ.prevBtn).parentNode;
			}
			else{
				nxt = document.getElementById(proQ.nextBtn);
				prv = document.getElementById(proQ.prevBtn);
			}
			if(proQ.currentPage != "quiz"){
				$(questHolder).show();
				$(optionsHolder).hide();
				if(responseHolder){$(responseHolder).hide();}
				if(thumbHolder){$(thumbHolder).hide();}
				if(timerDisp){$(timerDisp).hide();}
				if(flag){$(flag).hide();}
				if(questionDisp){$(questionDisp).hide();}
				document.getElementById("endSpace").style.display = "none";
			}
			else{
				$(questHolder).show();
				$(optionsHolder).show();
				nxt.style.display = "block";
				prv.style.display = "block";
				if(responseHolder){responseHolder.style.display = "none";}
				if(thumbHolder){thumbHolder.style.display = "block";}
				if(timerDisp){timerDisp.style.display = "block";}
				if(questionDisp){questionDisp.style.display = "inline-block";}
				if(flag){
					if(proQ.currentQuizMode == "live"){flag.style.display = "inline-block";}
					else{flag.style.display = "none";}
				}
				proQ.prepareQuestionare();
				document.getElementById("endSpace").style.display = "block";
			}
			if(proQ.currentPage == "coverPage") proQ.loadCoverAni();
			else $("#"+proQ.coverPageDiv).hide();
			if(proQ.currentPage == "homePage" || proQ.currentPage == "coverPage" || proQ.currentPage == "settingsPage" || proQ.currentPage == "tocPage" || proQ.currentPage == "myReviewPage") $(questHolder).removeClass("whiteBg");
			else $(questHolder).addClass("whiteBg");
			$(proQ.homeBtn).show();
			$(proQ.tocBtn).hide();
			$(proQ.submitBtn).hide();
			$("."+proQ.verticalDivCls).show();
			if(proQ.currentPage == "homePage") {
				questHolder.innerHTML = pages.pageList.homePage;
				proQ.onContentLoaded();
				$(nxt).hide();
				$(prv).hide();
				$(proQ.homeBtn).hide();
				$("."+proQ.verticalDivCls).hide();
			}
			else if(proQ.currentPage == "settingsPage") {
				questHolder.innerHTML = pages.pageList.settingsPage;
				proQ.onContentLoaded();
				$(nxt).hide();
				$(prv).show();
				$(proQ.tocBtn).show();
				$("."+proQ.verticalDivCls).eq(1).hide();
			}
			else if(proQ.currentPage == "instructionPage"){
				questHolder.innerHTML = pages.pageList.instructionPage;
				proQ.onContentLoaded();
				$(nxt).hide();
				$(prv).show();
				$(proQ.tocBtn).show();
				$("."+proQ.verticalDivCls).eq(1).hide();
			}
			else if(proQ.currentPage == "myReviewPage"){
				questHolder.innerHTML = pages.pageList.myReviewPage;
				proQ.onContentLoaded();
				$(nxt).hide();
				$(prv).hide();
				$(proQ.tocBtn).show();
				$("."+proQ.verticalDivCls).eq(1).hide();
			}
			else if (proQ.currentPage == "tocPage") {
				questHolder.innerHTML = pages.pageList.tocPage;
				proQ.loadTOC();
				proQ.onContentLoaded();
				$(nxt).hide();
				$(prv).show();
				$("."+proQ.verticalDivCls).hide();
			}
			else {
				$(proQ.tocBtn).show();
				if (proQ.currentQuizMode == "review" || !proQ.isReviewable) $("."+proQ.verticalDivCls).eq(1).hide();
				else $(proQ.submitBtn).show();
			}
			if(proQ.currentQuizMode == "review") $("#startBtn").text("Review Answers");
			else $("#myReviewBtn").css({"color":"#666"});
			if (!proQ.isReviewable) $("#myReviewBtn").hide();
			else $("#myReviewBtn").show();
			if(proQ.currentPage == "coverPage" || proQ.currentPage == "homePage"){
				$("#quitBtn").hide();
				$("#footer").hide();
			}
			else{
				$("#quitBtn").show();
				$("#footer").show();
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << loadPage", e);}//catchHere*/
	},
	loadTOC:function(){
		var eventHandlr = "";
		if(proQ.isTouchDevice) eventHandlr = "touchend";
		else eventHandlr = "mouseup";
		if (!proQ.TocContent) {
			proQ.TocContent = "";
			for(var i=0; i<proQ.totalQuestions; i++){
				var question = proQ.getQuestion(i);
				var prefix = proQ.questionTypePrefix(question);
				proQ.TocContent += "<div class=\"tocItem\""+eventHandlr+" value=\""+i+"\"><span class=\"tocIndex\">"+(i+1)+"</span>"+prefix+question.questionNo+"</div>";
			}
		}
		$("#tocContentHolder").html(proQ.TocContent);
		$(".tocItem").on(eventHandlr, proQ.tocClick)
	},
	questionTypePrefix:function(question){
		var prefix = "";
		if(question.questionType == "example") prefix = "Example ";
		else if(question.questionType == "choice") prefix = "Question with choice ";
		else if(question.questionType == "fillIn") prefix = "Fill-in one or two words ";
		else if(question.questionType == "shortFill") prefix = "Fill-in briefly ";
		else if(question.questionType == "longFill") prefix = "Explain about.. ";
		else if(question.questionType == "match") prefix = "Match column B with A ";
		else if(question.questionType == "trueOrFalse") prefix = "State True or False ";
		return prefix;
	},
	tocClick:function(event){
		var value = -1;
		var elem = $(event.target);
		if(elem.hasClass("tocItem")) value = elem.attr("value");
		else if(elem.parents(".tocItem").length > 0) value = elem.parent(".tocItem").attr("value");
		if (value) value = parseInt(value);
		if (value >= 0){
			if (proQ.downCoords.x) {
				var swipeData = proQ.swipeDirection(proQ.downCoords, event);
				if (swipeData.isYNotMoved) proQ.nextQuestion(value);
			}
		}
		proQ.isMouseDown = false;
	},
	getQuestion:function(index){
		return proQ.questions.questionList.question[index];
	},
	onResetClick:function(){
		proQ.resetAll();
		proQ.currentPage = "settingsPage";
		proQ.byLoadPage("homePage");
	},
	onContentLoaded:function(){},
	prepareQuestionare:function(){
		try//tryHere*/
		{
			proQ.questTimer("new");
			proQ.loadThumbView("setup");
			proQ.loadQuestion(proQ.currQuestion);
			var swipeThumbVal = -parseInt(proQ.initQuest/5);
			if(swipeThumbVal > 0){swipeThumbVal = 0;}
			setTimeout(function(){proQ.swipeThumb(swipeThumbVal);},200);
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << prepareQuestionare", e);}//catchHere*/
	},
	loadCoverAni: function(){
		try
		{
            proQ.isLoaded = false;
            $("#"+proQ.coverPageDiv).show();
            $("#"+proQ.coverPageDiv).html(pages.pageList.coverPage);
            proQ.coverAni = null;
            if(!proQ.isCoverImage){
                proQ.coverAni = document.createElement('video');
                proQ.coverAni.hide();
                $(proQ.coverAni).attr('id', 'coverAnimation');
                $(proQ.coverAni).attr('poster', './video/poster.png');
                $(proQ.coverAni).attr('webkit-playsinline','true');
                if($(window).width() > 640){
                    $(proQ.coverAni).attr('src', './video/iPad.mp4');
                    if($(window).width() > $(window).height()){
                        $(proQ.coverAni).attr('width', '1024px');
                        $(proQ.coverAni).attr('height', '768px');
                    }
                    else{
                        $(proQ.coverAni).attr('width', '768px');
                        $(proQ.coverAni).attr('height', '576px');
                    }
                }else{
                    if($(window).width() > $(window).height()){
                        $(proQ.coverAni).attr('src', './video/iPhoneLandscape.mp4');
                        $(proQ.coverAni).attr('width', '480px');
                        $(proQ.coverAni).attr('height', '320px');
                    }
                    else{
                        $(proQ.coverAni).attr('src', './video/iPhonePortrait.mp4');
                        $(proQ.coverAni).attr('width', '320px');
                        $(proQ.coverAni).attr('height', '480px');
                    }
                }
                $(proQ.coverAni).attr('control', 'false');
                $(proQ.coverAni).attr('preload', 'true');
                proQ.coverAni.load();
		try{proQ.playCoverAni();}catch(e){}
		$("#"+proQ.coverPageDiv).html(proQ.coverAni);
		proQ.coverAni.addEventListener("loadedmetadata", function(){
					       proQ.pushToPlay();
					});
		proQ.coverAni.addEventListener("ended", function(){
					       proQ.animationEnded();
					});
		proQ.coverAni.addEventListener("timeupdate", function(){
					       if(proQ.coverAni.currentTime > 0){
					       proQ.aniCurrentTime = proQ.coverAni.currentTime;}
					});
            }
	    else{
		$(proQ.coverAni).show();
		setTimeout(function(){
			//proQ.animationEnded();
		}, proQ.imageAniTime)
	    }
	    proQ.loadCoverInit = true;
	}
		catch(e){proQ.informMe("EXCEPTION THROWN in << loadCoverAni", e);}//catchHere*/
	},
pushToPlay: function(){
    proQ.isLoaded = true;
    proQ.playCoverAni();
},
playCoverAni: function(){
    if(proQ.isLoaded){
        proQ.coverAni.currentTime = proQ.aniCurrentTime;
        $(proQ.coverAni).show();
        proQ.coverAni.play();
        proQ.coverAni.currentTime = proQ.aniCurrentTime;
    }
},
animationEnded:function(){
    $("#"+proQ.coverPageDiv).hide();
    proQ.aniCurrentTime = 0;
    try{
	proQ.coverAni.currentTime = 0;
    }
    catch(e){}
    proQ.byLoadPage("homePage");
},
	resetAll: function(){
		try//tryHere*/
		{
		proQ.informMe("ResetAll()");
		var responseHolder;
		if(document.getElementById(proQ.holder).children[0].children.length > 2){responseHolder = document.getElementById(proQ.holder).children[0].children[2];}
		if(responseHolder){
			responseHolder.style.display = "none";
			responseHolder.innerHTML = "";
		}
		if(proQ.flagQ) $("#"+proQ.bmBtn).css("display","inline-block");
		
		proQ.setLocStrg("_CurrentQuestion",0);
		proQ.setLocStrg("_QuizMode","live");
		proQ.setLocStrg("_LastTime",0);
		
		proQ.setLocStrg("_Score",null);
		proQ.setLocStrg("_SelectedAnswer",null);
		proQ.setLocStrg("_BookmarkState",null);
		proQ.setLocStrg("_SubTimerTime",null);
		
		proQ.score = new Array();
		proQ.selectedAnswer = new Array();
		proQ.bmState = new Array();
		proQ.questSubTimerTime = new Array();
		proQ.questTimerTime = 0;
		
		proQ.currentQuizMode = "live";
		proQ.initQuest = 0;
		proQ.currQuestion = 0;
		proQ.selectedOption = 0;
		//proQ.loadQuestion(proQ.currQuestion);
		proQ.loadThumbView();}
		catch(e){proQ.informMe("EXCEPTION THROWN in << resetAll", e);}//catchHere*/
	},
	getLocStrg: function(varId,defaultVal){
		try//tryHere*/
		{
			proQ.informMe("getLocStrg");
			var localStrgVar;
			try{localStrgVar = localStorage.getItem(proQ.appID+varId);}
			catch(e){localStrgVar = defaultVal;}
			if(localStrgVar == "null"){localStrgVar = defaultVal;}
			var backUp = localStrgVar;
			if(!isNaN(defaultVal)){
				try{localStrgVar = parseInt(localStrgVar);}catch(e){localStrgVar = backUp;}
			}
			if(!localStrgVar) localStrgVar = defaultVal;
			return localStrgVar;
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << getLocStrg", e); return defaultVal;}//catchHere*/
	},
	getLocStrgArr: function(varId,defaultVal){
		try//tryHere*/
		{
			proQ.informMe("getLocStrgArr");
			var localStrgVar = new Array;
			try{localStrgVar = localStorage.getItem(proQ.appID+varId).split(",");}
			catch(e){localStrgVar = defaultVal;}
			if(!localStrgVar || localStrgVar == "null" || localStrgVar == null || localStrgVar == undefined){localStrgVar = defaultVal;}
			return localStrgVar;
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << getLocStrgArr", e); return defaultVal;}//catchHere*/
	},
	loadThumbView: function(type){
		try//tryHere*/
		{
			proQ.informMe("loadThumbView");
			$("#"+proQ.thumbnailSlider).empty();
			for(var i=0; i<proQ.totalQuestions; i++){
				var thumbTxt = "<div id=\"navBtn_"+(i+1)+"\" class=\""+proQ.subNavBtnClass+"\">"+(i+1)+"</div>";
				$("#"+proQ.thumbnailSlider).append(thumbTxt);
				//if(proQ.currentQuizMode == "review"){
				//	var result = proQ.currResult(i);
				//	if(result == "correct"){
				//		$("#navBtn_"+(i+1)).css({"background-color":"#ff0","border":"6px #ff0 solid"});
				//	}
				//	else{
				//		$("#navBtn_"+(i+1)).css({"background-color":"#f00","border":"6px #f00 solid"});
				//	}
				//}
				//else if(proQ.currentQuizMode == "live"){
				//	var isAnswered;
				//	var isBm;
				//	try{isAnswered = proQ.selectedAnswer[i];}catch(e){}
				//	try{isBm = proQ.bmState[i];}catch(e){}
				//	if(isAnswered){
				//		$("#navBtn_"+(i+1)).css({"background-color":"#3D3D3D","border":"6px #3D3D3D solid","color":"#fff"});
				//	}
				//	else{
				//		$("#navBtn_"+(i+1)).css({"background-color":"#fff","border":"6px #fff solid","color":"#000"});
				//	}
				//	if(isBm){
				//		if(isBm > 0){$("#navBtn_"+(i+1)).css({"border":"6px "+proQ.flaggedCol+" solid"});}
				//	}
				//}
			}
			var marginL = 0;
			var marginL = 0;
			var border = $("."+proQ.subNavBtnClass).css("border").replace("px","");
			if(border){
				try{
					var temp =  parseInt(border.substr(0, border.indexOf(" ")));
					if(temp > 0){
						marginL = marginR = temp;
					}
				}
				catch(e){}
			}
			try{marginL += parseInt($("."+proQ.subNavBtnClass).css("margin-left").replace("px",""));}catch(e){marginL = 0;}
			try{marginR += parseInt($("."+proQ.subNavBtnClass).css("margin-right").replace("px",""));}catch(e){marginR = 0;}
			if(proQ.totalQuestions && proQ.totalQuestions > 0){$("#"+proQ.thumbnailSlider).css({"width":(($("."+proQ.subNavBtnClass).width() + marginL + marginR)*proQ.totalQuestions)*2+"px"});}
			if(type){
				if(type=="setup"){
					try{proQ.unBindThumbEvents();}catch(e){}
					proQ.bindThumbEvents();
				}
			}
			if(proQ.displayQNo){
				if(!proQ.isThumbVisible){$("#"+proQ.thumbHolder).css({"margin-bottom":-($("#"+proQ.thumbHolder).height()+5)+"px"});}
				else{$("#"+proQ.thumbHolder).css({"margin-bottom":0+"px"});}
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << loadThumbView", e);}//catchHere*/
	},
	bindThumbEvents: function(){
		try{proQ.unBindThumbEvents();}catch(e){}
		try//tryHere*/
		{
			proQ.informMe("bindThumbEvents");
			if(proQ.isTouchDevice){
				$("#"+proQ.displayQNo).bind('touchstart',proQ.onDispDown);
				$("#"+proQ.displayQNo).bind('touchend',proQ.showHideThumbs);
				$("#"+proQ.thumbHolder).bind('touchend',proQ.onThumbClick);
			}
			else{
				$("#"+proQ.displayQNo).bind('mousedown',proQ.onDispDown);
				$("#"+proQ.displayQNo).bind('mouseup',proQ.showHideThumbs);
				$("#"+proQ.thumbHolder).bind('mouseup',proQ.onThumbClick);
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << bindThumbEvents", e);}//catchHere*/
	},
	unBindThumbEvents: function(){
		try//tryHere*/
		{
			proQ.informMe("unBindThumbEvents");
			if(proQ.isTouchDevice){
				$("#"+proQ.displayQNo).unbind('touchstart');
				$("#"+proQ.displayQNo).unbind('touchend');
				$("#"+proQ.thumbHolder).unbind('touchend');
			}
			else{
				$("#"+proQ.displayQNo).unbind('mousedown');
				$("#"+proQ.displayQNo).unbind('mouseup');
				$("#"+proQ.thumbHolder).unbind('mouseup');
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << unBindThumbEvents", e);}//catchHere*/
	},
	onAllTouchUp: function(){
		proQ.isMouseDown = false;
		$("#"+proQ.displayQNo).css({"color":"#fff"});
	},
	onThumbClick: function(event){
		try//tryHere*/
		{
			proQ.informMe("onThumbClick");
			if (proQ.downCoords.x) {
				var swipData = proQ.swipeDirection(proQ.downCoords,event);
				if(swipData.isYNotMoved && swipData.isXNotMoved){
					if(event.target.innerHTML.trim() != "" && event.target.innerHTML.length < 4){playClickAudio();}
					try{proQ.gotoQuestion(parseInt(event.target.innerHTML,10));}
					catch(e){}
				}
				else if(swipData.isYNotMoved && !swipData.isXNotMoved) proQ.swipeThumb(proQ.currentThumbView+swipData.direction);
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << onThumbClick", e);}//catchHere*/
	},
	swipeDirection: function(downCoords, upEvent){
		var upX = 0;
		var upY = 0;
		try{upX = upEvent.originalEvent.changedTouches[0].pageX; upY = upEvent.originalEvent.changedTouches[0].pageY;}
		catch(e){upX = event.pageX; upY = event.pageY;}
		var isYNotMoved = (Math.abs(downCoords.y - upY) < proQ.swipeSensitivityY);
		var isXNotMoved = (Math.abs(downCoords.x - upX) < proQ.swipeSensitivityX);
		var direction = ((proQ.downX > upX) > 0) ? -1 : 1;
		var retData = {isYNotMoved:(isYNotMoved && proQ.isYNotMoved), isXNotMoved:isXNotMoved, direction:direction };
		return retData;
	},
	swipeThumb: function(side){
		try//tryHere*/
		{
			if(-parseInt((proQ.totalQuestions-1)/5) <= side){
				proQ.informMe("swipeThumb");
				var addVal = $("#"+proQ.thumbnailSlider).parent().width();
				var currPos = parseInt($("#"+proQ.thumbnailSlider).css('margin-left').replace("px",""));
				var totalAllowed = parseInt($("#"+proQ.thumbnailSlider).css('width').replace("px",""));
				var toMove = addVal*side;
				if(toMove <= -totalAllowed){
					side = side+1;
					toMove = addVal*side;
				}
				else if(toMove >= -totalAllowed && toMove >= 0){
					side = 0;
					toMove = side;
				}
				if(currPos != toMove){
					proQ.unBindThumbEvents();
					proQ.currentThumbView = side;
					$("#"+proQ.thumbnailSlider).animate({"marginLeft":toMove+"px"},{duration: proQ.timeToSwipe, queue: true,
						complete: function() {
							proQ.bindThumbEvents();
						}
					});
				}
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << swipeThumb", e);}//catchHere*/
	},
	onDispDown: function(){
		$("#"+proQ.displayQNo).css({"color":proQ.dimColor});
	},
	showHideThumbs: function(){
		try//tryHere*/
		{
			proQ.informMe("showHideThumbs");
			playClickAudio();
			var showHideTime = 200;
			if(!proQ.isThumbVisible){
				$("#"+proQ.thumbHolder).animate({"marginBottom":-20+"px"},showHideTime);
				proQ.isThumbVisible = true;
			}
			else{
				$("#"+proQ.thumbHolder).animate({"marginBottom":-($("#"+proQ.thumbHolder).height()+5)+"px"},showHideTime);
				proQ.isThumbVisible = false;
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << showHideThumbs", e);}//catchHere*/
	},
	bindTouchEvents: function(){
		try{proQ.unBindTouchEvents();}catch(e){}
		try//tryHere*/
		{
			proQ.informMe("bindTouchEvents");
			if(proQ.isTouchDevice){
				if(proQ.useNavParent){
					$("#"+proQ.prevBtn).parent().bind('touchstart',proQ.prevQuestion);
					$("#"+proQ.nextBtn).parent().bind('touchstart',proQ.nextQuestion);
				}
				else{
					$("#"+proQ.prevBtn).bind('touchstart',proQ.prevQuestion);
					$("#"+proQ.nextBtn).bind('touchstart',proQ.nextQuestion);
				}
				$(window).bind('touchstart',proQ.onTouchDown);
				$(window).bind('touchmove',proQ.onTouchMove);
				$("#"+proQ.container).bind('touchend',proQ.onTouchUp);
				$("#"+proQ.bmBtn).bind('touchend',proQ.flagQ);
				$(window).bind('touchend',proQ.onAllTouchUp);
				$("#"+proQ.container).bind('touchend', proQ.onSwipeUp);
				$(proQ.tocBtn).bind('touchstart', proQ.gotoTOC);
				$(proQ.submitBtn).bind('touchstart', proQ.onSubmitClick);
			}
			else{
				if(proQ.useNavParent){
					$("#"+proQ.prevBtn).parent().bind('mousedown',proQ.prevQuestion);
					$("#"+proQ.nextBtn).parent().bind('mousedown',proQ.nextQuestion);
				}
				else{
					$("#"+proQ.prevBtn).bind('mousedown',proQ.prevQuestion);
					$("#"+proQ.nextBtn).bind('mousedown',proQ.nextQuestion);
				}
				$(window).bind('mousedown', proQ.onTouchDown);
				$(window).bind('mousemove',proQ.onTouchMove);
				$("#"+proQ.container).bind('mouseup', proQ.onTouchUp);
				$("#"+proQ.bmBtn).bind('mouseup',proQ.flagQ);
				$(window).bind('mouseup',proQ.onAllTouchUp);
				$("#"+proQ.container).bind('mouseup', proQ.onSwipeUp);
				$(proQ.tocBtn).bind('mousedown', proQ.gotoTOC);
				$(proQ.submitBtn).bind('mousedown', proQ.onSubmitClick);
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << bindTouchEvents", e);}//catchHere*/
	},
	gotoTOC:function(){
		proQ.byLoadPage("tocPage");
	},
	onSubmitClick:function(){
		if (proQ.currentQuizMode != "review") proQ.promptReviewMode();
	},
	onSwipeUp:function(event){
		if (proQ.downCoords.x) {
			var nxt;
			var prv;
			if(proQ.useNavParent){
				nxt = document.getElementById(proQ.nextBtn).parentNode;
				prv = document.getElementById(proQ.prevBtn).parentNode;
			}
			else{
				nxt = document.getElementById(proQ.nextBtn);
				prv = document.getElementById(proQ.prevBtn);
			}
			var swipeData = proQ.swipeDirection(proQ.downCoords, event);
			if (swipeData.isYNotMoved && !swipeData.isXNotMoved) {
				if (swipeData.direction < 0 && $(nxt).css("display") != "none") proQ.nextQuestion();
				else if (swipeData.direction > 0 && $(prv).css("display") != "none") proQ.prevQuestion();
			}
		}
	},
	unBindTouchEvents: function(){
		try//tryHere*/
		{
			try{$("#lolScrollBarV").css({"display":"none"});}catch(e){}
			try{$("#lolScrollBarH").css({"display":"none"});}catch(e){}
			proQ.informMe("unBindTouchEvents");
			try{
				if(proQ.useNavParent){
					$("#"+proQ.prevBtn).parent().unbind('touchstart');
					$("#"+proQ.nextBtn).parent().unbind('touchstart');
				}
				else{
					$("#"+proQ.prevBtn).unbind('touchstart');
					$("#"+proQ.nextBtn).unbind('touchstart');
				}
				$(window).unbind('touchstart');
				$(window).unbind('touchmove');
				$("#"+proQ.container).bind('touchstart');
				$("#"+proQ.container).unbind('touchend');
				$("#"+proQ.bmBtn).unbind('touchend');
				$(window).unbind('touchend');
				$(proQ.tocBtn).unbind('touchstart');
				$(proQ.submitBtn).unbind('touchstart');
			}catch(e){}
			try{
				if(proQ.useNavParent){
					$("#"+proQ.prevBtn).parent().unbind('mousedown');
					$("#"+proQ.nextBtn).parent().unbind('mousedown');
				}
				else{
					$("#"+proQ.prevBtn).unbind('mousedown');
					$("#"+proQ.nextBtn).unbind('mousedown');
				}
				$(window).unbind('mousedown');
				$(window).bind('mousemove');
				$("#"+proQ.container).bind('mousedown');
				$("#"+proQ.container).unbind('mouseup');
				$("#"+proQ.bmBtn).unbind('mouseup');
				$(window).unbind('mouseup');
				$(proQ.tocBtn).unbind('mousedown');
				$(proQ.submitBtn).unbind('mousedown');
			}catch(e){}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << unBindTouchEvents", e);}//catchHere*/
	},
	onTouchMove:function(event){
		if (proQ.downCoords.x) {
			var swipeData = proQ.swipeDirection(proQ.downCoords, event);
			proQ.isYNotMoved = swipeData.isYNotMoved;
		}
	},
	flagQ: function(){
		try//tryHere*/
		{
			proQ.informMe("flagQ");
			playClickAudio();
			if(proQ.bmState[proQ.currQuestion]){
				if(proQ.bmState[proQ.currQuestion] == 1){proQ.setBm(0);}
				else{proQ.setBm(1);}
			}
			else proQ.setBm(1);
			proQ.setLocStrg("_BookmarkState",proQ.bmState);
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << flagQ", e);}//catchHere*/
	},
	setBm: function(val){
		try//tryHere*/
		{
			proQ.informMe("setBm");
			//if(proQ.currentQuizMode == "live") {
			//	var col = "";
			//	if(val != undefined && val != null){proQ.bmState[proQ.currQuestion] = val;}
			//	else if(proQ.bmState[proQ.currQuestion]){val = proQ.bmState[proQ.currQuestion];}
			//	else{val = 0;}
			//	var bgUrl = "";
			//	if(val == 1){bgUrl = "./commonImages/flag_on.png"; col =proQ.flaggedCol;}
			//	else{
			//		bgUrl = "./commonImages/flag_off.png";
			//		if(proQ.selectedAnswer[proQ.currQuestion]) col = "#3D3D3D";
			//		else col = "#fff";
			//	}
			//	$("#"+proQ.bmBtn).attr('src',bgUrl);
			//	$("#navBtn_"+(proQ.currQuestion+1)).css({'border':'6px '+col+' solid'});
			//}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << setBm", e);}//catchHere*/
	},
	onTouchDown: function(event){
		proQ.downCoords = {};
		var isTouchAllowed = proQ.OnPageSwipeStart(event);
		if (isTouchAllowed == false) return;
		try//tryHere*/
		{
			proQ.isYNotMoved = true;
			proQ.informMe("onTouchDown");
			try{proQ.downX = event.originalEvent.touches[0].pageX; proQ.downY = event.originalEvent.touches[0].pageY;}
			catch(e){proQ.downX = event.pageX; proQ.downY = event.pageY;}
			proQ.downCoords.x = proQ.downX;
			proQ.downCoords.y = proQ.downY;
			proQ.isMouseDown = true;
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << onTouchDown", e);}//catchHere*/
	},
	onTouchUp: function(event){},
	OnScrollStart:function(event){
		//return false;
	},
	OnPageSwipeStart:function(event){
		var target = $(event.target);
		target = target.hasClass("xtraTable") ? target : target.parents(".xtraTable");
		if (target.length > 0)
			if (proQ.hasHScrollBar(target)) return false;
		try{
			if (myScroll.scale > 1) return false;
		}
		catch(e) {}
	},
	activateReviewMode:function(){
		try//tryHere*/
		{
			proQ.initQuest = proQ.currQuestion;
			proQ.informMe("activateReviewMode");
			$("#"+proQ.bmBtn).css({"display":"none"});
			proQ.setLocStrg("_QuizMode","review");
			proQ.currentQuizMode = "review";
			proQ.loadThumbView();
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << activateReviewMode", e);}//catchHere*/
	},
	applyDifImgSize: function(str){
		str = str.replace(/\<img /g, "<img onload='iPhoneImgSize(this);' ");
		return str;
	},
	handleEvent: function(e){
		try//tryHere*/
		{
			proQ.informMe('Prototype > Event Invoked');
			switch(e.type){
				case 'resize': proQ.onResize(); break;
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << handleEvent");}//catchHere*/
	},
	loadQuestion: function (questionNo){
		var currentQuestion;
		try//tryHere*/
		{
			currentQuestion = proQ.questions.questionList.question[questionNo];
			proQ.informMe("loadQuestion");
			if(proQ.currentQuizMode == "review")
				if(proQ.flagQ) $("#"+proQ.bmBtn).css("display","none");
			if(questionNo == null || questionNo == undefined || questionNo == ""){
				if(proQ.currQuestion) proQ.currQuestion = questionNo;
				else questionNo = 0;
			}
			var questHolder = document.getElementById(proQ.holder).children[0].children[0].children[0];
			var optionsHolder = document.getElementById(proQ.holder).children[0].children[1].children[0];
			proQ.currQuestion = questionNo;
			if(questionNo < proQ.totalQuestions){
				var initTime;
				if(proQ.currentQuizMode == "live"){
					if(!isNaN(proQ.questTimerTime) && proQ.questTimerTime != undefined && proQ.questTimerTime != null) initTime = proQ.questTimerTime;
					else initTime = 0;
					$("#"+proQ.timerDiv).text(proQ.secondsToTimeFormat(initTime,2));
				}
				var questionNumber = "";
				if(proQ.autoNumberQuestions){
					var spaces = "";
					if((questionNo) < 9) spaces = "&nbsp;&nbsp;"
					questionNumber = "<b>"+(parseInt(questionNo)+1)+spaces+"</b>&nbsp;";
				}
				var prefix = "<div class=\"questionPrefix\">" + proQ.questionTypePrefix(currentQuestion)+currentQuestion.questionNo + "</div><br/>";
				questHolder.innerHTML = prefix + proQ.applyDifImgSize(questionNumber+currentQuestion.quest);
				if (currentQuestion.questionType == "example" && currentQuestion.exampleSolution) {
					questHolder.innerHTML += "<br/><br /><div class=\"solutionHolder\"><div class=\"solutionPrefix\"><i>Solution</i>&nbsp;&nbsp;<span class=\"solutionArrow\"></span></div><br />"+currentQuestion.exampleSolution+"</div>"
				}
				optionsHolder.innerHTML = "";
					//Load by Type
				var existingAns = "";
				if(proQ.selectedAnswer[questionNo]){existingAns = proQ.selectedAnswer[questionNo];}
				if(currentQuestion.questionType == "simpleMath"){
					optionsHolder.innerHTML += "<div id=\"mathGrid\"></div>";
					proQ.applyMathGrid("mathGrid",8);
				}
				else if(currentQuestion.questionType == "choice"){
					var optionsString = "";
					proQ.isOptionsImage = false;
					for(var currOption = 0; currOption<currentQuestion.options.length; currOption++){
						if(currentQuestion.options[currOption].indexOf("<img") >= 0){
							proQ.isOptionsImage = true;
						}
					}
					for(var currOption = 0; currOption<currentQuestion.options.length; currOption++){
						var listId = "";
						var classId= "";
						if(proQ.optListType == "a"){
							if(proQ.optAltratePageChange) {
								if(questionNo%2 == 0){classId = proQ.alphaSet[currOption]; listId = "<div class=\"optionBtn"+classId.toLowerCase()+"\">"+proQ.alphaSet[currOption]+"</div>";}
								else{ classId = proQ.alphaSet[currOption+4]; listId = "<div class=\"optionBtn"+classId.toLowerCase()+"\">"+proQ.alphaSet[currOption+4]+"</div>";}
							}
							else{classId = proQ.alphaSet[currOption]; listId = "<div class=\"optionBtn"+classId.toLowerCase()+"\">"+proQ.alphaSet[currOption]+"</div>";}
						}
						var isAlltext = false;
						if(currentQuestion.special && currentQuestion.special.indexOf("allText") >=0){
							isAlltext = true;
						}
						if(proQ.isOptionsImage && !isAlltext){
							var border = 4;
							var imgMrgTop = (-28*($(window).width()/1024));
							var imgHeight = 0;
							var imgWidth = 290;
							var mixedLines = "inline-block";
							var addClass = "";
							try{if(currentQuestion.special && currentQuestion.special.indexOf("imageAndText") >= 0){mixedLines = "table-cell"; addClass = "class='optionTable'";}}catch(e){}
							try{if(currentQuestion.special && currentQuestion.special.indexOf("noLine") >= 0 ){border = 0;}}catch(e){}
							if(currOption%2 == 0){optionsString += "<div "+addClass+" style=\"display: "+mixedLines+"; margin:0px padding:0px;\">";}
							optionsString += "<div id=\"option_"+(currOption+1)+"\" class=\"option\" style=\"border:"+border+"px #000 solid; margin:10px; margin-left:5px; margin-right:5px; display:block; width:"+imgWidth+"px; padding-bottom:10px;\"><div id=\"optionBtn_"+(currOption+1)+"\" class=\"optionBtn\" style=\"margin-left:5px; margin-top:5px;\">"+listId+"</div><div style=\"margin:auto; margin-top:"+imgMrgTop+"px; \">"+currentQuestion.options[currOption]+"</div></div>";
							$("#"+optionsHolder.id).css({"text-align":"center", "padding":"0px", "padding-top":"10px"});
							if(currOption%2 == 1){optionsString += "</div>";}
						}
						else{
							optionsString += "<div id=\"option_"+(currOption+1)+"\" class=\"option\"><div id=\"optionBtn_"+(currOption+1)+"\" class=\"optionBtn\">"+listId+"</div><span class=\"optionContent\">"+currentQuestion.options[currOption]+"</span></div>";
						}
					}
					var mixed = false;
					try{if(currentQuestion.special && currentQuestion.special.indexOf("imageAndText") >= 0){mixed = true;}}catch(e){}
					if(mixed) optionsString = "<div style='display:table; margin:auto; margin-top:15px;'>"+optionsString+"</div>";
					optionsHolder.innerHTML = proQ.applyDifImgSize(optionsString);
					if($(window).width() > 850) $(".optionTable").css({"display":"table-cell"});
					else $(".optionTable").css({"display":"inline-block"});
				}
				else if(currentQuestion.questionType == "fillIn"){
					optionsHolder.innerHTML += "<textarea onKeyUp=\"proQ.onTextInput(this)\" id=\"inpText\" onClick=\"this.focus();\">"+existingAns+"</textarea>";
				}
				else if(currentQuestion.questionType == "shortFill"){
					optionsHolder.innerHTML += "<textarea onKeyUp=\"proQ.onTextInput(this)\" id=\"inpText\" onClick=\"this.focus();\">"+existingAns+"</textarea>";
				}
				else if(currentQuestion.questionType == "longFill"){
					optionsHolder.innerHTML += "<textarea onKeyUp=\"proQ.onTextInput(this)\" id=\"inpText\" onClick=\"this.focus();\">"+existingAns+"</textarea>";
				}
				else if(currentQuestion.questionType == "match"){
					optionsHolder.innerHTML += "";
					$(optionsHolder).hide();
				}
				else if(currentQuestion.questionType == "trueOrFalse"){
					var optionsString = "";
					optionsString += "<div id=\"option_1\" class=\"option\"><div id=\"optionBtn_1\" class=\"optionBtn\">"+"</div><span class=\"optionContent\">True</span></div>";
					optionsString += "<div id=\"option_2\" class=\"option\"><div id=\"optionBtn_2\" class=\"optionBtn\">"+"</div><span class=\"optionContent\">False</span></div>";
					optionsHolder.innerHTML += optionsString;
				}
				else if (currentQuestion.questionType == "example") {
					$(optionsHolder).hide();
				}
				else $(optionsHolder).hide();
				
				if(proQ.currentQuizMode == "live" && currentQuestion.options.length > 0){
					if(proQ.isTouchDevice){try{$(".option").unbind('touchend');}catch(e){}$(".option").bind('touchend',proQ.checkOption);}
					else{try{$(".option").unbind('mouseup');}catch(e){} $(".option").bind('mouseup',proQ.checkOption);}
				}
				if (currentQuestion.questionType == "example") {
					if(proQ.isTouchDevice){
						try{
							$(".solutionHolder").unbind("touchend");
						}catch(e){}
						$(".solutionHolder").bind("touchend", proQ.showSolution);
					}
					else{
						try{
							$(".solutionHolder").unbind("mouseup");
						}catch(e){ }
						$(".solutionHolder").bind("mouseup", proQ.showSolution);
					}
				}
				if(currentQuestion.options.length > 0 && proQ.selectedAnswer[questionNo] && !isNaN(proQ.selectedAnswer[questionNo]) && proQ.selectedAnswer[questionNo] != 0)
				$("#option_"+proQ.selectedAnswer[questionNo]).addClass("selected");
				
				if(proQ.currentQuizMode == "review"){proQ.reviewAnswer();}
				proQ.setLocStrg("_CurrentQuestion",questionNo);
				$("#"+proQ.displayQNo).html((questionNo+1) + "/" + proQ.totalQuestions);
				proQ.setBm();
				var swipeThumbVal = -parseInt(proQ.currQuestion/5);
				if(swipeThumbVal > 0){swipeThumbVal = 0;}
				proQ.swipeThumb(swipeThumbVal);
				proQ.showHideSol(proQ.selectedAnswer[proQ.currQuestion]);
			}
			try{M.parseMath(document.body);}catch(e){}
			proQ.checkBtnState();
			proQ.onContentLoaded();
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << loadQuestion",e);}//catchHere*/
	},
	showSolution:function(event){
		if (proQ.downCoords.x) {
			if(proQ.swipeDirection(proQ.downCoords, event).isYNotMoved){
				var target = $(event.target).hasClass("solutionPrefix") ? $(event.target) : $(event.target).parents(".solutionPrefix");
				if(target.length > 0){
					if(proQ.selectedAnswer[proQ.currQuestion]){
						proQ.selectedAnswer[proQ.currQuestion] = 0;
						proQ.showHideSol(false);
					}
					else {
						proQ.selectedAnswer[proQ.currQuestion] = 1;
						proQ.showHideSol(true);
					}
				}
			}
		}
	},
	showHideSol:function(isShow){
		try{
			var currentQuestion = proQ.questions.questionList.question[proQ.currQuestion];
			if (currentQuestion.questionType == "example") {
				proQ.selectedAnswer[proQ.currQuestion] = isShow ? 1 : 0;
				var questHolder = document.getElementById(proQ.holder).children[0];
				var solutionHolder = $(questHolder).find(".solutionHolder");
				if (solutionHolder.length > 0) {
					if (proQ.selectedAnswer[proQ.currQuestion]) {
						$(questHolder).find(".solutionHolder").css({"height":""});
						$(questHolder).find(".solutionArrow").html("&#9650;");
					}
					else{
						$(questHolder).find(".solutionHolder").css({"height":"20px"});
						$(questHolder).find(".solutionArrow").html("&#9660;");
					}
					setTimeout(function(){
						try {
							if(myScroll) myScroll.refresh();
						} catch(e) { }
					}, 100);
				}
			}
		}
		catch(e){ }
	},
	onTextInput: function(event){
		try//tryHere*/
		{
			if(proQ.currentQuizMode == "live"){
				var upX = 0;
				var upY = 0;
				try{upX = event.originalEvent.changedTouches[0].pageX; upY = event.originalEvent.changedTouches[0].pageY;}
				catch(e){upX = event.pageX; upY = event.pageY;}
				var isYMotMoved = (proQ.downY > (upY - proQ.swipeSensitivityY) && proQ.downY < (upY+proQ.swipeSensitivityY));
				if(proQ.downX < (upX+proQ.swipeSensitivityX) && proQ.downX > (upX-proQ.swipeSensitivityX) && isYMotMoved){
					playClickAudio();
                    var id = event.target.id;
					var columnId = "MG_d" + (id.substr(id.lastIndexOf("_")));
					if(document.getElementById(columnId).innerHTML.trim() == this.innerHTML.toString().trim()){
						document.getElementById(columnId).innerHTML = "&nbsp;";
					}
					else{
						document.getElementById(columnId).innerHTML = this.innerHTML.toString().trim();
					}
					proQ.selectedAnswer[proQ.currQuestion] = proQ.getTextVal();
					var borderCol = "";
					//if(proQ.selectedAnswer[proQ.currQuestion].replace(/\&nbsp;/g,"").replace(/\*/g,"").trim() == ""){$("#navBtn_"+(proQ.currQuestion+1)).css({"background-color":"#ffffff","color":"#000000"}); proQ.selectedAnswer[proQ.currQuestion] = null; borderCol = "#ffffff";}
					//else{$("#navBtn_"+(proQ.currQuestion+1)).css({"background-color":"#3D3D3D","color":"#ffffff"});borderCol = "#3D3D3D";}
					proQ.setLocStrg("_SelectedAnswer",proQ.selectedAnswer);
					//if(!proQ.bmState[proQ.currQuestion] || proQ.bmState[proQ.currQuestion] <= 0){
					//$("#navBtn_"+(proQ.currQuestion+1)).css({"border":"6px "+borderCol+" solid"});
					//}
				}
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << onTextInput", e);}//catchHere*/
		//if(proQ.selectedAnswer[proQ.currQuestion] > 0){proQ.selectedAnswer[proQ.currQuestion] = "+"+proQ.selectedAnswer[proQ.currQuestion];}
	},
	setTextVal: function(){
		var ansToFill;
		if(proQ.currentQuizMode == "live" && proQ.selectedAnswer[proQ.currQuestion]){
			ansToFill = proQ.selectedAnswer[proQ.currQuestion].split('*');
		}
		else if(proQ.currentQuizMode == "review" && proQ.selectedAnswer[proQ.currQuestion]){
			ansToFill = proQ.selectedAnswer[proQ.currQuestion].split('*');
		}
		var id = 0;
		var dispId = "MG_d_"+id;
		while(document.getElementById(dispId)){
			if(ansToFill){if(ansToFill[id]){document.getElementById(dispId).innerHTML = ansToFill[id];}}
			id++;
			dispId = "MG_d_"+id;
		}
	},
	getTextVal: function(){
		var id = 0;
		var dispId = "MG_d_"+id;
		var output = "";
		while(document.getElementById(dispId)){
			if(output != ""){output += "*"}
			output+=document.getElementById(dispId).innerHTML;
			id++;
			dispId = "MG_d_"+id;
		}
		return output;
	},
	checkBtnState: function(){
		try//tryHere*/
		{
			var prevBtn = document.getElementById(proQ.prevBtn);
			var nextBtn = document.getElementById(proQ.nextBtn);
			if(proQ.useNavParent){
				prevBtn = prevBtn.parentNode;
				nextBtn = nextBtn.parentNode;
			}
		proQ.informMe("checkBtnState");
		if(proQ.currQuestion <= 0){
			prevBtn.style.display = 'none';
		}
		else{
			prevBtn.style.display = 'block';
		}
		var end = proQ.totalQuestions;
		if(proQ.currentQuizMode == "review" || !proQ.isReviewable){end = proQ.totalQuestions-1;}
		if(proQ.currQuestion >= end){
			//nextBtn.innerHTML = proQ.replayBtnText;
			nextBtn.style.display = 'none';
		}
		else{
			nextBtn.style.display = 'block';
			//nextBtn.innerHTML = proQ.nextBtnText;
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << checkBtnState", e);}//catchHere*/
	},
	checkOption: function(event){
		try//tryHere*/
		{
		proQ.informMe("checkOption");
		var upX = 0;
		var upY = 0;
		try{upX = event.originalEvent.changedTouches[0].pageX; upY = event.originalEvent.changedTouches[0].pageY;}
		catch(e){upX = event.pageX; upY = event.pageY;}
		var isYMotMoved = (proQ.downY > upY - proQ.swipeSensitivityY && proQ.downY < upY+proQ.swipeSensitivityY);
		if(proQ.downX < upX+proQ.swipeSensitivityX && proQ.downX > upX-proQ.swipeSensitivityX && isYMotMoved){
			var opt = event;
			var optBckup = opt;
			if($(optBckup.target).hasClass("option")) opt = $(optBckup.target)[0]
			else opt = $(optBckup.target).parents(".option")[0];
			var isAlreadyActive = $(opt).hasClass("selected");
			var corrAnswer = proQ.questions.questionList.question[proQ.currQuestion].correctAnswer;
			$(".option").removeClass("selected");
			if(!isAlreadyActive){
				$(opt).addClass("selected");
				//$("#navBtn_"+(proQ.currQuestion+1)).css({"background-color":"#3D3D3D","color":"#ffffff"});
				//if(!proQ.bmState[proQ.currQuestion] || proQ.bmState[proQ.currQuestion] <= 0){$("#navBtn_"+(proQ.currQuestion+1)).css({"border":"6px #3D3D3D solid"});}
				proQ.selectedOption = parseInt(opt.id.substr(opt.id.indexOf('_')+1),10);
				proQ.selectedAnswer[proQ.currQuestion] = proQ.selectedOption;
				if(proQ.selectedOption == corrAnswer) proQ.score[proQ.currQuestion] = proQ.questions.questionList.question[proQ.currQuestion].value;
				else proQ.score[proQ.currQuestion] = 0;
			}
			else{
				proQ.score[proQ.currQuestion] = 0;
				proQ.selectedAnswer[proQ.currQuestion] = null;
				$(opt).removeClass("selected");
				//if(!proQ.bmState[proQ.currQuestion] || proQ.bmState[proQ.currQuestion] <= 0){$("#navBtn_"+(proQ.currQuestion+1)).css({"border":"6px #fff solid"});}
			}
			if(proQ.validateOnSelect) proQ.validateAnswer();
			playClickAudio();
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << checkOption", e);}//catchHere*/
	},
	validateAnswer: function(){
		try//tryHere*/
		{
		proQ.informMe("validateAnswer");
		if(!proQ.validateOnSelect){document.getElementById(proQ.validateBtn).style.display = 'none';}
		proQ.setLocStrg("_Score",proQ.score);
		proQ.setLocStrg("_SelectedAnswer",proQ.selectedAnswer);
		proQ.checkAllAnswers();
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << validateAnswer", e);}//catchHere*/
	},
	checkAllAnswers: function(){
		try//tryHere*/
		{
		proQ.informMe("checkAllAnswers");
		/*if(proQ.currQuestion+1 == proQ.totalQuestions && proQ.currentQuizMode == "live")
			if(proQ.selectedAnswer[proQ.currQuestion]) proQ.promptReviewMode();*/
		/*var isAllAnswered = false;
		if(proQ.selectedAnswer.length == proQ.totalQuestions){
			for(var i=0; i<proQ.selectedAnswer.length; i++)
			{
				if(!proQ.selectedAnswer[i]){
					isAllAnswered = false;
					break;
				}
				else{
					//informMe(i+' :> '+'States TRUE');
					isAllAnswered = true;
				}
			}
		}
		if(isAllAnswered){
			proQ.activateReviewMode();
		}*/
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << checkAllAnswers", e);}//catchHere*/
	},
	promptReviewMode: function(){
		try//tryHere*/
		{
		proQ.informMe("promptReviewMode");
		onSubmit();
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << promptReviewMode", e);}//catchHere*/
	},
	reviewAnswer: function(){
		try//tryHere*/
		{
		proQ.informMe("reviewAnswer");
		var result = proQ.currResult(proQ.currQuestion);
		var corrAnswer = proQ.questions.questionList.question[proQ.currQuestion].correctAnswer;
		var reviewComment = proQ.questions.questionList.question[proQ.currQuestion].reviewComment;
		var responseHolder = null;
		var applyBmCol = "";
		if(document.getElementById(proQ.holder).children[0].children.length > 2){responseHolder = document.getElementById(proQ.holder).children[0].children[2];}
		if(proQ.questions.questionList.question[proQ.currQuestion].options.length > 0){
			if(document.getElementById("option_"+corrAnswer)){$("#"+document.getElementById("option_"+corrAnswer).children[0].id).css({"background-color":"#ff0","color":"#000"})};
			if(result == "correct"){}
			else if(result == "wrong"){
				if(document.getElementById("option_"+corrAnswer)){
					$("#"+document.getElementById("option_"+(parseInt(proQ.selectedAnswer[proQ.currQuestion]))).children[0].id).css({"background-color":"#f00","border":"#f00 2px solid"});
					//$("#"+document.getElementById("option_"+(parseInt(proQ.selectedAnswer[proQ.currQuestion]))).children[0].id).html("<img src=\"./commonImages/wrong.png\" style=\"width:100%; height:100%\"/>");
					$("#"+document.getElementById("option_"+(parseInt(proQ.selectedAnswer[proQ.currQuestion]))).children[0].id).text("X");
				}
			}
			else{}
		}
		else{
			
		}
		if(responseHolder){
			responseHolder.style.display = "block";
			responseHolder.innerHTML = proQ.applyDifImgSize(reviewComment);
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << reviewAnswer", e);}//catchHere*/
	},
	currResult: function(qNo){
		try//tryHere*/
		{
		proQ.informMe("currResult");
		var corrAnswer = proQ.questions.questionList.question[qNo].correctAnswer;
		var selectedAns;
		if(proQ.selectedAnswer[qNo]){
			if(proQ.selectedAnswer[qNo].toString().indexOf("\u2013") >=0){ selectedAns = proQ.selectedAnswer[qNo].toString().replace("\u2013","-");}
			else{selectedAns = proQ.selectedAnswer[qNo];}
		}else{selectedAns = proQ.selectedAnswer[qNo];}
		if(!proQ.questions.questionList.question[qNo].options || proQ.questions.questionList.question[qNo].options.length == 0){
			if(selectedAns){selectedAns = parseFloat(selectedAns.replace(/\&nbsp;/g,"").replace(/\*/g,""));}
		}
		var isRange = false;
		try{
			if(corrAnswer.indexOf("~") > 0){isRange = true;}
			else{isRange = false;}
		}
		catch(e){isRange = false;}
		if(isRange){
			var minVal;
			var maxVal;
			if(corrAnswer.indexOf("~") > 0){
				minVal = parseFloat(corrAnswer.split("~")[0]);
				maxVal = parseFloat(corrAnswer.split("~")[1]);
			}
			else minVal = maxVal = corrAnswer;
			if(minVal <= selectedAns && selectedAns <= maxVal) return "correct";
			else if(selectedAns) return "wrong";
			else return "notAnswered";
			return "correct";
		}
		else{
			corrAnswer = parseFloat(corrAnswer);
			if(selectedAns == corrAnswer) return "correct";
			else if(selectedAns) return "wrong";
			else return "notAnswered";
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << currResult", e);}//catchHere*/
	},
	isOneOfThePages:function(str){
		if(str != "coverPage" && str != "homePage" && str != "tocPage" && str != "settingsPage" && str != "instructionPage" && str!= "myReviewPage") return false;
		else return true;
	},
	changeNavBtnsColor:function(str,newCol){
	        if(str.indexOf("prevBtn")!=-1)$("#"+str).css({'border-right-color':newCol});
		else if(str.indexOf("nextBtn")!=-1)$("#"+str).css({'border-left-color':newCol});
	},
	tryDisplayResult: function(){
		if(proQ.currentQuizMode == "review") proQ.displayResult();
	},
	displayResult: function(){
		//proQ.currQuestion = 0;
		setTimeout(function(){proQ.activateReviewMode();},250);
		proQ.currentQuizMode = "review";
		proQ.byLoadPage("myReviewPage");
		$("#resCorrect").text(proQ.getResult("correct"));
		$("#resTime").text(proQ.getResult("time"));
		$("#resUnanswered").text(proQ.getResult("notAnswered"));
		$("#resIncorrect").text(proQ.getResult("wrong"));
	},
	prevQuestion: function(questionNumber){
		try//tryHere*/
		{
		proQ.changeNavBtnsColor(proQ.prevBtn,proQ.dimColor);
		if(isNaN(questionNumber) && proQ.currentPage == "quiz"){
			try{
				if(!proQ.isOneOfThePages(questionNumber)) questionNumber = proQ.currQuestion-1;
			}
			catch(e){
				questionNumber = proQ.currQuestion-1;
			}
		}
		var result = "";
		if(!isNaN(questionNumber)){
			if(questionNumber >= 0) result = "passed";
			else{
				result = "blocked";
				questionNumber = 0;
			}
		}
		else if((proQ.currentPage == "quiz" && (questionNumber == "coverPage" || questionNumber == "homePage" || questionNumber == "tocPage")) || (proQ.currentPage == "myReviewPage" && (questionNumber == "coverPage" || questionNumber == "homePage")) || proQ.currentPage == "settingsPage" || proQ.currentPage == "instructionPage" || proQ.currentPage == "tocPage")
			result = "pages";
		else result = "blocked";
		if (proQ.currentPage == "tocPage") questionNumber = "homePage";
		if((result == "passed" || result == "pages" || questionNumber) && result!= "blocked"){
			proQ.beforePageLoad();	
			proQ.unBindTouchEvents();
			$("#"+proQ.container).css({'margin-left':-$(window).width()+'px'});
			proQ.addNewSlide(document.getElementById(proQ.holder),"_prev");
			if(proQ.currentPage == "quiz" && result == "passed") proQ.loadQuestion(questionNumber);
			else{
				if(!proQ.isOneOfThePages(questionNumber)){questionNumber = null;}
				if(!questionNumber) proQ.loadPage("prev");
				else proQ.loadPage(questionNumber);
			}
			proQ.swapSlides();
			proQ.applyScroll();
			$("#"+proQ.container).animate({'marginLeft':0+'px'},{ duration: proQ.timeToSwipe, queue: true,
				complete: function() {
					proQ.bindTouchEvents();
					proQ.onEveryPageLoadComplete();
				}
                });
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << prevQuestion", e);}//catchHere*/
	},
	nextQuestion: function(questionNumber){
        try//tryHere*/
		{
		proQ.changeNavBtnsColor(proQ.nextBtn,proQ.dimColor);
		if(isNaN(questionNumber) && proQ.currentPage == "quiz"){
			try{
				if(!proQ.isOneOfThePages(questionNumber)) questionNumber = proQ.currQuestion+1;
			}
			catch(e){
				questionNumber = proQ.currQuestion+1;
			}
		}
		var result = "";
		if(!isNaN(questionNumber)){
			if(questionNumber < proQ.totalQuestions){
				result = "passed";
			}
			else if(questionNumber == proQ.totalQuestions){
				result = "end";
			}
		}
		else if(proQ.currentPage != "quiz" && proQ.currentPage != "instructionPage"){
			result = "pages";
		}
		if(result == "end"){
			if(proQ.currentQuizMode == "live"){
				//proQ.displayResult();
				proQ.promptReviewMode();
			}
		}
		else if(result == "passed" || (result == "pages" && proQ.currentPage != "homePage") || questionNumber){
			proQ.beforePageLoad();
			proQ.unBindTouchEvents();
			proQ.addNewSlide(document.getElementById(proQ.holder),"_prev");
			if(proQ.currentPage == "quiz" && !isNaN(questionNumber))
				proQ.loadQuestion(questionNumber);
			else{
				if (proQ.currentPage == "tocPage" && !isNaN(questionNumber)) proQ.loadPage(questionNumber);
				else{
					if(!proQ.isOneOfThePages(questionNumber)){questionNumber = null;}
					if(!questionNumber) proQ.loadPage("next");
					else proQ.loadPage(questionNumber);
				}
			}
            proQ.applyScroll();
			$("#"+proQ.container).animate({'marginLeft':-$(window).width()+'px'},{ duration: proQ.timeToSwipe, queue: true,
				complete: function() {
						proQ.swapSlides();
						$("#"+proQ.container).css({'margin-left':0+'px'});
						proQ.bindTouchEvents();
						proQ.onEveryPageLoadComplete();
					}
				});
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << nextQuestion", e);}//catchHere*/
	},
	beforePageLoad: function(){
        if(navigator.userAgent.match(/iPad/i)=="iPad")playClickAudio();
        else clickAudio.play();

	},
	onEveryPageLoadComplete:function(){
		try//tryHere*/
		{
			//playClickAudio();
  //          if(navigator.userAgent.match(/iPad/i)!="iPad")playClickAudio();
			proQ.changeNavBtnsColor(proQ.prevBtn,"#fff")
			proQ.changeNavBtnsColor(proQ.nextBtn,"#fff")
			proQ.setLocStrg("_LastPage",proQ.currentPage);
			proQ.informMe("onEveryPageLoadComplete");
			proQ.checkAllAnswers();
			proQ.onPageLoadComplete();
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << onEveryPageLoadComplete", e);}//catchHere*/
	},
	onPageLoadComplete:function(){proQ.informMe("onPageLoadComplete");},
	gotoQuestion: function(questionNumber){
		try//tryHere*/
		{
		proQ.informMe("gotoQuestion");
		questionNumber--;
		if(proQ.currQuestion > questionNumber){
			proQ.prevQuestion(questionNumber);
		}
		else if(proQ.currQuestion < questionNumber){
			proQ.nextQuestion(questionNumber);
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << gotoQuestion", e);}//catchHere*/
	},
	swapSlides: function(){
		try//tryHere*/
		{
		proQ.informMe("swapSlides");
		$('#'+document.getElementById(proQ.container).children[1].id).prependTo('#'+proQ.container);
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << swapSlides", e);}//catchHere*/
	},
    applyScroll: function(){},
	addNewSlide: function(obj,str){
		try//tryHere*/
		{
		proQ.informMe("addNewSlide");
		try{$("#"+proQ.holder+"_prev").remove();}catch(e){}
		proQ.changeId(obj,str);
		$("#"+proQ.container).append(proQ.holderTemplate);
		$("#"+proQ.container).css({'width':($(window).width()*2)+'px'});
		$("."+$("#"+proQ.holder).attr('class')).css({'width':$(window).width()+'px'});
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << addNewSlide", e);}//catchHere*/
	},
	changeId: function(obj,str){
		try//tryHere*/
		{
		proQ.informMe("changeId");
		try{obj.id = obj.id+str;}
		catch(e){}
		for(var i=0; i<obj.children.length; i++){
			proQ.changeId(obj.children[i],str);
		}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << changeId", e);}//catchHere*/
	},
	setTimerState: function(state){
		try//tryHere*/
		{
		proQ.informMe("setTimerState");
		proQ.questTimerState = state;
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << setTimerState", e);}//catchHere*/
	},
	questTimer: function(funct){
		try//tryHere*/
		{
			if(funct == "new"){
				var startTime;
				if(proQ.questSubTimerTime[proQ.currQuestion] == undefined || proQ.questSubTimerTime[proQ.currQuestion] == null){
					proQ.questSubTimerTime[proQ.currQuestion] = 0;
				}
				startTime = proQ.questSubTimerTime[proQ.currQuestion];
				//New Timer Initalized
				try{window.clearInterval(proQ.timer);}catch(e){}
				proQ.timer = setInterval("proQ.questTimer()",1000);
				if(!startTime){startTime = 0;}
				proQ.questSubTimerTime[proQ.currQuestion] = startTime;
				proQ.questTimerState = "running";
			}
			//proQ.informMe("Time : > "+proQ.questTimerTime);
			if(proQ.currentQuizMode == "live" && proQ.currentPage == "quiz"){
				var startTime;
				if(proQ.questSubTimerTime[proQ.currQuestion] == undefined || proQ.questSubTimerTime[proQ.currQuestion] == null){
					proQ.questSubTimerTime[proQ.currQuestion] = 0;
				}
				startTime = proQ.questSubTimerTime[proQ.currQuestion];
				
				if(proQ.questTimerState == "start"){
					if(!startTime){startTime = 0;}
					proQ.questSubTimerTime[proQ.currQuestion] = startTime;
					proQ.questTimerState = "running";
				}
				else if(proQ.questTimerState == "pause"){}
				else if(proQ.questTimerState == "reset"){}
				else if(proQ.questTimerState == "running"){
					//proQ.questSubTimerTime[proQ.currQuestion]++;
					proQ.questTimerTime++;
					if(proQ.questTimerTime%900 == 0)
					{
						var times = parseInt((proQ.questTimerTime-900)/3600)+1;
						playTimerAudio(times);
					}
				}
				if(proQ.timerDiv){
					$("#"+proQ.timerDiv).text(proQ.secondsToTimeFormat(proQ.questTimerTime,2));
				}
				proQ.setLocStrg("_LastTime",proQ.questTimerTime);
				proQ.setLocStrg("_SubTimerTime",proQ.questSubTimerTime);
				$("#"+proQ.timerDiv).css({"color":"#fff"});
			}
			else{
				$("#"+proQ.timerDiv).text(proQ.reviewTime);
				$("#"+proQ.timerDiv).css({"color":"#ccc"});
			}
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << questTimer", e);}//catchHere*/
	},
	setLocStrg: function(id,val){
		try//tryHere*/
		{localStorage.setItem(proQ.appID+id,val);}
		catch(e){proQ.informMe("EXCEPTION THROWN in << setLocStrg", e);}//catchHere*/
	},
	secondsToTimeFormat:function(seconds, toDisp){
		try//tryHere*/
		{
		var sec = seconds%60;
		var min = parseInt((seconds/60)%60);
		var hrs = parseInt((seconds/3600)%60);
		var time;
		if(toDisp == 2){
			time = proQ.formatNumberLength(hrs,1)+":"+proQ.formatNumberLength(min,2);
		}
		else{
			time = proQ.formatNumberLength(hrs,1)+":"+proQ.formatNumberLength(min,2)+":"+proQ.formatNumberLength(sec,2);
		}
		return time;
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << secondsToTimeFormat", e);}//catchHere*/
	},
	formatNumberLength: function(num, length) {
		try//tryHere*/
		{
		var returnVal = "" + num;
		while (returnVal.length < length) {returnVal = "0" + returnVal;}
		return returnVal;
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << formatNumberLength", e);}//catchHere*/
	},
	onResize: function(){
		try//tryHere*/
		{
		proQ.informMe("onResize");
		$("#"+proQ.container).css({'width':($(window).width()*2)+'px','margin-left':0+'px'});
		$("."+$("#"+proQ.holder).attr('class')).css({'width':$(window).width()+'px'});
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << onResize", e);}//catchHere*/
	},
	evaluateValues: function(req){
		try//tryHere*/
		{
		proQ.informMe("evaluateValues");
		var retVal = 0;
		for(var i=0; i<proQ.totalQuestions; i++){
			var result = proQ.currResult(i);
			if(result == "correct" && req == "correct") retVal++;
			else if(result == "wrong" && req == "wrong") retVal++;
			else if(result == "notAnswered" && req == "notAnswered") retVal++;
		}
		return retVal;
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << evalueateValues", e);}//catchHere*/
	},
	getResult: function(type){
		try//tryHere*/
		{
			proQ.informMe("getResult");
			proQ.evaluateValues();
			if(type == "time") return proQ.secondsToTimeFormat(proQ.questTimerTime,2);
			else return proQ.evaluateValues(type);
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << getResult", e);}//catchHere*/
	},
	test:function(){
		alert('Invoked');
	},
	informMe: function(str, exc){
		//console.log(str, exc);
	},
	applyMathGrid: function(divId,cols){
		try//tryHere*/
		{
		var typeInTable = "<table cellspacing=\"0\" cellpadding=\"0\" class=\"mathGrid\">";
		for(var j=-2; j<=9; j++){
			var colText = "";
			colText += "<tr>";
			for(var i=0; i<cols; i++){
				var content = j;
				var additionalClass = "";
				if(i>0){
					if(j == -1){content = "."; additionalClass = " mathGridDot";}
					if(j == -2){content = "<div id=\"MG_d_"+i+"\" class=\"mathGridDisplay\" >&nbsp;</div>";}
				}
				if(i==0){
					if(j == -2){content = "<div id=\"MG_d_"+i+"\" class=\"mathGridDisplay\">&nbsp;</div>";}
					else if(j == -1){content = "+";}
					else if(j == 0){content = "&ndash;";}
					else{content = "&nbsp;";}
				}
				if(j != -2){
					try{if(content.toString().trim() != "" && content.toString().trim() != " " && content.toString().trim() != "&nbsp;"){content = "<div class=\"mathGridBtn"+additionalClass+"\" id=\"mathGridBtn_"+j+ "_" + i+"\">"+content+"</div>";}}catch(e){}
				}
				if(i==0){
					if(j > 0){colText += "<td style=\"border:0px;\">"+content+"</td>";}
					else{colText += "<td style=\"border-left:0px;\">"+content+"</td>";}
				}
				else{
					if(j==9){colText += "<td style=\"border-bottom:0px;\">"+content+"</td>";}
					else{colText += "<td>"+content+"</td>";}
				}
			}
			colText += "</tr>";
			typeInTable += colText;
		}
		typeInTable += "</table>";
		$("#"+divId).html(typeInTable);
		if(proQ.isTouchDevice){try{$(".mathGridBtn").unbind('touchend');}catch(e){} $(".mathGridBtn").bind('touchend',proQ.onTextInput);}
		else{try{$(".mathGridBtn").unbind('mouseup');}catch(e){} $(".mathGridBtn").bind('mouseup',proQ.onTextInput);}
		proQ.setTextVal();
		}
		catch(e){proQ.informMe("EXCEPTION THROWN in << applyMathGrid", e);}//catchHere*/
	},
	hasHScrollBar:function(element){
		return element.get(0).scrollWidth > element.width();
	}
}


function playClickAudio(){
    /*if(navigator.userAgent.match(/iPad/i)=="iPad")
    {
        try
        {
            clickAudio.load();
        }
        catch(e)
        {
        
        }
    }*/
    clickAudio.play();
}

function playTimerAudio(times)
{
    try
    {
        timeAudio.load();
    }
    catch(e)
    {
        
    }
    if(times > 0){
        timeAudio.play();
		times--;
		if(times > 0){setTimeout(function(){playTimerAudio(times);},1000);}
    }
}
function iPhoneImgSize(img){
	if($(window).width() < 550){
		img.width/=2;
	}
	$(img).css({"max-width":"100%"});
	img.onload=null;
}


lolScroll:
===============



/*
 *
 *
 *LOLScroll.js v2.2
 *This is a lolScroll by WEB.RND@LOL
 *Light weight scroller
 *
 *
 *
 *
 */


window.lolScroll = function(element, resetBtn) {
  if (!element) return null;
  var _this = this;
  this.currElementTop = 0;
  this.resetBtn = resetBtn;
  this.currentDownVal = 0;
  this.friction = 0.7;
  this.fricTemp = 0;
  
  this.container = document.getElementById(element);
  this.container.style.overflow = 'hidden';
  this.element = this.container.children[0]; // the slide pane
  this.snapVal = 200;
  this.timeToScroll = 150;
  this.isDrag = false;
  this.downVal = 0;
  obj = this;
  obj.isTouchDevice = 'ontouchstart' in document.documentElement;
  this.setup();

  if (this.element.addEventListener) {
    window.addEventListener('resize', this, false);
  }
};

lolScroll.prototype = {
	setup: function() {
	  obj = this;
	  for(var i=this.container.children.length; i>1; i--){
	    this.container.children[i-1].remove();
	  }
	  try{obj.unbindTouchEvents();}catch(e){}
	  obj.bindTouchEvents();
	  $("#"+this.container.id).append("<div id=\"lolScrollBar\" style=\"position:absolute; overflow: hidden; right:0px; top:0px; width:4px; background:#d4d4d4; border-radius: 2px; height:"+$("#"+this.container.id).css('height')+";\"><div id=\"lolScrollBtn\" style=\"height:100%; background:#787878; border-radius: 2px;\"></div></div>");
	  obj.refresh();
	  setTimeout(function(){obj.refresh();},100);
	  obj.informMe("Scroll >> Setup");
	},
	handleEvent: function(e) {
	  switch (e.type) {
	  case 'resize': break;
	  }
	  obj.informMe("Scroll >> EventInvoked");
	},
	bindTouchEvents: function(){
	  try{obj.unbindTouchEvents();}catch(e){}
	  if(obj.isTouchDevice){
	    $("#"+this.container.id).bind('touchstart', function(event){obj.onTouchDown(event);});
	    $("#"+this.container.id).bind('touchmove', function(event){obj.onTouchMove(event);});
	    $(window).bind('touchend', function(event){obj.onTouchUp(event);});
	  }
	  else{
		$("#"+this.container.id).bind('mousedown', function(event){obj.onTouchDown(event);});
	    $("#"+this.container.id).bind('mousemove', function(event){obj.onTouchMove(event);});
	    $(window).bind('mouseup', function(event){obj.onTouchUp(event);});
	  }
	  obj.informMe("Scroll >> BindTouch");
	},
	unbindTouchEvents: function(){
	  if(obj.isTouchDevice){
	    $("#"+this.container.id).unbind('touchstart');
	    $("#"+this.container.id).unbind('touchmove');
	    $(window).unbind('touchend');
	  }
	  else{
		$("#"+this.container.id).unbind('mousedown');
	    $("#"+this.container.id).unbind('mousemove');
	    $(window).unbind('mouseup');
	  }
	  obj.informMe("Scroll >> UnBindTouch");
	},
	onTouchDown: function(event){
	  this.isDrag = true;
	  try
	  {
	      this.downVal = event.originalEvent.touches[0].pageY;
	  }
	  catch(e){
	      this.downVal = event.pageY;
	  }
	  this.currElementTop = parseInt($("#"+this.element.id).css('margin-top').replace('px',''));
	  obj.informMe("Scroll >> onTouchDown");
	},
	onTouchMove: function(event){
	  if(this.isDrag)
	  {
	    try
	    {
		this.currentDownVal = event.originalEvent.touches[0].pageY;
	    }
	    catch(e){
		this.currentDownVal = event.pageY;
	    }
	    var elementHeight = $("#"+this.element.id).height();
	    var containerHeight = $("#"+this.container.id).height();
	    //var elementTop = parseInt($("#"+this.element.id).css('margin-top').replace('px',''));
	    var elementTop = this.currElementTop;
	    var touchVal = (this.currentDownVal-this.downVal);
	    var currentVal = parseInt($("#"+this.element.id).css('margin-top').replace('px',''));
	    var gotoVal;
	    if(elementTop+touchVal <= 0 && ((elementHeight-containerHeight)*-1) <= elementTop+touchVal){
	      gotoVal = elementTop+touchVal;
	      this.fricTemp = touchVal;
	    }
	    else{
	      var fricTemp = touchVal-this.fricTemp;
	      gotoVal = (elementTop + touchVal)-(fricTemp*this.friction);
	    }
	    $("#"+this.element.id).css({'marginTop':gotoVal+'px'});
		var scrollerVal = ((-gotoVal/elementHeight)*containerHeight);
		$("#lolScrollBtn").css({'marginTop':scrollerVal+'px'});
		obj.informMe("Scroll >> onTouchMove");
	  }
	},
	onTouchUp: function(event){
	  this.isDrag = false;
	  this.refresh();
	  this.currentDownVal = 0;
	  obj.informMe("Scroll >> onTouchUp");
	},
	refresh: function(){
	  this.currElementTop = parseInt($("#"+this.element.id).css('marginTop').replace('px',''));
	  var gotoVal = null;
	  var elementHeight = $("#"+this.element.id).height();
	  var containerHeight = $("#"+this.container.id).height();
	  if(parseInt(this.currElementTop) >= 0 || elementHeight <= containerHeight){
		gotoVal = 0;
	  }
	  else if(parseInt(elementHeight+this.currElementTop) < parseInt(containerHeight) && parseInt(elementHeight)>parseInt(containerHeight)){
	    gotoVal = -parseInt(elementHeight-containerHeight);
	  }
	  if(gotoVal != null)
	  {
		this.fricTemp = 0;
		$("#"+this.element.id).animate({'marginTop':gotoVal+'px'},{duration:this.timeToScroll,queue: true,complete: function(){obj.bindTouchEvents();}});
		this.currElementTop = gotoVal;
		var scrollerVal = ((-gotoVal/elementHeight)*containerHeight);
		$("#lolScrollBtn").animate({'marginTop':scrollerVal+'px'},this.timeToScroll);
	  }
	  if(elementHeight > containerHeight){
		$("#lolScrollBar").css({'visibility':'visible'});
		$("#lolScrollBtn").css({'height':((containerHeight/elementHeight)*100)+'%'});
		$("#lolScrollBar").css({'height':containerHeight+'px'});
	  }
	  else{
	    $("#lolScrollBar").css({'visibility':'hidden'});
	    this.currElementTop = 0;
	  }
	  obj.informMe("Scroll >> Refresh");
	},
	informMe: function(msg){
	  //console.log(msg);
	}
};

Questions.js:
===============

var questionAndAnswers = {
    "questionList":{
        "question":[
                {
                    //Example
                    "questionNo":"4.1",
                    "quest":"<div class='example_question'><span style='margin-left:95px;'>The table shows a five-day forecast indicating high (H) and low (L) temperatures in Fahrenheit. Organise the temperatures in a matrix where the first and second rows represent the High and Low temperatures respectively and identify which day will be the warmest?</span><br/><br/><span><img src=\"images/Ex_4_1_1.png\"></span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><div style='margin-left:95px;'>The above information can be represented in matrix form as</div><div class='example_solution'><div class='xtraTable'><table><tr><td></td><td style='padding-top:85px; text-align:right'>$A$</td><td style='padding-top:85px;'>$=$</td><td><span style='margin-left: 80px; word-spacing: 2px; font-size:20px;'><nobr>Mon Tue <span style='margin-left:10px; word-sapcing:55px;'>Wed&nbsp;&nbsp;Thu&nbsp;&nbsp;Fri</span></nobr></span><br />${\\table H;L}(\\table 88,90,86,84,85;54,56,53,52,52)$.</td></tr><tr><td class='equals'>That is ,</td><td class='equals tblright'> $A$</td><td class='equals'>$=$</td><td>$(\\table 88,90,86,84,85;54,56,53,52,52)$</td></tr></table></div></div><div style='margin-left:95px;'>By reading through the first row (High), the warmest day is Tuesday.</div></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
                {
                     //Example
                    "questionNo":"4.2",
                    "quest":"<div class='example_question'><span style='margin-left:95px;'>The amount of fat, carbohydrate and protein in grams present in each food item respectively are as follows:<br /><br /></span><div class='xtraTable'><table><tr><td style=\"background-color:#00BAF2;\"></td><td style=\"text-align:center; background-color:#C7EAFC;\">Item 1</td><td style=\"text-align:center; background-color:#C7EAFC;\">Item 2</td><td style=\"text-align:center; background-color:#C7EAFC;\">Item 3</td><td style=\"text-align:center; background-color:#C7EAFC;\">Item 4</td></tr><tr style=\"background-color:red;\"><td style=\"text-align:left; background-color:#00BAF2; color:#FFF;\">Fat</td><td style=\"text-align:center; background-color:#C7EAFC;\">5</td><td style=\"text-align:center; background-color:#C7EAFC;\">0</td><td style=\"text-align:center; background-color:#C7EAFC;\">1</td><td style=\"text-align:center; background-color:#C7EAFC;\">10</td></tr><tr><td style=\"text-align:left; background-color:#00BAF2; color:#FFF;\">Carbohydrate</td><td style=\"text-align:center; background-color:#C7EAFC;\">0</td><td style=\"text-align:center; background-color:#C7EAFC;\">15</td><td style=\"text-align:center; background-color:#C7EAFC;\">6</td><td style=\"text-align:center; background-color:#C7EAFC;\">9</td></tr><tr><td style=\"text-align:left; background-color:#00BAF2; color:#FFF;\">Protein</td><td style=\"text-align:center; background-color:#C7EAFC;\">7</td><td style=\"text-align:center; background-color:#C7EAFC;\">1</td><td style=\"text-align:center; background-color:#C7EAFC;\">2</td><td style=\"text-align:center; background-color:#C7EAFC;\">8</td></tr></table><br /></div><div style='margin-left:95px;'>Use the information to write $3&#x000D7;4$ and $4&#x000D7;3$ matrices.</div></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><div style='margin-left:95px;'>The above information can be represented in the form of $3&#x000D7;4$ matrix as</div><br/><div style='margin-left:95px;'>$A=(\\table 5,0,1,10;0,15,6,9;7,1,2,8)$ where the columns correspond to food items. We write</div><br/><div style='margin-left:95px;'>a $4&#x000D7;3$ matrix as $B=[\\table 5,0,7;0,15,1;1,6,2;10,9,8]$ where the rows correspond to food items.</div><br/><br/></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
                {
                     //Example
                    "questionNo":"4.3",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><div style='margin-left:95px;'>Let $A=[a_{ij}]=[\\table 1,4,8;6,2,5;3,7,0;9,-2,-1].$ Find<br>(i) the order of the matrix<br/>(ii) the elements $a_{13}$ and $a_{42}$<br/>(iii) the position of the element $2$.</div></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><div class='xtraTable'><table><tr><td>(i)</td><td>Since the matrix $A$ has $4$ rows and $3$ columns, $A$ is of order $4&#x000D7;3$.</td><td></td></tr><tr><td>(ii)</td><td>The element <em>a</em><sub>13</sub> is in the first row and third column.<br/>Similarly, $a_{42}=-2$, the element in $4^\\th$ row and $2^\\nd$ column.</td><td style=\"text-align:left\"> $&#x02234;a_13=8$.</td></tr><tr><td>(iii)</td><td>The element 2 occurs in $2^\\nd$ row and $2^\\nd$ column</td><td>$&#x02234;a_22=2$.</td></tr></table></div></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
                {
                     //Example
                    "questionNo":"4.4",
                    "quest":"<div class='example_question'><span style='margin-left:95px;'>Construct a 2$&#x00D7;$3 matrix $A$ = [$a_{ij}$] whose elements are given by $a_{ij} = |2i - 3j |$ </span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style='margin-left:20px;'>In general $a$ $2&#x00D7;3$ matrix is given by</span><br/><span style='margin-left:215px;'>$A={\\table}(\\table a_11,a_12,a_13;a_21,a_22,a_23)$<span style='margin-left:95px;'><br/>Now, $a_{ij} = |2i - 3j|$ where $i = 1,2$ and $j = 1,2,3$<br /><div class='xtraTable'><table><tr><td>$a_11 = |2(1) - 3(1)| = |-1| = 1,$</td> <td>$a_12 = |2(1) - 3(2)| = 4,$</td> <td>$a_13=|2(1) - 3(3)| = 7$</td></tr><tr><td>$a_21 = |2(2) - 3| = 1,$</td><td>$a_22 = |2(2) - 3(2)| = 2,$</td><td>$a_23 = |2(2) - 9| = 5$</td></tr></table></div><br/>Hence the required matrix $A=(\\table 1,4,7;1,2,5)$</div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
                {
                     //Example
                    "questionNo":"4.5",
                    "quest":"<div class='example_question'><div style='margin-left:95px;'>If $A={\\table}(\\table 8,5,2;1,-3,4)$, then find $A^T$ and $(A^T)^T$</div></div>",
                    "questionType":"example",
                    "exampleSolution":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_solution'><div style='margin-left:95px;'>$A={\\table}(\\table 8,5,2;1,-3,4)$<br />The transpose $A^T$ of a matrix $A$, is obtained by interchanging rows and columns of the matrix $A$.<br />Thus, $A^T={\\table}(\\table 8,1;5,-3;2,4)$ <br />Similarly $(A^T)^T$ is obtained by interchanging rows and columns of the matrix $A^T$.<br />Hence, $(A^T)^T$ = ${\\table}(\\table 8,5,2;1,-3,4)$</div></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
                {
                     //Example
                    "questionNo":"4.6",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>Find the values of $x$, $y$ and $z$ if $(\\table x,5,4;5,9,1)$ $=$ $(\\table 3,5,z;5,y,1)$</span></div></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:35px;\">As the given matrices are equal, their corresponding elements must be equal. Comparing the corresponding elements, we get $x$ = 3, $y$ = 9 and $z$ = 4.</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
                {
                    //Example
                    "questionNo":"4.7",
                    "quest":"<div class='example_question'><div style='margin-left:95px;'>Solve : ${\\table}(\\table y;3x)={\\table}(\\table 6-2x;31+4y)$</div></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style='margin-left:30px;'>Since the matrices are equal, the corresponding elements are equal.</span><br /><br /><span style='margin-left:30px;'>Comparing the corresponding elements, we get $y = 6-2x$ and $3x = 31 + 4y.$</span><br /><br /><div class='xtraTable'><table style='margin-left:0'><tr><td class='tblright'>Using $y = 6-2x$ in the other equation, we get $3x$</td><td>$=$</td> <td>$31 + 4(6-2x)$</td></tr><tr><td class=\"tblright\">$3x$</td><td>$=$</td><td>$31+24-8x$</td></tr></table></div><br /><span style='margin-left:195px;'>$&#8756;$ $x = 5$ and hence $y = 6-2(5)= -4.$</span><br/><span style='margin-left:195px;'>Thus, $x=5$ and $y = -4.$</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.8",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>If $A$ $=$ $(\\table -1,2,4;3,6,-5)$ then find $3A$</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:85px;\">The matrix $3A$ is obtained by multiplying every element of $A$ by 3.</span><br/><span style=\"margin-left:95px;\">$3A = 3 (\\table -1,2,4;3,6,-5)$ $=(\\table 3(-1),3(2),3(4);3(3),3(6),3(-5))$ $=(\\table -3,6,12;9,18,-15)$</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.9",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>Let $A = (\\table 8,3,2;5,9,1)$ and $B = (\\table 1,-1;3,0)$. Find $A+B$ if it exists.</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:85px;\">Since $A$ is order of 2&#x00D7;3 and $B$ is of order 2&#x00D7;2, addition of matrices $A$ and $B$ is not possible.</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.10",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>If $A =(\\table 5,6,-2,3;1,0,4,2)$ and $B =(\\table 3,-1,4,7;2,8,2,3)$, then find $A+B$.</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'></br/><span style=\"margin-left:85px;\">Since $A$ and $B$ are of the same order 2&#x00D7;4, addition of $A$ and $B$ is defined.</span></div><div class='example_solution'><div class='xtraTable'><table><tr><td class=\"equals\">So,</td><td class=\"equals\">$A + B$</td><td class=\"equals\">$=$</td><td>$(\\table 5,6,-2,3;1,0,4,2)+(\\table 3,-1,4,7;2,8,2,3)$</td></tr><tr><td></td><td></td><td class=\"equals\">$=$</td><td>$(\\table 5+3,6-1,-2+4,3+7;1+2,0+8,4+2,2+3)$</td></tr><tr><td class=\"equals\">Thus,</td><td class=\"equals\">$A + B$</td><td class=\"equals\">$=$</td><td>$(\\table 8,5,2,10;3,8,6,5)$</td></tr></table></div></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.11",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:85px;'>Matrix $A$ shows the weight of four boys and four girls in kg at the beginning of a diet programme to lose weight. Matrix $B$ shows the corresponding weights after the diet programme.</span><br/><span style=\"margin-left:85px;\">$A = (\\table 35,40,28,45;42,38,41,30)\\table \\Boys;\\Girls$, $B=(\\table 32,35,27, 41;40,30,34,27)\\table \\Boys;\\Girls$</span><br/><span style=\"margin-left:85px;\">Find the weight loss of the Boys and Girls.</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'></div><div class='example_solution'><div class='xtraTable'><table><tr><td>Weight loss matrix</td><td class=\"equals\">$A - B$</td><td class=\"equals\">$=$</td><td>$(\\table 35,40,28,45;42,38,41,30)-(\\table 32,35,27,41;40,30,34,27)$</td></tr><tr><td></td><td></td><td class=\"equals\">$=$</td><td>$(\\table 3,5,1,4;2,8,7,3).$</td></tr></table></div></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.12",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>Determine whether each matrix product is defined or not. If the product is defined, state the dimension of the product matrix.</span></div><div class='example_question'><div class='xtraTable'><table><tr><td>(i) $A_{2 &#x00D7; 5}$ and $B_{5 &#x00D7; 4}$ </td><td>(ii) $A_{1 &#x00D7; 3}$ and $B_{4 &#x00D7; 3}$ </td></tr></table></div></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:5px;\">(i) &nbsp;&nbsp;&nbsp;&nbsp;Now, the number of columns in $A$ and the number of rows in $B$ are equal.</span></br><br/><span style=\"margin-left:165px;\">So, the product $AB$ is defined.</span></br></br><span style=\"margin-left:165px;\">Also, the product matrix $AB$ is of order 2&#x00D7;4.</span><br/></br><span style=\"margin-left:5px;\">(ii) &nbsp;&nbsp;&nbsp;&nbsp;Given that $A$ is of order 1&#x00D7;3 and $B$ is of order 4&#x00D7;3</span><br/></br><span style=\"margin-left:165px;\">Now, the number of columns in $A$ and the number of rows in $B$ are not equal.</span></br></br><span style=\"margin-left:165px;\">So, the matrix product $AB$ is not defined.</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.13",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:85px;'>Solve $(\\table 3,2;4,5)$ $(\\table x;y)$ $=$ $(\\table 8;13)$</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:85px;\">Given that  $(\\table 3,2;4,5)$ $(\\table x;y)$ $=$ $(\\table 8;13)$</span><br/><span style=\"margin-left:125px;\">&#x021D2; <span style=\"margin-left:100px;\">$(\\table 3x+2y;4x+5y)$</span>&nbsp;&nbsp;&nbsp; $=$ $(\\table 8;13)$</span></br><span style=\"margin-left:85px;\">Equating the corresponding elements, we get</span></div></br><div class='example_solution'><div class='xtraTable'><table><tr><td></td><td></td><td style=\"text-align:right;\">$3x+2y=8$</td><td>and</td><td style=\"text-align:right;\">$4x+5y=13$</td></tr><tr><td style=\"text-align:right;\">&#x021D2;</td><td></td><td style=\"text-align:right;\">$3x+2y-8=0$</td><td>and</td><td style=\"text-align:right;\">$4x+5y-13=0.$</td></tr></table><div></div></br><div class='example_solution'><span style=\"margin-left:85px;\">Solving the equations by the method of cross multiplication, we get</span><br/></div><div class='example_solution'><div class='xtraTable'><table style='width: 50%;'><tr><td></td><td>x</td><td></td><td>y</td><td></td><td>1</td><td></td></tr><tr><td>$2$</td><td></td><td>$-8$</td><td></td><td>$3$</td><td></td><td>$2$</td></tr><tr><td>5</td><td></td><td>$-13$</td><td></td><td>$4$</td><td></td><td>$5$</td></tr></table></div></div><br/><div class='example_solution'><span style=\"margin-left:85px;\">&#x021D2; ${x} /{-26+40}$ $=$ ${y} /{-32+39}$ $=$ ${1} /{15-8}$ </span><span style=\"margin-left:50px;\"> &#x021D2; ${x} /{14}$ $=$ ${y} /{7}$ $=$ ${1} /{7}$  </span><br/><br/><span style=\"margin-left:120px;\">Thus, $x=2, y=1$</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.14",
                    "quest":"<style>tr td.fm-mtd{text-align:center;}</style><div class='example_question'><span style='margin-left:95px;'>If $A =(\\table a,b;c,d)$ and $I_2=(\\table 1,0;0,1)$, then show that $A^2-(a+d)A=(bc-ad)I_2$.</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><div class='xtraTable'><table><tr><td>Consider $A^2$ </td><td>$=$</td> <td>$A&#x00D7;A$</td><td></td></tr><tr><td></td><td class=\"Ex_2_14_equals\">$=$</td> <td>$(\\table a,b;c,d)$$(\\table a,b;c,d)$ $=$ $(\\table a^2+bc,ab+bd;ac+cd,bc+d^2)$</td><td class=\"blueText Ex_2_14_equals\">$(1)$</td></tr><tr><td class=\"Ex_2_14_equals\">Now, $(a+d)A$</td> <td class=\"Ex_2_14_equals\">$=$</td> <td>$(a+d)(\\table a,b;c,d)$</td><td></td></tr> <tr><td></td><td class=\"Ex_2_14_equals\">$=$</td><td> $(\\table a^2+ad,ab+bd;ac+cd,ad+d^2)$</td> <td class=\"blueText\">$(2)$</td></tr> <tr><td colspan=\"4\">From <span class=\"blueText\">$(1)$</span> and <span class=\"blueText Ex_2_14_equals\">$(2)$</span> we get,</td> </tr> <tr><td>$A^2 -(a+d)A$</td> <td class=\"Ex_2_14_equals\">$=$</td> <td>$(\\table a^2+bc,ab+bd;ac+cd,bc+d^2)-(\\table a^2+ad,ab+bd;ac+cd,ad+d^2)$</td><td></td> </tr> <tr><td></td> <td class=\"Ex_2_14_equals\">$=$</td> <td>$(\\table bc-ad,0;0,bc-ad)=(bc-ad)(\\table 1,0;0,1)$</td> <td></td></tr>  <tr><td>Thus, $A^2-(a+d)A$</td><td>$=$</td><td>$(bc-ad)I_2$.</td><td></td></tr> </table></div></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.15",
                    "quest":"<style>tr td.fm-mtd{text-align: center;}</style><div class='example_question'><span style='margin-left:95px;'>If $A =(\\table 8,-7;-2,4;0,3)$ and $B=(\\table 9,-3,2;6,-1,-5)$, then find $AB$ and $BA$ if they exist.</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:85px;\">The matrix $A$ is of order $3&#x00D7;2$ and $B$ is of order $2&#x00D7;3$. Thus, both the products $AB$ and $BA$ are defined. </span><div class='xtraTable'><table><td class=\"Ex_2_15_equals\">Now, $AB$</td> <td class=\"Ex_2_15_equals\">$=$</td> <td>$(\\table 8,-7;-2,4;0,3)$ $(\\table 9,-3,2;6,-1,-5)$ </td><td></td> </tr> <tr><td></td><td class=\"Ex_2_15_equals\">$=$</td> <td>$(\\table 72-42,-24+7,16+35;-18+24,6-4,-4-20;0+18,0-3,0-15) = (\\table 30,-17,51;6,2,-24;18,-3,-15)$</td><td></td> </tr> <tr><td colspan=\"4\"> Similarly,</td></tr> <tr><td  class=\"Ex_2_15_equals\">$BA$</td> <td class=\"Ex_2_15_equals\"> $=$</td> <td> $(\\table 9,-3,2;6,-1,-5)$ $(\\table 8,-7;-2,4;0,3)$ $=$ $(\\table 78,-69;50,-61;).$ </td> <td>(Note that $AB &#x2260; BA$)</td></tr> </table><div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"<div class=\"remarksbox\"><div class=\"remarkstitle\">Remarks</div><div class=\"remarkscontent\">Multiplication of two diagonal matrices of same order is commutative. Also, under matrix multiplication unit matrix commutes with any square matrix of same order.</div>", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.16",
                    "quest":"<style>tr td.fm-mtd{text-align: center;}</style><div class='example_question'><span style='margin-left:95px;'>If $A = (\\table 3,2; -1,4),\\ B =(\\table -2,5; 6,7)$ and $C =(\\table 1,1; -5,3)$ verify that $A(B + C) = AB + AC$ </span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><div class='xtraTable'><table><tr><td class=\"Ex_2_16_equals\">Now, $B+C$</td> <td class=\"Ex_2_16_equals\">$=$ </td> <td>$(\\table -2,5; 6,7)+(\\table 1,1; -5,3)$ $=$ $(\\table -1,6; 1,10)$</td><td></td></tr> <tr><td class=\"Ex_2_16_equals\">Thus, $A(B+C)$</td> <td class=\"Ex_2_16_equals\">$=$</td>  <td>$(\\table 3,2; -1,4)$ $(\\table -1,6; 1,10)$ $=$ $(\\table -1,38; 5,34)$ </td> <td class=\"blueText Ex_2_16_equals\">$(1)$</td></tr> <tr><td class=\"Ex_2_16_equals\">Now, $AB+AC$</td> <td class=\"Ex_2_16_equals\">$=$</td> <td>$(\\table 3,2; -1,4)$ $(\\table -2,5; 6,7)$ $+$ $(\\table 3,2; -1,4)$ $(\\table 1,1; -5,3)$</td><td></td></tr> <tr><td></td> <td class=\"Ex_2_16_equals\">$=$</td> <td> $(\\table -6+12,15+14; 2+24,-5+28)$  $+$  $(\\table 3-10,3+6; -1-20,-1+12)$</td> <td></td></tr> <tr><td></td><td class=\"Ex_2_16_equals\"> $=$</td><td> $(\\table 6,29; 26,23)$  $+$  $(\\table -7,9; -21,11)$</td><td></td></tr> <tr><td></td> <td class=\"Ex_2_16_equals\">$=$</td>  <td>$(\\table -1,38; 5,34)$</td> <td class=\"blueText Ex_2_16_equals\"> $(2)$</td></tr><tr><td colspan=\"4\">From <span class=\"blueText\">$(1)$</span> and <span class=\"blueText \">$(2)$</span>, we have $A(B + C) = AB + AC$.</td></tr></table><div></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.17",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>If $A$ $=$ $(\\table 1,3; 9,-6)$, then verify $AI = IA = A,$ where I is the unit matrix of order 2.</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:95px;\">Now, $AI$ $=$ $(\\table 1,3; 9,-6)$ $(\\table 1,0; 0,1)$ $=$ $(\\table 1+0,0+3; 9+0,0-6)$ $=$ $(\\table 1,3; 9,-6)$ $=$ $A$<br/></span><span style=\"margin-left:95px;\">Also, $IA$ $=$  $(\\table 1,0; 0,1)$ $(\\table 1,3; 9,-6)$  $=$ $(\\table 1+0,3+0; 0+9,0-6)$ $=$ $(\\table 1,3; 9,-6)$ $=$ $A$<br/> </span><span style=\"margin-left:85px;\">Hence $AI = IA = A$.</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.18",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>Prove that $(\\table 3,5; 1,2)$ and $(\\table 2,-5; -1,3)$ are multiplicative inverses to each other.</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'></div><div class='xtraTable'><table><tr><td>Now, $(\\table 3,5; 1,2)$ $(\\table 2,-5; -1,3)$</td><td class='equals'> $=$</td> <td>$(\\table 6-5,-15+15; 2-2,-5+6)$</td> <td class='equals'>$=$</td> <td>$(\\table 1,0; 0,1)$</td><td class='equals'> $=$</td> <td class='equals'>$I$</td></tr><tr><td>Also, $(\\table 2,-5; -1,3)$ $(\\table 3,5; 1,2)$</td> <td class='equals'>$=$</td> <td>$(\\table 6-5,10-10; -3+3,-5+6)$</td><td class='equals'> $=$</td> <td>$(\\table 1,0; 0,1)$</td> <td class='equals'>$=$</td> <td class='equals'>$I$</td></tr></table></div><span style=\"margin-left:25px;\">&#x2234; The given matrices are inverses to each other under matrix multiplication.</span>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                },
		{
                    //Example
                    "questionNo":"4.19",
                    "quest":"<style>tr td.fm-mtd{text-align: right;}</style><div class='example_question'><span style='margin-left:95px;'>If $A$ $=$ $(\\table -2;4;5)$ and $B$ = $(\\table 1,3,-6;)$, then verify that $(AB)^T $=$ B^T A^T.$</span></div>",
                    "questionType":"example",
                    "exampleSolution":"<div class='example_solution'><span style=\"margin-left:85px;\"><div class='xtraTable'><table><tr><td>Now, $AB$</td><td>$=(\\table -2;4;5)$ $(\\table 1,3,-6;)$</td><td>$=(\\table -2,-6,12; 4,12,-24;5,15,-30)$</td> <td></td><td></td></tr> <tr><td>Thus, $(AB)^T$</td><td>$=(\\table -2,4,5; -6,12,15;12,-24,-30)$</td><td> </td> <td></td> <td style=\"color:#46D2FB;\">$(1)$</td></tr> <tr><td>Now, $B^T A^T$</td><td> $=(\\table 1;3;-6;)$ $(\\table -2,4,5)$</td> <td>$=(\\table -2,4,5; -6,12,15;12,-24,-30)$</td><td></td> <td style=\"color:#46D2FB;\">$(2)$</td></tr> </table></div></span></br><span style=\"margin-left:85px;\">From <span style=\"color:#46D2FB;\">(1)</span> and <span style='color:#46D2FB; margin-top:50px;'>(2)</span>, we get $(AB)^T =B^TA^T.$</span></div>", //Solution of the example
                    "options":[], //Leave this blank
                    "correctAnswer":"0",
                    "reviewComment":"", //Leave this blank
                }
            ]
    }
};


script.js:
==========
var myScroll;
var myQuest;
var clickAudio = new Audio();
var timeAudio = new Audio();
clickAudio.src = "audio/buttonclick.mp3";
timeAudio.src = "audio/timebeep.mp3";
clickAudio.load();
timeAudio.load();
var isTouchDevice;
$(document).ready(function(){
	myQuest = new lolQuest("MMV_Geometry1","contentHolder", "prevBtn", "nextBtn", questionAndAnswers, "timerText", "currentQuestionDisp","navBarSlider", "subNavbar", "flag","navUnitScroller", "coverDiv", "homeBtn", "tocBtn", "submitBtn");
	isTouchDevice = 'ontouchstart' in document.documentElement;
	if(isTouchDevice){
		//document.addEventListener("touchmove", preventBehavior, false);
		$(".popupBtns").bind("touchstart", onPopupBtnsDown);
        $(".review_whbold").bind("touchstart", onPopupBtnsDown);
		$("#homeBtn").bind("touchstart", onHomeBtnClick);
		$("body").bind("touchend", onAllTouchUp);
		$("#resume").bind("touchend", resumeQuest);
		$("#submit").bind("touchend", onSubmit);
		$("#submitNo").bind("touchend", resumeQuest);
		$("#submitYes").bind("touchend", showResultPage);
		$("#quit").bind("touchend", quitApp);
		$("#reviewBtn").bind("touchend", reviewQuest);
	}
	else{
		//document.addEventListener("mousedown", preventBehavior, false);
		$(".popupBtns").bind("mousedown", onPopupBtnsDown);
		$(".review_whbold").bind("mousedown", onPopupBtnsDown);    
		$("#homeBtn").bind("mousedown", onHomeBtnClick);
		$("body").bind("mouseup", onAllTouchUp);
		$("#resume").bind("mouseup", resumeQuest);
		$("#submit").bind("mouseup", onSubmit);
		$("#submitNo").bind("mouseup", resumeQuest);
		$("#submitYes").bind("mouseup", showResultPage);
		$("#quit").bind("mouseup", quitApp);
		$("#reviewBtn").bind("mouseup", reviewQuest);
	}
	resizeContentHolder();
	setTimeout(function(){resizeContentHolder();},100);
	$("#tempJumpTo").keyup(function(event){
		if(event.keyCode == 13){
			var page;
			try{page = parseInt(document.getElementById("tempJumpTo").value);}
			catch(e){page = 1;}
			if(!page){page = 1;}
			myQuest.gotoQuestion(page);
		}
	});
	myQuest.onPageLoadComplete = function(){
		resizeContentHolder();
		//myScroll = new lolScroll("content");
		myScroll = new iScroll('content', { zoom:true, onBeforeScrollStart:myQuest.OnScrollStart });
		setTimeout(function(){
			if(myScroll) myScroll.refresh();
		}, 100);
	}
});
function jumpToUrl(url){
	window.location.href = url;
}
function onPopupBtnsDown(e){
	var btn = null;
	if(!isTouchDevice){btn = e.target;}
	else{btn = e.originalEvent.touches[0].target;}
	if(btn.classList.toString().indexOf("popupBtn") >=0 || btn.classList.toString().indexOf("review_whbold") >= 0){}else{
		btn = btn.parentNode;
	}
	if(btn){
		btn.style.color = "#14b5eb";
	}
	playClickAudio();
}
function deviceTilted(){
    if(myQuest.currentPage == "coverPage"){myQuest.loadCoverAni();}
	resizeContentHolder();
}
function onPageResize(){
	resizeContentHolder();
	if($(window).width() > 850){
	$(".optionTable").css({"display":"table-cell"});
	}
	else{
		$(".optionTable").css({"display":"inline-block"});
	}
}
function resizeContentHolder(){
	var adj = 1;
	var hH = $("#header").height();
	var fH = $("#footer").height();
	var wH = $(window).height();
	var cHH = wH-(hH+fH)-adj;
	$("#contentHolder").css({'height':cHH+'px','top':hH+'px'});
	$("#content").css({'height':cHH+'px'});
	$("#navUnitScroller").css({'bottom':(fH+adj)+'px'});
	if(!myScroll) myScroll = new iScroll('content', { zoom:true, onBeforeScrollStart:myQuest.OnScrollStart });
	try{myScroll.refresh();}catch(e){}
	setTimeout(function(){
		if(myScroll) myScroll.refresh();
	}, 100)
	try{$(".review_whbold").unbind("touchstart");}catch(e){}
	$(".review_whbold").bind("touchstart", onPopupBtnsDown);
}
function preventBehavior(e) {
	e.preventDefault();
}
function onHomeBtnClick(){
	playClickAudio();
	quitApp();
}
function onAllTouchUp(){
	
}
function resumeQuest(){
	hideAll();
	myQuest.setTimerState("running");
}
function showResultPage(){
	hideAll();
	myQuest.displayResult();
	
	/*document.getElementById("review_page").style.display="block";
	document.getElementById("quitBtn2").style.display="block";*/
}
function onSubmit(){
	hideAll();
	$("#submitScreen").css({"visibility" : "visible"});
}
function hideQuest(){
	$("#contentHolder").hide();
	$("#questionStatus").hide();
	$("#prevBtn").hide();
	$("#nextBtn").hide();
	$("#homeBtn").hide();
	$("#timerText").hide();
	$("#navUnitScroller").hide();
	myQuest.setTimerState("pause");
}
function reviewQuest(){
	$("review_page").hide();
	resumeQuest();
	myQuest.activateReviewMode();
}
function hideAll(){
	$("#coverDiv").hide();
	$("#submitScreen").css({"visibility" : "hidden"});
}
function quitApp(){
	hideAll();
	myQuest.byLoadPage('homePage');
}
