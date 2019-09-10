form   form문생성
fieldset    연관성있는 form문 요소들의 묶음
legend 입력문자 주변으로 박스생성
required: 필수입력으로됨
placeholer:입력값 서식 힌트(위에뜨고 입력하면 사라짐)
name:form제출할때 제출된 값의 이름 정함.

입력내용 숨기기 - class="a11y-hidden"

background:#ed8625 radial-gradient(circle at right top, #f7cc31, #ed8625);
background:linear-gradient(###, ###);

border-radius 모서리 둥글게

flex-basis 최소크기, 더큰게 들어가면 늘어남

DL DT DD -Def List, Def Term, Def Definition

float된 item들이 부모요소 높이를 없앨때: .class::after{
    content: "";
    background:lime;
    clear:both;
    display: bloack;
} 로 부모요소의 높이를 복구

