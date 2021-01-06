---
description: 이 장에서는 PC버전이나 모바일버전의 결제창으로 인증이 완료된 정보를 통해 실제 결제요청을 하고 결제결과를 처리하는 페이지를 설명합니다.
---

# 결제요청 및 응답

## 결제요청

### 1.인증처리 후 결제 창 전달 값

해당 값은 결제창에서 내려주는 값으로 임의로 값을 수정하시면 안됩니다. 결제창에서 내려주는 값을 그대로 샘플소스 pp\_cli\_hub 페이지로 전달하여 승인 요청을 진행하시기 바랍니다. 결제창에서 내려주는 res\_cd, res\_msg 는 결제창 내에서 인증처리가 완료되었다는 의미이며, 결제가 완료되었다는 것이 아님을 유의하시기 바랍니다. 반드시 결제창에서 인증완료 후 전달받은 enc\_info, enc\_data 로 승인 요청을 하신 후 “응답 파라미터” 의 최종 결제 결과 값을 확인하시기 바랍니다

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
      <td style="text-align:left">enc_data</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD1B5;&#xD569; &#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C;&#xBD80;&#xD130;
          &#xC804;&#xB2EC; &#xBC1B;&#xB294; &#xC778;&#xC99D;&#xACB0;&#xACFC; &#xC554;&#xD638;&#xD654;
          &#xB370;&#xC774;&#xD130;</p>
        <p><b>&#x203B; &#xC808;&#xB300; &#xC784;&#xC758;&#xB85C; &#xBCC0;&#xACBD; &#xBD88;&#xAC00;. &#xACB0;&#xC81C; &#xCC3D;&#xC5D0;&#xC11C; &#xB0B4;&#xB824;&#xC8FC;&#xB294; &#xAC12; &#xADF8;&#xB300;&#xB85C; &#xC0AC;&#xC6A9;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">enc_info</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD1B5;&#xD569; &#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C;&#xBD80;&#xD130;
          &#xC804;&#xB2EC; &#xBC1B;&#xB294; &#xC778;&#xC99D;&#xACB0;&#xACFC; &#xC554;&#xD638;&#xD654;
          &#xB370;&#xC774;&#xD130;</p>
        <p><b>&#x203B; &#xC808;&#xB300; &#xC784;&#xC758;&#xB85C; &#xBCC0;&#xACBD; &#xBD88;&#xAC00;. &#xACB0;&#xC81C; &#xCC3D;&#xC5D0;&#xC11C; &#xB0B4;&#xB824;&#xC8FC;&#xB294; &#xAC12; &#xADF8;&#xB300;&#xB85C; &#xC0AC;&#xC6A9;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">tran_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD1B5;&#xD569; &#xACB0;&#xC81C; &#xCC3D;&#xC5D0;&#xC11C; &#xCC98;&#xB9AC;&#xD558;&#xC5EC;
          &#xC804;&#xB2EC;&#xBC1B;&#xB294; &#xC0C1;&#xD0DC;&#xCF54;&#xB4DC; &#xAC12;</p>
        <p><b>&#x203B; &#xC808;&#xB300; &#xC784;&#xC758;&#xB85C; &#xBCC0;&#xACBD; &#xBD88;&#xAC00;. &#xACB0;&#xC81C; &#xCC3D;&#xC5D0;&#xC11C; &#xB0B4;&#xB824;&#xC8FC;&#xB294; &#xAC12; &#xADF8;&#xB300;&#xB85C; &#xC0AC;&#xC6A9; </b>
        </p>
        <p><b>&#x203B; &#xD574;&#xB2F9; &#xAC12;&#xC740; KCP &#xC2DC;&#xC2A4;&#xD15C;&#xC5D0;&#xC11C; &#xCD94;&#xAC00; &#xBC0F; &#xBCC0;&#xACBD;&#xC774; &#xB418;&#xB294; &#xAC12;&#xC774;&#xAE30; &#xB54C;&#xBB38;&#xC5D0; &#xC790;&#xCCB4; &#xAD00;&#xB9AC;&#xD558;&#xC2DC;&#xBA74; &#xC548;&#xB428;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">ordr_chk</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC778;&#xC99D;&#xC644;&#xB8CC; &#xD6C4; &#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C;&#xBD80;&#xD130;
          &#xC804;&#xB2EC; &#xBC1B;&#xB294; &#xC8FC;&#xBB38;&#xBC88;&#xD638;&#xC640;
          &#xC8FC;&#xBB38;&#xAE08;&#xC561; &#xC8FC;&#xBB38;&#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C;
          &#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C; &#xC804;&#xB2EC;&#xD55C; ordr_idxx,
          good_mny &#xAC12;&#xC774; &#xADF8;&#xB300;&#xB85C; &#xB9AC;&#xD134; &#xB418;&#xAE30;
          &#xB54C;&#xBB38;&#xC5D0; NHN KCP&#xB85C; &#xACB0;&#xC81C;&#xC694;&#xCCAD;
          &#xC804;, &#xB9AC;&#xD134; &#xBC1B;&#xC740; &#xD574;&#xB2F9; &#xAC12;&#xC5D0;
          &#xB300;&#xD574; &#xC5C5;&#xCCB4; &#xCE21;&#xC5D0;&#xC11C; &#xB2E4;&#xC2DC;
          &#xD55C;&#xBC88; &#xAC80;&#xC99D; &#xD558;&#xACE0; &#xACB0;&#xC81C;&#xC694;&#xCCAD;
          &#xD558;&#xC2DC;&#xAE30; &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;.</p>
        <p><b>&#x203B; PC&#xBC84;&#xC804;&#xC5D0;&#xB9CC; &#xC801;&#xC6A9;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">use_pay_method</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xACE0;&#xAC1D;&#xC774; &#xC120;&#xD0DD;&#xD55C; &#xACB0;&#xC81C; &#xC218;&#xB2E8;</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">cash_yn</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD604;&#xAE08;&#xC601;&#xC218;&#xC99D; &#xC120;&#xD0DD;&#xC5EC;&#xBD80;</td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">cash_tr_code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD604;&#xAE08;&#xC601;&#xC218;&#xC99D; &#xC120;&#xD0DD; &#xC2DC; &#xC2DD;&#xBCC4;&#xCF54;&#xB4DC;</p>
        <p>&#xC18C;&#xB4DD;&#xACF5;&#xC81C;&#xC6A9;(&#xAC1C;&#xC778;) : 0 / &#xC9C0;&#xCD9C;&#xC99D;&#xBE59;&#xC6A9;(&#xAE30;&#xC5C5;)
          : 1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">cash_id_info</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD604;&#xAE08;&#xC601;&#xC218;&#xC99D; &#xB4F1;&#xB85D;&#xC694;&#xCCAD;
        &#xC2DC; &#xC785;&#xB825;&#xD55C; &#xB4F1;&#xB85D; &#xC815;&#xBCF4;</td>
    </tr>
  </tbody>
