---
description: 이 페이지는 가맹점 사이트에서 NHN KCP Cancel API 연동 가이드에 따라 PG결제 연동 시스템을 개발하는 방법에 대해 설명합니다.
---

# 취소요청

## 취소처리 흐름도

![](.gitbook/assets/cancel_01.jpg)

## 결제 서버 IP 등록방법

KCP에서는 상점의 고유한 취소를 보호하기 위하여 결제 서버IP를 등록하는 기능을 제공하고 있습니다. 아래의 방법대로 NHN KCP 가맹점 관리자페이지 \[상점정보관리–정보변경–결제서버 IP설정\]에 접속하시어 취소를 요청하는 서버의 IP를 등록하시기 바랍니다.   
**해당 IP가 등록되지 않으면 취소시 “res\_cd=8012, res\_msg=취소불가-상점관리자 문의”가 발생하게 됩니다**.

## 취소 페이지 보안강화

**가\) 취소 기능이 필요 없는 상점**   
- 취소 기능이 필요 없는 상점에서는 취소 샘플을 웹 상에 연동하지 마시기 바랍니다.   
- 취소를 할 수 없는 상점에서 취소 샘플을 연동해놓는 경우 악의적으로 해당 웹에 접근하여 임의 취소를 할 수 있으므로 취소 관련 샘플이 존재하지 않도록 관리하시기 바랍니다. 

**나\) 상점의 관리자가 상점 자체의 시스템에서 취소를 하는 경우**   
- 취소 모듈이 구현되어 있는 시스템에 접속하는 관리자의 경우 세션처리를 통해 관리자 페이지 로그인 시 취소 권한 정보를 서버 내 세션을 이용하여 저장 관리하고, 취소 요청시 세션정보에 취소권한 가능한 사용자인지 체크하여 취소로직을 구동하도록 보안조치   
- 취소 요청시 요청한 Client IP \(취소 관리자사용IP\) 제한을 두어 취소 페이지 접근시 등록된 Client IP \(취소관리자 IP\)인 경우에만 취소되도록 보안조치 

**다\) 결제고객이 직접 마이페이지 등에서 취소를 하는 경우**   
- 고객 정보를 체크할 수 있는 인증단계 추가 권장 \(취소시 본인확인 및 계좌인증 등을 통한 본인확인\)  
- 고객 취소 페이지 호출시 HTTPS 기반 시큐어웹\(Secure Web\)을 이용 권장 

**라\) 결제연동과 관련한 모듈의 검색 불가**   
- 구글이나 네이버등 검색엔진을 통해 상점의 결제모듈 관련한 내용이 검색이 되지 않도록 관리

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
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xCDE8;&#xC18C;&#xC644;&#xB8CC; &#xC5EC;&#xBD80;&#xC5D0; &#xB300;&#xD55C;
          &#xC751;&#xB2F5; &#xAC12;</p>
        <p>&#xC815;&#xC0C1; &#xCC98;&#xB9AC; &#xAC74;&#xC5D0; &#xB300;&#xD574;&#xC11C;&#xB9CC;
          0000&#xC73C;&#xB85C; &#xCC98;&#xB9AC;&#xD558;&#xBA70;, &#xC774;&#xC678;&#xC5D0;&#xB294;
          &#xD574;&#xB2F9; &#xAC70;&#xC808; &#xC751;&#xB2F5; &#xCF54;&#xB4DC; &#xAC12;&#xC744;
          &#xB9AC;&#xD134; &#xD569;&#xB2C8;&#xB2E4;. &#xACB0;&#xACFC; &#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C;
          DB&#xCC98;&#xB9AC;&#xB97C; &#xD560; &#xACBD;&#xC6B0; res_cd&#xB97C; &#xC774;&#xC6A9;&#xD558;&#xC2DC;&#xAE30;
          &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;. Ex) 0000</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">res_msg</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">100</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xCDE8;&#xC18C; &#xC694;&#xCCAD; &#xACB0;&#xACFC;&#xC5D0; &#xB300;&#xD55C;
          &#xBA54;&#xC2DC;&#xC9C0; &#xAC12;</p>
        <p>&#x2018;&#xC815;&#xC0C1;&#xCC98;&#xB9AC;&#x2019; &#xC678;&#xC758; &#xAC70;&#xC808;
          &#xAC74;&#xC5D0; &#xB300;&#xD574;&#xC11C;&#xB294; &#xC751;&#xB2F5; &#xCF54;&#xB4DC;
          &#xAC12;&#xC5D0; &#xD574;&#xB2F9;&#xD558;&#xB294; &#xC624;&#xB958; &#xC751;&#xB2F5;
          &#xBA54;&#xC2DC;&#xC9C0;&#xB97C; &#xB9AC;&#xD134; &#xD569;&#xB2C8;&#xB2E4;.
          Ex) &#xC815;&#xC0C1;&#xCC98;&#xB9AC;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">card_cd</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xBC1C;&#xAE09; &#xC0AC; &#xCF54;&#xB4DC;</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">card_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xBC1C;&#xAE09; &#xC0AC; &#xBA85;</td>
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
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xCFE0;&#xD3F0; &#xD560;&#xC778;, &#xD398;&#xC774;&#xCF54;
        &#xD3EC;&#xC778;&#xD2B8; &#xC0AC;&#xC6A9; &#xAE08;&#xC561; &#xACB0;&#xC81C;
        &#xAC74;&#xC758; &#xCFE0;&#xD3F0; &#xD560;&#xC778; &#xAE08;&#xC561; &#xB610;&#xB294;
        &#xD398;&#xC774;&#xCF54; &#xD3EC;&#xC778;&#xD2B8; &#xC0AC;&#xC6A9; &#xAE08;&#xC561;</td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">canc_time</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xCDE8;&#xC18C; &#xC694;&#xCCAD; &#xC2DC;&#xAC04;</td>
    </tr>
  </tbody>
