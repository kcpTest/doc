---
description: 이 장은 공통통보 및 영수증 처리에 대한  안내 페이지 입니다.
---

# 공통 통보 및 영수증 처리

## 공통통보페이지

공통통보 페이지는 실시간으로 결제가 이루어지지 않는 가상계좌 결제수단의 변경되는 상태에 대한 통보를 받는 페이지로, NHN KCP가 제공하는 샘플소스 상에서 \[common\_return\] 페이지에 해당합니다. 가맹점은 이 페이지를 통해 결제 건에 대한 변경된 상태를 처리 할 수 있습니다. 

가상계좌의 경우, 결제자가 발급된 가상계좌에 대해 입금을 해야 최종적으로 결제가 완료됩니다. 그러나 결제자의 입금여부를 결제가 진행된 웹 페이지 상에서는 확인할 수 없기 때문에, 결제자가 입금을 하게 되면, 해당 결제 건에 대한 입금결과를 NHN KCP에서 가맹점 측으로 별도로 전송합니다.

 ※ 가맹점 서버의 common\_return 페이지가 NHN KCP 가맹점 관리자 페이지 \[상점정보관리 – 정보변경 – 공통 URL 정보\]에 미리 등록되어 있어야 실 거래 건에 대한 노티처리가 가능합니다. 

해당 페이지에 URL이 등록되지 않은 경우 NHN KCP에서는 DATA를 별도로 전송하지 못하게 됩니다. 

※ NHN KCP에서 가맹점의 common\_return 페이지로 데이터를 전송할 때, 아래와 같은 IP에서 전송을 합니다. NHN KCP 전송 건을 확인하기 위해 가맹점에서 해당 페이지를 통해 전송 받은 데이터 처리를 아래의 IP ADDRESS를 체크를 하여, 다른 경로를 통해서 전송된 데이터를 결과 처리에서 제외시켜 주시기 바랍니다

