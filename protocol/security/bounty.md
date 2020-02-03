# Bug Bounty

### Overview

Balancer has completed smart contract audits with Trail of Bits. We also will run a continuous bug bounty program for the bronze release of Balancer core.

### Scope

The bug bounty covers any of the core smart contracts deployed on mainnet. The code can be found at: [https://github.com/balancer-labs/balancer-core](https://github.com/balancer-labs/balancer-core)

Submissions should be based off commit hash: 

Mainnet contracts can be found at:

_Additional second layer contracts such as the exchange proxy or individual smart pool contracts may be added at a further date._

### Rewards

The bounty program will pay out rewards according to the severity of a vulnerability. The final reward amount is at the sole discretion of Balancer Labs.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Reward</th>
      <th style="text-align:left">Severity</th>
      <th style="text-align:left">Examples</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>$10,000 - $25,000</b>
      </td>
      <td style="text-align:left">Critical</td>
      <td style="text-align:left">
        <ul>
          <li>Stealing assets from a pool</li>
          <li>Permanently freezing a pools assets</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>$5,000 - $10,000</b>
      </td>
      <td style="text-align:left">High</td>
      <td style="text-align:left">
        <ul>
          <li>Severe rounding errors where an attacker can steal significant funds in
            excess of any gas costs or swap fees</li>
          <li>Manipulating a finalized pools assets / weights / fees</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>$1,000 - $2,500</b>
      </td>
      <td style="text-align:left">Medium</td>
      <td style="text-align:left">
        <ul>
          <li>Minor rounding errors that allow an attacker to slowly manipulate funds
            in their advantage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>$0 - $1,000</b>
      </td>
      <td style="text-align:left">Low</td>
      <td style="text-align:left">
        <ul>
          <li>Informational and code quality based disclosures</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>### Reporting / Disclosures

Please report any findings to [security@balancer.finance](mailto:security@balancer.finance) with full details about any vulnerability and steps / code to reproduce. Allow us time to review and remediate any findings before public disclosure.

### Ineligible Findings

* Duplicate vulnerabilities. Only the first reporter will be rewarded.
* Findings already known as part of a formal audit
