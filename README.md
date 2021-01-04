---
description: 이 문서는 가맹점 사이트에서 연동 가이드에 따라 PG결제 연동 시스템을 개발하는 방법에 대해 설명합니다.
---

# 개요 및 연동 전 준비사항

**문서개요**

* 가맹점에서 구현해야 하는 API 명세 가이드
* 서비스 설명 및 NHN KCP 권고 사항 설명
* 각 샘플 페이지 해당 역할 및 파라미터 상세 안내

**독자**

* 이 문서의 독자는 NHN KCP PG결제를 연동하는 가맹점 사이트 개발자입니다.

**문의처**

이 문서의 내용에 오류가 있거나 내용과 관련한 의문 사항이 있으시면 아래 연락처로 문의 바랍니다.

* NHN KCP 기술지원팀 : 1544-8661 혹은 support@kcp.co.kr

## 연동 전 준비사항

### 1.공통 안내 및 권장사항

* KCP 인코딩 방식은 **EUC-KR** 형식을 사용하며, 이에 따른 리턴 값도 **EUC-KR**로 제공합니다.
* 결제로그\(log\)는 기본적으로 관리를 권장합니다. \(※ 오류 거래 건에 대한 추적이 필요할 수 있음\)
* 통신방식은 샘플소스 기준으로 bin\pp\_cli \(실행파일\)를 통해 가맹점 서버와 소켓통신 합니다.\( JSP의 경우 lib\jPpcliE.jar 파일 \)
* 방화벽은 KCP와 결제 통신을 위해 TCP SOCKET을 사용합니다.
* 결과 요청 및 처리에 관한 변수처리는 기관의 정책이나 신규 서비스 출시 등에 따라 변경이 될 수 있으니 연동매뉴얼을 업데이트하여 관리하시기 바랍니다.
* **NHN KCP 결제 모듈에는 데이터베이스 연동 작업을 위한 기능은 포함되어있지 않습니다.**

  \(데이터베이스 연동을 위한 지불 결과 데이터만 제공하며 데이터베이스 처리에 관한 부분은 일체 가맹점에서 관리\)

* 결과 요청 및 처리에 관한 변수처리는 기관의 정책이나 신규 서비스 출시 등에 따라 변경이 될 수 있으니 연동매뉴얼을 업데이트하여 관리하시기 바랍니다.
* 설치 Directory 는 절대 Web으로 접근할 수 있는 경로에 설치하지 마십시오.

  결제서비스 관련 폴더 및 파일들은 보안상 절대 Web을 통해서 접근하지 않도록 관리해주시기 바랍니다.

* 결제 창 호출 시 요청하는 site\_cd 와 승인 요청 시 site\_cd 가 다를 경우 정산 시 불이익을 받을 수 있습니다.
* 반드시 결제 인증 및 승인 시 동일한 site\_cd 로 요청하시기 바랍니다.

**※특히 사이트 키 값, 결제거래번호, 환경설정파일의 경우 가맹점과 NHN KCP간의 보안을 유지하는 값이므로 Web 상에서 확인될 수 없도록 관리 바랍니다.**

### 2.결제 창 호출 가능한 운영체제 및 브라우저 안내

① PC버전 OS : 표준WEB\(Windows & Mac\), Plugin\(Windows only\)  
② PC버전 Browser : IE\(Ver. 6 ~\), Firefox \(Ver. 5.0 ~\), Chrome \(Ver. 16.0 ~\), Safari\(Ver. 5.0 ~\), Opera \(Ver. 10~\)  
③ 모바일버전 OS : Android, IOS  
④ 모바일버전 Browser : 스마트폰 기본브라우저

**※ 방화벽 설정 정보**