| 설명 | IP ADDRESS |
| :--- | :--- |
| NHN KCP 통보 테스트 서버 IP ADDRESS | [http://210.122.73.58/](http://210.122.73.58/) |
| NHN KCP 통보 실 서버 IP ADDRESS 1 | 203.238.36.173 / 103.215.144.173 |
| NHN KCP 통보 실 서버 IP ADDRESS 2 | 203.238.36.178 / 103.215.144.174 |

### 1.전달 파라미터\(공통정보\)

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
      <td style="text-align:left">site_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xAC00;&#xB9F9;&#xC810; &#xCF54;&#xB4DC;</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">tno</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xACB0;&#xC81C; &#xC644;&#xB8CC; &#xD6C4; NHN KCP&#xC5D0;&#xC11C; &#xB9AC;&#xD134;
          &#xD558;&#xB294; &#xAC70;&#xB798;&#xBC88;&#xD638;</p>
        <p>&#xAC01; &#xACB0;&#xC81C; &#xAC74;&#xC5D0; &#xB300;&#xD574; &#xACE0;&#xC720;&#xC758;
          &#xAC12; &#xAC00;&#xC9D0;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">order_no</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">40</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xAC00;&#xB9F9;&#xC810;&#xC5D0;&#xC11C; &#xC0DD;&#xC131;&#xD55C; &#xC8FC;&#xBB38;&#xBC88;&#xD638;</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">tx_cd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC5C5;&#xBB34;&#xCC98;&#xB9AC; &#xAD6C;&#xBD84;&#xCF54;&#xB4DC;</p>
        <p>&#xAC00;&#xC0C1;&#xACC4;&#xC88C; &#xC785;&#xAE08; &#xD1B5;&#xBCF4; &#x2013;
          TX00</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">tx_tm</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">16</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xD1B5;&#xBCF4;&#xB41C; &#xC5C5;&#xBB34;&#xC5D0; &#xB300;&#xD55C; &#xC5C5;&#xBB34;&#xCC98;&#xB9AC;
        &#xC644;&#xB8CC; &#xC2DC;&#xAC04;</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">result</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">NHN KCP&#xC5D0;&#xC11C; &#xC804;&#xC1A1;&#xD55C; &#xACB0;&#xACFC; &#xB370;&#xC774;&#xD130;&#xB97C;
        &#xAC00;&#xB9F9;&#xC810; &#xC11C;&#xBC84;&#xC5D0;&#xC11C; &#xC815;&#xC0C1;&#xC801;&#xC73C;&#xB85C;
        &#xBC1B;&#xC558;&#xB294;&#xC9C0;&#xB97C; &#xD655;&#xC778;&#xD558;&#xAE30;
        &#xC704;&#xD55C; &#xBCC0;&#xC218;&#xB85C; &#xAC00;&#xB9F9;&#xC810; &#xC11C;&#xBC84;&#xC5D0;&#xC11C;
        &#xACB0;&#xACFC; &#xB370;&#xC774;&#xD130;&#xB97C; &#xC815;&#xC0C1;&#xC801;&#xC73C;&#xB85C;
        &#xBC1B;&#xC544;&#xC11C; &#xC131;&#xACF5;&#xC801;&#xC73C;&#xB85C; &#xCC98;&#xB9AC;&#xD55C;
        &#xACBD;&#xC6B0; result &#xAC12;&#xC744; &#x2018;0000&#x2019;&#xC73C;&#xB85C;
        &#xC124;&#xC815; &#xC815;&#xC0C1;&#xC801;&#xC73C;&#xB85C; &#xCC98;&#xB9AC;
        &#xC644;&#xB8CC;&#xB418;&#xC9C0; &#xBABB;&#xD55C; &#xACBD;&#xC6B0; &#xC784;&#xC758;&#xC758;
        &#xAC12; &#xC124;&#xC815; result &#xAC12;&#xC744; &#xD655;&#xC778;&#xD558;&#xC5EC;
        &#x2018;0000&#x2019;&#xC774; &#xC544;&#xB2D0; &#xACBD;&#xC6B0; NHN KCP
        &#xD1B5;&#xBCF4; &#xC11C;&#xBC84;&#xC5D0;&#xC11C; &#xB2E4;&#xC2DC; &#xD1B5;&#xBCF4;&#xD568;</td>
    </tr>
  </tbody>
</table>

### 2.가상계좌 입금 건 통보



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
      <td style="text-align:left">ipgm_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">30</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xAC70;&#xB798;&#xC5D0; &#xB300;&#xD55C; &#xC8FC;&#xBB38;&#xC790;&#xBA85;</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">ipgm_mnyx</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC785;&#xAE08;&#xC790;&#xAC00; &#xC2E4;&#xC81C; &#xC785;&#xAE08;&#xD55C;
          &#xC785;&#xAE08; &#xAE08;&#xC561;</p>
        <p><b> &#x203B; &#xC8FC;&#xC758; &#x2013; &#xC785;&#xAE08;&#xC790;&#xAC00; &#xC8FC;&#xBB38; &#xAE08;&#xC561;&#xACFC; &#xC0C1;&#xC774;&#xD55C; &#xAE08;&#xC561;&#xC744; &#xC785;&#xAE08; &#xD55C; &#xACBD;&#xC6B0;, NHN KCP&#xC5D0;&#xC11C;&#xB294; &#xAC00;&#xB9F9;&#xC810;&#xC5D0; &#xD1B5;&#xBCF4; &#xD398;&#xC774;&#xC9C0;&#xB97C; &#xD1B5;&#xD574; &#xC2E4; &#xC785;&#xAE08; &#xB0B4;&#xC5ED;&#xC744; &#xD1B5;&#xBCF4;&#xD558;&#xACE0; &#xC785;&#xAE08; &#xAE08;&#xC561; &#xADF8;&#xB300;&#xB85C; &#xAC00;&#xB9F9;&#xC810;&#xC5D0; &#xC815;&#xC0B0;&#xC774; &#xC774;&#xB8E8;&#xC5B4;&#xC9D1;&#xB2C8;&#xB2E4;. &#xD574;&#xB2F9; &#xD398;&#xC774;&#xC9C0;&#xC5D0;&#xC11C; DB&#xCC98;&#xB9AC; &#xC2DC; &#xC2E4; &#xC785;&#xAE08; &#xAE08;&#xC561;&#xACFC; &#xC8FC;&#xBB38;&#xAE08;&#xC561;&#xC744; &#xBE44;&#xAD50;&#xD574;&#xC11C; &#xC0C1;&#xC774;&#xD55C; &#xACBD;&#xC6B0; &#xB0B4;&#xBD80;&#xC801;&#xC73C;&#xB85C; &#xD655;&#xC778;&#xD574;&#xC8FC;&#xC2DC;&#xAE30; &#xBC14;&#xB78D;&#xB2C8;&#xB2E4;. </b>
        </p>
        <p><b>(NHN KCP &#xD658;&#xBD88;&#xCC98;&#xB9AC; &#xBD88;&#xAC00;)</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">totl_mnyx</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xD574;&#xB2F9; &#xACC4;&#xC88C;&#xC5D0; &#xC785;&#xAE08; &#xB41C; &#xAE08;&#xC561;&#xC758;
          &#xD569;&#xACC4;</p>
        <p>&#xC77C;&#xD68C;&#xC131; &#xAC00;&#xC0C1;&#xACC4;&#xC88C;&#xC758; &#xACBD;&#xC6B0;
          ipgm_mnyx&#xC640; &#xB3D9;&#xC77C;&#xD55C; &#xAE08;&#xC561;&#xC774; &#xD1B5;&#xBCF4;&#xB418;&#xB098;,
          &#xACE0;&#xC815;&#xC2DD; &#xAC00;&#xC0C1;&#xACC4;&#xC88C;&#xC758; &#xACBD;&#xC6B0;
          &#xD574;&#xB2F9; &#xACC4;&#xC88C;&#xC5D0; &#xC785;&#xAE08;&#xB41C; &#xCD1D;
          &#xAE08;&#xC561;&#xC774; &#xD1B5;&#xBCF4;&#xB428;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">ipgm_time</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC5C5;&#xBB34;&#xCC98;&#xB9AC; &#xAD6C;&#xBD84;&#xCF54;&#xB4DC;</p>
        <p>&#xAC00;&#xC0C1;&#xACC4;&#xC88C; &#xC785;&#xAE08; &#xD1B5;&#xBCF4; &#x2013;
          TX00</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">bank_code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xD1B5;&#xBCF4;&#xB41C; &#xC5C5;&#xBB34;&#xC5D0; &#xB300;&#xD55C; &#xC5C5;&#xBB34;&#xCC98;&#xB9AC;
        &#xC644;&#xB8CC; &#xC2DC;&#xAC04;</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">account</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">NHN KCP&#xC5D0;&#xC11C; &#xC804;&#xC1A1;&#xD55C; &#xACB0;&#xACFC; &#xB370;&#xC774;&#xD130;&#xB97C;
        &#xAC00;&#xB9F9;&#xC810; &#xC11C;&#xBC84;&#xC5D0;&#xC11C; &#xC815;&#xC0C1;&#xC801;&#xC73C;&#xB85C;
        &#xBC1B;&#xC558;&#xB294;&#xC9C0;&#xB97C; &#xD655;&#xC778;&#xD558;&#xAE30;
        &#xC704;&#xD55C; &#xBCC0;&#xC218;&#xB85C; &#xAC00;&#xB9F9;&#xC810; &#xC11C;&#xBC84;&#xC5D0;&#xC11C;
        &#xACB0;&#xACFC; &#xB370;&#xC774;&#xD130;&#xB97C; &#xC815;&#xC0C1;&#xC801;&#xC73C;&#xB85C;
        &#xBC1B;&#xC544;&#xC11C; &#xC131;&#xACF5;&#xC801;&#xC73C;&#xB85C; &#xCC98;&#xB9AC;&#xD55C;
        &#xACBD;&#xC6B0; result &#xAC12;&#xC744; &#x2018;0000&#x2019;&#xC73C;&#xB85C;
        &#xC124;&#xC815; &#xC815;&#xC0C1;&#xC801;&#xC73C;&#xB85C; &#xCC98;&#xB9AC;
        &#xC644;&#xB8CC;&#xB418;&#xC9C0; &#xBABB;&#xD55C; &#xACBD;&#xC6B0; &#xC784;&#xC758;&#xC758;
        &#xAC12; &#xC124;&#xC815; result &#xAC12;&#xC744; &#xD655;&#xC778;&#xD558;&#xC5EC;
        &#x2018;0000&#x2019;&#xC774; &#xC544;&#xB2D0; &#xACBD;&#xC6B0; NHN KCP
        &#xD1B5;&#xBCF4; &#xC11C;&#xBC84;&#xC5D0;&#xC11C; &#xB2E4;&#xC2DC; &#xD1B5;&#xBCF4;&#xD568;</td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">noti_id</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">op_cd</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">remitter</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">cash_a_no</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">9</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">11</td>
      <td style="text-align:left">cash_no</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">14</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