</table>

### 2.결제금액 위변조 방지 기능 구현

pp\_cli\_hub 페이지에서 enc\_data와 enc\_info 값을 처리하는 위치에 아래 구문 추가 \(샘플소스에 명시되어있음\) 샘플소스에 코딩 되어있는 1원은 ordr\_mony 의 예제 값이며, 실제 상점 측에서 결제될 금액을 입력하여 전달하면 해당 금액과 암호화된 값에 있는 금액을 비교함

① PHP 사용하는 경우

```text
$c_PayPlus->mf_set_ordr_data( "ordr_mony",  "1" );
```

② JSP 사용하는 경우

```text
if(good_mny.trim().length() > 0)
{
    int ordr_data_set_no;
    ordr_data_set_no = c_PayPlus.mf_add_set( "ordr_data" );
    c_PayPlus.mf_set_us( ordr_data_set_no, "ordr_mony", "1" );
}
```

   
③ ASP 사용하는 경우 

   3-1\) sample/pp\_cli\_hub\_lib.asp 파일에서 54번째줄부터 91번째줄까지 추가  
     ORDER DATA 전문 구성 추가   
     REQUEST DATA 전문 구성 추가

   3-2\) sample/pp\_cli\_hub.asp 파일에서 134번째줄부터 145번째줄까지 추가

