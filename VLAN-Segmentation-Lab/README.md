<body>

<h1>VLAN Segmentation Lab – pfSense & Proxmox</h1>

<h2>Overview</h2>
<p>
This project demonstrates VLAN-based network segmentation using
pfSense and Proxmox VE to separate client, server,
and management traffic. The goal was to enforce <strong>least-privilege access</strong>,
prevent lateral movement, and validate firewall controls through real testing.
</p>

<p>
This lab simulates how segmented networks are designed and secured in
<strong>enterprise IT infrastructure environments</strong>.
</p>

<hr>

<h2>Architecture & Topology</h2>
<p>
The environment uses a <strong>VLAN-aware trunk</strong> on Proxmox, with pfSense acting
as the Layer 3 firewall and router.
</p>

<ul>
  <li>Proxmox VE as the hypervisor</li>
  <li>pfSense as the firewall/router</li>
  <li>Multiple VLANs routed and enforced by pfSense</li>
</ul>

<img src="diagrams/vlan-topology.png" alt="VLAN Network Topology Diagram">

<hr>

<h2>VLAN Design</h2>

<table>
  <tr>
    <th>VLAN</th>
    <th>Purpose</th>
    <th>Subnet</th>
  </tr>
  <tr>
    <td>VLAN 10</td>
    <td>Servers</td>
    <td>10.0.10.0/24</td>
  </tr>
  <tr>
    <td>VLAN 20</td>
    <td>Clients</td>
    <td>10.0.20.0/24</td>
  </tr>
  <tr>
    <td>VLAN 30</td>
    <td>Management</td>
    <td>10.0.30.0/24</td>
  </tr>
</table>

<p>
Each VLAN is isolated by default, with access only explicitly permitted through
firewall rules.
</p>

<hr>

<h2>Firewall Policy Overview</h2>

<h3>Client VLAN (VLAN 20)</h3>
<ul>
  <li>Allowed outbound Internet access</li>
  <li>Blocked from Server VLAN</li>
  <li>Blocked from Management VLAN</li>
  <li>Blocked from pfSense WebGUI</li>
</ul>

<h3>Server VLAN (VLAN 10)</h3>
<ul>
  <li>No direct access from Client VLAN</li>
  <li>Administrative access allowed only from Management VLAN</li>
</ul>

<h3>Management VLAN (VLAN 30)</h3>
<ul>
  <li>Exclusive access to pfSense WebGUI</li>
  <li>Administrative access to servers (SSH/RDP)</li>
  <li>Blocked from Client VLAN</li>
  <li>Restricted Internet access</li>
</ul>

<img src="https://github.com/odalomba/Omari-IT-Portfolio/blob/main/VLAN-Segmentation-Lab/firewall-rules/VLAN20-Clients-Rules.png" alt="Client VLAN Firewall Rules">
<img src="https://github.com/odalomba/Omari-IT-Portfolio/blob/main/VLAN-Segmentation-Lab/firewall-rules/VLAN30-Management-Rules.png" alt="Management VLAN Firewall Rules">

<hr>

<h2>DHCP & IP Assignment</h2>
<ul>
  <li>DHCP enabled on Client and Server VLANs</li>
  <li>Management VLAN uses controlled access (static or limited DHCP)</li>
  <li>pfSense acts as default gateway and DNS server</li>
</ul>

<hr>

<h2>Validation & Testing</h2>
<ul>
  <li>Client VLAN blocked from accessing pfSense WebGUI</li>
  <li>Management VLAN successfully accessed pfSense WebGUI</li>
  <li>Client VLAN blocked from Server VLAN (ping and service tests)</li>
  <li>Management VLAN permitted administrative access to servers</li>
  <li>Client VLAN allowed outbound Internet access</li>
  <li>Firewall rule counters and logs confirmed enforcement</li>
</ul>

<img src="https://github.com/odalomba/Omari-IT-Portfolio/blob/main/VLAN-Segmentation-Lab/validation/Client-Blocked-pfsense.png" alt="Client VLAN Blocked from pfSense">
<img src="https://github.com/odalomba/Omari-IT-Portfolio/blob/main/VLAN-Segmentation-Lab/validation/Management-SSH-Server.png" alt="Management VLAN-Sever SSH Access">
<img src="https://github.com/odalomba/Omari-IT-Portfolio/blob/main/VLAN-Segmentation-Lab/validation/Firewall-rules-blocked.png" alt="Firewall Logs Showing Blocked Traffic">

<hr>

<h2>Troubleshooting & Lessons Learned</h2>
<ul>
  <li>Resolved DHCP failures caused by missing broadcast rules</li>
  <li>Corrected VLAN tag mismatches between Proxmox and pfSense</li>
  <li>Learned stateful firewall behavior and when to reset states</li>
  <li>Recovered pfSense WebGUI access using console tools</li>
</ul>

<p>
These issues reinforced the importance of dedicated management networks,
proper firewall rule ordering, and console-based recovery methods.
</p>

<hr>

<h2>Skills Demonstrated</h2>
<ul>
  <li>VLAN segmentation and trunking</li>
  <li>pfSense firewall policy design</li>
  <li>Proxmox virtual networking</li>
  <li>DHCP and DNS troubleshooting</li>
  <li>Layer 2 / Layer 3 diagnostics</li>
  <li>Network security principles</li>
  <li>Infrastructure documentation</li>
</ul>

<hr>

<h2>Why This Matters</h2>
<p>
Network segmentation is a foundational security control used to reduce attack
surfaces, prevent lateral movement, protect critical infrastructure, and enforce
role-based access.
</p>

<p>
This lab demonstrates how those principles are implemented and validated in
practice.
</p>

<hr>

<h2>Next Improvements</h2>
<ul>
  <li>IDS/IPS integration (Snort or Suricata)</li>
  <li>Centralized logging</li>
  <li>Additional server services</li>
  <li>Site-to-site or multi-firewall designs</li>
</ul>

<hr>

<p class="status">Lab Status: COMPLETE ✅</p>

</body>
</html>