</table>



### 2. 부분취소

**\[요청\]**

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
        <p>&#xBD80; &#xCDE8;&#xC18C; : STPC</p>
        <p>Ex) STPC</p>
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
      <td style="text-align:left">mod_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xCDE8;&#xC18C;&#xC694;&#xCCAD; &#xAE08;&#xC561;</p>
        <p>Ex) 100</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">rem_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xBD80;&#xBD84;&#xCDE8;&#xC18C; &#xC774;&#xC804;&#xC5D0; &#xB0A8;&#xC740;
          &#xAE08;&#xC561;</p>
        <p>Ex) 1004</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
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
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">tax_flag</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xBCF5;&#xD569;&#xACFC;&#xC138; &#xAC70;&#xB798; &#xAD6C;&#xBD84; &#xAC12;&#xC785;&#xB2C8;&#xB2E4;.
          (&#xBCF5;&#xD569;&#xACFC;&#xC138;)</p>
        <p>Ex) TG03</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">mod_tax_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xACF5;&#xAE09;&#xAC00; &#xBD80;&#xBD84;&#xCDE8;&#xC18C; &#xC694;&#xCCAD;&#xAE08;&#xC561;
          (&#xBCF5;&#xD569;&#xACFC;&#xC138;)</p>
        <p>Ex) 80</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">mod_vat_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xBD80;&#xAC00;&#xC138; &#xBD80;&#xBD84;&#xCDE8;&#xC18C; &#xC694;&#xCCAD;&#xAE08;&#xC561;
          (&#xBCF5;&#xD569;&#xACFC;&#xC138;)</p>
        <p>Ex) 8</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">mod_free_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xBE44;&#xACFC;&#xC138; &#xBD80;&#xBD84;&#xCDE8;&#xC18C; &#xC694;&#xCCAD;&#xAE08;&#xC561;
          (&#xBCF5;&#xD569;&#xACFC;&#xC138;)</p>
        <p>Ex) 12</p>
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
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xCDE8;&#xC18C;&#xC644;&#xB8CC; &#xC5EC;&#xBD80;&#xC5D0; &#xB300;&#xD55C;
          &#xC751;&#xB2F5; &#xAC12;</p>
        <p>&#xC815;&#xC0C1; &#xCC98;&#xB9AC; &#xAC74;&#xC5D0; &#xB300;&#xD574;&#xC11C;&#xB9CC;
          0000&#xC73C;&#xB85C; &#xCC98;&#xB9AC;&#xD558;&#xBA70;, &#xC774;&#xC678;&#xC5D0;&#xB294;
          &#xD574;&#xB2F9; &#xAC70;&#xC808; &#xC751;&#xB2F5; &#xCF54;&#xB4DC; &#xAC12;&#xC744;
          &#xB9AC;&#xD134; &#xD569;&#xB2C8;&#xB2E4;. &#xACB0;&#xACFC; &#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C;
          DB&#xCC98;&#xB9AC;&#xB97C; &#xD560; &#xACBD;&#xC6B0; res_cd&#xB97C; &#xC774;&#xC6A9;&#xD558;&#xC2DC;&#xAE30;
          &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;. Ex) 0000</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">res_msg</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">100</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xCDE8;&#xC18C; &#xC694;&#xCCAD; &#xACB0;&#xACFC;&#xC5D0; &#xB300;&#xD55C;
          &#xBA54;&#xC2DC;&#xC9C0; &#xAC12;</p>
        <p>&#x2018;&#xC815;&#xC0C1;&#xCC98;&#xB9AC;&#x2019; &#xC678;&#xC758; &#xAC70;&#xC808;
          &#xAC74;&#xC5D0; &#xB300;&#xD574;&#xC11C;&#xB294; &#xC751;&#xB2F5; &#xCF54;&#xB4DC;
          &#xAC12;&#xC5D0; &#xD574;&#xB2F9;&#xD558;&#xB294; &#xC624;&#xB958; &#xC751;&#xB2F5;
          &#xBA54;&#xC2DC;&#xC9C0;&#xB97C; &#xB9AC;&#xD134; &#xD569;&#xB2C8;&#xB2E4;.
          Ex) &#xC815;&#xC0C1;&#xCC98;&#xB9AC;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">card_cd</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xBC1C;&#xAE09; &#xC0AC; &#xCF54;&#xB4DC;</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">card_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">256</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xBC1C;&#xAE09; &#xC0AC; &#xBA85;</td>
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
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xCFE0;&#xD3F0; &#xD560;&#xC778;, &#xD398;&#xC774;&#xCF54;
        &#xD3EC;&#xC778;&#xD2B8; &#xC0AC;&#xC6A9; &#xAE08;&#xC561; &#xACB0;&#xC81C;
        &#xAC74;&#xC758; &#xCFE0;&#xD3F0; &#xD560;&#xC778; &#xAE08;&#xC561; &#xB610;&#xB294;
        &#xD398;&#xC774;&#xCF54; &#xD3EC;&#xC778;&#xD2B8; &#xC0AC;&#xC6A9; &#xAE08;&#xC561;</td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">canc_time</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xACB0;&#xC81C; &#xAC74;&#xC758; &#xCDE8;&#xC18C; &#xC694;&#xCCAD; &#xC2DC;&#xAC04;</td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">panc_mod_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xCDE8;&#xC18C;&#xC694;&#xCCAD; &#xAE08;&#xC561;</td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">panc_rem_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xBD80;&#xBD84; &#xCDE8;&#xC18C; &#xC774;&#xC804;&#xC5D0; &#xB0A8;&#xC740;
        &#xAE08;&#xC561;</td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">panc_card_mod_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xCE74;&#xB4DC; &#xBD80;&#xBD84; &#xCDE8;&#xC18C; &#xC694;&#xCCAD; &#xAE08;&#xC561;</td>
    </tr>
    <tr>
      <td style="text-align:left">11</td>
      <td style="text-align:left">panc_coupon_mod_mny</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xCFE0;&#xD3F0; &#xBD80;&#xBD84; &#xCDE8;&#xC18C; &#xC694;&#xCCAD; &#xAE08;&#xC561;</td>
    </tr>
    <tr>
      <td style="text-align:left">12</td>
      <td style="text-align:left">mod_pcan_seq_no</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBD80;&#xBD84;&#xCDE8;&#xC18C; &#xC77C;&#xB828;&#xBC88;&#xD638; &#xBD80;&#xBD84;&#xCDE8;&#xC18C;&#xC2DC;&#xC5D0;&#xB9CC;
          &#xB9AC;&#xD134;&#xB418;&#xB294; &#xACE0;&#xC720;&#xAC12;&#xC785;&#xB2C8;&#xB2E4;.</p>
        <p>Ex) 20190114111111</p>
      </td>
    </tr>
  </tbody>
</table>

