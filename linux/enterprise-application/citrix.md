# Citrix

Ports



<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">组件</td>
      <td style="text-align:left">类型</td>
      <td style="text-align:left">端口</td>
      <td style="text-align:left">描述</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Citrix License Server</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">许可证管理器守护程序</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">27000</td>
      <td style="text-align:left">处理初始接触点许可请求</td>
    </tr>
    <tr>
      <td style="text-align:left">citrix供应商守护进程</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">7279</td>
      <td style="text-align:left">签入/签出citrix的许可证</td>
    </tr>
    <tr>
      <td style="text-align:left">许可证管理控制台</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">8082</td>
      <td style="text-align:left">基于web的管理控制台</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>citrix通信端口</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Citrix Receiver</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">80、443</td>
      <td style="text-align:left">WEB访问端口</td>
    </tr>
    <tr>
      <td style="text-align:left">ICA</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">1494</td>
      <td style="text-align:left">访问应用程序和虚拟桌面</td>
    </tr>
    <tr>
      <td style="text-align:left">会话可靠性</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">2598</td>
      <td style="text-align:left">访问应用程序和虚拟桌面</td>
    </tr>
    <tr>
      <td style="text-align:left">IMA</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">2512</td>
      <td style="text-align:left">独立的管理架构</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>management console</p>
        <p>（管理控制台）</p>
      </td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">2513</td>
      <td style="text-align:left">
        <p>citrix management console</p>
        <p>（citrix管理控制台）</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">应用程序/桌面请求</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">80、8080、440</td>
      <td style="text-align:left">XML service</td>
    </tr>
    <tr>
      <td style="text-align:left">STA</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">80,8080,443</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Xen App</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">离线插件</td>
      <td style="text-align:left">SMB</td>
      <td style="text-align:left">445</td>
      <td style="text-align:left">与应用程序通信中心</td>
    </tr>
    <tr>
      <td style="text-align:left">离线插件</td>
      <td style="text-align:left">HTTP/s</td>
      <td style="text-align:left">80/443</td>
      <td style="text-align:left">与应用程序通信中心</td>
    </tr>
    <tr>
      <td style="text-align:left">功率和容量管理代理</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">11161</td>
      <td style="text-align:left">与集中器通信</td>
    </tr>
    <tr>
      <td style="text-align:left">Database</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">1433</td>
      <td style="text-align:left">Microsoft SQL server</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Xen Desktop</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Xen server</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">80/443</td>
      <td style="text-align:left">communication with Xenserver infrastructure</td>
    </tr>
    <tr>
      <td style="text-align:left">Hyper-v</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">8100</td>
      <td style="text-align:left">SCVMM administrator console</td>
    </tr>
    <tr>
      <td style="text-align:left">Vmware</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">443</td>
      <td style="text-align:left">Vmware web services communication</td>
    </tr>
    <tr>
      <td style="text-align:left">Virtual desktop agent</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">8080</td>
      <td style="text-align:left">通信</td>
    </tr>
    <tr>
      <td style="text-align:left">Database</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">1433</td>
      <td style="text-align:left">Microsoft SQL Server</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Xen Server</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Xen Center</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">22</td>
      <td style="text-align:left">SSH</td>
    </tr>
    <tr>
      <td style="text-align:left">Xen Center</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">443</td>
      <td style="text-align:left">management using XenAPI</td>
    </tr>
    <tr>
      <td style="text-align:left">Xen Center</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">5900</td>
      <td style="text-align:left">VNC for linux Guests</td>
    </tr>
    <tr>
      <td style="text-align:left">Xen Center</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">3389</td>
      <td style="text-align:left">Rdp FOR WINDOWS gUESTS</td>
    </tr>
    <tr>
      <td style="text-align:left">资源池</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">22</td>
      <td style="text-align:left">SSH</td>
    </tr>
    <tr>
      <td style="text-align:left">资源池</td>
      <td style="text-align:left">TCP</td>
      <td style="text-align:left">443</td>
      <td style="text-align:left">Management using xenAPI</td>
    </tr>
    <tr>
      <td style="text-align:left">基础设施</td>
      <td style="text-align:left">TCP/UDP</td>
      <td style="text-align:left">123</td>
      <td style="text-align:left">NTP</td>
    </tr>
  </tbody>
</table>