**\[PC, Mobile 공통\]**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC5F0;&#xACB0;&#xB300;&#xC0C1; PORT</th>
      <th style="text-align:left"><b>8090</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#xC5F0;&#xACB0;&#xB300;&#xC0C1; &#xB3C4;&#xBA54;&#xC778;</td>
      <td style="text-align:left">
        <p>paygw.kcp.co.kr (&#xC2E4; &#xACB0;&#xC81C;)</p>
        <p>testpaygw.kcp.co.kr (&#xD14C;&#xC2A4;&#xD2B8; &#xACB0;&#xC81C;)</p>
      </td>
    </tr>
  </tbody>
</table>

**\[Mobile 전용\]**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#xC5F0;&#xACB0;&#xB300;&#xC0C1; PORT/&#xB3C4;&#xBA54;</b>
      </th>
      <th style="text-align:left">
        <p>smpay.kcp.co.kr 443/80 (&#xC2E4; &#xACB0;&#xC81C;)</p>
        <p>testsmpay.kcp.co.kr 443 (&#xD14C;&#xC2A4;&#xD2B8; &#xACB0;&#xC81C;)</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

* NHN KCP 결제는 TCP Socket 통신으로 이루어지며, 추가로 모바일버전의 경우 결제 창 호출 전 SOAP 통신을 통해 주요 주문데이터 검증을 위해 거래등록을 진행합니다. 아래 도메인, PORT 에 대해 방화벽 허가를 해주셔야 합니다.

### 3.API 규격 안내 및 특수문자

해당 항목에서는 결제 시스템을 구축하기 위한 파라미터 소개 및 규격 안내 페이지입니다. 제공해 드리는 샘플소스와 함께 해당 파라미터를 참고하시어 연동하시기 바랍니다.

**데이터 타입**

| Column | Type | Description |
| :--- | :--- | :--- |
| 1 | Number | 숫자형 Integer : \(0~9\) |
| 2 | String | 문자형 String : Alpha numeric \(A-Z; 0-9; UTF-8 characters\) |
| 3 | Etc | 기타 Etc |

**사용불가 특수문자**

| 콤마 | 엠퍼센트 | 세미콜론 | 뉴 라인 | 역 슬래쉬 | 파이프 라인 | 작은 따옴표 | 큰 따옴표 | 부등호 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **,** | & | ; | \n | \ | \| | ' | " | &lt; |

※ 스크립트 언어 불가 ex\) &lt;script&gt;. eval;\(\(.\*\)\)

※ \u0000 : unicode null

요청 페이지에서 데이터를 입력할 때, 위와 같은 특수 문자를 입력할 경우 오류가 발생할 수 있습니다. 위 특수 문자 목록을 반드시 참고하여, 데이터를 입력할 때에 반드시 체크해 주시기 바랍니다.

### 4.보안지침서

하기 사항을 지키지 않아 발생하는 보안관련 사고에 대해서는 NHN KCP에서 책임을 질 수 없는 부분이오니 반드시 결제모듈 연동 시 철저하게 관리 부탁 드립니다.

* **금액 검증을 위한 절차 \(필수사항\)** **※ 추후에 발생할 수 있는 결제금액 위 변조 위험에 대비해 해당 기능을 반드시 체크해 주시기 바랍니다.** ① 주문페이지\(order\)에서 전달하는 good\_mny 값과 별개로 pp\_cli\_hub 페이지에서 실제 결제될 금액 ordr\_mony 값 처리 ② 결제완료 후 전달되는 금액\(amount\)과 DB의 금액을 비교하여 다를 경우 자동 취소하는 bSucc 구문 처리로 자동취소 로직 구현
* **site\_key 관리 강화**  ① 주문페이지\(order\)에는 site\_cd 만 전달하고, site\_key 값은 서버사이드 구간 \(pp\_cli\_hub\)에서 사용사이트키를 주문페이지에서 전달하면 웹 상에 사이트키 값이 노출될 위험이 있을 수 있습니다. ② 결제 연동 시 사이트코드와 사이트키를 담당자 메일로 전달받으면 해당 사이트 키 값을 승인 및 취소 시에 적용해야 합니다. **※ 취소 시 사이트키를 적용하지 않으면 취소 거절이 발생합니다.**
* **결제 로그 파일 관리 강화** 결제완료 및 결제처리 시 발생하는 log 파일은 웹에서 접근이 불가한 위치에서 처리해야 합니다. ① Apache 와 WAS 에서 처리 시 pp\_cli 파일 위치에 log 파일이 생성되기 때문에 documentRoot로 설정된 곳에 pp\_cli 파일과 log 파일을 올리지 마시기 바랍니다. ② 설치 Directory 는 절대 Web으로 접근할 수 없는 경로에 설치해주시기 바랍니다. 결제 실행관련 파일들\(bin, key, log, site\_conf\_inc\)은 보안상 절대 web 을 통해서 접근하지 않도록 관리해주시기 바랍니다. ③ NHN KCP와 통신하는 pp\_cli\_hub 페이지 접근 시에는 접근권한을 반드시 적용하여 다른 외부에서 해당 페이지에 접근을 막을 수 있게 관리하시기 바랍니다. ④ 샘플소스내의 페이지명\(예. site\_conf\_inc, order, pp\_cli\_hub, cancel 등\)은 상점페이지명에 맞게 수정 **특히 pp\_cli\_hub 페이지명은 그대로 사용하지 않는 것을 권장 드립니다.**  **※가맹점에서 관리하는 소중한 고객 정보 등이 웹에 노출 될 우려가 있습니다.** 

### 5.환경설정

가맹점에 부여된 가맹점코드\(site\_cd\)와 암호화 관련 필드\(site\_key\), 가맹점 서버 경로 등을 설정하는 페이지입니다.  
환경설정 파일 경로는 샘플 소스 기준으로 {HOME 디렉터리}/PAYMENT\_STANDARD/cfg/site\_conf\_inc 페이지에 해당하며 REAL 정보와 TEST 정보를 구분하여 반영해 주시기 바랍니다.

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

※ TEST 환경설정예

```text
String g_conf_home_dir = "C:/APM_Setup/htdocs/ax_hub_windows_php";            // 절대경로 입력
String g_conf_key_dir = "C:/APM_Setup/htdocs/ax_hub_windows_php/bin/pub.key";  //pub.key 파일 경로(파일명까지 )
String g_conf_log_dir = "C:/APM_Setup/htdocs/ax_hub_windows_php/log";          // log 절대경로 입력
String g_conf_gw_url = “testpaygw.kcp.co.kr”
String g_conf_js_url = "https://testpay.kcp.co.kr/plugin/payplus_web.jsp";
String g_wsdl = "KCPPaymentService.wsdl";
String g_conf_site_cd = "T0000";
String g_conf_site_key = "3grptw1.zW0GSo4PQdaGvsF__";
String g_conf_site_name = "KCP TEST SHOP";
String g_conf_log_level = "3";
String g_conf_gw_port  = "8090";    // 포트번호(변경불가)
String module_type = "01";          // 변경불가
```

#### 리얼 전환 시 체크사항

```text
String g_conf_gw_url = “paygw.kcp.co.kr”;
String g_conf_js_url = “ https://pay.kcp.co.kr/plugin/payplus_web.jsp”;
String g_conf_site_cd = "실제 부여 받은 사이트코드";
String g_conf_site_key = "실제 부여 받은 사이트키";
```

※ 결제 로그의 레벨을 ‘0~3’으로 설정\_conf\_site\_cd, g\_conf\_site\_key 는 반드시 NHN KCP에서 발급한 사이트코드\(site\_cd\) 와 사이트키\(site\_key\) 설정

※ 스크립트 언어에 따른 추가 수정사항  
① ASP : g\_conf\_server = “REAL”   
② Windows ASP.NET : /mobile\_sample/STANDARD/order\_approval.aspx.cs   
103번째줄 this.Url = “[https://smpay.kcp.co.kr”](https://smpay.kcp.co.kr”)   
③ JSP : g\_conf\_server = “TRUE”   
④ PHP : $g\_wsdl = “real\_KCPPaymentService.wsdl”

