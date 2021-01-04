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
      <td style="text-align:left">g_conf_home_dir</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>pp_cli(bin &#xB514;&#xB809;&#xD1A0;&#xB9AC; &#xC804;) &#xBAA8;&#xB4C8;
          &#xC808;&#xB300;&#xACBD;&#xB85C;</p>
        <p>&#x203B; &#xC720;&#xB2C9;&#xC2A4;&#xC758; &#xACBD;&#xC6B0; &#xD544;&#xC218;
          &#xC124;&#xC815;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p>g_conf_key_dir</p>
        <p>g_kcp_key_path</p>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>pub.key &#xD30C;&#xC77C; &#xC808;&#xB300;&#xACBD;&#xB85C;</p>
        <p>&#x203B; &#xC708;&#xB3C4;&#xC6B0; &#xC804;&#xC6A9;</p>
        <p>&#x203B; g_kcp_key_path : ASP.NET &#xC804;&#xC6A9;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">g_conf_log_dir
        <br />g_conf_log_path</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xB85C;&#xADF8; &#xD3F4;&#xB354; &#xC0DD;&#xC131; &#xACBD;&#xB85C; &#xC9C0;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">g_conf_gw_url</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>NHN KCP &#xACB0;&#xC81C;&#xC11C;&#xBC84; URL</p>
        <p>Test : testpaygw.kcp.co.kr</p>
        <p>Real : paygw.kcp.co.kr</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">g_conf_js_url</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>Test : <a href="https://testpay.kcp.co.kr/plugin/payplus_web.jsp">https://testpay.kcp.co.kr/plugin/payplus_web.jsp</a> Real
          : <a href="https://pay.kcp.co.kr/plugin/payplus_web.jsp">https://pay.kcp.co.kr/plugin/payplus_web.jsp</a> 
        </p>
        <p>&#x203B; ASP.NET&#xC758; &#xACBD;&#xC6B0; sample/STANDARD/orderl.aspx
          &#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C; &#xC9C1;&#xC811; &#xC124;&#xC815;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">g_conf_site_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xAC00;&#xB9F9;&#xC810; &#xC0AC;&#xC774;&#xD2B8;&#xCF54;&#xB4DC;</p>
        <p>&#xAC00;&#xC785; &#xC2DC; &#xBC1C;&#xC1A1;&#xD574;&#xB4DC;&#xB9AC;&#xB294;
          &#xC5F0;&#xB3D9;&#xBA54;&#xC77C; &#xCC38;&#xC870;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">g_conf_site_key</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">25</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xAC00;&#xB9F9;&#xC810; &#xC0AC;&#xC774;&#xD2B8;&#xD0A4;</p>
        <p>&#xAC00;&#xC785; &#xC2DC; &#xBC1C;&#xC1A1;&#xD574;&#xB4DC;&#xB9AC;&#xB294;
          &#xC5F0;&#xB3D9;&#xBA54;&#xC77C; &#xCC38;&#xC870;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">g_conf_site_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xC0C1;&#xC810; &#xC774;&#xB984; &#xC548;&#xC2EC;&#xD074;&#xB9AD; &#xCC3D;&#xC5D0;
        &#xD310;&#xB9E4;&#xC790; &#xB610;&#xB294; &#xC0C1;&#xC810; &#xBA85;&#xC73C;&#xB85C;
        &#xD45C;&#xC2DC; &#x203B; &#xD2B9;&#xC218;&#xBB38;&#xC790; &#xAE08;&#xC9C0;</td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">g_conf_gw_port</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>NHN KCP &#xACB0;&#xC81C;&#xC11C;&#xBC84; PORT</p>
        <p>NHN KCP &#xACB0;&#xC81C; &#xC11C;&#xBC84;&#xC758; &#xD3EC;&#xD2B8;&#xB85C;
          &#xD14C;&#xC2A4;&#xD2B8; &#xC2E4; &#xACB0;&#xC81C;&#xC758; &#xACBD;&#xC6B0;
          &#xB3D9;&#xC77C;&#xD558;&#xAC8C; &#x2018;8090&#x2019;&#xC73C;&#xB85C; &#xC124;&#xC815;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">module_type</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xBAA8;&#xB4C8; &#xD0C0;&#xC785; (&#xBCC0;&#xACBD;&#xBD88;&#xAC00;) &#xBC18;&#xB4DC;&#xC2DC;
        &#x2018;01&#x2019;&#xB85C; &#xC124;&#xC815; (&#xC124;&#xC815; &#xBCC0;&#xACBD;
        &#xC2DC; &#xC815;&#xC0C1;&#xC801;&#xC73C;&#xB85C; &#xACB0;&#xC81C;&#xAC00;
        &#xC774;&#xB8E8;&#xC5B4;&#xC9C0;&#xC9C0; &#xC54A;&#xC744; &#xC218; &#xC788;&#xC74C;)</td>
    </tr>
    <tr>
      <td style="text-align:left">11</td>
      <td style="text-align:left">g_conf_log_level</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xB85C;&#xADF8;&#xC758; &#xB808;&#xBCA8;&#xC744; &#x2018;0~3&#x2019;&#xC73C;&#xB85C;
        &#xC124;&#xC815;</td>
    </tr>
  </tbody>
</table>
