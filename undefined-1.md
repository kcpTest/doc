---
description: 이 장에서는 PC버전이나 모바일버전의 결제창으로 인증이 완료된 정보를 통해 실제 결제요청을 하고 결제결과를 처리하는 페이지를 설명합니다.
---

# 결제요청 및 응답

## 결제요청

### 1.인증처리 후 결제 창 전달 값
해당 값은 결제창에서 내려주는 값으로 임의로 값을 수정하시면 안됩니다. 
결제창에서 내려주는 값을 그대로 샘플소스 pp_cli_hub 페이지로 전달하여 승인 요청을 진행하시기 바랍니다. 
결제창에서 내려주는 res_cd, res_msg 는 결제창 내에서 인증처리가 완료되었다는 의미이며, 결제가 완료되었다는 것이 아님을 유의하시기 바랍니다. 
반드시 결제창에서 인증완료 후 전달받은 enc_info, enc_data 로 승인 요청을 하신 후 “응답 파라미터” 의 최종 결제 결과 값을 확인하시기 바랍니다

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
      <td style="text-align:left">site_logo</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xACB0;&#xC81C; &#xCC3D; &#xC67C;&#xCABD; &#xC0C1;&#xB2E8;&#xC5D0; &#xAC00;&#xB9F9;&#xC810;
          &#xC0AC;&#xC774;&#xD2B8;&#xC758; &#xB85C;&#xACE0;&#xB97C; &#xB744;&#xC6C0;.
          &#xC5C5;&#xCCB4;&#xC758; &#xB85C;&#xACE0;&#xAC00; &#xC788;&#xB294; URL&#xC744;
          &#xC815;&#xD655;&#xD788; &#xC785;&#xB825;&#xD574;&#xC57C; &#xD558;&#xBA70;
          &#xD574;&#xB2F9; &#xBCC0;&#xC218; &#xC0DD;&#xB7B5; &#xC2DC;&#xC5D0;&#xB294;
          &#xB85C;&#xACE0;&#xAC00; &#xB728;&#xC9C0; &#xC54A;&#xACE0; site_name &#xAC12;&#xC774;
          &#xD45C;&#xC2DC;&#xB428; &#xB85C;&#xACE0; &#xD30C;&#xC77C;&#xC740; GIF,
          JPG &#xD30C;&#xC77C;&#xB9CC; &#xC9C0;&#xC6D0;</p>
        <p>&#xCD5C;&#xB300; &#xC0AC;&#xC774;&#xC988; : 150 X 50 &#xBBF8;&#xB9CC;
          &#xC774;&#xBBF8;&#xC9C0; &#xD30C;&#xC77C;&#xC744; 150 X 50 &#xC774;&#xC0C1;&#xC73C;&#xB85C;
          &#xC124;&#xC815; &#xC2DC; site_name &#xAC12;&#xC774; &#xD45C;&#xC2DC;&#xB428;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">eng_flag</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xACB0;&#xC81C; &#xCC3D; &#xD55C;&#xAE00;/&#xC601;&#xBB38; &#xBCC0;&#xD658;</p>
        <p>&#xC2E0;&#xC6A9;&#xCE74;&#xB4DC;, &#xACC4;&#xC88C;&#xC774;&#xCCB4;, &#xAC00;&#xC0C1;&#xACC4;&#xC88C;,
          &#xD734;&#xB300;&#xD3F0;&#xC18C;&#xC561;&#xACB0;&#xC81C;&#xC5D0; &#xC801;&#xC6A9;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">skin_indx</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xCC3D; &#xC2A4;&#xD0A8; &#xBCC0;&#xACBD;. 1~11&#xAE4C;&#xC9C0;
        &#xC124;&#xC815; &#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">good_expr</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">18</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC0C1;&#xD488; &#xC81C;&#xACF5;&#xAE30;&#xAC04;</p>
        <p>&#x201C;&#x201D;, &#x201C;0&#x201D; : &#xC77C;&#xBC18;&#xACB0;&#xC81C;</p>
        <p>&#x201C;1&#x201D; : &#xC81C;&#xACF5;&#xAE30;&#xAC04;</p>
        <p>&#x203B; &#xAE30;&#xBCF8; &#xC124;&#xC815;&#xC740; &#xC77C;&#xBC18;&#xACB0;&#xC81C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">good_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC0C1;&#xD488;&#xCF54;&#xB4DC; : &#xC8FC;&#xBB38;&#xC0C1;&#xD488;&#xBA85;&#xC73C;&#xB85C;
        &#xAD6C;&#xBD84;&#xC774; &#xC5B4;&#xB824;&#xC6B4; &#xACBD;&#xC6B0; &#xC0C1;&#xD488;&#xAD70;&#xC744;
        &#xB530;&#xB85C; &#xAD6C;&#xBD84;&#xD558;&#xC5EC; &#xCC98;&#xB9AC;&#xD560;
        &#xC218; &#xC788;&#xB294; &#xC635;&#xC158;&#xAE30;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">tax_flag</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xBCF5;&#xD569; &#xACFC;&#xC138; &#xAD6C;&#xBB38;</p>
        <p>TG01 : &#xACFC;&#xC138;</p>
        <p>TG02 : &#xBE44;&#xACFC;&#xC138;</p>
        <p>TG03 : &#xBCF5;&#xD569;&#xACFC;&#xC138;</p>
        <p>&#x203B; &#xD45C; &#xC544;&#xB798; &#xCD94;&#xAC00; &#xC548;&#xB0B4;&#xC0AC;&#xD56D;
          &#xD655;&#xC778;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">comm_tax_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xACFC;&#xC138; &#xC2B9;&#xC778;&#xAE08;&#xC561; (&#xACF5;&#xAE09;&#xAC00;&#xC561;)</p>
        <p>&#xACFC;&#xC138; &#xAE08;&#xC561;&#xC5D0; &#xD574;&#xB2F9;&#xD558;&#xB294;
          &#xACF5;&#xAE09;&#xAC00;&#xC561; &#xC124;&#xC815;</p>
        <p>&#xACFC;&#xC138; &#xAE08;&#xC561; = good_mny / 1.1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">comm_free_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBE44;&#xACFC;&#xC138; &#xC2B9;&#xC778;&#xAE08;&#xC561;</p>
        <p>&#xBE44;&#xACFC;&#xC138; &#xAE08;&#xC561;&#xC5D0; &#xD574;&#xB2F9;&#xD558;&#xB294;
          &#xACF5;&#xAE09;&#xAC00;&#xC561; &#xC124;&#xC815;</p>
        <p>&#xBE44;&#xACFC;&#xC138; &#xAE08;&#xC561; = good_mny &#x2013; &#xACFC;&#xC138;&#xAE08;&#xC561;
          &#x2013; &#xBD80;&#xAC00;&#xAC00;&#xCE58;&#xC138;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">comm_vat_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBD80;&#xAC00;&#xAC00;&#xCE58;&#xC138;</p>
        <p>&#xBD80;&#xAC00;&#xAC00;&#xCE58;&#xC138;&#xB294; &#xACFC;&#xC138;&#xAE08;&#xC561;
          &#xACF5;&#xAE08;&#xAC00;&#xC561;&#xC758; 10%</p>
        <p>&#xBD80;&#xAC00;&#xAC00;&#xCE58;&#xC138; = good_mny &#x2013; &#xACFC;&#xC138;&#xAE08;&#xC561;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">kcp_pay_title</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">30</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xACB0;&#xC81C;&#xCC3D; &#xC0C1;&#xB2E8; &#xBB38;&#xAD6C;</p>
        <p>ex ) NHN KCP &#x2013; &#xACB0;&#xC81C;&#xC758; &#xC911;&#xC2EC;!</p>
      </td>
    </tr>
  </tbody>
</table>