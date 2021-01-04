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

* callback 함수를 통하여 submit 여부를 정함

**표준WEB방식**

```text
<input name=“” type=”button” class=”submit” value=”결제요청” onclick=”jsf__pay(this.form);”/>
```

### 2.주문요청 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left"><b>Type</b>
      </th>
      <th style="text-align:left">Max Length</th>
      <th style="text-align:left">&#xD544;&#xC218; &#xC5EC;&#xBD80;</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">req_tx</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC694;&#xCCAD;&#xC758; &#xC885;&#xB958;&#xB97C; &#xAD6C;&#xBD84;&#xD558;&#xB294;
          &#xBCC0;&#xC218;</p>
        <p>&#xACB0;&#xC81C;&#xC694;&#xCCAD;&#xD398;&#xC774;&#xC9C0;&#xC758; &#xACBD;&#xC6B0;
          &#x2018;pay&#x2019;&#xB85C; &#xC124;&#xC815;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">site_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC0C1;&#xC810;&#xC774;&#xB984;(&#xC601;&#xBB38;&#xC73C;&#xB85C; &#xC791;&#xC131;&#xAD8C;&#xC7A5;)</td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">site_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xC0C1;&#xC810;&#xCF54;&#xB4DC;</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">ordr_idxx</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">40</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC0C1;&#xC810; &#xAD00;&#xB9AC; &#xC8FC;&#xBB38;&#xBC88;&#xD638; (&#xC720;&#xB2C8;&#xD06C;&#xD55C;
          &#xAC12; &#xC124;&#xC815; &#xAD8C;&#xC7A5;)</p>
        <p><b>&#x203B; &#xC8FC;&#xBB38;&#xBC88;&#xD638;&#xB294; &#xC601;&#xBB38;&#xACFC; &#xC22B;&#xC790;&#xB85C; &#xC124;&#xC815;&#xD558;&#xC154;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;.</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">pay_method</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p><b>&#xACB0;&#xC81C;&#xC218;&#xB2E8;&#xCF54;&#xB4DC; </b>
        </p>
        <p>12&#xC790;&#xB9AC; &#xC22B;&#xC790;&#xB85C; &#xAD6C;&#xC131;</p>
        <p>(&#xC0AC;&#xC6A9; : 1, &#xC0AC;&#xC6A9; &#xC548; &#xD568; : 0)</p>
        <p>&#xC2E0;&#xC6A9;&#xCE74;&#xB4DC; : 100000000000</p>
        <p>&#xACC4;&#xC88C;&#xC774;&#xCCB4; : 010000000000</p>
        <p>&#xAC00;&#xC0C1;&#xACC4;&#xC88C; : 001000000000</p>
        <p>&#xD3EC; &#xC778; &#xD2B8; : 000100000000</p>
        <p>&#xD734; &#xB300; &#xD3F0; : 000010000000</p>
        <p>&#xC0C1; &#xD488; &#xAD8C; : 000000001000</p>
        <p>&#xC2E0;&#xC6A9;&#xCE74;&#xB4DC;, &#xACC4;&#xC88C;&#xC774;&#xCCB4;, &#xAC00;&#xC0C1;&#xACC4;&#xC88C;&#xB97C;
          &#xD558;&#xB098;&#xC758; &#xACB0;&#xC81C; &#xCC3D;&#xC5D0; &#xAC19;&#xC774;
          &#xB098;&#xD0C0;&#xB098;&#xAC8C; &#xD558;&#xB294; &#xACBD;&#xC6B0;&#xC758;
          pay_method&#xB294; &#x2018;111000000000&#x2019; &#xB85C; &#xC124;&#xC815;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">good_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">100</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC0C1;&#xD488;&#xBA85;</p>
        <p><b>&#x203B; &#xACE0;&#xAC1D;&#xC548;&#xB0B4; &#xBC0F; &#xC8FC;&#xBB38;&#xC815;&#xBCF4; &#xAD00;&#xB9AC; &#xC704;&#xD574; &#xC815;&#xD655;&#xD55C; &#xC0C1;&#xD488;&#xBA85;&#xC73C;&#xB85C; &#xC124;&#xC815;&#xD558;&#xC154;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;.</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">good_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC8FC;&#xBB38;&#xC694;&#xCCAD;&#xAE08;&#xC561;</p>
        <p>(&#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C; &#xC804;&#xB2EC;&#xD558;&#xB294;
          &#xAE08;&#xC561;&#xC73C;&#xB85C; &#xACB0;&#xC81C; &#xCC3D;&#xC5D0; &#xBCF4;&#xC5EC;&#xC9C0;&#xB294; <b>&#xC2E4;&#xC81C; &#xACB0;&#xC81C;&#xAE08;&#xC561;&#xC774; &#xC544;&#xB2D8;</b>)</p>
        <p>&#xACB0;&#xC81C;&#xCC3D;&#xC774; &#xB2EB;&#xD78C; &#xD6C4; ordr_chk &#xAC12;&#xC5D0;
          &#xB9AC;&#xD134;&#xB418;&#xB294; &#xAE08;&#xC561;&#xC815;&#xBCF4;&#xAC00;
          &#xBCC0;&#xACBD;&#xB418;&#xB294;&#xC9C0; &#xCCB4;&#xD06C;</p>
        <p> <b>&#x203B; &#xD654;&#xD3D0;&#xB2E8;&#xC704;&#xAC00; &#x2018;USD&#x2019; &#xC77C; &#xACBD;&#xC6B0;, Cent&#xAE4C;&#xC9C0; &#xC124;&#xC815;</b> 
        </p>
        <p>ex ) $10.55 &#xC77C; &#xACBD;&#xC6B0; &#xCF64;&#xB9C8;&#xB97C; &#xBE80;
          1055</p>
        <p>$100 &#xC77C; &#xACBD;&#xC6B0; 10000&#xB85C; &#xC124;&#xC815;</p>
        <p><b>&#xACB0;&#xC81C; &#xAE08;&#xC561;&#xC740; &#xC22B;&#xC790; &#xC774;&#xC678;&#xC758; &#xBB38;&#xC790;(&#xCF64;&#xB9C8; &#xB4F1;)&#xB294; &#xD5C8;&#xC6A9;&#xD558;&#xC9C0; &#xC54A;&#xC2B5;&#xB2C8;&#xB2E4;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">buyr_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">30</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC8FC;&#xBB38;&#xC790; &#xC774;&#xB984;</td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">buyr_mail</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">50</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC8FC;&#xBB38;&#xC790; &#xC774;&#xBA54;&#xC77C;</td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">buyr_tel1</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC8FC;&#xBB38;&#xC790; &#xC804;&#xD654;&#xBC88;&#xD638;</td>
    </tr>
    <tr>
      <td style="text-align:left">11</td>
      <td style="text-align:left">buyr_tel2</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xC8FC;&#xBB38;&#xC790; &#xD734;&#xB300;&#xD3F0;&#xBC88;&#xD638;</td>
    </tr>
    <tr>
      <td style="text-align:left">12</td>
      <td style="text-align:left">currency</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD654;&#xD3D0;&#xB2E8;&#xC704;</p>
        <p>&#xC6D0;&#xD654; : WON / &#xB2EC;&#xB7EC; : USD</p>
        <p>&#xB2EC;&#xB7EC;&#xC758; &#xACBD;&#xC6B0; NHN KCP&#xC5D0; &#xBCC4;&#xB3C4;&#xC758;
          &#xC2E0;&#xCCAD;(&#xAD6D;&#xC81C; &#xC138;&#xBBF8;&#xB098;, &#xAD6D;&#xC81C;
          &#xD559;&#xC220;&#xB300;&#xD68C; &#xB4F1;&#xB9CC; &#xC2E0;&#xCCAD; &#xAC00;&#xB2A5;)&#xD574;&#xC57C;
          &#xC0AC;&#xC6A9; &#xAC00;&#xB2A5;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">13</td>
      <td style="text-align:left">shop_user_id</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC1FC;&#xD551;&#xBAB0;&#xD68C;&#xC6D0;ID</p>
        <p>&#xAE30;&#xAD00;&#xC5D0; &#xB530;&#xB77C; RM &#xC870;&#xCE58;&#xB97C;
          &#xC704;&#xD574; &#xC1FC;&#xD551;&#xBAB0; &#xAD00;&#xB9AC; ID&#xB97C; &#xD544;&#xC218;&#xB85C;
          &#xC694;&#xCCAD;</p>
        <p>&#xD734;&#xB300;&#xD3F0;&#xC18C;&#xC561;&#xACB0;&#xC81C; &#x2013; 40Byte</p>
        <p>&#xC0C1;&#xD488;&#xAD8C;&#xACB0;&#xC81C; &#x2013; 20Byte</p>
      </td>
    </tr>
  </tbody>
</table>

**※ pay\_method = “111000000000” 로 설정 했을 때 보여지는 결제 창**

![](.gitbook/assets/pay_method.jpg)

### 3.신용카드 옵션처리 파라미터



