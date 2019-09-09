20190909 background, animation

모든요소는 float되면 block요소의 특성을 갖게된다.
position:absolute 를 지정해도 block요소가 된다.

!important - css에서 우선순위로 취급한다.

::before/::after 안에는 content가 들어있어야한다.

z-index:#; 스택 순서를 지정한다. position된 요소들에만 적용됨.

float, position:relative 같이사용가능, pos:absolute는 float무시

white-space:nowrap; 줄바꿈 금지, 모든게 한줄로 표시

background-image:url() 기본으로 이미지가 repeat됨
background-repeat: no-repeat; 이미지 repeat 없앰
background-position: x좌표y좌표, x좌표y좌표(여럿일경우)
단축표기 background: url() no-repeat 0, 10px;
             silver url() no-repeat 670px -; 색깔은 마지막에선언

투명도 rgba로 지정가능(alpha가 opacity 지정)

예시:
@keyframes nameAni
0%P{opacity: 1;} 100%{opacity:0;} 투명도1이엇다 0(사라짐)
0%{
    font-size:12px;
    color: rgba(0,0,0,0)(rgb색 0로지정, alpha(투명도)0으로지정)
    transform:translate(0,0)(요소변형))
}
100%{
    font-size: 24px;
    color:rgba(0, 0, 0, 1);(alpha(투명도)1로지정)
    transform: translate(400px,75px);
}

animation-name:
animation-duration:
animation-fill-mode:
animation-iteration-count:infinite (반복회수, 무한반복)
animation-direction: alternate (방향교체)
animation-delay:1000ms 	지연
animation-timing-function:linear(일정속도)cubic-bezier(곡선으로 속도변환)
animation-play-state: paused (실행상태)
animation: bgAni 2000ms infinite alternate ease-in-out; 단축표기
    name  duration iteration-count direction speed(timing-function)