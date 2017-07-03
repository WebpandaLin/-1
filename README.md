# -1
基于JQ的轮播
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
    <title>Carusel</title>
		<script type="text/javascript" src="js/jquery-3.1.1.min.js"></script>
    <style>
    
h1{
	text-align: center;
	margin-bottom: 20px;
	margin-top:0;
}
a{
	text-decoration:none;
	color: white;
}
.active{
	background: rgba(255,255,255,0.6);
	border-radius: 15px;
	color: aquamarine;
	font-weight: bold;
}

.container{
	margin: 0 auto;
	width: 1024px;
}
.carousel{
	height: 582px;
	position: relative;
	overflow: hidden;
	width: 1024px;
}
.window{
	overflow: hidden;
	width: 1024px;
}
.image-group{
	position: absolute;
}
.image-group img{
	float: left;
}
.paging{
	position: absolute;
	right: 30px;
	bottom: 15px;
	display: none;
}
.paging a{
	padding: 2px 8px;
}
.paging a:hover{
	font-weight:bold;
	color: aquamarine;
}

    </style>
	</head>
	<body>
		<div class="container">
			<h1>Carousel</h1>
			<div class="carousel">
			  <div class="window">
				<div class="image-group">
					<a href="#"><img src="images/2.jpg" alt="star1"></a>
					<a href="#"><img src="images/1.jpg" alt="star2"></a>
					<a href="#"><img src="images/3.jpg" alt="star3"></a>
				</div>
			  </div>
			  <div class="paging">
			  	<a href="javascript:0" rel="1">1</a>
			  	<a href="javascript:0" rel="2">2</a>
			  	<a href="javascript:0" rel="3">3</a>
			  </div>
			</div>
		</div>
		<script type="text/javascript">
			$('.paging').show();
			$('.paging a:first').addClass("active");
			//显示指示器
			rotate = function(){
				var taggle_ID = $active.attr("rel")-1;
				var img_realposition = img_width*taggle_ID;
				$('.paging a').removeClass("active");
				$active.addClass('active');
				$('.image-group').animate({
					left: -img_realposition
				},500);
			}
			//移动动画
			var img_width = $('.image-group').find("img").width();
			var img_sum = $('.image-group').find('img').length;
			$(".image-group").width(img_width*img_sum);
			//设置window的宽；
			rotateWhich = function(){
				play = setInterval(function(){
					$active = $('.paging a.active').next();
					if($active.length === 0)
					{
						$active = $('.paging a:first');
					}
					rotate();
					},2000);
				};
				rotateWhich();
				//获取下一张图片的函数
				$(".paging a").click(function(){
					$(this).addClass("active");
					$(".paging a").not($(this)).removeClass("active");
					$active = $(this);
					clearInterval(play);
					rotate();
					rotateWhich();
			})
			//提示器点击事件；
			$('.image-group a').hover(function()
			{
				clearInterval(play);},function()
				{
				rotateWhich();
			});
		</script>
	</body>
</html>
