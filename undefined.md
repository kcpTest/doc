---
description: 이 페이지는 가맹점 사이트에서 NHN KCP Cancel API 연동 가이드에 따라 PG결제 연동 시스템을 개발하는 방법에 대해 설명합니다.
---

# 취소요청

## 취소처리 흐름도

![](.gitbook/assets/cancel_01.jpg)

## 결제 취소요청 페이지 

결제 취소요청 페이지는 결제 건에 대한 승인/매입 취소를 요청하는 페이지입니다. KCP가 제공하는 샘플소스 상에서는 cancel 페이지에 해당하며, 가맹점은 이 페이지를 통해 결제 승인/매입 건에 대한 취소요청을 할 수 있습니다. 

※ KCP를 통해 가맹된 모든 결제 수단에 공통적으로 적용되는 취소요청 페이지입니다. 기 취소된 건을 복구할 수 있는 기능은 존재하지 않습니다. 따라서 해당 로직의 구현 및 운영에 신중을 기하시기 바랍니다.

### 1. 전체취소

**\[요\]**

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
        <p>&#xD504;&#xB85C;&#xC138;&#xC2A4; &#xC694;&#xCCAD; &#xC885;&#xB958; &#xAD6C;&#xBD84;
          &#xBCC0;&#xC218; &#xACB0;&#xC81C;&#xAC74; &#xCDE8;&#xC18C; &#xC694;&#xCCAD;&#xC758;
          &#xACBD;&#xC6B0;&#xC5D0; &#xBC18;&#xB4DC;&#xC2DC; &#x2018;mod&#x2019;&#xB85C;
          &#xC124;&#xC815;&#xD574; &#xC8FC;&#xC2DC;&#xAE30; &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;.</p>
        <p>Ex) mod</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">mod_type</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD504;&#xB85C;&#xC138;&#xC2A4; &#xC694;&#xCCAD;&#xC758; &#xAD6C;&#xBD84;
          &#xBCC0;&#xC218;</p>
        <p>&#xC804;&#xCCB4; &#xCDE8;&#xC18C; : STSC</p>
        <p>Ex) STSC</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">tno</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xACB0;&#xC81C; &#xC644;&#xB8CC; &#xD6C4; &#xACB0;&#xC81C; &#xAC74;&#xC5D0;
          &#xB300;&#xD55C; &#xACE0;&#xC720;&#xD55C; &#xAC12;</p>
        <p>&#xD574;&#xB2F9; &#xAC12;&#xC73C;&#xB85C; &#xAC70;&#xB798;&#xAC74;&#xC758;
          &#xC0C1;&#xD0DC;&#xB97C; &#xC870;&#xD68C;/&#xBCC0;&#xACBD;/&#xCDE8;&#xC18C;
          &#xAC00; &#xAC00;&#xB2A5;&#xD558;&#xB2C8; &#xACB0;&#xACFC; &#xCC98;&#xB9AC;
          &#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C; tno &#xB97C; &#xBC18;&#xB4DC;&#xC2DC;
          &#xC800;&#xC7A5; &#xD574;&#xC8FC;&#xC2DC;&#xAE30; &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;.
          Ex) 20171201111111</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">mod_desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xD504;&#xB85C;&#xC138;&#xC2A4; &#xCDE8;&#xC18C; &#xC0AC;&#xC720;&#xC5D0;
          &#xB300;&#xD55C; &#xBCC0;&#xC218; &#xAC12;</p>
        <p>Ex) &#xACE0;&#xAC1D;&#xBCC0;&#xC2EC;</p>
      </td>
    </tr>
  </tbody>
</table>

**\[응답\]**

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
      <td style="text-align:left">3</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD504;&#xB85C;&#xC138;&#xC2A4; &#xC694;&#xCCAD; &#xC885;&#xB958; &#xAD6C;&#xBD84;
          &#xBCC0;&#xC218; &#xACB0;&#xC81C;&#xAC74; &#xCDE8;&#xC18C; &#xC694;&#xCCAD;&#xC758;
          &#xACBD;&#xC6B0;&#xC5D0; &#xBC18;&#xB4DC;&#xC2DC; &#x2018;mod&#x2019;&#xB85C;
          &#xC124;&#xC815;&#xD574; &#xC8FC;&#xC2DC;&#xAE30; &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;.</p>
        <p>Ex) mod</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">res_msg</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xD504;&#xB85C;&#xC138;&#xC2A4; &#xC694;&#xCCAD;&#xC758; &#xAD6C;&#xBD84;
          &#xBCC0;&#xC218;</p>
        <p>&#xC804;&#xCCB4; &#xCDE8;&#xC18C; : STSC</p>
        <p>Ex) STSC</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">card_cd</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xACB0;&#xC81C; &#xC644;&#xB8CC; &#xD6C4; &#xACB0;&#xC81C; &#xAC74;&#xC5D0;
          &#xB300;&#xD55C; &#xACE0;&#xC720;&#xD55C; &#xAC12;</p>
        <p>&#xD574;&#xB2F9; &#xAC12;&#xC73C;&#xB85C; &#xAC70;&#xB798;&#xAC74;&#xC758;
          &#xC0C1;&#xD0DC;&#xB97C; &#xC870;&#xD68C;/&#xBCC0;&#xACBD;/&#xCDE8;&#xC18C;
          &#xAC00; &#xAC00;&#xB2A5;&#xD558;&#xB2C8; &#xACB0;&#xACFC; &#xCC98;&#xB9AC;
          &#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C; tno &#xB97C; &#xBC18;&#xB4DC;&#xC2DC;
          &#xC800;&#xC7A5; &#xD574;&#xC8FC;&#xC2DC;&#xAE30; &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;.
          Ex) 20171201111111</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">card_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xD504;&#xB85C;&#xC138;&#xC2A4; &#xCDE8;&#xC18C; &#xC0AC;&#xC720;&#xC5D0;
          &#xB300;&#xD55C; &#xBCC0;&#xC218; &#xAC12;</p>
        <p>Ex) &#xACE0;&#xAC1D;&#xBCC0;&#xC2EC;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">amount</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAE08;&#xC561; &#xACB0;&#xC81C; &#xAC74;&#xC758; &#xCD1D;
        &#xACB0;&#xC81C; &#xAE08;&#xC561;</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">coupon_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">canc_time</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>



