title: "SQL Injection"  
date: 2025-07-27  
category: Database Management.  
tags: [SQL, DBMS, SQL Injection, nmap, ctf]

## What Is SQL Injection?

SQL Injection (SQLi) is a type of code injection attack where an attacker manipulates SQL queries by inserting malicious SQL statements into input fields such as login forms or search bars. If the application doesn’t properly validate user input, it may unintentionally execute these malicious commands.

Types of SQL Injections

<table>
  <thead>
    <tr>
      <th>Type</th>
      <th>Description</th>
      <th>Feedback Channel</th>
      <th>Example Tool</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>In-Band SQLi</td>
      <td>Data comes back in the same response</td>
      <td>Same channel</td>
      <td>sqlmap</td>
    </tr>
    <tr>
      <td>Blind SQLi</td>
      <td>Inferred via app behavior (true/false)</td>
      <td>Indirect (boolean/time)</td>
      <td>sqlmap</td>
    </tr>
    <tr>
      <td>Out-of-Band SQLi</td>
      <td>Data sent via external channel (DNS/HTTP)</td>
      <td>Different channel</td>
      <td>Burp Suite Pro</td>
    </tr>
  </tbody>
</table>
