```javascript
//모든 엘리먼트를 획득
$("*")

//현재 HTML 엘리먼트를 획득
$(this)

//모든 <p>엘리먼트에 class가 intro인것을 획득
$("p.intro") 

//첫번쨰 <p>엘리먼트를 획득
$("p:first") 

//첫번쨰 <ul>엘리먼트의 첫번쨰 <li>를 획득
$("ul li:first") 

//모든 <ul>엘리먼트의 첫번째 <li>를 획득
$("ul li:first-child") 

//모든 <a>태그를 선택하여 target속성값이 
$("a[target='_blank']") _blank인것 획득

//모든 <a>태그를 선택하여 target속성값이 
$("a[target!='_blank']") _blank아닌것 획득

//모든 버튼 선택
$(":button") 

//특정 opacity값으로 
$(selector).fadeTo(speed, opacity, callback) fading을 허용

//선택된 엘리먼트와 그것의 자식 엘리먼트를 제거
remove() 

//선택된 엘리먼트의 자식 엘리먼트를 제거
empty() 

//바로 상위의 부모 엘리먼트를 선택
parent() 

//자신보다 상위의 모든 엘리먼트를 선택
parents() 

//<div>엘리먼트내의 모든 <span>을 선택
$("div").find("span") 

//<h2>엘리먼트가 있는곳의 형제 엘리먼트를 모두 선택
$("h2").siblings() 

//<h2>엘리먼트가 있는곳의 형제 엘리먼트 <p>를 모두 선택
$("h2").siblings("p") 

//<h2>엘리먼트의 다음을 선택
$("h2").next() 

//<h2>엘리먼트의 다음 모든것을 선택
$("h2").nextAll() 

//<h2>엘리먼트와 <h6>엘리먼트 사이의 모든 엘리먼트를 
$("h2").nextUntil("h6") 선택

//첫번째 <p>엘리먼트를 선택
$("p").eq(1) 

//두번째 <span>엘리먼트를 선택
$("span:eq(2)")

//<p>태그중 class가 intro가 아닌것 선택
$("p").not(".intro") 

//<ul>엘리먼트의 class가 topnav인것을 획득하여 그 하위 엘리먼트가 li인것을 선택
$("ul.topnav > li") 

//<form>엘리먼트 하위의 <fieldest>엘리먼트 하위의 <input>엘리먼트에 배경을 yellow로 설정
$("form fieldest input").css("backgroundColor", "yellow")

//형제지간인 label엘리먼트와 input엘리먼트를 선택하여 color값을 blue로 설정
$("label + input").css("color", "blue").val("Labeled!")

//같은 부모밑에있는 엘리먼트 중에서, 아이디가 prev보다 뒤에 있는 모든 div에 대해서 color를 blue로 설정
("#prev ~ div").css("color", "blue")

//animateIt함수를 실행하고, mover라는 아이디의 div를 슬라이딩 토글한다. animateIt을 콜백으로 호출하여 반복되도록 처리한다.
function animateIt(){
	$("#mover").slideToggle("slow", animateIt);
}
animateIt();

//table에서 td의 인덱스는 순서대로 0부터 시작하므로.... td의 인덱스가 2인것을 선택하여 color를 red로 변경 설정
$("td:eq(2)").css("color", "red")

//table의 row에서 index가 0, 2, 4.... 인것을 획득
$("t:evenr")

//첫번쨰 table row 획득
$("tr:first")

//테이블의 td인덱스가 4보다 큰것 모두 선택
$("td:gt(4)")

//모든 <h1>.... 엘리먼트 선택
$(":header")

//<div>엘리먼트에 lang의 값이 ts인것을 획득
$("div:lang(ts)")

//<tr>엘리먼트의 마지막 로우 획득
$("tr:lat")

//td의 인덱스가 4보다 작은것 모두 획득
$("td:lt(4)")

//checked박스에 checked="checked"가 아니라면 span의 background 컬러를 yellow로 설정
$("input:not(:checked) + span").css("background-color", "yellow")
<div><input type="checkbox"><span>Mary</span></div>
<div><input type="checkbox" checked="checked"><span>Peter</span></div>

//<table>의 row에서 index가 1, 3, 5.... 인것을 획득
$("tr:odd")

//<div>의 텍스트값에 'John' 이 있는것을 획득하여 밑줄 설정
$("div:contains('John')").css("text-decoration", "underline")

//<td>의 text값이 비어있는것만을 획득
$("td:empty")

//엘리먼트 <div>하위의 <p>엘리먼트가 있다면 획득
$("div:has(p)")

//<a>엘리먼트의 greflang의 값에 문자로 연결되지 않은 en값이 있다면 획득 -> 첫번쨰, 두번쨰 획득
JS
$( "a[hreflang|='en']" )
HTML
<a href="example.html" hreflang="en">Some text</a>
<a href="example.html" hreflang="en-UK">Some other text</a>
<a href="example.html" hreflang="english">will not be outlined</a>

//<input>엘리먼트의 name의 값에 man이 포함되어 있다면 획득 -> 첫번쨰, 두번쨰, 세번쨰 획득
JS
$( "input[name*='man']" )

<input name="man-news">
<input name="milkman">
<input name="letterman2">
<input name="newmilk">

//<input>엘리먼트의 name의 값이 'man'이라는 단일 텍스트가 있다면 획득 -> 두번쨰 획득
JS
$( "input[name~='man']" )
HTML
<input name="man-news">
<input name="milk man">
<input name="letterman2">
<input name="newmilk">

//<input>엘리먼트의 name의 값이 'letter'로 끝나는것 획득
JS
$( "input[name$='letter']" ).val( "a letter" );
HTML
<input name="newsletter">
<input name="milkman">
<input name="jobletter">

//value값이 'Hot Fuzz'인것중 <input>엘리먼트를 획득
$("input[value='Hot Fuzz']")

//value값이 newsletter이 아닌것중 <input>엘리먼트를 획득
$("input[name != 'newsletter]'")

//name의 값이 news로 시작하는 <input>엘리먼트를 획득
$("input[name^='news']")

//id속성을 가지고 있는 <input>엘리먼트에 name의 속성값 끝나는 부분이 man인것 획득
$("input[id][name$='man']")

//div하위에 span엘리먼트가 여러개 있을 경우, div엘리먼트의 하위 span엘리먼트의 첫번째 획득. 그리고 그곳에 마우스 오버시 이벤트를 준다. 마우스 오버와 떠날때의 이벤트를 정의
$( "div span:first-child" ).hover(function() {
	alert("mouse over");
}, function() {
	alert("mouse leave");
});

//모든 <div>안에서 첫번째로 나오는 <span>을 획득
$( "span:first-of-type" )

//모든 div안에서 마지막에만 있는 <span>을 획득 -> 즉 마지막 엘리먼트가 <span>이 아니라면 획득 못함
$("div span:last-child")

//엘리먼트 하위의 마지막 <span>을 획득 -> 마지막 엘리먼트가 있기만 하면 획득
$("span:last-of-type")

//ul하위의 두번쨰 li 획득
$("ul li:nth-child(2)")

//ul하위의 마지막에서 두번째 li획득
$("ul li:nth-last-child(2)")

//ul하위의 마지막에서 두번쨰 li획득
$( "ul li:nth-last-of-type(2)")

//div하위에 오직 하나의 버튼이 있는것 획득
$( "div button:only-child" )

//check박스 체크시 countChecked함수 호출하여 체크된 체크박스 길이값 구함
var countChecked = function() {
  	var n = $( "input:checked" ).length;
	alert(n + "are checked");
}; 
$( "input[type=checkbox]" ).on( "click", countChecked );

//disabled된 모든 <input>엘리먼트를 획득
$( "input:disabled")

//enabled된 모든 <input>엘리먼트를 획득
$("input:enabled")

//<p>엘리먼트에 지정된 각 클래스명을 비교해서 하나라도 일치하는 클래스를 찾으면 true 반환
$("p").hasClass("bar")

//해당하는 엘리먼트에 highlight클래스를 추가 제거를 반복
$(this).toggleClass("highlight")

//<p>엘리먼트를 절대좌표 기준으로 위에서 400px에 해당하는 좌표로 이동
$("p").offset({top : 400});

//<p>엘리먼트를 절대좌표 기준으로 위에서 100px 그리고 좌측에서 200px 해당하는 좌표로 이동
$("p").offset({top : 100, left : 200});

//부모요소의 상단값을 기준으로 <p>엘리먼트 요소가 위치한 상대적 거리값
$("p").position().top

//부모의 좌표를 획득
$("li").offsetParent()

//왼쪽에서 스크롤 된 위치 값을 얻거나, 스크롤 위치를 초기에 설정
$("p").scrollLeft();
$("demo").scrollLeft(100);

//상단에서 스크롤 된 위치 값을 얻거나, 스크롤 위치를 초기에 설정 
$("p").scrollTop();
$("demo").scrollTop(100);

//jQuery:data를 이용하여 엘리먼트에 데이타 저장 및 읽기 -> 코드가 간결해짐
<html>  
    <head>
    <meta http-equiv="Context-Type" context="text/html;charset=UTF-8" />

    <script type="text/javascript">
        //span 엘리먼트에 data()함수로 "name"과 "address"세팅방법
        $("span").data("name", "Nextree");
        $("span").data("address", "가산");

        //데이타 읽기 (span의 name과 address 키로 되어 있는 데이타를 획득)
        var name = $("span").data("name");
        var address = $("span").data("address");
    </script>
    </head>

    <body>
    <!-- data()가 호출되면 span엘리먼트에 "name"과 "address"가 추가됩니다.-->
    <span>jQuery의 data()의 저장 방법</span>
    </body>
</html>  

//<p>엘리먼트를 모두 복사하여 body에 붙임
$("p").clone().appendTo("body");

//선택한 <p>엘리먼트에대해서 각각<div>로 감싸거나 제거
$("p").wrap('<div></div>');
$("p").unwrap();

//선택한 <p>엘리먼트에대해서 모두<div>로 감싸기
$( "p" ).wrapAll( "<div></div>" );

//<p>엘리먼트 내부에서 <div>로 감싸기
$( "p" ).wrapInner( "<div></div>");

//append와 반대로 보면 됨. .inner클래스에 <p>Test</p>가 추가
//만약 .inner이 복수개의 클래스라면 처음에는 이동되고 그 다음부터는 복사되며 추가된다.
//이걸 어디에 쓰지?
$('<p>Test</p>').appendTo('.inner');

//appendTo와 똑같지만 맨 앞에 추가된다라고 생각하면 되지 않을까?
$('<p>Test</p>').prependTo('.inner');

//.inner클래스를 가진 <div>요소 뒤에 새로운 내용의 <p>Test</p>가 추가
$('.inner').after('<p>Test</p>');

//.inner클래스를 가진 <div>요소 앞에 새로운 내용의 <p>Test</p>가 추가
$('.inner').before('<p>Test</p>');

//.after()와 .insertAfter() 함수는 동일한 기능을 한다. 중요한 차이점은 내용과 대상의 위치 차이
//A.after(B)라면 A뒤에 B를 추가, A.insertAfter(B)는 B뒤에 A를 추가
$('.inner').insertAfter('<p>Test</p>')

//insertAfter가 반대가 되지 않을까?
$('.inner').insertBefore('<p>Test</p>')

//detach()함수는 remove()와 같은것으로 보면 된다. 대신 detach()함수에 의해 제거된 요소들은
//추후에 다시 삽입할 수 있다. <p>엘리먼트가 2개 있었다고 가정한 후, 아래의 예제 참고
var p = $("p").detach();
console.log(p[0]);
console.log(p[1]);

//쓰레기통을 비운다고 생각 
$("p").empty();

//요소 자체 뿐만 아니라 그 안에 있는 모든 요소 제거
$("p").remove();

//inner클래스를 가진 엘리먼트를 <h2>New heading</h2>로 변경
$('<h2>New heading</h2>').replaceAll('.inner');

//<div>엘리먼트의 첫번째 요소 획득
$( "div" ).eq(0)

//div에 대하여 배경색상을 #c8ebcc로 설정한 후, 
//middle클래스를 가진 엘리먼트의 경계선 색상을 red로 설정한다.
$("div").css("background", "#c8ebcc")
	.filter(".middle")
	.css("border-color", "red");

//<p>엘리먼트의 첫번째 <span>요소에 highlight클래스를 추가
JS
$( "p span" ).first().addClass( "highlight" );
HTML
<p>
  <span>Look:</span>
  <span>This is some text in a paragraph.</span>
  <span>This is a note about it.</span>
</p>

//<ul>엘리먼트에 <li>요소가 있다면 border 스타일 적용
$("ul").has("li").css("border", "1px solid red");

//.is함수는 다른 탐색 함수들과는 달리 결과값으로 참/거짓을 리턴
//이 함수는 이벤트를 제어하는 부분과 같은 곳에 유용하게 사용됨
$( "div" ).one( "click", function() {
	//선택한 <div>가 첫번째 div인 경우
	if ( $( this ).is( ":first-child" ) ) {
		$( "p" ).text( "It's the first div." );
	} 

	//선택한 <div>가 가지고 있는 클래스가 blue 혹은 red인경우
	else if ( $( this ).is( ".blue,.red" ) ) {
		$( "p" ).text( "It's a blue or red div." );
	} 

	//선택한 <div>의 value값이 Peter가 포함되어 있는 경우
	else if ( $( this ).is( ":contains('Peter')" ) ) {
		$( "p" ).text( "It's Peter!" );
	} 

	//그외 다른 모든 경우
	else {
		$( "p" ).html( "It's nothing <em>special</em>." );
	}
	$( "p" ).hide().slideDown( "slow" );
	$( this ).css({
    	"border-style": "inset",
    	cursor: "default"
  	});
});

//<p>엘리먼트 하위의 마지막 요소 <span>찾아서 addClass 처리
//<p>가 중복일경우 마지막 <p>의 마지막 <span>을 획득
$( "p span" ).last().addClass( "highlight" );


//모든 체크박스에 대해서 아이디 값을 배열형태로 리턴
//아이디가 p1인 엘리먼트에 append 함
$("#p1").append($(':checkbox').map(function() {
	return this.id;
}).get().join(','));

//모든 체크박스에 대해서 벨류값을 배열형태로 리턴
//아이디가 p2인 엘리먼트에 append 함
$("#p2").append($(':checkbox').map(function() {
	return $(this).val();
}).get().join(','));

//체크박스에 대해서 id값과 벨류값을 배열로 받아서 for로 출력
var arrId = new Array();
var arrVal = new Array();
$(':checkbox').map(function() {
	arrId.push(this.id);
	arrVal.push($(this).val());
}).get().join(',');

for(var i = 0; i < arrId.length; i++){
	console.log(arrId[i]);
}

for(var i = 0; i < arrVal.length; i++){
	console.log(arrVal[i]);
}


//valArr에 input의 value값을 배열형태로 push
//아래쪽 for내부에서 값을 출력
HTML
<input type="text" name="name" value="John">
<input type="text" name="password" value="password">
<input type="text" name="url" value="http://ejohn.org/">

JS
var valArr = new Array();
$("input").map(function(){
	valArr.push($(this).val());
}).get().join(", ");

for(var i = 0; i < valArr.length; i++){
	console.log(valArr[i]);
}

//<li>엘리먼트 아이디가 notli아닌것 획득
$('li').not('#notli')

//div의 green클래스를 가진것 제외, blueone아이디를 가진것 제외 후 획득
$( "div" ).not( ".green, #blueone" ).css( "border-color", "red" );

//li의 2번째부터 css 적용
$( "li" ).slice( 2 ).css( "background-color", "red" );

//<div>엘리먼트에 border 스타일 지정 후, 모든 <p>요소에 background 스타일 지정
$( "div" ).css( "border", "2px solid red" ).add( "p" ).css( "background", "yellow" );

//child선택한것에 parent까지 추가 획득하여 class를 추가
$( "div" ).find( "p" ).addBack().addClass( "background" );

//contents함수는 일치하는 요소 내부의 테스트 노드를 포함한 자식요소들을 가져올 수 있는 함수
$( '.css_test' ).contents()
	.filter(function() { // filter 메서드를 사용하여 내용을 골라냄.
	return this.nodeType === 3; // nodeType 3 은 텍스트를 의미. 내용이 텍스트 인것만 반환
})

//첫번쨰 리스트에 있는 foo클래스 요소를 찾아서 그 내부의 배경색을 빨간색으로 변경
//그 다음으로 나오는 end()가 자신 앞에 나왔던 find()함수가 찾은 객체를 반환
//그래서 드번째로 나오는 find()함수는 <li class="foo">요소 안에서 찾는 것이 아니라
//<ul class="first">안에서 .bar를 찾게 됨.
//결과적으로 체이닝을 끊는 역할을 한다고 보면 됨
$('ul.first').find('.foo').css('background-color', 'red')
	.end().find('.bar').css('background-color', 'green');

//children()은 부모 요소의 바로 아래 단계인 자식요소만 선택 가능
//find()는 부모 태그의 모든 하위 요소의 자식을 선택 가능
//body바로 하위에 클래스가 red인것을 획득
$('body').children('.red');

//closet과 parents는 부모를 찾는다는것에서는 비슷하지만
//closet은 부모중 단 한개개의 결과만 리턴하고 parents는 자신부터 document root까지 검색하기때문에 1개 이상 결과가 나올 수 있음
//closet의 경우에는 item-a엘리먼트의 가장 가까운 부모 ul이 리턴
$("li.item-a").closet("ul").css("background-color", "red")

//parents의 경우에는 item-a엘리먼트의 모든 부모 ul이 리턴
$("li.item-a").parents("ul").css("background-color", "red")

//<p>요소 바로 다음에 나오는 요소중 클래스 selected를 가진 요소에 background 속성 추가
$("p").next(".selected").css("background", "yellow");

//제일 처음나오는 엘리먼트부터 뒤로 모든 p요소에 after 클래스 추가
$(":nth-child(1)").nextAll("p").addClass("after");

//아이디가 term-2인 엘리먼트부터 다음에 나오는 dt요소까지 배경색 red 적용
$("#term-2").nextUntil("dt").css("background-color", "red");

//아이디가 term-1인 엘리먼트부터 다음에 나오는 아이디가 term-3까지 dd인것만 green 색상 적용
$("#term-1").nextUntil("#term-3", "dd").css("color", "green");

//아이디가 test인 요소의 부모 요소 id값을 획득
$("#test").parent().attr("id")

//아이디가 test인 요소의 부모 요소 class값을 획득
$("#test").parent().attr("class")

//b요소의 부모요소들을 찾아서 태그명들을 map()함수를 사용해 배열로 변경
//콤마 연산자로 문자열로 변환한 뒤, 텍스트를 뿌려줌
var parentEls = $("b").parents().map(function() {
	return this.tagName;
}).get().join(", ");
$("b").append("<strong>" + parentEls + "</strong>");

//<li class="item-a"> 부모 요소들 중 <ul class="level-1">를 찾을 때까지 배경색을 빨간색으로 바꾼다.
$("li.item-a").parentsUntil(".level-1").css("background-color", "yellow");

//<li class="item-2">의 부모요소들중 클래스에 "yes"가 포함된 <ul class="level-1">를 만날때까지 녹색 테두리를 그린다.
$("li.item-2").parentsUntil($("ul.level-1"), ".yes").css("border", "3px solid green");

//.prev()함수는 DOM트리를 기준으로 하여 바로 이전 요소를 새로운 jQuery 객체로 만들어 반환
//아이디가 start인 요소를 $curr에 담고 배경색을 #f99로 설정한다
//버튼 선택시 $curr의 이전요소를 선택해 반환하고, 그 요소에 배경색을 #f99로 설정한다
var $curr = $("#start");
$curr.css("background", "#f99");
$("button").click(function() {
	$curr = $curr.prev();
	$curr.css("background", "#f99");
});

//div의 마지막 요소를 선택하여, 그 이전의 모든 div에 addClass 처리
$("div:last").prevAll().addClass("before");

//아이디가 term-2인 요소부터 시작해서 앞쪽 요소들 방향으로 쭈욱 가다가 dt 엘리먼트를 만날 때까지 빨간색을 칠하라
$("#term-2").prevUntil("dt").css("background-color", "red");

//아이디가 term-3인 요소부터 시작해서 아이디가 term-1인것을 만날 때까지 dd엘리먼트에 컬러를 green으로 칠하라
$("#term-3").prevUntil("#term-1", "dd").css("color", "green");

//hilite클래스를 가진 요소의 형제들을 찾아서 red로 변경하고 해당하는 갯수를 획득
var len = $(".hilite").siblings().css("color", "red").length;

//윈도우 width크기에 따른 값 변경
$( window ).resize(function() {
	$( "body" ).prepend( "<div>" + $( window ).width() + "</div>" );
});

//jquery의 bind를 이용하여 특정 이벤트를 수신하여 something을 처리
$("p").bind("click", function(event) {
});
$("p").bind("dblclick", function() {
});
$("p").bind("mouseenter mouseleave", function(event) {
});

//아이디가 test인 요소를 클릭하면 do something한다.
$("body").delegate("#test", "click", function() {
	//do something
});

//아이디가 test인 요소를 클릭시 alert창을 출력하는 이벤트 등록
$( '#test').on('click', function() {
	alert("success");
})

//아이디가 test인 요소를 클릭시 이벤트를 제거
$('#test').off('click');

//아이디가 foo인 요소를 선택시, 한번의 이벤트만 호출하고, 그 다음부터는 이벤트가 호출되지 않는다.
$("#foo").one("click", function() {
});

//아이디가 button1인 요소를 클릭 시, 아이디가 button2인 요소에 click이벤트를 trigger하라
$("#button1").click(function() {
	$("#button2").trigger("click");
	update($("span:last"));
});
$("#button2").click(function() {
	update($("span:first"));
});

//둘다 input에 focus()이벤트를 호출하여 실행시키고 있지만
//triggerHandler()함수로 호출된 focus()함수는 실행되지 않는다.
$("#old").click(function() {
	$("input").trigger("focus");
});
$("#new").click(function() {
	$("input").triggerHandler("focus");
});
$("input").focus(function() {
	$("<span>Focused!</span>").appendTo("body").fadeOut(1000);
});

//아이디가 bind인 요소를 클릭시
//아이디가 theone인 요소를 선택시 aClick이라는 함수가 호출 될 수 있도록 이벤트 연결
$("#bind").click(function() {
	$("#theone").click(aClick).text("Can Click!");
});
//아이디가 unbind인 요소를 클릭시
//아이디가 theone인 요소를 선택시 aClick이라는 함수가 호출 되지 않도록 이벤트 언바인드
$("#unbind").click(function() {
	$("#theone").unbind('click', aClick).text("Does nothing...");
});
function aClick() {
	$("div").show().fadeOut("slow");
}

//포커스 잃을 때 호출
blur()

//focus()의 업그레이드 버전 함수
focusin()

//input박스에서 어떤것이 선택되었다면 do something 이벤트 발생
$(":input").select(function() {
	//do something
});

//우측 마우스 버튼 클릭시 이벤트 발생
var div = $( "div:first" );
div.contextmenu(function() {
});

//currentTarget은 해당하는 요소를 반환
function checkTarget(event) {
	var ele = event.currentTarget;
}

// AJAX 시작시 호출할 함수를 등록
$(document).ajaxStart(function() {
   $('p').text('Loading !!!');
})

// AJAX가 끝날 경우 호출할 함수를 등록
$(document).ajaxStop(function() {
   $('p').text('');
})

//a태그에 href 속성이 #jsAddress2인 엘리먼트에 클래스 selected를 가지고 있다면 true를 반환
$("a[href^=#jsAddress2]").hasClass("selected")

//select박스의 옵션에 특정값이 포함되어 있으면 셀렉트하여 attr 주기
$("#selectNewDoro option:contains('"+selectNewDoroNm+"')").attr("selected", "selected");

//인덱스 값으로 셀렉트박스 값 가져오기
$("#selectNewDoro option:eq(0)").text();

//스크롤 맨위로 이동
$(".scroll").scrollTop(0);

//아이디가 selectGendMkSty 셀릭트박스 option이 selected인것의 인덱스를 획득
//얻은 인덱스 이용하여 해당하는 셀렉트박스 위치 알 수 있음
$("#selectGendMkSty option").index($("#selectGendMkSty option:selected"));

//아이디가 test인 셀렉트박스에 선택된 옵션의 data-admiCd값을 획득
$("#test option:selected").attr("data-admiCd");

//현재 선택한 엘리먼트에서 부모의 부모의 부모 엘리먼트 다음번째의 id값을 획득
$(this).parent().parent().parent().next().attr("id")

//아이디가 sty인 selectBox 엘리먼트의 option의 인덱스가 stySelIndexs.seasonInx 인 값을 획득
$("#sty option:eq("+stySelIndexs.seasonInx+")").val();
```
