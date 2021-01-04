---
description: 이 장에서는 주문자로부터 받은 주문정보를 전달하는 주문 요청 페이지에 대해 설명합니다.
---

# 결제요청

## 주문요청\(PC\)

### 1.스크립트 구성

**callback 함수 m\_Completepayment 안내**  
① 해당 함수는 결제 창 인증 완료 후 승인요청 처리를 위한 함수 \(비동기식으로의 변경에 따른 함수 추가\)  
② 해당 함수 명은 변경 불가   
③ 해당 함수의 위치는 결제 창 호출 js\_url 보다 반드시 먼저 선언   
④ 표준웹 방식의 경우 리턴 값이 form 으로 넘어옴

```text
function m_Completepayment( FormOrJson, closeEvent )
{
        var frm = document.order_info; // submit 시킬 폼데이터 지정
        
        /********************************************************************/
        /* FormOrJson은 가맹점 임의 활용 금지                               */
        /* frm 값에 FormOrJson 값이 설정 됨 frm 값으로 활용 하셔야 됩니다.  */
        /* FormOrJson 값을 활용 하시려면 기술지원팀으로 문의바랍니다.       */
        /********************************************************************/
                 GetField( frm, FormOrJson );            
        
        if( frm.res_cd.value == "0000" )
        {
                /*
                가맹점 리턴값 처리 영역
                */
                frm.submit(); // 
        }
        else
        {
                alert( "[" + frm.res_cd.value + "] " + frm.res_msg.value );
                closeEvent();
        }
}

```

**결제창 실행함수**

```text
/* 표준웹 실행 */
function jsf__pay( form )
{
    try
    {
        KCP_Pay_Execute( form ); 
    }
    catch (e)
    {
        /* IE 에서 결제 정상종료시 throw로 스크립트 종료 */ 
    }
}

```

**결제확인 버튼**  
  -  callback 함수를 통하여 submit 여부를 정함

**표준WEB방식**

```text
<input name=“” type=”button” class=”submit” value=”결제요청” onclick=”jsf__pay(this.form);”/>
```