```text
payx_data_set = ""
ordr_data_set = ""                        
ordr_data_set = c_Mesg.mf_set_ordr_data( "ordr_mony", "1") 
c_Mesg.InitialTX
tx_req_data_set = c_Mesg.mf_set_req_data( ordr_data_set )
c_Mesg.InitialTX
c_PayPlus.lf_PP_CLI_LIB__set_plan_data tx_req_data_set
c_Mesg.InitialTX
```

  
④ ASP.NET 사용하는 경우

​  4-1\) sample/App\_Code 폴더 안의 C\_PP\_CLI\_COM.cs 파일에서 229번째 줄 추가

```text
m_c_Payplus.lf_PP_CLI_LIB__set_plan_data(m_straDataSet_req[parm_nDataSetInx_req, 1]);
```

  4-2\) sample/AX\_HUB/pp\_cli\_hub.aspx.cs 파일에서 365번째 줄에서 382번째 줄까지 추가

```text
int nDataSetInx_req;
int nDataSetInx_ordr_no;
if (good_mny.Trim().Length > 0)
{
    nDataSetInx_req = parm_c_PP_CLI.m_f__get_dataset("plan_data");
    nDataSetInx_ordr_no = parm_c_PP_CLI.m_f__get_dataset("ordr_data");
    
    parm_c_PP_CLI.m_f__set_data(nDataSetInx_ordr_no, "ordr_mony", "1");
    
    parm_c_PP_CLI.m_f__add_data(nDataSetInx_req, nDataSetInx_ordr_no, "\x1c");
}
```

**※ ordr\_mony 값을 세팅 완료 후에 잘못된 금액을 넣어서 테스트 진행을 해주시기 바랍니다.**   
NHN KCP 응답코드로 res\_cd = 8059, res\_msg = 포맷에러\(지불정보-공통:결제금액 불일치\)를 받으면 정상적으로 적용된 것입니다.

 ※ 실제 가맹점에서 관리하는 결제정보와 승인 후 리턴 받는 결제정보를 비교 검증하셔서 해당 정보가 다를 경우 **bSucc 변수 처리 \(bSucc = “false”\)**를 해주시기 바랍니다.   
참조 : 샘플소스 pp\_cli\_hub 페이지의 “승인 결과 DB 처리 실패 시 : 자동취소” 

**※ 자동취소 로직 적용시 NHN KCP와 통신하는 실행파일이 올려진 서버 IP를 상점관리자페이지\(admin8.kcp.co.kr\)에 반드시 등록 바랍니다.** 서버 IP 등록경로 : admin8.kcp.co.kr→상점정보관리→정보변경→취소서버 IP설정 \(**미등록시 취소 오류**\)

### 3.응답파라미터

