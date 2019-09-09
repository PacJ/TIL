20190906
*CSS 구조선택자 n-th child()
    *nth-child(#)
    *nth-child(n+6) 6몇번쨰 이상부터 선택
    *nth-child(-n+9) 9번째 이하부터 선택
    *nth-child(n+4):nth-child(-n+8) 4이상 8이하 선택
    *nth-child(odd/even) 홀수/짝수 선택

*Icons
    *@import url('')
    *import한대로 class:icon-ellipsis-vert:before or content: '\f142'; 백슬레시:안보이게함
    *

*.a11y-hidden/off-screen/readable-hidden 숨김콘텐츠

*color:hsla(hue,saturation,lightness,alpha)

*clear:left/right/both 강제로 마진이주어짐, float랑 떨어트릴수있, margin-top/bottom 주면 clear강제마진과 병합.
    *margin-top/bottom 은 병합되서 큰것이 적용됨
    *clear는 블록요소한테만 적용가능

*속성선택자 .box[class^="box"] box내의 속성값으로 시작하는것들 선택

*float 후에 height가 덮임으로 height배정

*background-image:url() / linear-gradient(#deg,color,color,to bottom)
    *import 가능:(to bottom, rgba(255,187,50,1) 0%,rgba(204,40,40,1) 35%,rgba(204,40,40,1) 70%,rgba(255,187,50,1) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */

*border-radius: 모서리 깎기
*border-shadow/box-shadow/text-shadow: 그림자

*.menu::after{
    content: "";
    background: lime;
    clear: both;
    display: block;
}   컨텐트 비워두기, float관련

*.menu-item{
    float: left;
    line-height: 45px;
}   float공부해