#### \[결제 실패\]

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
      <td style="text-align:left">res_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xACB0;</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">res_msg</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD1B5;&#xD569; &#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C;&#xBD80;&#xD130;
          &#xC804;&#xB2EC; &#xBC1B;&#xB294; &#xC778;&#xC99D;&#xACB0;&#xACFC; &#xC554;&#xD638;&#xD654;
          &#xB370;&#xC774;&#xD130;</p>
        <p><b>&#x203B; &#xC808;&#xB300; &#xC784;&#xC758;&#xB85C; &#xBCC0;&#xACBD; &#xBD88;&#xAC00;. &#xACB0;&#xC81C; &#xCC3D;&#xC5D0;&#xC11C; &#xB0B4;&#xB824;&#xC8FC;&#xB294; &#xAC12; &#xADF8;&#xB300;&#xB85C; &#xC0AC;&#xC6A9;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">tran_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD1B5;&#xD569; &#xACB0;&#xC81C; &#xCC3D;&#xC5D0;&#xC11C; &#xCC98;&#xB9AC;&#xD558;&#xC5EC;
          &#xC804;&#xB2EC;&#xBC1B;&#xB294; &#xC0C1;&#xD0DC;&#xCF54;&#xB4DC; &#xAC12;</p>
        <p><b>&#x203B; &#xC808;&#xB300; &#xC784;&#xC758;&#xB85C; &#xBCC0;&#xACBD; &#xBD88;&#xAC00;. &#xACB0;&#xC81C; &#xCC3D;&#xC5D0;&#xC11C; &#xB0B4;&#xB824;&#xC8FC;&#xB294; &#xAC12; &#xADF8;&#xB300;&#xB85C; &#xC0AC;&#xC6A9; </b>
        </p>
        <p><b>&#x203B; &#xD574;&#xB2F9; &#xAC12;&#xC740; KCP &#xC2DC;&#xC2A4;&#xD15C;&#xC5D0;&#xC11C; &#xCD94;&#xAC00; &#xBC0F; &#xBCC0;&#xACBD;&#xC774; &#xB418;&#xB294; &#xAC12;&#xC774;&#xAE30; &#xB54C;&#xBB38;&#xC5D0; &#xC790;&#xCCB4; &#xAD00;&#xB9AC;&#xD558;&#xC2DC;&#xBA74; &#xC548;&#xB428;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">ordr_chk</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC778;&#xC99D;&#xC644;&#xB8CC; &#xD6C4; &#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C;&#xBD80;&#xD130;
          &#xC804;&#xB2EC; &#xBC1B;&#xB294; &#xC8FC;&#xBB38;&#xBC88;&#xD638;&#xC640;
          &#xC8FC;&#xBB38;&#xAE08;&#xC561; &#xC8FC;&#xBB38;&#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C;
          &#xACB0;&#xC81C; &#xCC3D;&#xC73C;&#xB85C; &#xC804;&#xB2EC;&#xD55C; ordr_idxx,
          good_mny &#xAC12;&#xC774; &#xADF8;&#xB300;&#xB85C; &#xB9AC;&#xD134; &#xB418;&#xAE30;
          &#xB54C;&#xBB38;&#xC5D0; NHN KCP&#xB85C; &#xACB0;&#xC81C;&#xC694;&#xCCAD;
          &#xC804;, &#xB9AC;&#xD134; &#xBC1B;&#xC740; &#xD574;&#xB2F9; &#xAC12;&#xC5D0;
          &#xB300;&#xD574; &#xC5C5;&#xCCB4; &#xCE21;&#xC5D0;&#xC11C; &#xB2E4;&#xC2DC;
          &#xD55C;&#xBC88; &#xAC80;&#xC99D; &#xD558;&#xACE0; &#xACB0;&#xC81C;&#xC694;&#xCCAD;
          &#xD558;&#xC2DC;&#xAE30; &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;.</p>
        <p><b>&#x203B; PC&#xBC84;&#xC804;&#xC5D0;&#xB9CC; &#xC801;&#xC6A9;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">use_pay_method</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xACE0;&#xAC1D;&#xC774; &#xC120;&#xD0DD;&#xD55C; &#xACB0;&#xC81C; &#xC218;&#xB2E8;</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">cash_yn</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD604;&#xAE08;&#xC601;&#xC218;&#xC99D; &#xC120;&#xD0DD;&#xC5EC;&#xBD80;</td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">cash_tr_code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD604;&#xAE08;&#xC601;&#xC218;&#xC99D; &#xC120;&#xD0DD; &#xC2DC; &#xC2DD;&#xBCC4;&#xCF54;&#xB4DC;</p>
        <p>&#xC18C;&#xB4DD;&#xACF5;&#xC81C;&#xC6A9;(&#xAC1C;&#xC778;) : 0 / &#xC9C0;&#xCD9C;&#xC99D;&#xBE59;&#xC6A9;(&#xAE30;&#xC5C5;)
          : 1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">cash_id_info</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD604;&#xAE08;&#xC601;&#xC218;&#xC99D; &#xB4F1;&#xB85D;&#xC694;&#xCCAD;
        &#xC2DC; &#xC785;&#xB825;&#xD55C; &#xB4F1;&#xB85D; &#xC815;&#xBCF4;</td>
    </tr>
  </tbody>
</table>

